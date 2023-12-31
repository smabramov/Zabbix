# Домашнее задание к занятию "Система мониторинга Zabbix" - Абрамов Сергей


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



1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
3. Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
4. Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.

 
```
Поле для вставки кода...
sudo apt install postgresql
# wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb
# dpkg -i zabbix-release_6.0-4+debian11_all.deb
# apt update
# apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts
su - postgres -c 'psql --command "CREATE USER zabbix WITH PASSWORD '\'123456789\'';"'
su - postgres -c 'psql --command "CREATE DATABASE zabbix OWNER zabbix;"'
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
sed -i 's/# DBPassword=/DBPassword=/123456789/g' /etc/zabbix/zabbix_server.conf
```

'![install zabbix-server](https://github.com/smabramov/Zabbix/blob/33909bf0fcad53d8bdaa2ede24539621cbc91503/img/install%20zabbix-server.png)'

'![web zabbix](https://github.com/smabramov/Zabbix/blob/33909bf0fcad53d8bdaa2ede24539621cbc91503/img/web%20zabbix.png)'




### Задание 2

`Приведите ответ в свободной форме........`

1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
5. Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.


```
Поле для вставки кода...
# wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb
# dpkg -i zabbix-release_6.0-4+debian11_all.deb
# apt update
# apt install zabbix-agent
# systemctl restart zabbix-agent
# systemctl enable zabbix-agent
```


![agent](https://github.com/smabramov/Zabbix/blob/b43ddb85339daeabd36ad0f38c166a8c90d2666e/img/agent.png)

![test-zabbix_log](https://github.com/smabramov/Zabbix/blob/b43ddb85339daeabd36ad0f38c166a8c90d2666e/img/test-zabbix_log.png)

![vm-1_log](https://github.com/smabramov/Zabbix/blob/b43ddb85339daeabd36ad0f38c166a8c90d2666e/img/vm-1_log.png)

![data_test-zabbix](https://github.com/smabramov/Zabbix/blob/b43ddb85339daeabd36ad0f38c166a8c90d2666e/img/data_test-zabbix.png)

![data_vm-1](https://github.com/smabramov/Zabbix/blob/b43ddb85339daeabd36ad0f38c166a8c90d2666e/img/data_vm-1.png)


---
