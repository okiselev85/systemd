#### Создаем watchlog - файл с конфигурацией сервиса
* vi /etc/sysconfig/watchlog
* vi /var/log/watchlog.log 

###### Создаем скрипт
* nano /opt/watchlog.sh
###### Создаем  unit для сервиса
* nano /etc/systemd/system/watchlog.service
###### Создаем  unit для таймера
* nano /etc/systemd/system/watchlog.timer
###### Стартуем таймер
* systemctl start watchlog.timer
#### Результат крона на скриншоте

#### Ставим spawn-fcgi и переписываем init-скрипт на unit-файл
* yum install epel-release -y && yum install spawn-fcgi php php-cli mod_fcgid httpd -y
###### Вносим изменения в строки файла 
* /etc/sysconfig/spawn-fcgi
###### Делаем unit файл  /etc/systemd/system/spawn-fcgi.service
###### Проверяем, что все работает
* systemctl start spawn-fcgi
*_ spawn-fcgi.service - Spawn-fcgi startup service by Otus
   Loaded: loaded (/etc/systemd/system/spawn-fcgi.service; disabled; vendor preset: disabled)
   Active: active (running) since Mon 2019-11-25 15:52:58 MSK; 7s ago
 Main PID: 24446 (php-cgi)
    Tasks: 33
   CGroup: /system.slice/spawn-fcgi.service
           ├─24446 /usr/bin/php-cgi
           ├─24453 /usr/bin/php-cgi
           ├─24454 /usr/bin/php-cgi
           ├─24455 /usr/bin/php-cgi
           ├─24456 /usr/bin/php-cgi
           ├─24457 /usr/bin/php-cgi
           ├─24458 /usr/bin/php-cgi
           ├─24459 /usr/bin/php-cgi
           ├─24460 /usr/bin/php-cgi
           ├─24461 /usr/bin/php-cgi
           ├─24462 /usr/bin/php-cgi
           ├─24463 /usr/bin/php-cgi
           ├─24464 /usr/bin/php-cgi
           ├─24465 /usr/bin/php-cgi
           ├─24466 /usr/bin/php-cgi
           ├─24467 /usr/bin/php-cgi
           ├─24468 /usr/bin/php-cgi
           ├─24470 /usr/bin/php-cgi
           ├─24471 /usr/bin/php-cgi
           ├─24472 /usr/bin/php-cgi
           ├─24473 /usr/bin/php-cgi
           ├─24474 /usr/bin/php-cgi
           ├─24475 /usr/bin/php-cgi
           ├─24476 /usr/bin/php-cgi
           ├─24477 /usr/bin/php-cgi
           ├─24478 /usr/bin/php-cgi
           ├─24479 /usr/bin/php-cgi
           ├─24480 /usr/bin/php-cgi
           ├─24481 /usr/bin/php-cgi
           ├─24482 /usr/bin/php-cgi
           ├─24483 /usr/bin/php-cgi
           ├─24484 /usr/bin/php-cgi
           └─24485 /usr/bin/php-cgi

Nov 25 15:52:58 srv-devops-omk systemd[1]: Started Spawn-fcgi startup service by Otus.

### Дополняем unit файл apache httpd возможностью запуска несколько инстансов разных конфигов
#### Создем шаблон файла конфигурации
* nano /etc/systemd/system/httpd-first
* nano /etc/systemd/system/httpd-second
* nano /etc/httpd/conf/first.conf
* nano /etc/httpd/conf/second.conf

#### Делаем юниты
cp /etc/systemd/system/httpd-first /etc/systemd/system/httpd@first.service
cp /etc/systemd/system/httpd-second /etc/systemd/system/httpd@second.service

### Скриншот с результатм запуска двух апачей на скриншоте
