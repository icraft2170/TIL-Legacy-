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

- 노드 뒤 소괄호의 숫자는 `EventTarget` 인터페이스에 지정되어 있는 숫자


## Node Interface
>https://www.w3.org/TR/ 참고문헌


## 노드 속성 변경


```html
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
        <section id="section5">
            <h1>Ex5 : 엘리먼트 노드의 속성변경</h1>
            <div>
                <input class="src-input" list="img-list" > 
                <datalist id="img-list">
                    <option value="img1.jpg">img1</option>
                    <option value="img2.jpg">img2</option>
                    <option value="img3.jpg">img3</option>
                </datalist>

                <select class="img-select">
                    <option value="img1.jpg">img1</option>
                    <option value="img2.jpg">img2</option>
                    <option value="img3.jpg">img3</option>
                </select>
                <input type="button" class="chage-button" value="변경하기" />
            </div>
            <div>
                <img class="img" src="images/img1.jpg"/>
            </div>
        </section>
        <hr>


    </body>
</html>

```

```js
//Ex5 : 엘리먼트 노드 속성 변경
window.addEventListener("load",function() {
    var section = document.querySelector("#section5");
    var srcInput = section.querySelector(".src-input");
    var imgSelect = section.querySelector(".img-select");
    var chageButton = section.querySelector(".chage-button");
    var img = section.querySelector(".img");

    chageButton.onclick=function(){
        // img.src = "images/" + srcInput.value;
        img.src = "images/" + imgSelect.value;
    };

});
```


### 텍스트 노드 추가하기

1. 텍스트 노드 생성
`var txt = document.createTextNode("안녕하세요");`

2. 텍스트 노드를 추가할 엘리먼트 노드 선택
`var div1 = document.getElementById("div1");`

3. 엘리먼트 노드에 텍스트 노드 추가(Append) 하기
`div1.appendChild(txt);`



### 엘리먼트 노드 추가/삭제

1. 엘리먼트 노드를 생성하고 자식노드에 추가하는 방법
```js
        var title = titleInput.value;
        var txtNode = document.createTextNode(title);

        var aNode = document.createElement("a");
        aNode.href = "";
        aNode.appendChild(txtNode);        
        
        var liNode = document.createElement("li");
        liNode.appendChild(aNode);


        menuListUl.appendChild(liNode);
```

2. innerHTML을 활용하는 방법
```js
    // 할 때마다 새로운 값 대입
    menuListUl.innerHTML = '<li><a>' + title + '</a></li>';
    // 뒤에 추가하는 방법, 단 할 때마다 추가가 아니라 추가한 코드로 전부 재생산하기 때문에 효율 떨어짐
    menuListUl.innerHTML += '<li><a href="">' + title + '</a></li>';
```
3. innerHTML과 appendChild동시 사용

```js
// menuListUl.innerHTML += '<li><a href="">' + title + '</a></li>';의 성능 이슈를 막아준다
var title = titleInput.value;

var html = '<a href="">' + title + '</a>'
var li = document.createElement("li");
li.innerHTML = html;
menuListUl.appendChild(li);
// append 라는 메서드도 추가되었는데, 노드를 여러개 넣거나, String의 텍스트도 넣을 수 있다.
```

```js
// Node 삭제 다른 방법
var liNode = menuListUl.children[0];
// menuListUl.removeChild(liNode);
liNode.remove();
// 자식이 아닌 자기 자신을 삭제하는 방법도 존재
```

## 노드 복제 및 템플릿 
```html
       <section id="section8">
            <h1>Ex8- 노드 복제와 템플릿 태그 </h1>
            <div>
                <input type="button" class="clone-button" value="복제" />
                <input type="button" class="template-button" value="템플릿 복제" />
            </div>
            
            <table class="notice-list">
                <thead style="border: 1px solid;">
                    <tr>
                        <td>번호</td>
                        <td>제목</td>
                        <td>작성일</td>
                        <td>작성자</td>
                        <td>조회수</td>
                    </tr>
                    <tbody>
                        <tr>
                            <td>1</td>
                            <td><a href="1">자바스크립트란 </a></td>
                            <td>2019-01-25</td>
                            <td>손현호</td>
                            <td>0</td>
                        </tr>
                        <tr>
                            <td>2</td>
                            <td><a href="2">자바스크립트란 </a></td>
                            <td>2019-01-27</td>
                            <td>손현호</td>
                            <td>0</td>
                        </tr>
                        <tr>
                            <td>3</td>
                            <td><a href="3">자바스크립트란 </a></td>
                            <td>2019-01-25</td>
                            <td>손현호</td>
                            <td>0</td>
                        </tr>
                        <tr>
                            <td>4</td>
                            <td><a href="4">자바스크립트란 </a></td>
                            <td>2019-01-25</td>
                            <td>손현호</td>
                            <td>0</td>
                        </tr>
                        <tr>
                            <td>5</td>
                            <td><a href="5">자바스크립트란 </a></td>
                            <td>2019-01-25</td>
                            <td>손현호</td>
                            <td>0</td>
                        </tr>
                    </tbody> 

                </thead>
            </table>

        </section>
        <hr>

```

