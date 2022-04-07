---
layout: default
title: docker shell
---

### docker shell

- gitlib
```shell
sudo docker run --detach \
  --publish 443:443 --publish 80:80 \
  --name gitlab \
  --restart always \
  --volume /home/a/container/data/gitlab/config:/etc/gitlab \
  --volume /home/a/container/data/gitlab/logs:/var/log/gitlab \
  --volume /home/a/container/data/gitlab/data:/var/opt/gitlab \
  gitlab/gitlab-ce:latest
```

- postgres
```shell
docker run -it \
  --name postgres \
  --restart always \
  -e POSTGRES_PASSWORD='abc123' \ 
  -e ALLOW_IP_RANGE=0.0.0.0/0 \
  -v /home/a/container/data/postgres/postgresql:/var/lib/postgresql \ 
  -p 5432:5432 \
  -d postgres
```

- mysql8
```shell
docker run --name mysql8 \
-p 3306:3306 \
-e MYSQL_ROOT_PASSWORD=123456 \
-v /home/a/container/data/mysql:/var/lib/mysql \
-v /home/a/container/data/mysql:/etc/mysql/conf.d \
--restart=always \
-itd mysql:8 \
--character-set-server=utf8mb4 
--collation-server=utf8mb4_unicode_ci
```

- nacos
```shell
docker run -itd \
--name nacos \
--restart=always \
-p 8848:8848 \
-e MODE=standalone \
-e SPRING_DATASOURCE_PLATFORM=mysql \
-e MYSQL_SERVICE_HOST=192.168.6.11 \
-e MYSQL_SERVICE_PORT=3306 \
-e MYSQL_SERVICE_DB_NAME=nacos_config \
-e MYSQL_SERVICE_USER=root \
-e MYSQL_SERVICE_PASSWORD=123456 \
-e MYSQL_SERVICE_DB_PARAM="allowPublicKeyRetrieval=true&useSSL=false&useUnicode=true&characterEncoding=UTF-8&serverTimezone=UTC&characterEncoding=utf8&connectTimeout=1000&socketTimeout=3000&autoReconnect=true&useSSL=false" \
-v /home/a/container/data/nacos/logs:/home/nacos/logs \
nacos/nacos-server
```