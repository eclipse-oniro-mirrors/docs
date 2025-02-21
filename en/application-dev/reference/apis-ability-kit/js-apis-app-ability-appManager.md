# @ohos.app.ability.appManager (appManager)

The **appManager** module implements application management. You can use the APIs of this module to query whether the application is undergoing a stability test, whether the application is running on a RAM constrained device, the memory size of the application, and information about the running process.

> **NOTE**
> 
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```ts
import appManager from '@ohos.app.ability.appManager';
```

## appManager.isRunningInStabilityTest

isRunningInStabilityTest(callback: AsyncCallback&lt;boolean&gt;): void

Checks whether this application is undergoing a stability test. This API uses an asynchronous callback to return the result.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | Yes|Callback used to return the API call result and the result **true** or **false**. You can perform error handling or custom processing in this callback. The value **true** means that the application is undergoing a stability test, and **false** means the opposite. | 

**Error codes**

| ID| Error Message|
| ------- | -------- |
| 16000050 | Internal error. |

For details about the error codes, see [Ability Error Codes](errorcode-ability.md).

**Example**

```ts
import appManager from '@ohos.app.ability.appManager';

appManager.isRunningInStabilityTest((err, flag) => {
    if (err) {
        console.error(`isRunningInStabilityTest fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log(`The result of isRunningInStabilityTest is: ${JSON.stringify(flag)}`);
    }
});  
```


## appManager.isRunningInStabilityTest

isRunningInStabilityTest(): Promise&lt;boolean&gt;

Checks whether this application is undergoing a stability test. This API uses a promise to return the result.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;boolean&gt; | Promise used to return the API call result and the result **true** or **false**. You can perform error handling or custom processing in this callback. The value **true** means that the application is undergoing a stability test, and **false** means the opposite.| 

**Error codes**

| ID| Error Message|
| ------- | -------- |
| 16000050 | Internal error. |

For details about the error codes, see [Ability Error Codes](errorcode-ability.md).

**Example**

```ts
import appManager from '@ohos.app.ability.appManager';
import { BusinessError } from '@ohos.base';

appManager.isRunningInStabilityTest().then((flag) => {
    console.log(`The result of isRunningInStabilityTest is: ${JSON.stringify(flag)}`);
}).catch((error: BusinessError) => {
    console.error(`error: ${JSON.stringify(error)}`);
});
```


## appManager.isRamConstrainedDevice

isRamConstrainedDevice(): Promise\<boolean>

Checks whether this application is running on a RAM constrained device. This API uses a promise to return the result.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;boolean&gt; | Promise used to return the API call result and the result **true** or **false**. You can perform error handling or custom processing in this callback. The value **true** means that the application is running on a RAM constrained device, and **false** means the opposite.| 

**Error codes**

| ID| Error Message|
| ------- | -------- |
| 16000050 | Internal error. |

For details about the error codes, see [Ability Error Codes](errorcode-ability.md).

**Example**

```ts
import appManager from '@ohos.app.ability.appManager';
import { BusinessError } from '@ohos.base';

appManager.isRamConstrainedDevice().then((data) => {
    console.log(`The result of isRamConstrainedDevice is: ${JSON.stringify(data)}`);
}).catch((error: BusinessError) => {
    console.error(`error: ${JSON.stringify(error)}`);
});
```

## appManager.isRamConstrainedDevice

isRamConstrainedDevice(callback: AsyncCallback\<boolean>): void

Checks whether this application is running on a RAM constrained device. This API uses an asynchronous callback to return the result.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | Yes|Callback used to return the API call result and the result **true** or **false**. You can perform error handling or custom processing in this callback. The value **true** means that the application is running on a RAM constrained device, and **false** means the opposite. | 

**Error codes**

| ID| Error Message|
| ------- | -------- |
| 16000050 | Internal error. |

For details about the error codes, see [Ability Error Codes](errorcode-ability.md).

**Example**

```ts
import appManager from '@ohos.app.ability.appManager';

