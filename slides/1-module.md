# JavaScript の module の変遷

---

## TL;DR

- 色々な変遷があったよ
- 現代では、
  - ES6 Module (import/export) と Node.js の commonJS 形式 (require/export) がよく使われているよ
  - Webpack という module bundler がよく使われているよ

---

## 最初期

- 元々は script tag を HTML にたくさん書いて大量の JS を読み込んでいた
  - 問題:
    - プロトコル的に一度に読み込めるファイルの数に限度がある
    - 全て同じ名前空間
    - a.js と b.js に同じ名前の変数定義があると読み込む順番によって上書きされてしまう
    - ファイル間の依存関係順にスクリプトタグを記述しないといけない
    - 再利用性が低い

---

## IIFE パターン

- 関数の中は scope がある
- 擬似的に private な空間として利用
- 関数の名前が衝突するのを防げる
- 問題:
  - dead code の検出はできない
  - 遅い・重い
  - JavaScript の言語仕様ではない Hack

---

## Node.js の誕生

- サーバーサイド JavaScript
- ブラウザ以外の初の JavaScript の実行環境
- commonJS という require/export を使った module の仕組みを実現！
- npm の誕生
- 問題：
  - commonJS は Node.js 独自の記法だったため、ブラウザの JavaScript では動かない！

---

## Bundler の登場

- Node.js のコードをブラウザで実行可能なものに変換する
- Browserify など
- 問題:
  - bundle された file は読み込みに時間のかかる単一な巨大なファイル
  - 少しコードを修正しただけでも、プロジェクト内の全ての JS を bundle し直す必要があった
  - 全ての module が commonJS 形式で書かれていたわけではなかった
    - IIFE
    - AMD 形式
    - 他にも色々

---

## ECMAScript 6 Module

- ECMAScript はブラウザベンダー各社でバラバラだった JavaScript の振る舞い・仕様を標準化するための基本仕様
- ECMAScript 6 (ES6 / ES2015 とも呼ばれる) で現代の JavaScript の基本となる文法の多くの仕様が策定された
- 以降、毎年 ES2016 / ES2017 のような形で、1 年に 1 度仕様の更新を行っている
- ES6 には Module と呼ばれる import / export を使った module の定義が含まれていた
- ついにブラウザで動く module の仕組みが実現
- 問題:
  - 今まで commonJS 形式で実装されてきた Node.js の資産はどうなる？
  - ブラウザで動く import/export の依存解決はとても遅い

---

## Webpack の登場

- どの環境で実行するか、を指定して bundle できる (ブラウザ向けか、commonJS 向けかなど)
- chunk と呼ばれる単位で bundle を分割できるため、script の読み込みにかかる時間を軽減できる
- 例: トップページで使う JS の chunk / マイページで使う JS の chunk
- 画像 / CSS なども module として解決できる
- JavaScript の中で CSS/画像を import して利用
- plugin で挙動を hack できる
- 問題:
  - Webpack の config が複雑になりすぎる
  - Webpack 職人、という meme
  - 職人の心のこもった webpack.config.js
  - webpack の config の属人化、そして誰も読めなくなる

---

## 最近の bundler 周りの動き

- 複雑な Webpack の config を書かなくとも、zero config で実行環境を作れるようにする動き
  - React.js だと create-react-app / Next.js など
- build の時間を短縮したい
  - :thinking_face: bundler は JavaScript で実装されていなくても良いのでは？
  - rust / go 製の build tool の登場
  - 例: esbuild / swc
