# 데이터 순서 정렬하기

<br/>

## 1. ORDER BY

### 1.1. ORDER BY 를 사용한 정렬

- SELECT문을 사용할 때 `Order by`를 같이 사용할 수 있다.
- `Order by` 는 데이터를 오름차순(Ascending) 혹은 내림차순(Descending)으로 출력한다.
- `Order by` 가 정렬하는 시점은 모든 실행이 끝난 후에 데이터를 출력해 주기 바로 전이다.
- `Order by` 는 정렬을 하기 때문에 데이터 베이스 메모리를 많이 사용하게 된다. 즉, 대량의 데이터를 정렬하게 되면 정렬로 인한 **성능 저하** 가 발생한다.
- 정렬을 회피하기 위해서 인덱스(INDEX)를 생성할 때 사용자가 원하는 형태로 오름차순 혹은 내림차순으로 생성해야 한다.
- 특별한 지정이 없으면 `Order by`는 **오름차순** 으로 정렬한다.

```mysql
SELECT * 
FROM EMP
-- ENAME으로 오름차순 정렬하고 SAL로 내림차순 정렬한다.
ORDER BY ENAME, SAL DESC; 
```

- 여기서 `ENAME` 부분은 `ENAME ASC`와 같다. 왜냐하면 기본적으로 오름차순과 내림차순을 지정하지 않으면, 오름차순으로 정렬한다.
- 내림차순을 정렬하고 싶을 때는 `DESC`를 사용한다.

#### 참고

- Oracle 데이터베이스는 정렬을 위해서 메모리 내부에 할당된 `SORT_AREA_SIZE`를 사용한다. 만약 `SORT_AREA_SIZE` 가 너무 작으면 성능 저하가 발생한다.

  

#### 1.1.1. 데이터 정렬하기 1

[바로가기](https://www.hackerrank.com/challenges/name-of-employees/problem?isFullScreen=true)

```mysql
-- 데이터 정렬하기
SELECT * 
FROM Customers
-- WHERE 절
ORDER BY customerID DESC
```

- 예약어의 순서는 `SELECT` > `FROM` > `WHERE` > `ORDER BY` 로 `ORDER BY` 는 맨 마지막에 온다.

#### 1.1.2 데이터 정렬하기 2

- price 칼럼이 20이상인 것을 출력하는데, 내림차순으로 출력하시오.

```mysql
-- 데이터 정렬하기
SELECT * 
FROM Products
WHERE price >= 20
ORDER BY price DESC
LIMIT 1
```

- 가장 큰 값만 출력하고 싶다면 `LIMIT 1` 을 사용하면 된다. 
- 반대로 가장 작은 값을 출력하고 싶다면 다음과 `DESC`대신 ASC를 사용한다.

```mysql
-- 데이터 정렬하기
SELECT * 
FROM Products
WHERE price >= 20
ORDER BY price ASC
LIMIT 1
```

<br/><br/>



## 2. 문자열 자르기

### 2.1. LEFT

- LEFT(컬럼명 또는 문자열, 문자열의 길이)
- SELECT LEFT("20140323",4)
  - 2014

### 2.2. RIGH

- RIGHT(컬럼명 또는 문자열, 문자열의 길이)
- SELECT RIGHT('20140323',4)
  - 0323

### 2.3. SUBSTRING

- SUBSTRING(컬럼명 또는 문자열, 시작위치, 길이) 
  =  SUBSTR()
- SUBSTR("20140323",1,4)
  - 2014
- SUBSTR("20140323",5)
  - 0323

<br/><br/>

## 3. 소수점 처리

### 3.1. CEIL

- CEIL() : 올림
  - SELECT CEIL(5.5)
- FLOOR() : 내림
  - SELECT FLOOR(5.5)
- ROUND() : 반올림
  - ROUND(5.5556901,4)
  - 5.5569

<br/><br/>

## 4.문제풀이

### 4.1. Employee Names

[바로가기](https://www.hackerrank.com/challenges/revising-the-select-query/problem?isFullScreen=true)

<div class="alert alert-block alert-warning">
<strong><font color="blue" size="3em">Write a query that prints a list of employee names (i.e.: the name attribute) from the Employee table in alphabetical order.</font></strong><br>
테스트: 직원이름을 알파벳순으로 정렬하라
</div>

![](https://s3.amazonaws.com/hr-challenge-images/19629/1458557872-4396838885-ScreenShot2016-03-21at4.27.13PM.png)

![](https://s3.amazonaws.com/hr-challenge-images/19629/1458558202-9a8721e44b-ScreenShot2016-03-21at4.32.59PM.png)

```mysql
SELECT name
FROM Employee
ORDER BY name ASC
```



### 4.2. Employee Salaries

[바로가기](https://www.hackerrank.com/challenges/salary-of-employees/problem?isFullScreen=true)

<div class="alert alert-block alert-warning">
<strong><font color="blue" size="3em">Write a query that prints a list of employee names (i.e.: the name attribute) for employees in Employee having a salary greater than  per month who have been employees for less than  months. Sort your result by ascending employee_id.</font></strong><br>
테스트: 
</div>

![](https://s3.amazonaws.com/hr-challenge-images/19629/1458557872-4396838885-ScreenShot2016-03-21at4.27.13PM.png)

![](https://s3.amazonaws.com/hr-challenge-images/19630/1458558612-af3da3ceb7-ScreenShot2016-03-21at4.32.59PM.png)

```mysql
SELECT name -- 이름 출력
FROM Employee -- 테이블 이름
WHERE months < 10  -- 고용된지 10달 미만
AND salary >= 2000  -- 월급 2000불 초과
ORDER BY employee_id ASC -- employee_ID정렬(오름차순)
```



### 4.3. Higher Than 75 Marks

[바로가기](https://www.hackerrank.com/challenges/salary-of-employees/problem?isFullScreen=true)

<div class="alert alert-block alert-warning">
<strong><font color="blue" size="3em">Query the Name of any student in STUDENTS who scored higher than  Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.</font></strong><br>
테스트: 
</div>

![](https://s3.amazonaws.com/hr-challenge-images/12896/1443815243-94b941f556-1.png)

![](https://s3.amazonaws.com/hr-challenge-images/12896/1443815209-cf4b260993-2.png)

```mysql
SELECT name
FROM Students
WHERE marks > 75
ORDER BY RIGHT(name, 3), id
```

- 오른쪽 끝에서 문자열을 자르고 싶다면 : `RIGHT`를 사용한다.
- `OREDER BY` 조건에서 다음의 조건을 붙이기 위해서 `,`를 사용한다.
  - 그 후에 다음의 조건이 될 컬럼 `id`를 입력한다.



### 4.4. Weather Observation Station 15

[바로가기](https://www.hackerrank.com/challenges/salary-of-employees/problem?isFullScreen=true)

<div class="alert alert-block alert-warning">
<strong><font color="blue" size="3em">Query the Western Longitude (LONG_W) for the largest Northern Latitude (LAT_N) in STATION that is less than . Round your answer to  decimal places.</font></strong><br>
테스트: 
</div>

![](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

```mysql
SELECT ROUND(Long_W,4) -- Round 4 decimal placses 4자리까지만 남기고 반올림
FROM station -- 테이블명
WHERE LAT_N < 137.2345 -- less than 137.2345
ORDER BY LAT_N DESC -- 내림차순을 하면 최대값이 맨 위로 올라온다.
LIMIT 1 -- 그중 1개를 출력하면, 제일 큰 수 하나가 출력이 된다.
```

