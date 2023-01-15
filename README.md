# Домашнее задание к занятию "`12.4. «SQL. Часть 2`" - `Александр Бакунин`

---

### Задание 1

SELECT CONCAT(s2.first_name, ' ', s2.last_name) staff_name,
c.city,
(SELECT COUNT(1) FROM customer c2 WHERE c2.store_id = s.store_id) customers_number
from store s
LEFT JOIN staff s2 ON s2.store_id = s.store_id
LEFT JOIN address a on s.address_id = a.address_id
LEFT JOIN city c on c.city_id = a.city_id
WHERE (SELECT COUNT(1) FROM customer c2 WHERE c2.store_id = s.store_id) > 300;

---

### Задание 2

SELECT COUNT(1) number_of_films
FROM film f
WHERE f.`length` > (SELECT AVG(f2.`length`) from film f2);

---

### Задание 3

SELECT summs.mon rental_month, summs.summa, COUNT(r.rental_id) number_of_rentals
FROM
(SELECT MONTH(p.payment_date) mon, SUM(p.amount) summa
FROM payment p
GROUP BY MONTH(p.payment_date)
ORDER BY summa DESC
LIMIT 1) summs
LEFT JOIN rental r ON MONTH(r.rental_date)=summs.mon
GROUP BY rental_month;
