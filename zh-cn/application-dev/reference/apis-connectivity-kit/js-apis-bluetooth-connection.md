# @ohos.bluetooth.connection (蓝牙connection模块)

connection模块提供了对蓝牙操作和管理的方法。

> **说明：**
>
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。



## 导入模块

```js
import connection from '@ohos.bluetooth.connection';
```


## connection.pairDevice

pairDevice(deviceId: string, callback: AsyncCallback&lt;void&gt;): void

发起蓝牙配对。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                  |
| -------- | ------ | ---- | ----------------------------------- |
| deviceId | string | 是    | 表示配对的远端设备地址，例如："XX:XX:XX:XX:XX:XX"。 |
| callback | AsyncCallback&lt;void&gt;  | 是    | 回调函数。当配对成功，err为undefined，否则为错误对象。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    // 实际的地址可由扫描流程获取
    connection.pairDevice('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.pairDevice

pairDevice(deviceId: string): Promise&lt;void&gt;

发起蓝牙配对。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                  |
| -------- | ------ | ---- | ----------------------------------- |
| deviceId | string | 是    | 表示配对的远端设备地址，例如："XX:XX:XX:XX:XX:XX"。 |

**返回值：**

| 类型                  | 说明            |
| ------------------- | ------------- |
| Promise&lt;void&gt; | 返回promise对象。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    // 实际的地址可由扫描流程获取
    connection.pairDevice('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.getRemoteDeviceName

getRemoteDeviceName(deviceId: string): string

获取对端蓝牙设备的名称。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                |
| -------- | ------ | ---- | --------------------------------- |
| deviceId | string | 是    | 表示远程设备的地址，例如："XX:XX:XX:XX:XX:XX"。 |

**返回值：**

| 类型     | 说明            |
| ------ | ------------- |
| string | 以字符串格式返回设备名称。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let remoteDeviceName: string = connection.getRemoteDeviceName('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.getRemoteDeviceClass

getRemoteDeviceClass(deviceId: string): DeviceClass

获取对端蓝牙设备的类别。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                |
| -------- | ------ | ---- | --------------------------------- |
| deviceId | string | 是    | 表示远程设备的地址，例如："XX:XX:XX:XX:XX:XX"。 |

**返回值：**

| 类型                          | 说明       |
| --------------------------- | -------- |
| [DeviceClass](#deviceclass) | 远程设备的类别。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let remoteDeviceClass: connection.DeviceClass = connection.getRemoteDeviceClass('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.getLocalName

getLocalName(): string

获取蓝牙本地设备名称。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**返回值：**

| 类型     | 说明        |
| ------ | --------- |
| string | 蓝牙本地设备名称。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let localName: string = connection.getLocalName();
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.getPairedDevices

getPairedDevices(): Array&lt;string&gt;

获取蓝牙配对列表。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**返回值：**

| 类型                  | 说明            |
| ------------------- | ------------- |
| Array&lt;string&gt; | 已配对蓝牙设备的地址列表。基于信息安全考虑，此处获取的设备地址为随机MAC地址。配对成功后，该地址不会变更；已配对设备取消配对后重新扫描或蓝牙服务下电时，该随机地址会变更。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let devices: Array<string> = connection.getPairedDevices();
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.getPairState<sup>11+</sup>

getPairState(deviceId: string): BondState

获取蓝牙配对状态。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                |
| -------- | ------ | ---- | --------------------------------- |
| deviceId | string | 是    | 表示远程设备的地址，例如："XX:XX:XX:XX:XX:XX"。 |

**返回值：**

| 类型                          | 说明       |
| --------------------------- | -------- |
| [BondState](#bondstate) | 表示设备的蓝牙配对状态。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let res: connection.BondState = connection.getPairState("XX:XX:XX:XX:XX:XX");
    console.log('getPairState: ' + res);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.getProfileConnectionState

getProfileConnectionState(profileId?: ProfileId): ProfileConnectionState

获取蓝牙Profile的连接状态，其中ProfileId为可选参数。如果携带ProfileId，则返回的是当前Profile的连接状态。如果未携带ProfileId，任一Profile已连接则返回[STATE_CONNECTED](js-apis-bluetooth-constant.md#profileconnectionstate)，否则返回[STATE_DISCONNECTED](js-apis-bluetooth-constant.md#profileconnectionstate)。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名       | 类型        | 必填   | 说明                                    |
| --------- | --------- | ---- | ------------------------------------- |
| ProfileId | [profileId](js-apis-bluetooth-constant.md#profileid) | 否    | 表示profile的枚举值，例如：PROFILE_A2DP_SOURCE。 |

**返回值：**

| 类型                                              | 说明                |
| ------------------------------------------------- | ------------------- |
| [ProfileConnectionState](js-apis-bluetooth-constant.md#profileconnectionstate) | profile的连接状态。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900004 | Profile is not supported.                |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
import constant from '@ohos.bluetooth.constant';
try {
    let result: connection.ProfileConnectionState = connection.getProfileConnectionState(constant.ProfileId.PROFILE_A2DP_SOURCE);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.setDevicePairingConfirmation

setDevicePairingConfirmation(deviceId: string, accept: boolean): void

设置设备配对请求确认。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH 和 ohos.permission.MANAGE_BLUETOOTH（该权限仅系统应用可申请）

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名    | 类型      | 必填   | 说明                               |
| ------   | ------- | ---- | -------------------------------- |
| deviceId | string  | 是    | 表示远端设备地址，例如："XX:XX:XX:XX:XX:XX"。 |
| accept   | boolean | 是    | 接受配对请求设置为true，否则设置为false。        |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
// 订阅“pinRequired”配对请求事件，收到远端配对请求后设置配对确认
function onReceivePinRequiredEvent(data: connection.PinRequiredParam) { // data为配对请求的入参，配对请求参数
    console.info('pin required  = '+ JSON.stringify(data));
    connection.setDevicePairingConfirmation(data.deviceId, true);
}
try {
    connection.on('pinRequired', onReceivePinRequiredEvent);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.setDevicePinCode

setDevicePinCode(deviceId: string, code: string, callback: AsyncCallback&lt;void&gt;): void

当蓝牙配对类型PinType为PIN_TYPE_ENTER_PIN_CODE或PIN_TYPE_PIN_16_DIGITS时调用此接口，请求用户输入PIN码。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名    | 类型      | 必填   | 说明                               |
| ------ | ------- | ---- | -------------------------------- |
| deviceId | string  | 是    | 表示远端设备MAC地址，例如："XX:XX:XX:XX:XX:XX"。 |
| code   | string  | 是    | 用户输入的PIN码。        |
| callback   | AsyncCallback&lt;void&gt;  | 是    | 回调函数，当设置PinCode成功，err为undefined，否则为错误对象。        |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
//callback
try {
    connection.setDevicePinCode('11:22:33:44:55:66', '12345', (err: BusinessError) => {
        console.info('setDevicePinCode,device name err:' + JSON.stringify(err));
    });
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.setDevicePinCode

setDevicePinCode(deviceId: string, code: string): Promise&lt;void&gt;

当蓝牙配对类型PinType为PIN_TYPE_ENTER_PIN_CODE或PIN_TYPE_PIN_16_DIGITS时调用此接口，请求用户输入PIN码。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名    | 类型      | 必填   | 说明                               |
| ------ | ------- | ---- | -------------------------------- |
| deviceId | string  | 是    | 表示远端设备MAC地址，例如："XX:XX:XX:XX:XX:XX"。 |
| code   | string  | 是    | 用户输入的PIN码。        |

**返回值：**

| 类型                  | 说明            |
| ------------------- | ------------- |
| Promise&lt;void&gt; | 返回promise对象。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
//promise
try {
    connection.setDevicePinCode('11:22:33:44:55:66', '12345').then(() => {
        console.info('setDevicePinCode');
    }, (error: BusinessError) => {
        console.info('setDevicePinCode: errCode:' + error.code + ',errMessage' + error.message);
    })

} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.setLocalName

setLocalName(name: string): void

设置蓝牙本地设备名称。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名  | 类型     | 必填   | 说明                    |
| ---- | ------ | ---- | --------------------- |
| name | string | 是    | 要设置的蓝牙名称，最大长度为248字节数。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    connection.setLocalName('device_name');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.setBluetoothScanMode

setBluetoothScanMode(mode: ScanMode, duration: number): void

设置蓝牙扫描模式，可以被远端设备发现。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                    | 必填   | 说明                           |
| -------- | --------------------- | ---- | ---------------------------- |
| mode     | [ScanMode](#scanmode) | 是    | 蓝牙扫描模式。                      |
| duration | number                | 是    | 设备可被发现的持续时间，单位为毫秒；设置为0则持续可发现。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    // 设置为可连接可发现才可被远端设备扫描到，可以连接。
    connection.setBluetoothScanMode(connection.ScanMode.SCAN_MODE_CONNECTABLE_GENERAL_DISCOVERABLE, 100);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.getBluetoothScanMode

getBluetoothScanMode(): ScanMode

获取蓝牙扫描模式。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**返回值：**

| 类型                    | 说明      |
| --------------------- | ------- |
| [ScanMode](#scanmode) | 蓝牙扫描模式。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let scanMode: connection.ScanMode = connection.getBluetoothScanMode();
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.startBluetoothDiscovery

startBluetoothDiscovery(): void

开启蓝牙扫描，可以发现远端设备。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
function onReceiveEvent(data: Array<string>) {
    console.log('data length' + data.length);
}
try {
    connection.on('bluetoothDeviceFind', onReceiveEvent);
    connection.startBluetoothDiscovery();
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.stopBluetoothDiscovery

stopBluetoothDiscovery(): void

关闭蓝牙扫描。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    connection.stopBluetoothDiscovery();
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.isBluetoothDiscovering<sup>11+</sup>

isBluetoothDiscovering(): boolean

查询设备的蓝牙发现状态。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**返回值：**

| 类型                  | 说明            |
| ------------------- | ------------- |
|   boolean           | 设备已开启蓝牙发现为true，否则为false。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let res: boolean = connection.isBluetoothDiscovering();
    console.log('isBluetoothDiscovering: ' + res);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.on('bluetoothDeviceFind')

on(type: 'bluetoothDeviceFind', callback: Callback&lt;Array&lt;string&gt;&gt;): void

订阅蓝牙设备发现上报事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                  | 必填   | 说明                                     |
| -------- | ----------------------------------- | ---- | -------------------------------------- |
| type     | string                              | 是    | 填写"bluetoothDeviceFind"字符串，表示蓝牙设备发现事件。 |
| callback | Callback&lt;Array&lt;string&gt;&gt; | 是    | 表示回调函数的入参，发现的设备集合。回调函数由用户创建通过该接口注册。基于信息安全考虑，此处获取的设备地址为随机MAC地址。配对成功后，该地址不会变更；已配对设备取消配对后重新扫描或蓝牙服务下电时，该随机地址会变更。    |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
function onReceiveEvent(data: Array<string>) { // data为蓝牙设备地址集合
    console.info('bluetooth device find = '+ JSON.stringify(data));
}
try {
    connection.on('bluetoothDeviceFind', onReceiveEvent);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.off('bluetoothDeviceFind')

off(type: 'bluetoothDeviceFind', callback?: Callback&lt;Array&lt;string&gt;&gt;): void

取消订阅蓝牙设备发现上报事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                  | 必填   | 说明                                       |
| -------- | ----------------------------------- | ---- | ---------------------------------------- |
| type     | string                              | 是    | 填写"bluetoothDeviceFind"字符串，表示蓝牙设备发现事件。   |
| callback | Callback&lt;Array&lt;string&gt;&gt; | 否    | 表示取消订阅蓝牙设备发现事件上报。不填该参数则取消订阅该type对应的所有回调。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
function onReceiveEvent(data: Array<string>) {
    console.info('bluetooth device find = '+ JSON.stringify(data));
}
try {
    connection.on('bluetoothDeviceFind', onReceiveEvent);
    connection.off('bluetoothDeviceFind', onReceiveEvent);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.on('bondStateChange')

on(type: 'bondStateChange', callback: Callback&lt;BondStateParam&gt;): void

订阅蓝牙配对状态改变事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                   |
| -------- | ---------------------------------------- | ---- | ------------------------------------ |
| type     | string                                   | 是    | 填写"bondStateChange"字符串，表示蓝牙配对状态改变事件。 |
| callback | Callback&lt;[BondStateParam](#bondstateparam)&gt; | 是    | 表示回调函数的入参，配对的状态。回调函数由用户创建通过该接口注册。    |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
function onReceiveEvent(data: connection.BondStateParam) { // data为回调函数入参，表示配对的状态
    console.info('pair state = '+ JSON.stringify(data));
}
try {
    connection.on('bondStateChange', onReceiveEvent);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.off('bondStateChange')

off(type: 'bondStateChange', callback?: Callback&lt;BondStateParam&gt;): void

取消订阅蓝牙配对状态改变事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                       |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | 是    | 填写"bondStateChange"字符串，表示蓝牙配对状态改变事件。     |
| callback | Callback&lt;[BondStateParam](#bondstateparam)&gt; | 否    | 表示取消订阅蓝牙配对状态改变事件上报。不填该参数则取消订阅该type对应的所有回调。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
function onReceiveEvent(data: connection.BondStateParam) {
    console.info('bond state = '+ JSON.stringify(data));
}
try {
    connection.on('bondStateChange', onReceiveEvent);
    connection.off('bondStateChange', onReceiveEvent);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.on('pinRequired')

on(type: 'pinRequired', callback: Callback&lt;PinRequiredParam&gt;): void

订阅远端蓝牙设备的配对请求事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                               |
| -------- | ---------------------------------------- | ---- | -------------------------------- |
| type     | string                                   | 是    | 填写"pinRequired"字符串，表示配对请求事件。     |
| callback | Callback&lt;[PinRequiredParam](#pinrequiredparam)&gt; | 是    | 表示回调函数的入参，配对请求。回调函数由用户创建通过该接口注册。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
function onReceiveEvent(data: connection.PinRequiredParam) { // data为配对请求参数
    console.info('pin required = '+ JSON.stringify(data));
}
try {
    connection.on('pinRequired', onReceiveEvent);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.off('pinRequired')

off(type: 'pinRequired', callback?: Callback&lt;PinRequiredParam&gt;): void

取消订阅远端蓝牙设备的配对请求事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                       |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | 是    | 填写"pinRequired"字符串，表示配对请求事件。             |
| callback | Callback&lt;[PinRequiredParam](#pinrequiredparam)&gt; | 否    | 表示取消订阅蓝牙配对请求事件上报，入参为配对请求参数。不填该参数则取消订阅该type对应的所有回调。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
function onReceiveEvent(data: connection.PinRequiredParam) {
    console.info('pin required = '+ JSON.stringify(data));
}
try {
    connection.on('pinRequired', onReceiveEvent);
    connection.off('pinRequired', onReceiveEvent);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## BondStateParam

描述配对状态参数。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称       | 类型   | 可读   | 可写   | 说明          |
| -------- | ------ | ---- | ---- | ----------- |
| deviceId | string      | 是    | 否    | 表示要配对的设备ID。 |
| state    | BondState   | 是    | 否    | 表示配对设备的状态。 |


## PinRequiredParam

描述配对请求参数。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称       | 类型   | 可读   | 可写   | 说明          |
| -------- | ------ | ---- | ---- | ----------- |
| deviceId | string | 是    | 否    | 表示要配对的设备ID。 |
| pinCode  | string | 是    | 否    | 表示要配对的密钥。   |



## DeviceClass

描述蓝牙设备的类别。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称              | 类型                                | 可读   | 可写   | 说明               |
| --------------- | ----------------------------------- | ---- | ---- | ---------------- |
| majorClass      | [MajorClass](js-apis-bluetooth-constant.md#majorclass)           | 是    | 否    | 表示蓝牙设备主要类别的枚举。   |
| majorMinorClass | [MajorMinorClass](js-apis-bluetooth-constant.md#majorminorclass) | 是    | 否    | 表示主要次要蓝牙设备类别的枚举。 |
| classOfDevice   | number                              | 是    | 否    | 表示设备类别。          |


## BluetoothTransport

枚举，表示设备类型。例如传统蓝牙设备或低功耗蓝牙设备，支持双模默认使用TRANSPORT_BR_EDR。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称                               | 值    | 说明              |
| -------------------------------- | ------ | --------------- |
| TRANSPORT_BR_EDR   | 0 | 表示传统蓝牙(BR/EDR)设备。 |
| TRANSPORT_LE  | 1 | 表示低功耗蓝牙(BLE)设备。  |


## ScanMode

枚举，扫描模式。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称                                       | 值  | 说明              |
| ---------------------------------------- | ---- | --------------- |
| SCAN_MODE_NONE                           | 0    | 没有扫描模式。         |
| SCAN_MODE_CONNECTABLE                    | 1    | 可连接扫描模式。        |
| SCAN_MODE_GENERAL_DISCOVERABLE           | 2    | general发现模式。    |
| SCAN_MODE_LIMITED_DISCOVERABLE           | 3    | limited发现模式。    |
| SCAN_MODE_CONNECTABLE_GENERAL_DISCOVERABLE | 4    | 可连接general发现模式。 |
| SCAN_MODE_CONNECTABLE_LIMITED_DISCOVERABLE | 5    | 可连接limited发现模式。 |


## BondState

枚举，配对状态。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称                 | 值  | 说明     |
| ------------------ | ---- | ------ |
| BOND_STATE_INVALID | 0    | 无效的配对。 |
| BOND_STATE_BONDING | 1    | 正在配对。  |
| BOND_STATE_BONDED  | 2    | 已配对。   |