---
title: JSP_03
---

# JSP의 구성요소

## Page 디렉티브
- JSP 페이지에 대한 설정 정보를 지정할 때 사용
- `<%@ ~ %>` 로 작성
- JSP가 제공하는 디렉티브

|디렉티브|설명|
|:-------:|:----------------------------------------------------------------|
|page|JSP 페이지에 대한 정보를 지정. JSP가 생성하는 문서의 타입으로 출력 버퍼의 크기, 에러 페이지 등 JSP 페이지에서 필요로 하는 정보 설정|
|taglib|JSP 페이지에서 사용할 태그 라이브러리 지정|
|include|JSP 페이지의 특정 영역에 다른 문서를 포함시킨다.|


### Page 디렉티브의 주요 속성

|속성|설명|기본값|
|:------:|------------------------------------|-------------------|
|`contentType`|JSP가 생성할 문서d의 MIME 타입과 캐릭터 인코딩 지정|text/html|
|`import`|JSP 페이지에서 사용할 자바 클래스 지정||
|`session`|JSP 페이지가 세션을 사용할지 여부를 지정|true|
|buffer|JSP페이지의 출력 버퍼 크기 지정|최소 8kb|
|autoFlush|출력 버퍼가 다 찼을 경우 자동으로 버퍼에 있는 데이터를 출력 스트림에 보내고 비울지 여부를 나타낸다|true|
|info|JSP 페이지에 대한 설명을 입력||
|`errorPage`|JSP 페이지를 실행하는 도중에 에러가 발생할 때 보여줄 페이지를 지정||
|isErrorPage|현재 페이지가 에러가 발생할 때 보여주는 페이지인지의 여부를 지정|false|
|pageEncoding|JSP 소수 코드의 캐릭터 인코딩을 지정||
|isELIgnored|true이면 표현언어를 문자열로 처리|false|
|deferredSyntaxAllowedAsLiteral|`#{`문자가 문자열 값으로 사용되는 것을 허용할지의 여부를 지정|false|
|trimDirectiveWhitespaces|출력 결과에서 템플릿 텍스트의 공백 문자를 제거할지의 여부 지정|false|

### contentType 속성과 charset

- JSP 페이지가 생성할 문서의 MIME 타입지정
    - text/html, text/xml, application/json 등이 존재
- `<%@ page contentType="text/html; charset=utf-8" %>` 형태로 구성된다.
    - charset은 생략될 수 있다.

### import 속성
- `<%@ page import="java.util.Calendar,java.util.*" %>`와 같은 형태로 사용하여 클래스를 사용할 수 있도록 함.

### trimDirectiveWhitespaces 속성
- `<%@ page trimDirectiveWhitespaces="true" %>`로 코드 내 불필요한 줄바꿈 공백문자를 제거한다.

### Encoding과 pageEncoding 속성
- JSP가 캐릭터 셋을 결정하는 과정
    1. 파일이 BOM으로 시작하지 않을 경우,
        1. 기본 인코딩으로 처음 읽고, pageEncoding속성을 확인해서 사용
        1. 없다면 contentType속성을 확인하고 지정 값을 사용
        1. 위 해당사항이 없으면 ISO-8859-1을 캐릭터 셋으로 사용

    2. 파일이 BOM으로 시작할 경우
        1. BOM을 이용해 결정된 인코딩을 이용하여 파일을 읽고 pageEncoding 검색
        1. BOM을 이용해서 결정된 인코딩과 pageEncoding값과 다르면 오류 발생



## 스크립트 요소
- JSP에서 문서의 내용을 동적 생성하기 위해 사용되는 것
- 데이터 베이스와 연결하여 입/출력을 진행할 수 있다.
- 스크립트 요소의 구성
    - 표현식(Expression): 값을 출력
    - 스크립트릿(Scriptlet): 자바 코드를 실행
    - 선언부(Declaration): 자바 메서드(함수)를 생성

