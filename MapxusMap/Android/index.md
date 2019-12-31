# MapxusMap Android SDK Instruction

## 1. About Mapxus Map

Mapxus Map SDK is a set of call interface for developing indoor map. Developers can easily install map features in their own Android application, including displaying map, changing map style, map events, drawing on the map, searching building, searching POI, route planning, etc.


### 1.1 Minimum Android Version

The Mapxus Map SDK for Android is deployed on Android 4.4 and above.

Notice: 

**When using Mapxus Map 3.0.0 and above version, please use Mapxus Positioning Map 0.4.0 and above version if you need to use Mapxus Positioning Map.** 

**When using Mapxus Map 2.4.1 and above version, please use Mapxus Positioning Map 0.3.7 and above version if you need to use Mapxus Positioning Map.** 

**When using Mapxus Map 2.3.3-beta and above version, please use Mapxus Positioning Map 0.3.6 and above version if you need to use Mapxus Positioning Map.**

### 1.2 Get an API key

Please contact us for api Key and secret。

## 2. Install Mapxus Map SDK

### 2.1 Create a Project

First of all, please create a project for your APP. Then, integrate your SDK through the following steps.

#### 2.1.1 Add jcenter repository


```java

allprojects {
    repositories {
        jcenter()
    }
}

```
#### 2.1.2 Add Dependencies

Add dependencies in your **build.gradle** in app

```java

dependencies { 
 ...

 // MapxusMap
    implementation "com.mapxus.map:mapxusmap:3.2.0"

    //mapbox
    implementation "com.mapbox.mapboxsdk:mapbox-android-sdk:7.3.2"

 ...
}	

```



#### 2.1.3 Set Java 8 Support

