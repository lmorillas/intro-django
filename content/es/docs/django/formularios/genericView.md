---
title: "Vistas Genéricas"
linkTitle: "GenericView"
date: 2021-10-21T10:36:54+02:00
weight: 20
description: >
  Formularios
tags: [Formularios]

docs: >
    * video csrf: https://www.youtube.com/watch?v=W9AvIUdhttA
---

{{% pageinfo %}}
Documentación: 
* https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Forms#generic_editing_views
{{% /pageinfo %}}

## Vistas Genéricas para edición
`CreateView`, `UpdateView`, `DeleteView`

## Gestión de Autores
### Vistas
```python
from django.views.generic.edit import CreateView, UpdateView, DeleteView
from django.urls import reverse_lazy

from catalog.models import Author

class AuthorCreate(CreateView):
    model = Author
    fields = ['first_name', 'last_name', 'date_of_birth', 'date_of_death']
    #initial = {'date_of_death': '11/06/2020'}

class AuthorUpdate(UpdateView):
    model = Author
    fields = '__all__' # Not recommended (potential security issue if more fields added)

class AuthorDelete(DeleteView):
    model = Author
    success_url = reverse_lazy('authors')
```

### Templates
`locallibrary/catalog/templates/catalog/author_form.html`
```html
{% extends "base.html" %}

{% block content %}
  <form action="" method="post">
    {% csrf_token %}  #  Atención!! Protección CSRF
    <table>
    {{ form.as_table }}
    </table>
    <input type="submit" value="Submit" />
  </form>
{% endblock %}
```

#### Confirm delete

`locallibrary/catalog/templates/catalog/author_confirm_delete.html`
```html
{% extends "base.html" %}

{% block content %}
  <p>Are you sure you want to delete this author?</p>
  <form action="" method="post">
    {% csrf_token %}
    <input type="submit" value="Confirm" />
  </form>
{% endblock %}
```

### URLs
```python
urlpatterns += [
    path('author/create/', views.AuthorCreate.as_view(), name='author-create'),
    path('author/<int:pk>/update/', views.AuthorUpdate.as_view(), name='author-update'),
    path('author/<int:pk>/delete/', views.AuthorDelete.as_view(), name='author-delete'),
]
```