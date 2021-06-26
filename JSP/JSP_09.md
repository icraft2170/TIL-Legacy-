---
title: 쿠키
---

# 쿠키(Cookie)

## 쿠키란?
- 쿠키는 `웹 브라우저가 보관`하는 데이터. 웹 브라우저는 웹 서버에 요청을 보낼 때 쿠키를 함께 전송하며, 웹 서버는 웹 브라우저가 전송한 쿠키를 사용해 필요 데이터를 읽을 수 있음

- 동작방식
    1. `쿠키 생성`
        - 웹 브라우저가 요청을 하면 웹 서버가 쿠키를 생성하고 응답 데이터의 헤더로 전송
    1. `쿠키 저장`
        - 웹 브라우저는 응답 데이터에 포함된 쿠키를 쿠키 저장소에 보관한다.
    1. `쿠키 전송`
        - 웹 브라우저는 저장한 쿠키를 요청이 있을 때 마다 웹 서버에 전송, 웹 서버는 웹 브라우저가 전송한 쿠키를 통해 작업 수행


### 쿠키의 구성
- `이름` : 각각의 쿠키를 구별하는 이름
    - 콤마,세미콜론,공백,등호를 제외한 아스키 문자로 구성 보통은 알파벳과 숫자만을 사용
- `값` : 쿠키의 이름과 관련된 값
- `유효시간` : 쿠키의 유지시간
- `도메인`: 쿠키를 전송할 도메인
- `경로` : 쿠키를 전송할 요청 경로

### 쿠키 생성
```jsp
<% 
    Cookie cookie = new Cookie("cookieName","cookieValue");
    // 쿠키를 생성한다.
    response.addCookie(cookie)
    // 응답 기본 객체에 쿠키를 저장
%>
```


### Cookie 클래스의 메서드

|메서드|리턴타입|설명|
|----------------|-------------------------------------|------------------------------|
|getName()|String|쿠키의 이름을 반환|
|getValue()|String|쿠키의 값을 반환|
|setValue(String value)|void|쿠키의 값을 지정|
|setDomain(String pattern)|void|쿠키가 전송될 도메인을 지정|
|getDomain()|String|쿠키가 전솔될 도메인 반환|
|setPath(String uri)|void|쿠키를 전송할 경로 지정|
|getPath()|String|쿠키를 전송할 경로 반환|
|setMaxAge(int expiry)|void|쿠키의 유효시간을 초 단위로 지정, 음수를 입력할 경우 웹 브라우저를 닫을 때 쿠키가 함께 삭제된다|
|getMaxAge()|int|쿠키의 유효시간을 구한다.|

### Cookie값 읽기

```java
Cookie[] cookies = request.getCookies();
```
- getCookies() 메서드는 Cookie배열을 리턴
```java
<%@ page contentType = "text/html; charset=utf-8" %>
<%@ page import = "java.net.URLDecoder" %>
<html>
<head><title>쿠키 목록</title></head>
<body>
쿠키 목록<br>
<%
	Cookie[] cookies = request.getCookies();
    // 응답받은 쿠키를 배열에 저장
	if (cookies != null && cookies.length > 0) {
		for (int i = 0 ; i < cookies.length ; i++) {
%>
	<%= cookies[i].getName() %> = 
	<%= URLDecoder.decode(cookies[i].getValue(), "utf-8") %><br>
    // 쿠키를 utf-8로 디코딩한 쿠키의 값들을 출력
<%
		}
	} else {
%>
쿠키가 존재하지 않습니다.
<%
	}
%>
</body>
</html>

```

### Cookie값 변경 및 삭제
- 쿠키 값 변경을 위해서는 같은 이름의 쿠키를 새로 생성해 응답데이터로 보내면 됨.
```java
Cookie cookie = new Cookie("name",URLEconder.encode("새로운값","euc-kr"));
response.addCookie(cookie);
```
- `쿠키를 삭제`하기 위해서는 Cookie클래스의 `setMaxAge()` 메서드를 호출할때 인자 값으로 0을 주면 된다.
```java
Cookie cookie = new Cookie(name,value);
// 쿠키이름이 name인 쿠키를 새로 만들고
cookie.setMaxAge(0);
// 지속시간을 0초로 주어 추가하여 삭제
response.addCookie(cookie);
```

### Cookie Domain
- 기본적으로 쿠키는 그 쿠키를 생성한 서버에만 전송되는데, 같은 도메인을 사용하는 모든 서버에 쿠키를 보내야 할 때, `setDomain()`메서드를 사용한다.
- `setDomain()` 값으로는 현재 서버의 도메인 및 상위 도메인에만 전송이 가능

#### `setDomain()`으로 지정할 도메인 형식
- `.somehost.com`
    -  점으로 시작하는 경우 관련 도메인에 모두 쿠키를 전송.
- `www.somehost.com`
    - 특정 도메인에 대해서만 쿠키를 전송.


### Cookie Path
- 도메인이 쿠키를 공유할 도메인 범위를 지정한다면, 경로는 쿠키를 공유할 기준 경로를 지정한다.
- `setPath()`메서드를 사용해 쿠키의 경로를 지정하면, 웹 브라우저는 지정한 경로 또는 하위 경로에 대해서만 쿠키를 전송한다.

```java
Cookie cookie = new Cookie("name","value");
cookie.setPath("/chap09");
```
- 웹 브라우저는 name쿠키를 /chap09 또는 그 하위 경로에만 전송할 수 있다.

### 쿠키의 유효시간
- 쿠키는 유효시간을 갖는다, 유효시간을 저장해주지 않는다면 웹브라우저 종료와 함께 삭제되고 유효시간을 설정해 둔다면, 그 시간이 지나면 쿠키가 삭제된다. 유효시간을 지정하면 웹 브라우저가 종료되더라도 설정한 시간이 지날 때 까지는 삭제가 되지 않는다.


> 아이디 기억하기 기능을 사용할 때 쿠키를 사용하는데 로그인 성공시 아이디 값을 저장하고 그 시간을 1달정도로 잡는다.


### 쿠키와 헤더
- response.addCookie()로 쿠키를 추가하면 실제로 Set-Cookie헤더를 통해서 전달된다. Set-Cookie헤더는 한 개의 쿠키 값을 전달한다.
- `Set-Cookie헤더` 구성
```java
쿠키이름=쿠키값;Domain=도메인값;Path=경로값;Expires=GMT형식의만료일시

ex)
Set-Cookie:id=madvirus;Domain=.somehost.com
```

### Cookies클래스를 이용한 쿠키 생성

```java
Cookie cookie1 = Cookies.createCookie("name","최범균");
Cookie cookie2 = Cookies.createCookie("name2","최범균","/path",-1);
// 유지시간이 음수이면 웹브라우저 종료시까지 쿠기가 유지된다.
Cookie cookie3 = Cookies.createCookie("id","jsp",".madvirus.net","/",60);
```

### Cookies클래스를 이용한 쿠키 읽기
- 웹 브라우저가 전송한 쿠키를 읽으려면 Cokkies객체 생성후 getCookie(),getValue(),exists()등의 메서드를 활용해야만 한다.

```java
Cookies cookies = new Cookies(request);

if(cookies.exists("name")){
    Cookie cookie= cookies.getCookies("name");
    ...
}

if(cookies.exists("id")){
    String value= cookies.getValue("name");
    // 값만 사용할 때.
    ...
}

```


### 쿠키를 활용한 로그인 상태 유지
1. 로그인 성공시 특정 이름을 갖는 쿠키 생성
1. 해당 쿠키 존재시 로그인 상태라고 판단
1. 로그아웃시 해당 쿠키를 삭제

