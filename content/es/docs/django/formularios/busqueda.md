---
title: "Búsqueda"
date: 2021-10-21T10:36:54+02:00
weight: 5
description: >
  Formularios
tags: [Formularios]

---

{{% pageinfo %}}
Documentación: 
{{% /pageinfo %}}

## Fomulario de búsqueda

Usamos el formulario de búsqueda de la aplicación de libros en navbar:

```html
<form class="form-inline mt-2 mt-md-0" 
    action="{% url 'search_results' %}"
    method="get">
    <input name="q" class="form-control mr-sm-2" type="text" 
        placeholder="Search" aria-label="Search">
</form>
```

Vista de búsqueda:
```python
class SearchResultsListView(ListView):
    model = Book
    context_object_name = 'book_list'
    template_name = 'books/search_results.html'
    def get_queryset(self): # new
        query = self.request.GET.get('q')
        return Book.objects.filter(title__icontains=query)
```

**Configurar urls.py**

Action del formulario ```search_results```

