# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

**Client:** Bartenders in Frontera — NYC premium mobile bartending & cocktail services  
**Live URL:** bartendersinfronteria.nyctailblazers.com  
**GitHub:** github.com/Kaoz625/bartendersinfronteria  
**Deployed via:** Cloudflare Pages (auto-deploy from `main` branch)

## Contact Info (never commit to public-facing code)
- Phone: 646-220-5276
- Email: Bartendersinfrontera@gmail.com
- Social: @bartendersinfrontera (IG), @bartendersinfronterany (TikTok/YT)

## Architecture

Single-file static site — `index.html` contains all HTML, CSS, and JS. No build process.

- **Fonts:** Google Fonts — Playfair Display (headings, serif) + Inter (body)
- **Animation:** GSAP 3 + ScrollTrigger (CDN), plus native IntersectionObserver for scroll reveals
- **Particles:** Custom canvas-based floating particle system (inline JS)
- **Deployment:** Push to `main` → Cloudflare Pages auto-deploys. No build command needed.

## Design System

CSS custom properties defined in `:root`:
```
--gold: #c8972e        (primary accent — cocktail amber)
--gold-light: #e8b84b  (hover states)
--amber: #e85d3a       (secondary accent — fire orange)
--black: #07070a       (page background)
--dark: #0d0d12        (section backgrounds)
--surface: #13131a     (cards, form)
--text: #f0ede8        (body copy)
--muted: #7a7570       (subdued text)
--border: rgba(200,151,46,0.15)  (borders)
```

Headings always use `font-family: 'Playfair Display', serif`. Italic `<em>` inside headings gets the gold gradient treatment via `-webkit-background-clip: text`.

## Common Tasks

**Test locally:**
```bash
open ~/Sites/bartendersinfronteria/index.html
# or
python3 -m http.server 8080 --directory ~/Sites/bartendersinfronteria
```

**Deploy (push to trigger Cloudflare auto-deploy):**
```bash
cd ~/Sites/bartendersinfronteria
git add -A && git commit -m "update: description" && git push
```

**Add a new section:** Follow the pattern of existing sections — `<section id="x" class="section-pad">` wrapping `<div class="container">`. Add `.reveal` class to elements for scroll-in animation. Register the section in the nav.

## Key Patterns

- `.reveal` + IntersectionObserver: add class `visible` on scroll into view → triggers `revealUp` keyframe
- GSAP used only for hero entry animations (eyebrow, h1, subtitle, CTA, scroll indicator)
- Parallax: hero content translates on `window.scroll` with opacity fade
- Counter animation: `animateCounter()` in JS, triggered once by IntersectionObserver on `.about-stats`
- Form submit: builds a `mailto:` link with form data — no backend needed
- Marquee: pure CSS `animation: marqueeRoll` on duplicated items for seamless loop

## Cloudflare Pages Setup

- **Project name:** bartendersinfronteria  
- **Branch:** main  
- **Build command:** (none — static HTML)  
- **Output directory:** / (root)  
- **Custom domain:** bartendersinfronteria.nyctailblazers.com (CNAME to Cloudflare Pages)

## Monthly Maintenance

See `MONTHLY-PLAN.md` for the full service plan and cost breakdown.
