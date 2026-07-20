# <Topic title>

Copy this file to `docs/specs/<topic-slug>.md` when starting a new topic.

```yaml
---
topic: <topic-slug>
lessons: lessons/<topic-slug>/
source: src/<topic-slug>/
status: draft
coding_train:
  playlist:        # optional URL
  videos: []       # optional list of { id, title, url }
---
```

## Goal

One paragraph: what interactive demos should exist when this topic is complete.

## Audience

Who this is for and what they should already know.

## Demos to build

Check off as you implement manually:

| # | Demo path | Runtime | Lesson | Done |
|---|-----------|---------|--------|------|
| 01 | `src/<topic-slug>/01-<name>/` | vanilla / p5 | `lessons/<topic-slug>/01-<name>.md` | [ ] |

## Acceptance criteria

- [ ] Each demo opens via local static server without a build step
- [ ] Lesson `NN` crosslinks to demo `NN` in frontmatter
- [ ] Shared logic lives in `src/shared/` only when used twice
- [ ] Demo map in `lessons/<topic-slug>/README.md` is up to date

## Constraints

- Follow [repository-structure.md](repository-structure.md)
- Build incrementally — one lesson + one demo at a time
- No framework beyond p5 CDN or vanilla ES modules unless spec says otherwise

## Out of scope

What this topic explicitly does **not** cover.
