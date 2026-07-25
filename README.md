# 30键 Anglo · 入门学习

Interactive Anglo concertina (C/G) layout compare, notation toggle, and duplicate-note explorer.

## Live site

https://spritytang.github.io/anglo-concertina/

GitHub Pages 发布 **`online`** 分支。推送到 **`main`** 后，Action 会自动同步到 `online`，并把 `data-deploy` 设为 `online`（施工中页面置灰不可进）。本地 / `main` 保持 `data-deploy="main"`，全部页面可访问。

| 分支 | 用途 |
|------|------|
| `main` | 完整开发版 |
| `online` | Deploy 版（自动同步 main；跨行换指 → 曲目暂锁） |

## Local

- **Canonical learning page:** `index.html`
- Sync after verified edits: `cp index.html anglo-intro.html`
- Docs: [`docs/shoulders-of-giants.md`](docs/shoulders-of-giants.md), [`docs/research/`](docs/research/)
- Agent skills / rules: `.cursor/skills/`, `.cursor/rules/`
- 预览 Deploy 置灰：把 `<html … data-deploy="main">` 临时改成 `online` 后刷新

## Cursor

请用 Cursor **打开本目录**作为工作区。
