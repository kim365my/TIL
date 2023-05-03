---
tag : 프론트엔드 마크업_언어 스타일시트
aliases : Cascading Style Sheets - 종속형 시트
---
>[!quote] 
>>[!hint] 새로운 소식
>> - [CSS 중첩(nesting)이 된다고?](https://developer.chrome.com/articles/css-nesting/
>
>>[!question]- 어려운 부분
>> - [ ] 선택자는 문자열이 아니라 객체 참조라는 말이 무슨 뜻이지
>> - [ ] 그라데이션이 어려워

>[!quote]- CSS 자주 쓰는 코드
>>[!example]- reset.css
>> ```css
>> @charset "utf-8";
>> /* CSS 불러오기 */
>> @import url(./font.css);
>> /* CSS 초기화 */
>> html,body,div,span,iframe,h1,h2,h3,h4,h5,h6,
>> p,blockquote,pre,cite,code,del,em,img,ins,q,small,strong,sub,sup,
>> dl,dt,dd,ol,ul,li,fieldset,form,legend,table,caption,
>> thead,thead,tfoot,tr,th,td,article,aside,canvas,details,figcaption,figure,
>> footer,header,nav,section,summary,time,mark,audio,video,button {
>>     margin: 0;
>>     padding: 0;
>>     border: 0;
>>     outline: 0;
>>     font-size: 100%;
>>     font-weight: normal;
>>     vertical-align: baseline;
>> }
>> /* 문서 전체 CSS 적용 */
>> body {
>>     line-height: 1;
>> }
>> /* List 요소 */
>> ul,li,ol {
>>     list-style: none;
>> }
>> /* A 요소 */
>> a {
>>     text-decoration: none;
>>     color: inherit;
>>     font-size: 1em;
>>     vertical-align: baseline;
>>     background: none;
>> }
>> /* img 요소 */
>> img {
>>     vertical-align: top;
>> }
>> /* hr 요소 */
>> hr {
>>     display: block;
>>     margin: 0;
>>     padding: 0;
>>     border: 0;
>> }
>> /* button 요소 */
>> button {
>>     background: none;
>> }
>> /* 박스사이징 */
>> * {
>>     box-sizing: border-box;
>> }
>> /* 플롯해제 */
>> .cf::after {
>>     content: "";
>>     display: block;
>>     clear: both;
>> }
>> /* 모든 환경에 안보여도 되지만, 반드시 입력해야할 html태그가 존재(웹접근성 때문에) */
>> /* 그때, 해당 요소를 숨기기 위해 사용되는 class */
>> .blind {
>>     position: absolute;
>>     left: -9999px;
>>     width: 0;
>>     height: 0;
>>     line-height: 0;
>>     text-indent: -9999px;
>>     overflow: hidden;
>> }
>> /* 패딩, 마진, 보더값 초기화 클래스 */
>> .no_mt {margin-top: 0 !important;}
>> .no_mr {margin-right: 0 !important;}
>> .no_mb {margin-bottom: 0 !important;}
>> .no_ml {margin-left: 0 !important;}
>> 
>> .no_pt {padding-top: 0 !important;}
>> .no_pr {padding-right: 0 !important;}
>> .no_pb {padding-bottom: 0 !important;}
>> .no_pl {padding-left: 0 !important;}
>> 
>> .no_bt {border-top: 0 !important;}
>> .no_br {border-right: 0 !important;}
>> .no_bb {border-bottom: 0 !important;}
>> .no_bl {border-left: 0 !important;}
>> ```
>
>>[!example]- font.css
>> ```css
>> @charset "utf-8";
>> 
>> /* 영문폰트 */
>> @import url('<https://fonts.googleapis.com/css2?family=Roboto&family=Open+Sans&family=Rowdies&family=Oswald&family=Roboto+Mono&family=Raleway&family=Ubuntu&family=Nunito&family=Merriweather&family=Playfair+Display&family=PT+Sans&family=Rubik&family=Mukta&family=Work+Sans&family=Sevillana&family=Lora&family=Fira+Sans&family=Barlow&family=Kanit&family=Quicksand&family=Passions+Conflict&family=Montserrat&family=PT+Serif&family=Play&family=Monoton&family=Fjalla+One&display=swap>');
>> /*각 링크{
>>     @import url('<https://fonts.googleapis.com/css2?family=Roboto&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Open+Sans&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Rowdies&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Oswald&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Roboto+Mono&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Raleway&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Ubuntu&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Nunito&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Merriweather&family=Nunito&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Playfair+Display&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=PT+Sans&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Rubik&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Mukta&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Work+Sans&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Sevillana&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Lora&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Fira+Sans&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Barlow&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Kanit&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Quicksand&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Passions+Conflict&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Montserrat&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=PT+Serif&display=swap>'); 
>>     @import url('<https://fonts.googleapis.com/css2?family=Play&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Monoton&display=swap>');
>> 		@import url('<https://fonts.googleapis.com/css2?family=Fjalla+One&display=swap>');
>> 		@import url('<https://fonts.googleapis.com/css2?family=Righteous&display=swap>');
>> } */
>> 
>> /* 한글폰트 */
>> @import url('<https://fonts.googleapis.com/css2?family=Noto+Sans+KR&family=Nanum+Gothic&family=East+Sea+Dokdo&family=Yeon+Sung&family=Black+Han+Sans&family=Nanum+Pen+Script&family=Jua&family=Gugi&family=Do+Hyeon&family=IBM+Plex+Sans+KR&family=Gowun+Dodum&family=Gowun+Batang&family=Song+Myung&family=Hahmlet&family=Dongle&family=Noto+Serif+KR&display=swap>');
>> /*각 링크{
>>     @import url('<https://fonts.googleapis.com/css2?family=Noto+Sans+KR&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Nanum+Gothic&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=East+Sea+Dokdo&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Yeon+Sung&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Black+Han+Sans&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Nanum+Pen+Script&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Jua&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Gugi&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Do+Hyeon&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+KR&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Gowun+Dodum&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Gowun+Batang&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Song+Myung&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Hahmlet&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Dongle&display=swap>');
>>     @import url('<https://fonts.googleapis.com/css2?family=Noto+Serif+KR&display=swap>');
>> }*/
>> 
>> /* 영문/한글폰트 나눠서 해야함 */
>> /* 영문 폰트 20개 이상 한글폰트 15개 이상 */
>> /* 영문폰트 */
>> .roboto{font-family: 'Roboto', sans-serif;}
>> .opensans{font-family: 'Open Sans', sans-serif;}
>> .rowdies{font-family: 'Rowdies', cursive;}
>> .oswald{font-family: 'Oswald', sans-serif;}
>> .robotoMono{font-family: 'Roboto Mono', monospace;}
>> .raleway{font-family: 'Raleway', sans-serif;}
>> .ubuntu{font-family: 'Ubuntu', sans-serif;}
>> .nunito{font-family: 'Nunito', sans-serif;}
>> .merriweather{font-family: 'Merriweather', serif;}
>> .playfairdisplay{font-family: 'Playfair Display', serif;}
>> .ptsans{font-family: 'PT Sans', sans-serif;}
>> .rubik{font-family: 'Rubik', sans-serif;}
>> .mukta{font-family: 'Mukta', sans-serif;}
>> .worksans{font-family: 'Work Sans', sans-serif;}
>> .sevillana{font-family: 'Sevillana', cursive;}
>> .lora{font-family: 'Lora', serif;}
>> .firasans{font-family: 'Fira Sans', sans-serif;}
>> .barlow{font-family: 'Barlow', sans-serif;}
>> .kanit{font-family: 'Kanit', sans-serif;}
>> .quicksand{font-family: 'Quicksand', sans-serif;}
>> .passionsconflict{font-family: 'Passions Conflict', cursive;}
>> .montserrat{font-family: 'Montserrat', sans-serif;}
>> .ptserif{font-family: 'PT Serif', serif;}
>> .play{font-family: 'Play', sans-serif;}
>> .monoton{font-family: 'Monoton', cursive;}
>> .fjallaone { font-family: 'Fjalla One', sans-serif;}
>> .righteous { font-family: 'Righteous', cursive;}
>> 
>> /* 한글폰트 */
>> .notosanskr {font-family: 'Noto Sans KR', sans-serif;}
>> .nanumgothic{font-family: 'Nanum Gothic', sans-serif;}
>> .eastseadokdo{font-family: 'East Sea Dokdo', cursive;}
>> .yeonsung{font-family: 'Yeon Sung', cursive;}
>> .blackhansans{font-family: 'Black Han Sans', sans-serif;}
>> .nonumpenscript{font-family: 'Nanum Pen Script', cursive;}
>> .jua{font-family: 'Jua', sans-serif;}
>> .gugi{font-family: 'Gugi', cursive;}
>> .dohyeon{font-family: 'Do Hyeon', sans-serif;}
>> .ibmplexsanskr{font-family: 'IBM Plex Sans KR', sans-serif;}
>> .gowundodum{font-family: 'Gowun Dodum', sans-serif;}
>> .gowunbatang{font-family: 'Gowun Batang', serif;}
>> .songmyung{font-family: 'Song Myung', serif;}
>> .hohmlet{font-family: 'Hahmlet', serif;}
>> .dongle{font-family: 'Dongle', sans-serif;}
>> .notoserifkorean{font-family: 'Noto Serif KR', serif;}
>> ```
>
>>[!example]- display_none_scrollbar.css
>> ```css
>> body {
>>    -ms-overflow-style: none;
>> }
>> ::-webkit-scrollbar 
>> { 
>>    display: none;
>> } 
>> /*특정 부분 스크롤바 없애기*/ 
>> .box {
>>     -ms-overflow-style: none;
>> }
>> .box::-webkit-scrollbar { 
>>      display:none;
>> }
>> ```
>
>>[!example]- 시스템 폰트 세팅
>> -   사용자가 기본으로 쓰는 폰트를 적용할 수 있게 세팅
>> -   기본폰트 : SF로 시작하는 폰트는 맥용 / 윈도우는 Arial
>> ```css
>> body {
>> 	font-family: "SF Pro Text", "SF Pro Icons", "Helvetica Neue", Helvetica, Arial, sans-serif;
>> }
>> 
>> /* "system" font family 설정*/
>> @font-face {
>> 	font-family: system;
>> 	font-style: normal;
>> 	font-weight: 300;
>> 	src: local("./font/SFNSText-Light.ttf"), local("./font/HelveticaNeueDeskInterface-Light.ttf"), local("./font/LucidaGrandeUI.ttf"), local("./font/Ubuntu-Light.ttf"), local("./font/SegoeUILight.ttf"), local("./font/Roboto-Light.ttf"), local("./font/DroidSans.ttf"), local("./font/Tahoma.ttf");
>> }
>> /* @font-family 적용 */
>> body {
>> 	font-family: "system";
>> }
>> ```


# 개요
- CSS 도구
	- [[SASS]] : Syntactically Awesome Style Sheets - 문법적으로 어썸한 스타일시트
	- [[SCSS]] : Sassy CSS - 문법적으로 짱 멋진(Sassy) CSS
	- PostCSS : [[Node JS]]와 함께 언급되는 css 후처리기
- CSS 프레임 워크
	- 부트스트랩 프레임워크 [설치 페이지](https://getbootstrap.com/docs/4.4/getting-started/download/)  [템플릿](https://learn2you.tistory.com/42)
		```html
		<link rel="stylesheet" href="https://unpkg.com/bootstrap@3.3.7/dist/css/bootstrap.min.css">
		```

>[!cite]- 참고 문서
> - https://cocoon1787.tistory.com/m/843
> - https://velog.io/@wiostz98kr/TIL8-l-CSS-Grid


# 기초 CSS
``` css
선택자 {
	 코드 작성;
}
```

## HTML과 CSS 연결
1.  임베디드 방법 : [[HTML]] 내부적용
	```html
	<style> CSS 코드 + 선택자 + 적용범위 + 속성 + : + 속성값+ ; (단일 속성 지정 마침 기호)</style>
	```
2. 인라인 방법 : 최적화를 생각하면 권고되는 방법은 아님
	```html
	<h1 style=”color:bule; text-align:center;”>인라인 css 적용</h1>
	```
3. 외부 CSS 파일과 연결
	- HTML문서 head에 `<link rel="stylesheet" href="style.css" />` 작성하기

## 선택자
|                                | 예시      | 설명                                                     |
| ------------------------------ | --------- | -------------------------------------------------------- |
| 전체 선택자 universal selector | `*`       | HTML 문서 내의 모든 요소를 선택                          |
| 유형 선택자 type selector      | `태그명`  | 지정된 태그가 가지는 요소를 선택                         |
| 아이디 선택자 id selector      | `#아이디` | 아이디를 지정하여 요소를 선택 ID는 한 요소에만 사용 가능 |
| 클래스 선택자 class selector     |   `.클래스명`        |특정 클래스에 속하는 요소를 선택 class는 여러 요소에 중복 사용가능                                                          |

### 복합 선택자
|                                            | 예시     | 설명                                                                                            |
| ------------------------------------------ | -------- | ----------------------------------------------------------------------------------------------- |
| 그룹선택자                                 | `,`      | ,를 통해서 여러개를 동시에 선택가능                                                             |
| 자손 선택자 descendant selector            | 띄어쓰기 | 자손선택시, 조상과 자손은 띄어쓰기를 통해 구분                                                  |
| 자식 선택자                                | `>`      | 부모 요소 하위에 있는 자식 요소를 선택하기 위해서는 부모와 자식 선택자를 > 기호로 구분하여 나열 |
| 인접 형제 선택자 adjacent sibling selector | `+`      | 첫번째 형제만 선택이 됨, + 기호로 구분하여 나열                                                 |
| 일반 형제 선택자 general sibling selector   |  `~`       |  모든 형제 선택, ~기호로 구분하여 나열                                                                                 |

### 속성 선택자
```
요소명[속성명 연산자 값]{
	속성 : 값;
}
```
| 요소명                 | 설명                                                             |
| ---------------------- | ---------------------------------------------------------------- |
| `요소명[속성명] `      | 상관없이 해당 속성을 사용하는 요소 선택                          |
| `요소명[속성명="값"]`  | 일치하는 요소 선택                                               |
| `요소명[속성명~="값"]` | 공백으로 구분한 요소 선택                                        |
| `요소명[속성명|="값"]` | 정확히 일치하거나 값으로 시작하고 바로 뒤에 `-` 기호로 요소 선택 |
| `요소명[속성명^="값"]` | 시작 부분의 문자와 일치하는 요소 선택                            |
| `요소명[속성명$="값"]` | 끝 부분의 문자와 일치하는 요소 선택                              |
| `요소명[속성명*="값"]` | 전체 중 어떤 일부분이라도 일치하는 요소 선택                     |



# CSS 속성 목록 정리
## @ at-rule 
>[!summary]- @ 기호는CSS에서 at-rules(at-규칙)이라고함 / 요소를 직접적으로 스타일링 하진않지만, 스타일을 적용하는 방법을 제어

- @import	: 다른 스타일시트를 불러올때 정의 ex) `@import url(’ ’);`
- @charset : 스타일 시트 인코딩 정의  ex) `@charset 'utf-8';`
- @container : 반응형 디자인에서 페이지 넓이 뿐만 아니라 부모 요소의 넓이를 기준으로 잡을 수 있음
- @font-face: 글꼴을 사용할때 정의	
- @font-face: 웹폰트 이전에 폰트가 기본으로 나오는걸 방지하기 위해 사용. 메모리 영역에 올라가서 설치되지 않아도 보이게 됨	
	```css
	@font-face {
		font-family: 'trana';
		src: url()
		url() format(),
		url(.) format()
	}
	```
