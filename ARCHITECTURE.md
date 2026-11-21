# DoseMate — System Architecture & Technical Specifications

## 1. System Topology & Routing Architecture

```
                                  [ User Visit ]
                                         |
                                (Fresh Page Load?)
                                  /            \
                              [Yes]            [No / Internal Navigation]
                               /                  \
              [ Experience A: IntroScreen ]         \
             (Grandfather Storytelling 3.5s)         \
                            \                        /
                    [ Experience B: Public Landing Page ( / ) ]
                    - Hero Two-Column Artwork (Grandfather & Daughter)
                    - Problem, Features, 3-Step Setup
                    - Inside DoseMate Live Tabs
                    - Navbar & Footer
                                    |
                    [ "Get Started" / "Log In" ]
                                    |
                    [ Experience C: Application Shell ]
            +------------------------------------------------+
            | Routes:                                        |
            | - /dashboard       (Timeline & Adherence Hero) |
            | - /medicines       (Catalog & Inventory)       |
            | - /medicines/add   (Photo OCR & Manual Wizard) |
            | - /schedule        (Daily, Weekly, Calendar)   |
            | - /history         (Recharts Adherence & Audit)|
            | - /refills         (Dynamic Supply Projection) |
            | - /caregiver       (Consent Sharing Codes)     |
            | - /settings        (Easy Care Mode & Audio)    |
            | - /login, /register(Authentication Pages)      |
            +------------------------------------------------+
                                    |
                      [ DoseMate Context Layer ]
                                    |
                 +------------------+------------------+
                 |                                     |
    [ Supabase Cloud Backend ]               [ Local Persistent Storage ]
    - PostgreSQL with RLS                    - Real User LocalStorage
    - Supabase Auth                          - No Fake Demo Mock Records
    - Supabase Photo Storage                 - Real Inventory Tracking
```

## 2. Audio & Speech Synthesis
- **Web Audio API Chime**:
  Dual-tone harmonic synthesizer (`523.25Hz C5` to `783.99Hz G5`) with exponential decay. Zero external audio downloads required, functional offline.
- **Web Speech API**:
  `speechSynthesis` engine configured with slower pace (`0.88x`) for senior comprehension, reading out dosage directions with one click.

## 3. Real Data Persistence
- Unlike demo-based prototypes, DoseMate manages authentic user data.
- Initial state starts clean. New medications added by the user are immediately stored in real storage (or synced with Supabase).
- Inventory counts decrement reliably when doses are confirmed.
- Dose confirmations prevent duplicate clicks and record exact timestamps.
