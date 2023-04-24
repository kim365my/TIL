> 자주 쓰는 템플릿

# HTML
## 팝이콘
```html
<link rel="shortcut icon" href="./images/favicon/favmc32.png">
<link rel="apple-touch-icon=precomposed" href="./images/favicon/montblanc_fav144.png">
```

## 외부파일 연결
### 가상이미지
```html
<img src="<https://place-hold.it/640x480>" alt="가상 이미지">
```
- https://place-hold.it/사이즈/배경색/텍스트색/문구(?Text=”작성하고 싶은 텍스트”) [공식사이트 : https://place-hold.it/](https://place-hold.it/) [설명 : https://ddorang-d.tistory.com/44](https://ddorang-d.tistory.com/44)
### 폰트어썸
```html
<!-- 폰트어썸 -->
<link rel="stylesheet" href="<https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css>">
```
```html
<!-- 폰트어썸 -->
<link rel="stylesheet" href="<https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css>">
```
### 제이쿼리
```html
<!-- 제이쿼리 코어파일 -->
<script src="./js/jquery-1.12.4.min.js"></script>
<script src="./js/jquery-3.3.1.min.js"></script>
<script src="./js/jquery-3.4.1.min.js"></script>
<!-- 코딩할때 웹킷 안써줘도 자동으로 브라우저에 인식하게 해줌 : 접두어 일일히 쓰는거 -->
<script src="./js/prefixfree.min.js"></script>
<!-- 제이쿼리 플러그인 -->
<script src="./js/jquery-ui.min.js"></script>
<script src="./js/jquery.bxslider.js"></script>
<script src="./js/jquery.scrollTo.min.js"></script>
```
## 기본 폼
```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mobile</title>
    <!-- 파비콘 -->
    <link rel="shortcut icon" href="./images/favicon/favmc32.png">
    <link rel="apple-touch-icon=precomposed" href="./images/favicon/montblanc_fav144.png">    
    <!-- 폰트어썸 -->
    <link rel="stylesheet" href="<https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css>">    
    <!-- 스타일 -->
    <link rel="stylesheet" href="./css/font.css">
    <link rel="stylesheet" href="./css/reset.css">
    <!-- <link rel="stylesheet" href="./css/jquery.bxslider.css"> -->
    <!-- 커스텀 css -->
    <link rel="stylesheet" href="./css/style.css">
    <!-- 제이쿼리 코어파일 -->
    <script src="./js/jquery-1.12.4.min.js"></script>
    <script src="./js/jquery-3.3.1.min.js"></script>
    <script src="./js/jquery-3.4.1.min.js"></script>
    <!-- 코딩할때 웹킷 안써줘도 자동으로 브라우저에 인식하게 해줌 : 접두어 일일히 쓰는거 -->
    <script src="./js/prefixfree.min.js"></script>
    <!-- 제이쿼리 플러그인 -->
    <script src="./js/jquery-ui.min.js"></script>
    <script src="./js/jquery.bxslider.js"></script>
    <script src="./js/jquery.scrollTo.min.js"></script>
</head>
</head>
<body>
    <div id="wrap">
        <!-- header -->
        <header>

        </header>
        <!-- /header -->
        <!-- content -->
        <main role="main">

        </main>
        <!-- /content -->
        <!-- footer -->
        <footer>

        </footer>
        <!-- /footer -->
    </div>
</body>
<!-- 커스텀 js -->
<script src=""></script>
</html>
```

