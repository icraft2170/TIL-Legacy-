---
title: 표현 언어 (Expression Language)
---

# 표현 언어 (Expression Language)
- 다른 형태의 스크립트 언어로서 스크립트 요소중 하나.
- 표현식 보다 간결하고 편리하기 때문에 많이 사용된다.

## 표현 언어란?

- 표현 언어는 값을 표현하는데 사용하는 스크립트 언어로, JSP에 스크립트 요소를 보완하는 역할을 한다.
    - JSP의 네 가지 기본 객체가 제공하는 영역의 속성 사용
    - 수치 연산, 관계 연산, 논리 연산자 제공
    - 자바 클래스 메서드 호출 기능 제공
    - 쿠키,기본 객체의 속성 등 JSP를 위한 표현 언어의 기본 객체 제공
    - 람다식을 이용한 함수 정의와 실행
    - 스크림 API를 통한 컬렉션 처리
    - 정적 메서드 실행

```java
<%-- 표현식 --%>
<%= member.getAddress().getZipcode() %>

<%-- 표현 언어 --%>
${memeber.address.zipcode}
```
- 위 와 같이 실제 프로젝트에서는 더 간결하고 이해가 쉬운 표현 언어를 사용한다.

### EL의 구성
```java
${expr}
// EL은 $와 (`{`,`}`) 그리고 표현식을 사용하여 값을 표현
```
- EL은 액션 태그나 JSTL의 속성값으로 사용할 수 있다.
    - JSP에 스크립트 요소(스크립트릿, 표현식, 선언부)를 제외한 나머지 부분에서 사용이 가능
```java
<jsp:include page="/module/${skin.id}/header.jsp" flush="true"/>

<b> ${sessionScope.memeber.id}</b>님 환영합니다
```

### EL 기초
- 일종의 스크립트 언어로 자료 타입, 수치 연산자, 논리 연산자, 비교 연산자 등을 제공

#### EL의 데이터 타입
- 불리언 타입: true,false
- 정수 타입: 0~9뢰 이루어진 값을 정수로 사용한다.(java.lang.Long타입)
- 실수 타입: java.lang.Double타입
- 문자열 타입: ' 또는 "로 둘러싼 문자열 `'`는 \와 같이 사용해야한다

#### EL의 기본 객체

- EL에서 사용할 수 있는 기본 객체

|기본 객체| 설명 |
|-----------|------------------|
|pageContext|JSP의 페이지와 동일|
|pageScope|pageContext에 저장된 속성의 <속성,값> 매핑을 저장한 Map 객체|
|requestScope|request 기본 객체에 저장된 속성의 <속성,값> 매핑을 저장한 Map객체|
|sessionScope|session 기본 객체에 저장된 속성의 <속성,값> 매핑을 저장한 Map객체|
|applicationScope|application 기본 객체에 저장된 속성의 <속성,값> 매핑을 저장한 Map객체|
|param|요청 파라미터의 <파라미터 이름, 값>매핑을 저장한 Map객체, 값 :String request.getParameter(이름)과 동일|
|paramValues|요청 파라미터의 <파라미터 이름, 값 배열>매핑을 저장한 Map객체, 값 :String[] request.getParameterValues(이름)과 동일|
|header|요청 정보의 <헤더이름, 값> 매핑을 저장한 Map객체이다 request.getHeader(이름)의 결과와 동일|
|headerValues|요청 정보의 <헤더이름, 값 배열> 매핑을 저장한 Map객체이다 request.getHeaders(이름)의 결과와 동일|
|cookie|<쿠키이름,Cookie>매핑을 저장한 Map객체 request.getCookies()로 구한 Cookie 배열로부터 매핑을 생성|
|initParam|초기화 파라미터의 <이름,값> 매핑을 저장한 Map객체 application.getinitParameter(이름)의 결과와 동일|













