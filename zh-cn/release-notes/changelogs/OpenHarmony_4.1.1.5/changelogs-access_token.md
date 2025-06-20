# 程序访问子系统变更说明
## cl.access_token.1 requestPermissionsFromUser申请位置权限时行为变更

**访问级别**

公开接口

**变更原因**

该变更为非兼容性变更。根据安全隐私要求，位置权限申请使用时，申请精确/后台位置权限，要同时申请模糊权限。

**变更影响**

变更前，通过调用[requestPermissionsFromUser](../../../application-dev/reference/apis/js-apis-abilityAccessCtrl.md#requestpermissionsfromuser9)接口申请位置权限，如下两种申请情况都可以顺利拉起弹窗：

1、在未申请模糊权限[ohos.permission.APPROXIMATELY_LOCATION](../../../application-dev/security/permission-list.md#ohospermissionapproximately_location)的情况下，请求后台位置权限[ohos.permission.LOCATION_IN_BACKGROUND](../../../application-dev/security/permission-list.md#ohospermissionlocation_in_background)

2、在未申请模糊权限[ohos.permission.APPROXIMATELY_LOCATION](../../../application-dev/security/permission-list.md#ohospermissionapproximately_location)的情况下，同时请求后台位置权限[ohos.permission.LOCATION_IN_BACKGROUND](../../../application-dev/security/permission-list.md#ohospermissionlocation_in_background)及精准权限[ohos.permission.LOCATION](../../../application-dev/security/permission-list.md#ohospermissionlocation)；

变更后，上述两种情况将无法拉起弹窗授予权限。应用在申请精准权限或后台权限时，必须同时申请模糊权限。

**变更发生版本**

从OpenHarmony SDK 4.1.1.5开始。

**变更的接口/组件**

@ohos.abilityAccessCtrl.d.ts中requestPermissionsFromUser接口，使用该接口申请位置权限的应用，在申请精准权限或后台权限时，必须同时申请模糊权限。

**可能影响接口**

| 文件 | 方法 |
| -------- | -------- |
| @ohos.geolocation.d.ts | geolocation.on('locationChange') |
| @ohos.geolocation.d.ts | geolocation.off('locationChange') |
| @ohos.geolocation.d.ts | geolocation.on('locationServiceState') |
| @ohos.geolocation.d.ts | geolocation.off('locationServiceState') |
| @ohos.geolocation.d.ts | geolocation.on('cachedGnssLocationsReporting') |
| @ohos.geolocation.d.ts | geolocation.off('cachedGnssLocationsReporting') |
| @ohos.geolocation.d.ts | geolocation.on('gnssStatusChange') |
| @ohos.geolocation.d.ts | geolocation.off('gnssStatusChange') |
| @ohos.geolocation.d.ts | geolocation.on('nmeaMessageChange') |
| @ohos.geolocation.d.ts | geolocation.off('nmeaMessageChange') |
| @ohos.geolocation.d.ts | geolocation.on('fenceStatusChange') |
| @ohos.geolocation.d.ts | geolocation.off('fenceStatusChange') |
| @ohos.geolocation.d.ts | geolocation.getCurrentLocation |
| @ohos.geolocation.d.ts | geolocation.getLastLocation |
| @ohos.geolocation.d.ts | geolocation.isLocationEnabled |
| @ohos.geolocation.d.ts | geolocation.requestEnableLocation |
| @ohos.geolocation.d.ts | geolocation.isGeoServiceAvailable |
| @ohos.geolocation.d.ts | geolocation.getAddressesFromLocation |
| @ohos.geolocation.d.ts | geolocation.getAddressesFromLocationName |
| @ohos.geolocation.d.ts | geolocation.getCachedGnssLocationsSize |
| @ohos.geolocation.d.ts | geolocation.flushCachedGnssLocations |
| @ohos.geolocation.d.ts | geolocation.sendCommand |
| @ohos.geolocation.d.ts | SatelliteStatusInfo |
| @ohos.geolocation.d.ts | CachedGnssLocationsRequest |
| @ohos.geolocation.d.ts | GeofenceRequest |
| @ohos.geolocation.d.ts | Geofence |
| @ohos.geolocation.d.ts | ReverseGeoCodeRequest |
| @ohos.geolocation.d.ts | GeoCodeRequest |
| @ohos.geolocation.d.ts | GeoAddress |
| @ohos.geolocation.d.ts | LocationRequest |
| @ohos.geolocation.d.ts | CurrentLocationRequest |
| @ohos.geolocation.d.ts | Location |
| @ohos.geoLocationManager.d.ts | geoLocationManager.on('nmeaMessage') |
| @ohos.geoLocationManager.d.ts | geoLocationManager.off('nmeaMessage') |
| @ohos.geoLocationManager.d.ts | geoLocationManager.on('locatingRequiredDataChange') |
| @ohos.geoLocationManager.d.ts | geoLocationManager.off('locatingRequiredDataChange') |
| @ohos.geoLocationManager.d.ts | geoLocationManager.getLocatingRequiredData |
| @ohos.bluetooth.d.ts | bluetooth.startBluetoothDiscovery |
| @ohos.bluetooth.d.ts | startBLEScan |
| @ohos.bluetoothManager.d.ts | bluetoothManager.startBluetoothDiscovery |
| @ohos.bluetoothManager.d.ts | startBLEScan |
| @ohos.telephony.observer.d.ts | observer.on('cellInfoChange') |
| @ohos.telephony.radio.d.ts | radio.sendUpdateCellLocationRequest |
| @ohos.telephony.radio.d.ts | radio.getCellInformation |
| @system.geolocation.d.ts | GetLocationOption |
| @system.geolocation.d.ts | SubscribeLocationOption |
| @system.geolocation.d.ts | geolocation.getLocation |
| @system.geolocation.d.ts | geolocation.subscribe |
| @system.geolocation.d.ts | geolocation.unsubscribe |
| @ohos.wifi.d.ts | wifi.scan |
| @ohos.wifi.d.ts | wifi.getScanInfos |
| @ohos.wifi.d.ts | wifi.getDeviceConfigs |
| @ohos.wifi.d.ts | wifi.getStations |
| @ohos.wifi.d.ts | wifi.getCurrentGroup |
| @ohos.wifi.d.ts | wifi.getP2pPeerDevices |
| @ohos.wifi.d.ts | wifi.p2pConnect |
| @ohos.wifi.d.ts | wifi.startDiscoverDevices |
| @ohos.wifi.d.ts | wifi.on('p2pDeviceChange') |
| @ohos.wifi.d.ts | wifi.off('p2pDeviceChange') |
| @ohos.wifi.d.ts | wifi.on('p2pPeerDeviceChange') |
| @ohos.wifi.d.ts | wifi.off('p2pPeerDeviceChange') |
| @ohos.wifiManager.d.ts | wifiManager.scan |
| @ohos.wifiManager.d.ts | wifiManager.getScanResults |
| @ohos.wifiManager.d.ts | wifiManager.getScanResultsSync |
| @ohos.wifiManager.d.ts | wifiManager.getCandidateConfigs |
| @ohos.wifiManager.d.ts | wifiManager.getDeviceConfigs |
| @ohos.wifiManager.d.ts | wifiManager.getStations |
| @ohos.wifiManager.d.ts | wifiManager.getCurrentGroup |
| @ohos.wifiManager.d.ts | wifiManager.getP2pPeerDevices |
| @ohos.wifiManager.d.ts | wifiManager.p2pConnect |
| @ohos.wifiManager.d.ts | wifiManager.startDiscoverDevices |
| @ohos.wifiManager.d.ts | wifiManager.getP2pGroups |
| @ohos.wifiManager.d.ts | wifiManager.on('p2pDeviceChange') |
| @ohos.wifiManager.d.ts | wifiManager.off('p2pDeviceChange') |
| @ohos.wifiManager.d.ts | wifiManager.on('p2pPeerDeviceChange') |
| @ohos.wifiManager.d.ts | wifiManager.off('p2pPeerDeviceChange') |

**适配指导**

修改EntryAbility.ets和导入GlobalThis等步骤参考[requestPermissionsFromUser](../../../application-dev/reference/apis/js-apis-abilityAccessCtrl.md#requestpermissionsfromuser9)

```ts
    let context: common.UIAbilityContext = GlobalThis.getInstance().getContext('context');
    atManager.requestPermissionsFromUser(context, ['ohos.permission.APPROXIMATELY_LOCATION', 'ohos.permission.LOCATION', 'ohos.permission.LOCATION_IN_BACKGROUND']).then((data) => {
        console.info('data:' + JSON.stringify(data));
    }).catch((err: BusinessError) => {
        console.info('data:' + JSON.stringify(err));
    })
```
