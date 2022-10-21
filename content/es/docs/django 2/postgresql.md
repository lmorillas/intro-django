---
title: "Postgresql"
date: 2021-10-21T10:36:54+02:00
weight: 18
description: >
  
tags: []
---

{{% pageinfo %}}
* https://docs.djangoproject.com/en/4.0/ref/databases/
* https://docs.djangoproject.com/en/4.0/ref/settings/#std:setting-DATABASES
* https://tutorial-extensions.djangogirls.org/es/optional_postgresql_installation
* https://www.section.io/engineering-education/django-app-using-postgresql-database/
* https://djangocentral.com/using-postgresql-with-django/
 
{{% /pageinfo %}}



## Instalación de postgresql en linux 
Buscar en la información

## Instalación con docker
* https://docs.docker.com/engine/install/ubuntu/
* https://docs.docker.com/engine/install/linux-postinstall/
* https://docs.docker.com/samples/django/

```bash
$ curl -fsSL https://get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh

$ sudo groupadd docker
$ sudo usermod -aG docker $USER
$ newgrp docker
```

```yaml
# Use postgres/example user/password credentials
version: '3.1'

services:

  db:
    image: postgres:13.0-alpine
    restart: never
    environment:
      - POSTGRES_USER=hello_django
      - POSTGRES_PASSWORD=hello_django
      - POSTGRES_DB=hello_django_dev
    volumes:
      - ./postgres_data:/var/lib/postgresql/data/
    ports:
      - 5432:5432

  adminer:
    image: adminer
    restart: never
    ports:
      - 8080:8080
```

```bash
$ docker-compose up -d --build
``` 