---
---

# JavaScript

##

```html
<!-- javascript1-dom.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="javascript1-dom.js"></script>
    <title>Document</title>
</head>
<body>
        <section>
            <h1>Ex1 : 계산기 프로그램</h1>
            <div>
                <input id="txt-x" type="text" value = "0" dir="rtl"  />
                +
                <input id="txt-y" type="text" value = "0" dir="rtl" />
                <input id="btn-add" type="button" value="=">
                <input id="txt-sum" type="text" value = "0" readonly dir="rtl" />
            </div>
        </section>
        <hr>
</body>
</html>
```
```js
// javascript1-dom.js 
window.addEventListener("load",function() {
    var txtX = document.getElementById("txt-x");
    var txtY = document.getElementById("txt-y");
    var btnAdd = document.getElementById("btn-add");
    var txtSum = document.getElementById("txt-sum");
    
    btnAdd.onclick= function(){
       var x = parseInt(txtX.value);
       var y = parseInt(txtY.value);
       txtSum.value = x + y;
    };
});
```



### 노드 선택방법 개선


#### 태그를 지정하기
```html
<section id="sec1">
    <h1></h1>
    <ul>
        <li>번호1</li>
        <li>번호2</li>
        <li>번호3</li>
    </ul>
</section>    
```

- 각각의 요소에 ID값을 주는 것이 아니라 섹션의 그룹으로 묶고 섹션별로 선택할 수 있도록 한다.

```js
var lis = sec1.getElementsByTagName("li");
// sec1 내부에 존재하는 모든 li태그들을 lis의 배열형태로 저장한다.
lis[0].textContent = "Hello";
// 태그 내부의 내용
```
- 해당 방식은 id값을 줄일 수 있는나. 태그 순서에 영향을 받아 코드 수정과 유지보수에 좋지 않음


```html
<section id="sec1">
    <h1></h1>
    <ul>
        <li>번호1</li>
        <li>번호2</li>
        <li>번호3</li>
    </ul>
</section>    
```

#### 클래스로 지정하기

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="javascript1-dom.js"></script>
    <title>Document</title>
</head>
<body>
        <section id="section2">
            <h1>Ex2 : 엘리먼트 선택방법 개선</h1>
            <div>
                <input type="text" class="txt-x" value = "0" dir="rtl"  />
                +
                <input type="text" class="txt-y" value = "0" dir="rtl" />
                <input type="button" class="btn-add" value="=">
                <input type="text" class="txt-sum" value = "0" readonly dir="rtl" />
            </div>
        </section>
        <hr>
</body>
</html>
```
- 각 선택지에 class와 그 값을 지정해준다.

```js
window.addEventListener("load",function() {
    var section2 = document.getElementById("section2");
    var txtX = section2.getElementsByClassName("txt-x")[0];
    var txtY = section2.getElementsByClassName("txt-y")[0];
    var btnAdd = section2.getElementsByClassName("btn-add")[0];
    var txtSum = section2.getElementsByClassName("txt-sum")[0];
       btnAdd.onclick= function(){
       var x = parseInt(txtX.value);
       var y = parseInt(txtY.value);
       txtSum.value = x + y;
    };
});
```
- 섹션 그룹을 가져오고 그 내부 클래스를 가져온다, 이 때 클래스로 가져온 내용들은 배열이기 때문에 배열의 값을 가져오는 형태를 가추어야 하고. 배열로 가져오는 이유는 class 속성의 특징을 생각해보면 알 수 있다.


## Selector API

- `querySelector`,`querySelectorAll`을 통해 CSS의 Selector형식으로 해당 요소들을 지정해서 불러올 수 있다.
- `querySelector`는 하나의 요소 `querySelectorAll`는 여러 요소를 배열 형태로 가져온다.


```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="javascript1-dom.js"></script>
    <title>Document</title>
</head>
<body>
        <section id="section3">
            <h1>Ex3 : Selectors API</h1>
            <div>
                <input type="text"  name="txt-x" value = "0" dir="rtl"  />
                +
                <input type="text" name="txt-y" value = "0" dir="rtl" />
                <input type="button" class="btn-add" value="=">
                <input type="text" class="txt-sum" value = "0" readonly dir="rtl" />
            </div>
        </section>
        <hr>
</body>
</html>
```    


```js
// Ex3 : Selectors API Level1
window.addEventListener("load",function() {
    var section3 = document.getElementById("section3");
    var txtX = section3.querySelector("input[name='txt-x']");
    var txtY = section3.querySelector("input[name='txt-y']");
    // 태그 선택자를 통해 가져 왔다.
    var btnAdd = section3.querySelector(".btn-add");
    var txtSum = section3.querySelector(".txt-sum");
   // 클래스 선택자를 통해 가져왔다.

    btnAdd.onclick= function(){
       var x = parseInt(txtX.value);
       var y = parseInt(txtY.value);
       txtSum.value = x + y;
    };
});
```

## ChildNodes
- document 요소의 자식 노드들을 선택하는 메서드이다. 다만, 노드에는 공백및 주석 역시 포함되기 때문에 활용이 어렵다

## children
- document 요소의 자식 노드들을 선택하는 메서드이다. 다만, 노드들중 `태그들만` 선택해 준다.

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="javascript1-dom.js"></script>
    <title>Document</title>
</head>
<body>
            <section id="section4">
            <h1>Ex4 : ChildNodes를 이용한 노드 선택</h1>
            <div class="box">
                <input />
                <input />
            </div>
        </section>
        <hr>
</body>
</html>

```

```js
// Ex4 : Child Nodes를 이용한 노드 선택
window.addEventListener("load",function() {
    var section4 = document.querySelector("#section4");
    var box = section4.querySelector(".box");
    
    var input1 = box.children[0];
    var input2 = box.children[1];        

    input1.value="hello";
    input2.value="event";


});
```

---

## 노드의 종류(Type)

- Document(9)
    - DocumentType(10)
    - Element(1)
        - Attr(2)
        - Entity(6)
        - EntityReference(5)
        - Text(3)
    - Comment(8)
    - CDATASection(4)
    - Notation(12)        


``` html
DocumentType(10)
-> <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML ..." > 문서 타입
Element(1)
-> <p><textarea><font> <태그> 태그들
Attr(2)
-> rows = "30" , cols="40" <태그 `Attribute="값"`> 속성들
Entity(6)
->  &lt; &nbsp; &gt; 와 같은 특수문자를 사용하는 키워드들
Text(3)
-> <p>Text</p> 태그 내부의 텍스트들
Comment(8)
->  <!-- Comment --> 주석을 의미
CDATASection(4)
-> <![CDATA[<,>]]> 특수문자를 HTML에 자유롭게 사용할 수 있는 방법
Notation(12)
-> <font color="ffff00" size="10px" >에서 16진법 색표기라던가 px과 같은 표기법 의미
```

## Node Interface
>https://www.w3.org/TR/ 참고문헌