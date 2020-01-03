# WAYFINDING

## Point to point pathway

Mapxus Map allows point to point route planning.

```js
// route planning service
var routeService = new MapxusMap.RouteService();
var fromCoord = [113.18279, 23.03523];
var toCoord = [113.18215, 23.03587];
var fromBuildingId = 'vivocity_foshan_d3fmv9';
var toBuildingId = 'vivocity_foshan_d3fmv9';
var fromFloor = 'B1';
var toFloor = '3';
// point to point route planning; parameters include fromCoord, toCoord, fromBuildingId, toBuildingId, fromFloor, toFloor
routeService
  .search(fromCoord, toCoord, fromBuildingId, toBuildingId, fromFloor, toFloor)
  .then(function(res) {
    console.log(res);
  })
  .catch(function(err) {
    console.error(err);
  });
```

Import dependencies:

```js
<script src='https://cdn.jsdelivr.net/npm/lodash@4.17.10/lodash.min.js'></script>
<script src='https://cdn.bootcss.com/jquery/3.2.1/jquery.slim.min.js'></script>
```
Below an example showing the wayfinding function:

- You car type keywords of any POI in the searching bar and select your starting point (A)
- OR you can click on the people icon on the right to the searching bar and click on the map to select the starting point directly. Ending point (B) as well.
- Click the “Planning” button to search and display the route.

<script async src="//jsfiddle.net/Mapxus/q0yn84ft/embed/result,js,css,html/"></script>
