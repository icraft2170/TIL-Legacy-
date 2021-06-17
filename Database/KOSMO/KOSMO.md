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

--DROP TABLE CUSTOMER;
--DROP TABLE emp;
--DROP TABLE dept;

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

-- 오라클의 함수는 반드시 리턴값이 존재
SELECT MAX(SALARY) AS "최대 연봉",MIN(SALARY) AS "최소 연봉",AVG(NVL(SALARY,0)) AS "평균 연봉",SUM(SALARY) AS "연봉 총합",COUNT(EMP_NO) AS "총 인원수"
FROM EMP;

SELECT count(DISTINCT emp_no)
FROM CUSTOMER;

SELECT *
FROM emp;

SELECT COUNT(MGR_EMP_NO)
FROM emp;

SELECT emp_no AS "직원 번호", emp_name AS "직원 이름",SUBSTR(JUMIN_NUM,3,2)||'-'||SUBSTR(JUMIN_NUM,5,2) "생일 월 일" 
FROM emp;
-- substr(컬럼,순서 번호,개수)

SELECT SUBSTR(JUMIN_NUM,1,6)||'-'||'********'
FROM emp;

SELECT CUS_NO ,CUS_NAME ,NVL(TO_CHAR(EMP_NO),'없음') 
FROM  CUSTOMER;

SELECT CUS_NO ,CUS_NAME ,NVL2(EMP_NO,'있음','없음') 
FROM  CUSTOMER;
--- nvl2(컬럼,널이 아닐 때 대체값, 널일 때 대체 값)


SELECT emp_no, emp_name,JIKUP,CASE SUBSTR(JUMIN_NUM,7,1) WHEN '1' THEN '남' 
														WHEN '2' THEN '여'
														WHEN '3' THEN '남'
														WHEN '4' THEN '여' END 
FROM emp;

SELECT emp_no, emp_name,JIKUP,CASE WHEN  SUBSTR(JUMIN_NUM,7,1) = '1' THEN '남' 
									WHEN SUBSTR(JUMIN_NUM,7,1) = '2' THEN '여'
									WHEN SUBSTR(JUMIN_NUM,7,1) = '3' THEN '남'
									WHEN SUBSTR(JUMIN_NUM,7,1) = '4' THEN '여' END 
FROM emp;


SELECT emp_no, emp_name,JIKUP,DECODE(
							SUBSTR(JUMIN_NUM,7,1)
							,1,'남자'
							,3,'남자'
							,'여자') 
FROM emp;



SELECT emp_no AS "직원 번호"
		,emp_name AS "직원 명"
		,JIKUP AS "직급"
		,CASE SUBSTR(JUMIN_NUM,7,1)
		WHEN '1' THEN '19'||SUBSTR(JUMIN_NUM,1,2)
		WHEN '2' THEN '19'||SUBSTR(JUMIN_NUM,1,2)
		ELSE  '20'||SUBSTR(JUMIN_NUM,1,2)
		END
FROM emp;


SELECT emp_no AS "직원 번호"
		,emp_name AS "직원 명"
		,JIKUP AS "직급"
		,TO_DATE(SUBSTR(JUMIN_NUM,1,2),'RR')  
FROM emp;

SELECT emp_no AS "직원 번호"
		,emp_name AS "직원 명"
		,JIKUP AS "직급"
		,CASE SUBSTR(JUMIN_NUM,7,1)
		WHEN '1' THEN '19'
		WHEN '2' THEN '19'
		ELSE  '20'
		END||SUBSTR(JUMIN_NUM,1,2) AS "생년"
FROM emp;


SELECT emp_no AS "직원 번호"
		,emp_name AS "직원 명"
		,JIKUP AS "직급"
		,DECODE(SUBSTR(JUMIN_NUM,7,1),1,'19',2,'19','20')||SUBSTR(JUMIN_NUM,1,2) AS "생년"
	FROM emp;


SELECT emp_no AS "직원 번호"
		,emp_name AS "직원 명"
		,JIKUP AS "직급"
		,TO_CHAR(TO_DATE(SUBSTR(JUMIN_NUM,1,2),'RR'),'RRRR') AS "생년"
