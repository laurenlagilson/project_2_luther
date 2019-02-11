# Challenge Set 9
## Part I: W3Schools SQL Lab 

*Introductory level SQL*

--

This challenge uses the [W3Schools SQL playground](http://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all). Please add solutions to this markdown file and submit.

1. Which customers are from the UK?  
- Around the Horn
- B's Beverages
- Consolidated Holidays
- Eastern Connection
- Island Trading
- North/South
- Seven Seas Imports
---
2. What is the name of the customer who has the most orders?
- Ernst Handel
---
3. Which supplier has the highest average product price?
- Aux joyeux ecclésiastiques
---
4. How many different countries are all the customers from? (*Hint:* consider [DISTINCT](http://www.w3schools.com/sql/sql_distinct.asp).)
- 21
---
5. What category appears in the most orders?
- 4
---
6. What was the total cost for each order?  

OrderID | Total Price
--------- | ------------
10248 | 566
10249 | 2329.25
10250 | 2267.25
10251 | 839.50
10252 | 4662.50

```
WITH merge_table AS (SELECT Products.ProductID, Products.Price, OrderDetails.OrderID, OrderDetails.Quantity 
FROM [OrderDetails]
INNER JOIN Products ON OrderDetails.ProductID = Products.ProductID)

SELECT SUM(Price*Quantity), OrderID FROM merge_table 
group by OrderID
order by SUM(Price*Quantity) DESC
```
 
---
7. Which employee made the most sales (by total price)?
- Margaret Peacock

```
WITH merged_table as (SELECT EmployeeID, Orders.OrderID, OrderDetails.Quantity, Products.Price 
FROM Orders 
JOIN OrderDetails ON Orders.OrderID=OrderDetails.OrderID
JOIN Products ON OrderDetails.ProductID=Products.ProductID)

SELECT SUM(Quantity*Price), EmployeeID
FROM merged_table
GROUP BY EmployeeID
ORDER BY SUM(Quantity*Price) DESC
```


8. Which employees have BS degrees? (*Hint:* look at the [LIKE](http://www.w3schools.com/sql/sql_like.asp) operator.)
- 2 

9. Which supplier of three or more products has the highest average product price? (*Hint:* look at the [HAVING](http://www.w3schools.com/sql/sql_having.asp) operator.)
-  Toyko Traders

```
SELECT COUNT(SupplierID), SupplierID, AVG(Price)
FROM Products
GROUP BY SupplierID
HAVING COUNT(SupplierID) >= 3
ORDER BY AVG(Price) DESC;
```
