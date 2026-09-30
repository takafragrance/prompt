---
name: bugfix
description: Fixes bugs by reproducing the symptom, tracing root cause, grepping all callers, and patching the shared point once. Use when the user reports a bug, バグ, 動かない, 直して, 白画面, regression, or broken behavior.
---

# バグ修正

症状だけを塞がない。根因を直す。`AGENTS.md`（ponytail）の梯子を実装前に辿る。

## 手順

1. **症状を固定する**
   - 何が起きているか / 期待は何か / 再現手順。不明なら推測で大きく進めず確認する。
2. **該当コードを読む**
   - 報告が指す画面・ハンドラ・状態から、実際の制御フローを端まで辿る。
3. **呼び出し元を全部 grep する**
   - 直す関数・フック・ユーティリティの全 caller を洗う。兄弟経路が同じ根因なら共有箇所を1回直す。
4. **最小差分で根因を直す**
   - 依頼範囲外のリファクタ、先回りの抽象化、新規依存はしない。
   - 境界での入力検証・データ喪失防止は削らない。
5. **確認する**
   - 再現手順で直ったこと、兄弟呼び出しが壊れていないことを通す。
   - 非自明なロジックなら、壊れたら落ちる最小の自己確認を1つ残す（または同等を手元で実行する）。自明な一行修正は不要。
6. **短く報告する**
   - 根因は何か、どこを直したか、何を確認したか。

## やってはいけないこと

- チケットが名指ししたパスだけに `if` を足し、同じ関数の別 caller を放置する。
- 原因不明のまま UI の見た目だけ合わせる。
- 「ついでに」広いリファクタや命名変更を混ぜる。

## 参照

- 実装方針: ルートの `AGENTS.md`
- React ならルール `react` / スキル `react-app`
- 静的 LP ならルール `html-css` / `javascript`
