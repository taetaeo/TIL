# 조건에 맞는 데이터 검색하기

<br/>

## 1. 비교연산자

### 1.1. WHERE문이 사용하는 연산자

- WHERE문이 사용할 수 있는 연산자는 `비교연산자`, `부정 비교 연산자`, `논리 연산자` , `SQL연산자`, `부정SQL연산자` 가 있다.

#### 1.1.1. 비교연산자

| 비교연산자 | 설명                       |
| :--------: | :------------------------- |
|     =      | 같은 것을 조회한다.        |
|     <      | 작은 것을 조회한다.        |
|     <=     | 작거나 같은 것을 조회한다. |
|     >      | 큰 것을 조회한다           |
|     >=     | 크거나 같은 것을 조회한다. |

- 비교연사자는 특정 컬럼이 특정 값을 가지는 데이터만 불러오기 위해서 사용한다.

```mysql
SELECT *
FROM CUSTOMERS
WHERE CustomerName < "B" AND Country = 'Germany'
-- 비교연산자, 특정 컬럼이 특정 값을 가지는 데이터만 불러오기 위해서 사용
-- =, <>, >=, <=, >, < 등이 있다.
```

#### 1.1.2. 부정 비교 연산자

|  비교연산자  | 설명                     |
| :----------: | :----------------------- |
|      !=      | 같지 않은 것을 조회한다. |
|      ^=      | 같지 않은 것을 조회한다. |
|      <>      | 같지 않은 것을 조회한다. |
| NOT 칼럼명 = | 같지 않은 것을 조회한다. |
| NOT 칼럼명 > | 크지 않는 것을 조회한다. |

#### 1.1.3. 논리연산자

| 비교연산자 | 설명                                                        |
| :--------: | ----------------------------------------------------------- |
|    AND     | 조건을 **모두** 만족해야 참(True)이 된다.                   |
|     OR     | 조건 중 하나만 만족해도 참(True)이 된다.                    |
|    NOT     | 참이면 거짓(Fasle)으로 바꾸고 거짓이면 참(True)으로 바꾼다. |

#### 다른 코드이지만, 같은 의미로 쓰이는 경우 (IN, OR)

```mysql
SELECT *
FROM CUSTOMERS
-- WHERE country = 'Germany' OR country = 'France'
WHERE country IN ('Germany', 'France')
```

- `WHERE country = 'Germany' OR country = 'France'` 과 `WHERE country IN ('Germany', 'France')` 은 결국 같은 값을 조회한다.
- `OR` 을 사용하게되면 코드가 너무 길어지는 것을 대비하여 `IN`을 사용하여 간략하게 줄일 수 있다.

#### 1.1.4. SQL연산자

|      비교연산자      | 설명                                                   |
| :------------------: | :----------------------------------------------------- |
| LIKE '%비교 문자열%' | 비교 문자열을 조회한다. '%' 는 모든 값을 의미한다.     |
|   BETWEEN A AND B    | A와 B사이의 값을 조회한다.                             |
|      IN (list)       | OR 를 의미하며, list 값 중에 하나만 일치해도 조회된다. |
|       IS NULL        | NULL 값을 조회한다.                                    |

- BETWEEN을 사용한 예시

```mysql
SELECT *
FROM CUSTOMERS
-- 3과 5사이의 customerID를 조회한다.
WHERE customerID BETWEEN 3 AND 5
```

#### 1.1.5. 부정 SQL 연산자

|     비교연산자      | 설명                                     |
| :-----------------: | :--------------------------------------- |
| NOT BETWEEN A AND B | A와 B사이의 해당도지 않는 값을 조회한다. |
|    NOT IN (list)    | list와 불일치한 것을 조회한다.           |
|     IS NOT NULL     | NULL 값이 아닌 것을 조회한다.            |

- 아무것도 없는 컬럼을 출력

```mysql
SELECT *
FROM CUSTOMERS
WHERE customerID IS NULL
-- NULL, NaN (Not a Number)
```



<br/>

## 2. LIKE

### 2.1 LIKE 문 사용

