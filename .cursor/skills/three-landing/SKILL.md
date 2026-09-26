---
name: three-landing
description: Implements immersive 3D landing pages with Three.js or React Three Fiber, Spline GLB models, scroll-linked motion, and 2D fallbacks. Use when the task is a 3D LP, or the user mentions Three.js, R3F, glTF, GLB, Spline, WebGL, or three-landing.
---

# 3D ランディングページ

実装前に 3D を使う目的（世界観 / 360°構造 / 操作デモ）とターゲットを確定する。未記入時はスマホ優先・説明なしで成立。

## 手順

1. 目的と「2D では不足する点」を一文で残す。
2. 挙動を必須 / 任意に分ける。フォールバック（静止画 → 動画）を必ず入れる。静止画・リンクはルール `markup` に従う。
3. モデルは Spline → glTF / GLB。描画は Three.js。React では R3F。embed は使わない。
4. 合計 5MB 以下、テクスチャ最大 2K。ローディングと失敗時フォールバックを実装する。
5. JS は `.cursor/rules/javascript.mdc` に従う（`const`/`let`、レキシカル環境、`js-` 接頭辞）。詳細仕様は [references/requirements.md](references/requirements.md)。
6. 受け入れ条件を満たしたら完了とする。

3D 関連で HTML/CSS ルールと矛盾する場合は本スキルを優先する。実装方針は `AGENTS.md`。本スキルと矛盾する場合は本スキルを優先する。

## 参照

- 要件定義: [references/requirements.md](references/requirements.md)
