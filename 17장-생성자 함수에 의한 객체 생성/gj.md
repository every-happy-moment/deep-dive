# 17. 생성자 함수에 의한 객체 생성

## 17.1 Object 생성자 함수

new 연산자와 함께 Object 생성자 함수를 호출하면 빈 객체를 생성하여 반환한다. 

**생성자 함수**란 연산자와 함께 호출하여 객체(인스턴스)를 생성하는 함수를 말한다. 생성자 함수에 의해 생성된 객체를 **인스턴스**라 한다.
```javascript
const strObj = new String('Lee');
console.log(typeof strObj); //object
console.log(strObj); // String('Lee');

const numObj = new Number(2);
console.log(typeof numObj); //object
console.log(numObj); // Number(2);

const boolObj = new Boolean(true);
console.log(typeof boolObj); //object
console.log(boolObj); // Boolean(true);

const funcObj = new Function('x','return x * x');
console.log(typeof funcObj); //Function
console.log(funcObj); // ƒ anonymous(x) {return x * x}

const arr = new Array(1,2,3);
console.log(typeof arr); //object
console.log(arr); // [1,2,3]

const regExp = new RegExp(2/ab+c/i);
console.log(typeof regExp); //object
console.log(regExp); // /ab+c/i;

const date = new Date();
console.log(typeof date); //object
console.log(date); // Wed Jan 24 2024 20:00:15 GMT+0900 (한국 표준시)
```

## 17.2 생성자 함수
### 17.2.1 객체 리터럴에 의한 객체 생성 방식의 문제점
객체 리터럴에 의한 객체 생성 방식은 단 하나의 객체만 생성한다. 따라서 동일한 프로퍼티를 갖는 객체를 여러개 생성해야 하는 경우 매번 같은 프로퍼티를 기술해야 하기 때문에 비효율적이다.

### 17.2.2 생성자 함수에 의한 객체 생성 방식의 장점
생성자 함수에 의한 객체 생성 방식은 마치 객체를 생성하기 위한 템플릿처럼 생성자 함수를 사용하여 프로퍼티 구조가 동일한 객체 여러개를 간편하게 생성할 수 있다.
```javascript
function Circle(radius){
    this.radius = radius;
    this.getDimeter = function (){
        return 2 * this.radius;
    }
}

const circle1 = new Circle(3);
const circle2 = new Circle(6);
console.log(circle1); // Circle{radius: 3, getDimeter: ƒ}
console.log(circle1.getDimeter()); // 6
```

일반함수와 동일한 방법으로 생성자 함수를 정의하고 new 연산자와 함께 호출하면 해당 함수는 생성자 함수로 동작한다. 만약 new 연산자와 함게 생성자 함수를 호출하지 않으면 생성자 함수가 아니라 일반 함수로 동작한다.
```javascript
function Circle(radius){
    this.radius = radius;
    this.getDimeter = function (){
        return 2 * this.radius;
    }
}

const circle1 = Circle(5);
console.log(circle1); //undefined
console.log(radius); // 3
```

### 17.2.3 생성자 함수의 인스턴스 생성 과정

생성자 함수의 역할을 프로퍼티 구조가 동일한 인스턴스를 생성하기 위한 템플릿(클래스)으로서 동작하여 **인스턴스를 생성**하는 것과 **생성된 인스턴스를 초기화**(인스턴스 프로퍼티 추가 및 초기값 할당)하는 것이다.

1. 인스턴스 생성과 this 바인딩
- 암묵적으로 빈 객체(인스턴스)가 생성된다. 인스턴스는 this에 바인딩 된다. 이 처리는 런타임 이전에 실행된다.
2. 인스턴스 초기화
- 코드가 한줄씩 실행되어 this에 바인딩되어 있는 인스턴스를 초기화 한다.
3. 인스턴스 반환
- 생성자 함수 내부에서 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this를 암묵적으로 반환한다. (만약 this가 아닌 다른 객체를 명시적으로 반환하면 this가 반환되지 못하고 return 문에 명시한 객체가 반환된다. 하지만 원시 값을 반환하면 원시 값 반환은 무시되고 암묵적으로 this가 반환된다.!! return문은 반드시 생략해야한다.)

### 17.2.4 내부 메서드 [[Call]] 과 [[Construct]]
함수가 일반 함수로서 호출되면 내부 메서드 [[Call]]이 호출되고 생성자 함수로서 호출되면 내부 메서드 [[Consttruct]]가 호출된다.
[[Call]]을 갖는 함수 객체를 callable이라 하며, [[Construct]]를 갖는 함수 객체를 constructor, [[Construct]]를 갖지 않는 함수 객체는 non-constructor라고 부른다.

결론적으로 함수 객체는 callable 이면서 constructor이거나 callable이면서 non-constructor이다. 즉, 모든 함수 객체는 호출할수 있지만 모든 함수 객체를 생성자 함수로서 호출할 수 있는 것은 아니다.

### 17.2.5 constructor와 non-constructor의 구분
- constructor: 함수 선언문, 함수 표현식, 클래스
- non-constructor: 메서드(ES 메서드 축약 표현), 화살표 함수

### 17.2.6 new 연산자
new 연산자와 함께 함수를 호출하면 해당 함수는 생성자 함수로 동작한다.(단, new 연산자와 함께 호출하는 함수는 constructor이어야 한다.)

> 생성자 함수는 일반적으로 첫 문자를 대문자로 기술하는 파스칼 케이스로 명명하여 일반함수와 구별할 수 있도록 노력한다.

### 17.2.7 new.target
new.target은 this와 유사하게 constructor인 모든 함수 내부에서 암묵적인 지역 변수와 같이 사용되며 메타 프로퍼티라고 부른다. (IE는 지원하지 않음)

함수 내부에서 new.target을 사용하면 생성자 함수로 호출되었는지 확인할 수 있다. 생성자 함수로서 호출되면 new.target은 함수 자신을 가리키며, 일반 함수로서 호출되면 new.target은 undefined다.

대부분의 빌트인 생성자 함수는 new 연산자와 함께 호출되었는지를 확인한 후 적절한 값을 반환한다.
```javascript
let obj = new Object();
console.log(obj, typeof obj); // {}'object'
obj = Object();
console.log(obj, typeof obj);  // {}'object'

let func = new Function('x','return x * x');
console.log(func, typeof func); // ƒ anonymous(x) {return x * x} 'function'
func = Function('x','return x * x');
console.log(func, typeof func); // ƒ anonymous(x) {return x * x} 'function'

let str = new String('str');
console.log(str, typeof str); // String{'str'} 'object'
str = String('str');
console.log(str, typeof str); // str string

let num = new Number(1);
console.log(num, typeof num); // Number {1} 'object'
num = Number(1);
console.log(num, typeof num); // 1 'number'

let bool = new Boolean(true);
console.log(bool, typeof bool); // Boolean {true} 'object'
bool = Boolean(true);
console.log(bool, typeof bool) // true 'boolean'
```