# Домашнее задание к занятию "Работа с данными (DDL/DML)" - `Вялов владислав`


### Задание 1

1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp.

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

1.4. Дайте все права для пользователя sys_temp.

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос:

ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.7. Восстановите дамп в базу данных.

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.

# Скачаk образ MySQL 
docker pull mysql:8.0

# Запуск контейнера
docker run --name mysql8 -e MYSQL_ROOT_PASSWORD=rootpassword -p 3306:3306 -d mysql:8.0

# Подключиться к контейнеру
docker exec -it mysql8 mysql -u root -p

# Создание профиля с паролем 'password'
CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY 'password';

# Просмотр всех пользователей
SELECT user, host FROM mysql.user;

# Даю права на базы данных
GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost';

# Применяю изменения
FLUSH PRIVILEGES;

# Просмотр прав пользователя
SHOW GRANTS FOR 'sys_temp'@'localhost';

# Выход из текущей сессии и переподключение
EXIT;
mysql -u sys_temp -p

# Скачивание и распаковка архива 
wget https://downloads.mysql.com/docs/sakila-db.zip

unzip sakila-db.zip

# Восстановление структуры базы и данных 
mysql -u sys_temp -p < sakila-schema.sql

mysql -u sys_temp -p < sakila-data.sql

# Показать все таблицы базы sakila
USE sakila;
SHOW TABLES;

![alt text](img/1.jpg)

![alt text](img/2.jpg)

![alt text](img/3.jpg)

![alt text](img/4.jpg)

![alt text](img/5.jpg)

![alt text](img/6.jpg)

![alt text](img/7.jpg)

### Задание 2
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)

![alt text](img/8.jpg)