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
<div style="text-align: left;">
JavaScriptの基本はオブジェクトです。
オブジェクトをシンプルに定義すると以下のように記載できます。
</div>

```JavaScript
var obj = {};
```

---

<div style="text-align: left;">
オブジェクトはプロパティの集合です。
プロパティはプロパティ名とプロパティ値の組み合わせです。
</div>

```JavaScript
var obj = {
    key : value
};
```

---

<div style="text-align: left;">
オブジェクトのプロパティには関数を定義することもできます。
これを「メソッド」と呼びます。
</div>

```JavaScript
var obj = {
    key : function () { .. };
};
```

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
