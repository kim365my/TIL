---
tag : 프론트엔드 마크업_언어 스타일시트
aliases : Cascading Style Sheets - 종속형 시트
---
# 개요
- 연관키워드
	- CSS 도구
		- [[SASS]] : Syntactically Awesome Style Sheets - 문법적으로 어썸한 스타일시트
		- [[SCSS]] : Sassy CSS - 문법적으로 짱 멋진(Sassy) CSS
		- PostCSS : [[Node JS]]와 함께 언급되는 css 후처리기
	- CSS 프레임 워크
		- 부트스트랩 프레임워크 [설치 페이지](https://getbootstrap.com/docs/4.4/getting-started/download/)  [템플릿](https://learn2you.tistory.com/42)
			```html
			<link rel="stylesheet" href="https://unpkg.com/bootstrap@3.3.7/dist/css/bootstrap.min.css">
			```
- 참고문서
	- https://cocoon1787.tistory.com/m/843
	- https://velog.io/@wiostz98kr/TIL8-l-CSS-Grid


# 기초 CSS
``` css
선택자 {
	 코드 작성;
}
```
 - 기본 구조

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

# 선택자
- DOM 요소를 선택
## 속성 선택자
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


## 가상 선택자
- 선택자와 달리 선택한 요소가 특별한 상태일 때 사용가능
- **가상 선택자의 종류**
	- **동적 가상 클래스** : 어떤 상태나 조건이 발생할 때, 사용자의 액션에 따라 스타일이 바뀜
	- **구조적 가상클래스** : 선택자를 사용하지 않고도 요소를 선택할 수 있게 해줌
- HTML 태그를 선택할 때는 `:root` 가상 선택자를 사용함



# CSS 속성 목록 정리
## 텍스트
## 폰트
### 폰트 속성
| 속성                                                                                                                                         | 값                                                                                                                     |
| -------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| font-family (글꼴 종류) | • 일반 폰트명 → 굴림체, 궁서체, ‘Times New Roman’, … • 폰트 패밀리 → serif, sans-serif, cursive, fantasy, monospace                                                                                                                         |
| font-size (글자 크기)                                                                                                                        | • 절대 단위(cm, mm, in, pt, pc, px), 상대 단위(em, ex, %) • xx-small, x-small, small, medium, large, x-large, xx-large |
| font-style (글자 스타일)                                                                                                                     | normal, italic, oblique                                                                                                |
| font-variant (작은 대문자로 변환)                                                                                                            | normal, small-caps                                                                                                     |
|  font-weight (글자 굵기)  |  • 100, 200, 300, 400, 500, 600, 700, 800, 900 • normal(=400), bold(=700), bolder, lighter                                                                                                                      |
| font (글꼴 속성의 일괄 지정)  |   [ font-style | font-variant | font-weight ] font-size [ / line-height ] font-family                                                                                                                     |

1. font-family 속성값
	1. 일반 폰트명
	2. 폰트 패밀리
		- serif (명조 계열)
		- sans-serif (고딕 계열)
		- cursive (필기체)
		- fantasy (장식이 된 글꼴)
		- monospace (일정한 공간으로 된 타자기 서체)

## 리스트


## 배경
## 박스모델
## 레이아웃
## 디스플레이
## 오버플로
## 캐스케이딩
- CSS에서는 HTML 태그에 하나 이상의 스타일이 적용될 때, 우선순위를 결정하는 규칙을 의미
- **캐스케이딩 규칙** : 중요도 · 특수성 > 코드 순서
	1. **코드 순서**
	2.  **중요도(importance)**
	    1.  Internal 방식으로 작성된 스타일
	    2.  Internal 방식으로 작성된 스타일 내부의 @import
	    3.  External 방식으로 연결된 스타일
	    4.  External 방식으로 연결된 스타일 내부의 @import
	    5.  브라우저의 기본 스타일
	3.  **특수성(specificity)**
	    1.  !important 속성이 지정된 스타일 (ex, `h2{ color: green !important; }`)
	    2.  Inline 방식으로 적용된 스타일
	    3.  아이디 선택자
	    4.  클래스 선택자 ・ 가상 선택자
	    5.  태그 선택자
	    6.  상속된 스타일
	- **특수성 계산기** : 점수를 매겨 우선순위를 결정하는 개념
	    1.  아이디 선택자 개수 계산
	    2.  클래스 ・ 속성 선택 자 및 가상 클래스 개수 계산
	    3.  요소 및 가상 요소 개수 계산
	    아이디 선택자 > 클래스 ・ 속성 선택자 및 가상 클래스 > 요소 및 가상 요소 순서대로 가중치
- `!important` : 일반적으로 !important는 적용된 우선순위를 무시하고 스타일을 강제하기 때문에, 차후에 유지 보수성을 고려한다면 최선책은 아니다. 따라서 너무 많이 사용하지 않는 것이 좋다. (아이디・클래스 선택자로 대체)
## 컬러
## 미디어 쿼리
## 애니메이션
## 사용자 지정 속성
## 링크에 지정 가능 스타일


# 레이아웃 만들기
- Floats
- Positioning
- Display
- Box Model
- CSS Grid
- Flex Box

# 반응형 디자인과 미디어 쿼리


# 그 외
## 와일드 카드 문자
- `*` : 여러문자
- `?` : 한문