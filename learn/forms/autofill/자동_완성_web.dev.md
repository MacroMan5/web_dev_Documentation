# 자동 완성  |  web.dev

**Source URL:** [https://web.dev/learn/forms/autofill?hl=ko](https://web.dev/learn/forms/autofill?hl=ko)  
**Last Updated:** 2025-05-23T01:35:06.560Z  
**Extracted:** 2025-05-31 16:58:10

---

# 자동 완성  |  web.dev

주소를 열 번째로 다시 입력해야 하는 것은 번거로운 일입니다. 브라우저와 사용자는 은 사용자가 데이터를 더 빠르게 입력하고 데이터 재입력을 방지하는 데 도움이 될 수 있습니다. 이 모듈에서는 자동 완성의 작동 방식과 `autocomplete` 및 기타 요소 속성을 사용하면 브라우저가 적절한 자동 완성 옵션을 제공할 수 있습니다.

## 자동 완성은 어떻게 작동하나요?

[자동 완성 소개](https://web.dev/learn/forms/auto?hl=ko)에서는 자동 완성 그런데 브라우저가 자동 완성을 제공하는 이유는 무엇일까요?

양식 작성은 흥미로운 활동이 아니지만 해야 하는 일입니다. 자주 사용합니다. 시간이 지남에 따라 여러 양식을 작성하게 되고 동일한 데이터를 채우는 경우가 많습니다. 사용자가 양식을 더 빨리 작성하도록 하는 한 가지 방법은 양식 입력란을 자동으로 채웁니다. 바로 자동 완성입니다.

브라우저는 자동 완성할 데이터를 어떻게 알 수 있나요? 예시 양식 살펴보기 필드를 사용하여 확인할 수 있습니다.

```
<label for="name">Name</label>
<input name="name" id="name">
```

이 양식 입력란을 제출하면 브라우저에서 해당 값 (입력한 데이터)을 저장합니다. `name` 속성 (이름)의 값과 함께 사용됩니다. 일부 브라우저는 데이터를 저장하고 채울 때 `id` 속성

몇 주 후에 다른 웹사이트에서 또 다른 양식을 작성한다고 가정해 보겠습니다. 이 사이트는 `name="name"`가 있는 양식 필드가 포함되어 있습니다. 이제 브라우저에서 자동 완성 기능을 이름 값이 이미 저장되어 있기 때문입니다.

<ph type="x-smartling-placeholder">

자동완성은 가입하기, 로그인, 결제, 결제, 양식을 입력할 수 있습니다. 있습니다.

적절한 자동 완성 옵션을 사용하여 브라우저가 최적의 자동 완성 옵션을 제공하도록 할 수 있습니다. `autocomplete` 속성 값입니다. `autocomplete`에는 가능한 여러 값이 있습니다. 이것은 주소의 예입니다.

  CodePen Embed - Learn forms – autocomplete address  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

브라우저에 저장된 주소가 이미 있나요? 좋습니다. 사용자가 주소 양식의 첫 번째 입력란과 상호작용하면 브라우저에 저장된 주소 중 개 하나를 선택할 수 있으며 브라우저에서 모든 필드를 채웁니다. 확인할 수 있습니다. 자동 완성을 사용하면 양식을 빠르고 쉽게 작성할 수 있습니다.

모든 주소 양식의 입력란이 동일한 것은 아니며 입력란 순서도 다릅니다. `autocomplete`에 올바른 값을 사용하면 브라우저가 올바른 값을 찾습니다. `country`, `postal-code`, 그리고 [많은 자세히 알아보기](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete#values)

## 사용자가 빠르게 로그인하고 안전한 비밀번호를 사용할 수 있도록 하기

많은 사람들이 비밀번호를 잘 기억하지 못합니다. [가장 일반적인 비밀번호](https://en.wikipedia.org/wiki/List_of_the_most_common_passwords)가 '123456' 다음에 기억하기 쉬운 다른 조합이 표시됩니다. GCP 콘솔이 안전하고 고유한 비밀번호를 찾을 수 있나요?

브라우저에는 생성, 저장, 입력을 위한 비밀번호 관리자가 내장되어 있습니다. 비밀번호 대신 사용됩니다 이메일 자동 완성으로 브라우저를 지원하는 방법을 알아보세요. 관리할 수 있습니다

  CodePen Embed - Learn forms – autocomplete sign-up  

[![](https://assets.codepen.io/5928893/internal/avatars/users/default.png?fit=crop&format=auto&height=256&version=1616020020&width=256)](https://codepen.io/web-dot-dev)

사용자가 자동 완성 기능을 사용할 수 있도록 이메일 필드에 `autocomplete="email"`를 사용할 수 있습니다. 이메일 주소에 대한 옵션이 있습니다.

가입 양식이므로 사용자에게 이전에 작성할 수 있는 옵션이 표시되지 않습니다. 사용자 인증 정보를 얻을 수 있습니다. `autocomplete="new-password"`를 사용하여 브라우저가 새 비밀번호를 생성하는 옵션을 제공합니다.

로그인 양식에서 `autocomplete="current-password"`를 사용하여 이 기능을 위해 이전에 저장한 비밀번호를 입력하는 옵션을 있습니다.

많은 웹사이트에서 2단계 인증을 설정할 수 있습니다. 'API 약관'의 SMS 또는 2단계 인증 앱으로 일회용 코드가 전송됩니다.

SMS 메시지로 받은 코드가 추천된 경우라면 좋지 않을까요? 키보드로 입력할 수 있고, 키보드로 직접 선택하여 입력 가능한 값은 무엇인가요? Safari 14 이상에서는 [`autocomplete="one-time-code"`](https://developer.apple.com/documentation/security/password_autofill/enabling_password_autofill_on_an_html_input_element) 드림 이러한 목표를 달성할 수 있습니다 Android용 Chrome에서는 [WebOTP API](https://developer.chrome.com/docs/identity/web-apis/web-otp?hl=ko)를 사용하여 JavaScript에서 가능합니다.

[SMS OTP 양식으로 웹에서 전화번호를 확인하는 방법 자세히 알아보기 권장사항](https://web.dev/articles/sms-otp-form?hl=ko)을 참고하세요.

## 사용자가 신용카드 정보를 입력하도록 지원하기

많은 전자상거래 웹사이트에서 신용카드를 사용하여 제품을 구매할 수 있습니다. 사이트에서 자체 양식을 제공하는 서드 파티 결제 플랫폼을 사용할 수 있지만 사용자가 결제 양식을 쉽게 작성할 수 있도록 결제 정보를 제공해야 합니다.

`autocomplete` 속성을 다시 사용하여 브라우저에서 올바른 자동 완성 옵션을 사용할 수 있습니다.

신용카드 번호 `cc-number`, 신용카드 만료에 대한 값이 있습니다. 날짜 `cc-exp` 및 [기타 모든 정보 필요할 때](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete#values) 신용카드 결제의 경우

신용카드 번호 및 전화번호와 같은 숫자에 대해 단일 입력 사용 브라우저가 자동 완성을 제공하도록 합니다. 표준 양식 요소를 사용하세요. 예를 들어 맞춤 요소 대신 결제 카드 날짜에 대한 `<select>`을 사용하여 자동 완성이 사용 가능한지 확인하세요

[사용자의 결제 재입력 방지를 돕는 방법 자세히 알아보기 데이터)](https://web.dev/learn/forms/payment?hl=ko#help_users_enter_their_payment_details)를 참조하세요.

## 모든 필드에서 자동 완성이 작동하는지 확인

주소, 계정 정보 및 신용카드 정보 외에도 브라우저가 사용자의 자동 완성에 도움을 줄 수 있는 더 많은 필드가 있습니다.

양식에 전화번호 입력란을 추가할 때 [사용 가능 값](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete#values) 을 사용합니다. 양식 입력란에 적합한 값을 찾으셨습니까? 추가하세요.

`autocomplete` 속성에 적절한 값을 사용하면 브라우저에서 사용자가 양식을 더 빠르게 작성할 수 있도록 도와줍니다.

## 필드가 자동 완성되면 안 된다는 것을 브라우저가 이해하도록 돕기

자동 완성의 작동 방식과 브라우저의 자동 완성을 지원하는 방법과 그 이유를 알아봤습니다. 자동 완성 을 사용하면 사용자가 양식을 편리하게 작성할 수 있습니다. 하지만 때로는 브라우저가 자동 완성을 제공하지 않도록 할 수 있습니다.

```
<label for="one-time-code">One-time code</label>
<input autocomplete="off" type="text" name="one-time-code" id="one-time-code">
```

일회성의 고유한 값을 입력하는 경우 자동 완성이 도움이 되지 않는 경우가 있습니다. 일회성 코드 입력란 등이 있습니다 이 값은 매번 다르며 브라우저에서 값을 저장하거나 자동 완성 옵션을 제공하지 않아야 합니다. 이때 `autocomplete="off"`: 자동 완성을 방지합니다.

`autocomplete="off"`의 또 다른 사용 사례는 허니팟 필드입니다 ([이전 참고). 모듈](https://web.dev/learn/forms/security-privacy?hl=ko#a_honeypot)). 필드가 브라우저가 나머지 입력란으로 자동 완성할 수 있습니다. 자동 완성 사용 설정 끄면 필드가 너무 많기 때문에 실제 사용자가 봇으로 식별되지 않습니다. 자동으로 완료됩니다

사용자에게 도움이 된다고 확신하는 경우에만 자동 완성을 사용 중지해야 합니다.

### 이해도 확인

자동 완성에 관한 지식 테스트

가입 양식의 비밀번호 입력란에 어떤 자동 완성 값을 사용해야 하나요?

`autocomplete="current-password"`

`autocomplete="new-password"`

## 리소스

*   [자동 완성 속성](https://developer.mozilla.org/docs/Web/HTML/Attributes/autocomplete)을 참조하세요.
    *   [최적의 결제 및 주소 양식 관행](https://web.dev/articles/payment-and-address-form-best-practices?hl=ko)

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
