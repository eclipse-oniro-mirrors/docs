# @ohos.resourceschedule.backgroundTaskManager (Background Task Management)

The **backgroundTaskManager** module provides APIs to request background tasks. You can use the APIs to request transient tasks, continuous tasks, or efficiency resources to prevent the application process from being terminated or suspended when your application is switched to the background.

>  **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```ts
import backgroundTaskManager from '@ohos.resourceschedule.backgroundTaskManager';  
```

## backgroundTaskManager.requestSuspendDelay

requestSuspendDelay(reason: string, callback: Callback&lt;void&gt;): DelaySuspendInfo

Requests a transient task.

>  **NOTE**
>
> The maximum duration of a transient task is 3 minutes in normal cases. In the case of a [low battery](../apis-basic-services-kit/js-apis-battery-info.md), the maximum duration is decreased to 1 minute.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.TransientTask

**Parameters**

| Name     | Type                  | Mandatory  | Description                            |
| -------- | -------------------- | ---- | ------------------------------ |
| reason   | string               | Yes   | Reason for requesting the transient task.                    |
| callback | Callback&lt;void&gt; | Yes   | Callback used to notify the application that the transient task is about to time out. Generally, the callback is invoked 6 seconds before the timeout.|

**Return value**

| Type                                   | Description       |
| ------------------------------------- | --------- |
| [DelaySuspendInfo](#delaysuspendinfo) | Information about the transient task.|

**Error codes**

For details about the error codes, see [backgroundTaskManager Error Codes](errorcode-backgroundTaskMgr.md).

| ID | Error Message            |
| ---- | --------------------- |
| 9800001 | Memory operation failed. |
| 9800002 | Parcel operation failed. |
| 9800003 | Inner transact failed. | |
| 9800004 | System service operation failed. |
| 9900001 | Caller information verification failed. |
| 9900002 | Background task verification failed. |

**Example**

```ts 
import { BusinessError } from '@ohos.base';

let myReason = 'test requestSuspendDelay';
try {
    let delayInfo = backgroundTaskManager.requestSuspendDelay(myReason, () => {
        console.info("Request suspension delay will time out.");
    })
    let id = delayInfo.requestId;
    let time = delayInfo.actualDelayTime;
    console.info("The requestId is: " + id);
    console.info("The actualDelayTime is: " + time);
} catch (error) {
    console.error(`requestSuspendDelay failed. code is ${(error as BusinessError).code} message is ${(error as BusinessError).message}`);
}
```


## backgroundTaskManager.getRemainingDelayTime

getRemainingDelayTime(requestId: number, callback: AsyncCallback&lt;number&gt;): void

Obtains the remaining time of a transient task. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.TransientTask

**Parameters**

| Name      | Type                         | Mandatory  | Description                                      |
| --------- | --------------------------- | ---- | ---------------------------------------- |
| requestId | number                      | Yes   | Request ID of the transient task.                              |
| callback  | AsyncCallback&lt;number&gt; | Yes   | Callback used to return the remaining time, in milliseconds.|

**Error codes**

For details about the error codes, see [backgroundTaskManager Error Codes](errorcode-backgroundTaskMgr.md).

| ID | Error Message            |
| ---- | --------------------- |
| 9800001 | Memory operation failed. |
| 9800002 | Parcel operation failed. |
| 9800003 | Inner transact failed.  |
| 9800004 | System service operation failed. |
| 9900001 | Caller information verification failed. |
| 9900002 | Background task verification failed. |


**Example**

```ts 
import { BusinessError } from '@ohos.base';

let id = 1;
backgroundTaskManager.getRemainingDelayTime(id, (error: BusinessError, res: number) => {
    if(error) {
        console.error(`callback => Operation getRemainingDelayTime failed. code is ${error.code} message is ${error.message}`);
    } else {
        console.log('callback => Operation getRemainingDelayTime succeeded. Data: ' + JSON.stringify(res));
    }
})
```


## backgroundTaskManager.getRemainingDelayTime

getRemainingDelayTime(requestId: number): Promise&lt;number&gt;

Obtains the remaining time of a transient task. This API uses a promise to return the result.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.TransientTask

**Parameters**

| Name      | Type    | Mandatory  | Description        |
| --------- | ------ | ---- | ---------- |
| requestId | number | Yes   | Request ID of the transient task.|

**Return value**

| Type                   | Description                                      |
| --------------------- | ---------------------------------------- |
| Promise&lt;number&gt; | Promise used to return the remaining time, in milliseconds.|

**Error codes**

For details about the error codes, see [backgroundTaskManager Error Codes](errorcode-backgroundTaskMgr.md).

| ID | Error Message            |
| ---- | --------------------- |
| 9800001 | Memory operation failed. |
| 9800002 | Parcel operation failed. |
| 9800003 | Inner transact failed. | |
| 9800004 | System service operation failed. |
| 9900001 | Caller information verification failed. |
| 9900002 | Background task verification failed. |

**Example**

```ts 
import { BusinessError } from '@ohos.base';

let id = 1;
backgroundTaskManager.getRemainingDelayTime(id).then((res: number) => {
    console.log('promise => Operation getRemainingDelayTime succeeded. Data: ' + JSON.stringify(res));
}).catch((error: BusinessError) => {
    console.error(`promise => Operation getRemainingDelayTime failed. code is ${error.code} message is ${error.message}`);
})
```


## backgroundTaskManager.cancelSuspendDelay

cancelSuspendDelay(requestId: number): void

Cancels a transient task.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.TransientTask

**Parameters**

| Name      | Type    | Mandatory  | Description        |
| --------- | ------ | ---- | ---------- |
| requestId | number | Yes   | Request ID of the transient task.|

**Error codes**

For details about the error codes, see [backgroundTaskManager Error Codes](errorcode-backgroundTaskMgr.md).

| ID | Error Message            |
| ---- | --------------------- |
| 9800001 | Memory operation failed. |
| 9800002 | Parcel operation failed. |
| 9800003 | Inner transact failed. | |
| 9800004 | System service operation failed. |
| 9900001 | Caller information verification failed. |
| 9900002 | Background task verification failed. |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';

  let id = 1;
  try {
    backgroundTaskManager.cancelSuspendDelay(id);
  } catch (error) {
    console.error(`cancelSuspendDelay failed. code is ${(error as BusinessError).code} message is ${(error as BusinessError).message}`);
  }
  ```

## backgroundTaskManager.startBackgroundRunning

startBackgroundRunning(context: Context, bgMode: BackgroundMode, wantAgent: WantAgent, callback: AsyncCallback&lt;void&gt;): void

Requests a continuous task. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.KEEP_BACKGROUND_RUNNING

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.ContinuousTask

**Parameters**

| Name      | Type                                | Mandatory  | Description                                      |
| --------- | ---------------------------------- | ---- | ---------------------------------------- |
| context   | Context                            | Yes   | Application context.<br>For details about the application context of the FA model, see [Context](../apis-ability-kit/js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| bgMode    | [BackgroundMode](#backgroundmode) | Yes   | Continuous task mode.                             |
| wantAgent | [WantAgent](../apis-ability-kit/js-apis-app-ability-wantAgent.md) | Yes   | Notification parameters, which are used to specify the target page that is redirected to when a continuous task notification is clicked.          |
| callback  | AsyncCallback&lt;void&gt;          | Yes   | Callback used to return the result. If the continuous task is requested, **err** is **undefined**. Otherwise, **err** is an error object.   |

**Error codes**

For details about the error codes, see [backgroundTaskManager Error Codes](errorcode-backgroundTaskMgr.md).

| ID | Error Message            |
| ---- | --------------------- |
| 9800001 | Memory operation failed. |
| 9800002 | Parcel operation failed. |
| 9800003 | Inner transact failed. | |
| 9800004 | System service operation failed. |
| 9800005 | Background task verification failed. |
| 9800006 | Notification verification failed. |
| 9800007 | Task storage failed. |

**Example**

```js
import UIAbility from '@ohos.app.ability.UIAbility';
import backgroundTaskManager from '@ohos.resourceschedule.backgroundTaskManager';  
import wantAgent, { WantAgent } from '@ohos.app.ability.wantAgent';
import Want from '@ohos.app.ability.Want';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import { BusinessError } from '@ohos.base';

function callback(error: BusinessError, data: void) {
    if (error) {
        console.error(`Operation startBackgroundRunning failed. code is ${error.code} message is ${error.message}`);
    } else {
        console.info("Operation startBackgroundRunning succeeded");
    }
}

export default class EntryAbility extends UIAbility {
    onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
        let wantAgentInfo: wantAgent.WantAgentInfo = {
            // List of operations to be executed after the notification is clicked.
            wants: [
                {
                    bundleName: "com.example.myapplication",
                    abilityName: "EntryAbility"
                }
            ],
            // Type of the operation to perform after the notification is clicked.
            actionType: wantAgent.OperationType.START_ABILITY,
            // Custom request code.
            requestCode: 0,
            // Execution attribute of the operation to perform after the notification is clicked.
            wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
        };

        try {
            // Obtain the WantAgent object by using the getWantAgent API of the wantAgent module.
            wantAgent.getWantAgent(wantAgentInfo).then((wantAgentObj: WantAgent) => {
                try {
                    backgroundTaskManager.startBackgroundRunning(this.context,
                        backgroundTaskManager.BackgroundMode.LOCATION, wantAgentObj, callback)
                } catch (error) {
                    console.error(`Operation startBackgroundRunning failed. code is ${(error as BusinessError).code} message is ${(error as BusinessError).message}`);
                }
            });
        } catch (error) {
            console.error(`Operation getWantAgent failed. code is ${(error as BusinessError).code} message is ${(error as BusinessError).message}`);
        }
    }
};
```

## backgroundTaskManager.startBackgroundRunning

startBackgroundRunning(context: Context, bgMode: BackgroundMode, wantAgent: WantAgent): Promise&lt;void&gt;

Requests a continuous task. This API uses a promise to return the result.

**Required permissions**: ohos.permission.KEEP_BACKGROUND_RUNNING

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.ContinuousTask

**Parameters**

| Name      | Type                                | Mandatory  | Description                                      |
| --------- | ---------------------------------- | ---- | ---------------------------------------- |
| context   | Context                            | Yes   | Application context.<br>For details about the application context of the FA model, see [Context](../apis-ability-kit/js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| bgMode    | [BackgroundMode](#backgroundmode) | Yes   | Continuous task mode.                             |
| wantAgent | [WantAgent](../apis-ability-kit/js-apis-app-ability-wantAgent.md) | Yes   | Notification parameters, which are used to specify the target page that is redirected to when a continuous task notification is clicked.                |

**Return value**

| Type            | Description              |
| -------------- | ---------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [backgroundTaskManager Error Codes](errorcode-backgroundTaskMgr.md).

| ID | Error Message            |
| ---- | --------------------- |
| 9800001 | Memory operation failed. |
| 9800002 | Parcel operation failed. |
| 9800003 | Inner transact failed. | |
| 9800004 | System service operation failed. |
| 9800005 | Background task verification failed. |
| 9800006 | Notification verification failed. |
| 9800007 | Task storage failed. |

**Example**

```js
import UIAbility from '@ohos.app.ability.UIAbility';
import backgroundTaskManager from '@ohos.resourceschedule.backgroundTaskManager'; 
import wantAgent, { WantAgent } from '@ohos.app.ability.wantAgent';
import Want from '@ohos.app.ability.Want';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
    onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
        let wantAgentInfo: wantAgent.WantAgentInfo = {
            // List of operations to be executed after the notification is clicked.
            wants: [
                {
                    bundleName: "com.example.myapplication",
                    abilityName: "EntryAbility"
                }
            ],
            // Type of the operation to perform after the notification is clicked.
            actionType: wantAgent.OperationType.START_ABILITY,
            // Custom request code.
            requestCode: 0,
            // Execution attribute of the operation to perform after the notification is clicked.
            wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
        };

        try {
            // Obtain the WantAgent object by using the getWantAgent API of the wantAgent module.
            wantAgent.getWantAgent(wantAgentInfo).then((wantAgentObj: WantAgent) => {
                try {
                    backgroundTaskManager.startBackgroundRunning(this.context,
                        backgroundTaskManager.BackgroundMode.LOCATION, wantAgentObj).then(() => {
                        console.info("Operation startBackgroundRunning succeeded");
                    }).catch((error: BusinessError) => {
                        console.error(`Operation startBackgroundRunning failed. code is ${error.code} message is ${error.message}`);
                    });
                } catch (error) {
                    console.error(`Operation startBackgroundRunning failed. code is ${(error as BusinessError).code} message is ${(error as BusinessError).message}`);
                }
            });
        } catch (error) {
            console.error(`Operation getWantAgent failed. code is ${(error as BusinessError).code} message is ${(error as BusinessError).message}`);
        }
    }
};
```

## backgroundTaskManager.stopBackgroundRunning

stopBackgroundRunning(context: Context, callback: AsyncCallback&lt;void&gt;): void

Cancels a continuous task. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.ContinuousTask

**Parameters**

| Name     | Type                       | Mandatory  | Description                                      |
| -------- | ------------------------- | ---- | ---------------------------------------- |
| context  | Context                   | Yes   | Application context.<br>For details about the application context of the FA model, see [Context](../apis-ability-kit/js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| callback | AsyncCallback&lt;void&gt; | Yes   | Callback used to return the result. If the continuous task is canceled, **err** is **undefined**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [backgroundTaskManager Error Codes](errorcode-backgroundTaskMgr.md).

| ID | Error Message            |
| ---- | --------------------- |
| 9800001 | Memory operation failed. |
| 9800002 | Parcel operation failed. |
| 9800003 | Inner transact failed. | |
| 9800004 | System service operation failed. |
| 9800005 | Background task verification failed. |
| 9800006 | Notification verification failed. |
| 9800007 | Task storage failed. |

**Example**

```js
import UIAbility from '@ohos.app.ability.UIAbility';
import backgroundTaskManager from '@ohos.resourceschedule.backgroundTaskManager';  
import Want from '@ohos.app.ability.Want';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import { BusinessError } from '@ohos.base';

