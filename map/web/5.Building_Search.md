# BUILDING SEARCH

## Global Search

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

You may perform a global search of buildings by building name.

```js
// buildings global search
service.searchByGlobal(value);
```

Below is an example showing the Mapxus global search of building by name. Matching results are displayed in the result list, with key information of the building including:

- Name
- Mapxus Map Building ID
- Street
- Floor List
- Coordinates

Clicking on the result will bring you to the building.

<iframe src="https://bssww.mapxus.com/buildingsSearchByGlobal?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/buildingsSearchByGlobal?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>



## Search by Building ID

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

The search by ID function enables you to search and locate a building directly if you have the Mapxus building Id.

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

Below is an example showing the search of building by Mapxus building ID. Matching results are displayed in the result list, with key information of the building including:

- Name
- Mapxus Map Building ID
- Street
- Floor List
- Coordinates

Clicking on the result will bring you to the building.

<iframe src="https://bssww.mapxus.com/buildingsSearchByIds?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/buildingsSearchByIds?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>



## Search Building within a Certain Distance

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

The search by distance function enables you to search and locate a building near a defined point. The searching area is a circle with the defined point as center and a self-defined radius.

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

Below is an example showing the search of building by name within 40km from **[114.16158, 22.30498]** (i.e. Elements). Matching results are displayed in the result list, with key information of the building including:

- Name
- Mapxus Map Building ID
- Street
- Floor List
- Coordinates

Clicking on the result will bring you to the building.

<iframe src="https://bssww.mapxus.com/buildingsSearchByDistance?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/buildingsSearchByDistance?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>



## Search Building within an Area

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

The search by area function enables you to search and locate a building within a defined area. You should define the area with specific longitude and latitude.

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

Below is an example showing the search of building by name within the area within coordinates **[114.15709623420952, 22.293868759302995, 114.17050186124692, 22.308570524727344]** (area around Tsim Sha Tsui, Hong Kong). Matching results are displayed in the result list, with key information of the building including:

- Name
- Mapxus Map Building ID
- Street
- Floor List
- Coordinates

Clicking on the result will bring you to the building.

E.g. search

- Elements
- 中港城

<iframe src="https://bssww.mapxus.com/buildingsSearchByBbox?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/buildingsSearchByBbox?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>
