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

