# sql_super_lessons
# SQL


# 00
```
SELECT menu.id as object_id, pizza_name as object_name FROM menu
UNION
SELECT person.id, name FROM person
ORDER BY object_id, object_name;
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/4790632d-bfc4-4b07-9fa4-026fb3fa007b)


# 01
```
(SELECT name as object_name FROM person ORDER by object_name)
UNION all
(SELECT pizza_name FROM menu
ORDER by pizza_name);

```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/009fd610-6295-4b22-bfa0-60c7c2350a46)


# 02
```
SELECT pizza_name FROM menu
INTERSECT
SELECT pizza_name FROM menu
ORDER BY pizza_name DESC;
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/29b371ed-f662-41f3-a8a7-55c054fb4808)


# 03
```
SELECT order_date as action_date, person_id FROM person_order
INTERSECT ALL
SELECT visit_date, person_id FROM person_visits
ORDER BY action_date, person_id DESC;
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/72289868-fb90-40b5-822e-535ac60247e4)

# 04

```

SELECT person_id, order_date  FROM person_order
WHERE order_date = '2022-01-07'
INTERSECT 
SELECT person_id, visit_date FROM person_visits
WHERE visit_date = '2022-01-07';
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/4c57a881-7bbc-4dba-9ad8-132e6f6f14a7)


# 05

```
SELECT person.id, person.name, age, gender, address, pizzeria.id, pizzeria.name, rating FROM person, pizzeria
ORDER by person.id;
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/0afcf02a-782e-469a-8be7-b779786b62be)

# 06

```
SELECT action_date, person.name as person_name FROM
	(SELECT order_date as action_date, person_id FROM person_order
	INTERSECT
	SELECT visit_date, person_id FROM person_visits) as tab
JOIN person ON tab.person_id = person.id
ORDER BY action_date, person.name DESC;
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/e1638149-0d27-4450-8778-1a8ba2c947cf)

# 07

```
SELECT 
	order_date, 
	p.name || ' (Age: ' || p.age || ')' as person_information 
FROM person_order, person p
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/39bf47f0-45a9-4e36-98a6-8f49c4bc0252)


# 08

```
SELECT order_date, p.name || '(Age: ' || p.age || ')' as person_information FROM 
	(SELECT order_date, person_id FROM person_order) as p_o
NATURAL JOIN person p;
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/02322cd2-8590-43b9-890e-901cefdb1252)

# 09

```
SELECT name FROM pizzeria
WHERE id NOT IN (SELECT pizzeria_id FROM person_visits);

SELECT name FROM pizzeria
WHERE NOT EXISTS 
	(SELECT pizzeria_id 
	 FROM person_visits pv 
	 WHERE pizzeria_id = pizzeria.id);
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/c846481b-b635-4f93-94c0-2cfe5d29528e)


# 10

```
SELECT 
	p.name as person_name,
	m.pizza_name as pizza_name,
	pi.name as pizzeria_name
FROM person_order po
JOIN menu m ON m.id = po.menu_id
JOIN person p ON p.id = po.person_id
JOIN pizzeria pi ON m.pizzeria_id = pi.id 
ORDER by 1, 2, 3
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/4a38746c-df9f-452c-81cd-f85012c177cb)
