# 10장 객체 리터럴

## 객체

<aside>
💡 자바스크립트의 대표적인 데이터 표현 방식으로,0개 이상의 프로퍼티로 구성된 집합으로 표현된다. 객체는 프로퍼티 키(property key)와 프로퍼티 값(value)으로 구성된다.

</aside>

### 👉 객체 리터럴에 의한 객체 생성

 객체 생성 방식 중 가장 일반적이고 간단한 방법으로, 사용하려는 데이터를 그대로 객체 안에 넣으면 된다.

```jsx
let obj = {
	key1: "value1",
	key2: "value2",
	key3: "value3"
};
```

### 👉 프로퍼티와 메서드

> 프로퍼티: 객체의 상태를 나타내는 값이다.

메서드: 프로퍼티를 참조하며 조작할 수 있는 행동으로, 객체의 프로퍼티로써 함수를 뜻한다.
> 

### 👉 프로퍼티 접근

1. 마침표 표기법

```jsx
console.log(obj.key1);
```

1. 대괄호 표기법

```jsx
console.log(obj['key2']);
```

### 👉 프로퍼티 수정

1. 프로퍼티 갱신

```jsx
let person = {
	name: 'Lee'
};

person.name = 'Kim'

console.log(person) // { name: 'Kim' }
```

1. 프로퍼티 동적 생성

```jsx
let person = {
	name: 'Lee'
};

person.age = 20

console.log(person) // { name: 'Lee', age: 20 }
```

1. 프로퍼티 삭제

```jsx
let person = {
	name: 'Lee',
	age: 20
};

delet person.age;

console.log(person) // { name: 'Lee' }
```

### 🧐 ES6에서 추가된 객체 리터럴의 확장 기능 - 참고

- 프로퍼티 축약 표현
- 계산된 프로퍼티 이름
- 메서드 축약 표현