# 조건문

<br/>

## CASE

### 1.1. CASE 함수

[바로가기](https://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all)

```mysql
SELECT CASE
			WHEN categoryid = 1 THEN '음료'
            WHEN categoryid = 2 THEN '조미료'
            ELSE '기타'
       END
FROM Products
```





```mysql
SELECT CASE
			WHEN categoryid = 1 THEN '음료'
            WHEN categoryid = 2 THEN '조미료' 
            ELSE '기타'
       END AS 'CategoryName', * -- *를 붙이면 전체 테이블 조회
FROM Products
```





```mysql
SELECT CASE
			WHEN categoryid = 1 AND SupplierID=1 THEN '음료'
            WHEN categoryid = 2 THEN '조미료' 
            ELSE '기타'
       END AS 'CategoryName', *
FROM Products
```





```mysql
SELECT CASE
			WHEN CategoryID = 1 THEN '음료'
            WHEN CategoryID = 2 THEN '소스'
            ELSE '이외'
       END AS NEW_Category
		, AVG(price)
FROM Products
GROUP BY NEW_Category
```





## 피벗팀

```mysql
SELECT AVG(CASE WHEN CategoryID=1 THEN price ELSE NULL END) AS Category1_Price
	 , AVG(CASE WHEN CategoryID=2 THEN price ELSE NULL END) AS Category2_Price
     , AVG(CASE WHEN CategoryID=3 THEN price ELSE NULL END) AS Category3_Price
FROM Products
```









## 문제풀이



### Type of Triangle



```mysql
SELECT CASE
            WHEN A=B AND B=C THEN 'Equilateral'
            WHEN A + B <= C OR A+C <=B OR B+C <=A THEN 'Not A Triangle'
            WHEN A=B AND B!=C OR B=C AND A!=B OR A=C AND A!=B THEN 'Isosceles'
            ELSE 'Scalene'
        END
FROM TRIANGLES
```







```mysql
/*
-- INNER JOIN
SELECT * 
FROM Orders
	INNER JOIN Customers ON orders.customerID=Customers.customerID
    INNER JOIN Shippers ON Orders.shipperID=Shippers.shipperID
*/

/*
-- LEFTJOIN
SELECT * 
FROM Customers
		LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID
WHERE OrderID is NULL
*/
```





# African Cities

```mysql
SELECT city.name
FROM City
        INNER JOIN country ON City.countrycode=country.code
WHERE country.continent = 'Africa'
```





# Population Census

```mysql
SELECT SUM(city.population) AS 'PEOPLE'
FROM City
        INNER JOIN country ON City.countrycode=country.code
WHERE country.continent = 'Asia'
```

