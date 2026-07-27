# Screen V0c — Forgot password

Part of the V0 auth gate; see `docs/venue-auth-v0-design.md`. Reached from the "Forgot password?" link on V0b.

## Flow
- Field: email. CTA "Send reset link" → inline confirmation ("If that email is on file, a reset link is on its way"), shown regardless of whether the address exists (no account enumeration). Button changes to "Resend link".
- "Back to log in" link returns to V0b.

## Out of scope
The reset-link landing (set-a-new-password screen) is a follow-up, wired with the real reset flow in the backend phase. V0c stubs the request side only.

## Design / stub
Golden Hour, Fraunces headline, Satoshi body, ink on the orange CTA, no em dashes, no dark backgrounds. Reuses the V0a auth shell. Stub only; real reset emails come with Supabase Auth.
