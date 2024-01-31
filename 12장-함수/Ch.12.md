# 12장 함수

## 함수 (function)

<aside>
💡 일련의 과정을 문(statement)으로 구현하고 코드 블록으로 감싸서 하나의 실행 단위로 정의한 것

</aside>

> 수학에서의 함수가 그러하듯, 프로그래밍에서 함수는 “입력”을 받아 “출력”을 내보낸다.
> 

![images_minj9_6_post_b32dc160-7742-4109-923d-eabd2153fb63_image.png](12%E1%84%8C%E1%85%A1%E1%86%BC%20%E1%84%92%E1%85%A1%E1%86%B7%E1%84%89%E1%85%AE%20ba1dfb7de04540e89434dc67e2fb392d/images_minj9_6_post_b32dc160-7742-4109-923d-eabd2153fb63_image.png)

## 🧐 함수를 사용하는 이유

1. 함수의 재사용
2. 함수 유지 보수의 편의성
3. 코드의 가독성

### 👉 함수 리터럴

```jsx
let f = function add(x, y) {
	return x + y;
};
```

함수 리터럴 구성 요소: 함수 이름, 매개변수 목록, 함수 몸체

## 함수 정의

| 함수 정의 방식 | 예시 |
| --- | --- |
| 함수 선언문 | function add(x, y) {
return x + y;
}; |
| 함수 표현식 | let add = function (x, y) {
return x + y;
}; |
| Function 생성자 함수 | let add = new Function('x', 'y', 'return x + y'); |
| 화살표 함수 () | let add = (x, y) => x + y; |

### 👉 함수 선언문

```jsx
function add(x, y) {
  return x + y;
};

console.dir(add); // f add(x, y)
console.log(add(2, 5)); // 7
```

🙅‍♀️ 함수 리터럴과 동일한 형태지만, 리터럴과 달리 **함수 이름을 생략할 수 없다!**

Why?      함수 선언문 = 표현식이 아닌 문!       함수 리터럴 = 표현식!

| 함수 선언문 | 함수 리터럴 |
| --- | --- |
| 표현식이 아닌 문 (변수에 할당X) | 표현식 (변수에 할당O) |
| 기명 함수 단독으로 사용할 때 | 피연산자로 활용할 때 |
| 함수 이름을 암묵적 식별자로 사용 | 할당하지 않으면 식별자X |

함수는 일급 객체다! (변수에 할당할 수 있는 객체)

### 👉 함수 생성 시점과 호이스팅

```jsx
// 함수 참조
console.dir(add); // f add(x, y)
console.log(sub); // undefined
// 함수 호출
console.log(add(2, 5)); // 7
console.log(sub(2, 5)); // TypeError: sub is not defined
// 함수 선언문
function add(x,y) {
    return x + y;
}
// 함수 표현식
var sub = function (x,y) {
    return x - y;
}
```

```jsx
var sub = function subtract(x,y) {
    return x - y;
}

console.log(subtract(5,3)) // error
console.log(sub(5,3)) // 2
```

🙅‍♀️ 선언문은 정의된 함수 전체가 스코프 앞으로 땡겨지는 `함수 호이스팅`이 발생, 표현식은 변수에 함수를 `할당`하는 형태이므로 `변수 호이스팅`이 발생

### 👉 Function 생성자 함수 (비추천!)

```jsx
let add = (function () {
  var a = 10;
  return new Function('x', 'y', 'return x+y+a');
})();

console.log(add(1,2)); // ReferenceError: a is not defined
```

### 👉 화살표 함수 (26.3절에서!)

## 함수 호출

```jsx
function add(x, y) {
  return x + y;
};

// 함수 호출
let result = add(1, 2);
```

![인수.png](12%E1%84%8C%E1%85%A1%E1%86%BC%20%E1%84%92%E1%85%A1%E1%86%B7%E1%84%89%E1%85%AE%20ba1dfb7de04540e89434dc67e2fb392d/%25EC%259D%25B8%25EC%2588%2598.png)

