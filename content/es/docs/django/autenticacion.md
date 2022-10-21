---
title: "Autenticación y permisos"
date: 2021-10-21T10:36:54+02:00
weight: 28
description: >
  Autenticación y permisos
tags: [Autenticación, Permisos]
---

{{% pageinfo %}}
* https://docs.djangoproject.com/en/3.1/topics/http/sessions/
* https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Authentication
* https://learndjango.com/tutorials/django-login-and-logout-tutorial
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
* Hay que tener configurada la búsqueda de templates en **settings.py**  https://github.com/lmorillas/biblioteca/blob/main/biblioteca/settings.py#L63

## LOGOUT
Se puede configurar LOGOUT_REDIRECT_URL en settings.py o facilitar la plantilla  **'registration/logged_out.html'** que responde a la acción de logout.

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
