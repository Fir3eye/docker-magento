# docker-magento
## Build the image
```
mkdir -p magento services/nginx_log services/phpfpm_log services/sock_data services/mysql_data services/mysql_log services/redis_data services/es_data services/es_log
```
## Build and start container

```
docker-compose build && docker-compose up -d
```

## Create new Composer Project
```
docker-compose exec phpfpm composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition .
```

## Install Magento

```
docker-compose exec -T phpfpm bin/magento setup:install --base-url=http://magento-dev.lh/ --db-host=db --db-name=magento --db-user=magento --db-password=magento --backend-frontname=admin  --admin-firstname=admin --admin-lastname=admin --admin-email=yourname@domain.com --admin-user=admin --admin-password=admin1234 --language=hu_HU --currency=HUF --timezone=Europe/Budapest --use-rewrites=1 --search-engine=elasticsearch7 --elasticsearch-host=elasticsearch --elasticsearch-port=9200 --elasticsearch-index-prefix=magento
```

## Your database credentials are mentioned in mysql.sh file. To get database user password, you can either enter the running container and check the /var/log/check.log file as


```

# Now, your server setup is all ready, hit your domain name or IP to install Magento 2.
