---
본딧말 : 스코프
요약 : 저장범위
---

# 스코프란?
- 스코프의 종류
	- page(기본값) : pageContext 기본 객체 
	- request : request 기본 객체
	- session : session 기본 객체
	- application : application 기본 객체
- 스코프의 범위 : `page` < `request` < `session` < `application`
	- session부터 Scope의 범위가 넓어서 브라우저를 종료하지 않는 한 한 서버내에서 값의 교환이 가능