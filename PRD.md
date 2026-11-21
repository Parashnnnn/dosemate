# DoseMate — Smart Medication Companion
## Product Requirements Document (PRD)

**Product Name:** DoseMate  
**Tagline:** Smart Medication Companion  
**Domain:** Healthcare Adherence & Routine Support

---

## 1. Executive Summary
DoseMate is an accessible, human-centered medication companion designed to solve prescription forgetfulness and cognitive overload for individuals and elderly patients. Built with three core entry experiences (Animated Grandfather Introduction, Comprehensive Public Landing Page, and Functional Medication Management Application), it provides clear visual timelines, voice guidance, photo scanning review, refill tracking, and caregiver privacy controls without clutter.

---

## 2. Core Entry Experiences

### Experience A: Animated Intro Screen
- Full-screen opening sequence shown once per session on fresh website visit.
- Visual storytelling: Elderly Indian grandfather in a peaceful living room gently takes his medicine with a glass of water, sets the glass down, and smiles with reassurance.
- Brand reveal: "DoseMate — Smart Medication Companion: Making every dose count..."
- Responsive, reduced-motion friendly, with an accessible "Skip" button.

### Experience B: Public Landing Page (`/`)
- Displayed immediately after the intro finishes.
- Two-column hero with custom healthcare artwork: Grandfather, caring family member, smartphone with DoseMate alert, and weekly organizer.
- Sections:
  1. The Everyday Problem ("Remembering Every Dose Shouldn't Be Difficult.")
  2. Features (8 core modules)
  3. How DoseMate Works (3-step setup)
  4. Designed for Everyone (Senior ergonomics & Easy Care Mode)
  5. A Look Inside DoseMate (Interactive live preview tabs)
  6. Final CTA ("Make Every Dose Count.")
  7. Footer with disclaimer and navigation
- **Logo Navigation Rule**: Clicking the DoseMate logo from ANY page in the app always navigates to `/`.

### Experience C: Medication Application (`/dashboard`)
- Real user data management without fake demo records.
- Time-of-day timeline: Morning, Afternoon, Evening, Night.
- Dose confirmation modals with auditory feedback and immediate stock decrement.

---

## 3. Product Features & Modules

| Module | Route | Key Capabilities |
|---|---|---|
| **Landing Page** | `/` | Hero artwork, problem statement, features, workflow, interactive tabs, footer |
| **Authentication** | `/login`, `/register` | Real profile creation, Supabase Auth integration, clean redirect |
| **Dashboard** | `/dashboard` | Next dose hero, adherence bar, time-of-day timeline, low-stock warnings |
| **My Medicines** | `/medicines` | Catalog cards, pill stock levels, voice TTS read-aloud, delete/edit |
| **Add Medicine** | `/medicines/add` | Option A (Camera/Photo drop with OCR preview) + Option B (Manual wizard) |
| **Schedule** | `/schedule` | Daily timeline, weekly matrix, monthly calendar with date picker |
| **History** | `/history` | 7-day adherence chart (Recharts), audit log table, printable medical report |
| **Refills** | `/refills` | Remaining count, dynamic days-left calculation, quick restock modal |
| **Caregiver** | `/caregiver` | Consent-based pairing code generator, simulated caregiver viewer |
| **Settings** | `/settings` | Easy Care Mode, Web Audio chime test, notifications, theme switch |

---

## 4. Healthcare Safety
DoseMate is an organizational reminder and adherence aid. It **never prescribes, diagnoses, or modifies medical dosages**. Scanned image text is strictly treated as an unconfirmed suggestion requiring mandatory patient review against their prescription.
