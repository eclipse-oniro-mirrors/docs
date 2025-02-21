# @ohos.geolocation (Geolocation)

The **geolocation** module provides a wide array of location services, including GNSS positioning, network positioning, geocoding, reverse geocoding, and geofencing.

> **NOTE**
> The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> The APIs provided by this module are no longer maintained since API version 9. You are advised to use [geoLocationManager](js-apis-geoLocationManager.md) instead.

## Applying for Permissions

Before using basic location capabilities, check whether your application has been granted the permission to access the device location information. If not, your application needs to obtain the permission from the user as described below.

The system provides the following location permissions:
- ohos.permission.LOCATION

- ohos.permission.APPROXIMATELY_LOCATION

- ohos.permission.LOCATION_IN_BACKGROUND

If your application needs to access the device location information, it must first apply for required permissions. Specifically speaking:

API versions earlier than 9: Apply for **ohos.permission.LOCATION**.

API version 9 and later: Apply for **ohos.permission.APPROXIMATELY_LOCATION**, or apply for **ohos.permission.APPROXIMATELY_LOCATION** and **ohos.permission.LOCATION**. Note that **ohos.permission.LOCATION** cannot be applied for separately.

| API Version| Location Permission| Permission Application Result| Location Accuracy|
| -------- | -------- | -------- | -------- |
| Earlier than 9| ohos.permission.LOCATION | Successful| Location accurate to meters.|
| 9 and later| ohos.permission.LOCATION | Failed| No location obtained.|
| 9 and later| ohos.permission.APPROXIMATELY_LOCATION | Successful| Location accurate to 5 kilometers.|
| 9 and later| ohos.permission.APPROXIMATELY_LOCATION and ohos.permission.LOCATION| Successful| Location accurate to meters.|

If your application needs to access the device location information when running in the background, it must be configured to be able to run in the background and be granted the **ohos.permission.LOCATION_IN_BACKGROUND** permission. In this way, the system continues to report device location information after your application moves to the background.

You can declare the required permission in your application's configuration file. For details, see [Access Control (Permission) Development](../../security/accesstoken-guidelines.md).


## Modules to Import

```ts
import geolocation from '@ohos.geolocation';
```

## geolocation.on('locationChange')<sup>(deprecated)</sup>

on(type: 'locationChange', request: LocationRequest, callback: Callback&lt;Location&gt;): void

