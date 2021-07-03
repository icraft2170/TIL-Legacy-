---
title:서블릿
---


# Servlet




## Servlet

### Console에서 Servlet 작성

```java
import javax.servelt.*;
import javax.servelt.http.*;
import java.io.*;

//HttpServlet을 상속받음으로 서블릿을 생성함
public class 서블릿명 extends HttpServlet
{
    // 메인함수가 아님 서블릿함수를 사용함으로서 WAS가 불러감
    public void service(HttpServletRequest request, HttpServletResponse response) throws IOException,ServletException
    {
        System.out.println("hello Servlet");
    }

}
```
- `javac -cp {톰캣 설치 경로}/lib/servlet-api.jar 서블릿파일` 형태로 콘솔창에서 컴파일가능

#### Servlet URL 맵핑

- WEB-INF/classes 내부에 컴파일된 class파일을 배치하고, WEB-INF/web.xml내부에
```xml
<servlet>
    <servlet-name>별칭</servelt-name>
    <servlet-class>컴파일된서블릿클래스명</servlet-class>
</servlet>

<servlet-mapping>
    <servlet-name>별칭</servelt-name>
    <url-pattern>브라우저에서접근할URL</url-pattern>
</servlet-mapping>
```
- 애너테이션(@WebServlet("URL"))을 이용한 주소맵핑
```java
import javax.servelt.*;
import javax.servelt.http.*;
import java.io.*;

@WebServlet("브라우저에서 접근할 URL")
public class 서블릿명 extends HttpServlet
{
    // 메인함수가 아님 서블릿함수를 사용함으로서 WAS가 불러감
    public void service(HttpServletRequest request, HttpServletResponse response) throws IOException,ServletException
    {
        System.out.println("hello Servlet");
    }

}
```



#### Servlet 문자열 출력
```java
import javax.servelt.*;
import javax.servelt.http.*;
import java.io.*;

public class 서블릿명 extends HttpServlet
{
    public void service(HttpServletRequest req, HttpServletResponse resp) throws IOException,ServletException
    {
        PrintWriter out = resp.getWriter();
        out.print("Hello Servlet!!")
    }
}
```
- 콘솔이 아닌 웹브라우저에 해당 내용을 출력하는 내용



#### Servlet 인코딩 타입 설정하기
```java
@WebServlet("/hi")
public class Nana extends HttpServlet {
	@Override
	public void service(ServletRequest request, ServletResponse response) throws ServletException, IOException {
		response.setCharacterEncoding("UTF-8");
        // 응답데이터의 인코딩을 UTF-8로 진행하도록 설정
		response.setContentType("text/html; charset=UTF-8");
        // 응답할때 헤더에 contentType과 charset에 관한 내용을 추가해준다.
		PrintWriter out = response.getWriter();
		for(int i=0;i<100;i++) {
			out.println((i+1)+":안녕 Servlet!!<br>");
		}	
	}	
}
```



### GET 요청과 쿼리 스트링

- 서버에 요청하는 방식중 하나로 GET 방식이 있다
- URL(쿼리스트링)으로 붙여서 값을 전달한다
```
     http://localhost/hello?cnt=3
     http: 프로토콜
     localhost : 접속하려는 서버 IP혹은 이름
     hello : 접속하려는 페이지
     ?cnt = 3 : 쿼리스트링( hello 라는 페이지에 함께 전달되는 파라미터 = 값) 
```

```java
@WebServlet("/hi")
public class Nana extends HttpServlet {
	@Override
	public void service(ServletRequest request, ServletResponse response) throws ServletException, IOException {
		response.setCharacterEncoding("UTF-8");
        // 응답의 인코딩 방법 설정
		response.setContentType("text/html; charset=UTF-8");
        // 응답의 형식설정
		PrintWriter out = response.getWriter();
		
		String temp = request.getParameter("cnt");
        // cnt라는 이름의 파라미터의 값을 받아 temp에 저장 (파라미터의 값은 언제나 String)
		int cnt = 100;
        // cnt의 기본값 설정	
		if(temp != null&& !temp.equals("")) {
			cnt = Integer.parseInt(temp);
            // 만약 받아온 파라미터가 존재한다면 int형으로 형변환을 진행한후 cnt에저장
		}
    
			for(int i=0;i<cnt;i++) {
				out.println((i+1)+":안녕 Servlet!!<br>");
			}
            // 기본값 혹은 파라미터가 존재했다면 파라미터에 기술한 숫자만큼 출력
	
	}
```


#### 사용자 입력을 통한 Get요청

