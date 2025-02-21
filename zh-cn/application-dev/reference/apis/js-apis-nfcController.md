# @ohos.nfc.controller (标准NFC)

本模块主要用于管理NFC状态，包括打开和关闭NFC，读取NFC的状态等。

> **说明：**
>
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## **导入模块**

```js
import controller from '@ohos.nfc.controller';
```

## NfcState

定义不同的NFC状态值。

**系统能力：** SystemCapability.Communication.NFC.Core

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| STATE_OFF | 1 | NFC已关闭状态。 |
| STATE_TURNING_ON | 2 | NFC正在打开状态。 |
| STATE_ON | 3      | NFC已打开状态。 |
| STATE_TURNING_OFF | 4      | NFC正在关闭状态。 |

## controller.isNfcAvailable

isNfcAvailable(): boolean

查询设备是否有NFC能力。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用canIUse("SystemCapability.Communication.NFC.Core")替代。

**系统能力：** SystemCapability.Communication.NFC.Core

**返回值：**

| **类型** | **说明** |
| -------- | -------- |
| boolean | true: 设备具备NFC能力，&nbsp;false: 设备不具备NFC能力。 |


## controller.openNfc

openNfc(): boolean

打开NFC开关。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用[enableNfc](#controllerenablenfc9)替代。

**需要权限：** ohos.permission.MANAGE_SECURE_SETTINGS

**系统能力：** SystemCapability.Communication.NFC.Core

**返回值：**

| **类型** | **说明** |
| -------- | -------- |
| boolean | true: 打开NFC成功，&nbsp;false: 打开NFC失败。 |

## controller.enableNfc<sup>9+</sup>

enableNfc(): void

打开NFC开关。

**需要权限：** ohos.permission.MANAGE_SECURE_SETTINGS

**系统能力：** SystemCapability.Communication.NFC.Core

**错误码：**

以下错误码的详细介绍请参见[NFC错误码](../errorcodes/errorcode-nfc.md)。

| 错误码ID | 错误信息|
| ------- | -------|
| 3100101 | NFC state is abnormal in service. |

## controller.closeNfc

closeNfc(): boolean

关闭NFC开关。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用[disableNfc](#controllerdisablenfc9)替代。

**需要权限：** ohos.permission.MANAGE_SECURE_SETTINGS

**系统能力：** SystemCapability.Communication.NFC.Core

**返回值：**

| **类型** | **说明**                                    |
| -------- | ------------------------------------------- |
| boolean  | true: 关闭NFC成功，&nbsp;false: 关闭NFC失败。 |

## controller.disableNfc<sup>9+</sup>

disableNfc(): void

关闭NFC开关。

**需要权限：** ohos.permission.MANAGE_SECURE_SETTINGS

**系统能力：** SystemCapability.Communication.NFC.Core

**错误码：**

以下错误码的详细介绍请参见[NFC错误码](../errorcodes/errorcode-nfc.md)。

| 错误码ID | 错误信息|
| ------- | -------|
| 3100101 | NFC state is abnormal in service. |

## controller.isNfcOpen

isNfcOpen(): boolean

查询NFC是否打开。

**系统能力：** SystemCapability.Communication.NFC.Core

**返回值：**

| **类型** | **说明**                            |
| -------- | ----------------------------------- |
| boolean  | true: NFC是打开的，&nbsp;false: NFC是关闭的。 |

## controller.getNfcState

getNfcState(): [NfcState](#nfcstate)

查询NFC状态。

**系统能力：** SystemCapability.Communication.NFC.Core

**返回值：**

| **类型** | **说明**               |
| -------- | ---------------------- |
| [NfcState](#nfcstate) | NFC状态值，详细请见[NfcState](#nfcstate)枚举值。 |

## controller.on('nfcStateChange')

on(type: "nfcStateChange", callback: Callback&lt;[NfcState](#nfcstate)&gt;): void

注册NFC开关状态事件，通过Callback方式获取NFC状态的变化通知。

**系统能力：** SystemCapability.Communication.NFC.Core

**参数**
  
| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"nfcStateChange"字符串。 |
| callback | Callback&lt;[NfcState](#nfcstate)&gt; | 是 | NFC状态改变通知的回调函数。 |

## controller.off('nfcStateChange')

off(type: "nfcStateChange", callback?: Callback&lt;[NfcState](#nfcstate)&gt;): void

取消NFC开关状态事件的注册，取消后NFC状态变化时，就不会再收到Callback的通知。

**系统能力：** SystemCapability.Communication.NFC.Core

**参数**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"nfcStateChange"字符串。 |
| callback | Callback&lt;[NfcState](#nfcstate)&gt; | 否 | NFC状态改变回调函数，可以空缺不填。如果callback不填，将取消注册该事件关联的所有回调函数 |
  
**示例**

```js
import controller from '@ohos.nfc.controller';

// register callback to receive the nfc state changed notification
controller.on("nfcStateChange", (err, nfcState)=> {
  if (err) {
      console.log("controller on callback err: " + err);
  } else {
      console.log("controller on callback nfcState: " + nfcState);
  }
});

// open nfc, require permission: ohos.permission.MANAGE_SECURE_SETTINGS
if (!controller.isNfcOpen()) {
  var ret = controller.openNfc();
  console.log("controller openNfc ret: " + ret);
}

// from api9, use 'enableNfc' to open nfc.
try {
    controller.enableNfc();
    console.log("controller enableNfc success");
} catch (busiError) {
    console.log("controller enableNfc busiError: " + busiError);
}

// close nfc, require permission: ohos.permission.MANAGE_SECURE_SETTINGS
if (controller.isNfcOpen()) {
  var ret = controller.closeNfc();
  console.log("controller closeNfc ret: " + ret);
}

// from api9, use 'disableNfc' to close nfc.
try {
    controller.disableNfc();
    console.log("controller disableNfc success");
} catch (busiError) {
    console.log("controller disableNfc busiError: " + busiError);
}

// unregister callback
controller.off("nfcStateChange");
```
