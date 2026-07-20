# Repository structure spec

Canonical reference for how this repo is organized. Follow this when adding topics, lessons, demos, or shared modules.

**Status:** active  
**Last updated:** 2026-07-20

---

## Purpose

This repo is a personal learning playground inspired by [The Coding Train](https://thecodingtrain.com). It holds:

1. **Runnable browser apps** — p5.js sketches and vanilla JavaScript demos
2. **Lesson theory** — human-readable breakdowns of concepts behind each demo
3. **AI specs** — build instructions and acceptance criteria for chatbots

Build everything **manually and incrementally**. This spec defines structure and rules, not finished content.

---

## Three pillars

| Pillar | Path | Audience | Contains |
|--------|------|----------|----------|
| Specs | `docs/specs/` | AI agents | What to build, constraints, acceptance criteria |
| Lessons | `lessons/` | Human learner | Theory, intuition, math, video links |
| Source | `src/` | Browser | Runnable demos + shared modules |

### Separation rules

- **Specs** → goals and verification. No long theory.
- **Lessons** → explanation and intuition. No agent instructions.
- **Source** → code only. No essay-length theory (link to `lessons/` instead).

---

## Topic slug

Every series uses one **kebab-case slug** across all three pillars:

```
bayes-theorem
beginners-p5js
perlin-noise
```

Same slug in:

- `docs/specs/<slug>.md`
- `lessons/<slug>/`
- `src/<slug>/`

---

## Repository tree

```
my-coding-train/
├── docs/
│   ├── README.md
│   └── specs/
│       ├── repository-structure.md   ← this file (repo-wide rules)
│       ├── _template.md              ← copy for new topic specs
│       └── <topic-slug>.md           ← per-topic AI spec
│
├── lessons/
│   ├── README.md
│   └── <topic-slug>/
│       ├── README.md                 ← topic index + demo map
│       ├── 01-<short-name>.md
│       ├── 02-<short-name>.md
│       └── ...
│
├── src/
│   ├── README.md
│   ├── shared/                       ← reusable modules (not playgrounds)
│   │   ├── math/
│   │   ├── format/
│   │   └── p5/                       ← p5-only helpers (add when needed)
│   └── <topic-slug>/
│       ├── README.md                 ← how to run demos for this topic
│       ├── 01-<short-name>/          ← one runnable demo per folder
│       └── 02-<short-name>/
│
├── .cursor/skills/coding-train-repo/ ← agent skill for this structure
└── skills-lock.json
```

---

## Numbering

Use **two-digit prefixes** so folders and files sort in learning order:

| Layer | Pattern | Example |
|-------|---------|---------|
| Lesson file | `NN-<short-name>.md` | `01-prior-and-likelihood.md` |
| Demo folder | `NN-<short-name>/` | `01-coin-flip/` |
| Variation | subfolder under same `NN-*` | `02-posterior-bars/dots-variant/` |

Rules:

- `01`, `02`, `03` — not `1`, `2` (keeps sort stable)
- Lesson `NN` should match its primary demo `NN` when they cover the same step
- Variations share the parent lesson number; distinguish by subfolder name

---

## Crosslinks

Every topic ties together through **YAML frontmatter** and README demo maps.

### Topic spec (`docs/specs/<slug>.md`)

```yaml
---
topic: bayes-theorem
lessons: lessons/bayes-theorem/
source: src/bayes-theorem/
status: draft          # draft | active | complete
---
```

### Topic lesson index (`lessons/<slug>/README.md`)

```yaml
---
topic: bayes-theorem
spec: docs/specs/bayes-theorem.md
source: src/bayes-theorem/
---
```

### Individual lesson (`lessons/<slug>/NN-*.md`)

```yaml
---
topic: bayes-theorem
lesson: 01
title: Prior and likelihood
demo: src/bayes-theorem/01-coin-flip/
video: https://www.youtube.com/watch?v=...   # optional
---
```

### Demo folder (`src/<slug>/NN-*/README.md` — optional but recommended)

```yaml
---
topic: bayes-theorem
lesson: 01
runtime: vanilla    # vanilla | p5
lesson_doc: lessons/bayes-theorem/01-prior-and-likelihood.md
---
```

### Demo map (in `lessons/<slug>/README.md`)

Maintain a table linking lesson ↔ demo ↔ runtime:

| # | Lesson | Demo | Runtime |
|---|--------|------|---------|
| 01 | [Prior and likelihood](01-prior-and-likelihood.md) | `src/bayes-theorem/01-coin-flip/` | vanilla |
| 02 | [Posterior update](02-posterior-update.md) | `src/bayes-theorem/02-posterior-bars/` | p5 |

---

## Source layout

### Demo folder (one runnable app)

Each demo is **self-contained** and opens in a browser:

**Vanilla JavaScript**

```
src/<slug>/01-coin-flip/
├── index.html
├── main.js
└── style.css          # optional
```

**p5.js (Coding Train style)**

```
src/<slug>/02-posterior-bars/
├── index.html         # loads p5 from CDN + sketch.js
└── sketch.js
```

Rules:

- One demo = one folder under `src/<slug>/`
- Do not mix `vanilla` and `p5` in the same demo folder
- Prefer CDN for p5 in `index.html`; no build step required
- Use `type="module"` in vanilla demos when importing from `src/shared/`

### Shared modules (`src/shared/`)

Reusable logic used by **two or more** demos:

```
src/shared/
├── math/              # pure JS — no DOM, no p5
├── format/            # display helpers (numbers, labels)
└── p5/                # p5-specific drawing helpers (create when needed)
```

Rules:

- Extract to `shared/` only after the second use, or when you know two demos will need it
- `math/` must stay framework-agnostic
- Demos import shared code; shared code never imports from a demo folder
- Import path example: `import { posterior } from '../../shared/math/bayes.js'`

---

## Coding Train alignment

Patterns borrowed from the [Coding Train website archive](https://github.com/CodingTrain/website-archive):

| Pattern | Our equivalent |
|---------|----------------|
| One sketch per folder | `src/<slug>/NN-<name>/` |
| `index.html` + `sketch.js` | p5 demos |
| Numbered lessons | `lessons/<slug>/NN-*.md` + matching `src/` folders |
| Multiple variations | subfolder under same `NN-*` demo |
| Self-contained examples | each demo runs without a bundler |

Group by **playlist / series** (topic slug), not by runtime. Runtime is per demo.

---

## Manual workflow: add a new topic

Do these steps in order. Do not skip crosslinks.

```
[ ] 1. Choose topic slug (kebab-case)
[ ] 2. Copy docs/specs/_template.md → docs/specs/<slug>.md
[ ] 3. Create lessons/<slug>/README.md (frontmatter + empty demo map)
[ ] 4. Create src/<slug>/README.md (frontmatter + "no demos yet")
[ ] 5. Add row to lessons/README.md topic index
[ ] 6. Add row to docs/README.md spec index
```

### Add one lesson + demo (repeat per step)

```
[ ] 1. Write lessons/<slug>/NN-<name>.md (theory only)
[ ] 2. Create src/<slug>/NN-<name>/ (index.html + main.js or sketch.js)
[ ] 3. Update demo map in lessons/<slug>/README.md
[ ] 4. Update checklist in docs/specs/<slug>.md
[ ] 5. Extract shared code to src/shared/ if reused
```

---

## Running demos

No bundler required. Use a local static server for ES modules:

```bash
npx serve src
# open http://localhost:3000/<slug>/01-<name>/
```

Add `package.json` with a `dev` script when you are ready — not required for structure setup.

---

## What not to do

| Don't | Do instead |
|-------|------------|
| Put theory in `docs/specs/` | Put theory in `lessons/` |
| Put AI build instructions in `lessons/` | Put them in `docs/specs/` |
| Put demo-specific code in `src/shared/` | Keep it in the demo folder |
| Use different slugs per pillar | One slug everywhere |
| Create demos without a lesson (unless exploratory) | Add lesson stub or note in topic README |
| Auto-scaffold all topics at once | One topic, one lesson, one demo at a time |

---

## Current topics

| Slug | Spec | Lessons | Source | Status |
|------|------|---------|--------|--------|
| `bayes-theorem` | — | `lessons/bayes-theorem/` | `src/bayes-theorem/` | draft |

Update this table when adding topics.
