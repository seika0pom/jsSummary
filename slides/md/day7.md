## Day7

---

## Agenda
1. JavaScriptの歴史
2. ES6
3. 確認テスト

---

### JavaScriptの歴史

---

1995年  
<div style="text-align: left;">
Netscape社のブレンダン・アイクが開発
最初はLiveScriptという名前だった。その当時Javaが熱かったので
JavaScriptに名前を改名
</div>

---

1996年  
<div style="text-align: left;">
MicrosoftがIE3.0を発表
IEにJavaScriptを搭載しようとしたが、Netscape社は拒否。
独自に「Jscript」を開発。
JavaScriptと互換性が低く、JavaScriptで作成したスクリプトはIEでは動作せず
JScriptで作成されたスクリプトはNNでは動作しないという状態が発生
</div>

---

<div style="text-align: left;">
同時期にFlashの誕生
Webページ上でのアニメーションやインタラクティブな動作を簡単に実現するFuture Splash Playerというプラグインが誕生
</div>

---

1997年
<div style="text-align: left;">
JscriptとJavaScriptとの互換性を解決しようと標準化がされる。
ECMA-262（初版）が策定される。
</div>

---

2000年代前半
<div style="text-align: left;">
ECMA-262（３版）まで標準化はうまくいったが、４版でうまく行かずなかなか標準化が進まない。
この頃、ECMA Scriptを元にしたAction ScriptがFlashに組み込まれ、
よりFlashの需要が高まり、ネイティブなJavascriptいらないんじゃないかという時代が続く。
</div>

---

2000年代後半
<div style="text-align: left;">
Ajax技術の登場。
2005年、GoogleはJavascriptのAjax技術（非同期通信）を使ったGoogle Mapを発表し世間を驚かす。
Javascriptが見直されJSライブラリも登場する。
2005年にはprototype.js、2010年にはJQueryが出てきてよりリッチな表現が可能となる。
</div>

---

2010年以降
<div style="text-align: left;">
サーバーサイドのJavascript環境であるNode.jsが登場し，
それまで，ブラウザでしか動かせないというJavascriptの常識を一気に覆す。
JSフレームワークも続々登場する。
</div>

---

2015年
<div style="text-align: left;">
ECMA-262（第６版）が策定される。
</div>

---

<div style="text-align: left;">
ということで、ES6について軽く説明します。
</div>

---

### ES6 (ECMAScript 2015)

---

#### letによるブロックスコープ
letを使用することで関数スコープではなく、ブロックスコープを実現できます。

---

```JavaScript
// Before
if (true) {
  var num = 1;
}

console.log(num); // 1

// After
if (true) {
  let num = 1;
}

console.log(num); // エラー
```

---

#### constによる定数の宣言

---

```JavaScript
const NUM = 1;
NUM = 2;   // エラー
```

<div style="text-align: left;">
定数を変更しようとするともちろんエラーとなります。
しかし、オブジェクトや配列はプロパティの変更ができてしまいます。
</div>

---

```JavaScript
// 直接変更は不可
const NUM_LIST = [1, 2, 3];
NUM_LIST = [5, 5, 5];   // エラー

// プロパティの変更は可能
const NUM_LIST = [1, 2, 3];
NUM_LIST[0] = 5;

console.log(NUM_LIST);   // [5, 2, 3]
```

---

#### テンプレート文字列

---

<div style="text-align: left;">Before</div>
```JavaScript
// 普通の文字列は「'」シングルクォート
var str = 'あ\nい\nう';

console.log(str);
/**
 * あ
 * い
 * う
 */
```

---

<div style="text-align: left;">After</div>
```JavaScript
// テンプレート文字列は「`」バッククォート
var str = `あ
い
う`;

console.log(str);
/**
 * あ
 * い
 * う
 */
```
「\n」を使用しなくても改行可能

---

変数の文字列への埋め込み

<div style="text-align: left;">Before</div>
```JavaScript
var name = '太郎';
var age = 23;

var str = '私の名前は' + name + 'です。' + age + '歳です';

console.log(str); // 私の名前は太郎です。23歳です
```

---

<div style="text-align: left;">After</div>
```JavaScript
var name = '太郎';
var age = 23;

var str = `私の名前は${name}です。${age}歳です`;

console.log(str); // 私の名前は太郎です。23歳です
```

---

#### 分割代入
分割代入により、一度に複数の変数に複数の値を代入することができます。

---

<div style="text-align: left;">Before</div>
```JavaScript
var name = '太郎';
var age  = 23;

console.log(name, age)   // 太郎 23
```

---

<div style="text-align: left;">After</div>
```JavaScript
var [name, age] = ['太郎', 23];

console.log(name, age)   // 太郎 23
```

---

分割代入による値の入れ替え

<div style="text-align: left;">Before</div>
```JavaScript
var num1 = 10;
var num2 = 20;

console.log(num1, num2) // 10 20

// 値の入れ替え
var tmp = num1;
num1 = num2;
num2 = tmp;

console.log(num1, num2) // 20 10
```

---

<div style="text-align: left;">After</div>
```JavaScript
var num1 = 10;
var num2 = 20;

console.log(num1, num2); // 10 20

// 値の入れ替えは一行
[num1, num2] = [num2, num1];

console.log(num1, num2); // 20 10
```

---

<div style="text-align: left;">
関数の引数で初期化
</div>

---

<div style="text-align: left;">Before</div>
```JavaScript
function show(name) {
  // nameがundefinedなら
  if (name === void 0) {
    name = 'タロウ';
  }

  console.log(name);
}

show();           // タロウ
show('太郎');   // 太郎
```

---

<div style="text-align: left;">After</div>
```JavaScript
function show(name = 'タロウ') {
  console.log(name);
}

show();           // タロウ
show('太郎');   // 太郎
```

---

### 確認テスト

---
