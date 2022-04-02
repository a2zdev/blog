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
  --volume /srv/gitlab/config:/etc/gitlab \
  --volume /srv/gitlab/logs:/var/log/gitlab \
  --volume /srv/gitlab/data:/var/opt/gitlab \
  gitlab/gitlab-ce:latest
```

- postgres
```shell
docker run -it 
  --name postgres 
  --restart always 
  -e POSTGRES_PASSWORD='abc123' 
  -e ALLOW_IP_RANGE=0.0.0.0/0 
  -v /home/postgres/data:/var/lib/postgresql 
  -p 5432:5432 
  -d postgres
```