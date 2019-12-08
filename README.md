## Project information

@@TODO

## Wercker check code

[![wercker status](https://app.wercker.com/status/42b1ea647417f1e02844d7363ea34d23/m/ "wercker status")](https://app.wercker.com/project/byKey/42b1ea647417f1e02844d7363ea34d23)

### Setup environment to development

First you need install docker and docker composer, after that just running the command below:

```
cp env.example .env
docker-compose up -d 
```

Then waiting a moment to download on image, but frm api need 
library php so that you also need running command below

``` 
docker-compose exec php bash
cd /app/ && composer install
```

### Migrate database

We use flyway tool to migration database so that you can take look docs at [https://flywaydb.org/](https://flywaydb.org/), to helper easy use flyway we have build a image docker you can see [here](https://github.com/gsviec/flyway-docker)

### Existing database setup

You only runing the line below the first time:

```
docker-compose exec flyway bash
flyway baseline  -configFiles=sql/config_dev.conf

```
Done. Congratulations ! You are now ready to migrate. When you execute

```
flyway -configFiles=sql/config_dev.conf migrate

```

the empty databases will be migrated to the state of production and the others will be left as is. As soon as you add a new migration, it will be applied identically to all databases.

### Use PHP MyAdmin tool

Then go to url http://localhost:9090 to import database, to get database
file go to directory [database](./databases), when you finish just open again http://localhost


### Fix and check code PSR2

```
vendor/bin/phpcs app --standard=PSR2 --ignore=app/migrations
vendor/bin/phpcbf app --standard=PSR2 --ignore=app/migrations
```
