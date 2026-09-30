---
name: three-review
description: Reviews 3D landing pages for purpose, fallbacks, asset size limits, R3F conventions, loading, and accessibility. Use when the user asks for a 3D review, 3Dレビュー, WebGLレビュー, Splineレビュー, or Three.js / R3F landing review.
---

# 3D レビュー

実装スキル（`three-landing`）ではなく、指摘を出す。直してほしいと頼まれるまでコードは変えない。

対象は 3D ヒーロー／中核セクション付き LP（Three.js / R3F / GLB）。静的 LP 全体は `lp-review`、React 画面全般は `react-review`。

## 手順

1. 対象を読む前に、ユーザーへ次をそのまま宣言する（言い換え禁止）:

レビュ〜〜〜〜やるぅぅ〜〜

2. 3D の目的（世界観 / 360°構造 / 操作デモ）とターゲット（デバイス・操作前提）を固定する。不明なら確認する。
3. 対象のシーン実装・フォールバック HTML・アセット参照を読む。チェックリストは [references/checklist.md](references/checklist.md) に従う。
4. 実装仕様との照合は `three-landing` の `requirements.md`、ルール `three-d` / `javascript` / `markup`。矛盾する場合は本スキルと `.cursor/rules/three-review.mdc` を優先する。
5. 指摘だけ出す。依頼がない限り修正しない。

## 出力ルール

- ポジティブな所見を先に短く書き、その後に改善指摘を続ける。
- 確認できない項目（実ファイルサイズ等）は推測せず **評価不能** と書く。
- 抽象指摘は禁止。具体的な修正指示にする。
- 各カテゴリを **1〜5** でスコアリングする（評価不能は `—`）。
- 各指摘に重要度 **Critical / High / Medium / Low**。
- 各指摘は **Issue / Reason / Actionable Advice**。
- 修正箇所を `ファイル:行` で明示し、git で教え、直し方を書く。

### 出力テンプレート

宣言のあと:

1. **前提**（3D の目的 / ターゲット）
2. **総評**（結論を先に。強み 1〜3 点）
3. **カテゴリスコア**（表）

| カテゴリ | スコア (1-5) |
| --- | --- |
| 目的・ターゲット適合 | |
| フォールバック・reduced-motion | |
| モデル・ランタイム規約 | |
| パフォーマンス・容量 | |
| ローディング・失敗時 | |
| アクセシビリティ | |

4. **指摘一覧**（表）

| 重要度 | カテゴリ | Issue | Reason | Actionable Advice | 根拠（ファイル:行 または評価不能） |
| --- | --- | --- | --- | --- | --- |

## 参照

- チェックリスト: [references/checklist.md](references/checklist.md)
- 3D 要件: [../three-landing/references/requirements.md](../three-landing/references/requirements.md)
