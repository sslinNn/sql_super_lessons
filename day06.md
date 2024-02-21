# 00
```sql
CREATE TABLE person_discounts (
    id BIGINT PRIMARY KEY,
    person_id BIGINT NOT NULL ,
    pizzeria_id BIGINT NOT NULL ,
    dsicount FLOAT DEFAULT NULL ,
    CONSTRAINT fk_person_discount_person_id FOREIGN KEY (person_id) REFERENCES person(id),
    CONSTRAINT fk_person_discount_pizzeria_id FOREIGN KEY (pizzeria_id) REFERENCES pizzeria(id)
    );

SELECT * FROM person_discounts;
```
  Я ПЕРЕИМЕНОВАЛ, ВСЕ НОРМ
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/a0f38f30-5ef8-43ed-8d1a-da38b13999e6)
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/b33eaec6-5758-4ec4-9eec-0335451d16c8)

# 01
```sql
WITH amount_of_orders as (
SELECT 
    po.person_id, 
    m.pizzeria_id, 
    count(*) 
FROM person_order po
JOIN menu m ON m.id = po.menu_id
GROUP BY 1, 2
ORDER BY 1, 2
)

INSERT INTO person_discounts(
    SELECT 
        ROW_NUMBER() OVER(ORDER BY 1) as id,
        person_id, 
        pizzeria_id,
        CASE
            WHEN count = 1 THEN 10.5
            WHEN count = 2 THEN 22
            ELSE 30 
        END
    FROM amount_of_orders
);
```
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/b3ecf09d-29cc-4802-a739-c72575a7e944)

# 02
```sql
SELECT 
    p.name, 
    m.pizza_name, 
    m.price,
    (m.price-(m.price/100) * pd.discount) as discount_price,
    pz.name 
FROM person p
JOIN person_order po ON po.person_id = p.id
JOIN menu m ON m.id = po.menu_id
JOIN pizzeria pz ON pz.id = m.pizzeria_id
JOIN person_discounts pd ON pd.id = p.id
ORDER BY 1;
```
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/17483bc5-cbd1-46ab-b669-4b3520d6419e)

# 04
```sql
ALTER TABLE person_discounts 
    ADD CONSTRAINT ch_nn_person_id CHECK (person_id IS NOT NULL);

ALTER TABLE person_discounts 
    ADD CONSTRAINT ch_nn_pizzeria_id CHECK (pizzeria_id IS NOT NULL);

ALTER TABLE person_discounts 
    ADD CONSTRAINT ch_nn_discount CHECK (discount IS NOT NULL);

ALTER TABLE person_discounts 
    ALTER discount SET DEFAULT 0;

ALTER TABLE person_discounts 
    ADD CONSTRAINT ch_range_discount CHECK (discount BETWEEN 0 AND 100);
```
![image](https://github.com/sslinNn/sql_super_lessons/assets/113080924/bf9d12d2-fc8b-4ab4-aa6a-3b178302ae38)


# 06
```sql
CREATE SEQUENCE seq_person_discounts;
```







