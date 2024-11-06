# MariaDB
  
Pull the latest version of the mariadb image from the registry on registry.do180.lab. 
  
Run a container in the background with the following parameters:

- Give the container the name of testsql
- Publish port 3306

And set the following environment variables:

- MYSQL_USER: micha
- MYSQL_PASSWORD: ex188
- MYSQL_ROOT_PASSWORD: SQLp4ss
- MYSQL_DATABASE: beer

Connect to your database as the root user and check for the existence of the beer database:

```bash
  echo "show databases;" |mysql -u micha -h <ip-address> -pex188
```

Run the command located in /sql/beer.sql to insert values into the database.

```bash
mysql -uroot -h <ip-address> -pSQLp4ss < ./003_beer.sql
```
