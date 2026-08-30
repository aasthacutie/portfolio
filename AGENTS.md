# AGENTS.md

Guidance for AI agents (and humans) working in this repo.

## Project

Static multi-page portfolio site for Astha Shukla (BBA Marketing student). Plain HTML/CSS/JS — no framework, no build step, no backend.

## Structure

```
/
├── index.html            Home (hero, typing effect, quick highlights)
├── about.html            Summary, education, strengths, languages/interests
├── skills.html           Marketing / Professional / Digital skill bars
├── projects.html         Academic projects, filterable by category
├── certifications.html   Certifications, achievements, animated counters
├── contact.html          Static contact info (tel:/mailto:, no form)
├── styles.css            Single stylesheet, CSS custom properties for theme
├── main.js               Single vanilla JS file, all interactivity
└── README.md
```

Flat structure by design — no `css/`/`js/` subfolders. Keep new assets at root unless the user asks otherwise.

## Conventions

- **No inline `<style>` blocks** in HTML except one-off layout tweaks already present (e.g. `style="margin-top: ..."` for spacing) — keep new styling in `css/styles.css`.
- **No JS frameworks/libraries.** Vanilla JS only, no jQuery, no build tools.
- **Theme tokens** live in `:root` in `css/styles.css` (`--color-*`, `--font-*`, `--space-*`). Change the palette by editing these variables only — don't hardcode new colors in rules.
- **Navbar/footer markup is duplicated per page** (no templating engine). When editing nav links or footer text, update all 6 HTML files identically.
- **Active nav link** is driven by `data-page` attribute on `<body>` matching `data-page` on the matching `<nav>` `<a>` — set in `js/main.js` (`initActiveNavLink`).
- **New page checklist**: copy an existing page's `<head>`, navbar, and footer verbatim; set a unique `data-page` value on `<body>` and add a matching nav link (with the same `data-page`) to all other pages.
- **Fonts**: Google Fonts CDN (Poppins for headings, Inter for body) — loaded per-page in `<head>`.
- **CSS reset**: `normalize.css` via cdnjs CDN, loaded before `css/styles.css`.

## Content source

All copy (summary, education, skills, projects, achievements, contact info) is sourced from Astha Shukla's resume. If the resume changes, update the corresponding page(s) directly — there is no CMS or data file.

## Running locally

No build step. Open `index.html` directly in a browser, or serve the folder with any static server (e.g. VS Code Live Server) so relative paths resolve consistently.

## Interactive features (js/main.js)

- Mobile hamburger nav toggle
- Active nav link highlighting
- Scroll-reveal animations (`IntersectionObserver`, `.reveal` class)
- Hero typing effect (`.hero-typed`, phrases via `data-phrases` JSON attribute)
- Animated counters (`.counter-number`, target via `data-target`)
- Animated skill bars (`.skill-bar-fill`, level via `data-level`)
- Project filter tabs (`.filter-tab` + `.project-card[data-category]`)

Each feature guards on the relevant element existing, so `main.js` is safe to include unchanged on every page.
