## 演算子(Operator)とは

レッスン1で演算子については簡単に算術演算子を学びました。算術演算子には数学の考えに似たものが多く含まれているため、理解しやすかったかもしれません。

簡単に算術演算子をおさらいすると、数学の考え方と少し違うところは、文字、つまり文字列や文章を連結させる事ができる事でしょう。

その他レッスン1ではここまで詳しくは言及していませんでしたが、数学で式を「計算する」事を、JavaScriptの演算子では「評価（evaluate）する」と言います。
数学でいう式を計算した結果得られる「計算結果」は、JavaScriptの式を評価した結果でいう、「値（value）をもつ」ことになります。

演算子は値を得るために行うアクション、つまり動作であり、式（値でもあります）を使ってその結果値（式でもあります）をまた得ることができます。
「式と値がイコール」と聞くと混乱しやすいのですが、x + y = 3を例に、x + yの計算結果、つまり値は3な訳ですが、式のx + yも、計算結果の値も3になるので、式も値も同じということになるということです。

## 比較演算子

算術演算子の次に数学に似た演算子が比較演算子です。比較演算子には**_厳密等価演算子_**と**_等価演算子_**の2つがあります。

ただし、数学的考え方と似ていると言っても、一部の内容は新しく理解する必要のある内容になります。

### 厳密等価演算子

よく混乱しやすいのが厳密等価演算子と等価演算子の違いです。
これは数学での考え方をするとどうしても陥りやすいですが、レッスン2で学んだオブジェクトや型（Types）を理解できていればそう難しくはありません。

まず厳密等価演算子ですが、要するに「厳密」とついているだけに同じデータ型（プリミティブ型）である文字列の「2」と、数値の「2」では型が全く同じではないので、比較した結果、`false`が返されるということです。

```js
const literalTwo = '2';
const numberTwo = 2;

console.log(literalTwo === numberTwo); // false
```

厳密等価を調べるには上記のように`===`でも良いですが、`!==`でも良いです。
※　ただし上記の例で`!==`を使用すると、「厳密等価で型がそれぞれ異なる」ということで値は`true`が返されます。

### 等価演算子

対照的に、等価演算子はそこまで厳密に型まで合っていなければ、比較対象はそれぞれ異なるものとはみなしません。
上記の厳密等価演算子の例を等価演算子にして返される値を見ることで、違いがわかります。

```js
const literalTwo = '2';
const numberTwo = 2;

console.log(literalTwo == numberTwo); // true
```

型が文字列と数値で異なっていても、型の違いまでは等価演算子は見ないので、`true`を返します。これは文字列の2が数値の2に暗黙的に変換されているからです。

以下に厳密等価演算子と等価演算子の等しいとみなす比較の基準の違いを表にまとめていますので参考にしてください。
基本は`==`は基本使わないで常に`===`を使うと良いとされています。

| 厳密等価演算子 | 等価演算子 |
| -------- | -------- |
| 同じオブジェクトは等しいとみなす |  同じオブジェクトは等しいとみなす  |
| プリミティブ型で、かつデータ型まで同じであれば等しいとみなす  |  型が違っても同じ値に変換されると等しいとみなす  |

### 関係演算子

関係演算子には `<、>、<=、>=` の4種類あります。
数値や文字列など、比較した時にどちらが大きいかなどと言った順序がわかるデータ型に対して使用できます。

### 特殊な数値

`NaN`という数値がJavaScriptにはあります。
これは「Not a number」という意味で、`NaN`同士でも絶対に等しくなることはありません。
これは厳密等価演算子で比較した結果でも同じです。

これが何の役に立つのかきになるところだと思いますが、一番簡単な例でいうと、変数を数値かどうか確認したい時に使えます。

`NaN`ではなく、`isNaN`という関数を使い、`isNaN(x)`のxが数値でない場合は`true`を返し、それ以外は`false`を返すことができます。

```js
console.log(isNaN(3)); // false
console.log(isNaN('3')); // true
```

## 論理演算子

### 論理値

さて、すでに何度か今までのレッスンでも出てきていますが、true（真）とfalse（偽）という値があります。
これは「論理値」と言って、論理演算子によってのみ扱われる値です。

