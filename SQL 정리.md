conn system(ID)/system(암호)

alter user hr identified by hr account unlock;

conn hr/hr

SQL> set pagesize 100; 한 페이지에 100줄
SQL> set linesize 150; 한 라인에 150자



### SQL 종류

* 테이블 생성 - 변경 - 삭제
  * 데이터 저장 구조 정의 언어
  * Data Definition lang. --> DDL
* 테이블에 데이터 저장-수정-삭제
  * 데이터 조작언어
  * DATA MANIPULATION LANG. -->DML
* 계정 생성 - DB 접속 허용 SQL
  * system 계정
  * DATA CONTROLL LANG.-->DCL
* 트랜잭션 제어 언어
  * TRANSACTION CONTROLL LANG -->TCL
  * DATA QUERY LANG--->DQL

| DDL     | create table...<br />alter table<br />drop table |
| ------- | ------------------------------------------------ |
| **dml** | insert...<br />update<br />delete                |
| **dcl** | grant, revoke<br />새로운 계정 생성시 사용       |
| **tcl** | commit<br />rollback                             |
| **dql** | select                                           |

### hr 8개 테이블 조회 실습

```sql
conn hr/hr;
select*from tab; --->테이블 목록 조회
```

* 문법

  * select조회컬럼from 테이블명;

  * ex) employees 테이블에서 first_name 열 조회

    ```sq
    select first_name from employees;
    ```

  * ex)employess 테이블에서 first_name, last_name열 조회

              ```sql
select first_name, last_name from employees;
cf) select * from employees;(employees 모든 정보 조회)
              ```

* 급여 컬럼 - salary

  ```
  select first_name, salary from employees;
  이름과 급여(월급) 출력
  select first_name, salary, salary*12 from employees;
  급여(연봉) 출력 
  
  --실제컬럼명을 조회 임시 변경 -alias
  select first_name as 이름, salary as 월급, salary*12as 연봉 from employees;
  이름/월급/연봉으로 출력
  
  salary + commission_pct
  ====> 숫자타입
  ```

