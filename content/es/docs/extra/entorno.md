---
title: "Variables de entorno"
date: 2021-10-21T10:29:17+02:00
linkTitle: "Entorno"
weight: 20
description: >
  
docs: 

draft: false

---

{{% pageinfo %}}
* https://saurabh-kumar.com/python-dotenv/
* https://github.com/henriquebastos/python-decouple/
* https://django-environ.readthedocs.io/en/latest/  
{{% /pageinfo %}}

* Instalar
`pip install python-dotenv`

* Crear fichero `.env` en la raíz del proyecto y añadirlo a `.gitignore` 

```sh
SECRET_KEY = 'YOUR SECRET KEY'

GITHUB_KEY = 'YOUR GITHUB KEY'
GITHUB_SECRET = 'YOUR GITHUB SECRET KEY'

GOOGLE_KEY = 'YOUR GOOGLE KEY'
GOOGLE_SECRET = 'YOUR GOOGLE SECRET KEY'
```
* Uso

```python
import os
from dotenv import load_dotenv

load_dotenv()  # loads the configs from .env

# SECURITY WARNING: keep the secret key used in production secret!
SECRET_KEY = str(os.getenv('SECRET_KEY'))

# social auth configs for github
SOCIAL_AUTH_GITHUB_KEY = str(os.getenv('GITHUB_KEY'))
SOCIAL_AUTH_GITHUB_SECRET = str(os.getenv('GITHUB_SECRET'))

# social auth configs for google
SOCIAL_AUTH_GOOGLE_OAUTH2_KEY = str(os.getenv('GOOGLE_KEY'))
SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET = str(os.getenv('GOOGLE_SECRET'))
```