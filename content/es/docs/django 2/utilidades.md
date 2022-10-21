---
title: "Utilidades"
date: 2021-10-21T10:36:54+02:00
weight: 20
description: >
  
tags: [dotenv]
---
## dotenv - uso de variables de entorno en desarrollo/despliegue

{{% pageinfo %}}
* https://pypi.org/project/python-dotenv/
{{% /pageinfo %}}

```bash
$ pip install python-dotenv
```

```bash
# .env

# DB
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
POSTGRES_DB=postgres

# app
SECRET_KEY=y6xg%o&^m4ggo5s!%mcdnu@v#neu#1v#2s9d&_q2(wixlxd((#
DATABASE_HOST=db
DATABASE_NAME=postgres
DATABASE_USER=postgres
DATABASE_PASSWORD=postgres

# for debugging and error reporting.
DEBUG=True
```


```python
# settings.py
import os
from dotenv import load_dotenv

load_dotenv([<path>])  # take environment variables from .env.

# SECURITY WARNING: keep the secret key used in production secret!
SECRET_KEY = str(os.getenv('SECRET_KEY'))

# Database 
if 'DATABASE_HOST' in os.environ:
    DATABASES = {
        'default': {
            'HOST': os.environ.get('DATABASE_HOST')
            # ENGINE read notes below
            'ENGINE': 'django.db.backends.postgresql_psycopg2',
            'NAME': os.environ.get('DATABASE_NAME'),
            'USER': os.environ.get('DATABASE_USER'),
            'PASSWORD': os.environ.get('DATABASE_PASSWORD'),
        }
    }
else :
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.sqlite3',
            'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
        }
    }

```

```yaml
# docker-compose.yml
version: '3.1'

services:
  db:
    image: postgres:13.0-alpine
    env_file: .env
    volumes:
      - ./postgres_data:/var/lib/postgresql/data/
    ports:
      - 5432:5432

  adminer:
    image: adminer
    ports:
      - 8080:8080
```