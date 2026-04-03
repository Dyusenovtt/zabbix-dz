# zabbix-dz
задание 1
<img width="1641" height="639" alt="5" src="https://github.com/user-attachments/assets/5bd22e2f-a2ef-4ecb-a0c3-7f655da0127f" />
текст кода сервера https://github.com/Dyusenovtt/zabbix-dz/blob/main/server%20code.txt
задание 2
<img width="1665" height="662" alt="1" src="https://github.com/user-attachments/assets/9fdb68b4-cfc8-41f5-9ddd-69ec7825430a" />
<img width="1661" height="1297" alt="2" src="https://github.com/user-attachments/assets/53079c5b-9c25-4026-b732-2d0fb5bccad8" />
<img width="1407" height="1169" alt="Снимок экрана 2026-04-03 085400" src="https://github.com/user-attachments/assets/de61046e-b31b-4437-9a91-dc84a381420d" />
текст кода агента https://github.com/Dyusenovtt/zabbix-dz/blob/main/agent%20coode.txt
Задание 1
# 1. Обновление системы
sudo apt update && sudo apt upgrade -y
# 2. Установка PostgreSQL
sudo apt install -y postgresql postgresql-contrib
sudo systemctl enable --now postgresql
# 3. Добавление репозитория Zabbix
wget https://repo.zabbix.com/zabbix/7.0/debian/pool/main/z/zabbix-release/zabbix-release_7.0-1+debian11_all.deb
sudo dpkg -i zabbix-release_7.0-1+debian11_all.deb
sudo apt update
# 4. Установка Zabbix Server
sudo apt install -y zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
# 5. Настройка базы данных
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
# 6. Настройка Zabbix Server
sudo sed -i 's/# DBHost=localhost/DBHost=localhost/' /etc/zabbix/zabbix_server.conf
sudo sed -i 's/# DBPassword=/DBPassword=your_password/' /etc/zabbix/zabbix_server.conf
# 7. Запуск сервисов
sudo systemctl restart zabbix-server zabbix-agent apache2
sudo systemctl enable zabbix-server zabbix-agent apache2
