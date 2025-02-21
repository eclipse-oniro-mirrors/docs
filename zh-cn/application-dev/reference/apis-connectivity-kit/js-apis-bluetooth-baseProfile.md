# @ohos.bluetooth.baseProfile (蓝牙baseProfile模块)

baseProfile模块提供了基础的profile方法。

> **说明：**
>
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。



## 导入模块

```js
import baseProfile from '@ohos.bluetooth.baseProfile';
```


## StateChangeParam

描述profile状态改变参数。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称     | 类型                           | 可读 | 可写 | 说明                            |
| -------- | ----------------------------- | ---- | ---- | ------------------------------- |
| deviceId | string                        | 是   | 否   | 表示蓝牙设备地址。   |
| state    | ProfileConnectionState        | 是   | 否   | 表示蓝牙设备的profile连接状态。 |


## baseProfile.getConnectedDevices

getConnectedDevices(): Array&lt;string&gt;

获取已连接设备列表。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**返回值：**

| 类型                  | 说明                  |
| ------------------- | ------------------- |
| Array&lt;string&gt; | 返回当前已连接设备的地址。基于信息安全考虑，此处获取的设备地址为随机MAC地址。配对成功后，该地址不会变更；已配对设备取消配对后重新扫描或蓝牙服务下电时，该随机地址会变更。 |

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
import a2dp from '@ohos.bluetooth.a2dp';
try {
    let a2dpSrc = a2dp.createA2dpSrcProfile();
    let retArray = a2dpSrc.getConnectedDevices();
} catch (err) {
    console.error("errCode:" + (err as BusinessError).code + ",errMessage:" + (err as BusinessError).message);
}
```


## baseProfile.getConnectionState

getConnectionState(deviceId: string): ProfileConnectionState

获取设备profile的连接状态。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名    | 类型     | 必填   | 说明      |
| ------ | ------ | ---- | ------- |
| deviceId | string | 是    | 远端设备地址。 |

**返回值：**

| 类型                                              | 说明                    |
| ------------------------------------------------- | ----------------------- |
| [ProfileConnectionState](js-apis-bluetooth-constant.md#profileconnectionstate) | 返回profile的连接状态。 |

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
import a2dp from '@ohos.bluetooth.a2dp';
try {
    let a2dpSrc = a2dp.createA2dpSrcProfile();
    let ret = a2dpSrc.getConnectionState('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## baseProfile.on('connectionStateChange')

on(type: 'connectionStateChange', callback: Callback&lt;StateChangeParam&gt;): void

订阅连接状态变化事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                       |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | 是    | 填写"connectionStateChange"字符串，表示连接状态变化事件。 |
| callback | Callback&lt;[StateChangeParam](#statechangeparam)&gt; | 是    | 表示回调函数的入参。                               |

**示例：**

```js
import { BusinessError } from '@ohos.base';
import a2dp from '@ohos.bluetooth.a2dp';
function onReceiveEvent(data: baseProfile.StateChangeParam) {
    console.info('a2dp state = '+ JSON.stringify(data));
}
try {
    let a2dpSrc = a2dp.createA2dpSrcProfile();
    a2dpSrc.on('connectionStateChange', onReceiveEvent);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## baseProfile.off('connectionStateChange')

off(type: 'connectionStateChange', callback?: Callback&lt;[StateChangeParam](#statechangeparam)&gt;): void

取消订阅连接状态变化事件。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                       |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | 是    | 填写"connectionStateChange"字符串，表示连接状态变化事件。 |
| callback | Callback&lt;[StateChangeParam](#statechangeparam)&gt; | 否    | 表示回调函数的入参。                               |

**示例：**

```js
import { BusinessError } from '@ohos.base';
import a2dp from '@ohos.bluetooth.a2dp';
function onReceiveEvent(data: baseProfile.StateChangeParam) {
    console.info('a2dp state = '+ JSON.stringify(data));
}
try {
    let a2dpSrc = a2dp.createA2dpSrcProfile();
    a2dpSrc.on('connectionStateChange', onReceiveEvent);
    a2dpSrc.off('connectionStateChange', onReceiveEvent);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```