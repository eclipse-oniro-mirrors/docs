# @ohos.bluetooth.connection (Bluetooth Connection Module)

The **connection** module provides APIs for operating and managing Bluetooth.

> **NOTE**
>
> The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version.



## Modules to Import

```js
import connection from '@ohos.bluetooth.connection';
```


## connection.pairDevice

pairDevice(deviceId: string, callback: AsyncCallback&lt;void&gt;): void

Pairs a Bluetooth device. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type    | Mandatory  | Description                                 |
| -------- | ------ | ---- | ----------------------------------- |
| deviceId | string | Yes   | Address of the device to pair, for example, XX:XX:XX:XX:XX:XX.|
| callback | AsyncCallback&lt;void&gt;  | Yes   | Callback used to return the result. If the pairing is successful, **err** is **undefined**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
try {
    // The address can be scanned.
    connection.pairDevice('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.pairDevice

pairDevice(deviceId: string): Promise&lt;void&gt;

Pairs a Bluetooth device. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type    | Mandatory  | Description                                 |
| -------- | ------ | ---- | ----------------------------------- |
| deviceId | string | Yes   | Address of the device to pair, for example, XX:XX:XX:XX:XX:XX.|

**Return value**

| Type                 | Description           |
| ------------------- | ------------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
try {
    // The address can be scanned.
    connection.pairDevice('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.getRemoteDeviceName

getRemoteDeviceName(deviceId: string): string

Obtains the name of a remote Bluetooth device.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type    | Mandatory  | Description                               |
| -------- | ------ | ---- | --------------------------------- |
| deviceId | string | Yes   | Address of the remote device, for example, XX:XX:XX:XX:XX:XX.|

**Return value**

| Type    | Description           |
| ------ | ------------- |
| string | Device name (a string) obtained.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
try {
    let remoteDeviceName: string = connection.getRemoteDeviceName('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.getRemoteDeviceClass

getRemoteDeviceClass(deviceId: string): DeviceClass

Obtains the class of a remote Bluetooth device.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type    | Mandatory  | Description                               |
| -------- | ------ | ---- | --------------------------------- |
| deviceId | string | Yes   | Address of the remote device, for example, XX:XX:XX:XX:XX:XX.|

**Return value**

| Type                         | Description      |
| --------------------------- | -------- |
| [DeviceClass](#deviceclass) | Class of the remote device obtained.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
try {
    let remoteDeviceClass: connection.DeviceClass = connection.getRemoteDeviceClass('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.getLocalName

getLocalName(): string

Obtains the name of the local Bluetooth device.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Return value**

| Type    | Description       |
| ------ | --------- |
| string | Name of the local Bluetooth device obtained.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
try {
    let localName: string = connection.getLocalName();
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.getPairedDevices

getPairedDevices(): Array&lt;string&gt;

Obtains the paired devices.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Return value**

| Type                 | Description           |
| ------------------- | ------------- |
| Array&lt;string&gt; | Addresses of the paired Bluetooth devices. For security purposes, the device addresses obtained are random MAC addresses. The random MAC address remains unchanged after a device is paired successfully. It changes when the paired device is unpaired and scanned again or the Bluetooth service is turned off.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
try {
    let devices: Array<string> = connection.getPairedDevices();
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.getPairState<sup>11+</sup>

getPairState(deviceId: string): BondState

Obtains the Bluetooth pairing state.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type    | Mandatory  | Description                               |
| -------- | ------ | ---- | --------------------------------- |
| deviceId | string | Yes   | Address of the remote device, for example, XX:XX:XX:XX:XX:XX.|

**Return value**

| Type                         | Description      |
| --------------------------- | -------- |
| [BondState](#bondstate) | Bluetooth pairing state obtained.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
try {
    let res: connection.BondState = connection.getPairState("XX:XX:XX:XX:XX:XX");
    console.log('getPairState: ' + res);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.getProfileConnectionState

getProfileConnectionState(profileId?: ProfileId): ProfileConnectionState

Obtains the connection state of a Bluetooth profile. The **ProfileId** parameter is optional. If **ProfileId** is specified, the connection state of the specified profile is returned. If no **ProfileId** is specified, [STATE_CONNECTED](js-apis-bluetooth-constant.md#profileconnectionstate) is returned by any connected profile. If no profile is connected, [STATE_DISCONNECTED](js-apis-bluetooth-constant.md#profileconnectionstate) is returned.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name      | Type       | Mandatory  | Description                                   |
| --------- | --------- | ---- | ------------------------------------- |
| ProfileId | [profileId](js-apis-bluetooth-constant.md#profileid) | No   | ID of the target profile, for example, **PROFILE_A2DP_SOURCE**.|

**Return value**

| Type                                             | Description               |
| ------------------------------------------------- | ------------------- |
| [ProfileConnectionState](js-apis-bluetooth-constant.md#profileconnectionstate) | Profile connection state obtained.|

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
import constant from '@ohos.bluetooth.constant';
try {
    let result: connection.ProfileConnectionState = connection.getProfileConnectionState(constant.ProfileId.PROFILE_A2DP_SOURCE);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.setDevicePairingConfirmation

setDevicePairingConfirmation(deviceId: string, accept: boolean): void

Sets the device pairing confirmation.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH and ohos.permission.MANAGE_BLUETOOTH (available only for system applications)

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name   | Type     | Mandatory  | Description                              |
| ------   | ------- | ---- | -------------------------------- |
| deviceId | string  | Yes   | Address of the remote device, for example, XX:XX:XX:XX:XX:XX.|
| accept   | boolean | Yes   | Whether to accept the pairing request. The value **true** means to accept the pairing request, and the value **false** means the opposite.       |

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
// Subscribe to the pinRequired event and configure the pairing confirmation after receiving a pairing request from the remote device.
function onReceivePinRequiredEvent(data: connection.PinRequiredParam) { // data is the input parameter for the pairing request.
    console.info('pin required  = '+ JSON.stringify(data));
    connection.setDevicePairingConfirmation(data.deviceId, true);
}
try {
    connection.on('pinRequired', onReceivePinRequiredEvent);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.setDevicePinCode

setDevicePinCode(deviceId: string, code: string, callback: AsyncCallback&lt;void&gt;): void

Sets the PIN for the device when **PinType** is **PIN_TYPE_ENTER_PIN_CODE** or **PIN_TYPE_PIN_16_DIGITS**.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name   | Type     | Mandatory  | Description                              |
| ------ | ------- | ---- | -------------------------------- |
| deviceId | string  | Yes   | MAC address of the remote device, for example, XX:XX:XX:XX:XX:XX.|
| code   | string  | Yes   | PIN to set.       |
| callback   | AsyncCallback&lt;void&gt;  | Yes   | Callback used to return the result. If the operation is successful, **err** is **undefined**. Otherwise, **err** is an error object.       |

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
//callback
try {
    connection.setDevicePinCode('11:22:33:44:55:66', '12345', (err: BusinessError) => {
        console.info('setDevicePinCode,device name err:' + JSON.stringify(err));
    });
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.setDevicePinCode

setDevicePinCode(deviceId: string, code: string): Promise&lt;void&gt;

Sets the PIN for the device when **PinType** is **PIN_TYPE_ENTER_PIN_CODE** or **PIN_TYPE_PIN_16_DIGITS**.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name   | Type     | Mandatory  | Description                              |
| ------ | ------- | ---- | -------------------------------- |
| deviceId | string  | Yes   | MAC address of the remote device, for example, XX:XX:XX:XX:XX:XX.|
| code   | string  | Yes   | PIN to set.       |

**Return value**

| Type                 | Description           |
| ------------------- | ------------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
//promise
try {
    connection.setDevicePinCode('11:22:33:44:55:66', '12345').then(() => {
        console.info('setDevicePinCode');
    }, (error: BusinessError) => {
        console.info('setDevicePinCode: errCode:' + error.code + ',errMessage' + error.message);
    })

} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.setLocalName

setLocalName(name: string): void

Sets the name of the local Bluetooth device.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name | Type    | Mandatory  | Description                   |
| ---- | ------ | ---- | --------------------- |
| name | string | Yes   | Bluetooth device name to set. It cannot exceed 248 bytes.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
try {
    connection.setLocalName('device_name');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.setBluetoothScanMode

setBluetoothScanMode(mode: ScanMode, duration: number): void

Sets the Bluetooth scan mode so that the device can be discovered by a remote device.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                   | Mandatory  | Description                          |
| -------- | --------------------- | ---- | ---------------------------- |
| mode     | [ScanMode](#scanmode) | Yes   | Bluetooth scan mode to set.                     |
| duration | number                | Yes   | Duration (in ms) in which the device can be discovered. The value **0** indicates unlimited time.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
try {
    // The device can be discovered and connected only when the discoverable and connectable mode is used.
    connection.setBluetoothScanMode(connection.ScanMode.SCAN_MODE_CONNECTABLE_GENERAL_DISCOVERABLE, 100);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.getBluetoothScanMode

getBluetoothScanMode(): ScanMode

Obtains the Bluetooth scan mode.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Return value**

| Type                   | Description     |
| --------------------- | ------- |
| [ScanMode](#scanmode) | Bluetooth scan mode obtained.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
try {
    let scanMode: connection.ScanMode = connection.getBluetoothScanMode();
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.startBluetoothDiscovery

startBluetoothDiscovery(): void

Starts to discover Bluetooth devices.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
function onReceiveEvent(data: Array<string>) {
    console.log('data length' + data.length);
}
try {
    connection.on('bluetoothDeviceFind', onReceiveEvent);
    connection.startBluetoothDiscovery();
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.stopBluetoothDiscovery

stopBluetoothDiscovery(): void

Stops discovering Bluetooth devices.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
try {
    connection.stopBluetoothDiscovery();
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.isBluetoothDiscovering<sup>11+</sup>

isBluetoothDiscovering(): boolean

Checks whether Bluetooth discovery is enabled.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Return value**

| Type                 | Description           |
| ------------------- | ------------- |
|   boolean           | Returns **true** if Bluetooth discovery is enabled; returns **false** otherwise.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
try {
    let res: boolean = connection.isBluetoothDiscovering();
    console.log('isBluetoothDiscovering: ' + res);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.on('bluetoothDeviceFind')

on(type: 'bluetoothDeviceFind', callback: Callback&lt;Array&lt;string&gt;&gt;): void

Subscribes to the discovery of a Bluetooth device.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                 | Mandatory  | Description                                    |
| -------- | ----------------------------------- | ---- | -------------------------------------- |
| type     | string                              | Yes   | Event type. The value is **bluetoothDeviceFind**, which indicates an event of discovering a Bluetooth device.|
| callback | Callback&lt;Array&lt;string&gt;&gt; | Yes   | Callback used to return the discovered devices. You need to implement this callback. For security purposes, the device addresses are random MAC addresses. The random MAC address remains unchanged after a device is paired successfully. It changes when the paired device is unpaired and scanned again or the Bluetooth service is turned off.   |

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
function onReceiveEvent(data: Array<string>) { // data is an array of Bluetooth device addresses.
    console.info('bluetooth device find = '+ JSON.stringify(data));
}
try {
    connection.on('bluetoothDeviceFind', onReceiveEvent);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.off('bluetoothDeviceFind')

off(type: 'bluetoothDeviceFind', callback?: Callback&lt;Array&lt;string&gt;&gt;): void

Unsubscribes from the discovery of a Bluetooth device.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                 | Mandatory  | Description                                      |
| -------- | ----------------------------------- | ---- | ---------------------------------------- |
| type     | string                              | Yes   | Event type. The value is **bluetoothDeviceFind**, which indicates an event of discovering a Bluetooth device.  |
| callback | Callback&lt;Array&lt;string&gt;&gt; | No   | Callback to unregister. If this parameter is not set, this API unregisters all callbacks for the specified **type**.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
function onReceiveEvent(data: Array<string>) {
    console.info('bluetooth device find = '+ JSON.stringify(data));
}
try {
    connection.on('bluetoothDeviceFind', onReceiveEvent);
    connection.off('bluetoothDeviceFind', onReceiveEvent);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.on('bondStateChange')

on(type: 'bondStateChange', callback: Callback&lt;BondStateParam&gt;): void

Subscribes to Bluetooth pairing state changes.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                  |
| -------- | ---------------------------------------- | ---- | ------------------------------------ |
| type     | string                                   | Yes   | Event type. The value is **bondStateChange**, which indicates a Bluetooth pairing state change event.|
| callback | Callback&lt;[BondStateParam](#bondstateparam)&gt; | Yes   | Callback used to return the pairing state. You need to implement this callback.   |

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
function onReceiveEvent(data: connection.BondStateParam) { // data, as the input parameter of the callback, indicates the pairing state.
    console.info('pair state = '+ JSON.stringify(data));
}
try {
    connection.on('bondStateChange', onReceiveEvent);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.off('bondStateChange')

off(type: 'bondStateChange', callback?: Callback&lt;BondStateParam&gt;): void

Unsubscribes from Bluetooth pairing state changes.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                      |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | Yes   | Event type. The value is **bondStateChange**, which indicates a Bluetooth pairing state change event.    |
| callback | Callback&lt;[BondStateParam](#bondstateparam)&gt; | No   | Callback to unregister. If this parameter is not set, this API unregisters all callbacks for the specified **type**.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
function onReceiveEvent(data: connection.BondStateParam) {
    console.info('bond state = '+ JSON.stringify(data));
}
try {
    connection.on('bondStateChange', onReceiveEvent);
    connection.off('bondStateChange', onReceiveEvent);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.on('pinRequired')

on(type: 'pinRequired', callback: Callback&lt;PinRequiredParam&gt;): void

Subscribes to the pairing request events of the remote Bluetooth device.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                              |
| -------- | ---------------------------------------- | ---- | -------------------------------- |
| type     | string                                   | Yes   | Event type. The value **pinRequired** indicates a pairing request event.    |
| callback | Callback&lt;[PinRequiredParam](#pinrequiredparam)&gt; | Yes   | Callback used to return the pairing request. You need to implement this callback.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
function onReceiveEvent(data: connection.PinRequiredParam) { // data is the pairing request parameter.
    console.info('pin required = '+ JSON.stringify(data));
}
try {
    connection.on('pinRequired', onReceiveEvent);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## connection.off('pinRequired')

off(type: 'pinRequired', callback?: Callback&lt;PinRequiredParam&gt;): void

Unsubscribes from the pairing request events of the remote Bluetooth device.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                      |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | Yes   | Event type. The value **pinRequired** indicates a pairing request event.            |
| callback | Callback&lt;[PinRequiredParam](#pinrequiredparam)&gt; | No   | Callback to unregister. The input parameter is the pairing request parameter. If this parameter is not set, this API unregisters all callbacks for the specified **type**.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**Example**

```js
import { BusinessError } from '@ohos.base';
function onReceiveEvent(data: connection.PinRequiredParam) {
    console.info('pin required = '+ JSON.stringify(data));
}
try {
    connection.on('pinRequired', onReceiveEvent);
    connection.off('pinRequired', onReceiveEvent);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


## BondStateParam

Represents the pairing state parameters.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name      | Type  | Readable  | Writable  | Description         |
| -------- | ------ | ---- | ---- | ----------- |
| deviceId | string      | Yes   | No   | ID of the device to pair.|
| state    | BondState   | Yes   | No   | State of the device.|


## PinRequiredParam

Represents the pairing request parameters.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name      | Type  | Readable  | Writable  | Description         |
| -------- | ------ | ---- | ---- | ----------- |
| deviceId | string | Yes   | No   | ID of the device to pair.|
| pinCode  | string | Yes   | No   | Key for the device pairing.  |



## DeviceClass

Represents the class of a Bluetooth device.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name             | Type                               | Readable  | Writable  | Description              |
| --------------- | ----------------------------------- | ---- | ---- | ---------------- |
| majorClass      | [MajorClass](js-apis-bluetooth-constant.md#majorclass)           | Yes   | No   | Major class of the Bluetooth device.  |
| majorMinorClass | [MajorMinorClass](js-apis-bluetooth-constant.md#majorminorclass) | Yes   | No   | Major and minor classes of the Bluetooth device.|
| classOfDevice   | number                              | Yes   | No   | Class of the device.         |


## BluetoothTransport

Enumerates the device types. The default device type is **TRANSPORT_BR_EDR**.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name                              | Value   | Description             |
| -------------------------------- | ------ | --------------- |
| TRANSPORT_BR_EDR   | 0 | Classic Bluetooth (BR/EDR) device.|
| TRANSPORT_LE  | 1 | BLE device. |


## ScanMode

Enumerates the scan modes.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name                                      | Value | Description             |
| ---------------------------------------- | ---- | --------------- |
| SCAN_MODE_NONE                           | 0    | No scan mode.        |
| SCAN_MODE_CONNECTABLE                    | 1    | Connectable mode.       |
| SCAN_MODE_GENERAL_DISCOVERABLE           | 2    | General discoverable mode.   |
| SCAN_MODE_LIMITED_DISCOVERABLE           | 3    | Limited discoverable mode.   |
| SCAN_MODE_CONNECTABLE_GENERAL_DISCOVERABLE | 4    | General connectable and discoverable mode.|
| SCAN_MODE_CONNECTABLE_LIMITED_DISCOVERABLE | 5    | Limited connectable and discoverable mode.|


## BondState

Enumerates the pairing states.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name                | Value | Description    |
| ------------------ | ---- | ------ |
| BOND_STATE_INVALID | 0    | Invalid pairing.|
| BOND_STATE_BONDING | 1    | Pairing. |
| BOND_STATE_BONDED  | 2    | Paired.  |
