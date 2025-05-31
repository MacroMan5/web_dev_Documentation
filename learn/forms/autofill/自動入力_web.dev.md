# 自動入力  |  web.dev

**Source URL:** [https://web.dev/learn/forms/autofill?hl=ja](https://web.dev/learn/forms/autofill?hl=ja)  
**Last Updated:** 2025-05-23T01:35:05.065Z  
**Extracted:** 2025-05-31 16:58:10

---

# 自動入力  |  web.dev

自動入力

bookmark\_border コレクションでコンテンツを整理 必要に応じて、コンテンツの保存と分類を行います。 bookmark\_border コレクションでコンテンツを整理 必要に応じて、コンテンツの保存と分類を行います。

10 回目も住所を再入力するのは面倒です。ブラウザ、 デベロッパーは、データをすばやく入力できるようになり、データの再入力を回避できます。 このモジュールでは、自動入力の仕組みと、`autocomplete` などの 要素の属性を使用することで、ブラウザで適切な自動入力オプションを提供できます。

## 自動入力の仕組み

[自動入力の概要](https://web.dev/learn/forms/auto?hl=ja)では、 自動的に入力されます。ではなぜブラウザが自動入力を提供しているのでしょうか。

フォームへの入力は面白くないが、何かできることがある よくあります。そのうちに、多くのフォームに記入して同じデータを入力することがよくあります。 フォームにすばやく入力できるようにする方法の一つは、 フォームのフィールドに以前に入力したデータが自動入力される。これは自動入力です

ブラウザが自動入力するデータを把握する仕組みフォームの例を見る フィールドで確認できます。

```
<label for="name">Name</label>
<input name="name" id="name">
```

このフォーム フィールドを送信すると、その値（入力したデータ）がブラウザに保存されます `name` 属性の値（名前）も付けます。一部のブラウザでは データの保存と入力時に `id` 属性を使用する。

数週間後に、別のウェブサイトで別のフォームに入力したとします。このサイトはまた `name="name"` のフォーム フィールドが含まれています。ブラウザで自動入力をできるようになりました name の値はすでに格納されているためです。

<ph type="x-smartling-placeholder">

自動入力は、登録や ログイン、支払い、購入手続き、フォームに名前やメールアドレスの入力 あります。

適切な自動入力オプションを使用すると、ブラウザで最適な自動入力オプションを利用できるようになります。 `autocomplete` 属性の値。`autocomplete` には多くの値があります。こちらは住所の例です。

  CodePen Embed - Learn forms – autocomplete address  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

ブラウザにすでに住所が保存されていますか？これでGoogle Chat の設定 最初のフィールドを操作すると、ブラウザには 住所のリストを表示します。いずれかを選択すると、ブラウザですべてのフィールドが入力されます 表示されます。自動入力により、フォームにすばやく簡単に入力できます。

住所フォームによって項目は異なり、項目の順序も異なります。 `autocomplete` に正しい値を使用すると、ブラウザでデータが入力されるようになります。 フォームの正しい値を確認します。`country`、`postal-code`、 その他[多数 をご覧ください](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete#values)。

## すばやくログインし、安全なパスワードを使用できるようにする

パスワードを覚えるのが苦手な人はたくさんいます。[最も一般的な パスワード](https://en.wikipedia.org/wiki/List_of_the_most_common_passwords)は 「123456」の後に、覚えやすい他の組み合わせが続きます。どのように セキュリティと固有のパスワードをすべて覚えておく必要はありません。

ブラウザにはパスワード マネージャーが組み込まれており、パスワードを生成、保存、入力できます 自動的に作成されます。ブラウザでのメールの自動入力をサポートする方法をご覧ください パスワードの管理などです

  CodePen Embed - Learn forms – autocomplete sign-up  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

メール フィールドに `autocomplete="email"` を使用して、ユーザーに自動入力が行われるようにする メールアドレスを入力します

これは登録フォームであるため、ユーザーが事前に入力することはできません。 確認できます。`autocomplete="new-password"` を使用すると、ブラウザが 新しいパスワードを生成するオプションが提示されます。

ログイン フォームで `autocomplete="current-password"` を使用して、 以前に保存したこのパスワードの入力オプションが 確認できます

2 要素認証は、多くのウェブサイトで設定できます。このコースでは、 SMS または 2 要素認証アプリでワンタイム コードが送信されます。

SMS メッセージで受け取ったコードが提案されたとしたら、素晴らしいと思います。 できます。また、そのボタンを直接選択して、 ？Safari 14 以降では、 [`autocomplete="one-time-code"`](https://developer.apple.com/documentation/security/password_autofill/enabling_password_autofill_on_an_html_input_element) 必要があります。Android 版 Chrome では、[WebOTP API](https://developer.chrome.com/docs/identity/web-apis/web-otp?hl=ja) を使用して、 使用します。

[SMS OTP フォームを使用してウェブ上で電話番号を確認する方法の詳細 ベスト プラクティス](https://web.dev/articles/sms-otp-form?hl=ja)をご覧ください。

## クレジット カード情報の入力をサポートする

多くの e コマース サイトでは、クレジット カードを使用して商品を購入できます。 サイトでは、独自のフォームを提供する第三者の決済プラットフォームを使用する場合がありますが、 独自の支払いフォームを作成する必要があり 支払い情報を記録します。

再度 `autocomplete` 属性を使用すると、ブラウザが 自動入力のオプションを確認できます

クレジット カード番号 `cc-number`、クレジット カードの有効期限の値があります 日付 `cc-exp`、および[その他すべての情報 必要](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete#values) 選択します

クレジット カード番号や電話番号など、複数の番号をまとめて入力できます ブラウザが自動入力されるようにします。標準のフォーム要素を使用して、 たとえば、カスタム要素ではなく、支払いカードの日付の `<select>` を使用して、 予測入力を利用できるようにすることです

[ユーザーが支払い情報を再度入力しないようにする方法の詳細](https://web.dev/learn/forms/payment?hl=ja#help_users_enter_their_payment_details) 。

## 自動入力がすべてのフィールドで機能することを確認する

住所、アカウント情報、クレジットカード情報のほか、 この他にも、ブラウザで自動入力をサポートするフィールドが多数あります。

フォームに電話番号の入力欄を追加する際には、 [利用可能 値](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete#values) 使用します。フォームのフィールドに適切な値が見つかった場合追加します。

`autocomplete` 属性に適切な値を使用すると、ブラウザで ユーザーがフォームにすばやく入力できるようにすることです。

## フィールドに自動入力すべきでないことをブラウザが認識できるようにする

自動入力の仕組み、ブラウザで自動入力をサポートする方法、およびその理由について学習しました 自動入力を使用すると、ユーザーがフォームに入力する際に便利です。とはいえ、 ブラウザによる自動入力を望まない場合もあります。

```
<label for="one-time-code">One-time code</label>
<input autocomplete="off" type="text" name="one-time-code" id="one-time-code">
```

1 回限りの一意の値を入力するときには自動入力があまり役に立たない たとえば ワンタイムコード欄などです値は毎回異なるため、 値を保存したり、自動入力オプションを提供したりしないでください。次を使用: このようなフィールドに `autocomplete="off"` を追加して、自動入力を防止します。

`autocomplete="off"` のもう 1 つのユースケースとして、ハニーポット フィールドがあります（[前の モジュールを参照](https://web.dev/learn/forms/security-privacy?hl=ja#a_honeypot)）。このフィールドを それ以外のフィールドは自動入力されます。自動入力を有効にしています 「OFF」にすると、実際のユーザーが bot として識別されなくなります。これは、 自動的に完了します。

自動入力は、ユーザーの役に立つことが確実な場合にのみ無効にしてください。

### 理解度をチェックする

自動入力に関する知識をテストする

登録フォームのパスワード欄には、どの予測入力値を使用する必要がありますか。

`autocomplete="new-password"`

`autocomplete="current-password"`

## リソース

*   [予測入力 属性です](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete)。
    *   [お支払いと住所のフォームが最適 プラクティス](https://web.dev/articles/payment-and-address-form-best-practices?hl=ja)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
