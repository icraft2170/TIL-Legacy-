---
title : 기본 객체와 영역
---

# 기본 객체

|기본 객체|실제 타입| 설명|
|----------|---------------|-------------------|
|`request`|javax.servlet.http.HttpServletRequest|`클라이언트 요청 정보를 저장`|
|`response`|javax.servlet.http.HttpServletResponse|`응답 정보를 저장`|
|pageContext|javax.servlet.jsp.PageContext|JSP 페이지에 대한 정보를 저장|
|`session`|javax.servlet.http.HttpSession|`HTTP 세션 정보를 저장한다`|
|application|javax.servlet.ServletContext|웹 어플리케이션 정보 제공|
|`out`|javax.servlet.jsp.JspWriter|`JSP 페이지가 생성하는 결과를 출력할 때 쓰는 출력스트림`|
|config|javax.servlet.ServletConfig|JSP페이지에 대한 설정 정보를 저장|
|page|java.lang.Object|JSP 페이지를 구현한 자바 클래스의 인스턴스|
|`exception`|java.lang.Throwable| 입셉션 객체, 에러페이지에 사용|

- exception을 제외한 8개의 기본객체는 JSP페이지에서 사용 가능.(exception은 에러페이지 에서만.)


## OUT 기본 객체

- JSP페이지가 생성하는 모든 내용은 out객체를 통해 전송된다.
- `비-스크립트요소(HTML, 텍스트)`은 out에 그대로 전달되고, `표현식(<%= %>` 결과값도 out객체에 전달된다
- 웹 브라우저에 데이터를 전송하는 출력 스트림으로서 데이터를 출력한다
```java
out.println("<html>");
out.println("<head>");
...
out.println(someValue);
```

### out객체의 출력 메서드
- print() : 데이터 출력
- println() : 데이터 출력하고, 줄바꿈 문자(\r\n 또는 \n)출력
- newLine() : 줄바꿈 문자(\r\n 또는 \n)출력
> print,println메서드는 기본 데이터타입과, String을 출력할 수 있음

### out객체와 버퍼와 관계
- 디렉티브에 조정한 buffer속성은 `out객체가 내부적으로 사용하는 버퍼`
- 버퍼 관련 메서드

|메서드|리턴 타입|설명|
|----------|--------------------|----------------------------------------|
|getBufferSize()|int|버퍼의 크기를 구한다|
|getRemaining()|int|현재 버퍼의 남은 크기를 구한다|
|clear()|void|버퍼의 내용을 비운다, 이미 플러시 했다면 IOException발생|
|clearBuffer()|void|버퍼의 내용을 비운다, 이미 플러시 했다해도 IOException발생하지 않음|
|flush()|void|버퍼를 플러시한다. 즉 버퍼의 내용을 클라이언트에 전송|
|isAutoFlush()|boolean|버퍼가 다 찼을 때 자동으로 플러시 할 경우 true 리턴|



## pageContext 기본 객체

- JSP페이지와 일대일로 연결된 객체로 아래의 기능 제공
    - 기본 객체 구하기
    - 속성 처리하기
    - 페이지의 흐름 제어
    - 에러 데이터 구하기
- 커스텀 태그를 구현할 때 사용한다.


### 기본 객체 접근 메서드
- pageContext 기본 객체는 다른 기본 객체에 접근할 수 있는 메서드 제공
- getRequest(),getResponse(),getSession() 등의 방법으로 기본 객체를 구한다(리턴한다)

## application 기본 객체
- 웹 어플리케이션 전반에 사용되는 정보를 담음


### 초기화 파라미터
- WEB-INF\web.xml 파일에 <context-param> 태그를 사용하여 추가
>web.xml파일 웹 어플리케이션을 위한 설정 정보를 담고있는 파일 JSP프로그래밍을 할 때 반드시 필요한 것은 아니지만 버전에 따라 필수인 경우도 있음 \WEB-INF폴더에 존재해야함

```xml
<context-param>
    <description>파라미터 설명(필수 x) </description>
    <param-name>파라미터 이름 </param-name>
    <param-value>파라미터 값 </param-value>
</context-param>
```