- `Like` 문은 와일드카드를 사용해서 데이터를 조회할 수 있다.

#### 2.1.1. 와일드 카드

|  와일드카드   | 설명                                                         |
| :-----------: | :----------------------------------------------------------- |
|       %       | - 어떤 문자를 포함한 모든 것을 조회한다.<br />- 예를 들어 '조%'는 '조'로 시작하는 모든 문자를 조회한다. |
| _(underscore) | - 한 개인 단일 문자를 의미한다.                              |

- `%`를 사용하여 br로 시작하는 컬럼을 조회하기

```mysql
SELECT *
FROM CUSTOMERS
-- country 컬럼에서 br로 시작하는 컬럼만 조회한다.
WHERE country LIKE 'Br%'
```

- `_`를 사용하여 조회하기

```mysql
SELECT *
FROM CUSTOMERS
-- 글자수를 정확히 안다면 _ 를 사용하면 정교하게 데이터를 조회할 수 있다. 
WHERE country LIKE 'B_____'
```

- `%`를 찾고 싶을 때

```mysql
SELECT *
FROM CUSTOMERS
-- \를 사용하여 두자리수의 %기호를 가진 데이터를 조회한다.  
WHERE discount LIKE '__\%'
```





<br/><br/>

## 3.문제풀이

### 3.1. Revising the Select Query I

[바로가기](https://www.hackerrank.com/challenges/revising-the-select-query/problem?isFullScreen=true)

<div class="alert alert-block alert-warning">
<strong><font color="blue" size="3em">Query all columns for all American cities in the CITY table with populations larger than 100000. The CountryCode for America is USA. The CITY table is described as follows:</font></strong><br>
테스트: 
</div>

![](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

```mysql
SELECT name
FROM city
WHERE countrycode='USA' 
AND poppulation >= 100000
```



### 3.2. SELECT BY ID

[바로가기](https://www.hackerrank.com/challenges/select-by-id/problem?isFullScreen=true)

<div class="alert alert-block alert-warning">
<strong><font color="blue" size="3em">Query all columns for a city in CITY with the ID 1661. The CITY table is described as follows:</font></strong><br>
테스트: CITY 테이블에서 ID가 1661인 컬럼을 조회
</div>

![](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

```mysql
SELECT *
FROM CITY
WHERE ID = '1661'
```

### 3.3. Weather Observation Station 6

[바로가기](https://www.hackerrank.com/challenges/weather-observation-station-6/problem?isFullScreen=true)

<div class="alert alert-block alert-warning">
<strong><font color="blue" size="3em">Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates .The STATION table is described as follows:</font></strong><br>
테스트: 
</div>

![](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

```mysql
/*
중복을 막기 위해서 DISTINCT
*/

SELECT DISTINCT city
FROM station
WHERE city LIKE 'i%'
OR city LIKE 'e%'
OR city LIKE 'a%'
OR city LIKE 'o%'
OR city LIKE 'u%'
```

- 중복을 허용하지 않으려면 SELECT 뒤에 DISTINCT를 사용하면 된다.

### 3.4. Weather Observation Station 12

[바로가기](https://www.hackerrank.com/challenges/weather-observation-station-12/problem?isFullScreen=true)

<div class="alert alert-block alert-warning">
<strong><font color="blue" size="3em">Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.</font></strong><br>
테스트: 모음으로 시작하지도 끝나지도 않는 CITY 컬럼을 조회하라.
</div>

```mysql
SELECT DISTINCT city
FROM station
WHERE city NOT LIKE 'a%'
AND city NOT LIKE 'e%'
AND city NOT LIKE 'i%' 
AND city NOT LIKE 'o%'
AND city NOT LIKE 'u%' 
AND city NOT LIKE '%a' 
AND city NOT LIKE '%e' 
AND city NOT LIKE '%i' 
AND city NOT LIKE '%o'
AND city NOT LIKE '%u' 
```

- 중복을 허용하지 않기 위해서는 `DISTINCT`
- `NOT LIKE` : 허용하지 않는 것을 맞추기 위해서 사용