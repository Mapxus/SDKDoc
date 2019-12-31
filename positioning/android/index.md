[API reference](https://mapxussample.github.io/mapxus-positioning-sample-android/)

[Change Log](https://github.com/MapxusSample/mapxus-positioning-sample-android/blob/master/CHANGELOG.md)

# Mapxus Positioning Android SDK Instruction


## 1. Versioning

### 1.1 Minimum Android Version

| Version |Supports| 
| --- | --- |
| 4.4| Mapxus Maps + Indoor Positioning|
| 6.0| Mapxus Maps + Indoor Positioning|
| 7.0 and above | Mapxus Maps + Indoor Positioning |

Devices that can provide raw GNSS measurements can perform indoor/outdoor positioning transition. Android version 7.0 or above is required.


### 1.2 Sensor Information

|Sensor|Impact of Missing Sensor|
| --- | --- |
| WIFI| Indoor positioning is inaccessible without WIFI sensor. For devices of Android 6.0 and above, you have to  activate location service (Setting --> Location) before getting WIFI information.| 
| GPS| Outdoor positioning is inaccessible without GPS sensor. Please activate location service and make sure that the device is not in battery saving mode (Setting -->Location, Battery Saving). GPS data cannot be acquired  and outdoor position will not be updated when in battery saving mode.| 
| GNSS| GNSS Measurements (only equipped in Android 7.0 and above)  support the switch between indoor positioning and outdoor positioning. For devices without GNSS measurements, outdoor positioning will not be working.| 
| Step Counter| -The lack of Step Counter and Accelerometer will lead to the missing of Mapxus Step Counter. The missing of Mapxus Step Counter hardly effects positioning accuracy. However, the positionig may shutter because of decreasing location update frequecy; <br>-If the device is equipped with Accelerometer but not Step Counter, it will shift to substitution algorithms. Substitution algorithms have high sensitivity that a minor shake of the device would be detected as a step;<br>-If the device is equipped with Step Counter but not Accelerometer, it will ask for Step Counter. However, some mobile models have less responsive Step Counter;<br> -If the device is equipped with both Step Counter and Accelerometer, it will ask for both sensors. When Step Counter of the device have no return of data for some time, it will shift to substitution algorithms until Step Counter has return of data. In this case, problem of less-responsive Step Counter will be solved.| 
| Accelerometer|  -The lack of Step Counter and Accelerometer will lead to the missing of Mapxus Step Counter. The missing of Mapxus Step Counter hardly effects positioning accuracy. However, the positionig may shutter because of decreasing location update frequecy; <br>-If the device is equipped with Accelerometer but not Step Counter, it will shift to substitution algorithms. Substitution algorithms have high sensitivity that a minor shake of the device would be detected as a step;<br>-If the device is equipped with Step Counter but not Accelerometer, it will ask for Step Counter. However, some mobile models have less responsive Step Counter;<br> -If the device is equipped with both Step Counter and Accelerometer, it will ask for both sensors. When Step Counter of the device have no return of data for some time, it will shift to substitution algorithms until Step Counter has return of data. In this case, problem of less-responsive Step Counter will be solved.| 
|Pressure| -During indoor positioning, floor will be always checked. Device without Pressure Sensor may suffer changing floor position. Floor change detection will be responsive but may be leaping; <br>-For device with Pressure Sensor, floor will be checked only when positioning floor is changed. Positioning floor detection will be stable. |
|Rotation vector| -For devices equipped with both Rotaton Vector and Gyroscope, the algorithms will calculate current rotation by both sensors so as to get a more accurate result;<br> -For devices equipped with Rotation Vector but not Gyroscope, the algorithms will calculate by Rotation Vector sensor. The result of rotation may not be that accurate;<br>-For devices equipped without Rotation Vector and Gyroscope, rotation cannot be obtained.|
|Gyroscope| -For devices equipped with both Rotaton Vector and Gyroscope, the algorithms will calculate current rotation by both sensors so as to get a more accurate result;<br> -For devices equipped with Rotation Vector but not Gyroscope, the algorithms will calculate by Rotation Vector sensor. The result of rotation may not be that accurate;<br>-For devices equipped without Rotation Vector and Gyroscope, rotation cannot be obtained.|



## 2. Create a Project

### 2.1 Create an Android Project

First of all, create a new Android project ([Instruction for creating an Android project](https://developer.android.com/studio/projects/create-project)).Then, configure your project according to the following steps.

### 2.2 Configure the Project

#### 2.2.1 Configure Repository Address of Your Project

Add jcenter() in build.gradle under the root directory in your project.

~~~groovy
allprojects {
	repositories {
		jcenter()
	}
}
~~~

#### 2.2.2 Add Positioning SDK Dependencies
Add dependencies in `build.gradle` file of necessary modules: 

~~~groovy
dependencies {
	implementation 'com.mapxus.positioning:positioning:0.3.13'
}
~~~

***Note***：Please make sure that your project's minimum SDK Version is at 19 or above. Therefore, please operate it in Android 4.4 or above.

#### 2.2.3 Add Licensed APP ID and Secret

There are two ways of adding app id and secret. You can choose one as needed.

##### Option 1: Add *meta-data* in *application* node of **AndroidManifest.xml** file.

```xml
<application ...
	<meta-data
	      android:name="com.mapxus.api.v1.appid"
	      android:value="your appid" />
	<meta-data
	      android:name="com.mapxus.api.v1.secret"
	      android:value="your secret" />
</application>
```

##### Option 2: Add app id and secret when getting MapxusPositioningClient instance


~~~java
MapxusPositioningClient mMapxusPositioningClient = 
MapxusPositioningClient.getInstance(this, "your appid", "your secret");
~~~


#### 2.2.4 Set up Permissions in AndroidMainfest.xml in Your Application Manifest Files
~~~xml
<!--access information about networks to support relevant interface-->
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<!--to access approximate location through Internet-->
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<!--to access precise location-->
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<!--to access information about Wifi networks for positioning-->
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!--to change Wifi connectivity state -->
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE"/>
<!--to open network socket-->
<uses-permission android:name="android.permission.INTERNET" />
~~~

**Remarks**:

Please refer to Positioning Sample APP about how to dynamically ask for permissions. `Manifest.permission.READ_PHONE_STATE` permission is not required to ask for in terms of **Mapxus Positioning SDK 0.3.3 and above**. Permission of `Manifest.permission.WRITE_EXTERNAL_STORAGE` is required to ask for in terms of **Mapxus Positioning SDK 0.3.4 and above**.


#### 2.2.5 Request Permissions When Using Android 6.0 or above

If your device is in Android 6.0 or above, when configuring your project, you need to grant all permissions as below.

For devices using Android 6.0 and above, if targetSdkVersion is less than 23, all permissions will be granted without asking. However, if targetSdkVersion is no more than 23, permissions will be asked. [Referrence: Guidebook of permissions requesting in Android](https://developer.android.com/training/permissions/requesting)


**Mapxus Positioning SDK** will ask these permissions：

*  `Manifest.permission.ACCESS_FINE_LOCATION`
*  `Manifest.permission.ACCESS_COARSE_LOCATION`


Remarks: You can refer to Positioning Sample APP about how to ask permissions dynamically. However, **Mapxus Positioning SDK 0.3.3** and above will not ask permission of `Manifest.permission.READ_PHONE_STATE`; **Mapxus Positioning SDK 0.3.4** and above will not ask `Manifest.permission.WRITE_EXTERNAL_STORAGE`.

### 2.3 Device Hardware Requirement

1. Location is always updated through asking network during the process of positioning. Please make sure your **network** is available;

2. Location is always updated through asking Wifi network. Please **activate Wifi** during positioning;

3. In terms of devices (Android 6.0 or above) with native system or some third-parties, manufacturers customized system, Wifi information is not accessible because GPS is not on. In this case, it is impossible to access location. Therefore, when using Bee Track in devices (Android 6.0 or above), **Location Service** should be available during positioning. 

4. Make sure the device is equipped with **pressure sensor** if you are using **Mapxus Positioning SDK 0.3.5 and below**. Pressure sensor is not required for **Mapxus Positioning SDK 0.3.5 and above**. However, in this case, current floor may not be stable. For **Mapxus Positioning SDK 0.3.6** and above, devices without pressure sensor can use positioning service in one floor. For changing floor during positioning, you should call changeFloor.

5. **Mapxus Positioning SDK 0.3.0** and above allow switch between  indoor positioning and outdoor positioning. This feature only works for smart phones with raw GNSS measurements (mostly producing after 2016 and equipped with Android 7.0 and above). Click [here] (https://developer.android.com/guide/topics/sensors/gnss#supported-devices) to see details of supporting devices. If your devices are not able to support switch between indoor positioning and outdoor positioning, it will position indoor by default. You may use `Utils.isSupportGnss(Context context)` to determine.

6. When using **Mapxus Positioning SDK 0.3.7** and above version, you should activate precise **location service**. Otherwise, it will return `ERROR_LOCATION_SERVICE_DISABLED` error. By the following codes, you can set location precision:

~~~java
Intent locationIntent = new Intent(Settings.ACTION_LOCATION_SOURCE_SETTINGS);
startActivity(locationIntent);
~~~
 


### 2.4 Notice

1. **Mapxus Positioning SDK 0.3.6** and above are using new authorization package. Please contact us and renew your id and secret.

2. When using **Mapxus Positioning SDK 0.3.6**, please use MapxusMap SDK versioning **2.3.3-beta** and above if you need to use Mapxus Map.

3. When using **Mapxus Positioning SDK 0.3.7** and above, please use Mapxus Map versioning **2.4.1** and above.

| Mapxus Positioning Map SDK Version  |  Mapxus Map SDK Version  |
| ----------------------- |  --------------------------- |
|    0.3.0 ~ 0.3.5        |  2.0.0-beta ~ 2.2.1-beta     |
|    0.3.6				   |  2.3.3-beta                  |
|    0.3.7 and above|  2.4.1 and above              |
|    0.4。0 and above     |    3.0.0 and above      |


## 3.Access Indoor Location

### 3.1 Examples

Example of IndoorPositionerClient (shoule be called at main thread): 

~~~java
//declaire MapxusPositioningClient object in main thread
public MapxusPositioningClient mMapxusPositioningClient;

//access MapxusPositioningClient example
mMapxusPositioningClient = MapxusPositioningClient.getInstance(getApplicationContext());

//set positioning listener
mMapxusPositioningClient.setPositioningListener(listener);
~~~

### 3.2 Configure Parameters

~~~java
//skip this option and positioning will take default value
MapxusPositioningOption option = new MapxusPositioningOption();

//configure positioning mode; NORMAL,BACKGROUND, and GAME is optional; default NORMAL, (BACKFROUND and GAME are disabled now)
positionerOption.setMode(LocationMode.NORMAL);

//configure positioning parameters; otherwise, default parameter will be taken when start positioning
mIndoorPositionerClient.setPositionerOption(option);
~~~

### 3.3 Access Location

Implement MapxusPositioningListener interface and access location 

~~~java
//implement MapxusPositioningListener
private MapxusPositioningListener listener = new MapxusPositioningListener() {
	@Override
	public void onStateChange(PositioningState state) {
		//callback of state change during positioning
		//WAITING >>>> callback between calling start() and position successfully
		//RUNNING >>>> callback  when position successfully
		//PAUSED  >>>> callback after successfully callling pause()
		//STOPPED >>>> callback after successfully calling stop()	}

	@Override
	public void onError(ErrorInfo errorInfo) {
		//callback of error information; check API documentation for detailed error information;
		//return of error information after positioning; if errorCode == ERROR_WARNING, position engine will keep running;
		//if other errors happen, engine will be destroyed after error return; then you should re-instantiate IndoorLocatorClient; initialize before location successfully may lead to error returns;	}

	@Override
	public void onOrientationChange(float orientation, SensorAccuracy accuracy) {
		//orientation change callback, value ranging [0, 360]; 0 due north, 90 east, 180 south, and 270 west;
		//accuracy refers to the accuracy level of current orientation. You can adjust the orientation by waving your device as arabic number 8 under the non-high accuarcy mode.
	}

	@Override
	public void onLocationChange(PositioningLocation location) {
		//location information callback, including building ID, floor, longitude&latitude, positioning accuracy
	}
	
};

~~~
### 3.4 Start Positioning

~~~java
//call start() and wait for automatic response of position result; constant ask of  updated location after successful positioning;
//Valid for the first call; invalid for the other states. Please stop() and renew IndoorPositionerClient example executio after restart();
//successfuly call back PositioningState.RUNNING
mMapxusPositioningClient.start(); //start positioning
~~~

### 3.5 Pause Positioning
~~~java
//positionging engine for pause running state (invalid for the other states); no calling position and not destroy positioning service
//successfully callback pause PositioningState.PAUSED
mMapxusPositioningClient.pause();
~~~
### 3.6 Resume Positioning
~~~java
//positioning engine for resume pause state (invalid for the other states); constant call for updated location
//successfully callback resume PositioningState.RUNNING
mMapxusPositioningClient.resume();
~~~
### 3.7 Change Positioning Mode
~~~java
//change positioning mode in running state after successfully positioning (invalid for the other states) (not working now)
mMapxusPositioningClient.changeMode(newMode);
~~~
### 3.8 Change Floor
~~~java
//change floor in running state after successfully positioning (invalid for the other states);
mMapxusPositioningClient.changeFloor(floor);
~~~
### 3.9 Stop Positioning
~~~java
//valid for any states after start positioning; able to stop positioning service in waiting, pause, running states; successfully callback PositionerState.STOPED
//stop positioning, destroy positioning engine and resume IndoorPositionerClient instance;
 mMapxusPositioningClient.stop();
~~~
### 3.10 Enable Backgroung Positioning Service
~~~java
//enable background positioning service;
//For devices (Android6.0 and above), once app goes to background, system will define it as vacant for energy saving;
//Stop network access and stop synchronization will lead to unusual positioning service. Enable background positioning service can avoid this case;
mMapxusPositioningClient.enableBackgroundPositioning(1, notification);
~~~
### 3.11 Disable Background Positioning Service
~~~java
//disable background positioning service when APP goes to the front;
mMapxusPositioningClient.disableBackgroundPositioning(true);
~~~

### 3.12 Change Floor During Positioning

~~~java
//change floor during positioning;
mMapxusPositioningClient.changeFloor(positioningFloor);
~~~



