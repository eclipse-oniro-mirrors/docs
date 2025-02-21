# @ohos.enterprise.systemManager (System Management) (System API)

The **systemManager** module provides system management capabilities.

> **NOTE**
> 
> - The initial APIs of this module are supported since API version 11. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
> - The APIs of this module can be used only in the stage model.
>
> - The APIs provided by this module can be called only by a [device administrator application](enterpriseDeviceManagement-overview.md#basic-concepts) that is [enabled](js-apis-enterprise-adminManager-sys.md#adminmanagerenableadmin).
> 
> - The APIs provided by this module are system APIs.

## Modules to Import

```ts
import systemManager from '@ohos.enterprise.systemManager';
```

## systemManager.setNTPServer

setNTPServer(admin: Want, server: string): void

Sets the NTP server information through the specified device administrator application.

**Required permissions**: ohos.permission.ENTERPRISE_MANAGE_SYSTEM

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | Yes   | Device administrator application.|
| server | string | Yes| NTP server addresses separated by a comma (,). For example, **ntpserver1.com,ntpserver2.com**.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                                     |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | the application is not an administrator of the device.                       |
| 9200002 | the administrator application does not have permission to manage the device. |

**Example**

```ts
import systemManager from '@ohos.enterprise.systemManager';
import Want from '@ohos.app.ability.Want';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};
let server: string = "ntpserver.com";
try {
  systemManager.setNTPServer(wantTemp, server);
  console.info('Succeeded in setting NTPserver');
} catch (err) {
  console.error(`Failed to set usb policy. Code is ${err.code}, message is ${err.message}`);
}
```

## systemManager.getNTPServer

getNTPServer(admin: Want): string

Obtains the NTP server information through the specified device administrator application.

**Required permissions**: ohos.permission.ENTERPRISE_MANAGE_SYSTEM

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager



**Parameters**

| Name| Type                               | Mandatory| Description          |
| ------ | ----------------------------------- | ---- | -------------- |
| admin  | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | Yes  | Device administrator application.|

**Return value**

| Type  | Description                           |
| ------ | ------------------------------- |
| string | NTP server information obtained.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 9200001  | the application is not an administrator of the device.       |
| 9200002  | the administrator application does not have permission to manage the device. |

**Example**

```ts
import systemManager from '@ohos.enterprise.systemManager';
import Want from '@ohos.app.ability.Want';
import { BusinessError } from '@ohos.base';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};
try {
  systemManager.getNTPServer(wantTemp);
  console.info('Succeeded in getting NTP server');
} catch (err) {
  console.error(`Failed to set usb policy. Code is ${err.code}, message is ${err.message}`);
}
```
## SystemUpdateInfo<sup>11+</sup>

Represents information about the system version to update.

 **System capability**: SystemCapability.Customization.EnterpriseDeviceManager

 **System API**: This is a system API.

| Name               | Type    | Mandatory | Description           |
| ----------------- | ------ | --- | ------------- |
| versionName       | string | Yes  | System version to update.  |
| firstReceivedTime | number | Yes  | Time when the system update package is received for the first time.|
| packageType       | string | Yes  | Type of the system update package to update. |
