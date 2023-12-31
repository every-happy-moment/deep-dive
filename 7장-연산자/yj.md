# 07장 연산자

## 7.1 산술 연산자 
### 7.1.1 이항 산술 연산자
이항 산술 연산자는 2개의 피연산자를 산술 연산하여 숫자 값을 만든다.
모든 이항 산술 연산자는 피연산자의 값을 변경하는 부수 효과(side effect)가 없다. <br />


|이항 산술 연산자|의미|부수 효과|
|:--:|:--|:--:|
|+|덧셈|X|
|-|뺄셈|X|
|*|곱셈|X|
|/|나눗셈|X|
|%|나머지|X|

<br />

### 7.1.2 단항 산술 연산자
단항 산술 연산자는 1개의 피연산자를 산술 연산하여 숫자 값을 만든다. <br />

|단항 산술 연산자|의미|부수 효과|
|:--:|--|:--:|
|++|증가|O|
|--|감소|O|
|+|어떠한 효과도 없다. 음수를 양수로 반전하지도 않는다.|X|
|-|양수를 음수로, 음수를 양수로 반전한 값을 반환한다.|X|

<br />

증가/감소(++/--) 연산자는 위치에 의미가 있다.
- 피연산자 앞에 위치한 전위 증가/감소 연산자(prefix increment/decrement operator)는 먼저 피연산자의 값을 증가/감소시킨 후, 다른 연산을 수행한다.
- 피연산자 뒤에 위치한 후위 증가/감소 연산자(postfix increment/decrement operator)는 먼저 다른 연산을 수행한 후, 피연산자의 값을 증가/감소시킨다.

<br />

숫자 타입이 아닌 피연산자에 + 단항 연산자를 사용하면 피연산자를 숫자 타입으로 변환하여 반환한다. 부수 효과는 없다.
```javascript
// 불리언 값을 숫자로 타입 변환한다.
x = true;
console.log(+x); // 1

// 부수 효과는 없다.
console.log(x); // true
```

<br />

-단항 연산자는 피연산자의 부호를 반전한 값을 반환한다. 부수 효과는 없다.
```javascript
// 문자열은 숫자로 타입 변환할 수 없으므로 NaN을 반환한다.
-'Hello'; // NaN
```
<br />

### 7.1.3 문자열 연결 연산자
+연산자는 피연산자 중 하나 이상이 문자열인 경우 문자열 연결 연산자로 동작한다. 그 외의 경우에는 산술 연산자로 동작한다.

```javascript
// null은 0으로 타입 변환된다.
1 + null; // 1

// undefined는 숫자로 타입 변환되지 않는다.
+undefined; // NaN
1 + undefined // NaN
```
이 예제에서 주목할 것은 개발자의 의도와는 상관없이 자바스크립트 엔진에 의해 암묵적으로 타입이 자동 변환되기도 한다는 것이다. 이를 암묵적 타입 변환(implicit coercion) 또는 타입 강제 변환(type coercion)이라고 한다.<br /><br />

## 7.2 할당 연산자
할당 연산자(assignment operator)는 우항에 있는 피연산자의 평가 결과를 좌항에 있는 변수에 할당한다. 할당 연산자는 좌항의 변수에 값을 할당하므로 변수 값이 변하는 부수 효과가 있다.
할당문은 값으로 평가되는 표현식인 문으로서 할당된 값으로 평가된다. 이러한 특징을 활용해 여러 변수에 동일한 값을 연쇄 할당할 수 있다. 
|할당 연산자|예|동일 표현|부수 효과|
|:--:|--|--|:--:|
|=|x = 5|x = 5|O|
|+=|x += 5|x = x + 5|O|
|-=|x -= 5|x = x - 5|O|
|*=|x *= 5|x = x * 5|O|
|/=|x /= 5|x = x / 5|O|
|%=|x %= 5|x = x % 5|O|

<br />

