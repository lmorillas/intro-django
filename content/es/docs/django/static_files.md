---
title: "Archivos estáticos"
date: 2021-10-21T10:36:54+02:00
weight: 34
description: >
  Subida de archivos
tags: [Estáticos]
---

{{% pageinfo %}}
Documentación:
* https://docs.djangoproject.com/en/3.2/howto/static-files/ 
{{% /pageinfo %}}

## Configurar
Incluir **django.contrib.staticfiles** en  **INSTALLED_APPS**.

En el archivo **settings.py**, incluir la siguiente línea:

```STATIC_URL = '/static/'```

En las plantillas:

```html
{% load static %}
<img src="{% static 'my_app/example.jpg' %}" alt="My image">
```

Los archivos van en una carptea **static** en las apps

## Servir los archivos estáticos

### Desarrollo
```python
from django.conf import settings
from django.contrib.staticfiles.urls import staticfiles_urlpatterns

if settings.DEBUG:
    # Serve static and media files from development server
    urlpatterns += staticfiles_urlpatterns()

```

### Despliegue
* https://docs.djangoproject.com/en/3.2/howto/static-files/deployment/
  