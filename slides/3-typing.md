# 型付けの変遷

---

## :thinking_face: 型って何？

- string / number / boolean などの、データの種類
- 例:
  - true は boolean 型
  - 1 は number 型
- 動的型付け言語と静的型付け言語がある
  - 動的: 変数・関数・クラスの定義時に、型を明示的に宣言しない
    - Ruby/JavaScript など
  - 静的: 変数・関数・クラスの定義時に、型を明示的に宣言しなければならない
    - C++/Go/Java など
- Web フロントエンドのリッチ化・Node.js でサーバーサイド JavaScript の考えかたが登場したことにより、JavaScript アプリケーションは大規模化・複雑化していった
  - JavaScript の動的型はあまり信用できなかった
    - 1 == ‘1’
    - true = ‘1’
    - undefined == null
  - :thinking_face: 既存の JavaScript のコードに少しずつ足していける、静的型つけのような型検査の仕組みがほしい...!

---

## TypeScript の登場

- JavaScript の文法はそのままに、型を追加した JavaScript の superset
- build 時に JavaScript に変換する
- どのぐらい型の検査を厳しくするかは config で設定できる
  - 0 ⇒ 1 なので厳しい config にしたり
  - JavaScript で数年開発した project に後から TypeScript を入れるのでゆるい config にしたり
  - (余談) React.js では、React.propTypes ⇒ flowtyped ⇒ TypeScript のように型付けのでデファクトが変化していったが、今回は割愛
