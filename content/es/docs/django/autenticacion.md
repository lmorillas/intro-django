---
title: "Autenticación y permisos"
date: 2021-10-21T10:36:54+02:00
weight: 28
description: >
  Autenticación y permisos
tags: [Autenticación, Permisos]
---

{{% pageinfo %}}
* https://docs.djangoproject.com/en/4.1/topics/auth/
* https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Authentication
* https://learndjango.com/tutorials/django-login-and-logout-tutorial
{{% /pageinfo %}}

{{% pageinfo color="danger" %}}
## Tarea:
* Repositorio base: https://github.com/lmorillas/django_blog_exercise/
* Instala y ejecuta el proyecto.
  * fork del repositorio
  * clonar en local
  * crear entorno virtual e instalar paquetes
  * migraciones
  * superuser
  * ejecutar
  * introduce unos post y comentarios
* Añade la posibilidad de hacer **login** y **logout**
* Modifica el modelo `Post` para que guarde información del usuario que ha creado el post. Fíjate en el [tutorial de Mozilla](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Authentication#models)
* Crea una vista+url `mis posts` para que un usuario pueda ver sus post. Cuando se ve la página como usuarios no autenticados, el link de `mis posts` está inactivo
* Un usuario solo puede modicar sus post pero puede comentar otros. Si no está logueado, no puede hacer comentarios, pero los puede leer.
{{% /pageinfo %}}

## Habilitar autenticación
```python
NSTALLED_APPS = [
    ...
    'django.contrib.auth',  #Core authentication framework and its default models.
    'django.contrib.contenttypes',  #Django content type system (allows permissions to be associated with models).
    ....

MIDDLEWARE = [
    ...
    'django.contrib.sessions.middleware.SessionMiddleware',  #Manages sessions across requests
    ...
    'django.contrib.auth.middleware.AuthenticationMiddleware',  #Associates users with requests using sessions.
    ....
```


## Creación de usuarios y grupos

Podemos usar el admin

###  Urls
```python
urlpatterns += [
    path('accounts/', include('django.contrib.auth.urls')),
]
```

## LOGIN_URL
Por defecto: **'/accounts/login/'**

* Escribir templates: **'registration/login.html'** dentro de la carpeta del proyecto.

Ejemplo login.html

```html
{% extends "base.html" %}

{% block content %}

{% if form.errors %}
<p>Your username and password didn't match. Please try again.</p>
{% endif %}

{% if next %}
    {% if user.is_authenticated %}
    <p>Your account doesn't have access to this page. To proceed,
    please login with an account that has access.</p>
    {% else %}
    <p>Please login to see this page.</p>
    {% endif %}
{% endif %}

<form method="post" action="{% url 'login' %}">
{% csrf_token %}
<table>
<tr>
    <td>{{ form.username.label_tag }}</td>
    <td>{{ form.username }}</td>
</tr>
<tr>
    <td>{{ form.password.label_tag }}</td>
    <td>{{ form.password }}</td>
</tr>
</table>

<input type="submit" value="login">
<input type="hidden" name="next" value="{{ next }}">
</form>

{# Assumes you set up the password_reset view in your URLconf #}
<p><a href="{% url 'password_reset' %}">Lost password?</a></p>

{% endblock %}

```

## LOGOUT
Se puede configurar LOGOUT_REDIRECT_URL en settings.py o facilitar la plantilla  **'registration/logged_out.html'** que responde a la acción de logout.


## Reset email
`registration/password_reset_email.html`

```html
Someone asked for password reset for email {{ email }}. Follow the link below:
{{ protocol}}://{{ domain }}{% url 'password_reset_confirm' uidb64=uid token=token %}

```


## Forzar login
```python
from django.conf import settings
from django.shortcuts import redirect

def my_view(request):
    if not request.user.is_authenticated:
        return redirect('%s?next=%s' % (settings.LOGIN_URL, request.path))
    # ...
```
Decorador:
```python
from django.contrib.auth.decorators import login_required

@login_required
def my_view(request):
    ...
```

Con vistas genéricas:
```python
from django.contrib.auth.mixins import LoginRequiredMixin

class MyView(LoginRequiredMixin, View):
    login_url = '/login/'
    redirect_field_name = 'redirect_to'

```

Usuarios qeu pasan un test:
```python
from django.shortcuts import redirect

def my_view(request):
    if not request.user.email.endswith('@example.com'):
        return redirect('/login/?next=%s' % request.path)
    # ...


from django.contrib.auth.mixins import UserPassesTestMixin

class MyView(UserPassesTestMixin, View):

    def test_func(self):
        return self.request.user.email.endswith('@example.com')

```

## Permisos
https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Authentication#permissions

Podemos detallar permisos en los modelos y después usarlos en las vistas:

```python
from django.contrib.auth.decorators import permission_required

@permission_required('catalog.can_mark_returned')
@permission_required('catalog.can_edit')
def my_view(request):
    ...


from django.contrib.auth.mixins import PermissionRequiredMixin

class MyView(PermissionRequiredMixin, View):
    permission_required = 'catalog.can_mark_returned'
    # Or multiple permissions
    permission_required = ('catalog.can_mark_returned', 'catalog.can_edit')
    # Note that 'catalog.can_edit' is just an example
    # the catalog application doesn't have such permission!

```

