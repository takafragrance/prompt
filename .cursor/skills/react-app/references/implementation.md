# タスク：Vite + React アプリ開発

Vite + React の既存プロジェクトで、画面・コンポーネント・状態・フォーム・ルーティングを実装する。

実装方針は `AGENTS.md`（ponytail）に従う。本ファイルと矛盾する場合は **本ファイルを優先**する。

---

## 1. 対象とファイル構成

既存の Vite 構成に合わせる。典型例:

| 種別 | パス |
| --- | --- |
| エントリ | `src/main.tsx` |
| ルート UI | `src/App.tsx` |
| 共通部品 | `src/components/` |
| 機能単位 | `src/<feature>/`（既存フォルダがある場合） |
| スタイル | Tailwind（`className`）。エントリで `@import "tailwindcss"` |
| ルート表 | `src/routes.js` |

- 新規ファイルは依頼範囲に必要なものだけ。同じ責務のヘルパが既にあればそれを使う。
- React の UI（エントリ、画面、コンポーネント）は `.tsx`。`.jsx` は新規に作らない。依頼で触る `.jsx` は同じ変更の中で `.tsx` にする。
- 画像はプロジェクト既存の置き場（`src/assets/` や `public/`）に合わせる。

### 画像・リンクマークアップ

正本はルール `markup`。要点:

- コンテンツ画像: 必須属性 + `<figure>` / `<figcaption>`。
- メイン画像は原則 1 枚（`fetchPriority="high"`、lazy/async なし）。2 枚目以降は `fetchPriority="low"`。
- 装飾／UI アイコンは `alt=""`・`figure` 省略可。
- `<a>` / `<Link>` は裸で置かない。
- `target="_blank"`: お問い合わせ系はそれのみ。外部は `rel="noopener noreferrer nofollow"`。その他の新規タブは `rel="noopener noreferrer"`。

```tsx
<figure>
  <img
    src={heroImage}
    width={750}
    height={1334}
    alt="製品概要が分かるメインビジュアル"
    fetchPriority="high"
  />
</figure>
```

```tsx
<div className="ext-link">
  <a href="https://example.com" target="_blank" rel="noopener noreferrer nofollow">
    関連サイト
  </a>
</div>
```

---

## 2. コンポーネント

- 関数コンポーネント + Hooks のみ。クラスコンポーネントは使わない。
- 名前付き export（`export const Foo = ...`）。ページルートの `App` など既存が default export ならそれに合わせる。
- props は分割代入で受け取る。ファイル内に `type Props` を置く。共通型ファイルは依頼がない限り作らない。
- 表示専用と入力専用を無理に分けない。リスト行だけが肥大化したら `FooItem` を足す。

```tsx
type Props = {
  title: string;
  amount: number;
};

export const ExpenseItem = ({ title, amount }: Props) => {
  return (
    <div className="flex items-baseline justify-between gap-4 py-2">
      <p className="text-base text-zinc-800">{title}</p>
      <p className="text-sm text-zinc-600">{amount}円</p>
    </div>
  );
};
```

- リストは `key={item.id}`。`id` が無いときだけ index。新規行の id は `crypto.randomUUID()`。
- イベントは React の合成イベント（`onClick` / `onSubmit`）。DOM の `onclick` 属性と `addEventListener` 直書きは使わない。

---

## 3. 状態

- 状態は **使う場所の最も近い共通親** に置く。子は props とコールバックだけを受ける。
- `useState` で足りるなら Context / reducer / 外部ストアを足さない。
- 派生値は render 中に計算する。`useEffect` で state を同期しない。
- `useEffect` は外部同期（`localStorage`、fetch、購読）に限定する。クリーンアップが必要なら返す。

```tsx
const [items, setItems] = useState(() => readStored() ?? samples);

const handleAdd = (item: { title: string; amount: number }) => {
  setItems((prev) => [{ id: crypto.randomUUID(), ...item }, ...prev]);
};

useEffect(() => {
  try {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(items));
  } catch (e) {
    console.error("保存に失敗:", e);
  }
}, [items]);
```

