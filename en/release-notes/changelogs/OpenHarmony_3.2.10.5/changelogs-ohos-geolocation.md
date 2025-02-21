# Location Subsystem ChangeLog

## cl.location.1 API Migration from @ohos.geolocation.d.ts to @ohos.geoLocationManager.d.ts

APIs in **@ohos.geolocation.d.ts** do not support throwing error codes. To support this function, all APIs in **@ohos.geolocation.d.ts** are migrated to the newly added **@ohos.geoLocationManager.d.ts** file, and corresponding error code description is added.

To use APIs of the location subsystem, you need to import **@ohos.geoLocationManager**.

import geoLocationManager from '@ohos.geoLocationManager';


**Change Impacts**

All APIs of the location subsystem are affected. To ensure normal use of these APIs, you need to import **@ohos.geoLocationManager**.

import geoLocationManager from '@ohos.geoLocationManager';

**Key API/Component Changes**

| Class       | API Type | Declaration                                                    | Change Type                                                    |
| ----------- | --------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| geolocation | namespace | declare namespace geolocation                                | Migrated to **@ohos.geoLocationManager.d.ts** and replaced by **namespace geoLocationManager**.|
| geolocation | method    | function on(type: 'locationChange', request: LocationRequest, callback: Callback<Location>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function off(type: 'locationChange', callback?: Callback<Location>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function on(type: 'locationServiceState', callback: Callback<boolean>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function off(type: 'locationServiceState', callback?: Callback<boolean>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function on(type: 'cachedGnssLocationsReporting', request: CachedGnssLocationsRequest, callback: Callback<Array<Location>>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function off(type: 'cachedGnssLocationsReporting', callback?: Callback<Array<Location>>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function on(type: 'gnssStatusChange', callback: Callback<SatelliteStatusInfo>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function off(type: 'gnssStatusChange', callback?: Callback<SatelliteStatusInfo>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function on(type: 'nmeaMessageChange', callback: Callback<string>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function off(type: 'nmeaMessageChange', callback?: Callback<string>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function on(type: 'fenceStatusChange', request: GeofenceRequest, want: WantAgent): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function off(type: 'fenceStatusChange', request: GeofenceRequest, want: WantAgent): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function getCurrentLocation(request: CurrentLocationRequest, callback: AsyncCallback<Location>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function getCurrentLocation(callback: AsyncCallback<Location>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function getCurrentLocation(request?: CurrentLocationRequest): Promise<Location>; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function getLastLocation(callback: AsyncCallback<Location>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function getLastLocation(): Promise<Location>;               | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function isLocationEnabled(callback: AsyncCallback<boolean>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function isLocationEnabled(): Promise<boolean>;              | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function requestEnableLocation(callback: AsyncCallback<boolean>): void; | Deleted.                                                    |
| geolocation | method    | function requestEnableLocation(): Promise<boolean>;          | Deleted.                                                    |
| geolocation | method    | function enableLocation(callback: AsyncCallback<boolean>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function enableLocation(): Promise<boolean>;                 | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function disableLocation(callback: AsyncCallback<boolean>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function disableLocation(): Promise<boolean>;                | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function getAddressesFromLocation(request: ReverseGeoCodeRequest, callback: AsyncCallback<Array<GeoAddress>>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function getAddressesFromLocation(request: ReverseGeoCodeRequest): Promise<Array<GeoAddress>>; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function getAddressesFromLocationName(request: GeoCodeRequest, callback: AsyncCallback<Array<GeoAddress>>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function getAddressesFromLocationName(request: GeoCodeRequest): Promise<Array<GeoAddress>>; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function isGeoServiceAvailable(callback: AsyncCallback<boolean>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function isGeoServiceAvailable(): Promise<boolean>;          | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function getCachedGnssLocationsSize(callback: AsyncCallback<number>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function getCachedGnssLocationsSize(): Promise<number>;      | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function flushCachedGnssLocations(callback: AsyncCallback<boolean>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function flushCachedGnssLocations(): Promise<boolean>;       | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function sendCommand(command: LocationCommand, callback: AsyncCallback<boolean>): void; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | method    | function sendCommand(command: LocationCommand): Promise<boolean>; | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | interface | SatelliteStatusInfo                                          | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | interface | CachedGnssLocationsRequest                                   | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | interface | GeofenceRequest                                              | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | interface | Geofence                                                     | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | interface | ReverseGeoCodeRequest                                        | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | interface | GeoCodeRequest                                               | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | interface | GeoAddress                                                   | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | interface | LocationRequest                                              | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | interface | CurrentLocationRequest                                       | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | interface | Location                                                     | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | enum      | LocationRequestPriority                                      | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | enum      | LocationRequestScenario                                      | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | enum      | GeoLocationErrorCode                                         | Deprecated.                                                    |
| geolocation | enum      | LocationPrivacyType                                          | Migrated to **@ohos.geoLocationManager.d.ts**.                     |
| geolocation | enum      | LocationCommand                                              | Migrated to **@ohos.geoLocationManager.d.ts**.                     |


**(Optional) Adaptation Guide**

The following sample code shows how to call **enableLocation** in the new version:

  ```ts
  import geoLocationManager from '@ohos.geoLocationManager';
  try {
      geoLocationManager.enableLocation((err, data) => {
          if (err) {
              console.log('enableLocation: err=' + JSON.stringify(err));
          }
      });
  } catch (err) {
      console.error("errCode:" + err.code + ",errMessage:" + err.message);
  }
  ```
