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


![Screen_1_1]()

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
Команды в Github

```


Скриншоты:


![Screen_2_1]()
![Screen_2_2]()
![Screen_2_3]()
![Screen_2_4]()
![Screen_2_5]()
![Screen_2_6]()

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