* employees 107명 사원 정보 저장

  *  직종코드 종류별 1개만 조회(중복제외) 출력

    ```sql
    select job_id from employees;
    직종코드 출력 (중복) 107개
    select distinct job_id from employees;
    직종코드 출력 (중복제외)19개
    ```

  * upper 함수

    ```sql
    select first_name, upper(first_name) as a from employees;
    first name 출력 first name(대문자로) a라는 이름으로 출력
    ```

  * employess테이블 급여 salary 10000 이상의 사원의 이름과 급여 출력

    ```sql
    select first_name,salary from employees where salary>=10000;
    salary 10000이상인 사원들의 이름과 급여 출력
    
    select first_name, salary from employees where salary>=10000 and salary<=11000;
    salary 10000이상 11000이하인 사원들의 이름과 급여 출력
    ```

    | 산술연산자      | + - * /                                                      |
    | --------------- | ------------------------------------------------------------ |
    | 비교연산자      | >/ >=/ </ <=/ !=(<>) /=                                      |
    | 논리연산자      | not and or                                                   |
    | 목록연산자      | in (....)                                                    |
    | 유사연산자      | %- 모든문자,문자갯수,상관없다(0개가능)<br />_ - 모든문자 1개 |
    | 범위연산자      | between ~ and                                                |
    | null처리 연산자 | is null<br />is not null (null제외)                          |

  * employee_id 컬럼 사번 50 100 150 200 250 300인 사원  사번, 이름 조회

    ```sql
    select employee_id,first_name from employees where employee_id=50 or employee_id=100 or employee_id=150 or employee_id=200 or employee_id=250 or employee_id=300;
    
    select employee_id,first_name from employees where employee_id in(50,100,150,200,250,300); 
    ```

    

  * employees 테이블에서 first_name Jennifer

    ```sql
    select first_name from employees where first_name='Jennifer';
    ```

  * employees 테이블에서 first_name이 J로 시작하는 사람 찾기

  * (암호나 ' ' 안에있는 문자데이터 ===> 대소문자 구분)

    ```sql
    select first_name from employees where first_name like 'J%';
    ```

  * employees 테이블에서 first_name r로 끝나는 사원 찾기

    ``` sql
    select first_name from employees where first_name like '%r';
    ```

  * employess 테이블에서 first_name er 을 포함하는 사원찾기

    ```sql
    select first_name from employees where first_name like '%er%';
    ```

  *  employees 테이블 job_id 컬럼에서 manager 직종 조회

     ( 단 MANAGER 직종은 MAN으로 끝난다)

    ```sql
    select job_id from employees where job_id like '%MAN';
    select job_id from employees where job_id like '___MAN';
    select job_id from employees where job_id like '__\_MAN' escape '\';
    ```

  * employees 테이블 first_name 이름, hire_date 컬럼(입사일 ) 조회

        ```sql
  select first_name, hire_date from employees where hire_date like '05%';
  05년도 입사자만 조회('05_____');
  select first_name, hire_date from employees where hire_date between '05/01/01' and '05/12/31';
  05년도 입사자만 조회
  select first_name, hire_date from employees where hire_date >= '05/01/01';
  05년도 이후 입사자 ( date 크다의 의미는 최근)
        ```

  *  order by 사용하기

    asc는 생략가능 // desc는 생략 불가
    order by 컬럼명 or index or alias  

    ```sql
    select first_name from employees order by first_name asc;
    알파벳 순서대로 출력
    select first_name from employees order by first_name desc;
    알파벳 역순대로 출력
    select salary from employees order by salary asc;
    급여 작은사람 먼저 출력
    select salary from employees order by salary desc;
    급여 많은사람 먼저 출력
    select hire_date from employees order by hire_date asc;
    오래된 날짜부터 출력
    select hire_date from employees order by hire_date desc;
    최근 날짜부터 출력
    select first_name, salary from employees order by salary desc, 
    first_name asc;
    급여 많은 사람 먼저 출력하는데 같은 급여라면이름 알파벳 순으로 출력
    ```

  * Null 처리 연산자 - 오라클 모든 타입의 데이터 값이 없으면 null -공백

    ```sql
    select commission_pct from employees where commission_pct is not null;
    ```

  * 최근 입사자 5명만 조회 (subquery 사용 - 정렬 이후 상위 몇개 가져오는 데 유용)

    ```sql
    select rownum,hire_date from employees order by hire_date desc;
    -->> 로우넘 순서 뒤섞임
    select rownum,hire_date from(select*from employees order by hire_date desc) where rownum <=5;
    ```

### sql 작성순서 조회순서

| 작성순서                                  | 실행순서                                                     |
| ----------------------------------------- | ------------------------------------------------------------ |
| select<br />from<br />where<br />order by | from 테이블찾는다<br />where 조건에 맞는 레코드를 찾는다<br />select 컬럼 조회한다<br />order by 정렬 기준 컬럼 정렬한다 = 순서 뒤바뀐다 |

* 다른테이블 정보 혼합 조회

  * Sales 부서에 근무하는 사원의 이름조회	

    ```sql
    select first_name, department_id from employees where department_id=(select department_id from departments where department_name='Sales');
    ```

  * Susan과 같은 부서에 일하는 사람 job_id와 salary

    ```sql
    select job_id, salary from employees where department_id =
    (select department_id from employees where first_name = 'Susan');
    --->subquery 리턴값이 한개여서 = 으로 가능하지만 in 써주는게 좋음
    ```

  * William과 같은 직종을 가진 사원의 부서,급여

    ```sql
    select department_id, salary, job_id from employees
    where job_id in (select job_id from employees where first_name = 'William');
    ```

  * Susan보다 더 급여를 많이 받는 사원의 사번, 이름, 급여 조회

    ```sql
    select employee_id, first_name, salary
    from employees
    where salary >= (select salary from employees where first_name = 'Susan');
    ```

  * William보다 더 급여를 많이 받거나 동일하게 받는 사원의 사번 이름 급여 조회

    ```sql
    select employee_id, first_name, salary
    from employees
    where salary >=all (select salary from employees where first_name =  'William');
    ---> 여러개 값중에 가장 큰값보다 크거나 같다 (>=all)
    select employee_id, first_name, salary
    from employees
    where salary >=any (select salary from employees where first_name =  'William');
    ---->여러개 값 각각보다 크기만 하면 나온다 (>=any)
    ```

