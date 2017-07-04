# Day4

---

## Agenda
1. Validation
2. Exception
3. Ajax
4. 確認テスト

---

## validation

---

### validationとは
<div style="text-align: left;">
データに対する妥当性検査です。
サーバでは常にデータを検証するべきですが、追加のデータ検証を Web ページ自身で行うことにも多くの利点があります。
</div>

---

### ブラウザが提供するフォーム検証
<div style="text-align: left;">
HTML5 の機能のひとつとして、スクリプトに頼ることなくほとんどのユーザデータを検証できます。
</div>

---

#### input要素の検証
<div style="text-align: left;">
すべてのinput要素は、pattern属性を使用して検証することができます。この属性は値として、大文字・小文字を区別した正規表現を想定します。要素の値が空ではなく、また pattern属性で指定された正規表現にマッチしないとき、その要素は不正であるとみなされます。
</div>

---

```HTML
<form>
  <label for="choose">Would you prefer a banana or a cherry?</label>
  <input id="choose" name="i_like" pattern="banana|cherry">
  <button>Submit</button>
</form>
```

<div style="text-align: left;">
このテキストボックスでは、"banana"または"cherry"かブランクしか入力を許しません。
</div>

---

#### required属性

```HTML
<form>
  <label for="choose">Would you prefer a banana or cherry?</label>
  <input id="choose" name="i_like" pattern="banana|cherry" required>
  <button>Submit</button>
</form>
```

<div style="text-align: left;">
required属性を指定したinput要素はフィールドを空にすることができなくなります。つまり、必須で入力してほしい項目に適用する検査となります。
</div>

---

### JavaScriptを使用してフォーム検証する
<div style="text-align: left;">
ネイティブのエラーメッセージを制御したい場合や、HTML5 のフォーム検証をサポートしないブラウザに対処したい場合は、JavaScript を使用するしかありません。
</div>

---

