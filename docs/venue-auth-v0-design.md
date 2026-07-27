# V0 — Venue auth: office-hours design doc

Date: 2026-06-23 · Mode: startup (supply side) · Status: APPROVED
Companion to `docs/venue-workflow.md` (Phase 1.5). Visual altitude: gbrain `venue-app-design-references`.

## What this is
The auth gate before onboarding for the Aventure venue app. Founding venues arrive via a unique invite link Ryan sends during recruitment; the link lands them on create-account with their venue name pre-filled, so it feels hand-picked, not generic. Public self-serve signup is deferred to post-launch. Build the invite-link version first.

## Premises (challenged, then settled)
1. Auth gates onboarding; V0 precedes V1. **Agreed.**
2. Invite-link-first, public signup later. **Agreed** — gives Ryan control of the founding cohort and makes it feel considered.
3. Stub the backend (Supabase Auth) for now. **Agreed** — screens and flow exist without a live DB.
4. Auth method. **Challenged:** the invite link already proves the venue controls that inbox, so a magic-link/passwordless flow would remove the password, confirm, forgot-password, and reset surface entirely. **User decision: email + password** (familiarity, works when login email is slow, clean path to public signup). Kept. A magic-link path can slot in behind the same screens later without rework, since the stub commits to nothing.

## Chosen approach — B: separate route-screens
Three screens, each its own file/folder, mirroring the eventual Supabase routes:
- `design/screens/venue-auth-create/` — V0a Create account (invite-link landing)
- `design/screens/venue-auth-login/` — V0b Log in (returning)
- `design/screens/venue-auth-forgot/` — V0c Forgot password

Rejected: A (single screen + toggle) — faster but blends three routes into one file. C (email-only continue) — contradicts the two-paths + password decision.

## Screen specs

### V0a — Create account (invite-link landing)
- Reads an invite token from the URL (`?invite=<token>` in the stub) and pre-fills the venue name, shown as a warm, specific welcome ("Let's get [Venue] set up"). Venue name editable in case Ryan typo'd it.
- Fields: email, password (with a visible show/hide and basic strength/length rule), venue name (pre-filled).
- Primary CTA "Create account" (terracotta bg, ink text) → advances to V1 onboarding.
- Secondary: quiet "Already have an account? Log in" link → V0b.
- No public-signup entry point yet (invite-only); a no-token visit shows a gentle "You'll need an invite link from the Aventure team" state.

### V0b — Log in (returning)
- Fields: email, password.
- Primary CTA "Log in" → dashboard (V5) if onboarding complete, else resume onboarding (V1).
- "Forgot password?" link → V0c. No create-account link (invite-only for now).

### V0c — Forgot password
- Field: email. CTA "Send reset link" → inline confirmation ("If that email is on file, a reset link is on its way"). Back-to-login link.
- Reset-link landing (set new password) is part of the reset flow; stub the request side for V0, note the set-new-password screen as a follow-up.

## Design bar
Golden Hour: bg #FBF6EE, card #FFFFFF, primary #E2693E, secondary #2D6A4F, success #3D8060, ink #2A2521, muted #7A6E68, divider #ECE4D8. Fraunces headline, Satoshi body. Ink on the orange CTA, never white. No em dashes on screen. No dark backgrounds. Professional but warm; carry over the V1 patterns (inline validation, focus rings, non-selectable chrome, search-field conventions where relevant).

## Stub behavior (no backend)
No Supabase Auth yet. Submits validate client-side then advance/show success. Invite token is a URL param that pre-fills; no token verification. Real Supabase Auth (sessions, password hashing, real reset emails) lands in the backend phase.

## Out of scope / deferred
Real Supabase Auth, session management, public self-serve signup, set-new-password reset screen wiring, SSO. Magic-link is a live future option, not built now.

## The assignment
Before building the screens: paste one real founding-venue invite email you'd actually send (subject + body + the link), and confirm what the link encodes (just a venue name to pre-fill, or a real per-venue token). That one artifact pins down V0a's pre-fill contract and the copy tone, and it's the thing only you can decide. Then we build V0a → V0b → V0c.