- @keyframes : 애니메이션을 제어하기 위한 정의
- @media : [[CSS#미디어 쿼리|미디어쿼리]]를 사용할때 정의
- @nest : 중첩 셀렉팅을 도와주고 코드 반복을 줄여주는 문법
- @namespace : 네임스페이스로 접두사가 붙을때 정의
- @page : 페이지를 프린트 할 때 레이아웃 설정을 정의
- @scope : 스타일 범위 지정. 테마 별로 스타일 분기처리할때 좋음 (지원되는 브라우저 적음)
	```css
	@scope (.aboutTime) {
		:scope { display: grid; grid-template-columns: 20px 2fr; } 
	img { 
		display: block; width: 100%; 
	}
	```
	- [[JS]]하고 같이 사용되는 문법인가봐... #이해부족  
- @viewport : 각 디바이스에 화면을 어떻게 표현할건지의 대한 정의

## 가상 선택자
- **가상선택자 사용 조건**
	- 선택자와 달리 선택한 요소가 특별한 상태일 때 사용가능
	- 단일태그인 [[HTML]]요소들은 가상선택자를 사용하지 못함
	- [[JS]]에서는 가상 요소를 선택할 수 없음
- **가상 선택자의 종류**
	- **구조적 가상클래스** : 선택자를 사용하지 않고도 요소를 선택할 수 있게 해줌
		- first-child : 형제 중 첫 번째 요소 선택
		- last-child : 형제 요소 중 마지막 요소 선택
		- nth-of-type : 형제 위치 기반 요소 선택
			- :nth-child(숫자) : 기본 / 특정번때 자식 스타일 변경
			- :nth-child(n + 숫자) : 숫자를 포함한 이후의 자식 스타일 변경
			- :nth-child(-n + 숫자) : 위의 반대 / 특정번때 이전 스타일 변경
			- :nth-child(n + 숫자):nth-child(-n + 숫자) : 숫자에서 ~ 숫자까지 스타일 변경
			- :nth-child(odd) : 홀수번 스타일 변경
			- :nth-child(even) : 짝수번 스타일 변경
			- :nth-child(n + 숫자):nth-child(odd나 even):nth-child(-n + 숫자) : 특정 범위 안에서 홀수 혹은 짝수의 자식들에게 스타일을 적용하는 방법
			- :nth-child(An + B) : B번 자식부터 A개 띄어서 스타일을 적용하는 방법
			- nth-child(An + B):nth-child(even) : 위 방법에서 짝수번 자식들에게만 스타일을 적용하는 방법
			- span:nth-of-type(4) > span:first-child : 옆 예시처럼 같은 태그 자식에 대해서 특정 숫자번째 자식 고를 수 있음
		- only-of-type : 자식 중 유일한 요소 선택
		- eq : 메모리 번지수에 따라서 스타일을 적용(nth과 다르게 0부터 시작)
		- lt(less than) : 인덱스 번호에 따라서 지정한 번호 미만이 되는 영역에 스타일을 적용
		- gt(greater than) : 인덱스 번호에 따라서 지정한 번호 초과하는 영역에 스타일을 적용
	- **동적 가상 클래스** : 어떤 상태나 조건이 발생할 때, 사용자의 액션에 따라 스타일이 바뀜
		- 타깃 요소
			- active : 액션이 필요해(클릭하면 반응)
			- visited : 방문 기록 남기기
			- disable : 비활성화
			- hover : 마우스로 상호작용
			- focus : tap시 반응
			- target : 앵커대상에 스타일 적용
		- 조건요소
			- not : 조건이 아닌 대상에 적용
			- checked : 체크되어있으면 적용
		- 가상요소 
			- `::before` : 선택된 요소 앞에 작성됨 `content`의 `“ ”`를 통해서 문자열을 넣을 수 있음
			- `::after` : 선택된 요소 뒤에 작성됨
			- 가상요소 사용이유 #기술면접 
				- 마크업 수정없이 다른 요소를 삽입할 때 사용
- HTML 태그를 선택할 때는 `:root` 가상 선택자를 사용함

## 케스케이딩
>[!note] 아이디 선택자 > 클래스・속성 선택자 및 가상 클래스 > 요소 및 가상 요소 순서대로 가중치

1.  코드 순서
2.  **중요도(importance)**
	1.  Internal 방식으로 작성된 스타일 (ex. head내부에 스타일방식으로 선언)
	2.  Internal 방식으로 작성된 스타일 내부의 @import
	3.  External 방식으로 연결된 스타일 (ex. link로 연결된 css 파일)
	4.  External 방식으로 연결된 스타일 내부의 @import
	5.  브라우저의 기본 스타일
3.  **특수성(specificity)**
	1.  !important 속성이 지정된 스타일 (ex, `h2{ color: green !important; }`)
	2.  Inline 방식으로 적용된 스타일
	3.  아이디 선택자
	4.  클래스 선택자 ・ 가상 선택자
	5.  태그 선택자
	6.  상속된 스타일
---
-   특수성 계산기 : 점수를 매겨 우선순위를 결정하는 개념
	1.  아이디 선택자 개수 계산
	2.  클래스 ・ 속성 선택 자 및 가상 클래스 개수 계산
	3.  요소 및 가상 요소 개수 계산
- `!important` #기술면접 
	- 일반적으로 !important는 적용된 우선순위를 무시하고 스타일을 강제하기 때문에, 차후에 유지 보수성을 고려한다면 최선책은 아니다. 따라서 너무 많이 사용하지 않는 것이 좋다. (아이디・클래스 선택자로 대체)


## 전역변수 (사용자지정 CSS 속성)
```css
/* 전역변수 설정 */
:root{
	--color : #ccc;
}
/* 전역변수 사용 */
body{
	color : var(--color);
}
```
- 기본 사용법 
	- :root(HTML 요소)에 변수를 지정하고 사용
	- css에서 변수식으로 담아서 적용 css를 줄 수 있음
	- 대소문자 구분
	- 상속됨

- 변수의 대안값 : 아래처럼 변수가 정의되지 않았을때 표시되는 대체제를 정의할 수 있음
    ```css
    body{
        color : var(--color, red);
    }
    ```

## 텍스트


## 폰트
>[!quote]- 폰트 사이즈에 대해
> ![[웹 개발론#1. 폰트 사이즈 단위]]

| 속성                                                                                                                                         | 값                                                                                                                     |
| -------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| font-family (글꼴 종류) | • 일반 폰트명 : 굴림체, 궁서체, ‘Times New Roman’, … <br>• 폰트 패밀리 : serif(명조 계열), sans-serif(고딕 계열), cursive(필기체), fantasy(장식이 된 글꼴), monospace(일정한 공간으로 된 타자기 서체)                                                                                                                         |
| font-size (글자 크기)                                                                                                                        | • 절대 단위(cm, mm, in, pt, pc, px), 상대 단위(em, ex, %) <br>• xx-small, x-small, small, medium, large, x-large, xx-large |
| font-style (글자 스타일)                                                                                                                     | normal, italic, oblique                                                                                                |
| font-variant (작은 대문자로 변환)                                                                                                            | normal, small-caps                                                                                                     |
|  font-weight (글자 굵기)  |  • 숫자 : 100, 200, 300, 400, 500, 600, 700, 800, 900 <br>• 문자열 : normal(=400), bold(=700), bolder, lighter                                                                                                                      |
| font (글꼴 속성의 일괄 지정)  |   [ font-style \| font-variant \| font-weight ] font-size [ \/ line-height ] font-family                                                                                                                     |

## 리스트
- list-style-type
	- 리스트의 앞머리 기호를 지정
	- 속성
		- 문자열 값 : 기호 대신 출력하고 싶은 값을 “”를 사용해 표현
		- 미리 정의된 모양 : disc, circle 등
- list-style-position	
	- 리스트 앞머리 기호의 위치를 지정
	- 속성 : inside,outside
		- 기본값이 ouside라 inside로 바꿔야 따로 안놈
- list-style-image
	- 리스트의 앞머리나 기호 대신 특정 이미지를 지정
	- 속성 : url

## 배경
## 박스모델
![[Pasted image 20230425101146.png|150]]
1.  요소 : 텍스트, 사진 등을 보여줌
2.  패딩(padding) : 요소 주변을 감쌈, 해당 부분은 투명색
	-   그 박스 안의 요소를 움직일때 사용
3.  테두리(border) : 요소와 패딩을 감싸는 테두리
4.  마진(margin) : 테두리 밖의 영역을 감쌈, 해당 부분은 투명색
	-   박스간의 관계
	-   마진값을 마이너스를 주면서 위치를 조정할 수 있음
	-   마진상쇄 (마진겹침현상) : 마진이 위아래로 서로 겹칠때 의도한것과는 다르게 나오는 현상
		-   상하만 좌우는 상관 ❌
		-   작은 값과 큰값이 있으면 큰값으로 마진이 생성됨/ 합쳐지는 것은 아님
		-   footer 밑바닥 공백 안됨, margin은 박스간의 관계라 더이상 밑에 아무것도 없으면 적용이 되지 않음
## 레이아웃
- Floats
	- float:left를 썼을 경우 영역사라짐(height:0)을 방지하는 방법 #기술면접 
		- clearfix 방식
			```css
			.clearfix {*zoom:1;}
			.clearfix:before, .clearfix:after{ 
				display: block; content: ''; line-height: 0;
			}
			.clearfix:after {clear: both;}
			```
- Positioning
- Display
- Box Model
- CSS Grid
- Flex Box


## 디스플레이
## 오버플로


## 컬러
## 미디어 쿼리
>[!abstract]- 선행조건
>- HTML 메타에 뷰포트가 꼭 있어야함
>    `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
>	-   디바이스는 기본 설정값이 자동으로 보이는 영역으로 설정
>		-   pc는 뷰포트와 연관없음 모니터 해상도를 기준, 따라서 pc는 제외하고 생각
>	-   viewport는 스마트 기기의 보이는 영역을 기기 실제 화면 크기로 변경해줌
>	-   그래서, 그 값을 이용하여 미디어쿼리 속성으로 기기 화면크기를 정확히 감지하며 반응형을 동작하게 함

```css
@media [only or not] 미디어 유형 and 또는 (조건문 실행문){
	선택자 {
		/* css 코드 작성 */
	}
}
```
- 정의
	- 화면의 크기와 기타 환경을 감지하여 웹 사이트를 변경하는 기술
	- 웹 반응형을 적용하려면 디바이스 기기의 종류를 알아야 하고 그 기기에 맞게 웹 사이트 구조를 바꿀 수 있기 때문에 반드시 필요
-   사용 가능 상황
	1.  CSS : @media & @import를 사용해 특정 조건에 따라 스타일 적용시
	2.  HTML : 요소에 media 특성을 사용해 특정 매체만 가리킬 때
- 조건식
	-   미디어 타입 : all, print, screen, speech *아무것도 안쓰면 기본값 all 적용
	-   조건
		- max-width : 최대가로, 반드시 미디어 쿼리 너비 크기가 큰것부터 작은것 순서대로 코딩 (선생님은 이걸 PC 퍼스트 방식이라고 함)
		- min-width : 최소가로, **반드시** 미디어쿼리 너비 크기가 작은 값부터 큰 것 순서대로 코딩
			-  (모바일 퍼스트 방식) 반응형을 만들때 실무에서는 모바일단을 먼저 만듬 / 연습할때는 넣고 쓰자
		- orientation:landscape : 가로모드
		- orientation:portrait :  세로모드(기본)
	-   연산자
		- `and` : 논리곱(&&)
		- `,` : 논리합(||)
		- not : 부정
- 미디어 쿼리와 함께 사용하는 기능들 #이해부족 
	- Custom-media 쿼리 : 미디어 쿼리를 변수화해서 재사용 가능
	- @nest
	- @container : 반응형 디자인에서 페이지 넓이 뿐만 아니라 부모 요소의 넓이를 기준으로 잡을 수 있음
	- @scope : 스타일 범위 지정. 테마 별로 스타일 분기처리할때 좋음

>[!danger]- 미디어쿼리 작성시 유의사항
> -   정해진 건 아님 : 360(모바일) | 768(태블릿) | 1024(PC)
>-   and 구문 앞, 뒤에는 반드시 공백 한칸
>-   (조건문){실행문} 사이는 붙여서 코딩
>-   조건문에 없는 애들은 공통 스타일이 적용됨
>-   CSS 코드 작성시 유의점
>	-   변화를 주고 싶은 박스 영역만 코딩
>	-   변경하고 싶은 선택자하고 속성명을 똑같이 맞춰줘야 함
>	-   반응형은 구조는 바꾸지 않아야 함

## 애니메이션

## 사용자 지정 속성


## 링크에 지정 가능 스타일





# 신기능 코너!
## nesting
- css 중첩 기능, 하지만 HTML 요소 앞에 `&`기호나 `:is()` 가상 선택자가 필요
- 선택자는 문자열이 아니라 객체 참조?
- `@scope`, `@layer`의 at-rule과 함께 사용됨
- 지원 브라우저 : 23년 04월부터 크롬, edge, 사파리, 안드로이드 기본브라우저에서 지원시작
	- 오페라나 파이어 폭스, 삼성인터넷은 지원하지 않음
	- 현재 전세계 비율로 따지면 40.94%의 브라우저가 지원

# 그 외

## 와일드 카드 문자
- `*` : 여러 문자
- `?` : 한 문자 

## 안전영역(Safe-Area)
- 안전영역(Safe-Area) : 여러 해상도기기 속에서도 필수적인 콘텐츠를 반드시 노출할 수 있게 하는 영역(보통 클래스화 해서 적용함)
    ```css
    .inside{
        width: 1280px;
        margin: 0 auto;
    }
    ```

## 가변 그리드(뷰포트 | 마진 계산하기) 
```css
#wrap{
    max-width: 1920px;
    min-width: 1280px;
    margin: 0 auto;
}
```
-   밀도가 높은 모바일 환경에서 유용
	-   밀도란 같은 색인데 색에 들어가는 픽셀의 수가 높은 것을 말하는 듯
-   max는 최대 / min은 최소값
- 브라우저 너비(pc, 태블릿, 휴대폰 등)에 반응
-   가변과 반응형은 다른 것
	-   pc(px) → 가변(%) → 반응형(%)
		-   기본이 가변단위(% 등), px을 못쓰는건 아님
	-   가변 그리드 : px → %로 변화
	-   그리드 : 화면레이아웃 격자
	-   퍼센트 안먹을 경우 픽셀 값 확인
-   가변 계산하기 (기준 값 필요, 반올림하지말고 소수점까지 다 적을것)
	- `$ (설정하고 \, 싶은 \, 픽셀 / 부모 \, 픽셀값) * 100 $`
	-   마진을 너비값에서 빼고 원하는 영역을 구한다음에 가변계산하기
-   뷰포트하면 무조건 브라우저, pc에서 할때도 설정가능
	-   pc는 모니터 해상도에 따라거 결정/ 모바일은 아님
	-   가로기준, 세로기준으로 계산

## 이슈 사항
-  `display:inline-block`으로 하면 `block`으로 할때와는 다르게 딱 붙지 않고 간격이 생김
	-   `float`이나 마진을 마이너스로 만들거나 폰트 사이즈를 줄이는 방법으로 간격을 없앨 수 있대


# 연관 문서