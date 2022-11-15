---
title: "Traducción"
date: 2021-10-21T10:36:54+02:00
weight: 18
description: 
---

{{% pageinfo %}}
Documentación: 
* https://docs.djangoproject.com/en/4.1/topics/i18n/translation/
* https://crowdin.com/blog/2021/11/10/django-translation
* https://poedit.net/ (editor de archivos .po)
{{% /pageinfo %}}


## Traducción de los textos de la aplicación (código python)

```python
from django.http import HttpResponse
from django.utils.translation import gettext as _

def my_view(request):
    output = _("Welcome to my site.")
    return HttpResponse(output)
```
### Ayuda de traducción

```python
def my_view(request):
    # Translators: This message appears on the home page only
    output = gettext("Welcome to my site.")
```

## Pluralización

```python
from django.utils.translation import ngettext

def my_view(request):
    output = ngettext(
        "There is %(count)s person in this room.",
        "There are %(count)s people in this room.",
        count
    ) % {'count': count}
    return HttpResponse(output)
```

## Marcadores de contexto

```python
from django.utils.translation import pgettext

month = pgettext("month name", "May")
```

## Lazy translation

```python
from django.db import models
from django.utils.translation import gettext_lazy as _

class MyThing(models.Model):
    name = models.CharField(help_text=_('This is the help text'))
```

## En plantillas

```html
{% load i18n %}

<title>{% translate "This is the title." %}</title>
<title>{% translate myvar %}</title>

{% blocktranslate %}This string will have {{ value }} inside.{% endblocktranslate %}

```

## Proceso:
* Creación de directorio `locale` en las aplicaciones si no existe.
* Creación de ficheros de cadenas (ficheros **.po**): `django-admin makemessages -l es` 
* Traducción (poedit)
* Generación de ficheros binarios (ficheros **.mo**): `django-admin compilemessages`

