# Домашнее задание к занятию "Резервное копирование баз данных" - `Нагорнов Антон Алексеевич`

### Задание 1

1.1 Возможно использовать полный или инкрементный бекап  
1.2 Инкрементный бекап  
1.3* Возможно при правильной настройке master-slave репликации  

### Задание 2

Для создания дампа:  
pg_dump <параметры> <имя базы> > <файл, куда сохранить дамп>  
Например: pg_dump testbd > /home/test/testb_dump  

Для восстановления:  
pg_restore <параметры> <имя базы> > <файл, куда восстановить дамп>  
Например: pg_restore -d testbd_dump > /home/test/testbd_restore  

2.1* Процесс возможно автоматизировать с помощью написания скрипта и добавления его в планировщик задач, например crontab  

### Задание 3

Для создания и обновления инкреметированного бекапа предлагается использовать сделующую команду:  

Для Enterprise версии:  
mysqldump --single-transaction --quick --skip-extended-insert \ --routines -umyuser -pmysecret dbname &gt; /path/to/dumps/dir/  
dbname.dump; rdiff-backup /path/to/dumps/dir/ /path/to/backup/dir/  

Для обычной версии:  
mysqldump --single-transaction --flush-logs --master-data=2 --databases mydatabase > mydatabase_incr_backup.sql  

3.1* Использование репликации дает преимущество по сравнению с обычным резервным копирование в случае отказа основной БД,  
повышенной нагрузки на основную БД, времени восстановления работоспособности основной БД.  
