# 11장 원시 값과 객체의 비교

## 원시 값과 객체 타입의 값의 차이

- 원시 타입의 값은 **변경 불가능한 값**, 객체 타입 값은 참조 값, 즉 **변경 가능한 값**
- 원시 값을 변수에 할당하면 변수(확보된 메모리 공간)에는 실제 값이 저장, 반면 객체를 변수에 할당하면 변수(확보된 메모리 공간)에는 참조 값이 저장
- 원시 값을 갖는 변수를 다른 변수에 할당하면 원시 값이 복사, 객체는 참조값이 복사되어 전달

## 🧐 원시 값

### 👉 변경 불가능한 값

🙅‍♀️ 원시값을 할당한 변수는 재할당 이외에 변수 값을  변경할 수 있는 방법이 없다.

### 👉 문자열과 불변성

> ☝ 유사 배열 객체
> 
> 
>     배열처럼 index로 property 값에 접근할 수 있고, length property를 갖는 객체, 따라서 for문으로 순회도 가능하다.
> 

```jsx
let str = 'string';

console.log(str[0]); // s

console.log(str.length); // 6
console.log(str.toUpperCase()); // STRING
```

하지만 배열이 아닌 원시값이므로 변경할 수 없다.

```jsx
 let str = 'string';

str[0] = 'S'
console.log(str); // 여전히 'string'이다
```

### 👉 값에 의한 전달

> 변수(복사본)에 원시 값을 갖는 변수(원본)를 할당하면 변수(복사본)에는 할당되는 변수(원본)의 원시 값이 복사되어 전달된다.
> 

```jsx
let score = 80;
let copy = score;

console.log(score); // 80
console.log(copy);  // 80

score = 100;

console.log(score);  // 100
console.log(copy);  // 80
```

## 🧐 객체

> ☝ JavaScipt의 객체 관리 방식
> 
> 
>     객체는 porperty key를 index로 사용하는 hash table이라고 생각할 수 있다. 대부분 JS엔진은 해시 테이블과 유사하지만 높은 성능을 위해 일반적인 해시 테이블보다 나은 방법으로 객체를 구현한다.
> 

### 👉 변경 가능한 값

객체 타입의 값, 즉 객체는 변경 가능한 값(mutable value)이다.

> ☝ 얕은 복사 (shallow copy)와 깊은 복사 (deep copy)
> 
> 
>     배열처럼 index로 property 값에 접근할 수 있고, length property를 갖는 객체, 따라서 for문으로 순회도 가능하다.
> 

### 👉 참조에 의한 전달

객체를 가리키는 변수(원본)를 다른 변수(사본)에 할당하면 원본의 참조 값이 복사되어 전달된다. 즉, 두 개의 식별자가 하나의 객체를 공유한다는 것이다.

```jsx
let person = {
  name: 'Lee',
};
//  참조값 복사 (얕은 복사)
let copy = person;
console.log(copy === person); // true

copy.name = 'Kim';
person.address = 'Seoul';

console.log(person); // {name: 'Kim', address: 'Seoul'}
console.log(copy); //
```

엄밀히 말하면 객체 또한 식별자가 기억하는 메모리 공간에 저장된 값을 전달하는 것이다. 따라서 JS에서는 “참조에 의한 전달”은 존재하지 않고 “값에 의한 전달”만 존재한다.