## 7.3 비교 연산자
비교 연산자(comparison operator)는 좌항과 우항의 피연산자를 비교한 다음 그 결과를 불리언 값으로 반환한다.

### 7.3.1 동등/일치 비교 연산자

|비교 연산자|의미|사례|설명|부수 효과|
|:--:|:--:|:--:|--|:--:|
|==|동등 비교|x == y|x와 y의 값이 같음|X|
|===|일치 비교|x === y|x와 y의 값과 타입이 같음|X|
|!=|부동등 비교|x != y|x와 y의 값이 다름|X|
|!==|불일치 비교|x !== y|x와 y의 값과 타입이 다름|X|

<br />

동등 비교(==) 연산자는 좌항과 우항의 피연산자를 비교할 때 먼저 암묵적 타입 변환을 통해 타입을 일치시킨 후 같은 값인지 비교한다. <br />따라서 동등 비교 연산자는 좌항과 우항의 피연산자가 타입은 다르더라도 암묵적 타입 변환 후에 같은 값일 수 있다면 true를 반환한다.
```javascript
// 타입은 다르지만 암묵적 타입 변환을 통해 타입을 일치시키면 동등하다.
5 == '5'; // true
```

일치 비교(===) 연산자는 좌항과 우항의 피연산자가 타입도 같고 값도 같은 경우에 한하여 true를 반환한다. 다시 말해, 암묵적 타입 변환을 하지 않고 값을 비교한다. <br />
일치 비교 연산자에서 주의할 것은 NaN 이다.
```javascript
// NaN은 자신과 일치하지 않는 유일한 값이다.
NaN === NaN; // false
```

숫자 0도 주의하자. 자바스크립트에는 양의 0과 음의 0이 있는데 이들을 비교하면 true를 반환한다.
```javascript
// 양의 0과 음의 0의 비교. 일치 비교/동등 비교 모두 결과는 true 이다.
0 === -0; // true
0 == -0; // true
```

Object.is 메서드 <br />
ES6에서 도입된 Object.is 메서드는 다음과 같이 예측 가능한 정확한 결과를 반환한다.
```javascript
-0 === +0; // true
Object.is(-0, +0); // false

NaN === NaN; // false
Object.is(NaN, NaN); // true
```

### 7.3.2 대소 관계 비교 연산자
|대소 관계 비교 연산자|예제|설명|부수 효과|
|:--:|:--:|--|:--:|
|>|x > y|x가 y보다 크다|X|
|<|x < y|x가 y보다 작다|X|
|>=|x >= y|x가 y보다 크거나 같다|X|
|<=|x <= y|x가 y보다 작거나 같다|X|

<br />

## 7.4 삼항 조건 연산자
삼항 조건 연산자(ternary operator)는 조건식의 평가 결과에 따라 반환할 값을 결정한다. 부수 효과는 없다.
물음표(?) 앞의 첫 번째 피연산자는 조건식, 즉 불리언 타입의 값으로 평가될 표현식이다. 만약 조건식의 평가 결과가 불리언 값이 아니면 불리언 값으로 암묵적 타입 변환된다.
삼항 조건 연산자 표현식은 if ... else 문과 중요한 차이가 있다. 삼항 조건 연산자 표현식은 값처럼 사용할 수 있지만 if ... else 문은 값처럼 사용할 수 없다. if ... else 문은 표현식이 아닌 문이기 때문이다.
삼항 조건 연산자 표현식은 값으로 평가할 수 있는 표현식인 문이다.

조건식 ? 조건식이 true일 때 반환할 값 : 조건식이 false일 때 반환할 값 <br /><br />

## 7.5 논리 연산자
|논리 연산자|의미|부수 효과|
|:--:|--|:--:|
|\|\||논리합(OR)|X|
|&&|논리곱(AND)|X|
|!|부정(NOT)|X|

<br />