```html
<!-- index.html -->

<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Insert title here</title>
</head>
<body>

<a href="/JSPPrj/hi">default</a>
<a href="/JSPPrj/hi?cnt=50">50</a>

<form action="/JSPPrj/hi" method="get">
<!-- get방식으로 /JSPPRj/hi로 보낸다 -->
	"안녕하세요"를 몇 번 듣고 싶으세요? <br/>
	<input type="text" name=cnt />
    <!-- "cnt = 입력 값" 의 형태로 쿼리스트링을 만들어서 form태그가 지정한 장소로 전송 -->
	<input type="submit" value="출력" />
</form>


</body>
</html>
```

### POST요청
- get방식과 같이 쿼리스트링에 붙여 파라미터를 보내면 길이제한이 존재한다
- get방식은 쿼리값에 나타나기 때문에 보안에 취약하다
- 요청바디에 붙여서 전달한다.

```html
<!-- reg.html -->
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<div>
		<form action="notice-reg" method="post">
        <!-- notice-reg로 post방식으로 전송 -->
			<div>
				<label>제목</label><input type="text" name="title" />
                <!-- title이라는 이름의 파라미터로 저장 -->
			</div>
			<div>
				<label>내용</label>
				<textarea name="content"></textarea>
                <!-- content라는 이름의 파라미터로 저장 -->
			</div> 
			<div>
				<input type="submit" value="등록" />
			</div>			
		</form>
	</div>
</body>
</html>
```

```java
// 서블릿 파일 애너테이션을 통해 notice-reg로 url설정
@WebServlet("/notice-reg")
public class NoticeReg extends HttpServlet {
	@Override
	public void service(ServletRequest request, ServletResponse response) throws ServletException, IOException {
		response.setCharacterEncoding("UTF-8");
		response.setContentType("text/html; charset=UTF-8");
		request.setCharacterEncoding("UTF-8");
		// WAS에서 입력값을 UTF-8로 해석함
		
		PrintWriter out = response.getWriter();
		
		String title = request.getParameter("title");
		String content = request.getParameter("content");
		
		out.print(title);
		out.print(content);
	}
}
```

### 서블릿 필터
- Tomcat은 기본적으로 Charset으로 `iso-8859-1`을 사용하기 때문에 한글을 사용하기 위해서는 `request.setCharacterEncoding("UTF-8");`를 사용해주어야 한다. Tomcat에 기본설정을 바꾸는 것은 다른 어플리케이션에 영향을 줄 수 있기때문에 부담스러운 부분이 존재하여 서블릿 필터를 통해서 모든 서블릿 파일이 `UTF-8`로 해석 할 수 있도록 해준다.
- 서블릿 파일들의 요청,응답 이전에 실행할 코드를 담을 수 있다.


#### 필터설정 방법
1. web.xml설정 방법

```xml
 <filter>
 	<filter-name>characterEncodingFilter</filter-name>
 	<filter-class>com.newlecture.filter.CharacterEncodingFilter</filter-class>
 </filter>
 <filter-mapping>
 	<filter-name>characterEncodingFilter</filter-name>
 	<url-pattern>/*</url-pattern>
 </filter-mapping>
```
```java
package com.newlecture.filter;

import java.io.IOException;

import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebFilter;

public class CharacterEncodingFilter implements Filter {
	// Filter인터페이스를구현함으로 실행
	@Override
	public void doFilter(ServletRequest request, 
			ServletResponse response, 
			FilterChain chain)
			throws IOException, ServletException {
		
		request.setCharacterEncoding("UTF-8");
		// 요청하기 이전에 WAS에서의 입력값을 UTF-8로 해석하도록 설정함(헤더에 추가)
		chain.doFilter(request, response);
		// 요청 응답에 대하여. 서블릿을 흐름에 따라 계속 진행한다. 
		// doFilter 이전에 쓰여진 코드는 요청 흐름이 가기 이전에 실행되고 이후의 값을 응답받은 후에 실행된다.	
	}
}

```

2. 애너테이션(@WebFilter())을 통해 구현

```java
package com.newlecture.filter;

import java.io.IOException;

import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebFilter;

@WebFilter("/*")
public class CharacterEncodingFilter implements Filter {
	// 톰캣이 실행될때,요청,응답시 동작  
	@Override
	public void doFilter(ServletRequest request, 
			ServletResponse response, 
			FilterChain chain)
			throws IOException, ServletException {
		
		request.setCharacterEncoding("UTF-8");
		// 요청이전에 실행
		//// WAS에서 입력값을 UTF-8로 해석함
		chain.doFilter(request, response);
		// 요청 응답에 대하여. 서블릿을 흐름에 따라 계속 진행한다. 
		System.out.println("hello filter");
		// 응답시 실행
	
	}
}
```



#### 파라미터전달

