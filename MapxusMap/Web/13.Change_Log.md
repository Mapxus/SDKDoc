# CHANGE LOG

## 3.2.3

#### 2019-06-14

🚀 Presets

- poi add property text-halo-color=white

## 3.2.2

#### 2019-06-14

🐛 Bugfixes

- Fix sdk can not support mapboxgl new and old version at the same time.
- Fix sdk can not use package tools(`for webpack`) production mode to build in the npm import.

## 3.2.1

#### 2019-06-10

🚀 Presets

- update mapboxgl to 1.0.0

## 3.2.0

#### 2019-04-15

🚀 Presets

- node server add cache policy;
- wayfinding search add vehicle param

## 3.1.0

#### 2019-04-01

🎉 New Features

- Poi and orientation search by interface (`poisService.searchOrientation`),
  search orientation infomation between center and other pois
- Poi category search by interface (`poisService.searchCategory`),
  search poi category list within building and floor.
- Route service add toDoor param, and local as option

🚀 Presets

- change return value of routeService.search to AxiosPromise<IResponse<IResponseRoute>>
- update mapbox-gl's version to 0.53.0

## 3.0.0

##### 2019-03-05

🎉 New Features

- Allow use `option.theme: 'themeName'` to set up `style theme`, _example: { theme: 'mapxus' }_
- Add new theme `landsD`
- Route service version update to v5
- All server url update to new domain name

## 2.9.3

##### 2019-02-13

🐛 Bugfixes

- Fixed `use on-click map listener` function will display error

## 2.9.2

##### 2019-01-31

🎉 New Features

- Remove poi-click event and building-select event priority handle
- Add `multi building overlap switch` function, default priority near small building select, _example: if A building overlap on the B building, and current selected B building, that can not to switch A building, must be to click outdoor or other no overlap building_

## 2.9.1

##### 2019-01-29

🎉 New Features

- Route-search default param `point_encoded` as false
- Poi click priority level more than the building click event

## 2.9.0

##### 2019-01-10

🚀 Presets

- Remove the global dependency by mapboxgl

🎉 New Features

- Poi search by distance interface (`poisService.searchByDistance`), distance unit from km change to meter.

## 2.8.0

##### 2018-12-28

🎉 New Features

- Add `enable/disableSwitch` function to map instance (allow user to enable or disable click switch outdoor/indoor or building)
- Add `enable/disableSwitchBuilding` function to map instance (allow use only switch building, click outdoor can not hidden current building)

## 2.7.3

##### 2018-12-25

🎉 New Features

- Floor controller appear zoom level max is 16

🐛 Bugfixes

- Fixed will hidden other layer when hidden outdoor layers

## 2.7.2

##### 2018-12-20

🎉 New Features

- Connector and toilet type poi not to display text
- Optimize transform poi text function by language

## 2.7.1

##### 2018-12-13

🐛 Bugfixes

- Fixed transform language function can not match poi by mapxus-style

## 2.7.0

##### 2018-12-10

🎉 New Features

- Update `building service` search function version to v2
- Update `route service` search function version to v4
- Update `floor selector` control to new style (mapxus style)
- Update `floor selector` control appear on the map, max zoom level is 17
- Add building change listener, `onBuildingChangeListener` function

## 2.6.0

##### 2018-11-23

🎉 New Features

- Allow user in init the map config `hiddenOutdoor` param to hidden outdoor data.
- Add `hiddenOutdoorLayer` interface, let user can to switch whether hidden or show outdoor data.

## 2.4.4

##### 2018-11-21

🎉 New Features

- Use mapxus style as default style
- Match all element info by new mapxue style
- Floor selector control use mapxus style

## 2.4.3

##### 2018-11-13

🎉 New Features

- Add transform poi language function by browser current language

## 2.4.2

##### 2018-10-26

🎉 New Features

- Get style's content interface update to v3 version

## 2.4.1

##### 2018-10-23

🎉 New Features

- Support auto to find fit's resource by network

## 2.4.0

##### 2018-10-23

🎉 New Features

- All request enable compress (add brm as resource-middleware)

## 2.3.2

##### 2018-10-11

🎉 New Features

- Use system default fonts

## 2.3.1

##### 2018-10-09

🎉 New Features

- Init map no longer mandatory call renderComplete function

🐛 Bugfixes

- Fixed api user/verification interface can not headers have identifier

## 2.3.0

##### 2018-09-10

🎉 New Features

