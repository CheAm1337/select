#SQL

## Task - 00
```sql
SELECT person_id, COUNT (*) AS count_of_visits
FROM person_visits
GROUP BY person_id
ORDER BY count_of_visits DESC, person_id ASC
```
![image](https://github.com/CheAm1337/select/assets/115126424/92e56b3d-2fca-4dc5-b931-27282aa7f334)

## Task - 01
```sql
SELECT p.name AS person_name, COUNT (*) AS total_visits
FROM person p
JOIN person_visits pv ON p.id = pv.person_id
GROUP BY p.name
ORDER BY total_visits DESC LIMIT 4;
```
![image](https://github.com/CheAm1337/select/assets/115126424/7d1156bc-2028-4712-bb81-80c7de3fc0cf)

## Task - 02
```sql
WITH restaurant_counts AS (
    SELECT pizzeria_id, COUNT(*) AS count, 'visit' AS action_type
    FROM person_visits
    GROUP BY pizzeria_id
    UNION ALL
    SELECT pizzeria_id, COUNT(*) AS count, 'order' AS action_type
    FROM person_visits
    GROUP BY pizzeria_id
)
SELECT p.name AS name, rc.action_type, rc.count
FROM restaurant_counts rc
JOIN pizzeria p ON rc.pizzeria_id = p.id
ORDER BY rc.action_type, rc.count DESC;
```
![image](https://github.com/CheAm1337/select/assets/115126424/3da76de6-941a-4216-a1f4-fe4c14db17d7)

## Task - 03
```sql
SELECT COALESCE(visits.name, orders.name) AS name,
       COALESCE(visits.total_visits, 0) + COALESCE(orders.total_orders, 0) AS total_count
FROM (
    SELECT pizzeria.name, COUNT(person_visits.id) AS total_visits
    FROM pizzeria
    LEFT JOIN person_visits ON pizzeria.id = person_visits.pizzeria_id
    GROUP BY pizzeria.name
) AS visits
FULL JOIN (
    SELECT pizzeria.name, COUNT(person_order.id) AS total_orders
    FROM pizzeria
    LEFT JOIN menu ON pizzeria.id = menu.pizzeria_id
    LEFT JOIN person_order ON menu.id = person_order.menu_id
    GROUP BY pizzeria.name
) AS orders ON visits.name = orders.name
ORDER BY total_count DESC, name ASC;
```
![image](https://github.com/CheAm1337/select/assets/115126424/29b4d4a4-cb26-4606-8a67-0b9543df38c0)

## Task - 04
```sql
SELECT person.name, COUNT(person_visits.id) AS count_of_visits
FROM person
JOIN person_visits ON person.id = person_visits.person_id
GROUP BY person.name
HAVING COUNT(person_visits.id) > 3;
```
![image](https://github.com/CheAm1337/select/assets/115126424/741f6757-7f81-4e73-a695-7d49f962136b)

## Task - 05
```sql
SELECT DISTINCT person.name
FROM person
JOIN person_order ON person.id = person_order.person_id
ORDER BY person.name;
```
![image](https://github.com/CheAm1337/select/assets/115126424/07f3e854-4729-4960-82c6-0c4b606780c5)

## Task - 06
```sql
SELECT pizzeria.name,
       COUNT(person_order.id) AS count_of_orders,
       ROUND(AVG(menu.price), 2) AS average_price,
       MAX(menu.price) AS max_price,
       MIN(menu.price) AS min_price
FROM pizzeria
LEFT JOIN menu ON pizzeria.id = menu.pizzeria_id
LEFT JOIN person_order ON menu.id = person_order.menu_id
GROUP BY pizzeria.name
ORDER BY pizzeria.name;
```
![image](https://github.com/CheAm1337/select/assets/115126424/1c400d1a-a6eb-4922-b7a9-65bbba1e8e0f)

## Task - 07
```sql
SELECT ROUND(AVG(rating), 4) AS global_rating
FROM pizzeria;
```
![image](https://github.com/CheAm1337/select/assets/115126424/ea341a27-65fd-4027-80aa-e79ddc64ef9c)

## Task - 08
```sql
SELECT p.address,
       pz.name,
       COUNT(po.id) AS count_of_orders
FROM person p
JOIN person_order po ON p.id = po.person_id
JOIN menu m ON po.menu_id = m.id
JOIN pizzeria pz ON m.pizzeria_id = pz.id
WHERE p.address = p.address
GROUP BY p.address, pz.name
ORDER BY p.address, pz.name;
```
![image](https://github.com/CheAm1337/select/assets/115126424/749fcf7f-c477-400f-b845-d49eb11864ee)

## Task - 09
```sql
SELECT address,
       ROUND(MAX(age) - (MIN(age) / MAX(age)), 2) AS formula,
       ROUND(AVG(age), 2) AS average,
       CASE WHEN ROUND(MAX(age) - (MIN(age) / MAX(age)), 2) > ROUND(AVG(age), 2) THEN 'true' ELSE 'false' END AS comparison
FROM person
GROUP BY address
ORDER BY address;
```
![image](https://github.com/CheAm1337/select/assets/115126424/85a7a23e-cb24-4324-b64b-1cddc7e5652b)