- web.xml에 정의한 초기화 파라미터는 application 기본객체의 메서드로 사용 할 수 있음
    - getInitParameter(String name) : 문자열을 반환하는 이름이 name 초기화 파라미터를 읽어옴, 존재하지않으면 Null 반환
    - getInitParameterNames(String name) : 초기화 파라미터 이름 목록을 리턴
- 초기화 파라미터는 웹 어플리케이션을 초기화 하는데 사용한다.
    - DB 연결과 관련된 설정 파일의 경로, 로깅 설정 파일 또는 웹 어플리케이션 주요 속성 정보를 담고 있는 파일 경로를 지정할 때.

### 서버 정보 읽기
    - getServerInfo() :서버 정보 리턴
    - getMajorVersion() : 서버가 지원하는 서블릿 규약의 메이저 버전을 리턴(버전의 정수부분)
    - getMinorVersion : 서버가 지원하는 서블릿 규약의 메이저 버전을 리턴(버전의 소수부분)

### 로그 메시지 기록
- log(String msg) : msg 로그 남김
- log(String msg, Throwable throwable) : msg 로그 남김 익셉션 정보도 함께 로그 기록

- 톰캣에 경우 톰캣 폴더\lops localhost-날짜 형식으로 로그데이터가 저장되어 있다.

### 웹 어플리케이션 자원 구하기
- 절대경로를 통해 파일을 읽어오는것이 가능 (다만, 유지보수에 문제가 생길 수 있다.)
```java
<%@ page contentType = "text/html; charset=utf-8" %>
<%@ page import = "java.io.*" %>
<html>
<head><title>절대 경로 사용하여 자원 읽기</title></head>
<body>

<%
	char[] buff = new char[128];
	int len = -1;
	
	String filePath = "C:\\JSP\\apache-tomcat-10.0.6\\webapps\\jsp23-master\\jsp23-master\\webapps\\chap05\\message\\notice.txt";
	try(InputStreamReader fr = new InputStreamReader(new FileInputStream(filePath), "UTF-8")) {
		while ( (len = fr.read(buff)) != -1) {
			out.print(new String(buff, 0, len));
		}
	} catch(IOException ex) {
		out.println("익셉션 발생: "+ex.getMessage());
	}
%>

</body>
</html>
```
#### 웹 어플리케이션 파일 접근 메서드
- getRealPath(String path)
    - 문자열 타입에 해당 경로에 시스템상 경로를 리턴
- getResource(String path)
    - 해당하는 경로에 자원에 접근할 수 있는 URL 반환
- getResourceAsStream(String path)
    - 웹 어플리케이션 내 지정한 경로에 해당하는 자원으로 부터 데이터를 읽어올 수 있는 InputStream 리턴

### JSP 기본 객체와 영역

- PAGE영역 : 하나의 JSP파일을 처리할 때 사용되는 영역
- REQUEST영역 : 하나의 HTTP 요청을 처리할 때 사용되는 영역
- SESSION영역 : 하나의 웹 브라우저와 관련된 영역
- APPLICATION영역 : 하나의 웹 어플리케이션과 관련된 영역

### JSP 기본 객체의 속성(Attribute)사용

- pageContext,request,session,application은 속성을 갖고. 존재하는동안 사용 가능

- 속성 처리 메서드
    - setAttribute(String name, Object value)
        - 이름이 name인 속성의 값을 value로 지정
    - getAttribute(String name)
        - 이름이 name인 속성의 값을 구한다. 지정한 이름의 속성이 존재하지 않으면 null 리턴
    - removeAttribute(String name)
        - 이름이 name인 속성을 삭제한다
    - getAttributeNames()
        - 속성의 이름 목록을 구한다.(PAGECONTEXT는 지원하지 않음)


- 속성의 쓰임새
    - pageContext :  pageContext에서는 커스텀 태그에 변수를 추가할 때 주로 사용
    - request : 요청과정에서  정보 전달을 위해 사용
    - session : 한 사용자와 관련된 정보를 JSP사이에 공유하기 위해 사용 주로 로그인 정보
    - application : 어플리케이션 설정정보를 주로 저장