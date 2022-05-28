## SQL 동작순서
```
SELECT 컬럼명 -----------------     (5)         추출된 데이터들을 조회
FROM 테이블명-------------------    (1)          테이블을 가장 먼저 확인
WHERE 테이블 조건 --------------    (2)          테이블에서 주어진 조건에 맞는 데이터들을 추출
GROUP BY 컬럼명 ----------------    (3)         공통적인 데이터들끼리 묶어 그룹
HAVING 그룹 조건 ---------------    (4)         주어진 주건에 맞는 그룹들을 추출
ORDER BY 컬럼명 ----------------    (6)         추출된 데이터들을 정렬
```

![images](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FRmiEB%2FbtqLWHOz4Pr%2FM0elhPJskIocPKKShzPrTk%2Fimg.png)
## SQL PROCEDURE 

 - 프로세스의 절차를 담당하는 문법이며 한개의 결과값을 반환해주는 문법이다.
 - 펑션과 다르게 결과값을 리턴시키지 않아도된다.  
 - dbms_output.putline()으로 저장된 변수애 대해서 값을 볼 수 있다.
  - RETURN 형식은 BEGIN 사이에 RETURN을 적어주거나 OUT 변수를 통해서 반환해줄 수 있다.
 - IN은 데이터를 대입 OUT은 데이터를 출력 INOUT은 데이터를 삽입하거나 출력할 수 있다.
 - 이거는 직접 그려가면서 이해하면 한방에 이해된다 해당 [링크](https://afsdzvcx123.tistory.com/entry/%EC%98%A4%EB%9D%BC%ED%81%B4-PLSQL-PLSQL-%ED%94%84%EB%A1%9C%EC%8B%9C%EC%A0%80-%EB%A7%A4%EA%B0%9C%EB%B3%80%EC%88%98-IN-OUT-%EC%9D%B4%EB%9E%80)에서 한번 공부해보자.   
    
    ```sql
    CREATE OR REPLACE PROCEDURE 프로시저이름 
    IS
        
        변수이름 [IN/OUT/INOUT]데이터타입;  -- 프로시저내에서 사용할 변수선언
        변수이름 [IN/OUT/INOUT]데이터타입;
        변수이름 [IN/OUT/INOUT]데이터타입;
        ...
        
    BEGIN
        기능 구현;
    END;
    
    ```
    
## SQL FUNCTION 

    - 프로세스의 절차를 담당하는 문법이며 한개의 결과값을 반환해주는 문법이다.    
    - 무조건 최소 하나의 결과값을 도출해내야한다.  
    
    CREATE OR REPLACE FUNCTION 함수이름 
    IS
        
        지역변수 선언;
        
    BEGIN
        기능 구현;
        return 값;
    END;

    예시)
    CREATE REPLACE FUNCTION f_name
	    (name VARCHAR2)
	    return VARCHAR2
    IS
    BEGIN
	    RETURN SUBSTR(name, 2, 3);
    END;


    
    
    
#### SQL 숫자함수 
- ABS(n) : n의 절대값을 반환
- CEIL(n) , FLOOR(n) : n보다 같거나 큰 정수를 반환한다
- ROUND(n,i) : n을 소수점 i+1번째 자리에서 반올림
- TRUNC(n,i) : n을 소수점 i+1번째 자리에서 버림
- POWER(n1,n2) : n1을 n2번 거듭제곱한 결과
- MOD(n1,n2) : n1을 n2로 나눈 나머지 값

