# Домашнее задание к занятию "`Система мониторинга Zabbix`" - `Вялов владислав`


### Задание 1

 скриншот 1
![alt text](img/1.jpg)
  



# 1. Установка PostgreSQL
sudo apt install -y postgresql postgresql-contrib
sudo systemctl start postgresql
sudo systemctl enable postgresql

# 2. Создание базы данных и пользователя для Zabbix
sudo -u postgres createuser --pwprompt zabbix
# Вводим пароль: zabbix
sudo -u postgres createdb -O zabbix zabbix

# 3. Установка репозитория Zabbix
wget https://repo.zabbix.com/zabbix/7.2/debian/pool/main/z/zabbix-release/zabbix-release_7.7-3+debian11_all.deb
sudo dpkg -i zabbix-release_7.2-3+debian11_all.deb
sudo apt update

# 4. Установка компонентов Zabbix
sudo apt install -y zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent

# 5. Импорт начальной схемы базы данных
sudo zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

# 6. Настройка конфигурации Zabbix Server
sudo sed -i 's/^# DBPassword=.*/DBPassword=zabbix/' /etc/zabbix/zabbix_server.conf
sudo sed -i 's/^# DBHost=.*/DBHost=localhost/' /etc/zabbix/zabbix_server.conf

# 7. Запуск и включение служб
sudo systemctl restart zabbix-server zabbix-agent apache2
sudo systemctl enable zabbix-server zabbix-agent apache2

# 8. Проверка статуса служб
sudo systemctl status zabbix-server
sudo systemctl status zabbix-agent
sudo systemctl status apache2





### Задание 2



 скриншот 1 ![alt text](img/2.jpg)
 
 скриншот 2 ![alt text](img/3.jpg)

 скриншот 3 ![alt text](img/4.jpg)



# 1. Установка репозитория Zabbix

wget https://repo.zabbix.com/zabbix/7.2/release/debian/pool/main/z/zabbix-release/zabbix-release_latest_7.2+debian12_all.deb
sudo dpkg -i zabbix-release_latest_7.2+debian12_all.deb
sudo apt update

# 2. Установка Zabbix Agent

sudo apt install zabbix-agent

# 3. Настройка конфигурации агента

sudo sed -i 's/Server=127.0.0.1/Server=10.0.2.30/g' /etc/zabbix/zabbix_agentd.conf
sudo sed -i 's/ServerActive=127.0.0.1/ServerActive=10.0.2.30/g' /etc/zabbix/zabbix_agentd.conf
sudo sed -i 's/Hostname=Zabbix server/Hostname=zbx-host01/g' /etc/zabbix/zabbix_agentd.conf

# 4. запуск и автозагрузка службы 
sudo systemctl restart zabbix-agent
sudo systemctl enable zabbix-agent

# 5. Проверка статуса службы
sudo systemctl status zabbix-agent

# 6. Проверка сетевых подключений
sudo netstat -tlnp | grep zabbix


---

