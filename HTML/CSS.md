---
title: CSS
---

# CSS

## CSS의 선언방식
1. 내장방식
1. 링크방식
1. 인라인방식
1. @import방식


### 내장방식
```html
<style>
 선택자{속성:값;}
</style>
```
- 위와 같이 `<style>` 태그 안에 작성되는 방식

### 링크방식
```html
<link rel="stylesheet" href="./css/main.css" />
```
- `<link/>` 로 외부 CSS문서를 가져와 연결하는 방식
- 가장 많이 쓰이는 방식이다. (CSS파일을 모듈화 할 수 있다.)

### 인라인방식

```html
<div style="color:red; margin:20px">
    요소에 style속성으로 직접 CSS를 적용하는 방식
</div>
```
- 요소에 직접 style 속성으로 적용하는 방식으로 우선순위가 가장높다


### @import방식

```css
/* main.css */
@import("./box.css");

/* 생략 */
```
- CSS문서 내부에 또 다른 CSS문서를 연결하는 방식




## CSS의 구성요소

```css
선택자{속성:값; 속성:값;}
```
- 선택자 : CSS(스타일)을 적용할 대상
- 속성 : CSS(스타일)의 종류
- 값 : CSS(스타일)의 값


## CSS의 선택자
1. 기본선택자
1. 복합선택자
1. 가상 클래스 선택자
1. 가상 요소 선택자
1. 속성 선택자

---
### 기본 선택자

#### 전체 선택자
```css
* {
    color:red;
}
/* 모든 요소를 선택한다 */
```
#### 태그 선택자
```css
div{
    color:red;
}
/* div태그에 적용하는 태그 선택자 */
```
#### 클래스 선택자

```css
.classValue{
    color:red
}
/*  전역속성 class의 값이 classValue인 태그를 선택하는 선택자 */
```
- `.(클래스값) { }`의 형태로 존재한다.

#### 아이디 선택자
```css
#idValue{
    color:red;
}
/* 전역속성 id의 값이 idValue인 태그들에 적용 */
```
---
### 복합선택자
#### 일치선택자
```css
span.orang{
    color:orange;
}
```
- 띄어 쓰기 없이 두 선택자를 연속으로 쓰면 AND의 의미로 둘 모두를 만족하는 선택자를 선택한다
    - 위 태그는 sapn태그이면서 클래스속성의 값이orange인 태그를 선택한다.

#### 자식선택자
```css
ul > .orange{
    color:orange
}
```
- `>`로 두 선택자를 연결하면 자식선택자를 선택한다.
    - 위 태그는 ul태그 자식태그중 클래스값이 orange인 태그를 선택한다

#### 하위선택자
```css
div .orange{
    color:orange;
}
```
- 두 선택자를 띄어쓰기로 연결하면 하위선택자를 선택한다
    - div태그의 하위선택자들 중에 클래스 값이 orange인 요소들을 선택한다

#### 인접 형제 선택자
```css
.orange + li {
    color: red;
}
```
- 두 선택자를 + 로 연결하면 인접 형제 선택자로 앞 선택자의 형제 선택자중 첫번째를 선택한다
    - 클래스값이 orange인 요소의 형제중 바로 다음 li요소를 선택한다

#### 일반 형제선택자
```css
.orange ~ li{
    color:red;
}
- 선택자의 형제선택자중 앞 선택자보다 뒤쪽에 위치한 모든 형제선택자를 선택한다.
```
---
### 가상 클래스 선택자

#### HOVER
```css
a:hover{
    color:red;
}
/* a태그에 마우스커서를 올리면 글자색이 red가 된다는 의미 */
```
- `선택자:hover{}`의 형태로 마우스 커서를 올리면 적용을 한다는 의미

#### ACTIVE
```css
a:active{
    color:red;
}
/* 마우스를 클릭하는 동안 a태그가 빨강색이 된다는 의미 */
```
- `선택자:active{ }`의 형태로 마우스 클릭을 하면 적용을 한다는 의미

#### FOCUS
```css
input:focus{
    background-color:orange;
}
/* 마우스로 선택되었던... 포커스가 가면 배경색이 오렌지가 된다는 의미 */
```
- `선택자:focus { }`의 형태로 포커스가 가면 적용을 한다는 의미

#### FIRST CHILD
```css
.fruits span:first-child{
    color:red;
}
/* 클래스값이 fruits인 요소의 하위요소인 span태그들 중 첫번째 요소에 적용 */
```
- 선택자의 형제 요소중 첫번째를 선택하여 적용
- 선택요소가 첫번째가 아니라면 선택되지않음
#### LAST CHILD
```css
.fruits h3:last-child{
    color:red;
}
/* 클래스값이 fruits인 요소의 하위요소인 h3태그들 중 마지막 요소에 적용 */
```
- 선택자의 형제 요소중 마지막 요소에 적용

#### nth-child(n)
```css
.fruits *:nth-child(2){
    color:red;
}
/* fruits의 하위요소중 2번째를 선택하여 적용 */
.fruits *:nth-child(2n){
    color:red;
}
/* fruits의 하위요소중 짝수를 선택하여 적용 */

.fruits *:nth-child(2n+1){
    color:red;
}
/* fruits의 하위요소중 홀수를 선택하여 적용 */


.fruits *:nth-child(n+2){
    color:red;
}
/* fruits의 하위요소중 두번째 요소부터 적용 */
```
- n번째 자식요소를 선택하여 적용하는 가상 클래스 선택자로서 n은 제로 베이스로 0을 포함하는 양의정수를 의미한다.

#### 부정 선택자
```css

.fruits *:not(span){
    color:red;
}
/* fruits의 하위요소들 중에  sapn요소를 제외하고 전부에 적용*/
```
- 부정선택자는 그것만을 제외하고 선택할 때 사용한다

### 가상 요소 선택자

#### BEFORE
```css
.box::before{
    content:"앞";
}
/* before는 해당하는 요소의 앞에 요소를 추가 */
```
- 가상요소 선택자에는 `content:value`가 필수로 추가된다.
- `before`는 선택 요소 앞에 요소를 추가한다는 의미

#### after
```css
.box::after{
    content:"앞";
}
/* before는 해당하는 요소의 앞에 요소를 추가 */
```
- 가상요소 선택자에는 `content:value`가 필수로 추가된다.
- `after`는 선택 요소 뒤에 요소를 추가한다는 의미

### 속성선택자
```css
[type] {
    color:red;
}
/* type 속성을 가진 모든 요소에 적용한다 */
[type="text"] {
    background-color:red;
}
/* 속성= 값 의 형태로도 진행할 수 있다. */
```
- [속성]으로 선택하여 해당 속성을 가진 모든 요소에게 적용한다


## 스타일 상속
- 모든 글자/문자 관련 CSS 속성들은 하위 요소들에게도 상속되는 특징을 가진다.


## 선택자 우선순위
### 우선순위
- 같은 요소가 여러 선언의 대상이된 경우, 어떤 선언을 요소에 적용할지 결정하는 우선순위

1. 점수가 높은 선언에 우선한다
1. 점수가 같으면 나중에 해석된 선언이 우선됨


```css
div {color:red !important;} 
/* !important 99999999999점 */
#collor_red { color:red;}
/* 아이디 선택자 100 점 */
.color_yellow{color:yellow;}
/* 클래스 선택자 10점 */
div { color:white;}
/* 태그 선택자 1점 */
* { color:pink;}
/* 전체 선택자 0점 */
```
```html
<div style="color:red;">
1000점
</div>
```