# CSS 
## reset.css
```css
@charset "utf-8";
/* CSS 불러오기 */
@import url(./font.css);
/* CSS 초기화 */
html,body,div,span,iframe,h1,h2,h3,h4,h5,h6,
p,blockquote,pre,cite,code,del,em,img,ins,q,small,strong,sub,sup,
dl,dt,dd,ol,ul,li,fieldset,form,legend,table,caption,
thead,thead,tfoot,tr,th,td,article,aside,canvas,details,figcaption,figure,
footer,header,nav,section,summary,time,mark,audio,video,button {
    margin: 0;
    padding: 0;
    border: 0;
    outline: 0;
    font-size: 100%;
    font-weight: normal;
    vertical-align: baseline;
}
/* 문서 전체 CSS 적용 */
body {
    line-height: 1;
}
/* List 요소 */
ul,li,ol {
    list-style: none;
}
/* A 요소 */
a {
    text-decoration: none;
    color: inherit;
    font-size: 1em;
    vertical-align: baseline;
    background: none;
}
/* img 요소 */
img {
    vertical-align: top;
}
/* hr 요소 */
hr {
    display: block;
    margin: 0;
    padding: 0;
    border: 0;
}
/* button 요소 */
button {
    background: none;
}
/* 박스사이징 */
* {
    box-sizing: border-box;
}
/* 플롯해제 */
.cf::after {
    content: "";
    display: block;
    clear: both;
}
/* 모든 환경에 안보여도 되지만, 반드시 입력해야할 html태그가 존재(웹접근성 때문에) */
/* 그때, 해당 요소를 숨기기 위해 사용되는 class */
.blind {
    position: absolute;
    left: -9999px;
    width: 0;
    height: 0;
    line-height: 0;
    text-indent: -9999px;
    overflow: hidden;
}
/* 패딩, 마진, 보더값 초기화 클래스 */
.no_mt {margin-top: 0 !important;}
.no_mr {margin-right: 0 !important;}
.no_mb {margin-bottom: 0 !important;}
.no_ml {margin-left: 0 !important;}

.no_pt {padding-top: 0 !important;}
.no_pr {padding-right: 0 !important;}
.no_pb {padding-bottom: 0 !important;}
.no_pl {padding-left: 0 !important;}

.no_bt {border-top: 0 !important;}
.no_br {border-right: 0 !important;}
.no_bb {border-bottom: 0 !important;}
.no_bl {border-left: 0 !important;}
```
## font.css
```css
@charset "utf-8";

/* 영문폰트 */
@import url('<https://fonts.googleapis.com/css2?family=Roboto&family=Open+Sans&family=Rowdies&family=Oswald&family=Roboto+Mono&family=Raleway&family=Ubuntu&family=Nunito&family=Merriweather&family=Playfair+Display&family=PT+Sans&family=Rubik&family=Mukta&family=Work+Sans&family=Sevillana&family=Lora&family=Fira+Sans&family=Barlow&family=Kanit&family=Quicksand&family=Passions+Conflict&family=Montserrat&family=PT+Serif&family=Play&family=Monoton&family=Fjalla+One&display=swap>');
/*각 링크{
    @import url('<https://fonts.googleapis.com/css2?family=Roboto&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Open+Sans&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Rowdies&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Oswald&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Roboto+Mono&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Raleway&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Ubuntu&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Nunito&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Merriweather&family=Nunito&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Playfair+Display&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=PT+Sans&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Rubik&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Mukta&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Work+Sans&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Sevillana&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Lora&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Fira+Sans&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Barlow&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Kanit&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Quicksand&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Passions+Conflict&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Montserrat&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=PT+Serif&display=swap>'); 
    @import url('<https://fonts.googleapis.com/css2?family=Play&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Monoton&display=swap>');
		@import url('<https://fonts.googleapis.com/css2?family=Fjalla+One&display=swap>');
		@import url('<https://fonts.googleapis.com/css2?family=Righteous&display=swap>');
} */

/* 한글폰트 */
@import url('<https://fonts.googleapis.com/css2?family=Noto+Sans+KR&family=Nanum+Gothic&family=East+Sea+Dokdo&family=Yeon+Sung&family=Black+Han+Sans&family=Nanum+Pen+Script&family=Jua&family=Gugi&family=Do+Hyeon&family=IBM+Plex+Sans+KR&family=Gowun+Dodum&family=Gowun+Batang&family=Song+Myung&family=Hahmlet&family=Dongle&family=Noto+Serif+KR&display=swap>');
/*각 링크{
    @import url('<https://fonts.googleapis.com/css2?family=Noto+Sans+KR&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Nanum+Gothic&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=East+Sea+Dokdo&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Yeon+Sung&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Black+Han+Sans&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Nanum+Pen+Script&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Jua&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Gugi&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Do+Hyeon&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+KR&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Gowun+Dodum&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Gowun+Batang&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Song+Myung&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Hahmlet&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Dongle&display=swap>');
    @import url('<https://fonts.googleapis.com/css2?family=Noto+Serif+KR&display=swap>');
}*/

/* 영문/한글폰트 나눠서 해야함 */
/* 영문 폰트 20개 이상 한글폰트 15개 이상 */
/* 영문폰트 */
.roboto{font-family: 'Roboto', sans-serif;}
.opensans{font-family: 'Open Sans', sans-serif;}
.rowdies{font-family: 'Rowdies', cursive;}
.oswald{font-family: 'Oswald', sans-serif;}
.robotoMono{font-family: 'Roboto Mono', monospace;}
.raleway{font-family: 'Raleway', sans-serif;}
.ubuntu{font-family: 'Ubuntu', sans-serif;}
.nunito{font-family: 'Nunito', sans-serif;}
.merriweather{font-family: 'Merriweather', serif;}
.playfairdisplay{font-family: 'Playfair Display', serif;}
.ptsans{font-family: 'PT Sans', sans-serif;}
.rubik{font-family: 'Rubik', sans-serif;}
.mukta{font-family: 'Mukta', sans-serif;}
.worksans{font-family: 'Work Sans', sans-serif;}
.sevillana{font-family: 'Sevillana', cursive;}
.lora{font-family: 'Lora', serif;}
.firasans{font-family: 'Fira Sans', sans-serif;}
.barlow{font-family: 'Barlow', sans-serif;}
.kanit{font-family: 'Kanit', sans-serif;}
.quicksand{font-family: 'Quicksand', sans-serif;}
.passionsconflict{font-family: 'Passions Conflict', cursive;}
.montserrat{font-family: 'Montserrat', sans-serif;}
.ptserif{font-family: 'PT Serif', serif;}
.play{font-family: 'Play', sans-serif;}
.monoton{font-family: 'Monoton', cursive;}
.fjallaone { font-family: 'Fjalla One', sans-serif;}
.righteous { font-family: 'Righteous', cursive;}

/* 한글폰트 */
.notosanskr {font-family: 'Noto Sans KR', sans-serif;}
.nanumgothic{font-family: 'Nanum Gothic', sans-serif;}
.eastseadokdo{font-family: 'East Sea Dokdo', cursive;}
.yeonsung{font-family: 'Yeon Sung', cursive;}
.blackhansans{font-family: 'Black Han Sans', sans-serif;}
.nonumpenscript{font-family: 'Nanum Pen Script', cursive;}
.jua{font-family: 'Jua', sans-serif;}
.gugi{font-family: 'Gugi', cursive;}
.dohyeon{font-family: 'Do Hyeon', sans-serif;}
.ibmplexsanskr{font-family: 'IBM Plex Sans KR', sans-serif;}
.gowundodum{font-family: 'Gowun Dodum', sans-serif;}
.gowunbatang{font-family: 'Gowun Batang', serif;}
.songmyung{font-family: 'Song Myung', serif;}
.hohmlet{font-family: 'Hahmlet', serif;}
.dongle{font-family: 'Dongle', sans-serif;}
.notoserifkorean{font-family: 'Noto Serif KR', serif;}
```
## display_none_scrollbar.css
```css
body {
    -ms-overflow-style: none;
}
::-webkit-scrollbar 
{ 
    display: none;
} 
/*특정 부분 스크롤바 없애기*/ 
.box {
    -ms-overflow-style: none;
}
.box::-webkit-scrollbar { 
     display:none;
}
```

## 시스템 폰트 세팅
-   사용자가 기본으로 쓰는 폰트를 적용할 수 있게 세팅
-   기본폰트 : SF로 시작하는 폰트는 맥용 / 윈도우는 Arial
```css
body {
	font-family: "SF Pro Text", "SF Pro Icons", "Helvetica Neue", Helvetica, Arial, sans-serif;
}

/* "system" font family 설정*/
@font-face {
	font-family: system;
	font-style: normal;
	font-weight: 300;
	src: local("./font/SFNSText-Light.ttf"), local("./font/HelveticaNeueDeskInterface-Light.ttf"), local("./font/LucidaGrandeUI.ttf"), local("./font/Ubuntu-Light.ttf"), local("./font/SegoeUILight.ttf"), local("./font/Roboto-Light.ttf"), local("./font/DroidSans.ttf"), local("./font/Tahoma.ttf");
}
/* @font-family 적용 */
body {
	font-family: "system";
}
```