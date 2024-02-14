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
CREATE OR REPLACE VIEW avg_order_cost_deviation AS
SELECT 
    customer_id,
    AVG(total_cost) AS avg_order_cost,
    AVG(total_cost) - (SELECT AVG(total_cost) FROM (SELECT SUM(price * quantity) AS total_cost 
													FROM Orders JOIN Products USING (product_id) 
													GROUP BY order_id) AS overall_avg) AS deviation
FROM (
    SELECT 
        order_id, 
        customer_id,
        SUM(price * quantity) AS total_cost
    FROM Orders
    JOIN Products USING (product_id)
    GROUP BY order_id, customer_id
) AS order_costs
GROUP BY customer_id;
```
![image](https://github.com/CheAm1337/select/assets/115126424/6ff391f3-4fbd-484d-9ca7-7a8920c9ea0f)

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

SELECT category as low
FROM Products
GROUP BY category
ORDER BY AVG(price) ASC
LIMIT 1;
```
![image](https://github.com/CheAm1337/select/assets/115126424/57d3e9c9-96f1-4c4c-b7f4-3b290716f03b)
![image](https://github.com/CheAm1337/select/assets/115126424/285316cf-bceb-47d4-a87e-318651136265)

## Task - 5
```sql
DELETE FROM Orders
WHERE order_id IN (
        SELECT AVG(quantity) AS avg_quantity
        FROM Orders
);

```
![image](https://github.com/CheAm1337/select/assets/115126424/8709459e-40df-4f0d-af5e-a7c9cedb5f0b)
