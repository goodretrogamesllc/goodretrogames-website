# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-page marketing/landing site for **Good Retro Games LLC** (Saline, MI). It is a
static site — no build step, no dependencies, no JavaScript. Just hand-written HTML and CSS
served as files.

The actual store is hosted elsewhere; this site links out to a Square store
(`goodgamesretro.com`) and an eBay storefront. It does not handle commerce itself.

## Files

- `index.html` — the landing page (header, hero, categories, about, footer).
- `returns.html` — Return & Exchange Policy page.
- `loyalty.html` — Customer Loyalty Program page.
- `contact.html` — Contact page (see email obfuscation note below).
- `style.css` — all styling, shared across every page.
- `CNAME` — custom domain for GitHub Pages (`goodretrogames.com`).

All pages share the same header and footer markup and the same `style.css`. The header
logo and nav on sub-pages link back to `index.html` (anchors use `index.html#about` etc.).
The footer link list is duplicated in each page — update all of them together. Policy/legal
and contact pages use the `.policy` / `.policy-inner` styles.

## Contact / email handling

To avoid spam-harvesting crawlers, the business email address is **never written as
plaintext or a `mailto:` link** in any HTML. All "Contact" / "Get in Touch" links point to
`contact.html`, where the address is stored reversed (`moc.liamg@...`) and reassembled by
JavaScript only when the visitor clicks "Show Email Address". If you need to change the
email, edit the reversed `encoded` string in the inline script at the bottom of
`contact.html` — do not reintroduce a plaintext `mailto:` anywhere.

## Deployment

Served via **GitHub Pages** from the `main` branch (the `CNAME` file sets the custom domain).
Pushing to `main` publishes the site — there is no CI, build, or test step. To preview
locally, open `index.html` in a browser or run a static server (e.g. `python -m http.server`)
from the repo root.

## Styling conventions

- The design is a **dark retro-arcade** theme. All colors, fonts, radius, and max-width are
  defined as CSS custom properties in the `:root` block at the top of `style.css` — change
  the palette or layout width there rather than hard-coding values in individual rules.
- Two fonts, both loaded from Google Fonts in `index.html`: **Press Start 2P** (`--font-pixel`,
  used for the logo, headings, and eyebrows) and **DM Sans** (`--font-body`, used for prose
  and buttons).
- Buttons share a base `.btn` class with `.btn-primary` / `.btn-secondary` / `.btn-outline`
  variants. Reuse these rather than introducing new button styles.
- The CSS is organized top-to-bottom in section-comment blocks matching the page sections
  (HEADER, HERO, BUTTONS, CATEGORIES, ABOUT, FOOTER, RESPONSIVE). Keep new rules in the
  matching section.
- Responsive behavior lives in a single `@media (max-width: 768px)` block at the bottom that
  hides decorative elements (cartridge, pixel grid) and collapses the about grid on mobile.
