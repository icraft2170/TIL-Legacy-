---
title: 자바빈과 <jsp:useBean>
---


# 자바빈(JavaBeans)

- 자바빈은 속성(데이터), 변경 이벤트, 객체 직렬화를 위한 표준이다. 이 중에서 JSP에서는 속성을 표현하기 위한 용도로 사용된다.

#### `자바빈 규약을 따르는 클래스 구조`
```java
public class BeanClassName implements java.io.Serializable
{
    // 값을 저장하는 필드
    private String value;

    // BeanClassName의 기본생성자
    public BeanClassName(){

    }

    public String getValue(){
        return value;
    }

    public void setValue(String value){
        this.value=value;
    }

}
```
- 데이터 저장 필드(value)
- 데이터를 읽어올 때 사용하는 메서드(get)
- 데이터를 저장할 때 사용하는 메서드(set)

```java
// 예시 

import java.util.Date;

public class MemberInfo {
	
	private String id;
	private String password;
	private String name;
	private Date registerDate;
	private String email;
	
	public String getId() {
		return id;
	}
	public void setId(String val) {
		this.id = val;
	}
	public String getPassword() {
		return password;
	}
	public void setPassword(String val) {
		this.password = val;
	}
	public String getName() {
		return name;
	}
	public void setName(String val) {
		this.name = val;
	}
	public Date getRegisterDate() {
		return registerDate;
	}
	public void setRegisterDate(Date val) {
		this.registerDate = val;
	}
	public String getEmail() {
		return email;
	}
	public void setEmail(String val) {
		this.email = val;
	}
}
```

## `<jsp:useBean>`

- JSP에서는 이런 데이터들을 자바빈과 같은 클래스에 담아서 값을 보여주는 것이 일반적이다.
```java
// 예시
<%
    MemberInfo mi = new MemberInfo();
    mi.setId("madvirus");
    mi.setName("최범균");
%>

이름-<%= mi.getName() %>, 아이디 - <%= mi.getId() %>
```

### `<jsp:useBean>` 액션 태그를 사용
- `<jsp:useBean>` 액션 태그는 JSP페이지에서 사용할 자바빈 객체를 지정할 때 사용

```java
<jsp:useBean id="[빈이름]" class="[자바빈 클래스 명]" scope="[범위]" />
```
- scope에 지정된 기본객체내에 저장하여 그 객체가 유효한 동안 사용할 수 있도록 한다.
    - id : JSP페이지에서 자바빈 객체에 접근할 때 사용할 이름을 지정
    - class: 패키지 이름을 포함한 자바빈 클래스의 완전한 이름을 입력한다
    - scope : 자바빈 객체를 저장할 영역을 지정, page, request, session, application 중 하나의 값을 갖는다. 기본값은 page

```java
//makeObject.jsp
<%@ page contentType = "text/html; charset=utf-8" %>
<jsp:useBean id="member" scope="request" class="chap08.member.MemberInfo" />
<%
	member.setId("madvirus");
	member.setName("최범균");
%>
<jsp:forward page="/useObject.jsp" />
```

```java
//useObject.jsp
<%@ page contentType = "text/html; charset=utf-8" %>
<jsp:useBean id="member" scope="request"
             class="chap08.member.MemberInfo" />
<html>
<head><title>인사말</title></head>
<body>

<%= member.getName() %> (<%= member.getId() %>) 회원님
안녕하세요.

</body>
</html>
```

- useObject.jsp를 직접 실행하면 Bean에서 가져온 데이터는 NULL 값이지만 makeObject로 실행하여 데이터를 저장하고 포워딩하여 useObject.jsp를 실행하도록하면 데이터를 받아 사용할 수 있다.

## `<jsp:setProperty>` 액션 태그와 `<jsp:getProperty>` 액션 태그

- `<jsp:setProperty>`: 프로퍼티 값을 변경할 수 있다.
- `<jsp:getProperty>`: 프로퍼티 값을 가져올 수 있다.

### `<jsp:setProperty>`

```java
<jsp:setProperty name="[자바빈]" property="이름" value="[값]" />
```
- name : 프로퍼티의 값을 변경할 자바빈 객체의 이름을 지정한다 <jsp:useBean> id 속성에서 지정한 값을 사용
- property : 값을 지정할 프로퍼티 이름을 지정한다.
- value : 프로퍼티의 값을 지정한다. `표현식(%= 값 %>)이나 EL($값)`을 사용할 수 있다

```java
<jsp:useBean id="member" class="chap08.member.MemberInfo" />
<jsp:setProperty name="member" property="name" value="최범균" />
// 자바빈 객체의  name 프로퍼티값을 최범균으로 변경하고 싶을때 지정
```
- `property="*"`와 같이 하여 모든 속성을 지정할 수 있다.

###  `<jsp:setProperty>`
- 자바빈 객체의 프로퍼티 값을 출력할 때 사용된다.
```java
<jsp:getProperty name="자바빈이름" property="프로퍼티이름" />
```

#### 자바빈의 사용 이유
- 여러 줄에 걸쳐 사용할 코드를 액션 태그로 하나로 줄일 수 있다.

#### 액션태그 사용빈도의 감소
- MVC패턴을 사용하거나 표현언어의 사용 때문.