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

- libreoffice
```shell
FROM centos:7
ADD LibreOffice_7.5.4_Linux_x86-64_rpm.tar.gz /home/office

# install LibreOffice
RUN yum localinstall /home/office/LibreOffice_7.5.4.2_Linux_x86-64_rpm/RPMS/* -y  \
        && rm -rf /home/office

# config ENV
ENV PATH /opt/libreoffice7.5/program:$PATH

# install dependency
RUN yum install cairo -y \
        && yum install cups-libs -y \
        && yum install libSM -y


# install font 
RUN yum groupinstall "Fonts" -y \
        && yum clean all

# ADD jdk
ADD jdk-8u202-linux-x64.tar.gz /usr/local/

# config ENV
ENV PATH /usr/local/jdk1.8.0_202/bin:$PATH

# ADD App
ADD *.jar /app/app.jar
#ADD file/* /app/file/

# expose port
EXPOSE 8080
WORKDIR /app

# run app
CMD ["java","-jar","app.jar"]
#CMD ["bash"]
```
- libreoffice
```
docker run --name libreoffice -v /home/a/dockerFile/file:/app/file --net=host -itd libreoffice
```
