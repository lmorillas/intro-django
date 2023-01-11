---
title: "Túneles con ngrok"
date: 2021-10-21T10:29:17+02:00
linkTitle: "Ngrok"
weight: 100
description: >
  
docs: 

draft: false

---

{{% pageinfo %}}
* https://ngrok.com/ 
{{% /pageinfo %}}

* Descarga la versión de `ngrok` para tu sistema operativo
* Date de alta en la plataforma https://dashboard.ngrok.com/signup si no tienes un usuario
* Configura el token `ngrok authtoken <TOKEN DE NGROK>`
* Crea el túnel: `ngrok http 8000` En este caso al puerto 8000 de tu ordenador porque es el que usa django por defecto. Si usas otro puerto, cambia el 8000 por el que uses.
* Tendrás un mensaje de este tipo:
```bash
ngrok by  ...

Session Status                online
Account                       <tu usuario> (Plan: Free)
Version                       2.3.40
Region                        United States (us)
Web Interface                 http://127.0.0.1:4040
Forwarding                    http://559b-88-7-36-xxx.ngrok.io -> http://localhost:8000

```
* Modifica el `settings.py` del proyecto para que el dominio sea el que te proporciona ngrok. Copia la dirección que aparece en el mensaje anterior, en este caso `559b-88-7-36-xxx.ngrok.io`

```python
ALLOWED_HOSTS = ['559b-88-7-36-xxx.ngrok.io']
```
* Lanza el servidor local de django `python manage.py runserver`
* Abre el navegador y accede a la dirección que te proporciona ngrok. En este caso `http://559b-88-7-36-xxx.ngrok.io`