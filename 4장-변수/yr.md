# 변수

## 1. 변수란 무엇인가

- 컴퓨터가 연산을 위해 하나의 값을 저장해둔 메리 공간 자체 또는 메모리 공간을 식별하기 위해 붙인 이름
  - 메모리는 메리 셀의 집합체
  - 메모리 셀 하의 크는 1byte(8bit)
  - 변수에 값을 저장하는것을 **할당**
  - 변수에 저장된 값을 읽어드리는 것을 **참조**
  - 가독성을 높이는 부수효과가 있음
  - 개발자의 의도를 나타내는 명확한 네이밍은 코드를 이해하기 쉽게만든다

## 2. 식별자

- 어떤 값을 구별해서 식별할 수 있는 고유한 이름
  - 식별자는 값이 아니라 메모리 주소를 기억하고 있다.
  - 메모리상에 존재하는 값을 식별할 수 있는 이름은 모두 식별자라고 한다
  - 자바스크립트 엔진에 **선언(declaration)** 을 통해 식별자의 존재를 알린다

## 3. 변수 선언

- 값을 저장하기 위해 메모리 공간을 확보하고 메모리 공간의 주소를 연결해서 값을 저장할 수 있게 준비하는 행위
  - var, let, const 키워드를 통해 변수를 선언한다.
    - es6에서 let, const가 도입되었는데 기존의 var는 블록레벨 스코프를 지원하지 않는다.</br>(전역변수가 선언되어 부작용이 많음)
  ```javascript
  var score; //변수 선언
  // 1. 선언 단계 : 변수이름등록, JS엔진에 변수의 존재를 알림
  // 2. 값을 저장하기 위해 메모리 공간을 확보하고 암묵적으로 undefined를 할당해 초기화.
  ```
  - 모든 식별자는 실행 컨텍스트<sup>[1](#실행컨텍스트)</sup>에 등록된다</br>
  - 선언하지 않은 식별자에 접근하면 ReferenceError(참조에러)가 발생한다.

## 4. 변수선언의 실행 시점과 변수 호이스팅

- 변수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 특징을 **변수 호이스팅**이라고 한다.
- 모든 식별자(var,let,const,function....)는 호이스팅된다.<br/>
  모든 선언문은 런타임 이전단계에서 실행되기 떄문

## 5. 값의 할당

```javascript
var score; //변수선언
score = 80; //값의 할당
var score = 80; //변수선언과 값의 할당
```

- 변수선언은 코드가 순차적으로 실행되는 시점인 런타임 이전에 먼저 실행되지만 값의 할당은 코드가 순차적으로 실행되는 런타임에 실행된다.

## 6. 값의 재할당

- 값을 재할당 할 수 없어서 변수에 저장된 값을 변경할 수 없다면 변수가 아니라 상수라고 한다.
- ES6의 const 를 사용하면 상수를 표현할 수 있다.

## 7. 식별자 네이밍 규칙

- 식별자는 특수 문자를 제외한 문자, 숫자, \_, $ 를 포함할 수 있다.
- 예약어<br/>

|           |           |            |           |              |
| --------- | --------- | ---------- | --------- | ------------ |
| abstract  | arguments | boolean    | break     | byte         |
| case      | catch     | char       | class\*   | const        |
| continue  | debugger  | default    | delete    | do           |
| double    | else      | enum\*     | eval      | export\*     |
| extends\* | false     | final      | finally   | float        |
| for       | function  | goto       | if        | implements   |
| import\*  | in        | instanceof | int       | interface    |
| let       | long      | native     | new       | null         |
| package   | private   | protected  | public    | return       |
| short     | static    | super\*    | switch    | synchronized |
| this      | throw     | throws     | transient | true         |
| try       | typeof    | var        | void      | volatile     |
| while     | with      | yield      |

> 식별자로 사용 가능하나 strict mode에서는 사용 불가

```javascript
var first-name;   // Unexpected token -
var 1st;          // Invalid or unexpected token
var this;         // Unexpected token this

// 대소문자 구분
var firstname;
var firstName;
var FIRSTNAME;

// 카멜케이스
var firstName;
// 스네이크 케이스
var first_name;
//파스칼 케이스
var FirstName;
// 헝가리언 케이스
var strFirstName;

```

##### <a name="실행컨텍스트" class="foot-name">실행 컨텍스트</a>: 자바스크립트 엔진이 소스코드를 평가하고 실행하기 위해 필요한 환경을 제공하고 코드의 실행 결과를 실제로 관리하는 영역. <br/> JS 엔진은 실행 컨텍스트를 통해 실별자와 스코프를 관리한다</br>변수이름과 변수 값은 실행컨텍스트 내에 key:value 형태로 등록되어 관리된다
