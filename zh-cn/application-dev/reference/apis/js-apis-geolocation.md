# @ohos.geolocation (位置服务)

位置服务提供GNSS定位、网络定位、地理编码、逆地理编码、国家码和地理围栏等基本功能。

> **说明：**
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> 从API Version 9开始，该接口不再维护，推荐使用新接口[geoLocationManager](js-apis-geoLocationManager.md)。

## 申请权限

应用在使用系统能力前，需要检查是否已经获取用户授权访问设备位置信息。如未获得授权，可以向用户申请需要的位置权限，申请方式请参考下文。

系统提供的定位权限有：
- ohos.permission.LOCATION

- ohos.permission.APPROXIMATELY_LOCATION

- ohos.permission.LOCATION_IN_BACKGROUND

访问设备的位置信息，必须申请权限，并且获得用户授权。

API9之前的版本，申请ohos.permission.LOCATION即可。

API9及之后的版本，需要申请ohos.permission.APPROXIMATELY_LOCATION或者同时申请ohos.permission.APPROXIMATELY_LOCATION和ohos.permission.LOCATION；无法单独申请ohos.permission.LOCATION。

| 使用的API版本 | 申请位置权限 | 申请结果 | 位置的精确度 |
| -------- | -------- | -------- | -------- |
| 小于9 | ohos.permission.LOCATION | 成功 | 获取到精准位置，精准度在米级别。 |
| 大于等于9 | ohos.permission.LOCATION | 失败 | 无法获取位置。 |
| 大于等于9 | ohos.permission.APPROXIMATELY_LOCATION | 成功 | 获取到模糊位置，精确度为5公里。 |
| 大于等于9 | ohos.permission.APPROXIMATELY_LOCATION和ohos.permission.LOCATION | 成功 | 获取到精准位置，精准度在米级别。 |

如果应用在后台运行时也需要访问设备位置，除需要将应用声明为允许后台运行外，还必须申请ohos.permission.LOCATION_IN_BACKGROUND权限，这样应用在切入后台之后，系统可以继续上报位置信息。

开发者可以在应用配置文件中声明所需要的权限，具体可参考[授权申请指导](../../security/accesstoken-guidelines.md)。


## 导入模块

```ts
import geolocation from '@ohos.geolocation';
```

## geolocation.on('locationChange')<sup>(deprecated)</sup>

on(type: 'locationChange', request: LocationRequest, callback: Callback&lt;Location&gt;): void

