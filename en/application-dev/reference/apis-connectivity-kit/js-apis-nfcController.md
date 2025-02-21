# @ohos.nfc.controller (Standard NFC)

The **nfcController** module provides APIs for opening and closing Near-Field Communication (NFC) and reading the NFC state.

> **NOTE**
>
> The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## **Modules to Import**

```js
import controller from '@ohos.nfc.controller';
```

## NfcState

Enumerates the NFC states.

**System capability**: SystemCapability.Communication.NFC.Core

| Name| Value| Description|
| -------- | -------- | -------- |
| STATE_OFF | 1 | NFC is closed (OFF).|
| STATE_TURNING_ON | 2 | NFC is turning on.|
| STATE_ON | 3      | NFC is open (ON).|
| STATE_TURNING_OFF | 4      | NFC is turning off.|

## controller.isNfcAvailable<sup>(deprecated)</sup>

isNfcAvailable(): boolean

Checks whether the device supports NFC.

> **NOTE**
> This API is supported since API version 7 and deprecated since API version 9. Use [canIUse("SystemCapability.Communication.NFC.Core")](../common/init.md#caniuse) instead.

**System capability**: SystemCapability.Communication.NFC.Core

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| boolean | Returns **true** if the device supports NFC; returns **false** otherwise.|


## controller.openNfc<sup>(deprecated)</sup>

openNfc(): boolean

Opens NFC.

> **NOTE**
> This API is supported since API version 7 and deprecated since API version 9. Use [enableNfc](#controllerenablenfc9) instead.

**Required permissions**: ohos.permission.MANAGE_SECURE_SETTINGS (available only for system applications)

**System capability**: SystemCapability.Communication.NFC.Core

**Return value**

| **Type**| **Description**|
| -------- | -------- |
| boolean | Returns **true** if the operation is successful; returns **false** otherwise.|

## controller.enableNfc<sup>9+</sup>

enableNfc(): void

Enables NFC.

**Required permissions**: ohos.permission.MANAGE_SECURE_SETTINGS (available only for system applications)

**System capability**: SystemCapability.Communication.NFC.Core

**Error codes**

For details about the error codes, see [NFC Error Codes](errorcode-nfc.md).

| ID| Error Message|
| ------- | -------|
| 3100101 | NFC state is abnormal in service. |

## controller.closeNfc<sup>(deprecated)</sup>

closeNfc(): boolean

Closes NFC.

> **NOTE**
> This API is supported since API version 7 and deprecated since API version 9. Use [disableNfc](#controllerdisablenfc9) instead.

**Required permissions**: ohos.permission.MANAGE_SECURE_SETTINGS (available only for system applications)

**System capability**: SystemCapability.Communication.NFC.Core

**Return value**

| **Type**| **Description**                                   |
| -------- | ------------------------------------------- |
| boolean  | Returns **true** if the operation is successful; returns **false** otherwise.|

## controller.disableNfc<sup>9+</sup>

disableNfc(): void

Disables NFC.

**Required permissions**: ohos.permission.MANAGE_SECURE_SETTINGS (available only for system applications)

**System capability**: SystemCapability.Communication.NFC.Core

**Error codes**

For details about the error codes, see [NFC Error Codes](errorcode-nfc.md).

| ID| Error Message|
| ------- | -------|
| 3100101 | NFC state is abnormal in service. |

## controller.isNfcOpen

isNfcOpen(): boolean

Checks whether NFC is open.

**System capability**: SystemCapability.Communication.NFC.Core

**Return value**

| **Type**| **Description**                           |
| -------- | ----------------------------------- |
| boolean  | Returns **true** if NFC is open; returns **false** otherwise.|

## controller.getNfcState

getNfcState(): [NfcState](#nfcstate)

Obtains the NFC state.

**System capability**: SystemCapability.Communication.NFC.Core

**Return value**

| **Type**| **Description**              |
| -------- | ---------------------- |
| [NfcState](#nfcstate) | NFC state obtained. For details, see [NfcState](#nfcstate).|

## controller.on('nfcStateChange')

on(type: "nfcStateChange", callback: Callback&lt;[NfcState](#nfcstate)&gt;): void

Subscribes to NFC state changes. A callback will be invoked to return the NFC state when the NFC state changes.

**System capability**: SystemCapability.Communication.NFC.Core

**Parameters**
  
| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type to subscribe to. The value is **nfcStateChange**.|
| callback | Callback&lt;[NfcState](#nfcstate)&gt; | Yes| Callback used to return the NFC state.|

## controller.off('nfcStateChange')

off(type: "nfcStateChange", callback?: Callback&lt;[NfcState](#nfcstate)&gt;): void

Unsubscribes from the NFC state changes. The subscriber will not receive NFC state change notifications.

**System capability**: SystemCapability.Communication.NFC.Core

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type. The value is **nfcStateChange**.|
| callback | Callback&lt;[NfcState](#nfcstate)&gt; | No| Callback for the NFC state changes. This parameter can be left blank. If this parameter is not specified, all callbacks associated with the specified event will be unregistered.|
  
**Example**

```js
import controller from '@ohos.nfc.controller';

// Register a callback to receive the NFC state change notification.
controller.on("nfcStateChange", (nfcState : number)=> {
  console.log("controller on callback nfcState: " + nfcState);
});

// Open NFC. The caller must have the ohos.permission.MANAGE_SECURE_SETTINGS permission. This permission is available only for system applications.
if (!controller.isNfcOpen()) {
  let ret = controller.openNfc();
  console.log("controller openNfc ret: " + ret);
}

// Use 'enableNfc' to enable NFC from API version 9.
try {
  controller.enableNfc();
  console.log("controller enableNfc success");
} catch (busiError) {
  console.error("controller enableNfc busiError: " + busiError);
}

// Close NFC. The caller must have the ohos.permission.MANAGE_SECURE_SETTINGS permission. This permission is available only for applications.
if (controller.isNfcOpen()) {
  let ret = controller.closeNfc();
  console.log("controller closeNfc ret: " + ret);
}

// Use 'disableNfc' to disable NFC from API version 9.
try {
  controller.disableNfc();
  console.log("controller disableNfc success");
} catch (busiError) {
  console.error("controller disableNfc busiError: " + busiError);
}

// Unregister the callback.
controller.off("nfcStateChange");
```
