# Day3

---

## Agenda

1. DOM
2. イベント
3. 確認テスト

---

## DOMとは
ドキュメントを制御するAPI

---

<div style="text-align: left;">
 DOMは、ツリーへのアクセスを可能にするメソッドを定義し、その結果、ドキュメント構造、スタイル、およびコンテンツを変更できます。 DOMは、さまざまなプロパティとメソッドを持つ、ノードとオブジェクトの構造化されたグループとしてドキュメントの表現を提供します。
</div>

---

### Documentオブジェクト

<div style="text-align: left;">
Documentインターフェイスはブラウザーに読み込まれたウェブページを表し、DOMツリーであるウェブページのコンテンツへのエントリーポイントとして働きます。DOMツリーはbodyタグやtableタグなど、多数の要素を持ちます。
</div>

---

### 要素の検索

<div style="text-align: left;">
要素を検索するには、HTMLタグ内のidやclassまたはタグ自体やCSSセレクタなどで検索することができます。 Documentオブジェクトには要素にアクセスするための便利なメソッドが用意されています。（Document API 情報）
</div>

---

### Documentインターフェースでの要素の検索

```JavaScript
//id指定
document.getElementById('id');

//class指定
document.getElementsByClassName('class');

//タグ指定
document.getElementsByTagName('div');

//cssセレクタで指定
document.querySelector('#main .posts h1'); //最初の一つを取得
document.querySelectorAll('a'); //すべて取得
```

---

### Elementインターフェースでの要素の検索

<div style="text-align: left;">
Element インターフェイスはDocumentの一部分を表現します。このインターフェイスは個々の種類の要素に共通するメソッドとプロパティを記述するものです。特異な挙動は Element から継承した特異なインターフェイスで記述します。
</div>

---

<div style="text-align: left;">
親子兄弟要素へのアクセスには以下のようにします。（Element API 情報）
</div>

```JavaScript
//親要素
element.parentNode;

//子要素
element.firstElementChild; //最初の子要素
element.lastElementChild;  //最後の子要素
element.children; //子要素リスト

//１つ前の要素
element.previousElementSibling;

//１つ後の要素
element.nextElementSibling;
```

---

<div style="text-align: left;">
DOMのアクセスにはコストがかかります。なので、DOMアクセスは最小限まで減らすべきです。 DOMアクセスを減らすとは以下のことです。
</div>
 - DOMアクセスのループを避ける
 - DOM参照をローカル変数に代入して、そのローカル変数で作業する
 - 可能ならばセレクタAPIを利用する - HTMLコレクションを反復処理するときはlengthをキャッシュする

---

<div style="text-align: left;">
[ 例：DOM参照をローカル変数に代入して、そのローカル変数で作業する ]
</div>

```JavaScript
// アンチパターン（都度DOMにアクセスしている）
var padding = document.getElementById("result").Style.padding,
    margin = document.getElementById("result").Style.margin

// より良いパターン（親となるDOMを取得してjsの変数としてアクセスする）
var style = document.getElementById("result").style,
    padding = style.padding,
    margin = style.margin;
```

---

### 要素の作成・追加

```JavaScript
//要素の作成
var div = document.createElement('div');
div.textContent = 'hoge';

//最後の子要素として追加
element.appendChild(div);

//最初の子要素として追加
element.insertBefore(div, element.firstChild);

//要素の直前に追加
element.parentNode.insertBefore(div, element);

//要素の直後に追加
element.parentNode.insertBefore(div, element.nextSibling);
```

---

### 要素の削除

```JavaScript
//特定の子要素削除
element.removeChild(child);

//自分を削除
element.parentNode.removeChild(element);

//子要素を全て削除
while (element.firstChild) element.removeChild(element.firstChild);

//子要素を全て削除(part2)
element.textContent = null;
```

---

### 属性の操作

```JavaScript
//属性の取得
element.getAttribute('href');

//属性を設定
element.setAttribute('href', 'http://localhost:3000');

//属性を削除
element.removeAttribute('href');
```

---

### スタイル関連の操作

```JavaScript
//class追加
element.classList.add('active');

//class削除
element.classList.remove('active');

//classをトグル
element.classList.toggle('active');

//スタイルを直接指定
element.style.backgroundColor = '#ff0000';
```

---

## イベント

---

### イベント処理

<div style="text-align: left;">
イベント駆動型のプログラムでは、イベントが発生したときに実行する関数を登録しておきます。
イベント時に実行される関数を、**イベントハンドラ** もしくは **イベントリスナ** と言います。
</div>

---

### イベントハンドラの登録方法

---

### HTML要素のイベントハンドラ属性に設定する