### 스크립트릿
- `<% 자바코드1; 2; 3;... %>`의 형태로 작성
```java
<%@ page contentType="text/html; charset=UTF-8" %>
	<html>
		<head>
			<title>1~ 10까지 합</title>
		</head>
		<body>
			<%
				int sum=0;
				for(int i=1;i<=10;i++){
					sum += i;
				}
			%>
			1부터 10까지의 합은 <%= sum %> 입니다.

			<%
				int sum2=0;
				for(int i=10;i<=20;i++){
					sum2 += i;
				}
			%>
			10부터 20까지의 합은 <%= sum2 %> 입니다.
		</body>
	</html>
```

### 표현식
- 표현식은 어떤 값을 출력 결과에 포함시키고자 할 때 사용된다.
- `<%= 값 %>`의 형태로 작성
```java
<body>
    1부터 10까지의 합은 <%= sum %> 입니다.
    ...
    10부터 20까지의 합은 <%= sum2 %> 입니다.
</body>
```

### 선언부
- JSP페이지의 스크립트릿이나 표현식에서 사용할 수 있는 `메서드를 작성`할 때에는 선언부(declaration)을 사용
- 아래와 같은 문법구조를 가진다.
```java
<%!
    public 리턴타입 메서드명(파라미터){
        ///자바코드
        //...
        return 값;
    }
%>
```

## request 기본 객체
- 웹 브라우저에 웹사이트의 주소를 입력하면, 웹 브라우저는 해당 웹 서버에 연결 후 요청 정보를 전송하는데, 이 `요청 정보를 제공하는 것이 request 기본객체`

- 제공기능
    - 클라이언트(웹 브라우저)와 관련된 정보 읽기 기능
    - 서버와 관련된 정보 읽기 기능
    - 클라이언트가 전송한 요청 `파라미터` 읽기 기능
    - 클라이언트가 전송한 요청 `헤더` 읽기 기능
    - 클라이언트가 전송한 `쿠키` 읽기 기능
    - 속성 처리 기능

### 클라이언트 정보 및 서버 정보 읽기

- request 기본 객체의 클라이언트, 서버 정보 관련 메서드

|메서드|리턴 타입|설명|
|-------------------|----------------------|---------------------------------------------------|
|getRemoteAddr()|String|웹 서버에 연결할 클라이언트의 IP주소를 구한다.|
|getContentLength()|long|클라이언트가 전송한 요청 정보의 길이를 구한다. 알수 없는 경우 -1을 리턴|
|getCharacterEncoding()|String|클라이언트가 요청 정보를 전송할 때 사용한 캐릭터의 인코딩을 구한다.|
|getContentType()|String|클라이언트가 요청 정보를 전송할 때 사용한 컨텐츠의 타입을 구한다|
|getProtocol()|String|클라이언트가 요청한 프로토콜을 구한다|
|getMethod()|String|웹 브라우저가 정보를 전송할 때 사용한 방식을 구한다|
|getRequestURI()|String|웹 브라우저가 요청한 URL에서 경로를 구한다|
|getContextPath()|String|JSP 페이지가 속한 웹 어플리케이션의 컨텍스트 경로를 구한다.|
|getServerName()|String|연결할 때 사용한 서버 이름을 구한다|
|getServerPort()|int|서버가 실행중인 포트 번호를 구한다.|

```java
<%@ page contentType="text/html; charset=UTF-8" %>
	<html>
		<head>
			<title>클라이언트 및 서버 정보</title>
		</head>
		<body>
			클라이언트IP =<%= request.getRemoteAddr()%><br>			
			요청정보길이 = <%= request.getContentLength()%><br>
			요청정보 인코딩= <%= request.getCharacterEncoding()%><br>
			요청정보 컨텐츠 타입= <%= request.getContentType()%><br>
			요청정보 프로토콜=<%= request.getProtocol()%><br>
			요청정보 전송방식=<%= request.getMethod()%><br>
			컨텍스트 경로=<%= request.getContextPath()%><br>
			서버이름 =<%= request.getServerName()%><br>
			서버포트=<%= request.getServerPort()%><br>
			요청 URI=<%= request.getRequestURI()%><br>
		</body>
	</html>
```

> http://localhost:9000/char03/requestInfo.jsp  
> localhost -> request.getServerName
> 9000 -> request.getServerPort()
> chap03/requestInfo.jsp -> request.getRequestURI()