Registers a listener for location changes with a location request initiated.

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.on('locationChange')](js-apis-geoLocationManager.md#geolocationmanageronlocationchange).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value **locationChange** indicates a location change event.|
  | request |  [LocationRequest](#locationrequestdeprecated) | Yes| Location request.|
  | callback | Callback&lt;[Location](#locationdeprecated)&gt; | Yes| Callback used to return the location change event.|



**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  let requestInfo = {'priority': 0x203, 'scenario': 0x300, 'timeInterval': 0, 'distanceInterval': 0, 'maxAccuracy': 0};
  let locationChange = (location) => {
      console.log('locationChanger: data: ' + JSON.stringify(location));
  };
  geolocation.on('locationChange', requestInfo, locationChange);
  ```


## geolocation.off('locationChange')<sup>(deprecated)</sup>

off(type: 'locationChange', callback?: Callback&lt;Location&gt;): void

Unregisters the listener for location changes with the corresponding location request deleted.

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.off('locationChange')](js-apis-geoLocationManager.md#geolocationmanagerofflocationchange).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value **locationChange** indicates a location change event.|
  | callback | Callback&lt;[Location](#locationdeprecated)&gt; | No| Callback to unregister. If this parameter is not specified, all callbacks of the specified event type are unregistered.|


**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  let requestInfo = {'priority': 0x203, 'scenario': 0x300, 'timeInterval': 0, 'distanceInterval': 0, 'maxAccuracy': 0};
  let locationChange = (location) => {
      console.log('locationChanger: data: ' + JSON.stringify(location));
  };
  geolocation.on('locationChange', requestInfo, locationChange);
  geolocation.off('locationChange', locationChange);
  ```


## geolocation.on('locationServiceState')<sup>(deprecated)</sup>

on(type: 'locationServiceState', callback: Callback&lt;boolean&gt;): void

Registers a listener for location service status change events.

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.on('locationEnabledChange')](js-apis-geoLocationManager.md#geolocationmanageronlocationenabledchange).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value **locationServiceState** indicates a location service status change event.|
  | callback | Callback&lt;boolean&gt; | Yes| Callback used to return the location service status change event.|


**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  let locationServiceState = (state) => {
      console.log('locationServiceState: ' + JSON.stringify(state));
  }
  geolocation.on('locationServiceState', locationServiceState);
  ```


## geolocation.off('locationServiceState')<sup>(deprecated)</sup>

off(type: 'locationServiceState', callback?: Callback&lt;boolean&gt;): void;

Unregisters the listener for location service status change events.

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.off('locationEnabledChange')](js-apis-geoLocationManager.md#geolocationmanagerofflocationenabledchange).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value **locationServiceState** indicates a location service status change event.|
  | callback | Callback&lt;boolean&gt; | No| Callback to unregister. If this parameter is not specified, all callbacks of the specified event type are unregistered.|


**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  let locationServiceState = (state) => {
      console.log('locationServiceState: state: ' + JSON.stringify(state));
  }
  geolocation.on('locationServiceState', locationServiceState);
  geolocation.off('locationServiceState', locationServiceState);
  ```


## geolocation.on('cachedGnssLocationsReporting')<sup>(deprecated)</sup>

on(type: 'cachedGnssLocationsReporting', request: CachedGnssLocationsRequest, callback: Callback&lt;Array&lt;Location&gt;&gt;): void;

Registers a listener for cached GNSS location reports.

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.on('cachedGnssLocationsChange')](js-apis-geoLocationManager.md#geolocationmanageroncachedgnsslocationschange).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Gnss

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value **cachedGnssLocationsReporting** indicates reporting of cached GNSS locations.|
  | request |  [CachedGnssLocationsRequest](#cachedgnsslocationsrequestdeprecated) | Yes| Request for reporting cached GNSS location.|
  | callback | Callback&lt;Array&lt;[Location](#locationdeprecated)&gt;&gt; | Yes| Callback used to return cached GNSS locations.|


**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  let cachedLocationsCb = (locations) => {
      console.log('cachedGnssLocationsReporting: locations: ' + JSON.stringify(locations));
  }
  let requestInfo = {'reportingPeriodSec': 10, 'wakeUpCacheQueueFull': true};
  geolocation.on('cachedGnssLocationsReporting', requestInfo, cachedLocationsCb);
  ```


## geolocation.off('cachedGnssLocationsReporting')<sup>(deprecated)</sup>

off(type: 'cachedGnssLocationsReporting', callback?: Callback&lt;Array&lt;Location&gt;&gt;): void;

Unregisters the listener for cached GNSS location reports.

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.off('cachedGnssLocationsChange')](js-apis-geoLocationManager.md#geolocationmanageroffcachedgnsslocationschange).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Gnss

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value **cachedGnssLocationsReporting** indicates reporting of cached GNSS locations.|
  | callback | Callback&lt;Array&lt;[Location](#locationdeprecated)&gt;&gt; | No| Callback to unregister. If this parameter is not specified, all callbacks of the specified event type are unregistered.|


**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  let cachedLocationsCb = (locations) => {
      console.log('cachedGnssLocationsReporting: locations: ' + JSON.stringify(locations));
  }
  let requestInfo = {'reportingPeriodSec': 10, 'wakeUpCacheQueueFull': true};
  geolocation.on('cachedGnssLocationsReporting', requestInfo, cachedLocationsCb);
  geolocation.off('cachedGnssLocationsReporting');
  ```


## geolocation.on('gnssStatusChange')<sup>(deprecated)</sup>

on(type: 'gnssStatusChange', callback: Callback&lt;SatelliteStatusInfo&gt;): void;

Registers a listener for GNSS satellite status change events.

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.on('satelliteStatusChange')](js-apis-geoLocationManager.md#geolocationmanageronsatellitestatuschange).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Gnss

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value **gnssStatusChange** indicates a GNSS satellite status change.|
  | callback | Callback&lt;[SatelliteStatusInfo](#satellitestatusinfodeprecated)&gt; | Yes| Callback used to return GNSS satellite status changes.|


**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  let gnssStatusCb = (satelliteStatusInfo) => {
      console.log('gnssStatusChange: ' + JSON.stringify(satelliteStatusInfo));
  }
  geolocation.on('gnssStatusChange', gnssStatusCb);
  ```


## geolocation.off('gnssStatusChange')<sup>(deprecated)</sup>

off(type: 'gnssStatusChange', callback?: Callback&lt;SatelliteStatusInfo&gt;): void;

Unregisters the listener for GNSS satellite status change events.

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.off('satelliteStatusChange')](js-apis-geoLocationManager.md#geolocationmanageroffsatellitestatuschange).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Gnss

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value **gnssStatusChange** indicates a GNSS satellite status change.|
  | callback | Callback&lt;[SatelliteStatusInfo](#satellitestatusinfodeprecated)&gt; | No| Callback to unregister. If this parameter is not specified, all callbacks of the specified event type are unregistered.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  let gnssStatusCb = (satelliteStatusInfo) => {
      console.log('gnssStatusChange: ' + JSON.stringify(satelliteStatusInfo));
  }
  geolocation.on('gnssStatusChange', gnssStatusCb);
  geolocation.off('gnssStatusChange', gnssStatusCb);
  ```


## geolocation.on('nmeaMessageChange')<sup>(deprecated)</sup>

on(type: 'nmeaMessageChange', callback: Callback&lt;string&gt;): void;

Registers a listener for GNSS NMEA message change events.

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.on('nmeaMessage')](js-apis-geoLocationManager.md#geolocationmanageronnmeamessage).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Gnss

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value **nmeaMessageChange** indicates a GNSS NMEA message change.|
  | callback | Callback&lt;string&gt; | Yes| Callback used to return GNSS NMEA message changes.|


**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  let nmeaCb = (str) => {
      console.log('nmeaMessageChange: ' + JSON.stringify(str));
  }
  geolocation.on('nmeaMessageChange', nmeaCb );
  ```


## geolocation.off('nmeaMessageChange')<sup>(deprecated)</sup>

off(type: 'nmeaMessageChange', callback?: Callback&lt;string&gt;): void;

Unregisters the listener for GNSS NMEA message change events.

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.off('nmeaMessage')](js-apis-geoLocationManager.md#geolocationmanageroffnmeamessage).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Gnss

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value **nmeaMessageChange** indicates a GNSS NMEA message change.|
  | callback | Callback&lt;string&gt; | No| Callback to unregister. If this parameter is not specified, all callbacks of the specified event type are unregistered.|


**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  let nmeaCb = (str) => {
      console.log('nmeaMessageChange: ' + JSON.stringify(str));
  }
  geolocation.on('nmeaMessageChange', nmeaCb);
  geolocation.off('nmeaMessageChange', nmeaCb);
  ```


## geolocation.on('fenceStatusChange')<sup>(deprecated)</sup>

on(type: 'fenceStatusChange', request: GeofenceRequest, want: WantAgent): void;

Registers a listener for status change events of the specified geofence.

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.on('gnssFenceStatusChange')](js-apis-geoLocationManager.md#geolocationmanagerongnssfencestatuschange).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Geofence

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value **fenceStatusChange** indicates a geofence status change.|
  | request |  [GeofenceRequest](#geofencerequestdeprecated) | Yes| Geofencing request.|
  | want | [WantAgent](js-apis-app-ability-wantAgent.md) | Yes| **WantAgent** used to return geofence (entrance or exit) events.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  import wantAgent from '@ohos.app.ability.wantAgent';
  
  let wantAgentInfo = {
      wants: [
          {
              bundleName: "com.example.myapplication",
              abilityName: "EntryAbility",
              action: "action1"
          }
      ],
      operationType: wantAgent.OperationType.START_ABILITY,
      requestCode: 0,
      wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG],
  };
  
  wantAgent.getWantAgent(wantAgentInfo).then((wantAgentObj) => {
    let requestInfo = {'priority': 0x201, 'scenario': 0x301, "geofence": {"latitude": 121, "longitude": 26, "radius": 100, "expiration": 10000}};
    geolocation.on('fenceStatusChange', requestInfo, wantAgentObj);
  });
  ```


## geolocation.off('fenceStatusChange')<sup>(deprecated)</sup>

off(type: 'fenceStatusChange', request: GeofenceRequest, want: WantAgent): void;

Unregisters the listener for status change events of the specified geofence.

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.off('gnssFenceStatusChange')](js-apis-geoLocationManager.md#geolocationmanageroffgnssfencestatuschange).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Geofence

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value **fenceStatusChange** indicates a geofence status change.|
  | request | [GeofenceRequest](#geofencerequestdeprecated) | Yes| Geofencing request.|
  | want | [WantAgent](js-apis-app-ability-wantAgent.md) | Yes| **WantAgent** used to return geofence (entrance or exit) events.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  import wantAgent from '@ohos.app.ability.wantAgent';
  
  let wantAgentInfo = {
      wants: [
          {
              bundleName: "com.example.myapplication",
              abilityName: "EntryAbility",
              action: "action1",
          }
      ],
      operationType: wantAgent.OperationType.START_ABILITY,
      requestCode: 0,
      wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
  };
  
  wantAgent.getWantAgent(wantAgentInfo).then((wantAgentObj) => {
    let requestInfo = {'priority': 0x201, 'scenario': 0x301, "geofence": {"latitude": 121, "longitude": 26, "radius": 100, "expiration": 10000}};
    geolocation.on('fenceStatusChange', requestInfo, wantAgentObj);
    geolocation.off('fenceStatusChange', requestInfo, wantAgentObj);
  });
  ```


## geolocation.getCurrentLocation<sup>(deprecated)</sup>

getCurrentLocation(request: CurrentLocationRequest, callback: AsyncCallback&lt;Location&gt;): void

Obtains the current location. This API uses an asynchronous callback to return the result. 

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.getCurrentLocation](js-apis-geoLocationManager.md#geolocationmanagergetcurrentlocation).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | request | [CurrentLocationRequest](#currentlocationrequestdeprecated) | Yes| Location request.|
  | callback | AsyncCallback&lt;[Location](#locationdeprecated)&gt; | Yes| Callback used to return the current location.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  let requestInfo = {'priority': 0x203, 'scenario': 0x300,'maxAccuracy': 0};
  let locationChange = (err, location) => {
      if (err) {
          console.log('locationChanger: err=' + JSON.stringify(err));
      }
      if (location) {
          console.log('locationChanger: location=' + JSON.stringify(location));
      }
  };
  geolocation.getCurrentLocation(requestInfo, locationChange);
  ```


## geolocation.getCurrentLocation<sup>(deprecated)</sup>

getCurrentLocation(callback: AsyncCallback&lt;Location&gt;): void


Obtains the current location. This API uses an asynchronous callback to return the result. 

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.getCurrentLocation](js-apis-geoLocationManager.md#geolocationmanagergetcurrentlocation).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;[Location](#locationdeprecated)&gt; | Yes| Callback used to return the current location.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  let locationChange = (err, location) => {
      if (err) {
          console.log('locationChanger: err=' + JSON.stringify(err));
      }
      if (location) {
          console.log('locationChanger: location=' + JSON.stringify(location));
      }
  };
  geolocation.getCurrentLocation(locationChange);
  ```


## geolocation.getCurrentLocation<sup>(deprecated)</sup>

getCurrentLocation(request?: CurrentLocationRequest): Promise&lt;Location&gt;

Obtains the current location. This API uses a promise to return the result. 

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.getCurrentLocation](js-apis-geoLocationManager.md#geolocationmanagergetcurrentlocation-2).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | request | [CurrentLocationRequest](#currentlocationrequestdeprecated) | No| Location request.|

**Return value**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | Promise&lt;[Location](#locationdeprecated)&gt; |[Location](#locationdeprecated)|NA| Promise used to return the current location.|


**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  let requestInfo = {'priority': 0x203, 'scenario': 0x300,'maxAccuracy': 0};
  geolocation.getCurrentLocation(requestInfo).then((result) => {
      console.log('current location: ' + JSON.stringify(result));
  });
  ```


## geolocation.getLastLocation<sup>(deprecated)</sup>

getLastLocation(callback: AsyncCallback&lt;Location&gt;): void

Obtains the previous location. This API uses an asynchronous callback to return the result.

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.getLastLocation](js-apis-geoLocationManager.md#geolocationmanagergetlastlocation).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;[Location](#locationdeprecated)&gt; | Yes| Callback used to return the previous location.|


**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  geolocation.getLastLocation((err, data) => {
      if (err) {
          console.log('getLastLocation: err=' + JSON.stringify(err));
      }
      if (data) {
          console.log('getLastLocation: data=' + JSON.stringify(data));
      }
  });
  ```


## geolocation.getLastLocation<sup>(deprecated)</sup>

getLastLocation(): Promise&lt;Location&gt;

Obtains the previous location. This API uses a promise to return the result. 

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.getLastLocation](js-apis-geoLocationManager.md#geolocationmanagergetlastlocation).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

**Return value**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | Promise&lt;[Location](#locationdeprecated)&gt; | [Location](#locationdeprecated)|NA|Promise used to return the previous location.|


**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  geolocation.getLastLocation().then((result) => {
      console.log('getLastLocation: result: ' + JSON.stringify(result));
  });
  ```


## geolocation.isLocationEnabled<sup>(deprecated)</sup>

isLocationEnabled(callback: AsyncCallback&lt;boolean&gt;): void

Checks whether the location service is enabled. This API uses an asynchronous callback to return the result.

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.isLocationEnabled](js-apis-geoLocationManager.md#geolocationmanagerislocationenabled).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | Yes| Callback used to return the location service status.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  geolocation.isLocationEnabled((err, data) => {
      if (err) {
          console.log('isLocationEnabled: err=' + JSON.stringify(err));
      }
      if (data) {
          console.log('isLocationEnabled: data=' + JSON.stringify(data));
      }
  });
  ```


## geolocation.isLocationEnabled<sup>(deprecated)</sup>

isLocationEnabled(): Promise&lt;boolean&gt;

Checks whether the location service is enabled. This API uses a promise to return the result.

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.isLocationEnabled](js-apis-geoLocationManager.md#geolocationmanagerislocationenabled).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

**Return value**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | Promise&lt;boolean&gt; | boolean|NA|Promise used to return the location service status.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  geolocation.isLocationEnabled().then((result) => {
      console.log('promise, isLocationEnabled: ' + JSON.stringify(result));
  });
  ```


## geolocation.requestEnableLocation<sup>(deprecated)</sup>

requestEnableLocation(callback: AsyncCallback&lt;boolean&gt;): void

Requests to enable the location service. This API uses an asynchronous callback to return the result.

> **NOTE**<br>
> This API has been discarded since API version 9. It is recommended that a dialog box be displayed in the application to request the user to go to Settings to enable the location function and specify the scenarios in which the location information will be used in the dialog box.

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | Yes| Callback used to return the location service status.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  geolocation.requestEnableLocation((err, data) => {
      if (err) {
          console.log('requestEnableLocation: err=' + JSON.stringify(err));
      }
      if (data) {
          console.log('requestEnableLocation: data=' + JSON.stringify(data));
      }
  });
  ```


## geolocation.requestEnableLocation<sup>(deprecated)</sup>

requestEnableLocation(): Promise&lt;boolean&gt;

Requests to enable the location service. This API uses a promise to return the result.

> **NOTE**<br>
> This API has been discarded since API version 9. It is recommended that a dialog box be displayed in the application to request the user to go to Settings to enable the location function and specify the scenarios in which the location information will be used in the dialog box.

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

**Return value**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | Promise&lt;boolean&gt; | boolean|NA|Promise used to return the location service status.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  geolocation.requestEnableLocation().then((result) => {
      console.log('promise, requestEnableLocation: ' + JSON.stringify(result));
  });
  ```


## geolocation.isGeoServiceAvailable<sup>(deprecated)</sup>

isGeoServiceAvailable(callback: AsyncCallback&lt;boolean&gt;): void

Checks whether the (reverse) geocoding service is available. This API uses an asynchronous callback to return the result.

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.isGeocoderAvailable](js-apis-geoLocationManager.md#geolocationmanagerisgeocoderavailable).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Geocoder

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | Yes| Callback used to return the (reverse) geocoding service status.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  geolocation.isGeoServiceAvailable((err, data) => {
      if (err) {
          console.log('isGeoServiceAvailable: err=' + JSON.stringify(err));
      }
      if (data) {
          console.log('isGeoServiceAvailable: data=' + JSON.stringify(data));
      }
  });
  ```


## geolocation.isGeoServiceAvailable<sup>(deprecated)</sup>

isGeoServiceAvailable(): Promise&lt;boolean&gt;

Checks whether the (reverse) geocoding service is available. This API uses a promise to return the result.

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.isGeocoderAvailable](js-apis-geoLocationManager.md#geolocationmanagerisgeocoderavailable).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Geocoder

**Return value**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | Promise&lt;boolean&gt; |boolean|NA| Promise used to return the (reverse) geocoding service status.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  geolocation.isGeoServiceAvailable().then((result) => {
      console.log('promise, isGeoServiceAvailable: ' + JSON.stringify(result));
  });
  ```


## geolocation.getAddressesFromLocation<sup>(deprecated)</sup>

getAddressesFromLocation(request: ReverseGeoCodeRequest, callback: AsyncCallback&lt;Array&lt;GeoAddress&gt;&gt;): void

Converts coordinates into geographic descriptions through reverse geocoding. This API uses an asynchronous callback to return the result. 

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.getAddressesFromLocation](js-apis-geoLocationManager.md#geolocationmanagergetaddressesfromlocation).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Geocoder

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | request | [ReverseGeoCodeRequest](#reversegeocoderequestdeprecated) | Yes| Reverse geocoding request.|
  | callback | AsyncCallback&lt;Array&lt;[GeoAddress](#geoaddressdeprecated)&gt;&gt; | Yes| Callback used to return the reverse geocoding result.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  let reverseGeocodeRequest = {"latitude": 31.12, "longitude": 121.11, "maxItems": 1};
  geolocation.getAddressesFromLocation(reverseGeocodeRequest, (err, data) => {
      if (err) {
          console.log('getAddressesFromLocation: err=' + JSON.stringify(err));
      }
      if (data) {
          console.log('getAddressesFromLocation: data=' + JSON.stringify(data));
      }
  });
  ```


## geolocation.getAddressesFromLocation<sup>(deprecated)</sup>

getAddressesFromLocation(request: ReverseGeoCodeRequest): Promise&lt;Array&lt;GeoAddress&gt;&gt;;

Converts coordinates into geographic descriptions through reverse geocoding. This API uses a promise to return the result. 

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.getAddressesFromLocation](js-apis-geoLocationManager.md#geolocationmanagergetaddressesfromlocation-1).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Geocoder

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | request | [ReverseGeoCodeRequest](#reversegeocoderequestdeprecated) | Yes| Reverse geocoding request.|

**Return value**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | Promise&lt;Array&lt;[GeoAddress](#geoaddressdeprecated)&gt;&gt; | Array&lt;[GeoAddress](#geoaddressdeprecated)&gt;|NA|Promise used to return the reverse geocoding result.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  let reverseGeocodeRequest = {"latitude": 31.12, "longitude": 121.11, "maxItems": 1};
  geolocation.getAddressesFromLocation(reverseGeocodeRequest).then((data) => {
      console.log('getAddressesFromLocation: ' + JSON.stringify(data));
  });
  ```


## geolocation.getAddressesFromLocationName<sup>(deprecated)</sup>

getAddressesFromLocationName(request: GeoCodeRequest, callback: AsyncCallback&lt;Array&lt;GeoAddress&gt;&gt;): void

Converts geographic descriptions into coordinates through geocoding. This API uses an asynchronous callback to return the result. 

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.getAddressesFromLocationName](js-apis-geoLocationManager.md#geolocationmanagergetaddressesfromlocationname).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Geocoder

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | request | [GeoCodeRequest](#geocoderequestdeprecated) | Yes| Geocoding request.|
  | callback | AsyncCallback&lt;Array&lt;[GeoAddress](#geoaddressdeprecated)&gt;&gt; | Yes| Callback used to return the geocoding result.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  let geocodeRequest = {"description": "No. xx, xx Road, Pudong District, Shanghai", "maxItems": 1};
  geolocation.getAddressesFromLocationName(geocodeRequest, (err, data) => {
      if (err) {
          console.log('getAddressesFromLocationName: err=' + JSON.stringify(err));
      }
      if (data) {
          console.log('getAddressesFromLocationName: data=' + JSON.stringify(data));
      }
  });
  ```


## geolocation.getAddressesFromLocationName<sup>(deprecated)</sup>

getAddressesFromLocationName(request: GeoCodeRequest): Promise&lt;Array&lt;GeoAddress&gt;&gt;

Converts geographic descriptions into coordinates through geocoding. This API uses a promise to return the result. 

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.getAddressesFromLocationName](js-apis-geoLocationManager.md#geolocationmanagergetaddressesfromlocationname-1).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Geocoder

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | request | [GeoCodeRequest](#geocoderequestdeprecated) | Yes| Geocoding request.|

**Return value**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | Promise&lt;Array&lt;[GeoAddress](#geoaddressdeprecated)&gt;&gt; | Array&lt;[GeoAddress](#geoaddressdeprecated)&gt;|NA|Promise used to return the geocoding result.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  let geocodeRequest = {"description": "No. xx, xx Road, Pudong District, Shanghai", "maxItems": 1};
  geolocation.getAddressesFromLocationName(geocodeRequest).then((result) => {
      console.log('getAddressesFromLocationName: ' + JSON.stringify(result));
  });
  ```


## geolocation.getCachedGnssLocationsSize<sup>(deprecated)</sup>

getCachedGnssLocationsSize(callback: AsyncCallback&lt;number&gt;): void;

Obtains the number of cached GNSS locations. 

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.getCachedGnssLocationsSize](js-apis-geoLocationManager.md#geolocationmanagergetcachedgnsslocationssize).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Gnss

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;number&gt; | Yes| Callback used to return the number of cached GNSS locations. |

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  geolocation.getCachedGnssLocationsSize((err, size) => {
      if (err) {
          console.log('getCachedGnssLocationsSize: err=' + JSON.stringify(err));
      }
      if (size) {
          console.log('getCachedGnssLocationsSize: size=' + JSON.stringify(size));
      }
  });
  ```


## geolocation.getCachedGnssLocationsSize<sup>(deprecated)</sup>

getCachedGnssLocationsSize(): Promise&lt;number&gt;;

Obtains the number of cached GNSS locations. 

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.getCachedGnssLocationsSize](js-apis-geoLocationManager.md#geolocationmanagergetcachedgnsslocationssize-1).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Gnss

**Return value**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | Promise&lt;number&gt; | number|NA|Promise used to return the number of cached GNSS locations.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  geolocation.getCachedGnssLocationsSize().then((result) => {
      console.log('promise, getCachedGnssLocationsSize: ' + JSON.stringify(result));
  });
  ```


## geolocation.flushCachedGnssLocations<sup>(deprecated)</sup>

flushCachedGnssLocations(callback: AsyncCallback&lt;boolean&gt;): void;

Obtains all cached GNSS locations and clears the GNSS cache queue. 

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.flushCachedGnssLocations](js-apis-geoLocationManager.md#geolocationmanagerflushcachedgnsslocations).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Gnss

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | Yes| Callback used to return the operation result.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  geolocation.flushCachedGnssLocations((err, result) => {
      if (err) {
          console.log('flushCachedGnssLocations: err=' + JSON.stringify(err));
      }
      if (result) {
          console.log('flushCachedGnssLocations: result=' + JSON.stringify(result));
      }
  });
  ```


## geolocation.flushCachedGnssLocations<sup>(deprecated)</sup>

flushCachedGnssLocations(): Promise&lt;boolean&gt;;

Obtains all cached GNSS locations and clears the GNSS cache queue. 

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.flushCachedGnssLocations](js-apis-geoLocationManager.md#geolocationmanagerflushcachedgnsslocations-1).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Gnss

**Return value**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | Promise&lt;boolean&gt; |boolean|NA| Promise used to return the operation result.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  geolocation.flushCachedGnssLocations().then((result) => {
      console.log('promise, flushCachedGnssLocations: ' + JSON.stringify(result));
  });
  ```


## geolocation.sendCommand<sup>(deprecated)</sup>

sendCommand(command: LocationCommand, callback: AsyncCallback&lt;boolean&gt;): void;

Sends an extended command to the location subsystem. 

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.sendCommand](js-apis-geoLocationManager.md#geolocationmanagersendcommand).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | command |  [LocationCommand](#locationcommanddeprecated) | Yes| Extended command (string) to be sent.|
  | callback | AsyncCallback&lt;boolean&gt; | Yes| Callback used to return the operation result.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  let requestInfo = {'scenario': 0x301, 'command': "command_1"};
  geolocation.sendCommand(requestInfo, (err, result) => {
      if (err) {
          console.log('sendCommand: err=' + JSON.stringify(err));
      }
      if (result) {
          console.log('sendCommand: result=' + JSON.stringify(result));
      }
  });
  ```


## geolocation.sendCommand<sup>(deprecated)</sup>

sendCommand(command: LocationCommand): Promise&lt;boolean&gt;;

Sends an extended command to the location subsystem. 

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.sendCommand](js-apis-geoLocationManager.md#geolocationmanagersendcommand).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | command | [LocationCommand](#locationcommanddeprecated) | Yes| Extended command (string) to be sent.|

**Return value**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | Promise&lt;boolean&gt; |boolean|NA| Callback used to return the operation result.|

**Example**

  ```ts
  import geolocation from '@ohos.geolocation';
  let requestInfo = {'scenario': 0x301, 'command': "command_1"};
  geolocation.sendCommand(requestInfo).then((result) => {
      console.log('promise, sendCommand: ' + JSON.stringify(result));
  });
  ```


## ReverseGeoCodeRequest<sup>(deprecated)</sup>

Defines a reverse geocoding request.

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.ReverseGeoCodeRequest](js-apis-geoLocationManager.md#reversegeocoderequest).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Geocoder

| Name| Type| Readable| Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| locale | string | Yes| Yes| Language used for the location description. **zh** indicates Chinese, and **en** indicates English.|
| latitude | number | Yes| Yes| Latitude information. A positive value indicates north latitude, and a negative value indicates south latitude. The value ranges from **-90** to **90**.|
| longitude | number | Yes| Yes| Longitude information. A positive value indicates east longitude , and a negative value indicates west longitude . The value ranges from **-180** to **180**.|
| maxItems | number | Yes| Yes| Maximum number of location records to be returned. The value must be greater than or equal to **0**. A value smaller than **10** is recommended.|


## GeoCodeRequest<sup>(deprecated)</sup>

Defines a geocoding request.

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.GeoCodeRequest](js-apis-geoLocationManager.md#geocoderequest).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Geocoder

| Name| Type| Readable|Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| locale | string | Yes| Yes| Language used for the location description. **zh** indicates Chinese, and **en** indicates English.|
| description | string | Yes| Yes| Location description, for example, **No. xx, xx Road, Pudong New District, Shanghai**.|
| maxItems | number | Yes| Yes| Maximum number of location records to be returned. The value must be greater than or equal to **0**. A value smaller than **10** is recommended.|
| minLatitude | number | Yes| Yes| Minimum latitude. This parameter is used with **minLongitude**, **maxLatitude**, and **maxLongitude** to specify the latitude and longitude ranges. The value ranges from **-90** to **90**.|
| minLongitude | number | Yes| Yes| Minimum longitude. The value ranges from **-180** to **180**.|
| maxLatitude | number | Yes| Yes| Maximum latitude. The value ranges from **-90** to **90**.|
| maxLongitude | number | Yes| Yes| Maximum longitude. The value ranges from **-180** to **180**.|


## GeoAddress<sup>(deprecated)</sup>

Defines a geographic location.

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.GeoAddress](js-apis-geoLocationManager.md#geoaddress).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Geocoder

| Name| Type| Readable|Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| latitude<sup>7+</sup> | number | Yes| No| Latitude information. A positive value indicates north latitude, and a negative value indicates south latitude. The value ranges from **-90** to **90**.|
| longitude<sup>7+</sup> | number | Yes| No| Longitude information. A positive value indicates east longitude , and a negative value indicates west longitude . The value ranges from **-180** to **180**.|
| locale<sup>7+</sup> | string | Yes| No| Language used for the location description. **zh** indicates Chinese, and **en** indicates English.|
| placeName<sup>7+</sup> | string | Yes| No| Landmark of the location.|
| countryCode<sup>7+</sup> | string | Yes| No| Country code.|
| countryName<sup>7+</sup> | string | Yes| No| Country name.|
| administrativeArea<sup>7+</sup> | string | Yes| No| Administrative region name.|
| subAdministrativeArea<sup>7+</sup> | string | Yes| No| Sub-administrative region name.|
| locality<sup>7+</sup> | string | Yes| No| Locality information.|
| subLocality<sup>7+</sup> | string | Yes| No| Sub-locality information.|
| roadName<sup>7+</sup> | string | Yes| No| Road name.|
| subRoadName<sup>7+</sup> | string | Yes| No| Auxiliary road information.|
| premises<sup>7+</sup> | string | Yes| No| House information.|
| postalCode<sup>7+</sup> | string | Yes| No| Postal code.|
| phoneNumber<sup>7+</sup> | string | Yes| No| Phone number.|
| addressUrl<sup>7+</sup> | string | Yes| No| Website URL.|
| descriptions<sup>7+</sup> | Array&lt;string&gt; | Yes| No| Additional descriptions.|
| descriptionsSize<sup>7+</sup> | number | Yes| No| Total number of additional descriptions. The value must be greater than or equal to **0**. A value smaller than **10** is recommended.|


## LocationRequest<sup>(deprecated)</sup>

Defines a location request.

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.LocationRequest](js-apis-geoLocationManager.md#locationrequest).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

| Name| Type| Readable|Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| priority | [LocationRequestPriority](#locationrequestprioritydeprecated) | Yes| Yes| Priority of the location request. For details about the value range, see [LocationRequestPriority](#locationrequestprioritydeprecated).|
| scenario | [LocationRequestScenario](#locationrequestscenariodeprecated) | Yes| Yes| Scenario of the location request. For details about the value range, see [LocationRequestScenario](#locationrequestscenariodeprecated).|
| timeInterval | number | Yes| Yes| Time interval at which location information is reported, in seconds. The value must be greater than **0**.|
| distanceInterval | number | Yes| Yes| Distance interval at which location information is reported. The value must be greater than **0**, in meters.|
| maxAccuracy | number | Yes| Yes| Location accuracy. This parameter is valid only when the precise location function is enabled, and is invalid when the approximate location function is enabled. The value must be greater than **0**.|


## CurrentLocationRequest<sup>(deprecated)</sup>

Defines the current location request.

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.CurrentLocationRequest](js-apis-geoLocationManager.md#currentlocationrequest).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

| Name| Type| Readable|Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| priority | [LocationRequestPriority](#locationrequestprioritydeprecated) | Yes| Yes| Priority of the location request. For details about the value range, see [LocationRequestPriority](#locationrequestprioritydeprecated).|
| scenario | [LocationRequestScenario](#locationrequestscenariodeprecated) | Yes| Yes| Scenario of the location request. For details about the value range, see [LocationRequestScenario](#locationrequestscenariodeprecated).|
| maxAccuracy | number | Yes| Yes| Location accuracy, in meters. This parameter is valid only when the precise location function is enabled, and is invalid when the approximate location function is enabled. The value must be greater than **0**.|
| timeoutMs | number | Yes| Yes| Timeout duration, in milliseconds. The minimum value is **1000**. The value must be greater than or equal to **1000**.|


## SatelliteStatusInfo<sup>(deprecated)</sup>

Defines the satellite status information.

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.SatelliteStatusInfo](js-apis-geoLocationManager.md#satellitestatusinfo).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Gnss

| Name| Type| Readable|Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| satellitesNumber | number | Yes| No| Number of satellites. The value must be greater than or equal to **0**.|
| satelliteIds | Array&lt;number&gt; | Yes| No| Array of satellite IDs. The value must be greater than or equal to **0**.|
| carrierToNoiseDensitys | Array&lt;number&gt; | Yes| No| Carrier-to-noise density ratio, that is, **cn0**. The value must be greater than **0**.|
| altitudes | Array&lt;number&gt; | Yes| No| Satellite altitude angle information. The value ranges from **-90** to **90**, in degrees.|
| azimuths | Array&lt;number&gt; | Yes| No| Azimuth information. The value ranges from **0** to **360**, in degrees.|
| carrierFrequencies | Array&lt;number&gt; | Yes| No| Carrier frequency. The value must be greater than or equal to **0**, in Hz.|


## CachedGnssLocationsRequest<sup>(deprecated)</sup>

Represents a request for reporting cached GNSS locations.

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.CachedGnssLocationsRequest](js-apis-geoLocationManager.md#cachedgnsslocationsrequest).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Gnss

| Name| Type| Readable|Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| reportingPeriodSec | number | Yes| Yes| Interval for reporting the cached GNSS locations, in milliseconds. The value must be greater than **0**.|
| wakeUpCacheQueueFull | boolean | Yes| Yes | **true**: reports the cached GNSS locations to the application when the cache queue is full.<br>**false**: discards the cached GNSS locations when the cache queue is full.|


## Geofence<sup>(deprecated)</sup>

Defines a GNSS geofence. Currently, only circular geofences are supported.

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.Geofence](js-apis-geoLocationManager.md#geofence).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Geofence

| Name| Type| Readable|Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| latitude | number | Yes| Yes|Latitude information. The value ranges from **-90** to **90**.|
| longitude | number | Yes|Yes| Longitude information. The value ranges from **-180** to **180**.|
| radius | number | Yes|Yes| Radius of a circular geofence. The value must be greater than **0**, in meters.|
| expiration | number | Yes|Yes| Expiration period of a geofence, in milliseconds. The value must be greater than **0**.|


## GeofenceRequest<sup>(deprecated)</sup>

Represents a GNSS geofencing request.

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.GeofenceRequest](js-apis-geoLocationManager.md#geofencerequest).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Geofence

| Name| Type| Readable|Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| priority | [LocationRequestPriority](#locationrequestprioritydeprecated) | Yes| Yes | Priority of the location information.|
| scenario | [LocationRequestScenario](#locationrequestscenariodeprecated) | Yes| Yes | Location scenario.|
| geofence | [Geofence](#geofencedeprecated)| Yes| Yes | Geofence information.|


## LocationCommand<sup>(deprecated)</sup>

Defines an extended command.

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.LocationCommand](js-apis-geoLocationManager.md#locationcommand).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

| Name| Type| Readable|Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| scenario | [LocationRequestScenario](#locationrequestscenariodeprecated)  | Yes| Yes | Location scenario.|
| command | string | Yes| Yes | Extended command, in the string format.|


## Location<sup>(deprecated)</sup>

Defines a location.

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.Location](js-apis-geoLocationManager.md#location).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

| Name| Type| Readable|Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| latitude<sup>7+</sup> | number | Yes| No| Latitude information. A positive value indicates north latitude, and a negative value indicates south latitude. The value ranges from **-90** to **90**.|
| longitude<sup>7+</sup> | number | Yes| No| Longitude information. A positive value indicates east longitude , and a negative value indicates west longitude . The value ranges from **-180** to **180**.|
| altitude<sup>7+</sup> | number | Yes| No| Location altitude, in meters.|
| accuracy<sup>7+</sup> | number | Yes| No| Location accuracy, in meters.|
| speed<sup>7+</sup> | number | Yes| No| Speed, in m/s.|
| timeStamp<sup>7+</sup> | number | Yes| No| Location timestamp in the UTC format.|
| direction<sup>7+</sup> | number | Yes| No| Direction information. The value ranges from **0** to **360**, in degrees.|
| timeSinceBoot<sup>7+</sup> | number | Yes| No| Location timestamp since boot.|
| additions<sup>7+</sup> | Array&lt;string&gt; | Yes| No| Additional description.|
| additionSize<sup>7+</sup> | number | Yes| No| Number of additional descriptions. The value must be greater than or equal to **0**.|


## LocationPrivacyType<sup>(deprecated)</sup>

Defines the privacy statement type.

> **NOTE**<br>
> This API is supported since API version 8.
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.LocationPrivacyType](js-apis-geoLocationManager.md#locationprivacytype).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

| Name| Value| Description|
| -------- | -------- | -------- |
| OTHERS | 0 | Other scenarios. Reserved field.|
| STARTUP | 1 | Privacy statement displayed in the startup wizard.  |
| CORE_LOCATION | 2 | Privacy statement displayed when enabling the location service.|


## LocationRequestPriority<sup>(deprecated)</sup>

Sets the priority of the location request.

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.LocationRequestPriority](js-apis-geoLocationManager.md#locationrequestpriority).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

| Name| Value| Description|
| -------- | -------- | -------- |
| UNSET | 0x200 | Priority unspecified.<br>If this option is used, [LocationRequestPriority](#locationrequestprioritydeprecated) is invalid.|
| ACCURACY | 0x201 | Location accuracy preferred.<br>This policy mainly uses the GNSS positioning technology. In an open area, the technology can achieve the meter-level location accuracy, depending on the hardware performance of the device. However, in a shielded environment, the location accuracy may significantly decrease.|
| LOW_POWER | 0x202 | Power efficiency preferred.<br>This policy mainly uses the base station positioning, WLAN positioning, and Bluetooth positioning technologies to obtain device location in both indoor and outdoor scenarios. The location accuracy depends on the distribution of surrounding base stations, visible WLANs, and Bluetooth devices and therefore may fluctuate greatly. This policy is recommended and can reduce power consumption when your application does not require high location accuracy or when base stations, visible WLANs, and Bluetooth devices are densely distributed.|
| FIRST_FIX | 0x203 | Fast location preferred. Use this option if you want to obtain a location as fast as possible.<br>This policy uses the GNSS positioning, base station positioning, WLAN positioning, and Bluetooth positioning technologies simultaneously to obtain the device location in both the indoor and outdoor scenarios. When all positioning technologies provide a location result, the system provides the most accurate location result for your application. It can lead to significant hardware resource consumption and power consumption.|


## LocationRequestScenario<sup>(deprecated)</sup>

  Sets the scenario of the location request.

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager.LocationRequestScenario](js-apis-geoLocationManager.md#locationrequestscenario).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

| Name| Value| Description|
| -------- | -------- | -------- |
| UNSET | 0x300 | Scenario unspecified.<br>If this option is used, [LocationRequestScenario](#locationrequestscenariodeprecated) is invalid.|
| NAVIGATION | 0x301 | Navigation scenario.<br>This option is applicable when your application needs to obtain the real-time location of a mobile device outdoors, such as navigation for driving or walking.<br>In this scenario, GNSS positioning is used to provide location services to ensure the optimal location accuracy of the system.<br>The location result is reported at a minimum interval of 1 second by default.|
| TRAJECTORY_TRACKING | 0x302 | Trajectory tracking scenario.<br>This option is applicable when your application needs to record user trajectories, for example, the track recording function of sports applications. In this scenario, the GNSS positioning technology is mainly used to ensure the location accuracy.<br>The location result is reported at a minimum interval of 1 second by default.|
| CAR_HAILING | 0x303 | Ride hailing scenario.<br>This option is applicable when your application needs to obtain the current location of a user who is hailing a taxi.<br>The location result is reported at a minimum interval of 1 second by default.|
| DAILY_LIFE_SERVICE | 0x304 | Daily life service scenario.<br>This option is applicable when your application only needs the approximate user location for recommendations and push notifications in scenarios such as when the user is browsing news, shopping online, and ordering food.<br>The location result is reported at a minimum interval of 1 second by default.|
| NO_POWER | 0x305 | Power efficiency scenario.<br>This option is applicable when your application does not proactively start the location service. When responding to another application requesting the same location service, the system marks a copy of the location result to your application. In this way, your application will not consume extra power for obtaining the user location.|


## GeoLocationErrorCode<sup>(deprecated)</sup>

Enumerates error codes of the location service.

> **NOTE**<br>
> This API is deprecated since API version 9. You are advised to use [geoLocationManager](../errorcodes/errorcode-geoLocationManager.md).

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Location.Location.Core

| Name| Value| Description|
| -------- | -------- | -------- |
| INPUT_PARAMS_ERROR<sup>7+</sup> | 101 | Incorrect input parameters.|
| REVERSE_GEOCODE_ERROR<sup>7+</sup> | 102 | Failed to call the reverse geocoding API.|
| GEOCODE_ERROR<sup>7+</sup> | 103 | Failed to call the geocoding API.|
| LOCATOR_ERROR<sup>7+</sup> | 104 | Failed to obtain the location.|
| LOCATION_SWITCH_ERROR<sup>7+</sup> | 105 | Failed to change the location service switch.|
| LAST_KNOWN_LOCATION_ERROR<sup>7+</sup> | 106 | Failed to obtain the previous location.|
| LOCATION_REQUEST_TIMEOUT_ERROR<sup>7+</sup> | 107 | Failed to obtain the location within the specified time.|
