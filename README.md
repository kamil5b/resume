# Kamil's CV Website (Astro)

A modern, responsive portfolio site built with [Astro](https://astro.build). Deployed to GitHub Pages.

## Stack

- **Astro 7** — static site generation
- **pnpm** — package manager
- **JSON data files** — single source of truth for content (`src/content/`)
- **Zero runtime JS** — only a mobile nav toggle script

## Getting Started

```bash
pnpm install
pnpm dev        # local dev server at http://localhost:4321
pnpm build      # build static site to dist/
pnpm preview    # preview the built site
```

## Deployment

GitHub Actions (`.github/workflows/deploy.yml`) builds and deploys to GitHub Pages on every push to `main`.

Config details are in `astro.config.mjs`:

- `site: https://kamil5b.github.io`
- `base: /resume`

## Project Structure

```
├── public/
│   ├── favicon.ico / favicon.svg
│   └── legacies/              # Archived original HTML versions, served at /resume/legacies/
│       ├── cv.html            # Legacy CV
│       ├── index.html         # Original self-contained portfolio
│       └── index-formal.html  # Formal CV
├── src/
│   ├── content/             # JSON data files (edit these to update content)
│   │   ├── meta.json        # Name, bio, contact, stats
│   │   ├── experience.json  # Work history
│   │   ├── projects.json    # Open source + private projects
│   │   ├── research.json    # IEEE publication
│   │   └── skills.json      # Tech stack, focus areas, approach
│   ├── components/          # .astro components (one per section)
│   ├── layouts/Base.astro   # Shared HTML shell
│   ├── pages/index.astro    # Main page
│   └── styles/global.css    # Design tokens + print/responsive styles
├── astro.config.mjs
└── package.json
```

## Updating Content

All content lives in JSON files under `src/content/`. Edit those files and rebuild:
`pnpm build`.

## Legacy Files

The original hand-written HTML versions were moved to `public/legacies/` during the 2026 Astro refactor and are served at `https://kamil5b.github.io/resume/legacies/`. They are archived for reference only.