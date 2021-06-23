---
title : 페이지 모듈화와 요청 흐름 제어
---

# 페이지 모듈화와 요청 흐름 제어

## `<jsp:include>` 액션 태그를 이용한 공통 영역 작성

`<jsp:include>` 태그 처리 순서
1. main.jsp가 웹 브라우저의 요청을 받는다.
2. [출력내용 A]를 출력 버퍼에 저장한다.
3. `<jsp:include>`가 실행되면 요청 흐름을 sub.jsp로 이동한다.
4. [출력내용 B]를 출력 버퍼에 저장한다.
5. sub.jsp의 실행이 끝나면 요청 흐름이 다시 main.jsp의 `<jsp:include>`로 돌아온다.
6. `<jsp:include>` 이후 부분인 [출력내용 C]를 출력 버퍼에 저장한다.
7. 출력 버퍼의 내용을 응답 데이터로 전송한다.

### `<jsp:include>` 액션 태그 사용법

`<jsp:include>` 액션 태그의 기본 사용방법은 다음과 같다

```xml
<jsp:include page="포함할페이지sub.jsp" flush="true" />
```
- page : 포함할 JSP 페이지의 경로 지정
- flush : 지정한 JSP페이지를 실행하기 전 출력버퍼를 플러시할지 여부를 지정 default는 'false'


### `<jsp:include>`액션 태그를 이용한 중복 영역 처리
- 상단메뉴,좌측메뉴 등 공통되는 부분이 존재할 때 `<jsp:include>`액션태그로 중복된 코드를 제거할 수 있다. 이와 같이 중복을 제거하면 유지보수 측면에서도 한 곳에서만 수정할 수 있다는 장점이 존재한다.



### `<jsp:param>`으로 포함할 페이지에 파라미터 추가하기
- `<jsp:param>`태그를 이용해 포함할 JSP 페이지에 파라미터를 추가할 수 있다.

```xml
<jsp:include page="포함할페이지sub.jsp" flush="true" />
    <jsp:param name="param1" value="value1" />
    <jsp:param name="param2" value="value2" />
</jsp:include>
```

- `<jsp:param>` 액션 태그는  `<jsp:include>`의 자식태그로 사용된다 해당 name 속성과 value 속성은 포함할 페이지에서 `파라미터=값`으로 입력된다.

```java
<%
	String param1 = request.getParameter("param1");
    String param2 = request.getParameter("param2");
	if (param1 == null||param2 == null) {
		return;
	}
%>
```
- 위와 같은 방법으로 파라미터를 받는다.

#### `<jsp:param>` 액션 태그와 캐릭터 인코딩
```java
<% 
    request.setCharacterEncoding("utf-8");
%>
```
- 위와 같은 방법을 통해 `<jsp:param>`이 전달한 파라미터 값을 인코딩 할 수 있는데 이 인코딩 타입이 알맞지 않으면 올바르게 전달되지 않는다.


### include 디렉티브를 이용한 중복된 코드 삽입
- include 디렉티브를 통해 다른 파일의 내용을 현재 위치에 삽입한 후 JSP 파일을 자바 파일로 변환하고 컴파일 하는 방식

#### include 디렉티브의 처리 방식과 사용법

```java
-- main.jsp
<%@ include file="sub.jspf(포함할파일)" %>
```

1. main.jsp 의 page 디렉티브위치에 포함할 페이지의 코드를 삽입시킨다.
1. 삽입시킨 코드를 자바 코드로 작성한다
1. 자바코드를 서블릿 클래스로 컴파일 한다.

#### include 디렉티브의 특성
- 코드를 합쳐 컴파일 하기 때문에 각자 선언한 변수등을 공유하게 된다.
- 합쳐지는 코드의 확장자를 구분하기 위해 `.jspf`로 하는 편이다.


#### include 디렉티브의 활용
- include 디렉티브는 직접 jsp코드를 포함하기 때문에 액션태그와는 다른 용도로 사용한다, 액션태그는 레이아웃의 한 구성요소를 모듈화하기 위해 사용되는 반면, include디렉티브는 
    - `모든 JSP 페이지에서 사용할 수 있는 변수 지정`
    - `저작권 표시와 같이 모든 페이지에 중복되는 간단한 문장`

#### 코드 조각 자동 포함 기능
- web.xml에 지정하여 모든 파일에 자동 코드 삽입을 시키는 기능

```xml
<jsp-config>
    <jsp-property-group>
        <url-pattern>/view/*</url-pattern>
        <include-prelude>/common/variable.jspf</include-prelude>
        <include-coda>/common/footer.jspf</include-coda>
    </jsp-property-group>
</jsp-config>
```

- `<jsp-property-group>` : JSP의 프로퍼티를 포함한다
- `<url-pattern>` : 프로퍼티를 적용할 JSP파일의 URL 패턴을 지정
- `<include-prelude>` : url-pattern 태그에 지정한 패턴에 해당하는 JSP 파일의 앞에 삽입할 파일을 지정
- `<include-coda>` : url-pattern 태그에 지정한 패턴에 해당하는 JSP파일의 뒤에 삽입할 파일을 지정한다.


#### `<jsp:include>` 액션 태그와 include 디렉티브의 비교

