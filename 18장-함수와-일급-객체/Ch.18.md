# 18장 함수와 일급 객체

## 🧐 일급 객체 **(First Class Object)**

<aside>
💡 `일급객체(First-class Object)`란 다른 객체들에 일반적으로 적용 가능한 연산을 모두 지원하는 객체를 가리킨다.
[위키백과]

</aside>

특징

- 무명의 리터럴로 생성 가능, 즉 런타임에 생성 가능
- 변수나 자료구조(객체, 배열 등)에 저장할 수 있다.
- 함수의 매개변수에 전달할 수 있다.
- 함수의 반환값으로 사용할 수 있다.

JS에서 함수는 위 사항에 모두 해당되므로 `일급 객체`이다. 다시말해, 함수를 객체와 동일하게 사용할 수 있다는 의미다. 이러한 특성으로 인해 고차함수를 만들 수 있으며, 콜백을 사용할 수 있다.

## ✍ 함수 객체의 프로퍼티

👉 arguments 프로퍼티

 함수 객체의 arguments 프로퍼티 값은 arguments 객체이다. arguments 객체는 인수들의 정보를 담고 있는 순회 가능한(iterable) 유사 배열 객체로, 함수 내부에서 참조가 가능. 단 ES3부터 표준에서 폐지되었으니 Function.arguments는 권장되지 않으며, arguments 객체를 사용하도록 권장

하는데, MDN에선 rest param을 권장하고 있네요

[arguments 객체 - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/arguments)

👉 caller 프로퍼티

자신을 호출하는 함수, ECMASript 사양에 포함되지 않는 비표준 프로퍼티로, 참고만 하자.

👉 length 프로퍼티 - 함수를 정의할 때 선언한 매개변수의 개수

👉 name 프로퍼티 -함수의 이름 프로퍼티 (함수 식별자와 구분할 것!)

👉 __proto__ 접근자 프로퍼티 - `[[Prototype]]` 내부 슬롯이 가리키는 프로토타입 객체에 접근하기 위해 사용하는 접근자 프로퍼티

👉 prototype 프로퍼티 - 생성자 함수로 호출할 수 있는 함수 객체, 즉 constructor만의 고유 프로퍼티

[일급 객체(First Class Object)란?](https://velog.io/@reveloper-1311/일급-객체First-Class-Object란)

🙋‍♀️ 참고 사항(질문 형태)