### 요청 파라미터 처리
- (파라미터이름 = 값)의 형식으로 파라미터 목록을 웹 서버에 전송한다.

``` html
<%@ page contentType="text/html; charset=UTF-8" %>
	<html>
		<head>
			<title>클라이언트 및 서버 정보</title>
		</head>
		<body>
			<form action = "/char02/viewParameter.jsp" method="post">
			이름: <input type="text" name="name" size="10"> <br/>
			주소: <input type="text" name="address" size="30"> <br/>
			좋아하는 동물:
     			  <input type= "checkbox" name="pet" value="dog">강아지
			  <input type= "checkbox" name="pet" value="cat">고양이
			  <input type= "checkbox" name="pet" value="pig">돼지
			<br>
			<input type="submit" value="전송">
			</form>
		</body>
	</html>
```
- `name ="속성명"` 이고 `value 혹은 입력 값` 속성에 대한 값이 된다.
- 위 코드 실행시 (파라미터 = value)의 형태로 viewParameter.jsp로 전송된다

### request 기본 객체의 요청 파라미터 관련 메서드

|메서드|리턴 타입|설명|
|--------------|---------------------|---------------------------------------------|
|getParameter(String name)|String|이름이 name인 파라미터 값을 구한다. 존재하지 않을 경우 null 리턴|
|getParameterValues(String name)|String[]|이름이 name인 모든 파라미터의 값을 배열로 구한다. 존재하지 않을 경우 null을 리턴|
|getParameterNames()|java.util.Enumeration|웹 브라우저가 전송한 파라미터의 이름 목록을 구한다|
|getParameterMap()|java.util.Map|웹 브라우저가 전송한 파라미터의 맵을 구한다 맵은 <Key, Value>쌍으로 구성|

```html
<%@ page contentType="text/html; charset=UTF-8"  %>
<%@ page import="java.util.Enumeration" %>
<%@ page import="java.util.Map" %>
<%
    request.setCharacterEncoding("utf-8");
%>
<html>
    <head><title>요청 파라미터 출력</title></head>
    <body>
        request.getPrameter()메서드 사용<br/>
        name 파라미터 = <%= request.getParameter("name") %> <br>
        address 파라미터 = <%= request.getParameter("address") %>
        <p>
            request.getParameterValues()메서드 사용
            <%
                String[] values=request.getParameterValues("pet");
                if(values!=null){
                    for(int i=0;i<values.length;i++){
            %>
            펫 <%= values[i] %> <br/>
            <% 
                }
            }
            %>
        </p>
        request.getParameterNames() 메서드 사용<br>
        <%
            Enumeration paramEnum = request.getParameterNames();
            while(paramEnum.hasMoreElements()){
                String name = (String)paramEnum.nextElement();
        %>
                <%= name %>
        <% 
            }
        %>
        <p>
                request.getParameterMap()메서드 사용
            <br/>
        </p>
        <%
            Map parameterMap=request.getParameterMap();
            String[] nameParam = (String[])parameterMap.get("name");
            if(nameParam!=null){
        %>
        name=<%=nameParam[0]%>
        name2=<%=nameParam[1]%>
        <%
            }
        %>


    
    </body>

</html>

```

### GET 방식과 POST 방식
- 웹 브라우저는 GET방식과 POST방식의 두 가지 방식 중 한 가지를 이용해서 파라미터를 전송한다.
`<form action = "/char02/viewParameter.jsp" method="post">`
- method="post"와 같이 설정함으로서 파라미터의 전송 방식을 POST방식으로 설정했다고 보면 된다.

#### GET
- URL경로 뒤에 `?`와 함께 쿼리 문자열을 붙여 전송한다  
`이름1=값&이름2=값&..이름n=값`을 `쿼리 문자열`이라고 한다.
- 웹 브라우저, 웹 서버 또는 웹 컨테이너에 따라 전송할 수 있는 파라미터 값의 길이에 제한이 있을 수 있음.

#### POST
- 데이터 영역을 이용하여 파라미터를 전송한다.
- 파라미터 길이에 제한이 없다.

