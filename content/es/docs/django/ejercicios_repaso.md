---
title: "Ejercicios repaso y profundización"
date: 2021-10-21T10:36:54+02:00
weight: 15
description: >
  Urls, vistas, plantillas, modelos
tags: [ejercicio]
---

{{% pageinfo %}}
Documentación: 
* https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/
* https://docs.djangoproject.com/en/3.2/intro/
{{% /pageinfo %}}


## Revisar instalación
* Entorno virtual
* Activar e instalar django
* Crear proyecto y app
* Si no has creado un repositorio git, es el momento.

## Modificar plantillas para página principal
* Crea un menú (navbar) https://getbootstrap.com/docs/5.1/examples/navbars/
* Crea una página de contacto/acerca de

## Añade los modelos que faltan
* Idiomas de los libros (modelo **Language**)
* Modelo **Bookinstance**
* Inserta unos libros
Revisa la documentación de https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Models

* Añade los modelos al admin

## Página inicial
En la página incial se verá:
* El menú
* Logo o imagen en grande de la web
* Resumen de número de libros del catálogo y número de autores
* Últimos libros añadidos

## Añade una nueva clase **Revisión** para que los usuarios puedan valorar un libro:
* Usuario. Usa el modelo **User** de Django:

   ```python
   from django.contrib.auth.models import User
   ```
* Fecha de la revisión
* Puntuación (1-5)
* Texto

Un usuario sólo puede valorar un libro una vez. Podrá modificar su valoración. 