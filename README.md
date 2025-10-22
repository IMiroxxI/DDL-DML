# 12.2 Работа с данными (DDL/DML)
Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1
1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp. 

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

1.4. Дайте все права для пользователя sys_temp. 

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос: 
```sql
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.7. Восстановите дамп в базу данных.

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*

#### *Ответ:*

1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.
```bash
wget -c https://dev.mysql.com/get/mysql-apt-config_0.8.28-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.28-1_all.deb
sudo apt update
sudo apt install mysql-server
sudo systemctl status mysql
sudo systemctl enable mysql
sudo mysql -u root
```
![1.1](https://github.com/IMiroxxI/DDL-DML/blob/main/img/1.1.png)
![1.1.1](https://github.com/IMiroxxI/DDL-DML/blob/main/img/1.1.1.png)

1.2. Создайте учётную запись sys_temp. 
```bash
CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY '1234567';
```
![1.2](https://github.com/IMiroxxI/DDL-DML/blob/main/img/1.2.png)

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)
```bash
SELECT user FROM mysql.user;
```
![1.3](https://github.com/IMiroxxI/DDL-DML/blob/main/img/1.3.png)

1.4. Дайте все права для пользователя sys_temp. 
```bash
GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost' WITH GRANT OPTION;
```
![1.4](https://github.com/IMiroxxI/DDL-DML/blob/main/img/1.4.png)

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)
```bash
SELECT * FROM information_schema.user_privileges WHERE GRANTEE="'sys_temp'@'localhost'";
```
![1.5](https://github.com/IMiroxxI/DDL-DML/blob/main/img/1.5.png)

1.6. Переподключитесь к базе данных от имени sys_temp.
```bash
SYSTEM mysql -u sys_temp -p
SELECT user();
```
![1.6](https://github.com/IMiroxxI/DDL-DML/blob/main/img/1.6.png)

Для смены типа аутентификации с sha2 используйте запрос: 
```sql
ALTER USER 'sys_temp'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
![1.6.1](https://github.com/IMiroxxI/DDL-DML/blob/main/img/1.6.1.png)

1.7. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.
```bash
wget https://downloads.mysql.com/docs/sakila-db.zip
unzip sakila-db.zip
```
![1.7](https://github.com/IMiroxxI/DDL-DML/blob/main/img/1.7.png)

1.8. Восстановите дамп в базу данных.
```bash
source /home/tverdyakov/sakila-db/sakila-schema.sql
source /home/tverdyakov/sakila-db/sakila-data.sql
SHOW DATABASES;
```
![1.8](https://github.com/IMiroxxI/DDL-DML/blob/main/img/1.8.png)
![1.8.1](https://github.com/IMiroxxI/DDL-DML/blob/main/img/1.8.1.png)
![1.8.2](https://github.com/IMiroxxI/DDL-DML/blob/main/img/1.8.2.png)

1.9. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)
```bash
SHOW TABLES;
```
![1.9](https://github.com/IMiroxxI/DDL-DML/blob/main/img/1.9.png)
![1.9.1](https://github.com/IMiroxxI/DDL-DML/blob/main/img/1.9.1.png)

*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*


### Задание 2
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)
```
Название таблицы | Название первичного ключа
customer         | customer_id
```

#### *Ответ:*
```bash
+---------------+--------------+
| TABLE_NAME    | COLUMN_NAME  |
+---------------+--------------+
| actor         | actor_id     |
| address       | address_id   |
| category      | category_id  |
| city          | city_id      |
| country       | country_id   |
| customer      | customer_id  |
| film          | film_id      |
| film_actor    | actor_id     |
| film_actor    | film_id      |
| film_category | film_id      |
| film_category | category_id  |
| film_text     | film_id      |
| inventory     | inventory_id |
| language      | language_id  |
| payment       | payment_id   |
| rental        | rental_id    |
| staff         | staff_id     |
| store         | store_id     |
+---------------+--------------+
```
![2](https://github.com/IMiroxxI/DDL-DML/blob/main/img/2.png)

---