## 7.6 쉼표 연산자
쉼표(,) 연산자는 왼쪽 피연산자부터 차례대로 피연산자를 평가하고 마지막 피연산자의 평가가 끝나면 마지막 피연산자의 평가 결과를 반환한다.
```javascript
var x, y, z;
x = 1, y = 2, z = 3; // 3
```

<br />

## 7.7 그룹 연산자
소괄호('( )')로 피연산자를 감싸는 그룹 연산자는 자신의 피연산자인 표현식을 가장 먼저 평가한다. 따라서 그룹 연산자를 사용하면 연산자의 우선순위를 조절할 수 있다. 그룹 연산자는 연산자 우선순위가 가장 높다. <br /><br />

## 7.8 typeof 연산자
typeof 연산자는 피연산자의 데이터 타입을 문자열로 반환한다. 하지만 typeof 연산자가 반환하는 문자열은 7개의 데이터 타입과 정확히 일치하지는 않는다.
```javascript
typeof 1 // number
typeof NaN // number
typeof null // object
typeof new Date() // object
typeof /test/gi // object
```
typeof 연산자로 null 값을 연산해 보면 "null"이 아닌 "object"를 반환한다는 데 주의하자. 이것은 자바스크립트의 첫 번째 버전의 버그다.
따라서 값이 null 타입인지 확인할 때는 typeof 연산자를 사용하지 말고 일치 연산자(===)를 사용하자.
```javascript
var foo = null;

typeof foo === null; // false
foo === null; // true
```

선언하지 않은 식별자를 typeof 연산자로 연산해 보면 ReferenceError 가 발생하지 않고 undefined를 반환한다는 점도 주의하자.
```javascript
// undeclared 식별자를 선언한 적이 없다.
typeof undeclared; // undefined
```

<br />

## 7.9 지수 연산자
ES7에서 도입된 지수 연산자는 좌항의 피연산자를 밑(base)으로, 우항의 피연산자를 지수(exponent)로 거듭 제곱하여 숫자 값을 반환한다.
```javascript
2 ** 0; // 1

// 음수를 거듭제곱의 밑으로 사용해 계산하려면 다음과 같이 괄호로 묶어야 한다.
(-5) ** 2; // 25

// 지수 연산자는 이항 연산자 중에서 우선순위가 가장 높다.
2 * 5 ** 2; // 50
```

<br />

## 7.10 그 외의 연산자
|연산자|개요|
|--|--|
|?.|옵셔널 체이닝 연산자|
|??|null 병합 연산자|
|delete|프로퍼티 삭제|
|new|생성자 함수를 호출할 때 사용하여 인스턴스를 생성|
|instanceof|좌변의 객체가 우변의 생성자 함수와 연결된 인스턴스인지 판별|
|in|프로퍼티 존재 확인|

<br />

## 7.11 연산자의 부수 효과
부수 효과가 있는 연산자는 할당 연산자(=), 증가/감소 연산자(++/--), delete 연산자 이다. <br /><br />

## 7.12 연산자 우선순위
연산자는 종류가 많아서 우선순위를 모두 기억하기 어렵고 실수하기도 쉽다. 연산자 우선순위가 가장 높은 그룹 연산자(( ))를 사용하여 우선순위를 명시적으로 조절하는 것을 권장한다.
```javascript
// 그룹 연산자를 사용하여 우선순위를 명시적으로 조절
10 * (2 + 3); // 50
```

<br />

## 7.13 연산자 결합 순서
연산자 결합 순서란 연산자의 어느 쪽(좌항 또는 우항)부터 평가를 수행할 것인지를 나타내는 순서이다.

|결합 순서|연산자|
|--|--|
|좌항 -> 우항|+, -, /, %, <, <=, >, >=, &&, \|\|, ., [], (), ??, ?., in, instanceof|
|우항 -> 좌항|++, --, 할당연산자(=, +=, -=, ...), !x, +x, -x, ++x ,--x, typeof, delete, ? ... : ..., **|

