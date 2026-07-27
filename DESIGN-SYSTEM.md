# Aventure — "Golden Hour" Design System

> **Status:** Locked 2026-06-06 · jade secondary updated 2026-06-09.
> Light theme only. WCAG AA verified. Supersedes the retired "Say Briefly" direction.
> Source of truth: [`design/tokens/tokens.css`](design/tokens/tokens.css). This file is the readable reference.

---

## 1. Colour palette

| Token | Hex | Role |
|---|---|---|
| **bg** | `#FBF6EE` | App background — warm linen |
| **card** | `#FFFFFF` | Cards, panels, elevated surfaces |
| **primary** | `#E2693E` | CTAs, buttons, active states (terracotta) |
| **secondary** | `#138A6B` | Nav bar, headers, brand accents (**jade**) |
| **success** | `#3D8060` | Confirmed states, paid avatars, positive badges |
| **ink** | `#2A2521` | ALL body text **and** CTA button text |
| **muted** | `#7A6E68` | Secondary labels, timestamps, metadata |
| **divider** | `#ECE4D8` | Card borders, separators (decorative) |

### Critical colour rules
- **Primary CTA** = terracotta `#E2693E` background + **ink `#2A2521`** text. **Never white on terracotta** (fails WCAG AA).
- **Nav / header** = jade `#138A6B` background + white text/icons.
- **Success badges & active-quest avatar rings** = `#3D8060` background + white.
- **Avatar status rings:** active quest → primary `#E2693E`; no active quest → divider `#ECE4D8`; paid member → success `#3D8060`.
- Dividers are decorative — no contrast requirement.

### Contrast reference (against white text unless noted)
- Ink on terracotta `#E2693E` ≈ 4.7:1 ✅
- White on jade `#138A6B` ≈ 4.3:1 ✅ (nav text is large/bold)
- White on success `#3D8060` ≈ 4.5:1 ✅

---

## 2. Typography

- **Display / headlines / quest titles / crew names:** **Fraunces** (Google Fonts, variable) — weights 500 / 600 / 700
- **Body / UI / labels / buttons / numbers:** **Satoshi** (Fontshare, variable) — weights 400 / 500 / 700

| Role | Size | Font / weight | Colour |
|---|---|---|---|
| Display | 32–40px | Fraunces 700 | ink |
| Section headline | 22–28px | Fraunces 600 | ink |
| Crew name | 16–17px | Fraunces 600 | ink |
| Body | 16px | Satoshi 400 | ink |
| Secondary | 14px | Satoshi 400 | muted |
| Button | 15px | Satoshi 500 | ink |
| Caption / timestamp | 12px | Satoshi 400 | muted |
| Label | 11px | Satoshi 500, tracking 0.07em, UPPERCASE | muted |

Line-height ≈ 1.3 throughout.

### Font setup
- **Fraunces** — built into Figma (Google Fonts); no install needed.
- **Satoshi** — install from https://www.fontshare.com/fonts/satoshi → "Download Family", install the OTF/TTF for all users, then restart the **Figma desktop app** (custom fonts need the desktop app or Figma Font Helper).

---

## 3. Components

| Component | Spec |
|---|---|
| **Primary button** | full-width, height 52, radius 14, bg `#E2693E`, text `#2A2521`, Satoshi 500 / 15 |
| **Secondary button** | bg `#138A6B`, text white, same sizing |
| **Ghost button** | transparent, 1px `#ECE4D8` border, text ink |
| **FAB** | 56px circle, bg `#E2693E`, ink icon |
| **Card** | bg white, 0.5px `#ECE4D8` border, radius 16, padding 16–20 |
| **Input** | bg white, 1px `#ECE4D8` border, radius 12, height 50 |
| **Pill / tag** | bg `#ECE4D8`, text ink, radius 100, padding 5×12 |
| **Success badge** | bg `#3D8060`, text white, radius 100 |
| **Status pill** | active → success bg + white · waiting → primary bg + ink · none → divider bg + muted |
| **Avatar** | 32–36px circle, 2px surface border, overlap −9/−10px, max 5 visible + `+N` chip; status ring per rules above |
| **Tab bar** | bg white, border-top 0.5px `#ECE4D8`; active = icon + label jade `#138A6B`; inactive = muted `#7A6E68` |

---

## 4. Spacing, radius & shape

| | Value |
|---|---|
| Radius — button | 14px |
| Radius — card | 16px |
| Radius — input | 12px |
| Radius — pill | 100px |
| Gap — element | 12px |
| Gap — card padding | 18px (16–20 range) |
| Gap — section | 24px |
| Density | Comfortable — flat-first, minimal shadows |

---

## 5. Device frame

- Screen: **390 × 844** (iPhone 14 / standard iOS viewport)
- Safe area top (status bar): **59px** · Safe area bottom (home indicator): **34px**
- **Thumb zone:** all primary interactive elements fall between y = 400 and y = 780

---

## 6. Brand

- **Name:** Aventure · **Domain:** aventure.world
- **Tagline:** "Your crew. Your quest. Your world."
- **Aesthetic:** warm golden-hour afternoon with friends. Strava × Airbnb Experiences. Tactile, real, alive, human — not corporate, not AI-generic, not cold.
- **Audience:** Gen Z (16–24), Greater Toronto Area. iOS first, Android second.

---

## 7. Do / Don't

**Do**
- Reserve terracotta `#E2693E` for the primary action ("Start a quest") and active states only.
- Keep all body and CTA text in ink `#2A2521`.
- Use jade `#138A6B` for nav/header chrome with white content.
- Let avatar rings + status pills carry crew status so the screen feels alive without noise.

**Don't**
- White text on terracotta (fails AA).
- Dark section backgrounds, cold tones, or purple.
- Reintroduce the retired "Say Briefly" tokens (Deep Olive `#1a3300`, Highlight Yellow `#ffe95c`, Bricolage Grotesque, Inter).
- Add Soft Teal `#a8e5e5` or Pale Pink `#f6d0ff` — intentionally off-brief.
