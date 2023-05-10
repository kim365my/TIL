---
tag : 백엔드
aliases : Java Server Page, HTML 코드에 자바코드를 넣어 동적웹페이지를 생성하는 웹어플리케이션 도구
---


# 개요
>[!info]- 자바 + [[HTML]], 기본적으로 [[Servlet|서블릿]]과 거의 동일함

>[!warning]
>코드를 읽는 시기가 다르기에 스크립틀릿과 표현식(EL, JSTL)은 함께 사용할 수 없음
>하지만 EL과 JSTL은 함께 사용 가능

# JSP란?
- 정의 
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
- JSP 구성요소
	1. HTML, CSS, JS
	2. JSP 기본태그
	3. JSP 액션태그
	4. 커스텀 태그
		- 개발자가 직접 제작하여 사용하는 태그와 프레임워크가 제공하는 태그를 말함

## JSP 파일 생성위치
- src -> main -> webapp에서 jsp 파일을 생성


## 다른 파일들과 연동해서 사용하기
### HTML, CSS, JS
- 서블릿은 HTML 파일에 작성하는 거
- css와 JS도 기본 HTML에서 사용하는 것처럼 사용하면 됨
- form에서 다른 페이지로 넘기기 : 서블릿과 방법 동일
- 다음 코드와 같이 스크립틀릿 연결을 끊었다 이었다하면서 HTML 코드사이사이에 적어넣을 수 있음
	- for문을 통해서 특정 HTML 구문을 반복해서 출력하게 할 수도 있음
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



# JSP 내장객체 (이외에도 존재)

## 스코프
| 객체명      | 서블릿 코드                             |  설명   |
| ----------- | --------------------------------------- | --- |
| page        | JSP에서만 존재하는 듯 #질문             |     |
| request     | HttpServletRequest request              | 요청에 관련된 메소드를 가짐|
| response    | HttpServletResponse response            | 응답에 관련된 메소드를 가짐 |
| session     | HttpSession session = request.getSession();  | 스코프의 범위가 request보다 넓음|
| application | ServletContext                          |     |
| out         | PrintWriter out = response.getWriter(); |     |

- JSP 내장 객체는 표현식에서만 사용가능(변수사용했을 때) 그래서 나온게 EL
- [[Scope|스코프]] 관련 객체들은 `get/setAttribute("keyname", Object)` 메소드를 가지는 데 이를 통해서 데이터를 공유가 가능
- [?] request는 `get/setParamter`이라는 파라미터 값을 받는 메소드가 존재 위의 Attributer와 어떤 차이가 있지?  #질문 


# JSP 기본 문법
### JSP에서 session 로그인 처리하기

- session의 유지시간은 밀리세컨드로 받음
	- `session.setMaxInactiveInterval(interval)`


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
| ------------------------ | -------- | --- |
| 선언문 (declaration tag) | `<%! %>` | 변수나 메서드 선언에서 사용|
| 스크립틀릿(scriptlet)    | `<% %>`   | 자바 코드 작성시 사용 |
| 표현식(expression tag)   | `<%= %>` | 변수 값 출력시 사용 |

#### 선언문 (declaration tag)
##### 선언부 page
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


### [[자바빈]]과 연결하기 
- <jsp:useBean>
	- id :  id 값을 이용해서 스크립틀릿에서 객체의 메소드에 접근 가능
	- class : 자바빈으로 사용할 클래스 이름(`패키지명.클래스_이름` 형식으로 작성)
	- [[scope]] : 자바빈에 접근할 수 있는 저장 범위를 지정 (기본값은 page)
- <jsp:setProperty>
	- [[자바빈]]과 파라미터 값의 name이 동일시 property 속성을 `*`로 지정하면 전송된 매개변수 이름과 자바빈 멤버변수를 비교하고 값을 자동으로 모두 넘겨줌
		- 같은 데이터 타입으로 맞추기(String으로 넘겨 받으니까 멤버변수를 String으로 작성하는 것이 중요)
	- 이외에 value 속성을 통해 값을 설정해주는 것도 가능
- <jsp:getProperty>
	- 문자열로 출력되니까 HTML에서 결과값을 보고 싶을 경우 사용

### 포워딩, 바인딩하기
- <jsp:forward>
	- 디스패처로 forward 한 것과 동일한 결과를 얻음
	- page 속성 뒤에 #Query_String 으로 파라미터 값을 넘겨줄 수 있음
- <jsp:param>
	- 파라미터에 자바빈으로 값을 넘겨주면 파라미터를 통해서 받을 수 있음


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


# EL (Expression Language)
>[!info]
> - 표현언어의 등장
>	- JSP 표현식을 보다 편하게 데이터를 출력하기 위해 JSP2.0에서부터 도입됨 (요즘 나오는 프로그래밍 언어들은 거의 표현식을 사용)
>	- JS ES6의 Xpath처럼 [[구조 분해 할당]]
>		- 메모리에 떠있는 객체들에 직접 접근이 가능함
>			- ex. `${i.title}`처럼 원래라면 get 메소드를 이용해 가져와야하는 데이터에 직접 접근이 가능

