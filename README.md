# Cargar VARIAS Capas Base
## Ya hemos visto como cargar UNA sola capa base, sin embargo, dependiendo de las necesidades nuestras y de los usuarios del mapa, será muy común tener que incluir mas de una capa base. En este video describiremos la metodología a seguir.
### Primero Ingresaremos nuevamente al catálogo de capas base, en la siguiente página https://leaflet-extras.github.io/leaflet-providers/preview/ 

![screenshot](https://raw.githubusercontent.com/sampach95/CargarVARIASCapasBase/master/img/catalogo.png)

### Seleccionaremos una o dos capas más aparte de la que incluimos previamente. En mi caso seleccione la capa de OSM de Topografía y la capa de ESRI de imágenes de satélite, copiamos las líneas de código correspondientes y pegamos en el archivo HTML de nuestro proyecto.

``` html
	var topo = L.tileLayer('https://{s}.tile.opentopomap.org/{z}/{x}/{y}.png', {
	maxZoom: 17,
	attribution: 'Map data: &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, <a href="http://viewfinderpanoramas.org">SRTM</a> | Map style: &copy; <a href="https://opentopomap.org">OpenTopoMap</a> (<a href="https://creativecommons.org/licenses/by-sa/3.0/">CC-BY-SA</a>)'
	}); 
	topo.addTo(map);
	
	var sat = L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}', {
	attribution: 'Tiles &copy; Esri &mdash; Source: Esri, i-cubed, USDA, USGS, AEX, GeoEye, Getmapping, Aerogrid, IGN, IGP, UPR-EGP, and the GIS User Community'
	});
```

## De esta manera ya tendríamos las capas incluidas en nuestro mapa, faltaría añadir el controlador que nos permita cambiar de una a otra.
### Para esto declararemos una nueva variable llamada “ basemaps”, en ella incluiremos:
- el  nombre o la etiqueta que queremos que aparezca en el controlador, seguido de dos puntos, 
- el nombre de la variable que contiene a la capa base declarada anteriormente.
Esto nos permite agrupar todas nuestras capas, posteriormente utilizamos el comando de leflet
- **L.control.layers,** que nos permite enlistar en el controlador todas nuestras capas base y poder activar y desactivarlas
Finalmente añadimos al mapa.

``` html
	var basemaps = {
		"OSM": osm,
		"Topografía": topo,										
		"Satélite": sat
		};
	L.control.layers(basemaps).addTo(map);
```
## Nuestro codigo completo debería parecerce a lo siguiente
``` html
<html>
<head>
	<meta charset="utf-8">
	<title>Mapa E14C17_2</title>
	<link rel="stylesheet" href="https://unpkg.com/leaflet@1.6.0/dist/leaflet.css"
  integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
  crossorigin=""/>
	<script src="https://unpkg.com/leaflet@1.6.0/dist/leaflet.js"
  integrity="sha512-gZwIG9x3wUXg2hdXF6+rVkLF/0Vi9U8D2Ntg4Ga5I5BZpVkVxlJWbSQtXPSiUTtC0TjtGOmxa1AJPuV0CPthew=="
  crossorigin=""></script>
	<style>
	#mapDIV {
	height: 100%;
	width: 100%;
	border: solid 2px black;
	}
	</style>
</head>
<body>
<div id="mapDIV"></div>

 <script>	
 var map = L.map('mapDIV', {
		center:[20.83748 , -99.71396],
		zoom:12
	});
	
	var scale = L.control.scale({
		'imperial':false
	});
	scale.addTo(map);
	
	var osm = L.tileLayer('http://a.tile.openstreetmap.org/{z}/{x}/{y}.png',
	{attribution: 'Map Data &copy; OpenStreetMap contributors'
	});
	osm.addTo(map);
	
	var topo = L.tileLayer('https://{s}.tile.opentopomap.org/{z}/{x}/{y}.png', {
	maxZoom: 17,
	attribution: 'Map data: &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, <a href="http://viewfinderpanoramas.org">SRTM</a> | Map style: &copy; <a href="https://opentopomap.org">OpenTopoMap</a> (<a href="https://creativecommons.org/licenses/by-sa/3.0/">CC-BY-SA</a>)'
	}); 
	topo.addTo(map);
	
	var sat = L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}', {
	attribution: 'Tiles &copy; Esri &mdash; Source: Esri, i-cubed, USDA, USGS, AEX, GeoEye, Getmapping, Aerogrid, IGN, IGP, UPR-EGP, and the GIS User Community'
	});

	
	var basemaps = {
		"OSM": osm,
		"Topografía": topo,										
		"Satélite": sat
		};
	L.control.layers(basemaps).addTo(map);
	
 </script>
</body>
</html>

```


### Ejecutamos en el navegador de nuestra preferencia y podremos observar en la esquina superior izquierda, que se incluyó un nuevo botón en el que esta alojado nuestro controlador y ya podremos usarlo sin ningún problema. 
![screenshot](https://raw.githubusercontent.com/sampach95/CargarVARIASCapasBase/master/img/topo.png)
![screenshot](https://raw.githubusercontent.com/sampach95/CargarVARIASCapasBase/master/img/osm.png)
![screenshot](https://raw.githubusercontent.com/sampach95/CargarVARIASCapasBase/master/img/satelital.png)

Siguiente Tutorial https://github.com/IngGeolAsist/Puntos

Haz click en el siguiente enlace para volver a la pagina inicial https://github.com/IngGeolAsist/ComoCrearMapasEnLaWebConLeaflet
