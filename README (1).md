

file:///home/kirill/%D0%98%D0%B7%D0%BE%D0%B1%D1%80%D0%B0%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA%20%D1%8D%D0%BA%D1%80%D0%B0%D0%BD%D0%B0%20%D0%BE%D1%82%202025-09-06%2023-20-15.png


```bash
# Обновление и установка PostgreSQL
sudo apt update
sudo apt install -y postgresql

# Подключение репозитория Zabbix 7.4 для Debian 12
sudo wget https://repo.zabbix.com/zabbix/7.4/release/debian/pool/main/z/zabbix-release/zabbix-release_latest_7.4+debian12_all.deb
sudo dpkg -i zabbix-release_latest_7.4+debian12_all.deb
sudo apt update

# Установка Zabbix Server, frontend и SQL‑скриптов
sudo apt install zabbix-server-pgsql zabbix-frontend-php php8.2-pgsql zabbix-apache-conf zabbix-sql-scripts
 
# Создание базы данных и пользователя
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix

# Импорт схемы
sudo zcat /usr/share/zabbix/sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

# Настройка конфигурации Zabbix Server
sudo nano /etc/zabbix/zabbix_server.conf
DBPassword=123

# Перезапуск сервисов
sudo systemctl restart postgresql zabbix-server apache2
sudo systemctl enable postgresql zabbix-server apache2
```
Вход и настройка сервера Zabbix осуществлялась через localhost/Zabbix