### *If 주어진 인수의 개수 < 사용한 매개변수의 개수*

전달할 인수가 없는 매개변수는 undefined로 주어진다.
단축평가를 이용해 undefined가 된 매개변수에 기본값을 설정하기도 가능

function add(x, y=2) {

}

### *If 주어진 인수의 개수 > 사용한 매개변수의 개수*

남는 인수는 무시되지만 암묵적으로 arguments 객체에 저장됨 (18.2.1에서 이어서)

🙏 매개변수의 최대 개수는 지정되지 않았으나 가독성, 유지보수를 위해 가급적 적게 (2~3개 이하)

> 주어진 인수의 개수와 매개변수의 개수가 다르더라도 JS는 에러 없이 코드를 출력할 것이다! why?
> 

> JS는 인수와 매개변수의 개수가 일치하는지 확인X
> 

> 동적 타입의 언어기 때문에 매개변수의 타입을 지정X
> 

매개변수가 너무 많으면 객체를 인수로 부여하는 방법도 있다! *property key를 사용하니 가독성도 오른다*

BUT! 함수 외부에서 함수 내부로 전달한 객체가 함수 내부에서 변경되면 함수 외부에서도 변경됨을 주의!

여기카쥐

---

### 👉 참조에 의한 전달과 외부 상태의 변경

```jsx
function changeVal(prim, obj) {
  prim += 100;
  obj.name = 'Kim';
}

let num = 100;
let person = { name: 'Lee' };

changeVal(num, person);
console.log(num); // 100
console.log(person); // 'Kim'
```

![참조.png](12%E1%84%8C%E1%85%A1%E1%86%BC%20%E1%84%92%E1%85%A1%E1%86%B7%E1%84%89%E1%85%AE%20ba1dfb7de04540e89434dc67e2fb392d/%25EC%25B0%25B8%25EC%25A1%25B0.png)

## 여러 함수의 종류

### 👉 즉시 실행 함수

정의하는 동시에 즉시 호출되는 함수, 그리고 사라진다…

```jsx
(function(){
let a = 3;
let b = 3;
return a * b;
}());
```

### 👉 재귀 함수

함수에 자기자신을 호출하는 함수의 형태, 자칫 잘못하면 무한으로 반복될 수 있기 때문에 탈출문 작성에 유념해야한다.

```jsx
function fac(n) {
  if (n <= 1) return 1;
  return n * fac(n - 1);
}

console.log(0); // 0! = 1
console.log(1); // 1! = 1
console.log(2); // 2! = 2
console.log(3); // 3! = 6
```

사실 대부분의 재귀함수는 while이나 if문으로 구현이 가능

### 👉 중첩 함수

함수 내부에서 함수를 선언한 형태

```jsx
function outer() {
  var x = 1;

  function inner() {
    var y = 2;
    console.log(x + y);
  }
  inner();
}
outer();
```

### 👉 콜백 함수 (callback func.)

함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수, 반대로 콜백 함수를 인수로 받은 함수를 고차 함수(higher-order func.)라고 한다.

```jsx
let logOdds = function (i) {
  if (i%2) console.log(i);
};

PaymentRequestUpdateEvent(5, logOdds); // 1 3
```

### 👉 순수 함수, 비순수 함수

### 순수 함수

어떠한 외부 상태에 의존하지 않고 변경하지 않는, 부수효과가 없는 함수

```jsx
let count = 0;

function inc(n) {
  return ++n;
}

count = inc(count);
console.log(count); // 1

count = inc(count);
console.log(count); // 2
```

### 비순수 함수

외부 상태에 의존하거나 외부 상태를 변경하는 부수 효과를 지닌 함수

```jsx
let count = 0;

function inc(n) {
  return ++count;
}

inc();
console.log(count); // 1

inc();
console.log(count); // 2
```

🙋‍♀️ Q. 함수 선언문과 함수 리터럴 표현식의 차이!