---
name: react-landing
description: Implements branded React landing pages with Vite, Tailwind, hero-first composition, and full-bleed visuals. Use when building or changing a React LP, ブランドページ, fashion/house/tobacco landing, or marketing surface in my-react-app (not PHP BEM LPs, not CRUD screens).
---

# React ランディング

Figma 静的 LP（`figma-html-css`）でも CRUD 画面（`react-app`）でもない。React + Tailwind のブランド／プロモ LP を実装する。

## 手順

1. 既存の `src/<feature>-landing/`（または同等）とルート表を読む。Figma / キャプチャ / 指示があればそれを正とする。
2. レイアウトとヒーロー制約は [references/design.md](references/design.md) に従う。コンポーネント規約の土台は `react-app` の `implementation.md`（`.tsx`、Tailwind、ルーティング）。
3. 画像・リンクはルール `markup`。a11y はルール `a11y`。JS はルール `javascript`。
4. 実装方針は `AGENTS.md`。矛盾する場合は本スキルと `.cursor/rules/react-landing.mdc` を優先する。
5. 3D が中核なら `three-landing` に委ね、本スキルは HTML／2D 周りだけ担う。
6. PC / SP と主 CTA を通し、何をなぜ変えたか短く報告する。

## 要件が曖昧なとき

推測で大きく進めない。確認事項を短く提示する。

## 参照

- デザイン制約: [references/design.md](references/design.md)
- React 実装土台: [../react-app/references/implementation.md](../react-app/references/implementation.md)
