📌 데이터베이스의 기본 - SQL(에스큐엘, 데이터 베이스 표준언어)
> SQL은 프로그래밍 언어가 아닌 **쿼리용 언어**
### 0.1. **SQL(에스큐엘, 데이터 베이스 표준언어)**
관계형 데이터베이스 관리 시스템의 데이터를 관리하기 위해 설계된 특수 목적의 프로그래밍 언어
-   row(행)과 column(열)이 존재
-   ORM을 이용하면 파이썬 등으로 작업한 코드를 SQL로 변경해줌.
    -   장점 : 시간 절약가능
    -   단점 : ORM에 너무 의존하면 SQL에서 어떻게 작동하는 지 생각을 못하게 됨
        풀스택개발자는 SQL의 기초적인 원리를 배워야 한다고 함

[데이터 분석, 먹고 들어가기 위한 SQL 공부법(1편)](https://brunch.co.kr/@minu-log/5)

# MySQL 설치 및 환경변수 설정
1. 설치
	- 설치 페이지 : https://dev.mysql.com/downloads/file/?id=514518
2. 환경변수 설정
	- 고급 시스템 설정 - 환경변수 - 새로 추가 - `C:\Program Files\MySQL\MySQL Server 8.0\bin`(mysqld.exe가 있는 곳으로)
	- window - R(실행) ->  cmd - `mysql -V` - 성공 문자 확인