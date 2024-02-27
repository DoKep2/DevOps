## **Цель работы**

Закрепить понимание процесса написания ролей и их конфигурирования и развертывания

## **Рекомендуемая документация**

- [Подборка по Ansible](https://gitlab.com/deusops/lessons/documentation/ansible)
- [Документация к PostgreSQL на русском](https://postgrespro.ru/docs/postgrespro/14/index)
- [Установка от ruvds](https://ruvds.com/ru/helpcenter/postgresql-pgadmin-ubuntu/)
- [Что такое pg_hba](https://postgrespro.ru/docs/postgrespro/10/auth-pg-hba-conf)
- [Как работать с пользователями в Postgres](https://www.dmosk.ru/miniinstruktions.php?mini=postgresql-users)
- [Про отказоустойчивость в БД](https://postgrespro.ru/docs/postgrespro/14/high-availability)
- [Настройка репликации в Postgres](https://selectel.ru/blog/tutorials/how-to-set-up-replication-in-postgresql/)
- [Управление высокодоступными PostgreSQL кластерами с помощью Patroni](https://habr.com/ru/post/504044/)

## **Ход работы**

1. Развернуть виртуальную машину для приложения (app) и виртуальную машину для будущей системы базы данных (db) через Vagrantfile
2. Написать роль установки **PostgreSQL** и плейбук, который ее разворачивает
3. Все параметры должны быть вынесены в переменные, все переменные должны быть префиксованы, значения переменных устанавливаются через group_vars для плейбука, роль должна быть покрыта тестами
4. Добавить возможность смены директории с данными на кастомную
5. Добавить возможность создания баз данных и пользователей
6. ***Добавить функционал настройки streaming-репликации***
7. ***Продумать логику определения master и replica нод СУБД и их настройки при работе роли***


### Смена директории данных на кастомную

Для смены директории данных на кастомную, необходимо в файле `group_vars/db.yml` изменить значение переменной `postgresql_data_directory` на путь к кастомной директории.

```yaml
postgresql_data_directory: /path/to/custom/data/directory
```

### Возможность создания баз данных и пользователей

Для создания баз данных и пользователей необходимо добавить их в переменные `postgresql_databases` и `postgresql_users` в файле `group_vars/db.yml`.

```yaml
postgresql_create_databases:
  - name: dbname1
  - name: dbname2
  - name: dbname3
postgresql_create_users:
  - name: user1
    password: secret1
  - name: user2
    password: secret2
  - name: user3
    password: secret3
```

[//]: # (### Функционал настройки Streaming Replication)

[//]: # ()
[//]: # (Для настройки Streaming Replication необходимо добавить в файл `group_vars/db.yml` следующие переменные:)

[//]: # ()
[//]: # (```yaml)

[//]: # (postgresql_master: master)

[//]: # (postgresql_standby: standby)

[//]: # (```)

[//]: # ()
[//]: # (### Логика определения master и replica нод СУБД и их настройка при работе роли)

[//]: # ()
[//]: # (Для определения master и replica нод СУБД используется переменная `postgresql_replication` в файле `group_vars/db.yml`.)

[//]: # ()
[//]: # (```yaml)

[//]: # (postgresql_replication: true)
```



