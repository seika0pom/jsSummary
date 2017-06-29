JavaScript基礎 3日目

アジェンダ

DOM
イベント
確認テスト
DOM

DOMとは

XMLやXHTML、HTMLのデータをどう表現し使用するかを定めたものです。 DOMは、ツリーへのアクセスを可能にするメソッドを定義し、その結果、ドキュメント構造、スタイル、およびコンテンツを変更できます。 DOMは、さまざまなプロパティとメソッドを持つ、ノードとオブジェクトの構造化されたグループとしてドキュメントの表現を提供します。 その中でも特に使用する機会がある、Documentオブジェクトについて説明します。

Documentオブジェクト

Documentインターフェイスはブラウザーに読み込まれたウェブページを表し、DOMツリーであるウェブページのコンテンツへのエントリーポイントとして働きます。DOMツリーはbodyタグやtableタグなど、多数の要素を持ちます。

alt

alt

要素の検索

要素を検索するには、HTMLタグ内のidやclassまたはタグ自体やCSSセレクタなどで検索することができます。 Documentオブジェクトには要素にアクセスするための便利なメソッドが用意されています。（Document API 情報）

//id指定
document.getElementById('id');

//class指定
document.getElementsByClassName('class');

//タグ指定
document.getElementsByTagName('div');

//cssセレクタで指定
document.querySelector('#main .posts h1'); //最初の一つを取得
document.querySelectorAll('a'); //すべて取得
Elementインターフェースでの要素の検索

Element インターフェイスはDocumentの一部分を表現します。このインターフェイスは個々の種類の要素に共通するメソッドとプロパティを記述するものです。特異な挙動は Element から継承した特異なインターフェイスで記述します。

alt

親子兄弟要素へのアクセスには以下のようにします。（Element API 情報）

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
DOMのアクセスにはコストがかかります。なので、DOMアクセスは最小限まで減らすべきです。 DOMアクセスを減らすとは以下のことです。 - DOMアクセスのループを避ける - DOM参照をローカル変数に代入して、そのローカル変数で作業する - 可能ならばセレクタAPIを利用する - HTMLコレクションを反復処理するときはlengthをキャッシュする

[ 例：DOM参照をローカル変数に代入して、そのローカル変数で作業する ]

// アンチパターン（都度DOMにアクセスしている）
var padding = document.getElementById("result").Style.padding,
    margin = document.getElementById("result").Style.margin

// より良いパターン（親となるDOMを取得してjsの変数としてアクセスする）
var style = document.getElementById("result").style,
    padding = style.padding,
    margin = style.margin;
要素の作成・追加

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
要素の削除

//特定の子要素削除
element.removeChild(child);

//自分を削除
element.parentNode.removeChild(element);

//子要素を全て削除
while (element.firstChild) element.removeChild(element.firstChild);

//子要素を全て削除(part2)
element.textContent = null;
属性の操作

//属性の取得
element.getAttribute('href');

//属性を設定
element.setAttribute('href', 'http://localhost:3000');

//属性を削除
element.removeAttribute('href');
スタイル関連の操作

//class追加
element.classList.add('active');

//class削除
element.classList.remove('active');

//classをトグル
element.classList.toggle('active');

//スタイルを直接指定
element.style.backgroundColor = '#ff0000';
イベント

イベント処理とは

たとえば、Webページのロードやカーソルの移動、テキストエリアへの入力やボタンの押下などブラウザ内で発生するイベントで、JavaScriptはこれに応答することができます。イベントに応じてなにかしらの処理を記述することができます。

イベントリスナーの作成方法

（使用してはいけない）インラインのイベントハンドラ

<form action="#" method="post" onsubmit="validationForm();">
// とか
<a href="somepage.html" onclick="doSomething();">リンク</a>
上記のように、HTMLのコード内に記述する方法をインラインのイベントハンドラといいます。 JavaScript関数をHTML要素のプロパティに割り当てる方法は、すべてのブラウザで確実に実行できる理由からよく見かけられます。 使用してはいけない理由は以下の3つです。

インラインで記述することにより、JavaScriptがHTML内に散在し見た目の悪さやデバッグのしづらさ
HTML内に直接記述されると、プログレッシブエンハンスメントが適用できなくなることがある
JavaScriptが常に機能すると思い込んで、標準的な機能を削いでしまう。
従来のイベントハンドラ

window.onload = init;
一般的なイベントの割り当てとしてよく見かけます。 従来の方法に無名関数を適用すると、関数を宣言する手数がなくなります。