#### SQL 문자함수 
- INITCAP(char) : char의 첫문자만 대문자 나머지 소문자
- LOWER(char) : char를 소문자로
- UPPER(char) : char을 대문자로
- CONCAT(char1, char2) : char1 char2를 붙인다. (|| 구문을 사용해서도 구현할 수 있다.)
- CONCAT_WS(string, char1, char2) : char1 char2 사이에 구문자 string을 붙인다. 
- SUBSTR(char, pos,len) : char의 pos번째 문자부터 len길이만큼 잘라서 반환.
- LTRIM: char1의 좌측부터 char2를 찾아서 삭제후 반환 (한번만 삭제한다.)
- RTRIM: LTRIM과 비슷. 오른쪽부터 검색을 진행
```sql
LTRIM&RTRIM

WITH DEPT AS (
    SELECT '0010' DEPTNO, 'ACCOUNTING' DNAME, '  NEW YORK  ' LOC FROM DUAL
)

SELECT LOC
     , LTRIM(LOC)
     , DEPTNO
     , LTRIM(DEPTNO, '0')
     , DNAME
     , LTRIM(DNAME, 'ACC')
  FROM DEPT

TRIM과의 차이점은 TRIM은 양쪽의 공백만을 제거해준다. 즉 유저가 서비스를 이용하면서 의도와는 다르게 공백을 사용했을 때
해당 리소스의 낭비를 줄여주는것이지만, RTRIM&LTRIM은 반복되는 문자열을 제거해준다.
```
![images](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile2.uf.tistory.com%2Fimage%2F994882385C20544F104539)
![images](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile3.uf.tistory.com%2Fimage%2F99200F385C2054501B9163)
![images](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile6.uf.tistory.com%2Fimage%2F99FCF5385C205450127C7F)

- LPAD(char1,n,char2) : char1의 왼쪽부터 char2를 채운다. n은 연산후 총 문자열 자릿수를 의미한다.
- RPAD(char1,n,char2)  : LPAD와 비슷 , 오른쪽부터 진행
```sql 
LPAD&RPAD 

WITH EMP AS (
    SELECT '7839' EMPNO, 'JAMES' ENAME, '30' DEPTNO FROM DUAL
)

SELECT EMPNO
     , ENAME
     , DEPTNO
     , LPAD(DEPTNO, 5)      --1
     , LPAD(DEPTNO, 5, ' ') --2
     , LPAD(DEPTNO, 5, '0') --3
     , LPAD(DEPTNO, 5, 'A') --4
  FROM EMP
  
  특정 문자열을 왼쪽혹은 오른쪽으로 가운데 선언된 자릿수만큼 채워준다.   
   그리고 뒤에 옵션을 넣어주면 남은 자릿수는 해당 문자로 채워주며 디폴트는 공백이다.
```
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile9.uf.tistory.com%2Fimage%2F99B1E04D5C10FF992DF3B7)
 
- REPLACE(char1,char2,char3) : char1에서 char2를 찾아 char3을 반환한다. LTRIM과 달리 여러번 진행한다.
- LENGTH(char) : char의 길이
- DECODE(input1, search1 , result1, search2, .. ,default) :  input1을 search1과 비교하여 같은 값이면 result1을 반환하고, 같지 않을 경우 search2를 비교하는 방식을 반복한다. 최종적으로 같은 값이 없으면 default를 반환한다.
```sql
DECODE 
기본적으로 프로그래밍에서의 IF~ELSE 구문과 같다. 설명은 어렵지만 아래 그림과 같다.
else부분은 생략이 가능하며 생략을 한다면 결과 값은 NULL이 나온다.
아래의 코드에서는 '기타' 부분이 else라고 생각하면 된다.

WITH temp AS (
  SELECT 'M' gender FROM dual UNION ALL
  SELECT 'F' gender FROM dual UNION ALL
  SELECT 'X' gender FROM dual 
)

SELECT gender
     , DECODE(gender, 'M', '남자', 'F', '여자', '기타') gender2
  FROM temp
```
![images](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile6.uf.tistory.com%2Fimage%2F99D8F6415CFFC3073165AA)
```sql
CASE WHEN 표현식 
이는 DECODE의 가독성을 조금 더 올리고 오라클 SQL말고 범위나 특정 조건을 사용해야하는 환경이나 
범용성이 높게 사용하는 ORACLE 방식의 case문이다. 이 역시 else를 생략할 수 있으며 사용법은 아래와 같다. 

|| IF문 방식 
SELECT ename
     , deptno
     , CASE WHEN deptno = '10' THEN 'New York'
            WHEN deptno = '20' THEN 'Dallas'
            ELSE 'Unknown'
       END AS loc_name
  FROM emp
 WHERE job = 'MANAGER'
 
 || Switch문 방식
 SELECT ename
     , deptno
     , CASE deptno 
            WHEN 10 THEN 'New York'
            WHEN 20 THEN 'Dallas'
            ELSE 'Unknown'
       END AS loc_name
  FROM scott.emp
 WHERE job = 'MANAGER'
```
![images](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F03vYC%2FbtqE5fwA1US%2FUf4jRvoPOFKFeEYGBcuZ0k%2Fimg.png)

