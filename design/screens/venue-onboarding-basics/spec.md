# Screen V1 — Account and venue basics

Venue app onboarding, step 1 of 4. Captures the minimum to create a venue and, critically, the SMS number that receives the booking doorbell. Reviewed via /autoplan (single-model, scoped to V1) and approved 2026-06-23.

## Purpose
First screen in the build order. Desktop-web dashboard onboarding step, mobile-friendly because the concierge (Ryan) fills it in person on a phone or tablet during recruitment. Stub data, no backend.

## Layout
- Two-pane on wide screens: left context panel (brand + vertical 4-step stepper + reassurance copy), right the form card. Stacks to single column on mobile.
- Not a centered marketing hero. A working form, content left-aligned.
- Progress: "Basics · Offerings · Availability · Done", step 1 active. Stepper accent uses secondary Jade `#2D6A4F` (T3); terracotta is reserved for the primary CTA.

## Fields (all required unless noted)
1. Venue name — text.
2. Venue type — select: Escape room, Bouldering gym, Axe throwing, Arcade, Other. "Other" reveals a free-text field.
3. Address — search-style typeahead input (magnifier icon + suggestion dropdown with map-pin rows). Stubbed with sample suggestions for the prototype; real Google Places autocomplete needs an API key + backend, swapped in during the backend phase.
4. Contact name — text.
5. SMS number (the doorbell) — tel. Helper: "This is where we text you when a crew wants to book." Strict format validation + a stubbed "Verify number" affordance (T1); the real test-text is deferred to the backend phase.

## States (resolved from review)
- Inline validation with required-field handling and per-field error messages.
- Submit/loading state on Continue (pattern exists now for when the backend lands).
- "Other" venue type reveals a free-text input.
- Accessibility: every input has an associated `<label>`; visible focus rings; keyboard navigable.

## Design system
Golden Hour. bg `#FBF6EE`, card `#FFFFFF`, primary `#E2693E`, secondary `#2D6A4F` (venue-app canonical, overrides the consumer `#138A6B`), success `#3D8060`, ink `#2A2521`, muted `#7A6E68`, divider `#ECE4D8`. Fraunces headlines, Satoshi UI/body. Primary CTA: terracotta background, ink text (never white). No em dashes in on-screen copy. No dark backgrounds.

## Copy
- Concierge framing line: a quiet note that Ryan can fill this in during recruitment.
- CTA: "Continue" advances to V2 (stubbed; no backend).

## Out of scope for V1
Real SMS verification / A2P 10DLC registration (backend phase), Places autocomplete, multi-staff logins. Logged as failure modes in `docs/venue-workflow.md`.

## Reference
Editor X progress-bar pattern (gbrain `venue-app-design-references`, id `9deb20ea`). Dark sidebar rejected per the no-dark-backgrounds ban.
