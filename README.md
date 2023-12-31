# Домашнее задание к занятию "`Система мониторинга Zabbix`" - `Макаров Денис`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1
Установите Zabbix Server с веб-интерфейсом.

Процесс выполнения
Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
1. Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
2. Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
3. Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.

Требования к результаты
1. Прикрепите в файл README.md скриншот авторизации в админке.
2. Приложите в файл README.md текст использованных команд в GitHub.

Решение:

 Установленный zabbix-server и авторизация в админке представлена на скриншоте ниже:
   

![Снимок33](https://github.com/Makarov-Denis/zabbixv1/assets/148921246/01e435ef-625b-4ef9-99fa-86621059733d)

Список использованных команд:

sudo apt install postgresql

wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-5+debian12_all.deb

sudo dpkg -i zabbix-release_6.0-5+debian12_all.deb

sudo apt update

sudo apt install zabbix-server-pgsql zabbix-frontend-php php8.2-pgsql zabbix-apache-conf zabbix-sql-scripts

sudo -u postgres createuser --pwprompt zabbix

sudo -u postgres createdb -O zabbix zabbix

zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

sudo nano /etc/zabbix/zabbix_server.conf

sudo systemctl restart zabbix-server apache2

sudo systemctl enable zabbix-server apache2

sudo systemctl status zabbix-server.service

---

### Задание 2

Установите Zabbix Agent на два хоста

Процесс выполнения

Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.

1. Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
2. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
3. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
4. Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.

Требования к результаты

1. Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
2. Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером
3. Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
4. Приложите в файл README.md текст использованных команд в GitHub

Решение:

Выполение задания представлены на скриншотах ниже:

![Снимок34](https://github.com/Makarov-Denis/zabbixv1/assets/148921246/21853cc9-5fb5-4bf8-87de-3f20312207cc)

![Снимок35](https://github.com/Makarov-Denis/zabbixv1/assets/148921246/9e616e09-d9c7-45c3-a336-555a478177f8)

![Снимок36](https://github.com/Makarov-Denis/zabbixv1/assets/148921246/38908600-9416-48a7-9096-024a11e9d7ec)

![Снимок37](https://github.com/Makarov-Denis/zabbixv1/assets/148921246/4222f093-b0fd-4986-9193-bf1c7407a09e)

![Снимок38](https://github.com/Makarov-Denis/zabbixv1/assets/148921246/cea27f37-f3ac-47bb-9800-c186f8a179b5)
   
Список использованных команд:

wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-5+debian12_all.deb

sudo dpkg -i zabbix-release_6.0-5+debian12_all.deb

sudo apt update

sudo apt install zabbix-agent

sudo systemctl enable zabbix-agent

systemctl status zabbix-agent.service

sudo nano /etc/zabbix/zabbix_agentd.conf

sudo systemctl restart zabbix-agent.service

sudo systemctl status zabbix-agent.service

sudo tail -f /var/log/zabbix/zabbix_agentd.log

---