- Developer can see the building Control and floor control is initiated by default. ([#160242067])
- Developer can create the map with particular building directly. ([#160242318])
- Developer can create the map with building in specific floor. ([#160242353])
- Developer can create the map with specific POI. ([#160242502])
- Modify setStyle url token from params change to header.

[#160242067]: https://www.pivotaltracker.com/story/show/160242067
[#160242318]: https://www.pivotaltracker.com/story/show/160242318
[#160242353]: https://www.pivotaltracker.com/story/show/160242353
[#160242502]: https://www.pivotaltracker.com/story/show/160242502

## 2.2.1

##### 2018-08-29

🎉 New Features

- Add enable and disable on-click outdoor map will hidden building function
- Route service use v2(api) version

## 2.2.0

##### 2018-08-28

🎉 New Features

- Optimize marker module, allow multi instance, load image speed more fast
- Add floor switch function for floors_control, let user can call it to change floor, and floors_control will sync change
- Add building switch by id function, input buildingId and then will auto jump to target building and select building

🐛 Bugfixes

- Fixed marker can not hidden when bind buildingId and floor, then click map outdoor place
- Fixed clicked map outdoor background content, building can not switch to without select status

## 2.1.4

##### 2018-08-23

🐛 Bugfixes

- Fixed any clicked map other layer, that will auto switch indoor or outdoor layer

## 2.1.3

##### 2018-08-16

🎉 New Features

- Add mapxus style theme map
- Developer can see the shape of the building even it is inactivated ([#159815045])

🐛 Bugfixes

- Fixed when on-click marker, it will together touch map click listener

[#159815045]: https://www.pivotaltracker.com/story/show/159815045

## 2.1.2

##### 2018-08-13

🐛 Bugfixes

- Fixed Request-filter beeview url path not need to add identifier

## 2.1.1

##### 2018-08-09

🐛 Bugfixes

- Fixed if without enabled onMapClickListener, will display can not switch floor

## 2.1.0

##### 2018-08-09

🎉 New Features

1. All request headers added identifier
2. Update switch theme function (use v2 version style)

## 2.0.0-beta.2

##### 2018-08-02

🎉 New Features

1. Developer can click to select building when I use the beemap SDK ([#159458589])

[#159458589]: https://www.pivotaltracker.com/story/show/159458589

## 2.0.0-beta.1

##### 2018-07-26

🎉 New Features

1. Add attribution control

## 2.0.0

##### 2018-07-24

🎉 New Features

1. No assembly the outdoor functions of mapbox, only the indoor functions of mapxus.
2. Must be dependent mapbox-gl.js and mapbox-gl.css
3. Optimize loading indoor data method

## 1.2.3

##### 2018-07-06

🎉 New Features

1. modify addPoint function, allow to change style
2. add setMinzoom function
3. add setMaxzoom function
4. add setMaxBounds function

## 1.2.2

##### 2018-07-02

🎉 New Features

1. Add **refresh token** function

## 1.2.1

##### 2018-06-27

✨ Usability

1. Do not hard code maphive_poi, use regular expression
2. Support old schema format

## 1.2.0

##### 2018-06-22

🎉 New Features

1. add token validation
2. add setLayoutProperty (for support layer icon switch)
3. server url use prod env

## 1.2.0-beta.2

##### 2018-06-14

🎉 New Features

1. base_url since bms-test change to bms-api-test
2. add setLayoutProperty (for support layer icon switch)

## 1.2.0-beta.1

##### 2018-06-13

🎉 New Features

- http-request methods since fetch change to axios
- all http-request url add token(style and bms)

## 1.1.1

##### 2018-06-08

🎉 New Features

- add **switch style theme** function

## 1.1.0

##### 2018-05-29

🎉 New Features

- add transformRequest apply to beeview api
- add the draw of remove function

✨ Usability

- optimize floors function
- optimize **building filter control**

🎓 Walkthrough

- add typedoc
- add GUIDE.md
- add tslint

## 1.0.0

##### 2018-05-11

🎉 New Features

- setup project function
  - Display Map
    1. Load Map
    2. Load Map Listener
  - Map Controller
    1. Floor Controller
    2. Building Filter
    3. Map Scale Controler
    4. Map Zoom and Compass Controller
  - Map Operation Controller
    1. Tilt Map
    2. Move Map
    3. Zoom Map
  - Map Event
    1. Switch Floor
    2. Click on Map
    3. Click on POI
    4. Add POI
  - Daw Map
    1. Draw Point
    2. Draw Line
    3. Draw Surface
  - Map Data Acquisition
    1. Getting Floor number
    2. No of Floors List
    3. Building Basic Info
  - Search Building
    1. Search by distance
    2. Search by area
    3. Search by ID
  - POI Search
    1. Search by distance
    2. search by area
    3. Search by ID
    4. Search by building
  - Indoor Pathway
    1. Point-to-Point Pathway
- mapbox logo replace mapxus
