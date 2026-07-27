# Aventure — Design Tokens & Direction

> ⚠️ **RETIRED (2026-06-06).** This document describes the original *Say Briefly* direction
> (Deep Olive / Highlight Yellow / Bricolage + Inter). The project moved to the **"Golden Hour"**
> system on 2026-06-06 — see [`tokens.css`](tokens.css) and the cheat sheet in [`../../CLAUDE.md`](../../CLAUDE.md).
> Kept for history only; do not apply the values below. Golden Hour = linen `#FBF6EE`, terracotta
> `#E2693E`, forest `#2D6A4F`, success `#3D8060`, ink `#2A2521`, fonts Fraunces + Satoshi.

> **Source (retired):** Refero style match — *Say Briefly* ("Olive Canvas, Highlighted Briefs, Warm Accents")
> Refero style ID: `2dab5b15-55c1-4835-8d8b-0d42f67604bc` · https://saybriefly.com
> **Theme:** light only (no dark mode) · **Mood:** warm, editorial, confident, inviting
>
> Selected as the closest match to Aventure's brief: a cream/off-white canvas with a deep
> forest-green *primary* brand color, warm and minimal with personality — a boutique travel /
> premium outdoor-lifestyle feel for a Gen-Z audience that is confident, not loud.
>
> **Aventure adaptation:** the source's Soft Teal and Pale Pink accents are dropped to honor
> Aventure's "no cold tones / no purple" rule (approved 2026-06-03).

---

## Color tokens

### Core (use everywhere)

| Name | Value | Token | Role |
|------|-------|-------|------|
| Canvas White | `#fcfaf5` | `--color-canvas-white` | Page background, primary surface. Warm cream — never pure white, never grey. |
| Deep Olive | `#1a3300` | `--color-deep-olive` | **Primary brand color.** Primary text, major headings, borders, main CTA buttons. Defines the identity. |
| Highlight Yellow | `#ffe95c` | `--color-highlight-yellow` | Highlighting key words, card backgrounds, and button text on Deep Olive backgrounds. |
| Charcoal Black | `#000000` | `--color-charcoal-black` | Secondary/body text, fine print. |

### Neutrals

| Name | Value | Token | Role |
|------|-------|-------|------|
| Light Gray | `#f1f1f1` | `--color-light-gray` | Minor text, subtle borders, faint background accents. |
| Border Gray | `#b6b6b6` | `--color-border-gray` | Hairline borders, dividers, subtle UI outlines. |

### Warm accents (optional, on-brief)

| Name | Value | Token | Role |
|------|-------|-------|------|
| Warm Orange | `#cb5521` | `--color-warm-orange` | Terracotta/burnt-orange card & section backgrounds. Use sparingly. |
| Muted Sage | `#d5f5c2` | `--color-muted-sage` | Soft pale sage-green for button backgrounds and subtle surfaces. |

### Dropped from source (do NOT use)

| Name | Value | Reason |
|------|-------|--------|
| Soft Teal | `#a8e5e5` | Cold tone — conflicts with "no cold tones". |
| Pale Pink | `#f6d0ff` | Reads cool/purple — conflicts with "no purple". |

---

## Typography

| Font | Token | Role | Weights | Substitute |
|------|-------|------|---------|------------|
| **Bricolage Grotesque** | `--font-bricolage-grotesque` | Hero headlines & major titles. Heavy weight + generous letter-spacing = impactful editorial presence with character. | 800 | system-ui |
| **Inter** | `--font-inter` | All body text, navigation, most UI. Handles full hierarchy. | 300–700 | Arial |
| Roboto Mono | `--font-roboto-mono` | Functional/data display only. Optional. | 400 | monospace |

**Display headline rule:** Bricolage Grotesque, weight 800, sizes 55–90px, letter-spacing `0.04em–0.05em`.

### Type scale

