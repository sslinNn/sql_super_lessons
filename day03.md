# 00
```sql
SELECT
    m.pizza_name as pizza_name,
    m.price,
    pz.name as pizzeria_name,
    pv.visit_date
FROM person p
JOIN person_visits pv ON pv.person_id = p.id
JOIN pizzeria pz ON pz.id = pv.pizzeria_id
JOIN menu m ON m.pizzeria_id = pz.id
WHERE
    p."name" = 'Kate' AND
    m.price BETWEEN 800 AND 1000
ORDER BY 1, 2, 3;
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/98c9ad42-1bf9-4683-b82d-fa52cfe16488)

# 01
```sql
SELECT menu.id 
FROM menu
WHERE menu.id NOT IN 
    (SELECT po.menu_id 
       FROM person_order po);
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/100e4442-1a66-4572-b359-ea72b993c496)

# 02
```sql
WITH not_ordered as 
    (SELECT menu.id as menu_id
       FROM menu
      WHERE menu.id NOT IN 
        (SELECT po.menu_id 
           FROM person_order po))
SELECT 
    m.pizza_name,
    m.price,
    pz.name as pizzeria_name
FROM not_ordered
JOIN menu m ON not_ordered.menu_id = m.id
JOIN pizzeria pz ON m.pizzeria_id = pz.id
ORDER BY 1, 2;
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/64c2fdb3-1ddd-4d3b-ae9a-6729466aa756)

# 03
```sql
WITH res_tab AS (
    SELECT 
        pz.name 
    FROM person_visits pv
    JOIN person p ON pv.person_id = p.id
    JOIN pizzeria pz ON pz.id = pv.pizzeria_id
    WHERE 
        p.gender = 'female'
    GROUP BY
        pz.name

    UNION ALL

    SELECT
        pz.name
    FROM person_visits pv
    JOIN person p ON pv.person_id = p.id
    JOIN pizzeria pz ON pz.id = pv.pizzeria_id
    WHERE
        p.gender = 'male'
    GROUP BY 
        pz.name)

SELECT DISTINCT * FROM res_tab
ORDER BY 1; 
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/ddefe0fc-563c-4ed4-9df5-fb7b3b080511)

# 04
```sql
WITH female AS (
    SELECT 
        pz.name
    FROM person_order po
    JOIN person p ON p.id = po.person_id
    JOIN menu m ON m.id = po.menu_id
    JOIN pizzeria pz ON pz.id = m.pizzeria_id
    WHERE 
        p.gender = 'female'),
male AS (
    SELECT
        pz.name
    FROM person_order po
    JOIN person p ON p.id = po.person_id
    JOIN menu m ON m.id = po.menu_id
    JOIN pizzeria pz ON pz.id = m.pizzeria_id
    WHERE 
        p.gender = 'male')

(        
    SELECT * FROM female
    EXCEPT
    SELECT * FROM male
)
UNION
(      
    SELECT * FROM male
    EXCEPT
    SELECT * FROM female
);
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/f2f92160-5fda-4d5e-bd42-59e2224991f1)

# 05
```sql
WITH andrey_visits AS (
    SELECT pv.pizzeria_id FROM person_visits pv
    JOIN person p ON p.id = pv.person_id
    WHERE p.name = 'Andrey'
), andrey_order AS (
    SELECT m.pizzeria_id FROM person_order po
    JOIN person p ON p.id = po.person_id
    JOIN menu m ON m.id = po.menu_id
    WHERE p.name = 'Andrey'
)

SELECT 
    pi.name AS pizzeria_name 
FROM andrey_order ao
RIGHT JOIN andrey_visits av ON ao.pizzeria_id = av.pizzeria_id
JOIN pizzeria pi ON pi.id = av.pizzeria_id
WHERE 
    ao.pizzeria_id IS NULL;
```

![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/41570a5c-51d2-4751-bd58-757a77afd13a)

# 06
```sql
SELECT 
    m1.pizza_name, 
    pz1.name AS pizzeria_name_1, 
    pz2.name AS pizzeria_name_2, 
    m1.price
FROM menu m1
JOIN menu m2 ON 
    m1.pizza_name = m2.pizza_name AND 
    m1.pizzeria_id > m2.pizzeria_id AND 
    m1.price = m2.price
JOIN pizzeria pz1 ON m1.pizzeria_id = pz1.id
JOIN pizzeria pz2 ON m2.pizzeria_id = pz2.id;
```
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/9b5c6635-575c-4f98-bd5d-ad1038b458d2)

# 07
```sql
INSERT INTO menu (pizza_name, id, price, pizzeria_id) 
    VALUES('greek pizza', 19, 800, 2);

SELECT * FROM menu
WHERE menu.id = 19;
```
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/fe3b8c12-6408-45df-be9b-a558a50c5133)
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/bd2d953b-2801-43ec-88cc-6060304656bc)

# 08
```sql
INSERT INTO menu (pizza_name, id, price, pizzeria_id) 
    VALUES('sicilian pizza', (SELECT MAX(id) FROM menu) + 1, 900, 2);

SELECT * FROM menu
WHERE menu.id = 20;
```
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/24e0fc56-c4c4-4f3e-9b4c-bc95327dff0d)

# 09 
```sql

```












