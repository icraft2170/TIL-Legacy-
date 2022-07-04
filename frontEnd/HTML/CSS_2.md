---
title: css2
---

# CSS 속성

- 박스 모델
- 글꼴,문자
- 배경
- 배치
- 플렉스(정렬)
- 전환
- 변환
- 띄움
- 애니메이션
- 그리드
- 다단
- 필터


## 박스모델

### width,height
- 요소의 가로/세로 너비를 선택
- default: auto
- 단위: px,em,vw등 단위 선택
- 인라인 요소는 가로 세로 너비를 지정할 수 없어 사용할수 없음
- EX) `width:300px; height:200px` 

### max-width/max-height/min-width/min-height
- 최대 최소 너비 높이 제한을 걸 수 있다.


### 단위
- px : 픽셀
- %  : 퍼센트
- em : 요소의 글꼴 크기
- rem : 루트 요소(html)의 글꼴 크기
- vw : 뷰포트 가로 너비의 백분위
- vh : 뷰포트 세로 너비의 백분위  

### `margin`
- 요소의 외부 여백을 지정한다
- defalut : 0
- 음수 사용 가능, auto(브라우저가 여백 계산)
- `margin:0;` top,bottom,right,left 모두 0
- `margin:10px 20px;` top,bottom 10px right,left 20px로 지정
- `margin:10px 20px 30px;` top 10px left right는 20px bottom 30px로 지정
- `margin:10px 20px 30px 40px;` top 10px right는 20px bottom 30px left 40px로 지정
- margin-방향(top,bottom...)의 형태로도 지정 가능

### `padding`
- 요소의 내부 여백 지정
- defalut : 0
- 음수 사용 가능, auto(브라우저가 여백 계산),%사용 가능
- `padding:0;` top,bottom,right,left 모두 0
- `padding:10px 20px;` top,bottom 10px right,left 20px로 지정
- `padding:10px 20px 30px;` top 10px left right는 20px bottom 30px로 지정
- `padding:10px 20px 30px 40px;` top 10px right는 20px bottom 30px left 40px로 지정
- padding-방향(top,bottom...)의 형태로도 지정 가능

### `border`
- 요소의 테두리선을 지정한다
- `border: 선두께(border-width) 선종류(border-style) 선색(border-color)`의 형태로 지정가능
- 선 종류는 대표적으로 none(선 없음), solid(실선)
- `border-raidus:10px` 요소의 모서리를 둥글께 깎는다(반지름 10px)


### `box-sizing`
- 요소의 크기 계산 기준을 정한다
- `content-box` 디폴트로 요소의 내용으로 크기계산
- border-box 요소의 내용 + border + padding로 크기계산


### overflow
- 요소의 크기 이상으로 내용이 넘쳤을 때, 보여짐 제어 속성
- visible : 기본 값으로 넘친 내용을 그대로 보여준다
- hidden : 넘친 내용을 숨김
- scroll : 넘친 내용을 잘라냄, 스크롤바 생성
- auto : 넘친 내용이 있는 경우에만 잘라내고 스크롤바 생성
- overflow-x,overflow-y로 좌우 지정 가능

### `display`
- 요소의 화면 출력 특성 지정
- `block, inline, inline-block`으로 블럭요소 ,인라인요소 , 인라인-블록요소로 변경가능
- `flex` : 플렉스 박스 사용 (1차원)
- `grid` : 그리드 (2차원)
- none : 화면에서 사라짐

### `opacity`
- 요소의 투명도 지정
- `1`: 불투명
- `0 ~ 1` : 0이상 1미만의 소수점으로 투명도 지정


## 글꼴

### font-style
- 글자의 기울기
- normal(기본값),italic 등

### font-weight
- 글자의 두께(가중치)
- normal(400 기본 두께, 기본 값)
- bold(700 두껍게)
- 100 ~ 900: 100 단위로 지정가능

### font-size
- 16px(기본 크기)
- 단위 px,em,rem등

### line-hieght
- 한 줄의 높이, 행간
- `숫자`:요소의 글꼴 크기의 배수
- 단위 : px,em,rem등


## 문자

### color
- 글자 색상지정
- 기본값은 rgb(0,0,0)[검정색]

### text-align
- 문자 정렬방식
- left(기본값),right,center

### text-decoration
- 문자의 장식(선)
- none(기본값:선 없음),underline:밑줄,line-through :중앙선

### text-indent
- 문자 첫 줄의 들여쓰기
- 0(기본 값: 들여쓰기 없음)
- 단위 px,em,rem
- 음수는 내어쓰기

## 배경

### background-color
- 요소의 배경 색상
- `transparent(기본값:투명함)`

### background-image
- 요소의 배경 이미지 지정
- none(이미지 없음), `url("경로")`
- `background-image:url("경로");`형태로 작성


### background-repeat
- 요소 배경 이미지 반복여부
- `repeat(기본값:이미지 수직수평으로 반복)`
- repeat-x,repeat-y : 수직 또는 수평으로 반복
- `no-repeat` : 반복 없음

### backgroud-position
- 요소의 배경 이미지 위치
- 방향 : top,bottom,left,right,center 방향
- 단위 : px,em,rem등

### background-size
- 배경 이미지 크기지정
- `auto(기본값)`
- 단위 : px,em,rem등
- `cover`: 비율을 유지, 요소의 위아래,좌우 너비중 더 넓은 쪽에 맞춤
- `contain` 비율을 유지, 요소의 위아래,좌우 너비중 더 짧은 쪽에 맞춤

