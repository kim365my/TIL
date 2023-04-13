---
tag : 백엔드
aliases : Java Server Page, HTML 코드에 자바코드를 넣어 동적웹페이지를 생성하는 웹어플리케이션 도구
---


# 개요
>자바 + [[HTML]]
![[웹 개발론#백엔드의 흐름]]

# JSP란?
- 정의 
	- JSP = 그냥 html +[[Java]], 자바를 충분히 공부했다면 그다지 어렵지 않음 
	- JSP 등장배경 : 서블릿을 View단에서 보여주기 위해
		- 서블릿은 화면 구현이 불편하므로 화면 구현을 편하게 하기 위해서 등장
		- 서블릿 비지니스 로직과 결과를 보여주는 화면과 기능을 분리하기 위해 사용
		- 백엔드 개발자와 프론트엔드 개발자의 업무 영역을 확실히 분리하기 위해
		- 재사용성과 유지관리가 수월해짐
	- 파싱 과정 
		```mermaid
		graph LR
		  JSP --파싱--> Servlet--WAS-->서버--> View
		```
		- JSP로 코딩을 했다고 해서 JSP로 파싱이 되는 것이 아니고 Servlet으로 변환이 되어 파싱됨 (WAS는 Servlet만 해석 가능)
		- html 파일에 JSP가 코딩되니까 같이 브라우저가 인식한다고 생각할 수 있지만 전혀 아님
			- 흐름
				- WAS에서 jsp 파일을 먼저 읽은 다음에 jsp 코드를 한곳에 모음
				-  `<% %>`로 처리된 jsp 코드를 자바로 변환
				- HTML 파일을 실행
- [[Servlet]]과의 차이점
	- JSP도 서블릿 기술과 동일하게 동적으로 서버에서 데이터를 다루는 기술
	- 서블릿과 JSP 모두 동적으로 데이터를 생성해 전송하는 것은 같지만 서블릿은 자바와 HTML코드가 별개로 작성하는 반면에 JSP는 HTML 구조안에 코드를 작성함. 따라서 서블릿에 비해 View단 구현이 쉽지만 코드가 뒤섞일 우려가 있어서 Contoller은 서블릿으로 함
	- JSP에서는 `Get/Post` 처리방식의 구분이 없음
	- 구분
		- 서블릿 : 자바 코드 기반으로 HTML과 JS로 화면을 구현
			- 쿼리스트링에 대한 처리는 Servlet이 담당
		- JSP : HTML, CSS, JS를 기반으로 JSP 요소를 사용해 화면을 구현
			- View 단은 JSP가 담당
- HTML과의 차이점
	- HTML 태그는 컨테이너 작업없이 바로 브라우저로 전송되므로 동적인 구성이 아님
	- JSP는 WAS에서 자바로 변환되는 과정을 거치므로 JSP 제공 스크립트 요소를 이용하여 조건, 상황에 맞게 HTML 태그를 선택적으로 전송가능하므로 화면이 동적으로 구성됨
## JSP 파일 생성하기
- src -> main -> webapp에서 jsp 파일을 생성


## 다른 파일들과 연동해서 사용하기
### HTML, CSS, JS
- css와 JS도 기본 HTML에서 사용하는 것처럼 사용하면 됨
- form에서 다른 페이지로 넘기기 : 서블릿과 방법 동일
- 다음 코드와 같이 스크립틀릿 연결을 끊었다 이었다하면서 HTML 코드사이사이에 적어넣을 수 있음
- 코드예시
	```jsp
	<%@ page language="java" contentType="text/html; charset=UTF-8"
	    pageEncoding="UTF-8"%>
	    
	<%
		// 한글처리
		request.setCharacterEncoding("utf-8");
		response.setCharacterEncoding("utf-8");
		response.setContentType("text/html; charset=utf-8");
	
		// 값 받기
		String id = request.getParameter("user_id");
		String pw = request.getParameter("user_pw");
	%>
	<!DOCTYPE html>
	<html>
	<head>
	<meta charset="UTF-8">
	<title>JSP 로그인 결과 출력</title>
	</head>
	<body>
	    <h1>JSP 로그인 결과 출력</h1>
	    <ul>
	        <li>아이디 : <%= id%></li>
	        <li>비밀번호 : <%= pw%></li>
	    </ul>
	    <hr>
	    <%
	    	if(id == null || id.length() == 0){ // 아이디 값이 없으면
	    		// 아이디 입력하기
	    %>
	    	<h3>아이디 입력하세요</h3>
	    <%
	    	} else{
	    		//아이디가 있는 데 adimin이라는 아이디로 입력하면 다른 곳으로가기
	    		if(id.equals("admin")){
	    			// 관리자 로그인
	    %>
	        <h3>관리자님 환영합니다.</h3>
	    <%
	    		} else{
	    			// ...님 환영합니다.
	    %>
	                <h3><%= id%>님 환영해여</h3>
	    <%
	    		}
	    	}
	    %>
	    
	</body>
	</html>
	```

### Servlet 연동하기
- 서블릿에 앵커태그를 넣어서 jsp 파일로 이동하게 할 수 있음 
	- 이동하려면 html에서 하는 것과 동일하게 `./`을 넣고 이동할 파일명을 적어주면 됨


# JSP 기본 문법
- JSP 구성요소
	1. HTML, CSS, JS
	2. JSP 기본태그
	3. JSP 액션태그
	4. 커스텀 태그
		- 개발자가 직접 제작하여 사용하는 태그와 프레임워크가 제공하는 태그를 말함


## JSP 내장객체
- session : HttpSession 객체를 선언안해도 사용가능
- out
- 등등
- JSP 내장 객체는 표현식에서만 사용가능(변수사용했을 때) 그래서 나온게 EL
### JSP에서 session 로그인 처리하기

- session의 유지시간은 밀리세컨드로 받음
	- `session.setMaxInactiveInterval(interval)`
### 바인딩 하기



## JSP 기본 태그
- JSP 기본폼(스크립트 요소) : `<% %>`
- 페이지 디렉티브 태그 : `<%@ %>`
- 주석 작성하기 : `<%-- --%>` 
	- [[이클립스]]에서는 `ctrl+alt+c` 단축키로 주석된다던데 오류인가? 안됨

### JSP 스크립트 요소 : 선언문, 스크립틀릿, 표현식
- JSP 스크립트 요소 안에서 자바코드를 작성
	- 선언문(declaration tag)  JSP에서 변수나 메서드 선언에서 사용
		- 서블릿으로 변환시 서블릿 클래스의 멤버변수로 변환
		- 일반적으로 상단에 코딩
		- 클래스 선언하는 것과 동일, 보통 따로 만들기에 안씀
	- 스크립틀릿(scriptlet) : JSP에서 자바 코드 작성시 사용
		- 코드 블록 안에 쓰는 코드는 지역변수 취급
		- 하나의 클래스를 만드는 것과 동일하게 취급(익명 클래스?)
	- 표현식(expression tag) : JSP에서 변수 값 출력시 사용
		- (주의) 변수나 자바 식에는 절대 세미콜론`;`을 사용해서는 안됨

- HTML 파일 어디에서나 사용해도 되지만 top-down은 지켜줘야 함
- JSP 스크립트 요소는 모두 서블릿의 자바 코드로 변환됨
	- 스크립트 요소는 브라우저로 전송이 바로 되지 않음
	- 브라우저는 HTML, CSS, JS만 전송됨
- JSP 코드는 +연산자를 사용해 쓸 필요가 전혀 없음 (섞여있는 거라)

#### 스크립트 요소 코드 형식
|                          | 코드형식 |  설명   |
| ------------------------ | :--------: | --- |
| 선언문 (declaration tag) | `<%!%>` | JSP에서 변수나 메서드 선언에서 사용|
| 스크립틀릿(scriptlet)    | `<%%>`   | JSP에서 자바 코드 작성시 사용 |
| 표현식(expression tag)   | `<%=%>` | JSP에서 변수 값 출력시 사용 |

#### 선언문 (declaration tag)

- 선언부 : Servlet에서 인코딩 설정할때와 똑같은 내용이라고 보면 됨
	```jsp
	<%@ page language="java" contentType="text/html; charset=UTF-8"
		pageEncoding="UTF-8"%>
	```
- 페이지 디렉티브 태그 : JSP 페이지에 대한 전반적인 설정 정보를 지정할 때 사용
	- 속성은 무조건 한번만 선언해야 함 (단, import 속성은 여러번 선언가능)
	- 대, 소문자 유의
	```jsp
	<%@ page
		language="java"
		import="java.util.*"
		contentType="text/html; charset=utf-8"
		pageEncoding="utf-8"
		session="true"
		info="페이지 설명"%>
	```

##### 인클루드 include 디렉티브
- 코드
	```jsp
	<%@ include file="/NewFile01.jsp" %>
	```
- 인클루드 사용장소
	- 공통으로 JSP 페이지에 사용할경우 적용 ex) gnb, footer
	- 재사용성과 유지보수가 쉬움
- 인클루드 작동방식
	- 인클루드 태그와 JSP 페이지를 요청
	- include.jsp의 자바코드가 해당 작성한 파일과 합쳐져서 브라우저에 전송
		- 한 페이지당 자바코드는 하나 (무조건)
		- JSP 페이지에서 실행하는 자바파일은 단 한개만 생성
	- 자바코드로 변환
	- 사바코드 서블릿 변환
	- class 컴파일 후 브라우저 출력




## JSP 액션 태그
- 액션태그의 형식
	- XML에서 문법을 받아왔으므로 태그 닫는거 필수
	- `< />`식으로 단일 태그로 할 수 있음
- 액션 태그의 탄생
	- 자바 코드를 JSP 파일에서 없애는 것이 목적으로 화면이 점점 복잡해짐에 따라 프론트엔드 개발자(=퍼블리셔)들도 자바코드를 써야하는 문제로 이슈 발생, 그래서 JSP는 스크립틀릿의 자바 코드를 제거하고 더 쉽고 편리하게 작업 할 수 있는 태그 형태로 기능을 제공해야 하는 필요성이 생김
- 액션 태그의 기능
	- 액션태그를 조합해서 파라미터 값을 넘겨주거나, 자바빈에 값을 저장하는 등

### 액션태그 종류 (이외에도 더 존재)
| 이름        | 설명                                                       | 코드예시                                                        |
| ----------- | ---------------------------------------------------------- | --------------------------------------------------------------- |
| include     | 해당 페이지를 현재 페이지에 포함시키는 것                  | <jsp:include page ="페이지.jsp" />                                |
| forward     | 서블릿의 RequestDispatcher 클래스와 [[포워딩]]을 대신하는 태그 | <jsp:forward page="./페이지.jsp" />                                                                |
| useBean     | 객체를 생성하기 위한 태그                                  | <jsp:useBean id="이름" class="자바빈 클래스 이름" scope="범위"> |
| getProperty | 자바빈 속성 설정 가져오는 태그, String으로 출력됨    |  <jsp:getProperty name="사용할 유즈빈 id값" property="속성값이름" />                                                               |
| setProperty | 자바빈 속성 설정, 자바빈의 멤버변수와 파라미터 값이 동일하면 `property="*"`를 통해서 일괄적으로 값 할당 가능             |  <jsp:setProperty name="사용할 유즈빈 id값" property="속성값이름" value="속성값" />                                                               |
| param  | 파라미터 설정을 통해서 값을 넘겨줄 수 있음                      | <jsp:param name="키명" value="키값"/>                                                         |


### 액션태그로  [[자바빈]]과 연결하기 
- <jsp:useBean>
	- id :  id 값을 이용해서 스크립틀릿에서 객체의 메소드에 접근 가능
	- class : 자바빈으로 사용할 클래스 이름(`패키지명.클래스_이름` 형식으로 작성)
	- [[scope]] : 자바빈에 접근할 수 있는 저장 범위를 지정 (기본값은 page)
- <jsp:setProperty>
	- [[자바빈]]과 파라미터 값이 동일하면 property 속성을 
	- property 속성을 `*`로 하면 전송된 매개변수 이름과 자바빈 멤버변수를 비교하고 값을 자동으로 모두 넘겨줌
		- 같은 데이터 타입으로 맞추기(String으로 넘겨 받으니까 멤버변수를 String으로 작성하는 것이 중요)
- <jsp:getProperty>
	- 문자열로 출력되니까 HTML에서 결과값을 보고 싶을 경우 사용


# EL (Expression Language)
- 형식 : `${ }`
	- ⭐사용하기 위해서는 선언문에서 `isELIgnored="false"` 설정필요 (안해도 출력은 됨)
	- 프로퍼티 표현법
		- [] 연산자 사용 : `${user["name"]}`
		- 점연산자 사용 : `${user.name}`
- 메소드 표현법 : `${user.size()}`
- 표현언어의 특징
	- 표현식이 아니고 언어? #질문 
	- JSP 표현식을 보다 편하게 데이터를 출력하기 위해 JSP2.0에서부터 도입됨 (요즘 나오는 프로그래밍 언어들은 거의 표현식을 사용)
		- JS ES6의 Xpath처럼 구조 분할 방식
	- 기본적으로 할 수 있는 기능
		- 변수와 여러가지 연산자 포함가능
		- JSP 내장 객체에 저장된 속성 및 자바빈 속성도 출력가능
		- EL 자체의 내장 객체 제공
		- EL의 취급가능한 데이터 
			- 문자, 숫자 출력 가능 (리터널 데이터로 취급)
			- 기본적인 연산가능 (산술, 비교, 논리, 논리부정, 크기비교 연산자)
				- 숫자형 문자열과 숫자를 연산할 경우 자동으로 숫자로 형변환하여 연산



## EL의 내장객체
> JSP에서 기본적으로 내장객체를 제공하지만 JSP 내장객체는 표현식에서만 사용가능
> 그래서 EL에서 따로 내장 객체를 제공하며 EL의 형식 내에서 사용가능

### EL Empty 연산자
- [[자바빈]]의 속성이 값으로 설정되었는지 또는 컬렉션 객체에 값이 존재하는지 판단하는 연산자
- 리턴값 : boolean
- 형식 : `${ empty mbean }`
- 예시
	```html
    <!-- 유즈빈에 값이 있으므로 false 반환 -->
	${empty mbean } <br>
    <!-- 논리부정 -->
	${not empty mbean } <br>
    <!-- 값이 없으면 true -->
	${empty "ezen" } <br> <!--false-->
	${empty "" } <br> <!--true-->
	${empty null } <br> <!--true-->
	```

### [[Scope]] 관련 내장객체
- 기본적으로 JSP와 동일하며 [[바인딩]] 된 데이터에 접근 가능
- DTO 작성시 [[자바빈]] 형태로 작성
- 객체명
	- requestScope : JSP request와 동일
	- sessionScope
	- applicationScope 
- 사용형식 : `${객체명.가져올_키명}`


#### EL form 데이터 받기
- `param` : getParamter()를 사용하지 않아도 사용가능
	- 사용예시 : `${param.name값}`

### EL로 [[바인딩]]하기
- 


# JSP 예외처리(exception) 페이지
- 정의
	- 보통 Servlet에서 예외처리를 하니까 있다는 것만 알아두기
- 형식
	- 오류가 발생 할 페이지에 선언문에  `errorPage=""`로 이동할 예외처리 페이지를 지정
	- 예외처리 페이지 코딩
		- 예외처리 내장객체 : `exception`
			- 주로 사용하는 메소드
				- .toString()
					- 에러 관련 문자열 출력
					- `<%= exception.toString() %>`
				- .getMessage()
					- 어느 부분에서 에러가 났는지 출력
					- `<%= exception.getMessage() %>`
				- .printStackTrace() 
					- 객체로 반환되기 때문에 다른 메소드와 다르게 스크립틀릿으로 사용해야 함
					- `<% exception.printStackTrace();%>`


# 연관문서