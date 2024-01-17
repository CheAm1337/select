#SQL

## Task - 1
```sql
SELECT object_name FROM (
	SELECT name AS object_name, 'person' as type FROM person
	UNION ALL
	SELECT pizza_name, 'pizza' FROM menu
	ORDER BY type, object_name
	) as tab;
```
![image](https://github.com/CheAm1337/select/assets/115126424/4203ea85-6460-46f7-b83b-dbc2bd6988d8)

## Task - 2
```sql
SELECT 
	pizza_name 
FROM menu 
INTERSECT 
SELECT 
	pizza_name 
FROM menu ORDER BY pizza_name DESC;
```
![image](https://github.com/CheAm1337/select/assets/115126424/0d22a6ad-5711-4184-9833-d26b33780134)

## Task - 3
```sql
SELECT visit_date, person_id FROM person_visits
INTERSECT
SELECT order_date, person_id FROM person_order
ORDER BY visit_date, person_id DESC
```
![image](https://github.com/CheAm1337/select/assets/115126424/152e6e3c-9e72-4c60-b4b2-5afb62b17d18)

## Task - 4
```sql

-----

```

## Task - 5
```sql
SELECT * FROM person
CROSS JOIN pizzeria
ORDER BY person,pizzeria;
```
![image](https://github.com/CheAm1337/select/assets/115126424/e41db5f5-15e3-4b7a-a2d1-8ddb7c2822a5)

## Task - 6
```sql
SELECT visit_date, person.name FROM person
	JOIN(
	SELECT visit_date, person_id FROM person_visits
	INTERSECT
	SELECT order_date, person_id FROM person_order
	ORDER BY visit_date DESC, person_id ASC) as tab ON person_id = person.id
```
![image](https://github.com/CheAm1337/select/assets/115126424/9e246419-4934-4581-9a90-63209c66bdd7)

## Task - 7
```sql
SELECT DISTINCT order_date, name ||'(age:'||age||')' AS person_information 
FROM person_order
NATURAL JOIN person
ORDER BY order_date, person_information ASC;
```
![image](https://github.com/CheAm1337/select/assets/115126424/7cd5333f-533c-46d6-a684-d2d91dea45f3)

