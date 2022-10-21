---
title: "Formularios"
date: 2021-10-21T10:36:54+02:00
weight: 17
description: >
  Formularios
tags: [Formularios]
---

{{% pageinfo %}}
Documentación: 
* https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Forms
* https://developer.mozilla.org/en-US/docs/Learn/Forms
* https://docs.djangoproject.com/en/3.2/topics/forms/
{{% /pageinfo %}}

## Qué son los formularios
Conjutos de etiquetas entre elementos ```<form>``` y ```</form>``` que permiten a los usuarios enviar datos a un servidor.

## Cómo se procesan en django
![formularios en django](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Forms/form_handling_-_standard.png)


## Fomulario de búsqueda

En template:
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

## Objetos forms.Form
Se declaran en forms.py

```python
import datetime

from django import forms

from django.core.exceptions import ValidationError
from django.utils.translation import ugettext_lazy as _

class RenewBookForm(forms.Form):
    renewal_date = forms.DateField(help_text="Enter a date between now and 4 weeks (default 3).")
    def clean_renewal_date(self):
        data = self.cleaned_data['renewal_date']

        # Check if a date is not in the past.
        if data < datetime.date.today():
            raise ValidationError(_('Invalid date - renewal in past'))

        # Check if a date is in the allowed range (+4 weeks from today).
        if data > datetime.date.today() + datetime.timedelta(weeks=4):
            raise ValidationError(_('Invalid date - renewal more than 4 weeks ahead'))

        # Remember to always return the cleaned data.
        return data    
```

**Uso: urs.py, views.py y templates**

```python
import datetime

from django.shortcuts import render, get_object_or_404
from django.http import HttpResponseRedirect
from django.urls import reverse

from catalog.forms import RenewBookForm

def renew_book_librarian(request, pk):
    book_instance = get_object_or_404(BookInstance, pk=pk)

    # If this is a POST request then process the Form data
    if request.method == 'POST':

        # Create a form instance and populate it with data from the request (binding):
        form = RenewBookForm(request.POST)

        # Check if the form is valid:
        if form.is_valid():
            # process the data in form.cleaned_data as required (here we just write it to the model due_back field)
            book_instance.due_back = form.cleaned_data['renewal_date']
            book_instance.save()

            # redirect to a new URL:
            return HttpResponseRedirect(reverse('all-borrowed') )

    # If this is a GET (or any other method) create the default form.
    else:
        proposed_renewal_date = datetime.date.today() + datetime.timedelta(weeks=3)
        form = RenewBookForm(initial={'renewal_date': proposed_renewal_date})

    context = {
        'form': form,
        'book_instance': book_instance,
    }

    return render(request, 'catalog/book_renew_librarian.html', context)
```


## ModelForms

Heredan de ModelForm

## Vistas genéricas de edición

* **CreateView**
* **UpdateView**
* **DeleteView**

