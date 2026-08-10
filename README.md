# favi

Public agent skill for the [favi favicon picker](https://favi.joe-taylor.me).

This repository is **skills-only**. It does not contain the application source or any hosting/deploy config.

## Install

```bash
npx skills add JoeBuildsStuff/favi
```

Or install just this skill:

```bash
npx skills add JoeBuildsStuff/favi --skill favi
```

## What it does

Teaches coding agents to:

1. Search free icon libraries via `https://favi.joe-taylor.me/api/icons`
2. Export a favicon zip via `POST /api/export`
3. Install `favicon.svg` / `favicon.ico` / `apple-touch-icon.png` into a web project

## Links

- Human UI: https://favi.joe-taylor.me
- Agent index: https://favi.joe-taylor.me/llms.txt
- Skill source: [`skills/favi/SKILL.md`](./skills/favi/SKILL.md)
