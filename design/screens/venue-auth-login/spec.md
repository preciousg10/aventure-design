# Screen V0b — Log in (returning venue)

Part of the V0 auth gate; see `docs/venue-auth-v0-design.md`. Returning founding venues sign in here.

## Fields
- Email (the address used at signup).
- Password, with a show/hide toggle. "Forgot password?" link sits inline next to the password label, routing to V0c (`venue-auth-forgot`).

## Flow
- Primary CTA "Log in" (terracotta bg, ink text) → dashboard (V5) if onboarding is complete, else resume onboarding (V1).
- No create-account link: founding phase is invite-only. A quiet note points invite-holders to the link Ryan emailed.

## Design / stub
Golden Hour, Fraunces headline, Satoshi body, ink on the orange CTA, no em dashes, no dark backgrounds. Reuses the V0a auth shell and V1 patterns (inline validation, focus rings, non-selectable chrome). Stub only; real session auth is Supabase Auth in the backend phase.
