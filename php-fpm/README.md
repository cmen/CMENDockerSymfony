1 : Create Docker images
-----------------------------

In Docker directory, run the commands : 
```bash
docker build -t cmeneses/apache:2.4 ./apache2.4/
docker build -t cmeneses/php-fpm:7.0 ./php-fpm7.0/
docker build -t cmeneses/data_application ./data_application/
docker build -t cmeneses/data_mysql ./data_mysql/
docker build -t cmeneses/mysql:5.7 ./mysql5.7/
docker build -t cmeneses/phpmyadmin:4.6 ./phpmyadmin4.6/
```

2 : Modify docker-compose.yml
-----------------------------
You must modify volumes for `test_application` and `test_data` containers with your own directory, for example :
```yaml
test_application:
    image: cmeneses/data_application
    volumes:
        - /home/Test-Docker-Sf/Symfony:/var/www/html
test_data:
    image: cmeneses/data_mysql
    volumes:
        - /home/Test-Docker-Sf/Data:/var/lib/mysql        
```

3 : Run the application
-----------------------------

In Symfony directory, run the command :
```bash
$ docker-compose up -d
```

4 : Test the application
-----------------------------

Add virtual host in file `/etc/hosts`. Open it and add this line :
```bash
127.0.0.1     app.local
```

Symfony application : [app.local:60000/app_dev.php](http://app.local:60000/app_dev.php)

PHPMyAdmin : [app.local:60002](http://app.local:60002)

MySQL : [app.local:60001](http://app.local:60001)

5 : Stop the application
-----------------------------
In Symfony directory, run the command :
```bash
$ docker-compose stop
```