# 09. 타입 변환과 단축 평가

## 9.1 타입 변환이란?

개발자가 의도적으로 값의 타입을 변환하는 것을 **명시적 타입 변환** 또는 **타입 캐스팅**이라 한다.

개발자의 의도와는 상관없이 표현식을 평가하는 도중에 자바스크립트 엔진에 의해 암묵적으로 타입이 자동변환되는 것을 **암묵적 타입 변환** 또는 **타입 강제 변환**이라 한다.

```javascript
var str = 3 + "";
console.log(typeof str, str); // string 3
```

## 9.2 암묵적 타입 변환

자바스크립트 엔진은 표현식을 평가할 때 개발자의 의도와는 상관없이 코드의 문맥을 고려해 암묵적으로 데이터 타입을 강제 변환(암묵적 타입 변환)할 때가 있다.

### 9.2.1 문자열 타입으로 변환

자바스크립트 엔진은 문자열 연결 연산자 표현식을 평가하기 위해 문자열 연결 연산자의 피연산자 중에서 문자열이 아닌 피연산자를 문자열 타입으로 암묵적 타입 변환한다.

```javascript
0 + '' // "0"
-0 + '' // "0"
NaN + '' // "NaN"
Infinity + '' // "Infinity"
-Infinity + '' // "-Infinity"
true + '' // "true"
null + '' // "null"

(Symbol()) + '' // TypeError
({}) + '' // "[Object Object]"
Math + '' // "[Object Math]"
[] + '' // ""
[10, 20] + '' // "10,20"
(function(){}) // "function(){}"
Array + '' // "function Array(){ [native code] }

```

### 9.2.2 숫자 타입으로 변환

산술 연산자 표현식을 평가하기 위해 산술 연산자의 피연산자 중에서 숫자 타입이 아닌 피연산자를 숫자 타입으로 암묵적 타입 변환한다. 이때 피연산자를 숫자 타입으로 변환할 수 없는 경우 산술 연산을 수행할 수 없으므로 표현식의 평가 결과는 NaN이 된다.

```javascript
+'' //0
+'string' // NaN
+true // 1
+false // 0
+null // 0
+undefined // NaN
+Symbol() // TypeError
+{} // NaN
+[] // 0
+[10,20] // NaN
+(function({})) // NaN
```

### 9.2.3 불리언 타입으로 변환
불리언 값으로 평가되어야 할 문맥에 Truthy값(참으로 평가되는 값)은 true로, false값은 Falsy(거짓으로 평가되는 값)로 암묵적 타입 변환된다.

* false로 평가되는 Falsy 값
  * false
  * undefined
  * null
  * 0, -0
  * NaN
  * ''(빈 문자열)
* False 값 외의 모든 값은 모두 true로 평가되는 Truthy값이다.

## 9.3 명시적 타입 변환
* 표준 빌트인 생성자 함수를 new 연산자 없이 호출하는 방법
* 암묵적 타입 변환을 이용하는 방법

### 9.3.1 문자열 타입으로 변환
* String 생성자 함수를 new 연산자 없이 호출하는 방법
* Object.prototype.toString 메서드를 사용하는 방법
* 문자열 연결 연산자를 이용하는 방법
````javascript
String(1); // '1'
(1).toString(); // '1'
1+ ''; // '1'
````
### 9.3.2 숫자 타입으로 변환
* Number 생성자 함수를 new 연산자 없이 호출하는 방법
* parseInt, parseFloat 함수를 사용하는방법(문자열만 숫자 타입으로 변환 가능)
* +단항 산술 연산자를 이용하는 방법
* *산술 연산자를 이용하는 방법
````javascript
Number('0') // 0
parseInt('0') // 0
parseFloat('1.2') //1.2
+0; //0
+true //1
'0' * 1; // 0
true * 1 // 1
````
### 9.3.3 불리언 타입으로 변환
* Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
* !부정 논리 연산자를 두 번 사용하는 방법
````javascript
Boolean('x') // true
Boolean('') // false
Boolean({}) // true
Boolean([]) // true
!!'x' // true
!!'' // false
!!Infinity // true
!!NaN // false
!!null // false
!!undefined // false
!!{} // true
!![] // true
````
## 9.4 단축 평가
### 9.4.1 논리 연산자를 사용한 단축 평가

