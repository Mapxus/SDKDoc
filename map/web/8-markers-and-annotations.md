# MARKERS AND ANNOTATIONS

### Create Marker

* Create a marker

```js
// create marker
var marker = new MapxusMap.Marker(map);
```

* Bind the marker(s) with floor and building:

```js
marker.create(coordinates, map.currentFloor, map.building.id);
```

* Add one marker on the map:

```js
// add a marker
var coordinates = [114.162477, 22.3046355];
```

* Add multiple markes on the map:

```js
// add multi marker
var coordinates = [
  [114.162477, 22.3046355],
  [114.16069, 22.3041753],
  [114.1616664, 22.3061098],
  [114.1636925, 22.3035161]
];
```

* Add a marker listener event:

```js
// marker on click event
marker.onEventListener('click', function(evt) {
  // do something or display any information
});
```

Tips:

- To add marker on a POI or on clicking a POI, you just need to use the marker function together with the Click POI or Click Map function which can return you the POI coordinates.

Example of adding markers:

<script async src="//jsfiddle.net/Mapxus/us4bq81h/embed/result,js,css,html/"></script>


## Create Custom Marker

To create custom marker you need an image url of your marker

```js
// add custom marker; parameters: Image Scale, Image URL
marker
  .setImageScale(0.25)
  .setImageUrl('https://bssww.maphive.cloud/assets/origin-marker.png');
```

Below is an example of applying a custom marker

<script async src="//jsfiddle.net/Mapxus/9vcmzsL4/embed/result,js,css,html/"></script>


## Draw a Point on Map

On the map, you may draw:

- A point
- A line
- A polygon

To draw a point on the map, prepare the:

- Coordinates of the point
- Circle radius (if you want to draw a circle point)
- Circle color (the color of the point)

```js
// use mapbox addSource and addLayer function
var sourceId = 'myPoint';
var layerId = sourceId + 'Layer';
var coordinates = [114.16158, 22.30498];
function addSource() {
  mapbox.addSource(sourceId, {
    type: 'geojson',
    data: {
      type: 'Feature',
      geometry: {
        type: 'Point',
        coordinates: coordinates
      }
    }
  });
}
function addLayer() {
  mapbox.addLayer({
    id: layerId,
    type: 'circle',
    source: sourceId,
    paint: {
      'circle-radius': 5,
      'circle-color': '#007cbf'
    }
  });
}
```

```js
<script src="https://cdn.bootcss.com/jquery/3.2.1/jquery.slim.min.js"></script>
<script src="https://cdn.bootcss.com/bootstrap/4.0.0/js/bootstrap.min.js"></script>
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/4.0.0/css/bootstrap.min.css">

Otherwise, you can use alert() instead.
```

Below is an example drawing a simple blue point on the map at Elements shopping mall in Hong Kong:

<script async src="//jsfiddle.net/Mapxus/2ed1toqs/embed/result,js,css,html/"></script>


## Draw a Line on Map

On the map, you may draw:

- A point
- A line
- A polygon

To draw a line on the map, prepare the:

- Coordinates of the line; possible to have multiple coordinates
- Line width
- Circle color (the color of the line)

```js
// use mapbox addSource and addLayer function
var sourceId = 'myLine';
var layerId = sourceId + 'Layer';
var coordinates = [
  [114.16139, 22.30704],
  [114.15964, 22.30312],
  [114.16059, 22.30289],
  [114.1634, 22.303],
  [114.16352, 22.30652]
];
function addSource() {
  mapbox.addSource(sourceId, {
    type: 'geojson',
    data: {
      type: 'Feature',
      geometry: {
        type: 'LineString',
        coordinates: coordinates
      }
    }
  });
}
function addLayer() {
  mapbox.addLayer({
    id: layerId,
    type: 'line',
    source: sourceId,
    layout: {
      'line-join': 'round',
      'line-cap': 'round'
    },
    paint: {
      'line-color': '#007cbf',
      'line-width': 8
    }
  });
}
```

Import dependencies:

```js
<script src="https://cdn.bootcss.com/jquery/3.2.1/jquery.slim.min.js"></script>
<script src="https://cdn.bootcss.com/bootstrap/4.0.0/js/bootstrap.min.js"></script>
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/4.0.0/css/bootstrap.min.css">
```

Below is an example drawing a simple blue line with multiple coordinates on the map at Elements shopping mall in Hong Kong:

<script async src="//jsfiddle.net/Mapxus/a2ntL7ju/embed/result,js,css,html/"></script>


## Draw a Polygon on Map

On the map, you may draw:

- A point
- A line
- A polygon

To draw a polygon on the map, prepare the:

- Coordinates of the polygon; the polygon closes automatically with the first and last coordinate points
- Outline color of the polygon
- Fill color of polygon

```js
// use mapbox addSource and addLayer function
var sourceId = 'myArea';
var layerId = sourceId + 'Layer';
var coordinates = [
  [
    [114.16139, 22.30704],
    [114.15964, 22.30312],
    [114.16059, 22.30289],
    [114.1634, 22.303],
    [114.16352, 22.30652]
  ]
];
function addSource() {
  mapbox.addSource(sourceId, {
    type: 'geojson',
    data: {
      type: 'Feature',
      geometry: {
        type: 'Polygon',
        coordinates: coordinates
      }
    }
  });
}
function addLayer() {
  mapbox.addLayer({
    id: layerId,
    type: 'fill',
    source: sourceId,
    layout: {},
    paint: {
      'fill-color': '#007cbf',
      'fill-outline-color': '#ffffcc'
    }
  });
}
```

Import dependencies:

```js
<script src="https://cdn.bootcss.com/jquery/3.2.1/jquery.slim.min.js"></script>
<script src="https://cdn.bootcss.com/bootstrap/4.0.0/js/bootstrap.min.js"></script>
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/4.0.0/css/bootstrap.min.css">
```

Below is an example drawing a simple blue irregular-shaped polygon on the map at Elements shopping mall in Hong Kong:

<script async src="//jsfiddle.net/Mapxus/7sfujo3c/embed/result,js,css,html/"></script>
