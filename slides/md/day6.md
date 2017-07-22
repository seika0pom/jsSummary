# Day6

---

## Agenda
1. オブジェクト
2. プロトタイプベース
3. 即時関数
4. クロージャ/無形関数
5. 確認テスト

---

### オブジェクト

---

```JavaScript
var obj = {};
```

<div style="text-align: left;">
JavaScriptの基本はオブジェクトです。
オブジェクトをシンプルに定義すると以下のように記載できます。
</div>

---

```JavaScript
var obj = {
    key : value
};
```

<div style="text-align: left;">
オブジェクトはプロパティの集合です。
プロパティはプロパティ名とプロパティ値の組み合わせです。
</div>

---

```JavaScript
var obj = {
    key : function () { .. };
};
```

<div style="text-align: left;">
オブジェクトのプロパティには関数を定義することもできます。
これを「メソッド」と呼びます。
</div>

---

### プロトタイプベース

---

クラスという概念はありますが、他の言語と仕組みが異なります。

---

![alt](.\image\JavaScript_14.png)

---

![alt](.\image\JavaScript_15.png)

---

```JavaScript
var　humanA = {
  weight = 60;
  height = 1.75;
  bmi: function() {
    console.log(“bmi is ”)
    console.log(this.weight / (this.height * this.height));
  }
};

var humanB = { weight: 50, height: 1.5 };
humanB.__proto__ = humanA;

var humanC = {};
humanC.__proto__ = humanB;

humanC.bmi();
// ⇒bmi is 22.2

```
<div style="text-align: left;">
humanCにはプロパティを設定していませんがbmiは表示されます。
</div>

---

<div style="text-align: left;">
各オブジェクトは__proto__を介して連鎖的に参照しています。
bmiが表示できたのは、humanCオブジェクトがhumanAオブジェクトまでの参照があるからです。
</div>

---

<div style="text-align: left;">
bmiが表示されるまでの軌跡
</div>

```JavaScript
// humanC.bmi()メソッドコール
humanC.bmi  // プロパティなし

humanC.__proto__.bmi  // プロパティなし

humanC.__proto__.__proto__.bmi // プロパティあり
```

---

<div style="text-align: left;">
bmiが表示されるまでの軌跡
</div>

```JavaScript
// humanC.weight属性の参照
humanC.weight  // プロパティなし

humanC.__proto__.weight  // プロパティあり

humanC.__proto__.__proto__.weight // プロパティあるが使用しない
```

---

```JavaScript
object.__proto__.__proto__.property
```
<div style="text-align: left;">
自分にない機能や属性を__proto__の参照する別なオブジェクトを
遡って検索する仕組みを **プロトタイプチェーン** と言います。
</div>

---

```JavaScript
humanA.__proto__ = otherObj;
```

<div style="text-align: left;">
実際には上記のような記載はしません。オブジェクトを生成する際はコンストラクタ関数を
一般的に使用します。
</div>

---

```JavaScript
// コンストラクタ関数定義
var　Human = function(weight, height) {
  this.weight = weight;
  this.height = height;
};

// prototypeの拡張
Human.prototype.bmi = function() {
  console.log(“bmi is ”)
  console.log(this.weight / (this.height * this.height));
}

// 利用
var tom = new HumanA(50, 150);
```

---

### 即時関数

---

<div style="text-align: left;">
即時関数は現在のスコープを汚染せずに新たなスコープを作成するための手段です。
</div>

---

```JavaScript
//即時関数の構文その１
(function () {
    //関数の中身・・・
}());

//即時関数の構文その２
(function () {
    //関数の中身・・・
})();
```

---

アンチパターン１

```JavaScript
// 関数を使わない場合
var bmi = 0;

// 一時的な変数だがグローバルに宣言しているので予期せぬ動きを引き起こす可能性がある
a = 50;
b = 1.5;

bmi = a / (b * b);

console.log(bmi);  // 22.2
```

---

アンチパターン２

```JavaScript
// 名前付き関数を使用する場合
var bmi = 0;

// パターン１よりいいが先ほどの問題は完全に解決されていない
calcBmi = function() {
  var a = 50,
      b = 1.5;

  return a / (b * b)
}
bmi = calcBmi();
console.log(bmi);  // 22.2
```

---

```JavaScript
// 即時関数を使用する場合
(function () {

    var bmi = function() {
      var a = 50;
      var b = 1.5;
      return a / (b * b);
    };
    console.log("bmi is " + bmi());
　  // bmi is 22.2....
}());
```

---

### クロージャ

---