FROM emp;

SELECT emp_no AS "직원 번호"
		,emp_name AS "직원 명"
		,JIKUP AS "직급"
		,DECODE(SUBSTR(JUMIN_NUM,7,1),1,'19',2,'19','20')||'00' AS "생년"
	FROM emp;

SELECT *
FROM emp
ORDER BY SALARY DESC;
	

SELECT *
FROM emp
ORDER BY jumin_num desc


SELECT *
FROM emp
ORDER BY CASE SUBSTR(JUMIN_NUM,7,1)
		WHEN '1' THEN '19'
		WHEN '2' THEN '19'
		ELSE  '20' END || SUBSTR(JUMIN_NUM,1,6); 
	
SELECT e.EMP_NAME, e.JIKUP
FROM emp e
ORDER BY CASE JIKUP 
		WHEN '사장' THEN 1
		WHEN  '부장' THEN 2
		WHEN  '과장' THEN 3
		WHEN  '대리' THEN 4
		WHEN '주임' THEN 5 ELSE 6
		END;

	
	SELECT EMP_NO AS "직원 번호", EMP_NAME AS "직원 명", TO_CHAR(HIRE_DATE,'RR-MM-DD')  
	FROM emp;
	
	
	SELECT EMP_NO AS "직원 번호", EMP_NAME AS "직원 명", TRUNC(MONTHS_BETWEEN(SYSDATE,TO_DATE(19||SUBSTR(JUMIN_NUM,1,6))+1)/12) AS "나이" 
	FROM emp
	
	
	SELECT EMP_NO AS "직원번호"
	, EMP_NAME AS "직원번호"
	, EMP_NAME AS "직원명"
	, TRUNC(MONTHS_BETWEEN(SYSDATE, HIRE_DATE)/12)+1||'년차' AS "근무년차" 
	FROM EMP;

	SELECT EMP_NO AS "직원번호"
	, EMP_NAME AS "직원번호"
	, EMP_NAME AS "직원명"
	, CEIL((SYSDATE-HIRE_DATE)/365)||'년차' AS "근무년차" 
	FROM EMP;



SELECT EMP_NO AS 직원번호
,EMP_NAME AS 직원이름 
, SUBSTR(to_char(SYSDATE,'RRRR') - TO_CHAR(TO_DATE(SUBSTR(JUMIN_NUM,1,2),'RR'),'RRRR'),1,1)||'0' AS 연령대
FROM EMP;


SELECT EMP_NO AS 직원번호
,EMP_NAME AS 직원이름 
, SUBSTR(to_char(SYSDATE,'RRRR') - TO_CHAR(TO_DATE(SUBSTR(JUMIN_NUM,1,2),'RR'),'RRRR'),1,1)||'0' AS 연령대
FROM EMP;


