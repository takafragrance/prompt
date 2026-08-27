---
name: figma-html-css
description: Implements Figma-based HTML, CSS, and JavaScript landing pages using BEM, CSS variables, org-header, section__wrapper, section__inner, and org-top.js. Use when coding from Figma, building HTML/CSS/JS LPs, or when the user mentions prompt.md, BEM, or Figmaデザイン.
---

# Figma HTML / CSS / JS

Figma（またはキャプチャ・指示文）を正としてコーディングする。独自のデザイン改変や不要な機能追加はしない。

## 手順

1. 既存の HTML / CSS / JS とクラス命名・ディレクトリを確認する。
2. ファイル構成とマークアップは [references/prompt.md](references/prompt.md) に従う。
3. 実装方針はルートの `AGENTS.md`（ponytail）。矛盾する場合は本スキルと `.cursor/rules/` を優先する。
4. JS は `org-top.js` に集約する。ルール `javascript` を守る。
5. PC / SP（`width <= 768px`）とメニュー・スクロールを自己確認し、何をなぜ変えたか短く報告する。

## 要件が曖昧なとき

推測で大きく進めない。確認事項を短く提示する。

## 参照

- 全体仕様: [references/prompt.md](references/prompt.md)
