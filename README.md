# brain.md-website

The official site for [BRAIN.md](https://github.com/mindmuxai/brain.md), hosted at [projectbrain.md](https://projectbrain.md).

Plain static HTML/CSS — no build step, no framework, no `package.json`. Every page is hand-authored.

## Preview locally

```
npx serve -p 3456 .
```

Or just open `index.html` directly in a browser — there are no server-side includes.

## Structure

- `index.html` — the English homepage (single page, all sections inline).
- `zh/index.html` — the Chinese translation. It mirrors `index.html` section-for-section with the same ids/classes.
- `styles.css` — the single global stylesheet for both pages.
- `DESIGN.md` — the source-of-truth design token spec (Geist design system) that `styles.css` is derived from.
- `icon.svg` / `icon-static.svg` — the animated (SMIL) and static fallback brain logo/favicon.
- `robots.txt`, `sitemap.xml`, `og-image.png` — SEO/crawler assets.

## Contributing

Any structural or copy change to `index.html` must be manually ported to `zh/index.html` to keep the two pages in sync — there's no i18n tooling. See `CLAUDE.md` for full conventions (design tokens, accessibility patterns, section structure).

## License

Apache-2.0, see [LICENSE](LICENSE).
