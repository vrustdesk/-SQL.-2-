# Домашнее задание к занятию «SQL. Часть 2»
Иванов Владислав

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.



### РЕШЕНИЕ


### Задание 1

```SQL
SELECT CONCAT(s2.first_name, ' ', s2.last_name) AS Name, a.address AS Address, COUNT(c.store_id) AS Customers
FROM store s 
JOIN customer c ON s.store_id = c.store_id 
JOIN staff s2 ON s.manager_staff_id = s2.staff_id 
JOIN address a ON s.address_id = a.address_id 
GROUP BY c.store_id 
HAVING COUNT(c.store_id) > 300;
```

<img width="886" height="263" alt="image" src="https://github.com/user-attachments/assets/116518ba-f708-45e9-a119-6276f6a450e0" />


### Задание 2

```SQL
SELECT (SELECT  AVG(`length`) from film) AS Average, (SELECT COUNT(1) from film) AS 'All films', COUNT(1) AS 'Long Films'
FROM film 
WHERE `length` > (SELECT AVG(`length`) from film) ;
```

<img width="864" height="188" alt="image" src="https://github.com/user-attachments/assets/2772eb7a-57cd-4705-9489-43e8e531bf35" />


### Задание 3

```SQL
SELECT MONTH(payment_date) AS Month, COUNT(payment_id) As Payments, SUM(amount) AS Amount
FROM payment
GROUP BY MONTH(payment_date) 
ORDER BY COUNT(payment_id)  DESC LIMIT 1 ;
```

<img width="876" height="201" alt="image" src="https://github.com/user-attachments/assets/3811ad6d-00cc-414e-98b9-3badeaf1ff5f" />
