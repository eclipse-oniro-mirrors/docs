# @ohos.telephony.data (Cellular Data) (System API)

The **data** module provides basic mobile data management functions. You can obtain and set the default slot of the SIM card used for mobile data, and obtain the uplink and downlink connection status of cellular data services and connection status of the packet switched (PS) domain. Besides, you can check whether cellular data services and data roaming are enabled.

>**NOTE**
>
>The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> This topic describes only system APIs provided by the module. For details about its public APIs, see [@ohos.telephony.data (Cellular Data)](js-apis-telephony-data.md).


## Modules to Import

```ts
import data from '@ohos.telephony.data';
```


## data.setDefaultCellularDataSlotId

setDefaultCellularDataSlotId(slotId: number, callback: AsyncCallback\<void\>): void 

Sets the default slot of the SIM card used for mobile data. This API uses an asynchronous callback to return the result. 

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CellularData

**Parameters**

| Name  | Type                 | Mandatory| Description                                                        |
| -------- | --------------------- | ---- | ------------------------------------------------------------ |
| slotId   | number                | Yes  | SIM card slot ID. <br>- **0**: card slot 1.<br>- **1**: card slot 2.<br>- **-1**: Clears the default configuration.|
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.                                                  |

**Error codes**

For details about the error codes, see[ohos.telephony (Telephony) Error Codes](errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301001  | SIM card is not activated.                   |

**Example**

```ts
import data from '@ohos.telephony.data';
import { BusinessError } from '@ohos.base';

data.setDefaultCellularDataSlotId(0, (err: BusinessError) => {
    if(err){
        console.error(`setDefaultCellularDataSlotId fail,callback: err->${JSON.stringify(err)}.`);
    }else{
        console.log(`setDefaultCellularDataSlotId success`);
    }
});
```

## data.setDefaultCellularDataSlotId

setDefaultCellularDataSlotId(slotId: number): Promise\<void\> 

Sets the default slot of the SIM card used for mobile data. This API uses a promise to return the result. 

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CellularData

**Parameters**

| Name| Type  | Mandatory| Description                                                        |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| slotId | number | Yes  | SIM card slot ID. <br>- **0**: card slot 1.<br>- **1**: card slot 2.<br>- **-1**: Clears the default configuration.|

**Return value**

| Type           | Description                           |
| --------------- | ------------------------------- |
| Promise\<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see[ohos.telephony (Telephony) Error Codes](errorcode-telephony.md).

| ID|                 Error Message                    |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300004  | Do not have sim card.                        |
| 8300999  | Unknown error code.                          |
| 8301001  | SIM card is not activated.                   |

**Example**

```ts
import data from '@ohos.telephony.data';
import { BusinessError } from '@ohos.base';

data.setDefaultCellularDataSlotId(0).then(() => {
    console.log(`setDefaultCellularDataSlotId success.`);
}).catch((err: BusinessError) => {
    console.error(`setDefaultCellularDataSlotId fail, promise: err->${JSON.stringify(err)}`);
});
```


## data.enableCellularData

enableCellularData(callback: AsyncCallback\<void\>): void

Enables the cellular data service. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CellularData

**Parameters**

| Name  | Type                 | Mandatory| Description      |
| -------- | --------------------- | ---- | ---------- |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see[ohos.telephony (Telephony) Error Codes](errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import data from '@ohos.telephony.data';
import { BusinessError } from '@ohos.base';

data.enableCellularData((err: BusinessError) => {
    if(err){
        console.error(`enableCellularData fail,callback: callback: err->${JSON.stringify(err)}`);
    }else{
        console.log(`enableCellularData success`);
    }
});
```

## data.enableCellularData

enableCellularData(): Promise\<void\>

Enables the cellular data service. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CellularData

**Return value**

| Type           | Description                   |
| --------------- | ----------------------- |
| Promise\<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see[ohos.telephony (Telephony) Error Codes](errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import data from '@ohos.telephony.data';
import { BusinessError } from '@ohos.base';

data.enableCellularData().then(() => {
    console.log(`enableCellularData success.`);
}).catch((err: BusinessError) => {
    console.error(`enableCellularData fail, promise: err->${JSON.stringify(err)}`);
});
```

## data.disableCellularData

disableCellularData(callback: AsyncCallback\<void\>): void

Disables the cellular data service. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CellularData

**Parameters**

| Name  | Type                 | Mandatory| Description      |
| -------- | --------------------- | ---- | ---------- |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see[ohos.telephony (Telephony) Error Codes](errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import data from '@ohos.telephony.data';
import { BusinessError } from '@ohos.base';

data.disableCellularData((err: BusinessError) => {
    if(err){
        console.error(`disableCellularData fail,callback: callback: err->${JSON.stringify(err)}`);
    }else{
        console.log(`disableCellularData success`);
    }
});
```

## data.disableCellularData

disableCellularData(): Promise\<void\>

Disables the cellular data service. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CellularData

**Return value**

| Type           | Description                       |
| --------------- | --------------------------- |
| Promise\<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see[ohos.telephony (Telephony) Error Codes](errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import data from '@ohos.telephony.data';
import { BusinessError } from '@ohos.base';

data.disableCellularData().then(() => {
    console.log(`disableCellularData success.`);
}).catch((err: BusinessError) => {
    console.error(`disableCellularData fail, promise: err->${JSON.stringify(err)}`);
});
```

## data.enableCellularDataRoaming

enableCellularDataRoaming(slotId: number, callback: AsyncCallback\<void\>): void

Enables the cellular data roaming service. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CellularData

**Parameters**

| Name  | Type                 | Mandatory| Description                                    |
| -------- | --------------------- | ---- | ---------------------------------------- |
| slotId   | number                | Yes  | Card slot ID.<br>**0**: card slot 1.<br>**1**: card slot 2.|
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.                              |

**Error codes**

For details about the error codes, see[ohos.telephony (Telephony) Error Codes](errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import data from '@ohos.telephony.data';
import { BusinessError } from '@ohos.base';

data.enableCellularDataRoaming(0, (err: BusinessError) => {
    if(err){
        console.error(`enableCellularDataRoaming fail,callback: err->${JSON.stringify(err)}`);
    }else{
        console.log(`enableCellularDataRoaming success`);
    }
});
```

## data.enableCellularDataRoaming

enableCellularDataRoaming(slotId: number): Promise\<void\>

Enables the cellular data roaming service. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CellularData

**Parameters**

| Name| Type  | Mandatory| Description                                    |
| ------ | ------ | ---- | ---------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>**0**: card slot 1.<br>**1**: card slot 2.|

**Return value**

| Type           | Description                     |
| --------------- | ------------------------- |
| Promise\<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see[ohos.telephony (Telephony) Error Codes](errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import data from '@ohos.telephony.data';
import { BusinessError } from '@ohos.base';

data.enableCellularDataRoaming(0).then(() => {
    console.log(`enableCellularDataRoaming success.`);
}).catch((err: BusinessError) => {
    console.error(`enableCellularDataRoaming fail, promise: err->${JSON.stringify(err)}`);
});
```

## data.disableCellularDataRoaming

disableCellularDataRoaming(slotId: number, callback: AsyncCallback\<void\>): void

Disables the cellular data roaming service. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CellularData

**Parameters**

| Name  | Type                 | Mandatory| Description                                    |
| -------- | --------------------- | ---- | ---------------------------------------- |
| slotId   | number                | Yes  | Card slot ID.<br>**0**: card slot 1.<br>**1**: card slot 2.|
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.                              |

**Error codes**

For details about the error codes, see[ohos.telephony (Telephony) Error Codes](errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import data from '@ohos.telephony.data';
import { BusinessError } from '@ohos.base';

data.disableCellularDataRoaming(0, (err: BusinessError) => {
    if(err){
        console.error(`disableCellularDataRoaming fail,callback: err->${JSON.stringify(err)}`);
    }else{
        console.log(`disableCellularDataRoaming success`);
    }
});
```

## data.disableCellularDataRoaming

disableCellularDataRoaming(slotId: number): Promise\<void\>

Disables the cellular data roaming service. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.SET_TELEPHONY_STATE

**System capability**: SystemCapability.Telephony.CellularData

**Parameters**

| Name| Type  | Mandatory| Description                                    |
| ------ | ------ | ---- | ---------------------------------------- |
| slotId | number | Yes  | Card slot ID.<br>**0**: card slot 1.<br>**1**: card slot 2.|

**Return value**

| Type           | Description                     |
| --------------- | ------------------------- |
| Promise\<void\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see[ohos.telephony (Telephony) Error Codes](errorcode-telephony.md).

| ID|                  Error Message                   |
| -------- | -------------------------------------------- |
| 201      | Permission denied.                           |
| 202      | Non-system applications use system APIs.     |
| 401      | Parameter error.                             |
| 8300001  | Invalid parameter value.                     |
| 8300002  | Operation failed. Cannot connect to service. |
| 8300003  | System internal error.                       |
| 8300999  | Unknown error code.                          |

**Example**

```ts
import data from '@ohos.telephony.data';
import { BusinessError } from '@ohos.base';

data.disableCellularDataRoaming(0).then(() => {
    console.log(`disableCellularDataRoaming success.`);
}).catch((err: BusinessError) => {
    console.error(`disableCellularDataRoaming fail, promise: err->${JSON.stringify(err)}`);
});
```
