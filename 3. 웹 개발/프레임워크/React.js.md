---
tag : 프론트엔드 프레임워크
aliases : 리액트
---

# 개요
- 리액트는 똑같은 요청에 하나의 응답만 되돌려줌
- SPA(싱글 페이지)를 만드는 데 최적화된 프레임워크, 대용으로 [[Vue.js]]가 존재
- [[React.js]]의 문법은 [[JS]]의 ES6버전 문법을 사용
- 라이브러리와 프레임워크
	- 라이브러리는 책처럼 쓸 수 있는 것으로 해당 문법만 사용하지 않아도 됨
	- 프레임워크는 프레임워크의 문법을 따라야함 (대표예 : 톰캣)

>[!warning] 주의사항
>- 기본적으로 [[JS]]와 문법이 거의 동일하지만 스크롤 이벤트나 alert() 등의 이벤트 메서드들은 여러번 반복하여 동작하는 경우가 존재하므로 Hooks의 useState를 사용해야 하는 불편함이 존재


## 설치하기
- [[Node.JS]] 설치 필요
- [[React.js]] 설치하기
	```
	npm install -g create-react-app
	npm i -g create-react-app 
	```
	- 경고창이 표시될텐데 무시하고 넘어가면 됨
- 보일러 플레이트
	```
	create-react-app 설치폴더명
	```
- 프로젝트 실행 : `npm start`에서 리액트 아이콘이 뱅글뱅글 돌아가면 성공
- 프로젝트 빌드 : `npm run build`
- 별도의 라이브러리를 설치하고 싶은 경우 `npm install 라이브러리명`으로 작성하면 되고, 특정 버전을 쓰고 싶으면 `@버전번호`를 뒤에 추가
- [i] [[VSC]] 필수 확장 프로그램 설치 : ES7+ React/Redux/React-Native snippets
	- 단축키 : `rce / rfc / rafc / rafce  / rcc`

# 리액트 문법
- **기본 폴더구성** : 위의 보일러 플레이트로 파일을 설치했다면 폴더 구성이 다음과 같이 되어있음
	- node_modules : node.js 파일이므로 건들일 일 없음
	- public 폴더 : 정적파일 (ex. html, css 등)
	- **src 폴더** : 동적파일로 실제로 코드 작업이 이뤄지는 부분
		- index.js : 코드를 보면 알다싶이 index.html의 `#root`를 받아서 `<App />` 컴포넌트를 출력하는 형태이다. 컴포넌트는 사용자지정태그로 표시할 수 있어서 `<App />`로 작성된 것으로 실제 출력되는 코드는 App.js 파일로 들어가야한다.
			```js
			const root = ReactDOM.createRoot(document.getElementById('root'));
			root.render(
			  <React.StrictMode>
				<App /> // app.js에 있는 함수 app부분이 출력됨
			  </React.StrictMode>
			);
			```
		- App.js : 코드를 보면  `<div>App</div>`을 return하는 함수임을 알 수 있다. 따라서 화면에는 App이라는 글자가 출력된다. 
			```jsx
			import React from 'react'
			function App() {
			  return (
			    <div>App</div>
			  )
			}
			export default App
			```
	- **package.json** : 제일 중요한 파일로 각종 라이브러리의 버전 관리를 해주거나 node_modules 폴더가 없어도 새로 설치해주는 파일이므로 잃어버리지 말 것
		- [*] `dependencies` : 의존관계
			- 의존하고 싶은 애를 이 json에 넣는걸 의존성 주입이라고 함
			- 뭐가 안될경우 여기서 버전 체크하고 해당 버전에 맞게 해야함
- ### 컴포넌트
	- 그래서 컴포넌트가 뭔데?라고 하면 레고를 쌓는것처럼 코드를 조합하는거라고 대답하래. #기술면접 
	- **컴포넌트 퍼스트**
		- 컴포넌트를 사용할 경우 사용자 태그 형식으로 지원하게 된다. (ex. `<AddCompontent/>`)
		- 컴포넌트들은 실제 작업파일을 의미하며 웹팩의 역할도 담당한다. 웹팩이란 여러 기능들을 모아두는 것으로 쉽게 말해서 모듈화를 의미한다.
		- 리액트는 이런 컴포넌트들을 서버에서 받아서 [[JS]] 객체로 **가상 DOM 영역**을 만들어 보관하는데, DOM 객체 구조에 변화가 없으면 서버에 재방문하지 않는다. 
			- 가상 DOM 영역을 만들기 위해서는 한개 이상의 트리구조가 존재해야 한다. 공백태그나 `<frameElement></frameElement>`를 사용해야 한다.
	- **컴포넌트의 종류**
		- **함수형**
			- 선언이 간편, 메모리 자원도 덜 사용, 리액트 v16.8 Hooks 기능이 도입되면서 사용이 편리해짐.
			- 기존 state, 생명주기함수의 사용이 안되었으나, 리액트 v16.8 업데이트 이후 사용이 가능해짐
			- [규칙] 반드시 return()에 코딩해서 값을 반환해주어야함
				```jsx
				// 기본 함수형
				import React from "react";
				function App() {
					return (
						<div>
							<h1>Hello Recat!!</h1>
						</div>
					)
				}
				// 화살표 함수 사용시
				import React from "react";
				const App = () => {
					return (
						<div>
							<h1>Hello Recat!!</h1>
						</div>
					)
				};
				```
		- **객체형**
		- state 가능, 생명주기 함수, 임의의 메서드를 정의해서 사용가능
		- [규칙] 클래스는 리턴값이 없으므로 `render()` 함수를 이용해서 출력
			```jsx
			import React, {Component} from "react";
			class App3 extends Component {
				render() {
					return(
						<div>
							<h2>클래스형 컴포넌트</h2>
						</div>
					);
				};
			};
			```
