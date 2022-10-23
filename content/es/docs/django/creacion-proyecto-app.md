---
title: "Creación de un proyecto y una app"
date: 2021-10-21T10:36:54+02:00
weight: 6
description: >
  Creación de un proyecto y una app
tags: [django]
---

{{% pageinfo %}}
Documentación
* https://developer.mozilla.org/es/docs/Learn/Server-side/Django/Tutorial_local_library_website
* https://docs.djangoproject.com/es/4.1/intro/tutorial01/
* Objetivo: **locallibrary** https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Tutorial_local_library_website
{{% /pageinfo %}}

> https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/skeleton_website

## Creación de proyecto

```bash
$ django-admin startproject locallibrary
```

```
locallibrary/
    manage.py
    locallibrary/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
```

```bash
$ python3 manage.py runserver
```

Parar con `Ctrl+C`

## Creación aplicación
```bash
$ python3 manage.py startapp catalog
```
** Estructura**
```bash
locallibrary/
    manage.py
    locallibrary/
    catalog/
        admin.py
        apps.py
        models.py
        tests.py
        views.py
        __init__.py
        migrations/
```


## Modelo Vista Template
Diseño común: patrón Modelo Vista Controlador (**MVC**)
Django usa: **MVT**: Permite que las templates puedan desarrollarse en cualquier lenguaje:
* Modelos y Vistas se escriben en **Python**
* Templates se escriben en **html**
  
## Registrar app

https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/skeleton_website#registering_the_catalog_application

## Especificar base de datos

https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/skeleton_website#specifying_the_database

## Configuración local

https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/skeleton_website#other_project_settings

##  URL mapper

https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/skeleton_website#hooking_up_the_url_mapper

## Testing 

https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/skeleton_website#testing_the_website_framework

## Running 

https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/skeleton_website#running_the_website