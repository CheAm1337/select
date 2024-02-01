#SQL

## Task - 02
```sql
SELECT
  COALESCE(p.name, '-') AS person_name,
  COALESCE(m.name, '-') AS pizzeria_name,
  COALESCE(to_char(v.visit_date, 'YYYY-MM-DD'), '-') AS visit_date
FROM
  (
    SELECT DISTINCT
      pv.person_id,
      pv.pizzeria_id,
      pv.visit_date
    FROM
      person_visits pv
    WHERE
      pv.visit_date BETWEEN '2022-01-01' AND '2022-01-03'
  ) v
FULL OUTER JOIN person p ON v.person_id = p.id
FULL OUTER JOIN pizzeria m ON v.pizzeria_id = m.id
ORDER BY
  person_name,
  pizzeria_name,
  visit_date;
```
![image](https://github.com/CheAm1337/select/assets/115126424/b3686abe-db79-43cc-9d1c-3a5782a57a32)


## Task - 03
```sql
WITH set_ AS (
    SELECT DISTINCT missing_date::date
    FROM generate_series(
        '2022-01-01'::date, 
        '2022-01-10'::date, 
        interval '1 day'
    ) AS missing_date
    LEFT JOIN person_visits pv
    ON pv.visit_date = missing_date
       AND (pv.person_id = 1 OR pv.person_id = 2)
    WHERE pv.visit_date IS NULL
)
SELECT * FROM set_
ORDER BY missing_date ASC;
```
![image](https://github.com/CheAm1337/select/assets/115126424/c17eb5a6-5448-42b7-950d-40f97364ffea)


## Task - 04
```sql
SELECT
    pizzeria.name AS pizzeria_name,
    menu.pizza_name,
    menu.price
FROM
    menu
JOIN
    pizzeria ON menu.pizzeria_id = pizzeria.id
WHERE
    menu.pizza_name IN ('mushroom pizza', 'pepperoni pizza')
ORDER BY
    menu.pizza_name,
    pizzeria.name;
```
![image](https://github.com/CheAm1337/select/assets/115126424/b5c8553e-a869-45bc-9b93-2111d7f3fa21)


## Task - 05
```sql

SELECT
    name
FROM
    person
WHERE
    gender = 'female' AND age > 25
ORDER BY
    name;

```
![image](https://github.com/CheAm1337/select/assets/115126424/1094d0a7-3fc6-406b-82d4-95c849d672d1)


## Task - 06
```sql

SELECT
    menu.pizza_name,
    pizzeria.name AS pizzeria_name
FROM
    person
JOIN
    person_order ON person.id = person_order.person_id
JOIN
    menu ON person_order.menu_id = menu.id
JOIN
    pizzeria ON menu.pizzeria_id = pizzeria.id
WHERE
    person.name IN ('Denis', 'Anna')
ORDER BY
    menu.pizza_name,
    pizzeria.name;

```
![image](https://github.com/CheAm1337/select/assets/115126424/94c795e4-5b0f-4d5d-b8ff-5de1ba9d4daf)

## Task - 07
```sql

SELECT 
    pzz.name AS pizza_place,
    pe.name AS guest_name,
    mn.price AS pizza_price,
    pv.visit_date AS visit_date
FROM
    person_visits pv
JOIN person pe ON pv.person_id = pe.id 
JOIN person_order po ON po.order_date = pv.visit_date
JOIN menu mn ON po.menu_id = mn.id
JOIN pizzeria pzz ON pzz.id = pv.pizzeria_id
WHERE 
    pv.visit_date = '2022-01-08'
    AND pe.name = 'Dmitriy'
    AND mn.price <= 800;


```
![image](https://github.com/CheAm1337/select/assets/115126424/d1bf5a60-a49b-4cd6-9d8b-f8d311fec7c6)

## Task - 08
```sql

SELECT
    person.name AS person_name
FROM
    person
JOIN
    person_order ON person.id = person_order.person_id
JOIN
    menu ON person_order.menu_id = menu.id
JOIN
    pizzeria ON menu.pizzeria_id = pizzeria.id
WHERE
    (person.gender = 'male')
    AND (person.address IN ('Moscow', 'Samara'))
    AND (menu.pizza_name IN ('pepperoni pizza', 'mushroom pizza'))
ORDER BY
    person.name DESC;


```

![image](https://github.com/CheAm1337/select/assets/115126424/d1646f7d-49af-4b4d-95cc-4a3c2cc9c0ce)

## Task - 09
```sql

SELECT
    person.name AS person_name
FROM
    person
JOIN
    person_order po1 ON person.id = po1.person_id
JOIN
    menu m1 ON po1.menu_id = m1.id
JOIN
    person_order po2 ON person.id = po2.person_id
JOIN
    menu m2 ON po2.menu_id = m2.id
WHERE
    person.gender = 'female'
    AND m1.pizza_name = 'pepperoni pizza'
    AND m2.pizza_name = 'cheese pizza'
ORDER BY
    person.name;


```

![image](https://github.com/CheAm1337/select/assets/115126424/d5141fa8-929b-4986-8370-f56e1f878ec7)

## Task - 10
```sql

SELECT
    p1.name AS person1_name,
    p2.name AS person2_name,
    p1.address AS common_address
FROM
    person p1
JOIN
    person p2 ON p1.address = p2.address AND p1.id < p2.id
ORDER BY
    p1.name,
    p2.name,
    p1.address;

```

![image](https://github.com/CheAm1337/select/assets/115126424/a96a308e-4c2f-4998-b40c-730a418d5436)
