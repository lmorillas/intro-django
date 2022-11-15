---
title: "Formularios - Crispy"
date: 2021-10-21T10:36:54+02:00
weight: 20
description: >
  Formularios con Crispy
tags: [Formularios, Crispy]
draft: true
---

{{% pageinfo %}}
Documentación oficial: 
* https://django-crispy-forms.readthedocs.io/en/latest/
* https://github.com/django-crispy-forms/django-crispy-forms

Tutoriales:
* https://simpleisbetterthancomplex.com/tutorial/2018/11/28/advanced-form-rendering-with-django-crispy-forms.html
* https://www.merixstudio.com/blog/django-crispy-forms-what-are-they-about/
* https://dontrepeatyourself.org/post/django-forms-django-crispy-forms/
{{% /pageinfo %}}

## Situación
Cuando nace **Django** internet era mucho más simple. No existían los UI toolkits como Boostrap. A partir de 2009 se empieza a trabajar en lo que ahora es **Crispy Forms**, que mejora la creación y presentación de formularios.

## Instalación

https://django-crispy-forms.readthedocs.io/en/latest/install.html

```bash
$ pip install django-crispy-forms
```
**Configuración de Django**
```python
INSTALLED_APPS = (
    ...
    'crispy_forms',
)
```

Se pueden usar distintos **template packs** https://django-crispy-forms.readthedocs.io/en/latest/install.html#template-packs

```python
# en settings.py
CRISPY_TEMPLATE_PACK = 'bootstrap4'
```

## Uso
### Crispy Filter
```html
{% load crispy_forms_tags %}

<form method="post" class="uniForm">
    {{ my_formset|crispy }}
</form>
```
###  {% crispy %} tag

* https://django-crispy-forms.readthedocs.io/en/latest/crispy_tag_forms.html
* https://django-crispy-forms.readthedocs.io/en/latest/form_helper.html

Podemos incluir el formulario y un **helper** que dirige su presentación.

```html
{% load crispy_forms_tags %}


{% crispy form  %}
```

## Layouts

* https://django-crispy-forms.readthedocs.io/en/latest/layouts.html
* Ejemplos de uso: 
** https://github.com/sibtc/advanced-crispy-forms-examples/blob/master/mysite/core/forms.py
** https://github.com/s-kust/django-advanced-forms
* 