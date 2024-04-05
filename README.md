# Docker Umgebung für Contao 4.9 , 4.13 , 5

- nginx
- mysql
- php-fpm73 
- php-fpm74
- php-fpm81
- php-fpm82 ( currently remmoved from docker-compose because not needed)
 

> Über die include config z.B include fpm73.conf; wird die jeweilige php-fpm instanz genutzt , somit kann gezielt die PHP Version pro Projekt ausgewählt werden auswählen. EASY TO UPGRADE IN FUTURE :D ! No Alpine Distroless !



`default.conf` (Definition Server Blöcke)
```
server {
    index index.php index.html;
    server_name contao.loc;
    root /var/www/contao.loc/web;

    include fpm82.conf;
}

server {
    listen 443 ssl;
    index index.php index.html;
    server_name tmv.loc;
    root /var/www/tmv.loc/web;

    ssl_certificate     /etc/nginx/certs/tmv.loc+2.pem;
    ssl_certificate_key /etc/nginx/certs/tmv.loc+2-key.pem;

    include fpm73.conf;
}

server {
    index index.php index.html;
    server_name gardels.loc;
    root /var/www/gardels.loc/web;

    include fpm74.conf;
}
```

