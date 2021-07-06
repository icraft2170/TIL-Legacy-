---
title: JavaScript
Date: 2021-07-04
author: 손현호
---

# JavaScript

- HTML파일이 `Load`되면 `Document Object(DOM)`객체가 생성되고 사용자 인터페이스로 보여지는데(`Show`) JavaScript는 Document Object를 Controll하는 방법을 제공한다.
- `Document Object(DOM)과 Window Object,URL`을 다루는 기능을 제공한다.
    - window, window.location, window.history, window.document


## JavaScript 탄생

-  불필요한 데이터 전송으로 서버 리소스의 낭비가 발생하였고, 전송하는 데이터에 대한 유효성 검사의 필요성 부각
    - Netscape사에서 LiveScript라는 언어를 내놓았고, 정식 버젼 출시하면서 JavaScript라는 이름으로 변경하였다.

- 유효성 검사를 위한, `form Object`가 존재했고 해당 객체를 이용하여 입력값을 확인하여 유효성 검사가 가능하였다.




## 스크립트 코드 작성

```html
<html>
    <head>
        <script>
            // 스크립트 코드
        </script>
    </head>
    <body>
        <script>
            // 스크립트 코드
        </script>
        <!-- 컨텐츠 -->
        <script>
            // 스크립트 코드
        </script>
    </body>
</html>
```
- 스크립트 코드는 `html파일`내에서 위치와 개수의 제약이 존재하지 않고, `<script></script>`코드 안에만 작성해주면 된다.


## JavaScript Data

### JS's Type
```JavaScript
var x = 3;
```
- 자바스크립트는 동적 타이핑(Dynamic Typing)을 지원해서 자료형을 컴파일이 아닌 런타임에 결정하여 자료형을 명확하게 정해주지 않아도 실행 가능하다.
- var는 참조타입으로 var로 생성된 언어는 선언되어 공간이 생성된후 그 공간에 데이터를 담는 동적 타이핑과는 다르게 값이 사용 될 때 그 값에 맞는 공간을 갖고, 그 공간을 참조한다. 이것을 우리는 `Autoboxing`이라고 한다
    - 자바스크립트는 타입이 아닌 Wrapper형 클래스들로 구성되어 박싱될 수 있다. 
- 참조타입변수는 객체의 주소를 저장하고 있지만, OOP 개념적으로는 객체의 이름을 나타낸다고 볼 수 있다.
- string, number, boolean, null, undefined, symbol와 같은 6개의 원시타입으로 이루어짐


### Wrapper
    - var로 선언된 변수가 어떤 메서드를 사용할 수 있는지는 할당되는 객체(Wrapper)에 따라 달라진다.
    - String, Number, Boolean, Symbol 원시타입과 대응하는 4가지 Wrapper object가 존재한다.

#### Boolean

#### Number
- 정수와 실수를 표현한다
```javascript
var x = 3;
var y = new Number(3);
//  위 두 내용은 같은 내용이다.
var z; 
// 정의되지 않은 값 (undefined)
if(z==undefined){
    // true
} 
```
#### String
- 문자와 문자열을 표현한다



### Array Object

####  push / pop 메서드를 이용한 데이터 관리 (`Stack 구조`)
```javascript
var nums = new Array();
nums.push(5);
// Stack구조 맨 하단에 5를 넣는다
var n1 = nums.pop();
// Stack구조 맨 위에서 데이터를 뽑는다.
```
- push/pop은 Stack형에 데이터 구조로 `FILO(First In Last Out)`의 형태를 지원한다.
- pop()을 사용시 데이터는 사라진다

#### List
```javascript
var nums = new Array();

nums[0] = 5;
alert(nums[0]);
nums[1] = 10;
alert(nums[1]);
nums[2] = 15;
alert(nums[2]);
```
- `배열(List)형`으로 데이터를 저장할 수 있다.

```javascript
var nums = new Array();

nums[3] = 5;

alert(nums.length);
// 4
alert(nums[0]);
alert(nums[1]);
alert(nums[2]);
// null
```

#### 배열 객체 초기화

```js
var nums = new Array();
var nums = new Array(5);
// 5개에 방을 가진 배열 생성
var nums = new Array(5, 10, 20);
// 생성자의 파라미터가 2개 이상이면 각 배열 데이터의 값으로 해석
var nums = new Array(5,10,20,"hello");
// javaScript에서 배열에 타입을 일관되지 않아도 가능하다
alert(typeof nums[3]);
var nums = new Array(5,10,20,"hello",new Array(2,3,4));
// 배열 내부에 배열을 넣는 것도 가능하다
alert(nums[4][1]);
// 3
```

#### splice() 메서드 이용 (List)
```js
var nums = new Array(5,10,20,"hello");

nums.splice(1)
// 1번 위치부터 지워라
nums.splice(1,2)
// 1번 위치부터 2개를 지워라
nums.splice(2,1,"hoho")
// 2번째에 1개를 지우고 hoho를 추가 (3번째 위치를 hoho로 변경)
nums.splice(2,0,"hoho")
// 2번째 위치에 hoho를 추가
```
- `splice(n)` n번 위치부터  삭제
- `splice(n,cnt)` n번 위치부터 cnt개 삭제
- `splice(n,cnt,replace)` n번 위치부터 cnt개 삭제하고 replace 추가


### JavaScript OOP?
- 동적인 객체 정의를 지원한다 autoBoxing

#### JavaScript OOP
- prototype
- class

#### 동적 객체 정의
```js
var exam = new Object();
//Expand Object
exam.kor = 30;
exam.eng = 70;
exam.math = 80;

alert("총점 :" + (exam.kor + exam.eng + exam.math));
//(exam.kor + exam.eng + exam.math)가 문자로 변경된다.
```
- 따로 정의하지 않아도 확장하여 사용할 수 있기 때문에, 대소문자등 구분을 확실히 해야 한다.

### Object(Map) 생성

```js
var exam = new Object();

var key = "eng";

exam["kor"] = 30;
exam[key] = 70;
exam["math"] = 80;
// MAP(Object) 형 exam
alert(exam["kor"]);
```
- 기본적으로 아래와 같은 방법으로 객체 생성과정을 이행하는것을 권고