window.onload = function() {
  // ロード時の処理を記載
}
イベントハンドラの削除は、適切なイベントプロパティに対してnullを代入することで実現できます。

window.onload = null;
イベントが設定されているか確認するには、イベントプロパティ値を調べます。

if (typeof window.onload == 'function') {
  // 存在する
}
従来の方法では、ひとつのイベントハンドラしか割り当てられないという欠点があります。

document.getElementById('theForm').onsubmit = validation;
document.getElementById('theForm').onsubmit = calculate;
上記のコードでは２行目のコード以降、フォームの送信時にはcalculate関数だけ呼び出されるようになり、 validation()関数と関連付けられた最初のイベントハンドラは置き換えられてしまいます。

addEventListener()によるイベントハンドラ

var theForm = document.getElementById('theForm');
theForm.addEventListener("click", validation, false);
theForm.addEventListener("click", calculate, false);
addEventListener()関数を用いると、イベントハンドラの上書きはされません。 addEventListener()を利用する利点は以下となります。

イベントに 1 つ以上のハンドラを追加することができます。これは、特に、他のライブラリ/拡張で利用しても上手く動作する必要がある DHTMLライブラリや Mozilla の拡張 のために役立ちます。
リスナーがアクティブ化されたときに、その動きを細かくコントロールすることを可能にします（キャプチャリング 対 バブリング）
HTML 要素だけでなく、任意の DOM 要素 で動作します。
イベントハンドラ一例

onBlur／onFocus

イベントハンドラ	説明
onBlur	ページやフォーム要素からフォーカスが外れた時に発生
onFocus	ページやフォーム要素にフォーカスが当たった時に発生
※ onBlur／onFocusイベントを指定できる要素は、a要素、area要素、label要素、input要素、select要素、textarea要素、button要素のみです。

onChange

イベントハンドラ	説明
onChange	フォーム要素の選択、入力内容が変更された時に発生
※ onChangeイベントを指定できる要素は、input要素、select要素、textarea要素のみです。

onSubmit／onReset

イベントハンドラ	説明
onSubmit	フォームが送信されそうになった時（送信ボタンをクリックした時）に発生
onReset	フォームがリセットされた時に発生
※ onSubmit／onResetイベントを指定できる要素は、form要素のみです。

onClick／onDblClick

イベントハンドラ	説明
onClick	要素やリンクをクリックした時に発生
onDblClick	要素をダブルクリックした時に発生
onKeyPress／onKeyDown／onKeyUp

イベントハンドラ	説明
onKeyPress	押していたキーをあげた時に発生
onKeyDown	キーを押した時に発生
onKeyUp	キーを押してる時に発生
イベントキャプチャとイベントバブリング

イベントにはキャプチャ（捕捉）とバブリング（浮上）という2つのイベントフェーズを通過します。

イベントフェーズとは

イベントが発生すると下記の流れでイベント伝播が発生します。

(キャプチャフェーズ) DOMツリーをたどってルート要素から発生要素を探しに行く
(ターゲットフェーズ) 発生要素を検出する
(バブリングフェーズ) 今度はルート要素まで遡る
alt

このような振る舞いに一体なんの意味があるのでしょうか。 例を見ながら考えてみましょう。

[ 例 ]

<div><h1>ここはタイトル</h1>
  <p>これは段落
    <a href="#" id="link">これはリンク</a>
  </p>
</div>

// link要素にmouseoverイベントを追加
var link = document.getElementById('link');
link.addEventListener("click", pageLoad, false);
上記の例では、マウスがリンクにかかるとページロードされますが、イベントリスナーをlinkではなくdivで設定すると 思っているように動作しないのではと思いますよね。 カーソルがdivに入るとイベント発生タイミングとなりますが、divはp要素とlink要素を持っているため、カーソルがpやlinkの上を通るとdivは有効ではなくるからです。これはイベントターゲットでなくなるということです。しかし、イベントバブリングによって要素を捕らえることができるのでdivのイベントは正しく動作します。このように、ある要素でイベントが起こると、その親要素でもイベントが起こることは便利であり、あるときは邪魔でもあります。 イベントバブリングが邪魔な場合は、stopPropagationによりバブリングをストップされることができます。

イベント処理の委譲

イベント処理の委譲は、イベントリスナーを親要素に割り当て、その子からバブリングしてくるイベントを捕らえる方法です。 委譲を利用すると、複数の要素が同じイベントを持っている状況でパフォーマンスが向上します。

確認テスト

問1

問2