- 아래 코드에는 필터가 존재한다.
```html
<!-- calc.html -->
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Insert title here</title>
</head>
<body>
	<form action="calc" method="post">
		값을 입력하세요 <br/>
		<div>
			<label> x: </label>
			<input type="text" name="x">
		</div>
		<div>
			<label> y: </label>
			<input type="text" name="y">
		</div>
		<div>
			<input type="submit" name="operator" value="덧셈">
			<input type="submit" name="operator" value="뺄셈">
		</div>
		
		<div>
			결과 : 0
		</div>
		
	</form>
</body>
</html>
```

```java
// Calc.java
package com.newlecture.web;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/calc")
public class Calc extends HttpServlet {

	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) 
			throws ServletException, IOException {
		String tempX = request.getParameter("x");
		String tempY = request.getParameter("y");
		String operator = request.getParameter("operator");
		int x = 0;
		int y = 0;
		if(tempX != null&&!tempX.equals("")) {
			x = Integer.parseInt(tempX);
		}
		if(tempY != null&&!tempY.equals("")) {
			y = Integer.parseInt(tempY);
		}
		
		PrintWriter out = response.getWriter();
		
		if(operator.equals("덧셈")){
		out.println("덧셈 결과: " +(x + y));
		}else if(operator.equals("뺄셈")) {
			out.println("뺄셈 결과: " +(x - y));	
		}
		
	
	}
}

```

#### 파라미터 배열 전달

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Insert title here</title>
</head>
<body>
	<form action="add2" method="post">
		배열로 보내기 <br/>
		<div>
			<label> num1: </label>
			<input type="text" name="num">
		</div>
		<div>
			<label> num2: </label>
			<input type="text" name="num">
		</div>
		<div>
			<label> num3: </label>
			<input type="text" name="num">
		</div>
		<div>
			<label> num4: </label>
			<input type="text" name="num">
		</div>
		
		<div>
			<input type="submit" value="덧셈">
		</div>
		
		<div>
			결과 : 0
		</div>
		
	</form>
</body>
</html>
```

```java
package com.newlecture.web;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/add2")
public class Add2 extends HttpServlet {

	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) 
			throws ServletException, IOException {
		String[] num_ = request.getParameterValues("num");
		// getParameterValues를 통해 배열로 받아온다.(파라미터를)
		int result = 0;
		
		for(int i = 0;i<num_.length;i++) {
			int num = Integer.parseInt(num_[i]);
			result+=num;
		}
		
		

		PrintWriter out = response.getWriter();
		out.println("덧셈 결과: " + result);
	}
}

```


## 상태 유지를 위한 5가지 방법


### application[서블릿 컨텍스트(Context)]
- WAS에 공용되는 저장공간
- 사용범위(scope): 전역 범위에서 사용하는 저장 공간
- 생명주기 : WAS가 시작해서 종료할 때 까지
- 저장위치: WAS서버의 메모리 


```java
@WebServlet("/calc2")
public class Calc2 extends HttpServlet {

	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) 
			throws ServletException, IOException {
		
		ServletContext application = request.getServletContext(); 
		
		String tempV = request.getParameter("v");
		String operator = request.getParameter("operator");
		int v = 0;
		
		if(tempV != null&&!tempV.equals("")) {
			v = Integer.parseInt(tempV);
		}
		if(operator.equals("=")) {
			int x = (Integer)application.getAttribute("value");
			// application.getAttribute의 반환값은 Object형으로 형변환 필 수 
			int y = v;
			String op = (String)application.getAttribute("operator");
			int result = 0;
			
			if(op.equals("+"))
				result = x + y;
			else
				result = x - y;
			
			response.getWriter().printf("result is %d\n", result);
		}
		else {
			 application.setAttribute("value", v);
			 application.setAttribute("operator", operator);			
		}	
	}
}

```
#### session
- 사용범위: 세션 범위에서 사용하는 저장공간
- 생명주기 : 세션이 시작해서 종료될 때 까지
- 저장위치 : WAS서버의 메모리


```java
package com.newlecture.web;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

