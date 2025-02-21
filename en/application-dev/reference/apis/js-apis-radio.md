# @ohos.telephony.radio (Network Search)

The **radio** module provides basic network search management functions. You can obtain the radio access technology (RAT) used in the CS and PS domains, network status, current network selection mode, ISO country code of the registered network, ID of the slot in which the primary card is located, list of signal strengths of the registered network, carrier name, and IMEI, MEID, and unique device ID of the SIM card in the specified slot. Besides, you can check whether the current device supports 5G\(NR\) and whether the radio service is enabled on the primary SIM card.

>**NOTE**
>
>The initial APIs of this module are supported since API version 6. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```
import radio from '@ohos.telephony.radio';
```

## radio.getRadioTech

getRadioTech\(slotId: number, callback: AsyncCallback<\{psRadioTech: RadioTechnology, csRadioTech: RadioTechnology\}\>\): void

Obtains the RAT used in the CS and PS domains for the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                                        | Mandatory| Description                                  |
| -------- | ------------------------------------------------------------ | ---- | -------------------------------------- |
| slotId   | number                                                       | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<{psRadioTech: [RadioTechnology](#radiotechnology), csRadioTech:[RadioTechnology](#radiotechnology)}\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.getRadioTech(slotId, (err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.getRadioTech

getRadioTech\(slotId: number\): Promise<\{psRadioTech: RadioTechnology, csRadioTech: RadioTechnology\}\>

Obtains the RAT used in the CS and PS domains for the SIM card in the specified slot. This API uses a promise to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type                                                        | Description                                           |
| ------------------------------------------------------------ | ----------------------------------------------- |
| Promise<{psRadioTech: [RadioTechnology](#radiotechnology), csRadioTech: [RadioTechnology](#radiotechnology)}> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
let promise = radio.getRadioTech(slotId);
promise.then(data => {
    console.log(`getRadioTech success, data->${JSON.stringify(data)}`);
}).catch(err => {
    console.log(`getRadioTech failed, err->${JSON.stringify(err)}`);
});
```


## radio.getNetworkState

getNetworkState\(callback: AsyncCallback<NetworkState\>\): void

Obtains the network status. This API uses an asynchronous callback to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                          | Mandatory| Description      |
| -------- | ---------------------------------------------- | ---- | ---------- |
| callback | AsyncCallback\<[NetworkState](#networkstate)\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
radio.getNetworkState((err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.getNetworkState

getNetworkState\(slotId: number, callback: AsyncCallback<NetworkState\>\): void

Obtains the network status. This API uses an asynchronous callback to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                          | Mandatory| Description                                  |
| -------- | ---------------------------------------------- | ---- | -------------------------------------- |
| slotId   | number                                         | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<[NetworkState](#networkstate)\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.getNetworkState(slotId, (err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.getNetworkState

getNetworkState\(slotId?: number\): Promise<NetworkState\>

Obtains the network status. This API uses a promise to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | No  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type                                    | Description                       |
| ---------------------------------------- | --------------------------- |
| Promise\<[NetworkState](#networkstate)\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
let promise = radio.getNetworkState(slotId);
promise.then(data => {
    console.log(`getNetworkState success, promise: data->${JSON.stringify(data)}`);
}).catch(err => {
    console.log(`getNetworkState failed, promise: err->${JSON.stringify(err)}`);
});
```


## radio.getNetworkSelectionMode

getNetworkSelectionMode\(slotId: number, callback: AsyncCallback<NetworkSelectionMode\>\): void

Obtains the network selection mode of the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                                        | Mandatory| Description                                  |
| -------- | ------------------------------------------------------------ | ---- | -------------------------------------- |
| slotId   | number                                                       | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<[NetworkSelectionMode](#networkselectionmode)\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.getNetworkSelectionMode(slotId, (err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.getNetworkSelectionMode

getNetworkSelectionMode\(slotId: number\): Promise<NetworkSelectionMode\>

Obtains the network selection mode of the SIM card in the specified slot. This API uses a promise to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type                                                    | Description                           |
| -------------------------------------------------------- | ------------------------------- |
| Promise\<[NetworkSelectionMode](#networkselectionmode)\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
let promise = radio.getNetworkSelectionMode(slotId);
promise.then(data => {
    console.log(`getNetworkSelectionMode success, promise: data->${JSON.stringify(data)}`);
}).catch(err => {
    console.log(`getNetworkSelectionMode failed, promise: err->${JSON.stringify(err)}`);
});
```


## radio.getISOCountryCodeForNetwork<sup>7+</sup>

getISOCountryCodeForNetwork\(slotId: number, callback: AsyncCallback<string\>\): void

Obtains the ISO country code of the network with which the SIM card in the specified slot is registered. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                   | Mandatory| Description                                    |
| -------- | ----------------------- | ---- | ---------------------------------------- |
| slotId   | number                  | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2  |
| callback | AsyncCallback\<string\> | Yes  | Callback used to return the result, which is an ISO country code, for example, **CN** (China).|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.getISOCountryCodeForNetwork(slotId, (err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.getISOCountryCodeForNetwork<sup>7+</sup>

getISOCountryCodeForNetwork\(slotId: number\): Promise<string\>

Obtains the ISO country code of the network with which the SIM card in the specified slot is registered. This API uses a promise to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type             | Description                                                        |
| ----------------- | ------------------------------------------------------------ |
| Promise\<string\> | Promise used to return the result, which is an ISO country code, for example, **CN** (China).|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
let promise = radio.getISOCountryCodeForNetwork(slotId);
promise.then(data => {
    console.log(`getISOCountryCodeForNetwork success, promise: data->${JSON.stringify(data)}`);
}).catch(err => {
    console.log(`getISOCountryCodeForNetwork failed, promise: err->${JSON.stringify(err)}`);
});
```


## radio.getPrimarySlotId<sup>7+</sup>

getPrimarySlotId\(callback: AsyncCallback\<number\>\): void

Obtains the ID of the slot in which the primary card is located. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                                        | Mandatory| Description                                                        |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback\<number\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
radio.getPrimarySlotId((err, data) => {
   console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.getPrimarySlotId<sup>7+</sup>

getPrimarySlotId\(\): Promise\<number\>

Obtains the ID of the slot in which the primary card is located. This API uses a promise to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Return value**

| Type                                                       | Description                                                        |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<number\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let promise = radio.getPrimarySlotId();
promise.then(data => {
    console.log(`getPrimarySlotId success, promise: data->${JSON.stringify(data)}`);
}).catch(err => {
    console.error(`getPrimarySlotId failed, promise: err->${JSON.stringify(err)}`);
});
```


## radio.getSignalInformation<sup>7+</sup>

getSignalInformation\(slotId: number, callback: AsyncCallback<Array<SignalInformation\>\>\): void

Obtains a list of signal strengths of the network with which the SIM card in the specified slot is registered. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                                        | Mandatory| Description                                                        |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| slotId   | number                                                       | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2                      |
| callback | AsyncCallback\<Array\<[SignalInformation](#signalinformation)\>\> | Yes  | Callback used to return the result, which is a list of [SignalInformation](#signalinformation) objects.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.getSignalInformation(slotId, (err, data) => {
   console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.getSignalInformation<sup>7+</sup>

getSignalInformation\(slotId: number\): Promise<Array<SignalInformation\>\>

Obtains a list of signal strengths of the network with which the SIM card in the specified slot is registered. This API uses a promise to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type                                                       | Description                                                        |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<Array\<[SignalInformation](#signalinformation)\>\> | Promise used to return the result, which is a list of [SignalInformation](#signalinformation) objects.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
let promise = radio.getSignalInformation(slotId);
promise.then(data => {
    console.log(`getSignalInformation success, promise: data->${JSON.stringify(data)}`);
}).catch(err => {
    console.error(`getSignalInformation failed, promise: err->${JSON.stringify(err)}`);
});
```

## radio.isNrSupported<sup>(deprecated)</sup>

isNrSupported\(\): boolean

Checks whether the current device supports 5G \(NR\).

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [isNRSupported](#radioisnrsupported9) instead.

**System capability**: SystemCapability.Telephony.CoreService

**Return value**

| Type   | Description                            |
| ------- | -------------------------------- |
| boolean | - **true**: The current device supports 5G \(NR\).<br>- **false**: The current device does not support 5G \(NR\).|

**Example**

```js
let result = radio.isNrSupported();
console.log("Result: "+ result);
```

## radio.isNrSupported<sup>(deprecated)</sup>

isNrSupported\(slotId: number\): boolean

Checks whether the current device supports 5G \(NR\).

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [isNRSupported](#radioisnrsupported9-1) instead.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type              | Description                                                        |
| ------------------ | ------------------------------------------------------------ |
| boolean | - **true**: The current device supports 5G \(NR\).<br>- **false**: The current device does not support 5G \(NR\).|

**Example**

```js
let slotId = 0;
let result = radio.isNrSupported(slotId);
console.log("Result: "+ result);
```


## radio.isNRSupported<sup>9+</sup>

isNRSupported\(\): boolean

Checks whether the current device supports 5G \(NR\).

**System capability**: SystemCapability.Telephony.CoreService

**Return value**

| Type   | Description                            |
| ------- | -------------------------------- |
| boolean | - **true**: The current device supports 5G \(NR\).<br>- **false**: The current device does not support 5G \(NR\).|

**Example**

```js
let result = radio.isNRSupported();
console.log("Result: "+ result);
```


## radio.isNRSupported<sup>9+</sup>

isNRSupported\(slotId: number\): boolean

Checks whether the current device supports 5G \(NR\).

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type              | Description                                                        |
| ------------------ | ------------------------------------------------------------ |
| boolean | - **true**: The current device supports 5G \(NR\).<br>- **false**: The current device does not support 5G \(NR\).|

**Example**

```js
let slotId = 0;
let result = radio.isNRSupported(slotId);
console.log("Result: "+ result);
```


## radio.isRadioOn<sup>7+</sup>

isRadioOn\(callback: AsyncCallback<boolean\>\): void

Checks whether the radio service is enabled on the primary SIM card. This API uses an asynchronous callback to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                    | Mandatory| Description                                                   |
| -------- | ------------------------ | ---- | ------------------------------------------------------- |
| callback | AsyncCallback\<boolean\> | Yes  | Callback used to return the result.<br>- **true**: The radio service is enabled.<br>- **false**: The radio service is disabled.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
radio.isRadioOn((err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.isRadioOn<sup>7+</sup>

isRadioOn\(slotId: number, callback: AsyncCallback<boolean\>\): void

Checks whether the radio service is enabled on the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                    | Mandatory| Description                                                   |
| -------- | ------------------------ | ---- | ------------------------------------------------------- |
| slotId   | number                   | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2                 |
| callback | AsyncCallback\<boolean\> | Yes  | Callback used to return the result.<br>- **true**: The radio service is enabled.<br>- **false**: The radio service is disabled.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.isRadioOn(slotId, (err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.isRadioOn<sup>7+</sup>

isRadioOn\(slotId?: number\): Promise<boolean\>

Checks whether the radio service is enabled on the SIM card in the specified slot. This API uses a promise to return the result.

**Required permission**: ohos.permission.GET_NETWORK_INFO

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | No  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2<br>If the slot ID is not specified, this API is defaulted to check whether the radio service is enabled on the primary SIM card.|

**Return value**

| Type              | Description                                                        |
| ------------------ | ------------------------------------------------------------ |
| Promise\<boolean\> | Promise used to return the result.<br>- **true**: The radio service is enabled.<br>- **false**: The radio service is disabled.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
let promise = radio.isRadioOn(slotId);
promise.then(data => {
    console.log(`isRadioOn success, promise: data->${JSON.stringify(data)}`);
}).catch(err => {
    console.error(`isRadioOn failed, promise: err->${JSON.stringify(err)}`);
});
```


## radio.getOperatorName<sup>7+</sup>

getOperatorName\(slotId: number, callback: AsyncCallback<string\>\): void

Obtains the carrier name for the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                   | Mandatory| Description                                      |
| -------- | ----------------------- | ---- | ------------------------------------------ |
| slotId   | number                  | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2    |
| callback | AsyncCallback\<string\> | Yes  | Callback used to return the result, which is the carrier name, for example, China Mobile.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.getOperatorName(slotId, (err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.getOperatorName<sup>7+</sup>

getOperatorName\(slotId: number\): Promise<string\>

Obtains the carrier name for the SIM card in the specified slot. This API uses a promise to return the result.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type             | Description                                                        |
| ----------------- | ------------------------------------------------------------ |
| Promise\<string\> | Promise used t return the result, which is the carrier name, for example, China Mobile.               |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
let promise = radio.getOperatorName(slotId);
promise.then(data => {
    console.log(`getOperatorName success, promise: data->${JSON.stringify(data)}`);
}).catch(err => {
    console.log(`getOperatorName failed, promise: err->${JSON.stringify(err)}`);
});
```

## radio.setPrimarySlotId<sup>8+</sup>

setPrimarySlotId(slotId: number, callback: AsyncCallback<void\>): void

Sets the ID of the slot in which the primary card is located. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                 | Mandatory| Description                                  |
| -------- | --------------------- | ---- | -------------------------------------- |
| slotId   | number                | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.setPrimarySlotId(slotId, (err) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```


## radio.setPrimarySlotId<sup>8+</sup>

setPrimarySlotId\(slotId: number\): Promise\<void\>

Sets the ID of the slot in which the primary card is located. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type           | Description                           |
| --------------- | ------------------------------- |
| Promise\<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
let promise = radio.setPrimarySlotId(slotId);
promise.then(() => {
    console.log(`setPrimarySlotId success.`);
}).catch((err) => {
    console.log(`setPrimarySlotId failed, promise: err->${JSON.stringify(err)}`);
});
```

## radio.getIMEI<sup>8+</sup>

getIMEI(callback: AsyncCallback<string\>): void

Obtains the IMEI of the SIM card in a card slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                   | Mandatory| Description                                      |
| -------- | ----------------------- | ---- | ------------------------------------------ |
| callback | AsyncCallback\<string\> | Yes  | Callback used to return the result. If the IMEI does not exist, an empty string is returned.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
radio.getIMEI((err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.getIMEI<sup>8+</sup>

getIMEI(slotId: number, callback: AsyncCallback<string\>): void

Obtains the IMEI of the SIM card in a card slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                   | Mandatory| Description                                      |
| -------- | ----------------------- | ---- | ------------------------------------------ |
| slotId   | number                  | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2    |
| callback | AsyncCallback\<string\> | Yes  | Callback used to return the result. If the IMEI does not exist, an empty string is returned.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.getIMEI(slotId, (err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.getIMEI<sup>8+</sup>

getIMEI(slotId?: number): Promise<string\>

Obtains the IMEI of the SIM card in the specified card slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | No  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type             | Description                                      |
| ----------------- | ------------------------------------------ |
| Promise\<string\> | Promise used to return the result. If the IMEI does not exist, an empty string is returned.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
let promise = radio.getIMEI(slotId);
promise.then(data => {
    console.log(`getIMEI success, promise: data->${JSON.stringify(data)}`);
}).catch(err => {
    console.error(`getIMEI failed, promise: err->${JSON.stringify(err)}`);
});
```

## radio.getMEID<sup>8+</sup>

getMEID(callback: AsyncCallback<string\>): void

Obtains the MEID of the SIM card in a card slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                   | Mandatory| Description      |
| -------- | ----------------------- | ---- | ---------- |
| callback | AsyncCallback\<string\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
radio.getMEID((err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.getMEID<sup>8+</sup>

getMEID(slotId: number, callback: AsyncCallback<string\>): void

Obtains the MEID of the SIM card in a card slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                   | Mandatory| Description                                  |
| -------- | ----------------------- | ---- | -------------------------------------- |
| slotId   | number                  | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<string\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.getMEID(slotId, (err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.getMEID<sup>8+</sup>

getMEID(slotId?: number): Promise<string\>

Obtains the MEID of the SIM card in the specified card slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | No  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type             | Description                                   |
| ----------------- | --------------------------------------- |
| Promise\<string\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
let promise = radio.getMEID(slotId);
promise.then(data => {
    console.log(`getMEID success, promise: data->${JSON.stringify(data)}`);
}).catch(err => {
    console.error(`getMEID failed, promise: err->${JSON.stringify(err)}`);
});
```

## radio.getUniqueDeviceId<sup>8+</sup>

getUniqueDeviceId(callback: AsyncCallback<string\>): void

Obtains the unique device ID of the SIM card in a card slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                   | Mandatory| Description      |
| -------- | ----------------------- | ---- | ---------- |
| callback | AsyncCallback\<string\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
radio.getUniqueDeviceId((err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.getUniqueDeviceId<sup>8+</sup>

getUniqueDeviceId(slotId: number, callback: AsyncCallback<string\>): void

Obtains the unique device ID of the SIM card in a card slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                   | Mandatory| Description                                  |
| -------- | ----------------------- | ---- | -------------------------------------- |
| slotId   | number                  | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<string\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.getUniqueDeviceId(slotId, (err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.getUniqueDeviceId<sup>8+</sup>

getUniqueDeviceId(slotId?: number): Promise<string\>

Obtains the unique device ID of the SIM card in the specified card slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | No  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type             | Description                                         |
| ----------------- | --------------------------------------------- |
| Promise\<string\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
let promise = radio.getUniqueDeviceId(slotId);
promise.then(data => {
    console.log(`getUniqueDeviceId success, promise: data->${JSON.stringify(data)}`);
}).catch(err => {
    console.error(`getUniqueDeviceId failed, promise: err->${JSON.stringify(err)}`);
});
```

## radio.sendUpdateCellLocationRequest<sup>8+</sup>

sendUpdateCellLocationRequest\(callback: AsyncCallback<void\>\): void

Sends a cell location update request. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.LOCATION and ohos.permission.APPROXIMATELY_LOCATION

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                 | Mandatory| Description      |
| -------- | --------------------- | ---- | ---------- |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
radio.sendUpdateCellLocationRequest((err) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```

## radio.sendUpdateCellLocationRequest<sup>8+</sup>

sendUpdateCellLocationRequest\(slotId: number, callback: AsyncCallback<void\>\): void

Sends a cell location update request. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.LOCATION and ohos.permission.APPROXIMATELY_LOCATION

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                 | Mandatory| Description      |
| -------- | --------------------- | ---- | ---------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.sendUpdateCellLocationRequest(slotId, (err) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```

## radio.sendUpdateCellLocationRequest<sup>8+</sup>

sendUpdateCellLocationRequest\(slotId?: number): Promise<void\>

Sends a cell location update request for the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.LOCATION and ohos.permission.APPROXIMATELY_LOCATION

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | No  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type           | Description                   |
| --------------- | ----------------------- |
| Promise\<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.sendUpdateCellLocationRequest(slotId).then(() => {
    console.log(`sendUpdateCellLocationRequest success.`);
}).catch((err) => {
    console.log(`sendUpdateCellLocationRequest failed, promise: err->${JSON.stringify(err)}`);
});
```

## radio.getCellInformation<sup>8+</sup>

getCellInformation(callback: AsyncCallback<Array<CellInformation\>>): void

Obtains cell information. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.LOCATION and ohos.permission.APPROXIMATELY_LOCATION

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                                        | Mandatory| Description                    |
| -------- | ------------------------------------------------------------ | ---- | ------------------------ |
| callback | AsyncCallback\<Array<[CellInformation](#cellinformation8)\>\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
radio.getCellInformation((err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.getCellInformation<sup>8+</sup>

getCellInformation(slotId: number, callback: AsyncCallback<Array<CellInformation\>\>): void

Obtains cell information. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.LOCATION and ohos.permission.APPROXIMATELY_LOCATION

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                                        | Mandatory| Description                                  |
| -------- | ------------------------------------------------------------ | ---- | -------------------------------------- |
| slotId   | number                                                       | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<Array<[CellInformation](#cellinformation8)\>\> | Yes  | Callback used to return the result.              |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.getCellInformation(slotId, (err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.getCellInformation<sup>8+</sup>

getCellInformation(slotId?: number): Promise<Array<CellInformation\>\>

Obtains cell information for the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.LOCATION and ohos.permission.APPROXIMATELY_LOCATION

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | No  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type                                                   | Description                   |
| ------------------------------------------------------- | ----------------------- |
| Promise\<Array<[CellInformation](#cellinformation8)\>\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
let promise = radio.getCellInformation(slotId);
promise.then(data => {
    console.log(`getCellInformation success, promise: data->${JSON.stringify(data)}`);
}).catch(err => {
    console.error(`getCellInformation failed, promise: err->${JSON.stringify(err)}`);
});
```

## radio.setNetworkSelectionMode

setNetworkSelectionMode\(options: NetworkSelectionModeOptions, callback: AsyncCallback<void\>\): void

Sets the network selection mode. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                                       | Mandatory| Description              |
| -------- | ----------------------------------------------------------- | ---- | ------------------ |
| options  | [NetworkSelectionModeOptions](#networkselectionmodeoptions) | Yes  | Network selection mode.|
| callback | AsyncCallback\<void\>                                       | Yes  | Callback used to return the result.        |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let networkInformation={
    operatorName: "China Mobile",
    operatorNumeric: "898600",
    state: radio.NetworkInformationState.NETWORK_AVAILABLE,
    radioTech: "CS"
}
let networkSelectionModeOptions={
    slotId: 0,
    selectMode: radio.NetworkSelectionMode.NETWORK_SELECTION_AUTOMATIC,
    networkInformation: networkInformation,
    resumeSelection: true
}
radio.setNetworkSelectionMode(networkSelectionModeOptions, (err) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```

## radio.setNetworkSelectionMode

setNetworkSelectionMode\(options: NetworkSelectionModeOptions\): Promise<void\>

Sets the network selection mode. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name | Type                                                       | Mandatory| Description              |
| ------- | ----------------------------------------------------------- | ---- | ------------------ |
| options | [NetworkSelectionModeOptions](#networkselectionmodeoptions) | Yes  | Network selection mode.|

**Return value**

| Type           | Description                   |
| --------------- | ----------------------- |
| Promise\<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let networkInformation={
    operatorName: "China Mobile",
    operatorNumeric: "898600",
    state: radio.NetworkInformationState.NETWORK_AVAILABLE,
    radioTech: "CS"
}
let networkSelectionModeOptions={
    slotId: 0,
    selectMode: radio.NetworkSelectionMode.NETWORK_SELECTION_AUTOMATIC,
    networkInformation: networkInformation,
    resumeSelection: true
}
let promise = radio.setNetworkSelectionMode(networkSelectionModeOptions);
promise.then(() => {
    console.log(`setNetworkSelectionMode success.`);
}).catch((err) => {
    console.log(`setNetworkSelectionMode failed, promise: err->${JSON.stringify(err)}`);
});
```

## radio.getNetworkSearchInformation

getNetworkSearchInformation\(slotId: number, callback: AsyncCallback<NetworkSearchResult\>\): void

Obtains network search information for the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                                        | Mandatory| Description                                  |
| -------- | ------------------------------------------------------------ | ---- | -------------------------------------- |
| slotId   | number                                                       | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<[NetworkSearchResult](#networksearchresult)\> | Yes  | Callback used to return the result.          |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
radio.getNetworkSearchInformation(0, (err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```

## radio.getNetworkSearchInformation

getNetworkSearchInformation\(slotId: number\): Promise<NetworkSearchResult\>

Obtains network search information for the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type                                                  | Description                   |
| ------------------------------------------------------ | ----------------------- |
| Promise\<[NetworkSearchResult](#networksearchresult)\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let promise = radio.getNetworkSearchInformation(0);
promise.then(data => {
    console.log(`getNetworkSearchInformation success, promise: data->${JSON.stringify(data)}`);
}).catch(err => {
    console.log(`getNetworkSearchInformation failed, promise: err->${JSON.stringify(err)}`);
});
```

## radio.getNrOptionMode<sup>8+</sup>

getNrOptionMode(callback: AsyncCallback<NrOptionMode\>): void

Obtains the NR option mode. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                           | Mandatory| Description      |
| -------- | ----------------------------------------------- | ---- | ---------- |
| callback | AsyncCallback\<[NrOptionMode](#nroptionmode8)\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
radio.getNrOptionMode((err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.getNrOptionMode<sup>8+</sup>

getNrOptionMode(slotId: number, callback: AsyncCallback<NrOptionMode\>): void

Obtains the NR option mode. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                           | Mandatory| Description                                  |
| -------- | ----------------------------------------------- | ---- | -------------------------------------- |
| slotId   | number                                          | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<[NrOptionMode](#nroptionmode8)\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.getNrOptionMode(slotId, (err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```


## radio.getNrOptionMode<sup>8+</sup>

getNrOptionMode(slotId?: number): Promise<NrOptionMode\>

Obtains the NR option mode for the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | No  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type                                     | Description                   |
| ----------------------------------------- | ----------------------- |
| Promise\<[NrOptionMode](#nroptionmode8)\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
let promise = radio.getNrOptionMode(slotId);
promise.then(data => {
    console.log(`getNrOptionMode success, promise: data->${JSON.stringify(data)}`);
}).catch(err => {
    console.error(`getNrOptionMode failed, promise: err->${JSON.stringify(err)}`);
});
```

## radio.turnOnRadio<sup>7+</sup>

turnOnRadio(callback: AsyncCallback<void\>): void

Turns on the radio function. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                 | Mandatory| Description      |
| -------- | --------------------- | ---- | ---------- |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
radio.turnOnRadio((err) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```


## radio.turnOnRadio<sup>7+</sup>

turnOnRadio(slotId: number, callback: AsyncCallback<void\>): void

Turns on the radio function. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                 | Mandatory| Description                                  |
| -------- | --------------------- | ---- | -------------------------------------- |
| slotId   | number                | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.turnOnRadio(slotId, (err) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```


## radio.turnOnRadio<sup>7+</sup>

turnOnRadio(slotId?: number): Promise<void\>

Turns on the radio function for the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | No  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type           | Description                   |
| --------------- | ----------------------- |
| Promise\<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.turnOnRadio(slotId).then(() => {
    console.log(`turnOnRadio success.`);
}).catch((err) => {
    console.error(`turnOnRadio failed, promise: err->${JSON.stringify(err)}`);
});
```

## radio.turnOffRadio<sup>7+</sup>

turnOffRadio(callback: AsyncCallback<void\>): void

Turns off the radio function. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                 | Mandatory| Description      |
| -------- | --------------------- | ---- | ---------- |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
radio.turnOffRadio((err) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```


## radio.turnOffRadio<sup>7+</sup>

turnOffRadio(slotId: number, callback: AsyncCallback<void\>): void

Turns off the radio function. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                 | Mandatory| Description                                  |
| -------- | --------------------- | ---- | -------------------------------------- |
| slotId   | number                | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.turnOffRadio(slotId, (err) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```


## radio.turnOffRadio<sup>7+</sup>

turnOffRadio(slotId?: number): Promise<void\>

Turns off the radio function for the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | No  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type           | Description                   |
| --------------- | ----------------------- |
| Promise\<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.turnOffRadio(slotId).then(() => {
    console.log(`turnOffRadio success.`);
}).catch((err) => {
    console.error(`turnOffRadio failed, promise: err->${JSON.stringify(err)}`);
});
```

## radio.setPreferredNetwork<sup>8+</sup>

setPreferredNetwork\(slotId: number, networkMode: PreferredNetworkMode, callback: AsyncCallback<void\>\): void

Sets the preferred network for the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name     | Type                                          | Mandatory| Description                                  |
| ----------- | ---------------------------------------------- | ---- | -------------------------------------- |
| slotId      | number                                         | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| networkMode | [PreferredNetworkMode](#preferrednetworkmode8) | Yes  | Preferred network mode.                      |
| callback    | AsyncCallback\<void\>                          | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.setPreferredNetwork(slotId, radio.PreferredNetworkMode.PREFERRED_NETWORK_MODE_GSM, (err) => {
    console.log(`callback: err->${JSON.stringify(err)}`);
});
```

## radio.setPreferredNetwork<sup>8+</sup>

setPreferredNetwork(slotId: number, networkMode: PreferredNetworkMode): Promise<void\>

Sets the preferred network for the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name     | Type                                          | Mandatory| Description                                  |
| ----------- | ---------------------------------------------- | ---- | -------------------------------------- |
| slotId      | number                                         | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| networkMode | [PreferredNetworkMode](#preferrednetworkmode8) | Yes  | Preferred network mode.                      |

**Return value**

| Type           | Description                   |
| --------------- | ----------------------- |
| Promise\<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let slotId = 0;
radio.setPreferredNetwork(slotId, radio.PreferredNetworkMode.PREFERRED_NETWORK_MODE_GSM).then(() => {
    console.log(`setPreferredNetwork success.`);
}).catch((err) => {
    console.log(`setPreferredNetwork failed, promise: err->${JSON.stringify(err)}`);
});
```

## radio.getPreferredNetwork<sup>8+</sup>

getPreferredNetwork\(slotId: number, callback: AsyncCallback<PreferredNetworkMode\>\): void

Obtains the preferred network for the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  |                              Type                              | Mandatory| Description                                  |
| -------- | --------------------------------------------------------------- | ---- | -------------------------------------- |
| slotId   | number                                                          | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| callback | AsyncCallback\<[PreferredNetworkMode](#preferrednetworkmode8)\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
radio.getPreferredNetwork(0, (err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```

## radio.getPreferredNetwork<sup>8+</sup>

getPreferredNetwork(slotId: number): Promise<PreferredNetworkMode\>

Obtains the preferred network for the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|

**Return value**

| Type           | Description                   |
| --------------- | ----------------------- |
| Promise\<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let promise = radio.getPreferredNetwork(0);
promise.then(data => {
    console.log(`getPreferredNetwork success, promise: data->${JSON.stringify(data)}`);
}).catch(err => {
    console.log(`getPreferredNetwork failed, promise: err->${JSON.stringify(err)}`);
});
```

## radio.getImsRegInfo<sup>9+</sup>

getImsRegInfo(slotId: number, imsType: ImsServiceType, callback: AsyncCallback<ImsRegInfo\>): void

Obtains the IMS registration status of the specified IMS service type for the SIM card in the specified slot. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                      | Mandatory| Description                                  |
| -------- | ------------------------------------------ | ---- | -------------------------------------- |
| slotId   | number                                     | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| imsType  | [ImsServiceType](#imsservicetype9)         | Yes  | IMS service type.                         |
| callback | AsyncCallback<[ImsRegInfo](#imsreginfo9)\> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
radio.getImsRegInfo(0, radio.ImsServiceType.TYPE_VIDEO, (err, data) => {
    console.log(`callback: err->${JSON.stringify(err)}, data->${JSON.stringify(data)}`);
});
```

## radio.getImsRegInfo<sup>9+</sup>

getImsRegInfo(slotId: number, imsType: ImsServiceType): Promise<ImsRegInfo\>

Obtains the IMS registration status of the specified IMS service type for the SIM card in the specified slot. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name | Type                              | Mandatory| Description                                  |
| ------- | ---------------------------------- | ---- | -------------------------------------- |
| slotId  | number                             | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| imsType | [ImsServiceType](#imsservicetype9) | Yes  | IMS service type.                         |

**Return value**

| Type                                 | Description                   |
| ------------------------------------- | ----------------------- |
| Promise\<[ImsRegInfo](#imsreginfo9)\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
let promise = radio.getImsRegInfo(0, radio.ImsServiceType.TYPE_VIDEO);
promise.then(data => {
    console.log(`getImsRegInfo success, promise: data->${JSON.stringify(data)}`);
}).catch(err => {
    console.log(`getImsRegInfo failed, promise: err->${JSON.stringify(err)}`);
});
```

## radio.on('imsRegStateChange')<sup>9+</sup>

on(type: 'imsRegStateChange', slotId: number, imsType: ImsServiceType, callback: Callback<ImsRegInfo\>): void

Enables listening for **imsRegStateChange** events. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                | Mandatory| Description                                  |
| -------- | ------------------------------------ | ---- | -------------------------------------- |
| type     | string                               | Yes  | IMS registration status changes.               |
| slotId   | number                               | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| imsType  | [ImsServiceType](#imsservicetype9)   | Yes  | IMS service type.                         |
| callback | Callback<[ImsRegInfo](#imsreginfo9)> | Yes  | Callback used to return the result.                            |

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
radio.on('imsRegStateChange', 0, radio.ImsServiceType.TYPE_VIDEO, data => {
    console.log(`callback: data->${JSON.stringify(data)}`);
});
```

## radio.off('imsRegStateChange')<sup>9+</sup>

off(type: 'imsRegStateChange', slotId: number, imsType: ImsServiceType, callback?: Callback<ImsRegInfo\>): void

Disables listening for **imsRegStateChange** events. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permission**: ohos.permission.GET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CoreService

**Parameters**

| Name  | Type                                | Mandatory| Description                                  |
| -------- | ------------------------------------ | ---- | -------------------------------------- |
| type     | string                               | Yes  | IMS registration status changes.    |
| slotId   | number                               | Yes  | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| imsType  | [ImsServiceType](#imsservicetype9)   | Yes  | IMS service type.                         |
| callback | Callback<[ImsRegInfo](#imsreginfo9)> | No  | Callback used to return the result. If this parameter is not set, the API unsubscribes from all callbacks.|

**Error codes**

For details about the error codes, see [Telephony Error Codes](../../reference/errorcodes/errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```js
radio.off('imsRegStateChange', 0, radio.ImsServiceType.TYPE_VIDEO, data => {
    console.log(`callback: data->${JSON.stringify(data)}`);
});
```

## RadioTechnology

 Enumerates radio access technologies.

**System capability**: SystemCapability.Telephony.CoreService

| Name                     | Value  | Description                                                        |
| ------------------------- | ---- | ------------------------------------------------------------ |
| RADIO_TECHNOLOGY_UNKNOWN  | 0    | Unknown RAT                                   |
| RADIO_TECHNOLOGY_GSM      | 1    | Global System for Mobile Communication (GSM) |
| RADIO_TECHNOLOGY_1XRTT    | 2    | Single-Carrier Radio Transmission Technology (1XRTT)|
| RADIO_TECHNOLOGY_WCDMA    | 3    | Wideband Code Division Multiple Access (WCDMA)|
| RADIO_TECHNOLOGY_HSPA     | 4    | High Speed Packet Access (HSPA)              |
| RADIO_TECHNOLOGY_HSPAP    | 5    | Evolved High Speed Packet Access (HSPA+)    |
| RADIO_TECHNOLOGY_TD_SCDMA | 6    | Time Division Synchronous Code Division Multiple Access (TD-SCDMA)|
| RADIO_TECHNOLOGY_EVDO     | 7    | Evolution-Data Optimized (EVDO)                  |
| RADIO_TECHNOLOGY_EHRPD    | 8    | Evolved High Rate Package Data (EHRPD)       |
| RADIO_TECHNOLOGY_LTE      | 9    | Long Term Evolution (LTE)                    |
| RADIO_TECHNOLOGY_LTE_CA   | 10   | Long Term Evolution_Carrier Aggregation (LTE_CA)|
| RADIO_TECHNOLOGY_IWLAN    | 11   | Industrial Wireless LAN (IWLAN)              |
| RADIO_TECHNOLOGY_NR       | 12   | New Radio (NR)                               |


## SignalInformation

Defines the signal strength.

**System capability**: SystemCapability.Telephony.CoreService

|      Name      |           Type             | Mandatory|      Description         |
| --------------- | --------------------------- | ---- | ------------------ |
| signalType      | [NetworkType](#networktype) | Yes  | Signal strength type.|
| signalLevel     | number                      | Yes  | Signal strength level.|
| dBm<sup>9+</sup>| number                      | Yes  | Signal strength, in dBm.    |

## NetworkType

Enumerates network types.

**System capability**: SystemCapability.Telephony.CoreService

| Name                | Value  | Description                                                        |
| -------------------- | ---- | ------------------------------------------------------------ |
| NETWORK_TYPE_UNKNOWN | 0    | Unknown network.                                              |
| NETWORK_TYPE_GSM     | 1    | GSM network.   |
| NETWORK_TYPE_CDMA    | 2    | CDMA network.           |
| NETWORK_TYPE_WCDMA   | 3    | WCDMA network. |
| NETWORK_TYPE_TDSCDMA | 4    | TD-SCDMA network.|
| NETWORK_TYPE_LTE     | 5    | LTE network.                      |
| NETWORK_TYPE_NR      | 6    | 5G NR network.                              |

## NetworkState

Defines the network status.

**System capability**: SystemCapability.Telephony.CoreService

|       Name          |                 Type               | Mandatory|                          Description                               |
| -------------------- | ----------------------------------- | ---- | ------------------------------------------------------------ |
| longOperatorName     | string                              |  Yes | Long carrier name of the registered network.                                    |
| shortOperatorName    | string                              |  Yes | Short carrier name of the registered network.                                    |
| plmnNumeric          | string                              |  Yes | PLMN code of the registered network.                                          |
| isRoaming            | boolean                             |  Yes | Whether the user is roaming.                                          |
| regState             | [RegState](#regstate)               |  Yes | Network registration status of the device.                                        |
| cfgTech<sup>8+</sup> | [RadioTechnology](#radiotechnology) |  Yes | RAT of the device.                                        |
| nsaState             | [NsaState](#nsastate)               |  Yes | NSA network registration status of the device.                                     |
| isCaActive           | boolean                             |  Yes | CA status.                                                  |
| isEmergency          | boolean                             |  Yes | Whether only emergency calls are allowed.                              |


## RegState

Defines the network status.

**System capability**: SystemCapability.Telephony.CoreService

| Name                         | Value  | Description                      |
| ----------------------------- | ---- | -------------------------- |
| REG_STATE_NO_SERVICE          | 0    | The device cannot use any services, including data, SMS, and call services.    |
| REG_STATE_IN_SERVICE          | 1    | The device can use services properly, including data, SMS, and call services.    |
| REG_STATE_EMERGENCY_CALL_ONLY | 2    | The device can use only the emergency call service.|
| REG_STATE_POWER_OFF           | 3    | The device cannot communicate with the network because the cellular radio service is disabled or the modem is powered off.     |


## NsaState

Enumerates NSA network states.

**System capability**: SystemCapability.Telephony.CoreService

| Name                      | Value  | Description                                                      |
| -------------------------- | ---- | ---------------------------------------------------------- |
| NSA_STATE_NOT_SUPPORT      | 1    | The device is in idle or connected state in an LTE cell that does not support NSA.        |
| NSA_STATE_NO_DETECT        | 2    | The device is in the idle state in an LTE cell that supports NSA but not NR coverage detection.|
| NSA_STATE_CONNECTED_DETECT | 3    | The device is connected to the LTE network in an LTE cell that supports NSA and NR coverage detection.         |
| NSA_STATE_IDLE_DETECT      | 4    | The device is in the idle state in an LTE cell that supports NSA and NR coverage detection.          |
| NSA_STATE_DUAL_CONNECTED   | 5    | The device is connected to the LTE/NR network in an LTE cell that supports NSA.              |
| NSA_STATE_SA_ATTACHED      | 6    | The device is idle or connected to the NG-RAN cell when being attached to the 5G Core.     |


## NetworkSelectionMode

Enumerates network selection modes.

**System capability**: SystemCapability.Telephony.CoreService

| Name                       | Value  | Description          |
| --------------------------- | ---- | -------------- |
| NETWORK_SELECTION_UNKNOWN   | 0    | Unknown network selection mode.|
| NETWORK_SELECTION_AUTOMATIC | 1    | Automatic network selection mode.|
| NETWORK_SELECTION_MANUAL    | 2    | Manual network selection mode.|

## PreferredNetworkMode<sup>8+</sup>

Enumerates preferred network modes.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name                                                     | Value  | Description                                         |
| --------------------------------------------------------- | ---- | --------------------------------------------- |
| PREFERRED_NETWORK_MODE_GSM                                | 1    | GSM network mode.                            |
| PREFERRED_NETWORK_MODE_WCDMA                              | 2    | WCDMA network mode.                          |
| PREFERRED_NETWORK_MODE_LTE                                | 3    | LTE network mode.                            |
| PREFERRED_NETWORK_MODE_LTE_WCDMA                          | 4    | LTE+WCDMA network mode.                      |
| PREFERRED_NETWORK_MODE_LTE_WCDMA_GSM                      | 5    | LTE+WCDMA+GSM network mode.                  |
| PREFERRED_NETWORK_MODE_WCDMA_GSM                          | 6    | WCDMA+GSM network mode.                      |
| PREFERRED_NETWORK_MODE_CDMA                               | 7    | CDMA network mode.                           |
| PREFERRED_NETWORK_MODE_EVDO                               | 8    | EVDO network mode.                           |
| PREFERRED_NETWORK_MODE_EVDO_CDMA                          | 9    | EVDO+CDMA network mode.                      |
| PREFERRED_NETWORK_MODE_WCDMA_GSM_EVDO_CDMA                | 10   | WCDMA+GSM+EVDO+CDMA network mode.            |
| PREFERRED_NETWORK_MODE_LTE_EVDO_CDMA                      | 11   | LTE+EVDO+CDMA network mode.                  |
| PREFERRED_NETWORK_MODE_LTE_WCDMA_GSM_EVDO_CDMA            | 12   | LTE+WCDMA+GSM+EVDO+CDMA network mode.        |
| PREFERRED_NETWORK_MODE_TDSCDMA                            | 13   | TD-SCDMA network mode.                        |
| PREFERRED_NETWORK_MODE_TDSCDMA_GSM                        | 14   | TD-SCDMA+GSM network mode.                    |
| PREFERRED_NETWORK_MODE_TDSCDMA_WCDMA                      | 15   | TD-SCDMA+WCDMA network mode.                  |
| PREFERRED_NETWORK_MODE_TDSCDMA_WCDMA_GSM                  | 16   | TD-SCDMA+WCDMA+GSM network mode.              |
| PREFERRED_NETWORK_MODE_LTE_TDSCDMA                        | 17   | LTE+TD-SCDMA network mode.                    |
| PREFERRED_NETWORK_MODE_LTE_TDSCDMA_GSM                    | 18   | LTE+TD-SCDMA+GSM network mode.                |
| PREFERRED_NETWORK_MODE_LTE_TDSCDMA_WCDMA                  | 19   | LTE+TD-SCDMA+WCDMA network mode.              |
| PREFERRED_NETWORK_MODE_LTE_TDSCDMA_WCDMA_GSM              | 20   | LTE+TD-SCDMA+WCDMA+GSM network mode.          |
| PREFERRED_NETWORK_MODE_TDSCDMA_WCDMA_GSM_EVDO_CDMA        | 21   | TD-SCDMA+WCDMA+GSM+EVDO+CDMA network mode.    |
| PREFERRED_NETWORK_MODE_LTE_TDSCDMA_WCDMA_GSM_EVDO_CDMA    | 22   | LTE+TD-SCDMA+WCDMA+GSM+EVDO+CDMA network mode.|
| PREFERRED_NETWORK_MODE_NR                                 | 31   | NR network mode.                             |
| PREFERRED_NETWORK_MODE_NR_LTE                             | 32   | NR+LTE network mode.                         |
| PREFERRED_NETWORK_MODE_NR_LTE_WCDMA                       | 33   | NR+LTE+WCDMA network mode.                   |
| PREFERRED_NETWORK_MODE_NR_LTE_WCDMA_GSM                   | 34   | NR+LTE+WCDMA+GSM network mode.               |
| PREFERRED_NETWORK_MODE_NR_LTE_EVDO_CDMA                   | 35   | NR+LTE+EVDO+CDMA network mode.               |
| PREFERRED_NETWORK_MODE_NR_LTE_WCDMA_GSM_EVDO_CDMA         | 36   | NR+LTE+WCDMA+GSM+EVDO+CDMA network mode.     |
| PREFERRED_NETWORK_MODE_NR_LTE_TDSCDMA                     | 37   | NR+LTE+TD-SCDMA network mode.                 |
| PREFERRED_NETWORK_MODE_NR_LTE_TDSCDMA_GSM                 | 38   | NR+LTE+TD-SCDMA+GSM network mode.             |
| PREFERRED_NETWORK_MODE_NR_LTE_TDSCDMA_WCDMA               | 39   | NR+LTE+TD-SCDMA+WCDMA network mode.           |
| PREFERRED_NETWORK_MODE_NR_LTE_TDSCDMA_WCDMA_GSM           | 40   | NR+LTE+TD-SCDMA+WCDMA+GSM network mode.       |
| PREFERRED_NETWORK_MODE_NR_LTE_TDSCDMA_WCDMA_GSM_EVDO_CDMA | 41   | NR+LTE+TD-SCDMA+WCDMA+GSM network mode.       |
| PREFERRED_NETWORK_MODE_MAX_VALUE                          | 99   | Maximum value of the preferred network mode.                         |

## CellInformation<sup>8+</sup>

Defines the cell information.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name             |                  Type                  | Mandatory|                           Description                              |
| ----------------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
| networkType       | [NetworkType](#networktype)             |  Yes | Network type of the cell.                                    |
| isCamped          | boolean                                 |  Yes | Cell status.                                        |
| timeStamp         | number                                  |  Yes | Timestamp when cell information is obtained.                                |
| signalInformation | [SignalInformation](#signalinformation) |  Yes | Signal information.                                                  |
| data              | [CdmaCellInformation](#cdmacellinformation8) \| [GsmCellInformation](#gsmcellinformation8) \| [LteCellInformation](#ltecellinformation8) \| [NrCellInformation](#nrcellinformation8) \| [TdscdmaCellInformation](#tdscdmacellinformation8) |  Yes | CDMA cell information\|GSM cell information\|LTE cell information\|NR cell information\|TD-SCDMA cell information|

## CdmaCellInformation<sup>8+</sup>

Defines the CDMA cell information.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name     | Type  | Mandatory| Description        |
| --------- | ------ | ---- | ------------ |
| baseId    | number |  Yes | Base station ID.    |
| latitude  | number |  Yes | Longitude.      |
| longitude | number |  Yes | Latitude.      |
| nid       | number |  Yes | Network ID.|
| sid       | number |  Yes | System ID.|

## GsmCellInformation<sup>8+</sup>

Defines the GSM cell information.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name  | Type  | Mandatory| Description                |
| ------ | ------ | ---- | -------------------- |
| lac    | number |  Yes | Location area code.        |
| cellId | number |  Yes | Cell ID.            |
| arfcn  | number |  Yes | Absolute radio frequency channel number.|
| bsic   | number |  Yes | Base station ID.        |
| mcc    | string |  Yes | Mobile country code.        |
| mnc    | string |  Yes | Mobile network code.          |

## LteCellInformation<sup>8+</sup>

LTE cell information.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name         | Type   | Mandatory| Description                   |
| ------------- | ------- | ---- | ----------------------- |
| cgi           | number  |  Yes | Cell global identification.         |
| pci           | number  |  Yes | Physical cell ID.         |
| tac           | number  |  Yes | Tracking area code.         |
| earfcn        | number  |  Yes | Absolute radio frequency channel number.   |
| bandwidth     | number  |  Yes | Bandwidth.                 |
| mcc           | string  |  Yes | Mobile country code.           |
| mnc           | string  |  Yes | Mobile network code.             |
| isSupportEndc | boolean |  Yes | Support for New Radio_Dual Connectivity.|

## NrCellInformation<sup>8+</sup>

Defines the 5G NR cell information.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name   | Type  | Mandatory| Description            |
| ------- | ------ | ---- | ---------------- |
| nrArfcn | number |  Yes | 5G frequency number.      |
| pci     | number |  Yes | Physical cell ID.  |
| tac     | number |  Yes | Tracking area code.  |
| nci     | number |  Yes | 5G network cell ID.|
| mcc     | string |  Yes | Mobile country code.    |
| mnc     | string |  Yes | Mobile network code.      |

## TdscdmaCellInformation<sup>8+</sup>

Defines the TD-SCDMA cell information.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name  | Type  | Mandatory| Description        |
| ------ | ------ | ---- | ------------ |
| lac    | number |  Yes | Location area code.|
| cellId | number |  Yes | Cell ID.    |
| cpid   | number |  Yes | Cell parameter ID.|
| uarfcn | number |  Yes | Absolute radio frequency number.|
| mcc    | string |  Yes | Mobile country code.|
| mnc    | string |  Yes | Mobile network code.  |

## WcdmaCellInformation<sup>8+</sup>

Defines the WCDMA cell information.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name  | Type  | Mandatory| Description        |
| ------ | ------ | ---- | ------------ |
| lac    | number |  Yes | Location area code.|
| cellId | number |  Yes | Cell ID.    |
| psc    | number |  Yes | Primary scrambling code.    |
| uarfcn | number |  Yes | Absolute radio frequency number.|
| mcc    | string |  Yes | Mobile country code.|
| mnc    | string |  Yes | Mobile network code.  |

## NrOptionMode<sup>8+</sup>

Enumerates NR selection modes.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name                | Value  | Description                              |
| -------------------- | ---- | ---------------------------------- |
| NR_OPTION_UNKNOWN    | 0    | Unknown NR selection mode.                |
| NR_OPTION_NSA_ONLY   | 1    | NR selection mode in 5G non-standalone networking.        |
| NR_OPTION_SA_ONLY    | 2    | NR selection mode in 5G non-standalone networking.          |
| NR_OPTION_NSA_AND_SA | 3    | NR selection mode in non-standalone and standalone networking.|

## NetworkSearchResult

Defines the network search result.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name                  | Type                                             | Mandatory| Description          |
| ---------------------- | ------------------------------------------------- | ---- | -------------- |
| isNetworkSearchSuccess | boolean                                           |  Yes | Successful network search.|
| networkSearchResult    | Array<[NetworkInformation](#networkinformation)\> |  Yes | Network search result.|

## NetworkInformation

Defines the network information.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name           |                         Type                       | Mandatory| Description          |
| --------------- | --------------------------------------------------- | ---- | -------------- |
| operatorName    | string                                              |  Yes | Carrier name.|
| operatorNumeric | string                                              |  Yes | Carrier number.  |
| state           | [NetworkInformationState](#networkinformationstate) |  Yes | Network information status.|
| radioTech       | string                                              |  Yes | Radio access technology.  |

## NetworkInformationState

Enumerates network information states.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name             | Value  | Description            |
| ----------------- | ---- | ---------------- |
| NETWORK_UNKNOWN   | 0    | Unknown state.  |
| NETWORK_AVAILABLE | 1    | Available for registration.|
| NETWORK_CURRENT   | 2    | Registered state.|
| NETWORK_FORBIDDEN | 3    | Unavailable for registration.  |

## NetworkSelectionModeOptions

Defines the network selection mode.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name              |                    Type                      | Mandatory|                 Description                  |
| ------------------ | --------------------------------------------- | ---- | -------------------------------------- |
| slotId             | number                                        |  Yes | Card slot ID.<br>- **0**: card slot 1<br>- **1**: card slot 2|
| selectMode         | [NetworkSelectionMode](#networkselectionmode) |  Yes | Network selection mode.                        |
| networkInformation | [NetworkInformation](#networkinformation)     |  Yes | Network information.                            |
| resumeSelection    | boolean                                       |  Yes | Whether to resume selection.                            |

## ImsRegState<sup>9+</sup>

Enumerates IMS registration states.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name            | Value  | Description    |
| ---------------- | ---- | -------- |
| IMS_UNREGISTERED | 0    | Not registered.|
| IMS_REGISTERED   | 1    | Registered.|

## ImsRegTech<sup>9+</sup>

Enumerates IMS registration technologies.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name                   | Value  | Description           |
| ----------------------- | ---- | --------------- |
| REGISTRATION_TECH_NONE  | 0    | None.   |
| REGISTRATION_TECH_LTE   | 1    | LTE.  |
| REGISTRATION_TECH_IWLAN | 2    | I-WLAN.|
| REGISTRATION_TECH_NR    | 3    | NR.   |

## ImsRegInfo<sup>9+</sup>

Defines the IMS registration information.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name       | Type                        | Mandatory| Description         |
| ----------- | ---------------------------- | ---- | ------------- |
| imsRegState | [ImsRegState](#imsregstate9) |  Yes | IMS registration state.|
| imsRegTech  | [ImsRegTech](#imsregtech9)   |  Yes | IMS registration technology.|

## ImsServiceType<sup>9+</sup>

Enumerates IMS service types.

**System API**: This is a system API.

**System capability**: SystemCapability.Telephony.CoreService

| Name      | Value  | Description      |
| ---------- | ---- | ---------- |
| TYPE_VOICE | 0    | Voice service.|
| TYPE_VIDEO | 1    | Video service.|
| TYPE_UT    | 2    | UT service.  |
| TYPE_SMS   | 3    | SMS service.|
