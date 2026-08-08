# ico

Public agent skill for the [ico favicon picker](https://ico.joe-taylor.me).

This repository is **skills-only**. It does not contain the application source or any hosting/deploy config.

## Install

```bash
npx skills add JoeBuildsStuff/ico
```

Or install just this skill:

```bash
npx skills add JoeBuildsStuff/ico --skill ico
```

## What it does

Teaches coding agents to:

1. Search free icon libraries via `https://ico.joe-taylor.me/api/icons`
2. Export a favicon zip via `POST /api/export`
3. Install `favicon.svg` / `favicon.ico` / `apple-touch-icon.png` into a web project

## Links

- Human UI: https://ico.joe-taylor.me
- Agent index: https://ico.joe-taylor.me/llms.txt
- Skill source: [`skills/ico/SKILL.md`](./skills/ico/SKILL.md)
