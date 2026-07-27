# Screen V2 — What you offer and your prices (`venue-offerings`)

Onboarding **step 2 of 4** for the Aventure venue app (supply side, Channel A).

## Purpose
The venue lists the experiences it runs and sets its own group price for each, plus
how many people fit per booking. For the founding cohort this is a concierge form:
Ryan fills it in on the venue's behalf during recruitment, then hands it over. This
data later feeds the AI booking engine (price and capacity per offering).

## Fields (per offering row)
- **Experience name** — text, required. e.g. "The Lost Vault escape room".
- **Group price** — number with a `$` prefix affordance, required, must be greater than 0.
  The flat price a group pays for this experience.
- **Capacity per booking** — number, required, whole number 1 or more. Most people
  the venue can take in one booking.

The screen renders **one offering row** by default. An "Add another offering" button
appends a new row. Every row past the first shows a quiet "Remove" affordance; the
list never drops below one row (Remove is hidden when only one remains).

## Validation
- Inline, reusing V1's `.field.invalid` + `.error-msg` pattern.
- Validate-on-blur once a field is touched, and again for every field on submit.
- Name required (non-empty); price a finite number > 0; capacity a whole integer >= 1.
- On a failed submit, focus jumps to the first invalid input.

## Flow
- Primary CTA **"Continue"** → on a valid submit, disables, swaps its label to
  "Saving…", then after a short stubbed delay navigates to
  `../venue-availability/index.html` (**Screen V3 — Availability**).
- Nothing is carried in the URL.
- Stub only: no backend, no fetch/network. Mirrors V1's submit pattern.

## Stepper (Editor X progress bar pattern)
Four steps: Basics, Offerings, Availability, Done.
- **Basics** = `li.done` — jade dot with an inline SVG check.
- **Offerings** = `li.active` — jade dot showing the number 2 (this screen).
- **Availability / Done** = plain, muted, numbered.

## Design notes
- Matches the V1 (`venue-onboarding-basics`) and V0a (`venue-auth-create`) design
  language exactly: V1's full `<style>` block is the verbatim base (Golden Hour tokens
  with `--secondary:#2D6A4F`, Fraunces + Satoshi, two-pane `.shell` grid, sticky left
  `.context` panel with wordmark + h1 + lede + `.stepper`, `.form-card`, the
  `.field`/`.error-msg`/`.invalid` validation pattern, jade focus ring,
  `.btn-primary` with `color:var(--ink)` on terracotta, the `cursor:default` chrome
  rule, the `@media (max-width:760px)` responsive block).
- Added on top: `.stepper li.done` rules for completed steps; `.offering` row card;
  `.btn-remove`; `.btn-add` (dashed jade outline, secondary weight); `.row-grid`
  (price + capacity two-up, stacks on mobile); `.money-field` `$` affix; number-spinner
  reset so the inputs read clean.
- Golden Hour throughout: warm linen background, white cards, ink text on the terracotta
  CTA (never white), jade secondary. No dark backgrounds, no em dashes in on-screen copy.
- Self-contained single HTML file, inline CSS + JS, only the two font `<link>`s as
  external deps. Opens over `file://` and an http server. The offering row lives in a
  `<template>` and is cloned per row.

## Reference
Editor X "set up your store" progress bar (gbrain `venue-app-design-references`),
recolored to Golden Hour with the dark sidebar rejected per the no-dark-backgrounds ban.
