# SELECT / FROM / LIMIT

<br/>

## 1. SELECT 문

### 1.1. SELECT문 사용

- 테이블에 입력된 데이터를 조회하기 위해서 `SELECT`문을 사용한다.
- `SELECT`문은 특정 칼럼이나 특정 행만을 조회할 수 있다.

```mysql
SELECT *  # 조회를 원하는 칼럼(Column)을 선택
FROM EMP # 조회를 원하는 테이블을 지정
WHERE 사원번호=1000; # 조회를 원하는 데이터의 조건을 지정
```

- 위의 `SELECT` 문에서 `EMP` 테이블의 모든 칼럼 `*` 출력하낟.
- 단, `WHERE` 절에 있는 조건문에 있는 행만 조회한다.

### 1.2 SELECT 문법

|     SELECT문 문법     |                             설명                             |
| :-------------------: | :----------------------------------------------------------: |
|       SELECT *        | - 모든 칼럼을 출력한다.<br />- `*` 는 모든 칼럼을 의미한다.  |
|       FROM EMP        | - FROM 절에는 테이블명을 쓴다.<br />- 즉, EMP 테이블을 지정했다. |
| WHERE 사원버호 = 1000 | - EMP 테이블에서 사원번호가1000번인 행을 조회한다.<br />즉, 조건문을 지정한다. |

### 1.3 SELECT 칼럼 지정

| 사용 예제                       | 설명                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| SELECT EMPNO, ENAME FROM EMP;   | EMP 테이블의 모든 행에서 EMPNO와 ENAME 칼럼만 출력한다.      |
| SELECT * FROM EMP;              | EMP 테이블의 모든 칼럼과 모든 행을 조회한다.                 |
| SELECT ENAME \|\|'님' FROM EMP; | - EMP 테이블의 모든 행에서 ENAME 칼럼을 조회한다.<br />- 단, ENAME 칼럼 뒤에 '님' 이라는 문자를 결합한다. |

### 1.4 LIMIT 사용

- `LIMIT` : 상위 몇개를 추출할 떄 쓰인다.

```mysql
SELECT CUSTOMERName, Address
FROM CUSTOMERS
LIMIT 10 
```

- CUSTOMER 테이블에서 `CUSTOMERName` 칼럼과 `Address` 칼럼을 조회한다.
- 단, 상단의 10개만 조회한다.

<br/><br/>

## 2.문제풀이

### 2.1. SELECT ALL

[바로가기](https://www.hackerrank.com/challenges/select-all-sql/problem?isFullScreen=true)

<div class="alert alert-block alert-warning">
<strong><font color="blue" size="3em">Query all columns (attributes) for every row in the CITY table. The CITY table is described as follows:</font></strong><br>
테스트: CITY 테이블에서 모든 COLOUM을 조회하라.
</div>

![](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

```mysql
SELECT *
FROM CITY
```



### 2.2. Whether Observation Station1

[바로가기](https://www.hackerrank.com/challenges/weather-observation-station-1/problem?isFullScreen=true)

<div class="alert alert-block alert-warning">
<strong><font color="blue" size="3em">Query a list of CITY and STATE from the STATION table. The STATION table is described as follows:</font></strong><br>
테스트: STATION 테이블에서 모든 CITY와 STATE 컬럼을 조회하라.
</div>

![](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

```mysql
SELECT city, state
FROM station
```

- SQL이 대소문자를 강조하는 것은 아니지만,
- 예약어(`SELECT` , `FROM`)는 대체적으로 대문자로 쓰이고, 나머지 문자들은 소문자로 사용한다. (약속)