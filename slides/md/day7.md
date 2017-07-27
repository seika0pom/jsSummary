## Day7

---

## Agenda
1. JavaScriptの歴史
2. ES6

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
この頃、ECMA Scriptを元にしたAction ScriptがFlashに組み込まれ，
よりFlashの需要が高まり，ネイティブなJavascriptいらないんじゃないかという時代が続く。
</div>

---

2000年代後半
<div style="text-align: left;">
Ajax技術の登場
2005年，Googleは，JavascriptのAjax技術（非同期通信）を使ったGoogle Mapを発表し世間を驚かす。
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
