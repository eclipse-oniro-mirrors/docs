# @ohos.bluetooth.ble (Bluetooth BLE Module)

The **ble** module provides APIs for accessing the Bluetooth personal area network.

> **NOTE**
>
> The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version.



## Modules to Import

```js
import ble from '@ohos.bluetooth.ble';
```


## ble.createGattServer<a name="createGattServer"></a>

createGattServer(): GattServer

Creates a **GattServer** instance.

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Return value**

| Type                           | Description        |
| ----------------------------- | ---------- |
| GattServer | **GattServer** instance created.|

**Example**

```js
let gattServer = ble.createGattServer();
console.info('gatt success');
```


## ble.createGattClientDevice<a name="createGattClientDevice"></a>

createGattClientDevice(deviceId: string): GattClientDevice

Creates a **GattClientDevice** instance.

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type    | Mandatory  | Description                                  |
| -------- | ------ | ---- | ------------------------------------ |
| deviceId | string | Yes   | Address of the remote device, for example, XX:XX:XX:XX:XX:XX.|

**Return value**

| Type                                   | Description                                  |
| ------------------------------------- | ------------------------------------ |
| [GattClientDevice](#gattclientdevice) | **GattClientDevice** instance created. Before using an API of the client, you must create a **GattClientDevice** instance.|

**Example**

```js
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


## ble.getConnectedBLEDevices<a name="getConnectedBLEDevices"></a>

getConnectedBLEDevices(): Array&lt;string&gt;

Obtains the Bluetooth Low Energy (BLE) devices connected to this device.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Return value**

| Type                 | Description                 |
| ------------------- | ------------------- |
| Array&lt;string&gt; | Addresses of the BLE devices connected to this device.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
try {
    let result = ble.getConnectedBLEDevices();
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


## ble.startBLEScan<a name="startBLEScan"></a>

startBLEScan(filters: Array&lt;ScanFilter&gt;, options?: ScanOptions): void

Starts a BLE scan.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name    | Type                                    | Mandatory  | Description                                 |
| ------- | -------------------------------------- | ---- | ----------------------------------- |
| filters | Array&lt;[ScanFilter](#scanfilter)&gt; | Yes   | Criteria for filtering the scan result. Set this parameter to **null** if you do not want to filter the scan result.|
| options | [ScanOptions](#scanoptions)            | No   | Scan options.                    |

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
function onReceiveEvent(data) {
    console.info('BLE scan device find result = '+ JSON.stringify(data));
}
try {
    ble.on("BLEDeviceFind", onReceiveEvent);
    ble.startBLEScan(
        [{
            deviceId:"XX:XX:XX:XX:XX:XX",
            name:"test",
            serviceUuid:"00001888-0000-1000-8000-00805f9b34fb"
        }],
        {
            interval: 500,
            dutyMode: ble.ScanDuty.SCAN_MODE_LOW_POWER,
            matchMode: ble.MatchMode.MATCH_MODE_AGGRESSIVE,
        }
    );
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


## ble.stopBLEScan<a name="stopBLEScan"></a>

stopBLEScan(): void

Stops the BLE scan.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
try {
    ble.stopBLEScan();
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


## ble.startAdvertising<a name="startAdvertising"></a>

startAdvertising(setting: AdvertiseSetting, advData: AdvertiseData, advResponse?: AdvertiseData): void

Starts BLE advertising.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name        | Type                                   | Mandatory  | Description            |
| ----------- | ------------------------------------- | ---- | -------------- |
| setting     | [AdvertiseSetting](#advertisesetting) | Yes   | Settings related to BLE advertising.   |
| advData     | [AdvertiseData](#advertisedata)       | Yes   | Content of the BLE advertisement packet.     |
| advResponse | [AdvertiseData](#advertisedata)       | No   | Response to the BLE scan request.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
let manufactureValueBuffer = new Uint8Array(4);
manufactureValueBuffer[0] = 1;
manufactureValueBuffer[1] = 2;
manufactureValueBuffer[2] = 3;
manufactureValueBuffer[3] = 4;

let serviceValueBuffer = new Uint8Array(4);
serviceValueBuffer[0] = 4;
serviceValueBuffer[1] = 6;
serviceValueBuffer[2] = 7;
serviceValueBuffer[3] = 8;
console.info('manufactureValueBuffer = '+ JSON.stringify(manufactureValueBuffer));
console.info('serviceValueBuffer = '+ JSON.stringify(serviceValueBuffer));
try {
    ble.startAdvertising({
            interval:150,
            txPower:0,
            connectable:true,
        },{
            serviceUuids:["00001888-0000-1000-8000-00805f9b34fb"],
            manufactureData:[{
                 manufactureId:4567,
                 manufactureValue:manufactureValueBuffer.buffer
            }],
            serviceData:[{
                serviceUuid:"00001888-0000-1000-8000-00805f9b34fb",
                serviceValue:serviceValueBuffer.buffer
            }],
        },{
            serviceUuids:["00001889-0000-1000-8000-00805f9b34fb"],
            manufactureData:[{
                manufactureId:1789,
                manufactureValue:manufactureValueBuffer.buffer
            }],
            serviceData:[{
                serviceUuid:"00001889-0000-1000-8000-00805f9b34fb",
                serviceValue:serviceValueBuffer.buffer
            }],
    });
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


## ble.stopAdvertising<a name="stopAdvertising"></a>

stopAdvertising(): void

Stops BLE advertising.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
try {
    ble.stopAdvertising();
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


## ble.on('BLEDeviceFind')

on(type: 'BLEDeviceFind', callback: Callback&lt;Array&lt;ScanResult&gt;&gt;): void

Subscribes to BLE device discovery events.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                 |
| -------- | ---------------------------------------- | ---- | ----------------------------------- |
| type     | string                                   | Yes   | Event type. The value is **BLEDeviceFind**, which indicates an event of discovering a BLE device.  |
| callback | Callback&lt;Array&lt;[ScanResult](#scanresult)&gt;&gt; | Yes   | Callback invoked to return the discovered devices. You need to implement this callback.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**Example**

```js
function onReceiveEvent(data) {
    console.info('bluetooth device find = '+ JSON.stringify(data));
}
try {
    ble.on('BLEDeviceFind', onReceiveEvent);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


## ble.off('BLEDeviceFind')

off(type: 'BLEDeviceFind', callback?: Callback&lt;Array&lt;ScanResult&gt;&gt;): void

Unsubscribes from BLE device discovery events.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                      |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | Yes   | Event type. The value is **BLEDeviceFind**, which indicates an event of discovering a BLE device.       |
| callback | Callback&lt;Array&lt;[ScanResult](#scanresult)&gt;&gt; | No   | Callback for the **BLEDeviceFind** event. If this parameter is not set, this API unsubscribes from all callbacks corresponding to **type**.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**Example**

```js
function onReceiveEvent(data) {
    console.info('bluetooth device find = '+ JSON.stringify(data));
}
try {
    ble.on('BLEDeviceFind', onReceiveEvent);
    ble.off('BLEDeviceFind', onReceiveEvent);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


## GattServer

Implements the Generic Attribute Profile (GATT) server. Before using an API of this class, you need to create a **GattServer** instance using **createGattServer()**.


### addService

addService(service: GattService): void

Adds a service to this GATT server.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name    | Type                         | Mandatory  | Description                      |
| ------- | --------------------------- | ---- | ------------------------ |
| service | [GattService](#gattservice) | Yes   | Service to add. Settings related to BLE advertising.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
// Create descriptors.
let descriptors = [];
let arrayBuffer = new ArrayBuffer(8);
let descV = new Uint8Array(arrayBuffer);
descV[0] = 11;
let descriptor = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
  descriptorUuid: '00002902-0000-1000-8000-00805F9B34FB', descriptorValue: arrayBuffer};
descriptors[0] = descriptor;

// Create characteristics.
let characteristics = [];
let arrayBufferC = new ArrayBuffer(8);
let cccV = new Uint8Array(arrayBufferC);
cccV[0] = 1;
let characteristic = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB', characteristicValue: arrayBufferC, descriptors:descriptors};
let characteristicN = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001821-0000-1000-8000-00805F9B34FB', characteristicValue: arrayBufferC, descriptors:descriptors};
characteristics[0] = characteristic;

// Create a gattService instance.
let gattService = {serviceUuid:'00001810-0000-1000-8000-00805F9B34FB', isPrimary: true, characteristics:characteristics, includeServices:[]};

try {
    gattServer.addService(gattService);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### removeService

removeService(serviceUuid: string): void

Removes a service from this GATT server.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name        | Type    | Mandatory  | Description                                      |
| ----------- | ------ | ---- | ---------------------------------------- |
| serviceUuid | string | Yes   | Universally unique identifier (UUID) of the service to remove, for example, **00001810-0000-1000-8000-00805F9B34FB**.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900004 | Profile is not supported.                |
|2900099 | Operation failed.                        |

**Example**

```js
let server = ble.createGattServer();
try {
    server.removeService('00001810-0000-1000-8000-00805F9B34FB');
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### close

close(): void

Closes this GATT server to unregister it from the protocol stack. The closed [GattServer](#gattserver) instance will no longer be used.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
let server = ble.createGattServer();
try {
    server.close();
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### notifyCharacteristicChanged

notifyCharacteristicChanged(deviceId: string, notifyCharacteristic: NotifyCharacteristic, callback: AsyncCallback&lt;void&gt;): void

Notifies a connected client device when a characteristic value changes. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name                 | Type                                      | Mandatory  | Description                                     |
| -------------------- | ---------------------------------------- | ---- | --------------------------------------- |
| deviceId             | string                                   | Yes   | Address of the client that receives the notifications, for example, XX:XX:XX:XX:XX:XX.|
| notifyCharacteristic | [NotifyCharacteristic](#notifycharacteristic) | Yes   | New characteristic value.                              |
| callback | AsyncCallback&lt;void&gt;  | Yes   | Callback invoked to return the result. If the operation is successful, **err** is **undefined**; otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
let arrayBufferC = new ArrayBuffer(8);
let notifyCharacter = {
    "serviceUuid": '00001810-0000-1000-8000-00805F9B34FB',
    "characteristicUuid": '00001820-0000-1000-8000-00805F9B34FB',
    "characteristicValue": arrayBufferC,
    "confirm": true,
};
try {
    gattServer.notifyCharacteristicChanged('XX:XX:XX:XX:XX:XX', notifyCharacter, (err) => {
        if (err) {
            console.info('notifyCharacteristicChanged callback failed');
        } else {
            console.info('notifyCharacteristicChanged callback successful');
        }
    });
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### notifyCharacteristicChanged

notifyCharacteristicChanged(deviceId: string, notifyCharacteristic: NotifyCharacteristic): Promise&lt;void&gt;

Notifies a connected client device when a characteristic value changes. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name                 | Type                                      | Mandatory  | Description                                     |
| -------------------- | ---------------------------------------- | ---- | --------------------------------------- |
| deviceId             | string                                   | Yes   | Address of the client that receives the notifications, for example, XX:XX:XX:XX:XX:XX.|
| notifyCharacteristic | [NotifyCharacteristic](#notifycharacteristic) | Yes   | New characteristic value.                              |

**Return value**

| Type                 | Description           |
| ------------------- | ------------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
let arrayBufferC = new ArrayBuffer(8);
let notifyCharacter = {
    "serviceUuid": '00001810-0000-1000-8000-00805F9B34FB',
    "characteristicUuid": '00001820-0000-1000-8000-00805F9B34FB',
    "characteristicValue": arrayBufferC,
    "confirm": true,
};
try {
    gattServer.notifyCharacteristicChanged('XX:XX:XX:XX:XX:XX', notifyCharacter).then(() => {
        console.info('notifyCharacteristicChanged promise successfull');
    });
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### sendResponse

sendResponse(serverResponse: ServerResponse): void

Sends a response to a read or write request from the GATT client.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name           | Type                               | Mandatory  | Description             |
| -------------- | --------------------------------- | ---- | --------------- |
| serverResponse | [ServerResponse](#serverresponse) | Yes   | Response returned by the GATT server.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
/* send response */
let arrayBufferCCC = new ArrayBuffer(8);
let cccValue = new Uint8Array(arrayBufferCCC);
cccValue[0] = 1123;
let serverResponse = {
    'deviceId': 'XX:XX:XX:XX:XX:XX',
    'transId': 0,
    'status': 0,
    'offset': 0,
    'value': arrayBufferCCC,
};
try {
    gattServer.sendResponse(serverResponse);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### on('characteristicRead')

on(type: 'characteristicRead', callback: Callback&lt;CharacteristicReadRequest&gt;): void

Subscribes to characteristic read request events.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                   |
| -------- | ---------------------------------------- | ---- | ------------------------------------- |
| type     | string                                   | Yes   | Event type. The value is **characteristicRead**, which indicates a characteristic read request event.|
| callback | Callback&lt;[CharacteristicReadRequest](#characteristicreadrequest)&gt; | Yes   | Callback invoked to return a characteristic read request event from the GATT client.           |

**Example**

```js
let arrayBufferCCC = new ArrayBuffer(8);
let cccValue = new Uint8Array(arrayBufferCCC);
cccValue[0] = 1123;
function ReadCharacteristicReq(CharacteristicReadRequest) {
    let deviceId = CharacteristicReadRequest.deviceId;
    let transId = CharacteristicReadRequest.transId;
    let offset = CharacteristicReadRequest.offset;
    let characteristicUuid = CharacteristicReadRequest.characteristicUuid;

    let serverResponse = {deviceId: deviceId, transId: transId, status: 0, offset: offset, value:arrayBufferCCC};

    try {
        gattServer.sendResponse(serverResponse);
    } catch (err) {
        console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
    }
}
gattServer.on('characteristicRead', ReadCharacteristicReq);
```


### off('characteristicRead')

off(type: 'characteristicRead', callback?: Callback&lt;CharacteristicReadRequest&gt;): void

Unsubscribes from characteristic read request events.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                      |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | Yes   | Event type. The value is **characteristicRead**, which indicates a characteristic read request event.   |
| callback | Callback&lt;[CharacteristicReadRequest](#characteristicreadrequest)&gt; | No   | Callback for the characteristic read request event. If this parameter is not set, this API unsubscribes from all callbacks corresponding to **type**.|

**Example**

```js
gattServer.off('characteristicRead');
```


### on('characteristicWrite')

on(type: 'characteristicWrite', callback: Callback&lt;CharacteristicWriteRequest&gt;): void

Subscribes to characteristic write request events.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                    |
| -------- | ---------------------------------------- | ---- | -------------------------------------- |
| type     | string                                   | Yes   | Event type. The value **characteristicWrite** indicates a characteristic write request event.|
| callback | Callback&lt;[CharacteristicWriteRequest](#characteristicwriterequest)&gt; | Yes   | Callback invoked to return a characteristic write request from the GATT client.            |

**Example**

```js
let arrayBufferCCC = new ArrayBuffer(8);
let cccValue = new Uint8Array(arrayBufferCCC);
function WriteCharacteristicReq(CharacteristicWriteRequest) {
    let deviceId = CharacteristicWriteRequest.deviceId;
    let transId = CharacteristicWriteRequest.transId;
    let offset = CharacteristicWriteRequest.offset;
    let isPrepared = CharacteristicWriteRequest.isPrepared;
    let needRsp = CharacteristicWriteRequest.needRsp;
    let value =  new Uint8Array(CharacteristicWriteRequest.value);
    let characteristicUuid = CharacteristicWriteRequest.characteristicUuid;

    cccValue[0] = value[0];
    let serverResponse = {deviceId: deviceId, transId: transId, status: 0, offset: offset, value:arrayBufferCCC};

    try {
        gattServer.sendResponse(serverResponse);
    } catch (err) {
        console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
    }
}
gattServer.on('characteristicWrite', WriteCharacteristicReq);
```


### off('characteristicWrite')

off(type: 'characteristicWrite', callback?: Callback&lt;CharacteristicWriteRequest&gt;): void

Unsubscribes from characteristic write request events.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                      |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | Yes   | Event type. The value is **characteristicWrite**, which indicates a characteristic write request event.  |
| callback | Callback&lt;[CharacteristicWriteRequest](#characteristicwriterequest)&gt; | No   | Callback for the characteristic write request event. If this parameter is not set, this API unsubscribes from all callbacks corresponding to **type**.|

**Example**

```js
gattServer.off('characteristicWrite');
```


### on('descriptorRead')

on(type: 'descriptorRead', callback: Callback&lt;DescriptorReadRequest&gt;): void

Subscribes to descriptor read request events.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                               |
| -------- | ---------------------------------------- | ---- | --------------------------------- |
| type     | string                                   | Yes   | Event type. The value is **descriptorRead**, which indicates a descriptor read request event.|
| callback | Callback&lt;[DescriptorReadRequest](#descriptorreadrequest)&gt; | Yes   | Callback invoked to return a descriptor read request event from the GATT client.       |

**Example**

```js
let arrayBufferDesc = new ArrayBuffer(8);
let descValue = new Uint8Array(arrayBufferDesc);
descValue[0] = 1101;
function ReadDescriptorReq(DescriptorReadRequest) {
    let deviceId = DescriptorReadRequest.deviceId;
    let transId = DescriptorReadRequest.transId;
    let offset = DescriptorReadRequest.offset;
    let descriptorUuid = DescriptorReadRequest.descriptorUuid;

    let serverResponse = {deviceId: deviceId, transId: transId, status: 0, offset: offset, value:arrayBufferDesc};

    try {
        gattServer.sendResponse(serverResponse);
    } catch (err) {
        console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
    }
}
gattServer.on('descriptorRead', ReadDescriptorReq);
```


### off('descriptorRead')

off(type: 'descriptorRead', callback?: Callback&lt;DescriptorReadRequest&gt;): void

Unsubscribes from descriptor read request events.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                      |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | Yes   | Event type. The value is **descriptorRead**, which indicates a descriptor read request event.       |
| callback | Callback&lt;[DescriptorReadRequest](#descriptorreadrequest)&gt; | No   | Callback for the descriptor read request event. If this parameter is not set, this API unsubscribes from all callbacks corresponding to **type**.|

**Example**

```js
gattServer.off('descriptorRead');
```


### on('descriptorWrite')

on(type: 'descriptorWrite', callback: Callback&lt;DescriptorWriteRequest&gt;): void

Subscribes to descriptor write request events.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                |
| -------- | ---------------------------------------- | ---- | ---------------------------------- |
| type     | string                                   | Yes   | Event type. The value is **descriptorWrite**, which indicates a descriptor write request event.|
| callback | Callback&lt;[DescriptorWriteRequest](#descriptorwriterequest)&gt; | Yes   | Callback invoked to return a descriptor write request from the GATT client.        |

**Example**

```js
let arrayBufferDesc = new ArrayBuffer(8);
let descValue = new Uint8Array(arrayBufferDesc);
function WriteDescriptorReq(DescriptorWriteRequest) {
    let deviceId = DescriptorWriteRequest.deviceId;
    let transId = DescriptorWriteRequest.transId;
    let offset = DescriptorWriteRequest.offset;
    let isPrepared = DescriptorWriteRequest.isPrepared;
    let needRsp = DescriptorWriteRequest.needRsp;
    let value = new Uint8Array(DescriptorWriteRequest.value);
    let descriptorUuid = DescriptorWriteRequest.descriptorUuid;

    descValue[0] = value[0];
    let serverResponse = {deviceId: deviceId, transId: transId, status: 0, offset: offset, value:arrayBufferDesc};

    try {
        gattServer.sendResponse(serverResponse);
    } catch (err) {
        console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
    }
}
gattServer.on('descriptorRead', WriteDescriptorReq);
```


### off('descriptorWrite')

off(type: 'descriptorWrite', callback?: Callback&lt;DescriptorWriteRequest&gt;): void

Unsubscribes from descriptor write request events.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                      |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | Yes   | Event type. The value is **descriptorWrite**, which indicates a descriptor write request event.      |
| callback | Callback&lt;[DescriptorWriteRequest](#descriptorwriterequest)&gt; | No   | Callback for the descriptor write request event. If this parameter is not set, this API unsubscribes from all callbacks corresponding to **type**.|

**Example**

```js
gattServer.off('descriptorWrite');
```


### on('connectionStateChange')

on(type: 'connectionStateChange', callback: Callback&lt;BLEConnectionChangeState&gt;): void

Subscribes to BLE connection state change events.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                      |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | Yes   | Event type. The value is **connectionStateChange**, which indicates a BLE connection state change event.|
| callback | Callback&lt;[BLEConnectionChangeState](#bleconnectionchangestate)&gt; | Yes   | Callback invoked to return the BLE connection state.                         |

**Example**

```js
function Connected(BLEConnectionChangeState) {
  let deviceId = BLEConnectionChangeState.deviceId;
  let status = BLEConnectionChangeState.state;
}
gattServer.on('connectionStateChange', Connected);
```


### off('connectionStateChange')

off(type: 'connectionStateChange', callback?: Callback&lt;BLEConnectionChangeState&gt;): void

Unsubscribes from BLE connection state changes.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                      |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | Yes   | Event type. The value is **connectionStateChange**, which indicates a BLE connection state change event.|
| callback | Callback&lt;[BLEConnectionChangeState](#bleconnectionchangestate)&gt; | No   | Callback for the BLE connection state change event. If this parameter is not set, this API unsubscribes from all callbacks corresponding to **type**.|

**Example**

```js
gattServer.off('connectionStateChange');
```


## GattClientDevice

Implements the GATT client. Before using an API of this class, you must create a **GattClientDevice** instance using **createGattClientDevice(deviceId: string)**.


### connect

connect(): void

Connects to the remote BLE device.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.connect();
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### disconnect

disconnect(): void

Disconnects from the remote BLE device.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.disconnect();
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### close

close(): void

Closes this GATT client to unregister it from the protocol stack. The closed [GattClientDevice](#gattclientdevice) instance will no longer be used.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**Example**

```js
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.close();
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### getDeviceName

getDeviceName(callback: AsyncCallback&lt;string&gt;): void

Obtains the name of the remote BLE device. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                         | Mandatory  | Description                             |
| -------- | --------------------------- | ---- | ------------------------------- |
| callback | AsyncCallback&lt;string&gt; | Yes   | Callback invoked to return the remote BLE device name obtained.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**Example**

```js
// callback
try {
    let gattClient = ble.createGattClientDevice("XX:XX:XX:XX:XX:XX");
    gattClient.connect();
    let deviceName = gattClient.getDeviceName((err, data)=> {
        console.info('device name err ' + JSON.stringify(err));
        console.info('device name' + JSON.stringify(data));
    })
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### getDeviceName

getDeviceName(): Promise&lt;string&gt;

Obtains the name of the remote BLE device. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Return value**

| Type                   | Description                                |
| --------------------- | ---------------------------------- |
| Promise&lt;string&gt; | Promise used to return the remote BLE device name.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**Example**

```js
// promise
try {
    let gattClient = ble.createGattClientDevice("XX:XX:XX:XX:XX:XX");
    gattClient.connect();
    let deviceName = gattClient.getDeviceName().then((data) => {
        console.info('device name' + JSON.stringify(data));
    })
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### getServices

getServices(callback: AsyncCallback&lt;Array&lt;GattService&gt;&gt;): void

Obtains all services of the remote BLE device. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                      |
| -------- | ---------------------------------------- | ---- | ------------------------ |
| callback | AsyncCallback&lt;Array&lt;[GattService](#gattservice)&gt;&gt; | Yes   | Callback invoked to return the services obtained.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**Example**

```js
// Callback
function getServices(code, gattServices) {
  if (code.code == 0) {
      let services = gattServices;
      console.log('bluetooth code is ' + code.code);
      console.log('bluetooth services size is ', services.length);

      for (let i = 0; i < services.length; i++) {
        console.log('bluetooth serviceUuid is ' + services[i].serviceUuid);
      }
  }
}

try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.connect();
    device.getServices(getServices);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### getServices

getServices(): Promise&lt;Array&lt;GattService&gt;&gt;

Obtains all services of the remote BLE device. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Return value**

| Type                                      | Description                         |
| ---------------------------------------- | --------------------------- |
| Promise&lt;Array&lt;[GattService](#gattservice)&gt;&gt; | Promise used to return the services obtained.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**Example**

```js
// Promise
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.connect();
    device.getServices().then(result => {
        console.info('getServices successfully:' + JSON.stringify(result));
    });
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### readCharacteristicValue

readCharacteristicValue(characteristic: BLECharacteristic, callback: AsyncCallback&lt;BLECharacteristic&gt;): void

Reads the characteristic value of the specific service of the remote BLE device. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name           | Type                                      | Mandatory  | Description                     |
| -------------- | ---------------------------------------- | ---- | ----------------------- |
| characteristic | [BLECharacteristic](#blecharacteristic)  | Yes   | Characteristic value to read.               |
| callback       | AsyncCallback&lt;[BLECharacteristic](#blecharacteristic)&gt; | Yes   | Callback invoked to return the characteristic value read.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2901000 | Read forbidden.                         |
|2900099 | Operation failed.                        |

**Example**

```js
function readCcc(code, BLECharacteristic) {
  if (code.code != 0) {
      return;
  }
  console.log('bluetooth characteristic uuid: ' + BLECharacteristic.characteristicUuid);
  let value = new Uint8Array(BLECharacteristic.characteristicValue);
  console.log('bluetooth characteristic value: ' + value[0] +','+ value[1]+','+ value[2]+','+ value[3]);
}

let descriptors = [];
let bufferDesc = new ArrayBuffer(8);
let descV = new Uint8Array(bufferDesc);
descV[0] = 11;
let descriptor = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
descriptorUuid: '00002903-0000-1000-8000-00805F9B34FB', descriptorValue: bufferDesc};
descriptors[0] = descriptor;

let bufferCCC = new ArrayBuffer(8);
let cccV = new Uint8Array(bufferCCC);
cccV[0] = 1;
let characteristic = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
characteristicValue: bufferCCC, descriptors:descriptors};

try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.readCharacteristicValue(characteristic, readCcc);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### readCharacteristicValue

readCharacteristicValue(characteristic: BLECharacteristic): Promise&lt;BLECharacteristic&gt;

Reads the characteristic value of the specific service of the remote BLE device. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name           | Type                                     | Mandatory  | Description      |
| -------------- | --------------------------------------- | ---- | -------- |
| characteristic | [BLECharacteristic](#blecharacteristic) | Yes   | Characteristic value to read.|

**Return value**

| Type                                      | Description                        |
| ---------------------------------------- | -------------------------- |
| Promise&lt;[BLECharacteristic](#blecharacteristic)&gt; | Promise used to return the characteristic value read.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2901000 | Read forbidden.                         |
|2900099 | Operation failed.                        |

**Example**

```js
let descriptors = [];
let bufferDesc = new ArrayBuffer(8);
let descV = new Uint8Array(bufferDesc);
descV[0] = 11;
let descriptor = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
descriptorUuid: '00002903-0000-1000-8000-00805F9B34FB', descriptorValue: bufferDesc};
descriptors[0] = descriptor;

let bufferCCC = new ArrayBuffer(8);
let cccV = new Uint8Array(bufferCCC);
cccV[0] = 1;
let characteristic = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
characteristicValue: bufferCCC, descriptors:descriptors};

try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.readCharacteristicValue(characteristic);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### readDescriptorValue

readDescriptorValue(descriptor: BLEDescriptor, callback: AsyncCallback&lt;BLEDescriptor&gt;): void

Reads the descriptor contained in the specific characteristic of the remote BLE device. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name       | Type                                      | Mandatory  | Description                     |
| ---------- | ---------------------------------------- | ---- | ----------------------- |
| descriptor | [BLEDescriptor](#bledescriptor)          | Yes   | Descriptor to read.               |
| callback   | AsyncCallback&lt;[BLEDescriptor](#bledescriptor)&gt; | Yes   | Callback invoked to return the descriptor read.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2901000 | Read forbidden.                         |
|2900099 | Operation failed.                        |

**Example**

```js
function readDesc(code, BLEDescriptor) {
    if (code.code != 0) {
        return;
    }
    console.log('bluetooth descriptor uuid: ' + BLEDescriptor.descriptorUuid);
    let value = new Uint8Array(BLEDescriptor.descriptorValue);
    console.log('bluetooth descriptor value: ' + value[0] +','+ value[1]+','+ value[2]+','+ value[3]);
}

let bufferDesc = new ArrayBuffer(8);
let descV = new Uint8Array(bufferDesc);
descV[0] = 11;
let descriptor = {
    serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
    characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
    descriptorUuid: '00002903-0000-1000-8000-00805F9B34FB',
    descriptorValue: bufferDesc
};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.readDescriptorValue(descriptor, readDesc);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### readDescriptorValue

readDescriptorValue(descriptor: BLEDescriptor): Promise&lt;BLEDescriptor&gt;

Reads the descriptor contained in the specific characteristic of the remote BLE device. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name       | Type                             | Mandatory  | Description      |
| ---------- | ------------------------------- | ---- | -------- |
| descriptor | [BLEDescriptor](#bledescriptor) | Yes   | Descriptor to read.|

**Return value**

| Type                                      | Description                        |
| ---------------------------------------- | -------------------------- |
| Promise&lt;[BLEDescriptor](#bledescriptor)&gt; | Promise used to return the descriptor read.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.               |
|2901000 | Read forbidden.                |
|2900099 | Operation failed.              |

**Example**

```js
let bufferDesc = new ArrayBuffer(8);
let descV = new Uint8Array(bufferDesc);
descV[0] = 11;
let descriptor = {
    serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
    characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
    descriptorUuid: '00002903-0000-1000-8000-00805F9B34FB',
    descriptorValue: bufferDesc
};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.readDescriptorValue(descriptor);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### writeCharacteristicValue

writeCharacteristicValue(characteristic: BLECharacteristic, writeType: GattWriteType, callback: AsyncCallback&lt;void&gt;): void

Writes a characteristic value to the remote BLE device.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name           | Type                                     | Mandatory  | Description                 |
| -------------- | --------------------------------------- | ---- | ------------------- |
| characteristic | [BLECharacteristic](#blecharacteristic) | Yes   | Binary value and other parameters of the BLE device characteristic.|
| writeType | GattWriteType | Yes   | Write type of the Bluetooth device characteristic value.|
| callback   | AsyncCallback&lt;void&gt; | Yes   | Callback invoked to return the result. If the write operation is successful, **err** is **undefined**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2901001 | Write forbidden.                        |
|2900099 | Operation failed.                        |

**Example**

```js
let descriptors = [];
let bufferDesc = new ArrayBuffer(8);
let descV = new Uint8Array(bufferDesc);
descV[0] = 11;
let descriptor = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
  descriptorUuid: '00002903-0000-1000-8000-00805F9B34FB', descriptorValue: bufferDesc};
descriptors[0] = descriptor;

let bufferCCC = new ArrayBuffer(8);
let cccV = new Uint8Array(bufferCCC);
cccV[0] = 1;
let characteristic = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
  characteristicValue: bufferCCC, descriptors:descriptors};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.writeCharacteristicValue(characteristic);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### writeCharacteristicValue

writeCharacteristicValue(characteristic: BLECharacteristic, writeType: GattWriteType): Promise&lt;void&gt;

Writes a characteristic value to the remote BLE device.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name           | Type                                     | Mandatory  | Description                 |
| -------------- | --------------------------------------- | ---- | ------------------- |
| characteristic | [BLECharacteristic](#blecharacteristic) | Yes   | Binary value and other parameters of the BLE device characteristic.|
| writeType | GattWriteType | Yes   | Write type of the Bluetooth device characteristic value.|

**Return value**

| Type                                      | Description                        |
| ---------------------------------------- | -------------------------- |
| Promise&lt;void&gt; | Promise used to return the descriptor read.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2901001 | Write forbidden.                        |
|2900099 | Operation failed.                        |

**Example**

```js
let descriptors = [];
let bufferDesc = new ArrayBuffer(8);
let descV = new Uint8Array(bufferDesc);
descV[0] = 11;
let descriptor = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
  descriptorUuid: '00002903-0000-1000-8000-00805F9B34FB', descriptorValue: bufferDesc};
descriptors[0] = descriptor;

let bufferCCC = new ArrayBuffer(8);
let cccV = new Uint8Array(bufferCCC);
cccV[0] = 1;
let characteristic = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
  characteristicValue: bufferCCC, descriptors:descriptors};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.writeCharacteristicValue(characteristic);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### writeDescriptorValue

writeDescriptorValue(descriptor: BLEDescriptor, callback: AsyncCallback&lt;void&gt;): void

Writes binary data to the specific descriptor of the remote BLE device.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name       | Type                             | Mandatory  | Description                |
| ---------- | ------------------------------- | ---- | ------------------ |
| descriptor | [BLEDescriptor](#bledescriptor) | Yes   | Binary value and other parameters of the BLE device descriptor.|
| callback   | AsyncCallback&lt;void&gt; | Yes   | Callback invoked to return the result. If the write operation is successful, **err** is **undefined**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2901001 | Write forbidden.                        |
|2900099 | Operation failed.                        |

**Example**

```js
let bufferDesc = new ArrayBuffer(8);
let descV = new Uint8Array(bufferDesc);
descV[0] = 22;
let descriptor = {
    serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
    characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
    descriptorUuid: '00002903-0000-1000-8000-00805F9B34FB',
    descriptorValue: bufferDesc
};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.writeDescriptorValue(descriptor);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### writeDescriptorValue

writeDescriptorValue(descriptor: BLEDescriptor): Promise&lt;void&gt;

Writes binary data to the specific descriptor of the remote BLE device.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name       | Type                             | Mandatory  | Description                |
| ---------- | ------------------------------- | ---- | ------------------ |
| descriptor | [BLEDescriptor](#bledescriptor) | Yes   | Binary value and other parameters of the BLE device descriptor.|

**Return value**

| Type                                      | Description                        |
| ---------------------------------------- | -------------------------- |
| Promise&lt;void&gt; | Promise used to return the descriptor read.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2901001 | Write forbidden.                        |
|2900099 | Operation failed.                        |

**Example**

```js
let bufferDesc = new ArrayBuffer(8);
let descV = new Uint8Array(bufferDesc);
descV[0] = 22;
let descriptor = {
    serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
    characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
    descriptorUuid: '00002903-0000-1000-8000-00805F9B34FB',
    descriptorValue: bufferDesc
};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.writeDescriptorValue(descriptor);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### getRssiValue

getRssiValue(callback: AsyncCallback&lt;number&gt;): void

Obtains the RSSI of the remote BLE device. This API uses an asynchronous callback to return the result. It can be used only after a connection is set up by calling [connect](#connect).

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                         | Mandatory  | Description                            |
| -------- | --------------------------- | ---- | ------------------------------ |
| callback | AsyncCallback&lt;number&gt; | Yes   | Callback invoked to return the RSSI, in dBm.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**Example**

```js
// callback
try {
    let gattClient = ble.createGattClientDevice("XX:XX:XX:XX:XX:XX");
    gattClient.connect();
    let rssi = gattClient.getRssiValue((err, data)=> {
        console.info('rssi err ' + JSON.stringify(err));
        console.info('rssi value' + JSON.stringify(data));
    })
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### getRssiValue

getRssiValue(): Promise&lt;number&gt;

Obtains the RSSI of the remote BLE device. This API uses a promise to return the result. It can be used only after a connection is set up by calling [connect](#connect).

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Return value**

| Type                   | Description                               |
| --------------------- | --------------------------------- |
| Promise&lt;number&gt; | Promise used to return the RSSI, in dBm.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900099 | Operation failed.                        |

**Example**

```js
// promise
try {
    let gattClient = ble.createGattClientDevice("XX:XX:XX:XX:XX:XX");
    let rssi = gattClient.getRssiValue().then((data) => {
        console.info('rssi' + JSON.stringify(data));
    })
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### setBLEMtuSize

setBLEMtuSize(mtu: number): void

Sets the maximum transmission unit (MTU) that can be transmitted between the GATT client and its remote BLE device. This API can be used only after a connection is set up by calling [connect](#connect).

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name | Type    | Mandatory  | Description            |
| ---- | ------ | ---- | -------------- |
| mtu  | number | Yes   | MTU to set, which ranges from 22 to 512 bytes.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**Example**

```js
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.setBLEMtuSize(128);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### setCharacteristicChangeNotification

setCharacteristicChangeNotification(characteristic: BLECharacteristic, enable: boolean, callback: AsyncCallback&lt;void&gt;): void

Sets the function of notifying the GATT client when the characteristic value of the remote BLE device changes.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name           | Type                                     | Mandatory  | Description                           |
| -------------- | --------------------------------------- | ---- | ----------------------------- |
| characteristic | [BLECharacteristic](#blecharacteristic) | Yes   | BLE characteristic to listen for.                     |
| enable         | boolean                                 | Yes   | Whether to enable the notify function. The value **true** means to enable the notify function, and the value **false** means the opposite.|
| callback   | AsyncCallback&lt;void&gt; | Yes   | Callback invoked to return the result. If the operation is successful, **err** is **undefined**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**Example**

```js
// Create descriptors.
let descriptors = [];
let arrayBuffer = new ArrayBuffer(8);
let descV = new Uint8Array(arrayBuffer);
descV[0] = 11;
let descriptor = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
  descriptorUuid: '00002902-0000-1000-8000-00805F9B34FB', descriptorValue: arrayBuffer};
descriptors[0] = descriptor;
let arrayBufferC = new ArrayBuffer(8);
let characteristic = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB', characteristicValue: arrayBufferC, descriptors:descriptors};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.setCharacteristicChangeNotification(characteristic, false);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}

```


### setCharacteristicChangeNotification

setCharacteristicChangeNotification(characteristic: BLECharacteristic, enable: boolean): Promise&lt;void&gt;

Sets the function of notifying the GATT client when the characteristic value of the remote BLE device changes.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name           | Type                                     | Mandatory  | Description                           |
| -------------- | --------------------------------------- | ---- | ----------------------------- |
| characteristic | [BLECharacteristic](#blecharacteristic) | Yes   | BLE characteristic to listen for.                     |
| enable         | boolean                                 | Yes   | Whether to enable the notify function. The value **true** means to enable the notify function, and the value **false** means the opposite.|

**Return value**

| Type                                      | Description                        |
| ---------------------------------------- | -------------------------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**Example**

```js
// Create descriptors.
let descriptors = [];
let arrayBuffer = new ArrayBuffer(8);
let descV = new Uint8Array(arrayBuffer);
descV[0] = 11;
let descriptor = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
  descriptorUuid: '00002902-0000-1000-8000-00805F9B34FB', descriptorValue: arrayBuffer};
descriptors[0] = descriptor;
let arrayBufferC = new ArrayBuffer(8);
let characteristic = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB', characteristicValue: arrayBufferC, descriptors:descriptors};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.setCharacteristicChangeNotification(characteristic, false);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}

```


### setCharacteristicChangeIndication

setCharacteristicChangeIndication(characteristic: BLECharacteristic, enable: boolean, callback: AsyncCallback&lt;void&gt;): void

Sets the function of notifying the GATT client when the characteristic value of the remote BLE device changes.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name           | Type                                     | Mandatory  | Description                           |
| -------------- | --------------------------------------- | ---- | ----------------------------- |
| characteristic | [BLECharacteristic](#blecharacteristic) | Yes   | BLE characteristic to listen for.                     |
| enable         | boolean                                 | Yes   | Whether to enable the notify function. The value **true** means to enable the notify function, and the value **false** means the opposite.|
| callback   | AsyncCallback&lt;void&gt; | Yes   | Callback invoked to return the result. If the operation is successful, **err** is **undefined**. Otherwise, **err** is an error object.|

**Return value**

| Type                                      | Description                        |
| ---------------------------------------- | -------------------------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**Example**

```js
// Create descriptors.
let descriptors = [];
let arrayBuffer = new ArrayBuffer(8);
let descV = new Uint8Array(arrayBuffer);
descV[0] = 11;
let descriptor = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
  descriptorUuid: '00002902-0000-1000-8000-00805F9B34FB', descriptorValue: arrayBuffer};
descriptors[0] = descriptor;
let arrayBufferC = new ArrayBuffer(8);
let characteristic = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB', characteristicValue: arrayBufferC, descriptors:descriptors};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.setCharacteristicChangeIndication(characteristic, false);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}

```


### setCharacteristicChangeIndication

setCharacteristicChangeIndication(characteristic: BLECharacteristic, enable: boolean): Promise&lt;void&gt;

Sets the function of notifying the GATT client when the characteristic value of the remote BLE device changes.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name           | Type                                     | Mandatory  | Description                           |
| -------------- | --------------------------------------- | ---- | ----------------------------- |
| characteristic | [BLECharacteristic](#blecharacteristic) | Yes   | BLE characteristic to listen for.                     |
| enable         | boolean                                 | Yes   | Whether to enable the notify function. The value **true** means to enable the notify function, and the value **false** means the opposite.|

**Return value**

| Type                                      | Description                        |
| ---------------------------------------- | -------------------------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Bluetooth Error Codes](../errorcodes/errorcode-bluetoothManager.md).

| ID| Error Message|
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900099 | Operation failed.                        |

**Example**

```js
// Create descriptors.
let descriptors = [];
let arrayBuffer = new ArrayBuffer(8);
let descV = new Uint8Array(arrayBuffer);
descV[0] = 11;
let descriptor = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB',
  descriptorUuid: '00002902-0000-1000-8000-00805F9B34FB', descriptorValue: arrayBuffer};
descriptors[0] = descriptor;
let arrayBufferC = new ArrayBuffer(8);
let characteristic = {serviceUuid: '00001810-0000-1000-8000-00805F9B34FB',
  characteristicUuid: '00001820-0000-1000-8000-00805F9B34FB', characteristicValue: arrayBufferC, descriptors:descriptors};
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.setCharacteristicChangeIndication(characteristic, false);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}

```


### on('BLECharacteristicChange')

on(type: 'BLECharacteristicChange', callback: Callback&lt;BLECharacteristic&gt;): void

Subscribes to BLE characteristic changes. The client can receive a notification from the server only after the **setNotifyCharacteristicChanged** method is called.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                      |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | Yes   | Event type. The value **BLECharacteristicChange** indicates a characteristic value change event.|
| callback | Callback&lt;[BLECharacteristic](#blecharacteristic)&gt; | Yes   | Callback invoked to return the characteristic value changes.                 |

**Example**

```js
function CharacteristicChange(CharacteristicChangeReq) {
    let serviceUuid = CharacteristicChangeReq.serviceUuid;
    let characteristicUuid = CharacteristicChangeReq.characteristicUuid;
    let value = new Uint8Array(CharacteristicChangeReq.characteristicValue);
}
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.on('BLECharacteristicChange', CharacteristicChange);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### off('BLECharacteristicChange')

off(type: 'BLECharacteristicChange', callback?: Callback&lt;BLECharacteristic&gt;): void

Unsubscribes from BLE characteristic change events.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                      |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | Yes   | Event type. The value **BLECharacteristicChange** indicates a characteristic value change event.|
| callback | Callback&lt;[BLECharacteristic](#blecharacteristic)&gt; | No   | Callback for the characteristic value change event. If this parameter is not set, this API unsubscribes from all callbacks corresponding to **type**.|

**Example**

```js
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.off('BLECharacteristicChange');
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### on('BLEConnectionStateChange')

on(type: 'BLEConnectionStateChange', callback: Callback&lt;BLEConnectionChangeState&gt;): void

Subscribes to BLE connection state changes.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                      |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | Yes   | Event type. The value **BLEConnectionStateChange** indicates a BLE connection state change event.|
| callback | Callback&lt;[BLEConnectionChangeState](#bleconnectionchangestate)&gt; | Yes   | Callback invoked to return the BLE connection state.                          |

**Example**

```js
function ConnectStateChanged(state) {
  console.log('bluetooth connect state changed');
  let connectState = state.state;
}
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.on('BLEConnectionStateChange', ConnectStateChanged);
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### off('BLEConnectionStateChange')

off(type: 'BLEConnectionStateChange', callback?: Callback&lt;BLEConnectionChangeState&gt;): void

Unsubscribes from BLE connection state changes.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                      |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | Yes   | Event type. The value **BLEConnectionStateChange** indicates a BLE connection state change event.|
| callback | Callback&lt;[BLEConnectionChangeState](#bleconnectionchangestate)&gt; | No   | Callback for the BLE connection state change event. If this parameter is not set, this API unsubscribes from all callbacks corresponding to **type**.|

**Example**

```js
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.off('BLEConnectionStateChange');
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### on('BLEMtuChange')

on(type: 'BLEMtuChange', callback: Callback&lt;number&gt;): void

Subscribes to MTU status changes.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                      |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | Yes   | Event type. The value is **BLEMtuChange**, which indicates a MTU status change event.|
| callback | Callback&lt;number&gt; | Yes   | Callback invoked to return the MTU status, which can be connected or disconnected.|

**Example**

```js
try {
    let gattClient = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    gattClient.on('BLEMtuChange', (mtu) => {
      console.info('BLEMtuChange, mtu: ' + mtu);
    });
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


### off('BLEMtuChange')

off(type: 'BLEMtuChange', callback?: Callback&lt;number&gt;): void

Unsubscribes from MTU status changes.

**Required permissions**: ohos.permission.ACCESS_BLUETOOTH

**System capability**: SystemCapability.Communication.Bluetooth.Core

**Parameters**

| Name     | Type                                      | Mandatory  | Description                                      |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| type     | string                                   | Yes   | Event type. The value is **BLEMtuChange**, which indicates a MTU status change event.|
| callback | Callback&lt;number&gt; | No   | Callback for MTU status changes. If this parameter is not set, this API unsubscribes from all callbacks corresponding to **type**.|

**Example**

```js
try {
    let device = ble.createGattClientDevice('XX:XX:XX:XX:XX:XX');
    device.off('BLEMtuChange');
} catch (err) {
    console.error('errCode: ' + err.code + ', errMessage: ' + err.message);
}
```


## GattService

Defines the GATT service API parameters.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name             | Type                                    | Readable  | Writable  | Description                                      |
| --------------- | ---------------------------------------- | ---- | ---- | ---------------------------------------- |
| serviceUuid     | string                                   | Yes   | Yes   | UUID of the service, for example, **00001888-0000-1000-8000-00805f9b34fb**.|
| isPrimary       | boolean                                  | Yes   | Yes   | Whether the service is a primary service. The value **true** means a primary service.               |
| characteristics | Array&lt;[BLECharacteristic](#blecharacteristic)&gt; | Yes   | Yes   | List of characteristics of the service.                            |
| includeServices | Array&lt;[GattService](#gattservice)&gt; | Yes   | Yes   | Services on which the service depends.                            |


## BLECharacteristic

Defines the characteristic API parameters.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name                 | Type                                    | Readable  | Writable  | Description                                |
| ------------------- | ---------------------------------------- | ---- | ---- | ---------------------------------------- |
| serviceUuid         | string                                   | Yes   | Yes   | UUID of the service, for example, **00001888-0000-1000-8000-00805f9b34fb**.|
| characteristicUuid  | string                  | Yes   | Yes   | UUID of the characteristic, for example, **00002a11-0000-1000-8000-00805f9b34fb**.|
| characteristicValue | ArrayBuffer                              | Yes   | Yes   | Binary value of the characteristic.                     |
| descriptors         | Array&lt;[BLEDescriptor](#bledescriptor)&gt; | Yes   | Yes   | List of descriptors of the characteristic.               |
| properties  | [GattProperties](#gattproperties) |   Yes  | Yes    | Properties of the characteristic.    |


## BLEDescriptor

Defines the BLE descriptor.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name                | Type       | Readable  | Writable  | Description                                      |
| ------------------ | ----------- | ---- | ---- | ---------------------------------------- |
| serviceUuid        | string      | Yes   | Yes   | UUID of the service, for example, **00001888-0000-1000-8000-00805f9b34fb**.|
| characteristicUuid | string      | Yes   | Yes   | UUID of the characteristic, for example, **00002a11-0000-1000-8000-00805f9b34fb**.|
| descriptorUuid     | string      | Yes   | Yes   | UUID of the descriptor, for example, **00002902-0000-1000-8000-00805f9b34fb**.|
| descriptorValue    | ArrayBuffer | Yes   | Yes   | Binary value of the descriptor.                             |


## NotifyCharacteristic

Defines the parameters in the notifications sent when the server characteristic value changes.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name                 | Type       | Readable  | Writable  | Description                                      |
| ------------------- | ----------- | ---- | ---- | ---------------------------------------- |
| serviceUuid         | string      | Yes   | Yes   | UUID of the service, for example, **00001888-0000-1000-8000-00805f9b34fb**.|
| characteristicUuid  | string      | Yes   | Yes   | UUID of the characteristic, for example, **00002a11-0000-1000-8000-00805f9b34fb**.|
| characteristicValue | ArrayBuffer | Yes   | Yes   | Binary value of the characteristic.                              |
| confirm             | boolean     | Yes   | Yes   | Whether the notification needs to be confirmed by the remote end. For a notification, set it to **true**. In this case, the remote end must confirm the receipt of the notification. For an indication, set it to **false**. In this case, the remote end does not need to confirm the receipt of the notification.|


## CharacteristicReadRequest

Defines the parameters of the **CharacteristicReadReq** event received by the server.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name                | Type  | Readable  | Writable  | Description                                      |
| ------------------ | ------ | ---- | ---- | ---------------------------------------- |
| deviceId           | string | Yes   | No   | Address of the remote device that sends the **CharacteristicReadReq** event, for example, XX:XX:XX:XX:XX:XX.|
| transId            | number | Yes   | No   | Transmission ID of the read request. The response returned by the server must use the same transmission ID.      |
| offset             | number | Yes   | No   | Position from which the characteristic value is read. For example, **k** means to read from the kth byte. The response returned by the server must use the same offset.|
| characteristicUuid | string | Yes   | No   | UUID of the characteristic, for example, **00002a11-0000-1000-8000-00805f9b34fb**.|
| serviceUuid        | string | Yes   | No   | UUID of the service, for example, **00001888-0000-1000-8000-00805f9b34fb**.|


## CharacteristicWriteRequest

Defines the parameters of the **CharacteristicWriteReq** event received by the server.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name                | Type  | Readable  | Writable  | Description                                      |
| ------------------ | ------ | ---- | ---- | ---------------------------------------- |
| deviceId           | string | Yes   | No   | Address of the remote device that sends the **CharacteristicWriteReq** event, for example, XX:XX:XX:XX:XX:XX.|
| transId            | number | Yes   | No   | Transmission ID of the write request. The response returned by the server must use the same transmission ID.      |
| offset             | number | Yes   | No   | Start position for writing the characteristic value. For example, **k** means to write from the kth byte. The response returned by the server must use the same offset.|
| isPrepared             | boolean | Yes   | No   | Whether the write request is executed immediately.|
| needRsp             | boolean | Yes   | No   | Whether to send a response to the GATT client.|
| value             | ArrayBuffer | Yes   | No   | Binary value of the descriptor to write.|
| characteristicUuid | string | Yes   | No   | UUID of the characteristic, for example, **00002a11-0000-1000-8000-00805f9b34fb**.|
| serviceUuid        | string | Yes   | No   | UUID of the service, for example, **00001888-0000-1000-8000-00805f9b34fb**.|


## DescriptorReadRequest

Defines the parameters of the **DescriptorReadReq** event received by the server.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name                | Type  | Readable  | Writable  | Description                                      |
| ------------------ | ------ | ---- | ---- | ---------------------------------------- |
| deviceId           | string | Yes   | No   | Address of the remote device that sends a **DescriptorReadReq** event, for example, XX:XX:XX:XX:XX:XX.|
| transId            | number | Yes   | No   | Transmission ID of the read request. The response returned by the server must use the same transmission ID.      |
| offset             | number | Yes   | No   | Position from which the descriptor is read. For example, **k** means to read from the kth byte. The response returned by the server must use the same offset.|
| descriptorUuid     | string | Yes   | No   | UUID of the descriptor, for example, **00002902-0000-1000-8000-00805f9b34fb**.|
| characteristicUuid | string | Yes   | No   | UUID of the characteristic, for example, **00002a11-0000-1000-8000-00805f9b34fb**.|
| serviceUuid        | string | Yes   | No   | UUID of the service, for example, **00001888-0000-1000-8000-00805f9b34fb**.|


## DescriptorWriteRequest

Defines the parameters of the **DescriptorWriteReq** event received by the server.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name                | Type       | Readable  | Writable  | Description                                      |
| ------------------ | ----------- | ---- | ---- | ---------------------------------------- |
| deviceId           | string      | Yes   | No   | Address of the remote device that sends a **DescriptorWriteReq** event, for example, XX:XX:XX:XX:XX:XX.|
| transId            | number      | Yes   | No   | Transmission ID of the write request. The response returned by the server must use the same transmission ID.      |
| offset             | number      | Yes   | No   | Start position for writing the descriptor. For example, **k** means to write from the kth byte. The response returned by the server must use the same offset.|
| isPrepared             | boolean     | Yes   | No   | Whether the write request is executed immediately.                            |
| needRsp            | boolean     | Yes   | No   | Whether to send a response to the GATT client.                      |
| value              | ArrayBuffer | Yes   | No   | Binary value of the descriptor to write.                          |
| descriptorUuid     | string      | Yes   | No   | UUID of the descriptor, for example, **00002902-0000-1000-8000-00805f9b34fb**.|
| characteristicUuid | string      | Yes   | No   | UUID of the characteristic, for example, **00002a11-0000-1000-8000-00805f9b34fb**.|
| serviceUuid        | string      | Yes   | No   | UUID of the service, for example, **00001888-0000-1000-8000-00805f9b34fb**.|


## ServerResponse

Defines the parameters of the server's response to the GATT client's read/write request.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name      | Type       | Readable  | Writable  | Description                                    |
| -------- | ----------- | ---- | ---- | -------------------------------------- |
| deviceId | string      | Yes   | No   | Address of the remote device, for example, XX:XX:XX:XX:XX:XX.      |
| transId  | number      | Yes   | No   | Transmission ID of the request. The value must be the same as the ID carried in the read/write request received.       |
| status   | number      | Yes   | No   | Response state. Set this parameter to **0**, which indicates a normal response.                  |
| offset   | number      | Yes   | No   | Start read/write position. The value must be the same as the offset carried in the read/write request.|
| value    | ArrayBuffer | Yes   | No   | Binary data in the response.                         |


## BLEConnectionChangeState

Defines the parameters of **BLEConnectChangedState**.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name    | Type                                         | Readable| Writable| Description                                         |
| -------- | ------------------------------------------------- | ---- | ---- | --------------------------------------------- |
| deviceId | string                                            | Yes  | No  | Address of the remote device, for example, XX:XX:XX:XX:XX:XX.|
| state    | [ProfileConnectionState](js-apis-bluetooth-constant.md#profileconnectionstate) | Yes  | Yes  | BLE connection state.                      |


## ScanResult

Defines the scan result.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name      | Type       | Readable  | Writable  | Description                                |
| -------- | ----------- | ---- | ---- | ---------------------------------- |
| deviceId | string      | Yes   | No   | Address of the scanned device, for example, XX:XX:XX:XX:XX:XX.|
| rssi     | number      | Yes   | No   | RSSI of the device.                   |
| data     | ArrayBuffer | Yes   | No   | Advertisement packets sent by the device.                   |
| deviceName | string | Yes   | No   | Name of the device detected.                   |
| connectable  | boolean | Yes   | No   | Whether the discovered device is connectable.                   |


## AdvertiseSetting

Defines the BLE advertising parameters.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name         | Type   | Readable  | Writable  | Description                                      |
| ----------- | ------- | ---- | ---- | ---------------------------------------- |
| interval    | number  | Yes   | Yes   | Interval for BLE advertising. The minimum value is **32** slots (20 ms). The maximum value is **16384** slots. The default value is **1600** slots (1s).|
| txPower     | number  | Yes   | Yes   | Transmit power, in dBm. The value range is -127 to 1. The default value is **-7**.  |
| connectable | boolean | Yes   | Yes   | Whether the advertisement is connectable. The default value is **true**.                  |


## AdvertiseData

Defines the content of a BLE advertisement packet.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name             | Type                                    | Readable  | Writable  | Description                         |
| --------------- | ---------------------------------------- | ---- | ---- | --------------------------- |
| serviceUuids    | Array&lt;string&gt;                      | Yes   | Yes   | List of service UUIDs to broadcast.|
| manufactureData | Array&lt;[ManufactureData](#manufacturedata)&gt; | Yes   | Yes   | List of manufacturers to broadcast.          |
| serviceData     | Array&lt;[ServiceData](#servicedata)&gt; | Yes   | Yes   | List of service data to broadcast.              |
| includeDeviceName | boolean                  | Yes   | Yes   | Whether the device name is contained. This parameter is optional.       |


## ManufactureData

Defines the content of a BLE advertisement packet.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name              | Type               | Readable  | Writable  | Description                |
| ---------------- | ------------------- | ---- | ---- | ------------------ |
| manufactureId    | number  | Yes   | Yes   | Manufacturer ID allocated by the Bluetooth SIG.|
| manufactureValue | ArrayBuffer         | Yes   | Yes   | Manufacturer data.    |


## ServiceData

Defines the service data contained in an advertisement packet.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name          | Type       | Readable  | Writable  | Description        |
| ------------ | ----------- | ---- | ---- | ---------- |
| serviceUuid  | string      | Yes   | Yes   | Service UUID.|
| serviceValue | ArrayBuffer | Yes   | Yes   | Service data.   |


## ScanFilter

Defines the scan filter parameters.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name                                    | Type   | Readable| Writable| Description                                                        |
| ---------------------------------------- | ----------- | ---- | ---- | ------------------------------------------------------------ |
| deviceId                                 | string      | Yes  | Yes  | Address of the BLE device to filter, for example, XX:XX:XX:XX:XX:XX.          |
| name                                     | string      | Yes  | Yes  | Name of the BLE device to filter.                                       |
| serviceUuid                              | string      | Yes  | Yes  | Service UUID of the device to filter, for example, **00001888-0000-1000-8000-00805f9b34fb**.|
| serviceUuidMask             | string      | Yes  | Yes  | Service UUID mask of the device to filter, for example, **FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF**.|
| serviceSolicitationUuid     | string      | Yes  | Yes  | Service solicitation UUID of the device to filter, for example, **00001888-0000-1000-8000-00805F9B34FB**.|
| serviceSolicitationUuidMask | string      | Yes  | Yes  | Service solicitation UUID mask of the device to filter, for example, **FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF**.|
| serviceData                 | ArrayBuffer | Yes  | Yes  | Service data of the device to filter, for example, **[0x90, 0x00, 0xF1, 0xF2]**.|
| serviceDataMask             | ArrayBuffer | Yes  | Yes  | Service data mask of the device to filter, for example, **[0xFF,0xFF,0xFF,0xFF]**.|
| manufactureId               | number      | Yes  | Yes  | Manufacturer ID of the device to filter, for example, **0x0006**.                |
| manufactureData             | ArrayBuffer | Yes  | Yes  | Manufacturer data of the device to filter, for example, **[0x1F,0x2F,0x3F]**.|
| manufactureDataMask         | ArrayBuffer | Yes  | Yes  | Manufacturer data mask of the device to filter, for example, **[0xFF, 0xFF, 0xFF]**.|


## ScanOptions

Defines the scan configuration parameters.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name       | Type                   | Readable  | Writable  | Description                                    |
| --------- | ----------------------- | ---- | ---- | -------------------------------------- |
| interval  | number                  | Yes   | Yes   | Delay in reporting the scan result. The default value is **0**.                   |
| dutyMode  | [ScanDuty](#scanduty)   | Yes   | Yes   | Scan duty. The default value is SCAN_MODE_LOW_POWER.       |
| matchMode | [MatchMode](#matchmode) | Yes   | Yes   | Hardware filtering match mode. The default value is **MATCH_MODE_AGGRESSIVE**.|


## GattProperties<a name="GattProperties"></a>

Defines the properties of a GATT characteristic.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name      | Type | Mandatory  | Description         |
| -------- | ------ |---- | ----------- |
| write    | boolean | Yes | Permits writes of the characteristic value (with a response).|
| writeNoResponse | boolean | Yes   | Permits writes of the characteristic value (without a response).|
| read | boolean   |  Yes   | Permits reads of the characteristic value.|
| notify | boolean   | Yes   | Permits notifications of the characteristic value.|
| indicate | boolean   | Yes   | Permits notifications of the characteristic value without acknowledgement.|


## GattWriteType<a name="GattWriteType"></a>

Enumerates the GATT write types.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name                                  | Value   | Description             |
| ------------------------------------| ------ | --------------- |
| WRITE               | 1 | Write a characteristic value with a response from the peer device.  |
| WRITE_NO_RESPONSE   | 2 | Write characteristic value without a response from the peer device. |


## ScanDuty

Enumerates the scan duties.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name                   | Value | Description          |
| --------------------- | ---- | ------------ |
| SCAN_MODE_LOW_POWER   | 0    | Low-power mode, which is the default value.|
| SCAN_MODE_BALANCED    | 1    | Balanced mode.     |
| SCAN_MODE_LOW_LATENCY | 2    | Low-latency mode.    |


## MatchMode

Enumerates the hardware match modes of BLE scan filters.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name                   | Value | Description                                      |
| --------------------- | ---- | ---------------------------------------- |
| MATCH_MODE_AGGRESSIVE | 1    | Hardware reports the scan result with a lower threshold of signal strength and few number of matches in a duration. This is the default value.|
| MATCH_MODE_STICKY     | 2    | Hardware reports the scan result with a higher threshold of signal strength and sightings.      |