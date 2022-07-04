---
title: Oracle 수업자료
date: 2021-06-10
---
# DataBase

- `검색이 용이`하도록 일정한 기준에 맞추어 자료를 분류하여 정리한 `자료의 집합`

### 데이터베이스 조건
- 실시간 접근성
- 지속적인 변화
- 동시 공유


### RDBMS(Relational Database Management System)

- 데이터가 column과 row로 (행과 열)이루어진 테이블에 저장되며, 테이블들 사이에 관께를 설정하여 관리 SW또는 시스템을 말한다.

### SQL (Structured Query Language)

- RDBMS에 데이터 `입력,수정,삭제,검색`하는 기능을 가진 관리 언어.
- `절차적 언어`가 아닌 `구조적 언어`이다.
	- 절차적(procedural) 언어
		- 모든 처리 과정을 일일이 기술하고 기술된 순서대로 로직이 처리되는 언어. (C, Java 등)
	- 구조적(structured) 언어
		- 처리 과정을 일일이 기술할 필요 없이 일정한 틀이나 패턴이 있어 맞게 조건들만 나열하면 로직이 처리되는 언어.


### SQL의 종류

- DDL(Data Definition Language, 데이터 정의 언어) : 객체 생성, 삭제, 수정등의 작업진행
    - CREATE
    - ALTER
    - DROP
    > DB에서의 객체는 이름을 가지고 저장되는 요소들. (ex. 테이블,뷰,트리거,인덱스,프로시저 등.)

- DML(Data Manipulation Language, 데이터 처리 언어) : 테이블 내부의 데이터 입력,수정,삭제,검색을 함.
    - INSERT
    - UPDATE
    - DELETE
    - SELECT

- DCL(Data Control Language, 데이터 제어 언어) : 
    - COMMIT - 트랜잭션 작업 단위의 데이터 입력,수정,삭제작업 모두 인정
    - ROLLBACK - 트랜잭션 작업 단위의 데이터 입력,수정,삭제작업 모두 취소
    - GRANT - 접근제어, 권한부여
    - REVOKE - 권한제거
> 트랜잭션(Transaction)은 데이터베이스의 상태를 변환시키는 하나의 논리적 기능을 수행하기 위한 작업의 단위 또는 한꺼번에 모두 수행되어야 할 일련의 연산들을 의미한다. (일종의 스냅샷)
- 명령의 단위로, 트랜잭션이 걸려있는 입출력과 수정작업은 가상의 상태로 명령을 실행한다.
- COMMIT혹은 ROLLBACK으로 단위작업을 실행하거나 취소한다.


### DB 사용자
- DB는 많은 사용자가 동시에 접속이 가능하다
- 사용자마다 접속에 대한 권한을 다르게 줄 수 있다.

- 오라클의 계정 종류
  
|계정|설명|
|:------------:|--------------------------------------------------|
|SYS|시스템 최고 권한을 가진, 기본 계정|
|SYSTEM|오라클 설치 시 기본적으로 만들어지는 계정으로 `데이터베이스 생성 권한`을 제외하고 전부 가능|
|생성계정| 계정 생성 권한을 가진 계정이 만드는 계정이므로 계정별 권한이 다르다.|


### 스키마(Schema)
- 데이터베이스의 구조`에 대한 정의와 제약조건 등을 기술한 `명세서`를 말한다
- 계정이 생성한 모든 객체들을 의미 (오라클 객체는 테이블,뷰,인덱스, 프로시져, 트리거) 객체들이 DB 구조에 대한 정의와 이에 대한 제약조건등을 기술한 `명세서` 이기 때문.
- 생성되는 객체는 [계정명.객체명]의 형식으로 저장된다.

### 테이블(table)
- RDBMS 에서 데이터가 실질적으로 저장되는 `논리적 장소`
- column과 row로 구성
- 데이터베이스 객체의 한 종류
- DML(Data Manipulation Language)을 통해 제어한다.

#### 테이블의 생성
```sql
CREATE `테이블명`(
    컬럼명1 자료형 제약조건
    ,컬럼명2 자료형 제약조건
    ,컬럼명3 자료형 제약조건
);
```

- `컬럼 명` : 컬럼(필드,속성)의 이름.
- `자료형(Data Type)` : 테이블 칼럼에 입력될 데이터의 유형( 문자, 숫자, 날짜 등).
- `제약조건` : 데이터의 무결성을 지키기위한 도메인을 결정하기 위한 조건.

#### 컨벤션 ( 테이블명, 컬럼 명명 규칙)
- `영문자 1~9,$,#,_`로 구성하고 `영문자로 시작`해야 함.
- `30자를` 초과할 수 없고, `SQL예약어`를 사용 할 수 없음
- 하나의 계정이 만든 테이블명을 `유일`해야 하고, 테이블 안에서 컬럼명은 `유일`해야함.
- 테이블명, 컬럼명, 제약조건명을 "로 감싸거나 "없이 써도 됨.
- 테이블을 쉽게 유추할 수 있는 가독성있는 이름을 지정










### 시퀀스(sequence)
- `고유 일련번호`를 생성해서 제공하는 객체, 일종의 일련번호 생성기
- 주로 하나의 테이블에서 `PRIMARY KEY`로 지정된 컬럼명에 입력될 `일련번호`를 생성함.

```sql
    create sequence 시퀀스명
        start with 시작값
        increment by 증가값
        minvalue 최소값
        maxvalue 최대값;

-- 증가된 새 일련번호를 얻는 SQL구문
시퀀스명.nextval
-- 마지막으롤 생성했던 일련번호를 얻는 SQL구문
시퀀스명.currval
-- 시퀀스 삭제 SQL구문
drop sequence 시퀀스명;
```
- 입력 실패시 건너뛰어지는 문제가 생긴다.


