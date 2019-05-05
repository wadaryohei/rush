# RUSH CSS FrameWork

Scss/Simple Grid Framework.
ClassベースまたはMixinベースでのシンプルなCSSフレームワークです。

## Concept / 名前の由来
[Bootstrap](https://getbootstrap.com/)のように多機能な面やコンポーネントがしっかりとしているフレームワークもありますが、プロジェクトに導入してみると実際はグリッドのみを使用して、コンポーネントに関してはオーバーライドが発生し、不必要なファイルやセレクタで溢れていることに気づきシンプルなグリッドのみのフレームワークの開発に着手致しました。

「RUSH」は「急ぐ」や「早く」といった、素早く組み立てることを目的として意味をつけました。

## Features / 特徴
* グリッドシステムがメインのシンプルかつ最小限の構成のフレームワーク。
* Classベース or Scssベースでの開発が可能。設定ファイルにグリッドの基本設定を入れています。
* グリッドはレスポンシブ対応済み。
* アイコンフォント[Font Awesome 5](https://fontawesome.com/)を設置。
* Bootstrapのような豊富なコンポーネントを持たない為、SCSSのみで動作可能。Vue.JSやReact.JSなどJavascriptライブラリを選ばず使用可能。

## Usage / 使い方

### Download
[ダウンロード](https://github.com/wadaryohei/rush/archive/master.zip)

### Setup
Sass/Scssベースのフレームワークです。
お使いのマシンに予めSassやCompassなどのインストールが必要です。

## SCSS
Venderフォルダに全ファイルをまとめています。

```
[ lib ]
│ ├[ css ]
│ | └[ style.css ]
│ ├[ js ]
│ │ └[ app.js ]
│ ├[ sass ]
│ │ └[ vendor ]
│ │ │ ├_copyright.scss
│ │ │ ├_custom.scss
│ │ │ ├_global.scss
│ │ │ ├_grid.scss
│ │ │ ├_mixin.scss
│ │ │ ├_reset.scss
│ │ │ ├_root.scss
│ │ │ ├_vendor.scss
│ │ │ ├ style.scss
│ ├ index.html
│ ├ README.md
```

### \_root.scss
グリッドやブレイクポイントなど基本設定のSCSS。

### \_global.scss
htmlやbodyなどのグローバルなセレクタの初期設定を記述。

### \_mixin.scss
よく使うmixinをまとめてあります。
個別にMixinを追加する場合はここに追加。

| Mixin | 説明 |
|-----|-----|
| @include max($width); | メディアクエリを書く時に使用します。()には最大ウィンドウ幅を指定します。モバイル用はmax(767)の一つだけで指定可能です。 |
| @include min($width); | メディアクエリを書く時に使用します。()には最小ウィンドウ幅を指定します。 |
| @include and($min-width,$max-width); | メディアクエリを書く時に使用します。引数それぞれにはウィンドウ幅を指定します。 |
| @include clearfix; | クリアフィックスです。 |
| @include position-center($top, $left, $translateX, $translateY); | 親要素にposition: relative;（absolute / fixedも可）を指定して、子要素にこのミックスインを使うと縦横中央に配置されます。|

### \_grid.scss

##### .classベース
最大12分割のグリッドをベースにcontainerとrow、そしてgridのみで組み上げます。
グリッドを使う場合は下記のように記述。


```
<div class="l-container">
    <div class="l-row">
        <div class="l-grid-6">
            <p>.l-grid-6</p>
        </div>
        <div class="l-grid-6">
            <p>.l-grid-6</p>
        </div>
    </div>
</div>
```


カラムを右に寄せる場合は`.l-offset-left-**`をクラス名に付与します。


```
<div class="l-container">
    <div class="l-row">
        <div class="l-grid-7">
            <p>.l-grid-6</p>
        </div>
        <div class="l-grid-4 l-offset-left-1">
            <p>.l-grid-4</p>
        </div>
    </div>
</div>
```

カラムを中央に寄せる場合は`.l-offset-left-**`と`.l-offset-right-**`をクラス名に付与します。

```
<div class="l-container">
    <div class="l-row">
        <div class="l-grid-8 l-offset-left-2 l-offset-right-2">
            <p>.l-grid-8.l-offset-left-2.l-offset-right-2</p>
        </div>
    </div>
</div>
```

インスタグラムのようなタイルレイアウトには`.l-container`は`.l-full`に変更、`.l-grid-*`は`.l-tile-grid-*`にクラス名を変更します。

```
<div class="l-full">
    <div class="l-tile-grid-4">
      <p>.l-tile-grid-4</p>
    </div>
    <div class="l-tile-grid-4">
      <p>.l-tile-grid-4</p>
    </div>
    <div class="l-tile-grid-4">
      <p>.l-tile-grid-4</p>
    </div>
</div>
```

##### ミックスインベースで使う
レスポンシブ対応でグリッドを細かく指定するときはミックスインで指定します。

```
// HTML
<section>
    <article>
        <div>
            <p>l-grid-4 > l-grid-6 > l-grid-12</p>
        </div>
        <div>
            <p>l-grid-4 > l-grid-6 > l-grid-12</p>
        </div>
        <div>
            <p>l-grid-4 > l-grid-6 > l-grid-12</p>
        </div>
        <div>
            <p>l-grid-4 > l-grid-6 > l-grid-12</p>
        </div>
        <div>
            <p>l-grid-4 > l-grid-6 > l-grid-12</p>
        </div>
        <div>
            <p>l-grid-4 > l-grid-6 > l-grid-12</p>
        </div>
    </article>
</section>

// SCSS
section {
    @include l-container;
}

article {
    @include l-row;
}

div {
    @include l-grid(4);

    @include max(767) {
        @include l-grid(6);
    }
}
```

`@include l-grid`と`@include l-tile-grid($tilegrid)`は引数に最大12分割のグリッド指定します。

`@include l-offset-left(n)`、`@include l-offset-right(n)`の2つのミックスインがあります。オフセット数１=グリッド１つ分でマージンを左右にとります。
レスポンシブ対応としてスマートフォンではオフセットが消えるように設定しています。

```
// HTML
<section>
    <article>
        <div>
            <p>grid = 8</p>
        </div>
    </article>
</section>

// SCSS
section {
    @include l-container;
}

article {
    @include l-row;
}

div {
    @include l-grid(12);
}

div {
    @include l-grid(4); // グリッド4
    @include l-offset-left(4); // 左だけオフセット
    @include l-offset-right(6); // 右だけオフセット
}
```

# change log

## 1.1(2018-06-10)
* ファイル構成を大幅に変更しました。
* フォントを変更（*SanFransiscoを指定）

## 1.0(2017-04-01)
* 公開