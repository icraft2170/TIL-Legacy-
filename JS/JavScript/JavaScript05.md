---
title: javascript
---

# Event Object

- Event
    - UIEvent
        - FocusEvent
        - MouseEvent
            - WheelEvent
        - InputEvent
        - KeyboardEvent
        - CompositorEvent
- CustomEvent        


## Event target Attribute (event.target)
- Event target은 Event가 적용된 엘리먼트(요소)를 가르킨다.

```js
//Ex1-선택된 이미지 보여주기:event target
window.addEventListener("load", function(){

    
    var section = this.document.querySelector("#section1");

    var imgs = section.querySelectorAll(".img");
    var currentImg = section.querySelector(".current-img");
    

    for(var i = 0; i < imgs.length;i++){
        imgs[i].onclick = function(e){
            currentImg.src = e.target.src;
        };
    }

}); 

```

## 이벤트 버블링

### 버블링을 사용한 사용자 이벤트 처리
- 버블링이란, 하위 태그의 발생한 이벤트를 상위 태그감 감시하여 반응 할 수 있음을 의미한다. 단, 상위 태그 영역에 작용한 모든 event에 적용된다.

```js
//Ex2-이벤트 버블링을 이용해 사용자 이벤트 처리하기:event Bubbling
window.addEventListener("load", function(){

    var section = document.querySelector("#section2");
    var imgList = section.querySelector(".img-list"); 
    var currentImg = section.querySelector(".current-img");
    
    imgList.onclick = function(e){
        if(e.target.nodeName != "IMG"){
            return;
        }
        currentImg.src = e.target.src;
    };
});  
```


### 이벤트 버블링 정지
- `e.stopPropagetion();`를 이용하여 버블링(전파)를 막는다.
```js
// Ex3-이벤트 버블링 멈추기
window.addEventListener("load", function(){

    var section = document.querySelector("#section3");
    
    var imgList = section.querySelector(".img-list"); 
    var addButton = section.querySelector(".add-button");
    var currentImg = section.querySelector(".current-img");
    
    imgList.onclick = function(e){
        if(e.target.nodeName != "IMG"){
            return;
        }
        currentImg.src = e.target.src;
    };

    addButton.onclick = function(e){
        e.stopPropagetion();
        var img = document.createElement("img");
        img.src = "images/img1.jpg";
        currentImg.insertAdjacentElement("afterend",img);
    };

}); 
```

### 여러 버튼을 가진 화면에서 이벤트 처리

```js
// Ex4
window.addEventListener("load", function(){

    var section = document.querySelector("#section4");
    
    var tbody = section.querySelector(".notice-list tbody");

    tbody.onclick = function(e){
        var target = e.target;
        if(target.nodeName != "INPUT")
            return;
        
        if(target.classList.contains("sel-button")){
            var tr = target.parentElement;
            for(;tr.nodeName !="TR"; tr = tr.parentElement);
            tr.style.background = "yellow";
        }else if(target.classList.contains("edit-buuton")){

        }else if(target.classList.contains("del-buuton")){

        }            
    
    
    };

}); 

```

### 엘리먼트 기본 행위 막기
- `event.preventDefault()`를 사용하면 해당요소의 기본 효과를 막을 수 있다

```js
// Ex4
window.addEventListener("load", function(){

    var section = document.querySelector("#section4");
    var tbody = section.querySelector(".notice-list tbody");

    tbody.onclick = function(e){

        e.preventDefault();

        var target = e.target;
        if(target.nodeName != "INPUT"&&target.nodeName != "A")
            return;

        if(target.classList.contains("sel-button")){
            var tr = target.parentElement;
            for(;tr.nodeName !="TR"; tr = tr.parentElement);
            tr.style.background = "yellow";
        }else if(target.classList.contains("edit-buuton")){

        }else if(target.classList.contains("del-buuton")){

        }            
    
    
    };

}); 
```

### DOM Event Object Interface

- https://developer.mozilla.org/ko/docs/Web/Events


## DOM Event 트리거

- 파일을 첨부하는 기능을 가진 버튼은 브라우저마다 고정이 되어있다, 그런데 이 디자인이 브라우저 마다 서로 달라 클로스 브라우징에 문제가 생기고 이에, 원래 기능을 하는 버튼을 보이지 않게 하고 다른 버튼을 통해 간접적으로 실행하게 하는 방법을 사용한다. 이때 간접적으로 사용하기위해 쓰는 버튼을 `트리거`라고 한다.

```js
var fileButton = document.getElementById("file-button");
fileButton.addEventListener("click",function(){
    var event = new MouseEvent("click",{
        'view': window,
        'bubbles':true,
        'cancelable':true
    });
    // IE는 지원하지 않는 방법
    // var event = document.createEvent("MouseEvent");
    // event.initEvent("click",true,true); [eventType,bubbles,cancelable]

    var file = document.getElementById("gallery-file");
    file.dispatchEvent(event);
});
```

### Click 위치에 박스 옮기기(마우스 이벤트 객체)

```js
//Ex6 - 마우스 이벤트 포지션
window.addEventListener("load",function(){
    var section = document.querySelector("#section6");
    var container = section.querySelector(".container");
    var box = section.querySelector(".box");
    container.onclick = function(e){
        // e.x,e.y
        console.log("(x,y):" + e.x +"," + e.y);
        box.style.position = "absolute";
        box.style.left = e.x + "px";
        box.style.top = e.y + "px";
    }
});

```
- 페이지 영역

- 옵셋 영역

- 클라이언트 영역



```js
//  클라이언트 영역의 x,y
e.x
e.y
// 페이지 영역의 x,y
e.pageX
e.pageY
// 옵셋 영역 x,y
e.offsetX
e.offsetY
```
