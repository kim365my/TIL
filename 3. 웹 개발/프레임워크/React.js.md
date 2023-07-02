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
	- npm 5버전 이하라면
		```
		npm install -g create-react-app
		npm i -g create-react-app 
		```
		- 경고창이 표시될텐데 무시하고 넘어가면 됨
	- npm 버전이 6이상이라면
		```
		npm init react-app 설치폴더
		```
- 보일러 플레이트
	```
	create-react-app 설치폴더명
	```
- 프로젝트 실행 : `npm start`에서 리액트 아이콘이 뱅글뱅글 돌아가면 성공
- 프로젝트 빌드 : `npm run build`
- 별도의 라이브러리를 설치하고 싶은 경우 `npm install 라이브러리명`으로 작성하면 되고, 특정 버전을 쓰고 싶으면 `@버전번호`를 뒤에 추가
- [i] [[VSC]] 필수 확장 프로그램 설치 : ES7+ React/Redux/React-Native snippets
	- 단축키 : `rce / rfc / rafc / rafce  / rcc`



# 리액트 기본 문법
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
	- **package.json** : 제일 중요한 파일로 각종 라이브러리의 버전 관리를 해주거나 node_modules 폴더가 없어도 package.json이 존재한다면 npm이 이를 확인하고 새로 설치해주므로 잃어버리지 말 것
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
			- 코드 예시
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
			- 코드예시
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
- ### 리액트에서의 데이터 관리 방법
	- **함수형 컴포넌트** : Hooks
		- ### Hooks 
			- 리액트 v16.8에서 도입됨
			- **useState** : 함수형 컴포넌트에서 data의 상태 관리를 할 수 있음
			- **ustEffect** : 랜더링 직후의 작업을 설정
			- 이외에도 많음
	- **클래스형 컴포넌트** : [[#state 사용]]


## JSX 문법
### 개요
- function 내의 return 메소드 내에서 JSX 문법을 사용하게 된다. JSX란 리액트만의 확장문법으로 [[HTML]] 태그를 작성해서 페이지를 반환할 수 있다고 보면 된다.
- [[XML]]의 형식을 따르기 때문에 [[HTML]] 태그에서 원 태그였다고 해도, 모든 태그는 반드시 닫는 태그가 존재해야하며, return 내 반드시 하나의 부모태그가 존재해야 한다.
- 최상위 부모태그를 `<div></div>`가 아닌 `<></>` 빈태그(아니면 Fragment)로 묶어도 된다.
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
- ### `{}` 사용하기
	- `{}`는 [[JSP]]의 EL 문법과 동일하게 [[HTML]] 태그 내에서 
	- 조건문 사용하기 (3항연산자, 물론 if문도 쓸수 있음)
		```jsx
		{(name === "mssam") ? "" : " name이 기본값이 아니네요"}
		{1-1 === 0 && "참인경우만 실행"}
		{1-2 === 0 || "거짓인 경우에만 실행"} 
		```
	- `{}`를 통해서 미리 선언해둔 [[JS]] 변수를 [[HTML]] 태그 내에 삽입할 수 있게 된다.
- ### 스타일 지정방식
	- [[HTML]] 요소에 추가해두기 : 정적파일 폴더에 있는 index.html에 스타일을 추가해두면 됨
	- 변수로 불러와서 추가하기
		```jsx
		import style from './style.css';
		const App = () => {
			return(
				<style />
			)
		};
		```
	- 인라인 방식 : `<h1 style={{cursor: "pointer"}}>` or `<h1 style={style}>`
		- style 안에 객체 형식으로 작성하거나 객체를 선언해 객체명만 작성하는 방식이 존재
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
	<AddComponent/> // 태그형식으로 추가하기
	```

### Props (properties, 매개변수)
- 부모 컴포넌트에서 자식컴포넌트로 데이터를 전달할 때 사용하는 속성으로 자식 컴포넌트를 부모 컴포넌트에서 조작할 때 사용되며 이때, 부모 컴포넌트에 자식컴포넌트가 포함된다. 따라서 부모 컴포넌트로 호출해야 값이 표시된다.
- **코드 예시**
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
- #### 기본 프롭스(defaultProps)
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
	- 클래스에서는 defaultProps를 다음과 같이 멤버변수로 설정할 수 있으며 this를 통해서 해당 멤버변수에 접근이 가능하다.
		```jsx
		import React, { Component } from 'react'
		class PropsClass extends Component {
		  static defaultProps = {
			name : "기본 값 이름",
			nickname : "기본 값 닉네임",
		  }
		  render() {
			const style = {fontSize:24, backgroundColor:"black", color:"#fff"};
			const {name, nickname} = this.props;
			return(
			  <>
				<p style={style}>
				  클래스형 리턴하기
				  {name}
				  {nickname}
				</p>
			  </>
			);
		  }
		}
		export default PropsClass
		```
- #### 슈퍼 컴포넌트(Super Component)
	- map 함수를 이용해 한 컴포넌트를 반복적으로 출력가능하다. 주로 서버나 외부 데이터를 사용할때 쓰이며 map의 특성 때문에 모든 데이터가 출력될 때까지 반복되므로, 동적인 데이터를 개수에 상관없이 쉽게 불러올 수 있다.
	- 슈퍼 컴포넌트 사용 형식 : `{불러온 사용할 데이터(=api, 내부배열, 서버 등등).map(배열아이템 받을 변수명 => (<자식컴포넌트 />))}`
	- 예시 코드
		```jsx
		import React from 'react'
		import Sport from './Sport'
		function SuperComponent() {
			return (
				<div>
					<h1>SuperComponent</h1>
					{sportsLike.map(sport => (<Sport name={sport.name} img={sport.img} />))}
				</div>
			)
		}
		
		export default SuperComponent
		```
		- sportsLike라는 배열을 이용해서 map을 통해 Sport 컴포넌트를 호출하게 되면 sportsLike 배열의 lenght만큼 해당 컴포넌트가 반복적으로 호출되어 출력되는 것을 확인할 수 있다. 
- #### Prop-types 라이브러리
	- 설치 : 기본적으로 react 패키지에 내장되어 있으며 아래 예시처럼 사용하면 된다. 경고문은 개발자 도구에서 Wanring 문구를 통해 확인이 가능하다. 
	- 사용
		```js
		import PropTypes from 'prop-types';
		Sports2.propType = {
			rating : PropTypes.string.isRequired,
			name : PropTypes.string,
			image : PropTypes.string,
		};
		```

### 라우터 사용하기
- SPA의 핵심으로 사용자가 입력한 URL을 통해 컴포넌트를 불러온다. 라우터는 기본적으로 [[HTML]]에서 사용하던 앵커태그와 동일하다고 생각하면 된다. 라우터를 지원하는 라이브러리는 꽤나 많으며 그 중 2가지만 설명해보면 다음과 같다.
- **라이브러리의 종류**
	- React-router-dom
		- HashRouter, Route, Link 등의 컴포넌트를 제공함
		- 설치방법 : `npm i react-router-dom`
	- Hash Router
		- 부모에 `<HashRouter>`를 추가해야함, 특징으로는 URL에 `#` 이 붙음
- **코드 예시**
	- App.js : 아래 Link 태그에서 사용한 경로를 HashRouter로 맵핑해서 사용해야 하며, 만약 React-router-dom 라이브러리의 버전이 6v 이상을 설치했다면 아래처럼 Routes태그로 감싸줘야함
		```js
		import {HashRouter, Route, Routes} from 'react-router-dom';
		const App  = () => {
			return (
				<HashRouter>
				<Routes>
					{/* 해시라우터 규칙 루트로 사용하고 싶은 거에 exact={true}를 해야함 */}
					<Route path="/" exact={true} Component={Home} />
					<Route path="/About" Component={About} />
					<Route path="/Contents" Component={Contents} />
					<Route path="/Navgers" Component={Navgers} />
				</Routes>
				</HashRouter>
			);
		};
		```
	- Home.js : 만약 React-router-dom 라이브러리의 버전이 6v 이상이고 Link 태그 대신 Route를 쓰게 되면 Router라는 태그로 감싸줘야함
		```js
		import React from 'react'
		import { Link } from 'react-router-dom'

		function Home() {
		return (
			<div>Home
				<Link to="/">메인화면</Link>
				<Link to="/About">About</Link>
				<Link to="/Contents">Contents</Link>
			</div>
		)
		}

		export default Home
		```

### 클래스 컴포넌트 사용하기
#### state 사용
- 객체형태의 데이터로 반드시 <mark class="hltr-purple">클래스형 컴포넌트에서만</mark> 사용해야한다. 또한 소문자로 타입핑 해야 한다. 
- 초기값의 설정이 필수
- state 값을 변경할 경우 직접 값에 접근하여 조작하면 안되고 setState() 메소드를 이용해야 한다.
- 코드 예시
	```js
	import React, { Component } from 'react'
	export default class State extends Component {
		// 동적 데이터 영역
		state = {
			count :0,
		}
		// 이벤트 리스너
		add = () => {this.setState({count : (this.state.count) + 1,})};
		dee = () => {this.setState({count : (this.state.count) - 1})};
		render() {
			return (
				<div>State
					<h2>이벤트 연결 동적 데이터 state 활용</h2>
					<p>
						동적 state : {this.state.count}
					</p>
					<button onClick={this.add}>PLUS</button>
					<button onClick={this.dee}>빼기</button>
				</div>
			)
		}
	}
	```
### 생명주기 함수
- 호출하지 않아도 리액트에서 알아서 컴포넌트를 생성하고 소멸시키는 함수를 말한다. 
- 생명주기함수와 관련있는 메소드들은 다음과 같다.
	- `constructor()` : 생성자함수로(생명주기 함수는 아님), 컴포넌트가 실행될 경우 호출되며 컴포넌트를 초기화하는 함수이다. 무조건 render()보다 먼저 실행된다.
	- `render()` 실행 : 클래스형 컴포넌트에서 브라우저에 DOM 그려주는 역할이다.
	- `componentDidMount()` : 컴포넌트가 처음 화면에 그려주는 실행함수
	- `componentDidUpdate()` : 화면이 새로 그려지면 실행되는 함수
	- `componentWillUnmount()` : 컴포넌트가 떠날경우 실행되는 함수
- #### 생성시
	- constructor() -> render() -> componentDidMount() 순으로 실행된다.
- #### 업데이트 시
	- render() -> componentDidUpdate() 순으로 실행된다.
	- 컴포넌트의 속성이나 상태값(state)이 변경되면 실행됨
- #### 소멸시
	- componentWillUnmount() 가 실행되며 컴포넌트는 소멸된다.