>[!warning] JSP에서 기본적으로 내장객체를 제공하지만 JSP 내장객체는 표현식에서만 사용가능. 그래서 EL에서 따로 내장 객체를 제공하며 EL의 형식 내에서 사용가능

## EL의 기본 형식
- 형식 : `${ }`
	- [*] 사용하기 위해서는 선언문에서 `isELIgnored="false"` 설정필요 (안해도 출력은 됨)
	- 직접 값 접근에 가능하기에 `${키명}`식으로 접근하면 됨
		- [*] [[Scope|스코프]]에 저장된 값만 출력이 가능(page, request, session, applictaion)
	- 프로퍼티 표현법
		- [] 연산자 사용 : `${user["name"]}`
		- 점연산자 사용 : `${user.name}`
	- 메소드 표현법 : `${user.size()}`
- 기본적으로 할 수 있는 기능
	- 변수와 여러가지 연산자 포함가능
	- JSP 내장 객체에 저장된 속성 및 자바빈 속성도 출력가능
	- EL 자체의 내장 객체 제공
	- EL의 취급가능한 데이터 
		- 문자, 숫자 출력 가능 (리터널 데이터로 취급)
			- 문자 출력 : `${'문자열'}`
			- 숫자 출력 : `${40}`
		- 기본적인 연산가능 (산술, 비교, 논리, 논리부정, 크기비교 연산자)
			- 숫자형 문자열과 숫자를 연산할 경우 자동으로 숫자로 형변환하여 연산

## EL의 내장객체
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


### EL의 [[Scope]] 우선순위
- EL은 값에 키명으로 직접 접근이 가능하므로 여러개의 스코프에서 동일한 변수명이 있을 경우 아래처럼 우선순위가 있음
	- [*] 1) page > 2) request > 3) session > 4) application



# JSTL (JSP 표준태그 라이브러리)
>[!info]
> - JSP의 단점을 개선하기 위해 나온 것
> -  커스텀 태그 중 가장 많이 사용하는 태그를 표준화하여 라이브러리로 제공하는 것
> - JSP2.0 규약에서부터 추가되어 톰켓에서는 기본적으로 제공되지 않음
>	- 따라서 플러그인을 설치해줘야 사용 가능
> - 자바의 기능을 태그로 대체가 가능하다는 개념 
> - 사용하려면 JSP 선언부에 taglib 태그에 추가하여 톰캣에 알려줘야함
>	- value 값의 출력은 EL 표기법을 사용
>		- 입력에도 EL 표기법 사용가능
> - JSTL 태그의 종류
>	- 라이브러리 코어
>		- 변수지원
>		- 제어문, 반복문 처리
>		- URL 처리등이 가능 
>		- 접두어 c(Core)를 가장 많이 사용

>[!warning] JSP의 스크립틀릿에서 JSTL로 선언한 변수를 사용하지 못하니까 JSTL의 제어문을 통해서 제어해야함

