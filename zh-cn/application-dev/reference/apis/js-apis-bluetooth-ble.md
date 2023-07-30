# @ohos.bluetooth.ble (蓝牙ble模块)

ble模块提供了访问蓝牙个人区域网相关功能的方法。

> **说明：**
>
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。



## 导入模块

```js
import ble from '@ohos.bluetooth.ble';
```


## ble.createGattServer<a name="createGattServer"></a>

createGattServer(): GattServer

创建Gatt profile实例。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**返回值：**

| 类型                            | 说明         |
| ----------------------------- | ---------- |
| GattServer | 返回一个JavaScript Gatt服务的实例。 |

**示例：**

```js
let gattServer = ble.createGattServer();
console.info('gatt success');
```


## ble.createGattClientDevice<a name="createGattClientDevice"></a>

createGattClientDevice(deviceId: string): GattClientDevice

创建一个可使用的GattClientDevice实例。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                   |
| -------- | ------ | ---- | ------------------------------------ |
| deviceId | string | 是    | 对端设备地址，&nbsp;例如："XX:XX:XX:XX:XX:XX"。 |

**返回值：**

| 类型                                    | 说明                                   |
| ------------------------------------- | ------------------------------------ |
| [GattClientDevice](#gattclientdevice) | client端类，使用client端方法之前需要创建该类的实例进行操作。 |

**示例：**

```js
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


## ble.getConnectedBLEDevices<a name="getConnectedBLEDevices"></a>

getConnectedBLEDevices(): Array&lt;string&gt;

获取和当前设备连接的BLE设备。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**返回值：**

| 类型                  | 说明                  |
| ------------------- | ------------------- |
| Array&lt;string&gt; | 返回当前设备作为Server端时连接BLE设备地址集合。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
try {
    let result = ble.getConnectedBLEDevices();
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


## ble.startBLEScan<a name="startBLEScan"></a>

startBLEScan(filters: Array&lt;ScanFilter&gt;, options?: ScanOptions): void

发起BLE扫描流程。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名     | 类型                                     | 必填   | 说明                                  |
| ------- | -------------------------------------- | ---- | ----------------------------------- |
| filters | Array&lt;[ScanFilter](#scanfilter)&gt; | 是    | 表示扫描结果过滤策略集合，如果不使用过滤的方式，该参数设置为null。 |
| options | [ScanOptions](#scanoptions)            | 否    | 表示扫描的参数配置，可选参数。                     |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
function onReceiveEvent(data) {
    console.info('BLE scan device find result = '+ JSON.stringify(data));
}
try {
    ble.on("BLEDeviceFind", onReceiveEvent);
    ble.startBLEScan(
        [{
            deviceId:"XX:XX:XX:XX:XX:XX",
            name:"test",
            serviceUuid:"00001888-0000-1000-8000-00805f9b34fb"
        }],
        {
            interval: 500,
            dutyMode: ble.ScanDuty.SCAN_MODE_LOW_POWER,
            matchMode: ble.MatchMode.MATCH_MODE_AGGRESSIVE,
        }
    );
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


## ble.stopBLEScan<a name="stopBLEScan"></a>

stopBLEScan(): void

停止BLE扫描流程。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
try {
    ble.stopBLEScan();
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


## ble.startAdvertising<a name="startAdvertising"></a>

startAdvertising(setting: AdvertiseSetting, advData: AdvertiseData, advResponse?: AdvertiseData): void

开始发送BLE广播。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名         | 类型                                    | 必填   | 说明             |
| ----------- | ------------------------------------- | ---- | -------------- |
| setting     | [AdvertiseSetting](#advertisesetting) | 是    | BLE广播的相关参数。    |
| advData     | [AdvertiseData](#advertisedata)       | 是    | BLE广播包内容。      |
| advResponse | [AdvertiseData](#advertisedata)       | 否    | BLE回复扫描请求回复响应。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
let manufactureValueBuffer = new Uint8Array(4);
manufactureValueBuffer[0] = 1;
manufactureValueBuffer[1] = 2;
manufactureValueBuffer[2] = 3;
manufactureValueBuffer[3] = 4;

let serviceValueBuffer = new Uint8Array(4);
serviceValueBuffer[0] = 4;
serviceValueBuffer[1] = 6;
serviceValueBuffer[2] = 7;
serviceValueBuffer[3] = 8;
console.info('manufactureValueBuffer = '+ JSON.stringify(manufactureValueBuffer));
console.info('serviceValueBuffer = '+ JSON.stringify(serviceValueBuffer));
try {
    ble.startAdvertising({
            interval:150,
            txPower:0,
            connectable:true,
        },{
            serviceUuids:["00001888-0000-1000-8000-00805f9b34fb"],
            manufactureData:[{
                 manufactureId:4567,
                 manufactureValue:manufactureValueBuffer.buffer
            }],
            serviceData:[{
                serviceUuid:"00001888-0000-1000-8000-00805f9b34fb",
                serviceValue:serviceValueBuffer.buffer
            }],
        },{
            serviceUuids:["00001889-0000-1000-8000-00805f9b34fb"],
            manufactureData:[{
                manufactureId:1789,
                manufactureValue:manufactureValueBuffer.buffer
            }],
            serviceData:[{
                serviceUuid:"00001889-0000-1000-8000-00805f9b34fb",
                serviceValue:serviceValueBuffer.buffer
            }],
    });
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


## ble.stopAdvertising<a name="stopAdvertising"></a>

stopAdvertising(): void

停止发送BLE广播。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
try {
    ble.stopAdvertising();
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


## ble.on('BLEDeviceFind')

on(type: 'BLEDeviceFind', callback: Callback&lt;Array&lt;ScanResult&gt;&gt;): void

订阅BLE设备发现上报事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                  |
| -------- | ---------------------------------------- | ---- | ----------------------------------- |
| type     | string                                   | 是    | 填写"BLEDeviceFind"字符串，表示BLE设备发现事件。   |
| callback | Callback&lt;Array&lt;[ScanResult](#scanresult)&gt;&gt; | 是    | 表示回调函数的入参，发现的设备集合。回调函数由用户创建通过该接口注册。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**示例：**

```js
function onReceiveEvent(data) {
    console.info('bluetooth device find = '+ JSON.stringify(data));
}
try {
    ble.on('BLEDeviceFind', onReceiveEvent);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


## ble.off('BLEDeviceFind')

off(type: 'BLEDeviceFind', callback?: Callback&lt;Array&lt;ScanResult&gt;&gt;): void

取消订阅BLE设备发现上报事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                       |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | 是    | 填写"BLEDeviceFind"字符串，表示BLE设备发现事件。        |
| callback | Callback&lt;Array&lt;[ScanResult](#scanresult)&gt;&gt; | 否    | 表示取消订阅BLE设备发现事件上报。不填该参数则取消订阅该type对应的所有回调。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**示例：**

```js
function onReceiveEvent(data) {
    console.info('bluetooth device find = '+ JSON.stringify(data));
}
try {
    ble.on('BLEDeviceFind', onReceiveEvent);
    ble.off('BLEDeviceFind', onReceiveEvent);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


## GattServer

server端类，使用server端方法之前需要创建该类的实例进行操作，通过createGattServer()方法构造此实例。


### addService

addService(service: GattService): void

server端添加服务。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名     | 类型                          | 必填   | 说明                       |
| ------- | --------------------------- | ---- | ------------------------ |
| service | [GattService](#gattservice) | 是    | 服务端的service数据。BLE广播的相关参数 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
// 创建descriptors
let descriptors = [];
let arrayBuffer = new ArrayBuffer(8);
let descV = new Uint8Array(arrayBuffer);
descV[0] = 11;
let descriptor = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
  descriptorUuid: '00002902-0000-1000-8000-00805F9B34FB', descriptorValue: arrayBuffer};
descriptors[0] = descriptor;

// 创建characteristics
let characteristics = [];
let arrayBufferC = new ArrayBuffer(8);
let cccV = new Uint8Array(arrayBufferC);
cccV[0] = 1;
let characteristic = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB', characteristicValue: arrayBufferC, descriptors:descriptors};
let characteristicN = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001821-0000-1000-8000-00805F9B34FB', characteristicValue: arrayBufferC, descriptors:descriptors};
characteristics[0] = characteristic;

// 创建gattService
let gattService = {serviceUuid:'00001810-0000-1000-8000-00805F9B34FB', isPrimary: true, characteristics:characteristics, includeServices:[]};

try {
    gattServer.addService(gattService);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### removeService

removeService(serviceUuid: string): void

删除已添加的服务。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名         | 类型     | 必填   | 说明                                       |
| ----------- | ------ | ---- | ---------------------------------------- |
| serviceUuid | string | 是    | service的UUID，例如“00001810-0000-1000-8000-00805F9B34FB”。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900004 | Profile is not supported.                |
|2900099 | Operation failed.                        |

**示例：**

```js
let server = ble.createGattServer();
try {
    server.removeService('00001810-0000-1000-8000-00805F9B34FB');
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### close

close(): void

关闭服务端功能，去注册server在协议栈的注册，调用该接口后[GattServer](#gattserver)实例将不能再使用。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
let server = ble.createGattServer();
try {
    server.close();
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### notifyCharacteristicChanged

notifyCharacteristicChanged(deviceId: string, notifyCharacteristic: NotifyCharacteristic, callback: AsyncCallback&lt;void&gt;): void

server端特征值发生变化时，主动通知已连接的client设备。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名                  | 类型                                       | 必填   | 说明                                      |
| -------------------- | ---------------------------------------- | ---- | --------------------------------------- |
| deviceId             | string                                   | 是    | 接收通知的client端设备地址，例如“XX:XX:XX:XX:XX:XX”。 |
| notifyCharacteristic | [NotifyCharacteristic](#notifycharacteristic) | 是    | 通知的特征值数据。                               |
| callback | AsyncCallback&lt;void&gt;  | 是    | 回调函数。当通知成功，err为undefined，否则为错误对象。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
let arrayBufferC = new ArrayBuffer(8);
let notifyCharacter = {
    "serviceUuid": '00001810-0000-1000-8000-00805F9B34FB',
    "characteristicUuid": '00001820-0000-1000-8000-00805F9B34FB',
    "characteristicValue": arrayBufferC,
    "confirm": true,
};
try {
    gattServer.notifyCharacteristicChanged('XX:XX:XX:XX:XX:XX', notifyCharacter, (err) => {
        if (err) {
            console.info('notifyCharacteristicChanged callback failed');
        } else {
            console.info('notifyCharacteristicChanged callback successful');
        }
    });
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### notifyCharacteristicChanged

notifyCharacteristicChanged(deviceId: string, notifyCharacteristic: NotifyCharacteristic): Promise&lt;void&gt;

server端特征值发生变化时，主动通知已连接的client设备。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名                  | 类型                                       | 必填   | 说明                                      |
| -------------------- | ---------------------------------------- | ---- | --------------------------------------- |
| deviceId             | string                                   | 是    | 接收通知的client端设备地址，例如“XX:XX:XX:XX:XX:XX”。 |
| notifyCharacteristic | [NotifyCharacteristic](#notifycharacteristic) | 是    | 通知的特征值数据。                               |

**返回值：**

| 类型                  | 说明            |
| ------------------- | ------------- |
| Promise&lt;void&gt; | 返回promise对象。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
let arrayBufferC = new ArrayBuffer(8);
let notifyCharacter = {
    "serviceUuid": '00001810-0000-1000-8000-00805F9B34FB',
    "characteristicUuid": '00001820-0000-1000-8000-00805F9B34FB',
    "characteristicValue": arrayBufferC,
    "confirm": true,
};
try {
    gattServer.notifyCharacteristicChanged('XX:XX:XX:XX:XX:XX', notifyCharacter).then(() => {
        console.info('notifyCharacteristicChanged promise successfull');
    });
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### sendResponse

sendResponse(serverResponse: ServerResponse): void

server端回复client端的读写请求。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名            | 类型                                | 必填   | 说明              |
| -------------- | --------------------------------- | ---- | --------------- |
| serverResponse | [ServerResponse](#serverresponse) | 是    | server端回复的响应数据。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
/* send response */
let arrayBufferCCC = new ArrayBuffer(8);
let cccValue = new Uint8Array(arrayBufferCCC);
cccValue[0] = 1123;
let serverResponse = {
    'deviceId': 'XX:XX:XX:XX:XX:XX',
    'transId': 0,
    'status': 0,
    'offset': 0,
    'value': arrayBufferCCC,
};
try {
    gattServer.sendResponse(serverResponse);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### on('characteristicRead')

on(type: 'characteristicRead', callback: Callback&lt;CharacteristicReadRequest&gt;): void

server端订阅特征值读请求事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                    |
| -------- | ---------------------------------------- | ---- | ------------------------------------- |
| type     | string                                   | 是    | 填写"characteristicRead"字符串，表示特征值读请求事件。 |
| callback | Callback&lt;[CharacteristicReadRequest](#characteristicreadrequest)&gt; | 是    | 表示回调函数的入参，client端发送的读请求数据。            |

**示例：**

```js
let arrayBufferCCC = new ArrayBuffer(8);
let cccValue = new Uint8Array(arrayBufferCCC);
cccValue[0] = 1123;
function ReadCharacteristicReq(CharacteristicReadRequest) {
    let deviceId = CharacteristicReadRequest.deviceId;
    let transId = CharacteristicReadRequest.transId;
    let offset = CharacteristicReadRequest.offset;
    let characteristicUuid = CharacteristicReadRequest.characteristicUuid;

    let serverResponse = {deviceId: deviceId, transId: transId, status: 0, offset: offset, value:arrayBufferCCC};

    try {
        gattServer.sendResponse(serverResponse);
    } catch (err) {
        console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
    }
}
gattServer.on('characteristicRead', ReadCharacteristicReq);
```


### off('characteristicRead')

off(type: 'characteristicRead', callback?: Callback&lt;CharacteristicReadRequest&gt;): void

server端取消订阅特征值读请求事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                       |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | 是    | 填写"characteristicRead"字符串，表示特征值读请求事件。    |
| callback | Callback&lt;[CharacteristicReadRequest](#characteristicreadrequest)&gt; | 否    | 表示取消订阅特征值读请求事件上报。不填该参数则取消订阅该type对应的所有回调。 |

**示例：**

```js
gattServer.off('characteristicRead');
```


### on('characteristicWrite')

on(type: 'characteristicWrite', callback: Callback&lt;CharacteristicWriteRequest&gt;): void

server端订阅特征值写请求事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                     |
| -------- | ---------------------------------------- | ---- | -------------------------------------- |
| type     | string                                   | 是    | 填写"characteristicWrite"字符串，表示特征值写请求事件。 |
| callback | Callback&lt;[CharacteristicWriteRequest](#characteristicwriterequest)&gt; | 是    | 表示回调函数的入参，client端发送的写请求数据。             |

**示例：**

```js
let arrayBufferCCC = new ArrayBuffer(8);
let cccValue = new Uint8Array(arrayBufferCCC);
function WriteCharacteristicReq(CharacteristicWriteRequest) {
    let deviceId = CharacteristicWriteRequest.deviceId;
    let transId = CharacteristicWriteRequest.transId;
    let offset = CharacteristicWriteRequest.offset;
    let isPrepared = CharacteristicWriteRequest.isPrepared;
    let needRsp = CharacteristicWriteRequest.needRsp;
    let value =  new Uint8Array(CharacteristicWriteRequest.value);
    let characteristicUuid = CharacteristicWriteRequest.characteristicUuid;

    cccValue[0] = value[0];
    let serverResponse = {deviceId: deviceId, transId: transId, status: 0, offset: offset, value:arrayBufferCCC};

    try {
        gattServer.sendResponse(serverResponse);
    } catch (err) {
        console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
    }
}
gattServer.on('characteristicWrite', WriteCharacteristicReq);
```


### off('characteristicWrite')

off(type: 'characteristicWrite', callback?: Callback&lt;CharacteristicWriteRequest&gt;): void

server端取消订阅特征值写请求事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                       |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | 是    | 填写"characteristicWrite"字符串，表示特征值写请求事件。   |
| callback | Callback&lt;[CharacteristicWriteRequest](#characteristicwriterequest)&gt; | 否    | 表示取消订阅特征值写请求事件上报。不填该参数则取消订阅该type对应的所有回调。 |

**示例：**

```js
gattServer.off('characteristicWrite');
```


### on('descriptorRead')

on(type: 'descriptorRead', callback: Callback&lt;DescriptorReadRequest&gt;): void

server端订阅描述符读请求事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                |
| -------- | ---------------------------------------- | ---- | --------------------------------- |
| type     | string                                   | 是    | 填写"descriptorRead"字符串，表示描述符读请求事件。 |
| callback | Callback&lt;[DescriptorReadRequest](#descriptorreadrequest)&gt; | 是    | 表示回调函数的入参，client端发送的读请求数据。        |

**示例：**

```js
let arrayBufferDesc = new ArrayBuffer(8);
let descValue = new Uint8Array(arrayBufferDesc);
descValue[0] = 1101;
function ReadDescriptorReq(DescriptorReadRequest) {
    let deviceId = DescriptorReadRequest.deviceId;
    let transId = DescriptorReadRequest.transId;
    let offset = DescriptorReadRequest.offset;
    let descriptorUuid = DescriptorReadRequest.descriptorUuid;

    let serverResponse = {deviceId: deviceId, transId: transId, status: 0, offset: offset, value:arrayBufferDesc};

    try {
        gattServer.sendResponse(serverResponse);
    } catch (err) {
        console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
    }
}
gattServer.on('descriptorRead', ReadDescriptorReq);
```


### off('descriptorRead')

off(type: 'descriptorRead', callback?: Callback&lt;DescriptorReadRequest&gt;): void

server端取消订阅描述符读请求事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                       |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | 是    | 填写"descriptorRead"字符串，表示描述符读请求事件。        |
| callback | Callback&lt;[DescriptorReadRequest](#descriptorreadrequest)&gt; | 否    | 表示取消订阅描述符读请求事件上报。不填该参数则取消订阅该type对应的所有回调。 |

**示例：**

```js
gattServer.off('descriptorRead');
```


### on('descriptorWrite')

on(type: 'descriptorWrite', callback: Callback&lt;DescriptorWriteRequest&gt;): void

server端订阅描述符写请求事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                 |
| -------- | ---------------------------------------- | ---- | ---------------------------------- |
| type     | string                                   | 是    | 填写"descriptorWrite"字符串，表示描述符写请求事件。 |
| callback | Callback&lt;[DescriptorWriteRequest](#descriptorwriterequest)&gt; | 是    | 表示回调函数的入参，client端发送的写请求数据。         |

**示例：**

```js
let arrayBufferDesc = new ArrayBuffer(8);
let descValue = new Uint8Array(arrayBufferDesc);
function WriteDescriptorReq(DescriptorWriteRequest) {
    let deviceId = DescriptorWriteRequest.deviceId;
    let transId = DescriptorWriteRequest.transId;
    let offset = DescriptorWriteRequest.offset;
    let isPrepared = DescriptorWriteRequest.isPrepared;
    let needRsp = DescriptorWriteRequest.needRsp;
    let value = new Uint8Array(DescriptorWriteRequest.value);
    let descriptorUuid = DescriptorWriteRequest.descriptorUuid;

    descValue[0] = value[0];
    let serverResponse = {deviceId: deviceId, transId: transId, status: 0, offset: offset, value:arrayBufferDesc};

    try {
        gattServer.sendResponse(serverResponse);
    } catch (err) {
        console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
    }
}
gattServer.on('descriptorRead', WriteDescriptorReq);
```


### off('descriptorWrite')

off(type: 'descriptorWrite', callback?: Callback&lt;DescriptorWriteRequest&gt;): void

server端取消订阅描述符写请求事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                       |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | 是    | 填写"descriptorWrite"字符串，表示描述符写请求事件。       |
| callback | Callback&lt;[DescriptorWriteRequest](#descriptorwriterequest)&gt; | 否    | 表示取消订阅描述符写请求事件上报。不填该参数则取消订阅该type对应的所有回调。 |

**示例：**

```js
gattServer.off('descriptorWrite');
```


### on('connectionStateChange')

on(type: 'connectionStateChange', callback: Callback&lt;BLEConnectionChangeState&gt;): void

server端订阅BLE连接状态变化事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                       |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | 是    | 填写"connectionStateChange"字符串，表示BLE连接状态变化事件。 |
| callback | Callback&lt;[BLEConnectionChangeState](#bleconnectionchangestate)&gt; | 是    | 表示回调函数的入参，连接状态。                          |

**示例：**

```js
function Connected(BLEConnectionChangeState) {
  let deviceId = BLEConnectionChangeState.deviceId;
  let status = BLEConnectionChangeState.state;
}
gattServer.on('connectionStateChange', Connected);
```


### off('connectionStateChange')

off(type: 'connectionStateChange', callback?: Callback&lt;BLEConnectionChangeState&gt;): void

server端取消订阅BLE连接状态变化事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                       |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | 是    | 填写"connectionStateChange"字符串，表示BLE连接状态变化事件。 |
| callback | Callback&lt;[BLEConnectionChangeState](#bleconnectionchangestate)&gt; | 否    | 表示取消订阅BLE连接状态变化事件。不填该参数则取消订阅该type对应的所有回调。 |

**示例：**

```js
gattServer.off('connectionStateChange');
```


## GattClientDevice

client端类，使用client端方法之前需要创建该类的实例进行操作，通过createGattClientDevice(deviceId: string)方法构造此实例。


### connect

connect(): void

client端发起连接远端蓝牙低功耗设备。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.connect();
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### disconnect

disconnect(): void

client端断开与远端蓝牙低功耗设备的连接。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.disconnect();
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### close

close(): void

关闭客户端功能，注销client在协议栈的注册，调用该接口后[GattClientDevice](#gattclientdevice)实例将不能再使用。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.close();
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### getDeviceName

getDeviceName(callback: AsyncCallback&lt;string&gt;): void

client获取远端蓝牙低功耗设备名。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                          | 必填   | 说明                              |
| -------- | --------------------------- | ---- | ------------------------------- |
| callback | AsyncCallback&lt;string&gt; | 是    | client获取对端server设备名，通过注册回调函数获取。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**示例：**

```js
// callback
try {
    let gattClient = ble.createGattClientDevice("XX:XX:XX:XX:XX:XX");
    gattClient.connect();
    let deviceName = gattClient.getDeviceName((err, data)=> {
        console.info('device name err ' + JSON.stringify(err));
        console.info('device name' + JSON.stringify(data));
    })
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### getDeviceName

getDeviceName(): Promise&lt;string&gt;

client获取远端蓝牙低功耗设备名。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**返回值：**

| 类型                    | 说明                                 |
| --------------------- | ---------------------------------- |
| Promise&lt;string&gt; | client获取对端server设备名，通过promise形式获取。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**示例：**

```js
// promise
try {
    let gattClient = ble.createGattClientDevice("XX:XX:XX:XX:XX:XX");
    gattClient.connect();
    let deviceName = gattClient.getDeviceName().then((data) => {
        console.info('device name' + JSON.stringify(data));
    })
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### getServices

getServices(callback: AsyncCallback&lt;Array&lt;GattService&gt;&gt;): void

client端获取蓝牙低功耗设备的所有服务，即服务发现 。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                       |
| -------- | ---------------------------------------- | ---- | ------------------------ |
| callback | AsyncCallback&lt;Array&lt;[GattService](#gattservice)&gt;&gt; | 是    | client进行服务发现，通过注册回调函数获取。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**示例：**

```js
// callkback 模式
function getServices(code, gattServices) {
  if (code.code == 0) {
      let services = gattServices;
      console.log('bluetooth code is ' + code.code);
      console.log('bluetooth services size is ', services.length);

      for (let i = 0; i < services.length; i++) {
        console.log('bluetooth serviceUuid is ' + services[i].serviceUuid);
      }
  }
}

try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.connect();
    device.getServices(getServices);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### getServices

getServices(): Promise&lt;Array&lt;GattService&gt;&gt;

client端获取蓝牙低功耗设备的所有服务，即服务发现。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**返回值：**

| 类型                                       | 说明                          |
| ---------------------------------------- | --------------------------- |
| Promise&lt;Array&lt;[GattService](#gattservice)&gt;&gt; | client进行服务发现，通过promise形式获取。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**示例：**

```js
// Promise 模式
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.connect();
    device.getServices().then(result => {
        console.info('getServices successfully:' + JSON.stringify(result));
    });
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### readCharacteristicValue

readCharacteristicValue(characteristic: BLECharacteristic, callback: AsyncCallback&lt;BLECharacteristic&gt;): void

client端读取蓝牙低功耗设备特定服务的特征值。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名            | 类型                                       | 必填   | 说明                      |
| -------------- | ---------------------------------------- | ---- | ----------------------- |
| characteristic | [BLECharacteristic](#blecharacteristic)  | 是    | 待读取的特征值。                |
| callback       | AsyncCallback&lt;[BLECharacteristic](#blecharacteristic)&gt; | 是    | client读取特征值，通过注册回调函数获取。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2901000 | Read forbidden.                         |
|2900099 | Operation failed.                        |

**示例：**

```js
function readCcc(code, BLECharacteristic) {
  if (code.code != 0) {
      return;
  }
  console.log('bluetooth characteristic uuid: ' + BLECharacteristic.characteristicUuid);
  let value = new Uint8Array(BLECharacteristic.characteristicValue);
  console.log('bluetooth characteristic value: ' + value[0] +','+ value[1]+','+ value[2]+','+ value[3]);
}

let descriptors = [];
let bufferDesc = new ArrayBuffer(8);
let descV = new Uint8Array(bufferDesc);
descV[0] = 11;
let descriptor = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
descriptorUuid: '00002903-0000-1000-8000-00805F9B34FB', descriptorValue: bufferDesc};
descriptors[0] = descriptor;

let bufferCCC = new ArrayBuffer(8);
let cccV = new Uint8Array(bufferCCC);
cccV[0] = 1;
let characteristic = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
characteristicValue: bufferCCC, descriptors:descriptors};

try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.readCharacteristicValue(characteristic, readCcc);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### readCharacteristicValue

readCharacteristicValue(characteristic: BLECharacteristic): Promise&lt;BLECharacteristic&gt;

client端读取蓝牙低功耗设备特定服务的特征值。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名            | 类型                                      | 必填   | 说明       |
| -------------- | --------------------------------------- | ---- | -------- |
| characteristic | [BLECharacteristic](#blecharacteristic) | 是    | 待读取的特征值。 |

**返回值：**

| 类型                                       | 说明                         |
| ---------------------------------------- | -------------------------- |
| Promise&lt;[BLECharacteristic](#blecharacteristic)&gt; | client读取特征值，通过promise形式获取。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2901000 | Read forbidden.                         |
|2900099 | Operation failed.                        |

**示例：**

```js
let descriptors = [];
let bufferDesc = new ArrayBuffer(8);
let descV = new Uint8Array(bufferDesc);
descV[0] = 11;
let descriptor = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
descriptorUuid: '00002903-0000-1000-8000-00805F9B34FB', descriptorValue: bufferDesc};
descriptors[0] = descriptor;

let bufferCCC = new ArrayBuffer(8);
let cccV = new Uint8Array(bufferCCC);
cccV[0] = 1;
let characteristic = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
characteristicValue: bufferCCC, descriptors:descriptors};

try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.readCharacteristicValue(characteristic);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### readDescriptorValue

readDescriptorValue(descriptor: BLEDescriptor, callback: AsyncCallback&lt;BLEDescriptor&gt;): void

client端读取蓝牙低功耗设备特定的特征包含的描述符。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名        | 类型                                       | 必填   | 说明                      |
| ---------- | ---------------------------------------- | ---- | ----------------------- |
| descriptor | [BLEDescriptor](#bledescriptor)          | 是    | 待读取的描述符。                |
| callback   | AsyncCallback&lt;[BLEDescriptor](#bledescriptor)&gt; | 是    | client读取描述符，通过注册回调函数获取。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2901000 | Read forbidden.                         |
|2900099 | Operation failed.                        |

**示例：**

```js
function readDesc(code, BLEDescriptor) {
    if (code.code != 0) {
        return;
    }
    console.log('bluetooth descriptor uuid: ' + BLEDescriptor.descriptorUuid);
    let value = new Uint8Array(BLEDescriptor.descriptorValue);
    console.log('bluetooth descriptor value: ' + value[0] +','+ value[1]+','+ value[2]+','+ value[3]);
}

let bufferDesc = new ArrayBuffer(8);
let descV = new Uint8Array(bufferDesc);
descV[0] = 11;
let descriptor = {
    serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
    characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
    descriptorUuid: '00002903-0000-1000-8000-00805F9B34FB',
    descriptorValue: bufferDesc
};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.readDescriptorValue(descriptor, readDesc);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### readDescriptorValue

readDescriptorValue(descriptor: BLEDescriptor): Promise&lt;BLEDescriptor&gt;

client端读取蓝牙低功耗设备特定的特征包含的描述符。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名        | 类型                              | 必填   | 说明       |
| ---------- | ------------------------------- | ---- | -------- |
| descriptor | [BLEDescriptor](#bledescriptor) | 是    | 待读取的描述符。 |

**返回值：**

| 类型                                       | 说明                         |
| ---------------------------------------- | -------------------------- |
| Promise&lt;[BLEDescriptor](#bledescriptor)&gt; | client读取描述符，通过promise形式获取。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.               |
|2901000 | Read forbidden.                |
|2900099 | Operation failed.              |

**示例：**

```js
let bufferDesc = new ArrayBuffer(8);
let descV = new Uint8Array(bufferDesc);
descV[0] = 11;
let descriptor = {
    serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
    characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
    descriptorUuid: '00002903-0000-1000-8000-00805F9B34FB',
    descriptorValue: bufferDesc
};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.readDescriptorValue(descriptor);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### writeCharacteristicValue

writeCharacteristicValue(characteristic: BLECharacteristic, writeType: GattWriteType, callback: AsyncCallback&lt;void&gt;): void

client端向低功耗蓝牙设备写入特定的特征值。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名            | 类型                                      | 必填   | 说明                  |
| -------------- | --------------------------------------- | ---- | ------------------- |
| characteristic | [BLECharacteristic](#blecharacteristic) | 是    | 蓝牙设备特征对应的二进制值及其它参数。 |
| writeType | GattWriteType | 是    | 蓝牙设备特征的写入类型。 |
| callback   | AsyncCallback&lt;void&gt; | 是    | 回调函数。当写入成功，err为undefined，否则为错误对象。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2901001 | Write forbidden.                        |
|2900099 | Operation failed.                        |

**示例：**

```js
let descriptors = [];
let bufferDesc = new ArrayBuffer(8);
let descV = new Uint8Array(bufferDesc);
descV[0] = 11;
let descriptor = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
  descriptorUuid: '00002903-0000-1000-8000-00805F9B34FB', descriptorValue: bufferDesc};
descriptors[0] = descriptor;

let bufferCCC = new ArrayBuffer(8);
let cccV = new Uint8Array(bufferCCC);
cccV[0] = 1;
let characteristic = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
  characteristicValue: bufferCCC, descriptors:descriptors};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.writeCharacteristicValue(characteristic);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### writeCharacteristicValue

writeCharacteristicValue(characteristic: BLECharacteristic, writeType: GattWriteType): Promise&lt;void&gt;

client端向低功耗蓝牙设备写入特定的特征值。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名            | 类型                                      | 必填   | 说明                  |
| -------------- | --------------------------------------- | ---- | ------------------- |
| characteristic | [BLECharacteristic](#blecharacteristic) | 是    | 蓝牙设备特征对应的二进制值及其它参数。 |
| writeType | GattWriteType | 是    | 蓝牙设备特征的写入类型。 |

**返回值：**

| 类型                                       | 说明                         |
| ---------------------------------------- | -------------------------- |
| Promise&lt;void&gt; | client读取描述符，通过promise形式获取。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2901001 | Write forbidden.                        |
|2900099 | Operation failed.                        |

**示例：**

```js
let descriptors = [];
let bufferDesc = new ArrayBuffer(8);
let descV = new Uint8Array(bufferDesc);
descV[0] = 11;
let descriptor = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
  descriptorUuid: '00002903-0000-1000-8000-00805F9B34FB', descriptorValue: bufferDesc};
descriptors[0] = descriptor;

let bufferCCC = new ArrayBuffer(8);
let cccV = new Uint8Array(bufferCCC);
cccV[0] = 1;
let characteristic = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
  characteristicValue: bufferCCC, descriptors:descriptors};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.writeCharacteristicValue(characteristic);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### writeDescriptorValue

writeDescriptorValue(descriptor: BLEDescriptor, callback: AsyncCallback&lt;void&gt;): void

client端向低功耗蓝牙设备特定的描述符写入二进制数据。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名        | 类型                              | 必填   | 说明                 |
| ---------- | ------------------------------- | ---- | ------------------ |
| descriptor | [BLEDescriptor](#bledescriptor) | 是    | 蓝牙设备描述符的二进制值及其它参数。 |
| callback   | AsyncCallback&lt;void&gt; | 是    | 回调函数。当写入成功，err为undefined，否则为错误对象。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2901001 | Write forbidden.                        |
|2900099 | Operation failed.                        |

**示例：**

```js
let bufferDesc = new ArrayBuffer(8);
let descV = new Uint8Array(bufferDesc);
descV[0] = 22;
let descriptor = {
    serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
    characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
    descriptorUuid: '00002903-0000-1000-8000-00805F9B34FB',
    descriptorValue: bufferDesc
};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.writeDescriptorValue(descriptor);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### writeDescriptorValue

writeDescriptorValue(descriptor: BLEDescriptor): Promise&lt;void&gt;

client端向低功耗蓝牙设备特定的描述符写入二进制数据。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名        | 类型                              | 必填   | 说明                 |
| ---------- | ------------------------------- | ---- | ------------------ |
| descriptor | [BLEDescriptor](#bledescriptor) | 是    | 蓝牙设备描述符的二进制值及其它参数。 |

**返回值：**

| 类型                                       | 说明                         |
| ---------------------------------------- | -------------------------- |
| Promise&lt;void&gt; | client读取描述符，通过promise形式获取。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2901001 | Write forbidden.                        |
|2900099 | Operation failed.                        |

**示例：**

```js
let bufferDesc = new ArrayBuffer(8);
let descV = new Uint8Array(bufferDesc);
descV[0] = 22;
let descriptor = {
    serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
    characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
    descriptorUuid: '00002903-0000-1000-8000-00805F9B34FB',
    descriptorValue: bufferDesc
};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.writeDescriptorValue(descriptor);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### getRssiValue

getRssiValue(callback: AsyncCallback&lt;number&gt;): void

client获取远端蓝牙低功耗设备的信号强度 (Received Signal Strength Indication, RSSI)，调用[connect](#connect)接口连接成功后才能使用。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                          | 必填   | 说明                             |
| -------- | --------------------------- | ---- | ------------------------------ |
| callback | AsyncCallback&lt;number&gt; | 是    | 返回信号强度，单位&nbsp;dBm，通过注册回调函数获取。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**示例：**

```js
// callback
try {
    let gattClient = ble.createGattClientDevice("XX:XX:XX:XX:XX:XX");
    gattClient.connect();
    let rssi = gattClient.getRssiValue((err, data)=> {
        console.info('rssi err ' + JSON.stringify(err));
        console.info('rssi value' + JSON.stringify(data));
    })
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### getRssiValue

getRssiValue(): Promise&lt;number&gt;

client获取远端蓝牙低功耗设备的信号强度 (Received Signal Strength Indication, RSSI)，调用[connect](#connect)接口连接成功后才能使用。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**返回值：**

| 类型                    | 说明                                |
| --------------------- | --------------------------------- |
| Promise&lt;number&gt; | 返回信号强度，单位&nbsp;dBm，通过promise形式获取。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**示例：**

```js
// promise
try {
    let gattClient = ble.createGattClientDevice("XX:XX:XX:XX:XX:XX");
    let rssi = gattClient.getRssiValue().then((data) => {
        console.info('rssi' + JSON.stringify(data));
    })
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### setBLEMtuSize

setBLEMtuSize(mtu: number): void

client协商远端蓝牙低功耗设备的最大传输单元（Maximum Transmission Unit, MTU），调用[connect](#connect)接口连接成功后才能使用。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名  | 类型     | 必填   | 说明             |
| ---- | ------ | ---- | -------------- |
| mtu  | number | 是    | 设置范围为22~512字节。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**示例：**

```js
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.setBLEMtuSize(128);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### setCharacteristicChangeNotification

setCharacteristicChangeNotification(characteristic: BLECharacteristic, enable: boolean, callback: AsyncCallback&lt;void&gt;): void

向服务端发送设置通知此特征值请求。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名            | 类型                                      | 必填   | 说明                            |
| -------------- | --------------------------------------- | ---- | ----------------------------- |
| characteristic | [BLECharacteristic](#blecharacteristic) | 是    | 蓝牙低功耗特征。                      |
| enable         | boolean                                 | 是    | 启用接收notify设置为true，否则设置为false。 |
| callback   | AsyncCallback&lt;void&gt; | 是    | 回调函数。当发送成功，err为undefined，否则为错误对象。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**示例：**

```js
// 创建descriptors
let descriptors = [];
let arrayBuffer = new ArrayBuffer(8);
let descV = new Uint8Array(arrayBuffer);
descV[0] = 11;
let descriptor = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
  descriptorUuid: '00002902-0000-1000-8000-00805F9B34FB', descriptorValue: arrayBuffer};
descriptors[0] = descriptor;
let arrayBufferC = new ArrayBuffer(8);
let characteristic = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB', characteristicValue: arrayBufferC, descriptors:descriptors};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.setCharacteristicChangeNotification(characteristic, false);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}

```


### setCharacteristicChangeNotification

setCharacteristicChangeNotification(characteristic: BLECharacteristic, enable: boolean): Promise&lt;void&gt;

向服务端发送设置通知此特征值请求。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名            | 类型                                      | 必填   | 说明                            |
| -------------- | --------------------------------------- | ---- | ----------------------------- |
| characteristic | [BLECharacteristic](#blecharacteristic) | 是    | 蓝牙低功耗特征。                      |
| enable         | boolean                                 | 是    | 启用接收notify设置为true，否则设置为false。 |

**返回值：**

| 类型                                       | 说明                         |
| ---------------------------------------- | -------------------------- |
| Promise&lt;void&gt; | 返回Promise对象。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**示例：**

```js
// 创建descriptors
let descriptors = [];
let arrayBuffer = new ArrayBuffer(8);
let descV = new Uint8Array(arrayBuffer);
descV[0] = 11;
let descriptor = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
  descriptorUuid: '00002902-0000-1000-8000-00805F9B34FB', descriptorValue: arrayBuffer};
descriptors[0] = descriptor;
let arrayBufferC = new ArrayBuffer(8);
let characteristic = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB', characteristicValue: arrayBufferC, descriptors:descriptors};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.setCharacteristicChangeNotification(characteristic, false);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}

```


### setCharacteristicChangeIndication

setCharacteristicChangeIndication(characteristic: BLECharacteristic, enable: boolean, callback: AsyncCallback&lt;void&gt;): void

向服务端发送设置通知此特征值请求。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名            | 类型                                      | 必填   | 说明                            |
| -------------- | --------------------------------------- | ---- | ----------------------------- |
| characteristic | [BLECharacteristic](#blecharacteristic) | 是    | 蓝牙低功耗特征。                      |
| enable         | boolean                                 | 是    | 启用接收notify设置为true，否则设置为false。 |
| callback   | AsyncCallback&lt;void&gt; | 是    | 回调函数。当发送成功，err为undefined，否则为错误对象。 |

**返回值：**

| 类型                                       | 说明                         |
| ---------------------------------------- | -------------------------- |
| Promise&lt;void&gt; | 返回Promise对象。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**示例：**

```js
// 创建descriptors
let descriptors = [];
let arrayBuffer = new ArrayBuffer(8);
let descV = new Uint8Array(arrayBuffer);
descV[0] = 11;
let descriptor = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
  descriptorUuid: '00002902-0000-1000-8000-00805F9B34FB', descriptorValue: arrayBuffer};
descriptors[0] = descriptor;
let arrayBufferC = new ArrayBuffer(8);
let characteristic = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB', characteristicValue: arrayBufferC, descriptors:descriptors};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.setCharacteristicChangeIndication(characteristic, false);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}

```


### setCharacteristicChangeIndication

setCharacteristicChangeIndication(characteristic: BLECharacteristic, enable: boolean): Promise&lt;void&gt;

向服务端发送设置通知此特征值请求。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名            | 类型                                      | 必填   | 说明                            |
| -------------- | --------------------------------------- | ---- | ----------------------------- |
| characteristic | [BLECharacteristic](#blecharacteristic) | 是    | 蓝牙低功耗特征。                      |
| enable         | boolean                                 | 是    | 启用接收notify设置为true，否则设置为false。 |

**返回值：**

| 类型                                       | 说明                         |
| ---------------------------------------- | -------------------------- |
| Promise&lt;void&gt; | 返回Promise对象。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](../errorcodes/errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**示例：**

```js
// 创建descriptors
let descriptors = [];
let arrayBuffer = new ArrayBuffer(8);
let descV = new Uint8Array(arrayBuffer);
descV[0] = 11;
let descriptor = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
  descriptorUuid: '00002902-0000-1000-8000-00805F9B34FB', descriptorValue: arrayBuffer};
descriptors[0] = descriptor;
let arrayBufferC = new ArrayBuffer(8);
let characteristic = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB', characteristicValue: arrayBufferC, descriptors:descriptors};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.setCharacteristicChangeIndication(characteristic, false);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}

```


### on('BLECharacteristicChange')

on(type: 'BLECharacteristicChange', callback: Callback&lt;BLECharacteristic&gt;): void

订阅蓝牙低功耗设备的特征值变化事件。需要先调用setNotifyCharacteristicChanged接口才能接收server端的通知。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                       |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | 是    | 填写"BLECharacteristicChange"字符串，表示特征值变化事件。 |
| callback | Callback&lt;[BLECharacteristic](#blecharacteristic)&gt; | 是    | 表示蓝牙低功耗设备的特征值变化事件的回调函数。                  |

**示例：**

```js
function CharacteristicChange(CharacteristicChangeReq) {
    let serviceUuid = CharacteristicChangeReq.serviceUuid;
    let characteristicUuid = CharacteristicChangeReq.characteristicUuid;
    let value = new Uint8Array(CharacteristicChangeReq.characteristicValue);
}
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.on('BLECharacteristicChange', CharacteristicChange);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### off('BLECharacteristicChange')

off(type: 'BLECharacteristicChange', callback?: Callback&lt;BLECharacteristic&gt;): void

取消订阅蓝牙低功耗设备的特征值变化事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                       |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | 是    | 填写"BLECharacteristicChange"字符串，表示特征值变化事件。 |
| callback | Callback&lt;[BLECharacteristic](#blecharacteristic)&gt; | 否    | 表示取消订阅蓝牙低功耗设备的特征值变化事件。不填该参数则取消订阅该type对应的所有回调。 |

**示例：**

```js
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.off('BLECharacteristicChange');
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### on('BLEConnectionStateChange')

on(type: 'BLEConnectionStateChange', callback: Callback&lt;BLEConnectionChangeState&gt;): void

client端订阅蓝牙低功耗设备的连接状态变化事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                       |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | 是    | 填写"BLEConnectionStateChange"字符串，表示连接状态变化事件。 |
| callback | Callback&lt;[BLEConnectionChangeState](#bleconnectionchangestate)&gt; | 是    | 表示连接状态，已连接或断开。                           |

**示例：**

```js
function ConnectStateChanged(state) {
  console.log('bluetooth connect state changed');
  let connectState = state.state;
}
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.on('BLEConnectionStateChange', ConnectStateChanged);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### off('BLEConnectionStateChange')

off(type: 'BLEConnectionStateChange', callback?: Callback&lt;BLEConnectionChangeState&gt;): void

取消订阅蓝牙低功耗设备的连接状态变化事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                       |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | 是    | 填写"BLEConnectionStateChange"字符串，表示连接状态变化事件。 |
| callback | Callback&lt;[BLEConnectionChangeState](#bleconnectionchangestate)&gt; | 否    | 表示取消订阅蓝牙低功耗设备的连接状态变化事件。不填该参数则取消订阅该type对应的所有回调。 |

**示例：**

```js
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.off('BLEConnectionStateChange');
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### on('BLEMtuChange')

on(type: 'BLEMtuChange', callback: Callback&lt;number&gt;): void

订阅Mtu状态变化事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                       |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | 是    | 填写"BLEMtuChange"字符串，表示Mtu状态变化事件。 |
| callback | Callback&lt;number&gt; | 是    | 表示Mtu状态，已连接或是断开。 |

**示例：**

```js
try {
    let gattClient = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    gattClient.on('BLEMtuChange', (mtu) => {
      console.info('BLEMtuChange, mtu: ' + mtu);
    });
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### off('BLEMtuChange')

off(type: 'BLEMtuChange', callback?: Callback&lt;number&gt;): void

订阅Mtu状态变化事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                       |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | 是    | 填写"BLEMtuChange"字符串，表示Mtu状态变化事件。 |
| callback | Callback&lt;number&gt; | 否    | 表示取消订阅Mtu状态变化事件。不填该参数则取消订阅该type对应的所有回调。 |

**示例：**

```js
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.off('BLEMtuChange');
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


## GattService

描述service的接口参数定义。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称              | 类型                                     | 可读   | 可写   | 说明                                       |
| --------------- | ---------------------------------------- | ---- | ---- | ---------------------------------------- |
| serviceUuid     | string                                   | 是    | 是    | 特定服务（service）的UUID，例如：00001888-0000-1000-8000-00805f9b34fb。 |
| isPrimary       | boolean                                  | 是    | 是    | 如果是主服务设置为true，否则设置为false。                |
| characteristics | Array&lt;[BLECharacteristic](#blecharacteristic)&gt; | 是    | 是    | 当前服务包含的特征列表。                             |
| includeServices | Array&lt;[GattService](#gattservice)&gt; | 是    | 是    | 当前服务依赖的其它服务。                             |


## BLECharacteristic

描述characteristic的接口参数定义 。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称                  | 类型                                     | 可读   | 可写   | 说明                                 |
| ------------------- | ---------------------------------------- | ---- | ---- | ---------------------------------------- |
| serviceUuid         | string                                   | 是    | 是    | 特定服务（service）的UUID，例如：00001888-0000-1000-8000-00805f9b34fb。 |
| characteristicUuid  | string                  | 是    | 是    | 特定特征（characteristic）的UUID，例如：00002a11-0000-1000-8000-00805f9b34fb。 |
| characteristicValue | ArrayBuffer                              | 是    | 是    | 特征对应的二进制值。                      |
| descriptors         | Array&lt;[BLEDescriptor](#bledescriptor)&gt; | 是    | 是    | 特定特征的描述符列表。                |
| properties  | [GattProperties](#gattproperties) |   是   | 是     | 特定特征的属性描述。     |


## BLEDescriptor

描述descriptor的接口参数定义 。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称                 | 类型        | 可读   | 可写   | 说明                                       |
| ------------------ | ----------- | ---- | ---- | ---------------------------------------- |
| serviceUuid        | string      | 是    | 是    | 特定服务（service）的UUID，例如：00001888-0000-1000-8000-00805f9b34fb。 |
| characteristicUuid | string      | 是    | 是    | 特定特征（characteristic）的UUID，例如：00002a11-0000-1000-8000-00805f9b34fb。 |
| descriptorUuid     | string      | 是    | 是    | 描述符（descriptor）的UUID，例如：00002902-0000-1000-8000-00805f9b34fb。 |
| descriptorValue    | ArrayBuffer | 是    | 是    | 描述符对应的二进制值。                              |


## NotifyCharacteristic

描述server端特征值变化时发送的特征通知参数定义。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称                  | 类型        | 可读   | 可写   | 说明                                       |
| ------------------- | ----------- | ---- | ---- | ---------------------------------------- |
| serviceUuid         | string      | 是    | 是    | 特定服务（service）的UUID，例如：00001888-0000-1000-8000-00805f9b34fb。 |
| characteristicUuid  | string      | 是    | 是    | 特定特征（characteristic）的UUID，例如：00002a11-0000-1000-8000-00805f9b34fb。 |
| characteristicValue | ArrayBuffer | 是    | 是    | 特征对应的二进制值。                               |
| confirm             | boolean     | 是    | 是    | 如果是notification则对端回复确认设置为true，如果是indication则对端不需要回复确认设置为false。 |


## CharacteristicReadRequest

描述server端订阅后收到的特征值读请求事件参数结构。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称                 | 类型   | 可读   | 可写   | 说明                                       |
| ------------------ | ------ | ---- | ---- | ---------------------------------------- |
| deviceId           | string | 是    | 否    | 表示发送特征值读请求的远端设备地址，例如："XX:XX:XX:XX:XX:XX"。 |
| transId            | number | 是    | 否    | 表示读请求的传输ID，server端回复响应时需填写相同的传输ID。       |
| offset             | number | 是    | 否    | 表示读特征值数据的起始位置。例如：k表示从第k个字节开始读，server端回复响应时需填写相同的offset。 |
| characteristicUuid | string | 是    | 否    | 特定特征（characteristic）的UUID，例如：00002a11-0000-1000-8000-00805f9b34fb。 |
| serviceUuid        | string | 是    | 否    | 特定服务（service）的UUID，例如：00001888-0000-1000-8000-00805f9b34fb。 |


## CharacteristicWriteRequest

描述server端订阅后收到的特征值写请求事件参数结构。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称                 | 类型   | 可读   | 可写   | 说明                                       |
| ------------------ | ------ | ---- | ---- | ---------------------------------------- |
| deviceId           | string | 是    | 否    | 表示发送特征值写请求的远端设备地址，例如："XX:XX:XX:XX:XX:XX"。 |
| transId            | number | 是    | 否    | 表示写请求的传输ID，server端回复响应时需填写相同的传输ID。       |
| offset             | number | 是    | 否    | 表示写特征值数据的起始位置。例如：k表示从第k个字节开始写，server端回复响应时需填写相同的offset。 |
| isPrepared             | boolean | 是    | 否    | 表示写请求是否立即执行。 |
| needRsp             | boolean | 是    | 否    | 表示是否要给client端回复响应。 |
| value             | ArrayBuffer | 是    | 否    | 表示写入的描述符二进制数据。 |
| characteristicUuid | string | 是    | 否    | 特定特征（characteristic）的UUID，例如：00002a11-0000-1000-8000-00805f9b34fb。 |
| serviceUuid        | string | 是    | 否    | 特定服务（service）的UUID，例如：00001888-0000-1000-8000-00805f9b34fb。 |


## DescriptorReadRequest

描述server端订阅后收到的描述符读请求事件参数结构。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称                 | 类型   | 可读   | 可写   | 说明                                       |
| ------------------ | ------ | ---- | ---- | ---------------------------------------- |
| deviceId           | string | 是    | 否    | 表示发送描述符读请求的远端设备地址，例如："XX:XX:XX:XX:XX:XX"。 |
| transId            | number | 是    | 否    | 表示读请求的传输ID，server端回复响应时需填写相同的传输ID。       |
| offset             | number | 是    | 否    | 表示读描述符数据的起始位置。例如：k表示从第k个字节开始读，server端回复响应时需填写相同的offset。 |
| descriptorUuid     | string | 是    | 否    | 表示描述符（descriptor）的UUID，例如：00002902-0000-1000-8000-00805f9b34fb。 |
| characteristicUuid | string | 是    | 否    | 特定特征（characteristic）的UUID，例如：00002a11-0000-1000-8000-00805f9b34fb。 |
| serviceUuid        | string | 是    | 否    | 特定服务（service）的UUID，例如：00001888-0000-1000-8000-00805f9b34fb。 |


## DescriptorWriteRequest

描述server端订阅后收到的描述符写请求事件参数结构。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称                 | 类型        | 可读   | 可写   | 说明                                       |
| ------------------ | ----------- | ---- | ---- | ---------------------------------------- |
| deviceId           | string      | 是    | 否    | 表示发送描述符写请求的远端设备地址，例如："XX:XX:XX:XX:XX:XX"。 |
| transId            | number      | 是    | 否    | 表示写请求的传输ID，server端回复响应时需填写相同的传输ID。       |
| offset             | number      | 是    | 否    | 表示写描述符数据的起始位置。例如：k表示从第k个字节开始写，server端回复响应时需填写相同的offset。 |
| isPrepared             | boolean     | 是    | 否    | 表示写请求是否立即执行。                             |
| needRsp            | boolean     | 是    | 否    | 表示是否要给client端回复响应。                       |
| value              | ArrayBuffer | 是    | 否    | 表示写入的描述符二进制数据。                           |
| descriptorUuid     | string      | 是    | 否    | 表示描述符（descriptor）的UUID，例如：00002902-0000-1000-8000-00805f9b34fb。 |
| characteristicUuid | string      | 是    | 否    | 特定特征（characteristic）的UUID，例如：00002a11-0000-1000-8000-00805f9b34fb。 |
| serviceUuid        | string      | 是    | 否    | 特定服务（service）的UUID，例如：00001888-0000-1000-8000-00805f9b34fb。 |


## ServerResponse

描述server端回复client端读/写请求的响应参数结构。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称       | 类型        | 可读   | 可写   | 说明                                     |
| -------- | ----------- | ---- | ---- | -------------------------------------- |
| deviceId | string      | 是    | 否    | 表示远端设备地址，例如："XX:XX:XX:XX:XX:XX"。       |
| transId  | number      | 是    | 否    | 表示请求的传输ID，与订阅的读/写请求事件携带的ID保持一致。        |
| status   | number      | 是    | 否    | 表示响应的状态，设置为0即可，表示正常。                   |
| offset   | number      | 是    | 否    | 表示请求的读/写起始位置，与订阅的读/写请求事件携带的offset保持一致。 |
| value    | ArrayBuffer | 是    | 否    | 表示回复响应的二进制数据。                          |


## BLEConnectionChangeState

描述Gatt profile连接状态 。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称     | 类型                                          | 可读 | 可写 | 说明                                          |
| -------- | ------------------------------------------------- | ---- | ---- | --------------------------------------------- |
| deviceId | string                                            | 是   | 否   | 表示远端设备地址，例如："XX:XX:XX:XX:XX:XX"。 |
| state    | [ProfileConnectionState](js-apis-bluetooth-constant.md#profileconnectionstate) | 是   | 是   | 表示BLE连接状态的枚举。                       |


## ScanResult

扫描结果上报数据。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称       | 类型        | 可读   | 可写   | 说明                                 |
| -------- | ----------- | ---- | ---- | ---------------------------------- |
| deviceId | string      | 是    | 否    | 表示扫描到的设备地址，例如："XX:XX:XX:XX:XX:XX"。 |
| rssi     | number      | 是    | 否    | 表示扫描到的设备的rssi值。                    |
| data     | ArrayBuffer | 是    | 否    | 表示扫描到的设备发送的广播包。                    |
| deviceName | string | 是    | 否    | 表示扫描到的设备名称。                    |
| connectable  | boolean | 是    | 否    | 表示扫描到的设备是否可连接。                    |


## AdvertiseSetting

描述蓝牙低功耗设备发送广播的参数。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称          | 类型    | 可读   | 可写   | 说明                                       |
| ----------- | ------- | ---- | ---- | ---------------------------------------- |
| interval    | number  | 是    | 是    | 表示广播间隔，最小值设置32个slot表示20ms，最大值设置16384个slot，默认值设置为1600个slot表示1s。 |
| txPower     | number  | 是    | 是    | 表示发送功率，最小值设置-127，最大值设置1，默认值设置-7，单位dbm。   |
| connectable | boolean | 是    | 是    | 表示是否是可连接广播，默认值设置为true。                   |


## AdvertiseData

描述BLE广播数据包的内容。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称              | 类型                                     | 可读   | 可写   | 说明                          |
| --------------- | ---------------------------------------- | ---- | ---- | --------------------------- |
| serviceUuids    | Array&lt;string&gt;                      | 是    | 是    | 表示要广播的服务&nbsp;UUID&nbsp;列表。 |
| manufactureData | Array&lt;[ManufactureData](#manufacturedata)&gt; | 是    | 是    | 表示要广播的广播的制造商信息列表。           |
| serviceData     | Array&lt;[ServiceData](#servicedata)&gt; | 是    | 是    | 表示要广播的服务数据列表。               |
| includeDeviceName | boolean                  | 是    | 是    | 表示是否携带设备名，可选参数。        |


## ManufactureData

描述BLE广播数据包的内容。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称               | 类型                | 可读   | 可写   | 说明                 |
| ---------------- | ------------------- | ---- | ---- | ------------------ |
| manufactureId    | number  | 是    | 是    | 表示制造商的ID，由蓝牙SIG分配。 |
| manufactureValue | ArrayBuffer         | 是    | 是    | 表示制造商发送的制造商数据。     |


## ServiceData

描述广播包中服务数据内容。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称           | 类型        | 可读   | 可写   | 说明         |
| ------------ | ----------- | ---- | ---- | ---------- |
| serviceUuid  | string      | 是    | 是    | 表示服务的UUID。 |
| serviceValue | ArrayBuffer | 是    | 是    | 表示服务数据。    |


## ScanFilter

扫描过滤参数。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称                                     | 类型    | 可读 | 可写 | 说明                                                         |
| ---------------------------------------- | ----------- | ---- | ---- | ------------------------------------------------------------ |
| deviceId                                 | string      | 是   | 是   | 表示过滤的BLE设备地址，例如："XX:XX:XX:XX:XX:XX"。           |
| name                                     | string      | 是   | 是   | 表示过滤的BLE设备名。                                        |
| serviceUuid                              | string      | 是   | 是   | 表示过滤包含该UUID服务的设备，例如：00001888-0000-1000-8000-00805f9b34fb。 |
| serviceUuidMask             | string      | 是   | 是   | 表示过滤包含该UUID服务掩码的设备，例如：FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF。 |
| serviceSolicitationUuid     | string      | 是   | 是   | 表示过滤包含该UUID服务请求的设备，例如：00001888-0000-1000-8000-00805F9B34FB。 |
| serviceSolicitationUuidMask | string      | 是   | 是   | 表示过滤包含该UUID服务请求掩码的设备，例如：FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF。 |
| serviceData                 | ArrayBuffer | 是   | 是   | 表示过滤包含该服务相关数据的设备，例如：[0x90,0x00,0xF1,0xF2]。 |
| serviceDataMask             | ArrayBuffer | 是   | 是   | 表示过滤包含该服务相关数据掩码的设备，例如：[0xFF,0xFF,0xFF,0xFF]。 |
| manufactureId               | number      | 是   | 是   | 表示过滤包含该制造商ID的设备，例如：0x0006。                 |
| manufactureData             | ArrayBuffer | 是   | 是   | 表示过滤包含该制造商相关数据的设备，例如：[0x1F,0x2F,0x3F]。 |
| manufactureDataMask         | ArrayBuffer | 是   | 是   | 表示过滤包含该制造商相关数据掩码的设备，例如：[0xFF,0xFF,0xFF]。 |


## ScanOptions

扫描的配置参数。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称        | 类型                    | 可读   | 可写   | 说明                                     |
| --------- | ----------------------- | ---- | ---- | -------------------------------------- |
| interval  | number                  | 是    | 是    | 表示扫描结果上报延迟时间，默认值为0。                    |
| dutyMode  | [ScanDuty](#scanduty)   | 是    | 是    | 表示扫描模式，默认值为SCAN_MODE_LOW_POWER。        |
| matchMode | [MatchMode](#matchmode) | 是    | 是    | 表示硬件的过滤匹配模式，默认值为MATCH_MODE_AGGRESSIVE。 |


## GattProperties<a name="GattProperties"></a>

描述gatt characteristic的属性。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称       | 类型  | 必填   | 说明          |
| -------- | ------ |---- | ----------- |
| write    | boolean | 是  | 表示该特征支持写操作，需要对端设备的回复。 |
| writeNoResponse | boolean | 是    | 表示该特征支持写操作，无需对端设备回复。 |
| read | boolean   |  是    | 表示该特征支持读操作。 |
| notify | boolean   | 是    | 表示该特征可通知对端设备。 |
| indicate | boolean   | 是    | 表示该特征可通知对端设备，需要对端设备的回复。 |


## GattWriteType<a name="GattWriteType"></a>

枚举，表示gatt写入类型。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称                                   | 值    | 说明              |
| ------------------------------------| ------ | --------------- |
| WRITE               | 1 | 表示写入特征值，需要对端设备的回复。   |
| WRITE_NO_RESPONSE   | 2 | 表示写入特征值，不需要对端设备的回复。  |


## ScanDuty

枚举，扫描模式。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称                    | 值  | 说明           |
| --------------------- | ---- | ------------ |
| SCAN_MODE_LOW_POWER   | 0    | 表示低功耗模式，默认值。 |
| SCAN_MODE_BALANCED    | 1    | 表示均衡模式。      |
| SCAN_MODE_LOW_LATENCY | 2    | 表示低延迟模式。     |


## MatchMode

枚举，硬件过滤匹配模式。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称                    | 值  | 说明                                       |
| --------------------- | ---- | ---------------------------------------- |
| MATCH_MODE_AGGRESSIVE | 1    | 表示硬件上报扫描结果门限较低，比如扫描到的功率较低或者一段时间扫描到的次数较少也触发上报，默认值。 |
| MATCH_MODE_STICKY     | 2    | 表示硬件上报扫描结果门限较高，更高的功率门限以及扫描到多次才会上报。       |