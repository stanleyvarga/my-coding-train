---
name: coding-train-repo
description: >-
  Enforces my-coding-train repository structure for Coding Train-style learning
  playgrounds. Use when adding topics, lessons, p5.js or vanilla JS demos,
  shared modules, or docs/specs in this repo. Follows docs/specs/repository-structure.md.
---

# Coding Train repo structure

Read [docs/specs/repository-structure.md](../../docs/specs/repository-structure.md) before creating or moving files.

## Three pillars

| Path | Purpose | Never put here |
|------|---------|----------------|
| `docs/specs/` | AI build specs, acceptance criteria | Long theory |
| `lessons/` | Human theory, intuition, video links | Agent instructions |
| `src/` | Runnable demos + `shared/` modules | Essay-length theory |

## Topic slug

One kebab-case slug across all pillars: `bayes-theorem`, `beginners-p5js`, etc.

```
docs/specs/<slug>.md
lessons/<slug>/
src/<slug>/
```

## Numbering

- Lessons: `lessons/<slug>/NN-<short-name>.md` (e.g. `01-prior-and-likelihood.md`)
- Demos: `src/<slug>/NN-<short-name>/` (e.g. `01-coin-flip/`)
- Variations: subfolder under same `NN-*` demo
- Use two-digit prefixes (`01`, not `1`)

## Crosslinks (required)

Every topic README and new lesson/demo must include YAML frontmatter linking siblings:

```yaml
topic: <slug>
spec: docs/specs/<slug>.md
lessons: lessons/<slug>/
source: src/<slug>/
```

Individual lessons add `lesson: NN`, `demo: src/<slug>/NN-<name>/`, optional `video:`.

Update the **demo map** table in `lessons/<slug>/README.md` when adding a lesson.

## Demo folder rules

One runnable app per folder. Self-contained — no bundler.

**Vanilla:** `index.html` + `main.js` (+ optional `style.css`). Use `type="module"` for imports.

**p5:** `index.html` (p5 CDN) + `sketch.js`. Do not mix with vanilla in the same folder.

Tag runtime in demo README frontmatter: `runtime: vanilla` or `runtime: p5`.

## Shared modules (`src/shared/`)

- `math/` — pure JS, no DOM/p5
- `format/` — display helpers
- `p5/` — p5-only helpers (create when needed)

Extract to `shared/` only after second use. Shared code never imports from demo folders.

## New topic checklist

```
[ ] Copy docs/specs/_template.md → docs/specs/<slug>.md
[ ] Create lessons/<slug>/README.md (frontmatter + empty demo map)
[ ] Create src/<slug>/README.md
[ ] Add rows to docs/README.md and lessons/README.md
[ ] Update "Current topics" table in repository-structure.md
```

## New lesson + demo checklist

```
[ ] lessons/<slug>/NN-<name>.md (theory)
[ ] src/<slug>/NN-<name>/ (index.html + main.js or sketch.js)
[ ] Update demo map in lessons/<slug>/README.md
[ ] Update demo checklist in docs/specs/<slug>.md
[ ] Extract to src/shared/ if logic is reused
```

## Manual pace

Build one lesson and one demo at a time. Do not bulk-scaffold topics, lessons, or demos unless the user explicitly asks.

## Run demos

```bash
npx serve src
```
