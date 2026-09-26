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

2. ターゲットユーザーと最終目的（CTA）を固定する。ユーザー指定がなければ [figma-html-css/references/requirements.md](../figma-html-css/references/requirements.md) の案件定義を使い、それでも不明なら確認する。その視点で障壁を探す。
3. 対象の HTML / CSS / JS（および渡された URL・テキスト）を読む。チェックリストは [references/checklist.md](references/checklist.md) に従う。
4. 実装仕様との照合は `figma-html-css` の `prompt.md` / `requirements.md`、ルール `html-css` / `javascript` / `markup`。矛盾する場合は本スキルと `.cursor/rules/lp-review.mdc` を優先する。
5. 指摘だけ出す。依頼がない限り修正しない。

## 出力ルール

- ポジティブな所見を先に短く書き、その後に改善指摘を続ける（建設的なトーン）。
- 入力から確認できない項目は推測せず **評価不能** と書く（理由を一文）。
- 抽象指摘（「もっと良く」「デザインが古い」）は禁止。具体的な修正指示にする。
- 各カテゴリを **1〜5** でスコアリングする（評価不能のカテゴリはスコア欄を `—`）。
- 各指摘に重要度 **Critical / High / Medium / Low** を付ける。
- 各指摘は次の 3 点セットにする: **Issue**（指摘）/ **Reason**（理由）/ **Actionable Advice**（具体的改善案）。
- 修正箇所を明示し、git で修正箇所を教えるとともに、どう修正したらいいかを明示する。
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

| 重要度 | カテゴリ | Issue | Reason | Actionable Advice | 根拠（ファイル:行 または評価不能） |
| --- | --- | --- | --- | --- | --- |

5. カテゴリごとの補足が必要なら短く箇条書き（任意）

## 参照

- チェックリスト: [references/checklist.md](references/checklist.md)
- 静的 LP 要件: [../figma-html-css/references/requirements.md](../figma-html-css/references/requirements.md)
- 実装仕様: [../figma-html-css/references/prompt.md](../figma-html-css/references/prompt.md)
