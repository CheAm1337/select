#SQL

## Task - 00
```sql
CREATE TABLE person_discounts(
  id bigint primary key ,
  person_id bigint not null ,
  pizzeria_id bigint not null ,
  discount integer default 0,
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
