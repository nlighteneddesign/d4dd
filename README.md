# php-local-docker-environment

## Preconfiguration for MacOS
1. ```gem install docker-sync```
2. ```brew install fswatch```
3. Update 'scr' variable in syncs section in docker-sync.yml file

## Configuration

1. ```cp .env.default .env```
2. Set the path to your projects folder in .env file
3. Configure ${PROJECT}.conf file in containers/nginx/sites folder
4. Add records to /etc/hosts file	
5. Example DB configuration in settings.php

```
$databases = array(
  'default' =>
  array(
    'default' =>
    array(
      //'database' => 'hid_brand_family',
      'database' => 'hidglobal',
      'username' => 'hidglobal',
      'password' => 'secret',
      'host' => 'mariadb',
      'port' => '3306',
      'driver' => 'mysql',
      'prefix' => '',
    ),
  ),
);
```


## Run instructions(Linux)
1. ```docker-compose build```
2. ```docker-compose up -d```

## Run instructions(Mac)
1. ```docker-sync-stack start```

Alternatively:

1. ```docker-sync start```
2. In a new shell run after you started docker-sync 
```docker-compose -f docker-compose.yml -f docker-compose-dev.yml up -d```


## FAQ
### How to I populate the DB, once all the containers are up and running?
- Get a recent .sql file of the full DB, and run the following from the directory where the .sql file exists.
```docker exec -i d7hid_mariadb_1 mysql -uroot -psecret hidglobal < hidglobal.db.sql```
### How do a I run a ```drush```command?
-  Run a ```docker exec``` which points at the ```d7hid_php-fpm_1``` container. I.e.,
```docker exec -i d7hid_php-fpm_1 drush cc all```