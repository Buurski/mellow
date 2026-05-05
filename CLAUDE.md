# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Single-page HTML website for Restaurant Mellow, Lemvig DK.
- **Live:** https://mellow-gold.vercel.app
- **GitHub:** https://github.com/Buurski/mellow.git
- **Deploy:** push to `main` → Vercel auto-deploys via GitHub integration

## Development

No build step. Open `index.html` directly in a browser, or serve locally:

```bash
python -m http.server 8080
# then open http://localhost:8080
```

To deploy manually:
```bash
vercel deploy --prod
```

## Architecture

Everything lives in `index.html` — all CSS in `<style>`, all JS in `<script>`. No framework, no bundler.

**Asset layout:**
- `images/` — all photos and logos (`logobrown.png`, `logowhite.png`, `gallery1-4.jpg`, etc.)
- `video/herovideo.mp4` — hero background video
- `Mellow-A-la-Carte-og-vinkort.pdf` — menu PDF linked from the site
- `DESIGN-SYSTEM.md` — CSS token and component spec; treat as source of truth for variables, class names, and breakpoints

**CSS tokens (`:root`):** `--c-cream`, `--c-dark`, `--c-accent`, `--c-cta`, `--f-display` (Playfair Display), `--f-body` (Outfit), `--ease`. Never deviate from these.

**Key JS behaviours (all inline in `<script>`):**
- Nav: `is-loaded` on paint, `is-scrolled` after `scrollY > 60` → swaps logo brown→white via opacity crossfade
- Scroll-reveal: IntersectionObserver on `.reveal`, `.reveal-scale`, `.reveal-left` → adds `.is-in`
- Gallery: sticky horizontal scroll inside `#galleryTrack`. Track height = 300vh. `totalSlides = 7`, `visibleSlides = 3`, 5 scroll positions. Counter shows `position / 5`.
- Brunch parallax: scroll-linked `translateY` on brunch image
- Mobile burger: creates/removes fullscreen drawer DOM at ≤1040px

**Section order:** nav → hero (60/40 split, video left) → selskaber (dark bg) → info-strip → menu (à la carte) → gallery → quote → brunch → events → footer

## Client context

- **Natasja** (owner) — mail@restaurantmellow.dk. Priorities: selskaber section prominent, beige/warm-brown palette.
- **Ismael** — co-owner, contact via SMS.
- Demo (forside) approved. Next step: scope and pricing for remaining pages.

## Design rules

- Language: Danish primary
- No AI slop: no gradient blobs, no emoji icons, no filler content
- Selskaber must remain prominent — it is the client's top priority
- Palette is beige/warm-brown only; `--c-accent: #C9A96E` is the only gold
