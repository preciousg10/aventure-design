# Aventure — Design Workspace

This is the design workspace for **Aventure**. Everything below is the product brain — full context, full user flow, governance rules, and pointers to the screen tracker. Any future Claude session reading this file should have enough to reason about any screen or design decision in the repo.

---

## Quick reference

| | |
|---|---|
| **Product** | Aventure — AI-powered group experience app |
| **Domain** | aventure.world |
| **Tagline** | "Your crew. Your quest. Your world." |
| **Target launch** | Late July 2026 |
| **Audience** | Gen Z (16–24) |
| **Platform** | iOS first, Android second |
| **Screen tracker** | See [`SCREENS.md`](SCREENS.md) |

---

## What Aventure is

An AI-powered group experience app. It solves the universal problem of plans dying in group chats — nobody decides, everyone has opinions, nothing happens. Aventure removes all planning friction. The crew just shows up.

---

## How it works (full user flow)

### Phase 1 — Onboarding

- **Splash screen** — 1–2 seconds, then auto-transitions.
- **Welcome slideshow** — 4 panels, auto-advance like Strava, explains the app. Only shown on first open.
- **Auth screen** — Google / Apple / email + login link. No explanation copy; they just watched the slideshow.
- **Details screen** — first name and age only. No last name, no username.
- **Notifications pre-prompt** — explains WHY notifications matter before iOS fires the system dialog. Without notifications, the waiting room mechanic breaks entirely.
- **Privacy confirmation** — two checkboxes (privacy policy + terms), not a wall of legal text.

### Phase 2 — Personality Survey

- Cannot be skipped.
- 10 questions, one per screen, progress bar.
- Each answer has a "Tell me more" option explaining why Aventure is asking.
- Before the survey, users can browse the app but can't create or join a crew — a soft persistent nudge pushes them toward it.
- Survey complete screen leads to crew formation.

### Phase 3 — Crew Formation

Users can create a crew or join one.

**Creating:** set crew name, max size (2–20), public or private.

**Joining — two ways:**
1. **Private** — 6-character code or invite link shared by a friend.
2. **Public** — Aventure surfaces compatible crews in the same city. Each crew card shows member photos, 3 things each member enjoys, compatibility percentage + what they have in common, and quest history snapshot.

**Crew governance:**
- Every crew has a Crew Leader.
- Crew Leader can start quests and set budget caps.
- Any member can anonymously vote to remove another — majority rules.
- Crew Leader has no more say in quest selection than anyone else.

### Phase 4 — Quest Initiation & Payment

Sequence: quest initiated → budget selection → quest vote → follow-up questions (if needed) → waiting room → AI generation.

- Crew Leader taps "Start a quest" — all members get a push notification immediately.
- Each member privately selects a budget tier (no one sees what others picked). 8% Aventure service fee shown transparently.
- Quest options are shown based on the combined budget pool, least to most expensive. Crew votes in real time — majority wins, ties go to the cheaper option.
- Follow-up questions only trigger for certain quest types (dietary restrictions, sizing, accessibility). Private per member.
- **Waiting room:** 24-hour countdown. Each avatar is grey until paid, then fills in with profile photo. Crew can see who has/hasn't paid.
- If timer hits zero and not everyone paid: Stripe auto-refunds everyone. Quest cancelled. No names revealed in the cancellation.
- Crew chat unlocks once quest vote is complete.

### Phase 5 — AI Quest Generation

- Once all payments confirmed in Stripe escrow, AI fires automatically.
- **Loading screen:** each member's avatar pulses. Lines of text appear and fade — reading the crew, finding the right night. Feels alive, not like a spinner. Estimated wait: 60–90 seconds.
- All bookings fully confirmed with confirmation numbers before reveal. Aventure pays all venues directly. Crew never handles money again after the waiting room.

### Phase 6 — Quest Reveal & In Progress

- All crew members see the quest at exactly the same time.
- The reveal is designed to feel like an event — a moment, not a results page.
- **Quest command centre** has 3 tabs:
  1. **Now** — current stop, venue, what to do, reservation details, confirmation number, one large Navigate button.
  2. **Full quest** — all stops in order, current highlighted, upcoming visible to build anticipation.
  3. **Crew chat** — accessible without leaving the quest screen.
- Between stops: navigation screen, travel time countdown, Google Maps integration. Used outdoors on someone's shared phone — must be simple and readable.
- **Restaurant stops (V1.1):** Quest Leader gets a Stripe virtual card loaded with exact dining budget. Declines anything over the amount. Unspent balance refunded after quest.

### Phase 7 — Post Quest

- **Photo dump** — each member uploads photos, all saved to the quest.
- **Memory & recap** — photos + caption + individual ratings, saved permanently to crew history.
- **Shareable quest card** (auto-generated) — quest name, crew name, 3 photos in a grid, date, subtle Aventure branding. Share to Instagram/TikTok or save to camera roll. This is the organic growth engine — like Strava's share card.
- **Budget settlement** — any unspent escrow refunded automatically via Stripe within 2–5 business days. Transparent breakdown.
- **Bucket lists** — personal (things I want to do) and crew (things we want to do together). AI references both when generating future quests.

### Additional screens

- **Invite link landing page** (mobile web, pre-download) — shows the crew, who's in it, one line of social proof. Detects iOS/Android. After download, deep links directly into crew join flow.
- **User profile** — name, photo, personality survey answers, quest history, personal bucket list, account settings.
- **Empty states** — every major screen needs one with a clear message and single CTA.

