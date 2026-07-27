# Screen 10 — Crew Hub

The primary home screen for returning users. Lands here every app open after onboarding.
Two states: **populated** (user has crews) and **empty** (no crews yet).

> **Design system:** "Golden Hour" (locked 2026-06-06). See [`/design/tokens/tokens.css`](../../tokens/tokens.css).
> All colors/fonts come from tokens — no ad-hoc values.

---

## Files

| File | What it is |
|---|---|
| `option-a-card-feed.html` | **Option A** — full-width crew cards in a scrollable feed + sticky CTA |
| `option-b-dashboard.html` | **Option B** — one hero status card + compact secondary rows + floating FAB |
| `option-c-minimal.html` | **Option C** — greeting-led, dividerless rows + fixed CTA |
| `empty-state.html` | No-crews state (also tracked as `empty-crew-hub` in SCREENS.md) |

All four render a pixel-accurate **390 × 844** iPhone 14 frame: 59px status bar, 34px home indicator, content actions inside the y≈400–780 thumb zone.

---

## Refero research → decisions (Step 1 summary)

- **UGLYCASH "Communities" hub** → Option B: warm color header over white cards, one featured story + a scannable list, translucent floating control.
- **Strava style** → discipline: a single saturated accent used *only* for the primary action; high-contrast neutral text; warmth from people, not chrome. → terracotta reserved for "Start a quest" everywhere.
- **Telegram / XChat group pages + Gizmo feed** → crew-card anatomy: overlapping avatar stack (cap ~5 + `+N`), status as both a colored pill and a status line; large rounded action on hero/active items only.
- **Empty-state patterns** (Apple Games, Mela, Wabi) → centered soft illustration + one headline + one subline + one primary action (+ optional ghost). Warm beats clinical.
- **Key insight:** the best apps create a single focal "story," then make the next action obvious; generic apps show a flat equal-weight list.

---

## The three options (Step 2)

| | A — Card Feed | B — Dashboard | C — Minimal Crew List |
|---|---|---|---|
| Information architecture | Equal-weight scrollable feed of full cards | One hero + compact list | Greeting + dividerless rows, no cards |
| Hero / focal point | The cards (Strava feed) | Most-active crew / live quest | Greeting + whitespace (iOS Contacts) |
| Status display | Big pills + prominent avatar rings | Hero: full quest progress; others mini | Single colored status dot per row |
| "Start a quest" placement | Sticky CTA above tab bar **+** inline on idle crews | Floating 56px terracotta FAB, bottom-right | Fixed full-width CTA above tab bar |
| Density | Comfortable, momentum-building | Hierarchical, one story at a time | Airy, fast to scan |
| Best when | Several active crews | One clear priority | Many crews, calm scanning |

**Recommendation:** **Option B (Dashboard)** for v1 — it best satisfies "communicate crew status at a glance" and makes "Start a quest" inevitable via the FAB, while the hero makes a live quest feel alive. Option A is the strong alternate if crews are usually multi-active. Option C is the fallback for power users with many crews.

---

## Component anatomy (shared)

