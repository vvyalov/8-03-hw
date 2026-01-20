# Домашнее задание к занятию "Резервное копирование." - `Вялов владислав`


## Задание 1

Финансовая компания решила увеличить надёжность работы баз данных и их резервного копирования.

Необходимо описать, какие варианты резервного копирования подходят в случаях:

1.1. Необходимо восстанавливать данные в полном объёме за предыдущий день.

1.2. Необходимо восстанавливать данные за час до предполагаемой поломки.

Приведите ответ в свободной форме.

Ответ

1.1 Для этого подходит полное ежедневное резервное копирование (Full Backup), выполняемое, например, ночью после окончания основных рабочих процессов и журналы транзакций для минимизации потерь данных на случай сбоя в течение дня,  преимущества этого в том что нужна только одна резервная копия за предыдущий день, что упрощает восстановление данных. 

1.2   Для этого подходит полное резервное копирование (ежедневное или еженедельное) + разностные резервные копии каждые несколько часов и непрерывное архивирование журналов транзакций с частотой, например, каждые 15–30 минут


## Задание 2

2.1. С помощью официальной документации приведите пример команды резервирования данных и восстановления БД (pgdump/pgrestore).

Приведите ответ в свободной форме.

Ответ

Резервное копирование 

### Создание дампа одной базы в custom-формате
pg_dump -U username -h localhost -d mydatabase -F c -b -v -f /backup/mydatabase_backup.dump

### Создание дампа в виде SQL-скрипта
pg_dump -U username -h localhost -d mydatabase -F p -f /backup/mydatabase_backup.sql

### Создание дампа всех баз данных кластера
pg_dumpall -U username -h localhost -f /backup/all_databases.sql

Восстановление 

### Восстановление из custom-формата в новую базу данных
pg_restore -U username -h localhost -d newdatabase -v /backup/mydatabase_backup.dump

### Восстановление с созданием новой базы
createdb -U username -h localhost newdatabase
pg_restore -U username -h localhost -d newdatabase -v /backup/mydatabase_backup.dump

### Восстановление только структуры
pg_restore -U username -h localhost -d newdatabase -s -v /backup/mydatabase_backup.dump

### Восстановление только данных 
pg_restore -U username -h localhost -d newdatabase -a -v /backup/mydatabase_backup.dump

### Восстановление из SQL-скрипта
psql -U username -h localhost -d newdatabase -f /backup/mydatabase_backup.sql


## Задание 3

MySQL

3.1. С помощью официальной документации приведите пример команды инкрементного резервного копирования базы данных MySQL.

### Создаем полный бэкап
mysqldump -u root -p --single-transaction --flush-logs --master-data=2 \
--all-databases > /backup/full_backup_$(date +%Y%m%d).sql

### После полного бэкапа смотрим текущий бинарный лог
SHOW MASTER STATUS;

### Находим нужные файлы бинарных логов
cp /var/lib/mysql/mysql-bin.000003 /backup/incremental/
cp /var/lib/mysql/mysql-bin.000004 /backup/incremental/



