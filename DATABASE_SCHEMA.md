# DoseMate — Database Schema & SQL Specifications

This PostgreSQL schema is optimized for Supabase with Row Level Security (RLS) policies, foreign key cascades, validation constraints, and indexes.

```sql
-- Enable UUID extension
create extension if not exists "uuid-ossp";

-- 1. Profiles Table (Users)
create table if not exists public.profiles (
  id uuid references auth.users on delete cascade primary key,
  full_name text not null,
  email text,
  phone text,
  emergency_contact_name text,
  emergency_contact_phone text,
  easy_care_mode boolean default false,
  theme_preference text default 'system' check (theme_preference in ('light', 'dark', 'system')),
  sound_enabled boolean default true,
  snooze_duration_minutes integer default 15,
  created_at timestamp with time zone default timezone('utc'::text, now()) not null,
  updated_at timestamp with time zone default timezone('utc'::text, now()) not null
);

-- 2. Medicines Table
create table if not exists public.medicines (
  id uuid default uuid_generate_v4() primary key,
  user_id uuid references public.profiles(id) on delete cascade not null,
  name text not null,
  dosage text not null,
  form text not null check (form in ('tablet', 'capsule', 'liquid', 'injection', 'inhaler', 'drops', 'topical', 'other')),
  instructions text,
  instructions_timing text check (instructions_timing in ('before_food', 'with_food', 'after_food', 'no_restriction')),
  image_url text,
  total_quantity integer default 30 not null check (total_quantity >= 0),
  refill_threshold integer default 5 not null check (refill_threshold >= 0),
  color_code text default '#4F8064',
  is_active boolean default true not null,
  notes text,
  created_at timestamp with time zone default timezone('utc'::text, now()) not null,
  updated_at timestamp with time zone default timezone('utc'::text, now()) not null
);

-- 3. Medication Schedules Table
create table if not exists public.medication_schedules (
  id uuid default uuid_generate_v4() primary key,
  user_id uuid references public.profiles(id) on delete cascade not null,
  medicine_id uuid references public.medicines(id) on delete cascade not null,
  frequency text not null check (frequency in ('once_daily', 'twice_daily', 'three_times_daily', 'custom', 'as_needed')),
  times text[] not null,
  days_of_week integer[] default '{0,1,2,3,4,5,6}',
  start_date date not null default current_date,
  end_date date,
  dose_quantity numeric(4,2) default 1.0 not null,
  is_active boolean default true not null,
  created_at timestamp with time zone default timezone('utc'::text, now()) not null
);

-- 4. Dose Logs Table
create table if not exists public.dose_logs (
  id uuid default uuid_generate_v4() primary key,
  user_id uuid references public.profiles(id) on delete cascade not null,
  schedule_id uuid references public.medication_schedules(id) on delete cascade not null,
  medicine_id uuid references public.medicines(id) on delete cascade not null,
  scheduled_date date not null,
  scheduled_time time not null,
  status text not null check (status in ('taken', 'skipped', 'missed', 'snoozed')),
  recorded_at timestamp with time zone default timezone('utc'::text, now()) not null,
  skip_reason text,
  snooze_until timestamp with time zone,
  notes text,
  created_at timestamp with time zone default timezone('utc'::text, now()) not null
);

-- 5. Caregiver Links Table
create table if not exists public.caregiver_links (
  id uuid default uuid_generate_v4() primary key,
  patient_id uuid references public.profiles(id) on delete cascade not null,
  caregiver_id uuid references public.profiles(id) on delete cascade,
  caregiver_email text not null,
  caregiver_name text not null,
  access_code text not null unique,
  status text not null check (status in ('pending', 'active', 'revoked')) default 'pending',
  permissions jsonb default '{"can_view_schedule": true, "can_view_history": true, "can_receive_alerts": true}'::jsonb,
  created_at timestamp with time zone default timezone('utc'::text, now()) not null,
  updated_at timestamp with time zone default timezone('utc'::text, now()) not null
);

-- Performance Indexes
create index if not exists idx_medicines_user_id on public.medicines(user_id);
create index if not exists idx_schedules_medicine_id on public.medication_schedules(medicine_id);
create index if not exists idx_dose_logs_lookup on public.dose_logs(user_id, scheduled_date);
create index if not exists idx_dose_logs_schedule on public.dose_logs(schedule_id);

-- Row Level Security
alter table public.profiles enable row level security;
alter table public.medicines enable row level security;
alter table public.medication_schedules enable row level security;
alter table public.dose_logs enable row level security;
alter table public.caregiver_links enable row level security;

-- Policies: Authenticated users manage their own data
create policy "Users can manage their own profile" on public.profiles
  for all using (auth.uid() = id);

create policy "Users can manage their own medicines" on public.medicines
  for all using (auth.uid() = user_id);

create policy "Users can manage their schedules" on public.medication_schedules
  for all using (auth.uid() = user_id);

create policy "Users can manage their dose logs" on public.dose_logs
  for all using (auth.uid() = user_id);

create policy "Patients can manage their caregiver links" on public.caregiver_links
  for all using (auth.uid() = patient_id);

create policy "Caregivers can view logs when active" on public.dose_logs
  for select using (
    exists (
      select 1 from public.caregiver_links
      where caregiver_links.patient_id = dose_logs.user_id
        and caregiver_links.caregiver_id = auth.uid()
        and caregiver_links.status = 'active'
    )
  );
```
