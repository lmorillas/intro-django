---
title: "Admin"
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
# Define the admin class en admin.py
class BookAdmin(admin.ModelAdmin):
    list_display = ('title', 'author', 'display_genre')

# Register the admin class with the associated model
admin.site.register(Author, AuthorAdmin)
```

```python
# añadir al modelo Book en models.py
    def display_genre(self):
        """Create a string for the Genre. This is required to display genre in Admin."""
        return ', '.join(genre.name for genre in self.genre.all()[:3])

    display_genre.short_description = 'Genre'
```

### list filters

```python
class BookInstanceAdmin(admin.ModelAdmin):
    list_filter = ('status', 'due_back')

    fieldsets = (
        (None, {
            'fields': ('book', 'imprint', 'id')
        }),
        ('Availability', {
            'fields': ('status', 'due_back')
        }),
    )
```
### Inlines

```python
class BooksInstanceInline(admin.TabularInline):
    model = BookInstance

@admin.register(Book)
class BookAdmin(admin.ModelAdmin):
    list_display = ('title', 'author', 'display_genre')

    inlines = [BooksInstanceInline]
```


### funciones especiales para el admin

```python
from django.contrib import admin
from django.db import models
from django.utils.html import format_html

class Bookinstance(models.Model):
    ...

    @admin.display
    def estado(self):
        return format_html(
            '<i class="bi bi-book-fill {}"></i>', 
            'text-success' if self.status == 'a' else 'text-danger'
        )
```