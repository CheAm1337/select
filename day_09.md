#SQL

## Task - 00
```sql
CREATE OR REPLACE FUNCTION fnc_trg_person_insert_audit()
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO person_audit (id, name, age, gender, address, action)
    VALUES (NEW.id, NEW.name, NEW.age, NEW.gender, NEW.address, 'INSERT');
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trg_person_insert_audit
AFTER INSERT ON person
FOR EACH ROW
EXECUTE FUNCTION fnc_trg_person_insert_audit();

INSERT INTO person(id, name, age, gender, address)
VALUES (10, 'Damir', 22, 'male', 'Irkutsk');
```
![image](https://github.com/CheAm1337/select/assets/115126424/fff2d530-d0f9-4e92-a221-88b3f5e175a2)
## Task - 01
```sql
CREATE OR REPLACE FUNCTION fnc_trg_person_update_audit()
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO person_audit (id, name, age, gender, address, action, timestamp)
    VALUES (OLD.id, OLD.name, OLD.age, OLD.gender, OLD.address, 'UPDATE', CURRENT_TIMESTAMP);
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trg_person_update_audit
AFTER UPDATE ON person
FOR EACH ROW
EXECUTE FUNCTION fnc_trg_person_update_audit();


```
![image](https://github.com/CheAm1337/select/assets/115126424/57ce9873-94bc-404c-8d5e-9c93454eacaf)

## Task - 02
```sql
CREATE OR REPLACE FUNCTION fnc_trg_person_delete_audit()
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO person_audit (id, name, age, gender, address, action, timestamp)
    VALUES (OLD.id, OLD.name, OLD.age, OLD.gender, OLD.address, 'DELETE', CURRENT_TIMESTAMP);
    RETURN OLD;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trg_person_delete_audit
AFTER DELETE ON person
FOR EACH ROW
EXECUTE FUNCTION fnc_trg_person_delete_audit();
```
![image](https://github.com/CheAm1337/select/assets/115126424/f60201c3-fe25-4f7b-a5cf-5fa8d3f4cb57)

## Task - 03
```sql
CREATE OR REPLACE FUNCTION fnc_trg_person_audit()
RETURNS TRIGGER AS $$
BEGIN
    IF TG_OP = 'INSERT' THEN
        INSERT INTO person_audit (id, name, age, gender, address, action, timestamp)
        VALUES (NEW.id, NEW.name, NEW.age, NEW.gender, NEW.address, 'INSERT', CURRENT_TIMESTAMP);
    ELSIF TG_OP = 'UPDATE' THEN
        INSERT INTO person_audit (id, name, age, gender, address, action, timestamp)
        VALUES (OLD.id, OLD.name, OLD.age, OLD.gender, OLD.address, 'UPDATE', CURRENT_TIMESTAMP);
    ELSIF TG_OP = 'DELETE' THEN
        INSERT INTO person_audit (id, name, age, gender, address, action, timestamp)
        VALUES (OLD.id, OLD.name, OLD.age, OLD.gender, OLD.address, 'DELETE', CURRENT_TIMESTAMP);
    END IF;
    
    RETURN NULL;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trg_person_audit
AFTER INSERT OR UPDATE OR DELETE ON person
FOR EACH ROW EXECUTE FUNCTION fnc_trg_person_audit();
```
![image](https://github.com/CheAm1337/select/assets/115126424/f60201c3-fe25-4f7b-a5cf-5fa8d3f4cb57)

## Task - 04
```sql
CREATE FUNCTION fnc_persons_female()
RETURNS TABLE (id INT, name VARCHAR, age INT, gender VARCHAR, address VARCHAR) AS $$
    SELECT id, name, age, gender, address
    FROM person
    WHERE gender = 'female';
$$ LANGUAGE SQL;

CREATE FUNCTION fnc_persons_male()
RETURNS TABLE (id INT, name VARCHAR, age INT, gender VARCHAR, address VARCHAR) AS $$
    SELECT id, name, age, gender, address
    FROM person
    WHERE gender = 'male';
$$ LANGUAGE SQL;

SELECT *
FROM fnc_persons_male();

SELECT *
FROM fnc_persons_female();
```
![image](https://github.com/CheAm1337/select/assets/115126424/fc50e575-a7b2-4ed0-bc69-b81951e6dba0)
![image](https://github.com/CheAm1337/select/assets/115126424/2c863fce-7375-42a2-8a1b-cea04c35e4df)

## Task - 05
```sql
CREATE FUNCTION fnc_persons(pgender VARCHAR DEFAULT 'female')
RETURNS TABLE (id INT, name VARCHAR, age INT, gender VARCHAR, address VARCHAR) AS $$
    SELECT id, name, age, gender, address
    FROM person
    WHERE gender = pgender;
$$ LANGUAGE SQL;

SELECT *
FROM fnc_persons('male');

SELECT *
FROM fnc_persons();
```
![image](https://github.com/CheAm1337/select/assets/115126424/35027415-02a7-4b79-9cd4-24675c65c4ab)
![image](https://github.com/CheAm1337/select/assets/115126424/415f6551-757c-4504-ae5d-56871298b85e)
![image](https://github.com/CheAm1337/select/assets/115126424/ed023235-3cc7-4ad5-970c-5c12c47061a1)

## Task - 06
```sql
CREATE OR REPLACE FUNCTION fnc_person_visits_and_eats_on_date(
    pperson VARCHAR DEFAULT 'Dmitriy',
    pprice INT DEFAULT 500,
    pdate DATE DEFAULT '2022-01-08'
)
RETURNS TABLE (pizzeria_name VARCHAR) AS $$
BEGIN
    RETURN QUERY
    SELECT DISTINCT pizzeria.name
    FROM person
    JOIN person_order ON person.id = person_order.person_id
    JOIN pizzeria ON person_order.pizzeria_id = pizzeria.id
    JOIN pizza ON person_order.pizza_id = pizza.id
    WHERE person.name = pperson
        AND pizza.price < pprice
        AND DATE(person_order.order_date) = pdate;
END;
$$ LANGUAGE PLPGSQL;
```
![image](https://github.com/CheAm1337/select/assets/115126424/61ca8922-94d8-4f37-be6a-f518919ea153)

