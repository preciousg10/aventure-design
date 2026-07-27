# Aventure — Venue App User Workflow (v0.1)

> This maps the full journey for a venue using Aventure, the supply side of the marketplace (Channel A). Venue-side companion to the crew User Workflow. Source of truth for designing and building the venue web app.

> **Positioning.** The venue app is NOT FareHarbor, Resova, or Peek Pro. It is a professional B2B booking dashboard, OpenTable-grade, not DoorDash Order Manager. A real, capable tool a business owner feels proud to use daily: a calendar view, time slot management, meaningful numbers on the dashboard, and a polished profile.

> **Design system:** Golden Hour. bg #FBF6EE, card #FFFFFF, primary #E2693E, secondary #2D6A4F, success #3D8060, ink #2A2521, muted #7A6E68, divider #ECE4D8. Headlines Fraunces, UI and body Satoshi. Ink on orange buttons never white. No em dashes. No dark backgrounds.

## Phase 1 — Recruitment (off-app)
Direct outreach by Ryan and Amogh. Pitch: "You pay nothing until we bring you a paying group." Ryan notes what booking system each venue currently runs during recruitment. Concierge model for founding cohort: Ryan enters venue data on their behalf.

## Phase 1.5 — Access and auth (the gate before onboarding)

### Screen V0 — Venue auth (sign up / log in)
The gate that stands before onboarding. This is a web app, so no Apple or Google sign-in: email and password only. Two paths on one surface: create account (new venue) and log in (returning venue), plus a forgot-password link.

**Access model (build this first):** founding venues arrive through a unique invite link Ryan sends during recruitment. The link lands them directly on the create-account screen with their venue name pre-filled, so it feels considered, not generic. A public self-serve signup URL comes later, post-launch; the invite-link version is the V1 build target.

**Design bar:** professional but warm. Golden Hour tokens, Fraunces headline, Satoshi body, ink on the orange CTA (never white), no em dashes, no dark backgrounds. Reference the gbrain `venue-app-design-references` page for visual altitude.

**Backend:** defer the real auth backend (Supabase Auth) to the backend phase. Stub it for now so the screens and flow exist without a live database. On submit, advance to Screen V1.

**Structure (office-hours decision, 2026-06-23):** three separate route-screens, mirroring the eventual Supabase routes — V0a create account (`venue-auth-create`), V0b log in (`venue-auth-login`), V0c forgot password (`venue-auth-forgot`). Auth method confirmed as email + password after weighing a passwordless magic-link path (kept password; magic-link remains a future option). Full rationale, screen specs, and the assignment in `docs/venue-auth-v0-design.md`.

## Phase 2 — Onboarding (done once)

### Screen V1 — Account and venue basics
Venue name, type, address, contact name, and the SMS number that receives the doorbell. Reference: Editor X progress bar pattern for the concierge form.

### Screen V2 — What you offer and your prices
Venue lists experiences and sets their own group price per offering. Also captures capacity per booking. Ryan fills this during recruitment for founding venues.

### Screen V3 — Availability
Weekly hours editor (Cal.com pattern: per-day toggles, time-range fields, date overrides for holidays and closures). For slot-based venues like escape rooms, specific bookable time slots. This feeds the AI booking engine.

### Screen V4 — You're all set
Confirmation. One line: "When a crew wants to come, we'll text you. Tap to accept. That's it." Stripe Connect is NOT here. It is deferred to first payout.

## Phase 3 — The dashboard (daily use)

### Screen V5 — Dashboard home
The screen a venue owner opens every day. KPI strip at top (Navan pattern): bookings today, occupancy, revenue pending, no-shows. Below: today's confirmed bookings as a list. Week-grid calendar (SavvyCal pattern) showing all upcoming bookings on a real calendar surface with hour rows, a now-marker, and shaded unavailable slots. Left navigation grouped by domain. This is the "established business" feel.

