# Day 1

---

## Agenda
1. JavaScriptとは
2. JavaScriptの実行環境
3. コーディング規約
4. 変数
5. データ型
6. 演算
7. 制御構文
8. 確認テスト  

---

## JavaScriptとは

---

<div style="text-align: left;">
WEB上でインタラクティブな表現をする為に開発されたオブジェクト指向のスクリプト言語
</div>
<br>

![alt](.\image\JavaScript_1.gif)

---

### JavaScriptってどこで動いている？

---

![alt](.\image\JavaScript_2.jpg)

---

<div style="text-align: left;">
JavaScriptはサーバからレスポンスとして受け取られ、クライアント側で実行されます。
実行時に機械語に翻訳されながら処理が行われます。これをインタプリター言語といいます。
JavaScriptはインタープリター言語です。また、JavaScriptはシングルスレッドで処理を実行します。
</div>

---

### ブラウザによる挙動の変化

---

![alt](.\image\JavaScript_3.jpg)

---

<div style="text-align: left;">
JavaScriptはクライアントで実行すると言いましたが、実行しているエンジンは各ブラウザにて異なります。
ブラウザの種類やバージョンによって動作に影響があるため、利用するブラウザを意識してコードを書く必要があります。
コードは、ブラウザが何であるかではなく、ブラウザができることに基づいて記述します。
</div>

---

### JavaScriptを記述する場所

---

<div style="text-align: left;">
JavaScriptはHTML内に記述する方法と、  
拡張子を「.js」とする外部ファイルとして記述する方法の２種類あります。
</div>
![alt](.\image\JavaScript_4.gif)

---

```html
<!-- HTML内に記述する方法 -->
<html>
  <head>
    <title>HELL WORLD</title>
  </head>
  <body>
    <script type="text/javascript">
	document.writeln('HELL javascript');
    </script>
  </body>
</html>
```

---

```html
<!-- 外部ファイルにする場合 -->
<html>
  <head>
    <title>HELL WORLD</title>
    <script type="text/javascript" src="test.js"></script>
  </head>
  <body>
    <input type="button" value="OK" onclick="testFunction();">
  </body>
</html>
```

```javascript
// 外部ファイル
testFunction(){
  // ここに処理
}
```

---

## JavaScriptの実行環境

---

JavaScriptはWebコンソールやNode.jsで間単に実行して動作を確認することができます。実演します。

---

## コーディング規約

---

<div style="text-align: left;">
JavaScriptのコーディング規約にはメジャーな以下２つがあります。
規約はプロジェクトやチーム単位でも細かく決めてある場合があるので、チームの人に確認してみてください。
</div>

