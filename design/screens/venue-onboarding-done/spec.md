# Screen V4 — You're all set (venue onboarding confirmation)

**Slug:** `venue-onboarding-done`
**Phase:** 2 — Onboarding (done once)
**Onboarding step:** 4 of 4 (final)

## Purpose

Close out venue onboarding. This is the confirmation screen the venue lands on
after completing Basics (V1), Offerings (V2), and Availability (V3). It tells them
the work is done, reassures them, and hands off to the dashboard. No new input is
collected here.

## Required copy

The screen must carry this line close to verbatim, and it appears prominently in
the right card:

> When a crew wants to come, we'll text you. Tap to accept. That's it.

This is the SMS doorbell promise — the core mental model for how a venue receives
bookings.

## No Stripe / payments here (deliberate)

There is **no payment, bank, or Stripe Connect step on this screen.** Stripe Connect
is deferred to the first payout (Screen V9 — Earnings and payouts), triggered by a
real payout being ready, not by onboarding. Do not add any payment/bank/connect
affordance here. The recap checklist intentionally lists only account, offerings,
and availability.

## Flow

- Entry: from V3 Availability (Continue / Finish).
- Exit: primary CTA **"Go to your dashboard"** → `../venue-dashboard/index.html`
  (Screen V5, not built yet — this is a forward placeholder link).

## Layout

- Two-pane `.shell` grid, identical structure to V1 (`venue-onboarding-basics`).
- **Left `.context` panel:** wordmark (Aventure / for venues), Fraunces headline
  "You're all set", a short warm lede, and the 4-step `.stepper`.
- **Right `.form-card`:** used here as a confirmation card (no form):
  - Success moment: a jade/success (`--success` #3D8060) check inside a soft
    tinted circle. Professional and warm — no confetti, no emoji.
  - Heading "Your venue is ready" + short sub.
  - The required doorbell line in an emphasized callout (jade left border).
  - A restrained recap checklist: Account and basics, Offerings and prices,
    Availability — each with a small jade check. No payments mentioned.
  - A founding-venue reassurance line (zero fees until paying groups arrive).
  - Primary CTA "Go to your dashboard".

## Stepper (Editor X progress pattern)

Four steps: Basics, Offerings, Availability, Done.

- Steps 1–3 (Basics, Offerings, Availability) = `li.done` — jade dots showing an
  inline SVG check instead of the number.
- Step 4 (Done) = `li.active` — current step, jade dot with the number 4.

Added CSS over the V1 base:

```css
.stepper li.done{color:var(--ink);}
.stepper li.done .dot{background:var(--secondary);border-color:var(--secondary);color:#fff;}
```

## Design notes

- Matches V1 (`venue-onboarding-basics`) and V0a (`venue-auth-create`) design
  language exactly: Golden Hour tokens with `--secondary:#2D6A4F`, Fraunces +
  Satoshi font links, two-pane shell, `.form-card`, ink-on-terracotta `.btn-primary`.
- The success-mark and `.reassure` styling echo V0a's jade-check confirmation feel.
- Hard rules honored: ink (`#2A2521`) text on the orange (`#E2693E`) CTA, never
  white. No em dashes in on-screen copy. No dark backgrounds. Fraunces headlines,
  Satoshi body.
- Self-contained single HTML file, inline CSS, no JS needed (CTA is a styled
  `<a>`). Opens via `file://` and over an HTTP server. Stub only — no backend, no
  network.
- `prefers-reduced-motion` and the `max-width:760px` responsive block carried from
  V1 so a concierge can show this on a phone/tablet in person.

## States / edge cases

- Single static state. No validation, no loading. The CTA navigates to the future
  V5 dashboard; until V5 exists the link is a known forward placeholder.
