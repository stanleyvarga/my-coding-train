# Shared modules

Reusable code imported by multiple demos. Not runnable on its own.

| Folder | Purpose |
|--------|---------|
| `math/` | Pure JavaScript — no DOM, no p5 |
| `format/` | Display helpers (numbers, labels) |
| `p5/` | p5-specific drawing helpers (add when needed) |

## Rules

- Extract here only when **two or more** demos need the same logic
- `math/` stays framework-agnostic
- Shared modules never import from `src/<topic-slug>/`

See [repository-structure.md](../../docs/specs/repository-structure.md).
