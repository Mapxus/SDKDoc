# BUILDING SEARCH

The building search service is used to search for a building in Mapxus Map.

```js
// buildings search service
service = new MapxusMap.BuildingsService();
```

Mapxus provides four kinds of building search service:

- global search
- search by ID
- search by distance
- search by area


## Global Search

You may perform a global search of buildings by **building name**.

```js
// buildings global search
service.searchByGlobal(value);
```

Returned Values:

- Name
- Mapxus Map Building ID
- Street
- Floor List
- Coordinates

Import bootstrap stylesheet(Optional):

```js
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/4.0.0/css/bootstrap.min.css">
```

Click on Search button to show the result:

<script async src="//jsfiddle.net/Mapxus/c2pz7q0b/embed/result,js,css,html/"></script>


## Search by Building ID

The search by building ID function enables you to search and locate a building directly if you have the Mapxus building Id.

```js
var ids = ['elements_hk_dc005f', 'k11_hk_59f074'];
// search by ID in an array of parameters
service
  .searchByIds(ids.join(','))
  .then(function(res) {
    console.log(res);
  })
  .catch(function(err) {
    console.error(err);
  });
```

For Instance,

- Building ID of Elements is **elements_hk_dc005f**
- Building ID of K11 is **k11_hk_59f074**

Returned Values:

- Name
- Mapxus Map Building ID
- Street
- Floor List
- Coordinates


Import bootstrap stylesheet(Optional):

```js
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/4.0.0/css/bootstrap.min.css">
```

Click on Search button to show the result:

<script async src="//jsfiddle.net/Mapxus/0ym9fp1t/embed/result,js,css,html/"></script>


## Search Building within a Certain Distance

The search by distance function enables you to search and locate a building near a defined point.

The searching area is a circle with the defined point as center and a self-defined radius.

```js
// search by distance parameters include keywords, center of search, distance in km
service
  .searchByDistance('elements', [114.16158, 22.30498], 40)
  .then(function(res) {
    console.log(res);
  })
  .catch(function(err) {
    console.error(err);
  });
```

Below is an example showing the search of building by name within 40km from **[114.16158, 22.30498]** (i.e. Elements).

Returned Values:

- Name
- Mapxus Map Building ID
- Street
- Floor List
- Coordinates

Import bootstrap stylesheet(Optional):

```js
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/4.0.0/css/bootstrap.min.css">
```

Click on Search button to show the result:

<script async src="//jsfiddle.net/Mapxus/zb9uq7a1/embed/result,js,css,html/"></script>


## Search Building within an Area

The search by area function enables you to search and locate a building within a defined area.

You should define the area with specific longitude and latitude.

```js
/**
 * bbox search
 * params:
 * 1. building name
 * 2. bbox, array => min_lon, min_lat, max_lon, max_lat
 */
service
  .searchByBbox('elements', [
    114.15709623420952,
    22.293868759302995,
    114.17050186124692,
    22.308570524727344
  ])
  .then(function(res) {
    console.log(res);
  })
  .catch(function(err) {
    console.error(err);
  });
```

Below is an example showing the search of building by name within the area within coordinates **[114.15709623420952, 22.293868759302995, 114.17050186124692, 22.308570524727344]** (area around Tsim Sha Tsui, Hong Kong).

Returned Values:

- Name
- Mapxus Map Building ID
- Street
- Floor List
- Coordinates


Import dependencies(Optional):

```js
<script src='https://npmcdn.com/@turf/turf/turf.min.js'></script>
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/4.0.0/css/bootstrap.min.css">
```

Click on Search button to show the result:

<script async src="//jsfiddle.net/Mapxus/a2ns9fe4/embed/result,js,css,html/"></script>
