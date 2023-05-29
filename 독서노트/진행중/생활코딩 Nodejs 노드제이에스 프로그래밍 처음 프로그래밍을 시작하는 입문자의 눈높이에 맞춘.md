
---
created: 2023-05-28 21:57
tag: 독서 국내도서 IT모바일 프로그래밍언어 프로그래밍교육
title: 생활코딩! Node.js 노드제이에스 프로그래밍：처음 프로그래밍을 시작하는 입문자의 눈높이에 맞춘
author: 이고잉
category: 국내도서
total_page: 624
publish_date: 2021-03-30
cover_url: http://image.yes24.com/goods/98550824/XL
status: 완료
start_read_date: 2023-05-28
finish_read_date: 2023-05-28
my_rate: 0
book_note: ""
---


# 개요
[[Node.JS]]를 이용해 웹 서버를 개발하거나 [[electron]]과 함께 사용해서 데스크톱 앱을 개발할 수 있다. 
- main.js를 수정하면 서버를 재실행해야하지만 html 파일등은 새로고침할 때마다 파일을 새로 불러오므로 내용이 반영됨


# [[Node.JS]]로 웹 서버 켜기
```js
var http = require('http');
var fs = require('fs');
var app = http.createServer(function(request, response){ 
	var url = request.url;
	if(request.url == '/'){
		url = '/index.html';
	}
	if(request.url == '/favicon.ico'){
		return response.writeHead(404);
	}
	response.writeHead(200);
	console.log(__dirname + url);
	response.end(fs.readFileSync(__dirname + url));
});
app.listen(3000); //웹 서버가 요청을 받는 통로, 즉 포트번호를 의미함
```
- `node 해당js파일명.js`을 통해서 실행하며 종료하려면 `ctrl + c`를 콘솔창에서 하면 됨
- `http://localhost:3000`을 통해 웹서버에 접속하면 내가 코딩한 [[HTML]] 문서가 출려됨
- 이 코드에서 `request.url`은 <mark class="hltr-purple">사용자가 요청한 URL</mark>이다. 해당 url에서 쿼리스트링을 추출할 수 있다. 
- `request.writeHead()`메소드는 HTTP 상태코드를 반환하는 메소드이다. 보통 2백대면 정상적인 응답을 말하고, 404는 경로를 찾지 못했다는 응답코드이다. 

# URL에 따라서 사용자에게 표시되는 내용을 다르게 출력하기
## URL 이해하기
```
프로토콜 :// 호스트(도메인 네임):포트번호/경로?쿼리스트링
http://navaer.com:3000/main?id=name&page=12
```
- **프로토콜** : 서버에 접속할 경우 어떤 방식으로 통신할 것인지를 나타내는 부분으로 [[HTTP]] 규칙에 따름
- **도메인 네임** : 호스트(Host)는 인터넷에 접속된 각각의 컴퓨터를 의미
- **포트번호(Port Number)** : 한대에 컴퓨터 안에 여러대의 서버가 존재할지 모르니까 접속할 경우 포트번호를 명시하면 해당 포트로 연결된 서버와 통신하게 됨
	- 포트번호를 80으로 설정하면 해당 80번 포트는 기본 값이기에 포트번호를 생략해서 접속할 수 있음
- **경로(Path)** : 서버의 어떤 디렉터리에서 파일을 불러올것인지를 의미
- **쿼리스트링(Query String)** : 쿼리스트링을 통해 웹 서버에 데이터를 전달할 수 있음

- [[Node.JS]]에서는 `require`를 통해서 [[Node.JS]]가 만들어 놓은 모듈(module)을 포함할 수 있음
	```js
	var url = require('url');
	```
- 참고로 `response.end()` 메소드에 작성된 내용이 웹화면에 표시되게 된다. 따라서 아래와 같이 코드를 적으면 쿼리스트링으로 받은 내용을 화면에 출력할 수 있다.
	```js
	var url = require('url'); // 모듈추가
	// 생략
	var _url = request.url; // 요청받은 url를 담는 변수
	var queryData = url.parse(_url, true).query;
	response.end(queryData.id);
	```

