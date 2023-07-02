---
tag : 
aliases : 
info : js에서 css 애니메이션을 제어할 수 있는 API
---

# 사용예시
```js
const box = document.querySelector('.box');
box.animate(
	[
		{transform: 'translateX(0)', opacity:0},
		{transform: 'translateX(200px)', opacity:1},
	],
	{
		duration: 1000, // 애니메이션 관련 설정 옵션
	}
);
```
- animate 메서드의 첫번째 인수로는 키프레임 내용을 작성하면 됨
- 두번째 인수로는 [[CSS]] 애니메이션 설정을 오브젝트 형태로 젆으면 됨