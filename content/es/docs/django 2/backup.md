---
title: "Copias de seguridad"
date: 2021-10-21T10:36:54+02:00
weight: 15
description: >
  Copias de segurdad. Backup y restore
tags: []
---

{{% pageinfo %}}
* https://django-dbbackup.readthedocs.io/
* https://docs.djangoproject.com/en/4.0/ref/django-admin/#dumpdata
* https://docs.djangoproject.com/en/4.0/ref/django-admin/#loaddata
{{% /pageinfo %}}

```python
pip install django-dbbackup


# settings.py
INSTALLED_APPS = (
    ...
    'dbbackup',  # django-dbbackup
)

DBBACKUP_STORAGE = 'django.core.files.storage.FileSystemStorage'
DBBACKUP_STORAGE_OPTIONS = {'location': '/my/backup/dir/'}


$ python manage.py dbbackup
$ python manage.py dbrestore
$ python manage.py mediabackup
```


```python
$ python manage.py dumpdata
$ python manage.py loaddata
```