| select ..(select) |                                                              |
| ----------------- | ------------------------------------------------------------ |
| 단일행 리턴       | = / > / >= / !=                                              |
| 다중행리턴        | = -> in<br />!= -> not in<br />> all 값들 중에서 제일 큰값보다 커야함<br />> any 각각의 값보다 크면된다 |

```sql
SELECT first_name, salary, hire_date, department_id
FROM employees 
WHERE department_id in (30, 50, 80) and hire_date LIKE '__/10/__' and 
salary between 5000 and 17000 and commission_pct is not null 
ORDER BY hire_date, salary desc;
```



### 그룹함수

* 그룹함수 조회 select 절에 다른 컬럼 조회 불가!

*  단 group by 뒤 기술 컬럼 제외

  ```sql
  ---> 사원이름, 최대급여 조회
  select first_name, max(salary) from employees;
  --> first_name 107 개 max(salary) 1개로 오류
  
  SQL> select first_name salary
    2  from employees
    3  where salary = (select max(salary) from employees);
  ```

| 100      | 1개                                                          |
| -------- | ------------------------------------------------------------ |
| 200      | 1개                                                          |
| 4300     | 1개                                                          |
| sum      | 총합-숫자                                                    |
| avg      | 평균-숫자                                                    |
| count    | 갯수-숫자,문자,날짜 (기본적으로 null값 미포함//null값 포함하고 싶으면 * 컬럼 사용) |
| max      | 최대값-숫자,문자(사전 뒤에나오는 순서),날짜(최근날짜)        |
| min      | 최소값-숫자,문자(사전 앞에 나오는 순서),날짜(오래된 날짜)    |
| stdev    | 표준편차-숫자                                                |
| variance | 분산-숫자                                                    |

#### Group by

* Group by 뒤에 나온 컬럼은 그룹함수와 사용가능!
* select from where group order 순

```sql
--부서별&직종별 급여 합을 구해라
select department_id as 부서, job_id as 직종, sum(salary) as 부서직종별급여합
from employees
where department_id is not null
group by department_id,job_id
order by department_id;
```

#### having

```sql
--부서별로 급여 총합 조회하되 부서별 급여 총합이 10000미만인 부서만 출력
select department_id, sum(salary)
from employees
where sum(salary)<10000
group by department_id;
----> 오류 (실행순서 from -> where -> group -> select)
----> where 절에는 그룹함수 조건 사용 불가!

select department_id, sum(salary)
from employees
group by department_id
having sum(salary)<10000;
----> (실행순서 from -> (where)(일반조건식 그룹합수 제외) 
----  -> group ->having(그룹함수조건)-> select)


--부서별로 급여 총합 조회하되 사원의 급여가 5000미만은 제외하고 
--부서별 급여 총합이 50000이상인 부서의 결과만 조회
select department_id, sum(salary)
from employees
where salary >5000
group by department_id
having sum(salary)>=50000
order by sum(salary) desc, department_id;
```

#### roll up//cube (부분합을 보여준다)

```sql
select department_id as 부서, job_id as 직종, sum(salary) as 부서직종별급여합
from employees
where department_id is not null
group by rollup (department_id,job_id);
group by cube (department_id,job_id);
```

### 2021 03 25

### 7장 

* 데이터형식 오라클 형식 31개

  * |  문자  | CHAR, VARCHAR2 -> 영문 -1바이트/ 한글 -3바이트<br />CHAR(50) --> 'ABC'--->[ABC+47바이트]<br />VARCHAR2(50)--->'ABC'--->[ABC] 최대50바이트저장 /메모리효율적<br />NCHAR, NVARCHAR2 -> 유니코드 2바이트 한글<br />'데이터'-->대소문자 구분 |
    | :----: | ------------------------------------------------------------ |
    |  정수  | BINARY_INT, INT,NUMBER(8)                                    |
    |  실수  | BINARY_FLOAT, FLOAT, NUMBER(8,2) -->정수6자리 소수점2자리    |
    |  날짜  | 초 표현 -> DATE<br />1/1000초 표현 -> TIMESTATMP TIMESTAMPXXXX |
    | 대용량 | CLOB - 1TB 문자열 대용량 데이터<br />BLOB - 1TB 바이너리 대용량 데이터<br />BFILE, BIN |

    

* 일반함수

  * SELECT SYSDATE FROM DUAL; (날짜 RR/MM/DD)

* 형변환

  * cast

    ```sql
    select sysdate from dual;
    select cast(sysdate as timestamp) from dual;
    select cast(12345.678 as number(10,2)) from dual; -->12345.68
    ```

  * to_char/to_number/to_date

    ​            --->to_char <----------

    ​     숫자           문자         날짜 

    <-----to_number  to_date---->

    ```sql
    select 100+ 200 from dual;
    select '100' + '200' from dual;-->'0-9구성' 자동 숫자 변환
    select '123,456' + '200' from dual;
    select to_number('123,456','999,999') + '200' from dual;
    --> '123,456' 숫자변환 to_number('123,456','999,999')--->123456
    --> to_number('숫자로변환할 데이터', '데이터구성형식설명')
    
    select to_char(123456, '$999,999') from dual;
    -->to_char(문자로변환할 데이터, '데이터구성형식설명')
    select to_char(123456789, '$999,999') from dual;-->오류
    select to_char(123456.789, '$999,999') from dual;
    --->정수 6자리 표시하겠다 // 소수점은 첫번째자리에서 반올림
    select to_char(123456.789, '$000,999.99') from dual;
    --->소수점 둘째자리까지 표시 세번째자리에서 반올림
    
    
    select table_name from DICT where table_name like '&NLS&'
    --->NLS포함테이블
    desc NLS_SESSION_PARAMETERS;
    select * from nls_session_parameters
    where PARAMETER = 'NLS_DATE_FORMAT';
    
    select sysdate from dual; ---> 21/03/25
    select to_char(sysdate, 'YYYY/MM/DD DAY HH24:MI:SS') FROM DUAL;
     -->2021/03/25 (요일) 13:39:11로 바꿔주기
     select to_char(sysdate, 'YYYY"년도" MM"월" DD"일" DAY HH"시" MI"분" SS"초"') FROM DUAL;
     --> 2021년도 03월 25일 01시 39분 10초
      select to_char(sysdate, 'FMYYYY"년도" MM"월" DD"일" DAY HH"시" MI"분" SS"초"') FROM DUAL;
       --> FM 붙이면 불필요한 0 미출력 2021년도 3월 25일 1시 39분 10초
       
    select sysdate +1 from dual;
    select '21/03/25' + 1 from dual; -->오류
    select to_date('21/03/25', 'yy/mm/dd') +1 from dual;
    select sysdate +365 from dual;
    -->오늘로부터 1년후 날짜 조회
    select to_char(sysdate, 'yyyy')+1 from dual; -->2022
    
    --->05년도 입사자 조회
    select hire_Date from employees where hire_date like '05/%';
    
    select hire_Date from employees 
    where to_char(hire_date, 'yyyy') = '2005';
    
    select hire_date from employees
    where instr(hire_date, '05') = 1;
    
    
    ```

* 기호

  | 데이터형식입력                             | 표시             |
  | ------------------------------------------ | ---------------- |
  | ,                                          | , 기호           |
  | L                                          | \                |
  | 9                                          | 1자리숫자        |
  | 0                                          | 1자리숫자        |
  | YY- 2000년대<br />YYYY<br />RR(0-49,50-99) | 년도             |
  | MM                                         | 월               |
  | DD                                         | 일               |
  | HH<br />HH24                               | 시간<br />24시간 |
  | MI                                         | 분               |
  | SS                                         | 초               |
  | DAY                                        | 요일             |

* 함수

| 함수           |                                                              |
| -------------- | ------------------------------------------------------------ |
| 타입변환함수   | cast, to_date, to_char, to_number                            |
| 그룹함수       | sum avg min max count stdev variance                         |
| 문자데이터함수 | substr,Itrim,rtrim                                           |
| 숫자데이터함수 | mod- 나머지함수 mod(10,3)<br />round- 반올림<br />round (3.6789, 0); 4 round(3.6789,2); 3.68 round(333.6789, -1); 330<br />trunc- 버림  //round랑 사용법 똑같다 |
| 날짜데이터함수 | sysdate / systimestamp - 1/1000초까지<br />add_months, months_between |
| 순위함수       | rownum, row_number(), rank(), dense_rank()<br />순위함수()over(partition by 분류컬럼명 order by 컬럼명) |
| null처리함수   | nvl(salary,0) --> salary 값이 null이면 0으로 변경<br />nvl(컬럼명정수/컬럼명문자열, null대체값정수/null대체값정수 + 문자열) |

```sql
--->같은해 입사년도 급여 평균
select substr(hire_Date,1,2) as 입사년도, trunc(avg(salary),0) as 급여평균
from employees
group by substr(hire_date,1,2)
order by avg(salary) desc;

--->현재날짜에서 1달 더할때
select add_months(sysdate,1) from dual;

-->입사한지 경과 년수 조회
select round((sysdate-hire_date)/365) from employees;

-->입사한지 경과 개월수 조회
select months_between(sysdate,hire_Date) from employees;

-->row_number 함수 급여가 많은 사원부터 순위
select first_name as 이름, salary as 급여,
row_number()over(order by salary desc)as 급여순위 from employees;

select first_name as 이름, salary as 급여, department_id as 부서,
row_number()over(partition by department_id order by salary desc)as 급여순위 from employees order by department_id;


select first_name as 이름, salary as 급여,
rank()over(order by salary desc)as 급여순위 from employees;
--->중복값있으면 같은 등수로 1/2/2/4

select first_name as 이름, salary as 급여,
dense_rank()over(order by salary desc)as 급여순위 from employees;
---->중복값있으면 같은 등수 + 바로이어서 등수 매기기 1/2/2/3

select first_name, nvl(to_char(commission_pct),'보너스없음') as "보 너 스" from employees;
---->별칭 공백 넣고 싶으면 ""안에 넣기!
```

```sql
1. 이름이 'adam' 인 직원의 급여와 입사일을 조회하시오. 

select first_name from employees
where lower(first_name) = 'adam';

2. 나라 명이 'united states of america' 인 나라의 국가 코드를 조회하시오.
select country_id
from countries
where instr(lower(country_name) ,'united states of america') =1;


3. 'Adam의 입사일은 05/11/2 이고, 급여는 7,000\ 입니다.' 의 형식으로 직원
정보를 조회하시오.
select first_name||'의 입사일은' ||to_char(hire_date,'yy/mm/fmdd')||'이고, 급여는'|| ltrim(to_char(salary,'999,999L')) || '입니다.'  from employees;


직원정보

Adam의 입사일은 05/11/2 이고, 급여는 7,000 입니다. 
......

4. 이름이 5글자 이하인 직원들의 이름, 급여, 입사일을 조회하시오.
select first_name, salary, hire_date
from employees
where length(first_name) <= 5 ;


5. 06년도에 입사한 직원의 이름, 입사일을 조회하시오.
select first_name,hire_date
from employees
where instr(hire_date, '06') = 1; 

6. 10년 이상 장기 근속한 직원들의 이름, 입사일, 급여, 근무년차를 조회하시오.
select first_name, hire_date, salary, round((sysdate-hire_date)/365)
from employees
where round((sysdate-hire_date)/365) >=10;

7. employees 테이블에서 
직종이(job_id) 'st_clerk'인 사원 중에서 급여가 1500 이상인 사원의
first_name, job_id, salary 를 조회하시오. 단 이름은 모두 대문자로 출력하시오.
select upper(first_name), job_id, salary from employees
where instr(lower(job_id), 'st_clerk') =1 and salary>1500;

8. 급여가 20000 이상인 직종(job_id)의
job_id, salary 조회하시오.
단, salary는 10자리로 출력하되 공백은 '0'으로 표시하시오.

select job_id, to_number(nvl(salary, 0),9999999999)
from employees
where salary>=20000;

9. 직원의 이름, 급여, 직원의 관리자 사번을 조회하시오. 단, 관리자가 없는 직원은
   '<관리자 없음>'이 출력되도록 합니다.
   
   select first_name, salary, nvl(to_char(manager_id),'관리자 없음')
   from employees ; 

```



* JOIN-SELECT