#### SQL 날짜함수
- SYSDATE : 현재 시스템 일자 반환
- ADD_MONTHS(date,int) : date에 int 수 만큼 월을 더한 날짜 반환
- MONTHS_BETWEEN(date1,date2) : date1을 기준으로 두 날짜 사이의 개월 수 반환 
- LAST_DAY(date) : date의 월말일 반환
- ROUND(date, format) : format에 따라 반올림한 날짜 반환
- TRUNC(date,format) : format에 따라 잘라낸 날짜 반환
- NEXT_DAY(date,char) : date기준으로 char에 명시한 요일의 날짜를 반환
```sql 
NEXT_DAY 
기본적으로 date에서 8을 빼주면 아래와 같이 이전과 다음을 동시에 구할 수 있다. 
그리고 아래와같은 표처럼 한글을 입력하거나 영어를 입력하거나 어떠한 값을 대입하더라도 값을 구할 수 있다.
SELECT SYSDATE
     , NEXT_DAY(SYSDATE-8,'SUN') prev_sunday --이전 일요일
     , NEXT_DAY(SYSDATE,'SUN')   next_sunday --다음 일요일
  FROM DUAL
```

#### SQL 변환함수 
- TO_CHAR(char or date , format)  : 숫자나 날짜를 format에 맞는 문자로 변환 마리아DB의 DATE_FORMAT과 같은 개념이다.                                                                   ex) to_char(sysdate , 'YYYY/MM/DD'), to_char(12345, 'L9,999.99')
- TO_NUMBER(char,format) : data를 format에 맞는 숫자로 변환
- TO_DATE(char, format) : char를 format에 맞는 날짜로 변환
- TO_TIMESTAMP(char,format) : char을 format에 맞는 타임스탬프로 변환

#### NULL 관련 함수 
- NVL(input1,input2) : input1이 null이면 input2를 반환 마리아DB의 IFNULL과 같은 개념이다. 
- LNNVL(조건식) : Not과 같은 의미이다. 조건식의 결과가 false이거나 unknown이면 true를 , true이면 false를 반환한다.
- NULLIF(input1, input2) : input1과 input2가 동일한 값이면 null을 아니면 input1을 반환한다.


* * *

## WHERE & JOIN 
- 기본적으로 WHERE과 JOIN에서의 조건절을 거는 위치에 따라서 결과 값은 다르게 나온다.
- JOIN에서는 INNER나 OUTER를 기점으로 기준이 되는 행에 따라서 우측 테이블의 데이터가 있던 없던 출력되기에 NULL 값이 나온다.
- JOIN에 조건을 걸고 출력을 하면 조건에 해당하지 않는 값이여도 NULL로 표기가 되며  
- WHERE에 조건을 걸고 출력하면 조건에 해당하지 않는 값은 출력이 되지 않는다. 
- INNER JOIN을 하게되면 WHERE절이나 JOIN절에 조건을 어디에다가 달아도 상관이 없다.
 
```
-기존 테이블 예시- 

test1      test2
aa|bb      aa|cc
-----      -----
1 | 4      1 | 7
2 | 5      2 | 8
3 | 6
```