---

## Open questions (answered for reference, not active blockers)

- Crew minimum: 2, maximum: 20.
- Same-day quests: 8-hour minimum lead time.
- If a member leaves before paying: app asks remaining crew if they want to proceed.
- Compatibility view: percentage + shared interests listed.

---

## Workspace structure

```
aventure-design/
├── CLAUDE.md         ← this file — product brain
├── SCREENS.md        ← screen inventory & status tracker
├── README.md
├── .gitignore
├── design/
│   ├── tokens/       ← DESIGN.md, tokens.css, palette-preview.html (locked-in design system)
│   ├── references/   ← Mobbin screenshots and other inspiration
│   ├── screens/      ← one folder per screen (created as we go)
│   └── components/   ← reusable UI pieces
└── .claude/
    └── commands/     ← custom slash commands (none yet)
```

### Per-screen folder convention

Each screen under `design/screens/<screen-slug>/` will contain:

- `index.html` — HTML/CSS prototype (clickable, iOS-styled)
- `spec.md` — layout notes, components used, copy, states, edge cases
- `figma/` — Figma exports (PNG/SVG) when available

Slugs are kebab-case and match the names in `SCREENS.md` (e.g. `splash`, `welcome-panel-1`, `quest-command-centre`).

---

## Screen inventory

The full screen tracker lives in [`SCREENS.md`](SCREENS.md) — phase-by-phase tables with status, last updated, and notes. Update it whenever a screen's status changes.

---

## Design tokens, colors, typography

**Status:** Locked in (2026-06-06) — **"Golden Hour"** system. Supersedes the 2026-06-03 "Say Briefly" direction (Deep Olive / Highlight Yellow / Bricolage), which is retired. Warm golden-hour afternoon — Strava meets Airbnb Experiences. Light theme only, no dark mode. WCAG AA verified.

**Files** (in [`design/tokens/`](design/tokens/)):
- [`DESIGN.md`](design/tokens/DESIGN.md) — full spec: rationale, every token, do/don't rules, component guidance.
- [`tokens.css`](design/tokens/tokens.css) — CSS custom properties + starter components. **Every screen's `index.html` should `<link>` this**, then build on the variables — no ad-hoc colors/fonts.
- [`palette-preview.html`](design/tokens/palette-preview.html) — open in a browser to see swatches and an in-context mock.

**Cheat sheet:**

| Role | Value |
|---|---|
| Background | Warm Linen `#FBF6EE` (warm cream — never white/grey) |
| Card / surface | White `#FFFFFF` |
| Primary | Terracotta `#E2693E` (CTAs, buttons, active states) |
| Secondary | Jade `#138A6B` (nav bar, headers, brand accents) |
| Success | `#3D8060` (confirmed states, paid avatars, positive badges) |
| Ink (body + CTA text) | `#2A2521` |
| Muted | `#7A6E68` (secondary labels, timestamps) |
| Divider | `#ECE4D8` (card borders, separators) |
| Display font | Fraunces (variable) 500/600/700 |
| Body / UI font | Satoshi (Fontshare, variable) 400/500/700 |
| Radius | 14px buttons · 16px cards · 12px inputs · 100px pills |
| Density | Comfortable — flat-first, minimal shadows. |

**Critical color rules:** Primary CTA = terracotta bg + **ink** text (NEVER white on terracotta — fails AA). Nav/header = jade bg + white. Success badges/avatar rings = `#3D8060` + white.

**Do not use:** dark section backgrounds, cold tones, or purple. The retired "Say Briefly" tokens (Deep Olive `#1a3300`, Highlight Yellow `#ffe95c`, Bricolage Grotesque, Inter) should not be reintroduced.

If a screen prototype needs a token that doesn't exist yet, add it to `tokens.css` (don't hardcode) and note it in the screen's `spec.md`.

---

## GBrain Configuration (configured by /setup-gbrain)
- Mode: local-stdio
- Engine: pglite
- Config file: `~/.gbrain/config.json` (Windows: `C:\Users\rizsa\.gbrain\config.json`)
- Brain DB: `C:\Users\rizsa\.gbrain\brain.pglite`
- Setup date: 2026-06-23 (Windows machine)
- MCP registered: yes (user scope, `C:\Users\rizsa\.bun\bin\gbrain.exe serve`) — restart Claude Code to load `mcp__gbrain__*` tools
- Embeddings: deferred (`embedding_disabled: true`). Semantic `gbrain search`/`query` is OFF until a key is set: `gbrain config set embedding_model <id>` (e.g. `voyage:voyage-code-3` with `VOYAGE_API_KEY`). Lexical put/search works today.
- Repo import: not yet done. Needs `jq` on PATH (gstack repo-policy helper) and is best run after embeddings are configured, then: `gbrain import . --no-embed`.
- Artifacts sync: off

## GBrain Search Guidance
<!-- gstack-gbrain-search-guidance:start -->
gbrain is set up locally but this repo is **not yet imported** and **embeddings are off**, so semantic/code search is not available yet. Until then, use Grep/Glob for code and docs in this repo. You can still `gbrain put`/`gbrain search` (lexical) for notes you explicitly store. Re-run `/setup-gbrain` or `/sync-gbrain` after setting an embedding key and importing the repo to unlock `gbrain search`/`query`/`code-def`/`code-refs`.
<!-- gstack-gbrain-search-guidance:end -->
