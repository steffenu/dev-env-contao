
WICHTIGE EXTENSION welche dem php-fpm
Container hinzugefügt werden müssen !
Ohne pdo_mysql ist keine datenbankverbindung möglich z.B
 !

Glücklicherweise hat das php:fpm docker image ansonsten alle Extensions mit dabei ! 

```
RUN chmod +x /usr/local/bin/install-php-extensions && \
    install-php-extensions intl gd pdo_mysql  
```


usr/local/etc/php-fpm.d/www.conf


The directory "/var/www/html/contao.loc/var/cache/prod/http_cache" is not writable.

FIX : add Z to volume to make it writeable
https://stackoverflow.com/a/34537509

Another solution is to create a user 
    - ./volumes/application:/var/www/html:Z

Probleme mit Zugriffsrechten
(sicherstellen das docker bzw der user www-data den application order lesen kann)

- user
- gruppe

sudo chown -R $USER ./application/

TODO : ggf noch anpassung nötig im bezug auf zugriffsrechte
# Contao 4.9 app.php problem

Für Backwards Compability existiert  
eine  app.php die dann zu index.php weiterleitet
dies müssen wir in nginx über eine rewrite rule
konfigurieren

> rewrite regex URL [flag];
> try_files file ... uri;
> index file ...;

Links  recommened :
https://www.nginx.com/blog/creating-nginx-rewrite-rules/

```
# rewrite regex URL [flag];
rewrite ^/app\.php/?(.*)$ /$1 permanent;

location / {
    #index file ...;
    index app.php;

    # try_files file ... uri;
    try_files $uri @rewriteapp;
}

location @rewriteapp {
    # rewrite regex URL [flag];
    rewrite ^(.*)$ /app.php/$1 last;
}
```

# Learning nginx

- beginners guide
> https://nginx.org/en/docs/beginners_guide.html

- Reihenfolge requestverarbeitung (nachschauen bei - A simple PHP site configuration)
> http://nginx.org/en/docs/http/request_processing.html

- docker php fpm example
> https://github.com/IshtarStar/docker-compose-nginx-phpfpm

- fastcgi parameters
>https://nginx.org/en/docs/http/ngx_http_fastcgi_module.html#fastcgi_pass

- fastcgi example (most basic)
> https://www.nginx.com/resources/wiki/start/topics/examples/phpfcgi/

- location block & rewrite rules
> https://www.nginx.com/blog/creating-nginx-rewrite-rules/

- nginx regex explained
> https://stackoverflow.com/a/59846239

- [root](https://nginx.org/en/docs/http/ngx_http_core_module.html#root)

- [location](https://nginx.org/en/docs/http/ngx_http_core_module.html#location)

-[index](http://nginx.org/en/docs/http/ngx_http_index_module.html)

- [try_files](https://nginx.org/en/docs/http/ngx_http_core_module.html#try_files)

- socket vs tcp fastcgi ( you can use both)
> https://stackoverflow.com/a/49818093

- configure socket instead of tcp (optional - makes sense if phpfpm and nginx run in the same container .. which this repo doesnt do . it seperates php-fpm and nginx to its own containers)
> https://stackoverflow.com/a/46666920

> PHP-FPM (FastCGI Process Manager) is an alternative to FastCGI implementation of PHP with some additional features useful for sites with high traffic. It is the preferred method of processing PHP pages with NGINX