```HTML
<!-- 一般的に使用NG -->
<form action="#" method="post" onsubmit="validationForm();">

<a href="somepage.html" onclick="doSomething();">リンク</a>
```

<div style="text-align: left;">
上記のように、HTMLのコード内に記述する方法をインラインのイベントハンドラといいます。 JavaScript関数をHTML要素のプロパティに割り当てる方法は、すべてのブラウザで確実に実行できる理由からよく見かけられます。
</div>

---

特徴と問題点
- インラインで記述することにより、JavaScriptがHTML内に散在し見た目の悪さやデバッグのしづらい
- ある要素のあるイベントに対して、１つのイベントハンドラしか登録できない
- HTML文書の読み込み時にイベントハンドラが設定されるため、簡単に設定できる

---

### DOMの要素オブジェクトのイベントハンドラプロパティに設定する

```JavaScript
var button = document.getElementById("button");
button.onclick = changeColor();
```

<div style="text-align: left;">
一般的なイベントの割り当てとしてよく見かけます。
</div>

---

```JavaScript
button.onclick = function() {
  // クリック時の処理を記述する
}
```

<div style="text-align: left;">
従来の方法に無名関数を適用すると、関数を宣言する手数がなくなります。
</div>

---

```JavaScript
button.onclick = null;
```

<div style="text-align: left;">
イベントハンドラの削除は、適切なイベントプロパティに対してnullを代入することで実現できます。
</div>

---

```JavaScript
if (typeof window.onload == 'function') {
  // 存在する
}
```

<div style="text-align: left;">
イベントが設定されているか確認するには、イベントプロパティ値を調べます。
</div>

---

特徴と問題点
- ある要素のあるイベントに対して、１つのイベントハンドラしか登録できない
- HTMLとJavaScriptプログラムを分離して記述できます。保守性が向上します。
- 同じ要素の同じイベントにイベントハンドラを登録すると、後から登録したもので上書きされてしまう。

---

```JavaScript
document.getElementById('theForm').onsubmit = validation;
document.getElementById('theForm').onsubmit = calculate;
```

<div style="text-align: left;">
上記のコードでは２行目のコード以降、フォームの送信時にはcalculate関数だけ呼び出されるようになり、 validation()関数と関連付けられた最初のイベントハンドラは置き換えられてしまいます。
</div>

---

### addEventListenerメソッドを用いる

<div style="text-align: left;">
addEventListenerメソッドを用いると、同じ要素の同じイベントに複数のイベントハンドラを登録できます。登録された
関数をイベントリスナと言います。
</div>

---

```JavaScript
var theForm = document.getElementById('theForm');
theForm.addEventListener("click", validation, false);
theForm.addEventListener("click", calculate, false);
```

<div style="text-align: left;">
addEventListener()関数を用いると、イベントハンドラの上書きはされません。 addEventListener()を利用する利点は以下となります。
</div>

---

### 書式

```JavaScript
terget.addEventListener(type, listener, useCapture);
```

- **taeget** ・・・イベントリスナを登録する対象であるDOMノード
- **type** ・・・イベントの種類を表す文字列("onclick"など)
- **listener** ・・・イベントが発生したときに処理を行うコールバック関数への参照
- **useCapture** ・・・イベントフェーズ

useCaptureには次のいずれかを指定します。
**true** ・・・キャプチャリングフェーズ
**false** ・・・バブリングフェーズ（省略時の初期値）

---

### イベントキャプチャとイベントバブリング

---

<div style="text-align: left;">
イベントにはキャプチャ（捕捉）とバブリング（浮上）という2つのイベントフェーズを通過します。
</div>

---

### イベントフェーズとは

イベントが発生すると下記の流れでイベント伝播が発生します。

- (キャプチャフェーズ) DOMツリーをたどってルート要素から発生要素を探しに行く
- (ターゲットフェーズ) 発生要素を検出する
- (バブリングフェーズ) 今度はルート要素まで遡る

---

![alt](.\image\JavaScript_7.png)

---

このような振る舞いに一体なんの意味があるのでしょうか。  
例を見ながら考えてみましょう。

---

<div style="text-align: left;">
[ 例 ]
</div>

```HTML
<div><h1>ここはタイトル</h1>
  <p>これは段落
    <a href="#" id="link">これはリンク</a>
  </p>
</div>
```

```JavaScript
// link要素にmouseoverイベントを追加
var link = document.getElementById('link');
link.addEventListener("mouseover", pageLoad, false);
```

---

###イベント処理の委譲

イベント処理の委譲は、イベントリスナーを親要素に割り当て、その子からバブリングしてくるイベントを捕らえる方法です。 委譲を利用すると、複数の要素が同じイベントを持っている状況でパフォーマンスが向上します。

---

確認テスト

問1

問2
