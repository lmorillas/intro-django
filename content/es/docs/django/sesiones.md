---
title: "Sesiones"
date: 2021-10-21T10:36:54+02:00
weight: 24
description: >
  Gestión de sesiones
tags: [Sesiones]
---

{{% pageinfo %}}
* https://docs.djangoproject.com/en/3.1/topics/http/sessions/
* https://developer.mozilla.org/es/docs/Learn/Server-side/Django/Sessions
{{% /pageinfo %}}

## Habilitar sesiones
```python
INSTALLED_APPS = [
    ...
    'django.contrib.sessions',
    ....

MIDDLEWARE = [
    ...
    'django.contrib.sessions.middleware.SessionMiddleware',
    ....
```

## Ejemplo: contador de visitas
```python
def index(request):
    ...
    
    # Number of visits to this view, as counted in the session variable.
    num_visits = request.session.get('num_visits', 0)
    request.session['num_visits'] = num_visits + 1

    context = {
        'num_visits': num_visits,
    }

    # Render the HTML template index.html with the data in the context variable.
    return render(request, 'index.html', context=context)
```

## Configuración 
* Database sessions (por defecto)
* File-based sessions
* Cached sessions
* Cookie-based sessions
  * SESSION_COOKIE_AGE
  * SESSION_COOKIE_DOMAIN
  * SESSION_COOKIE_SECURE
  * SESSION_EXPIRE_AT_BROWSER_CLOSE
  * SESSION_SAVE_EVERY_REQUEST
  * SESSION_COOKIE_HTTPONLY (para evitar acceso desde javascript)

Mejores prestaciones: cache-based sessions (Memcached, Redis).