| Role | Size | Line height | Token |
|------|------|-------------|-------|
| caption | 11px | 1.3 | `--text-caption` |
| body-sm | 14px | 1.3 | `--text-body-sm` |
| body | 17px | 1.3 | `--text-body` |
| body-lg | 18px | 1.3 | `--text-body-lg` |
| heading-sm | 24px | 1.3 | `--text-heading-sm` |
| heading | 30px | 1.3 | `--text-heading` |
| heading-lg | 36px | 1.3 | `--text-heading-lg` |
| display-sm | 38px | 1.3 | `--text-display-sm` |
| display | 64px | 1.3 | `--text-display` |

---

## Spacing & shape

**Density:** comfortable.

| Token | Value |
|-------|-------|
| Section gap | 40px (minimum) |
| Card padding | 16px |
| Element gap | 16px |
| Page max width | 1320px (web); mobile = full-bleed with comfortable margins |

### Border radius

| Element | Value |
|---------|-------|
| cards | 6px |
| buttons | 6px |
| navItems | 16px |
| highlighted / pill elements | 9999px |

### Shadows (flat-first — use minimally)

| Name | Value | Token |
|------|-------|-------|
| Button | `rgba(0,0,0,0.05) 0px 1px 2px 0px` | `--shadow-button` |
| Card / secondary | `rgba(0,0,0,0.1) 0px 1px 3px 0px, rgba(0,0,0,0.1) 0px 1px 2px -1px` | `--shadow-card-secondary` |

---

## Surfaces

| Level | Name | Value | Purpose |
|-------|------|-------|---------|
| 0 | Canvas White | `#fcfaf5` | Primary page background. |
| 1 | Muted Sage | `#d5f5c2` | Subtle background for specific sections / button groups. |
| 2 | Highlight Yellow | `#ffe95c` | Prominent content blocks; functional cards. |

---

## Components

### Primary CTA button
Deep Olive bg (`#1a3300`), Highlight Yellow text (`#ffe95c`), 6px radius (or 9999px pill),
12px vertical / 40px horizontal padding, subtle button shadow.

### Secondary outlined button
Transparent bg, Deep Olive text, 2px Deep Olive border, 6px radius, 12px / ~19px padding.

### Highlight card
Highlight Yellow bg (`#ffe95c`), 6–16px radius, generous padding, no shadow.

### Navigation
Fixed top bar, simple Inter text links in Deep Olive, prominent right-aligned action button.
Nav container uses Border Gray (`#b6b6b6`) outline with 16px radius.

### Subtle accent badge
Transparent bg, Deep Olive text, 8px radius; Highlight Yellow bg when emphasized.

---

## Do / Don't

### Do
- Use Deep Olive (`#1a3300`) for primary text and main CTAs — it carries the brand.
- Keep the page on Canvas White (`#fcfaf5`); reserve color for cards, highlights, and accents.
- Use Bricolage Grotesque 800 for display headlines (0.04–0.05em letter-spacing); Inter for everything else.
- Stick to the radius set: 6px (buttons/cards), 16px (nav/sections), 9999px (pills).
- Stay flat — minimal shadows; let color contrast do the work.
- Use Highlight Yellow to emphasize a single key word in a headline.

### Don't
- Don't use dark backgrounds for whole page sections — the theme is light throughout.
- Don't introduce heavy shadows, gradients, or cold/purple accents.
- Don't swap the font roles or add competing display faces.
- Don't use arbitrary radii or saturated colors across large background areas.

---

## Imagery

Minimal and functional. Clean line-drawn illustrations or subtle brand-color background patterns;
clean, focused product/photography. Filled icons in Deep Olive on light backgrounds. Text-dominant
layouts — imagery supports, never overwhelms.

---

## Adaptation notes for Aventure

1. **Olive = forest green:** Deep Olive (`#1a3300`) reads as a deep, grounded forest green and
   satisfies the "deep forest green primary" requirement. Approved as-is on 2026-06-03.
2. **Accent system:** Highlight Yellow (primary accent) + Warm Orange / Muted Sage (warm
   secondaries). Soft Teal and Pale Pink removed.
3. **Mobile-first:** source is a web page (1320px max). For Aventure's mobile app, keep the same
   tokens but use full-bleed layouts with comfortable margins; preserve comfortable density.
4. **No dark mode:** confirmed light-only.