|비교항목|`<jsp:include>`|`include디렉티브`|
|------------|----------------------------|------------------------|
|처리시간|요청 시간에 처리|JSP 파일을 자바 소스로 변환할 때 처리|
|기능|별도의 파일로 요청 처리 흐름을 이동|현재 파일에 삽입시킴|
|데이터 전달법|request 기본 객체나 <jsp:param>을 이용한 파라미터 전달|페이지 내 변수를 선언한 후 변수 값에 저장|
|용도|화면의 레이아웃의 일부분을 모듈화 할 때 주로 사용|다수의 JSP페이지에서 공통으로 사용되는 변수를 지정하는 코드나 저작권 같은 문장 포함|

## `<jsp:forward>` 액션 태그를 이용한 JSP 페이지 이동
- `<jsp:forward>` 액션 태그는 하나의 JSP페이지에서 다른 JSP페이지로 요청 처리를 전달할 때 사용.
    1. 웹브라우저가 요청을 보냄
    1. 요청을 받은 JSP파일에서 `<jsp:forward>`액션 태그를 실행
    1. `<jsp:forward>`로 요청 처리 흐름을 다른 JSP파일로 이동시킴
    1. 요청 흐름이 이동할 때 이전 JSP페이지에서 사용한 request기본 객체와 response 기본 객체가 전달됨
    1. 이동된 JSP페이지에서 응답 결과를 생성하여 전송

> 한 곳에서가 아니라 요청흐름을 이동시켜가면서 까지 여러곳에서 실행하는 이유는 "간결하고 구조적으로 웹/JSP 프로그래밍을 할 수 있기 때문" 개발진행 과정에서 다양한 조건에 따라 다른 처리가 필요한 상황이 존재하는데 이럴 때 `<jsp:forward>`를 이용해 각 조건을 처리하는 JSP를 분리하여 기능별로 모듈화 할 수 있게 된다.

### `<jsp:forward>` 액션 태그 사용법

```xml
<jsp:forward page="이동할 페이지"/>
```
- 웹 브라우저의 주소는 변경되지 않고, 리다이렉트 처럼 주소 변경이 되지 않는다.

### `<jsp:forward>`액션 태그와 출력 버퍼
- `<jsp:forward>`가 실행되면 출력 버퍼의 내용을 버리고 이동한 페이지의 출력결과를 출력 버퍼에 저장하기 때문에 이전 페이지의 출력결과가 나오지 않는다.
- `<jsp:forward>`태그가 정상 동작하기 위해서는 `<jsp:forward>` 액션 태그 실행 전 웹 브라우저에 데이터가 전송되면 안된다. 출력 버퍼를 플러시한 이후에는 `<jsp:forward>`액션태그가 작동하지 않는다.
    - 규약상 위 내용이 올바르나 WAS마다 결과 값이 다를 수 있다.

### `<jsp:forward>` 액션 태그의 활용

```java
<%@ page contentType = "text/html; charset=utf-8" %>
<%
    String forwardPage = null;

    // 조건에 따라 이동할 페이지 지정
    if(조건판단1){
        forwardPage="페이지URI1";
    } else if (조건판단2) {
        forwardPage="페이지URI2";
    }else {
        forwardPage="페이지URI3";
    }
%>
<jsp:forward page="<%= forwardPage %>" />
```
- 페이지 조건에 따라 다른 페이지로 이동하는 기능

### `<jsp:param>` 액션 태그를 이용해서 이동할 페이지에 파라미터 추가
```xml
<jsp:forward page="moveTo.jsp"/>
    <jsp:param name="first" value="BK" />
    <jsp:param name="last" value="Choi" />
</jsp:forward>
```

### `<jsp:include>`와 `<jsp:forward>`의 경로
- 웹 어플리케이션 폴더를 기준으로한 절대 경로
- 현재 JSP 페이지를 기준으로 한 상대 경로

### 기본객체를 이용하여 값 전달하기
- `<jsp:param>`을 이용해서 값을 전달하면 String 타입만을 전달 할 수 있기 때문에 포함하거나 이동할 페이지는 동일한 요청범위(request 범위) 갖기 때문에. request 기본 객체의 속성을 이용해 필요한 값을 전달할 수 있다.

- request객체는 한번 요청에 대해 유효하게 동작하며 한 번의 요청을 처리하는데 사용되는 모든 JSP에 공유된다.

```jsp
/* makeTime.jsp */
<%@ page contentType = "text/html; charset=utf-8" %>
<%@ page import = "java.util.Calendar" %>
<%
	Calendar cal = Calendar.getInstance();
	request.setAttribute("time", cal);
%>
<jsp:forward page="../to/viewTime.jsp" />
```

```jsp
/* viewTime.jsp */
<%@ page contentType = "text/html; charset=utf-8" %>
<%@ page import = "java.util.Calendar" %>
<html>
<head><title>현재 시간</title></head>
<body>

<%
	Calendar cal = (Calendar) request.getAttribute("time");
%>
현재 시간은 <%= cal.get(Calendar.HOUR) %>시
			<%= cal.get(Calendar.MINUTE) %>분
			<%= cal.get(Calendar.SECOND) %>초 입니다.
</body>
</html>
```

> 속성을 이용한 값 전달 방식은 웹 어플리케이션 개발에서 중요한 기법중 하나로 MVC(Model-View-Controller)패턴이라는 것에 기반하여 웹 앱을 구현할때 필수요소이기 때문