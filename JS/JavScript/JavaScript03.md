---
title: JS03
---

# JavaScript

## 브라우저 플랫폼(Browser Object)
- Browser Object는 브라우저가 기본으로 제공하는 객체들을 의미한다.

### 브라우저 플랫폼의 기능
- UI(동적 문서)
    - `Document Object (DOM)`
    - Cascading Style Sheets
- HTML5 API 멀티미디어,네트워크 통신,로컬 저장소
    - Graphics and Media
    - Web Application API
    - Internet Platform API

### Browser Object

#### window
- 브라우저의 하나의 창을 조작하는 객체
- `Adress Bar`를 조작할 수 있도록 하는 도구로 `window.location`이 존재
- `History`를 조작할 수 있도록 하는 도구로 `window.history`가 존재
    - 뒤로가기,앞으로가기 등을 HISTORY로 볼 수 있다
- Viewport내에 다양한 요소(HTML태그)들을 조작할 수 있도록 하는 객체로 `window.document`객체를 제공한다
- 이 외에도 window.screen 이나 window.navigator등도 제공

#### window Method
- `alert()`
- `confirm()`
- `prompt()`
- setTimeout()
- clearTimeout()
- setInterval()
- clearInterval()

```js
var x = 3;
var y = 0;
window.alert(x+y);
// window는 생략이 가능하다

var x,y;
x = prompt("x 값을 입력하세요",0);
// 1입력
y = prompt("y 값을 입력하세요",0);
// 2입력
alert((typeof x) +"," + (typeof y));
//(prompt()를 통해 받은 x,y는 문자열 형태로 받아온다)
// string,string으로 출력됨
x = parseInt(x);
y = parseInt(y);
// paseInt("12abc"); return 12; 숫자 + 문자는 숫자만 리턴해준다.
alert(x+y);

var answer = confirm("정말로 삭제하실 생각인가요?");
if(answer){
    alert("삭제되었습니다.");
}else{
    alert("삭제되지 않았습니다");
}
// cofirm 메서드로 브라우저에 확인 창을 띄운다.

```

#### window Properties
- status
- defaultStatus

### 이벤트 기반의 프로그래밍
- 이벤트 발생시 스크립트 실행을 위한 방법을 제공하여, 액션에 따른 행위를 사용할 수 있다
```html
<script>
    // 페이지가 읽혀질 때 실행된다.
        function printResult(){
            var x, y;
            x = prompt("x 값을 입력하세요",0);
            y = prompt("y 값을 입력하세요",0);
            alert(x+y);
        }
</script>

<input type="button" value="출력" onclick="scriptCode" />
    <!--  이벤트가 발생될 때 실행된다 -->
<input type="button" value="출력" onclick="printResult();" />
<!-- 위와 같이 스크립트 태그 안에 정의된 함수를 불러올 수 있다. -->
```


### 엘리먼트 객체 이용하기

`HTML -(Load)-> Document Object (DOM) -(show)-> User Interface`

- DOM을 수정하면 인터페이스가 수정되고, 인터페이스를 사용자가 수정하면 DOM객체의  속성 값들이 변경된다.

### 인터페이스 수정하기
```html
    <script>
        function printResult(){
            var x,y;
            var btnPrint = document.getElementById("btn-print");
            x = prompt("x 값을 입력하세요",0);
            y = prompt("y 값을 입력하세요",0);
            x = parseInt(x);
            y = parseInt(y);
            btnPrint.value = x + y;
            btnPrint.type = "text";
        }
         function init(){
            var btnPrint = document.getElementById("btn-print");
            // HTML ID 컨벤션은 카멜표기법이 아니고 단어사이에 대쉬로 구분한다.
            btnPrint.onclick=printResult;
            //()괄호가 없이 함수 객체를 대입 해야한다.
        }
        window.onload = init;
        // onload는 load가 되었을 대를 의미하고 window객체는 가장 먼저 생성되기 때문에 오류가 생기지 않는다.
         

    </script>
        <input type="button" value="출력"  id="btn-print" />
```

- `btnPrint.value = x + y;`를 통해서 인터페이스의 value 속성을 변경한다.
- `window.onload = init;`를 통해 window가 load되면 init을 실행하도록 한다.
    - window.onload에 서로 다른영역에서 대입하면 대체하여 앞에꺼는 삭제된다.



### 익명 함수
- 보통 이벤트 상황에 함수 사용할 때는 익명함수를 주로 사용한다


```js
        window.onload = function(){
            var btnPrint = document.getElementById("btn-print");
            btnPrint.onclick= function(){
                var x,y;
                x = prompt("x 값을 입력하세요",0);
                y = prompt("y 값을 입력하세요",0);

                x = parseInt(x);
                y = parseInt(y);
                btnPrint.value = x + y;
                btnPrint.type = "text";
            };
        };


```


### 코드 분리와 이벤트 바인딩 방법 두 가지

### MVC(Model View Controller)
- View 와 Controller를 물리적으로 나누기

```html
<!-- index.html -->
<!-- VIEW -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="index.js"></script>
    <title>Document</title>
</head>
<body>
        <input type="button" value="출력"  id="btn-print" />
</body>
</html>

```

```js
// index.js
// CONTROLLER
 window.onload = function(){
            var btnPrint = document.getElementById("btn-print");
            btnPrint.onclick= function(){
                var x,y;
                x = prompt("x 값을 입력하세요",0);
                y = prompt("y 값을 입력하세요",0);

                x = parseInt(x);
                y = parseInt(y);
                btnPrint.value = x + y;
                btnPrint.type = "text";
            };
        };

```
- `window.onload`에 두 가지 이상의 함수를 추가 할 수는 없다.
    - 이 때, `window.addEventListener()`로 누적할 수 있도록 할 수 있다.
    ```js
    window.addEventListener("load",function(){
        alert("test1");
    });
    window.addEventListener("load",function(){
        alert("test2");
    });
    ```
    