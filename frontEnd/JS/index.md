# JavaScript

## 변수
- 하나의 값을 저장하기 위해 확보한 메모리 공간 자체 또는 그 메모리 공간을 식별하기 위해 붙인 이름
    - 값의 위치를 가리키는 상징적 이름
- 변수이름
    - 메모리 공간에 저장딘 값을 식별할 수 있는 고유한 이름
    - 식별자(identifier) 라고도 한다
- 변수 값
    - 변수에 저장된 값
- 할당(assignment: 대입,저장)
    - 변수에 값을 저장하는 것
- 참조(reference)
    - 변수에 저장된 값을 읽어 들이는 것


### 식별자
- 식별자는 어떤 값을 구별해서 식별할 수 있는 고유한 이름을 말한다.
    - 변수,함수,클래스등 이름은 모두 식별자 이다
- 식별자는 어떤 값이 저장되어 있는 메모리 주소를 기억(저장) 해야 함.
    - 식별자는 메모리 주소와 매핑 관계를 맺으며, 이 매핑 정보도 메모리에 저장
- 식별자는 값이 아니라 메모리 주소를 기억하고 있다. 즉, 메모리 주소에 붙인 이름이라고 볼 수 있다.

### 변수 선언(variable declaration)
- 값을 저장하기 위한 메모리 공간을 확보(allocate)하고 변수 이름과 확보된 메모리 공간의 주소를 연결 해서 값을 저장할 수 있게 준비하는 것.
- 변수 선언으로 확보된 메모리 공간은 해제되기 전까지는 누구도 확보된 메모리 공간을 사용 할 수 없도록 보호된다.
- var,let,const 키워드를 사용한다.
- 선언하지 않은 식별자에 접근하면 ReferenceError(참조에러)가 발생
> 키워드 : 언어에서 미리 규정한 일종의 명령어

```js
var score;
// 메모리 공간을 확보 하고 score라는 변수명과 name binding을 진행하였다.
// 확보된 메모리 공간에는 자바스크립트 엔진에 의해 undefined라는 값이 암묵적으로 할당되어 초기화된다.
//  var 키워드의 변수선언은 선언단계와 undefined로 초기화단계를 동시에 진행된다.
//  자바스크립트는 암묵적으로 초기화를 진행하여 쓰레기 값으로 부터 안전한다.
```
> undefined는 자바스크립트에서 제공하는 원시 타입 값(primitive value)이다.

> 변수 이름을 비롯한 모든 식별자는 `실행 컨텍스트(execution context)`에 등록된다. 엔진이 소스코드를 평가 실행하기 위한 환경을 제공하고 결과를 관리하는 영역이며, 식별자와 스코프 또한 관리한다. 또한 변수 이름과 값이 Key/Value 형식인 객체로 등록되어 관리된다.



### 변수 선언의 실행 시점과 변수 호이스팅
```js
console.log(score);

var score;
```
- 변수 선언보다 변수 참조를 먼저 했음에도 참조 에러가 발생하지 않는다. `변수 선언이 소스코드가 한 줄씩 순차적으로 실행되는 시점, 즉 런타임(runtime)이 아니라 그 이전 단계에서 먼저 실행되기 때문`
    - 실행하기 전 소스코드의 평가 과정을 거치면서 선언을 먼저 한다. 즉, 변수 선언이 어디에 있든 상관 없이 다른 코드보다 먼저 실행한다.
> 이와 같이 `변수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 변수 회이스팅(variable hoisting)`이라고 한다. var,let,const,function,function*,class 키워드를 사용해 선언하는 모든 식별자들은 호이스팅 된다.

### 값의 할당
- `=`연산자를 사용하여 우변의 값을 좌변의 변수에 할당
```js
var score;//변수 선언
score = 80;// 값의 할당
```
- `var score = 80;`와 같이 변수 선언과 할당을 진행할 수 있는데 이때, 선언과 할당은 순차적으로 진행된다. `동시에 적혀 있지만 선언은 호이스팅 되어 런타임 이전에 실행되고 할당은 런타임 과정에서 진행된다.`

```js
console.log(score); // undefined

var score = 80; // 1. 변수 선언 -> 2. 변수 할당 

console.log(score); // 80
```

### 값의 재할당

```js
var score = 80; //변수 선언과 값의 할당
score = 90; //재할당
```

- 자바스크립트는 선언 시 undefined로 초기화 되기 때문에 엄밀히 말하면 할당도 재할당 이라고 할 수 있다.
- 값을 재할당 할 수 없다면 변수가 아니라 상수(constant)라 한다.

> const키워드를 사용해 선언한 변수는 재할당이 금지된다, 즉 const 키워드를 사용하면 상수를 표현할 수 있다. 하지만 반드시 const키워드가 상수를 위해서만 사용하지는 않는다.

> 재할당 이후에 이전에 값이 저장된 메모리 주소는 `가비지 콜렉터`에 의해 메모리가 해제된다. 자바스크립트는 가비지 콜렉터를 내장하고 있는 `매니지드 언어`로 `메모리 누수`를 방지.

### 식별자 네이밍 규칙
- 특수문자를 제외한 문자, 숫자, 언더스코어(_), 달러($)를 포함할 수 있다.
- 식별자는 문자 or 언더스코어 or 달러로 시작해야한다, 숫자로는 불가
- 예약어는 식별자로 사용할 수 없다.