开启位置变化订阅，并发起定位请求。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.on('locationChange')](js-apis-geoLocationManager.md#geolocationmanageronlocationchange)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“locationChange”，表示位置变化。 |
  | request |  [LocationRequest](#locationrequestdeprecated) | 是 | 设置位置请求参数。 |
  | callback | Callback&lt;[Location](#locationdeprecated)&gt; | 是 | 接收位置变化状态变化监听。 |



**示例**

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

关闭位置变化订阅，并删除对应的定位请求。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.off('locationChange')](js-apis-geoLocationManager.md#geolocationmanagerofflocationchange)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“locationChange”，表示位置变化。 |
  | callback | Callback&lt;[Location](#locationdeprecated)&gt; | 否 | 需要取消订阅的回调函数。若无此参数，则取消当前类型的所有订阅。 |


**示例**

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

订阅位置服务状态变化。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.on('locationEnabledChange')](js-apis-geoLocationManager.md#geolocationmanageronlocationenabledchange)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“locationServiceState”，表示位置服务状态。 |
  | callback | Callback&lt;boolean&gt; | 是 | 接收位置服务状态变化监听。 |


**示例**

  ```ts
  import geolocation from '@ohos.geolocation';
  let locationServiceState = (state) => {
      console.log('locationServiceState: ' + JSON.stringify(state));
  }
  geolocation.on('locationServiceState', locationServiceState);
  ```


## geolocation.off('locationServiceState')<sup>(deprecated)</sup>

off(type: 'locationServiceState', callback?: Callback&lt;boolean&gt;): void;

取消订阅位置服务状态变化。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.off('locationEnabledChange')](js-apis-geoLocationManager.md#geolocationmanagerofflocationenabledchange)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“locationServiceState”，表示位置服务状态。 |
  | callback | Callback&lt;boolean&gt; | 否 | 需要取消订阅的回调函数。若无此参数，则取消当前类型的所有订阅。 |


**示例**

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

订阅缓存GNSS定位结果上报事件。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.on('cachedGnssLocationsChange')](js-apis-geoLocationManager.md#geolocationmanageroncachedgnsslocationschange)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“cachedGnssLocationsReporting”，表示GNSS缓存定位结果上报。 |
  | request |  [CachedGnssLocationsRequest](#cachedgnsslocationsrequestdeprecated) | 是 | GNSS缓存功能配置参数 |
  | callback | Callback&lt;Array&lt;[Location](#locationdeprecated)&gt;&gt; | 是 | 接收GNSS缓存位置上报。 |


**示例**

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

取消订阅缓存GNSS定位结果上报事件。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.off('cachedGnssLocationsChange')](js-apis-geoLocationManager.md#geolocationmanageroffcachedgnsslocationschange)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“cachedGnssLocationsReporting”，表示GNSS缓存定位结果上报。 |
  | callback | Callback&lt;Array&lt;[Location](#locationdeprecated)&gt;&gt; | 否 | 需要取消订阅的回调函数。若无此参数，则取消当前类型的所有订阅。 |


**示例**

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

订阅GNSS卫星状态信息上报事件。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.on('satelliteStatusChange')](js-apis-geoLocationManager.md#geolocationmanageronsatellitestatuschange)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“gnssStatusChange”，表示订阅GNSS卫星状态信息上报。 |
  | callback | Callback&lt;[SatelliteStatusInfo](#satellitestatusinfodeprecated)&gt; | 是 | 接收GNSS卫星状态信息上报。 |


**示例**

  ```ts
  import geolocation from '@ohos.geolocation';
  let gnssStatusCb = (satelliteStatusInfo) => {
      console.log('gnssStatusChange: ' + JSON.stringify(satelliteStatusInfo));
  }
  geolocation.on('gnssStatusChange', gnssStatusCb);
  ```


## geolocation.off('gnssStatusChange')<sup>(deprecated)</sup>

off(type: 'gnssStatusChange', callback?: Callback&lt;SatelliteStatusInfo&gt;): void;

取消订阅GNSS卫星状态信息上报事件。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.off('satelliteStatusChange')](js-apis-geoLocationManager.md#geolocationmanageroffsatellitestatuschange)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“gnssStatusChange”，表示订阅GNSS卫星状态信息上报。 |
  | callback | Callback&lt;[SatelliteStatusInfo](#satellitestatusinfodeprecated)&gt; | 否 | 需要取消订阅的回调函数。若无此参数，则取消当前类型的所有订阅。 |

**示例**

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

订阅GNSS NMEA信息上报事件。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.on('nmeaMessage')](js-apis-geoLocationManager.md#geolocationmanageronnmeamessage)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“nmeaMessageChange”，表示订阅GNSS&nbsp;NMEA信息上报。 |
  | callback | Callback&lt;string&gt; | 是 | 接收GNSS&nbsp;NMEA信息上报。 |


**示例**

  ```ts
  import geolocation from '@ohos.geolocation';
  let nmeaCb = (str) => {
      console.log('nmeaMessageChange: ' + JSON.stringify(str));
  }
  geolocation.on('nmeaMessageChange', nmeaCb );
  ```


## geolocation.off('nmeaMessageChange')<sup>(deprecated)</sup>

off(type: 'nmeaMessageChange', callback?: Callback&lt;string&gt;): void;

取消订阅GNSS NMEA信息上报事件。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.off('nmeaMessage')](js-apis-geoLocationManager.md#geolocationmanageroffnmeamessage)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“nmeaMessageChange”，表示订阅GNSS&nbsp;NMEA信息上报。 |
  | callback | Callback&lt;string&gt; | 否 | 需要取消订阅的回调函数。若无此参数，则取消当前类型的所有订阅。 |


**示例**

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

添加一个围栏，并订阅地理围栏事件。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.on('gnssFenceStatusChange')](js-apis-geoLocationManager.md#geolocationmanagerongnssfencestatuschange)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geofence

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“fenceStatusChange”，表示订阅围栏事件上报。 |
  | request |  [GeofenceRequest](#geofencerequestdeprecated) | 是 | 围栏的配置参数。 |
  | want | [WantAgent](js-apis-app-ability-wantAgent.md) | 是 | 用于接收地理围栏事件上报（进出围栏）。 |

**示例**

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

删除一个围栏，并取消订阅该围栏事件。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.off('gnssFenceStatusChange')](js-apis-geoLocationManager.md#geolocationmanageroffgnssfencestatuschange)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geofence

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“fenceStatusChange”，表示订阅围栏事件上报。 |
  | request | [GeofenceRequest](#geofencerequestdeprecated) | 是 | 围栏的配置参数。 |
  | want | [WantAgent](js-apis-app-ability-wantAgent.md) | 是 | 用于接收地理围栏事件上报（进出围栏）。 |

**示例**

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

获取当前位置，使用callback回调异步返回结果。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.getCurrentLocation](js-apis-geoLocationManager.md#geolocationmanagergetcurrentlocation)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | request | [CurrentLocationRequest](#currentlocationrequestdeprecated) | 是 | 设置位置请求参数。 |
  | callback | AsyncCallback&lt;[Location](#locationdeprecated)&gt; | 是 | 用来接收位置信息的回调。 |

**示例**

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


获取当前位置，使用callback回调异步返回结果。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.getCurrentLocation](js-apis-geoLocationManager.md#geolocationmanagergetcurrentlocation)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;[Location](#locationdeprecated)&gt; | 是 | 用来接收位置信息的回调。 |

**示例**

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

获取当前位置，使用Promise方式异步返回结果。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.getCurrentLocation](js-apis-geoLocationManager.md#geolocationmanagergetcurrentlocation-2)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | request | [CurrentLocationRequest](#currentlocationrequestdeprecated) | 否 | 设置位置请求参数。 |

**返回值**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | Promise&lt;[Location](#locationdeprecated)&gt; |[Location](#locationdeprecated)|NA| 返回位置信息。 |


**示例**

  ```ts
  import geolocation from '@ohos.geolocation';
  let requestInfo = {'priority': 0x203, 'scenario': 0x300,'maxAccuracy': 0};
  geolocation.getCurrentLocation(requestInfo).then((result) => {
      console.log('current location: ' + JSON.stringify(result));
  });
  ```


## geolocation.getLastLocation<sup>(deprecated)</sup>

getLastLocation(callback: AsyncCallback&lt;Location&gt;): void

获取上一次位置，使用callback回调异步返回结果。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.getLastLocation](js-apis-geoLocationManager.md#geolocationmanagergetlastlocation)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;[Location](#locationdeprecated)&gt; | 是 | 用来接收上次位置的回调。 |


**示例**

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

获取上一次位置，使用Promise方式异步返回结果。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.getLastLocation](js-apis-geoLocationManager.md#geolocationmanagergetlastlocation)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**返回值**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | Promise&lt;[Location](#locationdeprecated)&gt; | [Location](#locationdeprecated)|NA|返回上次位置信息。 |


**示例**

  ```ts
  import geolocation from '@ohos.geolocation';
  geolocation.getLastLocation().then((result) => {
      console.log('getLastLocation: result: ' + JSON.stringify(result));
  });
  ```


## geolocation.isLocationEnabled<sup>(deprecated)</sup>

isLocationEnabled(callback: AsyncCallback&lt;boolean&gt;): void

判断位置服务是否已经打开，使用callback回调异步返回结果。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.isLocationEnabled](js-apis-geoLocationManager.md#geolocationmanagerislocationenabled)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 用来接收位置服务状态的回调。 |

**示例**

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

判断位置服务是否已经开启，使用Promise方式异步返回结果。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.isLocationEnabled](js-apis-geoLocationManager.md#geolocationmanagerislocationenabled)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**返回值**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | Promise&lt;boolean&gt; | boolean|NA|返回位置服务是否可用的状态。 |

**示例**

  ```ts
  import geolocation from '@ohos.geolocation';
  geolocation.isLocationEnabled().then((result) => {
      console.log('promise, isLocationEnabled: ' + JSON.stringify(result));
  });
  ```


## geolocation.requestEnableLocation<sup>(deprecated)</sup>

requestEnableLocation(callback: AsyncCallback&lt;boolean&gt;): void

请求打开位置服务，使用callback回调异步返回结果。

> **说明：**<br/>
> 从API version 9开始废弃，建议由应用本身弹框请求用户跳转到settings开启位置开关，并且在弹框上写清楚会在什么场景下使用位置信息。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 用来接收位置服务状态的回调。 |

**示例**

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

请求打开位置服务，使用Promise方式异步返回结果。

> **说明：**<br/>
> 从API version 9开始废弃，建议由应用本身弹框请求用户跳转到settings开启位置开关，并且在弹框上写清楚会在什么场景下使用位置信息。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**返回值**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | Promise&lt;boolean&gt; | boolean|NA|返回位置服务是否可用。 |

**示例**

  ```ts
  import geolocation from '@ohos.geolocation';
  geolocation.requestEnableLocation().then((result) => {
      console.log('promise, requestEnableLocation: ' + JSON.stringify(result));
  });
  ```


## geolocation.isGeoServiceAvailable<sup>(deprecated)</sup>

isGeoServiceAvailable(callback: AsyncCallback&lt;boolean&gt;): void

判断（逆）地理编码服务状态，使用callback回调异步返回结果。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.isGeocoderAvailable](js-apis-geoLocationManager.md#geolocationmanagerisgeocoderavailable)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 用来接收地理编码服务状态的回调。 |

**示例**

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

判断（逆）地理编码服务状态，使用Promise方式异步返回结果。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.isGeocoderAvailable](js-apis-geoLocationManager.md#geolocationmanagerisgeocoderavailable)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

**返回值**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | Promise&lt;boolean&gt; |boolean|NA| 返回地理编码服务是否可用的状态。 |

**示例**

  ```ts
  import geolocation from '@ohos.geolocation';
  geolocation.isGeoServiceAvailable().then((result) => {
      console.log('promise, isGeoServiceAvailable: ' + JSON.stringify(result));
  });
  ```


## geolocation.getAddressesFromLocation<sup>(deprecated)</sup>

getAddressesFromLocation(request: ReverseGeoCodeRequest, callback: AsyncCallback&lt;Array&lt;GeoAddress&gt;&gt;): void

调用逆地理编码服务，将坐标转换为地理描述，使用callback回调异步返回结果。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.getAddressesFromLocation](js-apis-geoLocationManager.md#geolocationmanagergetaddressesfromlocation)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | request | [ReverseGeoCodeRequest](#reversegeocoderequestdeprecated) | 是 | 设置逆地理编码请求的相关参数。 |
  | callback | AsyncCallback&lt;Array&lt;[GeoAddress](#geoaddressdeprecated)&gt;&gt; | 是 | 设置接收逆地理编码请求的回调参数。 |

**示例**

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

调用逆地理编码服务，将坐标转换为地理描述，使用Promise方式异步返回结果。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.getAddressesFromLocation](js-apis-geoLocationManager.md#geolocationmanagergetaddressesfromlocation-1)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | request | [ReverseGeoCodeRequest](#reversegeocoderequestdeprecated) | 是 | 设置逆地理编码请求的相关参数。 |

**返回值**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | Promise&lt;Array&lt;[GeoAddress](#geoaddressdeprecated)&gt;&gt; | Array&lt;[GeoAddress](#geoaddressdeprecated)&gt;|NA|返回地理描述信息。 |

**示例**

  ```ts
  import geolocation from '@ohos.geolocation';
  let reverseGeocodeRequest = {"latitude": 31.12, "longitude": 121.11, "maxItems": 1};
  geolocation.getAddressesFromLocation(reverseGeocodeRequest).then((data) => {
      console.log('getAddressesFromLocation: ' + JSON.stringify(data));
  });
  ```


## geolocation.getAddressesFromLocationName<sup>(deprecated)</sup>

getAddressesFromLocationName(request: GeoCodeRequest, callback: AsyncCallback&lt;Array&lt;GeoAddress&gt;&gt;): void

调用地理编码服务，将地理描述转换为具体坐标，使用callback回调异步返回结果。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.getAddressesFromLocationName](js-apis-geoLocationManager.md#geolocationmanagergetaddressesfromlocationname)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | request | [GeoCodeRequest](#geocoderequestdeprecated) | 是 | 设置地理编码请求的相关参数。 |
  | callback | AsyncCallback&lt;Array&lt;[GeoAddress](#geoaddressdeprecated)&gt;&gt; | 是 | 设置接收地理编码请求的回调参数。 |

**示例**

  ```ts
  import geolocation from '@ohos.geolocation';
  let geocodeRequest = {"description": "上海市浦东新区xx路xx号", "maxItems": 1};
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

调用地理编码服务，将地理描述转换为具体坐标，使用Promise方式异步返回结果。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.getAddressesFromLocationName](js-apis-geoLocationManager.md#geolocationmanagergetaddressesfromlocationname-1)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | request | [GeoCodeRequest](#geocoderequestdeprecated) | 是 | 设置地理编码请求的相关参数。 |

**返回值**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | Promise&lt;Array&lt;[GeoAddress](#geoaddressdeprecated)&gt;&gt; | Array&lt;[GeoAddress](#geoaddressdeprecated)&gt;|NA|设置接收地理编码请求的回调参数。 |

**示例**

  ```ts
  import geolocation from '@ohos.geolocation';
  let geocodeRequest = {"description": "上海市浦东新区xx路xx号", "maxItems": 1};
  geolocation.getAddressesFromLocationName(geocodeRequest).then((result) => {
      console.log('getAddressesFromLocationName: ' + JSON.stringify(result));
  });
  ```


## geolocation.getCachedGnssLocationsSize<sup>(deprecated)</sup>

getCachedGnssLocationsSize(callback: AsyncCallback&lt;number&gt;): void;

获取GNSS芯片缓存位置的个数。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.getCachedGnssLocationsSize](js-apis-geoLocationManager.md#geolocationmanagergetcachedgnsslocationssize)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;number&gt; | 是 | 用来接收GNSS芯片缓存位置个数的回调。 |

**示例**

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

获取GNSS芯片缓存位置的个数。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.getCachedGnssLocationsSize](js-apis-geoLocationManager.md#geolocationmanagergetcachedgnsslocationssize-1)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**返回值**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | Promise&lt;number&gt; | number|NA|返回GNSS缓存位置的个数。 |

**示例**

  ```ts
  import geolocation from '@ohos.geolocation';
  geolocation.getCachedGnssLocationsSize().then((result) => {
      console.log('promise, getCachedGnssLocationsSize: ' + JSON.stringify(result));
  });
  ```


## geolocation.flushCachedGnssLocations<sup>(deprecated)</sup>

flushCachedGnssLocations(callback: AsyncCallback&lt;boolean&gt;): void;

读取并清空GNSS芯片所有缓存位置。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.flushCachedGnssLocations](js-apis-geoLocationManager.md#geolocationmanagerflushcachedgnsslocations)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 用来接收清空GNSS芯片缓存位置操作的结果。 |

**示例**

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

读取并清空GNSS芯片所有缓存位置。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.flushCachedGnssLocations](js-apis-geoLocationManager.md#geolocationmanagerflushcachedgnsslocations-1)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**返回值**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | Promise&lt;boolean&gt; |boolean|NA| 清空所有GNSS缓存位置是否成功。 |

**示例**

  ```ts
  import geolocation from '@ohos.geolocation';
  geolocation.flushCachedGnssLocations().then((result) => {
      console.log('promise, flushCachedGnssLocations: ' + JSON.stringify(result));
  });
  ```


## geolocation.sendCommand<sup>(deprecated)</sup>

sendCommand(command: LocationCommand, callback: AsyncCallback&lt;boolean&gt;): void;

给位置服务子系统的各个部件发送扩展命令。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.sendCommand](js-apis-geoLocationManager.md#geolocationmanagersendcommand)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | command |  [LocationCommand](#locationcommanddeprecated) | 是 | 指定目标场景，和将要发送的命令（字符串）。 |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 用来接收命令发送的结果。 |

**示例**

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

给位置服务子系统的各个部件发送扩展命令。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.sendCommand](js-apis-geoLocationManager.md#geolocationmanagersendcommand)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | command | [LocationCommand](#locationcommanddeprecated) | 是 | 指定目标场景，和将要发送的命令（字符串）。 |

**返回值**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | Promise&lt;boolean&gt; |boolean|NA| 表示命令发送成功或失败。 |

**示例**

  ```ts
  import geolocation from '@ohos.geolocation';
  let requestInfo = {'scenario': 0x301, 'command': "command_1"};
  geolocation.sendCommand(requestInfo).then((result) => {
      console.log('promise, sendCommand: ' + JSON.stringify(result));
  });
  ```


## ReverseGeoCodeRequest<sup>(deprecated)</sup>

逆地理编码请求接口。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.ReverseGeoCodeRequest](js-apis-geoLocationManager.md#reversegeocoderequest)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| locale | string | 是 | 是 | 指定位置描述信息的语言，“zh”代表中文，“en”代表英文。 |
| latitude | number | 是 | 是 | 表示纬度信息，正值表示北纬，负值表示南纬。取值范围为-90到90。 |
| longitude | number | 是 | 是 | 表示经度信息，正值表示东经，负值表示西经。取值范围为-180到180。 |
| maxItems | number | 是 | 是 | 指定返回位置信息的最大个数。取值范围为大于等于0，推荐该值小于10。 |


## GeoCodeRequest<sup>(deprecated)</sup>

地理编码请求接口。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.GeoCodeRequest](js-apis-geoLocationManager.md#geocoderequest)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

| 名称 | 类型 | 可读|可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| locale | string | 是 | 是 | 表示位置描述信息的语言，“zh”代表中文，“en”代表英文。 |
| description | string | 是 | 是 | 表示位置信息描述，如“上海市浦东新区xx路xx号”。 |
| maxItems | number | 是 | 是 | 表示返回位置信息的最大个数。取值范围为大于等于0，推荐该值小于10。 |
| minLatitude | number | 是 | 是 | 表示最小纬度信息，与下面三个参数一起，表示一个经纬度范围。取值范围为-90到90。 |
| minLongitude | number | 是 | 是 | 表示最小经度信息。取值范围为-180到180。 |
| maxLatitude | number | 是 | 是 | 表示最大纬度信息。取值范围为-90到90。 |
| maxLongitude | number | 是 | 是 | 表示最大经度信息。取值范围为-180到180。 |


## GeoAddress<sup>(deprecated)</sup>

地理编码类型。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.GeoAddress](js-apis-geoLocationManager.md#geoaddress)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

| 名称 | 类型 | 可读|可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| latitude<sup>7+</sup> | number | 是 | 否 | 表示纬度信息，正值表示北纬，负值表示南纬。取值范围为-90到90。 |
| longitude<sup>7+</sup> | number | 是 | 否 | 表示经度信息，正值表示东经，负值表是西经。取值范围为-180到180。 |
| locale<sup>7+</sup> | string | 是 | 否 | 表示位置描述信息的语言，“zh”代表中文，“en”代表英文。 |
| placeName<sup>7+</sup> | string | 是 | 否 | 表示地区信息。 |
| countryCode<sup>7+</sup> | string | 是 | 否 | 表示国家码信息。 |
| countryName<sup>7+</sup> | string | 是 | 否 | 表示国家信息。 |
| administrativeArea<sup>7+</sup> | string | 是 | 否 | 表示省份区域信息。 |
| subAdministrativeArea<sup>7+</sup> | string | 是 | 否 | 表示表示子区域信息。 |
| locality<sup>7+</sup> | string | 是 | 否 | 表示城市信息。 |
| subLocality<sup>7+</sup> | string | 是 | 否 | 表示子城市信息。 |
| roadName<sup>7+</sup> | string | 是 | 否 | 表示路名信息。 |
| subRoadName<sup>7+</sup> | string | 是 | 否 | 表示子路名信息。 |
| premises<sup>7+</sup> | string | 是 | 否 | 表示门牌号信息。 |
| postalCode<sup>7+</sup> | string | 是 | 否 | 表示邮政编码信息。 |
| phoneNumber<sup>7+</sup> | string | 是 | 否| 表示联系方式信息。 |
| addressUrl<sup>7+</sup> | string | 是 | 否 | 表示位置信息附件的网址信息。 |
| descriptions<sup>7+</sup> | Array&lt;string&gt; | 是 | 否 | 表示附加的描述信息。 |
| descriptionsSize<sup>7+</sup> | number | 是 | 否 | 表示附加的描述信息数量。取值范围为大于等于0，推荐该值小于10。 |


## LocationRequest<sup>(deprecated)</sup>

位置信息请求类型。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.LocationRequest](js-apis-geoLocationManager.md#locationrequest)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 类型 | 可读|可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| priority | [LocationRequestPriority](#locationrequestprioritydeprecated) | 是 | 是 | 表示优先级信息。取值范围见[LocationRequestPriority](#locationrequestprioritydeprecated)的定义。 |
| scenario | [LocationRequestScenario](#locationrequestscenariodeprecated) | 是 | 是 | 表示场景信息。取值范围见[LocationRequestScenario](#locationrequestscenariodeprecated)的定义。 |
| timeInterval | number | 是 | 是 | 表示上报位置信息的时间间隔，单位是秒。取值范围为大于0。 |
| distanceInterval | number | 是 | 是 | 表示上报位置信息的距离间隔。单位是米，取值范围为大于0。 |
| maxAccuracy | number | 是 | 是 | 表示精度信息。仅在精确位置功能场景下有效，模糊位置功能生效场景下该字段无意义。取值范围为大于0。 |


## CurrentLocationRequest<sup>(deprecated)</sup>

当前位置信息请求类型。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.CurrentLocationRequest](js-apis-geoLocationManager.md#currentlocationrequest)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 类型 | 可读|可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| priority | [LocationRequestPriority](#locationrequestprioritydeprecated) | 是 | 是 | 表示优先级信息。取值范围见[LocationRequestPriority](#locationrequestprioritydeprecated)的定义。 |
| scenario | [LocationRequestScenario](#locationrequestscenariodeprecated) | 是 | 是 | 表示场景信息。取值范围见[LocationRequestScenario](#locationrequestscenariodeprecated)的定义。 |
| maxAccuracy | number | 是 | 是| 表示精度信息，单位是米。仅在精确位置功能场景下有效，模糊位置功能生效场景下该字段无意义。取值范围为大于0。 |
| timeoutMs | number | 是 | 是 | 表示超时时间，单位是毫秒，最小为1000毫秒。取值范围为大于等于1000。 |


## SatelliteStatusInfo<sup>(deprecated)</sup>

卫星状态信息。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.SatelliteStatusInfo](js-apis-geoLocationManager.md#satellitestatusinfo)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

| 名称 | 类型 | 可读|可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| satellitesNumber | number | 是 | 否 | 表示卫星个数。取值范围为大于等于0。 |
| satelliteIds | Array&lt;number&gt; | 是 | 否 | 表示每个卫星的ID，数组类型。取值范围为大于等于0。 |
| carrierToNoiseDensitys | Array&lt;number&gt; | 是 | 否 | 表示载波噪声功率谱密度比，即cn0。取值范围为大于0。 |
| altitudes | Array&lt;number&gt; | 是 | 否 | 表示卫星高度角信息。单位是“度”，取值范围为-90到90。 |
| azimuths | Array&lt;number&gt; | 是 | 否 | 表示方位角。单位是“度”，取值范围为0到360。 |
| carrierFrequencies | Array&lt;number&gt; | 是 | 否 | 表示载波频率。单位是Hz，取值范围为大于等于0。 |


## CachedGnssLocationsRequest<sup>(deprecated)</sup>

请求订阅GNSS缓存位置上报功能接口的配置参数。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.CachedGnssLocationsRequest](js-apis-geoLocationManager.md#cachedgnsslocationsrequest)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

| 名称 | 类型 | 可读|可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| reportingPeriodSec | number | 是 | 是 | 表示GNSS缓存位置上报的周期，单位是毫秒。取值范围为大于0。 |
| wakeUpCacheQueueFull | boolean | 是 | 是  | true表示GNSS芯片底层缓存队列满之后会主动唤醒AP芯片，并把缓存位置上报给应用。<br/>false表示GNSS芯片底层缓存队列满之后不会主动唤醒AP芯片，会把缓存位置直接丢弃。 |


## Geofence<sup>(deprecated)</sup>

GNSS围栏的配置参数。目前只支持圆形围栏。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.Geofence](js-apis-geoLocationManager.md#geofence)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geofence

| 名称 | 类型 | 可读|可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| latitude | number | 是 | 是 |表示纬度。取值范围为-90到90。 |
| longitude | number | 是 |是 | 表示经度。取值范围为-180到180。 |
| radius | number | 是 |是 | 表示圆形围栏的半径。单位是米，取值范围为大于0。 |
| expiration | number | 是 |是 | 围栏存活的时间，单位是毫秒。取值范围为大于0。 |


## GeofenceRequest<sup>(deprecated)</sup>

请求添加GNSS围栏消息中携带的参数，包括定位优先级、定位场景和围栏信息。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.GeofenceRequest](js-apis-geoLocationManager.md#geofencerequest)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geofence

| 名称 | 类型 | 可读|可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| priority | [LocationRequestPriority](#locationrequestprioritydeprecated) | 是 | 是  | 表示位置信息优先级。 |
| scenario | [LocationRequestScenario](#locationrequestscenariodeprecated) | 是 | 是  | 表示定位场景。 |
| geofence | [Geofence](#geofencedeprecated)| 是 | 是  | 表示围栏信息。 |


## LocationCommand<sup>(deprecated)</sup>

扩展命令结构体。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.LocationCommand](js-apis-geoLocationManager.md#locationcommand)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 类型 | 可读|可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| scenario | [LocationRequestScenario](#locationrequestscenariodeprecated)  | 是 | 是  | 表示定位场景。 |
| command | string | 是 | 是  | 扩展命令字符串。 |


## Location<sup>(deprecated)</sup>

位置信息类型。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.Location](js-apis-geoLocationManager.md#location)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 类型 | 可读|可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| latitude<sup>7+</sup> | number | 是 | 否 | 表示纬度信息，正值表示北纬，负值表示南纬。取值范围为-90到90。 |
| longitude<sup>7+</sup> | number | 是 | 否 | 表示经度信息，正值表示东经，负值表是西经。取值范围为-180到180。 |
| altitude<sup>7+</sup> | number | 是 | 否 | 表示高度信息，单位米。 |
| accuracy<sup>7+</sup> | number | 是 | 否 | 表示精度信息，单位米。 |
| speed<sup>7+</sup> | number | 是 | 否 | 表示速度信息，单位米每秒。 |
| timeStamp<sup>7+</sup> | number | 是 | 否 | 表示位置时间戳，UTC格式。 |
| direction<sup>7+</sup> | number | 是 | 否 | 表示航向信息。单位是“度”，取值范围为0到360。 |
| timeSinceBoot<sup>7+</sup> | number | 是 | 否 | 表示位置时间戳，开机时间格式。 |
| additions<sup>7+</sup> | Array&lt;string&gt; | 是 | 否 | 附加信息。 |
| additionSize<sup>7+</sup> | number | 是 | 否 | 附加信息数量。取值范围为大于等于0。 |


## LocationPrivacyType<sup>(deprecated)</sup>

定位服务隐私协议类型。

> **说明：**<br/>
> 从API version 8开始支持。
> 从API version 9开始废弃，建议使用[geoLocationManager.LocationPrivacyType](js-apis-geoLocationManager.md#locationprivacytype)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| OTHERS | 0 | 其他场景。预留字段。 |
| STARTUP | 1 | 开机向导场景下的隐私协议。在开机时弹出协议，提醒用户阅读并选择是否授权。 |
| CORE_LOCATION | 2 | 开启网络定位时弹出的隐私协议。 |


## LocationRequestPriority<sup>(deprecated)</sup>

位置请求中位置信息优先级设置。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.LocationRequestPriority](js-apis-geoLocationManager.md#locationrequestpriority)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| UNSET | 0x200 | 表示未设置优先级，表示[LocationRequestPriority](#locationrequestprioritydeprecated)无效。 |
| ACCURACY | 0x201 | 表示精度优先。<br/>定位精度优先策略主要以GNSS定位技术为主，在开阔场景下可以提供米级的定位精度，具体性能指标依赖用户设备的定位硬件能力，但在室内等强遮蔽定位场景下，无法提供准确的位置服务。 |
| LOW_POWER | 0x202 | 表示低功耗优先。<br/>低功耗定位优先策略主要使用基站定位和WLAN、蓝牙定位技术，也可以同时提供室内和户外场景下的位置服务，因为其依赖周边基站、可见WLAN、蓝牙设备的分布情况，定位结果的精度波动范围较大，如果对定位结果精度要求不高，或者使用场景多在有基站、可见WLAN、蓝牙设备高密度分布的情况下，推荐使用，可以有效节省设备功耗。 |
| FIRST_FIX | 0x203 | 表示快速获取位置优先，如果应用希望快速拿到一个位置，可以将优先级设置为该字段。<br/>快速定位优先策略会同时使用GNSS定位、基站定位和WLAN、蓝牙定位技术，以便室内和户外场景下，通过此策略都可以获得位置结果，当各种定位技术都有提供位置结果时，系统会选择其中精度较好的结果返回给应用。因为对各种定位技术同时使用，对设备的硬件资源消耗较大，功耗也较大。 |


## LocationRequestScenario<sup>(deprecated)</sup>

  位置请求中定位场景设置。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[geoLocationManager.LocationRequestScenario](js-apis-geoLocationManager.md#locationrequestscenario)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| UNSET | 0x300 | 表示未设置场景信息。<br/>表示[LocationRequestScenario](#locationrequestscenariodeprecated)字段无效。 |
| NAVIGATION | 0x301 | 表示导航场景。<br/>适用于在户外定位设备实时位置的场景，如车载、步行导航。<br/>在此场景下，为保证系统提供位置结果精度最优，主要使用GNSS定位技术提供定位服务<br/>此场景默认以最小1秒间隔上报定位结果。 |
| TRAJECTORY_TRACKING | 0x302 | 表示运动轨迹记录场景。<br/>适用于记录用户位置轨迹的场景，如运动类应用记录轨迹功能。主要使用GNSS定位技术提供定位服务。<br/>此场景默认以最小1秒间隔上报定位结果。 |
| CAR_HAILING | 0x303 | 表示打车场景。<br/>适用于用户出行打车时定位当前位置的场景，如网约车类应用。<br/>此场景默认以最小1秒间隔上报定位结果。 |
| DAILY_LIFE_SERVICE | 0x304 | 表示日常服务使用场景。<br/>适用于不需要定位用户精确位置的使用场景，如新闻资讯、网购、点餐类应用，做推荐、推送时定位用户大致位置即可。<br/>此场景默认以最小1秒间隔上报定位结果。 |
| NO_POWER | 0x305 | 表示无功耗功场景，这种场景下不会主动触发定位，会在其他应用定位时，才给当前应用返回位置。 |


## GeoLocationErrorCode<sup>(deprecated)</sup>

位置服务中的错误码信息。

> **说明：**<br/>
> 从API version 9开始废弃，建议使用[位置服务子系统错误码](../errorcodes/errorcode-geoLocationManager.md)替代。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| INPUT_PARAMS_ERROR<sup>7+</sup> | 101 | 表示输入参数错误。 |
| REVERSE_GEOCODE_ERROR<sup>7+</sup> | 102 | 表示逆地理编码接口调用失败。 |
| GEOCODE_ERROR<sup>7+</sup> | 103 | 表示地理编码接口调用失败。 |
| LOCATOR_ERROR<sup>7+</sup> | 104 | 表示定位失败。 |
| LOCATION_SWITCH_ERROR<sup>7+</sup> | 105 | 表示定位开关。 |
| LAST_KNOWN_LOCATION_ERROR<sup>7+</sup> | 106 | 表示获取上次位置失败。 |
| LOCATION_REQUEST_TIMEOUT_ERROR<sup>7+</sup> | 107 | 表示单次定位，没有在指定时间内返回位置。 |