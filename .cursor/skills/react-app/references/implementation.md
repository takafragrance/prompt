# タスク：Vite + React アプリ開発

Vite + React の既存プロジェクトで、画面・コンポーネント・状態・フォーム・ルーティングを実装する。

実装方針は `AGENTS.md`（ponytail）に従う。本ファイルと矛盾する場合は **本ファイルを優先**する。

---

## 1. 対象とファイル構成

既存の Vite 構成に合わせる。典型例:

| 種別 | パス |
| --- | --- |
| エントリ | `src/main.jsx` または `src/main.tsx` |
| ルート UI | `src/App.tsx`（既存が `.jsx` ならそれに合わせる） |
| 共通部品 | `src/components/` |
| 機能単位 | `src/<feature>/`（既存フォルダがある場合） |
| スタイル | コンポーネントまたは機能と同階層の `.css` |
| ルート表 | `src/routes.js` |

- 新規ファイルは依頼範囲に必要なものだけ。同じ責務のヘルパが既にあればそれを使う。
- 新規コンポーネントは `.tsx`。既存ファイルの拡張子は変えない。
- 画像はプロジェクト既存の置き場（`src/assets/` や `public/`）に合わせる。

---

## 2. コンポーネント

- 関数コンポーネント + Hooks のみ。クラスコンポーネントは使わない。
- 名前付き export（`export const Foo = ...`）。ページルートの `App` など既存が default export ならそれに合わせる。
- props の型はファイル内に `type Props = { ... }` で置く。不要な共通型ファイルを作らない。
- 表示専用と入力専用を無理に分けない。リスト行だけが肥大化したら `FooItem` を足す。

```tsx
import "./ExpenseItem.css";

type Props = {
  title: string;
  amount: number;
};

export const ExpenseItem = ({ title, amount }: Props) => {
  return (
    <div className="expense-item">
      <p>{title}</p>
      <p>{amount}円</p>
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
const [items, setItems] = useState<Item[]>(() => readStored() ?? samples);

const handleAdd = (item: Omit<Item, "id">) => {
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

## 6. スタイル

- **Tailwind は使わない。** ユーティリティクラスも書かない。
- 見た目は外部 CSS ファイルに書く。コンポーネント（または機能フォルダ）と同じ場所に `.css` を作り、TSX/JSX から `import "./Foo.css"` する。
- 既存の同名 CSS があればそれを更新する。新規コンポーネントには `Foo.tsx` に対して `Foo.css` を足す。
- JSX は `className` のみ。`style={{ ... }}` は使わない。
- CSS Modules（`*.module.css`）は依頼がない限り使わない。
- 既存のクラス名があればそれに合わせる。新規はコンポーネント名をプレフィックスにする。

```tsx
import "./ExpenseForm.css";

export const ExpenseForm = ({ onAdd }: Props) => {
  return (
    <form className="expense-form" onSubmit={handleSubmit}>
      <input className="expense-form-input" />
    </form>
  );
};
```

---

## 7. JS / TS

- `const` / `let` のみ。インデントは **2スペース**。
- `innerHTML` でマークアップを組まない。
- `any` を増やさない。既存が JS なら無理に TS 化しない。
- 依存追加（状態管理、UI ライブラリ、フォームライブラリ、Tailwind）は依頼がない限り行わない。入っているもの（`react-hook-form` 等）は、その画面が既に使っているときだけ使う。

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
- Tailwind とインライン `style` で見た目を組まない。
