# @ohos.resourceschedule.backgroundTaskManager (Background Task Management) (System API)

The **backgroundTaskManager** module provides APIs to request background tasks. You can use the APIs to request transient tasks, continuous tasks, or efficiency resources to prevent the application process from being terminated or suspended when your application is switched to the background.

>  **NOTE**
> 
> - The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> 
> - This topic describes only system APIs provided by the module. For details about its public APIs, see [@ohos.resourceschedule.backgroundTaskManager (Background Task Management)](js-apis-resourceschedule-backgroundTaskManager.md).

## Modules to Import

```ts
import backgroundTaskManager from '@ohos.resourceschedule.backgroundTaskManager';  
```

## backgroundTaskManager.applyEfficiencyResources

applyEfficiencyResources(request: EfficiencyResourcesRequest): void

Requests efficiency resources.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.EfficiencyResourcesApply

**System API**: This is a system API.

**Parameters**

| Name    | Type     | Mandatory  | Description                                      |
| ------- | ------- | ---- | ---------------------------------------- |
| request | [EfficiencyResourcesRequest](#efficiencyresourcesrequest) | Yes   | Necessary information carried in the request, including the resource type and timeout interval.|


**Error codes**

For details about the error codes, see [backgroundTaskManager Error Codes](errorcode-backgroundTaskMgr.md).

| ID | Error Message            |
| ---- | --------------------- |
| 9800001 | Memory operation failed. |
| 9800002 | Parcel operation failed. |
| 9800003 | Inner transact failed. | |
| 9800004 | System service operation failed. |
| 18700001 | Caller information verification failed. |

**Example**

```js
import { BusinessError } from '@ohos.base';

let request: backgroundTaskManager.EfficiencyResourcesRequest = {
    resourceTypes: backgroundTaskManager.ResourceType.CPU,
    isApply: true,
    timeOut: 0,
    reason: "apply",
    isPersist: true,
    isProcess: false,
};
try {
    backgroundTaskManager.applyEfficiencyResources(request);
    console.info("applyEfficiencyResources success. ");
} catch (error) {
    console.error(`applyEfficiencyResources failed. code is ${(error as BusinessError).code} message is ${(error as BusinessError).message}`);
}
```

## backgroundTaskManager.resetAllEfficiencyResources

resetAllEfficiencyResources(): void

Releases all efficiency resources.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.EfficiencyResourcesApply

**System API**: This is a system API.

**Error codes**

For details about the error codes, see [backgroundTaskManager Error Codes](errorcode-backgroundTaskMgr.md).

| ID | Error Message            |
| ---- | --------------------- |
| 9800001 | Memory operation failed. |
| 9800002 | Parcel operation failed. |
| 9800003 | Inner transact failed. | |
| 9800004 | System service operation failed. |
| 18700001 | Caller information verification failed. |

**Example**

```js
import { BusinessError } from '@ohos.base';

try {
    backgroundTaskManager.resetAllEfficiencyResources();
} catch (error) {
    console.error(`resetAllEfficiencyResources failed. code is ${(error as BusinessError).code} message is ${(error as BusinessError).message}`);
}
```

## BackgroundMode

Enumerates the continuous task modes.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.ContinuousTask

| Name                    | Value | Description                   |
| ----------------------- | ---- | --------------------- |
| WIFI_INTERACTION        | 7    | WLAN-related.<br>**System API**: This is a system API.|
| VOIP                    | 8    | Audio and video calls.<br>**System API**: This is a system API.|

## EfficiencyResourcesRequest

Describes the parameters for requesting efficiency resources.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.EfficiencyResourcesApply

**System API**: This is a system API.

| Name            | Type    | Mandatory  | Description                                      |
| --------------- | ------ | ---- | ---------------------------------------- |
| resourceTypes   | number  | Yes   | Type of the resource to request.                              |
| isApply         | boolean | Yes   | Whether the request is used to apply for resources.<br>The value **true** means that the request is used to apply for resources, and **false** means that the request is used to release resources.|
| timeOut         | number  | Yes   | Duration for which the resource will be used, in milliseconds.               |
| isPersist       | boolean | No   | Whether the resource is permanently held. The default value is **false**.<br>The value **true** means that the resource is permanently held, and **false** means the resource is held within a given period of time.|
| isProcess       | boolean | No   | Whether the request is initiated by a process. The default value is **false**.<br>The value **true** means that the request is initiated by a process, and **false** means that the request is initiated by an application.        |
| reason          | string  | Yes   | Reason for requesting the resource.               |

## ResourceType

Enumerates the efficiency resource types.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.EfficiencyResourcesApply

**System API**: This is a system API.

| Name                    | Value | Description                   |
| ----------------------- | ---- | --------------------- |
| CPU                     | 1    | CPU resource. Such type of resource prevents an application from being suspended.            |
| COMMON_EVENT            | 2    | Common event resource. Such type of resource ensures that an application in the suspended state can receive common events.|
| TIMER                   | 4    | Timer resource. Such type of resource ensures that an application in the suspended state can be woken up by system timers.|
| WORK_SCHEDULER          | 8    | Deferred task resource. Such type of resource provides a loose control policy for an application.|
| BLUETOOTH               | 16   | Bluetooth resource. Such type of resource ensures that an application in the suspended state can be woken up by Bluetooth-related events.|
| GPS                     | 32   | GPS resource. Such type of resource ensures that an application in the suspended state can be woken up by GPS-related events.|
| AUDIO                   | 64   | Audio resource. Such type of resource prevents an application from being suspended when the application has an audio being played.|
| RUNNING_LOCK<sup>10+</sup> | 128 | RUNNING_LOCK resources are not proxied when the application is suspended.|
| SENSOR<sup>10+</sup> | 256 | Sensor callbacks are not intercepted.|
