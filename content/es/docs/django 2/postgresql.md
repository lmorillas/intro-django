---
title: "Postgresql"
date: 2021-10-21T10:36:54+02:00
weight: 18
description: >
  
tags: []
---

{{% pageinfo %}}
* https://github.com/lmorillas/vagrant_docker/tree/postgres
* https://docs.djangoproject.com/en/4.1/ref/settings/#std-setting-DATABASES
* https://docs.djangoproject.com/en/4.1/ref/databases/#postgresql-notes
{{% /pageinfo %}}


## Revisión de instalación de postgres

Fíjate en el repositorio


## Uso en Django

> Si vas a migrar la bbdd haz antes un dumpdata

* Instala el driver de pg: `psycopg2-binary`

`$ pip install psycopg2-binary`

* Configura la BBDD en el settings:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'mydatabase',
        'USER': 'mydatabaseuser',
        'PASSWORD': 'mypassword',
        'HOST': '127.0.0.1',
        'PORT': '5432',
    }
}
```
* Comprueba que funciona
* Vuelve a cargar los datos con `loaddata`

* Ahora vamos a ocultar las contraseñas: [Uso de variables de entorno](/intro-django/docs/extra/entorno/)