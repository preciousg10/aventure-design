# Aventure — Screen Inventory

Status tracker for every screen in the Aventure app. Update the row whenever a screen's status changes.

For full product context (user flow, governance, reasoning), see [`CLAUDE.md`](CLAUDE.md).

**Status legend:**
- `Not Started` — no design work yet
- `In Progress` — actively being designed
- `Review` — HTML prototype done, awaiting feedback
- `Done` — HTML prototype + Figma exports locked in

**Per-screen folder:** `design/screens/<slug>/` containing `index.html`, `spec.md`, `figma/`.

**Design tokens:** every `index.html` must `<link rel="stylesheet" href="/design/tokens/tokens.css">` and build on those CSS variables — no ad-hoc colors or fonts. Full spec in [`design/tokens/DESIGN.md`](design/tokens/DESIGN.md).

---

## Phase 1 — Onboarding (9 screens)

| Screen | Slug | Status | Updated | Notes |
|---|---|---|---|---|
| Splash | `splash` | Not Started | — | 1–2s, auto-transitions |
| Welcome panel 1 | `welcome-panel-1` | Not Started | — | Auto-advance, Strava-style, first-open only |
| Welcome panel 2 | `welcome-panel-2` | Not Started | — | |
| Welcome panel 3 | `welcome-panel-3` | Not Started | — | |
| Welcome panel 4 | `welcome-panel-4` | Not Started | — | |
| Auth | `auth` | Not Started | — | Google / Apple / email link. No explanation copy |
| Your details | `your-details` | Not Started | — | First name + age only |
| Notifications pre-prompt | `notifications-pre-prompt` | Not Started | — | Explains *why* before iOS dialog fires |
| Privacy confirmation | `privacy-confirmation` | Not Started | — | Two checkboxes (privacy + terms) |

---

## Phase 2 — Personality Survey (3 screens)

| Screen | Slug | Status | Updated | Notes |
|---|---|---|---|---|
| Survey intro | `survey-intro` | Not Started | — | Cannot be skipped, sets expectations |
| Survey question (template) | `survey-question` | Not Started | — | Reusable template, 10 questions, progress bar, "Tell me more" per answer |
| Survey complete | `survey-complete` | Not Started | — | Leads into crew formation |

---

## Phase 3 — Crew Formation (8 screens)

| Screen | Slug | Status | Updated | Notes |
|---|---|---|---|---|
| Crew hub (home) | `crew-hub` | Review | 2026-06-06 | 3 layout options (A card-feed / B dashboard / C minimal) + empty state in `design/screens/crew-hub/`. Recommend Option B. Figma export guidance in spec.md |
| Create a crew | `create-a-crew` | Not Started | — | Name, max size (2–20), public/private |
| Invite screen | `invite-screen` | Not Started | — | 6-char code + shareable link |
| Join via code | `join-via-code` | Not Started | — | 6-character code entry |
| Browse public crews | `browse-public-crews` | Not Started | — | Same-city compatible crews. Has empty state variant |
| Public crew profile | `public-crew-profile` | Not Started | — | Photos, interests, compatibility %, quest history |
| Crew profile | `crew-profile` | Not Started | — | Member's view of their own crew |
| Crew settings & governance | `crew-settings-and-governance` | Not Started | — | Includes anonymous vote-to-remove flow |

---

## Phase 4 — Quest Initiation & Payment (7 screens)

| Screen | Slug | Status | Updated | Notes |
|---|---|---|---|---|
| Quest initiated | `quest-initiated` | Not Started | — | Pushed to all members the moment Leader starts |
| Budget tier selection | `budget-tier-selection` | Not Started | — | Private per member; 8% service fee shown |
| Quest vote | `quest-vote` | Not Started | — | Real-time, majority wins, ties → cheaper |
| Follow-up questions | `follow-up-questions` | Not Started | — | Only for certain quest types; private |
| Waiting room | `waiting-room` | Not Started | — | 24h countdown, avatars fill as members pay |
| Waiting room timeout | `waiting-room-timeout` | Not Started | — | Auto-refund; no names revealed |
| AI booking in progress | `ai-booking-in-progress` | Not Started | — | Pulsing avatars, fading status text, ~60–90s |

---

## Phase 5 — AI Quest Generation

Covered by `ai-booking-in-progress` above. No separate screens — Phase 5 is the bridge between payment and reveal.

---

## Phase 6 — Quest Reveal & In Progress (5 screens)

| Screen | Slug | Status | Updated | Notes |
|---|---|---|---|---|
| Quest reveal | `quest-reveal` | Not Started | — | All members see at the same instant. Designed as an event |
| Quest command centre | `quest-command-centre` | Not Started | — | 3 tabs: Now / Full quest / Crew chat |
| Step-by-step instructions | `step-by-step-instructions` | Not Started | — | Detail view for the current stop |
| Between stops | `between-stops` | Not Started | — | Navigation, travel countdown, Maps. Outdoor-readable |
| Restaurant virtual card | `restaurant-virtual-card` | Not Started | — | V1.1. Stripe virtual card for Quest Leader |

---

## Phase 7 — Post Quest (5 screens)

