#SQL

## Task 1

```sql
SELECT
  u.name,
  r.date,
  r.totalsum,
  GROUP_CONCAT(s.title) AS servicesall
FROM users u
JOIN records r
  ON u.id = r.user_id
JOIN services_records sr
  ON r.id = sr.records
JOIN services s
  ON sr.service_id = s.id
GROUP BY
  u.name,
  r.date,
  r.totalsum;
```

## Task 2

```sql
INSERT INTO records (user_id, date, totalsum)
VALUES (
    @user_id,
    @date,
    @totalsum
);

SET @records_id = LAST_INSERT_ID();

INSERT INTO services_records (service_id, records_id)
VALUES
    @services_list;
```

## Task 3

```sql
SELECT u.name, SUM(r.total_sum) AS sum, GROUP_CONCAT(s.services) AS servicesFROM users u
JOIN records r ON u.id = r.user_id JOIN service_records sr ON r.id = sr.record_id 
JOIN services s ON sr.service_id = s.idWHERE u.id = 1
GROUP BY u.name;
```
