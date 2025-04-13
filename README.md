# Домашнее задание к занятию "`Zabbix part 1`" - `Inshakov Vladimir`

### Задание 1

Установите Zabbix Server с веб-интерфейсом.

Процесс выполнения:

    * Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
    * Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
    * Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.

Требования к результатам:

    * Прикрепите в файл README.md скриншот авторизации в админке.
    * Приложите в файл README.md текст использованных команд в GitHub.

### Решение 1


```
    # Become root user 
    sudo -s

    # Install Zabbix repo
    wget https://repo.zabbix.com/zabbix/7.2/release/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.2+ubuntu24.04_all.deb
    dpkg -i zabbix-release_latest_7.2+ubuntu24.04_all.deb
    apt update
    
    # Install Zabbix-Server Zabbix-Frontend Zabbix-Agent and necessery stuff 
    apt install zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
    apt install postgresql
    
    # Setup Postgres DB
    sudo -u postgres createuser --pwprompt zabbix
    sudo -u postgres createdb -O zabbix zabbix
    zcat /usr/share/zabbix/sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
    
    # Change DBPassword via sed
    sudo sed -i 's/# DBPassword=/DBPassword=1/g' /etc/zabbix/zabbix_server.conf 

    # Restart and enable services
    sudo systemctl restart zabbix-server.service zabbix-agent.service apache2.service 
    sudo systemctl enable zabbix-server.service
    sudo systemctl enable zabbix-agent
    sudo systemctl enable apache2
 
```


Скриншоты:


![Screen1](https://github.com/MrVanG0gh/Netology-smon-zabbix-01/blob/main/pics/Screen1.png)

---

### Задание 2

Установите Zabbix Agent на два хоста.

Процесс выполнения:

    * Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
    * Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
    * Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
    * Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
    * Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.

Требования к результатам:

    * Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу.
    * Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером.
    * Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
    * Приложите в файл README.md текст использованных команд в GitHub.


### Решение 2


```
    # Become root user
    sudo -s

    # Add the Zabbix repo
    wget https://repo.zabbix.com/zabbix/7.2/release/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.2+ubuntu24.04_all.deb
    dpkg -i zabbix-release_latest_7.2+ubuntu24.04_all.deb
    apt update

    # Install Zabbix agent
    apt install zabbix-agent
    
    # Zabbix agent start and enable
    systemctl restart zabbix-agent
    systemctl enable zabbix-agent 

    # Add the correct server IP

    sudo sed -i 's/#Server=127.0.0.1/Server=172.16.185.145/g' /etc/zabbix/zabbix_agentd.conf
    sudo sed -i 's/#ServerActive=127.0.0.1/Server=172.16.185.145:10051/g' /etc/zabbix/zabbix_agentd.conf
    sudo systemctl restart zabbix-agent.service

    # Check the Zabbix Agent log
    tail -f /var/log/zabbix/zabbix_agentd.log
```

Скриншоты:

![Screen2_1](https://github.com/MrVanG0gh/Netology-smon-zabbix-01/blob/main/pics/Screen2_1.png)
![Screen2_2](https://github.com/MrVanG0gh/Netology-smon-zabbix-01/blob/main/pics/Screen2_2.png)
![Screen2_3](https://github.com/MrVanG0gh/Netology-smon-zabbix-01/blob/main/pics/Screen2_3.png)
![Screen2_4](https://github.com/MrVanG0gh/Netology-smon-zabbix-01/blob/main/pics/Screen2_4.png)

---

### Задание 3*

Установите Zabbix Agent на Windows (компьютер) и подключите его к серверу Zabbix.

Требования к результатам:

    * Приложите в файл README.md скриншот раздела Latest Data, где видно свободное место на диске C:

### Решение 3


```
Команды в Github

```


Скриншоты:


![Screen_3_1]()
