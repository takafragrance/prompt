---
name: react-review
description: Reviews React code for extra code, clarity, vulnerabilities, Hooks, state placement, component boundaries, performance, and TypeScript safety. Use when the user asks for a React review, コードレビュー, レビュー, or Reactレビュー.
---

# React レビュー

実装スキル（`react-app`）ではなく、指摘を出す。直してほしいと頼まれるまでコードは変えない。

「動くからOK」ではなく、「半年後の自分やチームメンバーが読んで、安全に改修できるコードか」という視点を持つことが、Reactのプロジェクトを長生きさせる秘訣です。

## 手順

1. 対象コードを読む前に、ユーザーへ次をそのまま宣言する（言い換え禁止）:

レビュ〜〜〜〜やるぅぅ〜〜

2. 対象の `src/` と差分を読む。呼び出し元まで辿る。
3. チェックリストは [references/checklist.md](references/checklist.md) に従う。画像・リンクはルール `markup` も照合する。
4. 実装方針はルートの `AGENTS.md`（ponytail）。矛盾する場合は本スキルと `.cursor/rules/react-review.mdc` を優先する。
5. 指摘だけ出す。依頼がない限り修正しない。

## 出力

宣言のあと、次の順で書く。該当なしは「問題なし」と一行。

- 総評（半年後に安全に改修できるか、結論を先に）
- 余計なコード / 簡潔明瞭 / 脆弱性
- 1. Hooksの適切な利用
- 2. 状態（State）の管理と配置
- 3. コンポーネントの設計と責務の分離
- 4. パフォーマンスの最適化
- 5. 型安全と堅牢性（`.tsx`。Props の型、`any` / `as`）
- 6. 画像・リンクマークアップ（ルール `markup`）
- 7. CSS 規約（Tailwind、ネガティブマージン禁止、インライン `style` 禁止）

各指摘は `ファイル:行` で修正箇所を明示し、何がまずいか・どう直すかを書く。重大度は 必須 / 推奨 / 任意。本文中の個別指摘はコードブロックにしない。

指摘のあとに **修正指示（一括コピー）** を必ず置く。直し方のある指摘を、次の `text` コードブロック **1 つだけ** にまとめる。チャットのコピーボタンで全件を一度に取れるようにする。表や複数ブロックへ分けない。評価不能で直し方がない項目と「問題なし」は入れない。0 件なら中身は `修正なし` の一行。

ブロックの先頭は `以下の指摘をすべて修正してください。`。各件は空行で区切り、指摘本文と同じ順・同じ件数にする。

````text
以下の指摘をすべて修正してください。

1. [必須] src/App.tsx:12
問題: 依存配列が不足している
修正: useEffect の依存に userId を足す

2. [推奨] src/List.tsx:40
問題: key に index を使っている
修正: 安定した id を key にする
````

## 参照

- チェックリスト: [references/checklist.md](references/checklist.md)
