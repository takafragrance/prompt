---
name: react-app
description: Implements Vite + React apps with function components, TypeScript, lifted state, forms, and react-router-dom. Use when building or changing a React app (CRUD, hooks, components, routing), or when the user mentions Reactアプリ, Vite, コンポーネント, useState, or react-hook-form.
---

# React アプリ

Vite + React の既存構成で画面・状態・フォームを実装する。スタイルは外部 `.css` を `import` する（Tailwind 禁止）。

## 手順

1. 対象の `src/` 構成、コンポーネント分割、状態の流れ（誰が `useState` を持つか）を読む。
2. ファイル配置とコンポーネント規約は [references/implementation.md](references/implementation.md) に従う。
3. 実装方針はルートの `AGENTS.md`（ponytail）。矛盾する場合は本スキルと `.cursor/rules/react.mdc` を優先する。
4. コンポーネントは `.tsx`。`const`/`let`、インデント 2、`innerHTML` 禁止はルール `javascript` を守る。イベントは合成イベント。
5. 変更した画面・ルート・状態をブラウザで通し、何をなぜ変えたか短く報告する。

## 要件が曖昧なとき

推測で大きく進めない。確認事項を短く提示する。

## 参照

- 実装規約: [references/implementation.md](references/implementation.md)
