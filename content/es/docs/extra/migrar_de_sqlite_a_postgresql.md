---
title: "Migración del proyecto de Django de sqlite a Postgresql"
date: 2021-10-21T10:36:54+02:00
weight: 130
description: >
  Migración de Sqlite a Postgresql
tags: [mibración, postgresql, django]
---

{{% pageinfo %}}
**Descripción**: Migración a Postgresql
{{% /pageinfo %}}

## Copia de datos de sqlite

```bash
# hacemos una copia de los datos de sqlite
# creamos antes el directorio backups si no está creado.
$ python manage.py dumpdata -o backups/datosbiblioteca.json
```

## Instalación y configuración de docker y docker-compose

Si trabajamos en linux o mac lo hacemos directametne en la mmáquina. Si trabajamos en Windows, usamos la máquina virtualbox que tenemos creada. 

{{% pageinfo %}}
**Documentación**
* https://docs.docker.com/engine/install/
* https://docs.docker.com/compose/install/
{{% /pageinfo %}}

### Instalación de docker
```bash
$ curl -fsSL https://get.docker.com -o get-docker.sh
$ DRY_RUN=1 sh ./get-docker.sh

# post instalación
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
$ newgrp docker 
```

Podemos comprobar que ha funcionado bien 
```bash
$ docker run hello-world
```

### Instalación de docker-compose

```bash
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
```

Podemos comprobar que ha funcionado bien 
```bash
$ docker-compose --version
```
## Instalación del servico de postgresql
Este servicio lo instalamos en linux o en la máquina **virtualbox** si usas windows

En una carpeta de este linux creamos el siguiente archivo con los serviciios de postgresql y adminer.


```yaml
# docker-compose.yml
version: '3.1'

services:
  db:
    image: postgres:13.0-alpine
    environment:
      - POSTGRES_USER=django
      - POSTGRES_PASSWORD=password
      - POSTGRES_DB=biblioteca
    volumes:
      - ./postgres_data:/var/lib/postgresql/data/
    ports:
      - 5432:5432

  adminer:
    image: adminer
    ports:
      - 8080:8080
```
En esa misma carpeta ejecutamos: 
```bash
$ docker-compose up -d
```

Y accedmos a la url del adminer: ```http://localhost:8080``` (o la ip de la máquina virtual si la estaś usando).

Podrás conectar con la base de datos seleccionando postgresql y el resto de datos.

## Configuración de la nueva base de datos en django
Como vamos a usar postgresql debemos instalar el cliente de python para postgresql en nuestra máquina. 

```bash
$ pip install psycopg2-binary
```
Y configuramos el archivo settings.py para que use postgresql.

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'biblioteca',
        'USER': 'django',
        'PASSWORD': 'password',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}

```
Si usas virutalbox tienes que poner la **ip de virtualbox** en el host.

## Creación de la estructura de la base de datos (migraciones)

```bash
$ python manage.py migrate
```


## Carga de los datos antiguos de sqlite
```bash
$ python manage.py loaddata backups/datosbiblioteca.json
```

Y comprobamos que todo ha ido bien.  Deberíamos de tener nuestro proyecto django ejecutándose con la nueva base de datos postgresql. Recordad que el servidor de docker de postgresql tiene que estar ejecutándose. 


## Mejoras
* Usar variables de entorno en ```docker-compose.yml``` y en ```settings.py```
* Puedes usar un fichero ```.env``` para configurar las variables de entorno.