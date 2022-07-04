```sql
alter session set nls_date_format='RR/MM/DD';

drop table emp;
drop table dept;

CREATE TABLE DEPT
       (DEPTNO number(10),
        DNAME VARCHAR2(14),
        LOC VARCHAR2(13) );

INSERT INTO DEPT VALUES (10, 'ACCOUNTING', 'NEW YORK');
INSERT INTO DEPT VALUES (20, 'RESEARCH',   'DALLAS');
INSERT INTO DEPT VALUES (30, 'SALES',      'CHICAGO');
INSERT INTO DEPT VALUES (40, 'OPERATIONS', 'BOSTON');

CREATE TABLE EMP (
 EMPNO               NUMBER(4) NOT NULL,
 ENAME               VARCHAR2(10),
 JOB                 VARCHAR2(9),
 MGR                 NUMBER(4) ,
 HIREDATE            DATE,
 SAL                 NUMBER(7,2),
 COMM                NUMBER(7,2),
 DEPTNO              NUMBER(2) );

INSERT INTO EMP VALUES (7839,'KING','PRESIDENT',NULL,'81-11-17',5000,NULL,10);
INSERT INTO EMP VALUES (7698,'BLAKE','MANAGER',7839,'81-05-01',2850,NULL,30);
INSERT INTO EMP VALUES (7782,'CLARK','MANAGER',7839,'81-05-09',2450,NULL,10);
INSERT INTO EMP VALUES (7566,'JONES','MANAGER',7839,'81-04-01',2975,NULL,20);
INSERT INTO EMP VALUES (7654,'MARTIN','SALESMAN',7698,'81-09-10',1250,1400,30);
INSERT INTO EMP VALUES (7499,'ALLEN','SALESMAN',7698,'81-02-11',1600,300,30);
INSERT INTO EMP VALUES (7844,'TURNER','SALESMAN',7698,'81-08-21',1500,0,30);
INSERT INTO EMP VALUES (7900,'JAMES','CLERK',7698,'81-12-11',950,NULL,30);
INSERT INTO EMP VALUES (7521,'WARD','SALESMAN',7698,'81-02-23',1250,500,30);
INSERT INTO EMP VALUES (7902,'FORD','ANALYST',7566,'81-12-11',3000,NULL,20);
INSERT INTO EMP VALUES (7369,'SMITH','CLERK',7902,'80-12-11',800,NULL,20);
INSERT INTO EMP VALUES (7788,'SCOTT','ANALYST',7566,'82-12-22',3000,NULL,20);
INSERT INTO EMP VALUES (7876,'ADAMS','CLERK',7788,'83-01-15',1100,NULL,20);
INSERT INTO EMP VALUES (7934,'MILLER','CLERK',7782,'82-01-11',1300,NULL,10);

commit;

drop  table  salgrade;

create table salgrade
( grade   number(10),
  losal   number(10),
  hisal   number(10) );

insert into salgrade  values(1,700,1200);
insert into salgrade  values(2,1201,1400);
insert into salgrade  values(3,1401,2000);
insert into salgrade  values(4,2001,3000);
insert into salgrade  values(5,3001,9999);

commit;


SELECT  ename, job , sal, RANK () OVER (ORDER BY sal DESC) 순위
FROM EMP
WHERE job IN('ANALYST','MANAGER');
-- 직업이 애널리스트와 매니저만 이름,직업,월급,월급 순위를 월급에 대하여 내림차순으로 정렬하라.


SELECT ename, sal,job, RANK() OVER (PARTITION BY job
									ORDER BY sal desc) AS 순위
FROM emp;
-- 직업별로 월급을 내림차순으로 정리하여 출력하라
-- PARTITION BY JOB으로 직업별로 분류하게 하였다.

SELECT ename, job, sal, RANK() OVER(ORDER BY sal desc) AS RANK,
						DENSE_RANK() OVER (ORDER BY sal desc) AS DENSE_RANK
FROM emp
WHERE job IN('ANALYST','MANAGER');
-- 애널리스트와 매니저가 직업인 직원의 월급순위(내림차순,rank: 동일 순위가 존재할 때 개수와 순위가 같게 된다), 월급순위(내림차순, dense_rank : 동일 순위가 존재할 때 동일 순위는 1개로 취급)

SELECT job,ename,sal,DENSE_RANK() OVER (PARTITION BY job
											ORDER BY sal desc) 순위
FROM emp
WHERE HIREDATE  BETWEEN TO_DATE('1981/01/01','RRRR/MM/DD') AND  TO_DATE('1981/12/31','RRRR/MM/DD'); 
-- DENSE_RANK로 직업별 월급순위를 정리하는데 대상은 1981년 입사자만!!

SELECT DENSE_RANK (2975) WITHIN GROUP (ORDER BY sal desc) 순위
FROM emp;
-- sal이 2975인 직원이 월급을 내림차순 정렬했을 때 몇 위인지 출력

SELECT DENSE_RANK('81/11/17') WITHIN GROUP (ORDER BY hiredate ASC) 순위
FROM emp;
-- hiredate 가 81/11/17 인 사람이 hiredate를 오름차순 정리했을 때 몇 순위인지 출력

SELECT ename , job, sal,
	NTILE(4) OVER (ORDER BY sal DESC NULLS LAST) 등급
FROM EMP
WHERE LOWER(job) IN('analyst','manager','clerk');

-- 월급을 4등급으로 나누어 각각의 튜플에 등급을 부여해서 출력하는 함수.
-- 0-25,25-50,50-75,75-100
-- NULLS LAST는 NULL을 마지막에 출력하겠다는 의미


SELECT ename, comm
FROM EMP
WHERE DEPTNO =30
ORDER BY comm DESC NULLS LAST;
-- NULLS LAST를 사용했을 때는 NULL 값이 마지막으로 정렬됩니다.

SELECT ename,sal, rank() over(ORDER BY sal desc) AS RANK,
				DENSE_RANK() OVER (ORDER BY sal desc) AS DENSE_RANK,
				CUME_DIST() over(ORDER BY sal desc) AS CUM_DIST
FROM emp;
-- 이름 월급 월급 순위(내림차순),월급 순위(내림차슨,dense),월급 순위 비율 출력
-- 월급순위 비율은 순위/전체튜플수


SELECT job, ename,sal, RANK() OVER (PARTITION BY job
										order BY sal desc) AS RANK,
										CUME_DIST() OVER (PARTITION BY job 
															ORDER BY sal desc) AS cum_DIST
FROM emp;														
-- 직업, 이름, 월급 직업별 월급순위 직업별 월급비율을 출력한다
-- come_dist()의 월급 순위 비율은 직업별로 나뉠것.

SELECT deptno, LISTAGG(ENAME,',') WITHIN GROUP (ORDER BY ename) AS EMPLOYEE
FROM emp
GROUP BY deptno;
-- 부서별로 이름을 구분자 ','로 구분해서 순서대로 가로로 출력
-- WITHIN GROUP : ~ 의 내에 , ~ 안에 라는 의미
-- LISTAGG() 함수 사용을 위해서는 group by 절이 반드시 필요하다.


SELECT job, LISTAGG(ename,',') WITHIN GROUP (ORDER BY ename asc) AS employee
FROM emp
GROUP BY job;
-- 직업별로 직업의 이름을 오름차순 정렬해서 가로로 출력하라.


SELECT job,
LISTAGG(ename||'('||sal||')',',') WITHIN GROUP (ORDER BY ename asc) AS employee
FROM emp
GROUP BY JOB;
--  직업별로 이름을 오름차순으로 정리한 그룹에서 "이름(월급)" 의 형태로 가로로 출력


SELECT empno,ename,sal,
		LAG(sal,1) OVER (ORDER BY sal asc) "전 행",
		LEAD(sal,1) OVER (ORDER BY sal asc) "다음 행"
FROM emp
WHERE job IN('ANALYST','MANAGER');
-- 애널리스트,매니져의 직원번호,이름,월급, 이전 튜플의 월급 이다음 튜플의 월급을 출력
-- LAG() : 바로 전행의 데이터를 출력하는 함수
-- LEAD() : 다음 행 데이터를 출력하는 함수

SELECT DEPTNO,empno, ename,hiredate,
	LAG(hiredate,1) OVER (PARTITION  BY DEPTNO 
							ORDER BY hiredate asc) "전 행",
	LEAD(hiredate,1) OVER (PARTITION BY DEPTNO 
							ORDER BY hiredate asc) "다음 행"
	FROM EMP;
-- 부서별로 전 행과 다음 행을 출력

SELECT  sum(decode(deptno,10,sal)) AS "10",
		sum(decode(deptno,20,sal)) AS "20",
		sum(decode(deptno,30,sal)) AS "30"
		FROM emp;
-- 부서별 월급의 합을 행으로 출력

SELECT deptno, DECODE(deptno,10,sal) AS "10"
FROM emp;
-- 부성번호와 부서번호가 10인 직원의 월급 출력

SELECT sum(decode(deptno,10,sal)) AS "10"
FROM emp;
-- 부서번호가 10인 직원의 월급의 합 출력

SELECT sum(DECODE(deptno,10,sal)) AS "10",
		sum(DECODE(deptno,20,sal)) AS "20",
		sum(DECODE(deptno,30,sal)) AS "30"
	FROM emp;

-- 부서별 월급의 총합을 행으로 출력

SELECT  sum(decode(job,'ANALYST',sal)) AS "애널리스트",
		sum(decode(job,'CLERK',sal)) AS "CLERK",
		sum(decode(job,'MANAGER',sal)) AS "매니져",
		sum(decode(job,'SALESMAN',sal)) AS "SALESMAN"
FROM emp;
-- 직업별로 월급의 합

SELECT  deptno,sum(decode(job,'ANALYST',sal)) AS "애널리스트",
		sum(decode(job,'CLERK',sal)) AS "CLERK",
		sum(decode(job,'MANAGER',sal)) AS "매니져",
		sum(decode(job,'SALESMAN',sal)) AS "SALESMAN"
	FROM emp
	GROUP BY deptno;
-- 부서별 직종의 월급의합

SELECT *
FROM  (SELECT deptno, sal FROM emp) pivot (sum(sal) FOR deptno IN (10,20,30));
-- 직원테이블중 부서번호 월급 컬럼만으로 만든 테이블에서 부서번호가 10,20,30것으로부터 월급의 합을
-- pivot은 열데이터를 행데이터로 회전시켜주는 역할을 한다.

SELECT *
FROM (SELECT job,sal FROM emp)
pivot(sum(sal) FOR job in('ANALYST','CLERK','MANAGER','SALESMAN'));
-- emp테이블의 직업 월급 테이블에서 직업이 애널리스트, 서기,매니져,세일즈맨의 월급의 합을 출력하는 테이블로 만들어 그 테이블을 출력하라.

SELECT *
	FROM (SELECT job, sal FROM emp)
	PIVOT (sum(sal) FOR job IN ('ANALYST' AS "ANALYST",'CLERK' AS "CLERK",'MANAGER' AS "MANAGER",'SALESMAN' AS "SALESMAN"));
-- 위 내용을 별칭을 붙여 출력

create table order2
( ename  varchar2(10),
  bicycle  number(10),
  camera   number(10),
  notebook  number(10) );

insert  into  order2  values('SMITH', 2,3,1);
insert  into  order2  values('ALLEN',1,2,3 );
insert  into  order2  values('KING',3,2,2 );

commit;


SELECT *
 FROM order2
 UNPIVOT (건수 for 아이템 in (BICYCLE, CAMERA, NOTEBOOK));
-- unpivot은 행데이터를 열데이러 변경시켜주는 내용을 얘기한다.
-- NULL은 출력되지않음
SELECT *
FROM ORDER2 
unpivot (건수 FOR 아이템 IN (BICYCLE AS 'B',CAMERA AS 'C', NOTEBOOK AS 'N'));
-- 위 내용을 각 행데이터를 이름붙여 출력

UPDATE ORDER2 SET NOTEBOOK=NULL WHERE ename='SMITH';
	
SELECT *
FROM ORDER2
UNPIVOT INCLUDE NULLS (건수 FOR 아이템 IN (BICYCLE AS 'B',CAMERA AS 'C', NOTEBOOK AS 'N'));
-- NULL값을 포함하여 행데이터를 열데이터로 변겅

SELECT empno,ename,sal,sum(sal) OVER (ORDER BY empno ROWS
										BETWEEN UNBOUNDED PRECEDING
										AND CURRENT row) 누적치
FROM EMP
WHERE job IN('ANALYST','MANAGER');
-- 애널리스트와 매니저의 직원번호 이름 월급 월급의 누적치
-- ROWS	/UNBOUNDED PRECEDING : 첫 행 UNBOUNDEㅇ FOLLOWING 맨 마지막행 CURRENT row: 현재행
--  order by empno rows BETWEEN UNBOUNDED PRECEDING AND CURRENT row는 empno를 정렬하는데 로우데이터가 첫행부터 현재행까지 정리한 테이블 정렬

SELECT  empno,ename,sal, RATIO_TO_REPORT(sal) OVER () AS 비율
FROM emp
WHERE DEPTNO  = 20;
-- 부서번호가 20인 직원의 번호 이름 월급 월급의 비율을 출력하라

SELECT empno,ename,sal, RATIO_TO_REPORT(sal) OVER () AS 비율,
				SAL/sum(sal) over() AS "비교 비율"
FROM EMP
WHERE deptno =20;
-- 부서번호가 20인 직원번호 직원이름 월급 월급의 비율 월급을/월급의 합으로 나눈 값을 출력

SELECT  job, sum(sal)
FROM emp
GROUP BY rollup(job);
-- 직업별로 월급의 합과 모든 직업의 총합을 추가해서 출력

SELECT DEPTNO, job,sum(sal)
FROM emp
GROUP BY ROLLUP (DEPTNO ,job);
-- 부서별 직업의 총합,부서별 월급 총합 전체 월급 총합을 출력하시오
-- rollup은 뒤에서부터 제거해나감.

SELECT job, sum(sal)
FROM emp
GROUP BY CUBE(job);
-- 직업별 토탈월급을 출력하는데 모든 직업의 토탈급여는 맨 첫 행에 출력

SELECT DEPTNO ,job, sum(sal)
FROM emp
GROUP BY CUBE(deptno,job);
-- 부서별 직업의 토탈월급 직업별 토탈월급, 부서별 토탈월급, 전체 토탈월급을 출력한다.
-- cube()는 두 테이블로 만들 수 있는 모든 경우의 수에 해당하는 데이터를 만들어 출력

SELECT deptno,job,sum(sal)
FROM EMP
GROUP BY GROUPING sets((DEPTNO),(job),());
-- 부서별, 직업별, 전체의 경우의 수에 나올 수 있는 모든 행을 출력한다.
-- deptno 별, job 별 , () 전체 별 나올 수 있는 행 데이터 모두 출력

SELECT empno,ename,sal,RANK() OVER (ORDER BY sal desc) RANK,
						DENSE_RANK() OVER (ORDER BY sal desc) DENSE_RANK,
						ROW_NUMBER() OVER (ORDER BY sal desc) 번호
FROM emp
WHERE DEPTNO  = 20;

SELECT  empno,ename,sal,ROW_NUMBER () OVER () 번호
FROM emp
WHERE DEPTNO  = 20;
-- over()뒤에는 order by함수를 사용해 줄 필요가 있다.


SELECT  deptno,ename,sal,ROW_NUMBER() OVER(PARTITION BY deptno
											ORDER BY sal DESC) 번호
FROM emp
WHERE deptno IN (10,20);
-- 부서번호가 10,20ㅇ을 부서번호별로 월급을 내림차순 정리해서 번호 붙여라


SELECT  ROWNUM,empno,ename,job,sal
FROM emp
WHERE  ROWNUM<=5;
-- ROWNUM을 번호를 매기고 5행 이상은 출력하지 않는 형태로 진행



SELECT empno, ename, job, sal
  FROM emp
  ORDER BY sal DESC FETCH FIRST 4 ROWS ONLY;
 -- 11g 에서 안되는 것으로 보임

 
 SELECT  ename, loc 
 FROM emp, dept
 WHERE emp.deptno = dept.deptno;
-- emp와 dept를 공유하는 컬럼 deptno를 이용해서 JOIN해서 이름 장소 출력
-- 공유하고 있는 키(조인조건)을 통해 연결해주지 않는다면 모든 조합 가능한 경우의 수에 데이터를 출력할 것이다.

SELECT  ename,loc,job
FROM emp,dept
WHERE emp.DEPTNO =dept.DEPTNO  AND emp.job='ANALYST';
-- emp와 dept를 조인해서 직업이 애널리스트인 멤버의 이름,지역,집업을 출력한다.

SELECT  ename,loc,job,deptno
FROM emp,dept
WHERE emp.DEPTNO =dept.DEPTNO  AND emp.job='ANALYST';
-- deptno가 emp와 dept모두 존재하기 때문에 어느쪽 테이블인지 명시에 주어야 한다.

SELECT  ename,loc,job,emp.deptno
FROM emp,dept
WHERE emp.DEPTNO =dept.DEPTNO  AND emp.job='ANALYST';
-- 이와 같이 deptno가 어느 테이블 소속인지 명시 해주어야 함.
-- 가급적 모든 컬럼의 출신을 얘기해주는 것 이좋음

SELECT  e.ename,d.loc,e.job,e.deptno
FROM emp e,dept d
WHERE e.DEPTNO =d.DEPTNO  AND e.job='ANALYST';
-- from 테이블 명 뒤에 설정해주면 별칭을 통해 위와 같이 명칭을 체크해 줄 수 있다
-- 가급적 모든 컬럼에 출신을 얘기해주는 것이 좋다.

SELECT emp.ENAME ,d.loc, e.job
FROM emp e, dept d
WHERE e.DEPTNO  = d.DEPTNO AND e.JOB  = 'ANALYST';
-- 별칭을 사용하면 emp.ename 이 아닌 e.ename으로 적어주어야함.
-- EQUI JOIN
create table salgrade
( grade   number(10),
  losal   number(10),
  hisal   number(10) );

insert into salgrade  values(1,700,1200);
insert into salgrade  values(2,1201,1400);
insert into salgrade  values(3,1401,2000);
insert into salgrade  values(4,2001,3000);
insert into salgrade  values(5,3001,9999);

commit;


SELECT  e.ename, e.sal, s.grade
FROM emp e, salgrade s
WHERE e.SAL  BETWEEN  s.losal AND s.hisal;
-- 이름 월급 급여 등급을 출력하는데 emp와 salgrade를 조인해서 losal과 hisal 사이의 데이터만 출력
-- NOT EQUI JOIN(연결 조건이 이퀄(=)이 아닌 경우 BETWEEN AND 연산자를 이용해 진행)
SELECT * FROM salgrade;


SELECT  e.ename,d.loc
FROM EMP e ,DEPT d 
WHERE e.DEPTNO  (+)= d.DEPTNO;
-- left outer join
-- 오른쪽 데이터가 덜나와서 오른쪽에 (+)를 붙여주면 right outer join 이라고 할 수 있음
-- 결과가 덜 나오는 쪽에 (+)를 붙여주어서 매칭 되는 값이 없는 데이터는 null과 함께 출력해준다.
-- 교집합 뿐 아니라(+) 붙여진 쪽에 데이터 집합을 모두 출력해준다.

SELECT e.ename AS 사원,e.job AS 직업,m.ENAME  AS 관리자,m.job AS 직업
FROM  EMP e ,EMP m
WHERE  e.MGR = m.EMPNO AND e.JOB ='SALESMAN'
-- 사원의 이름과 직업, 그 사원을 관리하느 관리자의 이름과 직업을 출력하라(세일즈맨 만)
-- 자기참조한 외래키를 통해 self join을 통해 직원과 관리자를 연결 출력

SELECT  e.ename AS 이름, e.job AS 직업, e.sal AS 월급, d.loc AS "부서 위치"
FROM emp e JOIN dept d
ON(e.DEPTNO=d.DEPTNO)
WHERE e.job = 'SALESMAN';
-- ON 절을 통해 조인 하는 방법
-- 이름,직업,월급,부서위치를 출력 (세일즈맨만) 부서위치 매칭을 위해 emp와 dept 조인

SELECT  e.ename, d.loc,s.grade
FROM emp e
JOIN dept d ON (e.deptno = d.DEPTNO)
JOIN salgrade s ON(e.SAL BETWEEN s.losal AND s.hisal);
-- 직원 이름, 근무 지역, 급여 등급를 출력하시오(equi join,non equi join모두 실행)

SELECT e.ename AS 이름, e.job AS 직업, e.sal AS 월급, d.loc AS "부서 위치"
	FROM emp e JOIN dept D
	USING(deptno)
	WHERE e.job='SALESMAN';
-- deptno를 공유키르 하여 두 테이블을 조인하여 세일즈맨의 이름 직업 월급 부서위치를 출력

SELECT e.ename,d.loc,s.grade
FROM EMP e 
JOIN DEPT d USING(deptno)
JOIN salgrade s on(e.sal BETWEEN s.losal
								AND s.hisal);
-- on과 using을 동시에 사용하여 여러 테이블을 조인했다.
							
SELECT e.ename AS 이름,e.JOB AS 직업, e.sal AS 월급, d.LOC AS "부서 위치"
FROM EMP e NATURAL JOIN dept d
WHERE e.JOB ='SALESMAN';
-- natural join을 통해 두 테이블을 조인하는 방법
-- 둘의 공통 키인 deptno를 오라클이 알아서 찾아 조인해줌



SELECT e.ename AS 이름,e.JOB AS 직업, e.sal AS 월급, d.LOC AS "부서 위치"
FROM EMP e NATURAL JOIN dept d
WHERE e.JOB ='SALESMAN' AND DEPTNO =30;
-- emp와 dept를 natural조인해서 세일즈맨과 부서번호 30번의 이름 직업 월급 부서위치를 출력

SELECT e.ename AS 이름, e.job AS 직업, e.sal AS 월급,d.loc AS "부서 위치"
 FROM emp e,dept d
 WHERE e.DEPTNO(+)=d.DEPTNO;
-- 데이터가 덜 많은 쪽에 (+)를 붙여주었고 왼쪽에 붙으면 right outer join
-- 오라클용
SELECT e.ename AS 이름, e.job AS 직업, e.sal AS 월급,d.loc AS "부서 위치"
 FROM emp e RIGHT OUTER JOIN dept d
 ON (e.DEPTNO=d.DEPTNO);
-- RIGHT OUTER JOIN 키워드를 이용한 RIGHT OUTER JOIN
-- 1999 ANSI/ISO

INSERT INTO emp(empno, ename, sal, job, deptno)
       VALUES(8282, 'JACK', 3000, 'ANALYST', 50) ;
      

SELECT e.ENAME AS 이름, e.JOB  AS 직업, e.SAL AS 월급, d.LOC AS "부서 위치"
FROM EMP e  LEFT OUTER JOIN DEPT d 
ON(e.DEPTNO=d.DEPTNO);
-- 1999 ansi/iso right outer join

SELECT e.ENAME AS 이름, e.JOB  AS 직업, e.SAL AS 월급, d.LOC AS "부서 위치"
FROM EMP e, DEPT d 
WHERE e.DEPTNO=d.DEPTNO(+);
-- 오라클 용 레프트아우터 조인

SELECT  e.ename AS 이름,e.job AS 직업, e.sal AS 월급, d.loc AS "부서 위치"
FROM emp e FULL OUTER JOIN dept D
ON (e.DEPTNO=d.deptno);
-- full outer join = leftouter join와 right outer join의 결과값중 중복은 한번만 출력하고 합쳐놓은것
-- 1999 ANSI/ISO 표준

SELECT  e.ename AS 이름,e.job AS 직업, e.sal AS 월급, d.loc AS "부서 위치"
FROM emp e, dept D
WHERE e.DEPTNO(+)=d.deptno(+);
-- 오류 (+)는 한쪽에먼 사용 할 수 있음

SELECT e.ENAME AS 이름, e.JOB  AS 직업, e.SAL AS 월급, d.LOC AS "부서 위치"
	FROM EMP e  LEFT OUTER JOIN DEPT d 
	ON(e.DEPTNO=d.DEPTNO)
UNION
SELECT e.ename AS 이름, e.job AS 직업, e.sal AS 월급,d.loc AS "부서 위치"
	FROM emp e RIGHT OUTER JOIN dept d
	ON (e.DEPTNO=d.DEPTNO);
-- full outer join을 left right로 만들어주는 방법 ( 합집합 UNION)

SELECT  deptno,sum(sal)
FROM emp
GROUP BY deptno
UNION ALL
SELECT  TO_NUMBER(null) AS DEPTNO , sum(sal)
FROM emp;
-- 부서별로 월급의 합과 합집합 속성이름이 deptno에 null이 들어간 친구와 총 월급의 합을 합집합 해서 출력
-- 위 아래 쿼리가 컬럼 개수가 동일해야함
-- 위 아래 쿼리의 컬럼이 데이터 타입이 바꾸어야함
-- 결과로 출력되는 컬럼명은 위쪽 커리의 컬럼명으로 출력
-- order by절에는 아래쪽 쿼리에만 가능
-- 위 아래 쿼리의 결과값을 붙여서 출력 하는 UNION ALL



SELECT deptno,sum(sal)
FROM emp
GROUP BY DEPTNO
UNION
SELECT NULL AS DEPTNO ,sum(sal)
FROM emp;
-- deptno와 부서별 월급의 합과 총합을 출력
-- UNION ALL과 다른점 중복된 데이터를 하나의 고유값으로 출력합니다.
-- 첫 번째 컬럼의 데이터를 기준으로 내림차순으로 정렬하여 출력합니다.



SELECT  ename, sal,job,deptno
FROM EMP
WHERE deptno IN (10,20)
INTERSECT
SELECT ename,sal,job,DEPTNO
FROM emp
WHERE deptno IN (20,30);





							
```
