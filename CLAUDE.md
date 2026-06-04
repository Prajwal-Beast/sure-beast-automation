# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

**Beast Automation** — AI automation agency website for Prajwal Bista.
- **Live URL:** https://sure-beast-automation.vercel.app
- **Stack:** Single-file HTML/CSS/JS — no build step, no framework, no npm

## Deployment

The site deploys automatically via Vercel on every push to `master`.

```bash
git add index.html
git commit -m "your message"
git push origin master
```

Vercel reads `vercel.json` (implicit — no config file needed). The `.vercelignore` excludes all large media files except `prajwal.jpg`.

There is **no local dev server configured**. Open `index.html` directly in a browser, or use any static server:

```bash
npx serve . -p 3000
```

## Architecture — single `index.html`

Everything lives in one file, in this order:

1. **`<head>`** — Google Fonts, Three.js CDN, Ahrefs analytics, all inline `<style>`
2. **CSS** — variables/tokens → utilities → components → sections → responsive
3. **HTML body** — cursor elements → background layers → nav → sections → footer
4. **`<script>`** — all JS inline at bottom, in this order:
   - Custom cursor (dot + ring + spotlight)
   - Magnetic buttons
   - 3D card tilt (desktop only, skipped on `hover:none`)
   - Three.js hero particle sphere
   - Nav scroll handler
   - Mobile nav toggle
   - Scroll reveal (IntersectionObserver)
   - Counter animation
   - Floating background particles
   - Parallax orbs on scroll
   - Interactive star field canvas
5. **External scripts** — Calendly widget, ElevenLabs voice widget

## Key design tokens (CSS variables)

```css
--bg-primary:  #030812   /* deepest background */
--bg-secondary:#060D1A   /* alternate sections */
--bg-card:     rgba(255,255,255,0.035)
--teal:        #00E0FF   /* primary accent */
--purple:      #A855F7   /* secondary accent */
--pink:        #F472B6
--text-1:      #EEF4FF   /* headings */
--text-2:      #7A90AA   /* body copy */
--text-3:      #3D5268   /* captions, placeholders */
```

## Interactive 3D elements

- **Star field** — `<canvas id="star-canvas">` fixed behind everything (z-index:0). Adaptive: 260 stars desktop, 80 mobile. Cursor repulsion disabled on touch.
- **Three.js hero** — `<canvas id="hero-canvas">` inside `.canvas-wrap`. Particle count adaptive: 900 desktop → 380 tablet → 220 phone. Pixel ratio capped at 1.5 on mobile.
- **3D card tilt** — applied via `.tilt-card` class, JS-driven, disabled on `hover:none` (touch) devices.
- **Magnetic buttons** — `.magnetic` class, also disabled on touch.

## Sections & IDs

`#hero` → `#about` → `#services` → `#portfolio` → `#projects` → `#process` → `#contact`

The **Projects section** (`#projects`) lists 7 live clickable project cards + 1 "Coming Soon" card (DalBhat Fit).

## Responsive breakpoints

| Breakpoint | Target |
|---|---|
| 1280px | Large laptop |
| 1024px | Laptop / iPad landscape |
| 900px | iPad landscape / small laptop |
| 768px | iPad portrait |
| 640px | Large phone |
| 480px | Medium phone |
| 380px | Small phone |

## Assets

| File | Purpose |
|---|---|
| `prajwal.jpg` | Founder photo used in About section |
| `brand/logo-horizontal.png` | Nav + footer logo (horizontal transparent lockup) |
| `brand/logo-mark.png` | Mark-only version |
| `brand/logo-profile.png` | Profile picture version |

## What NOT to include in commits

The `.vercelignore` intentionally excludes: `*.csv`, `*.mov`, `*.pdf`, `*.docx` — these are personal files sitting in the folder and must never be deployed.