#### HTML5 constraint validation API
API情報：[データフォームの検証](https://developer.mozilla.org/ja/docs/Learn/HTML/Forms/Data_form_validation)

---

<div style="text-align: left;">
独自のエラーメッセージを作成したり、エラー後の挙動を作成する例です。
</div>

```HTML
<form novalidate>
  <p>
    <label for="mail">
      <span>Please enter an email address:</span>
      <input type="email" id="mail" name="mail">
      <span class="error" aria-live="polite"></span>
    </label>
  <p>
  <button>Submit</button>
</form>
```

---

```JavaScript
// DOM ノードの選択法はたくさんあります。ここではフォーム自体、メールアドレス
// 入力ボックス、そしてエラーメッセージを配置する span 要素を取得しています。

var form  = document.getElementsByTagName('form')[0];
var email = document.getElementById('mail');
var error = document.querySelector('.error');

email.addEventListener("keyup", function (event) {
  // ユーザが何かを入力するたびに、メールアドレスのフィールドが妥当かを
  // 確認します。
  if (email.validity.valid) {
    // エラーメッセージを表示している場合に、フィールドが妥当になれば
    // エラーメッセージを取り除きます。
    error.innerHTML = ""; // メッセージの内容物をリセットします
    error.className = "error"; // メッセージの表示状態をリセットします
  }
}, false);
form.addEventListener("submit", function (event) {
  // ユーザがデータを送信しようとするたびに、メールアドレスの
  // フィールドが妥当かをチェックします。
  if (!email.validity.valid) {

    // フィールドが妥当ではない場合、独自のエラーメッセージを
    // 表示します。
    error.innerHTML = "I expect an e-mail, darling!";
    error.className = "error active";
    // また、イベントをキャンセルしてフォームの送信を止めます。
    event.preventDefault();
  }
}, false);
```

---

#### 組み込みAPIを使用しないフォーム検証
完全にオリジナルで検証ロジックを作成することになります。

---

- **どのような検証を実施するべきか?**
<div style="text-align: left;">
どのようにデータを検証するかを決めなければなりません。文字列演算、型変換、正規表現など。これは開発者次第です。フォームのデータは常にテキストであり、スクリプトには常に文字列として渡されることを忘れないようにしてください。
</div>

---

- **フォームが妥当でない場合に何をするべきか?**
<div style="text-align: left;">
これは明らかに UI の問題です。フォームがどのように動作するかを決めなければなりません。 それでもフォームのデータを送信しますか? エラー状態のフィールドを強調しますか? エラーメッセージを表示しますか?
</div>

---

- **ユーザが不正なデータを直すために何をしますか?**
<div style="text-align: left;">
ユーザの不満を軽減する目的で、ユーザが入力内容を直せるよう案内するために、可能な限り役に立つ情報を提供することがとても重要です。明瞭なエラーメッセージはもちろん、ユーザが何を求められているかをわかるように前もって提案するべきです。
フォーム検証 UI の要件について深く学びたいなら、ぜひ読むべきである有用な記事が以下です。
</div>

---

- SmashingMagazine: [Form-Field Validation: The Errors-Only Approach](https://www.smashingmagazine.com/2012/06/form-field-validation-errors-only-approach/)
- SmashingMagazine: [Web Form Validation: Best Practices and Tutorials](https://www.smashingmagazine.com/2009/07/web-form-validation-best-practices-and-tutorials/)
- Six Revision: [Best Practices for Hints and Validation in Web Forms](https://www.webpagefx.com/blog/web-design/best-practices-for-hints-and-validation-in-web-forms/)
- A List Apart: [Inline Validation in Web Forms](http://www.alistapart.com/articles/inline-validation-in-web-forms/)

---

## Exception

---

### try...catch
<div style="text-align: left;">
try 文は、1 つ以上の文を含む try ブロック、および少なくとも 1 つの catch 節、または finally 節、もしくはその両方から成り立っています。すなわち、try 文には 3 つの形式があります。
</div>

- try...catch
- try...finally
- try...catch...finally

---

```JavaScript
try {
  // 通常の処理
} catch (e) {
  // try句の中でエラーが発生した際に実行される処理
}
// try句の中でエラーがなければここの処理を継続
```

---

```JavaScript
try {
  // 通常の処理
} finally {
  // 例外の発生有無に関係なく、try句の処理の後に必ず実行される
}
// finaly句の後にここの処理を継続
```

---

```JavaScript
try {
  // 通常の処理
} catch (e) {
  // try句の中でエラーが発生した際に実行される処理
} finally {
  // 例外の発生有無に関係なく実行
}
```

---

### throw
<div style="text-align: left;">
throw文はユーザ定義の例外を投げることができます。
throw文が実行されると、現在の関数の実行をとめて現在のコンテキスト内のcatchブロックに制御を移します。
</div>

---

```JavaScript
try {
  // 通常の処理
  throw "Error" // catch句に制御が移ります。
  // ここから下の処理は実行されません。
} catch (e) {
  // try句の中でエラーが発生した際に実行される処理
}
```

---

### エラーハンドリング
<div style="text-align: left;">
エラー処理はアプリケーションにとってとても重要な要素です。エラーハンドリングがきちんとされていないコードは
途中で処理を中断してしまうかもしれません。中途半端なデータを作りこみ処理が終わってしまうかもしれません。
逆に不正な状態にも関わらず動き続けてしまうかもしれません。
また、エラーの内容は運用保守にとって重要な情報になります。エラー制御をしっかり設計することは欠かせません。
</div>

---

#### 例外を無視しない/破棄しない
<div style="text-align: left;">
例外は処理実行時に発生した問題を示してくれます。そのため、例外を無視や破棄してしまうと、不正なプログラムやデータなどを検出する機会を失ってしまうとともに、不正な状態のままシステムが動き続けてしまい、二次障害にもつながる可能性があります。
</div>

---
<div style="text-align: left;">
[ 良くない例 ]
</div>

```JavaScript
// 例外を無視して処理を継続している。エラー情報もまともに出力していない
try {
  hoge();
} catch (e) {
  console.log(e.message);
}
```

---

```JavaScript
// エラー情報を握りつぶして別なものにしている
try {
  hoge();
} catch (e) {
  return null;
}
```

---

```JavaScript
// エラーを握りつぶして別なものにしている(part2)
try {
  hoge();
} catch (e) {
  throw "エラー";
}
```

---

これらを解決する策として、次のようなパターンがあります。

---

<div style="text-align: left;">
[ 改善コード ]
</div>

```JavaScript
// エラー情報を詳細にログに出力する。
try {
  if (業務エラー判定) {
    // 業務エラー
    var e = new Error('Malformed input'); // e.name is 'Error'
    e.name = 'ParseError';
    throw e;
  }
} catch (e) {
  console.log(e.toString());
}
```

---

```JavaScript
// 関数内でエラーが発生した場合は、上位の関数に例外処理を委譲する。
try {
  hoge();
} catch (e) {
  throw e;
}
```

---

## Ajax
<div style="text-align: left;">
ajaxとは簡単にいうと、追加的な情報を取得したりサーバサイドの応答を引き起こすためにブラウザのJavaScriptからサーバ要求を出す処理です。Webサーバと非同期通信を行い、DOMを利用してダイナミックにWebページを書き換えることができます。
</div>

---

### 基本
<div style="text-align: left;">
Ajax要求の実行は以下の3つの手順で始まります。
</div>

- Ajaxオブジェクトを作成する
- 要求をだす
- サーバからの応答を処理する

---

#### Ajaxオブジェクトを作成する
<div style="text-align: left;">
ajaxオブジェクトはブラウザによって作成方法が少し異なります。
</div>

---

```JavaScript
var ajax;
if (window.XMLHttpRequest) {
  ajax = new XMLHttpRequest();
} else if (window.ActiveXObject) { // 旧式のIE
  ajax = new ActiveXObject('MSXML2.XMLHTTP.3.0');
}
```

---
### サーバと通信時の処理定義
<div style="text-align: left;">
非同期で処理を行う場合、サーバとの通信状態を監視して、変化したら処理を行うようにします。
</div>

---

```JavaScript
request.onreadystatechange = function() { ... }
```

<div style="text-align: left;">
通信の状態が変化するとWebブラウザはreadystatechangeイベントを発生させます。
</div>

---

```JavaScript
request.onreadystatechange = function() {
    if (request.readyState == 4) {
        if (request.status == 200) {
            // サーバがリクエストを正常に処理できた場合の処理を記述
        }
    }
}
```

<div style="text-align: left;">
HTTPのステータスコードを元に処理を記述します。
</div>

---

### リクエストを送信して通信を開始する
<div style="text-align: left;">
通信時の処理が定義できたら、リクエストを送信します。
リクエストを送信するにはopenメソッドで初期化しsendメソッドで送信します。
</div>

---

```JavaScript
request.open(method, url, [,async [,user [,password]]]);
request.send(null);  // GETメソッドの場合
```

- method・・・HTTPメソッド
- url・・・アクセス先URL
- async・・・非同期通信かどうか（省略可能、初期値true(非同期通信)）
- user・・・認証時のユーザ名
- password・・・認証時のパスワード

---

## 確認テスト

---

問１

---
