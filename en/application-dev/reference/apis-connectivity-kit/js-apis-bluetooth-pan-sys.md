# @ohos.bluetooth.pan (Bluetooth PAN Module) (System API)

The **pan** module provides APIs for accessing the Bluetooth personal area network (PAN).

> **NOTE**
>
> - The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> - This topic describes only the system APIs provided by the module. For details about its public APIs, see [@ohos.bluetooth.pan (Bluetooth PAN Module)](js-apis-bluetooth-pan.md).


## Modules to Import

```js
import pan from '@ohos.bluetooth.pan';
```

## PanProfile

Before using any API of **PanProfile**, you need to create an instance of this class by using **createPanProfile()**.

### disconnect

disconnect(deviceId: string): void

Disconnects from the PAN service of a device.

**System API**: This is a system API.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name   | Type    | Mandatory  | Description     |
| ------ | ------ | ---- | ------- |
| deviceId | string | Yes   | Address of the remote device.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900004 | Profile is not supported.                |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
try {
    let panProfile: pan.PanProfile = pan.createPanProfile();
    panProfile.disconnect('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


### setTethering

setTethering(enable: boolean): void

Sets Bluetooth tethering, which shares a mobile connection.

**System API**: This is a system API.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH and ohos.permission.MANAGE_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name   | Type    | Mandatory  | Description     |
| ------ | ------ | ---- | ------- |
| value | boolean | Yes   | Whether to set tethering over a Bluetooth PAN.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900004 | Profile is not supported.                |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
try {
    let panProfile: pan.PanProfile = pan.createPanProfile();
    panProfile.setTethering(false);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


### isTetheringOn

isTetheringOn(): boolean

Checks whether Bluetooth tethering is activated.

**System API**: This is a system API.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Return value**

| Type     | Description                 |
| --------------------- | --------------------------------- |
| boolean | Returns **true** if tethering is available over a Bluetooth PAN; returns **false** otherwise.|

**Example**

```js
import { BusinessError } from '@ohos.base';
try {
    let panProfile: pan.PanProfile = pan.createPanProfile();
    panProfile.isTetheringOn();
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```
