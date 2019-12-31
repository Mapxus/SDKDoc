# MAP EVENT LISTENERS

## Load Map Complete

You may trigger an action upon map preparation complete, e.g. adding a pop-up, marker or action, etc.

```js
// mapxus load map listener
map.renderComplete(function() {
  // do something
});
```

Below is an example displaying a pop-up message when map preparation is completed.

<iframe src="https://bssww.mapxus.com/loadMapListener?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/loadMapListener?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>


## Click POI

You may trigger an action upon clicking on a point of interest (POI), e.g. adding a pop-up, marker or action, etc.

```js
// poi click event
map.onIndoorPoiListener(function(evt) {
  // do something
});
```

For instance you may use mapbox popup function to display the POI information upon clicking on a POI. Contents can be

```js
// poi click event
map.onIndoorPoiListener(function(evt) {
  // use mapbox popup function to display
  new mapboxgl.Popup()
    .setLngLat(evt.lngLat)
    .setHTML('name: ' + evt.feature.properties.name)
    .addTo(mapbox);
});
```

Try to click on the POI of below Mapxus map example to get the on-click POI pop-up message.

<iframe src="https://bssww.mapxus.com/poiClickEvent?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/poiClickEvent?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>


## Click Map

You may trigger an action upon clicking on any point of the map, e.g. calling back the detailed coordinates and floor information, adding a pop-up, marker or action, etc.

```js
// map click event
map.onMapClickListener(function(event) {
  // do something
});
```

For instance you may display a bootstrap modal dialog box/pop-up window upon clicking anywhere on the map.

```js
// map click event
map.onMapClickListener(function(event) {
  var result = {
    floor: map.currentFloor,
    lat: event.lngLat.lat,
    lon: event.lngLat.lng
  };
  $('code').text(JSON.stringify(result, null, 2));
  $('.modal').modal('show');
});
```

Try to click anywhere on below Mapxus map example to get the on-click map pop-up message.

<iframe src="https://bssww.mapxus.com/mapClickEvent?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:
<iframe src="https://bssww.mapxus.com/mapClickEvent?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>



## Switch Floor

You may trigger an action upon switching floor of an indoor map, e.g. calling back the detailed coordinates and floor information, adding a pop-up, marker or action, etc.

```js
// switch floor event
map.onFloorChangeListener(function(evt) {
  // do something
});
```

For instance you may display a bootstrap modal dialog box/pop-up window upon floor switch:

```js
// switch floor event
map.onFloorChangeListener(function(evt) {
  $('code').text(JSON.stringify(evt, null, 2));
  $('.modal').modal('show');
});
```

Try to go to different floors with the floor controller on below Mapxus map example to get the floor change pop-up message.

<iframe src="https://bssww.mapxus.com/floorChangeEvent?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/floorChangeEvent?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>
