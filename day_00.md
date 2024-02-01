#SQL

## Task - 1
```sql
SELECT name, age, address FROM person
WHERE address = 'Kazan';
```
![image](https://github.com/CheAm1337/select/assets/115126424/dab15b1a-1cdd-4490-8bae-4b0614cb8fc8)

## Task - 2
```sql
SELECT 
	name, 
	age, 
	address
FROM person
WHERE gender = 'female' and address = 'Kazan'
ORDER BY name;
```
![image](https://github.com/CheAm1337/select/assets/115126424/b2726008-c052-4080-b176-a4992f4a47db)

## Task - 3

```sql
SELECT name, rating FROM pizzeria
WHERE rating >= 3.5 and rating <= 5
ORDER BY rating;
```

```sql
SELECT name, rating FROM pizzeria
WHERE rating BETWEEN 3.5 and 5
ORDER BY rating;
```
![image](https://github.com/CheAm1337/select/assets/115126424/85106f9d-bd9a-4f0c-bece-ad613d621a15)

## Task - 4

```sql
SELECT 
	DISTINCT person_id
	
FROM person_visits
WHERE visit_date >= '2022-01-05' or pizzeria_id = 2
ORDER BY person_id DESC;
```
![image](https://github.com/CheAm1337/select/assets/115126424/90edbe1d-9347-4ee7-b89d-3f0e3981e41c)

## Task - 5

```sql
SELECT 
	name
FROM person
WHERE id IN(SELECT person_id FROM person_order WHERE order_date ='2022-01-01' or order_date = '2022-01-07' or order_date = '2022-01-07');
```
![image](https://github.com/CheAm1337/select/assets/115126424/c5ce4845-4b56-48f8-ac73-64e619594a1a)

## Task - 6

```sql
SELECT true FROM person
WHERE name = 'Anna';
```
![image](https://github.com/CheAm1337/select/assets/115126424/2d6e936e-c03d-45b5-b4b1-fb28cbfd8f5a)

## Task - 1

```sql
SELECT
	pizzeria_id,
	pizza_name
FROM menu
UNION
SELECT id, name FROM person ORDER BY pizzeria_id, pizza_name;
```
![image](https://github.com/CheAm1337/select/assets/115126424/f8a9eae8-3396-4a37-af06-6050a94865bd)


## Task - 2

```sql
SELECT
	name,'person' AS source
FROM person
UNION ALL
SELECT pizza_name, 'menu' AS source FROM menu ORDER BY source,name;
```
![image](https://github.com/CheAm1337/select/assets/115126424/43025240-4bbd-4100-82aa-40d854b9f78c)



## Task - 3

```sql
SELECT
	po.order_date,
	po.person_id,
	v.visit_date
FROM person_order po
JOIN person_visits v ON po.person_id = v.person_id
AND po.order_date = v.visit_date
ORDER BY visit_date ASC, person_id DESC;
```
![image](https://github.com/CheAm1337/select/assets/115126424/5bf336d2-1733-4159-ad63-06a685c51fa2)

