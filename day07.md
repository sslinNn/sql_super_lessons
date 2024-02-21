# 00
```sql
SELECT
  person_id,
  count(person_id) as count_of_visits
FROM person_visits
GROUP BY person_id
ORDER BY 2 DESC;
```
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/13867008-988e-4a64-806a-c73b33ca8dc1)

# 01
```sql
SELECT 
    p.name, 
    count(pv.person_id) as count_of_visits 
FROM person_visits pv
JOIN person p ON p.id = pv.person_id
GROUP BY p.name
ORDER BY 2 DESC LIMIT 4;
```
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/f609de1d-0d56-4f8c-911c-f4eef35a6113)

# 02
```sql
WITH visit as (
SELECT 
    pz.name, 
    count(pv.pizzeria_id), 
    'visit' as action_type 
FROM person_visits pv
JOIN pizzeria pz ON pz.id = pv.pizzeria_id
GROUP BY pz.name
), orders as (
SELECT 
    pz.name, 
    count(pz.id), 
    'order' as action_type 
FROM person_order po
JOIN menu m ON m.id = po.menu_id
JOIN pizzeria pz ON pz.id = m.pizzeria_id
GROUP BY pz.name
)

SELECT * FROM visit
UNION
SELECT * FROM orders
ORDER BY 3, 2 DESC;
```
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/92192b18-b9f4-4516-9c96-544d94fb413f)

# 03
```sql


```