## 템플릿 리터널 ([[JS]] 문법)을 이용해서 동적으로 데이터 출력가능 
```js
var letter = `Dear ${user} 

Lorem ipsum dolor sit amet, ${user} 
`
```
- 완전 [[JSP]]에 있는 EL 문법같네. 하지만 [[JSP]]의 EL문법과 달리 역따음표(\`)로 묶어서 표현해야함. pre태그를 쓴것처럼 줄바꿈이 되어서 출력됨.


##  파일 읽어오기
```js
var fs = require('fs');
fs.readfile('text.txt', 'utf-8', function(err, data){
	console.log(data);
})
```
- 이 기능을 응용해서  `fs.readFile('data/${queryData.page}'`에 쿼리스트링으로 입력받은 값을 넣음으로써 data 폴더에 있는 파일을 불러와서 페이지를 동적으로 관리가능


# node와 친해지기
- 파일 실행하기
	```
	node 파일경로/js파일명
	```
- 입출력
	```js
	var args = process.argv;
	console.log(args);
	```
	```
	node main.js egoing // 출력될 입력값
	```
- 사용자가 접속한 url 분석
	```js
	console.log(url.parse(_url, true));
	```
	- `url.parse`를 통해서 url 정보를 분석할 수 있음
	- pathname : 사용자가 입력한 경로 이름만 표시(쿼리스트링은 표시 안됨)
	- path : 쿼리스트링이 포함된 URL이 출력됨
- 파일 목록 알아내기
	```js
	var testFolder = './data';
	var fs = require('fs');
	fs.readdir(testFolder, function(err, filelist){
		console.log(fileelist)
	})
	```

# 동기(synchronous)와 비동기(asynchrous) API
- [[Node.JS]]에서는 동기(synchronous) 처리방식과 비동기(asynchrous) 처리방식이 존재한다. 하나의 작업이 끝날 때까지 기다렸다가 다음 작업을 처리하는 방식을 동기 처리방식이라고 하고, 병렬로 동시에 여러가지 일을 처리하는 방식을 비동기 처리방식이라고 한다.
- [[Node.JS]]에서는 함수이름에 =='Sync'==라는 단어가 붙어있으면 동기처리 방식으로 처리하는 함수이다. 

# 콜백(callback)함수란?
- 어떤 실행문을 마치면 내부적으로 자동 호출하는 기능을 말함
	```js
	var fs = require('fs');
	fs.readdir('./data', (err, filelist)=>{
		// 이를 콜백함수라고 함. 또한 이름이 없으므로 익명함수(anonymous function)라고도 함
	})
	```

# 패키지 매니저(Package Mannager)
- 패키지 : 소프트웨어를 일컫는 여러가지 표현 중 하나
- 패키지 매니저 : 패키지를 설치, 업데이트, 삭제하는 등 관리하는 데 도움을 주는 프로그램을 말함
	- **npm** : [[Node.JS]]에서 가장 광범위하게 사용되는 기본 패키지 매니저
	- **pm2** : [[Node.JS]]로 만든 프로세스를 관리해주는 프로그램 , 프로그램을 감시하고 있다가 의도하지 않게 꺼지거나 소스가 변경될 때 자동으로 재시동함으로써 서비스를 안정적으로 유지하게 도움
		```
		// pm2 설치
		npm install pm2 -g // 관리자 권한으로 설치하려면 앞에 sudo를 붙임
		// pm2 실행
		pm2 start main.js // js 파일은 아무거나 ok
		```
		- pm2을 실행시키면 실행시간을 비롯해 CPU나 메모리 등 시스템 자원을 얼마나 소비하고 있는지를 보여줌
		- 프로세스 감시  `pm2 monit`  : 현재 pm2가 감시하는 프로세스 정보를 표시 
		- 프로세스 목록확인 `pm2 list` : 현재 실행 중인 프로세스 목록 확인
		- 프로세스 종료 `pm2 stop 파일이름` : 종료
		- 프로세스 실행 및 감시 `pm2 start main.js --watch` : `--watch`옵션을 통해서 소스파일을 감시할 수 있음
			- 이 기능을 사용하면 [[Node.JS]]를 재시동하지 않아도 변경한 내용이 자동으로 반영되지만 오류메세지가 출력되지 않음 따라서 `pm2 log`명령어를 통해서 오류 메세지를 확인해야 함
   
# [[Node.JS]]로 form 데이터 처리하기 
- **처리페이지에서 전송받은 form 데이터 확인하기** : 크롬 개발자도구에서 Network에서 Headers를 살펴보면 form에서 Post 방식으로 전송한 내용을 확인할 수 있음![[Pasted image 20230529162250.png]]
- **Post로 데이터 받아오기**
	1. 쿼리스트링 모듈을 포함시키기
		```js
		var qs = require('querystring');
		```
	2. `request.on()`으로 전송받은 데이터 받기
		```js
		var body = '';
		request.on('data', function(data){
			body += data;
		});
		request.on('end', function(){
			var post = qs.parse(body);
			var title = post.title;
			var description = post.description;
			console.log(post); // post로 받은 내용이 출력됨
		});
		```
	3. 받은 데이터를 `fs.writeFile()` 메소드로 파일에 작성하기
		```js
		fs.writeFile(`data/${title}`, description 'UTF-8', function(err){
			response.writeHead(200);
			response.end('success');
		});
		```
		- 파일이름을 지정해서 description이라는 변수에 담긴 내용을 작성하고 UTF-8로 파일을 저장함. 파일쓰기를 마쳤을 경우 콜백함수를 호출. <mark class="hltr-purple">이때 파일이 새로 생성됨</mark>
	4. 결과 화면으로 리다이렉트 시키기
		```js
		fs.writeFile(`data/${title}`, description 'UTF-8', function(err){
			response.writeHead(302, {Location:`/?id=${title}`});
			- response.end('success');
		});
		```
		- [[HTTP]] 상태코드 3백번대는 리다이렉션을 의미
			- 301 : 요청한 페이지가 새 위치로 영구적으로 이동
			- 302 : 현재 서버가 다른 위치의 페이지로 요청에 응답하고 있지만 요청자는 향후 요청할 때 원래 위치를 계속 사용해야 함
	- Delete는 `fs.unlink(path, function(err){})`를 이용해 처리
	- Update는 `fs.rename(path, 바꿀 이름, 'UTF-8', function(err){})`를 이용해 처리

# [[JS]] 객체 문법
- 객체 데이터 순회 코드
	```js
	var roles = {
		'programmer':'egoing',
		'title' : 'content'
	};
	for(var name in roles){
		console.log('object : ', name);
	}
	```
- [[Java|자바]]의 객체와 비교하면 별로 다른 점이 없다. 똑같이 멤버변수와 멤버함수로 구성되어있다. [[JS]]에서는 다음과 같이 함수를 객체에 추가 가능
	```js
	var o = {
		// 멤버변수
		v1:'v1',
		v2:'v2',
		// 멤버함수
		f1:function(){
			console.log(this.v1);
		},
		f2:function(){
			console.log(this.v2);
		}
	};
	```
	- this 키워드는 자신이 속한 객체를 가리키는 키워드 

# [[Node.JS]]에서 모듈로 파일 분산하기
- 객체를 외부에서 사용할 수 있게 하는 [[JS]]코드
	```js
	var M = {
		v : 'v',
		f : function(){
			console.log(this.v);
		}
	}
	module.exports = M;
	```
- 모듈화한 파일 포함시키기
	```js
	var part = require('./part.js');
	part.f(); // v를 출력함
	```
- 라이브러리(library)를 만드는 방법 (폴더 이름을 보통 lib라고 함)
	- 

# [[Node.JS]]로 CRUD 하기
> [!info] 책에서는 [[MY SQL]]을 기준으로 설명하고 있음


# Express 프레임워크

# 쿠키와 세션 이용하기

# Passport.js 
```js
npm install -s passport
```



# 다중 사용자 시스템


# 구글 / 페이스북 로그인


