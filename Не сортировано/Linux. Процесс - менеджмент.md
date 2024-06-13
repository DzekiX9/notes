## Установка

``` bash
sudo apt install nodejs

​sudo apt install npm
```

``` bash
npm install pm2 -g
```

## Настройка

Добавление нового процесса:

``` bash
pm2 start app_name.py --interpreter=python3
```
 
 Просмотр списка всех процессов:
 
``` bash
pm2 list
```

![[Pasted image 20240614004356.png]]

Остановка:
```
pm2 stop id


Запуск:

pm2 start id

Рестарт:

pm2 restart id

Удаление из списка:

pm2 delete id

Также можно просмотреть логи отдельных приложений. Для этого используем эту команду:

pm2 monit

И выбираем свое приложение из списка.

![[Pasted image 20240614004649.png]]