### background-attachment
- 배경 이미지의 스크롤 특성 지정
- `scroll(기본값)` : 이미지가 요소를 따라서 같이 스크롤
- fixed : 이미지가 뷰포트에 고정, 스크롤 X

## 배치

### `position`
- 요소의 위치 지정 기준 
- `static(기본요소)` : 기준 없음
- `relative` : 요소 자신을 기준(원래 배치된 위치 기준) 
- `absolute` : 위치 상 부모 요소를 기준(부모요소의 위치 지정 기준이 존재하는 부모요소를 찾는다.)
- fixed : 뷰포트를 기준
- position 속성의 값으로 absolute, fixed가 지정된 요소는, 
display 속성이 block으로 변경됨


### `top,bottom,left,right`
- 요소의 각 방향별 거리지정(position으로 결정된 기준 위치부터)
- auto(기본값:브라우저가 계산)
- 단위 : px,em,rem등



### 요소 쌓임 순서(Stack order)
- 어떤 요소가 사용자와 더 가깝게 있는지(위에 쌓이는지) 결정

1. 요소에 position 속성의 값이 있는 경우 위에 쌓임.(기본값 static 제외) 
2. 1번 조건이 같은 경우, z-index 속성의 숫자 값이 높을 수록 위에 쌓임. 
3. 1번과 2번 조건까지 같은 경우, HTML의 다음 구조일 수록 위에 쌓임

### z-index
- 요소의 쌓임 정도를 지정한다
- 숫자가 높을 수록 위에 쌓임


## 플렉스 (정렬)
- `display:flex;`로 지정하여 정렬 방식을 수직 -> 수평으로 바꿈
- display:inline-flex;로 지정하면 수평 정렬을 하면서 콘텐츠 크기만큼 좌우 크기가 줄어듬

### flex-direction
- 주 축을 설정한다.
- row(기본값: 행 축을 주축으로 좌->우)
- row-reverse 행축(우->좌)

### flex-wrap
- flrx items를 묶는다 (줄바꿈 여부 결정)
- nowrap(기본값 : 묶음(줄바꿈) 없음)
- wrap : 여러줄로 묵음
- wrap으로 지정하면 뷰포트 크기가 줄어들면 요소가 아래로 내려간다

### `justify-content`
- 주 축의 정렬방법을 정한다
- flex-start(기본값:Flex Items를 시작점으로 정렬)
- flex-end:Flex Items를 끝점으로 정렬
- center:Flex Items를 가운데로 정렬

### `align-content`
- 교차 축의 여러 줄 정렬 방법
- stretch (기본값:Flex Items를 시작점으로 정렬)
- flex-start : Flex Items를 시작점으로 정렬
- flex-end : Flex Items를 끝점으로 정렬
- center : Flex Items를 가운데 정렬

### `align-items`
- 교차 축의 한 줄 정렬 방법
- stretch (기본값:Flex Items를 교차축으로 늘림)
- flex-start : Flex Items를 시작점으로 정렬
- flex-end : Flex Items를 끝점으로 정렬
- center : Flex Items를 가운데 정렬

### order
- FLEX ITEM의 순서
- `0` (기본값 : 순서 없음)
- `숫자` : 숫자가 작을 수록 먼저
### flex-grow
- Flex Item의 증가 너비 비율
- `0` (기본값 : 증가 비율 없음)
- `숫자` : 증가 비

### flex-shrink
- Flex Item의 감소 너비 비율
- `0` (기본값 : 감소 비율 없음)
- `숫자` : 감소 비

### flex-basis
- Flex Item의 공간 배분 전 기본 너비
- auto(기본값:요소의 Content 너비)
- 단위 :px,em,rem등


## 전환

### `transition`
- 요소의 전환(시작과 끝) 효과를 지정하는 단축 속성
```
transition: 속성명 지속시간(필수포함) 타이밍함수 대기시간;
속성명 : transition-property
지속시간 : transition-duration
타이밍함수 : transition-timing-function 
대기시간 : transition-delay
```

### transition-property
- 전환 효과를 사용할 속성 이름을 지정
- `all(기본값 : 모든 속성에 지정)`
- 속성이름을 값으로 준다

### transition-duration
- 전환 효과의 지속시간을 지정
- 0s(기본값), 시간

### transition-timing-function
- 전환효과에 타이밍 함수 지정
- ease(기본값 : 느리게-빠르게-느리게)
- linear,ease-in,ease-out,ease-in-out

### transition-delay
- 전환 효과가 몇 초 뒤에 시작할지 대기시간을 지정
- 0s(기본값), 시간을 초 단위로 지정한다.

## 변환

### transform
- transform : 변환함수1 변환함수2, 변환함수3 ...;
- transform : 원근법 이동 크기 회전 기울임;

### 변환함수(2D)
- translate(x,y),translateX(x), translateY(y) : 이동 X,Y축 
- scale(x,y) : 크기(x,y축)
- rotate(degree): 회전(각도)
- skew(x,y), skewX(x), skewY(y) : 기울임(X,Y축)

### 변환함수(3D)
- rotateX(x),rotateY(y): 회전(x축), 회전(y축)
- perspective(n) : 원근법(거리)


### perspective
- 하위 요소를 관찰하는 원근 거리 지정
- 단위 : px


### backface-visibility
- 3D 변환으로 회전된 요소의 뒷면 숨김 여부
- visible(기본값:뒷면 보임)
- hidden( 뒷면 숨김 )