### 네이밍 컨벤션
```js
//카멜 케이스(camelCase)
var firstName;

// 스네이크 케이스(snake_case)
var first_name;

//파스칼 케이스(PascalCase)
var FirstName;

// 헝가리언 케이스(typeHungarianCase)
var strFirstName; // type + identifier
var $elem = document.getElementById('myId'); //DOM Node
var observable$ = fromEvent(document, 'click') // RxJS 옵저버블
```
- 자바스크립트에서는 일반적으로 사용하는 네임 컨벤션
    - 변수,함수 : 카멜 케이스
    - 생성자 함수, 클래스 이름 : 파스칼 케이스
    

##  표현식과 문

### 값(Value)
- 값은 식(표현식:expression)이 평가(evaluate)되어 생성된 결과를 말한다.
- 모든 값은 데이터 타입을 가지며, 2진수(비트)의 나열로 저장된다.

### 리터럴(literal)
- 리터럴은 사람이 이해할 수 있는 문자 또는 약속된 기호를 사용해 값을 생성하는 표기법(notation)을 말한다.
    - 사람이 이해할 수 있는 문자 또는 미리 약속된 기호로 표기한 코드
    - 런타임에 리터럴을 평가해 값을 생성한다.
- 정수, 부동소수, 2진수, 8진수 , 16진수, 문자열, 불리언, null, undefined, 객체, 배열, 함수, 정규표현식등

### 표현식(expression)
- 표현식(expression)은 값으로 평가될 수 있는 문(statement)이다. 즉, 표현식이 평가되면 새로운 값을 생성하거나 기존 값을 참조한다.
- 값으로 평가될 수 있는 문은 모두 표현식이다, 이것은 문법적으로 값이 위치할 수 있는 모든 자리에는 표현식도 위치할 수 있다.


### 문(Statement)
- 프로그램을 구성하는 기본 단위이자 최소 실행 단위로, 명령문 이라고 부르기도 함.

> 토큰(token)이란 문법적인 의미를 가지며, 문법적으로 더 이상 나눌 수 없는 코드의 기본 요소를 의미한다.
>    - 키워드, 식별자, 연산자, 리터럴, 세미콜론(;), 마침표(.)등의 특수 기호

### 세미콜론과 세미콜론 자동 삽입 기능
- 세미콜론은 문의 종료를 나타낸다.
- 코드블럭은 자체 종결성을 갖기 때문에 붙이지 않는다.
- 자바스크립트는 세미콜론 자동 삽입 기능(ASI)가 존재하여 세미콜론이 옵션이다.

### 표현식인 문과 표현식이 아닌 문

```js
var x;
// 변수 선언문은 값으로 평가될 수 없기 때문에 표현식이 아니다.
x = 1 + 2;
// x를 3으로 대체할 수 있기 때문에 표현식 이라고 할 수 있다.
```
- 표현식의 여부를 구별하는 간단한 방법은 변수를 할당해 보는 것이다. 할당이 가능하면 표현식 불가하다면 표현식으로 볼 수 없다.



## 데이터 타입(Data Type)

- 원시 타입
    - 숫자(number) 타입
        - 정수,실수 모두 포함
    - 문자열(string) 타입
    - 불리언(boolean) 타입
    - undefined 타입
        - var 키워드로 선언된 변수에 암묵적으로 할당되는 값
    - null 타입
        - 값이 없다는 것을 의도적으로 명시할 때 사용하는 값
    - 심벌(symbol) 타입
- 객체 타입

### 숫자(Number) 타입
- 정수와 실수를 구별하지 않고 포함하는 하나의 타입
- 배정밀도 64비트 부동소수점 형식을 따른다. 즉, `모든 수를 실수로 처리한다`.
    - 따라서 자바스크립트에서는 `3/2 == 1.5`
- 자바스크립트는 2진수,8진수, 16진수의 값을 참조하면 10진수로 해석
- 숫자 타입이 표현할 수 있는 특별한 값
    - Infinity : 양의 무한대
    - -Infinity : 음의 무한대
    - NaN: 산술 연산 불가(not-a-number)


### 문자열(String) 타입
- 텍스트 데이터를 나타내는데 사용하며, 0개 이상의 16비트 유니코드 문자의 집합으로 표현할 수 있다.
- 싱글쿼테이션(''), 더블쿼테이션(""), 백틱(``)으로 텍스트를 감싼다. 일반적으로는 싱글쿼테이션으로 감싼다
- 자바스크립트의 문자열은 원시 타입이며, 변경 불가능한 값(immutable value)이다.

