---
name: figma-html-css
description: Implements Figma-based HTML, CSS, and JavaScript landing pages using BEM, CSS variables, org-header, section__wrapper, section__inner, and org-top.js. Use when coding from Figma, building HTML/CSS/JS LPs or static LP requirements, or when the user mentions BEM, 要件定義, AIO, LLMO, or Figmaデザイン.
---

# Figma HTML / CSS / JS

Figma（またはキャプチャ・指示文）を正としてコーディングする。独自のデザイン改変や不要な機能追加はしない。

## 手順

1. 実装前に [references/requirements.md](references/requirements.md) で目的・ブランド・ページ構成・AIO/LLMO（定義ブロック、見出し、FAQ の初期 HTML、JSON-LD、信頼情報）を確認する。実案件がサンプル（NORI）と違う場合は、差分をユーザーに確認してから進める。
2. **新規サイト制作**では、HTML 骨格の起点を Cursor User スニペット **`php.json`**（`~/Library/Application Support/Cursor/User/snippets/php.json`）とする。展開は当該ファイルの `prefix` に従う。`html.json` は使わない。既存ページの改修では既存マークアップを優先し、不足している AIO/LLMO 要素だけ足す。エージェントが新規 `index.php` 等を書く場合も、このスニペットと同等の骨格を出す。
3. 既存ファイルを読み、実装を始める前に、ユーザーへ次をそのまま宣言する（言い換え禁止）:

AIコーディングはっじめるよぉぉぉぉ〜〜〜〜

4. 既存の HTML / CSS / JS とクラス命名・ディレクトリを確認する。
5. ファイル構成とマークアップは [references/prompt.md](references/prompt.md) に従う。画像・リンクはルール `markup`。
6. 実装方針はルートの `AGENTS.md`（ponytail）。矛盾する場合は本スキルと `.cursor/rules/` を優先する。
7. JS は `org-top.js` に集約する。ルール `javascript` を守る（`const`/`let`、レキシカル環境、`js-` 接頭辞）。
8. PC / SP（`width <= 768px`）とメニュー・スクロールに加え、要件の受け入れ条件（定義ブロック・FAQ 全文・構造化データ等）を自己確認し、何をなぜ変えたか短く報告する。

## 要件が曖昧なとき

推測で大きく進めない。確認事項を短く提示する。

## 参照

- 新規サイトの HTML 起点（User スニペット）: `~/Library/Application Support/Cursor/User/snippets/php.json`
- 要件定義（案件・情報設計）: [references/requirements.md](references/requirements.md)
- 実装仕様（マークアップ・CSS・JS）: [references/prompt.md](references/prompt.md)
