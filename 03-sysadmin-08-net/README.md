# Домашнее задание к занятию "3.8. Компьютерные сети, лекция 3"

1. Подключитесь к публичному маршрутизатору в интернет. Найдите маршрут к вашему публичному IP
```
telnet route-views.routeviews.org
Username: rviews
show ip route x.x.x.x/32
show bgp x.x.x.x/32
```
_show bgp 217.197.201.41_
https://docs.google.com/document/d/1i6S2TYob8R35xfSDf1Qgl58XSpqXBP7EDTJyRLrHskQ/edit?usp=sharing

2. Создайте dummy0 интерфейс в Ubuntu. Добавьте несколько статических маршрутов. Проверьте таблицу маршрутизации.
![image](https://user-images.githubusercontent.com/48878229/136662242-15bfb252-0912-4ca3-8063-8d7da61dc5ab.png)

Создать адаптеры:  
![image](https://user-images.githubusercontent.com/48878229/136260074-a3ee0e8c-86ac-48f8-adf5-bdf9ae694a31.png)  
Присвоить адаптерам адреса:  
sudo ip addr add 192.168.1.1/24 dev dummy0  
sudo ip addr add 192.168.1.2/24 dev dummy1  

Включить адаптеры:  
sudo ifconfig dummy0 up  
sudo ifconfig dummy1 up  

Добавить маршруты:  
sudo route add -net 192.168.3.0 netmask 255.255.255.0 dev dummy0  
sudo route add -host 192.168.2.100 dev dummy1  
![image](https://user-images.githubusercontent.com/48878229/136665470-5905156f-e988-48e9-b479-dfb866bcb326.png)  


3. Проверьте открытые TCP порты в Ubuntu, какие протоколы и приложения используют эти порты? Приведите несколько примеров.

sudo netstat -tulpn
![image](https://user-images.githubusercontent.com/48878229/136665536-9519df20-0fdb-42dd-bd86-fe9e5d27a03e.png)


4. Проверьте используемые UDP сокеты в Ubuntu, какие протоколы и приложения используют эти порты?

ss -u -a
![image](https://user-images.githubusercontent.com/48878229/136665779-a37c87d9-6cc2-4c58-a9ee-7c1c3700db18.png)


5. Используя diagrams.net, создайте L3 диаграмму вашей домашней сети или любой другой сети, с которой вы работали. 

![diagram](https://user-images.githubusercontent.com/48878229/136668302-23a2ee49-824e-4912-bdbb-d4868af85c45.jpg)


 ---
## Задание для самостоятельной отработки (необязательно к выполнению)

6*. Установите Nginx, настройте в режиме балансировщика TCP или UDP.

<!--
   Пример конфига tcp-балансировщика:

   upstream backend {
   server 10.0.0.100:44433;
   server 10.0.0.200:44433;
}

server {
   listen 80;
   location / {
       proxy_read_timeout 1800;
       proxy_connect_timeout 1800;
       proxy_send_timeout 1800;
       send_timeout 1800;
       proxy_set_header        Accept-Encoding   "";
       proxy_set_header        X-Forwarded-By    $server_addr:$server_port;
       proxy_set_header        X-Forwarded-For   $remote_addr;
       proxy_set_header        X-Forwarded-Proto $scheme;
       proxy_set_header Host $host;
       proxy_set_header X-Real-IP $remote_addr;
       proxy_pass http://backend;
   }
 -->
7*. Установите bird2, настройте динамический протокол маршрутизации RIP.

8*. Установите Netbox, создайте несколько IP префиксов, используя curl проверьте работу API.

 ---

### Как оформить ДЗ?

Домашнее задание выполните в файле readme.md в github репозитории. В личном кабинете отправьте на проверку ссылку на .md-файл в вашем репозитории.

Также вы можете выполнить задание в [Google Docs](https://docs.google.com/document/u/0/?tgif=d) и отправить в личном кабинете на проверку ссылку на ваш документ.
Название файла Google Docs должно содержать номер лекции и фамилию студента. Пример названия: "1.1. Введение в DevOps — Сусанна Алиева"
Перед тем как выслать ссылку, убедитесь, что ее содержимое не является приватным (открыто на комментирование всем, у кого есть ссылка). 
Если необходимо прикрепить дополнительные ссылки, просто добавьте их в свой Google Docs.

Любые вопросы по решению задач задавайте в чате Slack.

---
