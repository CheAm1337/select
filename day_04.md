#SQL

## Task - 00
```sql
CREATE VIEW v_persons_female
AS 

SELECT * FROM person p
WHERE p.gender = 'female'



CREATE VIEW v_persons_male
AS 

SELECT * FROM person p
WHERE p.gender = 'male'
```
![image](https://github.com/CheAm1337/select/assets/115126424/90492085-74dc-4c32-a8b9-f7cd6e61c7eb)
![image](https://github.com/CheAm1337/select/assets/115126424/4f859e2b-0f20-4f16-b7f9-2b5d208dbb65)


## Task - 01
```sql
CREATE VIEW v_persons
AS 

SELECT name FROM person p
ORDER BY 1;
```
![image](https://github.com/CheAm1337/select/assets/115126424/1059e421-e06a-4b88-a80a-02877e198258)

## Task - 02
```sql
CREATE VIEW v_generated_dates
AS 

SELECT gs::date
from generate_series('2022-01-01', '2022-01-31', interval '1 day') as gs;
```
![image](https://github.com/CheAm1337/select/assets/115126424/b7dd8d51-f9b2-4fa2-9f88-b0ec19054b7c)

## Task - 03
```sql
CREATE VIEW v_generated_dates
AS 

SELECT gs::date
FROM generate_series('2022-01-01', '2022-01-31', interval '1 day') AS gs
WHERE NOT EXISTS (
    SELECT visit_date
    FROM person_visits
    WHERE visit_date = gs::date
    AND EXTRACT(YEAR FROM visit_date) = 2022
    AND EXTRACT(MONTH FROM visit_date) = 1
)
ORDER BY 1;
```
![image](https://github.com/CheAm1337/select/assets/115126424/26756be8-1f33-4319-99b9-b3e7e19a90e2)


## Task - 04
```sql
CREATE VIEW v_price_with_discount AS
SELECT 
    p.name AS name,
    m.pizza_name AS pizza_name,
    m.price AS price,
    ROUND(m.price - (m.price * 0.1)) AS discount_price
FROM 
    person_order po
JOIN 
    menu m ON po.menu_id = m.id
JOIN 
    person p ON po.person_id = p.id
ORDER BY 
    p.name,
    m.pizza_name;
```
![image](https://github.com/CheAm1337/select/assets/115126424/58a8e1cb-8602-4be3-8ef7-75088ee817bb)

## Task - 05
```sql

```
