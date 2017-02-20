# Challenge Set 9
## Part I: W3Schools SQL Lab 

*Introductory level SQL*

--

This challenge uses the [W3Schools SQL playground](http://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all). Please add solutions to this markdown file and submit.

1. Which customers are from the UK?

Around the Horn, B's Beverages, Consolidated Holdings, Eastern Connection, Island Trading, North/South, Seven Seas Imports

```sql
SELECT
    *
FROM 
    Customers 
WHERE 
    Country = "UK";
```

2. What is the name of the customer who has the most orders?

Ernst Handel
```sql
SELECT 
	  CustomerName, 
	  Count(*) AS Number 
FROM 
    Customers AS c 
  JOIN 
    Orders AS o 
  ON 
    c.CustomerID = o.CustomerID 
GROUP BY 
	  o.CustomerID
ORDER BY
	  Number DESC
LIMIT 5;
```

3. Which supplier has the highest average product price?

Aux joyeux ecclésiastiques, $140.75
``` sql
SELECT 
    SupplierName,
    AVG(p.Price) AS AvgPrice
FROM 
    Suppliers AS s
  JOIN
    Products AS p
  ON
    s.SupplierID=p.SupplierID
GROUP BY
    SupplierName
ORDER BY
    AvgPrice DESC
LIMIT 5;
```
4. How many different countries are all the customers from? (*Hint:* consider [DISTINCT](http://www.w3schools.com/sql/sql_distinct.asp).)

21
```sql
SELECT
    COUNT(DISTINCT(Country)) AS
FROM
    Customers
```

5. What category appears in the most orders?

Dairy Products
```sql
SELECT
    CategoryName,
    Count(*) as CategoryCount
FROM
    Categories as C
  JOIN
    Products as P
  JOIN
    OrderDetails as O
  ON
    C.CategoryID=P.CategoryID 
  AND
    P.ProductID=O.ProductID
GROUP BY
    CategoryName
ORDER BY
    CategoryCount DESC
LIMIT 5;
```

6. What was the total cost for each order?
```sql
SELECT
    OrderID,
    SUM(O.Quantity * P.Price) AS TotalCost
FROM
    OrderDetails AS O
  JOIN
    Products AS P
  ON
    O.ProductID=P.ProductID
GROUP BY
    OrderID;
```

7. Which employee made the most sales (by total price)?

Margaret Peacock, $105,696.50
```sql
SELECT
    LastName,
    FirstName,
    SUM(OD.Quantity * P.Price) AS TotalSales
FROM
    Employees AS E
  JOIN
    Orders AS O
  JOIN
    OrderDetails AS OD
  JOIN
    Products AS P
  ON
    E.EmployeeID = O.EmployeeID 
  AND
    O.OrderID = OD.OrderID 
  AND
    OD.ProductID = P.ProductID
GROUP BY
    LastName,
    FirstName
ORDER BY
    TotalSales DESC;
```

8. Which employees have BS degrees? (*Hint:* look at the [LIKE](http://www.w3schools.com/sql/sql_like.asp) operator.)

Janet Leverling, Steven Buchanan
```sql
SELECT
    LastName,
    FirstName,
    Notes 
FROM
    Employees
WHERE
    Notes LIKE '%BS%';
```
9. Which supplier of three or more products has the highest average product price? (*Hint:* look at the [HAVING](http://www.w3schools.com/sql/sql_having.asp) operator.)

Tokyo Traders
```sql
SELECT
    SupplierName,
    AVG(Price) AS AvgPrice
From
    Suppliers AS S
  JOIN
    Products AS P
  ON
    S.SupplierID=P.SupplierID
GROUP BY
    SupplierName
HAVING
    COUNT(*) > 2
ORDER BY
    AvgPrice DESC;
```
