# @ohos.bluetooth.connection (蓝牙connection模块)（系统接口）

connection模块提供了对蓝牙操作和管理的方法。

> **说明：**
>
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> 当前页面仅包含本模块的系统接口，其他公开接口参见[@ohos.bluetooth.connection (蓝牙connection模块)](js-apis-bluetooth-connection.md)


## 导入模块

```js
import connection from '@ohos.bluetooth.connection';
```


## connection.pairCredibleDevice

pairCredibleDevice(deviceId: string, transport: BluetoothTransport, callback: AsyncCallback&lt;void&gt;): void

向可信的远端设备发起蓝牙配对。通过非蓝牙扫描的方式(例如NFC等)获取到外设的地址，可以通过该接口发起配对。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH 和 ohos.permission.MANAGE_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                  |
| -------- | ------ | ---- | ----------------------------------- |
| deviceId | string | 是    | 表示配对的远端设备地址，例如："XX:XX:XX:XX:XX:XX"。 |
| transport | [BluetoothTransport](js-apis-bluetooth-connection.md#bluetoothtransport) | 是    | 表示设备类型，例如传统蓝牙设备或低功耗蓝牙设备。 |
| callback | AsyncCallback&lt;void&gt; | 是    | 回调函数。当发起配对成功，err为undefined，否则为错误对象。   |

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
    connection.pairCredibleDevice('68:13:24:79:4C:8C', connection.BluetoothTransport
        .TRANSPORT_BR_EDR, (err: BusinessError) => {
        if (err) {
            console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
            return;
        }
        console.info('pairCredibleDevice, err: ' + JSON.stringify(err));
    });
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.pairCredibleDevice

pairCredibleDevice(deviceId: string, transport: BluetoothTransport): Promise&lt;void&gt;

向可信的远端设备发起蓝牙配对。通过非蓝牙扫描的方式(例如NFC等)获取到外设的地址，可以通过该接口发起配对。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH 和 ohos.permission.MANAGE_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                  |
| -------- | ------ | ---- | ----------------------------------- |
| deviceId | string | 是    | 表示配对的远端设备地址，例如："XX:XX:XX:XX:XX:XX"。 |
| transport | [BluetoothTransport](js-apis-bluetooth-connection.md#bluetoothtransport) | 是    | 表示设备类型，例如传统蓝牙设备或低功耗蓝牙设备。 |

**返回值：**

| 类型                                              | 说明                |
| ------------------------------------------------- | ------------------- |
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
    connection.pairCredibleDevice('68:13:24:79:4C:8C', 0).then(() => {
        console.info('PairCredibleDevice');
    }, (err: BusinessError) => {
        console.error('PairCredibleDevice:errCode' + err.code + ', errMessage: ' + err.message);
    });
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.cancelPairedDevice

cancelPairedDevice(deviceId: string, callback: AsyncCallback&lt;void&gt;): void

删除配对的远程设备。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                    |
| -------- | ------ | ---- | ------------------------------------- |
| deviceId | string | 是    | 表示要删除的远程设备的地址，例如："XX:XX:XX:XX:XX:XX"。 |
| callback | AsyncCallback&lt;void&gt; | 是    | 回调函数。当删除远程配对设备成功，err为undefined，否则为错误对象。   |

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
    connection.cancelPairedDevice('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.cancelPairedDevice

cancelPairedDevice(deviceId: string): Promise&lt;void&gt;

删除配对的远程设备。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                    |
| -------- | ------ | ---- | ------------------------------------- |
| deviceId | string | 是    | 表示要删除的远程设备的地址，例如："XX:XX:XX:XX:XX:XX"。 |

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
    connection.cancelPairedDevice('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.cancelPairingDevice

cancelPairingDevice(deviceId: string, callback: AsyncCallback&lt;void&gt;): void

删除正在配对中的远程设备。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                    |
| -------- | ------ | ---- | ------------------------------------- |
| deviceId | string | 是    | 表示要删除的远程设备的地址，例如："XX:XX:XX:XX:XX:XX"。 |
| callback | AsyncCallback&lt;void&gt; | 是    | 回调函数。当删除远程配对设备成功，err为undefined，否则为错误对象。   |

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
    connection.cancelPairingDevice('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.cancelPairingDevice

cancelPairingDevice(deviceId: string): Promise&lt;void&gt;

删除正在配对中的远程设备。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                    |
| -------- | ------ | ---- | ------------------------------------- |
| deviceId | string | 是    | 表示要删除的远程设备的地址，例如："XX:XX:XX:XX:XX:XX"。 |

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
    connection.cancelPairingDevice('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.getLocalProfileUuids

getLocalProfileUuids(callback: AsyncCallback&lt;Array&lt;ProfileUuids&gt;&gt;): void

获取本地设备的profile UUID。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                  |
| -------- | ------ | ---- | ----------------------------------- |
| callback | AsyncCallback&lt;Array&lt;[ProfileUuids](js-apis-bluetooth-constant-sys.md#profileuuids)&gt;&gt; | 是    | 回调函数。当获取UUID成功，err为undefined，否则为错误对象。 |

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
    connection.getLocalProfileUuids('XX:XX:XX:XX:XX:XX', (err: BusinessError, data: Array<connection.ProfileUuids>) => {
        console.info('getLocalProfileUuids, err: ' + JSON.stringify(err) + ', data: ' + JSON.stringify(data));
    });
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.getLocalProfileUuids

getLocalProfileUuids(): Promise&lt;Array&lt;ProfileUuids&gt;&gt;

获取本地设备的profile UUID。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**返回值：**

| 类型                  | 说明            |
| ------------------- | ------------- |
|   Promise&lt;Array&lt;[ProfileUuids](js-apis-bluetooth-constant-sys.md#profileuuids)&gt;&gt; | 返回promise对象。 |

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
    connection.getLocalProfileUuids('XX:XX:XX:XX:XX:XX').then(() => {
        console.info('getLocalProfileUuids');
    }, (err: BusinessError) => {
        console.error('getLocalProfileUuids: errCode' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
    });
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.getRemoteProfileUuids

getRemoteProfileUuids(deviceId: string, callback: AsyncCallback&lt;Array&lt;ProfileUuids&gt;&gt;): void

获取对端蓝牙设备支持的Profile UUID。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                  |
| -------- | ------ | ---- | ----------------------------------- |
| deviceId | string | 是    | 表示配对的远端设备地址，例如："XX:XX:XX:XX:XX:XX"。 |
| callback | AsyncCallback&lt;Array&lt;[ProfileUuids](js-apis-bluetooth-constant-sys.md#profileuuids)&gt;&gt; | 是    | 回调函数。当获取UUID成功，err为undefined，否则为错误对象。 |

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
    connection.getRemoteProfileUuids('XX:XX:XX:XX:XX:XX', (err: BusinessError, data: Array<connection.ProfileUuids>) => {
        console.info('getRemoteProfileUuids, err: ' + JSON.stringify(err) + ', data: ' + JSON.stringify(data));
    });
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}

```


## connection.getRemoteProfileUuids

getRemoteProfileUuids(deviceId: string): Promise&lt;Array&lt;ProfileUuids&gt;&gt;

获取对端蓝牙设备支持的Profile UUID。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                  |
| -------- | ------ | ---- | ----------------------------------- |
| deviceId | string | 是    | 表示配对的远端设备地址，例如："XX:XX:XX:XX:XX:XX"。 |

**返回值：**

| 类型                  | 说明            |
| ------------------- | ------------- |
|   Promise&lt;Array&lt;[ProfileUuids](js-apis-bluetooth-constant-sys.md#profileuuids)&gt;&gt; | 返回promise对象。 |

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
    connection.getRemoteProfileUuids('XX:XX:XX:XX:XX:XX').then(() => {
        console.info('getRemoteProfileUuids');
    }, (err: BusinessError) => {
        console.error('getRemoteProfileUuids: errCode' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
    });
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.connectAllowedProfiles<sup>11+</sup>

connectAllowedProfiles(deviceId: string, callback: AsyncCallback&lt;void&gt;): void

连接远端设备所有允许连接的profiles。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH 和 ohos.permission.MANAGE_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                  |
| -------- | ------ | ---- | ----------------------------------- |
| deviceId | string | 是    | 表示连接的远端设备地址，例如："XX:XX:XX:XX:XX:XX"。 |
| callback | AsyncCallback&lt;void&gt; | 是    | 以callback形式异步返回结果。当发起连接成功，err为undefined，否则为错误对象。   |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|201     | Permission denied.                       |
|202     | Non-system applications are not allowed to use system APIs.                       |
|401     | Invalid parameter.                       |
|801     | Capability not supported.                |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    connection.connectAllowedProfiles('68:13:24:79:4C:8C', (err: BusinessError) => {
        if (err) {
            console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
            return;
        }
        console.info('connectAllowedProfiles, err: ' + JSON.stringify(err));
    });
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.connectAllowedProfiles<sup>11+</sup>

connectAllowedProfiles(deviceId: string): Promise&lt;void&gt;

连接远端设备所有允许连接的profiles。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH 和 ohos.permission.MANAGE_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                  |
| -------- | ------ | ---- | ----------------------------------- |
| deviceId | string | 是    | 表示连接的远端设备地址，例如："XX:XX:XX:XX:XX:XX"。 |

**返回值：**

| 类型                                              | 说明                |
| ------------------------------------------------- | ------------------- |
| Promise&lt;void&gt; | 以Promise形式返回连接profiles的结果，返回true为成功，false为失败。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|201     | Permission denied.                       |
|202     | Non-system applications are not allowed to use system APIs.                       |
|401     | Invalid parameter.                       |
|801     | Capability not supported.                |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    connection.connectAllowedProfiles('68:13:24:79:4C:8C').then(() => {
        console.info('connectAllowedProfiles');
    }, (err: BusinessError) => {
        console.error('connectAllowedProfiles:errCode' + err.code + ', errMessage: ' + err.message);
    });
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.disconnectAllowedProfiles<sup>11+</sup>

disconnectAllowedProfiles(deviceId: string, callback: AsyncCallback&lt;void&gt;): void

断开远端设备所有连接的profiles。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH 和 ohos.permission.MANAGE_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                  |
| -------- | ------ | ---- | ----------------------------------- |
| deviceId | string | 是    | 表示断开的远端设备地址，例如："XX:XX:XX:XX:XX:XX"。 |
| callback | AsyncCallback&lt;void&gt; | 是    | 以callback形式异步返回结果。当发起断开成功，err为undefined，否则为错误对象。   |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|201     | Permission denied.                       |
|202     | Non-system applications are not allowed to use system APIs.                       |
|401     | Invalid parameter.                       |
|801     | Capability not supported.                |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    connection.disconnectAllowedProfiles('68:13:24:79:4C:8C', (err: BusinessError) => {
        if (err) {
            console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
            return;
        }
        console.info('disconnectAllowedProfiles, err: ' + JSON.stringify(err));
    });
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.disconnectAllowedProfiles<sup>11+</sup>

disconnectAllowedProfiles(deviceId: string): Promise&lt;void&gt;

断开远端设备所有连接的profiles。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH 和 ohos.permission.MANAGE_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                  |
| -------- | ------ | ---- | ----------------------------------- |
| deviceId | string | 是    | 表示断开的远端设备地址，例如："XX:XX:XX:XX:XX:XX"。 |

**返回值：**

| 类型                                              | 说明                |
| ------------------------------------------------- | ------------------- |
| Promise&lt;void&gt; | 以Promise形式返回断开profiles的结果，返回true为成功，false为失败。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|201     | Permission denied.                       |
|202     | Non-system applications are not allowed to use system APIs.                       |
|401     | Invalid parameter.                       |
|801     | Capability not supported.                |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    connection.disconnectAllowedProfiles('68:13:24:79:4C:8C').then(() => {
        console.info('disconnectAllowedProfiles');
    }, (err: BusinessError) => {
        console.error('disconnectAllowedProfiles:errCode' + err.code + ', errMessage: ' + err.message);
    });
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.getRemoteProductId<sup>11+</sup>

getRemoteProductId(deviceId: string): string

获取对端蓝牙设备的Product ID。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH 和 ohos.permission.MANAGE_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型     | 必填   | 说明                                |
| -------- | ------ | ---- | --------------------------------- |
| deviceId | string | 是    | 表示远程设备的地址，例如："XX:XX:XX:XX:XX:XX"。 |

**返回值：**

| 类型     | 说明            |
| ------ | ------------- |
| string | 以字符串格式返回设备Product ID。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import connection from '@ohos.bluetooth.connection';
try {
  let remoteDeviceProductId = connection.getRemoteProductId('XX:XX:XX:XX:XX:XX');
} catch (err) {
  console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


## PinRequiredParam

描述配对请求参数。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称       | 类型   | 可读   | 可写   | 说明          |
| -------- | ------ | ---- | ---- | ----------- |
| pinType | [PinType](#pintype) | 是    | 否    | 表示要配对的设备类型。<br/>此接口为系统接口。   |



## PinType

枚举，蓝牙配对类型。

**系统接口：** 此接口为系统接口。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称                               | 值    | 说明              |
| -------------------------------- | ------ | --------------- |
| PIN_TYPE_ENTER_PIN_CODE | 0 | 用户需要输入对端设备上显示的PIN码。<br/>此接口为系统接口。 |
| PIN_TYPE_ENTER_PASSKEY  | 1 | 用户需要输入对端设备上显示的PASSKEY。<br/>此接口为系统接口。  |
| PIN_TYPE_CONFIRM_PASSKEY  | 2 | 用户需要确认本地设备上显示的PASSKEY。<br/>此接口为系统接口。  |
| PIN_TYPE_NO_PASSKEY_CONSENT  | 3 | 无PASSKEY，用户需要接受或拒绝配对请求。<br/>此接口为系统接口。  |
| PIN_TYPE_NOTIFY_PASSKEY   | 4 | 本地设备显示PASSKEY，用户需要在对端设备上输入该PASSKEY。<br/>此接口为系统接口。  |
| PIN_TYPE_DISPLAY_PIN_CODE    | 5 | bluetooth 2.0设备，用户需要输入对端设备上显示的PIN码。<br/>此接口为系统接口。  |
| PIN_TYPE_OOB_CONSENT    | 6 | 用户需要接受或拒绝OOB配对请求。<br/>此接口为系统接口。  |
| PIN_TYPE_PIN_16_DIGITS    | 7 | 用户需要输入对端设备上显示的16位PIN码。<br/>此接口为系统接口。  |