JavaScriptではどのデータ型も論理演算の対象なので、どの値も真偽のどちらかに分けられるというところが、その他の言語とは少し違います。

以下にtrueと見なされる値と、falseと見なされる値の一覧をまとめています。

| true（真） | false（偽） |
| -------- | -------- |
| undefined | 任意のオブジェクト（valueOf()でfalseを返すものも含む） |
| null | 任意の配列（空配列も含む）  |
| false | 空白スペースだけ含む文字列 |
| 0 | 文字列"false"   |
| NaN |  |
| 空文字列の'' |  |

### 論理演算子：AND OR NOT

ANDとOR、NOTがJavaScriptで取り扱われる論理演算子です。ただしJavaScriptで表記するときはそれぞれ`&&`と`||`と`!`です。

`AND(&&)`と`OR(||)`の違いが初めの頃ははっきり理解しにくいかもしれませんが、要するに語の意味そのままで考えるとわかりやすいです。

比較対象のxとyがあったとして、ANDはxもyも`true`の値でなければ比較結果は`true`にはなりません。れ以外はたとえxかyのどちらかが`true`だったとしても全て結果はfalseです。
英語のANDがxとy両方のことを意味するのと同じですね。

対象的に、ORは英語の意味そのままでxとyどちらかが`true`であれば結果は`true`ですし、当然どちも`true`であれば結果も`true`になります。
falseになるのはどちらもfalseの時だけです。

ではNOTはどうなのでしょうか？
実はNOTの方が単純で、値の結果を反転させるだけです。
つまり`true`は`false`になり、`false`は`true`になるだけです。

```js
const x = true;
const y = false;

console.log(x && y); // false
console.log(x || y); // true
console.log(!x); // false
console.log(!y); // true
```

## グループ化演算子

数学で()で囲まれているところは優先順位が上がるので先に計算するルールがあります。グループ化演算子もこれと同じで、()で囲まれている箇所は、演算子の優先順位を上位に変えます。

例えば以下の例ですと、`a > 7`の比較と、`(a + b === 15 || a - b > 0)`の比較の両方の結果がtrueかどうかの判断をしています。

```js
const a = 8;
const b = 9;
const c = 10;

if (a > 7 && (a + b === 15 || a - b > 0)) {
  console.log('trueが返りました。')
} else {
  console.log('falseが返りました。')
}
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/jb329erw/2/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

## typeof演算子

**_typeof演算子_**は、ある変数の値がどのtypeに属しているのかを返す演算子です。例えば、`undefined`の判定を行うには以下のように書きます。

```js
let i;
console.log(i); // undefined
console.log(typeof i); // undefined
console.log(typeof i === 'undefined'); // true
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/mpqz5ych/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

以下は、**_typeof演算子_**の戻り値一覧です。

| 式 | 戻り値 |
| -------- | -------- |
| typeof undefined | "undefined" |
| typeof true | "boolean" |
| typeof 1 | "number" |
| typeof "" | "string" |
| typeof Symbol() | "symbol"（ES6から追加された） |
| typeof function() {} | "function" |
| typeof {} | "object" |
[ typeof [] | "object" |
| typeof null | "object"（本来ならプリミティブ） |

注意点として、typeof演算子には数十年に渡って残り続けているバグがあります。それは`null`の判断を行うと、`object`という値が返ってきてしまうことです。

```js
let i = null;
console.log(i); // null
console.log(typeof i); // object
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/zg1y6fpn/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

なぜこのバグが残り続けているかというと、JSの歴史は長くこの仕様に依存している既存のアプリケーションがあるため、バグを修正することで新たなバグが生み出されるためです。nullと同じようにobjectという値が返ってくるのはObject型とArray型の2つなのでこの2つを判定したい場合は気をつけましょう。

```js
let person = {name: 'Kei', age: 28 };
// 何かのミスでpersonがnullになってしまったと想定
person = null;

if (typeof person === 'object') { // 
  return person.name; // personはnullなのでエラーが発生する。
}
```

ある変数がnullかどうかの判断をするには以下のようにするのが最も簡単です。

```js
let person = {name: 'Kei', age: 28 };
// 何かのミスでpersonがnullになってしまったと想定
person = null;

if (person) { // personがnullでなければtrueを返す。
  return person.name;
}
```
