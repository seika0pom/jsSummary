# Day2

---

## Agenda
1. オブジェクトとは
2. 関数について
3. 確認テスト

---

## オブジェクトとは

---

<div style="text-align: left;">
オブジェクトはプロパティ（属性ともいう）とメソッド（つまり関数）から構成されています。
</div>

---

### オブジェクトの生成
<div style="text-align: left;">
オブジェクトの生成はnew演算子を利用する方法とリテラルを利用する方法があります。
</div>

```JavaScript
// new演算子を利用する方法
var newObj = new Object();

// リテラルを利用する方法
let newObj = {};
```
---

<div style="text-align: left;">
プロパティを定義して生成する記述
</div>

```JavaScript
var human = {
  name: 'Taro',
  age: 20,
  weight: 50,
  height: 150,
  car:{
    make: 'TOYOTA',
    model: 'アルファード'
  },
  bmi: function(){
    console.log(this.weight / (this.height * this.height));
  }
}
```

---

### プロパティへのアクセス
<div style="text-align: left;">
オブジェクトのプロパティにアクセスする方法は、「オブジェクト名.プロパティ名」で可能です。
また、「オブジェクト名["プロパティ名"]」の2通りあります。
</div>

```JavaScript
// オブジェクト記法
console.log(human.name);  // Taro

// 配列記法
console.log(human["age"]);  // 20
```

---

### プロパティの追加と削除
<div style="text-align: left;">
存在しないプロパティ名のプロパティ値に値を代入すると、プロパティが追加されます。
delete演算子を使用するとプロパティを削除できます。
</div>

```JavaScript
var obj = {};
obj.value = "test";
console.log(obj);  // obj{value: "test"}

delete obj.value;
console.log(obj);  // obj{}
```

---

### 組み込みオブジェクト
<div style="text-align: left;">
これまではオリジナルのオブジェクトを作成してきましたが、JavaScriptには組み込みのオブジェクトが提供されています。
Array、Boolean、Date、Error、Function、Global、JSON、Math、Number、Object、RegExp と String の各オブジェクトです。
</div>

---

```JavaScript
var str = new String("a");
console.log(str.length);  // 1
```

<div style="text-align: left;">
組み込みオブジェクトを使用してオブジェクトを生成する方法です。
※ 基本的に以下のように定義することはありません。
</div>

---

```JavaScript
var str = "a";
console.log(str.length);  // 1
```

<div style="text-align: left;">
JavaScriptではすべてがオブジェクトのように振舞われます。
それはプリミティブ型でもそうです。例をみながら説明します。
</div>

---

```JavaScript
var str = "a";
str.length = 2;
console.log(str.length);  // 1
```

<div style="text-align: left;">
変数strにはプリミティブ型の値が格納されています。
オブジェクト型でないにも関わらず、lenghtプロパティが使用できるのは、strがStringオブジェクトによってラップされているからです。これはプロパティへアクセスするタイミングでのみ発生します。
</div>

---

<div style="text-align: left;">
二行目でプロパティのアクセスが完了しているので値の変更自体は一時的に生成されたオブジェクトに対して行われ、その変更はオブジェクトとともに失われるのでもともとの文字列の長さが表示されます。
</div>

---

## 関数について

---

### 関数とは
関数とは、今まで見てきたように、与えられた入力に対して何らかの処理を行い
その結果を返す仕組みのことを言います。

---

![alt](.\image\JavaScript_5.png)

---

<div style="text-align: left;">
関数には必ず引数を指定する必要もなければ、必ず処理結果を返す必要もありません。
</div>

---

![alt](.\image\JavaScript_6.png)

---

### 関数定義方法
#### 関数定義

```JavaScript
function bmi() {
  return 20;
}
```

<div style="text-align: left;">
関数は関数宣言文によって定義できます。
</div>

---

#### 関数呼び出し

```JavaScript
var humanA = bmi();
console.log(humanA);  // 20
```

<div style="text-align: left;">
定義した関数を呼び出す方法です。
</div>

---

#### 関数宣言文の巻上げ
```JavaScript
console.log(humanA);  // 20
var humanA = bmi();
```

<div style="text-align: left;">
関数宣言文は変数宣言文と同じようにプログラムの先頭に巻き上げられます。
なので、上記のような場合でもエラーとはなりません。
</div>

---

### 値渡しと参照渡し
関数の引数にプリミティブ型を渡す場合とオブジェクトを渡す場合で挙動が異なってきます。

---

<div style="text-align: left;">
[ 例：引数にプリミティブを指定した場合 ]
</div>

```JavaScript
function hoge(a) {return a*a};
var a = 2;
var b = hoge(a);
console.log(a);  // 2
console.log(b);  // 4
```

<div style="text-align: left;">
引数がプリミティブの場合、変数aの値のコピーが関数の引数に代入されます。
なので、元の変数aの値は変更されません。これを値渡しといいます。
</div>

---

<div style="text-align: left;">
[ 例：引数にオブジェクトを指定した場合 ]
</div>

```JavaScript
function huga(p) { p.x++; p.y++; return p;};
var a = {x:3, y:4};
var b = huga(a);
console.log(a,b);  // { x: 4, y: 5 } { x: 4, y: 5 }
```

