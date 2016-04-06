## Image description

Based on the official PHP 7 FPM image, this new flavour comes with:
- Extensions: xdebug, pdo, pdo_mysql, zip, blackfire
- Git & unzip
- Composer (in path)

Overwritten `WORKDIR`- now at `/var/www` rather than the html subdirectory.

---
### Example service/docker-compose.yml
Using the current directory as mountpoint
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
### Using Blackfire
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
---
### Remote interpreter in PHPSTORM
To use this as an interpreter you have a few options:
- Craft a script file that executes the php container. If you're using compose.yml, make sure you force the `container_name` - then just run `docker exec -it your_container_name php`. This is easier said than done on Windows because of pathing issues.
- Use an SSH container to gain access

#### SSH container
Replace the container variable with whatever you named your PHP container. Unfortunately, this doesn't currently work with Windows. See [https://github.com/jeroenpeeters/docker-ssh/issues/7#issuecomment-205892305](for more details.) Eventually, however, it should provide a cross-platform and easy to implement remote interpreter.

Your docker socket has to be mounted - this is a security risk - don't expose this publically.
```
  ssh:
    image: jeroenpeeters/docker-ssh
    ports:
      - "2222:22"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      - CONTAINER=your_php_container_name
      - AUTH_MECHANISM=noAuth
```