SELECT EMP_NO AS 직원번호
,EMP_NAME AS 직원이름 
, FLOOR(TO_NUMBER(to_char(SYSDATE,'RRRR') - TO_CHAR(TO_DATE(SUBSTR(JUMIN_NUM,1,2),'RR')
																,'RRRR') AS 연령대
FROM EMP;



SELECT EMP_NO AS 직원번호
,EMP_NAME AS 직원이름 
,TO_CHAR(TO_DATE(SUBSTR(JUMIN_NUM,1,6),'RRMMDD') + 100,'RRRR-MM-DD') 																
FROM EMP;


SELECT TO_DATE('2021-11-10','RRRR-MM-DD')-TO_DATE('2021-05-12','RRRR-MM-DD')
FROM dual;

SELECT EMP_NO AS "직원 번호"
		, EMP_NAME AS "직원 명"
		, TRUNC(MONTHS_BETWEEN(SYSDATE,TO_DATE(19||SUBSTR(JUMIN_NUM,1,6)))/12+1)||'살' AS "현재 나이"		
		, TRUNC((MONTHS_BETWEEN(SYSDATE,TO_DATE(19||SUBSTR(JUMIN_NUM,1,6)))/12+1)- (MONTHS_BETWEEN(SYSDATE,HIRE_DATE)/12))||'살' AS "입사일 당시 나이"
FROM EMP;

SELECT EMP_NO AS 직원번호
		,EMP_NAME AS 직원이름
		,JUMIN_NUM AS 주민번호
		,CASE
		WHEN SYSDATE-TO_DATE(SUBSTR(JUMIN_NUM,3,4),'MMDD') >=0 
		THEN TO_DATE(SUBSTR(JUMIN_NUM,3,4),'MMDD')+365
		ELSE TO_DATE(SUBSTR(JUMIN_NUM,3,4),'MMDD')
		END
		AS "다가올 생일"
		,CASE
		WHEN SYSDATE-TO_DATE(SUBSTR(JUMIN_NUM,3,4),'MMDD') >=0 
		THEN (TO_DATE(SUBSTR(JUMIN_NUM,3,4),'MMDD')+365) - SYSDATE
		ELSE TO_DATE(SUBSTR(JUMIN_NUM,3,4),'MMDD') - SYSDATE
		END
		AS "남은 일수"
FROM EMP;



SELECT EMP_NO AS 직원번호
		,EMP_NAME AS 직원이름
		,JUMIN_NUM AS 주민번호
		,CASE
		WHEN SYSDATE-TO_DATE(SUBSTR(JUMIN_NUM,3,4),'MMDD') >=0 
		THEN TO_DATE(SUBSTR(JUMIN_NUM,3,4),'MMDD')+(INTERVAL '1' YEAR)
		ELSE TO_DATE(SUBSTR(JUMIN_NUM,3,4),'MMDD')
		END
		AS "다가올 생일"
		,CASE
		WHEN SYSDATE-TO_DATE(SUBSTR(JUMIN_NUM,3,4),'MMDD') >=0 
		THEN (TO_DATE(SUBSTR(JUMIN_NUM,3,4),'MMDD')+(INTERVAL '1' YEAR)) - SYSDATE
		ELSE TO_DATE(SUBSTR(JUMIN_NUM,3,4),'MMDD') - SYSDATE
		END
		AS "남은 일수"
FROM EMP;


SELECT EMP_NO AS 직원번호
		,EMP_NAME AS 직원이름
		,JUMIN_NUM AS 주민번호
		,CASE
		WHEN SYSDATE-TO_DATE(SUBSTR(JUMIN_NUM,3,4),'MMDD') >=0 
		THEN TO_DATE(SUBSTR(JUMIN_NUM,3,4),'MMDD')+(INTERVAL '1' YEAR)
		ELSE TO_DATE(SUBSTR(JUMIN_NUM,3,4),'MMDD')
		END
		AS "다가올 생일"
		,CASE
		WHEN SYSDATE-TO_DATE(SUBSTR(JUMIN_NUM,3,4),'MMDD') >=0 
		THEN (TO_DATE(SUBSTR(JUMIN_NUM,3,4),'MMDD')+(INTERVAL '1' YEAR)) - SYSDATE
		ELSE TO_DATE(SUBSTR(JUMIN_NUM,3,4),'MMDD') - SYSDATE
		END
		AS "남은 일수"
FROM EMP;


--min,mas,avg,sum,count 함수들은 그룹합수 또는 통계함수 라고 부르기도 함.
--그룹을 지어 연산하는 함수이기 때문
--주로 GROUP by와 함께 사용
--NULL 값 제외하고 계산


SELECT EMP_NO 
		,EMP_NAME
		,to_char(hire_date,'YYYY-MM-DD(DAY) AM HH:MI:SS', 'NLS_DATE_LANGUAGE = Korean')
FROM EMP;

SELECT EMP_NO 
		,EMP_NAME
		,to_char(SYSDATE ,'YYYY-MM-DD(DY) HH24:MI:SS', 'NLS_DATE_LANGUAGE = Korean')
FROM EMP;

SELECT EMP_NO 
		,EMP_NAME
		,to_char(hire_date ,'YYYY-MM-DD(DY) Q PM HH:MI:SS', 'NLS_DATE_LANGUAGE = Korean')
FROM EMP;
-- 분기

select
       emp_no 
      , emp_name 
      , to_char( hire_date ,'YYYY"년"-MM"월"-DD"일" (DY) Q"분기" AM HH"시":MI"분":SS"초"' , 'NLS_DATE_LANGUAGE = Korean')    -- 시분초 HH:MI:SS
   from 
       emp; 
       
SELECT 
	EMP_NO 
	,EMP_NAME
	, TO_NUMBER(TO_CHAR(sysdate,'RRRR'))-
	TO_NUMBER(CASE SUBSTR(JUMIN_NUM,7,1) WHEN '1' THEN '19' WHEN '2' THEN '19' else '20' END||SUBSTR(JUMIN_NUM,1,2)) 
FROM EMP e;

select
      emp_no      as "직원번호"
      , emp_name   as "직원명"
      , jumin_num   as "주민번호"
      , case when 
            to_date(
               to_char(sysdate, 'YYYY')||substr(jumin_num, 3, 4)
               , 'YYYYMMDD'
            )
            -
            sysdate
            >=0
         then to_char(
            to_date(
               to_char(sysdate, 'YYYY')||substr(jumin_num, 3, 4)
               , 'YYYY-MM-DD'
            )
          )
         else to_char(
            to_date(
               to_number(to_char(sysdate,'YYYY'))+1||substr(jumin_num, 3, 4)
                , 'YYYYMMDD'
            )
            , 'YYYY-MM-DD'
            )
      end      as "다가올 생일날"
   from
      emp;
     
     
     
      SELECT TO_DATE(SUBSTR(jumin_num,3, 4),'mm-dd') 
      FROM emp;
      
     SELECT emp_no   AS 직원번호
       ,emp_name AS 직원명
       ,jumin_num ,
       TO_DATE(
       CASE
              WHEN TO_DATE(SUBSTR(jumin_num,3, 4),'mmdd') - SYSDATE >= 0
              THEN TO_CHAR(SYSDATE,'yyyy')
                            ||SUBSTR(jumin_num,3, 4)
              ELSE TO_CHAR(SYSDATE,'yyyy')+1
                            ||SUBSTR(jumin_num,3, 4)
       END,'YYYY-MM-DD') 
       AS 다가올생일날 
       ,FLOOR( TO_DATE(
       CASE
              WHEN TO_DATE(SUBSTR(jumin_num,3, 4),'mmdd') - SYSDATE >= 0
              THEN TO_CHAR(SYSDATE,'yyyy')
                            ||SUBSTR(jumin_num,3, 4)
              ELSE TO_CHAR(SYSDATE,'yyyy')+1
                            ||SUBSTR(jumin_num,3, 4)
       END,'yyyy-mm-dd' )-SYSDATE ) 
       AS 생일까지남은일수
FROM   EMP;


SELECT EMP_NAME
FROM (SELECT SUBSTR(JUMIN_NUM,1,1) AS "Y",SUBSTR(JUMIN_NUM,7,1) AS "S", EMP_NAME FROM emp)
WHERE y = 7 AND s = 1; 
	 
SELECT EMP_NAME
FROM emp
WHERE SUBSTR(JUMIN_NUM,1,1) LIKE '7%' AND SUBSTR(JUMIN_NUM,7,1) LIKE '1%' 

select * 
from emp 
WHERE jumin_num like '7_____1%'

select * from employee
      where
      to_char(   
         to_date(   
            case 
               when substr(jumin_num, 7, 1)='1' then '19' 
               when substr(jumin_num, 7, 1)='2' then '19' 
            else '20'
         end||substr(jumin_num,1,6) 
         , 'YYYY-MM-DD'
         )
      , 'DY'
      )
      = 'WED'   
      
      select * from emp
      where
      to_char( 
         to_date(
             case 
               when substr(jumin_num, 7, 1)='1' then '19' 
               when substr(jumin_num, 7, 1)='3' then '20' 
            else '00'
         end||substr(jumin_num,1,1)||'0'
         , 'YYYY' 
         )
      , 'YYYY'
      )
      ='1970'


```
