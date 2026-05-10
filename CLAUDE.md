# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Jekyll static site for Christian Hatch's personal website. Deployed via GitHub Pages (custom domain set in `CNAME` — `dev.chatch.me`, with the production domain `chatch.me` configured in `_config.yml`). No JavaScript build step, no Node toolchain — Tailwind is loaded from the CDN in `_includes/head.html`.

## Commands

```bash
bundle install              # install Ruby gems (jekyll, jekyll-feed, jekyll-sitemap)
bundle exec jekyll serve    # local dev server with live-reload at http://localhost:4000
bundle exec jekyll build    # build static site into _site/
```

`_site/` and `.jekyll-cache/` are build artifacts (gitignored) — never edit by hand.

## Architecture

- **Pages are top-level `.html` files** with Jekyll front matter (`index.html`, `apps.html`, `contact.html`, `opensource.html`, `privacy.html`, etc.). Each declares `layout:` and optional `title`/`description`. There are no `_posts/` — this is not a blog.
- **`_layouts/default.html`** is the root template (loads `head.html`, `nav.html`, `footer.html`, renders `{{ content }}`). `home.html` and `page.html` both extend `default` — `page` wraps content in a `prose` container with an `<h1>`, `home` is bare.
- **`_includes/head.html`** configures Tailwind inline via `tailwind.config = { darkMode: 'media', theme: { extend: { colors: { accent: '#f75d59', 'accent-dark': '#BF4845' } } } }`. The `accent` color is the site's brand red — reuse it for new CTAs/links rather than introducing new colors. Dark mode is automatic via `prefers-color-scheme`, so every new component needs `dark:` variants.
- **`_includes/nav.html`** holds the nav links as a hard-coded pipe-delimited Liquid string: `"Home|/,Apps|/apps,..."`. To add/rename a nav item, edit that string in both the desktop and mobile blocks (they're duplicated).
- **`404.shtml`** uses the `.shtml` extension intentionally so GitHub Pages serves it as the 404 page — do not rename to `.html`.

## Conventions

- Tailwind utility classes only; there's no SCSS pipeline. `style.css` exists but is minimal.
- Every interactive/colored element has paired light + `dark:` classes — match that pattern when adding markup.
- Images live in `/img/` and are referenced with absolute paths (`/img/foo.png`).
