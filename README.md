


# JQueryの読み込み

JavaScriptはそのまま使うこともできるんだけど，WEBでは実は生で使うと結構使いづらい！

 → WEBでは，jQueryっていうJavaScriptを使いやすくするためのライブラリを用いることが多い
 
jQueryを使うためには下の1行をHTMLファイルのheadタグの中のどっかに入れよう！
 
```html
<script src="https://code.jquery.com/jquery-3.4.1.js" integrity="sha256-WpOohJOqMqqyKL9FccASB9O0KwACQJpFTUBLTYOVvVU=" crossorigin="anonymous"></script>
```

# JavaScriptファイルの作成

JavaScriptのプログラムを作るために，まずはプログラムを書くためのJavaScriptファイルとして，index.htmlがあるのと同じフォルダの中に「main.js」というファイルを作ろう！

作ったら，そのファイルをHTMLから読み込むために，下の1行をHTMLファイルのheadタグの中のどっかに入れよう！


```html
<script src="main.js"></script>
```

# 初めてのJavaScript
まずはJavaScriptのファイル内に下のプログラムを書いてみよう

```js

$(() => {
  alert("こんにちは")
})

```

保存したらブラウザでサイトをリロードして，「こんにちは」っていうアラートが表示されたら成功！

- コードの説明

外側に書いた
```js

$(() => {
  
})

```
の部分は，サイトの読み込みが完了してからプログラムを実行するためのコード．
WEBサイトの読み込みが完全に完了する前にプログラムが実行されちゃうと色々不具合が起こる可能性があるから，JavaScriptのプログラムを作ったらまず最初にこれを書いて，この内側にいろんなコードを書いていくようにしよう

今回その中に書いた
```js
alert("こんにちは")
```

は，アラートを表示するためのコード．


# メニューを開く用のボタンを作る

index.htmlのbodyの一番最初に，下のコードを追加．

```html
<div id="menu-button"> </div>
```

そしたら以下のコードをCSSに追加！

```css
#menu-button {
  width: 60px;
  height: 60px;
  background-color: #aaaaaa;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1;
}
```

サイトをリロードすると画面の左上にグレーの四角が出てくるよ．
ボタンのデザインは後々変えていくからとりあえずこれで行こう

# JQueryでクリックの検知

「左上のボタンがクリックされた時にメニューを出す」という機能を実現するために，「○○をクリックしたら△△をする」という機能の作り方を学ぼう！

さっき書いたmain.jsを下のように修正！


```js

$(() => {
  $("#menu-button").click(() => {
    alert("こんにちは")
  })
})
```

これができたら，サイトをリロードして，画面の左上のグレーの四角をクリックしてみよう．クリックした時に「こんにちは」が表示された成功！

- コードの説明


```js

$("#menu-button").click(() => {

})

```

ここの部分が「要素がクリックされた時に何かを実行する」っていうコードだよ！

"#menu-button"っていうところにボタンにしたい要素のIDを入れると，要素のクリックを検知できるよ！例えば，「hogehoge」っていうIDの要素をボタンにしたかったら，


```js

$("#hogehoge").click(() => {

})
```


って書くかんじ！
ということで，今回のコードの内容は，「menu-buttonっていうIDの要素をクリックしたら”こんにちは”っていうアラートを表示する」っていう意味になるよ

# メニューを作る

「ボタンをクリックしたら○○する」が作れるようになったらから，いよいよ「ボタンをクリックしたらメニューを表示する」を実装しよう！でもその前に，HTMLで，表示するメニューを先に作っておこう！

まずはindex.htmlのbodyタグの中の一番上に以下のコードを入力


```html

<div id="menu">
  <a href="#"> メニューだよ </a>
</div>
```


上のコードができたらCSSに下のコードを追加しよう


```css
#menu {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  width: 45%;
  background-color: #717171;
}

#menu-content {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
```


ここまでかけたらブラウザをリロードしてみよう．画面の左側にグレーのメニューが表示されたらOK!メニューの中身は後々実装するから今はとりあえずこれで大丈夫１

でもボタンを押さなくても最初からメニューが開いていると困るから，今書いたCSSを以下のように編集してメニューを非表示にしておこう

```css

#menu {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  width: 45%;
  background-color: #717171;
  display: none;
}

#menu-content {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

```

今書いた「visibility: invisible」は，要素を非表示にできるCSSだよ

# ボタンが押されたらメニューを表示する

メニューのHTMLもできたところで，最後にボタンが押されたらメニューを表示するようにしよう！

main.jsを以下のように編集！


```js

$(() => {
  $("#menu-button").click(() => {
    $("#menu").fadeToggle(500);
  })
})
```

サイトをリロードして左上のボタンをクリックすると，メニューが出てきたり消えたりしたら成功！

- コードの解説

```js

    $("#menu").fadeToggle(500);

```

は，「IDがmenuの要素を表示/非表示する」っていう意味．これを書いたからボタンがクリックされるたびにメニューが出てきたり消えたりするようになった

1000ってところはフェードイン・フェードアウトにかかる時間を指定してるよ．
500だと0.5秒，1000だと1秒，2000だと２秒，みたいな感じで秒数を1000倍した値を入れると，その秒数かけて現れたり消えたりするようになるから色々調節してみてね
．
