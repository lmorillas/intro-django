---
title: "Vistas genéricas: listados y detalle"
date: 2021-10-21T10:36:54+02:00
weight: 15
description: >
  Vistas genéricas son una forma de crear vistas que se pueden reutilizar en
  diferentes proyectos.
tags: [Vistas genéricas]
---

{{% pageinfo %}}
Documentación: 
* https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Generic_views
* https://docs.djangoproject.com/en/4.1/topics/class-based-views/generic-display/
{{% /pageinfo %}}


## URL mapping

```python
urlpatterns = [
    path('', views.index, name='index'),
    path('books/', views.BookListView.as_view(), name='books'),
]
```

## Redirección incial
**urls.py del proyecto**
```python
from django.views.generic import RedirectView
from django.urls import include, path
from django.contrib import admin
from django.conf.urls.static import static


urlpatterns = [
    path('admin/', admin.site.urls),
    path('catalog/', include('catalog.urls')),
    path('/', RedirectView.as_view(url='/catalog/', permanent=True)),
] + static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)

# Este static es solo para DEBUG = True
```

## generic.ListView

```python
from django.views import generic

class BookListView(generic.ListView):
    model = Book
```

* La vista genérica consultará a la base de datos para obtener todos los registros del modelo especificado (Book)
* renderizará una plantilla ubicada en **/biblioteca/catalogo/templates/catalogo/book_list.html**
* Dentro de la plantilla puedes acceder a la lista de libros mediante la variable de plantilla llamada **object_list** O **book_list**
* Paginación: Añade un **page_obj** al contexto https://docs.djangoproject.com/en/4.1/topics/pagination/ 

Estos datos se pueden sobreescribir: 
* context_object_name
* queryset
* template_name

