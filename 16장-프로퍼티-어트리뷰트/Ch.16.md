# 16장 프로퍼티 어트리뷰트

### 내부 슬롯과 내부 메서드란?

<aside>
💡 Js 엔진 구현 알고리즘을 설명하기 위한 ECMAScript 사양에서 사용하는 의사 프로퍼티(pseudo-property), 의사 메소드(pseudo-method). 단, 직접적 접근은 어려운 편이며, 일부 내부 슬롯과 메서드에 한하여 간접적인 접근 수단을 제공한다. (**ex : object.__proto__**)

</aside>

### 👉 프로퍼티 어트리뷰트**와 프로퍼티 디스크립터 객체**

> **프로퍼티 어트리뷰트**
프로퍼티의 상태를 나타내는 속성

**프로퍼티 디스크립터 객체**
프로퍼티 어트리뷰트에 대한 정보를 나타내는 객체
> 

> JS 엔진은 프로퍼티를 생성할 때 프로퍼티의 상태를 나타내는 `프로퍼티 어트리뷰트`를 기본값으로 자동 정의한다.  여기서 `프로퍼티 어트리뷰트`는 `[[Value]]`, `[[Writable]]`, `[[Enumerable]]`, `[[Configurable]]`이다. 프로퍼티 어트리뷰트에 직접 접근은 어려우나 `Object.getOwnPropertyDescriptor` 메서드로 간접적으로 확인할 수 있다.
> 

🙋‍♀️`Object.getOwnPropertyDescriptor` 이 함수는 프로퍼티 디스크립터 객체를 반환함, 존재하지 않는 프로퍼티 or 상속받은 프로퍼티에 대한 프로퍼티 디스크립터를 요구하면 `undefined`가 반환

```jsx
const person = {
  name: 'Lee',
};

console.log(Object.getOwnPropertyDescriptor(person, 'name'));
// {value: 'Lee', writable: true, enumerable: true, configure: true}
```

### 👉 데이터 프로퍼티

 키와 값으로 구성된 일반적인 프로퍼티, 지금까지 살펴본 모든 프로퍼티가 이에 해당된다. 프로퍼티 어트리뷰트는 JS 엔진이 프로퍼티를 생성할 때 기본값으로 자동 정의된다.

| 프로퍼티 어트리뷰트 | 프로퍼티 디스크립터 객체의 프로퍼티 | 설명 |
| --- | --- | --- |
| [[Value]] | value | - 프로퍼티 키를 통한 값 접근 시 반환
- 프로퍼티 값 변경 시 Value에 값을 재할당함 |
| [[Writable]] | writable | - 값의 변경 여부
- false면 읽기 전용으로만 사용 가능 |
| [[Enumerable]] | enumerable | - 열거 가능 여부
- false면 for…in, Object.key 사용 불가 |
| [[Configurable]] | configurable | - 재정의 가능 여부
- false의 경우 삭제, 어트리뷰트 값 변경이 불가, 단 writable이 true면 value 변경과 writable false가 가능 |

### 👉 접근자 프로퍼티

자체적으로는 값을 가지지X, 다른 데이터 프로퍼티 값을 읽거나 저장할 때 호출하는 접근자 함수(accessor function)로 구성된 프로퍼티

| 프로퍼티 어트리뷰트 | 프로퍼티 디스크립터 객체의 프로퍼티 | 설명 |
| --- | --- | --- |
| [[Get]] | get | - 접근자 프로퍼티를 통해 데이터 프로퍼티의 값을 읽을 때 호출되는 접근자 함수
- 접근자 프로퍼티 키로 프로퍼티 값에 접근하면 프로퍼티 어트리뷰[[Get]]]의 값, 즉 getter 함수가 호출되고 그 결과가 프로퍼티 값으로 반환. |
| [[Set]] | set | - 접근자 프로퍼티를 통해 데이터 프로퍼티의 값을 저장할 때 호출되는 접근자 함수
- 접근자 프로퍼티 키로 프로퍼티 값을 저장하면 프로퍼티 어트리뷰[[Set]]]의 값, 즉 setter 함수가 호출되고 그 결과가 프로퍼티 값으로 저장 |
| [[Enumerable]] | go
(가 아니고 enumerable) | - 데이터 프로퍼티의 [[Enumerable]]와 동일 |
| [[Configurable]] | configurable | - 데이터 프로퍼티의 [[Configurable]]와 동일 |

> **프로토타입**
어떤 객체의 상위(부모) 객체의 역할을 하는 객체
프로토타입은 하위 객체(자식)에게 자신의 프로퍼티와 메서드를 상속
상속받은 하위 객체는 자기 것인 양 사용할 수 있다

**프로토타입 체인**
객체들의 위계를 통해 만들어진 객체들의 연결고리. 하위 객체가 사용한 프로퍼티와 메소드의 원본을 프로토타입 체인을 거슬러 찾아간다.
(스코프 체인처럼!)
> 

### 👉 프로퍼티 정의

1. 새로운 프로퍼티를 주가하면서 프로퍼티 어트리뷰트를 명시적으로 정의하는것
2. 기존 프로퍼티의 프로퍼티 어트리뷰트를 재정의 하는 것

 Object.defineProperty 메서드를 이용하여 프로퍼티의 어트리뷰트를 정의할 수 있다. 여러 개를 한 번에 정의할 경우 Object.defineProperties 활용

[Object.defineProperty() - JavaScript | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)

### 👉 객체 변경 방지

객체는 참조형 값이기 때문에 재할당 없이 요소들을 바꿀 수 있음. 
즉, 프로퍼티 추가와 삭제, 프로퍼티 값 갱신, 어트리뷰트 재정의가 가능하다.

| 구분 | 메서드 | 프로퍼티 추가 | 프로퍼티 삭제 | 프로퍼티 값 읽기 | 프로퍼티 값 쓰기 | 프로퍼티 어트리뷰트 재정의 |
| --- | --- | --- | --- | --- | --- | --- |
| 객체 확장 금지 | Object.preventExtensions | X | O | O | O | O |
| 객체 밀봉 | Object.seal | X | X | O | O | X |
| 객체 동결 | Object.freeze | X | X | O | X | X |

> **객체 확장 금지 (Object.preventExtensions)**
객체의 확장을 막는 메서드로, 프로퍼티 동적 추가와 Object.defineProperty의 프로퍼티 추가가 금지된다.
> 

> **객체 밀봉 (seal)**
Object.seal 매서드를 사용해 프로퍼티 추가 및 삭제, 프로퍼티 어트리뷰트 재정을 금지한다. 즉, 프로퍼티의 읽기, 쓰기만 가능하다.
> 

> **객체 동결 (freeze)**
Object.freeze 메서드를 이용해 객체의 모든 수정을 금지, 즉 동결된 객체는 읽기만 가능하다.
> 

> **불변 객체**
객체 동결은 얕은 변경방지만 가능할 뿐, 중첩 객체는 여전히 수정이 가능하다. 따라서 모든 프로퍼티에 대해 재귀적으로 Object.freeze 메서드를 호출해야한다.
> 

🙋‍♀️ 참고 사항(질문 형태)