#SQL

## Task - 00
```sql
CREATE TABLE person_discounts(
  id bigint primary key ,
  person_id bigint not null ,
  pizzeria_id bigint not null ,
  discount float default 0,
  constraint fk_person_discounts_person_id foreign key  (person_id) references person(id),
  constraint fk_person_discounts_pizzeria_id foreign key  (pizzeria_id) references pizzeria(id)
);
```
![image](https://github.com/CheAm1337/select/assets/115126424/c0e7e151-062d-4aad-8b25-260642573a40)


## Task - 01
```sql
WITH amount_of_orders AS (
	SELECT po.person_id, m.pizzeria_id , COUNT (*) FROM person_order po
	JOIN menu m ON m.id = po.menu_id
	GROUP BY 1, 2 
	ORDER BY 1, 2
)
INSERT INTO person_discounts
	SELECT
	ROW_NUMBER() OVER(ORDER BY 1) AS id,
	person_id,
	pizzeria_id,
	CASE
		WHEN count = 1 THEN 10.5
		WHEN count = 2 THEN 22
		ELSE 30
	END
	FROM amount_of_orders
```


## Task - 02
```sql
WITH pizza_order AS (
        SELECT
            person_id,
            person.name,
            menu.pizza_name,
            price,
            pizzeria_id,
            pizzeria.name AS pizzeria_name
        FROM person_order
        INNER JOIN menu ON menu.id = person_order.menu_id
        INNER JOIN person ON person.id = person_order.person_id
        INNER JOIN pizzeria ON pizzeria.id = menu.pizzeria_id
    )
SELECT
    pizza_order.name,
    pizza_order.pizza_name,
    pizza_order.price,
    (price - price * (person_discounts.discount / 100)) AS discount_price,
    pizza_order.pizzeria_name
    FROM person_discounts
    INNER JOIN pizza_order ON person_discounts.person_id = pizza_order.person_id
        AND person_discounts.pizzeria_id = pizza_order.pizzeria_id
    ORDER BY 1,2;
```
![image](https://github.com/CheAm1337/select/assets/115126424/7c5b7405-45f9-468d-b652-c6d945b9cd8d)


## Task - 04
```sql

```