### 계정생성

```sql
CREATE USER scott IDENTIFIED BY tiger;
```
- 계정 scott를 pw tiger로 생성

### 권한 부여

```sql
GRANT CONNECT,resource,dba TO SCOTT;
```
- `GRANT`명령어로 권한부여


```sql
CREATE TABLE dept(
	dept_no NUMBER(10) NOT NULL
	,dept_name VARCHAR2(10) NOT NULL UNIQUE
	,loc VARCHAR2(10) NOT NULL
	,PRIMARY KEY(dept_no)
);

-- 데이터 삽입
INSERT INTO dept(dept_no,dept_name,loc)
VALUES (10,'총무부','서울');
INSERT INTO dept(dept_no,dept_name,loc)
VALUES (20,'영업부','부산');
INSERT INTO dept(dept_no,dept_name,loc)
VALUES (30,'전산부','대전');
INSERT INTO dept(dept_no,dept_name,loc)
VALUES (40,'자재부','광주');

SELECT * FROM dept;



CREATE TABLE emp( emp_no NUMBER(3) ,
emp_name VARCHAR2(20) ,
dept_no NUMBER(10) NOT NULL ,
jikup VARCHAR2(20) NOT NULL ,
salary NUMBER(10) DEFAULT 0 ,
hire_date DATE DEFAULT sysdate ,
jumin_num CHAR(13) NOT NULL UNIQUE ,
phone_num VARCHAR(15) NOT NULL ,
mgr_emp_no NUMBER(3) ,
PRIMARY KEY(emp_no) ,
FOREIGN KEY(dept_no) REFERENCES dept(dept_no) ,
CONSTRAINT emp_mrg_no_fk FOREIGN KEY(mgr_emp_no) REFERENCES emp(emp_no)
-- 제약조건의 이름 붙이기/제약조건의 무력화를 위해 이름을 붙임
);

ALTER TABLE

DROP TABLE emp;
DROP TABLE dept;
-- 테이블 삭제


ALTER TABLE EMP disable CONSTRAINT emp_mrg_no_fk;
-- 제약조건 무력화

ALTER TABLE EMP enable CONSTRAINT emp_mrg_no_fk;
-- 제약조건 원복

INSERT INTO EMP 
VALUES( 1, '홍길동', 10, '사장', 5000, '1980-01-01', '7211271109410', '01099699515', null );
INSERT INTO EMP 
VALUES( 2, '한국남', 20, '부장', 3000, '1988-11-01', '6002061841224', '01024948424', 1 );
INSERT INTO EMP 
VALUES( 3, '이순신', 20, '과장', 3500, '1989-03-01', '6209172010520', '01026352672', 2 );
INSERT INTO EMP 
VALUES( 4, '이미라', 30, '대리', 2503, '1983-04-01', '8409282070226', '01094215694', 17 );
INSERT INTO EMP
VALUES( 5, '이순라', 20, '사원', 1200, '1990-05-01', '8401041483626', '01028585900', 3 );
INSERT INTO EMP 
VALUES( 6, '공부만', 30, '과장', 4003, '1995-05-01', '8402121563616', '01191338328', 17 );
INSERT INTO EMP 
VALUES( 7, '놀기만', 20, '과장', 2300, '1996-06-01', '8011221713914', '01029463523', 2 );
INSERT INTO EMP 
VALUES( 8, '채송화', 30, '대리', 1703, '1992-06-01', '8105271014112', '01047111052', 17 );
INSERT INTO EMP 
VALUES( 9, '무궁화', 10, '사원', 1100, '1984-08-01', '8303291319116', '01025672300', 12 );
INSERT INTO EMP 
VALUES( 10, '공부해', 30, '사원', 1303, '1988-11-01', '8410031281312', '01027073174', 4 );
INSERT INTO EMP 
VALUES( 11, '류별나', 20, '과장', 1600, '1989-12-01', '8409181463545', '01071628290', 2 );
INSERT INTO EMP 
VALUES( 12, '류명한', 10, '대리', 1800, '1990-10-01', '8207211661117', '01042072622', 20 );
INSERT INTO EMP 
VALUES( 13, '무궁화', 10, '부장', 3000, '1996-11-01', '8603231183011', '01098110955', 1 );
INSERT INTO EMP 
VALUES( 14, '채시라', 20, '사원', 3400, '1993-10-01', '8001172065410', '01044452437', 3 );
INSERT INTO EMP 
VALUES( 15, '최진실', 10, '사원', 2000, '1991-04-01', '8303101932611', '01027491145', 12 );
INSERT INTO EMP 
VALUES( 16, '김유신', 30, '사원', 4000, '1981-04-01', '7912031009014', '01098218448', 4 );
INSERT INTO EMP 
VALUES( 17, '이성계', 30, '부장', 2803, '1984-05-01', '8102261713921', '0165358075', 1 );
INSERT INTO EMP 
VALUES( 18, '강감찬', 30, '사원', 1003, '1986-07-01', '8203121977315', '01033583130', 4 );
INSERT INTO EMP 
VALUES( 19, '임꺽정', 20, '사원', 2200, '1988-04-01', '8701301040111', '01086253078', 7 );
INSERT INTO EMP 
VALUES( 20, '깨똥이', 10, '과장', 4500, '1990-05-01', '8811232452719', '01090084876', 13 );


SELECT * FROM emp;

--DELETE FROM EMP;
-- 모든 튜플 삭제
```








