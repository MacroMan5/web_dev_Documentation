# 自動填入  |  web.dev

**Source URL:** [https://web.dev/learn/forms/autofill?hl=zh-tw](https://web.dev/learn/forms/autofill?hl=zh-tw)  
**Last Updated:** 2025-05-23T01:34:47.764Z  
**Extracted:** 2025-05-31 16:58:10

---

# 自動填入  |  web.dev

在第 10 次中，您必須重新輸入地址，瀏覽器 開發人員可藉此加快輸入資料的速度，避免重新輸入資料。 本單元將說明自動填入功能的運作方式，以及 `autocomplete` 和其他方面的運作方式 元素屬性可確保瀏覽器提供適當的自動填入選項。

## 自動填入功能如何運作？

您已在[自動填入簡介](https://web.dev/learn/forms/auto?hl=zh-tw)中，瞭解 自動填入。不過，瀏覽器為什麼提供自動填入功能？

填寫表單不是有趣的活動，但你仍須完成 經常更新。您已填寫多份表單，且通常會填寫相同的資料。 如要協助使用者加快表單填寫速度，其中一個方法就是提供使用者選擇 自動將先前輸入的資料填入表單欄位。這是自動填入功能。

瀏覽器如何得知要自動填入哪些資料？查看範例表單 \] 欄位加以確認。

```
<label for="name">Name</label>
<input name="name" id="name">
```

如果您提交這個表單欄位，瀏覽器會儲存值 (您輸入的資料) 以及 `name` 屬性的值 (name)。有些瀏覽器也會考量 `id` 屬性 (用於儲存及填入資料)。

假設幾週後，您在另一個網站上填寫了其他表單。也在這個網站 包含表單欄位，其中含有 `name="name"`。你的瀏覽器現在可以提供自動填入功能 因為 name 值已經儲存。

自動填入功能在常用的表單內 (例如註冊 登入、付款、結帳，以及輸入姓名或 讓我們看看 DNS 解析 進一步探索內部和外部位址

您可以使用適當的 `autocomplete` 屬性的值。`autocomplete` 的值有很多種。以下是地址的範例。

  CodePen Embed - Learn forms – autocomplete address  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

您的瀏覽器是否已為您儲存地址？太好了！之後 與地址表單的第一個欄位互動時，瀏覽器會顯示一份清單 。您可以選擇其中一項，瀏覽器會自動填入所有欄位 與特定地址相關的資訊自動填入功能讓表單填寫過程快速又簡單。

並非所有地址表單都有相同的欄位，且欄位的順序也不盡相同。 為 `autocomplete` 使用正確的值，可確保瀏覽器填入資訊 正確的表單值有 `country`、`postal-code`、 和[許多 瞭解詳情](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete#values)。

## 確保使用者可以快速登入，並使用安全的密碼

許多人不擅長記住密碼。最常見的 [密碼](https://en.wikipedia.org/wiki/List_of_the_most_common_passwords)是 「123456」，後面加上其他易於記住的組合。運用方式 安全又獨特的密碼，卻無法牢記嗎？

瀏覽器內建密碼管理工具，可產生、儲存及填入密碼 而非密碼瞭解如何協助瀏覽器自動填入電子郵件 以及管理密碼

  CodePen Embed - Learn forms – autocomplete sign-up  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

您可以使用 `autocomplete="email"` 做為電子郵件欄位，讓使用者取得自動填入功能 代表電子郵件地址

由於這是註冊表單，因此使用者不應看到先前填寫內容的選項 或密碼您可以使用 `autocomplete="new-password"` 確保瀏覽器 提供產生新密碼的選項。

在登入表單中，您可以使用 `autocomplete="current-password"` 提供下列資訊 瀏覽器可以讓您選擇是否要填入先前儲存的密碼 網站。

您可以為許多網站設定雙重驗證功能。除了 密碼、動態驗證碼會透過簡訊或雙重驗證應用程式傳送。

如果系統提供簡訊中的驗證碼，那就太棒了 即可直接選取該鍵盤來填入 值呢？在 Safari 14 以上版本中，你可以透過 [`autocomplete="one-time-code"`](https://developer.apple.com/documentation/security/password_autofill/enabling_password_autofill_on_an_html_input_element)敬上 。在 Android 版 Chrome 中，您可以使用 [WebOTP API](https://developer.chrome.com/docs/identity/web-apis/web-otp?hl=zh-tw) 實現 這應該和 JavaScript 有關

進一步瞭解如何使用[簡訊動態密碼表單驗證網頁電話號碼 最佳做法](https://web.dev/articles/sms-otp-form?hl=zh-tw)

## 協助使用者填寫信用卡資訊

你可以在許多電子商務網站上使用信用卡購買商品。 網站可以使用自行提供表單的第三方付款平台，前提是 你必須先建立自己的付款方式 確保使用者能輕鬆填妥你的資訊 付款資訊。

您可以再次使用 `autocomplete` 屬性，確保瀏覽器提供 正確的自動填入選項

信用卡有 `cc-number` 的數值，信用卡到期 日期 `cc-exp`，和[所有其他資訊 需求](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete#values) 信用卡付款。

使用單一輸入號碼輸入信用卡號碼，例如信用卡號碼和電話號碼 ，以確保瀏覽器提供自動填入功能。請使用標準表單元素， 例如將付款卡日期的 `<select>` (而非自訂元素) 設為 確保自動完成功能可供使用

進一步瞭解如何[協助使用者不必重新輸入付款 資料](https://web.dev/learn/forms/payment?hl=zh-tw#help_users_enter_their_payment_details)。

## 確保自動填入功能適用於所有欄位

除了地址、帳戶資訊和信用卡資訊以外， 瀏覽器可透過自動填入功能為使用者提供更多欄位。

在表單中加入電話欄位時，您是否可以使用任一 [可購買 價值](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete#values) 自動完成功能。已為表單欄位找到合適的值嗎？新增資料。

為 `autocomplete` 屬性使用合適的值有助於瀏覽器提供 可以幫助使用者更快填寫表單。

## 協助瀏覽器瞭解不應自動填入欄位

你已瞭解自動填入功能的運作方式、如何協助瀏覽器使用自動填入功能，以及這麼做的原因 自動填入功能可讓使用者輕鬆填寫表單。有時您 因為您不希望瀏覽器提供自動填入功能。

```
<label for="one-time-code">One-time code</label>
<input autocomplete="off" type="text" name="one-time-code" id="one-time-code">
```

自動填入功能沒幫助的地方 就是輸入一次性的專屬值 例如一次性代碼欄位每次這個值都不同，且 瀏覽器不應儲存值或提供自動填入選項。別擔心！您可以使用 `autocomplete="off"` 適用於這類欄位，以防止自動填入。

`autocomplete="off"` 的另一個用途是 Honeypot 欄位 (請參閱[先前 模組](https://web.dev/learn/forms/security-privacy?hl=zh-tw#a_honeypot))。雖然這個欄位 顯示，瀏覽器可能會自動填入資訊以及其他欄位。正在啟用自動填入功能 關閉後，使用者就不會因為輸入 自動完成作業

除非您確定自動填入功能可協助使用者，再停用自動填入功能。

### 隨堂測驗

測試你對自動填入功能的瞭解程度

你該在註冊表單的密碼欄位輸入哪個自動完成值？

`autocomplete="new-password"`

`autocomplete="current-password"`

## 資源

*   [自動完成功能 屬性](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete)。
    *   [付款和地址表單最好 做法](https://web.dev/articles/payment-and-address-form-best-practices?hl=zh-tw)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
