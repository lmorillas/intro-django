---
title: "Debug toolbar"
date: 2021-10-21T10:36:54+02:00
weight: 14
description: >
  
tags: 
---

{{% pageinfo %}}
Documentación: 
* https://django-debug-toolbar.readthedocs.io/en/latest/
{{% /pageinfo %}}

## Instalación

```bash
pip install django-debug-toolbar
```

## Prerrequisitos

```python
# settings.py
INSTALLED_APPS = [
    "django.contrib.staticfiles",

]

STATIC_URL = "static/"

TEMPLATES = [
    {
        "BACKEND": "django.template.backends.django.DjangoTemplates",
        "APP_DIRS": True,
        # ...
    }
]
```

## Instalar la app

```python
INSTALLED_APPS = [
    # ...
    "debug_toolbar",
    # ...
]
```

## Añadir las urls

```python
from django.urls import include, path

urlpatterns = [
    # ...
    path('__debug__/', include('debug_toolbar.urls')),
]
```
## Añadir el Middleware

```python
MIDDLEWARE = [
    # ...
    "debug_toolbar.middleware.DebugToolbarMiddleware",
    # ...
]
```
## Configurar internal ips

```python
INTERNAL_IPS = [
    # ...
    "127.0.0.1",
    # ...
]
```