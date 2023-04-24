---
tag : 마크업_언어 프론트엔드
aliases : Hypertext Markup Language, 하이퍼텍스트 마크업 언어
---
# 개요
- [표준 HTML위키](https://html.spec.whatwg.org/multipage/)
- 박스 모델 레이아웃이 HTML의 핵심
- XML에서 발전한 형태
- CSS과 연결시 주의점
	- 단일 태그 : 가상 선택자를 사용하지 못함
		- 가상 클래스는 dom 요소가 아니기에 스크립트로 선택할 수 없음
			- 가상 클래스는 해당 태그 객체의 속성으로 편입됨
			- 따라서 after()나 before()를 이용해 js로 가상선택자에 접근은 되도 권장하지는 않음
			- 가상 dom과 dom의 차이는 리액트 내용이기에 css의 가상클래스와 연관이 전혀 없음 
	- 인라인 태그 : 너비/높이 조절 못함


# HTML 사용이유와 기초
## 왜 HTML을 쓰는가?
|      | 설명                                                                        |
| ---- |:--------------------------------------------------------------------------- |
| 특징 | W3C에 의한 웹문서의 표준                                                    |
| 장점 | • 수정/관리 용이 및 독립적(컴퓨터 시스템에 종속 ❌)  <br> • 파일의 용량이 작아 클라이언트-서버 간의 빠른 문서 전달 가능               |
| 단점 | • 웹 문서의 내용(디자인)표현에 집중되어 문서 내용의 의미 정보를 표현의 한계 <br> • 정보의 구조화 및 데이터 간의 연관성 표현의 어려워 검색이 어려움 <br> • 사용 가능한 태그의 제한 (융통성 및 확장성의 결여) <br> • 내용이 구조화되지 않아 문서의 정확성\유효성 검증과 제약조건 정의의 어려움 |
| 역사 | 1991. 팀 버너스-리 개발 -> 2014. HTML5                                      |

## 기초 HTML
### HTML의 기본 구조 
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!-- 주석문 -->
</body>
</html>
```
- <!DOCTYPE html> : 문자 형식을 알려주는 지시어
- HTML은 크게 head와 body로 구성되어있음
	- head는 메타태그를 이용해 문서의 내용을 규정
	- body는 실제로 화면에 표시되는 내용을 보여줌 
- HTML은 요소로 이루어져 있음
  ![[Pasted image 20230423162855.png|400]]
- 특수문자를 사용하기 위해서는 

### 태그의 구조
|                | 설명                                                      |
| -------------- | --------------------------------------------------------- |
| 시작/종료태그  | <></> ex) `<body></body>` <br>• 꺽쇠가 없으면 모두 문자열로 인식함 <br>• 태그는 얼마든지 중첩가능                               |
| 자체 닫기 태그 | ex) `<br>`                                                |
| 속성           | • 지역속성 : 개별 요소에 영향을 끼침 ex) `style` 등  <br> • 전역속성 : 모든 문서에 영향을 끼침 ex) `class, id, title`           |
| 태그 작성 주의점  | • 태그는 대소문자를 구분 ❌ → 하지만 소문자 표기를 권고 <br> • 두칸 이상 연속된 공백은 하나의 공백으로 처리 <br> • 요소 안에 다른 요소를 포함할 수 있음  |


## 클래스와 아이디
```html
<div id="wrap"> <!--더 못씀-->
	 <p class="roboto red">roboto</p> <!--띄어쓰기하고 더 작성가능-->
</div>
```

-   아이디 : 한 태그에 딱 한번밖에 못씀(고유의 값)
-   클래스 : 한 태그에 여러 아이디를 작성할 수 있음
    -   클래스를 통해서 스타일을 모듈화시켜서 적용
    -   세이프티존이나 보통 여러항목에 공통적으로 적용시켜야하는것
-   [[코드 컨벤션]]같은 꼭 지켜야할 건 아니지만 라벨링을 잘해야함.

## 박스모델

## 블록요소와 인라인요소
|     | 블록요소                                                       | 인라인요소 |
| --- | -------------------------------------------------------------- | ---------- |
|     | 문서구조요소                                                   | 텍스트요소 |
|     | 항상 새로운 줄에서 시작해서 하나의 줄은 전부 차지해서 내용표시 |  입력하는 내용만큼의 공간을 차지해서 내용 표시          |
| 줄바꿈 | 자동으로 줄바꿈 수행                                           |   줄바꿈 안됨         |
| 예시 |  div, p, h1 등               | span, img, strong 등           |

## 물리적 스타일과 논리적 스타일
- 

# HTML 요소종류
## head 요소
### meta 요소
```html
<meta charset="UTF-8">
<meta name="keywords" content="쇼핑몰, 악세서리">
<meta name="description" content="사이트의 상세정보 설명하는 영어">
```
- charset을 유니코드로 인코딩을 맞춰주어야 함
- [[seo]] 최적화를 위해서 head의 meta 태그에 여러 정보를 기입함

### base 요소
```html
<base href="">
```
- body 요소 내의 상대 경로로 표시된 URL을 절대 경로로 취급

### link 요소
```html
<link rel="" href="">
```
- 외부 스타일(CDN 등)이나 파비콘을 적용할 수 있음 
	-   파비콘 (favorite icon | shortcut icon) 코드 : 주소창에 나타나는 아이콘 / 모바일에 북마크시 나타나는 아이콘
	    ```html
	    <link rel="shortcut icon" href="./img/icon_32x32.png">
	    <link rel="apple-touch-icon" href="./img/icon_180x180.png">
	    <link rel="apple-touch-icon=precomposed" href="./img/icon_180x180.png">
	    ```


## a 요소
```html
<a href=""></a>
```
- 속성
	- href  : 이동할 링크 주소 
		-  id값을 작성해서 해당 페이지의 특정 위치로 이동가능 ex) `#id값`, `다른페이지#id값` 
		- href 속성을 이용하여 다양한 링크 지정 가능
			- 이메일 → href=“mailto:이메일주소” 
			- 자바스크립트 코드 → href=“javascript:코드”
			- 음악/동영상 파일 재생 → href=“파일명”
			- 파일 다운로드 → href=“압축/실행 파일명”|
		-  target  
			- \_blank : 새창 또는 새탭에서 열기
			- \_self : 새창, 기본값 현재 프레임 영역에 결과가 나타남
			-  \_parent : 부모 프레임 영역에 결과가 표시됨
			-  \_top :  무조건 현재 창의 전체 화면 영역에 결과가 나타남
			- 프레임명 : 해당 '프레임명'에 해당하는 프레임 영역에 결과가 나타남
	- download : 파일 다운로드 



## 리스트 요소
|     | 설명                          | 속성                                                                                                                        |
| --- | ----------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| ol  | 순서 있는 목록                | • `type` : 숫자, 영문, 로마자로 자유롭게 변경가능<br> • `start` : 시작 번호를 지정 가능 <br>• `reversed` : 역순 |
| ul  | 순서 없는 목록                |                                                                                                                             |
| li  | ol과 ul의 자식태그            |  • value : 항목번호 변경(ol의 경우에만 사용)                                                                                                                           |
| dl  | 정의형 목록                   |                                                                                                                             |
| dt  | dl에서의 제목태그, 자동줄바꿈 |                                                                                                                             |
| dd    | dt에 대한 설명. 자동 줄바꿈. 들여쓰기됨                                                                                                                        |


## 이미지 요소
- 프론트엔드를 최적화하기 위해서는 이미지의 용량을 고려해야 함 
- 이미지 최적화를 위해서 picture 요소를 사용하거나 img 요소에 lazy를 추가해서 로딩 속도를 늦춤
- 지원하는 이미지 파일![[웹 개발론#이미지: jpg, png, gif, svg]]

### img 요소
```html
<img src="" alt="">
```
- 단일 태그
- 속성
	- src  :  문서에 표시할 이미지 파일의 경로/이름 #필수속성   
	- width / height  : px 등 단위를 안쓰면 이미지 원본 크기로 표시됨 
	- alt  : 대체 텍스트. 웹 접근성을 위해서 꼭 써줘야함 
	- usemap : 클라이언트 측의 이미지맵, map의 name과 연동 (#맵이름)

###  이미지맵 
```html
<img src="" alt="" usemap="#map">
<map name="map">
    <area 
        shape="이미지맵에서 각 영역의 모양(default-기본, rect-사각형, circle-원, poly-다각형)" 
        coords="각 영역을 구성하는 좌표값" 
        href="URL" 
        target="링크된 내용이 열릴창"
				title="마우스 호버시 내용이 보여짐"
        download="href로 지정된 파일을 다운로드"
        alt="대체 텍스트 내용">
</map>
```
- 하나의 이미지에 대해 여러 영역으로 나누어 링크 지정 
- map 요소 안에서 필요한 영역의 개수만큼 area 요소로 각 영역 지정
- 하나의 이미지에 여러 개의 링크를 걸어 클릭 위치에 따라 서로 다른 링크가 열리는 기능
>[!cite]- 참고 문서
> - [img map](https://hsunnystory.tistory.com/44?category=793287)

### picture 요소
```html
<picture>
	<img src="" alt="">
	<source src="" type="">
</picture>
```
- [[웹 개발론#이미지 최적화|이미지 최적화]]를 위해서 사용되는 태그

## 멀티미디어 요소
### figure
```html
<figure>
	<figcaption>제목</figcaption>
</figure>
```
- 시맨틱 태그
- 내용에 대한 이해를 돕기위해 사진, 다이어그램, 코드등의 멀티미디어를 포함할때 사용함 • `figcaption` : 제목을 쓸때 사용, 중앙정렬안됨


### audio
```html
<audio>
	<souce src="경로" type="video/mp4">
</audio>
```
- 오디오 요소

### video
```html
<video muted autoplay loop>
	<souce src="경로" type="video/mp4">
</video>
```
- src에 넣으면 하나밖에 못써서 주로 souce 태그와 함께 사용됨
- 속성 
	-  muted : 음소거
	- autoplay : 자동재생
	- controls : 영상의 제어 기능 
	- poster : 영상이 끊기거나 재생이 안될때 섬네일

## iframe 
```html
<iframe src="" name="" srcdoc=""></iframe>
```
- 현재 웹 페이지 안에 새로운 창 삽입 웹 페이지나 동영상 등을 보여주는 프레임
- a태그의 target 속성을 통해 iframe과 연결하면 해당 a의 링크가 iftame에 표시됨
	```html
	<a href="" target="frameBox">링크 이름</a>
	<iframe src="" name="frameBox"></iframe>
	```
- [[JS]] 함수 중 새로운 윈도우 창을 띄우는 window.open(url, name, spes, replace)를 사용가능 
- 속성
	- name : 창이름
	- src : 창에 표시할 URL
	- srcdoc : 창에 보여줄 콘텐츠
	- width / height


## 테이블 요소
```html
<table>
	<caption>테이블의 제목</caption>
	<colgroup>
		<col class="제목1">
		<col class="제목2">
	</colgroup>
	<thead>
		<th>
			<td colspan="2">thead</td>
		</th>
	</thead>
	<tbody>
		<tr>
			<td rowspan="2"></td>
			<td>tbody 영역</td>
		</tr>
	</tbody>
	<tfoot>
		<tr>
			<td>tfoot 영역</td>
		</tr>
	</tfoot>
</table>
```
- colgroup 요소를 통해서 한 행에 클래스를 줄 수 있음
- [[CSS]]에 적용은 주로 td에 함
- 테이블 시맨틱 태그 : thead, tbody, tfoot
- 속성
	- rowspan / colspan : 행이나 열을 병합하는 속성, td에서 사용



## Form 요소
```html
<form action="" method="">
    <fieldset>
        <legend>form 제목</legend>
        <!--이하 form 내용 작성-->
        <label for=""></label>
        <input type="" id="" name="" value="">
    </fieldset>
</form>
```
### 서버와 사용하기
- HTML에서 서버 쪽으로 데이터를 넘겨줄 수 있는 유일한 방법 (무조건 **문자열**)
	- form 태그 안에 있는 input 태그 name을 키로 getAttruebute 함
	- type을 hidden으로 값을 숨겨진 키도 넘어감
	- 한번에 여러개의 데이터를 묶어서 제출버튼을 클릭시 배열로 전송됨 ex) 체크박스 등
	- 제출(submit) 버튼을 누르면 데이터가 전송됨 (form 내에 한개만)
- 웹 접근성
	- label과 input(or select, datalist)을 사용할때 for과 id로 연결해둠
	- input에서 유효성 검사가능
- form태그의 속성
	- `action` 속성 : 데이터를 처리할 곳을 지정
		- action에서 서블릿의 매핑된 이름을 작성하면 HTML과 서블릿이 연결됨
	- `method` 속성 : get/post 데이터 방식 결정, 기본값은 get
		- 서블릿의 doGet/doPost 중 어떤 것을 선택할 것인지에 대한 차이
	- `navalidate` : 데이터의 유효성검사 비활성화 

## Input 요소
```html
<input type="" id="" name="" value="">
```

### input 요소 속성
| 속성                     | 설명                                                                                                                                                                                                                                   |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type                     | input 태그의 유형을 지정가능                                                                                                                                                                                                           |
| id                       | label 태그의 for에 id 값을 넣어서 연결할 수 있음                                                                                                                                                                                       |
| name                     | 텍스트 필드를 구별할 수 있는 이름으로 서버에 넘어갈 때 해당 이름으로 값을 불러옴                                                                                                                                                       |
| size                     | 텍스트 필드의 길이를 지정. 즉 ==화면에 몇 글자가 보이도록 할 것인지==를 지정<br>예를 들어 최대 입력 가능한 글자 수가 10개 인데 size를   5로 지정하면 텍스트 필드 크기가 5개 글자 크기에 맞추어져 나머지 5개 글자는 화면에 보이지 않음. |
| value                    | 텍스트 필드 요소가 화면에 표시될 때 텍스트 필드 부분에 표시될 내용. 이 속성을 사용하지 않으면 빈 텍스트 필드가 표시됨.                                                                                                                 |
| maxlength(<-> minlength) | 텍스트 필드에 입력할 수 있는 최대(<->최소) 문자 개수를 지정                                                                                                                                                                            |
| autofocus                | 자동으로 해당 입력칸 포커스를 맞춰줌(다른 인풋에 동시에 넣으면 작동안함)                                                                                                                                                               |
| autocomplete       |  자동완성기능/ 기본 속성값이 on이므로 꺼두고 싶으면 off로 할 것                                                                                                                                                                                                  |
| placeholder              | 사용자에게 input 안에 뭘 작성해야 하는지 알려줌                                                                                                                                                                                        |
| required                 | 필수 작성 요소를 지정해줌, 유효성 검사할때 유용                                                                                                                                                                                        |
| readonly                 | 읽기 전용으로 수정 안됨 <br> 데이터를 반드시 보내야 한다고 할때 사용 / 꼭 쓸일은 없음                                                                                                                                                  |
| disabled                 | input 요소 비활성화, 조건이 충족하지 않으면 사용자가 쓸 수도 없고 클릭도 안됨. 또한 서버로 제출도 안됨                                                                                                                                 |


### type 속성의 유형
| 유형           | 설명                                                                                  |
|:-------------- |:------------------------------------------------------------------------------------- |
| hidden         | 사용자에게는 보이지 않지만 서버로 넘겨지는 값을 가짐 #서버                            |
| text           | 한 줄짜리 텍스트를 입력할 수 있는 텍스트 상자                                         |
| search         | 검색 상자                                                                             |
| tel            | 전화번호 입력 필드                                                                    |
| url            | URL 주소를 입력할 수 있는 필드                                                        |
| email          | 메일 주소를 입력할 수 있는 필드                                                       |
| password       | 비밀번호를 입력할 수 있는 필드                                                        |
| datetime       | 국제 표준시(UTC)로 설정된 날짜와 시간(연, 월, 일, 시, 분, 초, 분할 초)                |
| datetime-local | 사용자가 있는 지역을 기준으로 날짜와 시간(연, 월, 일, 시, 분, 초, 분할 초)            |
| date           | 사용자 지역을 기준으로 날짜(연, 월, 일)                                               |
| month          | 사용자 지역을 기준으로 날짜(연, 월)                                                   |
| week           | 사용자 지역을 기준으로 날짜(연, 주)                                                   |
| time           | 사용자 지역을 기준으로 시간(시, 분, 초, 분할 초)                                      |
| number         | 숫자를 조절할 수 있는 화살표                                                          |
| range          | 숫자를 조절할 수 있는 슬라이드 막대                                                   |
| color          | 색상 표                                                                               |
| checkbox       | 주어진 항목에서 2개 이상 선택 가능한 체크박스                                         |
| radio          | 주어진 항목에서 1개만 선택할 수 있는 라디오 버튼                                      |
| file           | 파일을 첨부할 수 있는 버튼                                                            |
| submit         | 서버 전송 버튼                                                                        |
| image          | submit 버튼 대신 사용할 이미지                                                        |
| reset          | 리셋 버튼                                                                             |
| button         | 버튼                                                                                  |

### select 요소
```html
<select name="" id="">
	<optgroup>
		<option value="옵션1">옵션1</option>
		<option value="옵션">옵션2</option>
	</optgroup>
</select>
```
- 데이터를 선택할 수 있게해주는 바를 생성하고 `option`태그의 내용을 데이터로 사용함
### datalist 요소
```html
<input type="text" id="intrest" list="choice">
<datalist id="choice">
	<!-- id값과 위의 list 값을 맞춘다. -->
	<!-- 레이블에 설명 2개 쓸수있음 -->
	<!-- 한번 선택시 수정이 안됨 -->
	<option value="html" label="문법"></option>
	<option value="css" label="어휘"></option>
	<option value="js" label="회화"></option>
</datalist>
```
- 데이터 목록에 제시한 값 중에서 선택하면 자동으로 텍스트 필드에 입력
- id값과 input 요소의 list 속성명을 맞춰줘야 연결됨


## 컨테이너 요소
### div요소
```html
<div></div>
```
- 블록요소로 요소를 감싸는 컨테이너로 사용됨
- 너무 남발하지 말 것

### span 요소
```html
<span></span>
```
- 인라인 요소로 요소를 감싸는 컨테이너로 사용됨


## dialog 요소
- dialog 태그를 이용하면 쉽게 모달을 구현가능
- HTML, form mthod는 dialog로 설정 필요
```html
<button id="diaglogBtn">클릭</button>
<dialog>
	<!--실제 모달에 표시되는 내용-->
	
	<!--모달 닫는 버튼, 별다른 js를 사용안해도 닫는 버튼 구현가능-->
    <form method="dialog">
        <button value="close">close</button>
        <button value="confirm">confirm</button>
    </form>
</dialog>
```
- js에서는 showModal 메소드로 모달을 표시되게 할 수 있음
	```js
	const diaglogBtn = document.querySelector("#diaglogBtn");
	const diaglog = document.querySelector("dialog");
	// 모달 표시
	diaglogBtn.addEventListener("click", ()=>{
	    diaglog.showModal();
	})
	// 모달 버튼이 전송하는 내용을 받을 수 있음
	diaglog.addEventListener("close", ()=>{
	    console.log(diaglog.returnValue);
	})
	```
- css의 ::backdrop을 이용해서 백그라운드 색상을 진하게 할 수 있음
	```css
	dialog{
	    width: 90%;
	    border: 1px solid rgba(0, 0, 0, 0.1);
	    border-radius: 20px;
	    box-shadow: 0 0 10px 0 rgba(255,255,255,1);
	    text-align: center;
	}
	dialog::backdrop{
	    background-color: rgba(0, 0, 0, 0.8);
	}
	```


# 시멘틱 태그
- HTML 문서에 의미 부여가 가능
	- 검색엔진, 문서 해석기 등에 의한 자동적인 문서 해석이 가능하도록 ) [[seo]]

## 시맨틱 태그 요소
- 문서 구조화를 위한 요소
	- header : 머리말을 나타내는 요소
	- nav : 메뉴 영역을 나타내는 요소
	- main : body에 해당하는 태그
		- 주로 SNB와 본문 컨텐츠가 들어감
		- section, article 를 자식태그로 주로 씀
	- section : 제목 \ 주제별로 나눌 수 있는 문서의 내용영역을 구성하는 요소
	- article : 개별 콘텐츠를 나타내는 요소, 독립적인 요소
	- aside : 좌우측의 보조 콘텐츠 영역을 나타내는 요소
	- footer : 꼬릿말을 나타내는 요소
- 시맨틱 블록 요소
	- figure
- 시맨틱 인라인 요소
	- 

# HTML 전역속성
>[!cite]- 참고 문서
> - [Global attributes - HTML: HyperText Markup Language | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes)


# 그 외
## 에멧 단축키 
- ! 를 작성 HTML 기본 구조가 자동으로 써짐, 그외에도 다른 기능 많음

## 특수문자 표현 (entity code, entity name)
- 특수문자(’<’,’>’등) HTML에서 사용되고 있는 예약어는 그대로 출력이 안됨
- entity code or entity name을 사용해야 함
	- [Entity Code - A Clear and Quick Reference to HTML Entities Codes](https://entitycode.com/)
- 엔터티는 예약된 문자를 구현하거나 키보드로 쉽게 입력할 수 없는 문자를 표현하는 데 사용   
    - 아스키 코드나 유니코드와 비슷하게 국가별로 여러가지 버전이 존재
    - 더 알아보고 싶다면 → [컴퓨터 데이터의 표현](https://www.notion.so/7ac659862cf34af69b082828c86923cd)
- 자주 쓰는 특수문자
	- 공백 : &nspb;

## CDN 링크 모음
-   부트스트랩 CDN
    ```html
    <link rel="stylesheet" href="<https://maxcdn.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css>">
    ```

- 폰트 어썸4
	```html
	<link rel="stylesheet" href="<https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css>">
	```
- 폰트 어썸5
	```html
	<link rel="stylesheet" href="<https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css>">
	```
- 폰트 어썸이 적용되지 않을 시
	- `font-family: "FontAwesome";`를 적용하거나 폰트 weight를 400으로 설정

- 참고링크
	- [폰트어썸5 사용법](https://www.daleseo.com/font-awesome/)
	- [웹디자인에 꼭 필요한 무료 아이콘 사이트 3곳](https://smartsolar.tistory.com/entry/%EC%9B%B9%EB%94%94%EC%9E%90%EC%9D%B8%EC%97%90-%EA%BC%AD-%ED%95%84%EC%9A%94%ED%95%9C-%EB%AC%B4%EB%A3%8C-%EC%95%84%EC%9D%B4%EC%BD%98-%EC%82%AC%EC%9D%B4%ED%8A%B8-3%EA%B3%B3)




# 연관문서