- `localStorage` / `JSON.parse` は `try/catch`。壊れたデータでも初期値に戻し、白画面にしない。

---

## 4. フォーム

- デフォルトは制御コンポーネント（`value` + `onChange`）。
- 送信は `onSubmit`。`preventDefault` する。空文字・`NaN`・0 以下など無効値は state に入れない。
- `react-hook-form` は **既存ファイルが使っている、または明示依頼されたときだけ**。新規導入はしない。
- エラーメッセージは入力の直下に出す。送信後にフィールドを初期値へ戻すかは既存画面に合わせる。

---

## 5. ルーティング

- ルータは既存の `react-router-dom` のみ。
- ページを足す／パスを変えるときは `src/routes.js` の `KNOWN_PATHS` も更新する。
- 同じ state を複数ルートが表示するなら、持ち上げ先を変えずに両方の画面を確認する。

---

## 6. スタイル（Tailwind CSS）

- 見た目は **Tailwind CSS** のユーティリティを `className` に書く。
- プロジェクトは Vite + `@tailwindcss/vite`。エントリ CSS（例: `src/index.css`）で `@import "tailwindcss";` する。未導入なら依存とプラグインを足してから実装する。
- コンポーネント横の新規 `.css` / BEM / CSS Modules は作らない。既存の大きな `.css` を触る依頼なら、可能ならその範囲を Tailwind の `className` へ寄せる。
- 例外として `@keyframes` や `@theme` などユーティリティに落ちない定義だけ、エントリ近傍の CSS に最小限残してよい。
- ネガティブマージン（`margin` の負値 / `-mt-*` 等）は使用しない。位置調整は Flexbox / Grid / `transform` / 正の余白で行う。
- JSX は `className` のみ。`style={{ ... }}` は使わない（CSS 変数の動的代入など、ユーティリティで表現できない場合のみ例外を明示）。
- 条件付きクラスは文字列連結または小さなヘルパで足りる範囲に留める。クラス結合ライブラリは依頼がない限り追加しない。
- レスポンシブは Tailwind のブレークポイント（例: `md:`）。デザイン指定が `width <= 768px` なら `max-md:` / `md:` で合わせる。

```tsx
export const ExpenseForm = ({ onAdd }) => {
  return (
    <form className="flex flex-col gap-3" onSubmit={handleSubmit}>
      <input className="rounded border border-zinc-300 px-3 py-2 text-base" />
    </form>
  );
};
```

---

## 7. TS

- React の UI は `.tsx`。`const` / `let` のみ。インデントは **2スペース**。
- グローバル汚染を避ける（モジュールのレキシカル環境内で書く）。
- DOM をクラス名で掴む場合は先頭を **`js-`** にする（例: `js-menu`）。合成イベントだけで足りる場合は不要。
- `innerHTML` でマークアップを組まない。
- `any` を増やさない。外部入力（`JSON.parse`、API、`localStorage`）は形を確認してから使う。
- 依存追加（状態管理、UI ライブラリ、フォームライブラリ）は依頼がない限り行わない。`tailwindcss` / `@tailwindcss/vite` はスタイルの前提として未導入なら入れてよい。入っているもの（`react-hook-form` 等）は、その画面が既に使っているときだけ使う。

---

## 8. 検証・報告

UI / 状態 / ルーティングを変えたら、スクリーンショット 1 枚で終わらせない。

- 変更した操作を最初から最後まで行う（入力、送信、一覧反映、削除など）。
- 同じ state を読む他ルート・他コンポーネントも見る。
- 空状態・バリデーション失敗・保存失敗を確認する。
- レイアウト変更時は PC と `width <= 768px`。

報告は何を・なぜ変えたかを短く。未確認の項目があれば明記する。

---

## 9. 禁止

- 秘密情報を埋め込まない。破壊的な git 操作をしない。
- 依頼範囲外のリファクタ、ファイル分割、README 更新をしない。
- 見た目をコンポーネント専用の新規 `.css` やインライン `style` で組まない（Tailwind を使う）。
- ネガティブマージン（`margin` の負値 / `-m-*`）を使わない。
