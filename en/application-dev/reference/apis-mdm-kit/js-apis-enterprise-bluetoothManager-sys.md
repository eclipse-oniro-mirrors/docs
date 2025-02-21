# @ohos.enterprise.bluetoothManager (Bluetooth Management) (System API)

The **bluetoothManager** module provides Bluetooth management capabilities, including setting and obtaining Bluetooth information.

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
import bluetoothManager from '@ohos.enterprise.bluetoothManager';
```

## bluetoothManager.getBluetoothInfo

getBluetoothInfo(admin: Want): BluetoothInfo;

Obtains device Bluetooth information through the specified device administrator application. This API returns the result synchronously. If the operation is successful, the Bluetooth information obtained is returned. If the operation fails, an exception is thrown.

**Required permissions**: ohos.permission.ENTERPRISE_MANAGE_BLUETOOTH

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager



**Parameters**

| Name     | Type                                      | Mandatory  | Description                      |
| -------- | ---------------------------------------- | ---- | ------------------------------- |
| admin    | [Want](../apis-ability-kit/js-apis-app-ability-want.md)     | Yes   | Device administrator application.                 |

**Return value**

| Type            | Description                                                  |
| ---------------- | ------------------------------------------------------ |
| [BluetoothInfo](#bluetoothinfo)| Bluetooth information, including the Bluetooth name, state, and profile connection state.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                                      |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | the application is not an administrator of the device.                        |
| 9200002 | the administrator application does not have permission to manage the device. |

**Example**

```ts
import Want from '@ohos.app.ability.Want';
import bluetoothManager from '@ohos.enterprise.bluetoothManager';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};

try {
    let result: bluetoothManager.BluetoothInfo = bluetoothManager.getBluetoothInfo(wantTemp);
    console.info(`Succeeded in getting bluetooth info. `);
} catch(err) {
    console.error(`Failed to get bluetooth info. Code: ${err.code}, message: ${err.message}`);
}
```

## BluetoothInfo

Represents the device Bluetooth information.

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager



**Model restriction**: This API can be used only in the stage model.

| Name        | Type    | Mandatory| Description                           |
| ----------- | --------| ---- | ------------------------------- |
| name        | string   | Yes  | Bluetooth name of the device.|
| state |[access.BluetoothState](../apis-connectivity-kit/js-apis-bluetooth-access.md#bluetoothstate)  | Yes  | Bluetooth state of the device.|
| connectionState | [constant.ProfileConnectionState](../apis-connectivity-kit/js-apis-bluetooth-constant.md#profileconnectionstate)  | Yes  | Bluetooth profile connection state of the device.|

## bluetoothManager.isBluetoothDisabled

isBluetoothDisabled(admin: Want): boolean

Checks whether Bluetooth is disabled. This API returns the result synchronously.

**Required permissions**: ohos.permission.ENTERPRISE_MANAGE_BLUETOOTH

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

 

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | Yes   | Device administrator application.|

**Return value**

| Type                  | Description                     |
| :-------------------- | ------------------------- |
| boolean | Returns **true** if Bluetooth is disabled; returns **false** otherwise.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                                    |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | the application is not an administrator of the device.                        |
| 9200002 | the administrator application does not have permission to manage the device. |

**Example**

```ts
import Want from '@ohos.app.ability.Want';
import bluetoothManager from '@ohos.enterprise.bluetoothManager';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};

try {
  let isDisabled: boolean = bluetoothManager.isBluetoothDisabled(wantTemp);
  console.info(`Succeeded in query the bluetooth is disabled or not, isDisabled : ${isDisabled}`);
} catch(err) {
  console.error(`Failed to query the bluetooth is disabled or not. Code: ${err.code}, message: ${err.message}`);
};
```

## bluetoothManager.setBluetoothDisabled

setBluetoothDisabled(admin: Want, disabled: boolean): void

Disables Bluetooth. This API returns the result synchronously.

**Required permissions**: ohos.permission.ENTERPRISE_MANAGE_BLUETOOTH

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

 

**Parameters**

| Name    | Type                               | Mandatory| Description                                     |
| ---------- | ----------------------------------- | ---- | ----------------------------------------- |
| admin      | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | Yes  | Device administrator application.                           |
| disabled   | boolean                             | Yes  | Whether to disable Bluetooth. The value **true** means to disable Bluetooth; **false** means the opposite.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 9200001  | the application is not an administrator of the device.       |
| 9200002  | the administrator application does not have permission to manage the device. |

**Example**

```ts
import Want from '@ohos.app.ability.Want';
import bluetoothManager from '@ohos.enterprise.bluetoothManager';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};

try {
  bluetoothManager.setBluetoothDisabled(wantTemp, true);
  console.info('Succeeded in set the bluetooth disabled');
} catch(err) {
  console.error(`Failed to set the bluetooth disabled. Code: ${err.code}, message: ${err.message}`);
};
```
