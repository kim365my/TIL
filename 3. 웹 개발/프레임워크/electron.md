---
tag : 
aliases : 일렉트론
---

# 개요
>[!info] [electron 소개페이지](https://www.electronjs.org/)
> - JavaScript, HTML 및 CSS와 같은 웹 기술을 사용하여 기본 애플리케이션을 만들기 위한 GUI 프레임워크
> - 백엔드로는 [[Node.JS]] 런타임을, 프론트엔드로는 Chromium을 사용
> 	- electron ↔ node js ↔ 운영체제
> 	- chromium(검색창 없는 크롬) → 유저 인터페이스
> - **개발된 데스크탑 애플리케이션** ![[Pasted image 20221017161321.png]]
> - **특징**
> 	1.  웹 기술 : Chromium 및 [[Node.JS]]를 사용하므로 HTML, CSS 및 [[JS|Java script]]로 앱을 빌드할 수 있음
> 	2.  오픈 소스
> 	3.  크로스 플랫폼 
> - [Electron Dos](https://www.electronjs.org/docs/latest) 

- 디자인 라이브러리
	- [ant-design](https://github.com/ant-design/ant-design)

>[!cite]- 참고 문서
> - [https://www.youtube.com/watch?v=6Ep8ot0ABH0](https://www.youtube.com/watch?v=6Ep8ot0ABH0)
> - [FE개발자의 성장 스토리 11 : Electron, 저도 한번 해보겠습니다.](https://tech.kakao.com/2021/08/17/frontend-growth-11/)


# 시작하기
>[!info] [[VSC]]의 경우 콘솔에서 아래 코드를 입력하면 됨

1. [[Node.JS]] 버전체크 후 초기화
	```
	node -v
	npm -v
	npm init -y // 디폴트 값으로 초기화
	```
2. [[electron]] 프로젝트 생성하기
	```
	npx create-electron-app "app-name"
	```
3. [[electron]] 저장하고 실행하기
	```
	cd "app-name"
	npm install --save-dev electron
	npm start
	```
- 이런 형식으로 폴더가 구성됨
  ![[Pasted image 20230528210257.png|200]]

## electron 빌드도구
1. electron -forge : windows 빌더 지원안함
2. electron -builder : 모든 os 지원
	- 빌더를 내가 진행 중인 프로젝트에 설치해야함 (우선 [[Node.JS#패키지 관리자 설치하기|yarn]] 설치해야함)
		```
		yarn add electron-builder --dev
		```
	- package.json의 스크립트에 실행명령어 추가
		```js
		"scripts": { 
			"dist": "electron-builder", 
			"dist:win": "electron-builder --win"
		}
		```
	- 실행
		```
		yarn dist:win
		```
	- 실행이 완료되면 dist 폴더에 exe 실행파일이 생성되어있는 것을 확인할 수 있음
		- unpacked 파일은 압축 안된거
3. electron -packager


# 용어해설

 |     | 설명 |
 | --- | ---- |
 | [[구조 분해 할당]]    | 사용되는 배열이나 객체의 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 하는 [[JS]] 표현식 (출처 : MDN)      |


# 연관문서