# Mapxus Map SDK Instruction

## 1. About Mapxus Map

Mapxus Map SDK is a set of call interface for developing indoor map. Developers can easily call Mapxus indoor map services and data in their iOS applications, to expanded the usage scenarios of geographic applications.

### 1.1 Minimum iOS Version

The Mapxus Map SDK for iOS is deployed on iOS 9 and above.

### 1.2 Get an API Key

Please contact us for api Key and secret。



## 2. Project Integration

### 2.1 Automatical Integration Using Cocoapods

1. Open the terminal, navigate to your project root directory, which is as same as project's file(.xcodeproj) . Create Profile using command：

```objectivec
pod init
```

2. Add the following text to Podfile and save：

```objectivec
target 'your project target' do
  use_frameworks!
  pod 'MapxusMapSDK'
end
```

3. Execute the command：

```objectivec
pod install
```

4. After the integration is successful, open the project through the file which the suffix is .xcworkspace.

### 2.2 Manual Integration

#### 2.2.1 Add MapxusMapSDK and its Dependencies

MapxusMapSDK depends on MapxusBaseSDK，AFNetworking，YYModel，Mapbox. 

Download **MapxusMapSDK.framework** from [github/mapxus-map-sdk-ios](https://github.com/MapxusSample/mapxus-map-sdk-ios). 

Download **MapxusBaseSDK.framework** form [github/mapxus-base-sdk-ios](https://github.com/MapxusSample/mapxus-base-sdk-ios) .

* **MapxusMapSDK.framework**

* **MapxusBaseSDK.framework**

* **AFNetworking.framework**

* **YYModel.framework**

* **Mapbox.framework** 

**Copy** or **drag** five files which is above into project folder and add them in **General**->**Embedded Binaries** as shown in the picture. In addition, Mapbox.framework can be downloaded [here](https://www.mapbox.com/install/ios/). 

Mapbox.framework, AFNetworking.framework, YYModel.framework can also be managed by Cocoapods or Carthage, but you have to generate **dynamic dependencies**. 

![image](https://service.mapxus.com/dpw/api/v1/image/digitalMap/ios/3.6.0/20180525164611.png)

#### 2.2.2 Configuration Considerations

For smaller application volume, you can remove the path of Simulator code on MapxusBaseSDK.framework、MapxusMapSDK.framework、Mapbox.framework、AFNetworking.framework and YYModel.framework by the **copy-frameworks** function of Carthage, because the framework containt Simulator code. Set the Run Script like below:

![image](https://service.mapxus.com/dpw/api/v1/image/digitalMap/ios/3.6.0/20180702062028.png)

Of couse, you would remove it by the Shell Script which writting yourself.



## 3. Create a Map

### 3.1 Register for Map Service

Register your map service in **AppDelegate**:

```objectivec
import MapxusBaseSDK

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

    [[MXMMapServices sharedServices] registerWithApiKey:@"your apiKey" secret:@"your secret"];

    return YES;

}
```

### 3.2 The Easy Way to Create Your Map

Add your map in ViewController（**Remarks:  **delegate** of **MGLMapView** is not allowed to be **nil** **）：

```objectivec
#import "SimpleMapViewController.h"
@import Mapbox;
@import MapxusMapSDK;

@interface SimpleMapViewController () <MGLMapViewDelegate>

@property (nonatomic, strong) MGLMapView *mapView;
@property (nonatomic, strong) MapxusMap *map;

@end

@implementation SimpleMapViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view.
    self.title = self.nameStr;
    self.view.backgroundColor = [UIColor whiteColor];
    [self.view addSubview:self.mapView];
    //initialize MGLMapView
    self.map = [[MapxusMap alloc] initWithMapView:self.mapView];
}

- (void)viewDidLayoutSubviews
{
    [super viewDidLayoutSubviews];
    self.mapView.frame = self.view.bounds;
}


- (MGLMapView *)mapView
{
    if (!_mapView) {
        _mapView = [[MGLMapView alloc] init];
        _mapView.centerCoordinate = CLLocationCoordinate2DMake(22.304716516178253, 114.16186609400843);
        _mapView.zoomLevel = 16;
        _mapView.delegate = self;
    }
    return _mapView;
}

@end
```

### 3.3 The Easy Way to Initialize Your Map

MapxusMap can configurate map through MXMConfiguration during initialization. MXMConfiguration is a configuration class of MapxusMap.

**defaultStyle** sets style of the map. It could be configurate with the other parameters at the same time.

**buildingID** and **floor** can move the map, zoom in the map to specific  building assigned by **buildingID** and show specific floor corresponding to **floor**. If not configurate **floor**, it will show ground floor of that building by default.

After setting **poiID**, the map will zoom into **zoomLevel** 19 with that POI as the center, and show the building and floor of that POI when activating the map. If **poiID** is configurated, configuration of **buildingID** is not valid anymore.


```objectivec
- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view.
    self.title = self.nameStr;
    self.view.backgroundColor = [UIColor whiteColor];

    // initialize outdoor map
    self.mapView = [[MGLMapView alloc] initWithFrame:self.view.bounds];
    self.mapView.delegate = self;
    self.mapView.autoresizingMask = UIViewAutoresizingFlexibleWidth|UIViewAutoresizingFlexibleHeight;
    [self.view addSubview:self.mapView];
    // configurate initialized project
    MXMConfiguration *configuration = [[MXMConfiguration alloc] init];
    configuration.buildingId = @"admiraltystation_hk_mqx5mp";
    configuration.floor = @"L3";
    // initialize indoor map
    self.map = [[MapxusMap alloc] initWithMapView:self.mapView configuration:configuration];
}
```

### 3.4 Change Map Style

Mapxus offers a variety of map styles to choose from. You can change your map style at anytime by the following method:

```objectivec
[self.mapxusMap setMapSytle:MXMStyleCOMMON];
```

Now Mapxus Map provides:

- MXMStyleCOMMON 
- MXMStyleCHRISTMAS 
- MXMStyleHALLOWMAS 
- MXMStyleMAPPYBEE 
- MXMStyleMAPXUS

The default map style is MXMStyleCOMMON.

### 3.5 Display Location

Mapbox location display function, please refer to [Mapbox location related documents](https://docs.mapbox.com/ios/maps/overview/).

MapxusMapSDK has the ability to automatically switch building floors with follow-up positioning. This feature is based on the iOS system's CoreLocation module. If CoreLocation returns **floor** with a value and the current MGLMapView positioning mode is not **MGLUserTrackingModeNone**, it will automatically follow the user positioning to switch to the corresponding floor.

If CoreLocation returns **floor** with a value, but the current MGLMapView positioning mode is **MGLUserTrackingModeNone**, the positioned blue dot will show a translucent effect when the selected floor on the map does not match the floor.

**Note**: If you need to customize MGLMapView.locationManager, location must be brought with **floor** information when updating the location via the method **[self.delegate locationManager:self didUpdateLocations:@[location]];**.



## 4. Map Interactions

### 4.1 Getting Map Information

MapxusMapSDK provides interface for reading current indoor map information.


```objectivec
/// Selected floor currently
@property (nonatomic, copy, readonly) NSString *floor;

/// Selected building currently
@property (nonatomic, copy, readonly) MXMGeoBuilding *building;

/**
 The floor where the user is located. This value is trusted Only if the `MGLMapView.userTrackingMode` is not the `MGLUserTrackingModeNone`. It will be nil if there is no indoor positioning data.
 */
@property (nonatomic, copy, readonly) NSString *userLocationFloor;

/**
 The building where the user is located. This value is trusted Only if the `MGLMapView.userTrackingMode` is not the `MGLUserTrackingModeNone`. It will be nil if there is no indoor positioning data.
 */
@property (nonatomic, copy, readonly) MXMGeoBuilding *userLocationBuilding;

/// Returns all visible measured buildings in MGLMapView's window
@property (nonatomic, copy, readonly) NSDictionary<NSString *, MXMGeoBuilding *> *buildings;
```


### 4.2 Map Control


#### 4.2.1 Select Building And Floor

MapxusMapSDK provides several ways to switch between the currently selected building and floor.

```objectivec
/**
 Select the floor of the currently selected building, and the map will move to the building area by default.
 @param floor The name of the selected floor.
 */
- (void)selectFloor:(nullable NSString *)floor;

/**
 Select the floor of the currently selected building.
 @param floor The name of the selected floor.
 @param zoomTo Whether the current building is zoomed to occupy the entire screen after setting the floor.
 */
- (void)selectFloor:(nullable NSString *)floor shouldZoomTo:(BOOL)zoomTo;

/**
 When you select a building, the floor will automatically switch to the last floor switch history of the map's life cycle. If not, switch to the ground floor and the map will move to the building area by default.
 @param buildingId The building ID to be selected.
 */
- (void)selectBuilding:(nullable NSString *)buildingId;

/**
 When you select a building, the floor will automatically switch to the last floor switch history of the map's life cycle. If not, switch to the ground floor.
 @param buildingId The building ID to be selected.
 @param zoomTo Whether the selected building is zoomed to occupy the entire screen after setting the buildingId.
 */
- (void)selectBuilding:(nullable NSString *)buildingId shouldZoomTo:(BOOL)zoomTo;

/**
 Select the building and the floor, the map will move to the building area by default.
 @param buildingId The building ID to be selected.
 @param floor The name of the selected floor.
 */
- (void)selectBuilding:(nullable NSString *)buildingId floor:(nullable NSString *)floor;

/**
 Choose the building and the floor.
 @param buildingId The building ID to be selected.
 @param floor The name of the selected floor.
 @param zoomTo Whether the selected building is zoomed to occupy the entire screen after setting the buildingId.
 */
- (void)selectBuilding:(nullable NSString *)buildingId floor:(nullable NSString *)floor shouldZoomTo:(BOOL)zoomTo;
```

#### 4.2.2 Indoor Map Controller Hidden

If you don't need to display the indoor map controller, you can set **MapxusMap.indoorControllerAlwaysHidden** to hide, the sample code is as follows：

```objectivec
self.map.indoorControllerAlwaysHidden = YES;
```

#### 4.2.3 Indoor Map Controller Position

Set the **selectorPosition** of **MapxusMap** to modify the position where the map controller is placed. The values can be set below:

- MXMSelectorPositionCenterLeft
- MXMSelectorPositionCenterRight
- MXMSelectorPositionBottomLeft
- MXMSelectorPositionBottomRight
- MXMSelectorPositionTopLeft
- MXMSelectorPositionTopRight

The sample code as follows:

```objectivec
self.map.selectorPosition = MXMSelectorPositionTopLeft;
```

#### 4.2.4 Outdoor Map Information Hidden

The **MapxusMap.outdoorHidden** property provides the ability to hide outdoor map information. By hiding outdoor map information, you can focus your map on indoor map information. The sample code is as follows:

```objectivec
self.map.outdoorHidden = YES;
```

#### 4.2.5 Gesture Switch Building 

By default, MapxusMap provides a gesture-switching building feature. When a user clicks on an unselected building, the map focuses on the clicked building. If this feature is not required, the function can be turned off as follows:

```objectivec
self.map.gestureSwitchingBuilding = NO;
```

#### 4.2.6 Setting Map Language

Mapxus maps are available in English, Simplified Chinese, and Traditional Chinese for switching. By default, the map will follow the system switch language. If the system language or the set language is not within these three language specifications, the default language for the map data is displayed. If you need to specify a language, you can set it up with the following sample code:

```objectivec
/// The incoming values are en，zh-Hant，zh-Hans，default
[self.map setMapLanguage:@"en"];
```

### 4.3 Map Event

Please refer to [documentation](https://www.mapbox.com/ios-sdk/api/4.2.0/Protocols/MGLMapViewDelegate.html) of Mapbox for **MGLMapView**'s lifestyle and other basic callbacks of Mapbox.

Take a look at callbacks of <MapxusMapDelegate >:

#### 4.3.1 Change Floor


```objectivec
/**
 Use this interface when changing selected floor.
 @param mapView Map View.
 @param floorName Floor name of the selected building.
 @param building Building information of the selected building. Detailed information can be referred at `MXMIndoorBuilding`.
 */
- (void)mapView:(MapxusMap *)mapView didChangeFloor:(NSString *)floorName atBuilding:(MXMGeoBuilding *)building;
```

#### 4.3.2 Click the Map

```objectivec
/**
 callback of clicking the map. If - mapView:didSingleTappedAtCoordinate:onFloor:inBuilding: successes, there will be no callback of this method
  
 @param mapView responding MapxusMap object
 @param coordinate coordinates of the clicking position
 */
- (void)mapView:(MapxusMap *)mapView didSingleTappedAtCoordinate:(CLLocationCoordinate2D)coordinate;

/**
 callback of clicking the map

 @param mapView responding object of MapxusMap
 @param coordinate coordinates of the clicking position
 @param floorName floor name of the clicking position. If you click an outdoor position, then return nil
 @param building building information of the clicking position. If you click an outdoor position, then return nil
 */
- (void)mapView:(MapxusMap *)mapView didSingleTappedAtCoordinate:(CLLocationCoordinate2D)coordinate onFloor:(nullable NSString *)floorName inBuilding:(nullable MXMGeoBuilding *)building;

/**
 callback of a long press of the map. If - mapView:didLongPressedAtCoordinate:onFloor:inBuilding: successes, then this method has no callback
 
 @param mapView responding MapxusMap object
 @param coordinate coordinates of the clicking position
 */
- (void)mapView:(MapxusMap *)mapView didLongPressedAtCoordinate:(CLLocationCoordinate2D)coordinate;

/**
 callback of a long press of the map

 @param mapView responding MapxusMap object
 @param coordinate coordinates of the long-pressing position
 @param floorName floor name of the long-pressing position. If it is an outdoor position, then return nil
 @param building building information of the long-pressing position. If it is an outdoor position, then return nil
 */
- (void)mapView:(MapxusMap *)mapView didLongPressedAtCoordinate:(CLLocationCoordinate2D)coordinate onFloor:(nullable NSString *)floorName inBuilding:(nullable MXMGeoBuilding *)building;
```

#### 4.3.3 Click a POI


```objectivec
/**
 Call this interface when clicking POI.
 @param mapView Map View.
 @param poi Information of selected POI. Detailed information can be referred at `MXMIndoorPOI`。
 */
- (void)mapView:(MapxusMap *)mapView didTappedOnPOI:(MXMGeoPOI *)poi;
```

#### 4.3.4 Click on the Map Blank Events

```objectivec
/**
 Clicking on the blank space in the map will call back this interface.
 @param mapView Responsive MapxusMap object
 @param coordinate The coordinate point of the blank where you clicked
 */
- (void)mapView:(MapxusMap *)mapView didTappedOnMapBlank:(CLLocationCoordinate2D)coordinate;
```

#### 4.3.5 Enter Indoor Scene Events

```objectivec
/**
 Enter/exit indoor scene callback, the same result may be called multiple times

 @param mapView Responsive MapxusMap object
 @param flag Enter/exit indoor scene sign，YES:enter；NO:exit
 @param buildingId Enter the building ID of the scene
 @param floor Enter the floor of the scene
 */
- (void)mapView:(MapxusMap *)mapView indoorMapWithIn:(BOOL)flag building:(NSString *)buildingId floor:(NSString *)floor;
```



## 5. Draw on the Map

### 5.1 Draw a Default Point Annotation

MapxusMapSDK provides **MXMPointAnnotation** to display point annotation belong to the selected floor. You can also implement  Mapbox annotation classes for the same purpose. 

1. Add default point annotation on a map through MapxusMapSDK

Add the following code in **-viewDidLoad:**

```objectivec
MXMPointAnnotation *mxmAnn = [[MXMPointAnnotation alloc] init];
mxmAnn.coordinate = CLLocationCoordinate2DMake(22.304816516178253, 114.16226609400843);
mxmAnn.title = @"test point";
mxmAnn.subtitle = @"Floor G";
mxmAnn.buildingId = @"elements_hk_dc005f";
mxmAnn.floor = @"G";
[self.mapxusMap addMXMPointAnnotations:@[mxmAnn]]; // You have to use - addMXMPointAnnotations: in MapxusMap to add MXMPointAnnotation
```

2. If you need to change point annotation icon, you can implement callback in <MGLMapViewDelegate>

```objectivec
- (MGLAnnotationImage *)mapView:(MGLMapView *)mapView imageForAnnotation:(id<MGLAnnotation>)annotation
{
    if ([annotation isKindOf:[MXMPointAnnotation class]]) {
        MGLAnnotationImage *img = [MGLAnnotationImage annotationImageWithImage:[UIImage imageNamed:@"location_p"] reuseIdentifier:@"test"];

		return img;
    }
    return nil;
}
```

3. To remove **MXMPointAnnotation**, you need to call **- removeMXMPointAnnotaions:** in MapxusMap to remove it completely.

4. The **MapxusMap.MXMAnnotations** array records all MXMPointAnnotations that have been joined in the map.



## 6. Data Retrieval

### 6.1 Search Buildings

MapxusMapSDK provides search building service. Parameters are defined as belows: 

```objectivec
/**
 Building Search Request Configuration Class
 
 There are four search modes:
 1. Global search, parameter combination is keywords (optional), offset, page;
 2. Specify the keyword search in the rectangular area, the parameter combination is keywords (optional), bbox, offset, page;
 3. Specify the keyword search in the circular area, the parameter combination is keywords (optional), center, distance, offset, page;
 4. Specify the building ID search with the parameter buildingIds.
 */
@interface MXMBuildingSearchRequest : NSObject
/// Keywords, only a single character is allowed
@property (nonatomic, strong) NSString *keywords;
/// Bounding box. Choose one between bbox and center
@property (nonatomic, strong) MXMBoundingBox *bbox;
/// Center point. Choose one between bbox and center
@property (nonatomic, strong) MXMGeoPoint *center;
/// Searching distance from the center point; unit: km ; should be used together with center
@property (nonatomic, assign) double distance;
/// How much data is displayed on one page
@property (nonatomic, assign) NSUInteger offset;
/// How many pages
@property (nonatomic, assign) NSUInteger page;
/// Mutually exclusive with the above parameters
@property (nonatomic, strong) NSArray *buildingIds;
@end
```

#### 6.1.1 Search within a Circular Area

When searching within a circular area, use the parameters: keywords (optional), center, distance, offset, page. Where center is the center of the circle and distance is the radius.

Take a look at the example code:

```objectivec
- (void)requestData
{
    [ProgressHUD show];
    MXMGeoPoint *point = [[MXMGeoPoint alloc] init];
    point.latitude = 22.304716516178253;
    point.longitude = 114.16186609400843;
    
    MXMBuildingSearchRequest *re = [[MXMBuildingSearchRequest alloc] init];
    re.keywords = self.keyTF.text;
    re.center = point;
    re.distance = 100;
    re.offset = 100;
    re.page = 1;
    
    MXMSearchAPI *api = [[MXMSearchAPI alloc] init];
    api.delegate = self;
    [api MXMBuildingSearch:re];
}

#pragma mark - MXMSearchDelegate

- (void)MXMSearchRequest:(id)request didFailWithError:(NSError *)error
{
  if ([request isKindOfClass:[MXMBuildingSearchRequest class]]) {
    // Processing failure results here
  }
}

- (void)onBuildingSearchDone:(MXMBuildingSearchRequest *)request response:(MXMBuildingSearchResponse *)response
{
    // Processing success results here
}
```

#### 6.1.2 Search in Rectangular Area

When searching for the selected rectangular area, use the parameters: keywords (optional), bbox, offset, page.

See the example code:

```objectivec
- (void)requestData:(NSString *)key
{
    [ProgressHUD show];
    MXMBoundingBox *box = [[MXMBoundingBox alloc] init];
    box.min_latitude = 22.292540;
    box.min_longitude = 114.158608;
    box.max_latitude = 22.310600;
    box.max_longitude = 114.172422;
    
    MXMBuildingSearchRequest *re = [[MXMBuildingSearchRequest alloc] init];
    re.keywords = key;
    re.bbox = box;
    re.offset = 100;
    re.page = 1;
    
    MXMSearchAPI *api = [[MXMSearchAPI alloc] init];
    api.delegate = self;
    [api MXMBuildingSearch:re];
}

#pragma mark - MXMSearchDelegate

- (void)MXMSearchRequest:(id)request didFailWithError:(NSError *)error
{
  if ([request isKindOfClass:[MXMBuildingSearchRequest class]]) {
    // Processing failure results here
  }
}

- (void)onBuildingSearchDone:(MXMBuildingSearchRequest *)request response:(MXMBuildingSearchResponse *)response
{
    // Processing success results here
}
```


#### 6.1.3 Search by ID

When searching by building ID accurately, use the parameter: buildingIds.

See the example code shown belows:

```objectivec
- (void)requestData:(NSString *)key
{
    if (key) {
        [ProgressHUD show];
        MXMBuildingSearchRequest *re = [[MXMBuildingSearchRequest alloc] init];
        re.buildingIds = @[key];
        
        MXMSearchAPI *api = [[MXMSearchAPI alloc] init];
        api.delegate = self;
        [api MXMBuildingSearch:re];
    }
}

#pragma mark - MXMSearchDelegate

- (void)MXMSearchRequest:(id)request didFailWithError:(NSError *)error
{
  if ([request isKindOfClass:[MXMBuildingSearchRequest class]]) {
    // Processing failure results here
  }
}

- (void)onBuildingSearchDone:(MXMBuildingSearchRequest *)request response:(MXMBuildingSearchResponse *)response
{
    // Processing success results here
}
```

#### 6.1.4 Global Search

Global building keyword search, using parameters: keywords (optional), offset, page.

Example code:

```objectivec
- (void)requestData:(NSString *)key
{
   [ProgressHUD show];
    MXMBuildingSearchRequest *re = [[MXMBuildingSearchRequest alloc] init];
    re.keywords = self.keyTF.text;
    re.offset = 100;
    re.page = 1;
    
    MXMSearchAPI *api = [[MXMSearchAPI alloc] init];
    api.delegate = self;
    [api MXMBuildingSearch:re];
}

#pragma mark - MXMSearchDelegate

- (void)MXMSearchRequest:(id)request didFailWithError:(NSError *)error
{
  if ([request isKindOfClass:[MXMBuildingSearchRequest class]]) {
    // Processing failure results here
  }
}

- (void)onBuildingSearchDone:(MXMBuildingSearchRequest *)request response:(MXMBuildingSearchResponse *)response
{
    // Processing success results here
}
```

### 6.2 POI Category Search

MapxusMapSDK provides POI category search, which allows you to know what type of POI is in a building floor. The POI category search request parameter configuration class is as follows:

```objectivec
/**
 POI category search request configuration class
 
 Search for all POI category names in the designated building and floor, floor can not pass, no pass will search the entire building.
 */
@interface MXMPOICategorySearchRequest : NSObject
/// Specify search building id
@property (nonatomic, strong) NSString *buildingId;
/// Specify search floor
@property (nonatomic, strong) NSString *floor;
@end
```

Example code：

```objectivec
- (void)requestCategory
{
   [ProgressHUD show];
    MXMPOICategorySearchRequest *re = [[MXMPOICategorySearchRequest alloc] init];
    re.buildingId = @"elements_hk_dc005f";
		re.floor = @"G";
    
    MXMSearchAPI *api = [[MXMSearchAPI alloc] init];
    api.delegate = self;
    [api MXMPOICategorySearch:re];
}

#pragma mark - MXMSearchDelegate

- (void)MXMSearchRequest:(id)request didFailWithError:(NSError *)error
{
  if ([request isKindOfClass:[MXMPOICategorySearchRequest class]]) {
    // Processing failure results here
  }
}

- (void)onPOICategorySearchDone:(MXMPOICategorySearchRequest *)request response:(MXMPOICategorySearchResponse *)response
{
    // Processing success results here
}
```

### 6.3 Search POI

MapxusMapSDK provides search POI service. Parameters are defined as belows:

```objectivec
/**
 Configuration of search POI calls
 
 There are four search modes:
  1. Specify keyword search in buildings and floors, parameter combination is keywords (optional), buildingId, floor (optional), offset, page, category (optional);
  2. Specify keyword search in the rectangular area, the parameter combination is keywords (optional), bbox, offset, page, category (optional);
  3. Specify keyword search in the circular area, the parameter combination is keywords (optional), center, meterDistance (or distance), offset, page, category (optional);
  4. Specify the building ID search, the parameter is POIIds;
 
 Category reference value：
 
 | Key                            | 中文名         |
 | ------------------------------ | -------------- |
 | shop                           | 商店           |
 | restaurant                     | 餐厅           |
 | toilet                         | 厕所           |
 | outdoor                        | 户外           |
 | transport                      | 运输           |
 | parking                        | 停车场         |
 | classroom                      | 教室           |
 | study                          | 自习室         |
 | reading                        | 阅读           |
 | meeting                        | 会议           |
 | computer                       | 电脑室         |
 | auditorium                     | 礼堂           |
 | lab                            | 实验室         |
 | library                        | 图书馆         |
 | function                       | 多功能厅       |
 | media                          | 多媒体室       |
 | security_room                  | 保安室         |
 | prayer_room                    | 祈祷室         |
 | lounge                         | 休息室         |
 | workshop                       | 工作室         |
 | anteroom                       | 接待室         |
 | operating_theater              | 手术室         |
 | therapy_room                   | 治疗室         |
 | consulation_room               | 咨询室         |
 | ward                           | 病房           |
 | dispensary                     | 药房           |
 | examination_room               | 检查室         |
 | cashier                        | 收银处         |
 | registration                   | 挂号处         |
 | huddle_room                    | 小型会议室     |
 | kitchen                        | 厨房           |
 | laboratory                     | 实验室         |
 | lobby                          | 大堂           |
 | mail_room                      | 收发室         |
 | non_public                     | 非公开         |
 | office                         | 办公室         |
 | phone_room                     | 通讯室         |
 | server_room                    | 机房           |
 | shower                         | 淋浴室         |
 | smoking_area                   | 吸烟区         |
 | atm                            | 自动取款机     |
 | customer_service               | 客户服务       |
 | coins_collector                | 投币机         |
 | directory                      | 目录           |
 | fire_hydrant                   | 消防栓         |
 | game_station                   | 游戏站         |
 | mobile_charger                 | 手机充电器     |
 | parcel_locker                  | 包裹储物柜     |
 | recycling_bin                  | 回收站         |
 | storage_locker                 | 储物柜         |
 | telephone                      | 电话           |
 | ticketing                      | 票务           |
 | undefined                      | 未定义的       |
 | vending_machine                | 自动售货机     |
 | waste_bin                      | 垃圾箱         |
 | water_machine                  | 饮水机         |
 | printer                        | 打印机         |
 | scanner                        | 扫描仪         |
 | computer                       | 电脑           |
 | add_value_machine              | 增加价值的机器 |
 | fountain                       | 喷泉           |
 | mini_ktv                       | 小型卡拉ok     |
 | braille_signs                  | 点字指示牌     |
 | doll_machine                   | 娃娃机         |
 | cashier                        | 收银机         |
 | defibrillator                  | 除颤器         |
 | information                    | 指示牌         |
 | mailbox                        | 邮箱           |
 | power_charging_station         | 充电站         |
 | removable_restroom             | 移动式洗手间   |
 | braille_and_tactile_floor_plan | 触觉平面图     |
 | guide_path                     | 引路径         |
 | entry_gate                     | 入闸位         |
 | exit_gate                      | 出闸位         |
 | gate                           | 闸位           |
 | type                           | 门口           |
 | guest_services                 | 客户服务       |
 */
@interface MXMPOISearchRequest : NSObject
/// Keywords, only a single character is allowed
@property (nonatomic, strong) NSString *keywords;
/// The Id of building which you want to search.
@property (nonatomic, strong) NSString *buildingId;
/// The floor that search on. Must be used in conjunction with the buildingId
@property (nonatomic, strong) NSString *floor;
/// Rectangular search area.
@property (nonatomic, strong) MXMBoundingBox *bbox;
/// Circular area search center.
@property (nonatomic, strong) MXMGeoPoint *center;
/// Round area search radius. The unit is km and must be used in conjunction with the center.
@property (nonatomic, assign) double distance DEPRECATED_ATTRIBUTE;
/// Round area search radius. The unit is m and must be used in conjunction with the center.
@property (nonatomic, assign) NSUInteger meterDistance;
/// How much data is displayed per page
@property (nonatomic, assign) NSUInteger offset;
/// Number of pages
@property (nonatomic, assign) NSUInteger page;
/// The category to filter
@property (nonatomic, strong) NSString *category;
/// A list of POI ids for the query. Mutually exclusive with the above parameters
@property (nonatomic, strong) NSArray *POIIds;
@end
```

#### 6.3.1 Search POI in Circular Area

Search the POI in the circular area, using the parameters: keywords (optional), center, meterDistance, offset, page, category (optional). Where center is the search center and meterDistance is the search radius.

Example code:

```objectivec
- (void)requestData:(NSString *)key
{
    [ProgressHUD show];
    MXMGeoPoint *point = [[MXMGeoPoint alloc] init];
    point.latitude = 22.304716516178253;
    point.longitude = 114.16186609400843;
    
    MXMPOISearchRequest *re = [[MXMPOISearchRequest alloc] init];
    re.keywords = key;
    re.center = point;
    re.meterDistance = 57;  // 57m
    re.offset = 100;
    re.page = 1;
    
    MXMSearchAPI *api = [[MXMSearchAPI alloc] init];
    api.delegate = self;
    [api MXMPOISearch:re];
}

#pragma mark - MXMSearchDelegate

- (void)MXMSearchRequest:(id)request didFailWithError:(NSError *)error
{
  if ([request isKindOfClass:[MXMPOISearchRequest class]]) {
    // Processing failure results here
  }
}
   
- (void)onPOISearchDone:(MXMPOISearchRequest *)request response:(MXMPOISearchResponse *)response
{
    // Processing success results here
}
```

#### 6.3.2 Search POI in Rectangular Area

Search for POI in the rectangular area, using the parameters: keywords (optional), bbox, offset, page, category (optional).

Example code:

```objectivec
- (void)requestData:(NSString *)key
{
    [ProgressHUD show];
    MXMBoundingBox *box = [[MXMBoundingBox alloc] init];
    box.min_latitude = 22.292540;
    box.min_longitude = 114.158608;
    box.max_latitude = 22.310600;
    box.max_longitude = 114.172422;
    
    MXMPOISearchRequest *re = [[MXMPOISearchRequest alloc] init];
    re.keywords = key;
    re.bbox = box;
    re.offset = 100;
    re.page = 1;
    
    MXMSearchAPI *api = [[MXMSearchAPI alloc] init];
    api.delegate = self;
    [api MXMPOISearch:re];
}

#pragma mark - MXMSearchDelegate

- (void)MXMSearchRequest:(id)request didFailWithError:(NSError *)error
{
  if ([request isKindOfClass:[MXMPOISearchRequest class]]) {
    // Processing failure results here
  }
}
   
- (void)onPOISearchDone:(MXMPOISearchRequest *)request response:(MXMPOISearchResponse *)response
{
    // Processing success results here
}
```

#### 6.3.3 Search by POI ID

Accurate search based on POI ID, using the parameter: POIIds.

Example codes:

```objectivec
- (void)requestData:(NSString *)key
{
    [ProgressHUD show];
    MXMPOISearchRequest *re = [[MXMPOISearchRequest alloc] init];
    re.POIIds = @[key];
    
    MXMSearchAPI *api = [[MXMSearchAPI alloc] init];
    api.delegate = self;
    [api MXMPOISearch:re];
}

#pragma mark - MXMSearchDelegate

- (void)MXMSearchRequest:(id)request didFailWithError:(NSError *)error
{
  if ([request isKindOfClass:[MXMPOISearchRequest class]]) {
    // Processing failure results here
  }
}
   
- (void)onPOISearchDone:(MXMPOISearchRequest *)request response:(MXMPOISearchResponse *)response
{
    // Processing success results here
}
```

#### 6.3.4 Search by Building Information

Search for POIs in the specified building using parameters: keywords (optional), buildingId, floor (optional), offset, page, category (optional).

Example code:

```objectivec
- (void)requestData:(NSString *)key
{
    [ProgressHUD show];
    MXMPOISearchRequest *re = [[MXMPOISearchRequest alloc] init];
    re.keywords = key;
    re.buildingId = self.building.text;
    re.offset = 100;
    re.page = 1;
    
    MXMSearchAPI *api = [[MXMSearchAPI alloc] init];
    api.delegate = self;
    [api MXMPOISearch:re];
}

#pragma mark - MXMSearchDelegate

- (void)MXMSearchRequest:(id)request didFailWithError:(NSError *)error
{
  if ([request isKindOfClass:[MXMPOISearchRequest class]]) {
    // Processing failure results here
  }
}
   
- (void)onPOISearchDone:(MXMPOISearchRequest *)request response:(MXMPOISearchResponse *)response
{
    // Processing success results here
}
```

#### 6.3.5 Query the angle of the nearby POI relative to the center point

Through this function, you can view the nearby POI in relative orientation and provide the user with a positioning reference. The query request parameter configuration class is defined as follows:

```objectivec
/**
 Given the map deflection angle, search for nearby POI points and derive the orientation of the POI point relative to the phone direction.
 */
@interface MXMOrientationPOISearchRequest : NSObject
/// The clockwise angle from the north direction of the map to the phone pointing, the value range：[0,359]
@property (nonatomic, assign) NSUInteger angle;
/// Distance search type (default: Point). Point: Find the POI point of the circle with the center as the center and the distance as the radius; Polygon: Find the POI information of the circle intersecting room with the center as the center and the distance as the radius
@property (nonatomic, strong) NSString *distanceSearchType;
/// The Id of building which you want to search.
@property (nonatomic, strong) NSString *buildingId;
/// The floor that search on. 
@property (nonatomic, strong) NSString *floor;
/// Center point position
@property (nonatomic, strong) MXMGeoPoint *center;
/// Round area search radius. The unit is m
@property (nonatomic, assign) NSUInteger distance;
@end
```

Example code:

```objectivec
- (void)requestData
{
    [ProgressHUD show];
    
    CLLocationCoordinate2D coor = [self.mapView convertPoint:self.mapView.center toCoordinateFromView:self.mapView];
    
    MXMGeoPoint *point = [[MXMGeoPoint alloc] init];
    point.latitude = coor.latitude;
    point.longitude = coor.longitude;
    
    MXMOrientationPOISearchRequest *re = [[MXMOrientationPOISearchRequest alloc] init];
    re.center = point;
    re.distance = 10;
    re.angle = self.mapView.direction;
    re.buildingId = self.map.building.identifier;
    re.floor = self.map.floor;
    re.distanceSearchType = @"Polygon";
    
    MXMSearchAPI *api = [[MXMSearchAPI alloc] init];
    api.delegate = self;
    [api MXMOrientationPOISearch:re];
}

#pragma mark - MXMSearchDelegate

- (void)MXMSearchRequest:(id)request didFailWithError:(NSError *)error
{
	if ([request isKindOfClass:[MXMOrientationPOISearchRequest class]]) {
    // Processing failure results here
  }
}

- (void)onOrientationPOISearchDone:(MXMOrientationPOISearchRequest *)request response:(MXMOrientationPOISearchResponse *)response
{
    // Processing success results here
    for (MXMPOI *poi in response.pois) {
        MXMPointAnnotation *ann = [[MXMPointAnnotation alloc] init];
        ann.coordinate = CLLocationCoordinate2DMake(poi.location.latitude, poi.location.longitude);
        ann.title = poi.name_default;
        if (poi.angle > 315 || poi.angle <= 44) {
            ann.subtitle = @"In the front";
        } else if (poi.angle > 44 && poi.angle <= 134) {
            ann.subtitle = @"On the right";
        } else if (poi.angle > 134 && poi.angle <= 224) {
            ann.subtitle = @"In the back";
        } else if (poi.angle > 224 && poi.angle <= 314) {
            ann.subtitle = @"On the left";
        }
        ann.buildingId = poi.buildingId;
        ann.floor = poi.floor;
        [anns addObject:ann];
    }
    // Center Point
    MXMPointAnnotation *ann = [[MXMPointAnnotation alloc] init];
    ann.coordinate = CLLocationCoordinate2DMake(request.center.latitude, request.center.longitude);
    ann.title = @"your location";
    [anns addObject:ann];
    
    [self.map addMXMPointAnnotations:anns];
    [self.mapView showAnnotations:anns animated:YES];
    
    [ProgressHUD dismiss];
}
```

### 6.4 Reverse geocoding (coordinate to address)

With this function, you can convert the positioning coordinates to the specific building and floor, providing users with more detailed and more user-friendly positioning information.

Example code:

```objectivec
// Initialize the retrieved object
MXMGeoCodeSearch *geoCodeSearch = [[MXMGeoCodeSearch alloc] init];
// Set up a retrieval agent
geoCodeSearch.delegate = self;
// Constructing a retrieval parameter object
MXMReverseGeoCodeSearchOption *opt = [[MXMReverseGeoCodeSearchOption alloc] init];
opt.location = self.mapView.userLocation.location.coordinate; // Positioning latitude and longitude
opt.ordinalFloor = @(self.mapView.userLocation.location.floor.level); // Number of positioned floor
// Initiate a request
[geoCodeSearch reverseGeoCode:opt];

#pragma mark - MXMGeoCodeSearchDelegate

- (void)onGetReverseGeoCode:(MXMGeoCodeSearch *)searcher result:(nullable MXMReverseGeoCodeSearchResult *)result error:(nullable NSError *)error
{
  if (error != nil) {
    // Processing failure results here
  } else {
    // Processing success results here
  }
}
```



## 7. Route Planning

Mapxus Map provides route planning service. Parameters are defined as belows:

```objectivec
/**
 request configuration of route search
 */
@interface MXMRouteSearchRequest : NSObject
/// starting builing
@property (nonatomic, strong) NSString *fromBuilding;
/// starting floor
@property (nonatomic, strong) NSString *fromFloor;
/// starting point longitude
@property (nonatomic, assign) double fromLon;
/// starting point latitude
@property (nonatomic, assign) double fromLat;
/// ending point building
@property (nonatomic, strong) NSString *toBuilding;
/// ending point floor
@property (nonatomic, strong) NSString *toFloor;
/// ending point longitude
@property (nonatomic, assign) double toLon;
/// ending point latitude
@property (nonatomic, assign) double toLat;
/// Navigation method. The optional values are foot, wheelchair. Default foot
@property (nonatomic, strong) NSString *vehicle;
/// Returns the result language version. The optional values are zh-HK, zh-CN, en. Default en
@property (nonatomic, strong) NSString *locale;
/// The end point is set in front of the door. Set to YES and the end will only end at the POI store door.
@property (nonatomic, assign) BOOL toDoor;
@end
```

Example call codes:

```objectivec
  [ProgressHUD show];
  MXMRouteSearchRequest *re = [[MXMRouteSearchRequest alloc] init];
  re.fromBuilding = @"elements_hk_dc005f";
  re.fromFloor = @"G";
  re.fromLat = 22.304636500000001;
  re.fromLon = 114.16299189999999;
  re.toBuilding = @"elements_hk_dc005f";
  re.toFloor = @"L2";
	re.toLat = 22.304689;
  re.toLon = 114.16220269999999;
  re.locale = @"zh-CN";
	re.vehicle = @"foot";
	re.toDoor = YES;

  MXMSearchAPI *api = [[MXMSearchAPI alloc] init];
  api.delegate = self;
  [api MXMRouteSearch:re];
```

result:

We've provided a quick way to draw a route, adding the following references to the profile:

```objectivec
  pod 'MapxusComponentKit'
```

Reference [2.1 Automatical Integration Using Cocoapods](#2.1-Automatical-Integration-Using-Cocoapods) Install MapxusComponentKit.

The following is a sample code that references the MapxusComponentKit:

```objectivec
- (void)viewDidLoad {
        .
        .
        .
    // create route drawing and controlling object
    self.painter = [[MXMRoutePainter alloc] initWithMapView:self.mapView];
    self.painter.routeScaleFit = YES;
    self.painter.FittedEdgeInsets = UIEdgeInsetsMake(130, 30, 110, 80);
}
```

```objectivec
#pragma mark - MapxusMapDelegate

- (void)mapView:(MapxusMap *)mapView didChangeFloor:(NSString *)floorName atBuilding:(MXMGeoBuilding *)building
{
    [self.painter changeOnBuilding:building.identifier floor:floorName];
}
```

Implement the callback function of <MXMSearchDelegate>, obtain result and draw the route. 

```objectivec
- (void)MXMSearchRequest:(id)request didFailWithError:(NSError *)error
{
    [ProgressHUD showError:NSLocalizedString(@"We can't find the route", nil)];
}

- (void)onRouteSearchDone:(MXMRouteSearchRequest *)request response:(MXMRouteSearchResponse *)response
{
    self.fromAnnotation = nil;
    self.toAnnotation = nil;
    [self.map removeMXMPointAnnotaions:self.map.MXMAnnotations];
    
    [self.painter paintRouteUsingResult:response];
    for (NSString *key in self.painter.dto.keys) {
        if (![key containsString:@"outdoor"]) {
            MXMParagraph *paph = self.painter.dto.paragraphs[key];
            [self.map selectBuilding:paph.buildingId floor:paph.floor shouldZoomTo:NO];
            [self.painter changeWithKey:key];
            break;
        }
    }
    [ProgressHUD dismiss];
}
```



## 8. API

Please click [HERE] to check our APIs.

[HERE]: https://service.mapxus.com/dpw/api/v1/api/digitalMap/ios/3.6.0/index.html



# Change Log

## 3.6.0

2019-7-3

🎉 New Features

1. Add set map label language function.
2. Add geographic coordinate interpretation function.



## 3.5.2

2019-6-27

🐛 Bugfixes

1. Remove the labels of stairs、elevators、toilets and ramps on the map.



## 3.5.1

2019-6-26

🐛 Bugfixes

1. Fixed a Bug where clicking POI also calls **- mapView:didTappedOnMapBlank:** .
2. **- mapView:didTappedOnPOI:** passed poi is never nil.



## 3.5.0

2019-6-20

🎉 New Features

1. Add the gestureSwitchingBuilding property to turn off the ability to switch buildings by clicking on a map.
2. MXMRouteSearchRequest to add vehicle property, can set the navigation mode to walk or wheelchair.

🐛 Bugfixes

1. Fix Bug where indoor Annotation does not display after switching building by building button.



## 3.4.1

2019-6-6

🐛 Bugfixes

1. Repair MXMOrientationPOISearchResponse error explanation.



## 3.4.0

2019-5-31

🎉 New Features

1. Add callback to enter and exit indoor scene.
2. Add starting point to return pathfinding results.
3. Add click empty base image callback.
4. Add mxannotations.

🐛 Bugfixes

1. Fix the location Bug in the location analysis room.
2. Fix POI position error of tile.

 

## 3.3.0

2019-4-24

🎉 New Features

1. MXMFloorSelectorBar adds the addVoiceOverLabe attribute.You can add the voiceover read value you want.



## 3.2.0

2019-4-4

🎉 New Features

1. Route search adds the toDoor attribute.
2. Add the search POI bearing interface.



## 3.1.1

2019-3-21

🎉 New Features

1. Changes associated with server address changes.



## 3.1.0

2019-3-14

🎉 New Features

1. Add POI category queries for all specified building floors.
2. Add POI to search for a specific floor



## 3.0.0

2019-3-6

🎉 New Features

1. Split the base functionality into MapxusBaseSDK.

🐛 Bugfixes

1. Fixed an issue where the map was not loaded after the move and the indoor map was not displayed.



## 2.8.3

2019-3-4

🐛 Bugfixes

1. Fix clicking on one will switch to the other when two buildings overlap.



## 2.8.2

2019-3-4

🐛 Bugfixes

1. Fixed an incompleteness issue on the left side of the building selection list.



## 2.8.1

2019-1-22

🎉 New Features

1. Change the floorBar font color to black.



## 2.8.0

2019-1-10

🎉 New Features

1. Add the default distance property meterDistance of MXMPOISearchRequest in meters. Discard the distance attribute with kilometers as a unit.
2. MXMPOISearchRequest adds category filtering.



## 2.7.1

2019-1-2

🐛 Bugfixes

1. FloorBar and buildingSelectButton are exposed to the public to solve the voiceover unreadable problem.
2. Fix** - removeMXMPointAnnotaions: **crash.
3. Fixed **outdoorHidden** attribute to hide layers that are not outdoor maps.
4. Make the userLocationBuilding and userLocationFloor reset only when there is a change.



## 2.7.0

2018.12.10

🎉 New Features

1. Wayfinding use v4 engine.
2. Building search use v2 engine.

🐛 Bugfixes

1. **MXMPointAnnotation** when updated floor cannot be displayed in time.



## 2.6.0

2018-11-26

🎉 New Features

1. Update MXMStyleMAPXUS style and make it as default.
2. Now can set to hidden outdoor map.



## 2.5.2

2018-11-21

🐛 Bugfixes

1. Fix bitcode configuration error.



## 2.5.1

2018-11-15

🐛 Bugfixes

1.Fix circular references.
2.**MXMGeoPOI** adds longitude and latitude



## 2.5.0

2018-11-13

🎉 New Features

1. Change the language of labels to the system’s preferred language.
2. Add indoor positioning information.

🐛 Bugfixes

1. Fixing known bugs.



## 2.4.2

2018-10-29

🐛 Bugfixes

1. Fix initialization crash using buildingId or poiId. 



## 2.4.1

2018-10-27

🐛 Bugfixes

1. Fixing known bugs.



## 2.4.0

2018-10-24

🎉 New Features

1. Use system font rendering and compressing tile data to improve loading speed.
2. Update the route searching interface.
3. Empty search is supported in searchBuilding and searchPOI.
4. Add object factory methods to MXMGeoPoint and MXMBoundingBox.

🐛 Bugfixes

1. Token expiration validation failed to be repaired.



## 2.3.0

2018-10-9

🎉 New Features

1. Developer can create the map with particular building directly.
2. Developer can create the map with building in specific floor.
3. Developer can create the map with specific POI.
4. Developers click on the mapxus logo, they will jump to the mapxus home page.

🐛 Bugfixes

1. Fix **MXMGeoPOI** attributes are nil.



## 2.2.2

2018-9-22

🐛 Bugfixes

1. Repair the bug that Mapbox function **- mapView: regionDidChangeWithReason:** cannot display.



## 2.2.1

2018-9-14

🐛 Bugfixes

1. Fix the error of indoor positioning dot transparency setting.



## 2.2.0

2018-8-27

🎉 New Features

1. User can click to select building.
2. Update map controls UI.
3. Developer can set the display and hide of the map controls.
4. Developer can set the position of the map controls.
5. Add new map style Mapxus.



## 2.1.1

2018-8-23

🐛 Bugfixes

1. Fix the error that positioning would crash and the floor switch worng.