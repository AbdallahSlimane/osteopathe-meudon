# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Static marketing site (site vitrine) for Aurélie Diméglio, ostéopathe D.O. in Meudon (France). All content is in French. **No build step, no dependencies, no package manager, no framework.** Just hand-written HTML files served as-is.

## Commands

- **Preview locally**: open any `.html` directly in a browser, or `python3 -m http.server` then visit http://localhost:8000
- **Deploy**: pushing to the connected GitHub repo triggers Render (static site, publish dir `.`, empty build command — see `render.yaml`). There is nothing to compile.

## Architecture

Each page is a **fully self-contained HTML document** — there are no shared CSS/JS files. This is the single most important thing to understand before editing:

- Every page carries its **own `<style>` block** in `<head>` and its **own `<script>` block** before `</body>`.
- **Images live in `images/` as WebP files** and are referenced with relative paths (`src="images/xxx.webp"`). They were previously inlined as base64 data URIs; that was removed in September 2026, which cut the HTML from 2.04 MB to 243 KB (plus 512 KB of images, now cacheable). Never re-inline images. Every `<img>` carries explicit `width`/`height`, and images below the fold use `loading="lazy" decoding="async"`.
- **Deploying requires committing `images/` alongside the HTML.** Relative paths resolve under `file://` too, so opening a `.html` directly still works as long as `images/` sits next to it — but never move a page without its folder.
- **Beware the responsive safety rule** `img:not([style*="height"]):not([class]) { height: auto; }` at the top of each `<style>`: its specificity (0,2,1) beats component rules like `.hero-avatar img` (0,1,1). Any `<img>` whose container sizes it must carry its own inline `height`, as every photo on the site does.
- The **nav, footer, and menu JS are duplicated across pages**. A change to shared chrome (nav links, dropdown behavior, footer, contact info, phone number, Doctolib link) must be applied to **every** page, not just one. The pages are: `index.html`, `apropos.html`, `cycle.html`, `femme-enceinte.html`, `nourrisson.html`, `machoire.html`, `endometriose.html`, `politique-cookies.html`.

### Conventions to preserve

- **CSS design tokens** live in `:root` (e.g. `--sage`, `--blue`, `--white`, `--ink`, `--muted`, `--r` radius, `--sh` shadow). Reuse these variables rather than hard-coding colors.
- **Fonts** are Cormorant Garamond + DM Sans, loaded from Google Fonts via `<link>` (with `preconnect`). Keep the same font links when adding pages.
- **Vanilla JS only**: burger menu (`#burger` / `#navLinks` `.open`), a click-to-open "Spécialités" dropdown (`.has-drop` / `.drop-toggle` / `.dropdown`) present on **every** page, and on `index.html` a reviews carousel (`#carrTrack` / `#carrDots`, responsive `visibleCount()`). No libraries. The flat nav does not fit more than ~6 top-level items above the 1024px burger breakpoint — new pages go in the dropdown, not in the top-level list.
- **SEO/structured data**: `index.html` contains a `schema.org` `MedicalBusiness` JSON-LD block with the business address, phone, hours, and geo. Keep it in sync with any contact-info change elsewhere on the site.
- `lang="fr"` and French copy throughout — write new content in French.

When creating a new specialty page, copy an existing specialty page (e.g. `machoire.html` or `cycle.html`) as the template so the nav, footer, fonts, and JS stay consistent, then add a link to it in the "Spécialités" dropdown on every page.

## Positioning (since September 2026)

The practice is positioned as **santé de la femme & périnatalité**. The homepage splits "Pour qui ?" into a primary grid (Règles & cycle, Femmes enceintes, Post-partum & nourrisson, Endométriose, Drainage lymphatique) and a visually de-emphasised `.profiles-grid.secondary` block (Douleurs nerveuses, Mâchoire, Vie de bureau, TMS). Keep that hierarchy when adding cards — new women's-health motifs go in the primary grid, everything else in the secondary one.
