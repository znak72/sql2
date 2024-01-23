# Домашнее задание к занятию 12.4 "Реляционные базы данных: SQL. Часть 2" 

### Задание 1.

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина,
- город нахождения магазина,
- количество пользователей, закрепленных в этом магазине.

```sql
SELECT s.store_id, count(c.customer_id) AS "number of buyers", ci.city, concat(st.last_name, ' ', st.first_name) AS "salesman"
FROM store s
JOIN customer c ON c.store_id = s.store_id
JOIN address a ON a.address_id = s.address_id
JOIN city ci ON ci.city_id = a.city_id
JOIN staff st ON st.store_id = s.store_id
GROUP BY s.store_id, ci.city_id, st.staff_id
HAVING count(c.customer_id) > 300;
```

![image](https://github.com/znak72/sql2/blob/main/SQL_PART_2_TASK_01.png)

### Задание 2.

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

```sql
SELECT COUNT(film_id) AS 'number of films'
FROM (SELECT *, AVG(LENGTH) OVER () AS TIME FROM film) t
WHERE TIME < LENGTH;
```

![image](https://github.com/znak72/sql2/blob/main/SQL_PART_2_TASK_02.png)

### Задание 3.

Получите информацию, за какой месяц была получена наибольшая сумма платежей и добавьте информацию по количеству аренд за этот месяц.

```sql
SELECT MONTH(p.payment_date) AS month, SUM(p.amount) AS 'total amount', count(p.rental_id) AS 'rentals by month'
FROM payment p
GROUP BY MONTH(p.payment_date)
ORDER BY SUM(p.amount) DESC
LIMIT 1;
```

![image](https://github.com/znak72/sql2/blob/main/SQL_PART_2_TASK_03.png)
