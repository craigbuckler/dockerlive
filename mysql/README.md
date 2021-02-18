# MySQL database

Launch latest MySQL:

```bash
docker run --rm --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=password mysql
```

Launch latest Adminer:

```bash
docker run --rm --name adminer -p 8080:8080 adminer
```

Log in using actual network IP rather than <localhost>.


## Improved

Use a persistent volume and attach to the same network:

```bash
docker network create mysqlnet
docker run --rm --name mysql --mount "src=mysqldata,target=/var/lib/mysql" -p 3306:3306 --net mysqlnet -e MYSQL_ROOT_PASSWORD=password mysql
docker run --rm --name adminer -p 8080:8080 --net mysqlnet adminer
```

## Docker Compose

Easier option:

```bash
docker-compose up
```
