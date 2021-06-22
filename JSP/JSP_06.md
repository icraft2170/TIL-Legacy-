---
title : 에러처리
---

# 에러처리

- JSP 페이지 수행 과정에서 에러발생을 막기위해 `try-catch` 에러처리를 해주어야 한다.
- 에러페이지 노출은 사이트 `신뢰 측면과 보안 측면`에서 좋지 않다.

## 에러페이지 지정

```java
<%@ page contentType = "text/html; charset=utf-8" %>
<%@ page errorPage = "/error/viewErrorMessage.jsp" %>
<html>
<head><title>파라미터 출력</title></head>
<body>

name 파라미터 값: <%= request.getParameter("name").toUpperCase() %>

</body>
</html>
```
- JSP에서는 에러 발생시 이동할 에러페이지를 아래와 같이 지정할 수 있다.
`<%@ page errorPage = "/error/viewErrorMessage.jsp" %>`

### 에러페이지 작성
- 디렉티브에서 isErrorPage속성을 `True`지정
```java
<%@ page contentType = "text/html; charset=utf-8" %>
<%@ page isErrorPage = "true" %>
// 디렉티브 속성
<html>
<head><title>에러 발생</title></head>
<body>
요청 처리 과정에서 에러가 발생하였습니다.<br>
빠른 시간 내에 문제를 해결하도록 하겠습니다.
<p>
에러타입 <%= exception.getClass().getName() %>
에러 메시지 <%= exception.getMessage() %>
</body>

</html>
```


### 응답 상태 코드별로 에러 퍼이지 지정
- `web.xml`파일에 에러 코드별로 사용할 에러 페이지를 지정할 수 있다.
```xml
<?xml version="1.0" encoding="utf=8"?>

<web-app...>
...
    <error-page>
        <error-code>404</error-code>
        <location>/error/error404.jsp</location>
    </error-page>
</web-app>
```

> `주요 응답 상태 코드`  
> HTTP 프로토콜은 응답 상태 코드를 이용해, 서버의 처리 결과를 웹 브라우저에 알려준다.
> - 200 : 요청을 정상적으로 처리
> - 307 : 임시로 페이지를 리다이렉트함
> - 400 : 클라이언트의 요청이 잘못된 구문으로 구성
> - 401 : 접근을 허용하지 않음
> - 404 : 요청한 URL을 처리하기 위한 자원이 존재하지 않음
> - 405 : 요청한 메서드(GET,POST,HEAD 등의 전송 방식)를 허용하지 않음
> - 500 : 서버 내부 에러가 발생(예로 JSP에서 익셉션 발생)
> - 503 : 서버가 일시적으로 서비스 제공 불가(급격하게 부하가 몰리거나, 서버가 임시 보수중일 때)
> JSP가 정상적으로 실행되는 경우 응답 코드로 200이 전성되며, response.sendRedirect()를 이용할 경우 응답코드로 307을 전송


### 익셉션 타입별 에러페이지 지정

- `web.xml`파일에 익셉션 타입별로 사용할 에러 페이지를 지정할 수 있다.
```xml
<?xml version="1.0" encoding="utf=8"?>

<web-app...>
...
    <error-page>
        <exception-type>java.lang.NullPointerException</exception-type>
        <location>/error/errorNullPointer.jsp</location>
    </error-page>
</web-app>
```

### 에러페이지 우선순위와 지정형태
- 디렉티브에 작성
- web.xml에 작성(2가지 방법)

- 우선순위
    1. page 디렉티브의 errorPage 속성에 지정한 에러 페이지를 보여준다
    1. JSP 페이지에서 발생한 익셉션 타입이 web.xml 파일의 `<exception-type>`에 지정한 익셉션 타입과 동일한 경우 지정한 에러 페이지를 보여줌
    1. 에러 코드가 web.xml 파일의 `<error-code>`속성으로 지정한 에러코드와 동일한 경우
    1. 아무것도 해당하지 않는 경우, 웹 컨테이너가 제공하는 기본 웹페이지

### 버퍼와 에러 페이지의 관계
- 버퍼가 다 차 버퍼를 플러시 할 때 `응답 헤더도 전송`한다, `응답 상태 코드는 응답 헤더 앞에 전송`되므로 최초로 버퍼를 플러시하면 응답 상태 코드가 가장 먼저 전송된다. 따라서 버퍼를 최초로 플러시할 때 까지 에러가 발생하지 않으면 웹 브라우저에서는 200 응답 상태 코드가 전달된다. 최초 플러시 이후에 발생한 에러코드는 전달 되지 않아 웹 브라우저는 정상적으로 응답했다고 판단한다.