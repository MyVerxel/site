---
title: "docker"
date: 1401-04-06T18:29:27
draft: false
---

تمام دستورات با sudo اجرا میشود

### ایجاد یک داکر

```python
$ cat Dockerfile
FROM ubuntu:latest
RUN apt-get update -y
RUN apt-get install curl cron -y
CMD [ '/bin/bash' ]
```

ساختن داکر

```python
docker build -t NAME:TAG .
docker build -t mybash:v1 .
```

### اجرا

```python
docker run --rm -it mybash:v1 [/bin/bash]
```

### Expose Port

```python
docker run --rm -it -p 8080:80 mybash:v1 [ CMD ]
```

### Map Volume

```python
docker run --rm -it -p 8080:80 -v /home/app:/home/a mybash:v1 [ CMD ]
```

### LOGIN

```python
docker login --username [USERNAME]
docker login ghcr.io
docker login registry.gitlab.com
```

### BUILD and PUSH remote registry
```python
docker build -t registry.gitlab.com/[USERNAME]/[REPOSITORY_NAMEs]:[TAG] .
docker push registry.gitlab.com/[USERNAME]/[REPOSITORY_NAMEs]:[TAG]
```

### MAINTENANCE

```python
docker images
docker rmi [IMAGE ID or IMAGE NAME:TAG]

docker ps -a
docker rm [ID]
```

