---
title: "Subida de archivos"
date: 2021-10-21T10:36:54+02:00
weight: 30
description: >
  Subida de archivos
tags: [Imágenes, Documentos]
---

{{% pageinfo %}}
Documentación:
* https://docs.djangoproject.com/en/3.2/topics/files/
{{% /pageinfo %}}

## Configuración
Django usa STACIT_ROOT y STATIC_URL para servir lso archivos estáticos (css, js, assets).
Para los archivos que se suben de forma dinámica:
* MEDIA_ROOT
* MEDIA_URL
 
```python
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
MEDIA_URL = '/media/'
```

En templates:
```django.template.context_processors.media```

## Servidor en desarrollo
```python
if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, 
               document_root=settings.MEDIA_ROOT)
```

## Test
Subir un estático a mano y comprobar que se ve en el servidor.

## Subida de archivos con formularios
```html
<form action="{% url 'upload' %}" method="post" enctype="multipart/form-data">
    <input type="file" name="file">
    <input type="submit" value="Upload">
</form>
```

## Trabajar con archivos en una vista
El contenido llega en ```request.FILES```
```python
with open(os.path.join(settings.MEDIA_ROOT, 'archivo.txt'), 'wb+') as destination:
    for chunk in request.FILES['file'].chunks():
        destination.write(chunk)
```

## Problema de seguridad
El navegador da unos valores:
```python
upload = request.FILES['file']
size = upload.sizecontent = request.FILES['file'].read()
name = upload.name
content_type = upload.content_type
charset = upload.charset
```
¿Entorno de confianza?

```python
import mimetypes

upload = request.FILES['file']
mimetype, encoding = mimetypes.guess_type(upload.name)
if mimetype is None or not mimetype.startswith('image/'):
    raise ...
```

## Ejemplo vista sencilla
```python
from django.conf import settings

def vista_ejemplo(request):
    if request.method == 'POST':
        save_path = os.path.join(settings.MEDIA_ROOT, request.FILES["file_upload"].name)

        with open(save_path, "wb") as output_file:
            for chunk in request.FILES["file_upload"].chunks():
                output_file.write(chunk)

    return render(request, "media-example.html")
```

## Uso con Django Forms
```python
from django import forms

class UploadForm(forms.Form):
    file_upload = forms.FileField()
```

```python
import os
from django.conf import settings
from django.shortcuts import render

from .forms import UploadForm

def media_example(request):
    if request.method == 'POST':
        form = UploadForm(request.POST, request.FILES)
        if form.is_valid():
            save_path = os.path.join(settings.MEDIA_ROOT, form.cleaned_data["file_upload"].name)

            with open(save_path, "wb") as output_file:
                for chunk in form.cleaned_data["file_upload"].chunks():
                    output_file.write(chunk)
    else:
        form = UploadForm()

    return render(request, "media-example.html", {"form": form})
```
```html
<form method="post" enctype="multipart/form-data">
        {% csrf_token %}
        {{ form.as_p }}
        <button type="submit">Submit</button>
</form>
```

## Imágenes con Django Forms
Instalar Pillow

```python
class UploadForm(forms.Form):
    file_upload = forms.ImageField()
```

```python
import os
from PIL import Image
from django.conf import settings
from django.shortcuts import render

from .forms import UploadForm

def media_example(request):
    if request.method == 'POST':
        form = UploadForm(request.POST, request.FILES)
        if form.is_valid():
            save_path = os.path.join(settings.MEDIA_ROOT, form.cleaned_data["file_upload"].name)

            image = Image.open(form.cleaned_data["file_upload"])
            image.thumbnail((50, 50))
            image.save(save_path)
    else:
        form = UploadForm()

    return render(request, "media-example.html", {"form": form})
```


## Uso de Modelos

```python
from django.db import models

class ExampleModel(models.Model):
    image_field = models.ImageField(upload_to="images/")
    file_field = models.FileField(upload_to="files/")
```

```python
from django.shortcuts import render

from .forms import UploadForm
from .models import ExampleModel

def media_example(request):
    instance = None

    if request.method == 'POST':
        form = UploadForm(request.POST, request.FILES)

        if form.is_valid():
            instance = ExampleModel()
            instance.image_field = form.cleaned_data["image_upload"]
            instance.file_field = form.cleaned_data["file_upload"]
            instance.save()
    else:
        form = UploadForm()

    return render(request, "media-example.html", {"form": form, "instance": instance})
``` 

```html
    <form method="post" enctype="multipart/form-data">
        {% csrf_token %}
        {{ form.as_p }}
        <button type="submit">Submit</button>
    </form>
    {% if instance %}
        <img src="{{ instance.image_field.url }}">
    {% endif %}
```