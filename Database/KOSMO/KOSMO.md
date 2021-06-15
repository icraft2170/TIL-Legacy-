---
title:kosmo sql
---

```sql
DROP TABLE CUSTOMER;
DROP TABLE emp;
DROP TABLE dept;

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

CREATE SEQUENCE emp_sq
START WITH 1
INCREMENT BY 1
MINVALUE 1
MAXVALUE 999;



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

--ALTER TABLE
--
--DROP TABLE emp;
--DROP TABLE dept;
-- 테이블 삭제


ALTER TABLE EMP disable CONSTRAINT emp_mrg_no_fk;
-- 제약조건 무력화

--ALTER TABLE EMP enable CONSTRAINT emp_mrg_no_fk;
-- 제약조건 원복


INSERT INTO EMP 
VALUES( emp_sq.nextval, '홍길동', 10, '사장', 5000, '1980-01-01', '7211271109410', '01099699515', null );
INSERT INTO EMP 
VALUES( emp_sq.nextval, '한국남', 20, '부장', 3000, '1988-11-01', '6002061841224', '01024948424', 1 );
INSERT INTO EMP 
VALUES( emp_sq.nextval, '이순신', 20, '과장', 3500, '1989-03-01', '6209172010520', '01026352672', 2 );
INSERT INTO EMP 
VALUES( emp_sq.nextval, '이미라', 30, '대리', 2503, '1983-04-01', '8409282070226', '01094215694', 17 );
INSERT INTO EMP
VALUES( emp_sq.nextval, '이순라', 20, '사원', 1200, '1990-05-01', '8401041483626', '01028585900', 3 );
INSERT INTO EMP 
VALUES( emp_sq.nextval, '공부만', 30, '과장', 4003, '1995-05-01', '8402121563616', '01191338328', 17 );
INSERT INTO EMP 
VALUES( emp_sq.nextval, '놀기만', 20, '과장', 2300, '1996-06-01', '8011221713914', '01029463523', 2 );
INSERT INTO EMP 
VALUES( emp_sq.nextval, '채송화', 30, '대리', 1703, '1992-06-01', '8105271014112', '01047111052', 17 );
INSERT INTO EMP 
VALUES( emp_sq.nextval, '무궁화', 10, '사원', 1100, '1984-08-01', '8303291319116', '01025672300', 12 );
INSERT INTO EMP 
VALUES( emp_sq.nextval, '공부해', 30, '사원', 1303, '1988-11-01', '8410031281312', '01027073174', 4 );
INSERT INTO EMP 
VALUES( emp_sq.nextval, '류별나', 20, '과장', 1600, '1989-12-01', '8409181463545', '01071628290', 2 );
INSERT INTO EMP 
VALUES( emp_sq.nextval, '류명한', 10, '대리', 1800, '1990-10-01', '8207211661117', '01042072622', 20 );
INSERT INTO EMP 
VALUES( emp_sq.nextval, '무궁화', 10, '부장', 3000, '1996-11-01', '8603231183011', '01098110955', 1 );
INSERT INTO EMP 
VALUES( emp_sq.nextval, '채시라', 20, '사원', 3400, '1993-10-01', '8001172065410', '01044452437', 3 );
INSERT INTO EMP 
VALUES( emp_sq.nextval, '최진실', 10, '사원', 2000, '1991-04-01', '8303101932611', '01027491145', 12 );
INSERT INTO EMP 
VALUES( emp_sq.nextval, '김유신', 30, '사원', 4000, '1981-04-01', '7912031009014', '01098218448', 4 );
INSERT INTO EMP 
VALUES( emp_sq.nextval, '이성계', 30, '부장', 2803, '1984-05-01', '8102261713921', '0165358075', 1 );
INSERT INTO EMP 
VALUES( emp_sq.nextval, '강감찬', 30, '사원', 1003, '1986-07-01', '8203121977315', '01033583130', 4 );
INSERT INTO EMP 
VALUES( emp_sq.nextval, '임꺽정', 20, '사원', 2200, '1988-04-01', '8701301040111', '01086253078', 7 );
INSERT INTO EMP 
VALUES( emp_sq.nextval, '깨똥이', 10, '과장', 4500, '1990-05-01', '8811232452719', '01090084876', 13 );
-- 시퀀스 사용시 데이터 입력 실패시 번호를 건너 뛰어 넘어가는 문제가 생길 수 있음

SELECT * FROM emp;

--DELETE FROM EMP;
-- 모든 튜플 삭제


CREATE SEQUENCE cus_sq
START WITH 1
INCREMENT BY 1
MINVALUE 1
MAXVALUE  999;


CREATE  TABLE customer (
	cus_no number(3)
	,cus_name varchar2(10) NOT NULL
	,tel_num varchar2(15)
	, jumin_num char(13) NOT NULL UNIQUE
	,emp_no number(3)
	,PRIMARY KEY(cus_no)
	,FOREIGN KEY(emp_no) REFERENCES EMP(emp_no)
);


--DELETE FROM customer;

insert into customer values( cus_sq.nextval, '류민이', '123-1234', '7001131537915', 3);
insert into customer values( cus_sq.nextval, '이강민', '343-1454', '6902161627914', 2);
insert into customer values( cus_sq.nextval, '이영희', '144-1655', '7503202636215', null);
insert into customer values( cus_sq.nextval, '김철이', '673-1674', '7704301234567', 4);
insert into customer values( cus_sq.nextval, '박류완', '123-1674', '7205211123675', 3);
insert into customer values( cus_sq.nextval, '서캔디', '673-1764', '6507252534566', null);
insert into customer values( cus_sq.nextval, '신똘이', '176-7677', '0006083648614', 7);
insert into customer values( cus_sq.nextval, '도쇠돌', '673-6774', '0008041346574', 9);
insert into customer values( cus_sq.nextval, '권홍이', '767-1234', '7312251234689', 13);
insert into customer values( cus_sq.nextval, '김안나', '767-1677', '7510152432168', 4);


--SELECT * FROM CUSTOMER;

CREATE TABLE salary_grade(
	sal_grade_no number(2) PRIMARY KEY
	,min_salary number(5) NOT NULL
	,max_salary number(5) NOT NULL
);

INSERT INTO salary_grade 
values(1,8000,10000);
INSERT INTO salary_grade 
values(2,6000,7999);
INSERT INTO salary_grade 
values(3,4000,5999);
INSERT INTO salary_grade 
values(4,2000,3999);
INSERT INTO salary_grade 
values(5,1000,1999);

SELECT emp_name
FROM EMP
WHERE (salary*12)>=3000;

SELECT *
FROM emp
ORDER BY DEPT_NO ASC, (SALARY*12) DESC; 

SELECT *
FROM EMP
WHERE JIKUP ='과장' AND SALARY >=3400;

SELECT *
FROM EMP
WHERE (SALARY*0.88)>=4000

SELECT EMP_NAME , SALARY*0.12 AS 세금 
FROM EMP
WHERE JIKUP ='사원'
ORDER BY 세금 ASC,DEPT_NO DESC;




SELECT *
FROM EMP
WHERE DEPT_NO ='20' AND SALARY BETWEEN 2000 AND 3000;

SELECT *
FROM EMP e 
WHERE MGR_EMP_NO IS NULL;

SELECT *
FROM EMP e 
WHERE MGR_EMP_NO IS NOT NULL;



```