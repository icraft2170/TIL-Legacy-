---
title: JSP_02
---

# JSP
- 목적
    - 웹 브라우저에 보여 줄 HTML 문서를 생성하는 것( XML 등 다른 종류의 문서도 가능.)

```html
<%@ page contentType="text/html; charset=UTF-8" %>
	<html>
		<head>
			<title>HTML 문서 제목</title>
		</head>
		<body>
			<%
				String bookTitle="JSP 프로그래밍";
				String author ="최범균";
			%>
			<b><%=bookTitle%></b>(<%= author %>) 입니다.
		</body>
	</html>
```
- `page 디렉티브`
    - JSP 페이지가 생성하는 문서의 타입(종류)
    - JSP 페이지에서 사용할 커스텀 태그
    - JSP 페이지에서 사용할 자바 클래스 지정
    
`<%@ page contentType="text/html; charset=UTF-8" %>`
> JSP 페이지가 `생성할 문서가 HTML`이며, 문서의 캐릭터 셋이 `UTF-8`임을 나타낸다.

## JSP Page의 구성 요소
- 디렉티브(Directive)
- 스크립트: 스크립트릿(Scriptlet),표현식(Expression),선언부(Declaration)
- 표현 언어(Expression Language)
- 기본 객체(Implicit Object)
- 정적 데이터
- 표준 액션 태크(Action Tag)
- 커스텀 태그(Custom Tag)와 표준 태그 라이브러리(JSTL)

### 디렉티브(Directive)
- JSP 페이지에 대한 설정 정보를 지정할 때 사용
- 디렉티브 선언 방법 
```
    <%@ 디렉티브명 속성1="값1" 속성2="값2"... %>
```
- `<%@ ~ %>` 로 작성
- JSP가 제공하는 디렉티브

|디렉티브|설명|
|:-------:|:----------------------------------------------------------------|
|page|JSP 페이지에 대한 정보를 지정. JSP가 생성하는 문서의 타입으로 출력 버퍼의 크기, 에러 페이지 등 JSP 페이지에서 필요로 하는 정보 설정|
|taglib|JSP 페이지에서 사용할 태그 라이브러리 지정|
|include|JSP 페이지의 특정 영역에 다른 문서를 포함시킨다.|


### 스크립트 요소
- JSP에서 문서의 내용을 동적 생성하기 위해 사용되는 것
- 데이터 베이스와 연결하여 입/출력을 진행할 수 있다.
- 스크립트 요소의 구성
    - 표현식(Expression): 값을 출력
    - 스크립트릿(Scriptlet): 자바 코드를 실행
    - 선언부(Declaration): 자바 메서드(함수)를 생성


### 기본 객체
- 웹 어플리케이션 프로그래밍을 위해 `기본 객체(Implicit Object)`를 제공한다.
- `request, response, session, application, page`등 다수의 객체 존재
    - 요청 파라미터 읽어오기,응답 결과 전송하기, 세션처리하기, 웹 어플리케이션 정보 읽어오기등

### 표현 언어
- 스크립트를 사용하여 코드의 가독석이 떨어지는 것을 막고 코드를 간결하고 이해하기 좋게 하기 위해 사용
- `${~}`의 형태로 작성

### 표준 액션 태그와 태그 라이브러리

#### 액션 태그
- 액션 태그는 JSP 페이지에서 특별한 기능 제공한다.
- `<jsp:액션태그이름>`의 형태로 작성
```html
// 예시
<%@ page contentType="text/html; charset=UTF-8" %>
    <html>
    ...
    <jsp:include page="header.jsp" flush="true" />
    // 특정한 페이지의 실행결과를 현재위치에 포함시킬 때 사용된다.
    ...
    </html>
```

#### 커스텀 태그
- JSP를 확장시켜주는 기능, 액션 태그와 마찬가지로 태그 형태로 기능을 제공
- JSP코드 내 중복되는 것을 모듈화 하거나 소스코드의 복잡성을 없애기 위해 사용
- 커스텀 태그중 자주 사용하는 것들을 별도로 표준화한 라이브러리가 `JSTL(JavaServer Pages Standard Tag Library)`

