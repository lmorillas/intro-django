---
title: "Instalación"
date: 2021-10-21T10:36:54+02:00
weight: 5
description: >
  Instalación entorno
tags: [django, instalación]
---

{{% pageinfo %}}
Instalación y configuración del entorno para desarrollo:
* https://docs.djangoproject.com/en/4.1/intro/install/
* https://code.visualstudio.com/docs/python/tutorial-django
* https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/development_environment
{{% /pageinfo %}}

## Instalación de Python
* Versión de python? https://docs.djangoproject.com/en/4.1/faq/install/#faq-python-version-support
* https://www.python.org/downloads/

## Configuración de una base de datos
Al inicio no será necesario. Luego podremos usar PostgreSQL, MariaDB, MySQL, Oracle (https://docs.djangoproject.com/en/3.2/topics/install/#database-installation)



## Entorno virtual

Creamos carpeta para el proyecto y dentro de esa carpeta:

```bash
# Linux
python3 -m venv env

# macOS
python3 -m venv env

# Windows
py -m venv env
```
Activar entorno:

```bash
# Windows
env\Scripts\activate.bat
# linux/mac
source tutorial-env/bin/activate

```


## Instalación de Django

Instalación de una versión oficial: https://docs.djangoproject.com/en/3.2/topics/install/#installing-official-release

```bash
# Linux / Mac
$ pip install Django

# Windows
...\> py -m pip install Django

```
## Comprobación 
Usa el intérprete de python

```python
>>> import django
>>> print(django.get_version())
4.1
```

## Configuración del entorno (Visual Studio Code)
* https://code.visualstudio.com/docs/python/tutorial-django
* https://docs.microsoft.com/es-es/visualstudio/python/learn-django-in-visual-studio-step-01-project-and-solution


## Browser para SQLite
* https://sqlitebrowser.org/dl/