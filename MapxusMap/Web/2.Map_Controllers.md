# Map Controllers

## Floor Controller

The floor controller and building selector are displayed by default at the top-right of the map. To disable the floor controller at map initialization:

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

Upon map render complete, to disable/enable the floor controller you may use:

```js
map.disableFloorControl();
```

```js
map.enableFloorControl();
```

You can choose where to put the floor controller, by default it is located at the top-right of the map.

```
options('top-left', 'top-right', 'bottom-left', 'bottom-right')
```

e.g.

```js
map.enableFloorControl('top-left');
```

Below an example disabling the floor controller:

<iframe src="https://bssww.mapxus.com/floorsControl?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/floorsControl?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>


## Building Selector

The floor controller and building selector are displayed by default at the top-right of the map. To disable the building selector at map initialization:

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

Upon map render complete, to disable/enable the building selector you may use:

```js
map.disableBuildingSelector();
```

```js
map.enableBuildingSelector();
```

You can choose where to put the building selector, by default it is located at the top-right of the map.

```
options('top-left', 'top-right', 'bottom-left', 'bottom-right')
```

e.g.

```js
map.enableBuildingSelector('top-left');
```

<iframe src="https://bssww.mapxus.com/buildingFilterControl?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/buildingFilterControl?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>


## Map Scale Controller

The map scale shows the scale at the current map zoom level. The map scale is not displayed by default, to add:

```js
// mapboxgl listener
mapbox.on('load', function() {
  // add scale control, position in 'bottom-right'
  mapbox.addControl(new mapboxgl.ScaleControl(), 'bottom-right');
});
```

You can choose where to put the map scale on the map:

```js
options（'top-left', 'top-right', 'bottom-left', 'bottom-right'）
```

e.g.

```js
mapbox.addControl(new mapboxgl.ScaleControl(), 'bottom-right');
```

<iframe src="https://bssww.mapxus.com/scaleControl?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/scaleControl?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>


## Map Zoom and Compass Controller

The map scale shows the scale at the current map zoom level. The map scale is not displayed by default, to add:

```js
// mapboxgl listener
mapbox.on('load', function() {
  // add navigation control
  mapbox.addControl(new mapboxgl.NavigationControl());
});
```

By default when you add the map zoom and compass controller it is put at the top-right of the map. You can also choose where to put the map scale on the map:

```js
options('top-left', 'top-right', 'bottom-left', 'bottom-right');
```

e.g.

```js
mapbox.addControl(new mapboxgl.NavigationControl(), 'bottom-right');
```

<iframe src="https://bssww.mapxus.com/navigationControl?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/navigationControl?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>
