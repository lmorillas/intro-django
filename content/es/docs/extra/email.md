---
title: "Enviar correo"
date: 2021-10-21T10:29:17+02:00
linkTitle: "Correo"
weight: 5
description: >
  
docs: 

draft: false

---

{{% pageinfo %}}
**{{< emoji ":books:" >}} Documentación**:
* https://docs.djangoproject.com/en/4.1/topics/email/
{{% /pageinfo %}}

## Para testing/debug

```python
# en settings.py
EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend'
```
SMTP de gmail
```python

EMAIL_HOST = 'smtp.googlemail.com'
EMAIL_PORT = 587
EMAIL_HOST_USER = 'USER_MAIL'
EMAIL_HOST_PASSWORD = 'USER_MAIL_PASSWORD'
EMAIL_USE_TLS = True
```
Para utilizar gmail como servidor de corres es necesario permitir el acceso de aplicaciones poco seguras https://myaccount.google.com/lesssecureapps 

## Producción

* AWS SES
* Sendgrid
* Mailgun
* ...
