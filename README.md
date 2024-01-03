# docker-magento
# magento-docker
## Build the image
```
docker-compose build
```
## Check the images

```
docker images
```

## Run the container 
```
docker-compose up -d 
```

## List running container

```
docker-compose ps
```

## Your database credentials are mentioned in mysql.sh file. To get database user password, you can either enter the running container and check the /var/log/check.log file as
```
docker exec -ti mysql bash
```

```
cat /var/log/check.log
```

## Or, you can get it directly from host as:

```
docker exec -i mysql cat /var/log/check.log

```

# Now, your server setup is all ready, hit your domain name or IP to install Magento 2.
