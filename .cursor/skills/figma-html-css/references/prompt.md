# タスク：Figmaデザインの HTML / CSS / JS コーディング

提供する Figma デザインを基に、HTML・CSS・JavaScript を実装してください。

---

## 1. ファイル構成・ディレクトリ指定

| 種別 | パス / ファイル名 |
| --- | --- |
| HTML | `index.php` |
| CSS | `style.css` |
| JavaScript | `org-top.js` |
| 画像資産 | すべて `images/` フォルダ内に保存・参照する |

※ プロジェクト構成に合わせて `header.php` / `footer.php` や `css/` `js/` 配下への分割がある場合は、クラス名・要件は本プロンプトに準拠すること。
※ 新規サイトの HTML 起点（`php.json`）はルール `html-css` とスキル `figma-html-css` の手順に従う。

---

## 2. 実装要件

### レスポンシブ

- PC・モバイル・メニューを統合したレスポンシブデザインで実装する。

### モダンコーディング

#### CSS 変数（Custom Properties）

- `:root` で `--main-color`、`--accent-color`、`--section-padding` などを定義し、サイト全体で統一管理する。
- インナー幅も変数化する。
  - PC: `1140px`
  - スマホ: `89.3333vw`

#### レイアウト

- Flexbox / CSS Grid を適材適所で使用する。
- `.section__inner`（または同等のインナー）は次を満たす。
  - PC: `width: 1140px`
  - スマホ: `width: 89.3333vw`
  - `margin: 0 auto;` などで中央配置

#### 画像

- `.main-view__img img` など主要画像には `width: 100%;` や `aspect-ratio` を設定し、アスペクト比を維持して表示崩れを防ぐ。

#### メディアクエリ

- 比較演算子（range syntax）を使用する。例: `@media (width <= 768px)`
- メディアクエリ内のサイズ指定は、可能な限り `vw` に変換する。

#### 命名規則（BEM）

- `Block__Element--modifier` 方式のクラス名を採用する。

#### インデント

- HTML / CSS: **4スペース**
- JavaScript: **2スペース**（「4. JS 構成要件」参照）

#### 共通 CSS（属性セレクタ）

- `[class*=""]` など共通化できるスタイルは積極的に使う。
- 共通 CSS は **header / footer / section** ごとに分けて記述する（同一セレクタをサイト全体へ無差別適用しない）。

---

## 3. 共通 HTML 構造

各パーツは以下のクラス構成で実装する。セクションごとに `modifier` を付与してスタイルを制御する。

```html
<header class="org-header">
    <div class="org-header__inner">
        <!-- header contents -->
    </div>
</header>

<main class="l-main">
    <div class="main-view">
        <div class="main-view__img">
            <img src="./images/mv.webp" alt="製品概要が分かるメインビジュアル">
        </div>
        <div class="main-view__txt">
            <h1><!-- 製品名｜誰向けの価値（ページに h1 は1つのみ） --></h1>
            <!-- 定義アンサーブロック / lead / CTA -->
        </div>
    </div>

    <section class="section__wrapper--example">
        <div class="section__inner--example">
            <div class="ttl-box">
                <h2 class="section-ttl">タイトル</h2>
                <p class="section-sub-ttl">サブタイトル</p>
            </div>
            <!-- section contents -->
        </div>
    </section>
</main>

<footer class="org-footer">
    <div class="org-footer__inner">
        <!-- footer contents -->
    </div>
</footer>
```

---

## 4. JS 構成要件

### 記述ルール

- `const` または `let` で記述する（`var` は使わない）。
- グローバル汚染を防ぐため、即時関数（IIFE）やモジュールなど、適切なレキシカル環境内で記述する。
- インデントは **2スペース** で揃える。
- JS 内に CSS（インラインスタイルの大量付与など）を記述しない。見た目の制御は CSS クラスの付け外しで行う。

### 保守性・安全性

- `innerHTML` の無闇な使用は避け、`textContent` や `classList` などを用いて安全に実装する。
- DOM 取得時は null チェックを行い、エラーに強いコードにする。

### 外部ファイルへの集約（インライン禁止）

- HTML 内へのインライン `<script>` は禁止する。処理はすべて `org-top.js`（またはプロジェクトで指定した JS ファイル）に集約する。
- HTML 要素へのインラインイベントハンドラ（`onclick=""` / `onload=""` など）は禁止する。
- イベントは JavaScript 側で `addEventListener` を用いて設定する。

---

## 5. AI コーディング要件

AI（Cursor 等）に実装を依頼する場合、以下を必ず守ること。本プロンプトの **1〜4** と矛盾する出力は採用しない。

### 作業前の確認

- 読み込んで実装する前に、次をそのまま宣言する（言い換え禁止）: `AIコーディングはっじめるよぉぉぉぉ〜〜〜〜`
- 実装前に、対象の HTML / CSS / JS と既存クラス命名・ディレクトリ構成を確認する。
- 新規サイトの HTML 起点はルール `html-css` / スキル手順（`php.json`）に従う。
- Figma / キャプチャ / 指示文がある場合はそれを正とし、独自のデザイン改変や不要な機能追加をしない。
- 要件が曖昧なときは推測で大きく進めず、確認事項を短く提示する。

### 出力の範囲

- 依頼されたファイル・範囲のみを変更する。無関係なリファクタ、ファイル分割、ライブラリ追加は行わない。
- 新規ファイルが必要な場合は、本プロンプトの構成（`images/` 参照、BEM、共通クラス分割など）に合わせる。
- ドキュメント（README 等）や設定ファイルは、明示的に求められない限り作成・更新しない。

### コード品質

- 既存コードのスタイル（インデント、命名、セレクタ粒度、コメント量）に合わせる。
- 「動くだけのコード」ではなく、本プロンプトの命名規則・メディアクエリ・変数管理・JS 安全要件を満たすこと。
- 過剰な抽象化、未使用のユーティリティ、説明コメントの羅列は避ける。
- プレースホルダ文言（`TODO` / `lorem` / `xxx`）やダミー実装を残さない。必要な場合は明示する。

### デザイン・レスポンシブ

- ピクセルパーフェクトを目指しつつ、既存の変数・インナー幅・ブレイクポイント（`width <= 768px`）に従う。
- PC で組んだ数値を SP へ写すときは `vw` 変換を行い、固定 `px` のままにしない。
- 画像は `images/` 配下を参照し、パス切れやアスペクト崩れがないことを確認する。

### JavaScript

- インライン script / インラインイベントは出力しない。
- `innerHTML` でマークアップを組み立てない。DOM 操作は `textContent` / `classList` / `createElement` 等を使う。
- 取得した要素は必ず存在確認してから扱う。
- 見た目の制御は CSS クラスの付け外しに寄せ、JS から直接 `style` を多用しない。

### 検証・報告

- 変更後は、主要ブレイクポイント（PC / SP）と主要インタラクション（メニュー、スクロール、アニメーション等）を意識して自己確認する。
- ユーザーへの説明は簡潔にし、何を・なぜ変えたかが分かるようにする。
- 本プロンプトに未記載の技術選定（ビルドツール、フレームワーク導入など）は、依頼がない限り行わない。

### 禁止事項

- 秘密情報（API キー、認証情報）をコードやコメントに埋め込まない。
- 破壊的な git 操作（force push、履歴改変など）を勝手に実行しない。
- 既存の header / footer / 共通スタイルを、依頼範囲外で書き換えない。

### 実装方針

- 実装方針は `AGENTS.md`（ponytail）に従う。ただし本プロンプト 1〜5 と矛盾する場合は 1〜5 を優先する。