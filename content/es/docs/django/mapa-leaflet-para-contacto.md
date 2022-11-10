---
title: "Mapa Leaflet"
date: 2021-10-21T10:36:54+02:00
weight: 16
description: 
---

{{% pageinfo %}}
Documentación: 
* https://leafletjs.com/reference.html
* https://leafletjs.com/examples/quick-start/
{{% /pageinfo %}}

## Preparar página
Añadir CSS en el `head` de la página (**crea un bloque `extra_css` en la plantilla base**)
```html
     <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.2/dist/leaflet.css"
         integrity="sha256-sA+zWATbFveLLNqWO2gtiw3HL/lh1giY/Inf1BJ0z14="
         crossorigin=""/>
```
Añadir el js de Leavlet después del CSS (**crea un bloque `extra_js` en la plantilla base**)
```html
     <!-- Make sure you put this AFTER Leaflet's CSS -->
     <script src="https://unpkg.com/leaflet@1.9.2/dist/leaflet.js"
         integrity="sha256-o9N1jGDZrf5tS+Ft4gbIK7mYMipq9lqpVJ91xHSyKhg="
         crossorigin=""></script>
```

Coloca un div con un id en la plantilla donde quieres que aparezca el mapa
```html
     <div id="map"></div>
```

Asegúrate de que el div tiene una altura definida en el css
```css
     #map {
         height: 400px;
     }
```
Inicializa los valores de Leaflet en el js de la página

```js
     var mymap = L.map('map').setView([41.6448418,-0.9241785], 13);
```

Valores de tileLayer:

```js
L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 19,
    attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'
}).addTo(map);
``` 

Aquí puedes ver más información de la configuración de Leaflet: https://leafletjs.com/examples/quick-start/
* **maxZoom**: Nivel máximo de zoom
* **attribution**: Atribución del mapa
* **addTo(map)**: Añade el mapa a la variable `map`
* **setView([lat,lon], zoom)**: Establece la vista del mapa en la latitud y longitud indicadas y el nivel de zoom
* creación de popups: https://leafletjs.com/examples/quick-start/#popup