```js
// 노드 복제
window.addEventListener("load",function() {
    var notices =[
        {id:5,title:"퐈이야~",regDate:"2019-01-26",writeId:"손현호",hit:0},
        {id:6,title:"복제각",regDate:"2019-01-26",writeId:"손현호",hit:17}
    ]
    var section = document.querySelector("#section8");
    
    var noticeList = section.querySelector(".notice-list");
    var tbodyNode = section.querySelector("tbody"); 
    var cloneButton = section.querySelector(".clone-button");
    var templateButton = section.querySelector(".template-button");

    cloneButton.onclick = function(){
        var trNode = noticeList.querySelector("tbody tr")
        var cloneNode = trNode.cloneNode(true);
        // false는 껍데기만 복제 true는 자식노드까지 복제
        var tds = cloneNode.querySelectorAll("td");
        tds[0].textContent = notices[0].id;
        tds[1].innerHTML = '<a href="' +notices[0].id+ '">' +notices[0].title+ '</a>';
        tds[2].textContent = notices[0].regDate;
        tds[3].textContent = notices[0].writeId;
        tds[4].textContent = notices[0].hit;


        tbodyNode.append(cloneNode);
    };
    templateButton.onclick = function(){

    };
});
```
- `cloneNode(true/false);` 를 통해 해당 Node를 복제 할 수 있다
    - true는 하위 노드까지 전부 복제
    - false는 틀만 복제

### 템플릿 생성

```html

```
```js
// 템플릿 생성
<section id="section8">
            <h1>Ex8- 노드 복제와 템플릿 태그 </h1>
            <div>
                <input type="button" class="clone-button" value="복제" />
                <input type="button" class="template-button" value="템플릿 복제" />
            </div>
            <template>
                <tr>
                    <td>1</td>
                    <td><a href="1">자바스크립트란</a></td>
                    <td>2019-01-25</td>
                    <td>손현호</td>
                    <td>0</td>
                </tr>
            </template>


            <table class="notice-list">
                <thead style="border: 1px solid;">
                    <tr>
                        <td>번호</td>
                        <td>제목</td>
                        <td>작성일</td>
                        <td>작성자</td>
                        <td>조회수</td>
                    </tr>
                    <tbody>
                    </tbody> 

                </thead>
            </table>

        </section>
```

```js
// Ex8 : 엘리먼트 노드의 속성 & CSS 속성 변경
window.addEventListener("load",function() {
    var notices =[
        {id:5,title:"퐈이야~",regDate:"2019-01-26",writeId:"손현호",hit:0},
        {id:6,title:"복제각",regDate:"2019-01-26",writeId:"손현호",hit:17}
    ]
    var section = document.querySelector("#section8");
    
    var noticeList = section.querySelector(".notice-list");
    var tbodyNode = section.querySelector("tbody"); 
    var cloneButton = section.querySelector(".clone-button");
    var templateButton = section.querySelector(".template-button");

    cloneButton.onclick = function(){
        var trNode = noticeList.querySelector("tbody tr:first-child")
        var cloneNode = trNode.cloneNode(true);
        // false는 껍데기만 복제 true는 자식노드까지 복제
        var tds = cloneNode.querySelectorAll("td");
        tds[0].textContent = notices[0].id;
        tds[1].innerHTML = '<a href="' +notices[0].id+ '">' +notices[0].title+ '</a>';
        tds[2].textContent = notices[0].regDate;
        tds[3].textContent = notices[0].writeId;
        tds[4].textContent = notices[0].hit;

        tbodyNode.append(cloneNode);
    };
    templateButton.onclick = function(){
        var template = section.querySelector("template");
        var cloneNode = document.importNode(template.content, true);
        // false는 껍데기만 복제 true는 자식노드까지 복제
        var tds = cloneNode.querySelectorAll("td");
        tds[0].textContent = notices[0].id;
        // tds[1].innerHTML = '<a href="' +notices[0].id+ '">' +notices[0].title+ '</a>';
        var aNode = tds[1].children[0];
        aNode.href = notices[0].id;
        aNode.textContent = notices[0].title;
        tds[2].textContent = notices[0].regDate;
        tds[3].textContent = notices[0].writeId;
        tds[4].textContent = notices[0].hit;

        tbodyNode.append(cloneNode);
    };
});
```

