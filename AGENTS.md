# AGENTS.md — recipes

## Repo at a glance

- **What**: Personal recipe collection served as a static site via [Docsify](https://docsify.js.org/), deployed to GitHub Pages (`https://digitaldoggo.github.io/recipes/`).
- **Source root**: `docs/` (all prose, recipes, sidebar config live here).
- **Entry point**: `docs/index.html` — Docsify bootstrap + config.
- **Runtime dep**: `docsify-cli@^4` (devDependency only).

## Commands

| Action | Command |
|---|---|
| Local dev server | `yarn start` → serves `docs/` on port 3000 |
| Build static site | `yarn build` |
| Deploy to GitHub Pages | `yarn deploy` (pushes `docs/` content to the repo) |

All commands run from repo root. No lint, test, or typecheck — this is a markdown-only project.

## Recipe format conventions

Every recipe file follows this structure:

```markdown
# Recipe Title

> Optional subtitle / alias (blockquote on line 2)

## Ingredients

| Ingredient | Quantity |
| --- | --- |
| ... | ... |

## Directions   (or "Instructions")

1. Step one.
2. Step two.

> ## Notes          (optional — blockquote with bullet list)
> - Tip or variation.

<!-- ## Nutrition Facts  (optional, commented out by default) -->
```

**Rules**:
- Ingredients table: two columns (`Ingredient`, `Quantity`). Parenthetical prep notes go inside the ingredient name cell (e.g., `Onion (chopped)`).
- Steps are numbered lists under `## Directions` or `## Instructions`.
- Notes go in a blockquote with `> ## Notes` heading.
- Nutrition Facts tables are commented out (`<!-- -->`) — leave them that way unless explicitly enabled.
- Optional add-ins use a separate blockquote line: `> Optional Add-ins: ...`

## Sidebar & navigation

- **Sidebar config**: `docs/_sidebar.md` — the single source of truth for Docsify sidebar links.
- **Category index pages**: `docs/baking/main.md`, `docs/cooking/main.md` — each lists recipes in that category with relative links (e.g., `baking/chocolate_chip_cookies.md`).
- When adding a new recipe: update both `_sidebar.md` and the relevant `main.md`.

## Docsify config (`docs/index.html`)

Key settings in `window.$docsify`:
- `loadSidebar: true` — reads `_sidebar.md`
- `alias` maps any `/_sidebar.md` path to the root sidebar file
- `subMaxLevel: 2` — heading depth for TOC/sidebar nesting
- `search: 'auto'` — built-in search enabled
- Sidebar collapse plugin + search plugin loaded from CDN

## Git / workflow

- Single branch (`main`). No CI, no pre-commit hooks.
- `.gitignore` only excludes `node_modules/`.
- Commit messages are terse and imperative (e.g., "add banana bread", "fix sidebar").
- Recipes are added as new markdown files under `docs/baking/` or `docs/cooking/`.

## Gotchas

- **No build step** — changes to markdown are live on next serve. Only `yarn deploy` pushes content.
- **CDN dependencies** — Docsify, sidebar-collapse, and search plugins load from jsDelivr CDN. No local copies. If the site breaks, check CDN availability first.
- **Relative links** — all recipe links in `_sidebar.md` and `main.md` use paths relative to `docs/` root (e.g., `baking/chocolate_chip_cookies.md`, NOT `/recipes/baking/...`).
- **Filenames**: kebab-case with underscores for multi-word items (e.g., `coconut_oil_sugar_cookies.md`, `egg_tarts-hong_kong_style.md`). Be consistent with existing files in the same category.
