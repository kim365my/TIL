---
tag : 마크업_언어 
---

- 참고문서
	- [JSDoc을 통해 JavaScript API 문서 만들기](https://geniee.tistory.com/28)
	- [JSDOC란?](https://medium.com/@su_bak/javascript-jsdoc-%EC%9D%B4%EB%9E%80-fb7747189200)

# JSDOC란? 
- [[JS]] 소스 코드에 대한 설명을 하기 위해 사용되는 마크업 언어
- JSDOC를 이용하여 JS 함수에 대한 설명을 작성할 수 있음
- 마크 다운도 사용가능, 코드 하이라이팅도 가능해서 사용예제등을 적을 수 있음
	```jsx
	/** 이렇게 쓰면 나중에 함수 쓸때 밑에 설명 나옴 */
	function hello(){return name}
	```
-   C++ : Musketeer
-   파이썬 : Python docstring, 함수 안 최상단에 주석쓰면 나옴
-   자바 : Desc나 since 말고도 여러가지 있음
# JSDOC 태그 문법
- JSDoc에서 지원하는 태그는 _block tag_와 _inline tag_로 나눠지는데요. 사용 문법이 약간 다름
	- HTML의 경우 태그는 꺽쇠 기호(<>)를 사용하여 태그를 표현하지만 JSDoc의 경우 @을 사용하여 태그를 표현
- @alias(block tag)와 @link(inline tag) 태그로 차이점을 확인해보면 HTML의 block tag, inline tag와 비슷하게 주석 안에서 한 줄을 차지하느냐(block tag) 주석 안의 다른 설명 안에 속하느냐(inline tag)에 따라 다른 것을 확인할 수 있습니다.

##. Block tag

```jsx
/**  
* Bar function.  
* @alias bar  
*/  
function foo() {}
```
![[Pasted image 20221027204341.png|200]]
##. Inline tag

```jsx
/**  
* See {@link MyClass} and [MyClass’s foo property]{@link MyClass#foo}.  
* Also, check out {@link http://www.google.com|Google} and  
* {@link https://github.com GitHub}.  
*/  
function myFunction() {}
```
![[Pasted image 20221027204449.png|400]]