Please refer to Google about Java 8 language documentation and set Java 8 Support. 
[https://developer.android.com/studio/write/java8-support](https://developer.android.com/studio/write/java8-support)


#### 2.1.4 Prevent Obfuscation

Please configurate these in ProGuard to avoid obfuscation:

```
-keep class com.mapxus.map.** {*;}
-keep class com.mapxus.services.** {*;}
-dontwarn com.mapxus.map.**
-dontwarn com.mapxus.services.**

```


#### 2.1.5 Set Key and Secret

There are two options to set your api key and secret:

##### Option One:

1. Add them in onCreate() Method of BaseApplication

```java
	MapxusMapContext.init(getApplicationContext());
```

2. Configure the following codes in AndroidManifest.xml:

``` java
	<meta-data
	        android:name="com.mapxus.api.v1.appid"
	        android:value="acquiredkey" />
	<meta-data
	    android:name="com.mapxus.api.v1.secret"
	    android:value="acquiredsecret" />
```

##### Option Two:

Add them in onCreate() Method of BaseApplication

``` java
	MapxusMapContext.init(getApplicationContext()，Key，secret);
```

### 2.2 Create Your First Map
	
#### 2.2.1 Add Your Map in Activity Application

First of all, add Mapbox Map controllers in the layout xml file:

```xml
      <com.mapbox.mapboxsdk.maps.MapView
        android:id="@+id/mapView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:mapbox_cameraTargetLat="22.304716516178253"
        app:mapbox_cameraTargetLng="114.16186609400843"
        app:mapbox_cameraZoom="17" />
```

Then, add map codes as follows in Activity file:

```java

    public class SimpleMapViewActivity extends AppCompatActivity {

    private MapView mapView;
    private MapViewProvider mapViewProvider;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_basic_simple_mapview);
        mapView = (MapView) findViewById(R.id.mapView);
        mapView.onCreate(savedInstanceState);
        mapViewProvider = new MapboxMapViewProvider(this, mapView);
    }

    // Add the mapView lifecycle to the activity's lifecycle methods
    @Override
    public void onResume() {
        super.onResume();
        mapView.onResume();
    }

    @Override
    protected void onStart() {
        super.onStart();
        mapView.onStart();
    }

    @Override
    protected void onStop() {
        super.onStop();
        mapView.onStop();
    }

    @Override
    public void onPause() {
        super.onPause();
        mapView.onPause();
    }

    @Override
    public void onLowMemory() {
        super.onLowMemory();
        mapView.onLowMemory();
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        mapView.onDestroy();
        mapViewProvider.onDestroy();
    }

    @Override
    protected void onSaveInstanceState(Bundle outState) {
        super.onSaveInstanceState(outState);
        mapView.onSaveInstanceState(outState);
    }
	}
```

Please be aware that maps lifecycle requires reasonable management during using map in your project.

![image](https://service.mapxus.com/dpw/api/v1/image/digitalMap/android/3.1.0/Getting_started1.png)

#### 2.2.2 Display Map by Fragment

Add SupportMapxusMapFragment in Activity file:

```java

    SupportMapxusMapFragment mapFragment;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_basic_support_map_frag);
        if (savedInstanceState == null) {
            // Create fragment
            final FragmentTransaction transaction = getSupportFragmentManager().beginTransaction();
            MapboxMapOptions options = new MapboxMapOptions();
            options.camera(new CameraPosition.Builder()
                    .target(LatLngConstant.ELEMENT_LATLON)
                    .zoom(17)
                    .build());

            MapView mapView = new MapView(SupportMapFragmentActivity.this, options);
            // Create map fragment
            mapFragment = SupportMapxusMapFragment.newInstance(mapView);
            // Add map fragment to parent container
            transaction.add(R.id.container, mapFragment, "com.mapxus.map");
            transaction.commit();
        } else {
            mapFragment = (SupportMapxusMapFragment) getSupportFragmentManager().findFragmentByTag("com.mapxus.map");
        }
    }
```
![image](https://service.mapxus.com/dpw/api/v1/image/digitalMap/android/3.1.0/Getting_started2.png)

#### 2.2.3 Create Dynamic Map

Add MapView in Activity file:

```java
    private MapViewProvider mapViewProvider;
    private MapView mapboxMapView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        // create mapbox map
        MapboxMapOptions mapboxMapOptions = new MapboxMapOptions();
        mapboxMapOptions.camera(new CameraPosition.Builder().target(LatLngConstant.ELEMENT_LATLON).zoom(17).build());
        mapboxMapView = new MapView(this, mapboxMapOptions);
        mapboxMapView.onCreate(savedInstanceState);
        mapViewProvider = new MapboxMapViewProvider(this, mapboxMapView);
        setContentView(mapboxMapView);
    }
```
![image](https://service.mapxus.com/dpw/api/v1/image/digitalMap/android/3.1.0/Getting_started3.png)

#### 2.2.4 Create Your Map with Particular buildingId and floor

Add MapView in Activity file:

```java

    private MapViewProvider mapViewProvider;
    private MapView mapboxMapView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_basic_init_with_building);
        mapboxMapView = (MapView) findViewById(R.id.mapView);
        MapxusMapOptions mapxusMapOptions = new MapxusMapOptions().setBuildingId("elements_hk_dc005f").setFloor("L2");
        mapViewProvider = new MapboxMapViewProvider(this, mapboxMapView, mapxusMapOptions);
    }
```

#### 2.2.5 Create Your Map with Particular POI

Add MapView in Activity file:

```java

    private MapViewProvider mapViewProvider;
    private MapView mapboxMapView;
    private static final String POI_ID = "74233";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_basic_init_with_building);
        mapboxMapView = (MapView) findViewById(R.id.mapView);
        MapxusMapOptions mapxusMapOptions = new MapxusMapOptions().setPoiId(POI_ID);
        mapViewProvider = new MapboxMapViewProvider(this, mapboxMapView, mapxusMapOptions);
    }
```



## 3.SDK Features

### 3.1 Map Controllers

Controllers refer to components displaying above the map with the function of operating maps, such as floor selector, etc. MapxusUiSettings class is used to manage these controllers so as to tailor your map view. MapxusUiSettings could be instantiated by MapxusMap. 

``` java
     mapViewProvider.getMapxusMapAsync(new OnMapxusMapReadyCallback() {
            @Override
            public void onMapxusMapReady(MapxusMap mapxusMap) {
            	MapxusUiSettings mapxusUiSettings = mapxusMap.getMapxusUiSettings();
            }
    }
```

#### 3.1.1 Selector

Selector is a button for APP users to alter displaying or hiding floor selecting list and building selecting list on the map. It is on (displaying) by default but you can hide it by the following interface: 


```java
mapxusUiSettings.setSelectorEnabled(false);
```

#### 3.1.2 Building Selector

Building selector allows APP users to decide whether displaying building selecting list on the map or not. It is on (displaying) by default but you can hide it by this interface:

```java
mapxusUiSettings.setBuildingSelectorEnabled(false);
```

### 3.2 Map Events

#### 3.2.1 Change Building Listener

```java
mapxusMap.addOnBuildingChangeListener(new MapxusMap.OnBuildingChangeListener() {
            @Override
            public void onBuildingChange(IndoorBuilding indoorBuildingInfo) {
                
            }
        });
```
#### 3.2.2 Change Floor Listener

```java

mapxusMap.addOnFloorChangeListener(new MapxusMap.OnFloorChangeListener() {
            @Override
            public void onFloorChange(IndoorBuilding indoorBuilding, String floor) {
                
            }
        });
    }
```

#### 3.2.3 Click Indoor POI Listener

Click on the map and listen to the change of POI position:

```java
     @Override
    public void onMapxusMapReady(MapxusMap mapxusMap) {

        mapxusMap.addOnIndoorPoiClickListener(new MapxusMap.OnIndoorPoiClickListener() {
            @Override
            public void onIndoorPoiClick(Poi poi) {

                String message = String.format(getString(R.string.click_poi_message), poi.getName());

                poiClickTv.setText(message);
            }
        });
    }
```

### 3.3 Draw on the Map

#### 3.3.1 Draw a Marker

A marker can mark any site containing position information on the map, such as user position, car position, store position, etc.
When creating a marker, you can set its buildingID and floor. In this case, the marker is only displayed with corresponding building and floor.
To draw a marker:

```java 
     mapViewProvider.getMapxusMapAsync(new OnMapxusMapReadyCallback() {
            @Override
            public void onMapxusMapReady(MapxusMap mapxusMap) {

                MapxusMarkerOptions mapxusMarkerOptions = new MapxusMarkerOptions();
                mapxusMarkerOptions.setPosition(new LatLng(LatLngConstant.ELEMENT_LATLON.getLatitude(), LatLngConstant.ELEMENT_LATLON.getLongitude()));
                mapxusMarkerOptions.setFloor("3");
                mapxusMarkerOptions.setBuildingId("elements_hk_dc005f");


                MapxusMarkerOptions mapxusMarkerOptions2 = new MapxusMarkerOptions();
                mapxusMarkerOptions2.setPosition(new LatLng(22.304616516178253, 114.16176609400843)).setFloor("2");
                mapxusMarkerOptions2.setBuildingId("elements_hk_dc005f");


                MapxusMarkerOptions mapxusMarkerOptions3 = new MapxusMarkerOptions();
                mapxusMarkerOptions3.setPosition(new LatLng(22.304516516178253, 114.16186609400843));

                mapxusMap.addMarker(mapxusMarkerOptions);
                mapxusMap.addMarker(mapxusMarkerOptions2);
                mapxusMap.addMarker(mapxusMarkerOptions3);
            }
        });
```
![image](https://service.mapxus.com/dpw/api/v1/image/digitalMap/android/3.1.0/Annotations1.png)

#### 3.3.2 Draw a Customized Marker

You can specify your marker as needed.

To create a marker with custom icon:

```java
      mapViewProvider.getMapxusMapAsync(new OnMapxusMapReadyCallback() {
            @Override
            public void onMapxusMapReady(MapxusMap mapxusMap) {
                mapxusMap.addMarker(new MapxusMarkerOptions()
                        .setBuildingId("elements_hk_dc005f")
                        .setFloor("3")
                        .setPosition(new LatLng(LatLngConstant.ELEMENT_LATLON.getLatitude(),LatLngConstant.ELEMENT_LATLON.getLongitude()))
                        .setTitle(getString(R.string.draw_custom_marker_options_title))
                        .setSnippet(getString(R.string.draw_custom_marker_options_snippet))
                        .setIcon(R.drawable.purple_marker));
            }
        });
```
![image](https://service.mapxus.com/dpw/api/v1/image/digitalMap/android/3.1.0/Annotations2.png)

### 3.5 Search a Building

##### Instantiate BuildingSearch Object

```java
        buildingSearch = BuildingSearch.newInstance();
```
##### Set Search Result Listener

```java
        buildingSearch.setBuildingSearchResultListener(this);
```

#### 3.5.1 Search Nearby Building

##### 3.5.1.1 Set Parameters

```java
        NearbySearchOption nearbySearchOption = new NearbySearchOption();
        nearbySearchOption.mRadius = 2;
        nearbySearchOption.location(new LatLng(LatLngConstant.ELEMENT_LATLON.getLatitude(), LatLngConstant.ELEMENT_LATLON.getLongitude()));
        nearbySearchOption.keyword(keyWord);
        
    }
```

##### 3.5.1.2 Implement Searching

```java
buildingSearch.searchNearby(nearbySearchOption);
```
##### 3.5.1.3 Get Search Result

```java
     @Override
    public void onGetBuildingResult(BuildingResult buildingResult) {

        if (buildingResult.status != 0) {
            Toast.makeText(this, buildingResult.error.toString(), Toast.LENGTH_LONG).show();
            return;
        }
        if (buildingResult.getIndoorBuildingList() == null || buildingResult.getIndoorBuildingList().isEmpty()) {
            Toast.makeText(this, getString(R.string.no_result), Toast.LENGTH_LONG).show();
            return;
        }

        mapboxMap.clear();
        indoorBuildingOverlay = new MyIndoorBuildingOverlay(mapboxMap, buildingResult.getIndoorBuildingList());
        indoorBuildingOverlay.addToMap();
        indoorBuildingOverlay.zoomToSpan();

    }

    @Override
    public void onGetBuildingDetailResult(BuildingDetailResult buildingDetailResult) {

    }
```
![image](https://service.mapxus.com/dpw/api/v1/image/digitalMap/android/3.1.0/Search_services2.png)

#### 3.5.2 Search by Area

##### 3.5.2.1 Set Parameters

```java       
        private LatLngBounds latLngBounds;
        com.mapxus.map.model.LatLng southweast = new com.mapxus.map.model.LatLng(22.2918962, 114.1353782);
        com.mapxus.map.model.LatLng northeast = new com.mapxus.map.model.LatLng(22.3418344, 114.2089048);
        latLngBounds = new LatLngBounds(southweast, northeast);
        BoundSearchOption boundSearchOption = new BoundSearchOption();

        boundSearchOption.bound(latLngBounds);
        boundSearchOption.keyword(keyWord);

```

##### 3.5.2.2 Implement Searching

```java
        
        buildingSearch.searchInBound(boundSearchOption);
        
```

##### 3.5.2.3 Get Search Result

```java
 @Override
    public void onGetBuildingResult(BuildingResult buildingResult) {

        if (buildingResult.status != 0) {
            Toast.makeText(this, buildingResult.error.toString(), Toast.LENGTH_LONG).show();
            return;
        }
        if (buildingResult.getIndoorBuildingList() == null || buildingResult.getIndoorBuildingList().isEmpty()) {
            Toast.makeText(this, getString(R.string.no_result), Toast.LENGTH_LONG).show();
            return;
        }

        if (indoorBuildingOverlay != null) {
            indoorBuildingOverlay.removeFromMap();
            indoorBuildingOverlay = null;
        }
        indoorBuildingOverlay = new MyIndoorBuildingOverlay(mapboxMap, buildingResult.getIndoorBuildingList());
        indoorBuildingOverlay.addToMap();
        indoorBuildingOverlay.zoomToSpan();
    }

```

       

![image](https://service.mapxus.com/dpw/api/v1/image/digitalMap/android/3.1.0/Search_services3.png)

#### 3.5.3 Search by Building ID

##### 3.5.3.1 Set Parameters

```java
	DetailSearchOption detailSearchOption = new DetailSearchOption();
	detailSearchOption.id(keyWord);

```
##### 3.5.3.2 Implement Searching

```java
	buildingSearch.searchBuildingDetail(detailSearchOption);
```
##### 3.5.3.3 Get Searching Result

```java
	@Override
    public void onGetBuildingDetailResult(BuildingDetailResult buildingDetailResult) {
        if (buildingDetailResult.status != 0) {
            Toast.makeText(this, buildingDetailResult.error.toString(), Toast.LENGTH_LONG).show();
            return;
        }
        if (buildingDetailResult.getIndoorBuildingInfo() == null) {
            Toast.makeText(this, getString(R.string.no_result), Toast.LENGTH_LONG).show();
            return;
        }

        mapboxMap.clear();
        IndoorBuildingInfo indoorBuildingInfo = buildingDetailResult.getIndoorBuildingInfo();

        Marker marker = mapboxMap.addMarker(new ObjectMarkerOptions()
                .position(
                        new LatLng(indoorBuildingInfo.getLabelCenter()
                                .getLat(), indoorBuildingInfo
                                .getLabelCenter().getLon()))
                .title(indoorBuildingInfo.getName().get("default")).snippet(indoorBuildingInfo.getAddress().get("default").toShortAddress())
                .object(indoorBuildingInfo));
        mapboxMap.moveCamera(CameraUpdateFactory.newLatLngZoom(marker.getPosition(), 16));
    }

```


![image](https://service.mapxus.com/dpw/api/v1/image/digitalMap/android/3.1.0/Search_services4.png)

#### 3.5.4 Global Search

##### 3.5.4.1 Set Parameters

```java

	GlobalSearchOption globalSearchOption = new GlobalSearchOption();
	globalSearchOption.keyword(keyWord);
```
##### 3.5.4.2 Implement Searching

```java

	buildingSearch.searchInGlobal(globalSearchOption);
```
##### 3.5.4.3 Get Searching Result

```java
@Override
    public void onGetBuildingResult(BuildingResult buildingResult) {

        if (buildingResult.status != 0) {
            Toast.makeText(this, buildingResult.error.toString(), Toast.LENGTH_LONG).show();
            return;
        }
        if (buildingResult.getIndoorBuildingList() == null || buildingResult.getIndoorBuildingList().isEmpty()) {
            Toast.makeText(this, getString(R.string.no_result), Toast.LENGTH_LONG).show();
            return;
        }

       mapboxMap.clear();
        indoorBuildingOverlay = new MyIndoorBuildingOverlay(mapboxMap, buildingResult.getIndoorBuildingList());
        indoorBuildingOverlay.addToMap();
        indoorBuildingOverlay.zoomToSpan();
    }

    @Override
    public void onGetBuildingDetailResult(BuildingDetailResult buildingDetailResult) {


    }

```

    
![image](https://service.mapxus.com/dpw/api/v1/image/digitalMap/android/3.1.0/Search_services5.png)

### 3.6 Search POI

POI Search is implemented through PoiSearch. It could be instantiated through the following steps:

##### Instantiate BuildingSearch Object

```java
        poiSearch = PoiSearch.newInstance();
```
##### Set POI Search Result Listener

```java
        poiSearch.setPoiSearchResultListener(this);
```

#### 3.6.1 Search Nearby POI

##### 3.6.1.1 Set Parameters

```java
		NearbySearchOption nearbySearchOption = new NearbySearchOption();
		nearbySearchOption.mRadius = 2;
		nearbySearchOption.location(new LatLng(
		        LatLngConstant.ELEMENT_LATLON.getLatitude(),
		        LatLngConstant.ELEMENT_LATLON.getLongitude()));
		nearbySearchOption.keyword(keyWord);

```
##### 3.6.1.2 Implement Searching

```java
poiSearch.searchNearby(nearbySearchOption);

```
##### 3.6.1.3 Get Search Result

```java
public void onGetPoiResult(PoiResult poiResult) {
        if (poiResult.status != 0) {
            Toast.makeText(this, poiResult.error.toString(), Toast.LENGTH_LONG).show();
            return;
        }
        if (poiResult.getAllPoi() == null || poiResult.getAllPoi().isEmpty()) {
            Toast.makeText(this, getString(R.string.no_result), Toast.LENGTH_LONG).show();
            return;
        }

        mapboxMap.clear();
        poiOverlay = new MyPoiOverlay(mapboxMap, poiResult.getAllPoi());
        poiOverlay.addToMap();
        poiOverlay.zoomToSpan();
    }

```
![image](https://service.mapxus.com/dpw/api/v1/image/digitalMap/android/3.1.0/Search_services6.png)

#### 3.6.2 Search POI by Area


##### 3.6.2.1 Set Parameters

```java

BoundSearchOption boundSearchOption = new BoundSearchOption();
boundSearchOption.bound(latLngBounds);
boundSearchOption.keyword(keyWord);

```
##### 3.6.2.2 Implement Searching

```java
poiSearch.searchInBound(boundSearchOption);
```
##### 3.6.2.3 Get Search Result

```java
public void onGetPoiResult(PoiResult poiResult) {
        if (poiResult.status != 0) {
            Toast.makeText(this, poiResult.error.toString(), Toast.LENGTH_LONG).show();
            return;
        }
        if (poiResult.getAllPoi() == null || poiResult.getAllPoi().isEmpty()) {
            Toast.makeText(this, getString(R.string.no_result), Toast.LENGTH_LONG).show();
            return;
        }

        mapboxMap.clear();
        poiOverlay = new MyPoiOverlay(mapboxMap, poiResult.getAllPoi());
        poiOverlay.addToMap();
        poiOverlay.zoomToSpan();
    }

```

![image](https://service.mapxus.com/dpw/api/v1/image/digitalMap/android/3.1.0/Search_services7.png)

       
#### 3.6.3 Search POI by ID

##### 3.6.3.1 Set Parameters

```java
DetailSearchOption detailSearchOption = new DetailSearchOption();
detailSearchOption.id(keyWord);

```
##### 3.6.3.2 Implement Search

```java
poiSearch.searchPoiDetail(detailSearchOption);
```
##### 3.6.3.3 Get Search Result

```java
public void onGetPoiDetailResult(PoiDetailResult poiDetailResult) {
        if (poiDetailResult.status != 0) {
            Toast.makeText(this, poiDetailResult.error.toString(), Toast.LENGTH_LONG).show();
            return;
        }
        if (poiDetailResult.getPoiInfo() == null) {
            Toast.makeText(this, getString(R.string.no_result), Toast.LENGTH_LONG).show();
            return;
        }

        mapboxMap.clear();
        PoiInfo poiInfo = poiDetailResult.getPoiInfo();

        Marker marker = mapboxMap.addMarker(new ObjectMarkerOptions()
                .position(
                        new LatLng(poiInfo.getLocation()
                                .getLat(), poiInfo
                                .getLocation().getLon()))
                .title(poiInfo.getName().get("default")).snippet("buildingId:" + poiInfo.getBuildingId())
                .object(poiInfo));
        mapboxMap.moveCamera(CameraUpdateFactory.newLatLngZoom(marker.getPosition(), 19));
    }

```
![image](https://service.mapxus.com/dpw/api/v1/image/digitalMap/android/3.1.0/Search_services8.png)

#### 3.6.4 Search Indoor POI

##### 3.6.4.1 Set Parameters

```java
InBuildingSearchOption inBuildingSearchOption = new InBuildingSearchOption();
inBuildingSearchOption.buildingId(buildingId);
inBuildingSearchOption.keyword(keyWord);

```
##### 3.6.4.2 Implement Searching

```java
poiSearch.searchInBuilding(inBuildingSearchOption);
```
##### 3.6.4.3 Get Search Result

```java
@Override
    public void onGetPoiResult(PoiResult poiResult) {
        if (poiResult.status != 0) {
            Toast.makeText(this, poiResult.error.toString(), Toast.LENGTH_LONG).show();
            return;
        }
        if (poiResult.getAllPoi() == null || poiResult.getAllPoi().isEmpty()) {
            Toast.makeText(this, getString(R.string.no_result), Toast.LENGTH_LONG).show();
            return;
        }

        mapboxMap.clear();
        poiOverlay = new MyPoiOverlay(mapboxMap, poiResult.getAllPoi());
        poiOverlay.addToMap();
        poiOverlay.zoomToSpan();
    }

```

![image](https://service.mapxus.com/dpw/api/v1/image/digitalMap/android/3.1.0/Search_services9.png)

#### 3.6.5 Search Indoor POI Category

##### 3.6.5.1 Set Parameters

~~~java
PoiCategorySearchOption poiCategorySearchOption = new PoiCategorySearchOption();
poiCategorySearchOption.buildingId(buildingId);
poiCategorySearchOption.floor(floor);
~~~
##### 3.6.5.2 Implement Searching

~~~java
poisearch.searchPoiCategoryInBuilding(poiCategorySearchOption);
~~~

##### 3.6.5.3 Get Search Result

~~~java
@Override
public void onPoiCategoriesResult(PoiCategoryResult poiCategoryResult){
	poiCategoryResult.getResult();
}
~~~

#### 3.6.6 Search Indoor POI with orientation

##### 3.6.6.1 Set Parameters

~~~java
PoiOrientationSearchOption option = new PoiOrientationSearchOption();
option.orientation(mOrientation);
option.indoorLatLng(indoorLatLng);
option.meterRadius(distance);
~~~

##### 3.6.6.2 Implement Searching

~~~java
 poiSearch.searchPoiByOrientation(option);
~~~

##### 3.6.6.3 Get Search Result

~~~java
 @Override
public void onGetPoiByOrientationResult(PoiOrientationResult poiOrientationResult) {
}
~~~
![](https://service.mapxus.com/dpw/api/v1/image/digitalMap/android/3.1.0/Search_services10.jpg)

### 3.7 Route Planning

Route planning can draw a route, including start point, end point and turning point, with WalkRouteOverlay according to the start point and end point.

##### First step, instantiate RoutePlanning object

```java
        private RoutePlanning routePlanning;
        routePlanning = RoutePlanning.newInstance();
```
##### Second step, set route planning listener

```java
        routePlanning.setRoutePlanningListener(this);
```
##### Third step, set searching parameters

```java
     private RoutePlanningPoint origin = new RoutePlanningPoint("elements_hk_dc005f", "L1", 114.16130, 22.30585);
    private RoutePlanningPoint destination = new RoutePlanningPoint("elements_hk_dc005f", "L3", 114.16185, 22.30405);
```
  
##### Fourth step, request route

```java
        routePlanning.route(origin, destination);
```
##### Fifth step, get route planning result

```java
   @Override
    public void onGetRoutePlanningResult(RoutePlanningResult routePlanningResult) {
        if (routePlanningResult.status != 0) {
            Toast.makeText(this, routePlanningResult.error.toString(), Toast.LENGTH_LONG).show();
            return;
        }
        if (routePlanningResult.getRouteResponseDto() == null) {
            Toast.makeText(this, getString(R.string.no_result), Toast.LENGTH_LONG).show();
            return;
        }
        RouteResponseDto routeResponseDto = routePlanningResult.getRouteResponseDto();
        drawRoute(routeResponseDto);
        mMapxusMap.switchFloor(origin.getFloor());
    }
```
##### Sixth step, draw the route

```java
    private void drawRoute(RouteResponseDto route) {
        // Convert LineString coordinates into LatLng[]

        WalkRouteOverlay walkRouteOverlay = new WalkRouteOverlay(this, mapboxMap, mMapxusMap, route, origin, destination);
        walkRouteOverlay.addToMap();
    }
```
![image](https://service.mapxus.com/dpw/api/v1/image/digitalMap/android/3.1.0/Search_services1.png)

### 3.8 Change Map Style

You can change your map style by changing color, visibility of elements and characters of the basemap. Therefore, it will render differently to fit different APP styles. 

Mapxus Map presents four styles now: Style.COMMON, Style.MAPPYBEE, Style.HALLOWEEN, Style.CHRISTMAS, and Style.COMMON.
You can change your map style by this interface:

```java
mapViewProvider.setStyle(Style.COMMON);
```
      
![image](https://service.mapxus.com/dpw/api/v1/image/digitalMap/android/3.1.0/Styles.png)


## 4. API

Please click [HERE] to check our APIs.

[HERE]: https://service.mapxus.com/dpw/api/v1/api/digitalMap/android/3.2.0/index.html


# Change Log

## 3.2.0

### Bugs 
* Fix wayfinding instructions.(the first point of instruction not match it's instruction)
* Fix map TalkBack.(do not read the logo)

### Features
* User can config the map element language and not dependence on system language.
* When we trigger the even of buildingChange,we can get the properties like 'bbox' and 'mult language name' from building.
* When we click the poi.We can get the buildingId、floor、type and location.
* Wayfinding add vehicle param.Support foot and wheelchair.
	