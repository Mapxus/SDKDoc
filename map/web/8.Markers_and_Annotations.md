# MARKERS AND ANNOTATIONS

### Create Marker

To create a marker

```js
// create marker
var marker = new MapxusMap.Marker(map);
```

To bind the marker(s) with floor and building:

```js
marker.create(coordinates, map.currentFloor, map.building.id);
```

To add one marker on the map:

```js
// add a marker
var coordinates = [114.162477, 22.3046355];
```

To add multiple markes on the map:

```js
// add multi marker
var coordinates = [
  [114.162477, 22.3046355],
  [114.16069, 22.3041753],
  [114.1616664, 22.3061098],
  [114.1636925, 22.3035161]
];
```

To add a marker listener event:

```js
// marker on click event
marker.onEventListener('click', function(evt) {
  // do something or display any information
});
```

Tips:

- To add marker on a POI or on clicking a POI, you just need to use the marker function together with the Click POI or Click Map function which can return you the POI coordinates.

Example of adding markers:

<iframe src="https://bssww.mapxus.com/defineMarkerClickEvent?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/defineMarkerClickEvent?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>



## Create Custom Marker

To create custom marker you need an image url of your marker

```js
// add custom marker; parameters: Image Scale, Image URL
marker
  .setImageScale(0.25)
  .setImageUrl('https://bssww.maphive.cloud/assets/origin-marker.png');
```

Below is an example of applying a custom marker

<iframe src="https://bssww.mapxus.com/customMarkerStyle?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/customMarkerStyle?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>


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

Below is an example drawing a simple blue point on the map at Elements shopping mall in Hong Kong:

<iframe src="https://bssww.mapxus.com/drawPoint?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/drawPoint?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>


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

Below is an example drawing a simple blue line with multiple coordinates on the map at Elements shopping mall in Hong Kong:

<iframe src="https://bssww.mapxus.com/drawLine?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/drawLine?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>


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

Below is an example drawing a simple blue irregular-shaped polygon on the map at Elements shopping mall in Hong Kong:

<iframe src="https://bssww.mapxus.com/drawArea?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/drawArea?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>
