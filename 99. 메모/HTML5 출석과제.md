# 1. 주어진 HTML 요소(태그)에 대해서 다음 조건이 만족되도록 정리하시오.
| HTML 요소 | 1. header, hgroup <br>2. nav, section, article, aside, footer <br>3. mark, time, meter, progress, <br>4. ruby, wbr, details, datalist, output |
| --------- | --- |

1. 각 요소는 주어진 순서대로 정리하여 설명한다. 
2. 각 요소에 대해서는 요소의 기능, 주요 속성(또는 하위 요소)의 기능, 그리고 간단한 활용 예시는 반드시 포함해서 설명해야 한다. 
	- 속성(하위 요소)이 없는 경우에는 속성(하위 요소) 설명은 생략해도 된다.
	- 활용 예시에는 해당 요소와 주요 속성(하위 요소)들의 사용 방법을 간단히 설명하는 정도의 예시를 포함한다
---
- header 요소는 HTML5의 시맨틱요소 중의 하나이다. 시맨틱태그란 문서를 구조화하기 위해 사용되는 요소로 header 요소는 해당 HTML 파일의 제목을 나타내는 요소이다.
- hgroup 요소는 제목요소 (h1~h6)를 그룹핑하는 요소로, 목차를 만들기 위해서 사용되었으나 현재는 거의 사용되지 않는다.
	```html
	<header>
		<hgroup>
			<h1>제목이나 로고 등을 넣는 부분</h1>
			<p>
				제목에 대한 부가적인 설명
			</p>
		</hgroup>
	</header>
	```
- nav요소는 메뉴영역을 나타내는 요소로 주로 gnb를 만드는 경우에 사용된다.
- section은 제목, 주제별로 나눌 수 있는 문서의 내용 영역을 구성하는 요소이다.
- article은 개별 콘텐츠를 나타내는 독립적인 요소이다. 신문을 빗대어서 설명해보자면, 기사와는 상관없는 짜투리 만화나 광고 같은 부분을 들 수 있다.
- footer는 꼬릿말을 나타내는 요소로 주로 웹사이트의 마지막 부분에 회사정보나 법률정보를 표시하는 데 사용된다.
	```html
	<nav>
		<ul class="gnb">
			<li><a href="#">about</a></li>
			<li><a href="#profile">profile</a></li>
			<li><a href="#goal">goal</a></li>
			<li><a href="#contact">contact me</a></li>
		</ul>
	</nav>
	<section>
		<article>
			독립적인 영역
		</article>
		문서의 내용 작성
	</section>
	<footer>
		회사 정보 등
	</footer>
	```
- mark는 html 요소에서 형광펜으로 하이라이트를 해주는 듯이 텍스트에 색을 칠해주는 요소이다.
- time은 datetime 속성으로 값을 지정하면 시간을 저장할 수 있다. 이 속성이 없는 경우 텍스트를 해당 속성 값으로 인식하기에 자식요소가 있어서는 안된다.
- meter는 html 요소에서 수치를 그래픽하게 보여주는 요소이다. 속성을 통해 최소, 최댓값을 지정할 수 있으며 low, high를 통해 범위를 지정할 수 있다. 최솟값 속성인 min은 생략하면 기본값 0이 지정된다.
	- <meter min="0" max="100" low="30" high="70" optimum="80" value="80">
	    at 80/100
		</meter>
- progress는 meter와 동일하게 수치를 그래픽하게 보여주는 요소이지만 meter에 비해 단순한 속성을 가지고 있다. 예를 들어 meter에서는 최솟값을 지정해주는 속성이 있었지만 progress는 최솟값을 지정하는 속성이 존재하지 않는다.
	- <progress  max="100" value="10"> 10% </progress>
	```html
	mark는 html 요소에서 형광펜으로 <mark>하이라이트</mark>를 해주는 듯이 텍스트에 색을 칠해주는 요소이다.
	time은 datetime 속성으로 값을 지정하면 <time datetime-"2023-05-08">시간</time>을 저장할 수 있다.
	<meter max="100" low="30" high="70" optimum="80" value="80">at 80/100</meter>
	<progress  max="100" value="10"> 10% </progress>
	```
- ruby는 동아시아에서 특히 일본에서 사용되는 발음 주석을 표현하는 데 사용된다. rp와 rt요소 안에 있는 텍스트가 작게 표시되고 ruby요소 위에 올라가게 된다.
- wbr는 줄바꿈이 가능할 경우 줄바꿈이 되는 부분을 지정할 수 있는 요소이다. br 요소와 다르게 텍스트가 표현되는 부분이 충분할 경우 줄바꿈이 되지 않고 부족하게 되었을 경우에만 줄이 바뀌는 특성이 있다. 태그는 하나만 사용된다.
- details는 노션의 토클기능처럼 열고 닫을 수 있는 텍스트 상자를 표현하는 요소이다. summary요소와 함께 사용되며 summary 요소의 텍스트가 닫혀있을 경우 표시된다. summary 요소 이외에 details 안에 있는 텍스트는 닫혀 있는 경우 보이지 않고 열었을 경우에만 보이는 특징이 있다. 
- datalist는 option 요소와 함께 사용되며 option 데이터를 선택할 수 있는 요소이다. 
- output은 사용자가 입력한 값을 통해 동적으로 변경되는 값을 출력할 수 있는 요소이다. form요소와 함께 사용되며 아래 예시처럼 oninput 속성을 통해 어떤 값을 표시할 것인지 지정가능하다.
	```html
	 <details>
		 <summary>요약</summary>
		 ruby는 동아시아에서 특히 일본에서 사용되는 발음 주석을 표현하는 데<wbr> 사용된다. 이 예시처럼 <ruby>동아시아<rp><rt>일본</rt><rp></ruby>사용된다. 
		 <datalist id="laungre">
			<option value="한국어" label="한국어"></option>
			<option value="한국어"></option>
			<option value="한국어"></option>
		</datalist>
		<form oninput="sum.value=parseInt(num1.value)+parseInt(num2.value)">
			  <input type="number" id="num1" name="num1" value="50" /> +
			  <input type="number" id="num2" name="num2" value="10" /> =
			  <output name="sum" for="num1 num2">60</output>
		</form>		 
	 </details>
	```



# 2. 수업을 통해 학습한 HTML5 요소를 사용하여 자기 소개 페이지(3~5페이지)를 작성하여 HTML 문서 및 관련 자료(이미지, 동영상 등)를 압축하여 보조파일로 제출한다.

