# 두 개 이상 테이블 결합하기

<br/>

## GROUP BY & HAVING

### 1.1. GROUP BY

```mysql
SELECT SupplierID
		, CategoryID
        , AVG(Price)
FROM Products
GROUP BY SupplierID, CategoryID
ORDER BY AVG(Price) DESC
```

- `ORDER BY`를 쓰기 위해서는 `GROUP BY` 다음에 사용한다.



### 1.2. HAVING

```mysql
SELECT SupplierID
		, CategoryID
        , AVG(Price) AS avg_price
FROM Products
GROUP BY SupplierID, CategoryID
HAVING AVG(price) >= 100
ORDER BY AVG(Price) DESC
```

- `GROUP BY` 에 대한 조건은 `WHERE`이 아니라 `HAVING` 을 사용한다.





문제풀이





### Revising Aggregations - Averages

```mysql
SELECT AVG(population) -- population 평균
FROM city -- 테이블명
WHERE district='California' -- 조건문 = district가 California 중에서
```



### Revising Aggregations - The Sum Function

```mysql
SELECT SUM(population) -- population 합계
FROM city -- 테이블명
WHERE DISTRICT='California' -- 조건문 = district가 California 중에서
```



### Revising Aggregations - The Count Function

```mysql
SELECT COUNT(DISTRICT) -- DISTRICT의 개수
FROM city -- 테이블명
WHERE population > 100000 -- 조건절 인구가 10000이상인 지역중에
```



### Average Population

```mysql
SELECT FlOOR(AVG(population))
FROM city
```



### Population Density Difference

![](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

```mysql
SELECT MAX(population)-MIN(population)
FROM city
```

- SELECT 구문에서 자연스럽게 사칙연산이 가능하다.



### Weather Observation Station 4

```mysql
SELECT COUNT(city) - COUNT(DISTINCT city)
FROM station

```





### Top Earners



/* 
직원의 총 수입을 월간 근무로 정의하고 최대 총 수입을 Employee 테이블에 있는 직원의 최대 총 수입으로 정의합니다. 모든 직원의 최대 총 수입과 최대 총 수입을 가진 직원의 수를 찾는 쿼리를 작성하십시오. 그런 다음 이 값을 공백으로 구분된 정수로 인쇄합니다.
*/



```mysql
/* 
1. salary x months = earning
2. 각 earning 별로 몇 명이 그만큼 벌었는 계산
ex) 5000, 2 / 3000, 5 / 10000, 1 이런식으로 각 벌이  별로 몇명이 벌었는지 계산
- GROUP BY 를 사용
3. earning 중에 가장 큰 값을 가져온다.
*/
SELECT salary * months AS earnings
        , COUNT(*)
FROM employee
GROUP BY earnings 
ORDER BY earningS DESC
LIMIT 1
```

