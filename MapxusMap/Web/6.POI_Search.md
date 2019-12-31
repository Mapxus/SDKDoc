# POI SEARCH

## Search by POI ID

The POI search service is used to search for a point of interest (POI, e.g. shop, restaurant…) in Mapxus Map.

```js
// POI search service
service = new MapxusMap.PoisService();
```

Mapxus provides four kinds of building search service:

- search by ID
- search by distance
- search by area
- search within building

The search by ID function let you search and locate the exact POI with the unique Mapxus POI ID.

```js
/**
 * distance search
 * params:
 * 1. poi ids
 */
service
  .searchByIds('74216', '76122')
  .then(function(res) {
    console.log(res);
  })
  .catch(function(err) {
    console.error(err);
  });
```

Below is an example showing the search of building by POI ID. Matching results are displayed in the result list, with key information of the POI including:

- Name
- Mapxus POI ID
- Mapxus Building ID
- Floor
- Coordinates

Clicking on the result will bring you to the POI directly.

<iframe src="https://bssww.mapxus.com/poisSearchByIds?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/poisSearchByIds?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>


## Search Orientation

The Orientation search service is used to search for orientation and poi near center in Mapxus Map.

```js
// POI search service
service = new MapxusMap.PoisService();
```

Mapxus provides two kinds of orientation search service:

- search by Point
- search by Polygon

```js
/**
 * search orientation and poi
 *
 *  @param angle the angle between cellphone's orientation and the north
 *  @param buildingId  within the building
 *  @param center the user's current position, [lon, lat]
 *  @param distance unit: meter, radius distance of the center point
 *  @param distanceSearchType search type enum: Point, Polygon. default Point
 *  @param floor within floor
 */
service
  .searchOrientation(
    10,
    'vivocity_foshan_d3fmv9',
    [113.1820529763915, 23.035507036556652],
    50,
    'Point',
    1
  )
  .then(function(res) {
    console.log(res);
  })
  .catch(function(err) {
    console.error(err);
  });
```

Below is an example showing the search of building by POI ID. Matching results are displayed in the result list, with key information of the POI including:

- Name
- Mapxus POI ID
- Angle
- Coordinates

Clicking on the result will bring you to the POI directly.

<iframe src="https://bssww.mapxus.com/poisSearchOrientation?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/poisSearchOrientation?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

## Search POI Category

The POI category search service is used to search for poi categories within a building or some floor in Mapxus Map.

```js
// POI search service
service = new MapxusMap.PoisService();
```

Mapxus provides two kinds of search service:

- search within building
- search within building and floor

The search by ID function let you search and locate the exact POI with the unique Mapxus POI ID.

```js
/**
 * search poi category
 * params:
 * 1. buildingId
 * 2. floor (optional)
 */
service
  .searchCategory('vivocity_foshan_d3fmv9', '1')
  .then(function(res) {
    console.log(res);
  })
  .catch(function(err) {
    console.error(err);
  });
```

Below is an example showing the search of category by building. Matching results are displayed in the result list, with key information of the POI including:

- Categories

<iframe src="https://bssww.mapxus.com/poisSearchCategory?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/poisSearchCategory?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>


## Search POI within a Certain Distance

The POI search service is used to search for a point of interest (POI, e.g. shop, restaurant…) in Mapxus Map.

```js
// buildings search service
service = new MapxusMap.BuildingsService();
```

Mapxus provides four kinds of building search service:

- global search
- search by ID
- search by distance
- search by area

The search by distance function enables you to search and locate a POI near a defined point. The searching area is a circle with the defined point as center and a self-defined radius.

```js
// search by distance parameters include keywords, center of search, distance in km
service
  .searchByDistance('starbucks', [114.16158, 22.30498], 2)
  .then(function(res) {
    console.log(res);
  })
  .catch(function(err) {
    console.error(err);
  });
```

Below is an example showing the search of POI by name within 2km from **[114.16158, 22.30498]** (i.e. Elements). Matching results are displayed in the result list, with key information of the building including:

- Name
- Mapxus POI ID
- Mapxus Building ID
- Floor
- Coordinates

Clicking on the result will bring you to the POI.

<iframe src="https://bssww.mapxus.com/poisSearchByDistance?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/poisSearchByDistance?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>



## Search POI within an Area

The POI search by Area service is used to search for a POI in Mapxus Map within a defined POI distance.

```js
// buildings search service
service = new MapxusMap.BuildingsService();
```

Mapxus provides four kinds of building search service:

- Name
- Mapxus POI ID
- Mapxus Building ID
- Floor
- Coordinates

The search by area function enables you to search and locate a building within a defined area. You should define the area with specific longitude and latitude.

```js
/**
 * bbox search
 * params:
 * 1. poi name
 * 2. bbox, array => min_lon, min_lat, max_lon, max_lat
 */
service
  .searchByBbox('starbucks', [114.15816, 22.30124, 114.16561, 22.30908])
  .then(function(res) {
    console.log(res);
  })
  .catch(function(err) {
    console.error(err);
  });
```

Below is an example showing the search of POI by name within the area within coordinates **[114.15816, 22.30124, 114.16561, 22.30908]** (area around Elements, Hong Kong). Matching results are displayed in the result list, with key information of the building including:

- Name
- Mapxus Map Building ID
- Street
- Floor List
- Coordinates

Clicking on the result will bring you to the POI.

<iframe src="https://bssww.mapxus.com/poisSearchByBbox?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/poisSearchByBbox?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>



## Search POI within a Building

The POI search service is used to search for a point of interest (POI, e.g. shop, restaurant…) in Mapxus Map.

```js
// POI search service
service = new MapxusMap.PoisService();
```

Mapxus provides four kinds of building search service:

- search by ID
- search by distance
- search by area
- search within building

The search of POI within building function let you search and locate the POI within a building by inputting POI keywords.

```js
/**
 * buildingId search
 * params:
 * 1. poi name keyword
 * 2. building id
 */
service
  .searchByBuildingId('starbucks', 'elements_hk_dc005f')
  .then(function(res) {
    console.log(res);
  })
  .catch(function(err) {
    console.error(err);
  });
```

Below is an example showing the search of POI in Elements (shopping mall in Hong Kong). Matching results are displayed in the result list, with key information of the POI including:

- Name
- Mapxus POI ID
- Mapxus Building ID
- Floor
- Coordinates

Clicking on the result will bring you to the POI directly.

<iframe src="https://bssww.mapxus.com/poisSearchByBuildingId?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

<iframe src="https://bssww.mapxus.com/poisSearchByBuildingId?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>
