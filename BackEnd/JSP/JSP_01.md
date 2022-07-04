---
title: JSP2.3
--- 

# 웹프로그래밍

### 웹페이지, 웹사이트
- 웹 페이지(Web Page): 웹 브라우저에 출력된 내용
- 웹 사이트(Web Site): 웹 페이지의 묶음

### URL(Uniform Resource Locator)
- 일종의 리소스가 위치한 주소 역할을 한다.

```
http://www.11st.co.kr/html/category/1.html?xzone=ctgr1^html

[URL의 구성]
http : 프로토콜
www.11st.co.kr : 서버 이름
html/category/1.html : 경로
?xzone=ctgr1^html : 쿼리 문자열
```
|구성 요소| 설명|
|:-----------:|:-----------------------------------:|
|프로토콜|웹 브라우저가 서버와 내용을 주고받을 때 사용할 규칙 이름. (http/https)|
|서버 이름|웹 페이지를 요청할 서버의 이름을 지정, 서버이름은 도메인 혹은 IP주소의 형태로 입력할 수 있다.|
|경로|웹 페이지의 상세 주소에 해당. 즉, 웹페이지마다 다른 경로를 가짐|
|쿼리문자열|추가로 서버에 보내는 데이터에 해당. 같은 경로라 하더라도 입력한 값에 따라 다른 결과를 보여줘야 할 때 쿼리 문자열을 사용한다.|

 
 ### 웹 브라우저, 웹 서버

####  웹 브라우저에 웹페이지가 출력되는 과정
 1. 웹 브라우저가 DNS(Domain Name Server)서버에 도메인에 맞는 IP주소를 요청(Request)
 2. 응답(Response) 받은 `IP주소로 페이지를 요청(Request)`
 3. `응답(Response) 받은 페이지`를 화면에 출력

> 이 때, `요청(Request)` 하는 쪽을 `클라이언트(Client)`라고 하며 `응답(Response)` 하는 쪽을 서버(Server)라고 부른다.

- 하나의 서버 컴퓨터에서 하나의 서버만을 실행하는 것은 아니다. 다수의 서버를 동시에 실행할 수 있는데 이 때, IP주소 만으로는 접속할 서버를 선택할 수 없다. 
그래서 클라이언트가 연결할 때 다른 서버 프로그램과 구분하기 위해 `포트(PORT)`를 사용한다.
    - 웹 서버가 사용하는 `기본(default) 포트 번호는 80`이다.

### HTML/HTTP

#### HTML(HyperText Markup Language): 웹을 구성하는 표준이다.
- HTML 문서로 부터 알맞은 화면을 생성하는 과정을 `렌더링(rendering)`이라고 함.

#### `HTTP(HyperText Transfer Protocol)`: 웹 브라우저와 웹 서버가 HTML,이미지,동영상,XML등 다양한 데이터를 주고 받을 때 사용하는 일종의 규칙
- 두 가지 관점에서 정의한 규칙
    - 요청 규칙 : 웹 브라우저가 웹 서버에 HTML과 같은 것을 요청할 때 사용할 데이터 구성 규칙
    - 응답 규칙: 웹 서버가 웹 브라우저에 HTML과 같은 것을 전송할 때 사용할 데이터 구성 규칙
- [`요청/응답 줄`]/[`헤더`]/[`몸체`] 세 개의 영역으로 구성된다.
- HTTP의 요청/응답 데이터의 구성요소

|구성요소|요청 데이터|응답 데이터|
|:-----------:|:----------------------------:|:---------------------|
|요청/응답 줄| `GET/POST` 같은 HTTP 요청 방식과 요청하는 자원의 경로 지정| 요청에 대해 200이나 404 같은 응답 코드를 전송한다. 200은 정상 처리 했음을 의미.
|헤더|서버가 응답을 생성하는데 `참조할 수 있는 정보를 전송한다. 예를들어 브라우저의 종류나 언어등의 정보`|응답에 대한 정보를 전송 응답의 몸체가 어떤 데이터인지, 길이는 어떻게 되는지 등에 대한 정보를 담음.|
|몸체|`정보를 전송`해야 할 때 사용한다. 예를 들어, 파일 업로드와 같은 기능을 사용하면 몸체 영역에 파일을 담아 웹 서버에 전송|웹 브라우저가 요청한 자원의 내용을 담는다. HTML문서나 이미지 파일 데이터 등이 몸체 영역을 이용해전달|


### 정적 자원과 동적 자원

#### 정적 자원 (Static Resource)
- 웹서버에 URL을 통해 웹페이지를 요청하면 URL 경로에 기록된 위치와 동일한 파일을 웹브라우저에 전송한다. 이렇게 서버에서 파일이 변하지 않으면 늘 같은 응답 데이터를 받는 동일한 화면을 출력하는 것을 정적(Static) 페이지,자원 이라고 함.
- 보통 이미지 파일이나 HTML파일과 같이 자주 바뀌지 않는 것들을 제공
#### 동적 자원 (Dynamic Resource)
- 시간이나 특정 조건에 따라 응답 데이터가 달라지는 자원을 동적(Dynamic) 페이지,자원이라고 부른다.


## 웹 프로그래밍과 JSP

### 웹 프로그래밍
- 웹 서버가 웹 브라우저에 응답으로 전송할 데이터를 생성해주는 프로그램을 작성하는 것
- 웹 서버 종류에 따라 사용 기술이 달라진다
    - 아파치/PHP
    - 윈도우 IIS/ASP.net
    - Tomcat,Jetty,JBoss EAP/`JavaServer Pages(JSP)`

### JavaServer Pages(JSP)

- 동적 페이지를 작성하는데 사용되는 자바의 표준 기술로 HTML 응답을 생성하는데 필요한 기능을 제공

> JEE(Java Enterprise Edition) : 자바를 이용해 어플리케이션을 개발하는데 필요한 표준을 정의한 것으로 JSP,서블릿,JSTL,JPA등 여러 표준으로 구성

