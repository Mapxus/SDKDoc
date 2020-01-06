# Map Controllers

## Floor Controller

The floor controlleris displayed at the top-right of the map by default.

* To disable the floor controller at map initialization:

```js
// init mapxus map
var map = new MapxusMap.Map({
  map: mapbox,
  appId: 'your_appId',
  secret: 'your_secret',
  buildingId: 'elements_hk_dc005f',
  enableFloorControl: false
});
```

* Upon map render complete, to disable/enable the floor controller you may use:

```js
map.disableFloorControl();

map.enableFloorControl();
```

* You can choose where to put the floor controller.

```
options('top-left', 'top-right', 'bottom-left', 'bottom-right')
```

e.g.

```js
map.enableFloorControl('top-left');
```

<script async src="//jsfiddle.net/Mapxus/gc2Lywq9/embed/result,js,css,html/"></script>



## Building Selector

The building selector is displayed at the top-right of the map by default.

* To disable the building selector at map initialization:

```js
// init mapxus map
var map = new MapxusMap.Map({
  map: mapbox,
  appId: 'your_appId',
  secret: 'your_secret',
  buildingId: 'elements_hk_dc005f',
  enableBuildingSelector: false
});
```

* Upon map render complete, to disable/enable the building selector you may use:

```js
map.disableBuildingSelector();

map.enableBuildingSelector();
```

* You can choose where to put the building selector:

```
options('top-left', 'top-right', 'bottom-left', 'bottom-right')
```

e.g.

```js
map.enableBuildingSelector('top-left');
```

<script async src="//jsfiddle.net/Mapxus/q2dshkL5/embed/result,js,css,html/"></script>



## Map Scale Controller

The map scale shows the scale at the current map zoom level. The map scale is not displayed by default.

* To display the map scale controller:

```js
// mapboxgl listener
mapbox.on('load', function() {
  // add scale control, position in 'bottom-right'
  mapbox.addControl(new mapboxgl.ScaleControl(), 'bottom-right');
});
```

* You can choose where to put the map scale on the map:

```js
options（'top-left', 'top-right', 'bottom-left', 'bottom-right'）
```

e.g.

```js
mapbox.addControl(new mapboxgl.ScaleControl(), 'bottom-right');
```

<script async src="//jsfiddle.net/Mapxus/pLkdesr3/embed/result,js,css,html/"></script>


## Map Zoom and Compass Controller

The map scale shows the scale at the current map zoom level. The map scale is not displayed by default.

* To display the zoom and compass controller:

```js
// mapboxgl listener
mapbox.on('load', function() {
  // add navigation control
  mapbox.addControl(new mapboxgl.NavigationControl());
});
```

* The zoom and compass controller is displayed at the top-right of the map. You can also choose where to put the map scale controller on the map:

```js
options('top-left', 'top-right', 'bottom-left', 'bottom-right');
```

e.g.

```js
mapbox.addControl(new mapboxgl.NavigationControl(), 'bottom-right');
```

<script async src="//jsfiddle.net/Mapxus/0a7z3vgk/embed/result,js,css,html/"></script>
