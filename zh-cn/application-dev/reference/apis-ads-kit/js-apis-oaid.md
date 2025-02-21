# @ohos.identifier.oaid (广告标识服务)


本模块提供开放匿名设备标识符（Open Anonymous Device Identifier, OAID，以下简称OAID）的获取和重置能力。


> **说明：**
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> 使用获取开放匿名设备标识符接口，需[向用户申请授权](../../security/AccessToken/request-user-authorization.md)：ohos.permission.APP_TRACKING_CONSENT


## 导入模块

```
import identifier from '@ohos.identifier.oaid';
```


## identifier.getOAID

getOAID(): Promise&lt;string&gt;

获取开放匿名设备标识符（Open Anonymous Device Identifier, OAID），使用Promise异步返回。

**需要权限：** ohos.permission.APP_TRACKING_CONSENT

**系统能力：** SystemCapability.Advertising.OAID

**返回值：**

| 类型 | 说明 | 
| -------- | -------- |
| Promise&lt;string&gt; | Promise对象。返回开放匿名设备标识符（Open&nbsp;Anonymous&nbsp;Device&nbsp;Identifier,&nbsp;OAID）。<br/>1.如应用已配置ohos.permission.APP_TRACKING_CONSENT权限且弹框后用户手动授权，则返回OAID。<br/>2.如应用已配置ohos.permission.APP_TRACKING_CONSENT权限，但弹框后用户未手动授权，则返回00000000-0000-0000-0000-000000000000。<br/>3.如应用未配置ohos.permission.APP_TRACKING_CONSENT权限，则返回00000000-0000-0000-0000-000000000000。| 

**错误码：**

以下错误码的详细介绍请参见[广告标识服务错误码参考](errorcode-oaid.md)。

| 错误码ID | 错误信息 | 
| -------- | -------- |
| 17300001 | System&nbsp;internal&nbsp;error. | 

**示例：**
```
import identifier from '@ohos.identifier.oaid';
import hilog from '@ohos.hilog';
import { BusinessError } from '@ohos.base';

try {
  identifier.getOAID().then((data) => {
    const oaid: string = data;
    hilog.info(0x0000, 'testTag', '%{public}s', `get oaid by promise success, oaid: ${oaid}`);
  }).catch((err: BusinessError) => {
    hilog.error(0x0000, 'testTag', '%{public}s',
      `get oaid by promise failed, code: ${err.code}, message: ${err.message}`);
  })
} catch (err) {
  hilog.error(0x0000, 'testTag', '%{public}s', `get oaid by promise catch error: ${err.code} ${err.message}`);
}
```


## identifier.getOAID

getOAID(callback: AsyncCallback&lt;string&gt;): void

获取开放匿名设备标识符（Open Anonymous Device Identifier, OAID），使用callback异步回调。

**需要权限：** ohos.permission.APP_TRACKING_CONSENT

**系统能力：** SystemCapability.Advertising.OAID

**参数：**


| **参数**名 | **类型** | 必填 | 说明 | 
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;string&gt; | 是 | 异步获取开放匿名设备标识符（Open&nbsp;Anonymous&nbsp;Device&nbsp;Identifier,&nbsp;OAID）的回调。<br/>1.如应用已配置ohos.permission.APP_TRACKING_CONSENT权限且弹框后用户手动授权，则返回OAID。<br/>2.如应用已配置ohos.permission.APP_TRACKING_CONSENT权限，但弹框后用户未手动授权，则返回00000000-0000-0000-0000-000000000000。<br/>3.如应用未配置ohos.permission.APP_TRACKING_CONSENT权限，则返回00000000-0000-0000-0000-000000000000。| 


**错误码：**


以下错误码的详细介绍请参见[广告标识服务错误码参考](errorcode-oaid.md)。


| 错误码ID | 错误信息 | 
| -------- | -------- |
| 17300001 | System&nbsp;internal&nbsp;error. | 


**示例：**
```
import identifier from '@ohos.identifier.oaid';
import hilog from '@ohos.hilog'; 
import { BusinessError } from '@ohos.base';
 
try {
  identifier.getOAID((err: BusinessError, data: string) => {
    if (err.code) {
      hilog.error(0x0000, 'testTag', '%{public}s', `get oaid by callback failed, error: ${err.code} ${err.message}`);
    } else {
      const oaid: string = data;
      hilog.info(0x0000, 'testTag', '%{public}s', 'get oaid by callback success');
    }
   });
} catch (err) {
  hilog.error(0x0000, 'testTag', '%{public}s', `get oaid by callback catch error: ${err.code} ${err.message}`);
}
```
