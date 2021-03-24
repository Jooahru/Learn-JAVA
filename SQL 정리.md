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