- ### Hooks 
	- 리액트 v16.8에서 도입됨
	- **useState** : 함수형 컴포넌트에서 data의 상태 관리를 할 수 있음
	- **ustEffect** : 랜더링 직후의 작업을 설정
	- 이외에도 많음


## JSX 문법

- [[JS]]만의 확장문법, [[XML]]의 형식을 따름
- [기본형식]  [[XML]] 폼을 따르기 때문에 모든 태그는 반드시 닫는 태그가 존재해야하며, return 내 반드시 하나의 부모태그가 존재해야함
- ### 기본 함수형
	- 최상위 부모태그를 `<div></div>`가 아닌 `<></>` 빈태그(아니면 Fragment)로 묶어도 됨
		- Fragment란, Dom에 별도의 노드를 추가하지 않고 여러 자식을 하나로 그룹화해줌 16.8v 이후에 사용가능
			```jsx
			import React, {Fragment} from "react";
			function app6() {
			  return(
				<frameElement>
				  <h1>데이터</h1>
				</frameElement>
			  );
			}
			```
	- 조건문 사용하기 (3항연산자, 물론 if문도 쓸수 있음)
		```jsx
		{(name === "mssam") ? "" : " name이 기본값이 아니네요"}
		{1-1 === 0 && "참인경우만 실행"}
		{1-2 === 0 || "거짓인 경우에만 실행"}
		```
- ### 인라인 스타일 지정
	- `<h1 onClick={meg} style={{cursor: "pointer"}}>` 이런식으로 괄호를 두개씩
		```jsx
		function app8 () {
		  const name = "mc";
		  const jsxStyle = {
			"background-color" : "red",
			"font-size" : "24px",
			"padding" : "8px",
			"color" : "#fff"
		  };
		  return(
			<frameElement>
			  <p style={jsxStyle}>{name}을 출력합시다</p>
			</frameElement>
		  );
		}
		```
- ### 컴포넌트 추가방식
	```jsx
	{AddComponent()} // 함수형식으로 추가하기
	<AddComponent/> // 태그형식으로 추가하기, 아무거나 써도 ok
	```
	- 태그 형식은 같은 파일 내에서는 사용 못하나봐.
- ### Props(=properties)
	- 부모 컴포넌트에서 자식컴포넌트로 데이터를 전달할 때 사용하는 속성
	- 컴포넌트를 외부에서 조작할 때 사용
	- [!] 부모 컴포넌트로 호출해야 값이 표시됨
	- 예시
		- 부모 컴포넌트
			```jsx
			import React from 'react'
			import SecoundComponent from './SecoundComponent' // 값을 보내줄 컴포넌트 지정
			/** 부모 컴포넌트 역항 */
			function AddComponent() {
			  return (
				// 데이터 전달 값
				<SecoundComponent name="이름" nickname="mssccs" />
			  )
			}
			export default AddComponent
			```
		- 자식 컴포넌트
			```jsx
			import React from 'react'
			
			/** 자식 컴포넌트 역할 */
			function SecoundComponent({name, nickname}) {
			  const jsxStyle = {
				fontSize : 24,
				fontWeight : 600,
			  };
			  return (
				<div style={jsxStyle}>
					부모 컴포넌트에서 전달받은 이름 : {name} <br/>
					부모 컴포넌트에서 전달받은 별명 : {nickname} <br/>
					<hr/>
					<p style={{color : "blue"}}>
					  {name} : {nickname}
					</p>
				</div>
			  )
			}
			export default SecoundComponent
			```
	- #### default Props가 존재
		```jsx
		function Read({logo, gnb}) {
			return (
				<>
					{logo}와 {gnb}가 함께 출력됨
				</>
			);
		}
		Read.defaultProps = {
			logo : "로고",
			gnb : "gnb 메뉴",
		}
		```
		- 초기값 설정해주는 거라고 생각하면 됨

