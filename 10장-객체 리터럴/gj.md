# 10. 객체 리터럴

## 10.1 객체란?

자바스크립트는 객체 기반의 프로그래밍 언어이며, 원시 값을 제외한 나머지 값은 모두 객체다.

객체 타입은 다양한 타입의 값을 하나의 단위로 구성한 복합적인 자료구조이며, 변경 가능한 값이다.

- 프로퍼티: 객체의 상태를 나타내는 값(data)
- 메서드: 프로퍼티(상태 데이터)를 참조하고 조작할 수 있는 동작(behavior)

## 10.2 객체 리터럴에 의한 객체 생성

자바스크립트는 프로토타입 기반 객체지향 언어로서 다양한 객체 생성 방법을 지원한다.

- 객체 리터럴
- Object 생성자 함수
- 생성자 함수
- Object.create 메서드
- 클래스(es6)

객체 리터럴은 객체를 생성하기 위한 표기법이다.

> > 리터럴: 사람이 이해할 수 있는 문자 또는 약속된 기호를 사용하여 값을 생성하는 표기법

객체 리터럴은 중괄호({}) 내에 0개 이상의 프로퍼티를 정의한다. 변수에 할당되는 시점에자바스크립트 엔진은 객체 리터럴을 해석해 객체를 생성한다.

```javascript
var person = {
  name: "lee",
};
console.log(typeof person); // object
```

## 10.3 프로퍼티

객체는 프로퍼티의 집합이며, 프로퍼티는 키와 값으로 구성된다.

```javascript
var person = {
  name: "lee",
  //프로퍼티 키는 name, 프로퍼티 값은 'lee'
};
```

- 프로퍼티 키: 빈 문자열을 포함하는 모든 문자열 또는 심벌 값
- 프로퍼티 값: 자바스크립트에서 사용할 수 있는 모든 값

식별자 네이밍 규칙을 따르지 않는 프로퍼티 키에는 반드시 따옴표를 사용해야 한다.

키를 동적으로 생성해 사용할 경우에는 대괄호([])로 묶어야 한다.

```javascript
var key = "hi";
var person = {
  firstName: "gildong",
  "last-name": "lee",
  [key]: "hello",
};
```

## 10.4 메서드

메서드는 객체에 묶여있는 함수를 의미한다.

```javascript
var person = {
  sayHi: () => {
    console.log("hi");
  },
};
```

## 10.5 프로퍼티 접근

프로퍼티에 접근하는 방법

- 마침표 프로퍼티 접근 연산자(.)를 사용하는 마침표 표기법
- 대괄호 프로퍼티 접근 연산자([])를 사용하는 대괄호 표기법

프로퍼티 키가 식별자 네이밍 규칙을 준수하는 이름일 경우 두 가지 방법 모두 사용할 수 있으나, 식별자 네이밍 규칙을 준수하지 않는 이름일 경우 대괄효 표기법을 사용해야 한다.

대괄호 표기법을 사용하는 경우 대괄호 프로퍼티 접근 연산자 내부에 지정하는 프로퍼티 키는 반드시 따옴표로 감싼 문자열이어야 한다.

```javascript
var person = {
  firstName: "gildong",
  "last-name": "lee",
};
console.log(person.firstName); //gildong
console.log(person["last-name"]); //lee
```

## 10.6 프로퍼티 값 갱신

이미 존재하는 프로퍼티에 값을 할당하면 프로퍼티 값이 갱신된다.

```javascript
var person = {
  firstName: "gildong",
};
person.firstName = "minsu";
console.log(person.firstName); //minsu
```

## 10.7 프로퍼티 동적 생성

존재하지 않는 프로퍼티에 값을 할당하면 프로퍼티가 동적으로 생성되어 추가되고 프로퍼티 값이 할당된다.

```javascript
var person = {
  firstName: "gildong",
};
person.lastName = "lee";
console.log(person); //{ firstName:'gildong', lastName:'lee'}
```

## 10.8 프로퍼티 삭제

`delete` 연산자는 객체의 프로퍼티를 삭제한다. 만약 존재하지 않는 프로퍼티를 삭제하면 아무런 에러 없이 무시된다.

```javascript
var person = {
  firstName: "gildong",
  age: 30,
};
delete person.age;
delete person.lastName;
console.log(person); //{ firstName:'gildong'}
```

## 10.9 ES6에서 추가된 객체 리터럴의 확장 기능

### 10.9.1 프로퍼티 축약 표현

ES6에서는 프로퍼티 값으로 변수를 사용하는 경우 변수 이름과 프로퍼티 키가 동일한 이름일 때 프로퍼티 키를 생략할 수 있다.

```javascript
let x = 1,
  y = 2;
var obj = {
  x,
  y,
};
console.log(obj); // {x:1, y:2}
```

### 10.9.2 계산된 프로퍼티 이름

ES6에서는 객체 리터럴 내부에서도 계산된 프로퍼티 이름으로 프로퍼티 키를 동적 생성할 수 있다.

```javascript
let x = "test",
  y = 0;
var obj = {
  [`${x}-${++y}`]: y,
  [`${x}-${++y}`]: y,
};
console.log(obj); // { "test-1": 1,"test-2": 2}
```

### 10.9.4 메서드 축약 표현

ES6에서는 메서드를 정의할 때 `function` 키워드를 생략한 축약 표현을 사용할 수 있다.

```javascript
var obj = {
  sayHi() {
    console.log("hi");
  },
};
obj.sayHi(); //hi;
```
