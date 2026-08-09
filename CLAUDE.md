# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

The official site for BRAIN.md, hosted at projectbrain.md. It's plain static HTML/CSS with no build step, no framework, and no package.json — every page is hand-authored.

## Commands

There is no build, lint, or test tooling. To preview locally, serve the directory as static files:

```
npx serve -p 3456 .
```

(This matches the `.claude/launch.json` debug configuration.) Just opening `index.html` directly in a browser also works since there are no server-side includes.

## Structure

- `index.html` — the English homepage (single page, all sections inline).
- `zh/index.html` — the Chinese translation. It mirrors `index.html` section-for-section with the same ids/classes; **any structural or copy change to `index.html` must be manually ported here too** (there's no i18n tooling — see `hreflang`/`sitemap.xml` entries linking the two).
- `styles.css` — single global stylesheet for both pages, organized into clearly delimited `/* ── Section ── */` comment blocks (design tokens, reset, base, then one block per UI section in the order it appears on the page).
- `icon.svg` / `icon-static.svg` — the animated (SMIL) and static fallback versions of the brain logo/favicon.
- `DESIGN.md` — the source-of-truth design token spec (Geist design system: colors for light/dark themes, typography, spacing, radii, elevation, component tokens). The CSS custom properties at the top of `styles.css` are hand-derived from these tokens — when changing a color/spacing/type value, update both `DESIGN.md` and the corresponding CSS variable so they stay in sync.
- `robots.txt`, `sitemap.xml`, `og-image.png` — SEO/crawler assets referencing `https://projectbrain.md/`.

## Conventions

- No JS framework or build pipeline — keep changes as plain HTML/CSS. Inline `<script>` blocks are limited to: Google Analytics (gtag) and the JSON-LD structured data block in `<head>`, plus a dark-mode toggle and a hero terminal typewriter effect near the end of `<body>` (both vanilla JS, no dependencies). Keep these in sync between `index.html` and `zh/index.html`.
- Fonts (Geist Sans/Mono) load from `cdn.jsdelivr.net`; don't add a bundler dependency for them.
- CSS follows Geist's design language: dark/light theme colors are defined as CSS custom properties (light theme root, dark theme via a class/media toggle — see `/* ── Dark toggle ── */` in `styles.css`), a 4px spacing scale, and tight border radii (6/12/16px). Follow `DESIGN.md`'s Do's and Don'ts when adding new UI (use tokens instead of hand-picked values, keep WCAG AA contrast, don't mix rounded/sharp corners in one view).
- Section headings use `id`s referenced by `aria-labelledby` — preserve this pattern for accessibility when adding sections.
- Keep `index.html` and `zh/index.html` structurally identical (same section ids, same class names) so `styles.css` applies to both without page-specific overrides.
- When adding/removing a page or changing canonical URLs, update `sitemap.xml` and the `hreflang`/canonical `<link>` tags in both HTML files together.