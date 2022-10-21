---
title: "Sitio administrativo"
date: 2021-10-21T10:36:54+02:00
weight: 9
description: >
  Configuración del admin
tags: 
---

{{% pageinfo %}}
Documentación: 
* https://developer.mozilla.org/es/docs/Learn/Server-side/Django/Admin_site

{{% /pageinfo %}}


## Registrar modelos

**archivo admin.py**

```python
from .models import Author, Genre, Book, BookInstance

admin.site.register(Book)
admin.site.register(Author)
admin.site.register(Genre)
admin.site.register(BookInstance)
```

## Crear Administrador

## Configurar
### Clases ModelAdmin

```python
# Define the admin class
class AuthorAdmin(admin.ModelAdmin):
    pass

# Register the admin class with the associated model
admin.site.register(Author, AuthorAdmin)
```
### list_display

### list_filter

### fields y fieldsets

### Edición
