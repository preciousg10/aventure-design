# aventure-design

![Design System](https://img.shields.io/badge/Design%20System-Golden%20Hour-E2693E)
![HTML](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)
![Figma](https://img.shields.io/badge/Figma-F24E1E?logo=figma&logoColor=white)

> The design workspace for Aventure, an AI-powered group experience app for Gen Z. Design system, screen mockups, and the single source of truth for the product's look and feel.

This repo holds the design work behind [Aventure](https://github.com/preciousg10/aventure): the locked-in "Golden Hour" design system, HTML screen prototypes, and a screen-by-screen tracker. It is a public showcase of my design-system and UI work on a team project.

## Table of Contents

- [What's Inside](#whats-inside)
- [Design System](#design-system)
- [Structure](#structure)
- [Viewing the Mockups](#viewing-the-mockups)

## What's Inside

- **Product brain:** [`CLAUDE.md`](CLAUDE.md) holds the full product context and user flow.
- **Screen tracker:** [`SCREENS.md`](SCREENS.md) tracks the status of every screen, phase by phase.
- **Design system:** `design/tokens/` holds the Golden Hour tokens, CSS variables, and a palette preview.
- **Mockups:** `design/screens/<slug>/` holds an HTML prototype plus Figma exports per screen.
- **Inspiration:** `design/references/` holds curated Mobbin screenshots and references.

## Design System

"Golden Hour" is a warm, golden-hour palette (Strava meets Airbnb Experiences), light theme only, verified to WCAG AA.

| Role | Value |
|------|-------|
| Background | Warm Linen `#FBF6EE` |
| Card / surface | White `#FFFFFF` |
| Primary | Terracotta `#E2693E` |
| Secondary | Jade `#138A6B` |
| Display font | Fraunces |
| Body font | Satoshi |

The full spec lives in `design/tokens/DESIGN.md`.

## Structure

```
aventure-design/
  CLAUDE.md          # product brain: context and full user flow
  SCREENS.md         # screen inventory and status tracker
  design/
    tokens/          # Golden Hour design system (DESIGN.md, tokens.css, palette-preview.html)
    references/      # inspiration
    screens/         # one folder per screen (HTML prototype + Figma exports)
    components/      # reusable UI pieces
```

## Viewing the Mockups

Open any screen's `index.html` in a browser, or open `design/tokens/palette-preview.html` to see the full palette and components in context.