appManager.isRamConstrainedDevice((err, data) => {
    if (err) {
        console.error(`isRamConstrainedDevice fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log(`The result of isRamConstrainedDevice is: ${JSON.stringify(data)}`);
    }
});
```

## appManager.getAppMemorySize

getAppMemorySize(): Promise\<number>

Obtains the memory size of this application. This API uses a promise to return the result.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;number&gt; | Promise used to return the memory size, in MB. You can perform error processing or other custom processing based on the size.  | 

**Error codes**

| ID| Error Message|
| ------- | -------- |
| 16000050 | Internal error. |

For details about the error codes, see [Ability Error Codes](errorcode-ability.md).

**Example**

```ts
import appManager from '@ohos.app.ability.appManager';
import { BusinessError } from '@ohos.base';

appManager.getAppMemorySize().then((data) => {
    console.log(`The size of app memory is: ${JSON.stringify(data)}`);
}).catch((error: BusinessError) => {
    console.error(`error: ${JSON.stringify(error)}`);
});
```

## appManager.getAppMemorySize

getAppMemorySize(callback: AsyncCallback\<number>): void

Obtains the memory size of this application. This API uses an asynchronous callback to return the result.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;number&gt; | Yes|Callback used to return the memory size, in MB. You can perform error processing or other custom processing based on the size.  | 

**Error codes**

| ID| Error Message|
| ------- | -------- |
| 16000050 | Internal error. |

For details about the error codes, see [Ability Error Codes](errorcode-ability.md).

**Example**

```ts
import appManager from '@ohos.app.ability.appManager';

appManager.getAppMemorySize((err, data) => {
    if (err) {
        console.error(`getAppMemorySize fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log(`The size of app memory is: ${JSON.stringify(data)}`);
    }
});
```

## appManager.getRunningProcessInformation

getRunningProcessInformation(): Promise\<Array\<ProcessInformation>>

Obtains information about the running processes. This API uses a promise to return the result.

> **NOTE**
>
> In versions earlier than API version 11, this API requires the **ohos.permission.GET_RUNNING_INFO** permission, which is available only for system applications. Since API version 11, no permission is required for calling this API.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Return value**

| Type| Description|
| -------- | -------- |
| Promise\<Array\<[ProcessInformation](js-apis-inner-application-processInformation.md)>> | Promise used to return the API call result and the process running information. You can perform error handling or custom processing in this callback.|

**Error codes**

| ID| Error Message|
| ------- | -------- |
| 16000050 | Internal error. |

For details about the error codes, see [Ability Error Codes](errorcode-ability.md).

**Example**

```ts
import appManager from '@ohos.app.ability.appManager';
import { BusinessError } from '@ohos.base';

appManager.getRunningProcessInformation().then((data) => {
    console.log(`The running process information is: ${JSON.stringify(data)}`);
}).catch((error: BusinessError) => {
    console.error(`error: ${JSON.stringify(error)}`);
});
```

## appManager.getRunningProcessInformation

getRunningProcessInformation(callback: AsyncCallback<Array\<ProcessInformation>>): void

Obtains information about the running processes. This API uses a promise to return the result.  

**Required permissions**: ohos.permission.GET_RUNNING_INFO

> **NOTE**
>
> Since API version 11, the **ohos.permission.GET_RUNNING_INFO** permission is no longer required for calling this API.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name| Type| Mandatory| Description| 
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;Array\<[ProcessInformation](js-apis-inner-application-processInformation.md)>&gt; | Yes| Callback used to return the API call result and the process running information. You can perform error handling or custom processing in this callback.| 

**Error codes**

| ID| Error Message|
| ------- | -------- |
| 16000050 | Internal error. |

For details about the error codes, see [Ability Error Codes](errorcode-ability.md).

**Example**

```ts
import appManager from '@ohos.app.ability.appManager';
import { BusinessError } from '@ohos.base';

appManager.getRunningProcessInformation((err, data) => {
    if (err) {
        console.error(`getRunningProcessInformation fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log(`ProcessInformation: ${JSON.stringify(data)}`);
    }
});
```

## ProcessState<sup>10+</sup>

Enumerates the processes states.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name                | Value | Description                              |
| -------------------- | --- | --------------------------------- |
| STATE_CREATE    | 0   |      The process is being created.      |
| STATE_FOREGROUND          | 1   |            The process is running in the foreground.     |
| STATE_ACTIVE  | 2   |          The process is active.  |
| STATE_BACKGROUND        | 3   |       The process is running in the background.          |
| STATE_DESTROY        | 4   |         The process is destroyed.        |
