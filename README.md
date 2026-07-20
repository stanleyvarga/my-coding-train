<p align="center">
  <a href="https://thecodingtrain.com">
    <img src="https://thecodingtrain.com/images/train.mini.svg" alt="The Coding Train" width="320" />
  </a>
</p>

# my-coding-train

A personal learning playground inspired by [The Coding Train](https://thecodingtrain.com). Runnable browser apps, lesson notes, and AI specs — built manually, one step at a time.

## What’s here

| Pillar | Path | What it holds |
|--------|------|---------------|
| **Lessons** | [`lessons/`](lessons/) | Theory, intuition, and links to Coding Train videos |
| **Source** | [`src/`](src/) | Runnable p5.js and vanilla JavaScript demos |
| **Specs** | [`docs/specs/`](docs/specs/) | Build instructions and acceptance criteria for AI agents |

Full layout, numbering, and crosslink rules: **[Repository structure spec](docs/specs/repository-structure.md)**

## Topics

| Topic | Lessons | Demos |
|-------|---------|-------|
| Bayes theorem | [lessons/bayes-theorem/](lessons/bayes-theorem/) | `src/bayes-theorem/` (in progress) |

## Run a demo

```bash
npx serve src
```

Then open `http://localhost:3000/<topic-slug>/01-<demo-name>/`.

## Repo layout

```
docs/specs/     → AI specs + repository rules
lessons/        → human-readable theory
src/            → runnable demos + shared modules
```

## Credits

Tutorials and inspiration from **Daniel Shiffman** and [The Coding Train](https://thecodingtrain.com). This repo is a personal study project, not affiliated with the channel.
