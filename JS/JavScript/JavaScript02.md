---
title: JSON
---

# JSON(JavaScript Object Notation)



### JavaScript Object

- Boolean
    - `var n = new Boolean(true);`
- Number
    - `var n = new Number(3);`
- String
    - `var s = new String("hello");`
- Array
    - `var ar = new Array();`
- Object
    - `var ob = new Object();`


### JSON 표기
- Boolean
    - `var n = true;`
- Number
    - `var n = 3;`
- String
    - `var s = "hello";` , `var s = 'hello';`
    - 최근에는 싱글 쿼테이션을 자주 사용하는데 스크립트에서 사용될 때 더블 쿼테이션이 충돌이 생길 수 있는 경우가 많이 생기기 때문.
- Array
    - `var ar = [];`
```js
var ar = [3,4,5,6,exam,[7,8,9]];

console.log(ar[5][1]);
//8
```
- Object
    - `var ob = {};`
```js
    var exam = {
        "kor":30,
        "eng":70,
        "math":80
    }
console.log("총점 :" + (exam.kor + exam.eng + exam.math));
// 총점 180    
```    


```js
var notice = [
    {"id":1,"title":"hello json"},
    {"id":2,"title":"hello JS"},
    {"id":3,"title":"hello ME"}
];

console.log(notice[2]);
```
- 최근에는 위와 같이 데이터를 구분하기 위한 표현하는 방법으로 JSON을 많이 사용한다
    - XML,CSV,JSON등이 비슷한 역할을 한다.


### EVAL()
- 문자열 형태의 JavaScript를 실행해준다

#### Eval()를 통해 String으로 JSON 받기

```js
var data = `[ \
        {"id":1,"title":"hello json"}, \
        {"id":2,"title":"hello JS"}, \
        {"id":3,"title":"hello ME"} \
    ]`;
// (띄어쓰기)\ 는 여러줄 문자열을 저장하기 위한 방법

    eval("var ar = " + data + ";" );

    console.log(ar[1].id);
```

### JSON parser

### Object 선언하는 다양한 방식

```js
var data = {"id":1,"title":"arae"};
var data2 = {id:1,title:"arae"};
```
- Key값에 대한 더블 쿼테이션은 생략이 가능하다

### Json parser
```js
var data = JSON.parse('{"id":1,"title":"arae"}');
console.log(data.title);
// area
var data2 = JSON.parse('{id:1,title:"arae"}');
console.log(data2.title);  
// undefined
```
- Json parser를 사용할 때는 KEY값에는 더블 쿼테이션이 반드시 필요하다
```js
    var json = JSON.stringify(data2);
    alert(json);
```
- JSON표기법의 더블 쿼테이션은 JSON.stringify()메서드를 통해 추가할 수 있다.



## 자바 스크립트 제어구조

### 조건문
- if, while, do-while
### 반복문
- while, for, for-in
### 선택문
- else, else if, switch

```js
    var arr = ['hello','hi','greeting'];
        var ob = {id:1,title:"hello",writeID:"hyeonho"};

        for( var i=0;i<arr.length; i++){
            document.write( arr[i] + "<br />");
        }

        for( var i in arr){
            document.write( arr[i] + "<br />");
        }
        // JS의 FOR IN은 KEY값을 꺼내온다    
        for( var i in ob){
            document.write( ob[i] + "<br />");
        }
        // object 사용방법중 []를 통해 사용하는 방법을 통해 KEY값으로 결과를 뽑아낼 수 있다.

```

## 함수와 표현식

### 함수의 정의
- 자바스크립트 에서 함수는 `객체`이다
```js
var add = new Function("x,y","return x + y;");
// 함수의 정의 new Function("파라미터","구현부");
alert(add(3,4));
// 함수의 사용

var add = function(x,y){
    return x + y;
};

function add(x,y){
    return x + y;
};
```

### 함수의 파라미터(매개변수)
- JS에서 함수는 객체이고 추가 파라미터를 받아줄 `arguments`라는 내용이 내부적으로 탑재되어있다. 

```js
function add(x,y){
    alert(arguments[10]);

    return x + y;
};

document.write(add(3,4,5,9,8,1,4,5,8,7,"hello"));
// hello(alert로)
// 7
```

### 변수의 가시영역과 전역변수
- var의 선언 변수는 정적인 방식으로 생성된다.(지역변수)

- globar 변수는 동적인 방식으로 생성(전역변수)
```js
a = 1;
// window.a = 1;로 선언된다.
// 전역객체 Windwo의 속성으로 추가된다.
```
- 지역변수의 우선순위가 전역변수의 우선순위보다 높다.
```js
a = 1;
// window.a = 1;이라는 의미
var a = 2;
a++;
// var a = 2로 선언한 지역변수 2에 증감연산자를 붙인 의미
// 우선순위는 지역변수가 높다.
```
- 함수 내에서 전역변수 사용의 유의점
```js
function f1(){
    a = 3;
}
f1();
alert(a);
// f1()함수의 지역에 a가 전역변수로 선언되었기 때문에 지역 외부에서 사용할 수 있게된다
```


### 변수의 생명주기와 클로저(Closure)
- JS는 함수를 객체로 만들기 때문에 

```js
function f1(){
    var a = 1;
// f1()의 지역변수 a는 f2가 참조하고 있기 때문에 자원을 닫고 있지 못하고 생명주기가 계속 이어지고 있다.
    return function f2(){
        return a;
    }
    // f1()함수의 변수 a의 생명주기를 끝내는 키를 가진 f2()를 클로져 라고 부른다
}

var f = f1();
var a = f();
 
alert(a);
```




