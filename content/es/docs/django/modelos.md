---
title: "Modelos"
date: 2021-10-21T10:36:54+02:00
weight: 8
description: >
  Creación y uso de modelos
tags: 
---

{{% pageinfo %}}
Documentación: 
* https://docs.djangoproject.com/en/4.1/intro/tutorial02/
* https://developer.mozilla.org/es/docs/Learn/Server-side/Django/Models 
{{% /pageinfo %}}

![Base de datos](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Models/local_library_model_uml.svg)


## Trabajando con modelos
* archivo **models.py**
* Argumentos comunes
* Tipos comunes de campos

## Gestión de modelos
* Creación y modificación de registros
* Búsqueda 

## Tarea: Definir los modelos de la biblioteca
* Género
* Book
* Bookinstance
* Autor

## Migraciones

## Modelo Language

## Fixtures 
* Carga de datos iniciales
* En carpeta `fixtures` de la aplicación

> Copia el archivo [catalogo.json](https://raw.githubusercontent.com/lmorillas/tutorial-locallibrary-mozilla/develop/locallibrary/catalog/fixtures/catalogo.json) en `locallibrary/catalog/fixtures/` y ejecuta 
> ```bash
> $ python manage.py loaddata catalogo.json```   

## Usando el shell de Django
> https://docs.djangoproject.com/en/4.1/intro/tutorial02/#playing-with-the-api
> Ejecuta:
```powershell
$ python manage.py shell
```
### Búsquedas
```python
>>> from catalog.models import Book, Author, Genre
# Cuántos libros hay?
>>>  Book.objects.all().count()
# Libro con el id 1
>>> Book.objects.get(id=1)

# Compara los resultados
>>> Book.objects.filter(title='The Idiot')
>>> Book.objects.filter(title__icontains='idiot')
>>> Book.objects.filter(title='The idiot')
>>> Book.objects.filter(title__iexact='The idiot')

>>> libro = Book.objects.filter(title='The Idiot')[0]
>>> libro.title
>>> libro.author
>>> libro.author.last_name
>>> libro.summary
>>> libro.isbn
>>> libro.genre.all()
```

### Creación de registros
```python
>>> from catalog.models import Book, Author, Genre
>>> autor = Author()
>>> autor.first_name = 'xxxxxxxx'
>>> autor.last_name = 'yyyyyyyy'
>>> autor.save()
>>> autor.id
>>> libro = Book()
>>> libro.title = 'xxxxxxxxx'
>>> libro.author = autor
>>> libro.save()
>>> libro.id
# Crea y asigna un nuevo género
# por ejemplo: 'Fantasía'
>>> libro.genre.add(Genre.objects.get(name='Fantasía'))
```
> Comprueba que se han creado los registros en la base de datos haciendo consultas.