| Screen | Slug | Status | Updated | Notes |
|---|---|---|---|---|
| Photo dump | `photo-dump` | Not Started | — | Each member uploads; all saved to the quest |
| Memory & recap | `memory-and-recap` | Not Started | — | Photos + caption + individual ratings |
| Shareable quest card | `shareable-quest-card` | Not Started | — | Auto-generated. Share to IG/TikTok. Growth engine |
| Budget settlement | `budget-settlement` | Not Started | — | Unspent escrow → Stripe refund in 2–5 business days |
| Bucket lists | `bucket-lists` | Not Started | — | Personal + crew. AI references both for future quests |

---

## Other (5 screens)

| Screen | Slug | Status | Updated | Notes |
|---|---|---|---|---|
| Invite link landing (web) | `invite-link-landing-web` | Not Started | — | Pre-download mobile web. Detects iOS/Android. Deep links after install |
| User profile | `user-profile` | Not Started | — | Name, photo, survey answers, quest history, bucket list, account settings |
| Empty state — Crew hub | `empty-crew-hub` | Review | 2026-06-06 | Built as `crew-hub/empty-state.html`. Pre-crew formation state |
| Empty state — Quest history | `empty-quest-history` | Not Started | — | No quests yet |
| Empty state — Browse | `empty-browse` | Not Started | — | No compatible crews surfaced |

---

## Venue App — Channel A (supply side)

Separate product from the consumer crew app. Full journey in [`docs/venue-workflow.md`](docs/venue-workflow.md). Design references in gbrain page `venue-app-design-references`. Venue-app secondary is Jade `#2D6A4F` (overrides the consumer `#138A6B`).

| Screen | Slug | Status | Updated | Notes |
|---|---|---|---|---|
| V0a — Create account (invite landing) | `venue-auth-create` | Review | 2026-06-23 | Built. Tokenized invite, pre-fills venue name, founding-only. No-token state. Office-hours design doc |
| V0b — Log in | `venue-auth-login` | Review | 2026-06-23 | Built. Email + password, inline forgot link, invite-only note |
| V0c — Forgot password | `venue-auth-forgot` | Review | 2026-06-23 | Built. Reset request + confirmation state. Set-new-password screen deferred |
| V1 — Account and venue basics | `venue-onboarding-basics` | Review | 2026-06-23 | Built. Onboarding step 1/4. SMS doorbell + verify affordance. /autoplan-reviewed |
| V2 — Offerings and prices | `venue-offerings` | Review | 2026-06-24 | Built. Repeatable offering rows: experience, group price, capacity |
| V3 — Availability | `venue-availability` | Review | 2026-06-24 | Built. Cal.com weekly-hours editor: day toggles, time ranges, date overrides |
| V4 — You're all set | `venue-onboarding-done` | Review | 2026-06-24 | Built. Confirmation + recap. No Stripe (deferred to first payout) |
| V5 — Dashboard home | `venue-dashboard` | Review | 2026-06-25 | Built. Left nav (warm linen, grouped) + KPI strip (Navan: bookings today, occupancy, revenue pending, no-shows) + week grid (SavvyCal: hour rows, now-marker, Closed shading) + today's bookings list with Monarch hero number. Stub data: Greenpoint Escape Co., realistic Thu week |
| V6 — Calendar and availability | `venue-calendar` | Review | 2026-06-25 | Built. Two-pane: Cal.com weekly-hours editor (toggles drive the grid live) + SavvyCal week grid, pause-bookings toggle with banner, block-a-date with chips. Shares V5 shell + stub data |
| V7 — Booking request | `venue-booking-request` | Review | 2026-06-26 | Built. Focused doorbell card: live 10-min countdown, already-paid emphasis, accessibility notes, accept/decline with inline states. Accept links to V8 |
| V8 — Booking detail | `venue-booking-detail` | Review | 2026-06-26 | Built. App-shell detail: booking facts, confirmation ref, crew roster, mark-crew-arrived completion state |
| V9 — Earnings and payouts | `venue-earnings` | Review | 2026-06-26 | Built. App-shell: ElevenReader connect-bank hero (first/only Stripe), Monarch hero number, payout history, founding-venue zero commission |
| V10 — Settings | `venue-settings` | Review | 2026-06-26 | Built. In-app edit-and-save: venue basics, offerings/prices, availability toggles, account (email/password), pause-bookings toggle, log out. Per-section save. Reached from Settings nav |

---

## Totals

| Phase | Count |
|---|---|
| Phase 1 — Onboarding | 9 |
| Phase 2 — Personality Survey | 3 |
| Phase 3 — Crew Formation | 8 |
| Phase 4 — Quest Initiation & Payment | 7 |
| Phase 5 — AI Quest Generation | (covered by Phase 4) |
| Phase 6 — Quest Reveal & In Progress | 5 |
| Phase 7 — Post Quest | 5 |
| Other | 5 |
| **Total** | **42** |

> Note: the original brief said "41 screens" — the actual enumerated count comes out to 42 once each empty state is treated as its own screen. Flagging here so the discrepancy isn't a surprise later. Adjust if you want any of these merged or removed.