- `document.importNode(template.content, true);`를 통해 해당 template의 content로 import한다

## 노드 삽입과 바꾸기

```html
        <section id="section9">
            <h1>Ex8-노드 삽입과 바꾸기</h1>            
            <div>                
                <input type="button" class="up-button" value="위로" />                
                <input type="button" class="down-button" value="아래로" />
            </div>
            <table border="1" class="notice-list">
                <thead>
                    <tr>
                        <td>번호</td>
                        <td>제목</td>
                        <td>작성일</td>
                        <td>작성자</td>
                        <td>조회수</td>
                    </tr>
                </thead>
                <tbody>
                    <tr style="background: lightblue;">
                        <td>1</td>
                        <td><a href="1">자바스크립트란..</a></td>
                        <td>2019-01-25</td>
                        <td>newlec</td>
                        <td>2</td>
                    </tr>
                    <tr>
                        <td>2</td>
                        <td><a href="2">유투브에 끌려다니지 않으려고 했는데....ㅜㅜ..</a></td>
                        <td>2019-01-25</td>
                        <td>newlec</td>
                        <td>0</td>
                    </tr>
                    <tr>                        
                        <td>3</td>
                        <td><a href="3">기본기가 튼튼해야....</a></td>
                        <td>2019-01-25</td>
                        <td>newlec</td>
                        <td>1</td>
                    </tr>
                    <tr>
                        <td>4</td>
                        <td><a href="4">근데 조회수가 ㅜㅜ..</a></td>
                        <td>2019-01-25</td>
                        <td>newlec</td>
                        <td>0</td>
                    </tr>
                </tbody>
            </table>
        </section>
        <hr />
```
```js
window.addEventListener("load", function(){

    var section = document.querySelector("#section9");
    
    var noticeList =section.querySelector(".notice-list"); 
    var tbodyNode = noticeList.querySelector("tbody");
    var upButton = section.querySelector(".up-button");
    var downButton = section.querySelector(".down-button");

    var currentNode = tbodyNode.firstElementChild;

    downButton.onclick = function(){
        var nextNode = currentNode.nextElementSibling;
        if(nextNode == null){
            alert("더 이상 이동 할 수 없습니다");
            return;
        }
        tbodyNode.insertBefore(nextNode,currentNode);
    };

    upButton.onclick = function(){
        var previousNode = currentNode.previousElementSibling;
        if(previousNode == null){
            alert("더 이상 이동 할 수 없습니다");
        }
        tbodyNode.insertBefore(currentNode,previousNode);

    };
});
```
- `insertBefore(newChild: Node, refChild: Node)`를 활용하여 삭제하고 추가하는 방식으로 진행한다.

### targetElement.insertAdjacentElement(position,element);
- `position`
    - beforebegin
    - afterbegin
    - beforeend
    - afterend
```html
<!-- beforebegin -->
<p>
<!-- afterbegin -->
<!-- beforeend -->
</p>
<!-- afterend -->
```

```js
window.addEventListener("load", function(){

    var section = document.querySelector("#section9");
    
    var noticeList =section.querySelector(".notice-list"); 
    var tbodyNode = noticeList.querySelector("tbody");
    var upButton = section.querySelector(".up-button");
    var downButton = section.querySelector(".down-button");

    var currentNode = tbodyNode.firstElementChild;

    downButton.onclick = function(){
        var nextNode = currentNode.nextElementSibling;
        if(nextNode == null){
            alert("더 이상 이동 할 수 없습니다");
            return;
        }
        // tbodyNode.removeChild(nextNode);
        // tbodyNode.insertBefore(nextNode,currentNode);
        currentNode.insertAdjacentElement("beforebegin",nextNode);
    };

    upButton.onclick = function(){
        var previousNode = currentNode.previousElementSibling;
        if(previousNode == null){
            alert("더 이상 이동 할 수 없습니다");
        }
        // tbodyNode.removeChild(currentNode);
        // tbodyNode.insertBefore(currentNode,previousNode);
        currentNode.insertAdjacentElement("afterend",previousNode);
    };
});
```
- 자리 바꾸던 예제를 이렇게 바꿀 수 도 있다.


## 다중 엘리먼트 삭제방법과 노드의 자리바꾸기

```js


```