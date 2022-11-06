---
title: "Página inicial"
date: 2021-10-21T10:36:54+02:00
weight: 11
description: >
  Urls, vistas, plantillas
tags: [view, template, urls]
---

{{% pageinfo %}}
Documentación: 
* https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Home_page
* https://docs.djangoproject.com/en/3.2/intro/tutorial03/
{{% /pageinfo %}}


## Visión general

![Proceso de una petición](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Home_page/basic-django.png)

## Definiendo URLs

**urls.py** principal:

```python
# Redirección incial
from django.views.generic import RedirectView
from django.urls import include, path
from django.contrib import admin

urlpatterns = [
    path('admin/', admin.site.urls),
    path('catalog/', include('catalog.urls')),
    path('/', RedirectView.as_view(url='/catalog/', permanent=True)),
] + static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```

**Urls de nuestra app**
* catalog/ — La página home/index.
* catalog/books/ — La lista de todos los libros.
* catalog/authors/ — La lista de todos los autores.
* catalog/book/<id> — La vista detallada para el libro específico con un campo de clave primaria de <id> (el valor por defecto). Así por ejemplo, /catalog/book/3, para el tercer libro añadido.
* catalog/author/<id> — La vista detallada para el autor específico con un campo de clave primaria llamada <id>. Así por ejemplo, /catalog/author/11, para el 11vo autor añadido.

## Crear vista para pagina inicial del sitio 

```python

def index(request):

    ...
```

## Reproduce este modelo

![Locallibrary](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Home_page/index_page_ok.png)