### 요청 파라미터 인코딩
- `웹 브라우저`는 웹 서버에 파라미터를 전송할 때 알맞은 캐릭터 셋으로 `인코딩`한다.
- `웹 서버`는 웹 브라우저가 전송한 파라미터를 알맞은 캐릭터 셋으로 `디코딩`한다
- 인코딩과 디코딩이 같은 캐릭터 셋을 이용해야 올바른 파라미터 값을 사용할 수 있다.

### POST방식의 캐릭터 셋
- 입력 폼을 보여주는 응답 화면이 사용하는 캐릭터 셋을 사용하여 인코딩한다.
- `<% request.setCharacterEncoding("utf-8"); %>`을 이용해서 디코딩 하여 파라미터 값을 받아 사용한다.
- request.setCharacterEncoding() 메서드는 http 프로토콜의 데이터 영역을 인코딩 할 때 사용할 캐릭터 셋을 지정한다.
### GET방식의 캐릭터 셋

#### 파라미터 전송방법
- `<a>` tag의 링크 태그에 쿼리 문자열 추가
    - 웹 페이지에 인코딩 사용
 ```html 
 <a href="viewParameter.jsp?name=홍길동&address=아차곡">링크</a>
 ```
- HTML 폼의 method 속성값을 "GET"으로 지정해서 폼을 전송
    - 웹 페이지 인코딩 사용
```html
<form action = "/char02/viewParameter.jsp" method="GET">
```
- 웹 브라우저에 주소에 직접 쿼리 문자열을 포함하는 URL 입력
    - 웹 브라우저마다 다른 인코딩 방법 사용


#### 요청 헤더 정보 처리
- HTTP 프로토콜은 헤더 정보에 부가 정보를 담도록 하고 있다.
- 헤더와 관련된 메서드

| 메서드 | 리턴 타입 | 설명 |
|--------------------|-----------------------------------------|-----------------------|
|getHeader(String name)|String|지정한 이름의 헤더 값을 구한다|
|getHeaders(String name)|java.util.Enumeration|지정한 이름의 헤더 목록을 구한다|
|getHeaderNames(String name)|java.util.Enumeration|모든 헤더의 이름을 구한다|
|getintHeader(String name)|int|지정한 헤더의 값을 정수 값으로 읽어온다|
|getDateHeader(String name)|long|지정한 헤더의 값을 시간 값으로 읽어온다.|

```java
<%@ page contentType="text/html; charset=UTF-8"  %>
<%@ page import="java.util.Enumeration" %>
<html>
<head>
    <title>헤더 목록 출력</title>
</head>
<body>
    <%
    Enumeration headerEnum = request.getHeaderNames();
        while(headerEnum.hasMoreElements()){
            String headerName = (String)headerEnum.nextElement();
            String headerValue = request.getHeader(headerName);
    %>
        <%= headerName %> = <%= headerValue %> <br>
    <%
        }
    %>

</body>


</html>
```

## response 기본 객체
- 서버가 웹 브라우저에 보내는 응답정보를 답는객체로 request객체의 반대역할을 한다.
- response 기본 객체가 응답 정보와 관련해 제공하는 기능
    - 헤더 정보 입력.
    - 리다이렉트.

### 헤더 정보 전송
- reponse 기본 객체가 제공하는 헤더 추가 메서드

|메서드|설명|
|-----------------------------------------|------------------------------------------|
|addDataHeader(String name,long date)|name 헤더에 date를 추가한다.|
|addHeader(String name,String value)|name 헤더에 value 값을 추가|
|addIntHeader(String name,int value)|name헤더에 정수값 value를 추가한다|
|setDateHeader(String name,long date)|name 헤더의 값을 date로 지정한다.|
|setHeader(String name, String value)|name 헤더값을 value로 지정한다|
|setIntHeader(String name,int value)|name헤더의 값을 정수 값 value로 지정한다|
|containsHeader(String name)|이름이 name인 헤더를 포함하고 있을 경우 true를, 그렇지 않은 경우 false를 리턴한다|

- add...메서드는 헤더에 새로운 값을 추가할 때 사용
- set ... 메서드는 새로운 헤더를 정의할 때 사용

### 웹 브라우저 캐시 제어를 위한 응답 헤더 입력