## 플러그인 설치
- [설치 페이지](http://www.java2s.com/Code/Jar/j/Downloadjstl12jar.htm#google_vignette)에서 다운 받고 압축 푼 다음, 이클립스 프로젝트파일의 src->main->webapp-> WEB-INF->lib 경로에 .jar 파일을 넣으면 됨

## JSTL 라이브러리 코어 태그 문법
```jsp
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
```
- 코어 태그를 사용하겠다고 선언

###  변수관련
#### import : 페이지 임포트
```jsp
<c:import url="${login }"/>
```
- 페이지 임포트

#### set : 변수선언
```jsp
<c:set var="변수명" value="값" scope="범위"
```
- value : EL로 작성 가능
- [[scope]] : 생략가능, 기본값은 page
	- [?] 전역변수로 저장됨, page는 한 page에서 사용할 수 있는 범위인가? 아직 명확하게 생각이 정리가 안돼 #질문  : [[Scope]]에서 설명했듯이 page는 JSP에서만 사용되며 지역변수처럼 이용됨
- EL로 value에 대입할 경우 `""`를 써줘야함
	```jsp
	<c:set var="age" value="${43}" />
	```


#### out : 변수 출력
```jsp
<c:set var="str" value="<h3>수업중입니다.</h3>"/>
<c:out value="${str})" escapeXml="false"/>
```
- 출력, 이스케이프 문자 등을 지정가능
- escapeXml="false"로 할시 html 태그를 인식시킬 수 있음
	- 기본값은 true


- <c:out>태그안에 내용을 넣어주면 다 문자열이 됩니다  
- 컨트롤러에서 alert()이라는 문자열이 어떤 키 안에 특정값으로 들어갔다고 하면 이상태에서 <c:out>을쓰지 않으면 alert창이 웹상에서 떠 버립니다
- <c:out>”alert()”</c:out> 이렇게 c:out을 써주면 alert()라는 문자열로만 보여집니다 alert창이 따로 뜨질 않는거죠
- 보안에도 관련이 있는데 alert()이 아닌 악성코드라고 한다면 감염이 될 것입니다 그것을 String으로 받아버리면 alert()이 아니라 <c:out>이 문자열로 받아버리니까 감염 될 일이 없고요 그래서 무조건 c:out으로 문자열로 만들어 주는게 중요합니다

### 제어문
#### if문 (단일if만 존재)
```jsp
<c:if test="${비교값}">참일 경우 실행시킬 구문</c:if>
```
- test에는 EL 표기법으로 작성
	- EL empty 연산자를 많이 사용(null 체크를 위해서)

#### choose 태그 (if~else)
```jsp
<c:choose>
	<c:when test="조건식">
		참일경우 실행할 구문
	</c:when>
	<c:otherwise>
		거짓일경우 
	</c:otherwise>
</c:choose>
```
- null 체크
	- 고정값 이외의 값은 동적으로 변하니까  처음 로딩시 null이 기본값으로 들어가니까 고정값을 넣어주기 위해서 사용

### 반복문
#### forEach (가장 많이 사용)
```jsp
<c:forEach var="변수명" items="반복 객체 파일" begin="시작점" end="마지막값" step="증가값" varStatus="반복상태">
	반복할 구문
	${반복상태.count} <!--몇번 반복했는지 표시-->
</c:forEach>
```
- [*] var와 items 속성은 필수
- varStatus : 반복문의 상태를 알려줌
	- status.index : 인덱스 (0부터 시작)
	- status.count : 카운트 (1부터 시작)
	- status.current : 현재 아이템, var 속성의 값과 동일
	- status.first : 현재가 첫번째 루프면 참
	- status.last : 현재가 마지막 루프면 참
	- status.begin : begin 속성 사용시 나옴
	- status.end : end 속성 사용시 나옴
	- status.step : step 속성 사용시 나옴
##### 객체값
```jsp
<c:forEach var="변수명" items="${반복 객체 파일}">
	반복할 구문 ${변수명 }
</c:forEach>
```
- 변수명을 통해서 반복할 객체 파일에 접근가능
- 참고로 EL은 Scope에 있는 값만 접근 할 수 있기에 객체를 사용하려면 변수에 담아주는 과정을 거쳐야함

#### forTokens
```jsp
<c:set var="football" value="최범근, 이희택, 박지성, 안정환, 최순호"/>
<c:forTokens var="football2" items="${football }" delims=",">
	${football2 }
</c:forTokens>	
```
- 구분자를 이용해 문자열을 분리하여 출력하는 태그
- delims : 구분자를 선택
- items : 문자열

### 주소창 관련
#### c:redirect
```jsp
<c:redirect url="./206_reditc2.jsp">
	<c:param name="param2" value="ezen" />
	<c:param name="param3" value="computer" />
</c:redirect>
```
#### url
```jsp
<c:url var="login" value="주소값"/>
```
- url 주소값을 담기 위해 사용됨
- 단지 경로만 저장됨

## JSTL fmt 태그 문법
```jsp
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt"%>
```
- 포맷을 지정가능
## 시간
### formatDate
```jsp
<c:set var="today" value="<%= new Date() %>"/>
오늘날짜:<fmt:formatDate value="${today }" type="both" dateStyle="full"/>
```
- type
	- both : 둘다 출력
	- time : 시간만 출력
	- date : 날짜만 출력
- dateStyle  : 날짜 표시 스타일
	- full : 전부 `ex) 2023년 4월 17일 월요일
	- long : 요일을 제외하고 `ex) 2023년 4월 17일`
	- medium : `ex) 2023. 4. 17.`
	- short : `ex) 23. 4. 17.`
- timeStyle : 시간 표시 스타일
	- full : 전부  `ex) 오전 10시 28분 0초 대한민국 표준시`
	- long : `ex) 오전 10시 28분 0초 KST`
	- medium : `ex) 오전 10:28:00`
	- short : `ex) 오전 10:28`
- pattern : 패턴 사용, 아래 예약어를 사용해 원하는 대로 출력할 수 있음
	- YYYY : 년도
	- MM : 월
	- dd : 일
	- HH : 24시간 표시 | hh : 12시간 표시
	- ss : 초
	- SS : 밀리초 
	- EEEE : 요일
	- a : 오전, 오후

### fmt:timeZone
```jsp
<fmt:timeZone value="Asia/Seoul">
	런던 : <fmt:formatDate value="${today }" type="both"/>
</fmt:timeZone>
```
- value로 지역을 선택해서 시간을 보여줄 수 있음

### fmt:setTimeZone
```jsp
<fmt:setTimeZone value="America/New_York"/>
```
- value로 지역을 설정해서 앞으로 나오는 formatDate의 시간을 해당 지역의 시간으로 맞춤



# 연관문서