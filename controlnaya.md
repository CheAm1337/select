#SQL

## Task - 1
```sql
select 
	c.first_name,
	c.last_name,
	SUM(o.quantity * p.price)
from orders o
JOIN customers c ON c.customer_id = o.customer_id 
JOIN Products p ON o.product_id = p.product_id
WHERE order_date >= current_date - interval '1 month'
GROUP BY c.first_name, c.last_name
order by sum desc
LIMIT 3;
```
![image](https://github.com/CheAm1337/select/assets/115126424/c58065b3-fa9c-4d35-8bce-b9dde32967e0)

## Task - 2
```sql

```

## Task - 3
```sql
UPDATE Products
SET price = price * 0.9
WHERE category = 'Clothing';
```
![image](https://github.com/CheAm1337/select/assets/115126424/3860c100-5d89-441b-8163-ebd01d6d5f01)

## Task - 4
```sql
SELECT category as high
FROM Products
GROUP BY category
ORDER BY AVG(price) DESC
LIMIT 1;
![image](https://github.com/CheAm1337/select/assets/115126424/57d3e9c9-96f1-4c4c-b7f4-3b290716f03b)

SELECT category as low
FROM Products
GROUP BY category
ORDER BY AVG(price) ASC
LIMIT 1;
![image](https://github.com/CheAm1337/select/assets/115126424/c6773fca-734d-416c-9e20-8e65d0b39ae3)
```

## Task - 
```sql
DELETE FROM Orders
WHERE order_id IN (
    SELECT o.order_id
    FROM Orders o
    JOIN (
        SELECT AVG(quantity) AS avg_quantity
        FROM Orders
    ) AS avg_orders ON o.quantity > avg_orders.avg_quantity
);

```
