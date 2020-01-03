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

Import dependencies:

```js
<script src="https://cdn.bootcss.com/jquery/3.2.1/jquery.slim.min.js"></script>
<script src="https://cdn.bootcss.com/bootstrap/4.0.0/js/bootstrap.min.js"></script>
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/4.0.0/css/bootstrap.min.css">
```

Below is an example you may enable/disable the map tilt and rotation action.

<script async src="//jsfiddle.net/Mapxus/k38pjyru/embed/result,js,css,html/"></script>



## Move Map

To lock the map / disable the moving of the map by dragging:

```js
// use mapbox dragPan property
mapbox.dragPan.disable();
```

Import dependencies:

```js
<script src="https://cdn.bootcss.com/jquery/3.2.1/jquery.slim.min.js"></script>
<script src="https://cdn.bootcss.com/bootstrap/4.0.0/js/bootstrap.min.js"></script>
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/4.0.0/css/bootstrap.min.css">
```


Below is an example you may enable/disable the map move by dragging action.

<script async src="//jsfiddle.net/Mapxus/863hdqw2/embed/result,js,css,html/"></script>



## Zoom Map

To disable the zooming of the map:

```js
// use mapbox scrollZoom property
mapbox.scrollZoom.disable();
```

Import dependencies:

```js
<script src="https://cdn.bootcss.com/jquery/3.2.1/jquery.slim.min.js"></script>
<script src="https://cdn.bootcss.com/bootstrap/4.0.0/js/bootstrap.min.js"></script>
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/4.0.0/css/bootstrap.min.css">
```


Below is an example that you may disable/enable the zooming.

<script async src="//jsfiddle.net/Mapxus/vjamph0k/embed/result,js,css,html/"></script>



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

<script async src="//jsfiddle.net/Mapxus/k6cj8pyq/embed/result,js,css,html/"></script>


## Restrict Map Planning

To restrict the map move within an area, input the minimum and maximum latitude, longitude like below.

```js
// use mapbox setMaxBounds function
mapbox.setMaxBounds([[114.15867, 22.30276], [114.16503, 22.30729]]);
```

Below is an example showing the restriction of map planning.

<script async src="//jsfiddle.net/Mapxus/5voerady/embed/result,js,css,html/"></script>
