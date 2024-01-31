# 20장 strict mode

## 🧐 strict mode란?

<aside>
💡 오류를 발생시킬 가능성이 높거나 최적화 작업에 문제를 일으킬 수 있는 코드를 명시적인 에러 메세지를 발생시키는 모드

</aside>

`StrictMode`는 아래와 같은 부분에서 도움이 된다.

- 안전하지 않은 생명주기를 사용하는 컴포넌트 발견
- 레거시 문자열 ref 사용에 대한 경고
- 권장되지 않는 findDOMNode 사용에 대한 경고
- 예상치 못한 부작용 검사
- 레거시 context API 검사
- Ensuring reusable state

[Strict 모드 참고 사이트](https://ko.legacy.reactjs.org/docs/strict-mode.html#:~:text=StrictMode%20%EB%8A%94%20%EC%95%A0%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98%20%EB%82%B4%EC%9D%98%20%EC%9E%A0%EC%9E%AC%EC%A0%81,%EC%99%80%20%EA%B2%BD%EA%B3%A0%EB%A5%BC%20%ED%99%9C%EC%84%B1%ED%99%94%ED%95%A9%EB%8B%88%EB%8B%A4.&text=Strict%20%EB%AA%A8%EB%93%9C%EB%8A%94%20%EA%B0%9C%EB%B0%9C%20%EB%AA%A8%EB%93%9C,%EC%98%81%ED%96%A5%EC%9D%84%20%EB%81%BC%EC%B9%98%EC%A7%80%20%EC%95%8A%EC%8A%B5%EB%8B%88%EB%8B%A4)

ESLint를 포함한 린트 도구들도 비슷한 역할을 수행한다.

### ✍ strict mode의 적용

전역 혹은 함수 몸체의 선두에 ‘use strict;’를 추가
뒤에 ‘use strict;’를 추가하면 적용 X

```jsx
'use strict';

function foo() {
x = 10; // ReferenceError: x is not defined
};
```

### 🙅‍♀️ 전역 strict mode 적용하는 것은 피하자

Why? strict mode 스크립트와 non-strict mode 스크립트의 혼용이 오류를 발생시킬 수 있음!

Why? 외부 서드파티 라이브러리를 사용하는 경우 라이브러리가 no-strict mode인 경우도 있음!

따라서 가능한! *따라해보세요 가능한!* 즉시 실행 함수로 스크립트를 감싸서 선두에 strict mode를 적용하자

[Strict mode - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)

### 🙅‍♀️ 함수 단위로 strict mode를 적용하는 것도 피하자! *아까는 하라며!*

함수에 따라 선택적으로 strict mode의 적용 여부가 다르면 오류를 발생시킬 수 있다! 그렇다고 일일이 strict mode를 주긴 그러고…그리고 함수가 참조한 함수 외부의 컨텍스트에 적용되지 않는다는 문제점이 있다!

따라서 strict mode는 즉시 실행 함수로 감싼 스크립트 단위로 적용하는게 **best!**

## 🧐 strict mode가 잡을 수 있는 에러

### 👉 암묵적 전역 - 선언하지 않는 변수 참조

```jsx
(function () {
  'use strict';

  x = 1;
  console.log(x); // ReferenceError: x is not defined
}());
```

### 👉 변수, 함수, 매개변수의 삭제

```jsx
(function () {
  'use strict';

  var x = 1;
  delete x;
  // SyntaxError: Delete of an unqualified identifier in strict mode.

  function foo(a) {
    delete a;
    // SyntaxError: Delete of an unqualified identifier in strict mode.
  }
  delete foo;
  // SyntaxError: Delete of an unqualified identifier in strict mode.
}());
```

### 👉 매개변수 이름의 중복

```jsx
(function () {
  'use strict';

  //SyntaxError: Duplicate parameter name not allowed in this context
  function foo(x, x) {
    return x + x;
  }
  console.log(foo(1, 2));
}());
```

### 👉 with문의 사용

```jsx
(function () {
  'use strict';

  // SyntaxError: Strict mode code may not include a with statement
  with({ x: 1 }) {
    console.log(x);
  }
}());
```

## 🧐 strict mode 적용에 의한 변화

### 👉 일반 함수의 this

strict mode에서 함수를 일반 함수로 호출하면 `this`에 `undefined`가 바인딩, 이때 에러는 발생하지 않는다.

```jsx
(function () {
  'use strict';

  function foo() {
    console.log(this); // undefined
  }
  foo();

  function Foo() {
    console.log(this); // Foo
  }
  new Foo();
}());
```

### 👉 arguments 객체

```jsx
(function (a) {
  'use strict';
  // 매개변수에 전달된 인수를 재할당하여 변경
  a = 2;

  // 변경된 인수가 arguments 객체에 반영되지 않는다.
  console.log(arguments); // {0: 1, length: 1}
});
```

🙋‍♀️ 참고 사항(질문 형태)