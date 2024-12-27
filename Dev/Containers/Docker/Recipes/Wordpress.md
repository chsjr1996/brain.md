```yml
services:
  db:
    image: mysql:5.7
    container_name: project-mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: project
      MYSQL_DATABASE: project
      MYSQL_USER: project
      MYSQL_PASSWORD: project
    volumes:
      - ./.docker/database:/var/lib/mysql:z
    ports:
      - 3306:3306

  wordpress:
    image: wordpress:5.6
    container_name: project-wordpress
    restart: always
    depends_on:
      - db
    volumes:
      - ./wp-content:/var/www/html/wp-content:z
      - ./wp-config.php:/var/www/html/wp-config.php:z
      - ./.htaccess:/var/www/html/.htaccess:z
      - ./.docker/uploads.ini:/usr/local/etc/php/conf.d/uploads.ini:z
    ports:
      - 8080:80

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: project-phpmyadmin
    restart: always
    depends_on:
      - db
    environment:
      PMA_HOST: db
      MYSQL_ROOT_PASSWORT: project
      UPLOAD_LIMIT: 2048M
    ports:
      - 3333:80
```