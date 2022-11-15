---
title: "Form"
date: 2021-10-21T10:36:54+02:00
weight: 10

description: >
  Formularios
tags: [Formularios]

docs: >
    * video csrf: https://www.youtube.com/watch?v=W9AvIUdhttA
---
{{% pageinfo %}}
Documentación:
https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Forms#renew-book_form_using_a_form_and_function_view

{{% /pageinfo %}}

## Objeto Form
```python
from django import forms

```

## Declarar un formulario
```python
# archivo forms.py
from django import forms

class RenewBookForm(forms.Form):
    renewal_date = forms.DateField(help_text="Introduce una fecha entre hoy y 4 semanas(default 3).")

```   
> **Nota**: Los form fields son clases que heredan de django.forms.Field. Cada uno tiene un tipo de dato asociado. Por ejemplo, CharField es un campo de texto, DateField es un campo de fecha, etc. Y generan un input HTML asociado a su tipo de dato.
> Revisa los `form fields` y sus argumentos en https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Forms#renew-book_form_using_a_form_and_function_view

## Validación
Declaramos un método `clean_<fieldname>()` para cada campo que queremos validar. Este método recibe el valor del campo y devuelve el valor validado. Si hay un error, se lanza una excepción `ValidationError`.

```python

class RenewBookForm(forms.Form):
    renewal_date = forms.DateField(help_text="Introduce una fecha entre hoy y 4 semanas(default 3).")
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

## Configurar urls.py

```python
urlpatterns += [
    path('book/<uuid:pk>/renew/', views.renew_book_librarian, name='renew-book-librarian'),
```

## Vista

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

## Template
En el contexto llega el formulario (`form`) y el objeto `book_instance` que se está renovando.

```html
{% extends "base_generic.html" %}

{% block content %}
  <h1>Renovar libro</h1>
  <form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <input type="submit" value="Renovar" />
  </form>
{% endblock %}
```
```html
 {{ form.as_table }} 
 {{ form.as_ul }}) 
 {{ form.as_p }}
```
> Muy importante siempre que va a haber una modificación: `{% csrf_token %}`

```html
{% extends "base_generic.html" %}

{% block content %}

  <h1>Renovar libro para {{ book_instance.book.title }} </h1>

  <form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <input type="submit" value="Renovar" />
  </form>

{% endblock %}
```