@WebServlet("/calc2")
public class Calc2 extends HttpServlet {

	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) 
			throws ServletException, IOException {
		
		ServletContext application = request.getServletContext(); 
		HttpSession session =request.getSession();
		
		
		String tempV = request.getParameter("v");
		String operator = request.getParameter("operator");
		int v = 0;
		
		if(tempV != null&&!tempV.equals("")) {
			v = Integer.parseInt(tempV);
		}
		if(operator.equals("=")) {
			int x = (Integer)session.getAttribute("value");
			int y = v;
			String op = (String)session.getAttribute("operator");
			int result = 0;
			
			if(op.equals("+"))
				result = x + y;
			else
				result = x - y;
			
			response.getWriter().printf("result is %d\n", result);
		}
		else {		
			 session.setAttribute("value", v);
			 session.setAttribute("operator", operator);
		}
	}
}
// 한 번 값을 저장한 이후 다른 브라우저로 실행하면 NullPointException처리
```


#### 웹 서버의 세션 구분 방식
- 서로 다른 클라이언트가 서버에 요청을 하면 응답 시 SID값을 통해 서로 다른 저장소를 부여받는다.

- void setAttribute(String name, Object value)
	- 지정된 이름으르 객체 설정
- Object getAttribute(String name)
	- 지정한 이름으로 객체 반환
- void invalidate()
	- 세션에 사용되는 객체들을 바로 해제


- void setMaxInactiveInterval(int interval)
	- 세선 타임을 정수(초)로 설정
- boolean isNew()
	- 세션이 새로 생성되었는지 확인
- Long getCreationTime()
	- 세션이 시작된 시간을 반환,1970년1월1일을 시작으로 하는 밀리초
- long getLastAccessedTime()
	- 마지막 요청 시간,1970년1월1일을 시작으로 하는 밀리초


### cookie
- 클라이언트(브라우져)가 가지고 있는 저장소
- 사용범위 : Web Browser별 지정한 path범주 공간
- 생명주기 : Browser에 전달한 시간부터 만료시간 까지
- 저장위치 : Web Browser메모리 또는 파일

```java
// 쿠키 저장하기
Cookie cookie = new Cookie("cookie", String.valueOf(result));
response.addCookie(cookie);
//쿠키 읽기
Cookie[] cookies = request.getCookies();
String tempC = "";

if(cookies != null){
	for(Cookie cookie : cookies)
		if("cookie".equals(cookie.getName()))
			tempC = cookie.getValue();
}		
```




```java
@WebServlet("/calc2")
public class Calc2 extends HttpServlet {

	@Override
	protected void service(HttpServletRequest request, HttpServletResponse response) 
			throws ServletException, IOException {
		
		Cookie[] cookies = request.getCookies();
		String tempV = request.getParameter("v");
		String operator = request.getParameter("operator");
		int v = 0;
		String op = ""; 
		
		if(tempV != null&&!tempV.equals("")) {
			v = Integer.parseInt(tempV);
		}
		if(operator.equals("=")) {
			int x = 0;
			
			for(Cookie c:cookies) {
				if(c.getName().equals("value"))
				{
					x = Integer.parseInt(c.getValue());
					break;
				}
			}
			
			for(Cookie c:cookies) {
				if(c.getName().equals("operator"))
				{
					op = c.getValue();
					break;
				}
			}
			
			int y = v;
			int result = 0;
			if(op.equals("+"))
				result = x + y;
			else
				result = x - y;

			response.getWriter().printf("result is %d\n", result);	
	}
		else {
			Cookie valueCookie = new Cookie("value", String.valueOf(v));
			Cookie opCookie = new Cookie("operator", operator);
			valueCookie.setPath("/calc2");
			opCookie.setPath("/calc2");
			response.addCookie(valueCookie);
			response.addCookie(opCookie);
		}
	}
}

```

#### Cookie Path

```java
cookie.setPath("경로");
// 쿠키가 전송될 수 있는 경로 설정
```
#### Cookie Maxage ( 쿠키 생명 주기 설정 )
- 쿠키는 기간을 설정해주지 않으면 기본값으로 브라우저 프로세스가 켜져 있는 동안만 유지된다.
- maxAge옵션을 통해서 기간을 설정 해줄 수 있다.
- 기간 설정해준 쿠키는 브라우저 In-Memory 형태가 아닌 File 형태로 로컬 환경에 저장된다.

```java
cookie.setMaxAge(24*60*60);
// 하루 동안 쿠키를 유지하도록 한다.
```


### hidden input

### quertstring









### Redirection
```java
response.sendRedirect("calc2.html");
// 다시 calc2.html로 돌아간다는 의미
```


### GET , POST 함수

```java
if(request.getMethod().equals("GET")){
	// GET방식으로 요청왔을 때 실행
}

if(request.getMethod().equals("POST")){
	// POST방식으로 요청왔을 때 실행
}

```


- super.service(request,response)
	- POST방식으로 요청이 왔다면 doPost를 호출하고, GET방식으로 요청이 오면 doGet을 호출한다.
	- 수퍼 클래스에는 doPost와 doGet이 구현이 안되어있기 때문에 `super.service(request,response);`사용 하면 반드시 오버라이딩 해주어야한다 [ `doPost(),doGet()`중 하나를 ]
```java
super.service(request,response);

@Override
protected void doGet(HttpServletRequest request,HttpServletResponse response){
	System.out.println("doGet메서드 호출");
}
@Override
protected void doPost(HttpServletRequest request,HttpServletResponse response){
	System.out.println("doPost메서드 호출");
}
```