[Google JavaScript Style Guide](https://google.github.io/styleguide/javascriptguide.xml "Google JavaScript Style Guide")

[Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript "Airbnb JavaScript Style Guide")

---

## 変 数

---

```JavaScript
var a;
let b;
const c;
```
```JavaScript
var a;
console.log(a);  // undefined
```
<div style="text-align: left;">
このステートメントによってa,b,cという名前のついた変数の領域がメモリに作成されます。  
varやletやconstのことを宣言子といいます。変数を宣言しただけの状態では、変数には「undefiend」という値が入っています。
</div>

---

```JavaScript
var a;
a = "test";

var b = 1;

var c = 1,
    d = 2,
    e = 3;
```
<div style="text-align: left;">
変数にはイコール演算子を使って値を代入することができます。また、変数の宣言と同時に値を代入することもできます。複数の変数をカンマ区切りに宣言することも可能です。
</div>

---

### 変数宣言の省略

---

```JavaScript
console.log(a);  // 参照エラー
```
<div style="text-align: left;">
宣言されていない変数を参照しようとすると参照エラーとなります。
</div>

---

```JavaScript
a = 1;
console.log(a);  // 1
```
<div style="text-align: left;">
こっちはエラーになりません。
これは宣言を省略して値を代入すると自動でグローバル変数となってしまうからです。
グローバル変数をむやみに利用するのは良くありません。
<div>

---

#### ホイスティング

---

```JavaScript
console.log(a);  // undefined
var a;
```
<div style="text-align: left;">
上記のコードは変数aを宣言する前に参照しようとしているので、エラーとなりそうですが、
結果は「undefined」となります。
これは変数宣言がプログラムの途中で行われても、あたかも先頭で宣言されたかのように振舞うからです。
これを変数宣言の巻上げ（ホイスティング）といいます。
</div>

---

```JavaScript
console.log(x);  // undefined
var x = "Hello";
console.log(x);  // "Hello"
```

ただし、初期化の部分は巻き上げられません。

---

#### スコープ

---

```JavaScript
var a = "global";
function hoge() {
  var b = "local";
  console.log(a);  // グローバル変数なのアクセスできる。
  return b
}
hoge();
console.log(b);  // bは関数hogeのローカル変数なので、関数外からアクセスできない。
```

<div style="text-align: left;">
JavaScriptは構文のみでスコープが決まってしまいます。これをレキシカルスコープといいます。
スコープにはグローバルとローカルがあります。
それぞれ、グローバルが関数の外側で宣言された変数で、有効範囲は全体です。どこからでもアクセスできます。
ローカルは関数内で宣言された変数で、有効範囲は関数内のみです。
</div>

---

```JavaScript
var a = "global";
function hoge() {
  var a = "local";
  console.log(a);  // "local"
  return a
}
hoge();
console.log(a);  // "global"
```
<div style="text-align: left;">
変数名が衝突した場合、ローカル変数が有効となります。
</div>

---

## データ型

---

<div style="text-align: left;">
データの種類はプリミティブ型とオブジェクト型の２種類あります。  
**プリミティブ型**  
  数値、文字列、論理値、null、undefined、シンボル  
**オブジェクト型**  
  プリミティブ型以外の全て
</div>

---

## 式と演算
### 算術二項演算子

| 演算子     | 意味         | 例           | 例の意味               |
|:-----------|:------------|:-------------|:----------------------|
| +          | 加算        | a + b        | aとbを足した値         |
| -          | 減算        | a - b        | aとbを引いた値         |
| *          | 乗算        | a * b        | aとbをかけた値         |
| /          | 除算        | a / b        | aとbを割った値         |
| %          | 剰余算      | a % b        | aをbで割った余りの値    |

---

```JavaScript
1 + 2       //  3
1 + "2"     // "12" ←文字列
1 + "Hello" // "1Hello"

1 * "2"       //  NaN
True + True   //  2
1 + null      //  1
1 + undefined //  NaN
```

- +演算子はオペランドの片方でも文字列の場合は、文字列の結合となります。
- 計算不能な場合はNaNとなる。
- 論理値のTrueは１、Falseは０に評価される。
- nullは0に評価される。
- undefinedはNaNとして評価される。

---

### 算術三項演算子
<div style="text-align: left;">
条件 (三項) 演算子は JavaScript では唯一の、3 つのオペランドをとる演算子です。この演算子は、if 文のショートカットとしてよく用いられます。
</div>

---

```JavaScript
// if文で書いた場合
var money = 10000;
if (money > 5000) {
  console.log(“お金持ち”);
} else {
  console.log(“貧乏”);
}

// 上記を三項演算子で記載した場合
var money = 10000;
money > 5000 ? console.log(“お金持ち”) : console.log(“貧乏”);
```

---

### 算術単項演算子

---

| 演算子         | 意味           | 例           | 例の意味                                       |
|:---------------|:--------------|:-------------|:----------------------------------------------|
| ++             | インクリメント | ++a          | aの値を1増やし、その後でaの値を評価する。         |
|                |               | a++          | aの値を評価し、その後でaの値を1増やす            |

+++

| 演算子         | 意味           | 例           | 例の意味                                       |
|:---------------|:--------------|:-------------|:----------------------------------------------|
| --             | デクリメント   | --a          | aの値を1減らし、その後でaの値を評価する。         |
|                |               | a--          | aの値を評価し、その後でaの値を1減らす            |

---

### 算術代入演算子

| 演算子         | 例           | 例の意味     |
|:---------------|:------------|:-------------|
| +=             | a += b      | a = a + b    |
| -=             | a -= b      | a = a - b    |
| \*=            |  a \*= b    | a = a \* b   |
| /=             | a /= b      | a = a / b    |
| %=             | a %= b      | a = a % b    |

---

### 論理演算子と関係演算子
#### 等価演算子（==）同値演算子（===）
<div style="text-align: left;">
等価演算子は値が等しいかどうかを判断します。同値演算子は値と型が等しいかを判断します。
比較するデータがプリミティブ型かオブジェクトかでも評価が異なってきます。
比較時の左右のオペランドの型が異なる場合は以下のように評価します。（暗黙の型変換）
</div>

---

- undefinedとnullは等しい
- 一方が数値、もう一方が文字列の場合、文字列を数値に変換して比較
- 一方が論理値の場合、trueなら１に、falseなら０に変換して比較
- 一方がオブジェクトで、もう一方が数値か文字列の場合、オブジェクトをプリミティブ型に変換して比較
- 上記以外は全て「等しくない」

---

[ 等価演算 ]
等価演算では上記の暗黙の型変換によって、すべてtrueと評価されてしまいます。
```JavaScript
null == undefined  // true
"1" == 1           // true
true == 1          // true
true == "1"        // true
2 == [2]           // true
```

---

[ 同値演算 ]
同値演算では型と値を比較するので暗黙の型変換は行われません。
```JavaScript
null === undefined  // false
"1" === 1           // false
true === 1          // false
true === "1"        // false
2 === [2]           // false
```

---

**※ 注意**
```JavaScript
NaN === NaN  // false
```
<div style="text-align: left;">
NaNは自分自身も含めてすべての値と比較して等しくないと評価されます。
</div>

---

#### 論理演算子

| 演算子         | 例                | 例の意味                                            |
|---------------|-------------------|----------------------------------------------------|
| &&            | a && b            | aとbの両方がtrueの時はtrue、それ以外はfalse           |
| &#124;&#124;  | a &#124;&#124; b  | aとbのいずれかがtrueの時はtrue、両方falseの時はfalse  |
| !             | !a                | aがtrueの時はfalse、aがfalseの時はtrue               |

---

#### オペランドの短絡評価
<div style="text-align: left;">
オペランドは論理値である必要はありません。論理値でない場合は、以下のように型変換されます。
０、-０、ブランク（""）、NaN、null、undefinedは **false** に変換される。
０以外の数値、ブランク以外の文字列、オブジェクト、シンボルは **true** に変換される。
</div>

---

<div style="text-align: left;">
論理積と論理和は **短絡評価** を行います。
短絡評価とは、第一オペランドの値でその式の値が決まる時、第二のオペランドを **評価しない** ことです。
また、評価後は論理値を返却するのではなく、**最後に評価したオペランドの値** を返します。
この特性を利用して以下のような使い方とかよく見ます。
</div>

```JavaScript
var player = name || member.name || "Taro";
```

---

## 制御命令

---

### if条件
if条件は処理の分岐にしようします。

<div style="text-align: left;">
[ 基本シンタックス ]
</div>
```JavaScript
if ("条件") {
  // 条件がtrueの場合、ここの複数のステートメントを実行
}
```

---

<div style="text-align: left;">
**true** とは何か
trueとはfalse以外のすべてです。
JavaScriptでは、以下の値は条件内でfalseと評価されます。
</div>

- false
- NaN
- 0
- null
- 空のストリング(""や'')
- undefined

---

<div style="text-align: left;">
条件を連続して記載したい場合は以下のように記載します。
</div>

```JavaScript
if ("条件1") {
  // 条件1がtrueの場合、ここの複数のステートメントを実行
} else if ("条件2") {
  // 条件2がtrueの場合、ここの複数のステートメントを実行
} else {
  // 条件1、条件2がfalseの場合、ここの複数のステートメントを実行
}
```

---

### switch条件
<div style="text-align: left;">
switch条件も処理の分岐に使用しますが、ifで if-elseを延々と記載するよりも
明快で読みやすいコードがかけます。
</div>

---

<div style="text-align: left;">
[ 基本シンタックス ]
</div>
```JavaScript
var expression = 0,
    result = '';

switch(expression){
case 0:
  result = "zero";
  break;
case 1:
  result = "one";
  break;
default:
  result = "unknown";
}
console.log(result);  // zero
```

---

<div style="text-align: left;">
switch条件で気をつける点は、caseの最後はきちんとbreakしてあげることです。
breakを省略した場合、次のcaseを満たすかどうかに関係なく、次のcase内のステートメントが実行されます。
</div>

---

```JavaScript
var expression = 0,
    result = '';

switch(expression){
case 0:
  result = "zero";
  console.log(result);  // breakがないので、次のcase1内を実行してしまう。
case 1:
  result = "one";
  console.log(result);
  break;
default:
  result = "unknown";
}
// 実行結果は以下
// zero
// one
```

---

<div style="text-align: left;">
上記の特性は複数の条件を記述する際に利用することもできます。
</div>

---

```JavaScript
var expression = 0,
    result = '';

switch(expression){
case 0:
case 1:
  console.log("0でも1でもここを表示")
  break;
default:
  result = "unknown";
}
// 実行結果は以下
// 0でも1でもここを表示
```

---

### forループ
for文は繰り返しの処理を記述する際に利用します。

<div style="text-align: left;">
[ 基本シンタックス ]
</div>
```JavaScript
for ( 最初の式; 条件; 後の式) {
  // ここに繰り返し行いたい処理を記載する。
}
```

---

<div style="text-align: left;">
繰り返しの度に後の式を評価し、条件を満たすまで繰り返します。
条件を満たす場合は、ループ処理を抜けます。


[ 例：配列の中身をすべて表示する ]
</div>
```JavaScript
var array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
for (var i = 0; i < array.length; i++) {
  console.log(array[i]);
}
```

---

<div style="text-align: left;">
上記の例は、実は最適化されていません。
その理由は、ループの繰り返しごとに配列の長さがアクセスされる点です。
これによって処理がおそくなってしまいます。
これを解消するには次のように記載します。
</div>

---

```JavaScript
var array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
for (var i = 0, max = array.length; i < max; i++) {
  console.log(array[i]);
}
```

---

## コメント
<div style="text-align: left;">
JavaScriptの構文内に必要に応じてコメントを記載することができます。
コメントの記載方法は以下です。
</div>

```JavaScript
// この行すべてがコメント

/*
この間に記載すればコメントになるよ。
改行も、もちろんできるよ。

*/
```

---

## 確認テスト

---

### 問1
<div style="text-align: left;">
"test.js"という名前のJSファイルをhtmlに読み込む際のscriptタグを書け。
</div>

---

### 問2
<div style="text-align: left;">
以下JavaScriptコードを実行した際、最後に出力される x, y の値はそれぞれいくつか。
</div>

```JavaScript
var x = 0;
var y = 0;

if( 0 == ++y )
{
	++x;
}
else if( 1 == x++ )
{
	y++;
}

console.log( x );
console.log( y );
```

---

### 問3
次の3つの数値の比較を答えよ。

```JavaScript
1 === 1.0
1 === '1'
1 == '1'
```

---

### 問4
下記の２つのコード出力結果を答えよ

```JavaScript
// ①
var n = 10;
while (n < 1) {
    document.writeln(n);
    n++;
}

// ②
var m = 10;
do {
    document.writeln(m);
    m++;
} while (m < 1) ;
```
