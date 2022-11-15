---
title: "ModelForm"
date: 2021-10-21T10:36:54+02:00
weight: 15
description: >
  Formularios
tags: [Formularios]

docs: >
    * video csrf: https://www.youtube.com/watch?v=W9AvIUdhttA
---

{{% pageinfo %}}
Documentación: 
* https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Forms#modelforms*
{{% /pageinfo %}}


## ModelForms 
* Heredan de `ModelForm` (`from django.forms import ModelForm`)
* Se crean a partir de un modelo
* `fields`: lista de campos del modelo que se incluirán en el formulario
* `exclude`: lista de campos del modelo que se excluirán del formulario
* 
```python
from django.forms import ModelForm
from django.utils.translation import gettext_lazy as _

from catalog.models import BookInstance

class RenewBookModelForm(ModelForm):
    class Meta:
        model = BookInstance
        fields = ['due_back']
        labels = {'due_back': _('New renewal date')}
        help_texts = {'due_back': _('Enter a date between now and 4 weeks (default 3).')}
```

### Con validación

```python
from django.forms import ModelForm

from catalog.models import BookInstance

class RenewBookModelForm(ModelForm):
    def clean_due_back(self):
       data = self.cleaned_data['due_back']

       # Check if a date is not in the past.
       if data < datetime.date.today():
           raise ValidationError(_('Invalid date - renewal in past'))

       # Check if a date is in the allowed range (+4 weeks from today).
       if data > datetime.date.today() + datetime.timedelta(weeks=4):
           raise ValidationError(_('Invalid date - renewal more than 4 weeks ahead'))

       # Remember to always return the cleaned data.
       return data

    class Meta:
        model = BookInstance
        fields = ['due_back']
        labels = {'due_back': _('Renewal date')}
        help_texts = {'due_back': _('Enter a date between now and 4 weeks (default 3).')}
```
