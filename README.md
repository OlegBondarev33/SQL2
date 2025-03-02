# Домашнее задание к занятию «SQL. Часть 2» Бондарев Олег

### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и ваши фамилию и имя;
   - в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
   - для корректного добавления скриншотов воспользуйтесь инструкцией [«Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.

Желаем успехов в выполнении домашнего задания.

---

Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

- SELECT
-    s.store_id,
-    st.first_name AS staff_first_name,
-    st.last_name AS staff_last_name,
-    ci.city AS store_city,
-    COUNT(c.customer_id) AS customer_count
- FROM store AS s
- JOIN staff AS st ON s.store_id = st.store_id
- JOIN address AS a ON s.address_id = a.address_id
- JOIN city AS ci ON a.city_id = ci.city_id
- JOIN customer AS c ON s.store_id = c.store_id
- GROUP BY s.store_id, st.first_name, st.last_name, ci.city
- HAVING COUNT(c.customer_id) > 300;

![image](https://github.com/user-attachments/assets/6047779e-312d-47af-b40b-e3292933109a)


### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

- SELECT COUNT(*)
- FROM film
- WHERE length > (SELECT AVG(length) FROM film);

![image](https://github.com/user-attachments/assets/a9920ab3-d493-4c64-b4a2-5b580e231980)


### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

- SELECT
-    MONTH(payment_date) AS payment_month,
-    YEAR(payment_date) AS payment_year,
-    SUM(amount) AS total_payment_amount,
-    COUNT(DISTINCT rental_id) AS total_rentals
- FROM payment
- GROUP BY payment_month, payment_year
- ORDER BY total_payment_amount DESC
- LIMIT 1;

![image](https://github.com/user-attachments/assets/9e97a745-379f-4a54-b385-cadc3da24758)


## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 4*

Посчитайте количество продаж, выполненных каждым продавцом. Добавьте вычисляемую колонку «Премия». Если количество продаж превышает 8000, то значение в колонке будет «Да», иначе должно быть значение «Нет».

### Задание 5*

Найдите фильмы, которые ни разу не брали в аренду.
