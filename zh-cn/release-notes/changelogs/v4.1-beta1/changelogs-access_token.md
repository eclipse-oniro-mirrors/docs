# 程序访问子系统变更说明
## cl.access_token.1 requestPermissionsFromUser申请位置权限时行为变更

**访问级别**

公开接口

**变更原因**

该变更为非兼容性变更。根据安全隐私要求，位置权限申请使用时，申请精确/后台位置权限，要同时申请模糊权限。

**变更影响**

变更前，通过调用[requestPermissionsFromUser](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.1-Beta1/zh-cn/application-dev/reference/apis/js-apis-abilityAccessCtrl.md#requestpermissionsfromuser9)接口申请位置权限，如下两种申请情况都可以顺利拉起弹窗：

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

修改EntryAbility.ets和导入GlobalThis等步骤参考[requestPermissionsFromUser](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.1-Beta1/zh-cn/application-dev/reference/apis/js-apis-abilityAccessCtrl.md#requestpermissionsfromuser9)

```ts
    let context: common.UIAbilityContext = GlobalThis.getInstance().getContext('context');
    atManager.requestPermissionsFromUser(context, ['ohos.permission.APPROXIMATELY_LOCATION', 'ohos.permission.LOCATION', 'ohos.permission.LOCATION_IN_BACKGROUND']).then((data) => {
        console.info('data:' + JSON.stringify(data));
    }).catch((err: BusinessError) => {
        console.info('data:' + JSON.stringify(err));
    })
```

## cl.access_token.1 通过getPermissionUsedRecord获取权限访问记录时的返回结果变更

**变更影响**

变更前，通过调用[getPermissionUsedRecord](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.1-Beta1/zh-cn/application-dev/reference/apis/js-apis-privacyManager.md#privacymanagergetpermissionusedrecord)接口获取权限访问记录时的返回结果，包括访问时的前后台状态、访问时的时间戳、访问时长数据。

变更后，获取权限访问记录时的返回结果中将新增一条可选结果，访问时的锁屏状态。

具体变更内容参考[UsedRecordDetail](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.1-Beta1/zh-cn/application-dev/reference/apis/js-apis-privacyManager.md#usedrecorddetail)单条权限访问记录新增访问时的锁屏状态。

**适配指导**

使用和接口描述等信息参考[getPermissionUsedRecord](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.1-Beta1/zh-cn/application-dev/reference/apis/js-apis-privacyManager.md#privacymanagergetpermissionusedrecord)

调用getPermissionUsedRecord获取权限访问记录，解析对应权限访问记录的锁屏状态。

示例代码:
```ts
import privacyManager from '@ohos.privacyManager';

try {
    privacyManager.getPermissionUsedRecord({
        flag:1
    }, (err, data) => {
        try {
            let record = data.bundleRecords[0].permissionRecords[0];
            let access = record.accessRecords;
            let reject = record.rejectRecords;
            for (let i = 0; i < access.length; i++) {
                let detail = access[i];
                console.log(`access record detail lockscreen status: ` + detail.lockScreenStatus);
            }
            for (let i = 0; i < reject.length; i++) {
                let detail = reject[i];
                console.log(`reject record detail lockscreen status: ` + detail.lockScreenStatus);
            }
        } catch(err) {
            console.log(`catch err->${JSON.stringify(err)}`);
        }
    })
} catch(err) {
    console.log(`catch err->${JSON.stringify(err)}`);
}
```

## cl.access_token.1 requestPermissionsFromUser申请位置权限时行为变更

**访问级别**

公开接口

**变更原因**

该变更为非兼容性变更。根据安全隐私要求，地理位置支持使用期间允许的管控能力。位置权限申请使用时，无法通过弹窗形式授予后台位置权限。

**变更影响**

地理位置支持使用期间允许的管控能力。位置权限申请使用时，无法通过弹窗形式授予后台位置权限。具体受影响的弹窗场景见下文：

a) 应用仅申请后台权限（前台权限未弹窗授予）

变更前：弹出弹窗，点击允许可授予后台权限

变更后：不弹窗，不授予后台权限

b) 应用仅申请后台权限（前台权限已弹窗授予）

变更前：不弹窗，后台权限在第一次授予前台权限时同时授予

变更后：不弹窗，不授予后台权限

c) 应用同时申请前台和后台权限

变更前：弹窗展示允许和拒绝选项，选择允许则授予前台+后台权限

变更后：弹窗展示使用期间允许和拒绝选项，选择使用期间允许，仅授予前台权限

**变更发生版本**

从OpenHarmony SDK 4.1.5.3开始。

**变更的接口/组件**

@ohos.abilityAccessCtrl.d.ts中requestPermissionsFromUser接口，应用使用该接口申请位置权限时，无法通过弹窗形式授予后台位置权限。

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

接口使用的示例代码可参考[requestPermissionsFromUser接口指导](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.1-Beta1/zh-cn/application-dev/reference/apis/js-apis-abilityAccessCtrl.md#requestpermissionsfromuser9)

<!--no_check-->