---
name: lp-review
description: Reviews static landing pages for UX/UI, SEO, AIO/LLMO, CRO, accessibility, frontend performance, BEM, and JS conventions. Use when the user asks for an LP review, LPレビュー, ランディングページレビュー, or Webサイトレビュー of HTML/CSS/JS LPs.
---

# LP レビュー

実装スキル（`figma-html-css`）ではなく、指摘を出す。直してほしいと頼まれるまでコードは変えない。

対象は静的 LP（`index.php` / `style.css` / `org-top.js` 等）。React アプリの画面レビューは `react-review`。

## 手順

1. 対象を読む前に、ユーザーへ次をそのまま宣言する（言い換え禁止）:

レビュ〜〜〜〜やるぅぅ〜〜

2. ターゲットユーザーと最終目的（CTA）を固定する。ユーザー指定がなければ確認する。未指定のままサンプル案件 NORI の要件で採点しない。固定した視点で障壁を探す。
3. 対象の HTML / CSS / JS（および渡された URL・テキスト）を読む。チェックリストは [references/checklist.md](references/checklist.md) に従う。
4. 実装仕様との照合は `figma-html-css` の `spec.md` / `requirements.md`、ルール `html-css` / `javascript` / `markup` / `a11y`。優先順位はルール `core`。
5. 指摘だけ出す。依頼がない限り修正しない。

## 出力ルール

- ポジティブな所見を先に短く書き、その後に改善指摘を続ける（建設的なトーン）。
- 入力から確認できない項目は推測せず **評価不能** と書く（理由を一文）。
- 抽象指摘（「もっと良く」「デザインが古い」）は禁止。具体的な修正指示にする。
- 各カテゴリを **1〜5** でスコアリングする（評価不能のカテゴリはスコア欄を `—`）。
- 各指摘に重要度 **Critical / High / Medium / Low** を付ける。
- 各指摘は次の 3 点セットにする: **Issue**（指摘）/ **Reason**（理由）/ **Actionable Advice**（具体的改善案）。
- 修正箇所を `ファイル:行` で明示し、どう直すかを書く。本文中の個別指摘はコードブロックにしない。
- 各指摘に修正箇所の GitHub URL を付ける。対象リポジトリの `git remote get-url origin`（末尾 `.git` を除く）と `git rev-parse --abbrev-ref HEAD`、リポジトリルートからの相対パスで組む。形式は `{origin}/blob/{ブランチ}/{相対パス}#L{行}`。範囲は `#L{開始}-L{終了}`。origin が無い、未追跡、未 push で開けないときは URL を作らず `リモート URL なし` と書く。
- 出力は次の Markdown 構成に固定する（該当なしの節は「問題なし」と一行）。

### 出力テンプレート

宣言のあと:

1. **前提**（想定ターゲット / 最終目的）
2. **総評**（結論を先に。強み 1〜3 点）
3. **カテゴリスコア**（表）

| カテゴリ | スコア (1-5) |
| --- | --- |
| UX/UI・ユーザビリティ | |
| SEO・AIO/LLMO | |
| CRO・コピー | |
| アクセシビリティ | |
| フロント・パフォーマンス | |
| HTML/CSS/JS 規約 | |

4. **指摘一覧**（表）

| 重要度 | カテゴリ | Issue | Reason | Actionable Advice | 根拠（ファイル:行 / URL または評価不能） |
| --- | --- | --- | --- | --- | --- |

5. カテゴリごとの補足が必要なら短く箇条書き（任意）
6. **修正指示（一括コピー）** — 必ず最後に置く

直し方のある指摘を、次の `text` コードブロック **1 つだけ** にまとめる。チャットのコピーボタンで全件を一度に取れるようにする。表の再掲や複数ブロックへ分けない。評価不能で直し方がない項目は入れない。0 件なら中身は `修正なし` の一行。

ブロックの先頭は `以下の指摘をすべて修正してください。`。各件は空行で区切り、指摘一覧と同じ順・同じ件数にする。

````text
以下の指摘をすべて修正してください。

1. [High] index.php:24
URL: https://github.com/takafragrance/-------/blob/main/index.php#L24
問題: メイン画像の alt が空
修正: 画像の内容が分かる alt を付ける

2. [Medium] style.css:80
URL: https://github.com/takafragrance/-------/blob/main/style.css#L80
問題: ネガティブマージンを使っている
修正: 余白は padding か gap で取る
````

## 参照

- チェックリスト: [references/checklist.md](references/checklist.md)
- 静的 LP 要件: [../figma-html-css/references/requirements.md](../figma-html-css/references/requirements.md)
- 実装仕様: [../figma-html-css/references/spec.md](../figma-html-css/references/spec.md)