### 템플릿 리터럴(template literal)
- ES6부터 도입된 문자열 표기법, 멀티라인(muli-line) 문자열, 표현식 삽입(expression interpolation), 태그드 템플릿(tagged template)등 편리한 문자열 처리기능을 제공
- 런타임에 일반 문자열로 변환되어 처리되며, (\` \`) `백틱`을 사용하여 표현한다.
```js
var template = `Template Literal`;
console.log(template);
```

#### 멀티라인 문자열
- 일반 문자열 내에서는 줄바꿈(개행)이 허용되지 않아, `이스케이프 시퀀스(escape sequence)`를 사용해야한다

| 이스케이프 시퀀스 | 의미 |
|------------------|-------------|
| `\0` |Null|
|`\b`|백스페이스|
|`\f`|폼 피드|
|`\n`|개행: 다음 행으로 이동|
|`\r`|개행: 커서를 처음으로 이동|
|`\t`|탭(수평)|
|`\v`|탭(수직)|
|`\uXXXX`|유니코드|
|`\'`|작은따옴표|
|`\"`|큰따옴표|
|`\\`|백슬래시|


> 라인 피드와 캐리지 리턴 : 개행문자에는 Line Feed 와 Carriage Return이 있다. 라인 피드(\n)는 커서를 정지한 상태에서 종이를 한줄 올리는 것이고. 캐리지 리턴(\r)은 종이를 두고 커서를 맨 앞줄로 이동하는 것이다.

- 위와 같이 개행문자를 포함해야하는 문자열과 달리 템플릿 리터럴은 이스케이프 시퀀스 없이도 줄바꿈이 허용된다.
```js
var template = `<ul>
    <li><a href="#">HOME</a></li>
</ul>`;

console.log(template);
```

#### 표현식 삽입
- 보통 문자열은 `+` 연산자를 통해 서로를 연결하지만 템플릿 리터럴을 사용한다면, 문자열 내부에 표현식(값으로 대체할 수 있는 문)을 삽입할 수 있다
- 삽입 할 때는 `${표현식}`을 통해 표현한다

```js
var first = 'Ung-mo';
var last = 'Lee';

console.log(`My name is ${first} ${last}.`);
```

#### 불리언 타입
- 논리적 참, 거짓을 나타내는 true, false의 값을 가진다.

#### undefined타입
- var키워드로 선언한 변수는 암묵적으로 undefined로 초기화된다.
- 개발자가 의도적으로 할당하기 위한 값이 아니라 JS 엔진이 변수를 초기화 할 때 사용하는 값.

#### null 타입
- 변수의 값이 없다는 것을 의도적으로 명시(의도적부재:intentional absence)할 때 사용.

#### Symbol 타입
- ES6에 추가된 7번째 타입으로. 변경 불가능한 원시 타입의 값
- 다른 값과 중복 되지 않는 유일무이한 값으로 객체의 유일한 프로퍼티 키를 만들기 위해 사용된다.
- Symbol 함수를 호출해 생성하며, 이 때 생성된 값은 외부에 노출되지 않고 중복되지 않는 값이다.
```js
var key = Symbol('key');
console.log(typeof key);

var obj = {};

obj[key] = 'value';
console.log(obj[key]);
```

#### 객체 타입
- 자바스크립트를 이루는 거의 모든 것이 객체라고 할 수 있고, 원시타입을 제외한 모든 타입을 객체 타입이다.

### 데이터 타입의 필요성
- 데이터 타입에 의한 메모리 공간의 확보와 참조
    - 데이터 저장 공간을 확보하기 위해서는 해당 데이터의 크기를 알 수 있어야한다. 이 때 해당하는 크기를 타입으로 구분하여 자동으로 확보한다
    - 값을 참조할 때, 해당 메모리를 어디까지 읽어야 할 지 알기위해서는 해당 타입에 지정된 크기를 알아야한다.

> `심벌 테이블` : 식별자를 키로 바인딩된 값의 메모리 주소, 데이터 탕비, 스코프등을 관리한다.
- 데이터 타입에 의한 값의 해석
    - 값을 해석할 때 2진수(비트)로 표현된 값을 어떤 것으로 해석할지 결정한다.
```
- 값을 저장할 때 확보해야 하는 메모리 공간의 크기를 결정하기 위해
- 값을 참조할 때 한 번에 읽어 들여야 할 메모리 공간의 크기를 결정하기 위해
- 메모리에서 읽어 들인 2진수를 어떻게 해석할지 결정하기 위해
```

### 동적 타이핑

C나 자바와 같은 `정적 타입(static type)언어`는 변수를 선언할 때 할당할 수 있는 값의 종류, 즉 데이터 타입을 사전에 선언해야한다. 이를 `명시적 타입 선언(explicit type declaration)`이라 한다. 이때, 타입은 변경할 수 없다.
그런데 자바스크립트는 동적 타입을 지원하는 언어로서 변수 선언시점이 아닌 변수에 값을 할당하는 시점에 타입이 동적으로 결정하고 자유롭게 변결할 수 있다.

- `동적 타이핑(dynamic typing)` 을 지원하는 `동적 타입 언어`
    - 자바스크립트의 변수는 선언이 아닌 할당에 의해 타입이 결정(타입 추론)된다.
    - 재할동에 의해 변수의 타입은 언제든지 동적으로 변경할 수 있다.

```
- 변수는 꼭 필요한 경우만 제한적으로 사용한다.
- 변수의 유효범위(Scope)는 최대한 좁게 만들어 부작용을 억제한다
- 전역변수는 최대한 사용하지 않는다
- 변수보다는 상수를 사용해 값의 변경을 억제
- 변수 이름은 목적이나 의미를 파악할 수 있게 네이밍한다
```


## 연산자(Operator)
- 하나 이상의 표현식을 대상으로 산술,할당,비교,논리,타입,지수 연산등을 수행하여 값을 만든다.

### 산술 연산자(arithmatic operator)
- 피연산자를 수학적 계산으로 숫자 값을 만든다, 산술 연산이 불가능한 값의 경우 NaN을 반환한다.
- 이항 산술 연산자
    - +,-,*,/,% 등이 존재
- 단항 산술 연산자
    - ++,--,부호연산자
    - 증감연산자는 전위, 후위에 따라 다른 효과를 가져온다.
- 문자열 연결 연산자
    - `+`는 피연산자가 문자열인 경우 문자열을 연결하는 연산자로 변환된다.
- 암묵적 타입변환
```js
'1' + 2; //'12'

1 + 2; //3

1 + true; // 2 (true는 1로 타입 변환된다.)
1 + false; // 1 (false는 0로 타입 변환된다.)
1 + null; // 1 (null은 0로 타입 변환된다.)
```

### 할당 연산자(assignment operator)
- 할당을 하는 연산자이다
    - =, +=, -=, *=, /=, %= 등이 존재

### 비교 연산자(comparison operator)
- 좌항 우항의 피연산자를 비교한 다음 그 결과를 불리언 값으로 반환한다.

#### 동등/일치 비교연산자
- 좌항 우항이 같은지 여부를 판단하는데, 그 엄격성에 따라 동등인지 일치인지 구분한다
    - (부)동등비교 : == , !=
    - (불)일치비교 : === , !==
- 일치 비교는 타입까지 일치해야 하고, 동등 비교는 타입은 달라도 상관 없다

```js
5 == '5' // true
5 === '5' // false
```
- 동등 비교는 예측이 힘든 결과를 만들기 때문에 동등 비교 연산자보다는 일치 비교 연산자 사용을 권장한다.
    - 일치 연산자는 NaN인지를 비교할 수 없고 `isNaN()`메서드 사용
    - +0과 -0을 구분할 수 없어 `Object.is()` 메서드를 사용한다
- 값이 NaN인지 확인 하기 위해서는 `isNaN()` 메서드를 사용해야 한다.
- Es6에 도입된 Object.is()메서드를 통해 비교도 가능

#### 대소 관계 비교 연산자
- 피연산자의 크기를 비교하여 불리언 값을 반환
    - \>, \<, \>= , \<= 등이 존재

#### 삼항 조건 연산자(ternary operator)
` 조건식 ? 조건식이 true일 때 반환할 값 : 조건식이 false일 때 반환할 값 `

#### 논리 연산자
- 좌황 우항의 피연산자를 논리연산한다.
    - || : 논리합(OR)
    - && : 논리곱(AND)
    - !  : 부정(NOT)
> 드 모르간 법칙을 사용하면 복잡한 표현식을 가독성 있게 표현할 수 있다
```js
!(x||y) === (!x && !y)
!(x&&y) === (!x ||!y)
```

#### typeof 연산자
- typeof연산자는 피연산자의 데이터 타입을 문자열로 반환
    - string,number,boolean,undefined,symbol,object,function중 하나를 반환
    - null을 typeof연산을 진행하면 object를 반환한다, 자바스크립트 첫 번째 버전의 버그인데 하위호환성 때문에 변경을 하지 못하고 있다. 따라서 null을 비교할 때는 `===` 일치 연산자를 사용하자.
    - 선언하지 않은 식별자를 연산했을 때는 undefined를 반환
#### 지수 연산자
- ES7에서 도입된 지수 연산자는 좌항의 피연산자를 밑으로 우항의 펴연산자를 지수로 거듭제고 하여 반환
```js
2 ** 2; // 4
2 ** 0; // 1
```
- 음수를 거듭제곱 하는 경우 소괄호(`()`)를 통해서 묶어주어야 한다.

#### 그외 연산자
- `?.` : 옵셔널 체이닝 연산자
- `??` : null 병합
- `delete` : 프로퍼티 삭제
- `new`: 인스턴스 생성
- `instanceof` : 좌변의 객체가 우변의 생성자 함수와 연결된 인스턴스인지 확인
- `in` : 프로퍼티 존재확인

### 연산자의 부수 효과
- 할당 연산자(=), 증감 연산자(++/--), delete연산자는 부수 효과가 존재한다.
```js
var x;
x = 1;
// 변수의 값이 변하는 부수효과
x++;
// 변수의 값이 변하는 부수효과
var o = { a: 1};

delete o.a;
// 객체의 프로퍼티를 삭제하는 부수효과
```
### 연산자의 우선순위
1. ()
2. new(매개변수 존재),[](프로퍼티 접근), ()(함수 호출), ?.(옵셔널 체이닝 연산자)
3. new(매개변수 미존재)
4. x++ , x--
5. !x, +x, -x, ++x, --x, typeof, delete
6. **(이항 연산자중 우선순위가 가장 높다)
7. *,/,%
8. +,-
9. <,<=,>,>=,in,instanceof
10. ==,!=,===,!==
11. ??(null 병합)
12. &&
13. ||
14. ? ... : ... (삼항 연산자)
15. 할당 연산자
16. ,(쉼표 연산자)

### 연산자 결합 순서
- 연산자의 어느쪽 부터 평가를 수행하는지 나타내는 순서

- 좌항 -> 우항
    - +,-,/,%, <,>,&&,||,.,[],(),??,?.,in,instanceof
- 우항 -> 좌항
    - ++, -- , 할당연산자 , !x,+x,-x,typeof,delete, 삼항연산자


# 타입 변환과 단축 평가

## 타입 변환

- `명시적 타입 변환(explicit corecion)`
    - 개발자가 의도를 가지고 값의 타입을 변경하는 것을 얘기하며, 타입 캐스팅 (type casting)으로 부르기도 한다.
```js
var x = 10;
var str = x.toString();
```
- `암묵적 타입 변환(implicit coercion)`
    - 개발자의 의도와는 상관 없이 표현식을 평가하는 도중에 스크립트 엔진에 의해 타입이 변환되는 것으로 타입 강제 변환(type coercion)으로 부르기도 함
```js
var x = 10
var str = x + '';
```

> 이러한 타입변환이 기존 원시값을 변경하는 것이 아니다 원시 값은 변경 불가능한 값(immutabla value)이므로 변경할 수 없다. 타입 변환이란 기존 원시 값을 사용해 다른 타입의 새로운 원시 값을 생성하는 것이다.


### 암묵적 타입 변환

```js
// 피연산자가 모두 문자열 타입이어야 하는 문맥
'10' + 2 // '102'
// 피연산자가 모두 숫자 타입이어야 하는 문잭
5 * '10' // 50
// 피연산자 또는 표현식이 불리언 타입어야 하는 문맥
!0 // true
```

```js
0 + '' // "0"
-0 + '' //"0"
1 + '' // "1"
-1 + '' // "-1"
NaN + '' // "NaN"
Infinity + '' // "Infinity"
-Infinity + '' // "-Infinity"

// 불리언
true + '' // "true"
false + '' // "false"

//null
null + '' // "null"

// undefined
undefined + '' // "undefined"

// 심벌
(Symbol()) + '' // TypeError : Cannot convert a Symbol value to a string

// 객체 타입
({}) + '' // "[object Object]"
Math + '' // "[object Math]"
[] + '' // ""
[10,20] + '' //"10,20"
(function(){})+'' // "function(){}"
Array + '' // "function Array() {[native code]}"
```

- 숫자 타입으로 변환
    - 아라비아 숫자를 문자열로 표현한 경우 다른 한쪽이 Number 타입이면 Number타입으로 연산한다
    - 불리언 타입은 true : 1 false : 0
    - null 타입은 : 0
- 불리언 타입으로 변환
    - 불리언 타입은 Falsy값을 제외하고는 전부 Truthy다
    - Falsy 값
        - false
        - undefined
        - null
        - 0, -0
        - NaN
        - ''(빈문자열)

### 명시적 타입 변환
>- 표준 빌트인 생성자 함수(String, Number, Boolean)을 new연산자 없이 호출하는 방법
>- 암묵적 타입 변환을 이용하는 방법

- 문자열 타입으로 변환
```js
// 1. String 생성자 함수를 new연산자 없이 사용하는 방법
console.log(String(1)); //"1"

// 2. Object.prototype.toString 메서드 사용
console.log((1).toString()); // "1"

//3. 문자열 연결 연산자 사용 방법
console.log(1 + ''); //"1"
```

- 숫자 타입으로 변환

```js
// 1 Number()
Number('1'); //1

//2. parseInt,parseFloat함수
parseInt('1'); //1
parseFloat('1.0'); //1.0

//3 + 단항 산술 연산자 이용
+'1' // 1
+true // 1

//4. * 산술 연산자 이용
'1' * 1; //1
true * '1'; //1
```

- 불리언 타입 변환
```js
// 1. Boolean()
Boolean('x'); //true
Boolean(''); //false
```

### 단축 평가

#### 논리 연산자를 사용한 단축 평가
- 논리합(||) 또는 논리곱(&&)연산자 표현식의 평가 결과는 불리언 값이 아니고 어느 한쪽으로 평가된다.

```js
true && true // true
'Cat' && 'Dog' // -> "Dog"
```
- 논리곱(&&) 연산자는 두 개의 피연산자가 모두 true로 평가될 때 true를 반환한다
- 논리곱은 앞에서 true라고 해도 뒤에도 true 값이 나와야 되기 때문에 뒤쪽 결과로 반환한다.

```js
true || false // true
'Cat' && 'Dog' // -> "Cat"
```
- 논리합(||) 연산자는 두 개의 피연산자중 하나가 true로 평가되면 true를 반환한다
- 논리합 연산은 앞에가 true면 뒤를 보지 않아도 true값이기 때문에 Cat을 출력한 것

### 옵셔널 체이닝 연산자
- ES11(ECMAScript2020)에서 도입된 옵셔널 체이닝(Optional Chaining)연산자 `?.`는 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고 그렇지 않으면 우항의 프로퍼티 참조를 이어나간다.
```js
var elem = null;
// elem이 null 또는 undefined이면 undefined를 반환, 아니면 우항의 프로퍼티 참조를 이어나감
var value = elem?.value;
console.log(value);// undefined
```

# 객체 리터럴

## 객체
- 자바스크립트는 객체기반 프로그래밍 언어이며, 구성하는 거의 모든 것이 객체다, 원시 값을 제외한 나머지 값(함수, 배열, 정규표현식 등)
- 원시 타입의 값은 변경 불가능한 값이지만 객체 타입의 값은 변경 가능한 값이다.
```js
var person = {
    name: 'Lee'
    ,age: 20
}
// name:'Lee' : 프로퍼티
//  name : 프로퍼티 키
// 'Lee' : 프로퍼티 값
//  객체는 프로퍼티의 집합이다.
```

```js
var counter = {
    num:0,
    increase: function(){
        this.num++;
    }
}
// num:0 -> 프로퍼티
//increase: function(){this.num++;} -> 메서드
```
- 프로퍼티 : 객체의 상태를 나타내는 값(data)
- 메서드 : 프로퍼티(상태 데이터)를 참조하고 조작할 수 있는 동작(behavior)

> 객체와 함수 : 자바스크립트에서 함수와 객체는 밀접한 관계를 가진다 함수는 자체가 객체이기도 하고 함수로 객체생성을 하기도 한다. 함수와 객체는 분리할 수 없는 개념이라고 할 수 있다(자바스크립트에서)

## 객체 리터럴에 의한 객체 생성
- 자바스크립트는 프로토타입 기반 객체지향 언어로서 클래스 기반 객체지향 언어와는 달리 다양한 객체 생성 방법을 지원한다
    - 객체 리터럴
    - Object 생성자 함수
    - 생성자 함수
    - Object.create 메서드
    - 클래스(ES6)
- 이중 가장 일반적인 방법은 객체 리터럴을 이용하는 방법인데, 중괄호({...})안에 0개 이상의 프로퍼티를 정의한다. `할당되는 시점에 자바스크립트엔진은 객체리터럴을 해석해 객체를 생성`한다.
```js
var person = {
    name :'Lee'
    ,sayHello:function(){
        console.log(`Hello! My name is ${this.name}.`);
    }
};

console.log(typeof person); //object
console.log(person); // { name: 'Lee', sayHello: [Function: sayHello] }
```
> 코드블럭과 다르며, 코드블럭은 세미콜론을 붙이지 않는다.

## 프로퍼티
- 객체는 프로퍼티의 집합이며, 프로퍼티는 키와 값으로 구성된다.
    - 프로퍼티 키: 빈 문자열을 포함한 모든 문자열 또는 심벌 값
    - 프로퍼티 값: 자바스크립트에서 사용할 수 있는 모든 값
- 프로퍼티의 키는 네이밍 규칙을 꼭 지켜야하는 것은 아니지만, 지키지 않았을 경우 더블(싱글)쿼테이션으로 묶어주어야 한다.
```js
var person = {
    firstName = 'Ung-mo', // 식별자 네이밍 규칙 준수한 키
    'last-name': 'Lee'    // 식별자 네이밍 규칙을 준수하지 않는 키
};
```
- 문자열 또는 문자열로 평가할 수 있는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수 있다.
대괄호([...])로 묶어야 한다.
```js
var obj = {};
var key = 'hello';

//Es5: 프로퍼티 키 동적 생성
obj[key] = 'world';
// Es6: 계산된 프로퍼티 이름
var obj = {[key]:'world'};

console.log(obj); //{hello:"world"}

```

## 메서드
- 자바스크립트에서 사용할 수 있는 모든 값은 프로퍼티로 사용할 수 있고. 함수 역시 객체(일급 객체)로 값으로 취급하여 프로퍼티 값으로 사용할 수 있다.
- 프로퍼티 값이 함수일 경우 메서드 라고 부른다. 즉, 객체에 묶여있는 함수를 메서드라고 한다.
```js
var circle = {
    radius : 5, // <- 프로퍼티
    //원의 지름
    getDiameter:function(){
        return 2 * this.radius; // this는 circle을 의미
    }
}
```

## 프로퍼티 접근
- 프로퍼티의 접근하는 방법
    1. 마침표 프로퍼티 접근 연산자(.) 사용하는 마침표 표기법(dot notation)
    1. 대괄호 프로퍼티 접근연산자([...])를 사용하는 대괄호 표기법(bracket notation)

```js
var person = {
    name : 'Lee',
    'last-name': 'Lee'
};
//dot notation
console.log(person.name); //Lee
//bracket notation
console.log(person['name']); //Lee
// 불가
console.log(person[name]); //name is not defined
// 객체에 존재하지 않는 프로퍼티 접근
console.log(person.age); //undefined
// Key값이 네이밍 컨벤션에 맞지않은 이름일 경우
person.'last-name'; //SyntaxError: Unexpected string
person.last-name; //SyntaxError: Unexpected string
console.log(person['last-name']); // Lee
```
### 프로퍼티 값 갱신
```js
var person = {
    name:'Lee'
};
person.name = 'Kim';
```
### 프로퍼티 동적 생성
```js
var person = {
    name:'Lee'
};
person.age = 20;
// person객체에 age 프로퍼티가 생성되고 20 값을 넣어서 프로퍼티를 동적으로 생성한다.
```

### 프로퍼티 삭제
```js
var person = {
    name : 'Lee'
};
person.age = 20;
// age 프로퍼티를 delete연산자를 통해 삭제
delete person.age;
// address 프로퍼티가 존재하지 않아 삭제되지는 않으나 에라가 발생하지도 않는다.
delete person.address;
```

## Es6에서 추가된 객체 리터럴 확장기능

### 프로퍼티 축약표현
```js
// ES6
let x = 1, y = 2;
// 프로퍼티 축약 표현
const obj = { x, y};

console.log(obj);
//{x:1 , y:2}
```

### 계산된 프로퍼티 이름
```js
//ES6
const prefix = 'prop';
let i = 0;

const obj = {
    [`${prefix}-${++i}`] : i,
    [`${prefix}-${++i}`] : i,
    [`${prefix}-${++i}`] : i
}
console.log(obj);
//{ 'prop-1': 1, 'prop-2': 2, 'prop-3': 3 }
```

### 메서드 축약 표현
```js
const obj = {
    name:'Lee',
    sayHi(){
        console.log(`Hi! ${this.name}`);
    }
};

obj.sayHi();
```

# 원시 값과 객체의 비교
- 원시 타입과 객체 타입의 차이점
    1. 원시타입의 값은 변경불가능한 값이고 객체(참조)타입의 값, 즉 객체는 변경 가능한 값이다.
    1. 원시 값을 변수에 할당하면 변수(확보된 메모리 공간)에는 실제 값이 저장된다, 객체를 변수에 할당하면 변수(확보된 메모리 공간)에는 참조 값이 저장된다.
    1. 원시 값을 갖는 변수를 다른 변수에 할당하면 원본의 원시 값이 복사되어 전달된다. 이를 값에 의한 전달 이라고 하고 객체를 가리키는 변수를 다른 변수에 할당하면 참조 값이 복사되어 전달된다 이를 참조에 의한 전달이라고 함


## 원시 값
### 변경 불가능한 값
- 원시 타입의 값은 변경 불가능한 값이다. 다시 말해 한번 생성된 원시 값은 읽기 전용(read only)으로 변경 불가.
- 변경이 불가하다는 것은 변수가 아닌 값에 대한 진술이다.
- 값이 재할당 된다는 것은, 값이 변경된 것이 아니라 변수가 다른 주소를 참조하는 것이다.

### 문자열과 불변성
- 자바스크립트에서는 String을 원시타입으로 제공하고, 변경 불가능하다.
- 문자열은 유사 배열 객체이면서, 이터러블 이므로 배열과 유사하게 각문자에 접근 가능
> 유사 배열 객체(array-like object)
> 마치 배열처럼 인덱스로 프로퍼티 값에 접근할 수 있고 length 프로퍼티를 갖는 객체를 말한다. 원시 값을  `객체처럼 사용하면 원시 값을 감싸는 래퍼 객체로 자동 변환`된다.

```js
var str = 'string';
//  문자열은 유사 배열으로 배열과 유사하게 인덱스를 사용해 각 문자에 접근할 수 있다.하지만 문자열은 원시 값이므로 변경할 수 없다. 이때, 에러가 발생하지 않는다.
str[0] = 'S'

console.log(str); //string
```


### 값에 의한 전달
```js
var score =80;
var copy = score;

console.log(score); // 80
console.log(copy); // 80

score =100;

console.log(score); // 100
console.log(copy);  // 80
```
- 값에 의한 전달
    - 변수에 원시 값을 갖는 변수를 할당하면 할당 받는 변수에는 할당되는 변수의 원시 값이 복사되어 전달된다.
    - score변수와 copy변수의 값 80은 다른 메모리 공간에 저장된 별개의 값이다.
        - 확실한 것은 아니다 파이썬 처럼 어느 한쪽에 재할당이 있을 때 비로소 변경될 수도 있다.
    - 사실 값에 의한 전달 역시 값을 전달하는 것이 아니라 메모리 주소를 전달하고, 내부 적으로 서로가 서로 간섭할 수 없도록 분리되게 해석할 뿐이다.

### 객체
- 객체는 프로퍼티의 개수가 정해져 있지 않으며, 동적으로 추가 삭제할 수 있다.따라서 객체는 원시 값과 같이 확보해야 할 메모리 공간의 크기를 사전에 정해 둘 수 없다.
- 객체는 상대적으로 많은 리소스를 잡아먹기 때문에 원시 값과 다른 방식으로 동작하도록 설계되었다.

> 자바스크립트의 객체 관리 방식 : 자바스크립트 객체는 프로퍼티 키를 인덱스로 사용하는 해시 테이블이라고 생각 할 수 있다. 대부분의 자바스크립트 엔진은 해시 테이블과 유사하지만 높은 성능을 위해 일반적인 해시 테이블보다 나은 방법으로 객체를 구현한다. 자바스크립트는 클래스 없이 객체를 생성할 수 있고, 동적으로 프로퍼티와 메서드를 추가할 수 있다. 이는 유연하지만 클래스 기반언어보다 비효율적인 방식이다. 따라서 v8 엔진에서는 프로퍼티에 접근을 위해 동적 탐색 대신 `히든 클래스`라는 방식을 사용해 빠른 프로퍼티 접근 성능을 보장한다.

### 변경 가능한 값
- 객체 타입의 값, 즉 객체는 변경 가능한 값이다. 원시 값은 변경 불가능한 값이므로 원시 값을 갖는 변수의 값을 변경하려면 재할당말고는 방법이 없지만, 객체는 재할당 없이 직접 변경할 수 있다 프로퍼티를 동적으로 추가하거나 값을 갱신, 값을 삭제할 수 있다.
- 보통 원시 타입을 참조한 변수들은 원시 타입 자체의 주소를 참조 하지만 객체를 참조한 변수는 그 객체를 참조 하고 있는 참조값을 참조한 변수라고 할 수 있다.
    - 원시 값은 read only 값이다.
- 객체는 크기가 클수도 작을 수도 있다 이를 복사해서 생성하는 비용은 많이 들고 메모리가 효율적으로 사용되기 힘들다 따라서 구조적인 단점을 보안하고자한 설계라고 할 수 있다. 다만, 이러한 설계에 부작용이 있다.`여러 개의 식별자가 하나의 객체를 공유할 수 있다`는 것이다.
> 객체를 프로퍼티 값으로 갖는 객체의 경우 얕은 복사는 한단계만 복사하는 것이고 깊은 복사는 내부의 객체도 복사하는 것을 의미한다.

## 참조에 의한 전달
- 참조에 의한 전달은 참조하고 있는 참조값을 복사하여 전달하는 것으로 엄밀히 말하면 값을 전달한 것이라고 할 수 있으나, 그 값이 다른 메모리 공간을 참조하는 참조값이다. 한마디로 말하면  두개의 식별자가 하나의 객체를 공유한다는 의미이다.




# 함수
- 일련의 과정을 구현하고 코드 블록으로 감싸 하나의 실행 단위로 정의한 것

## 함수의 정의
- 함수의 정의 방법 4가지
```js
// 함수 선언 : 호이스팅되어 가장 위로 올라가서 런타임 이전에 평가단계에서 먼저 실행된다
var add = new Function("x,y","return x + y;");

var add = function(x,y){
    return x + y;
};

function add(x,y){
    return x + y;
};

var add = (x,y) => x + y;

// 함수 호출
var result = add(2,5);
```
> 변수는 선언이라고 하고, 함수는 정의라고 표현한다. 함수 선언문이 평가되면 식별자가 암묵적으로 생성하고 객체가 할당된다, ECMAScript 사양에서도 변수는 선언 함수는 정의라고 표현한다.

## 함수 사용 이유
- 코드의 중복을 없애는 코드 재사용
- 유지보수의 편의성을 높이고 실수를 줄여 코드의 신뢰성을 높인다.
- 적절한 함수 이름을 통해 구현을 이해하지 않고도 사용할 수 있도록 하여 코드의 가독성 향상시킨다.
## 함수 리터럴
- 자바스크립트의 함수는 객체 타입의 값이다.
- 함수 이름
    - 함수 이름은 식별자로 네이밍 규칙을 준수해야 함.
    - 함수 이름은 몸체 내에서만 참조할 수 있는 식별자.
    - 함수 이름은 생략할 수 있다. 이름이 있는 함수는 기명 함수, 없는 함수를 익명함수라 한다.
- 매개변수 목록
    - 0개 이상의 매개변수를 소괄호로 감싸고 쉼표로 구분
    - 각 매개변수에는 함수를 호출할 때 지정한 인수가 순서대로 할당, 즉 매개변수의 목록은 순서에 의미가 있다.
    - 매개변수는 함수 내부에서 변수이다. 즉,식별자로 네이밍 규칙을 지켜야함
- 함수 몸체
    - 함수가 호출되었을 때 일괄적으로 실행될 문들을 하나의 실행단위로 정의한 코드 블럭
    - 함수 몸체는 함후 호출에 의해 실행
- 함수는 객체이다. 다만 일반 객체와의 차이점은 일반 객체는 호출할 수 없지만, 함수는 호출 할 수 있다.

### 함수 선언문

```js
function add(x,y){
    return x + y;
}
// 함수 선언문 : 함수 선언문은 함수 이름을 생략할 수 없다.
// 표현식이 아닌 문으로서 완료값이 undefined가 출력된다.

var add = function add(x,y){
    return x + y;
}
// 이와 같은 경우는 변수에 대입할 수 있는 표현식으로 해석된다.
// 문맥에 따라 문 or 표현식으로 해석된다.

console.log(add(2,5));
```
- 함수는 함수의 이름으로 호출하는 것이 아니라 함수 객체를 가리키는 식별자로 호출한다.



### 함수 표현식
- 자바스크립트의 함수는 객체 타입의 값, 프로퍼티의 값, 배열의 요소가 될 수 있다. 이와 같은 객체를 `일급객체`라고 부른다. 자바스크립트의 함수는 `일급 객체`다.

```js
var add = function foo(x,y){
    return x + y;
};

console.log(add(2,5)); // 7
console.log(foo(2,5)); // ReferenceError
// 함수의 이름은 함수 몸체 내부에서만 유효한 식별자다.
```

### 함수 생성 시점과 함수 호이스팅
```js
console.dir(add); //f add(x,y)
console.dir(sub); //undefined

// 함수 선언문
function add(x,y){
    return x + y;
}

// 함수 표현식
var sub = function(x,y){
    return x - y;
};
```

- 함수 선언문으로 정의한 함수와 함수 표현식으로 정의한 함수의 생성 시점이 다르다.
- 함수 선언문은 코드의 선두로 끌어 올려진 것 처럼 동작하는 함수 호이스팅을 진행한다.
- 변수 할당문의 값은 할당문이 실행되는 시점, 즉 런타임에 평가되므로 함수 리터럴도 할당문이 실행되는 시점에 평가되어 함수 객체가 된다. 이같은 함수 호이스팅 때문에 함수 선언문 대신 함수 표현식을 사용할 것을 권장한다.

