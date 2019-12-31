# CAMERA

## Tilt and Rotate Map

To set default tilt degree:

```js
// tilt in degrees
pitch: 60,
```

To set default map rotation angle:

```js
// rotation angle in degrees
bearing: -60,
```

To disable the map tilt and rotation action:

```js
// use mapbox dragRotate property
mapbox.dragRotate.disable();
```

Below is an example you may enable/disable the map tilt and rotation action.

<iframe src="https://bssww.mapxus.com/dragRotateHandler?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/dragRotateHandler?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>



## Move Map

To lock the map / disable the moving of the map by dragging:

```js
// use mapbox dragPan property
mapbox.dragPan.disable();
```

Below is an example you may enable/disable the map move by dragging action.

<iframe src="https://bssww.mapxus.com/dragPanHandler?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/dragPanHandler?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>


## Zoom Map

To disable the zooming of the map:

```js
// use mapbox scrollZoom property
mapbox.scrollZoom.disable();
```

Below is an example that you may disable/enable the zooming.

<iframe src="https://bssww.mapxus.com/scrollZoomHandler?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/scrollZoomHandler?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>


## Restrict Map Zoom Level

To set the minimum and maximum zoom level for your Mapxus map:

```js
// use mapbox setMinZoom function
mapbox.setMinZoom(16);
// use mapbox setMaxZoom function
mapbox.setMaxZoom(18);
```

Remark:

- the default zoom level of initiating Mapxus Map is level 17.

Below an example showing a minimum zoom level of 16 and maximum zoom level of 18.

<iframe src="https://bssww.mapxus.com/restrictMapZoom?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/restrictMapZoom?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>



## Restrict Map Planning

To restrict the map move within an area, input the minimum and maximum latitude, longitude like below.

```js
// use mapbox setMaxBounds function
mapbox.setMaxBounds([[114.15867, 22.30276], [114.16503, 22.30729]]);
```

Below is an example showing the restriction of map planning.

<iframe src="https://bssww.mapxus.com/restrictMapPanning?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/restrictMapPanning?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>
