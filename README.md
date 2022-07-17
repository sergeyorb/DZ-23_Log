# Домашнее задание Сбор и анализ логов  
<ol> 
  <li>Создать сденд для выполнения домашнего задания
  <li> Настроить стенд для выполнения домашнего задания
  <li> Настраиваем Ubuntu_Syslog
  <li> Настраиваем Ubuntu_Nginx  
  <li> Получаем логи с Web на rsyslog
</ol>  

# 1. Создать сденд для выполнения домашнего задания
<ul>
  <p> Развернута VM на базе Ubuntu ubuntu-20.04.3-live-server-amd64 с названием Ubuntu_Syslog
  <p> Развернута VM на базе Ubuntu ubuntu-20.04.3-live-server-amd64 с названием Ubuntu_Nginx   
</ul> 

# 2. Настроить стенд для выполнения домашнего задания

# 3. Настраиваем Ubuntu_Syslog
  <ul>
  <li> Переходим в root и устанавливаем время по Москве</li>
  <p> root@ubuntusyslog:~# date
  <p> Sat 16 Jul 2022 05:44:45 PM UTC
  <p> root@ubuntusyslog:~# cp /usr/share/zoneinfo/Europe/Moscow /etc/localtime
  <p> root@ubuntusyslog:~# date
  <p> Sat 16 Jul 2022 08:45:13 PM MSK  
  
  <li> Перезапуск systemd-timesyncd.service и проверка работы</li>
  <p> root@ubuntusyslog:~# systemctl restart systemd-timesyncd.service
  <p> root@ubuntusyslog:~# systemctl status systemd-timesyncd.service
      
  <li> Откоректировал /etc/rsyslog.conf</li>
   
  <li> Рестарт syslog и проверил порты</li>
  <p> root@ubuntusyslog:~# systemctl restart rsyslog
  <p> root@ubuntusyslog:~# ss -tuln
  </ul>

# 4. Настраиваем Ubuntu_Nginx
<ul>
<li> Переходим в root и устанавливаем время по Москве</li>
  <p> root@ubuntusyslog:~# date
  <p> Sat 16 Jul 2022 05:44:45 PM UTC
  <p> root@ubuntusyslog:~# cp /usr/share/zoneinfo/Europe/Moscow /etc/localtime
  <p> root@ubuntusyslog:~# date
  <p> Sat 16 Jul 2022 08:45:13 PM MSK  
<li> Перезапуск systemd-timesyncd.service и проверка работы</li>
  <p> root@ubuntusyslog:~# systemctl restart systemd-timesyncd.service
  <p> root@ubuntusyslog:~# systemctl status systemd-timesyncd.service  
<li> Установил nginx</li>
  <p> apt install nginx   
<li> Проверил работу nginx</li>
  <p> systemctl status nginx  
<li> Корректируем /etc/nginx/nginx.conf</li> 
  <p> error_log syslog:server=192.168.56.101:514,tag=nginx_error;
  <p> access_log syslog:server=192.168.56.101:514,tag=nginx_access,severity=info combined;   
<li> Проверяем конфигурацию nginx</li>
  <p> nginx -t   
<li>Рестарт Nginx</li>
  <p> root@ubuntunginx:~# systemctl restart nginx
  <p> root@ubuntunginx:~# systemctl status nginx
</ul>  

# 5. Получаем логи с Web на rsyslog
<ul>
<li> Читаем логи с машины Ubuntu_Nginx на сервере Ubuntu_Syslog</li> 
<p> Логи прикреплены в текстовом формате в выводе с терминала  
</ul>  