- **Top nav bar** — bg `--secondary` (#138A6B, jade). Left: `aventure` wordmark, Fraunces 600, #FFF. Right: bell, #FFF 22px, terracotta unread dot. Status bar shares the green, white glyphs.
- **Greeting** — time-aware ("Good evening, {name}." / "Ready for a quest, {name}?"), Fraunces 600 22–30px ink + Satoshi 14 muted subtext (crew count / what needs you).
- **Crew card / row**
  - Crew name: Fraunces 600, 16–17px, ink.
  - Avatar row: 32–36px circles, 2px surface border, overlap −9/−10px, max 5 + `+N`. **Ring codes status:** active quest → `--primary` ring; no active quest → `--divider` ring; paid members render `--success` with a check.
  - Quest status pill: `Quest active` (success bg, #FFF) · `Waiting for crew` (primary bg, ink) · `No quest yet` (divider bg, muted). Option C compresses this to a colored status dot.
  - Last-activity line: Satoshi 12px muted.
  - Chevron: muted 16px; whole card/row tappable.
- **Primary CTA** — "Start a quest", 52px, radius 14, bg `--primary`, text ink (never white — fails AA), spark icon. Sticky (A/C) or FAB (B). Inline contextual variant (44px) appears only on **idle** crews in A.
- **Tab bar** — 4 tabs, bg #FFF, border-top 0.5px divider. Active (Home) = icon + label in `--secondary`; others muted. Heart=Memories, compass=Explore, person=Profile.

---

## Copy

- Greeting: "Good evening, Zaydaan." / "Ready for a quest, Zaydaan?"
- Subtext: "You're in 3 crews · 1 quest live right now" / "1 is waiting on you"
- Pills: "Quest active" · "Waiting for crew" · "No quest yet"
- CTA: "Start a quest"
- Empty: H "You're not in a crew yet." · B "Create one or join your friends to start your first quest." · Buttons "Create a crew" / "Join a crew"

## States & edge cases

- **1 crew:** A/C collapse gracefully; B promotes that crew to hero, hides "Your other crews" label.
- **No active quests:** B hero falls back to the most-recently-active crew with a "Start a quest" hero CTA instead of "Open quest".
- **Many crews (6+):** prefer C (rows scroll fastest) or A with virtualized feed.
- **Unpaid waiting room you're part of:** surface "waiting on you" in the greeting subtext (C demonstrates this).
- **Empty state:** primary = Create, ghost = Join; no tab-bar disable (user can still browse).

## Accessibility

- CTA contrast: ink #2A2521 on terracotta #E2693E ≈ 4.7:1 (passes AA). White on terracotta is **banned**.
- Nav: white on jade #138A6B ≈ 4.3:1 (passes AA — nav text is large/bold: wordmark, time, icons). Success badge white on #3D8060 ≈ 4.5:1.
- Avatar ring is a redundant cue — every status also has text (pill/line/dot), so it's not color-only.
- All actions sit in the thumb zone (y 400–780).

---

## STEP 4 — Figma export guidance

Recreate the chosen option natively in Figma (don't paste screenshots — build real layers so it's editable and componentized).

### 1. File + page setup
- Frame: **iPhone 14 — 390 × 844**. Name it `Screen 10 / Crew Hub / Option {A|B|C}`.
- Layout grid: 4-col, 20px margins, 16px gutter (Option C uses 24px margins).
- Create a second frame `… / Empty` for the no-crews state.

### 2. Color & text styles (build once, reuse everywhere)
Create **color styles** mirroring the tokens exactly:
`bg #FBF6EE · card #FFFFFF · primary #E2693E · secondary #2D6A4F · success #3D8060 · ink #2A2521 · muted #7A6E68 · divider #ECE4D8`.
Create **text styles** (Fraunces variable + Satoshi variable — install both; Satoshi from Fontshare):
- `Display/Fraunces 700 32` · `Section/Fraunces 600 22` · `CrewName/Fraunces 600 16`
- `Body/Satoshi 400 16` · `Secondary/Satoshi 400 14 muted` · `Button/Satoshi 500 15` · `Caption/Satoshi 400 12 muted`
- `Label/Satoshi 500 11, tracking 7%, uppercase, muted`

### 3. Components to build (with variants)
- **Avatar** — 32 & 36px sizes; `ring = active | idle | paid` variant (use an outer 2px stroke ring + 2px white inner border). Build an **Avatar Row** auto-layout with −9 spacing and a `+N` chip.
- **Status pill** — variants `active | waiting | none` (bg + text per spec). 
- **Crew card** (Option A/B) — auto-layout, 18px padding, 16px radius, 0.5px divider stroke; slots: name, pill, avatar row, last-activity, optional progress bar, optional inline CTA.
- **Crew row** (Option C) — auto-layout horizontal, 16px vertical padding, 1px top divider; status-dot variant.
- **Primary button** — 52px, radius 14, primary fill, ink label; `+ icon` boolean. **FAB** variant = 56px circle. **Ghost** & **Secondary** variants.
- **Tab bar** — 4 items, `active` variant per item (start with Home active).
- **Status bar** & **Home indicator** — make these shared components reused across all 42 screens.

### 4. Auto layout & constraints
- Body content = vertical auto-layout, `Fill` width, scrollable. Pin nav to top, pin CTA/FAB + tab bar to bottom (constraints: Left+Right, Bottom).
- Hero/cards `Fill` container width so they reflow at other device sizes.

### 5. Prototype wiring (optional but recommended)
- "Start a quest" → `quest-initiated`. Crew card tap → `crew-profile` / `quest-command-centre` (if active). Tab bar → Memories / Explore / Profile. Empty "Create a crew" → `create-a-crew`, "Join a crew" → `join-via-code`.

### 6. Export
- Export each frame at **2x PNG** into `design/screens/crew-hub/figma/` for the SCREENS.md preview, and keep the editable Figma file as source of truth.
- Quick path: these HTML files are 1:1 with the tokens — you can screenshot at 390×844 for an instant reference image while rebuilding layers natively.
