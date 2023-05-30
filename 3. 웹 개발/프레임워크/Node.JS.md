---
tag : 백엔드
aliases : 노드JS
---
# 개요
>[!info]  [[JS]]를 위한 소프트웨어 플랫폼
> - 공부흐름
> 	1. [[JS]] 문법 이해
> 	2. [[Node.JS]]의 기능이해
> 	3. [[Node.JS]] 애플리케이션 개발

>[!cite]- 참고 문서 
> - [NodeJS](https://hanamon.kr/nodejs-%EA%B0%9C%EB%85%90-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0/)
# Node JS 시작하기
- 공식 홈페이지에서 설치
- 환경변수 설정
	- Window 설정 - 시스템 - 정보 - 고급 시스템 설정 - 환경변수로 이동해서 시스템 변수에서 Path를 편집해서 새로만들기 버튼을 누른 뒤 nodejs가 설치된 경로를 입력
- 설치된 버전 조회
	```
	node -v
	npm -v
	npm init -y // 디폴트 값으로 초기화
	```

## 패키지 관리자 설치하기
- npm : [[Node.JS]] 설치와 동시에 기본으로 설치되는 패키지 관리자
- yarn : 따로 설치해야함
	```
	npm install -g yarn 
	yarn --version
	```
	- [[VSC]]에서 권한때문에 작동을 안하는 경우가 있는데 이때 Windows PowerShell을 관리자 권한으로 실행해서 `get-ExecutionPolicy`로 권한이 Restricted이면, `set-ExecutionPolicy RemoteSigned`을 해서 이 권한을 풀어줘야함
	- 전역 사용에 문제가 있으면 path 설정을 해줘야함

## 관련 프레임워크

| ⚡프레임워크                | 설명                                                                            |
| --------------------------- | ------------------------------------------------------------------------------- |
| [[Express.js]] (익스프레스) | 웹 애플리케이션, API 개발을 위해 설계된 Node.js의 사실상의 표준 서버 프레임워크 |
| [[electron]] (일렉트론)     | 웹에서 넘어서 데스크톱 앱을 만들 수 있는 프레임워크<br>좀 무겁다                |
| [[Neutralino.js]]     | [[electron]]에 비해 가벼운 데스크톱 앱을 구축할 수 있는 프레임워크                                                                               |


# 웹 서버 만들기



