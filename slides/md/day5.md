# Day5

---

## Agenda
1. Jsフレームワーク
2. JQuery
3. 確認テスト

---

### フレームワークとは
<div style="text-align: left;">
フレームワークとは、プログラミングに必要な特定の機能を持たせようとする枠組みのことです。
</div>

---

### フレームワークの種類

- AngularJS
- Backbone.js
- Ember.js
- Vue.js
- React
- JQuery

---

### AngularJS

![alt](.\image\JavaScript_8.png)


---

<div style="text-align: left;">
クライアント側の JavaScript のコントローラでデータモデルを管理し、画面ビューとリアルタイムでデータを交換するのに適していることが特徴的です。
他にも、モデルとinputフィールドをバインドすることによって、モデル変更やユーザー入力によるフィールド変更など双方向のデータバインディングが可能になります。
</div>

---

### Backbone.js

![alt](.\image\JavaScript_9.png)


---

<div style="text-align: left;">
グローバル変数を排除したり、モデルの保持が可能という特徴を持ちます。
</div>

---


### Ember.js

![alt](.\image\JavaScript_10.png)

---

<div style="text-align: left;">
Web MVCではなくクライアントサイドMVCフレームワークで、コンポーネントやデータバインディングなどの機能を提供しています。そのため、アプリパターンではなく、コンポーネントパターンになります。
</div>

---

### Vue.js

![alt](.\image\JavaScript_11.jpg)

---

<div style="text-align: left;">
双方向データバインディングの実現に特化しています。また、単一ファイルコンポーネント作成のためのツールも提供しています。
</div>

---

### React

![alt](.\image\JavaScript_12.png)

---

<div style="text-align: left;">
UIを構築するためのライブラリで、HTMLとJavaScriptデータバインディング部分に特化している特徴を持ちます。
大規模でも管理しやすく、仮想DOMが高速です。
</div>

---

### JQuery

![alt](.\image\JavaScript_13.png)

---

<div style="text-align: left;">
ウェブブラウザ用のJavaScriptコードをより容易に記述できるようにするために設計された軽量なJavaScriptライブラリ
</div>

---

#### JQueryの基本的な書き方

```JavaScript
$("セレクタ").メソッド(パラメータ);

```

---

```JavaScript
$(document).ready(function(){
  // ここに処理を記述します
});
```

<div style="text-align: left;">
jqueryオブジェクトを作成して、そのオブジェクトに対してメソッドを呼び出すのが基本です。
</div>

---

<div style="text-align: left;">
JQueryオブジェクトのは、**$('セレクタ')** と記述するだけで作成できます。
</div>

---

#### セレクタの書き方

---

```JavaScript
$("#navi")  // idセレクタ
$(".navi")  // クラスセレクタ
$("a img")  // 子孫セレクタ
$("p.warning, p.attention");  // グループセレクタ
```

<div style="text-align: left;">
CSSセレクタエンジンが付いているので簡単にDOMを指定することができます。
</div>

---

```JavaScript
$("li:first")  //一番始めの要素
$("li:last")  //一番最後の要素
$("li:even")  //偶数番目の要素
$("li:odd")  //奇数番目の要素
```

<div style="text-align: left;">
フィルタという仕組みを利用すれば上記のような書き方もできます。
</div>

---

#### メソッドの使い方

<div style="text-align: left;">
メソッドは以下のサイトに利用方法が詳しく記載してあります。
</div>

[jQuery日本語リファレンス](http://semooh.jp/jquery/)

[jQuery](https://jquery.com/)

[githunリポジトリ](https://github.com/jquery/jquery)

---

## 確認テスト

---
