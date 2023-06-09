---
tag : 데이터베이스 쿼리용_언어 백엔드
aliases : 에스큐엘, 데이터베이스 표준언어
---

# 개요
>[!info] [[데이터베이스]]의 기본 - SQL(에스큐엘, 데이터 베이스 표준언어)
> - [[오라클]]을 기준으로 설명함
> - SQL은 프로그래밍 언어가 아닌 **쿼리용 언어**
> 	- 관계형 데이터베이스 관리 시스템(RDBMS)를 관리하기 위해 설계된 특수 목적의 프로그래밍 언어
> 	- 쿼리 : RDBMS에서 이해하는 유효한 명령
> 		-  row(행)과 column(열)이 존재
> - ORM(객체 관계)을 이용하면 [[python|파이썬]] 등으로 작업한 코드를 SQL로 변경해줌
>	- 장점 : 시간 절약가능
>	- 단점 : ORM에 너무 의존하면 SQL에서 어떻게 작동하는 지 생각을 못하게 됨
>		- 풀스택개발자는 SQL의 기초적인 원리를 배워야 한다고 함
>- 일단 뭐가 뭔지 모르겠으면 ⭐[[CRUD]]만 잘 하면 됨

## DBMS 설치
>[!quote] DBMS 설치
>>[!quote]- [[오라클]] 11gEE 설치 및 환경변수 설정
>> ![[오라클#오라클 설치하기]]
>
>>[!quote]- MySQL 설치 및 환경변수 설정
>> 1. 설치 페이지 : https://dev.mysql.com/downloads/file/?id=514518
>> 2. 환경변수 설정
>>	- 고급 시스템 설정 - 환경변수 - 새로 추가 - `C:\Program Files\MySQL\MySQL Server 8.0\bin`(mysqld.exe가 있는 곳으로)
>>	- window - R(실행) ->  cmd - `mysql -V` - 성공 문자 확인
>

## 기본 문법
>[!warning] 주의 
>- 변수 개념이 없음. 대신 오라클에서는 dual 이라는 한행짜리 테스트 테이블을 제공하므로 이 dual을 이용해서 함수를 출력하거나 하는 등의 일이 가능
>- SQL에서 무조건 작은 따음표를 사용하고 AS에서 문자열 넣을때만 큰 따음표
> - 대소문자 구별안함 (데이터 값은 예외)
- `ctrl+enter`로 한줄씩 실행가능
- **기본 지원** : 데이터 타입제공 / 사칙연산 가능 / 메소드 지원
- **오라클 DB 이름 명명 규칙**
	- 문자로 시작해야함
	- 1자부터 30자까지 가능
	- A-z, 0-9, $ 포함가능
	- 동일한 사용자가 소유한 다른 DB의 이름과 중복되지 않아야함
	- 오라클의 예약어가 아니어야함
- **주석**
	- 한줄 주석 : `--`
	- 여러줄 주석 : `/**/`
- **기본 데이터 타입**
	- 숫자 데이터 
		- NUMBER(n) : 정수 저장
		- NUMBER(n, num)  : 실수 저장, num부분에 소수점을 얼마까지 쓸건지 작성
	- 문자 데이터 
		- CHAR(n) 
			- 설정된 칼럼 크기보다 적은 양의 데이터가 들어오더라도 설정된 길이를 모두 차지
			- 오버플로시 오류가 발생
			- 데이터가 낭비될 수 있지만 크기계산이 없어서 속도는 빠름 
		- VARCHAR2(n)
			- 가변 길이 문자 데이터를 저장하는 칼럼타입
			- 저장하는 데이터의 크기에 따라 알맞은 공간을 사용
			- 데이터를 저장할 때 저장공간이 절약되지만 크기 계산이 필요
	- 날짜 데이터 : 거의 문자열과 비슷하게 취급
- **연산자**
	- `=` : 같으면 true
	- `<, >, <=, >=` : 대소 비교
	- `!=, <>, ^= = >` : 다르면 true


# 명령어의 종류
![[Pasted image 20230428093752.png|400]]
  
| 명칭                                               | 정의                                                |
|--------------------------------------------------|---------------------------------------------------|
| DDL(Data Definition Language)          | 데이터 정의어 <br> 테이블, 시퀀스, 뷰 등 DB에서 사용하는 DB 오브젝트 구조를 생성할때 사용하는 명령어 |
| DML (Data Manipulation Language)     | 데이터 조작 언어                                                  |
| DCL  (Data Control Language)        | 데이터 제어 명령어                                                  |
| TCL (Transaction Control Language) |[[#트랜잭션(Transaction)]] 제어 명령어 | 


## DDL 명령어

| 명령어    | 설명                                                                             |
| --------- | -------------------------------------------------------------------------------- |
| [[#Create]]    | DB 오브젝트 생성                                                                 |
| [[#DROP]]      | DB 오브젝트 삭제                                                                 |
| [[#ALTER\|ALTER]]     | DB 오브젝트 수정하는 명령어로 제약조건을 추가, 수정, 삭제할 수 있음                                                                 |
| [[#TRUNCATE\|TRUNCATE]]  | DB 오브젝트 완전 삭제 <br> DB 데이터 관련된 하나의 트랜직션이 삭제               |
| [[#show 명령어\|show]]      | 데이터베이스 목록이나, 테이블 목록 등 다양한 정보를 보기 원할 때 사용하는 명령어 |
| show user | 현재 접속한 계정을 확인하는 명령어                                               |
| [[#show recyclebin : 휴지통 보기\|show recyclebin]]  | 휴지통에 있는 삭제 테이블 보기                                                   |
| [[#PURGE RECYCLEBIN : 휴지통 비우기\|PURGE RECYCLEBIN]]     | 휴지통 비우기                                                                    |
| [[#FLASHBACK TABLE 테이블명 to BEFORE : 테이블 복구\|FLASHBACK TABLE 테이블명 to BEFORE]] | 테이블 복구                                                                      |


## DML 명령어

| 명령어                       | 설명                                                                              |
| ---------------------------- | --------------------------------------------------------------------------------- |
| [[#INSERT INTO\|INSERT INTO ]]                 | 데이터 생성 <br> VALUES()를 이용해 데이터를 삽입                                  |
| [[#DESC]]                         | 테이블 구조 확인 명령어                                                    |
| [[#select\|select]]                       | 데이터 조회                                                                       |
| [[#AS\|AS]]                           | 칼럼을 원하는 이름으로 생성 후 조회할 수 있음                                     |
| [[#order by\|order by ]]                    | 정렬                                                                              |
| [[#DISTINCT\|DISTINCT]]                     | 중복값 제거                                                                       |
| [[#WHERE\|WHERE]]                        | 조건문                                                                            |
| [[#AND, OR, NOT\|AND, OR, NOT]]                 |                                                                                   |
| [[#MOD(value1, value2)\|MOD(value1, value2)]]          | 나머지 구하기                                                                     |
| [[#column BETWEEN 조건 AND 조건\|column BETWEEN 조건 AND 조건]] | 조건과 조건을 만족할 때                                                           |
| [[#IS NULL\|IS NULL]]                      | null 조회가능                                                                     |
| [[#⭐ like : 데이터의 내용 조회\|like ]]                        | 데이터의 일부분으로 원하는 내용을 검색할 수 있음                                  |
| [[#NVL(column, value)\|NVL(column, value)]]           | null 있는 칼럼을 찾아서 해당 값으로 치환해주는 메소드                             |
| [[#IN(value)\|IN(value)]]                    | 해당 값을 포함되었다면 boolean 값을 반환하는 메소드                               |
| 집합                         |                                                                                   |
| [[#UNION\|UNION]]                        | 합집합                                                                            |
| [[#UNION ALL\|UNION ALL]]                    | UNION와 다르게 중복 제거 안함                                                     |
| [[#INTERSECT\|INTERSECT]]                    | 교집합                                                                            |
| [[#MINUS\|MINUS]]                        | 차집합                                                                            |
| [[#DECODE\|DECODE]]                       | switch~ case 문과 비슷한 함수로 위처럼 지정한 값을 원하는 이름으로 출력할 수 있음 |
| [[#GROUP BY\|GROUP BY]]                     | 그룹 함수                                                                         |
| [[#HAVING]]                       | 그룹 함수에 조건을 줄때 사용하는 명령어                                           |

## DCL 명령어

| 명령어      | 설명                                                                           |
|----------|------------------------------------------------------------------------------|
| [[#GRANT]]   | 권한 부여 |
| [[#REVOKE]] | 권한 회수                               |

## TCL 명령어

| 명령어      | 설명                                                                           |
|----------|------------------------------------------------------------------------------|
| [[#COMMIT]]   | - 작업 적용하는 키워드로 하나의 트랜직션을 종료시키는 의미를 가지고 있음 <br> - 외부 작업시 반드시 커밋을 적용시킨 후에 외부 작업을 진행해야 혼란을 줄일 수 있음 <br>- 커밋을 하게 되면 세이브 포인트를 통한 [[#ROLLBACK]]이 어려우므로 신중하게 해야함 |
| [[#ROLLBACK]] | 트랜잭션 취소, 커밋한 상태로 되돌릴 수 있음                                                             |


# DB 오브젝트
>[!warning] RBDMS마다 객체의 종류가 다른가봐

| DB 오브젝트 | 설명                                    |
|-----------|---------------------------------------|
| 테이블(Table)       | 데이터를 담고 있는 객체<br>- 데이터베이스의 가장 기본적인 객체로 행(Row, 튜플), 열(Column, 컬럼)로 구성 <br>- 논리 설계 단계의 <mark class="hltr-purple">개체(Entity)</mark>에 대응하는 객체                         |
| 뷰(View)         | 하나 이상의 테이블을 연결해 마치 테이블인 것처럼 사용하는 가상객체 |
| 인덱스(Index)       | 테이블에 있는 데이터를 빠르게 찾기 위한 객체             |
| 시소님(Synonym)       | 데이터베이스 객체에 별칭을 부여한 객체로 보통 다른 유저의 객체를 참조할 때 많이 사용됨                 |
| 시퀀스(Sequence)       | 일련번호 채번을 할 때 사용되는 객체                  |
| 함수        | 특정 연산을 하고 값을 반환하는 객체                  |
| 프로시저      | 함수와 비슷하지만 값을 반환하지 않는 객체               |
| 패키지       | 용도에 맞게 함수나 프로시저를 하나로 묶어 놓은 객체         |

>[!warning] DB에서 개체(entity)를 객체(object)라고 하면 안되는 이유 
> - 하나의 개체는 하나 이상의 속성(attribute)으로 구성되고 각 속성은 그 개체의 특성이나 상태를 설명함
> - 객체는 실제로 컴퓨터 내에서 구현되는 코드 블럭같은 거
> - [참고 문서 : 한빛출판네트워크](https://m.hanbit.co.kr/network/category/category_view.html?cms_code=CMS4926333301)

## 트랜잭션(Transaction)
- **정의**
	- 데이터베이스에 올라가는 작업단위, 데이터 처리의 한 단위
	- 하나의 트랜잭션은 여러 명령어로 이루어져 있음
	- 새로운 [[#COMMIT]]을 실행하기 전까지 수행되는 SQL문을 의미함
	- 트랜잭션 관리 명령어를 [[#TCL 명령어]]라고 함
- 트랜잭션의 모든 과정이 정상적으로 완료되는 경우에만 변경사항이 확정됨, [[#COMMIT]]을 통해서 트랜잭션을 완료하고 작업단위를 저장할 수 있음
- 


## 데이터 딕셔너리(Data Dictionary) 
- **데이터 딕셔너리란?** [[정보처리기사#7. 시스템 카탈로그(System Catalog) ⭐⭐|시스템 카탈로그]]라고 부르며 사용가능한 데이터베이스 및 테이블의 정보를 요약해서 가지고 있는 시스템 테이블
	- 테이블의 요약된 정보는 **메타데이터**라고 하며 종류는 <mark class="hltr-purple">스키마 · 사용자 · 객체 · 권한 · 롤 · 데이터 베이스의 정보</mark> 등이 있음
		- 마치 옵시디언에서 메타데이터를 이용해 하나의 노트를 관리하는 것처럼 데이터 딕셔너리는 테이블을 이러한 방식으로 관리함
	- 시스템 정보를 가지고 있기에 일반 사용자는 조회만 가능
	- [[Pasted image 20230502091637.png|오라클의 딕셔너리]]
- [[#시퀀스(Sequence)]]
	- 기본 키를 사용하기 편하도록 설계된 자동번호 생성기
	- 호출할 때마다 번호를 자동으로 증가시키는 DB 오브젝트   
	- [ibm에서 설명한 시퀀스](https://www.ibm.com/docs/ko/db2/11.1?topic=objects-sequences)

## View
- DB에서 제공하는 가상의 테이블로 대충 쿼리문 저장해서 실행하는 거라고 생각하면 됨
- 뷰 사용시 복잡한 쿼리문을 대신할 수 있어서 개발의 용이함을 가짐
- 주로 복잡한 서브쿼리 사용시 다음에 다시 사용할 목적으로 사용

### 사용자 유형별 접근 권한별 뷰

|      | 설명                                                       |
| ---- | ---------------------------------------------------------- |
| ALL  | 모든 개체에 접근가능                         |
| DBA  | DB관리자들만 접속가능 직접 접근이 가능하며 데이터 사전을 직접 갱신 할 수 있음    |
| USER | 뷰를 통해 소유중인 개체에만 접근 가능, 읽기만 할 수 있을 뿐 다른 작업은 불가 |
- 오라클 명령어의 접두어를 통해서 어떤 뷰가 무슨 유형에서 사용되는지 알 수 있음

### 시스템 뷰의 종류
- 동적 뷰 : 테이블에서 동적으로 변경되는 메모리나 현재 세션에 관한 정보를 알 수 있는 뷰
- 정적 뷰 : 하나 이상의 테이블에 있는 데이터들의 부분 집합

## 조인의 종류
### 논리적 조인

| 구분                 | 조인 유형                        | 설명                                          |
|--------------------|------------------------------|---------------------------------------------|
| INNER JOIN <br>(내부 조인) | EQUI JOIN (동등 조인)            | 공통 존재 컬럼의 값이 같은 경우를 추출                      |
|                    | NATURAL JOIN (자연 조인)         | 두 테이블의 모든 컬럼을 비교해, 같은 컬럼 명을 가진 값이 같은 경우를 추출 |
|                    | CROSS JOIN (교차 조인)           | 조인 조건이 없는 모든 데이터 조합을 추출 ★                   |
| OUTER JOIN <Br>(외부 조인) | LEFT OUTER JOIN (왼쪽 외부 조인)   | 왼쪽 테이블의 모든 데이터와 오른쪽 테이블의 동일 데이터를 추출         |
|                    | RIGHT OUTER JOIN (오른쪽 외부 조인) | 오른쪽 테이블의 모든 데이터와 왼쪽 테이블의 동일 데이터를 추출         |
|                    | FULL OUTER JOIN (완전 외부 조인)   | 양쪽의 모든 데이터를 추출                              |



### 물리적 조인

| 종류                          | 설명                                                           |
|-----------------------------|--------------------------------------------------------------|
| NESTED-LOOP JOIN <br>(중첩 반복 조인) | 2개 이상의 테이블에서 하나의 집합을 기준으로 순차적으로 상대방 Row를 결합해 원하는 결과를 조합하는 방식 |
| SORT-MERGE JOIN <Br>(정렬 합병 조인)  | 양쪽 테이블의 정렬한 결과를 차례로 검색하면서 연결고리 형태로 합병하는 방식                   |
| HASH JOIN <Br>(해시 조인)           | 해싱 함수 기법을 활용하여 조인을 수행하는 방식                                   |




### 데이터 제약조건
- **데이터 무결성** : 데이터에 결함이 존재해서는 안됨
	- 데이터에 결함이 없는 성질
	- 정확성, 일관성, 유효성이 유지되는 데이터를 말함
	 - 데이터 무결성 제약 조건
		- NOT NOLL : 해당 도메인에 null을 허용하지 않음
		- UNIQUE : 해당 도메인에 중복되는 값을 허용하지 않음
		- primary key : 해당 도메인을 테이블의 기본 키로 사용 UNIQUTE = NOT null
		- CHECK : 원하는 조건을 지정, 도메인 무결성을 유지함
	- CONSTRAINT_TYPE
		- P : Primary Key
		- R : Foregin Key
		- C : Check or Not null
		- U : Unique
			- 유니크와 PK의 차이점 : PK는 참조 주소가 FK와 연동이 됨
- **개체 무결성**
	- 테이블의 데이터 = 반드시 한 행을 구분할 수 있어야함
	- 테이블의 개체 무결성을 지키기 위한 제약조건 = PK 사용
- **참조 무결성**
	- 참조 관계에 있는 데이터는 항상 일관된 값을 가져야함
	- 참조 무결성을 지키기 위한 제약조건 = FK 사용
	- JOIN을 통해서 FK와 PK를 연결해줄 수 있음
	- e.g. departments에서 departments_id는 PK이고 employess에서는 departments_id는 FK로 되어있음

>[!note]- 제약조건을 걸면 DB에서 조건에 맞지 않는 값은 받아들이지 않음, 하지만 DB에서 처리하기 전에 프론트엔드에서 유효성 검사를 하면 DB연결 비용절약 가능



### 데이터 딕셔너리 쿼리문
- 색인(index) : DML, DCM 만드는 것처럼 `Create index 인덱스명`으로 생성
- `user_catalog` : 뷰, 시퀀스 등을 확인할 수 있는 데이터 딕셔너리 쿼리문
- AS를 통해서 표를 복사할 수 있는 데, 복사할때 CHECK만 복사되고 다른 제약조건은 복사가 되지 않음

### 조회하기
#### 테이블 목록 조회 (뷰, 시퀀스 포함)
- 해당 유저가 소유하고 있는 테이블 목록을 다 보여줌
	```sql
	select * from user_catalog;
	```

#### 제약조건 조회하기
- 제약사항에 대해 볼 수 있는 데이터 딕셔너리 뷰로 접속 사용자의 제약사항만 볼 수 있음
	```sql
	select * from user_constraints;
	```
- 모든 사용자의 제약사항을 볼 수 있는 데이터 딕셔너리 뷰
	```sql
	select * from all_constraints;
	```
- 한 테이블의 제약사항 조회
	```sql
	select * from user_constraints where table_name = 'FRUTS2';
	```
	- [!] 테이블명을 대문자로 작성해야함

### CONSTRAINT : 생성과 동시에 제약 걸기
```sql
칼럼명 칼럼타입 제약조건(이름이 자동으로 정해짐)
칼럼명 칼럼 타입 CONSTRANT 제약조건명 제약조건
```
>[!example]- CONSTRAINT를 통해서 생성과 동시에 제약조건을 설정할 수 있음
> ```sql
> -- CONSTRAINT 실습
> select * from fruites5;
> 
> create table fruites5(
> 	fid     number(4) -- PK
> 		CONSTRAINT f5_fid_pk        PRIMARY KEY,
> 	fname   varchar2(20)
> 		CONSTRAINT f5_fname_uk      UNIQUE
> 		CONSTRAINT f5_fname_nn  NOT NULL,
> 	grade   varchar2(2)
> 		CONSTRAINT f5_grade_chk     CHECK(grade IN('A+','A','B+','B')),
> 	fsize     number(2)
> 		CONSTRAINT f5_fsize_chk     CHECK(fsize BETWEEN 0 AND 20)
> );
> select * from user_constraints where table_name = 'FRUITES5';
> ```


### ALTER
- 기존 테이블의 무언가를 변경하는 예약어
- **테이블명 변경**
	```sql
	RENAME 현재 테이블명 TO 바꿀 테이블명;
	```
- **칼럼** 추가 | 수정 | 삭제
	- 데이터 새 칼럼 추가하기
		```sql
		ALTER TABLE 테이블명 ADD (칼럼명, 칼럼타입, ...);
		```
	- 칼럼이름 변경하기
		```sql
		ALTER TABLE 테이블명 RENAME COLUMN 현재칼럼명 TO 바꿀 칼럼명;
		```
	- 테이블 컬럼 삭제 : 해당 컬럼의 제약조건들도 함께 삭제됨
		```sql
		ALTER TABLE 테이블명 DROP COLUMN 컬럼명
		```
- **제약조건** 추가 | 수정 | 삭제
	- 이미 생성된 테이블 제약조건 추가
		```sql 
		ALTER TABLE 테이블명 ADD CONSTRAINT 제약조건명 제약조건(칼럼)
		```
	-  이미 존재하는 칼럼을 수정
		```sql 
		ALTER TABLE 테이블명 MODIFY
		```
	- 테이블 제약조건 삭제 : 대소문자 상관없음
		```sql
		ALTER TABLE 테이블명 DROP CONSTRAINT 제약조건명
		```
	- [!] 제약조건 추가시 NOT NULL과 CHECK는 ADD  CONSTRAINT 대신 MODIFY를 사용
	- [?] NOT NULL의 제약조건 키명은 C로 되어 있던데 이것과 관련이 있는걸까?  #질문 

### 색인(index)
- DML, DCM 만드는 것처럼 생성함
- DB 인덱스를 빠르게 하기 위해 사용되는 기능
	- 장점 : 검색속도 빠르고 시스템 부하를 줄여 DB 성능 향상
	- 단점 : insert, update, delete 등 변경 작업이 자주 일어나면 오히려 DB 성능이 저하됨
		- 주기적인 기억공간이 필요
	- [!] 오라클은 테이블 생성시 PK를 설정하면 자동으로 인덱스로 등록
- **인덱스 생성**
	```sql
	Create index 인덱스명 ON 테이블명(칼럼1, 칼럼2, 칼럼3...)
	```
-  **인덱스 정보조회**
    ```sql
    select index_name, table_name, column_name
    from user_ind_columns
    where table_name = 'TEST_LABLE100';
    ```
- **특정 집합 index 만들기**
	```sql
	create index test01_dx on test01(name);
	```
	- 많이 사용하는 칼럼만 만들어서 사용해야 효율성이 높아짐, 아무대나 index를 사용하면 비효율적이므로 주의해서 사용할 것
- 인덱스 속도 테스트

### 시퀀스(Sequence)
- 기본키로 사용하기 편하도록 설계된 **자동 번호 생성기**
- 호출할 때마다 번호를 자동으로 증가시키는 DB 오브젝트
- **시퀀스 생성**
	```sql
	Create SEQUENCE 시퀀스 | 옵션명|;
	Create SEQUENCSE 시퀀스명 INCREMENT BY 1 MAXVAULE 10003 START WITH 10001;
	```
- **시퀀스 조회**
	```sql
	select * from user_sequences;
	```
- **시퀀스 사용법**
	```sql
	insert into bb_board VALUES(
	    BB_BOARD_SEQ.nextval
	);
	```
- **시퀀스 삭제**
	```sql
	Delete SEQUENCE 시퀀스명;
	```

#### 시퀀스 옵션

| 옵션명                   |                      |
| ------------------------ | -------------------- |
| START WITH n             | 시퀀스 시작번호 설정 |
| INCREMENT BY n           | 시퀀스 증가값 설정   |
| MAXVAULE n \| NOMAXVALUE | 최대값 설정          |
| MINVAULE n \| NOMINVALUE | 최솟값 설정          |


### 함수
- 오라클의 함수를 이용하면 테이블의 데이터를 가공하여 조회 가능
- dual^[^오라클에서 제공하는 한행짜리 테스트 테이블]를 통해서 함수 출력가능
- **함수의 종류**
	- abs(n) : 절대값 
		```sql
		select abs(-13) from dual; -- 13
		```
	- floor(n) : 내림
		```sql
		select floor(123.23232) from dual; --123
		```
	- ceil(n) : 올림
		```sql
		select ceil(1212.23232) from dual; --1213
		```
	- ROUND(n) : 반올림
	- MOD(n) : 나머지 연산
	- TRUNC(value, n) : 해당 값의 n자리 밑으로 잘라냄
	- TRIM : 문자 제거
		- [!] 문자 바로앞에 특수문자 &가 있으면 해당값을 변수로 인식하여 대체변수 입력 대화창이 나옴
		```sql
		SELECT LTRIM('^&^&^&^&^&^&^&^&^&^ABC', '^&') FROM DUAL;
		SELECT RTRIM('ABC@#','@#') FROM DUAL;
		```
	    - LTRIM(원본, 제거할 문자) : 왼쪽
	    - RTRIM(원본, 제거할 문자) : 오른쪽
	- TO_CHAR() : 데이터를 문자 타입으로 변경하는 함수
	- TO_NUMBER() : 데이터를 숫자 타입으로 변환
	    ```sql
	    select to_char(300000, '999,999L') from dual;
	    select to_number('300,000￦','999,999L') from dual;
	    ```
	- TO_DATE() : 데이터를 날짜 타입으로 변환





# 명령어 모음
## TRUNCATE
```sql

```
- 이건 뭐하는 거지?

##  COMMIT
```sql
COMMIT;
```
- 작업 적용하는 키워드로 하나의 트랜직션을 종료시키는 의미를 가지고 있음
- 외부 작업시 반드시 커밋을 적용시킨 후에 외부 작업을 진행해야 혼란을 줄일 수 있음
- 커밋을 하게 되면 세이브 포인트를 통한 [[#ROLLBACK]]이 어려우므로 신중하게 해야함

##  ROLLBACK
```sql
ROLLBACK;
```
- 커밋한 상태 즉, 트랜직션의 시작상태로 되돌리거나 세이브 포인트를 통해 저장해둔 상태로 돌아갈 수 있는 명령어
- 

## show 명령어
- 현재 접속한 계정을 확인하는 명령어
	```sql
	show user;
	```

### show recyclebin : 휴지통 보기
```sql
show recyclebin;
```
- 휴지통에 있는 삭제 테이블 보기

## PURGE RECYCLEBIN : 휴지통 비우기
```sql
PURGE RECYCLEBIN; 
```
- 휴지통 비우기

## FLASHBACK TABLE 테이블명 to BEFORE : 테이블 복구
```sql
FLASHBACK TABLE fruits to BEFORE DROP;
```

## Create
```sql
CREATE TABLE b_member(
    id VARCHAR2(20) PRIMARY key,
    pwd VARCHAR2(20) NOT NULL,
    name VARCHAR2(20) NOT NULL,
    email VARCHAR2(20) DEFAULT 'indopop@naver.com'
);
```
- `칼럼명 데이터유형 NULL?` 순으로 작성해야 함
	- [[#DESC : 테이블에 대한 정보 출력|DESC]]에서 테이블의 정보를 본 것처럼 생성해야함
	- NULL?에 들어가는 데이터
		- NULL : null 값
		- NOT NULL : null 값이 들어가서는 안되는 데이터일때
		- DEFAULT : 기본 값
		- [[#PK와 FK란|PK와 FK]]

### 테이블 복사하기
```sql
-- 서브 쿼리 이용 같은 구조 테이블 생성 가능
CREATE table fruts2 as(select * from fruts where 1 != 1);
insert into fruts2(select * from fruts);
select * from fruts2;
```
- 테이블 복사의 경우 NOT NULL 제약조건은 복사됨
	- 서브쿼리문은 select만 되어서 참인게 다 들어옴
	- 복사했을 경우  NOT NULL과 CHECK이외의 제약조건은 복사가 안되는 것을 확인할 수 있음

##  INSERT INTO
```sql
INSERT INTO b_member VALUES(
    'mc4', '1111', 'name', DEFAULT
);
```
- VALUES()를 이용해 데이터를 삽입
- DEFAULT나 NULL 키워드를 넣을 수 있음

```sql
insert into fruts(qty, price, name) VALUES('10', '5000', '오렌지');
```
- 이런 식으로 칼럼명을 지정해서 해당 순서로 해당 내용에만 데이터를 넣을 수 있음
- 칼럼명 생략시 테이블 생성했을 때의 칼럼 순서대로 데이터를 모두 넣어야 함

## DESC
```sql
DESC employees;
```
- 테이블 구조 확인 명령어
- NOT NULL은 값이 비어있으면 안된다는 표시
- 컬럼명과 데이터 타입이 꼭 있어야함
   ![[Pasted image 20230417124200.png|400]]

## Update
```sql
UPDATE b_member SET name = '김수돌', email='mc@naver.com' where id = 'mc';
```
- 업데이트는 거의 where 조건절과 함께 사용
- 테이블 데이터 수정
	- `UPDATE 테이블명 set 칼럼 = 값 where 조건;`
	- 중요 조건을 만족하는 모든 행을 수정함
	- 조건을 안쓰면 모든 행을 수정
	- 하나의 행을 구분할 수 있는 칼럼이 조건으로 사용되는 경우가 많음 (예. pk)

## DROP
- DB의 오브젝트를 삭제하는 명령어
- DROP을 통해 삭제한다고 해도 [[SQL]]은 쓰레기통이라는 개념이 존재하기 때문에 복원가능
- 테이블 삭제
	```sql
	drop table B_Member;
	```
	- 테이블 칼럼 삭제
		```sql
		ALTER TABLE 테이블명 DROP COLUMN 컬럼명
		```
	- 테이블 제약조건 삭제
		```sql
		ALTER TABLE 테이블명 DROP CONSTRAINT 제약조건명
		```
	- 



## Delete
```sql
delete from b_member where id ='mc';
```
- mc 인 사람의 레코드를 삭제
- 조건을 만족하는 모든 행을 수정
- 조건을 안쓰면 모든 행을 수정

## select
- 조회는 알파벳 순으로 존재
- 해당 테이블의 모든 파일 읽어오기 
	```sql
	select*from employees;--이외에도 가능
	```
	- `*`에는 선택하고 싶은 cloumn 명이 들어감
	- 조회하고 싶은 cloumn은 아래처럼 작성
		```sql
		select first_name,last_name from employees;
		```
- 현재 접속한 계정이 가지고 있는 모든 테이블을 확인하는 명령어
	```sql
	select*from tab;
	```
- 모든 사용자 계정에 대한 정보 확인
	```sql
	select*from all_users;
	```

### AS
```sql
select 
    last_name,
    SALARY/0.8 AS "20퍼센트 삭감"
    from employees;
```
- 띄어쓰기 하려면 `" "`쌍 따음표가 있어야함

### order by
```sql
select*from b_board order by seq desc;
```
- 내림차순 desc  | 오름차순 ASC (기본값)
- 칼럼 순서대로 정렬되며 키워드를 생략했을 경우 ASC로 작동됨
- NULL은 오름차순으로 정렬하면 가장 나중에 출력되고 내림차순으로 정렬하면 가장 먼저 조회됨
- 각각 정렬 주기
	```sql
	SELECT * FROM employees  ORDER BY job_id ASC, hire_date ASC;
	```


### DISTINCT
```sql
select DISTINCT job_id, last_name from employees;
```
- null 값도 중복되면 하나로 출력해줌

### WHERE
```sql
select * from employees where first_name = 'Steven';
```
- select 문에 where 문을 추가하여 해당 조건을 만족하는 행만 조회가능
- 오라클의 비교 연산자들을 활용

### AND, OR, NOT
```sql
select * from employees where hire_date >= '1998/05/01' AND hire_date < '2022/06/01';
select * from employees where job_id = 'IT_PROG' OR job_id = 'ST_CLERK';
select*from employees where not job_id = 'IT_PROG';
```
- 다른 언어에서 사용했던 것과 사용방법은 동일
- not의 사용위치는 비교적 자유로움
	```sql
	select * from employees where salary not BETWEEN 2000 AND 3000;
	select * from employees where not salary BETWEEN 2000 AND 3000;
	```
	- 위 예시처럼 위치가 달라도 동일한 결과값을 출력

### MOD(value1, value2)
```sql
select * from employees where MOD(employee_id, 2) = 0;
```
- employee_id를 2로 나눴을 경우 나머지가 0과 같은 조건의 데이터만 출력

### column BETWEEN 조건 AND 조건
```sql
select*from employees where salary BETWEEN 2000 AND 3000;
```
- 해당 칼럼의 값이 A이상 B 이하인 경우

### IS NULL
```sql
select * from employees where commission_pct IS NULL;
```
- null 값은 비교연산자 사용을 못하기에 is null을 사용해서 조회해야함
- not 연산자와 함께 많이 사용
	```sql
	select * from employees where commission_pct IS NOT NULL;
	```

### ⭐ like : 데이터의 내용 조회
- 데이터의 일부분으로 원하는 내용을 검색할 수 있음
	- vsc의 정규식 같은 느낌
- 문자, 날짜 데이터 타입에 사용할 수 있음 (대소문자 구분됨)
- **와일드 카드**
	-  퍼센트(`%`) : 길이 제한 없이 아무 문자가 와도 상관 없는 와일드 카드
		```sql
		select * from employees where first_name LIKE 'D%'; -- 
		```
		- D로 시작하는 문자열 모두 출력하는 예제
	- 언더바(`_`) : 하나의 문자가 반드시 와야하는 와일드 카드(하나의 문자만 대응)
		```sql
		select * from employees where first_name LIKE '_e%';
		```
		- 두번째 글자가 e로 나오는 뭐든 이름을 찾아 주는 예제
			- 위 예제에서 언더바를 중첩해서 사용하면 언더바를 사용한 만큼의 위치에 있는 e를 찾을 수 있음 (두번째 글자를 찾으려면 언더바 하나)


### NVL(column, value) 
- NVL(column, value) 형식, null Value
	- null 있는 칼럼을 찾아서 해당 값으로 치환해주는 메소드
	- 계산에 사용되는 칼럼의 값에 null 값이 있는 경우 null을 치환할 값을 지정하는 함수
	```sql
	select
		(salary * (1+NVL(commission_pct, 0)))*12 AS "연봉"
		from employees;
	```


### IN(value)
```sql
select first_name, job_id AS "department_name"
from employees where department_id IN(10, 20, 30);
```
- 해당 값을 포함한 것을 출력하는 쿼리문


### 집합
#### UNION
```sql
select * from employees where first_name like 'J%n'
union
select * from employees where first_name like 'J%s';
```
- 합집합으로 첫글자가 J로 시작하는 first_name에서 끝 글자가 n과 s일 경우의 모든 데이터를 불러오는 코드

#### UNION ALL
```sql
select department_id from employees where department_id = 30
union all
select department_id from employees where department_id BETWEEN 10 AND 30;
```
- 위와 다르게 중복 제거 안함

#### INTERSECT
```sql
select department_id from employees where department_id = 30
INTERSECT
select department_id from employees where department_id BETWEEN 10 AND 30;
```
- 교집합

#### MINUS
```sql
select department_id from employees where department_id = 50
MINUS
select department_id from employees where department_id BETWEEN 10 AND 30;
```
- 차집합

### DECODE
```sql
select first_name, job_id, decode(department_id,
    10 , 'Adimn', 20,'Maketing', 30, 'Planning'
    )AS "department_name"
from employees where department_id IN(10, 20, 30);
```
- switch~ case 문과 비슷한 함수로 위처럼 지정한 값을 원하는 이름으로 출력할 수 있음

## ⭐ 서브 쿼리문 
- 하나의 SELECT 문 내부에 포함된 또 하나의 SELECT 문으로 서브쿼리를 포함하고 있는 쿼리를 메인쿼리라고 하며 항상 서브 쿼리가 먼저 실행됨 (사칙연산 생각하면 쉬움)
- 실행결과에 따라 단일행 서브쿼리, 다중행 서브쿼리로 분류됨
	- 단일행 서브쿼리
		- 서브쿼리의 실행결과가 단 하나의 행인 서브쿼리
		- 단일값끼리 비교하는 연산자들을 사용할 수 있음
	- 다중행 서브쿼리
- 자주 함께 사용하는 메소드
	- `IN` : 뒤에 나오는 값이 포함되어 있으면 참
	- `ANY, SOME` : 뒤에 나오는 여러 값 중 하나 이상 조건을 만족시키면 참
	- `ALL` : 뒤에 나오는 여러 값들이 모두 해당 조건을 만족시키면 참

>[!warning] 하나의 쿼리문에 다른 쿼리문을 중첩할 수 있음 (select 문만 가능)
>```sql
> insert into b_board(seq,title,nickname,content)
> values((select nvl(max(seq),0)+1 from b_board),'타이틀','글쓴이','글내용' );


## GROUP BY
- 정의
	- 테이블의 행들을 특정 칼럼 기준으로 그룹화하여 계산하는 함수들
	- 특정 그룹의 종합, 갯수, 평균등을 구하는 함수들
	- 그룹의 기준이 되는 칼럼 GROUP BY열과 함께 사용됨
	- 그룹 함수의 결과는 일반 칼럼과 함께 출력될 수 있음
- 그룹 함수의 종류
	- SUM(column) : 총합
	- AVG(column) : 평균
	- MAX(column) : 최대값
	- MIN(column) : 최소값
	- COUNT(column) : 갯수

>[!example]
>-  job_id를 기준으로 그룹으로 묶어서 각 그룹의 합을 보여주는 쿼리문
>- ```sql
select job_id, SUM(SALARY) from employees GROUP BY job_id;
>-  job_id를 그룹으로 평균 연봉을 구하는 쿼리문
>- ```sql
select job_id, AVG((SALARY*(NVL(commission_pct,0)+1))*12) AS "평균 연봉" from employees GROUP By job_id;``
>- HAVING과 함께 사용하는 쿼리문
>- ```sql 
select job_id, AVG(salary) AS sag_id from employees GROUP BY job_id HAVING AVG(salary) > = 10000;``
> - `where`절과 함께 사용가능


### HAVING
```sql
select job_id, AVG(salary) AS sag_id from employees GROUP BY job_id HAVING AVG(salary) > = 10000;
```
- 그룹 함수에 조건을 줄때 사용하는 명령어


# 용어정리 
- 릴레이션(Relation)
	- 표, 테이블
	- 스키마 :  
	- 인스턴스 : 저장된 스키마에 따라 실제 저장된 값
- 시퀀스 : 번호 생성기


## 릴레이션과 열, 행
![[데이터베이스#테이블 용어정리]]

## PK와 FK란
- PK(primary key) : 해당 테이블에 반드시 존재해야하는 키로 유니크 해야함
- FX(Foreign Key) : 외부 키
- PK와 FK를 묶어서 각각 관리 할 수 있는 방식으로 RDB에서 사용됨
	- 자바처럼 모듈화해서 관리하는 시스템


# 연관문서


