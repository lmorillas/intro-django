---
title: "Generación de archivos CSV"
date: 2021-10-21T10:36:54+02:00
weight: 2
description: >
  Generación de salida csv
tags: []
---

{{% pageinfo %}}
* https://docs.djangoproject.com/en/4.0/howto/outputting-csv/
{{% /pageinfo %}}

## Generación de un CSV dinámico

```python
import csv
from django.http import HttpResponse

def some_view(request):
    # Create the HttpResponse object with the appropriate CSV header.
    response = HttpResponse(
        content_type='text/csv',
        headers={'Content-Disposition': 'attachment; filename="somefilename.csv"'},
    )

    writer = csv.writer(response)
    writer.writerow(['First row', 'Foo', 'Bar', 'Baz'])
    writer.writerow(['Second row', 'A', 'B', 'C', '"Testing"', "Here's a quote"])

    return response
```