```sql
1)
SELECT *
FROM test1 a LEFT JOIN test2 b
ON (a.aa = b.aa)
WHERE b.cc = 7;

2)
SELECT *
FROM test1 a LEFT JOIN test2 b
ON (a.aa = b.aa AND b.cc = 7);
```

```sql
1)
1 | 4 | 1 | 7

2)
1 | 4 | 1    | 7
2 | 5 | null | null
3 | 6 | null | null

```   
## PARTITION BY vs GROUP BY
- GROUP BY는 데이터를 요약해서 표로 나타내주는 문법이다.
- PARTION BY는 데이터 전체를 표로 나타낸주는 문법이다. 
- PARTION BY는 함수() OVER(PARTITION BY 테이블명) 으로 정의한다.
- GROUP BY는 SELECT 절에서 함수()를 선언하고 맨 마지막에 GROUP BY 테이블명 으로 정의한다.   
```sql
-GROUP BY
SELECT Continent
	   ,SUM(GNP)
FROM world.country
GROUP BY Continent;

-PARTITION BY 
SELECT Continent
	   ,SUM(GNP) OVER(PARTITION BY Continent)
FROM world.country;
```
#### 실행결과 
![images](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FboxQJF%2Fbtq6VDY4XFp%2Fc7Fee6yWKejd2whKAyBrB1%2Fimg.png)   
![images](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc24lEE%2Fbtq6Wv0zFd5%2F2aXK8DkoOznE7hTfxJvlNK%2Fimg.png)

## SQL LOB 
- LOB은 TEXT, 그래픽, 이미지, 비디오, 사운드 등 구조화되지 않은 대형 데이터를 저장하는데 사용한다.
- 일반적으로 테이블에 저장되는 구조화된 데이터들은 크기가 작지만, 멀티미디어 데이터는 크기가 크다.
- 크기가 큰 데이터는 DB에 저장하기 힘들기 때문에 OS상 존재하는 파일을 데이터베이스가 접근하게 된다.
- LONG, LONG RAW 데이터 유형은 예전에 사용던 것이고, 현재는 대부분 LOB 데이터 유형을 사용한다.
- TO_LOB 함수를 이용하여 LONG 및 LONG RAW 를 LOB 으로 변경할 수 있다.
- DBMX_LOB를 사용하여 기존에 문자열 형식으로 데이터를 주고 받는것이 아닌 바이트형식으로 주고받기 때문에 속도면에서 DBMS_LOB를 사용하는것이 유리하다.

#### 종류
   - CLOB: 문자 대형 객체 (Character). Oracle Server는 CLOB과 VARCHAR2 사이에 암시적 변환을 수행한다.
   - BLOB: 이진 대형 객체 (Binary). 이미지, 동영상, MP3 등... 
   - NCLOB: 내셔널 문자 대형 객체 (National). 오라클에서 정의되는 National Character Set을 따르는 문자.
   - BFILE: OS에 저장되는 이진 파일의 이름과 위치를 저장. 읽기 전용 모드로만 액세스 가능.

#### 데이터베이스 내부, 외부에 따라
   - 내부 : BLOB, CLOB, NCLOB - Table에 LOB 형식의 컬럼을 생성하고 이곳에 데이터의 실제위치를 가리키는 Locator(위치자) 저장.
   - 외부 : BFILE

#### 특징
- 하나의 테이블에 여러 개의 LOB 열(column) 가능
- 최고 4GB까지 저장
- SELECT로 위치자 반환
- 순서대로 또는 순서없이 데이터 저장
- 임의적 데이터 액세스
 

#### LOB 구성
- LOB 값 : 저장될 실제 객체를 구성하는 데이터
- LOB 위치자 : 데이터베이스에 저장된 LOB값의 위치에 대한 포인터
- LOB열에는 데이터가 없고 LOB 위치자만 들어있다.
