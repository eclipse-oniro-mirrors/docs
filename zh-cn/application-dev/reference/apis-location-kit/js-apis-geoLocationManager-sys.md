# @ohos.geoLocationManager (位置服务)(系统接口)

位置服务提供GNSS定位、网络定位、地理编码、逆地理编码、国家码和地理围栏等基本功能。

> **说明：**
>
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> 当前页面仅包含本模块的系统接口，其他公开接口参见[@ohos.geoLocationManager (位置服务)](js-apis-geoLocationManager.md)。
> 本模块能力仅支持WGS-84坐标系。

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

如果应用在后台运行时也需要访问设备位置，需要申请ohos.permission.LOCATION_IN_BACKGROUND权限或申请LOCATION类型的长时任务，这样应用在切入后台之后，系统可以继续上报位置信息。

应用如需使用ohos.permission.LOCATION_IN_BACKGROUND权限，需要在设置界面由用户手动授予，具体授权方式可参考[ohos.permission.LOCATION_IN_BACKGROUND权限说明](../../security/AccessToken/permissions-for-all.md#ohospermissionlocation_in_background)。

长时任务申请可参考[长时任务](../../task-management/continuous-task.md)。

开发者可以在应用配置文件中声明所需要的权限，具体可参考[向用户申请授权](../../security/AccessToken/request-user-authorization.md)。


## 导入模块

```ts
import geoLocationManager from '@ohos.geoLocationManager';
```

## GeoAddress

地理编码地址信息。

**系统能力**：SystemCapability.Location.Location.Geocoder

| 名称 | 类型 | 可读|可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| isFromMock | Boolean | 是 | 否 | 表示地名信息是否来自于逆地理编码模拟功能。<br>**系统API**：此接口为系统接口。 |


## Location

位置信息。

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 类型 | 可读|可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| isFromMock | Boolean | 是 | 否 | 表示位置信息是否来自于位置模拟功能。<br>**系统API**：此接口为系统接口。 |


## ReverseGeocodingMockInfo

逆地理编码模拟功能的配置信息，包含一个位置信息和一个地名信息。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口。

| 名称 | 类型 | 可读|可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| location |  [ReverseGeoCodeRequest](js-apis-geoLocationManager.md#reversegeocoderequest) | 是 | 是 | 表示经纬度信息。 |
| geoAddress |  [GeoAddress](#geoaddress) | 是 | 是 |表示地名信息。 |


## LocationMockConfig

位置模拟功能的配置参数，包含了模拟位置上报的时间间隔和模拟位置数组。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口。

| 名称 | 类型 | 可读|可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| timeInterval | number | 是 | 是 | 表示模拟位置上报的时间间隔，单位是秒。 |
| locations | Array&lt;[Location](#location)&gt; | 是 | 是 | 表示模拟位置数组。 |

## LocatingRequiredDataConfig<sup>10+</sup>

获取定位所需数据时的配置参数。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口。

| 名称 | 类型 | 可读|可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| type | [LocatingRequiredDataType](#locatingrequireddatatype10) | 是 | 是 | 表示请求获取数据的类型。 |
| needStartScan |  boolean | 是 | 是 | 表示是否需要发起扫描。 |
| scanInterval |  number | 是 | 是 | 表示扫描的时间间隔。单位是毫秒，默认值是10000毫秒，取值范围为大于0。 |
| scanTimeout |  number | 是 | 是 | 表示单次扫描的超时时间。单位是毫秒，默认值是10000毫秒，取值范围为大于0小于600000。 |


## LocatingRequiredData<sup>10+</sup>

表示定位业务所需的数据，包含WiFi或蓝牙扫描结果，APP拿到这些数据之后可以用于网络定位等业务。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口。

| 名称 | 类型 | 可读|可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| wifiData | [WifiScanInfo](#wifiscaninfo10) | 是 | 否 | 表示WiFi扫描结果。 |
| bluetoothData |  [BluetoothScanInfo](#bluetoothscaninfo10) | 是 | 否 | 表示蓝牙扫描结果。 |


## WifiScanInfo<sup>10+</sup>

WiFi扫描信息，包含扫描到的WiFi热点的ssid、bssid和rssi等信息。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口。

| 名称 | 类型 | 可读|可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| ssid | string | 是 | 否 | WiFi热点的SSID，编码格式为UTF-8。 |
| bssid | string | 是 | 否 | WiFi热点的BSSID。 |
| rssi | number | 是 | 否 | WiFi热点的信号强度(dBm)。 |
| frequency | number | 是 | 否 | WiFi热点的频率。 |
| timestamp | number | 是 | 否 | 时间戳。 |


## BluetoothScanInfo<sup>10+</sup>

蓝牙扫描信息。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口。

| 名称 | 类型 | 可读|可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| deviceName | string | 是 | 否 | 蓝牙设备名称。 |
| macAddress | string | 是 | 否 | 蓝牙设备的MAC地址。 |
| rssi | number | 是 | 否 | 蓝牙设备的信号强度(dBm)。 |
| timestamp | number | 是 | 否 | 时间戳。 |

## LocationPrivacyType

定位服务隐私协议类型。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口。

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| OTHERS | 0 | 其他场景。预留字段。 |
| STARTUP | 1 | 开机向导场景下的隐私协议。在开机时弹出协议，提醒用户阅读并选择是否授权。 |
| CORE_LOCATION | 2 | 开启网络定位时弹出的隐私协议。 |

## LocatingRequiredDataType<sup>10+</sup>

定位业务所需数据的类型。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口。

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| WIFI  | 1 | 表示WiFi扫描信息。 |
| BLUETOOTH | 2 | 表示蓝牙扫描信息。 |

## geoLocationManager.on('locatingRequiredDataChange')<sup>10+</sup>

on(type: 'locatingRequiredDataChange', config: LocatingRequiredDataConfig, callback: Callback&lt;Array&lt;LocatingRequiredData&gt;&gt;): void;

订阅定位业务所需数据的变化，主要包含WiFi和蓝牙扫描信息；根据入参决定是否启动WiFi和蓝牙扫描。

**需要权限**：ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口。

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“locatingRequiredDataChange”，表示订阅定位业务所需数据的变化。 |
  | config | [LocatingRequiredDataConfig](#locatingrequireddataconfig10) | 是 | 表示获取定位所需数据时的配置参数。 |
  | callback | Callback&lt;Array&lt;[LocatingRequiredData](#locatingrequireddata10)&gt;&gt; | 是 | 接收定位业务所需数据的上报。 |

**错误码**：

以下错误码的详细介绍请参见[位置服务子系统错误码](errorcode-geoLocationManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
|3301800 | Failed to start WiFi or Bluetooth scanning.                            |

**示例**

  ```ts
  import geoLocationManager from '@ohos.geoLocationManager';
  import BusinessError from "@ohos.base";
  let callback = (code:Array<geoLocationManager.LocatingRequiredData>):void => {
      console.log('locatingRequiredDataChange: ' + JSON.stringify(code));
  }
  let config:geoLocationManager.LocatingRequiredDataConfig = {'type': 1, 'needStartScan': true, 'scanInterval': 10000};
  try {
      geoLocationManager.on('locatingRequiredDataChange', config, callback);
  } catch (err) {
      console.error("errCode:" + (err as BusinessError.BusinessError).code + ",errMessage:" + (err as BusinessError.BusinessError).message);
  }
  ```


## geoLocationManager.off('locatingRequiredDataChange')<sup>10+</sup>

off(type: 'locatingRequiredDataChange', callback?: Callback&lt;Array&lt;LocatingRequiredData&gt;&gt;): void;

取消订阅定位业务所需数据的变化，并停止WiFi和蓝牙扫描。

**需要权限**：ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口。

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“locatingRequiredDataChange”，表示取消订阅定位业务所需数据的变化。 |
  | callback | Callback&lt;Array&lt;[LocatingRequiredData](#locatingrequireddata10)&gt;&gt; | 否 | 需要取消订阅的回调函数。若无此参数，则取消当前类型的所有订阅。 |

**错误码**：

错误码的详细介绍请参见[位置服务子系统错误码](errorcode-geoLocationManager.md)。

**示例**

  ```ts
  import geoLocationManager from '@ohos.geoLocationManager';
  import BusinessError from "@ohos.base";
  let callback = (code:Array<geoLocationManager.LocatingRequiredData>):void => {
      console.log('locatingRequiredDataChange: ' + JSON.stringify(code));
  }
  let config:geoLocationManager.LocatingRequiredDataConfig = {'type': 1, 'needStartScan': true, 'scanInterval': 10000};
  try {
      geoLocationManager.on('locatingRequiredDataChange', config, callback);
      geoLocationManager.off('locatingRequiredDataChange', callback);
  } catch (err) {
      console.error("errCode:" + (err as BusinessError.BusinessError).code + ",errMessage:" + (err as BusinessError.BusinessError).message);
  }
  ```

## geoLocationManager.enableLocation

enableLocation(callback: AsyncCallback&lt;void&gt;): void;

打开位置服务，使用callback回调异步返回结果。

**系统API**：此接口为系统接口。

**需要权限**：ohos.permission.MANAGE_SECURE_SETTINGS

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;void&gt; | 是 | 用来接收错误码信息。 |

**错误码**：

以下错误码的详细介绍请参见[位置服务子系统错误码](errorcode-geoLocationManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
|3301000 | Location service is unavailable.                                            |

**示例**

  ```ts
  import geoLocationManager from '@ohos.geoLocationManager';
  import BusinessError from "@ohos.base";
  try {
      geoLocationManager.enableLocation((err) => {
          if (err) {
              console.error('enableLocation: err=' + JSON.stringify(err));
          }
      });
  } catch (err) {
      console.error("errCode:" + (err as BusinessError.BusinessError).code + ",errMessage:" + (err as BusinessError.BusinessError).message);
  }
  ```


## geoLocationManager.enableLocation

enableLocation(): Promise&lt;void&gt;

打开位置服务，使用Promise方式异步返回结果。

**系统API**：此接口为系统接口。

**需要权限**：ohos.permission.MANAGE_SECURE_SETTINGS

**系统能力**：SystemCapability.Location.Location.Core

**返回值**：

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 返回Promise对象。 |

**错误码**：

以下错误码的详细介绍请参见[位置服务子系统错误码](errorcode-geoLocationManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
|3301000 | Location service is unavailable.                                            |

**示例**

  ```ts
  import geoLocationManager from '@ohos.geoLocationManager';
  import BusinessError from "@ohos.base";
  try {
      geoLocationManager.enableLocation().then(() => {
          console.log('promise, enableLocation succeed');
      })
      .catch((error:number) => {
          console.error('promise, enableLocation: error=' + JSON.stringify(error));
      });
  } catch (err) {
      console.error("errCode:" + (err as BusinessError.BusinessError).code + ",errMessage:" + (err as BusinessError.BusinessError).message);
  }
  ```

## geoLocationManager.disableLocation

disableLocation(): void;

关闭位置服务。

**系统API**：此接口为系统接口。

**需要权限**：ohos.permission.MANAGE_SECURE_SETTINGS

**系统能力**：SystemCapability.Location.Location.Core

**错误码**：

以下错误码的详细介绍请参见[位置服务子系统错误码](errorcode-geoLocationManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
|3301000 | Location service is unavailable.                                            |

**示例**

  ```ts
  import geoLocationManager from '@ohos.geoLocationManager';
  import BusinessError from "@ohos.base";
  try {
      geoLocationManager.disableLocation();
  } catch (err) {
      console.error("errCode:" + (err as BusinessError.BusinessError).code + ",errMessage:" + (err as BusinessError.BusinessError).message);
  }
  ```

## geoLocationManager.enableLocationMock

enableLocationMock(): void;

使能位置模拟功能。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口。

**错误码**：

以下错误码的详细介绍请参见[位置服务子系统错误码](errorcode-geoLocationManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
|3301000 | Location service is unavailable.                                            |
|3301100 | The location switch is off.|

**示例**

  ```ts
  import geoLocationManager from '@ohos.geoLocationManager';
  import BusinessError from "@ohos.base";
  try {
      geoLocationManager.enableLocationMock();
  } catch (err) {
      console.error("errCode:" + (err as BusinessError.BusinessError).code + ",errMessage:" + (err as BusinessError.BusinessError).message);
  }
  ```


## geoLocationManager.disableLocationMock

disableLocationMock(): void;

去使能位置模拟功能。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口。

**错误码**：

以下错误码的详细介绍请参见[位置服务子系统错误码](errorcode-geoLocationManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
|3301000 | Location service is unavailable.                                            |
|3301100 | The location switch is off.|

**示例**

  ```ts
  import geoLocationManager from '@ohos.geoLocationManager';
  import BusinessError from "@ohos.base";
  try {
      geoLocationManager.disableLocationMock();
  } catch (err) {
      console.error("errCode:" + (err as BusinessError.BusinessError).code + ",errMessage:" + (err as BusinessError.BusinessError).message);
  }
  ```


## geoLocationManager.setMockedLocations

setMockedLocations(config: LocationMockConfig): void;

设置模拟的位置信息，后面会以该接口中携带的时间间隔上报模拟位置。

该接口需要在调用[geoLocationManager.enableLocationMock](#geolocationmanagerenablelocationmock)之后才能调用。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口。

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | config |  [LocationMockConfig](#locationmockconfig) | 是 | 指示位置模拟的配置参数，包含模拟位置上报的时间间隔和模拟位置数组。 |

**错误码**：

以下错误码的详细介绍请参见[位置服务子系统错误码](errorcode-geoLocationManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
|3301000 | Location service is unavailable.                                            |
|3301100 | The location switch is off.|

**示例**

  ```ts
  import geoLocationManager from '@ohos.geoLocationManager';
  import BusinessError from "@ohos.base";
  let locations:Array<geoLocationManager.Location> = [
      {"latitude": 30.12, "longitude": 120.11, "altitude": 123, "accuracy": 1, "speed": 5.2, "timeStamp": 16594326109, "direction": 123.11, "timeSinceBoot": 1000000000, "additionSize": 0, "isFromMock": true},
      {"latitude": 31.13, "longitude": 121.11, "altitude": 123, "accuracy": 2, "speed": 5.2, "timeStamp": 16594326109, "direction": 123.11, "timeSinceBoot": 2000000000, "additionSize": 0, "isFromMock": true},
      {"latitude": 32.14, "longitude": 122.11, "altitude": 123, "accuracy": 3, "speed": 5.2, "timeStamp": 16594326109, "direction": 123.11, "timeSinceBoot": 3000000000, "additionSize": 0, "isFromMock": true},
      {"latitude": 33.15, "longitude": 123.11, "altitude": 123, "accuracy": 4, "speed": 5.2, "timeStamp": 16594326109, "direction": 123.11, "timeSinceBoot": 4000000000, "additionSize": 0, "isFromMock": true},
      {"latitude": 34.16, "longitude": 124.11, "altitude": 123, "accuracy": 5, "speed": 5.2, "timeStamp": 16594326109, "direction": 123.11, "timeSinceBoot": 5000000000, "additionSize": 0, "isFromMock": true}
  ];
  let config:geoLocationManager.LocationMockConfig = {"timeInterval": 5, "locations": locations};
  try {
      geoLocationManager.enableLocationMock();
      geoLocationManager.setMockedLocations(config);
  } catch (err) {
      console.error("errCode:" + (err as BusinessError.BusinessError).code + ",errMessage:" + (err as BusinessError.BusinessError).message);
  }
  ```


## geoLocationManager.enableReverseGeocodingMock

enableReverseGeocodingMock(): void;

使能逆地理编码模拟功能。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口。

**错误码**：

以下错误码的详细介绍请参见[位置服务子系统错误码](errorcode-geoLocationManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
|3301000 | Location service is unavailable.                                            |

**示例**

  ```ts
  import geoLocationManager from '@ohos.geoLocationManager';
  import BusinessError from "@ohos.base";
  try {
      geoLocationManager.enableReverseGeocodingMock();
  } catch (err) {
      console.error("errCode:" + (err as BusinessError.BusinessError).code + ",errMessage:" + (err as BusinessError.BusinessError).message);
  }
  ```


## geoLocationManager.disableReverseGeocodingMock

disableReverseGeocodingMock(): void;

去使能逆地理编码模拟功能。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口。

**错误码**：

以下错误码的详细介绍请参见[位置服务子系统错误码](errorcode-geoLocationManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
|3301000 | Location service is unavailable.                                            |

**示例**

  ```ts
  import geoLocationManager from '@ohos.geoLocationManager';
  import BusinessError from "@ohos.base";
  try {
      geoLocationManager.disableReverseGeocodingMock();
  } catch (err) {
      console.error("errCode:" + (err as BusinessError.BusinessError).code + ",errMessage:" + (err as BusinessError.BusinessError).message);
  }
  ```


## geoLocationManager.setReverseGeocodingMockInfo

setReverseGeocodingMockInfo(mockInfos: Array&lt;ReverseGeocodingMockInfo&gt;): void;

设置逆地理编码模拟功能的配置信息，包含了位置和地名的对应关系，后续进行逆地理编码查询时如果位置信息位于配置信息中，就返回对应的地名。

该接口需要在调用[geoLocationManager.enableReverseGeocodingMock](#geolocationmanagerenablereversegeocodingmock)之后才能调用。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口。

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | mockInfos | Array&lt;[ReverseGeocodingMockInfo](#reversegeocodingmockinfo)&gt; | 是 | 指示逆地理编码模拟功能的配置参数数组。逆地理编码模拟功能的配置参数包含了一个位置和一个地名。 |

**错误码**：

以下错误码的详细介绍请参见[位置服务子系统错误码](errorcode-geoLocationManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
|3301000 | Location service is unavailable.                                            |

**示例**

  ```ts
  import geoLocationManager from '@ohos.geoLocationManager';
  import BusinessError from "@ohos.base";
  let mockInfos:Array<geoLocationManager.ReverseGeocodingMockInfo> = [
      {"location": {"locale": "zh", "latitude": 30.12, "longitude": 120.11, "maxItems": 1}, "geoAddress": {"locale": "zh", "latitude": 30.12, "longitude": 120.11, "isFromMock": true}},
      {"location": {"locale": "zh", "latitude": 31.12, "longitude": 121.11, "maxItems": 1}, "geoAddress": {"locale": "zh", "latitude": 31.12, "longitude": 121.11, "isFromMock": true}},
      {"location": {"locale": "zh", "latitude": 32.12, "longitude": 122.11, "maxItems": 1}, "geoAddress": {"locale": "zh", "latitude": 32.12, "longitude": 122.11, "isFromMock": true}},
      {"location": {"locale": "zh", "latitude": 33.12, "longitude": 123.11, "maxItems": 1}, "geoAddress": {"locale": "zh", "latitude": 33.12, "longitude": 123.11, "isFromMock": true}},
      {"location": {"locale": "zh", "latitude": 34.12, "longitude": 124.11, "maxItems": 1}, "geoAddress": {"locale": "zh", "latitude": 34.12, "longitude": 124.11, "isFromMock": true}},
  ];
  try {
      geoLocationManager.enableReverseGeocodingMock();
      geoLocationManager.setReverseGeocodingMockInfo(mockInfos);
  } catch (err) {
      console.error("errCode:" + (err as BusinessError.BusinessError).code + ",errMessage:" + (err as BusinessError.BusinessError).message);
  }
  ```


## geoLocationManager.isLocationPrivacyConfirmed

isLocationPrivacyConfirmed(type: LocationPrivacyType): boolean;

查询用户是否同意定位服务隐私申明，是否同意启用定位服务。只有系统应用才能调用。

**系统API**：此接口为系统接口。

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type |  [LocationPrivacyType](#locationprivacytype)| 是 | 指定隐私申明场景，例如开机向导中的隐私申明、开启网络定位功能时弹出的隐私申明等。 |

**返回值**：

  | 类型 | 说明 |
  | -------- | -------- |
  | boolean | 表示用户是否同意定位服务隐私申明。 |

**错误码**：

以下错误码的详细介绍请参见[位置服务子系统错误码](errorcode-geoLocationManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
|3301000 | Location service is unavailable.                                            |

**示例**

  ```ts
  import geoLocationManager from '@ohos.geoLocationManager';
  import BusinessError from "@ohos.base";
  try {
      let isConfirmed = geoLocationManager.isLocationPrivacyConfirmed(1);
  } catch (err) {
      console.error("errCode:" + (err as BusinessError.BusinessError).code + ",errMessage:" + (err as BusinessError.BusinessError).message);
  }
  ```


## geoLocationManager.setLocationPrivacyConfirmStatus

setLocationPrivacyConfirmStatus(type: LocationPrivacyType, isConfirmed: boolean): void;

设置用户勾选定位服务隐私申明的状态，记录用户是否同意启用定位服务。只有系统应用才能调用。

**系统API**：此接口为系统接口。

**需要权限**：ohos.permission.MANAGE_SECURE_SETTINGS

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | [LocationPrivacyType](#locationprivacytype) | 是 | 指定隐私申明场景，例如开机向导中的隐私申明、开启网络定位功能时弹出的隐私申明等。 |
  | isConfirmed | boolean | 是 | 表示用户是否同意定位服务隐私申明。 |

**错误码**：

以下错误码的详细介绍请参见[位置服务子系统错误码](errorcode-geoLocationManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
|3301000 | Location service is unavailable.                                            |

**示例**

  ```ts
  import geoLocationManager from '@ohos.geoLocationManager';
  import BusinessError from "@ohos.base";
  try {
      geoLocationManager.setLocationPrivacyConfirmStatus(1, true);
  } catch (err) {
      console.error("errCode:" + (err as BusinessError.BusinessError).code + ",errMessage:" + (err as BusinessError.BusinessError).message);
  }
  ```


## geoLocationManager.getLocatingRequiredData<sup>10+</sup>

getLocatingRequiredData(config: LocatingRequiredDataConfig): Promise&lt;Array&lt;LocatingRequiredData&gt;&gt;;

单次获取定位业务所需数据，包含WiFi蓝牙扫描信息，使用Promise方式异步返回结果。

**需要权限**：ohos.permission.LOCATION 和 ohos.permission.APPROXIMATELY_LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口。

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | config | [LocatingRequiredDataConfig](#locatingrequireddataconfig10) | 是 | 表示获取定位所需数据时的配置参数。 |

**返回值**：

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;Array&lt;[LocatingRequiredData](#locatingrequireddata10)&gt;&gt; | 以Promise形式返回定位业务所需数据，包含WiFi蓝牙扫描信息。 |

**错误码**：

以下错误码的详细介绍请参见[位置服务子系统错误码](errorcode-geoLocationManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
|3301800  | Failed to start WiFi or Bluetooth scanning.                    |

**示例**

  ```ts
  import geoLocationManager from '@ohos.geoLocationManager';
  import BusinessError from "@ohos.base";
  let config:geoLocationManager.LocatingRequiredDataConfig = {'type': 1, 'needStartScan': true, 'scanInterval': 10000};
  try {
      geoLocationManager.getLocatingRequiredData(config).then((result) => {
          console.log('getLocatingRequiredData return: ' + JSON.stringify(result));
      })  
      .catch((error:number) => {
          console.error('promise, getLocatingRequiredData: error=' + JSON.stringify(error));
      });
  } catch (err) {
      console.error("errCode:" + (err as BusinessError.BusinessError).code + ",errMessage:" + (err as BusinessError.BusinessError).message);
  }
  ```