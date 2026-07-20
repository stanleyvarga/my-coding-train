# Source

Runnable browser demos and shared modules.

## Layout

- `src/<topic-slug>/` — self-contained playgrounds (one folder per demo)
- `src/shared/` — reusable modules imported by demos

See [repository-structure.md](../docs/specs/repository-structure.md) for naming, numbering, and crosslink rules.

## Topics

| Topic | Path | Demos |
|-------|------|-------|
| Bayes theorem | [bayes-theorem/](bayes-theorem/) | 0 |

## Run a demo

```bash
npx serve src
# http://localhost:3000/<topic-slug>/01-<name>/
```
