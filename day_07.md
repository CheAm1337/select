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
