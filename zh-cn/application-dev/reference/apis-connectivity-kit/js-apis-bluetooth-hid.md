# @ohos.bluetooth.hid (蓝牙hid模块)

hid模块提供了访问蓝牙hid相关功能的方法。

> **说明：**
>
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。



## 导入模块

```js
import { hid } from '@kit.ConnectivityKit';
```


## BaseProfile

type BaseProfile = baseProfile.BaseProfile

基础Profile接口定义。

**系统能力**：SystemCapability.Communication.Bluetooth.Core

| 类型                            | 说明         |
| ----------------------------- | ---------- |
| [baseProfile.BaseProfile](js-apis-bluetooth-baseProfile.md#ohosbluetoothbaseprofile-蓝牙baseprofile模块) | 基础Profile接口定义。 |


## hid.createHidHostProfile

createHidHostProfile(): HidHostProfile

创建hid profile实例。

**系统能力**：SystemCapability.Communication.Bluetooth.Core

**返回值：**

| 类型                            | 说明         |
| ----------------------------- | ---------- |
| HidHostProfile | 返回该profile的实例。 |

**错误码**：

以下错误码的详细介绍请参见[通用错误码说明文档](../errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|401 | Invalid parameter. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3. Parameter verification failed.                 |
|801 | Capability not supported.          |


**示例：**

```js
import { AsyncCallback, BusinessError } from '@kit.BasicServicesKit';
try {
    let hidHostProfile = hid.createHidHostProfile();
    console.info('hidHost success');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```

