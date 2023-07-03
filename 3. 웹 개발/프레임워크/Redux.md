---
tag : 라이브러리/상태관리
aliases : 리덕스
---

# 개요
>[!info] 리덕스는 상태를 효율적으로 관리할 수 있게 도와주는 도구로 [[React.js]] 뿐만 아니라 [[JQuery]], [[Augulor]] 등을 사용하는 app에서도 사용할 수 있음

# 리덕스 개념 ![[Pasted image 20230703155833.png]]
- **액션 Action**
	- Action Creator : 액션 생성함수로 파라미터를 입력받아 액션 객체 형태로 만들어줌
- **리듀서 Reducer** : 변화를 일으키는 함수, 이전 상태와 액션을 파라미터로 받음
- **스토어 Store** : 컴포넌트 외부에 있는 상태 저장소로 현재 상태들, 리듀서, 그리고 몇가지의 내장함수를 포함하고 있음

- 용어정리
	- `subscribe(listener)` : 특정 함수를 구독해서 해당 상태값이 스토어에 변동이 생기면 전달 받았던 함수를 호출해줌
	- `dispatch(action)` : action의 상태를 업데이트 해줌
	- 여기서 불변성이란 뭘까?

## 리덕스 규칙
- 단일 스토어 사용을 권장
- 상태는 읽기 전용이어야한다.
- 리듀서는 순수한 함수이여야 한다. 

## 리덕스 설치하기
- [리덕스 dev 툴](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd/related?page=1&hl=ko&itemlang=en-GB)


## 참고 문서
- [리덕스 설치와 실제 예제 보여줌](https://chaeyoung2.tistory.com/59)
- [리덕스 개념설명](https://velog.io/@youthfulhps/What-is-Redux-and-why-use-it)
- [리덕스 개념설명2](https://velopert.com/3528)