>`캐시(Cache)` :
 데이터나 값을 미리 저장해 놓은 임시 저장소를 의미한다. 웹에서는 동일한 페이지를 중복해서 로딩하게 되는 상황에 웹 애플리케이션 서버에 요청 마다 접속하지 않고 로컬 PC 캐시에 저장된 데이터를 사용하여 훨씬 빠른 응답을 출력할 수 있도록 한다.


- HTTP는 특수한 응답 헤더를 통해서 웹 브라우저가 응답 결과를 캐시 할 것인지에 대한 여부를 설정할 수 있다.

|응답헤더| 설명|
|----------|-----------------------------------------|
|Cache-Control|`HTTP1.1`버전에서 지원하는 헤더로, 헤더의 값을 "`no-cache`"로 지정하면 웹 브라우져는 `응답 결과를 캐시하지 않는다`. (no-cache로 설정하여도 캐시저장소에 보관할 수 있다. 예로 웹 브라우저에 따라 뒤로가기 버튼을 클릭하면 캐시 저장소에 보관된 응답 내용을 사용하기도 한다 그것조차 막고자 한다면 "no-store"로 추가해야 한다.)|
|Pragma|`HTTP1.0`버전에서 지원하는 헤더로, "`no-cache`" 지정시 응답 결과를 캐시에 저장하지 않는다.
|Expires|`HTTP1.0`버전에서 지원하는 헤더로서, 응답 결과의 만료일을 지정한다. 만료일을 현 시간보다 이전으로 설정하면 캐시 보관을 하지 않게 할 수 있다.|

```java
<%
    response.setHeader("Cache-Control","no-cache");
    response.addHeader("Cache-Control","no-store");
    response.setHeader("Pragma","No-cache");
    response.setDataHeader("Expires",1L);
    /*해당 내용은 1970년 1월 1일 0시 0분 0.0001초로 설정한 것*/
%>
```
>최근에는 대부분 웹브라우저에서 HTTP1.1을 지원하지만, 아닌 경우도 존재할 수 있기 때문에 모두 추가하여 대비해 주는 것이 좋다.

### 리다이렉트를 이용하여 페이지 이동
- response 객체에서 가장 많이 사용되는 기능은 리다이렉트 기능으로, 웹 서버가 웹 브라우저에게 다른 페이지로 이동하라고 응답하는 기능이다.
    - 예를 들어 사용자가 로그인에 성공한 후 메인 페이지로 자동으로 이동하는 사이트가 많은데 이렇게 특정한 페이지를 실행한 후 지정한 페이지로 이동하길 원할 때 리다이렉트 기능을 사용

- 리다이렉트의 기능의 흐름
    1. `요청`보냄
    1. 리다이렉트로 다른 페이지로 이동하라고 지정
    1. 이동하라고 응답받은 페이지를 `요청`

- response 객체는 `response.sendRedirect(String location)`을 통해 웹 브라우저가 리다이렉트 하도록 지시할 수 있다.
```java
<%@ page contentType="text/html; charset=utf-8" %>
<%
    String id = request.getParameter("memberId");
    if(id != null && id.equals("madvirus")){
        response.sendRedirect("/chap02/index.jsp");
    }else{
%>
<html>
    <head>
        <title>로그인 실패</title>
    </head>
    <body>
        잘못된 아이디 입니다.
    </body>
</html>
<% 
    }
%>
```

> 위 코드에 url로 `url?memberId=madvirus`로 검색하면 index.jsp로 가라는 리다이렉트 응답을 받을것이고 서버에 index.jsp를 요청하여 index.jsp로 이동할 것이다.

- 웹 서버에 전송할 파라미터 값은 알맞게 인코딩 해야하는데, 리다이렉트도 마찬가지이다. 인코딩을 하는 것을 직접하는것은 무리가 있기 때문에 인코딩 기능을 제공하는 `java.net.URLEncoder`클래스가 존재하여 `URLEncode.encode()`메서드로 인코딩이가능하다


## JSP 주석
- 스크립트릿과 선언부에서드 자바의 주석이 사용 가능
- `<%-- --%>` JSP 자체 주석
