---
title: 세선
---

# 세선(Session)
- `서버에 클라이언트의 상태를 저장`할 수 있으며, 하나의 웹 컨테이너에 정보를 보관할 때 사용한다.
- 웹 컨테이너는 하나의 웹 브라우저에 한 세션을 생성한다.


### 세션 생성
- JSP에서 세션생성을 위해서는 디렉티브에 `session="true"`로 설정하면 된다, 사실 기본값이 트루이기 때문에 false로 설정하지만 않는다면 사용이 가능하다.
```java
<%@ page contentType=... %>
<%@ page session = "true" %>
<%
    ...
    session.setAttribute("userInfo",userInfo);
    ...
%>

```

### session 기본 객체
- 세션을 사용한다는 것은 session기본 객체를 사용한다는 것을 말하고, session기본객체는 request기본객체와 마찬가지로 속성을 제공한다.
    - setAttribute(),getAttribute()등의 메서드를 사용하여 속성값을 저장하거나 읽어올 수 있다.
- 세션은 세션만의 고유 정보를 제공하고, 이들 정보를 구할 때 사용하는 메서드는 아래와 같다

|메서드|리턴타입|설명|
|--------------|-----------------|----------------|
|getId()|String|생성의 고유 ID를 구한다.(세선ID라고 함)|
|getCreationTime()|long|세션이 생성된 시간을 구한다. 시간은 1970년 1월1일 이후|
|getLastAccessedTime()|long|웹 브라우저가 가장 마지막에 세션에 접근한 시간을 구한다.|
- 웹 브라우저 마다 존재하는 세션은 각 세션을 구분하기위해 세션ID를 갖는다.
- 웹 서버는 웹 브라우저에 세션ID를 전송한다. 웹 서버는 연결 시마다 매번 세션ID를 보내 웹 서버가 어떤 세션을 사용할지 판단할 수 있게한다.
- 웹 서버는 세션ID를 이용해 웹 브라우저를 위한 세션을 찾기 때문에, 웹 서버와 웹브라우저는 쿠키를 통해 세션ID를 공유한다.
    - `JSESSIONID`쿠키가 세션ID를 공유할 때 사용하는 쿠키이다.

```java
 page contentType = "text/html; charset=utf-8" %>
<%@ page session = "true" %>
<%@ page import = "java.util.Date" %>
<%@ page import = "java.text.SimpleDateFormat" %>
<%
	Date time = new Date();
	SimpleDateFormat formatter = 
	  new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
%>
<html>
<head><title>세션정보</title></head>
<body>
세션ID: <%= session.getId() %> <br>
// 세션아이디 출력
<%
	time.setTime(session.getCreationTime());
%>
// 세션 생성시간 출력
세션생성시간: <%= formatter.format(time) %> <br>
<%
	time.setTime(session.getLastAccessedTime());
%>
// 세션 최근 접근 시간 출력
최근접근시간: <%= formatter.format(time) %>

</body>
</html>
```

### 기본 객체의 속성 사용
- 한 번 생성된 세션은 지정한 유효 시간 동안 유지, 웹 어플리케이션을 실행하는 동안 지속적으로 사용해야하는 데이터 저장소로는 세션이 적당하다. 


### 세션과 쿠키
- 세션보다 쿠키를 사용하는 가장 큰 이유는 세션이 보안이 앞선다는 점. `쿠키는 네트워크를 통해 전달`되기 때문에 HTTP프로토콜을 사용하는 경우 중간에 누군가 쿠키 값을 읽어올 수 있으나. `세션의 값은 오직 서버`에만 저장되기 때문에 중요한 데이터를 저장하기에 알맞은 장소이다.

- 웹 브라우저가 쿠키를 지원하지 않을 경우 또는 강제적으로 쿠키를 막는 경우 쿠키는 사용할 수 없도록 되지만. 세션은 쿠키 설정 여부와 상관없이 사용할 수 있다는 점이다.

- 세션은 여러 서버가 공유할 수 없다. 예로 daum.net서버와 mail.daum.net서버는 다르기때문에 같이 로그인 정보를 저장할 수 없다.


### 세션 종료
- 세션을 유지할 필요가 없으면 `session.invalidate()` 메서드를 사용해 세션을 종료한다.


### 세션의 유효시간
#### 세션의 유효 시간을 설정하는 방법
1. WEB-INF\web.xml 파일에 `<session-config>`태그를 사용해 세션 유효 시간을 지정할 수 있다.
```xml
	<session-config>
		<session-timeout>60</session-timeout>
        // 값에 단위는 분이다.
    </session-config>
```
2. session 기본 객체가 제공하는 `setMaxInactiveInterval()`메서드 사용
```java
<%
    session.setMaxInactiveInterval(60*60);
    // 60분으로 지정(0이나 음수로 설정하면 세션은 유효시간을 갖지 않아 세션종료전까지 유지)
%>
```

#### `request.getSession()`을 이용한 세션생성

- request.getSession() 현재 요청과 관련된 session객체를 리턴
```java
<%@ page session="false" %>
<%
    HttpSession httpSession = request.getSession();
    List list = (List)httpSession.getAttribute("list");
    list.add(productId);
%>
// 세션을 request.getSession()으로 구하기 때문에 디렉티브에 세션을 false로 지정
```
- `request.getSession()`메서드는 session존재하면 해당 session을 리턴하고 존재하지않으면 만들어 리턴한다.
- Session이 생성된 경우에만 객체를 구하고 싶으면 `request.getSession()`메서드에 파라미터를 false로 전달하면 된다.


#### 세션을 사용한 로그인 상태 유지

1. 로그인에 성공하면 session 기본 객체의 특정 속성에 데이터를 기록
1. 이후에 session 기본 객체의 특정 속성이 존재하면 로그인한 것으로 간주
1. 로그아웃할 경우 session.invalidate()메서드를 호출하여 세션 종료
    - `session.removeAttribute("MEMBERID");`를 통해 같은 효과를 낼 수 있다.

### 연관된 정보 저장을 위한 클래스 작성
- 연관된 정보를 클래스를 사용해 하나의 타입으로 저장하여 사용한다면 유지보수 단계에서 수정에 있어 편리함을 얻을 수 있다.

### 서블릿 컨텍스트와 세션