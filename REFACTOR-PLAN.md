# Refactor Plan: Static HTML → Astro

**Goal:** Migrate the resume/portfolio site to [Astro](https://astro.build) for GitHub Pages deployment, eliminating content duplication and enabling a proper build pipeline.

---

## Current State

| Aspect | Status |
|--------|--------|
| Pages | 3 HTML files (`index.html`, `index-formal.html`, `cv.html`) |
| Styling | 3 CSS files + large inline `<style>` blocks |
| Scripts | 1 JS file + inline JS (mobile nav toggle) |
| Assets | None (unicode icons, Font Awesome CDN on formal page) |
| Content | Hardcoded in HTML, duplicated across pages |
| Build | None — raw HTML served directly |
| Deploy | GitHub Pages (`kamil5b.github.io/resume/`) |
| Deps | Zero (`package.json` does not exist) |

---

## Target Architecture

```
resume/
├── public/
│   ├── favicon.ico
│   └── legacies/                  # Archived original HTML pages (served at /resume/legacies/)
│       ├── cv.html
│       ├── index-formal.html
│       ├── index.html
│       ├── styles.css
│       └── styles-formal.css
├── src/
│   ├── content/
│   │   ├── experience.json        # Work history data
│   │   ├── education.json         # Education data
│   │   ├── projects.json          # Open source + production projects
│   │   ├── skills.json            # Skills/tech stack data
│   │   ├── research.json          # IEEE publication
│   │   └── meta.json              # Name, title, bio, links, stats
│   ├── components/
│   │   ├── Head.astro             # <head> with meta, fonts, favicon
│   │   ├── Nav.astro              # Sticky navigation bar
│   │   ├── Hero.astro             # Landing hero section
│   │   ├── Stats.astro            # Stats bar (repos, commits, etc.)
│   │   ├── Experience.astro       # Work history cards
│   │   ├── Research.astro         # IEEE publication card
│   │   ├── Projects.astro         # Open source / project cards
│   │   ├── Skills.astro           # Tech stack / bar chart
│   │   ├── Contact.astro          # Contact card
│   │   ├── Footer.astro           # Site footer
│   │   └── ...                    # Additional section components
│   ├── layouts/
│   │   └── Base.astro             # Shared HTML shell (html, head, body)
│   ├── pages/
│   │   └── index.astro            # Main portfolio (→ current index.html)
│   └── styles/
│       └── global.css             # Shared base/reset styles + print styles
├── astro.config.mjs               # Astro config (static, base path)
├── package.json
├── pnpm-lock.yaml
└── tsconfig.json
```

---

## Step-by-Step Plan

### Phase 1: Scaffold Astro Project

1. Move legacy HTML files to `legacies/` folder
2. Initialize Astro in the repo root (`pnpm create astro@latest .`)
3. Configure `astro.config.mjs` for GitHub Pages:
   ```js
   import { defineConfig } from 'astro/config';
   export default defineConfig({
     site: 'https://kamil5b.github.io',
     base: '/resume',
     output: 'static',
   });
   ```
4. Create `package.json` with scripts (`dev`, `build`, `preview`)
5. Add `.gitignore` for `node_modules/`, `dist/`, `.astro/`

### Phase 2: Extract Content into Data Files

Move all hardcoded HTML content into JSON data files under `src/content/`. This is the key refactor — **single source of truth** for all content.

**Files to create:**

| Data File | Content |
|-----------|---------|
| `meta.json` | `name`, `title`, `bio`, `email`, `github`, `linkedin`, `stats` (repo count, commits, experience years) |
| `experience.json` | Array of jobs: `company`, `role`, `period`, `type`, `bullets[]`, `tech[]` |
| `education.json` | Array of degrees: `institution`, `degree`, `period`, `details[]` |
| `projects.json` | Array of projects: `name`, `description`, `tags[]`, `url`, `category` (open-source / production) |
| `skills.json` | `categories[]` each with `name`, `skills[]`, and optional `usageLevel` (for bar chart) |
| `research.json` | Publication: `title`, `venue`, `year`, `doi`, `authors[]` |

Content will be sourced from the existing `REQUIREMENT.md` and `ADDITIONAL.md` as reference, but the canonical source becomes the JSON files.

### Phase 3: Create Layout

**`Base.astro`** — shared HTML shell:
- Contains `<!DOCTYPE html>`, `<html>`, `<head>`, `<body>` boilerplate
- Renders `<Head.astro>` and `<Nav.astro>`
- Slot for page content
- Includes the mobile nav toggle `<script>` (JS stays minimal, inline)

The formal CV page is archived in `legacies/` — no separate formal layout needed.

### Phase 4: Build Components

Create `.astro` components that read from the JSON data files. Each component is self-contained and responsible for one visual section.

| Component | Reads From | Key Logic |
|-----------|-----------|-----------|
| `Nav.astro` | Props | Renders nav links for portfolio |
| `Hero.astro` | `meta.json` | Name, title, bio, CTA buttons |
| `Stats.astro` | `meta.json` | 4-column stats grid |
| `Experience.astro` | `experience.json` | Timeline cards, nested role cards |
| `Research.astro` | `research.json` | IEEE publication card |
| `Projects.astro` | `projects.json` | Grid of project cards, filterable by category |
| `Skills.astro` | `skills.json` | Bar chart + tech-group cards |
| `Contact.astro` | `meta.json` | Contact links card |
| `Footer.astro` | — | Attribution line |
| `Icons.astro` | — | Inline SVG icon components (replaces Font Awesome CDN) |

**Component pattern:**
```astro
---
import experience from '../content/experience.json';
---
<section id="experience" class="section">
  {experience.map(job => (
    <div class="job-card">...</div>
  ))}
</section>
```

### Phase 5: Create Pages

**`pages/index.astro`** (main portfolio):
```astro
---
import Base from '../layouts/Base.astro';
import Hero from '../components/Hero.astro';
import Stats from '../components/Stats.astro';
import Experience from '../components/Experience.astro';
// ... etc
---
<Base title="Kamil — Portfolio">
  <Hero />
  <Stats />
  <Experience />
  <Research />
  <Projects category="open-source" />
  <Projects category="production" />
  <Skills />
  <Contact />
</Base>
```

The formal CV and legacy CV are archived in `public/legacies/` as static HTML files and served at `/resume/legacies/`.

### Phase 6: Migrate Styles & Icons

1. Extract shared base styles (reset, typography, color variables) into `src/styles/global.css`
2. Move page-specific styles into each component's `<style>` block (Astro scopes styles to the component by default)
3. Preserve the `@media print` styles in `global.css`
4. Keep CSS custom properties (design tokens) at the `:root` level in `global.css`
5. Replace Font Awesome CDN with lightweight inline glyphs (↗, ☰, ×) — already unicode
   - The main page uses unicode arrows and symbols, no icon library needed
   - Zero HTTP requests for icons

**CSS variable migration:**
```css
:root {
  --bg-primary: #0a0a0f;
  --text-primary: #e8e8ed;
  --accent: #6366f1;
  /* ... */
}
```

### Phase 7: Handle Responsive & Print Styles

- Responsive breakpoints (`900px`, `680px`) stay in component `<style>` blocks (Astro auto-scopes them)
- Print styles go in `global.css` under `@media print`
- `.print-only` class preserved for print metadata
- Only one page to maintain now (main portfolio), not three

### Phase 8: GitHub Pages Deployment

**Option A: GitHub Actions (recommended)**

Create `.github/workflows/deploy.yml`:
```yaml
name: Deploy to GitHub Pages
on:
  push:
    branches: [main]
permissions:
  contents: read
  pages: write
  id-token: write
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: pnpm/action-setup@v4
        with:
          version: 9
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: pnpm
      - run: pnpm install --frozen-lockfile
      - run: pnpm run build
      - uses: actions/upload-pages-artifact@v3
        with:
          path: dist
  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - id: deployment
        uses: actions/deploy-pages@v4
```

**Option B: Manual** — run `npm run build`, commit `dist/` to a `gh-pages` branch.

### Phase 9: Cleanup

1. Remove orphaned files not in `legacies/`: `script.js`, `script-formal.js` (if exists)
2. Move remaining legacy assets to `public/legacies/`: `styles.css`, `styles-formal.css`
3. Update `README.md` with new build instructions (`pnpm install && pnpm dev`)
4. The `public/legacies/` folder is archived and served at `/resume/legacies/`

### Phase 10: Verification

- [ ] `pnpm dev` — portfolio page renders correctly
- [ ] `pnpm build` — no errors, `dist/` output generated
- [ ] `pnpm preview` — site works at `/resume/` base path
- [ ] All navigation links work (anchor + cross-page)
- [ ] Responsive layout matches current at 900px and 680px breakpoints
- [ ] Print stylesheet produces correct A4 output
- [ ] Mobile nav toggle works
- [ ] No 404s in browser console
- [ ] `public/legacies/` folder contains archived HTML files, served at `/resume/legacies/`
- [ ] Deploy to GitHub Pages and verify live site

---

## Benefits of This Refactor

| Before | After |
|--------|-------|
| 3 copies of the same content | Single JSON data source |
| Edit 3 files to update a job | Edit 1 JSON file |
| No build step | `pnpm build` → optimized static output |
| Inline CSS (470 lines in HTML) | Scoped component styles |
| Font Awesome CDN (external dep) | Inline SVG icons (zero deps) |
| Broken JS reference | Clean component imports |
| No `.gitignore` | Proper git ignores |
| Manual deployment | Automated GitHub Actions CI/CD |

## Migration Order

Execute phases 1→2→3→4→5→6→7→8→9→10 sequentially. The site should be functional after each phase.

**Estimated effort:** 2–4 hours for a developer familiar with Astro.

---

## Decisions Made

- **`cv.html` + `index-formal.html` + original `index.html`:** Moved to `public/legacies/`, served at `/resume/legacies/` as archived static HTML. Internal links updated to stay consistent within the archive.
- **Font Awesome:** Replaced with unicode glyphs (↗, ☰, ×) — the main page never used Font Awesome, only the archived formal CV does (as a CDN link, unchanged).
- **`sessions.md`:** Kept in repo as documentation (not part of the site).
- **Base path:** Current deployment is at `/resume/`. Astro's `base: '/resume'` handles this.
