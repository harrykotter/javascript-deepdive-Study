# 14장 전역 변수의 문제점

## 🧐 변수의 생명 주기

  변수는 선언된 후 할당으로 값을 얻고, 언젠가는 소멸. 지역 변수의 소멸은 해당 변수의 스코프가 끝날 때 소멸된다고 이해하면 편하다.

🙋‍♀️ 왜 갑자기 생명 주기?

변수는 메모리에 할당된 값을 사용하므로 생명이 계속되는 동안 메모리 리소스를 소비한다. 따라서 변수의 생명 주기는 곧 메모리 소비와 직결된다. 자세한 내용은 전역 변수의 단점에서 다뤄보겠다.

Tip. `변수 호이스팅`은 선언된 스코프의 최상단으로 끌어올린다. 즉, 호이스팅은 `스코프 단위`로 이루어진다.

## 🧐 전역 변수의 문제점

### 👉 암묵적 결합

전역 변수는 어디서든 변수를 참조하고 재할당이 가능한데, 이는 의도치 않게 `암묵적 결합`으로 이어질 수 있다. 변수의 유효 범위가 클수록 가독성이 떨어지고 의도치 않게 상태가 변경될 수 있다.

### 👉 긴 생명 주기

앞서 말했듯 생명 주기는 곧 메모리의 소비

전역 변수는 생명 주기가 코드 전체이므로 메모리의 리소스가 오랜 시간 소비된다. 

### 👉 스코프 체인 상에서 종점에 존재

스코프 체인을 통해 상위 스코프를 검색할 때 종점에 존재하므로 변수 검색 속도가 가장 느리다.

### 👉 네임스페이스 오염

JS의 문제점 중 하나로 다른 파일이더라도 같은 전역 스코프를 공유한다는 것이다. 같은 이름으로 정의된 전역 변수, 전역 함수가 있을 시 의도치 않은 오류가 발생할 수 있다.

## ☝ 전역 변수의 사용을 억제하는 방법

### 👉 즉시 실행 함수

단 한 번만 실행하는 즉시 실행 함수를 만들어 전역 변수를 함수의 지역 변수로 바꾼다.

### 👉 네임스페이스 객체

전역에 네임스페이스 역할을 담당할 객체를 만들고, 사용할 변수를 객체의 property로 추가하는 방법

### 👉 모듈 패턴

> 클래스를 모방하여 관련이 있는 변수와 함수를 모아 즉시 실행 함수로 감싸 하나의 모듈을 만드는 것
> 

### 👉 ES6 모듈

파일 자체가 독자적인 모듈 스코프를 사용하도록 script를 추가하는 것

```jsx
<script type="module" src="lib.mjs"></script>
<script type="module" src="app.mjs"></script>
```

🙋‍♀️ Q. 왜 스코프 설정에 있어 변수의 생명 주기가 중요한가?