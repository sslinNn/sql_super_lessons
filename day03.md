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

```



















