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


## Task - 3
```sql
UPDATE Products
SET price = price * 0.9
WHERE category = 'Clothing';
```

![image](https://github.com/CheAm1337/select/assets/115126424/3860c100-5d89-441b-8163-ebd01d6d5f01)

## Task - 4
```sql

```
