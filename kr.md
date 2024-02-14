# 1
```sql
WITH tab AS (
    SELECT 
        customer_id, 
        SUM(o.quantity * p.price),
        o.order_date
    FROM orders o
    JOIN products p ON p.product_id = o.product_id
    GROUP BY o.customer_id, o.order_date
)

SELECT sum, c.first_name, c.last_name FROM tab
JOIN customers c ON c.customer_id = tab.customer_id
WHERE tab.order_date BETWEEN '2024-01-13' AND '2024-02-13'
ORDER BY sum DESC;
```
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/54b7126b-d868-407e-9d97-852cbaeef216)
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/79dd616a-fec6-4326-a913-4af745f050a3)

# 2
```sql

```

# 3
```sql
UPDATE products 
SET price = price * 0.9
WHERE products.category = 'Clothing';

```
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/220b8a89-2a0c-4d06-ac80-63b005039ae9)


# 4
```sql
WITH avg AS (
    SELECT 
        p.category, 
        AVG(price) 
    FROM products p
    GROUP BY p.category 
)
SELECT * FROM avg
ORDER BY 2 DESC;
```
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/19a6cd3e-486b-4ee8-9178-910755faf14f)


# 5
```sql
DELETE FROM orders
WHERE quantity > (SELECT avg(quantity) FROM orders);
```
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/f377dfaa-405f-4aee-91db-36762c670b08)


















