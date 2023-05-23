---
tag : 데이터베이스
---

# 개요
- Create : 생성
- Read : 읽기
- Update : 수정
- Delete : 삭제
---
- CRUD 관점에서 데이터 봐야 함 (만약 CRUD 중 특정 기능이 없는 기획은, 그 기획 의도가 명확해야 하며, 이유도 설명할 수 있어야 함)
- **CPUD에서 API를 사용해야 하는 이유**
	- 타임라인의 CRUD 요청은 각각의 주소를 가짐
		- C : 컴퓨터주소/timelinecreate 
		- R : 컴퓨터주소/timelineread 
		- U : 컴퓨터주소/timelineupdate 
		- D : 컴퓨터주소/timelinedelete
		- 이렇게 주소를 구성하면, 많은 주소를 가져 관리하기 힘드므로 따라서 실무에서는 **API**를 구축해서 CRUD를 <mark class="hltr-purple">하나의 주소로 관리</mark>하여 위의 단점타파 (물론 모든 회사에서 통용되는 규칙이 아님)
			👉 **RESTful API CRUD**
			- C : POST 
			- R : GET 
			- U : PUT(전체) / PATCH(일부) 
			- D : DELETE