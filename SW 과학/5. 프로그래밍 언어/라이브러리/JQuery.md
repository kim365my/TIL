---
tag : 프론트엔드 라이브러리
aliases : 제이쿼리
---

# 개요
- 💡 **왜 사용하는가?**
	- 멀티브라우져 지원, 이벤트+애니메이션+복잡한 CSS 변환+AJAX의 기능 모두를 다양하게 사용할 때, 그리고 위의 기능들을 구현할만한 시간적 여유가 없고 jquery에 대해서 이미 알고 있을 때. 그리고 무엇보다도 페이지가 퍼포먼스를 크게 요구하지 않고 사용자와의 인터렉션이 많지 않을 때 사용
	- 장점
		- 멀티브라우저 지원
		- 간단한 이벤트 설정, DOM 탐색
	- 단점
		- jquery API를 별도로 공부
		- 퍼포먼스(32k 용량)의 문제 
		- 가상 DOM의 등장
- 서드파티 플로그인 연결
	- 반드시 코어 제이쿼리 밑에 추가해야함 : [jQuery UI - 공식위키](https://jqueryui.com/)
	- 파일확장자에서 이런식으로 min이 있는 건 들여쓰기 없는거
>[!cite]- 참고 문서  
	 -  [[자바스크립트] 왜 jquery를 사용하는가?](https://unikys.tistory.com/300)
	 - https://www.samsungsds.com/kr/insights/jquery.html

# 코어 제이쿼리
- 코어 제이쿼리
	-   문자열로 작성해야 함
	-   바꿀 속성이 2개 이상일 경우, 객체 형식(`{}`)으로 작성 단위를 작성할때 문자열없이 작성하면 브라우저가 자동으로 px로 인식
	-   콜론(`:`)으로 해당 속성을 가지고 있는 요소를 선택
	-   dom은 화면에 보여지는 거고 스크롤이나 기타등등 화면 밖은 윈도우

## HTML과 연결
-   HTML과 연결
    ```html
    <!-- 1. 제이쿼리 코어파일 -->
    <script src="./js/jquery-1.12.4.min.js"></script>
    <script src="./js/jquery-3.3.1.min.js"></script>
    <script src="./js/jquery-3.4.1.min.js"></script>
    <!-- 2. 제이쿼리 cdn방식 -->
    <script src="<http://code.jquery.com/jquery-1.12.4.min.js>"></script>
    <script src="<http://code.jquery.com/jquery-3.3.1.min.js>"></script>
    ```
-   기본 틀
    ```jsx
    $(document).ready(function(){})
    ```
	- window.onload와 동일하게 메모리에 먼저 올리고 HTML을 읽음 같이 사용은 못하더라 
	- $()에 익명함수를 넣으면 ready 축약가능

## 코어 제이쿼리 문법
- $() 
	- dom 객체 선택
		- 요소 선택자, 변수할당하지 않고 사용해도 됨 
		- CSS에서 사용하는 선택자를 쓰면 됨
	- 태그 생성가능
		- 매개 변수로 사용, html 요소를 문자열로 작성시 dom 객체 생성가능 
		- ex) `$("<h1>태그명</h1>") / $("태그명").appendTo("추가할 위치")`
	- ready 메소드를 이용해 HTML을 다 읽은 다음에 코드 실행할 수도 있음
- .css() : 스타일 변경
- .height() / .widht() : 가로세로 값
- event : 이벤트의 정보가 담기는 특별한 매개변수, e로 줄여서 사용하기도 함

### 요소 선택
- .children() : 자식선택
- .parent() : 부모선택
- .siblings() : 형제선택
- .next() : 다음 형제 선택
- .filter() : 필터를 이용
- .eq(number) 多 : 요소들의 인덱스 번호(0부터 시작)을 이용하여 선택 -1이면 last를 쓴것과 같음
- .first(), .last() : 요소의 맨 처음과 맨 마지막을 선택
- .find(string) : 선택된 dom 객체에서 **후손**문서 객체를 선택
- .is(string) : 해당 자식의 존재유무를 논리값으로 반환
- .hasClass(string) : 해당 클래스를 가지고 있는지 논리값으로 반환

### DOM 객체 추가
- .attr() : js에서의 어트리뷰트 같은거 속성값을 확인하거나 속성값을 추가 매개변수가 2개일 경우 값을 변경하는 것(속성명:속성값)
- .html() : 선택 Dom 객체의 첫번째 요소 문자열만 반환 인자값 작성시 해당 요소에 추가 / html 태그 인식 ⭕
- .text() : 선택 Dom 객체의 모든 문자열을 묶어서 반환 인자값 작성시 해당 요소에 추가 / html 태그 인식 ❌
	- ex)  `$(”추가할 요소명”).text(”텍스트”)`
- .appendTo() : 매개변수의 맨 마지막 자식요소로 태그 생성 
	- ex ) `$("<h6>이벤트</h6>").appendTo("body");`
- .remove() : 선택 Dom 객체 제거 = 매개 변수 없음 = 태그 자체를 삭제
- .empty() : 자식노드 제거(텍스트 노드도 삭제)

