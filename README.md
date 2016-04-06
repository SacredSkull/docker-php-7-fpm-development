Based on the official PHP 7 FPM image, this new flavour comes with:
- Extensions: xdebug, pdo, pdo_mysql, zip, blackfire
- Git & unzip
- Composer (in path)

Overwritten `WORKDIR`- now at `/var/www` rather than the html subdirectory.

---

Example service/docker-compose.yml - using the current directory as mountpoint
```
  php:
    image: sacredskull/php-7-fpm-development
    volumes:
      - .:/var/www
      - ./conf/php/php.ini:/usr/local/etc/php/conf.d/php.ini
    ports:
      - "9000:9000"
```
---

To connect to a **blackfire agent**, just add the following service (replacing with your own values):
```
  blackfire:
    image: blackfire/blackfire
    environment:
      - BLACKFIRE_CLIENT_ID=yourclientID
      - BLACKFIRE_CLIENT_TOKEN=yourclienttoken
      - BLACKFIRE_SERVER_ID=yourserverID
      - BLACKFIRE_SERVER_TOKEN=yourservertoken
```
