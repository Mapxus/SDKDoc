# Mapxus Visual Javascript API

## 1. About Mapxus Visual

Mapxus visual SDK is a set of call interface for visual map. Developers can easily install map features in their own webpage, including adaptive interface, add popups information, add tags information, etc. 

## 2. Install Visual

### 2.1 SDK CSS Address

```html
https://service.mapxus.com/bvs/mapxus-visual-1.4.0.css
```

### 2.2 SDK JS Address

```html
https://service.mapxus.com/bvs/mapxus-visual-1.4.0.js
```

### 2.3 Import SDK to Your Html

```html
<link href='https://service.mapxus.com/bvs/mapxus-visual-1.4.0.css' rel='stylesheet' />
<script src='https://service.mapxus.com/bvs/mapxus-visual-1.4.0.js'></script>
```

### 2.4 Create Page Container

```html
<div id="viewer"></div>
```

### 2.5 Create Page Container Style

```html
<style>
	body { 
		margin: 0; 
		padding: 0; 
	}
	html, body, #viewer { 
		height: 100%; 
	}
</style>
```

## 3. Create Your First Visual Map

```js
var baseOption = {
	appId: '<your_app_id>',
	secret: '<your_secret>',
	container: '<html Container id>',
}
/**
 * if need to default specify init image id
 * else should be ignore `imageId and component.cover = false`
 */
var specifyInitImageOption = {
	appId: '<your_app_id>',
	secret: '<your_secret>',
	container: '<html Container id>',
	imageId: '<image id>',
	component: {
		cover: false,
	}
}
// Init. Mapxus Visual Viewer
var viewer = new MapxusVisual.Viewer(baseOption);
```

## 3.1 Close Cache Component

```js
var baseOption = {
	appId: '<your_app_id>',
	secret: '<your_secret>',
	container: '<html Container id>',
	imageId: '<image id>',
	component: {
		cache: false,
		cover: false,
	}
}
// Init. Mapxus Visual Viewer
var viewer = new MapxusVisual.Viewer(baseOption);
```

### OR

```js
viewer.deactivateComponent('cache');
```

## 4. Event Listeners

### 4.1 Load Viewer Complete

```js
viewer.renderComplete(function() {
	// TODO
});
```

### 4.2 Bearing Changed

```js
viewer.on(MapxusVisual.Viewer.bearingchanged, function() {
	// TODO
});
```

### 4.3 Context Menu

```js
viewer.on(MapxusVisual.Viewer.contextmenu, function() {
	// TODO
});
```

### 4.4 Double click

```js
viewer.on(MapxusVisual.Viewer.dblclick, function() {
	// TODO
});
```

### 4.5 Loading Changed

```js
viewer.on(MapxusVisual.Viewer.loadingchanged, function() {
	// TODO
});
```

### 4.6 Mouse Down

```js
viewer.on(MapxusVisual.Viewer.mousedown, function() {
	// TODO
});
```

### 4.7 Mouse Move

```js
viewer.on(MapxusVisual.Viewer.mousemove, function() {
	// TODO
});
```

### 4.8 Mouse Out

```js
viewer.on(MapxusVisual.Viewer.mouseout, function() {
	// TODO
});
```

### 4.9 Mouse Over

```js
viewer.on(MapxusVisual.Viewer.mouseover, function() {
	// TODO
});
```

### 4.10 Mouse Up

```js
viewer.on(MapxusVisual.Viewer.mouseup, function() {
	// TODO
});
```

### 4.11 Move End

```js
viewer.on(MapxusVisual.Viewer.moveend, function() {
	// TODO
});
```

### 4.12 Move Start

```js
viewer.on(MapxusVisual.Viewer.movestart, function() {
	// TODO
});
```

### 4.13 Node Changed

```js
viewer.on(MapxusVisual.Viewer.nodechanged, function() {
	// TODO
});
```

### 4.14 Pan Changed

```js
viewer.on(MapxusVisual.Viewer.panchanged, function() {
	// TODO
});
```

### 4.15 Pan Without Inertia Changed

```js
viewer.on(MapxusVisual.Viewer.panwithoutinertiachanged, function() {
	// TODO
});
```

## 5. Search Data API

### 5.1 Search Buildings By Id

```js
// buildingId typeof string. eq => 'k11_hk_59f074'
viewer.searchBuildingsById(buildingId).then(function(result) {
	// TODO
});
```

### 5.2 Search dates By building id

```js
// buildingId typeof string. eq => 'k11_hk_59f074'
viewer.searchDatesByBuildingId(buildingId).then(function(result) {
	// TODO
});
```

## 6. Move Position

### 6.1 Move to image id

```js
// imageId typeof string. eq => '0024795a635ee2b0cb500cac392c28fb'
// date typeof number (optional). eq => 20190101
viewer.moveToKey(imageId).then(function(result) {
	// TODO
});
```

### 6.2 Move to coordinate

```js
// lat typeof number. eq => 22.297619444444447
// lon typeof number. eq => 114.17366111111112
// floor typeof string. eq => 'L1'
// buildingIf typeof string. eq => 'k11_hk_59f074'
// distance typeof number (optional). eq => 1
// date typeof number (optional). eq => 20190101
viewer.moveCloseTo(lat, lon, floor, buildingId).then(function(result) {
	// TODO
});
```

## 7. Change Camera

### 7.1 Set the photo's current zoom level

```js
// zoom typeof number. eq => 2
viewer.setZoom(zoom);
```

### 7.2 Set the photo's pan to bearing

```js
// bearing typeof number. eq => 90
// the angle (0 - 360)
viewer.setBearing(bearing);
```

### 7.3 Set the basic coordinates of the current photo to be in the center of the viewport

```js
// center typeof number[x: number, y: number]. eq => [0.5, 0.5]
viewer.setCenter(center);
```

## 8. Resize Window Size

```js
viewer.resize();
```

## 9. Refresh Token

As long as the user is always online, the authorization information will be automatically refreshed after it expires, and the last failed request will be restored.