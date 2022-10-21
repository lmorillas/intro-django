---
title: "Salida JSON"
date: 2021-10-21T10:36:54+02:00
weight: 6
description: >
  Generación de salida json
tags: []
---

{{% pageinfo %}}
* https://docs.djangoproject.com/en/4.0/ref/request-response/#django.http.JsonResponse
* https://dev.to/brian101co/how-to-return-a-json-response-in-django-gen
{{% /pageinfo %}}


## Generación salida JSON

```python
from django.http import JsonResponse

def view_list_json(request):
    ...
    data = {} # diccionario
    return JsonResponse(data)


# views.py
from django.core.serializers import serialize
from django.http import HttpResponse
from .models import Post

def django_models_json(request):
    qs = Post.objects.all()
    data = serialize("json", qs, fields=('title', 'content'))
    return HttpResponse(data, content_type="application/json")
```
