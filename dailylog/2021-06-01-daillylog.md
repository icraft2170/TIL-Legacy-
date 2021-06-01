---
title: 06.01일 ( studylog )
author : 손현호
date: 2021-06-01
---


# SQL



### 함수

- 단일행 함수
    - 정의 : 하나의 행을 입력받아 하나의 행을 반환하는 함수
    - 종류 : 문자함수, 숫자함수, 날짜함수, 변환 함수, 일반함수
- 다중 행 함수
    - 정의 : 여러 개의 행을 입력받아 하나의 행을 반환하는 함수
    - 종류 : 그룹 함수

| 단일행 함수 | 함수 |
| ---------|-----------------------------------|
|문자 함수| UPPER, LOWER, INICAP, SUBSTR, LENGTH, CONCAT, INSTR, TRIM, LPAD, RPAD등

<br/>

```sql
SELECT ename, sal
    FROM emp
    WHERE LOWER(ename)='scott';
```
- ename을 전부 받아와 소문자로 바꾼후 `scott`라는 이름으로 검색했다.
- 많은 데이터가 존재할 때는 대,소문자 어느 것으로 저장되어 있는지 알 수 없기 때문에 대문자 혹은 소문자로 변경하여 검색하는 것이 정확하다.



### 함수 UPPER ,LOWER ,INITCAP


```sql
SELECT UPPER(ename), LOWER(ename), INITCAP(ename)
    FROM emp;
-- ename을 각각 대문자, 소문자, 첫 글자만 대문자로 출력하라.
```
- `UPPER`   : 대문자로 출력하라
- `LOWER`   : 소문자로 출력하라
- `INITCAP` : 첫 글자만 대문자 나머지는 소문자로 출력하라
- 함수는 컬럼명을 파라미터로 하여 그 출력 전체에 영향을 미친다.




### SUBSTR

```sql
SELECT SUBSTR('SMITH',1,3)
    FROM DUAL;
```
- `SUBSTR` 함수는 문자에서 특정 위치의 문자열을 추출합니다. 첫 번째 글짜는 `1`로 시작합니다
    - 0으로 시작하지 않으니 주의하자
- 마이너스 값이 오면 뒤에서 부터 세면된다.
- 마지막을 지정해주지 않으면 끝까지 선택된다.
### LENGTH

```sql
SELECT ename, LENGTH(ename)
    FROM emp;
/*이름과 이름 철자의 길이를 출력하라*/
```
- `LENGTH` 함수는 문자열의 길이를 출력하는 함수.
- 한글도 마찬가지로 문자의 길이가 출력됨
- `LENGTHB`라고 하는 함수도 존재하며 이는 Byte의 길이를 반환.

### INSTR

```sql
SELECT INSTR('SMITH','M')
    FROM DUAL;
/* 특정 문자까 몇변 자리(인덱스)에 있는지 출력*/
```

- `INSTR`함수는 특정 철자의 위치를 출력하는 함수.

```sql
SELECT SUBSTR('baro1999@gmail.com',0,INSTR('baro1999@gmail.com','@')-1)
    FROM DUAL;
-- 이메일에서 아이디 부분만 출력하라
```

- 위와 같이 함수의 조합으로 다양한 결과를 뽑아 낼 수 있다.
    - 위 sql문은 substr,instr을 이용하여 아이디 부분만 짤라냈다.


### REPLACE

```sql
SELECT ename, REPLACE(sal,0,'*')
    FROM emp;
-- 이름과 월급을 출력하는데 월급의 0을 *로 바꾸어서 출력하라

SELECT REPLACE(ENAME, SUBSTR(ENAME,2,1),'*') as "전광판_이름"
    FROM test_ename;
    -- 이름의 두번째 글자를 *로 바꾸고 컬럼명을 전광판_이름으로 출력하라
```
- `REPLACE` 함수는 특정 문자를 변경하여 출력하는데 쓰인다.

```sql
SELECT ename, REGEXP_REPLACE(sal,'[0-3]','*') as salary
    FROM emp;
-- 이름과 월급을 출력하는데 월급의 0,1,2,3을 *로 바꾸어서 컬럼명 salary로 출력하라
```
- `REGEXP_REPLACE`는 정규식을 이용한 `REPLACE` 함수



### LPAD, RPAD (칸 채우기)
```sql
SELECT ename, LPAD(sal,10,'*') as salary1, RPAD(sal,10,'*') as salary2
    FROM emp;
-- 이름,월급,월급을 출력하는데 월급 출력칸을 10칸으로 하고 남는 칸은 *로 채운다. 
-- LPAD 왼쪽을 *로 RPAD 오른쪽을 *로 채운다
```

### TRIM , LTRIM, RTRIM (공백,글자 제거)

```sql
SELECT 'smith', LTRIM('smith','s'), RTRIM('smith','h'), TRIM('s' from 'smiths')
FROM dual;
```
- TRIM은 제거하고 출력한다는 의미
-  LTRIM 은 왼쪽부터 s한개 RTRIM 오른쪽부터 h한개 TRIM은 smiths로 부터 s를 제거하라는 의미.
- TRIM ,LTRIM, RTRIM을 추가 파라미터 지정 없이 사용하면 왼쪽 오른쪽 양쪽 공백제거가 된다 

### ROUND (반올림)

```sql
SELECT '876.567' as 숫자, ROUND(876.567,1)
    FROM dual;
```

- ROUND는 반올림을 해주는 함수.
    - `ROUND(876.567,1)` = 876.5
    - `ROUND(876.567,-1)` = 880
    - `ROUND(876.567, -2)` = 900
    - `ROUND(876.567,2)`=876.57
- `.`(소수점)을 0으로 기준잡고 오른쪽은 `+` 왼쪽은  `-` 이다.