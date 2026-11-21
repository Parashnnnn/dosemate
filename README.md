# DoseMate

> A modern, accessible healthcare web application designed to help individuals organize, manage, and track daily medication schedules with precision, clarity, and peace of mind.

---

## 🌟 The DoseMate Experience

DoseMate delivers a seamless, production-ready healthcare journey:

1. **Cinematic Animated Intro Screen**:
   - Displays on a fresh page load.
   - Built on a dark medical-tech background (`#071B18`) with an active telemetry grid.
   - Features a glowing ECG heartbeat waveform line that travels and pulses smoothly across the screen.
   - High-precision 0% to 100% telemetry counter rendered via `requestAnimationFrame`.
   - At 100%, the entire screen slides upward smoothly (`-translate-y-full`) to unveil the public landing page.
   - Session-only replay check (`sessionStorage`) with a quick accessible **Skip** option.

2. **Public Landing Page (`/`)**:
   - The first actual page users see after the intro completes.
   - **Header**: DoseMate logo and wordmark (always links to top / `/`), primary navigation links, light/dark theme switch, Log In, and Get Started CTA.
   - **Hero Section**: Two-column layout with bold headlines, clear value proposition, and an original healthcare illustration featuring an elderly grandfather taking medication with a water tumbler, phone reminder, and caring family member in the new brand palette.
   - **Section A (The Problem)**: "Managing Multiple Medicines Can Be Difficult" — highlighting forgotten schedules, complex instructions, and lack of routine tracking.
   - **Section B (Core Features)**: Strictly focused on the 6 real capabilities:
     1. *Medicine Management* (prescriptions, forms, strengths, meal timing)
     2. *Photo Upload & Camera OCR* (smart simulated label extraction)
     3. *Custom Medication Scheduling* (exact reminder times, weekdays, date ranges)
     4. *Dose Notifications & Reminders* (in-app alerts and browser notifications)
     5. *Dose Tracking* (one-tap taken confirmations, skipped with reasons, snooze)
     6. *Medication History & Adherence* (audit event trail and 7-day adherence charts)
   - **Section C (How It Works)**: Simple 3-step setup (Add Your Medicine, Set Your Schedule, Receive Reminders & Track).
   - **Section D (Product Preview)**: Interactive UI preview of the actual Dashboard, Catalog, Schedule, Notifications, and History.
   - **Section E (Final CTA)**: "Make Every Dose Count."
   - **Section F (Footer)**: DoseMate logo, navigation links, and healthcare disclaimer.

3. **Core Medication Management Web Application**:
   - **Dashboard (`/dashboard`)**: Personalized greeting, current date, today's schedule summary, next upcoming dose card, chronological timeline (Morning, Afternoon, Evening, Night), and recent activity feed.
   - **My Medications (`/medicines`)**: Medication catalog with search, active filters, form/strength details, meal instructions, schedule times, and deletion.
   - **Add Medicine (`/medicines/add`)**: Photo upload and camera OCR scanner simulation with unconfirmed value warnings, plus a detailed manual entry wizard with custom frequencies, weekdays, and start/end dates.
   - **Schedule (`/schedule`)**: Interactive daily timeline, weekly matrix, and monthly calendar views with one-tap dose actions.
   - **History (`/history`)**: KPI summaries, 7-day compliance bar chart (Recharts) in brand teal and orange, filterable audit event log table, data export, and print view.
   - **Settings (`/settings`)**: Appearance theme (strictly Light and Dark modes), browser notification permissions, default snooze interval, user profile, emergency contact, offline JSON backup export, and local data wipe.

---

## 🎨 New Brand Color Palette

- **Medical Orange** (`#D47C32`): Primary call-to-action buttons, active highlights, and badges.
- **Deep Medical Teal** (`#1D6570`): Brand identity, headers, navigation, and primary surfaces.
- **Medical Red** (`#B51F2C`): Critical alerts, skipped doses, and destructive actions.
- **Warm Ivory** (`#F7F6F1`): Primary glare-free light canvas background.
- **Charcoal** (`#202321`): High-contrast dark typography and dark surface foundations.
- **Soft Grey** (`#E7E6E0`): Dividers, subtle borders, and disabled states.
- **Muted Teal** (`#DCE9E8`): Subtle card accents and pill badges.
- **Dark Green-Black** (`#071B18`): Deep cinematic intro and telemetry backgrounds.

---

## 🛠️ Tech Stack

- **Framework**: Next.js 16 (App Router with Turbopack)
- **Language**: TypeScript (Strict typing)
- **Styling**: Tailwind CSS & Vanilla CSS variables
- **Icons**: Lucide React
- **Data Visualizations**: Recharts
- **Storage & State**: React Context with LocalStorage persistence + optional Supabase cloud synchronization

---

## 🚀 Getting Started

### Installation & Run

```bash
# Clone the repository
git clone <repo-url>
cd HaCKETHON

# Install dependencies
npm install

# Run the local development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### Production Build

```bash
npm run build
```

---

## 🛡️ Healthcare Safety Notice

DoseMate is an organizational reminder and adherence aid. It **does not provide medical advice, diagnosis, or prescription modifications**. Users must verify all entered dosages with their prescribing physician or pharmacist.
