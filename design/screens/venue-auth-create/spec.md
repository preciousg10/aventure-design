# Screen V0a — Create account (invite-link landing)

First screen in the build order. The tokenized invite link from Ryan's email lands here. Part of the V0 auth gate; see `docs/venue-auth-v0-design.md`.

## Invite contract
The link encodes a **real per-venue token** (e.g. `?invite=fnd_<token>`), not just a name. The token:
- is unique per venue,
- marks them as a founding partner (zero fees),
- pre-fills the venue name on this screen,
- is the only way to create an account during the founding phase (no public signup yet).

Stub: with no backend to resolve token to name, the screen reads `?invite=<token>` to enter the founding flow and `?venue=<name>` as the demo source for the pre-filled name (defaults to a sample venue when omitted). Real token resolution lands with Supabase Auth.

**No-token state:** a visit with no `?invite=` shows a gentle, warm message ("You'll need an invite from the Aventure team") instead of the form. Invite-only during the founding phase.

## Fields
1. Venue name — pre-filled from the token, editable (in case of a typo).
2. Email — work email for the venue.
3. Password — with show/hide toggle and a minimum-length rule (8+).

## Flow
- Primary CTA "Create account" (terracotta bg, ink text) advances to V1 onboarding.
- Secondary: quiet "Already have an account? Log in" link to V0b (`venue-auth-login`).

## Tone (from Ryan's invite email)
Warm, direct, a real person who already met them. No corporate fluff. The left panel echoes the email: a "Founding venue" badge and "zero fees until we're sending you paying groups." Headline welcomes them by venue name.

Invite email copy (source of truth for voice):
> Subject: You're in. Aventure is bringing you crews.
> Hi [Venue name], Thanks for the chat. You're officially one of Aventure's founding venues, which means zero fees until we're actually sending you paying groups. Tap below to set up your account. It takes about a minute, and your venue is already pre-filled. [Set up my venue] Any questions, just reply to this email. Talk soon. Ryan, Aventure

## Design
Golden Hour, Fraunces headline, Satoshi body. Ink on the orange CTA, never white. No em dashes on screen. No dark backgrounds. Reuses V1 patterns: inline validation, focus rings, non-selectable chrome. Stub only, no backend.