### Screen V6 — Calendar and availability management
Full calendar view. Weekly hours editor on the left (Cal.com). Week grid on the right (SavvyCal). Venue can see, edit, and block slots from one surface. Pause toggle to stop incoming bookings when slammed. Date blocking for closures.

## Phase 4 — Receiving a booking (the core loop)

### The doorbell (SMS)
When the AI matches a crew, the venue gets a text: "Group of 5, Saturday 8pm, already paid, tap to accept." The link opens the dashboard directly to the booking request screen.

### Screen V7 — Booking request (accept or decline)
The heart of the app. Shows group size, time, experience, payment amount, crew leader name, and any dietary or accessibility notes. Two large buttons: Accept or Decline. 10-minute timeout: if no response, auto-routes to next ranked backup venue. Crew never waits.

### Screen V8 — Booking detail
Full picture for any confirmed booking: arrival time, group size, roster, confirmation reference, crew leader, notes. Contains the mark-arrived / done action used at completion.

## Phase 5 — After the crew (completion and payout)

### Completing a booking
Venue taps "done" when crew shows up. Releases payout instantly via Stripe Connect (commission netted, zero for founding venues) and records arrival. Failsafe: if venue forgets, payout auto-releases 24 hours after booking time.

### No-shows
Venue marks no-show. Cost falls on crew, not Aventure, not venue.

### Screen V9 — Earnings and payouts
Payout history: pending, paid, running total. A summary rail with one hero number (Monarch Money pattern). A "connect your bank" state when Stripe is not yet connected (ElevenReader "payouts disabled" pattern). This is the first and only time Stripe Connect appears, triggered by a real payout being ready, not by onboarding.

## Phase 6 — Settings and account (ongoing)

### Screen V10 — Settings
Where a venue edits everything they set during onboarding, reached from inside the app (the Settings item in the left nav), not a first-time wizard. One scrolling column of section cards, each with an edit-and-save context: a Save button that stays quiet until a field changes, then confirms.

Sections:
- **Venue basics** (mirrors V1): venue name, address, contact name, and the SMS number that receives the doorbell.
- **Offerings and prices** (mirrors V2): each experience with its group price and capacity, inline-editable, plus a link to the full offerings editor for adding or removing.
- **Availability and hours** (mirrors V3 and V6): per-day open and closed toggles with the standard hours, plus a link into the calendar (V6) for date overrides and finer control. The calendar stays the single source of truth for hours; settings is a fast surface for the common edits.
- **Account**: email and a change-password control.
- **Bookings**: the pause-new-bookings toggle (same control as V6), with a line explaining existing bookings are unaffected.
- A quiet log-out link at the foot.

Reuses the onboarding field patterns (labels, inputs, toggles) but framed as editing existing values, not entering them for the first time. Same Golden Hour shell as V5 to V9, Settings nav active.

## The availability model

- Layer 1, set once: hours, capacity, and time slots from onboarding (Screen V3).
- Layer 2, live check: the accept or decline ping is the real-time availability check.
- Layer 3, failsafe: 10-minute timeout auto-routes to backup venue.

## Design references mapped to screens

- V1 to V4 onboarding: Editor X progress bar pattern
- V5 dashboard: Navan KPI strip + Monarch hero number rail
- V5 and V6 calendar: SavvyCal week grid + Cal.com weekly hours editor
- V7 booking request: clean two-button accept/decline, no clutter
- V9 earnings: ElevenReader payouts surface with deferred Stripe Connect state
- V10 settings: sectioned edit-and-save account/settings pattern, onboarding fields in an edit context

## Out of scope for launch
Full POS, waivers, OTA distribution, CRM, analytics, multi-staff logins, calendar sync with existing systems.

## Build order
1. Auth gate V0 (invite-link create-account first; stub Supabase Auth)
2. Onboarding V1 to V4 (no backend needed, stub data)
3. Dashboard V5 and calendar V6 (the daily-use surface)
4. Booking request and detail V7 and V8 (core loop, needs Supabase)
5. Earnings V9 and Stripe Connect deferred payout trigger
6. Settings V10 (edit everything from onboarding, in-app)
