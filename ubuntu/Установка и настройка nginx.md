# Установка и настройка nginx🔀
Оригинал: https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-20-04

## # Step 1 – Установка Nginx🚀
```
sudo apt update | apt upgrade -y
```
```
sudo apt install nginx
```
## # Step 2 – настройка Firewall
```
sudo ufw app list
```
#### Output:
```
Available applications:
  Nginx Full
  Nginx HTTP
  Nginx HTTPS
  OpenSSH
```
Как видно из выходных данных, для Nginx доступно три профиля:
- `Nginx Full` : этот профиль открывает как порт 80 (обычный незашифрованный веб-трафик), так и порт 443 (зашифрованный трафик TLS/SSL).
- `Nginx HTTP` : этот профиль открывает только порт 80 (обычный незашифрованный веб-трафик).
- `Nginx HTTPS` : этот профиль открывает только порт 443 (зашифрованный трафик TLS/SSL)

#### Включаем то, что нужно, командой:
```
sudo ufw allow 'Nginx HTTP'
```
#### Проверяем изменение:
```
sudo ufw status
```
#### Output:
```
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere                  
Nginx HTTP                 ALLOW       Anywhere                  
OpenSSH (v6)               ALLOW       Anywhere (v6)             
Nginx HTTP (v6)            ALLOW       Anywhere (v6)
```
Если ничего не появилось нужно включть UFW:
```
sudo ufw enable
```
```
sudo ufw status
```
### ⚠️Важно⚠️
#### У вас должнен быть открыт `22` (OpenSSH) порт, чтобы в дальгейшем можно было подключиться к серверу
#### Команда:
```
sudo ufw allow ssh
```
## # Step 3 — Проверка вашего веб-сервера
```
systemctl status nginx
```
#### Output:
```
● nginx.service - A high performance web server and a reverse proxy server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
   Active: active (running) since Fri 2020-04-20 16:08:19 UTC; 3 days ago
     Docs: man:nginx(8)
 Main PID: 2369 (nginx)
    Tasks: 2 (limit: 1153)
   Memory: 3.5M
   CGroup: /system.slice/nginx.service
           ├─2369 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
           └─2380 nginx: worker process
```