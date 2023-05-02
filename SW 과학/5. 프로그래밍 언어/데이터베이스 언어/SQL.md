---
tag : 데이터베이스 쿼리용_언어 백엔드
aliases : 에스큐엘, 데이터베이스 표준언어
---


# 개요
>[!info] [[데이터베이스]]의 기본 - SQL(에스큐엘, 데이터 베이스 표준언어)
> - SQL은 프로그래밍 언어가 아닌 **쿼리용 언어**
> 	- 관계형 데이터베이스 관리 시스템(RDBMS)를 관리하기 위해 설계된 특수 목적의 프로그래밍 언어
> 	- 쿼리 : RDBMS에서 이해하는 유효한 명령
> 		-  row(행)과 column(열)이 존재
> - DBMS : 오라클 등
> -   ORM(객체 관계)을 이용하면 파이썬 등으로 작업한 코드를 SQL로 변경해줌.
>	-   장점 : 시간 절약가능
>	-   단점 : ORM에 너무 의존하면 SQL에서 어떻게 작동하는 지 생각을 못하게 됨
>		- 풀스택개발자는 SQL의 기초적인 원리를 배워야 한다고 함

>[!cite]- 데이터베이스란?
> ![[데이터베이스#개요]]

# DBMS 설치
>[!quote]- 오라클 11gEE 설치 및 환경변수 설정
> ![[오라클#오라클 설치하기]]

>[!quote] MySQL 설치 및 환경변수 설정
> 1. 설치 페이지 : https://dev.mysql.com/downloads/file/?id=514518
> 2. 환경변수 설정
>	- 고급 시스템 설정 - 환경변수 - 새로 추가 - `C:\Program Files\MySQL\MySQL Server 8.0\bin`(mysqld.exe가 있는 곳으로)
>	- window - R(실행) ->  cmd - `mysql -V` - 성공 문자 확인


# 기본 문법
- 대소문자 구별안함 (데이터 값은 예외)
- `ctrl+enter`로 한줄씩 실행가능
- 기본 지원 : 데이터 타입제공 / 사칙연산 가능 / 메소드 지원

>[!warning] 주의 
>- 변수 개념이 없음
>- SQL에서 무조건 작은 따음표를 사용하고 AS에서 문자열 넣을때만 큰 따음표

## 주석
- 한줄 주석 : `--`
- 여러줄 주석 : `/**/`

## SQL 기본 데이터 타입
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
- 날짜 데이터
	- 거의 문자열과 비슷하게 취급

## SQL 연산자
|     | 설명        |
| --- | ----------- |
| =   | 같으면 true |
| <, >, <=, >= | 크거나 같음 |
| !=, <>, ^= = > |  다르면 true  |


## DML과 DDL, DCL, TCL
  ![[Pasted image 20230428093752.png|400]]
- DDL(데이터 정의어 : Data Definition Language) 
	- 테이블, 시퀀스, 뷰 등 DB에서 사용하는 DB 오브젝트 구조를 생성할때 사용하는 명령어
	- CREATE : DB 오브젝트 생성
	- DROP : DB 오브젝트 삭제
	- ALTER : DB 오브젝트 수정
	- TRUNCATE : DB 오브젝트 완전 삭제
		- DB 데이터 관련된 하나의 트랜직션이 삭제
- DML (데이터 조작 언어 : Data Manipulation Language)
- DCL  (데이터 제어 명령어 : Data Control Language)
	- GRANT : 권한 부여
	- REVOKE : 권한 회수
- TCL (트랜직션 제어 명령어 : Transaction Control Language)

## DDL 명령어
### show 명령어
- 현재 접속한 계정을 확인하는 명령어
	```sql
	show user;
	```
### show recyclebin : 휴지통 보기
```sql
show recyclebin;
```
- 휴지통에 있는 삭제 테이블 보기

### PURGE RECYCLEBIN : 휴지통 비우기
```sql
PURGE RECYCLEBIN; 
```
- 휴지통 비우기

### FLASHBACK TABLE 테이블명 to BEFORE : 테이블 복구
```sql
FLASHBACK TABLE fruits to BEFORE DROP;
```


## DML 명령어
####  INSERT INTO 테이블명 VALUES() : 데이터 생성
```sql
INSERT INTO b_member VALUES(
    'mc4', '1111', 'name', DEFAULT
);
```
- VALUES()를 이용해 데이터를 삽입
- DEFAULT나 NULL 키워드를 넣을 수 있음

### DESC : 테이블에 대한 정보 출력
```sql
DESC employees;
```
- 테이블에 대한 정보를 줄력
- NOT NULL은 값이 비어있으면 안된다는 표시
- 컬럼명과 데이터 타입이 꼭 있어야함

   ![[Pasted image 20230417124200.png|400]]


### select : 데이터 읽기
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

#### AS : 칼럼을 원하는 이름으로 생성 후 조회할 수 있음
```sql
select 
    last_name,
    SALARY/0.8 AS "20퍼센트 삭감"
    from employees;
```
- 띄어쓰기 하려면 `" "`쌍 따음표가 있어야함

#### order by : 정렬
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


#### DISTINCT : 중복값 제거
```sql
select DISTINCT job_id, last_name from employees;
```
- null 값도 중복되면 하나로 출력해줌

#### WHERE : 조건문
```sql
select * from employees where first_name = 'Steven';
```
- select 문에 where 문을 추가하여 해당 조건을 만족하는 행만 조회가능
- 오라클의 비교 연산자들을 활용

##### AND, OR, NOT
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

##### MOD(value1, value2) : 나머지 구하기
```sql
select * from employees where MOD(employee_id, 2) = 0;
```
- employee_id를 2로 나눴을 경우 나머지가 0과 같은 조건의 데이터만 출력

##### column BETWEEN 조건 AND 조건 : 조건과 조건을 만족할 때
```sql
select*from employees where salary BETWEEN 2000 AND 3000;
```
- 해당 칼럼의 값이 A이상 B 이하인 경우

##### IS NULL : null 조회가능
```sql
select * from employees where commission_pct IS NULL;
```
- null 값은 비교연산자 사용을 못하기에 is null을 사용해서 조회해야함
- not 연산자와 함께 많이 사용
	```sql
	select * from employees where commission_pct IS NOT NULL;
	```

##### ⭐ like : 데이터의 내용 조회
- 데이터의 일부분으로 원하는 내용을 검색할 수 있음
- 문자, 날짜 데이터 타입에 사용할 수 있음 (대소문자 구분됨)
- vsc의 정규식 같은 느낌
- 와일드 카드
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


##### NVL(column, value) 
- NVL(column, value) 형식, null Value
	- null 있는 칼럼을 찾아서 해당 값으로 치환해주는 메소드
	- 계산에 사용되는 칼럼의 값에 null 값이 있는 경우 null을 치환할 값을 지정하는 함수
	```sql
	select
		(salary * (1+NVL(commission_pct, 0)))*12 AS "연봉"
		from employees;
	```


##### IN(value)
```sql
select first_name, job_id AS "department_name"
from employees where department_id IN(10, 20, 30);
```
- 해당 값을 포함한 것을 출력하는 쿼리문


#### 집합
##### UNION : 합집합
```sql
select * from employees where first_name like 'J%n'
union
select * from employees where first_name like 'J%s';
```
- 합집합으로 첫글자가 J로 시작하는 first_name에서 끝 글자가 n과 s일 경우의 모든 데이터를 불러오는 코드

##### UNION ALL
```sql
select department_id from employees where department_id = 30
union all
select department_id from employees where department_id BETWEEN 10 AND 30;
```
- 위와 다르게 중복 제거 안함

##### INTERSECT : 교집합
```sql
select department_id from employees where department_id = 30
INTERSECT
select department_id from employees where department_id BETWEEN 10 AND 30;
```
- 교집합

##### MINUS : 차집합
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

### GROUP BY 그룹 함수
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


### HAVING : 그룹함수에 조건을 줄 때
```sql
select job_id, AVG(salary) AS sag_id from employees GROUP BY job_id HAVING AVG(salary) > = 10000;
```
- 그룹 함수에 조건을 줄때 사용하는 명령어


## 서브 쿼리문
- 하나의 쿼리문에 다른 쿼리문을 중첩할 수 있음 (select 문만 가능)
```sql
insert into b_board(seq,title,nickname,content)
values((select nvl(max(seq),0)+1 from b_board),'타이틀','글쓴이','글내용' );
```
- values 앞에 띄워쓰기 해줘야함

```sql
-- 서브 쿼리 이용 같은 구조 테이블 생성 가능
CREATE table fruts2 as(select * from fruts where 1 != 1);
insert into fruts2(select * from fruts);
select * from fruts2;
```

# CRUD
>[!cite]- CRUD란?
>![[CRUD#개요]]

## Create
### 테이블 생성
```sql
CREATE TABLE b_member(
    id VARCHAR2(20) PRIMARY key,
    pwd VARCHAR2(20) NOT NULL,
    name VARCHAR2(20) NOT NULL,
    email VARCHAR2(20) DEFAULT 'indopop@naver.com'
);
```

- [[SQL#DESC : 테이블에 대한 정보 출력|DESC]]에서 테이블의 정보를 본 것처럼 생성해야함
- `칼럼명 데이터유형 NULL?` 순으로 작성해야 함
	- 데이터유형은 SQL 기본 데이터처럼?
	- NULL?에 들어가는 데이터
		- NULL : null 값
		- NOT NULL : null 값이 들어가서는 안되는 데이터 일때
		- DEFAULT : 기본 값
		- PK, FK ![[SQL#PK와 FK란]]
###  데이터 생성
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


###  COMMIT
```sql
COMMIT;
```
- 작업 적용하는 키워드
- 외부 작업시 반드시 커밋을 적용시켜줘야함
- 커밋을 하게 되면 다시 롤백이 어려우므로 신중하게 해야함

###  ROLLBACK
```sql
ROLLBACK;
```
- 커밋한 상태로 되돌릴 수 있음

## Read
- select 구문

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

## Delete
### 테이블 삭제 (DROP)
```sql
drop table B_Member;
```
- B_Member 테이블 자체 삭제

### 데이터 삭제
```sql
delete from b_member where id ='mc';
```
- mc 인 사람의 레코드를 삭제
- 조건을 만족하는 모든 행을 수정
- 조건을 안쓰면 모든 행을 수정



# 데이터 딕셔너리(Data Dictionary) 
- 시스템 카탈로그라고 부르며 사용가능한 데이터베이스 및 테이블의 정보를 가지고 있는 시스템 테이블
- DBMS만이 추가, 수정, 삭제가 가능하고 사용자는 조회만 가능
- 오라클의 데이터 딕셔너리
  ![[Pasted image 20230502091637.png|200]]

## 데이터 제약조건
- 데이터 무결성 : 데이터에 결함이 존재해서는 안됨
	- 데이터에 결함이 없는 성질
	- 정확성, 일관성, 유효성이 유지되는 데이터를 말함
	 - 데이터 무결성 제약 조건
		- NOT NOLL : 해당 도메인에 null을 허용하지 않음
		- UNIQUE : 해당 도메인에 중복되는 값을 허용하지 않음
		- primary key : 해당 도메인을 테이블의 기본 키로 사용 UNIQUTE = NOT null
		- CHECK : 원하는 조건을 지정, 도메인 무결성을 유지함
- 개체 무결성
	- 테이블의 데이터 = 반드시 한 행을 구분할 수 있어야함
	- 테이블의 개체 무결성을 지키기 위한 제약조건 = PK 사용
	- 주의! 객체라고 하면 안되는 이유 :  한 컬럼값으로 묶어져있기 때문에 #질문 
- 참조 무결성
	- 참조 관계에 있는 데이터는 항상 일관된 값을 가져야함
	- 참조 무결성을 지키기 위한 제약조건 = FK 사용
	- JOIN을 통해서 FK와 PK를 연결해줄 수 있음
	- e.g. departments에서 departments_id는 PK이고 employess에서는 departments_id는 FK로 되어있음

## 키에 대해서


### 생성과 동시에 제약 걸기
```sql
-- CONSTRAINT 실습
select * from fruites5;

create table fruites5(
    fid     number(4) -- PK
        CONSTRAINT f5_fid_pk        PRIMARY KEY,
    fname   varchar2(20)
        CONSTRAINT f5_fname_uk      UNIQUE
        CONSTRAINT f5_fname_nn  NOT NULL,
    grade   varchar2(2)
        CONSTRAINT f5_grade_chk     CHECK(grade IN('A+','A','B+','B')),
    fsize     number(2)
        CONSTRAINT f5_fsize_chk     CHECK(fsize BETWEEN 0 AND 20)
);
select * from user_constraints where table_name = 'FRUITES5';
```


# 용어정리

## 릴레이션과 열, 행
![[데이터베이스#테이블 용어정리]]

## PK와 FK란
- PK(primary key) : 해당 테이블에 반드시 존재해야하는 키로 유니크 해야함
- FX(Foreign Key) : 외부 키
- PK와 FK를 묶어서 각각 관리 할 수 있는 방식으로 RDB에서 사용됨
	- 자바처럼 모듈화해서 관리하는 시스템


# 연관문서