function callback(error: BusinessError, data: void) {
    if (error) {
        console.error(`Operation stopBackgroundRunning failed. code is ${error.code} message is ${error.message}`);
    } else {
        console.info("Operation stopBackgroundRunning succeeded");
    }
}

export default class EntryAbility extends UIAbility {
    onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
        try {
            backgroundTaskManager.stopBackgroundRunning(this.context, callback);
        } catch (error) {
            console.error(`Operation stopBackgroundRunning failed. code is ${(error as BusinessError).code} message is ${(error as BusinessError).message}`);
        }
    }
};
```

## backgroundTaskManager.stopBackgroundRunning

stopBackgroundRunning(context: Context): Promise&lt;void&gt;

Cancels a continuous task. This API uses a promise to return the result.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.ContinuousTask

**Parameters**

| Name    | Type     | Mandatory  | Description                                      |
| ------- | ------- | ---- | ---------------------------------------- |
| context | Context | Yes   | Application context.<br>For details about the application context of the FA model, see [Context](../apis-ability-kit/js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|

**Return value**

| Type            | Description              |
| -------------- | ---------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [backgroundTaskManager Error Codes](errorcode-backgroundTaskMgr.md).

| ID | Error Message            |
| ---- | --------------------- |
| 9800001 | Memory operation failed. |
| 9800002 | Parcel operation failed. |
| 9800003 | Inner transact failed. | |
| 9800004 | System service operation failed. |
| 9800005 | Background task verification failed. |
| 9800006 | Notification verification failed. |
| 9800007 | Task storage failed. |

**Example**

```js
import UIAbility from '@ohos.app.ability.UIAbility';
import backgroundTaskManager from '@ohos.resourceschedule.backgroundTaskManager';  
import Want from '@ohos.app.ability.Want';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
    onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
        try {
            backgroundTaskManager.stopBackgroundRunning(this.context).then(() => {
                console.info("Operation stopBackgroundRunning succeeded");
            }).catch((error: BusinessError) => {
                console.error(`Operation stopBackgroundRunning failed. code is ${error.code} message is ${error.message}`);
            });
        } catch (error) {
            console.error(`Operation stopBackgroundRunning failed. code is ${(error as BusinessError).code} message is ${(error as BusinessError).message}`);
        }
    }
};
```

## DelaySuspendInfo

Defines the information about the transient task.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.TransientTask

| Name            | Type    | Mandatory  | Description                                      |
| --------------- | ------ | ---- | ---------------------------------------- |
| requestId       | number | Yes   | Request ID of the transient task.                              |
| actualDelayTime | number | Yes   | Actual duration of the transient task that the application requests, in milliseconds.<br>The maximum duration of a transient task is 3 minutes in normal cases. In the case of a [low battery](../apis-basic-services-kit/js-apis-battery-info.md), the maximum duration is decreased to 1 minute.|

## BackgroundMode

Enumerates the continuous task modes.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.ContinuousTask

| Name                    | Value | Description                   |
| ----------------------- | ---- | --------------------- |
| DATA_TRANSFER           | 1    | Data transfer.                 |
| AUDIO_PLAYBACK          | 2    | Audio playback.                 |
| AUDIO_RECORDING         | 3    | Audio recording.                   |
| LOCATION                | 4    | Positioning and navigation.                 |
| BLUETOOTH_INTERACTION   | 5    | Bluetooth-related task.                 |
| MULTI_DEVICE_CONNECTION | 6    | Multi-device connection.                |
| TASK_KEEPING            | 9    | Computing task (for specific devices only).       |

   