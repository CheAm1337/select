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
