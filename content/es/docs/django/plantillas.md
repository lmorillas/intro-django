---
title: "Plantillas"
date: 2021-10-21T10:36:54+02:00
weight: 12
description: >
  Urls, vistas, plantillas
tags: [view, template, urls]
---

{{% pageinfo %}}
Documentación: 
* https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Home_page
* https://docs.djangoproject.com/en/4.1/topics/templates/
{{% /pageinfo %}}


## Visión general
> A template is a text file that defines the structure or layout of a file (such as an HTML page), it uses placeholders to represent actual content.

## Arquitectura de plantillas
* Crearemos una carpeta llamada **templates** en la raíz de nuestro aplicación.
* Diseño de una plantilla base `base.html` que será extendida por las demás plantillas.
* La plantilla base definirá los bloques que luego serán reemplazados por las plantillas hijas.
* Usamos `include` para incluir bloques de código en otras plantillas.
* Usamos `extends` para extender una plantilla base.
* Usamos `block` para definir bloques de código.

## Ejemplo de plantilla base (`base.html`)
```html
<!DOCTYPE html>
<html lang="en">
<head>
  {% block title %}<title>Local Library</title>{% endblock %}
</head>
<body>
  {% block sidebar %}<!-- insert default navigation text for every page -->{% endblock %}
  {% block content %}<!-- default content text (typically empty) -->{% endblock %}
</body>
</html>
```
## Ejemplo de plantilla hija

```html
{% extends "base.html" %}

{% block title %}<title>Specific Book Page</title>{% endblock %}

{% block content %}
  <h1>{{ book.title }}</h1>
  <p>Author: {{ book.author }}</p>
  <p>Summary: {{ book.summary }}</p>
  <p>ISBN: {{ book.isbn }}</p>
  <p>Genre: {{ book.genre.all|join:", " }}</p>
{% endblock %}
```

## TAREA: Crear un tema con bootstrap 5 y usarlo en el sitio

* https://getbootstrap.com/docs/5.2/getting-started/introduction/
* https://bootswatch.com/flatly/

### Estructura

```html
<!doctype html>
<html lang="es">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Bootstrap demo</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-Zenh87qX5JnK2Jl0vWa8Ck2rdkQ2Bzep5IDxbcnCeuOxjzrPF/et3URy9Bv1WTRi" crossorigin="anonymous">
  </head>
  <body>
    <h1>Hello, world!</h1>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-OERcA2EqjJCMA+/3y+gxIOqMEjwtxJY7qPCqsdltbNJuaOe923+mo//f6V8Qbsw3" crossorigin="anonymous"></script>
  </body>
</html>
```

### Modificar para Django

```html
{% load static %}
<!doctype html>
<html lang="es">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>{% block title %}{% endblock %}</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-Zenh87qX5JnK2Jl0vWa8Ck2rdkQ2Bzep5IDxbcnCeuOxjzrPF/et3URy9Bv1WTRi" crossorigin="anonymous">
    <link rel="stylesheet" href="{% static 'css/custom_styles.css' %}">
  </head>
  <body>
    {% block content %}{% endblock %}
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-OERcA2EqjJCMA+/3y+gxIOqMEjwtxJY7qPCqsdltbNJuaOe923+mo//f6V8Qbsw3" crossorigin="anonymous"></script>
  </body>
</html>
```

### Navbar

```html
<nav class="navbar navbar-expand-lg navbar-dark bg-primary">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">Navbar</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarColor01" aria-controls="navbarColor01" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarColor01">
      <ul class="navbar-nav me-auto">
        <li class="nav-item">
          <a class="nav-link active" href="#">Home
            <span class="visually-hidden">(current)</span>
          </a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Catalogo</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Libros disponibles</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Acerca de</a>
        </li>
        
      </ul>
      <form class="d-flex">
        <input class="form-control me-sm-2" type="text" placeholder="Search">
        <button class="btn btn-secondary my-2 my-sm-0" type="submit">Buscar</button>
      </form>
    </div>
  </div>
</nav>
```

### Mover Navbar a include

### Corregir urls

### Logo

### Pagina de inicio
Elige un modelo
* https://getbootstrap.com/docs/5.2/examples/cover/
* https://getbootstrap.com/docs/5.2/examples/heroes/
* Imágenes: 
  * https://commons.wikimedia.org/wiki/File:Librarian.svg
  * https://commons.wikimedia.org/wiki/File:Library.svg
  * [Más imágenes de wikimedia commons](https://commons.wikimedia.org/w/index.php?search=Library&title=Special:MediaSearch&type=image&filemime=svg)
