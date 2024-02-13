![image](https://github.com/CheAm1337/select/assets/115126424/f7cd4e54-5611-4688-9366-4c5ead873a7c)#SQL

## Task - 00
```sql
select
	m.pizza_name,
	m.price,
	pz.name,
	pv.visit_date
from person p
JOIN person_visits pv ON pv.person_id = p.id
JOIN pizzeria pz ON pz.id = pv.pizzeria_id
JOIN menu m ON m.pizzeria_id = pz.id
WHERE 
	p.name = 'Kate' and
	m.price BETWEEN 800 AND 1000
```
![image](https://github.com/CheAm1337/select/assets/115126424/dee3f598-3ecb-493f-9605-372060c1f522)

## Task - 01
```sql
SELECT id
FROM menu
WHERE menu.id not in 
(SELECT menu_id FROM person_order);
```
![image](https://github.com/CheAm1337/select/assets/115126424/77769b38-ff44-433e-822d-9b7a61a03f4e)

## Task - 02
```sql
WITH ordered as(
SELECT id
FROM menu
WHERE menu.id not in 
(SELECT menu_id FROM person_order))

select 
	pz.name,
	m.price,
	m.pizza_name
from ordered
join menu m on ordered.id = m.id
join pizzeria pz on pz.id = m.pizzeria_id
order by 2,3
```

![image](https://github.com/CheAm1337/select/assets/115126424/03793e67-86fc-4f69-a523-8523559f4485)

## Task - 03
```sql
WITH _table AS 
	(
    SELECT 
        pz.name 
    FROM person_visits pv
	JOIN pizzeria pz ON pz.id = pv.pizzeria_id
    JOIN person p ON pv.person_id = p.id
    WHERE 
        p.gender = 'male'
    GROUP BY
        pz.name

    UNION ALL

    SELECT
        pz.name
    FROM person_visits pv
	JOIN pizzeria pz ON pz.id = pv.pizzeria_id
    JOIN person p ON pv.person_id = p.id
    WHERE
        p.gender = 'female'
    GROUP BY 
        pz.name
	)

SELECT DISTINCT name FROM _table
ORDER BY name
```
![image](https://github.com/CheAm1337/select/assets/115126424/f95aa662-3c82-4f89-beeb-e8264f1eb95d)

## Task - 04
```sql
WITH _male AS (
    SELECT pz.name
    FROM person_order po
    JOIN menu m ON m.id = po.menu_id
    JOIN pizzeria pz ON pz.id = m.pizzeria_id
	JOIN person p ON p.id = po.person_id
    WHERE p.gender = 'male'),
		
    _female AS (
    SELECT pz.name
    FROM person_order po
    JOIN menu m ON m.id = po.menu_id
    JOIN pizzeria pz ON pz.id = m.pizzeria_id
	JOIN person p ON p.id = po.person_id
    WHERE p.gender = 'female')

(   SELECT * FROM _male
    EXCEPT
    SELECT * FROM _female)
	
UNION

(   SELECT * FROM _female
    EXCEPT
    SELECT * FROM _male);
```
![image](https://github.com/CheAm1337/select/assets/115126424/1c19cf01-4ca0-4363-84ff-cba1634c173c)


## Task - 05
```sql
SELECT 
    pi.name AS pizzeria_name 
FROM 
    (SELECT pv.pizzeria_id FROM person_visits pv
    JOIN person p ON p.id = pv.person_id
    WHERE p.name = 'Andrey') AS andrey_visits
LEFT JOIN 
    (SELECT m.pizzeria_id FROM person_order po
    JOIN person p ON p.id = po.person_id
    JOIN menu m ON m.id = po.menu_id
    WHERE p.name = 'Andrey') AS andrey_order 
ON 
    andrey_visits.pizzeria_id = andrey_order.pizzeria_id
JOIN 
    pizzeria pi ON pi.id = andrey_visits.pizzeria_id
WHERE 
    andrey_order.pizzeria_id IS NULL;
```
![image](https://github.com/CheAm1337/select/assets/115126424/78fdd205-6ed0-46dc-96d9-32a4a04a4669)
