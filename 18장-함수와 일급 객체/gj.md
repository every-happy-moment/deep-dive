# 18. 함수와 일급 객체 

## 18.1 일급 객체
다음과 같은 조건을 만족하는 객체를 **일급 객체**라 한다.
- 무명의 리터럴로 생성할 수 있다. 즉, 런타임에 생성이 가능하다.
- 변수나 자료구조(객체, 배열 등)에 저장할 수 있다.
- 함수의 매개변수에 전달할 수 있다.
- 함수의 반환값으로 사용할 수 있다.
```javascript
// 1번, 2번 만족
const increase = function(num){
    return ++num;
} 
// 2번 만족
const auxs = { increase };

// 3번, 4번 만족
function makeCounter(aux){
    let num = 0;
    return function (){
        num = aux(num);
        return num;
    }
}

// 3번 만족
const increaser = makeCounter(auxs.increase());
console.log(increaser()); //1
```

함수가 일급 객체라는 것은 함수를 객체와 동일하게 사용할 수 있다는 의미다. 일급 객체로서 함수가 가지는 가장 큰 특징은 함수의 매개변수에 전달할 수 있으며, 함수의 반환값으로 사용할 수 있다는 것이다. 

함수는 객체이지만 일반 객체와는 차이가 있다. 일반 객체는 호출할 수 없지만 함수 객체는 호출할 수 있다. 그리고 함수 객체는 일반 객체에는 없는 함수 고유의 프로퍼티를 소유한다.

## 18.2 함수 객체의 프로퍼티

### 18.2.1 arguments 프로퍼티
arguments 프로퍼티 값은 arguments 객체다. arguments 객체는 함수 호출 시 전달된 인수들의 정보를 담고 있는 순회 가능한 유사 배열 객체이며, 함수 내부에서 지역 변수처럼 사용된다. 즉, 함수 외부에서는 참조할 수 없다.

arguments 객체는 인수를 프로퍼티 값으로 소유하며 프로퍼티 키는 인수의 순서를 나타낸다. arguments 객체의 callee 프로퍼티는 호출되어 arguments 객체를 생성한 함수, 즉 함수 자신을 가리키고 arguments 객체의 length 프로퍼티는 인수의 개수를 가리킨다.
arguments 객체는 매개변수 개수를 확정할 수 없는 가변 인자 함수를 구현할 때 유용하다.


### 18.2.2 caller 프로퍼티
caller프로퍼티는 ECMAScript 사양에 포함되지 않은 비표준 프로퍼티다. 

caller프로퍼티는 함수 자신을 호출한 함수를 가리킨다.

### 18.2.3 length 프로퍼티
length 프로퍼티는 함수를 정의할 때 선언한 매개변수의 개수를 가리킨다. 
> arguments 객체의 length 프로퍼티는 인자의 개수를 가리키고, 함수 객체의 length 프로퍼티는 매개변수의 개수를 가리킨다.

### 18.2.4 name 프로퍼티
name 프로퍼티는 함수 이름을 나타낸다. 

익명 함수 표현식의 경우 ES5에서 name 프로퍼티는 빈 문자열을 값으로 갖지만 ES6에서는 함수 객체를 가리키는 식별자를 값으로 갖는다.
```javascript
// 기명 함수 표현식
const namedFunc = function foo(){
    console.log(namedFunc.name); // foo
}

// 익명 함수 표현식
const anonymousFunc = function (){};
// ES5: 빈 문자열 , ES6: 함수 객체를 가리키는 변수 이름
console.log(anonymousFunc.name); // anonymousFunc

// 함수 선언문
function bar(){}
console.log(bar.name); // bar
```

### 18.2.5 __proto__ 접근자 프로퍼티
모든 객체는 [[Prototype]]이라는 내부 슬롯을 갖는다. [[Prototype]] 내부 슬롯은 객체지향 프로그래밍의 상속을 구현하는 프로토타입 객체를 가리킨다.

__proto__ 프로퍼티는 [[Prototype]] 내부 슬롯이 가리키는 프로토타입 객체에 접근하기 위해 사용하는 접근자 프로퍼티다. 
> 내부 슬롯에는 직접 접근할 수 없고 간접적인 접근 방법을 제공하는 경우에 한하여 접근할 수 있다.[[Prototype]] 내부 슬롯에도 직접 접근할 수 없으며, __proto__ 접근가 프로퍼티를 통해 간접적으로 프로토타입 객체에 접근할 수 있다.

### 18.2.6 prototype 프로퍼티
prototype 프로퍼티는 생성자 함수로 호출할 수 있는 함수 객체, 즉 constructor만에 소유하는 프로퍼티다. 일반 객체와 생성자 함수로 호출할 수 없는 non-constructor에는 prototype 프로퍼티가 없다. prototype 프로퍼티는 함수가 객체를 생성하는 생성자 함수로 호출될 때 생성자 함수가 생성한 인스턴스의 프로토타입 객체를 가리킨다.