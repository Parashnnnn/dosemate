# DoseMate — Design System & Visual Specification

## 1. Brand Philosophy
DoseMate delivers an atmosphere of **safety, clarity, reassurance, and calm**. Using organic nature-grounded tones (deep forest greens and soft sage) with porcelain backdrops and warm amber alerts, it avoids cold clinical hospital aesthetics as well as over-saturated tech dashboards.

## 2. Color Palette

| Token Name | Hex Code | Purpose |
|---|---|---|
| **Midnight Forest** | `#17231D` | Headings, high-contrast text, dark canvas surfaces |
| **Soft Porcelain** | `#F7F8F4` | Light canvas background, gentle and glare-free |
| **Soft Sage** | `#DDE9DF` | Subdued borders, badge backgrounds, pill tag accents |
| **Care Green** | `#4F8064` | Primary CTAs, active states, confirmed doses, progress bars |
| **Warm Amber** | `#E8B86A` | Gentle alerts, low-stock warnings, snoozes, attention tags |
| **Mist Grey** | `#E5E8E3` | Dividers, subtle borders, disabled states |
| **White** | `#FFFFFF` | Primary light card surfaces, modals, popovers |

## 3. Typography
- **Headings**: `Plus Jakarta Sans`, sans-serif (Weights: 700 Bold, 800 ExtraBold)
- **Body & Controls**: `Inter`, system-ui, sans-serif (Weights: 400 Regular, 500 Medium, 600 SemiBold)
- **Tabular Figures**: `font-variant-numeric: tabular-nums` for timers, pill counts, and hours.

## 4. Senior Accessibility: Easy Care Mode
- Base font scales up to `1.15rem` (18-20px+).
- Minimum button height expands to **56px**.
- Headings scale to `2.35rem` (38px+).
- Contrast ratio strictly exceeds **7:1** (WCAG 2.1 AAA).
- Web Speech API integration reads medicine names, instructions, and dosages aloud with a single click.

## 5. Navigation & Brand Identity
- **DoseMate Symbol**: Heart-pulse healthcare emblem inside a smooth rounded badge.
- **Logo Behavior**: Clicking the DoseMate logo from **ANY** screen always navigates to `/` (the public landing page).
