# sql_super_lessons
# SQL

# 00
```sql
SELECT name, rating FROM pizzeria p
LEFT JOIN person_visits pv
	ON p.id = pv.pizzeria_id
WHERE pv.id IS NULL;
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/cac01c75-1785-4cd3-bf06-50ea25e20655)

# 01
```sql
SELECT DISTINCT visit_date FROM person_visits pv
LEFT JOIN (SELECT missing_date::date 
		   FROM generate_series(
			   '2022-01-1', 
			   '2022-01-10', 
			   interval '1 day'
		   ) AS missing_date
		   JOIN person_visits pv
		   ON pv.visit_date = missing_date 
		   WHERE pv.person_id = 1 OR pv.person_id = 2) AS md
ON visit_date = md.missing_date
WHERE missing_date IS null;

```
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/e55fd451-79ed-4830-8521-3b8f527ff7fd)


# 02
```sql
SELECT 
	COALESCE (p.name, '-'),
	tab.visit_date,
	COALESCE (pz.name, '-') 
FROM (
	SELECT visit_date, pizzeria_id, person_id FROM person_visits pv 
	WHERE visit_date BETWEEN '2022-01-01' and '2022-01-03'
) AS tab
FULL JOIN pizzeria pz ON pizzeria_id = pz.id
FULL JOIN person p ON person_id = p.id
ORDER BY 1, 2, 3;
```
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/5fffafef-e160-4ff1-a7ac-08e71e1d489e)


# 03
```sql
WITH res_set AS(
	SELECT DISTINCT visit_date FROM person_visits pv
	LEFT JOIN (SELECT missing_date::date 
		   FROM generate_series(
			   '2022-01-1', 
			   '2022-01-10', 
			   interval '1 day'
		   ) AS missing_date
		   JOIN person_visits pv
		   ON pv.visit_date = missing_date 
		   WHERE pv.person_id = 1 OR pv.person_id = 2) AS md
ON visit_date = md.missing_date
WHERE missing_date IS null
)
SELECT * FROM res_set;
```
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/80de5b0e-9ff5-405d-a529-d6f8bb41f0e4)

# 04
```sql
SELECT pizza_name, pz.name, price  FROM menu m
JOIN pizzeria pz ON m.pizzeria_id = pz.id
WHERE pizza_name = 'mushroom pizza' OR pizza_name = 'pepperoni pizza'
ORDER BY 1, 2;
```
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/feb5477d-1f4d-4b1f-ad77-34d1dab67ddc)


# 05
```sql
SELECT name FROM person
WHERE age > 25 AND gender = 'female'
ORDER BY 1;
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/e82da91b-20ba-49ba-a0a3-f9c8ea1ce87c)

# 06
```sql
WITH tab as(
	SELECT pizza_name, pz.name as pizzeria_name, p.name FROM menu m
	JOIN pizzeria pz ON m.pizzeria_id = pz.id
	JOIN person_order po ON po.menu_id = m.id
	JOIN person p ON po.person_id = p.id
)

SELECT pizza_name, pizzeria_name FROM tab
WHERE tab.name = 'Anna' OR tab.name = 'Denis'
ORDER BY 1;
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/a0c8950b-8f1c-429c-aa10-6d3f9b5f7f20)

# 07
```sql
SELECT 
	pz.name AS pizzeria_name,
	p.name AS person_name,
	m.price,
	pv.visit_date
FROM
	person_visits pv
JOIN person p ON pv.person_id = p.id 
JOIN person_order po ON po.order_date = pv.visit_date
JOIN menu m ON po.menu_id = m.id
JOIN pizzeria pz ON pz.id = pv.pizzeria_id
WHERE 
	visit_date = '2022-01-8'
	AND p.name = 'Dmitriy'
	AND m.price <= 800;
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/d5417e83-f2ea-4a01-bbf2-88df0d3aa563)

# 08
```sql
SELECT p.name FROM person p
JOIN person_order po ON p.id = po.person_id 
JOIN menu m ON m.id = po.menu_id
WHERE (
		p.address = 'Moscow' OR
		p.address = 'Samara'
	) AND (
		m.pizza_name = 'mushroom pizza' OR
		m.pizza_name = 'pepperoni pizza'
	) AND p.gender = 'male'
ORDER BY 1 DESC;
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/581fbed1-2a4f-4a14-a351-f92599b68239)

# 09
```sql
SELECT p.name FROM person p
JOIN person_order po ON p.id = po.person_id 
JOIN menu m ON m.id = po.menu_id
WHERE (
		m.pizza_name = 'cheese pizza' OR
		m.pizza_name = 'pepperoni pizza'
	) AND p.gender = 'female'
ORDER BY 1;
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/e4981b11-67af-4164-86c8-50e1c2517ed4)

# 10
```sql
SELECT p1.name, p2.name, p1.address FROM person p1
JOIN person p2 ON p1.address = p2.address
WHERE p2.name > p1.name
ORDER BY 1, 2, 3;
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/d8bd9764-90e4-4cbe-b11e-1648ccf33817)






