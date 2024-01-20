# sql_super_lessons
# SQL

# 1
```
SELECT name, age FROM person
WHERE address = 'Moscow';
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/0b3c396d-25d1-4368-a6dc-0c07c9a09fc6)

# 2
```
SELECT name, age FROM person
WHERE address = 'Moscow' and gender = 'female';
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/d8dbfd9b-88e4-4b0c-9005-c38be18509be)


# 3.1
```
SELECT name, rating FROM pizzeria
WHERE rating  >= 3.5 and rating <= 5
ORDER BY rating;
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/17f5f068-8ee4-4498-82df-421e1fbfad44)

# 3.2
```
SELECT name, rating FROM pizzeria 
WHERE rating BETWEEN 3.5 and 5
ORDER BY rating;
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/e46462da-90a0-4100-ac45-305887fc3f63)

# 4
```
SELECT DISTINCT person_id FROM person_visits
WHERE visit_date BETWEEN '2022-01-01' AND '2022-01-09' or pizzeria_id = 2
ORDER BY person_id DESC;
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/897a18dc-402f-4f01-8a7c-e89120b710d2)


# 5
```
SELECT name, id FROM person
WHERE id
	IN (SELECT person_id FROM person_order 
		WHERE order_date = '2022-01-01'
	   	OR order_date = '2022-01-03'
	    OR order_date = '2022-01-06');
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/f8bd012a-0baf-45ef-825d-d51cba71019a)

# 6
```
SELECT EXISTS (
	SELECT name FROM person WHERE name='Kate'
);
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/3b2b5344-d97d-4429-8fb3-151c5bbc10d1)
