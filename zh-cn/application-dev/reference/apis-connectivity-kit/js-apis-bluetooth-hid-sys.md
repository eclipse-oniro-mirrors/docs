# @ohos.bluetooth.hid (蓝牙hid模块)（系统接口）

hid模块提供了访问蓝牙hid相关功能的方法。

> **说明：**
>
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> 当前页面仅包含本模块的系统接口，其他公开接口参见[@ohos.bluetooth.hid (蓝牙hid模块)](js-apis-bluetooth-hid.md)


## 导入模块

```js
import hid from '@ohos.bluetooth.hid';
```

## HidHostProfile

使用HidHostProfile方法之前需要创建该类的实例进行操作，通过createHidHostProfile()方法构造此实例。

### connect

connect(deviceId: string): void

连接设备的HidHost服务。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH 和 ohos.permission.MANAGE_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名    | 类型     | 必填   | 说明      |
| ------ | ------ | ---- | ------- |
| deviceId | string | 是    | 远端设备地址。 |

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
try {
    let hidHostProfile = hid.createHidHostProfile();
    hidHostProfile.connect('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


### disconnect

disconnect(deviceId: string): void

断开连接设备的HidHost服务。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH 和 ohos.permission.MANAGE_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名    | 类型     | 必填   | 说明      |
| ------ | ------ | ---- | ------- |
| deviceId | string | 是    | 远端设备地址。 |

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
try {
    let hidHostProfile = hid.createHidHostProfile();
    hidHostProfile.disconnect('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```