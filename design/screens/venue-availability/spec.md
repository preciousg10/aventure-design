# Screen V3 — Availability

**Onboarding step 3 of 4** (Basics → Offerings → **Availability** → Done)

## Purpose

The weekly-hours editor for a venue. It captures when the venue is open so the
AI booking engine knows when it can send a crew. This is Layer 1 of the
availability model from `docs/venue-workflow.md` — hours set once at onboarding.
The live accept/decline ping (Layer 2) and the 10-minute timeout (Layer 3) are
later, runtime concerns, not part of this screen.

## The model (stub data, no backend)

### Weekly hours
A row per day (Monday through Sunday). Each day has:
- An **open/closed toggle** (jade switch when on).
- One or more **time ranges** (`from`–`to`), each an `<input type="time">`.
- A **second range** can be added per day for split hours (e.g. lunch closure).
  Added ranges get a remove control; at least one range stays while open.
- When **closed**, time fields hide and the row reads a muted "Closed".

Defaults: Mon–Fri 10:00–18:00, Sat 10:00–16:00, Sun closed.

### Date overrides
Exceptions that beat the weekly hours for a specific date (holidays, private
events, one-off closures). Add row = a date input + an Open/Closed segmented
control (+ from/to times when Open) + an "Add date" button. Added overrides
render as a list with a pill (Open/Closed), a readable meta line, and a remove
control. Empty state: "No date overrides yet."

### Slot-based venues
A helper note explains that for slot-based venues (escape rooms), these hours
define the bookable window; specific start times come from the offering (V2).

## Flow

Arrives from V2 (Offerings). Primary CTA **Continue** validates open days, then
(stubbed) disables, shows "Saving…", and navigates to
`../venue-onboarding-done/index.html` (V4) after ~700ms. Mirrors V1's submit
pattern.

## Validation (light)

For every open day, each range's close time must be after its open time;
invalid ranges flag with the V1 `.invalid` / error-message idiom (`.has-error`
on the row, terracotta-danger border on the time inputs). Override add-row
validates the same way before appending. Closed days never error.

## Design notes

- Matches V1 (`venue-onboarding-basics`) and V0a (`venue-auth-create`) exactly:
  Golden Hour tokens with `--secondary:#2D6A4F`, Fraunces headlines + Satoshi
  body, the two-pane `.shell` grid, sticky left `.context` panel with wordmark +
  h1 + lede + `.stepper`, `.form-card`, jade focus rings, ink-on-terracotta CTA.
- **Stepper (Editor X pattern):** Basics + Offerings = `li.done` (jade dot with a
  check SVG), Availability = `li.active` (numbered 3), Done = future/plain.
- **New components**, kept in the same idiom (divider borders, jade accents,
  `--radius-input`, muted labels):
  - **Day toggle**: a real switch, jade track when on, white knob, focus ring.
  - **Time fields**: `<input type="time">` at 44px height matching input styling.
  - **Add/remove range**: jade-outlined round icon buttons + a text "Add hours".
  - **Date overrides**: segmented Open/Closed control, list rows on the warm-linen
    surface with Open (success) / Closed (danger) pills.
- Reference: **Cal.com Availability** (Refero `c07105e3`) — per-day toggles,
  time-range fields, add-slot affordance, Date overrides section. Structure
  borrowed, recolored to Golden Hour.
- Rules honored: ink (`#2A2521`) on the terracotta CTA, never white; no em
  dashes in on-screen copy; no dark backgrounds; Fraunces headlines, Satoshi
  body. Single self-contained HTML file, inline CSS + JS, only the two font
  links as external deps. Opens via `file://` and over an http server. No
  fetch/network; all JS is local DOM.
