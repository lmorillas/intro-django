---
title: "Uso de mapas"
date: 2021-10-21T10:36:54+02:00
weight: 36
description: >
  Ejemplo uso de mapas con leaflet
tags: [Estáticos]
---

{{% pageinfo %}}
Documentación:
* https://leafletjs.com/examples/quick-start/
* Apps específicas: https://django-leaflet.readthedocs.io/en/latest/
* Tutoriales: https://mappinggis.com/?s=leaflet
* Ejemplos: https://github.com/tomik23/leaflet-examples
{{% /pageinfo %}}

## Configurar
1. Css de leaflet
```html
 <link rel="stylesheet" href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css"
   integrity="sha512-xodZBNTC5n17Xt2atTPuE1HxjVMSvLVW9ocqUKLsCC5CXdbqCmblAshOMAS6/keqq/sMZMZ19scR4PsZChSR7A=="
   crossorigin=""/>
```
2. JS de Leaflet
```html
 <!-- Make sure you put this AFTER Leaflet's CSS -->
 <script src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js"
   integrity="sha512-XQoYMqMTK8LvdxXYG3nZ448hOEQiglfqkJs1NOQV44cWnUrBc8PkAOcXy20w0vlaXaVUearIOBhiXZ5V3ynxwA=="
   crossorigin=""></script>
```
3. En plantilla:
```html
 <div id="map"></div>
 ```
 4. Configurar mapa desde js
Ejemplo en plantilla de django con coordenadas en variable **coords**
```html
<script>
    var mimapa = L.map('map').setView([{{coords}}], 13);

    L.tileLayer('http://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: 'Map data &copy; <a href="http://openstreetmap.org">OpenStreetMap</a> contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="http://cloudmade.com">CloudMade</a>',
    maxZoom: 18
    }).addTo(mimapa);

    L.marker([{{coords}}]).addTo(mimapa).bindPopup("CPI Los Enlaces");
</script>
 ```
5. Configurar el mapa en css
```html
<style>
    #map { height: 400px ;}
</style>
 ```