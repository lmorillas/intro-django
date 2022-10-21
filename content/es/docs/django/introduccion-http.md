---
title: "Introducción a HTTP"
date: 2021-10-21T10:36:54+02:00
weight: 7
description: >
  HTTP requests & responses
tags: [http]
---

{{% pageinfo %}}
Documentación
* https://developer.mozilla.org/en-US/docs/Web/HTTP
* https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview
{{% /pageinfo %}}

## HTTP
Djando procesa peticiones HTTP y genera respuestas HTTP

### Petición
```
GET / HTTP/1.1
Host: www.cpilosenlaces.com
Cache-Control: no-cache
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: es-ES,es;q=0.9,en;q=0.8,gl;q=0.7,ca;q=0.6
Cookie: _ga=GA1.2.35175891.163;
```
Verbos: GET, POST, PUT, DELETE


### Respuesta

```
HTTP/1.1 200 OK
Server: nginx/1.14.1
Date: Thu, 21 Oct 2021 10:09:34 GMT
Content-Type: text/html; charset=UTF-8
Content-Length: 15482
Connection: keep-alive
Vary: Accept-Encoding
Last-Modified: Thu, 21 Oct 2021 09:54:43 GMT
ETag: "3a7f-5xxx9e24f3b6f"
Accept-Ranges: bytes
Cache-Control: max-age=2708
Expires: Thu, 21 Oct 2021 10:54:43 GMT
Content-Encoding: gzip

```

### Status Codes
* https://es.wikipedia.org/wiki/Anexo:C%C3%B3digos_de_estado_HTTP
* https://developer.mozilla.org/en-US/docs/Web/HTTP/Status

1. Respuestas informativas (100–199)
1. Respuestas satisfactorias (200–299)
1. Redirecciones (300–399)
1. Errores de los clientes (400–499)
1. Errores de los servidores (500–599)


### Requests y responses en django [opt]
https://docs.djangoproject.com/en/3.2/intro/tutorial01/