<div style="text-align: left;">
引数にオブジェクトを指定すると、参照値が引き渡されます。
この場合、変数aと引数pは同じオブジェクトを参照しています。
結果として、p.xやp.yを変更することはa.xやa.yを変更していることと同じです。
これを参照渡しといいます。
</div>

---

### argumentsオブジェクト
```JavaScript
arguments[0] // １番目の実引数の値
arguments[1] // ２番目の実引数の値
arguments[2] // ３番目の実引数の値
```
<div style="text-align: left;">
すべての関数でローカル変数として利用可能。関数が実引数3つで呼び出されたとすると
以下のようにargumentsに値が格納されます。
</div>

---

<div style="text-align: left;">
また、Argumentsにはlengthとcalleeというプロパティがあります。
lengthプロパティは実引数の数が格納されており、calleeプロパティには現在実行中の関数への参照が格納されています。
</div>

---

### スコープチェーン
#### callオブジェクトとローカル変数

<div style="text-align: left;">
関数の呼び出しを行うと、現在実行しているコードの処理は一旦停止し制御が呼び出した関数に移ります。
すると、はじめにローカル変数を格納する変数オブジェクトを生成します。関数コードにおいての変数オブジェクトをcallオブジェクトと言います。callオブジェクトはプログラムからアクセスできません。また、以下のプロパティを持ちます。
</div>

---

- 関数の仮引数
- 関数内の関数宣言文で定義されたローカル変数
- 関数内でvarで宣言されたローカル変数
- arguments
- 呼び出し元の変数オブジェクトへの参照

---

<div style="text-align: left;">
callオブジェクトの生成後はthisの値が決定します。
その後に実際のコードが実行されます。コード実行には、ローカル変数や関数定義などは利用できる状態となっています。
これが変数や関数宣言文の巻上げ（ホイスティング）の正体となります。
</div>

---

#### スコープ
<div style="text-align: left;">
ローカルスコープは関数内でしか生成できません。
</div>

---

### コンテキストとthis
<div style="text-align: left;">
JavaScriptの各コードはそのコードが実行されるコンテキストがあります。
例えば、HTML内にscriptタグを用いて記述したコードについてはグローバルコンテキストで実行されます。
関数本体にあるコードはそれとは異なるコンテキストで実行されます。
コンテキストは関数の処理が終了すると呼び出し元のコンテキストに戻ります。
thisは特殊なオブジェクトで、**呼び出し元** に左右され、実行コンテキストから値を取得します。
</div>

---

<div style="text-align: left;">
[ メソッド呼び出しパターン ]
</div>

```JavaScript
var myObject = {
  value: 10,
  show: function() {
    console.log(this.value);
  }
}
myObject.show(); // 10
```

<div style="text-align: left;">
これは直感的にわかりやすいですね。thisにはmyObjectが入っています。
呼び出し元はオブジェクトなので、thisはそのオブジェクトを参照します。
</div>

---

<div style="text-align: left;">
[ 関数呼び出し ]
</div>

```JavaScript
function show() {
  console.log(this);
  this.value = 1; // 注１
}
show(); // thisはグローバルオブジェクトをさします。
```

<div style="text-align: left;">
オブジェクトに関連づけられない関数の場合は、thisは通常グローバルオブジェクトを参照します。
注１のthisはグローバルオブジェクトを参照するので、valueはグローバル変数となります。
</div>

---

```JavaScript
var myObject = {
  value: 1,
  show: function() {
    console.log(this.value); // 注１

    function show2() {
      console.log(this.value); // 注２
    }
    show();
  }
};
myObject.show();
```

<div style="text-align: left;">
この例では、注1と注2のthisは別なオブジェクトを参照してしまいます。<br >
注1は、myObjectからメソッド呼び出しされるので、thisはmyObjectを参照します。しかし、注2はshowメソッドの中で関数呼び出しされるのでthisはグローバルオブジェクトを参照してしまいます。
</div>

---

```JavaScript
var myObject = {
  value: 1,
  show: function() {
    var self = this;
    console.log(self.value); // 1

    function show() {
      console.log(self.value); // 1
    }
    show();
  }
};
myObject.show();
```

<div style="text-align: left;">
これを解決する方法は、thisを別なプロパティに保持することです。
そのプロパティとしては、「self」「that」などが用いられます。
</div>

---

### コールバック関数
<div style="text-align: left;">
関数はオブジェクトなので、他の関数に引数として渡すことができます。
引数に渡す関数のことをコールバック関数といいます。コールバック関数を実行するタイミングは渡された関数内で決めることができます。
</div>

---

```JavaScript
function writeCode(callback) {
  // 普段通りステートメントを記述できる。
  callback();  // 引数に渡された関数が実行される。
  // 普段通りステートメントを記述できる。
}

function cat () {
  console.log("猫");
}

writeCode(cat);
```

<div style="text-align: left;">
writeCode関数への引数としてcat関数を指定していますが、括弧をつけていません。
これは、cat関数の実行タイミングをwriteCodeに任せるためです。括弧があると関数はそのタイミングで実行されます。
</div>

---

## 確認テスト

---