### 이벤트 추가
- .on() : `addEventListner(”click”, funtion(){})`과 동일
- .click() : 클릭했을 때, 이벤트 발생 단일 이벤트 방식과 동일
- .stop() : 과한클릭방지용, 현재 실행중인 효과가 진행중이면 클릭무시 효과 메서드 사용하기 전에 씀
- 요소 효과
	- .show() : 요소를 보임
	- .hide() : 요소를 숨김
	- .toggle() : 위 두기능을 합침
	- .slideDown() : 요소를 아래로 미끄러지듯 밀어내리면서 표시
	- .slideUp() : 요소를 위로 미끄러지듯 밀어올리면서 숨김
	- .slideToggle() : 위 두기능을 합침
	- .fadeIn() : 요소를 천천히 나타나게 함
	- .fadeOut() : 요소를 천천히 사라지게 함
	- .fadeToggle() : 위 두기능을 합침
- .animate{속성명 : 속성값(숫자)}, 시간, 속도, 콜백함수) : 애니메이션 효과 
	- 속성 : 객체로 반드시 매개변수 값으로 입력 
	- 시간 : 'slow' 'normal' 'fast' 
	- 속도 : swing(기본값), linear(동일속도) 
	- 콜백함수 : 해당 메서드가 실행이 된 이후 호출하여 사용하는 함수 
	- 코어 제이쿼리에서는 숫자로 사용되는 속성들만 사용가능
- .delay() : 밀리세컨드 이후 애니메이션 실행

### 제이쿼리 이벤트 등록방식
1.  단일 이벤트 형식 : 한번에 한 이벤트
	-   효과메서드는 모두 시간을 매개변수로 가지고 있음
	-   시간 : {fast 200, 'normal' 400, 'slow' 500} 밀리세컨으로 입력가능
	-   인자를 입력하지 않으면 normal
	```jsx
	$("h5").click(function(){
		alert("h5 클릭")
	})
	```
2.  one 이벤트 : 딱 한번만 이벤트 발생
	```jsx
	$("h5").one("click", function(){
		alert("이벤트 실행");
	})
	```
3.  on 이벤트
	- 하나의 이벤트를 등록하는 방식
	```jsx
	$("h5").on("click", function(){
		console.log("내용");
	})
	```
	- on() 메서드는 객체로 여러개 이벤트 등록 가능
	```jsx 
	$("h5").on({mouseenter:function(){
	  console.log("마우스 인");
	}, mouseleave:function(){
	  console.log("마우스 아웃");
	}})
	```
4.  hover 이벤트 (mouseenter+mouseleave)
	```jsx
	$("h5").hover(function(){
		console.log("mouseenter");
	}, function(){
		console.log("mouseleave");
	})
	```


### 이벤트 종류
- 마우스
	- click : 클릭
	- mouseenter : 요소위에 마우스 / css 패딩 인식
	- mouseleave : 떠나기 / css 패딩 인식
	- mouseover : css 패딩 X
	- mouseout : css 패딩 X
- 스크롤 이벤트
	- scroll
	- .scrollTop() : 세로 스크롤
	- .scrollLeft() : 가로 스크롤

## 코드 예시
### 비디오 제어 
```jsx
var video = $("video");
    var btn = $(".mov button");
    btn.children().eq(1).css({display:"none"});
    btn.click(function(){
        if (video.get(0).paused) {
            video.get(0).play();
            btn.children().eq(0).css({display:"none"});
            btn.children().eq(1).css({display:"block"});
        } else {
            video.get(0).pause();
            btn.children().eq(1).css({display:"none"});
            btn.children().eq(0).css({display:"block"});
        }        
    })
```

```jsx
// 제이쿼리
var videoBtn = $("figure button");

videoBtn.eq(0).on("click", ()=>{
    console.log("play");
    $("video").get(0).play();
})
videoBtn.eq(1).on("click", ()=>{
    console.log("pause");
    $("video").get(0).pause();
})
videoBtn.eq(2).on("click", ()=>{
    console.log("stop");
    $("video").get(0).load();    
    $("video").get(0).pause();
})

videoBtn.eq(3).children().eq(1).css({display:"none"});
videoBtn.eq(3).on("click", ()=>{
    console.log("sound");
    if ($("video").prop('muted')) {
        $("video").prop('muted', false);
        videoBtn.eq(3).children().eq(0).css({display:"none"});
        videoBtn.eq(3).children().eq(1).css({display:"block"});
    } else {
        $("video").prop('muted', true);
        videoBtn.eq(3).children().eq(0).css({display:"block"});
        videoBtn.eq(3).children().eq(1).css({display:"none"});
    }
})
```

# 플러그인
- [스크롤 플러그인](https://github.com/flesler/jquery.scrollTo)
- [UI 플러그인](https://jqueryui.com/effect/)
- [슬라이더 플러그인](https://bxslider.com/)
	```html
	<html>
	<head>
	  <link rel="stylesheet" href="<https://cdn.jsdelivr.net/bxslider/4.2.12/jquery.bxslider.css>">
	  <script src="<https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js>"></script>
	  <script src="<https://cdn.jsdelivr.net/bxslider/4.2.12/jquery.bxslider.min.js>"></script>
	
	  <script>
	    $(document).ready(function(){
	      $('.slider').bxSlider();
	    });
	  </script>
	</head>
	<body>
	  <div class="slider">
	    <div>I am a slide.</div>
	    <div>I am another slide.</div>
	  </div>
	</body>
	</html>
	```
- [swiper 플러그인](https://swiperjs.com/swiper-api)
	```html
	<!-- 스와이퍼 최상위 구조 클래스 -->
	<div class="swiper-container">
	    <!-- 스와이퍼 휠 content 부모 클래스 -->
	    <div class="swiper-wraper">
	        <!-- 스와이퍼 휠 slider 각각 내용들 -->
	        <div class="swiper-slide">
	            <!-- 이 안에서 자유롭게 작성 -->
	        </div>
	    </div>
	</div>
	```