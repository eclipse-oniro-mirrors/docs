# @ohos.backgroundTaskManager (Background Task Management)

The **BackgroundTaskManager** module provides APIs to manage background tasks.

If a service needs to be continued when the application or service module is running in the background (not visible to users), the application or service module can request a transient task to delay the suspension or a continuous task to prevent the suspension.

If an application has a task that needs to be continued when the application is switched to the background and can be completed within a short period of time, the application can request a transient task. For example, if a user chooses to clear junk files in the **Files** application and exits the application, the application can request a transient task to complete the cleanup.

If an application has a service that can be intuitively perceived by users and needs to run in the background for a long period of time (for example, music playback in the background), the application can request a continuous task.

If a privileged system application needs to use certain system resources (for example, it wants to receive common events when suspended), it can request efficiency resources.

>  **NOTE**
> - This module is deprecated since API version 9. You are advised to use [@ohos.resourceschedule.backgroundTaskManager](js-apis-resourceschedule-backgroundTaskManager.md) instead.
> - The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```js
import backgroundTaskManager from '@ohos.backgroundTaskManager';  
```


## backgroundTaskManager.requestSuspendDelay

requestSuspendDelay(reason: string, callback: Callback&lt;void&gt;): DelaySuspendInfo

Requests delayed suspension after the application switches to the background.

The default duration of delayed suspension is 3 minutes when the battery level is higher than or equal to the broadcast low battery level and 1 minute when the battery level is lower than the broadcast low battery level.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.TransientTask

**Parameters**

| Name     | Type                  | Mandatory  | Description                            |
| -------- | -------------------- | ---- | ------------------------------ |
| reason   | string               | Yes   | Reason for delayed transition to the suspended state.                    |
| callback | Callback&lt;void&gt; | Yes   | Invoked when a delay is about to time out. Generally, this callback is used to notify the application 6 seconds before the delay times out.|

**Return value**

| Type                                   | Description       |
| ------------------------------------- | --------- |
| [DelaySuspendInfo](#delaysuspendinfo) | Information about the suspension delay.|

**Example**

  ```js
  import backgroundTaskManager from '@ohos.backgroundTaskManager';

  let myReason = 'test requestSuspendDelay';
  let delayInfo = backgroundTaskManager.requestSuspendDelay(myReason, () => {
      console.info("Request suspension delay will time out.");
  })

  let id = delayInfo.requestId;
  let time = delayInfo.actualDelayTime;
  console.info("The requestId is: " + id);
  console.info("The actualDelayTime is: " + time);
  ```


## backgroundTaskManager.getRemainingDelayTime

getRemainingDelayTime(requestId: number, callback: AsyncCallback&lt;number&gt;): void

Obtains the remaining duration before the application is suspended. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.TransientTask

**Parameters**

| Name      | Type                         | Mandatory  | Description                                      |
| --------- | --------------------------- | ---- | ---------------------------------------- |
| requestId | number                      | Yes   | ID of the suspension delay request. The value is obtained by calling [requestSuspendDelay](#backgroundtaskmanagerrequestsuspenddelay).|
| callback  | AsyncCallback&lt;number&gt; | Yes   | Callback used to return the remaining duration before the application is suspended, in milliseconds.|

**Example**

  ```js
  import backgroundTaskManager from '@ohos.backgroundTaskManager';

  let delayInfo = backgroundTaskManager.requestSuspendDelay("test", () => {});
  backgroundTaskManager.getRemainingDelayTime(delayInfo.requestId, (err, res) => {
      if(err) {
          console.log('callback => Operation getRemainingDelayTime failed. Cause: ' + err.code);
      } else {
          console.log('callback => Operation getRemainingDelayTime succeeded. Data: ' + JSON.stringify(res));
      }
  })
  ```


## backgroundTaskManager.getRemainingDelayTime

getRemainingDelayTime(requestId: number): Promise&lt;number&gt;

Obtains the remaining duration before the application is suspended. This API uses a promise to return the result.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.TransientTask

**Parameters**

| Name      | Type    | Mandatory  | Description        |
| --------- | ------ | ---- | ---------- |
| requestId | number | Yes   | ID of the suspension delay request. The value is obtained by calling [requestSuspendDelay](#backgroundtaskmanagerrequestsuspenddelay).|

**Return value**

| Type                   | Description                                      |
| --------------------- | ---------------------------------------- |
| Promise&lt;number&gt; | Promise used to return the remaining duration before the application is suspended, in milliseconds.|

**Example**

  ```js
  let delayInfo = backgroundTaskManager.requestSuspendDelay("test", () => {});
  backgroundTaskManager.getRemainingDelayTime(delayInfo.requestId).then( res => {
      console.log('promise => Operation getRemainingDelayTime succeeded. Data: ' + JSON.stringify(res));
  }).catch( err => {
      console.log('promise => Operation getRemainingDelayTime failed. Cause: ' + err.code);
  })
  ```


## backgroundTaskManager.cancelSuspendDelay

cancelSuspendDelay(requestId: number): void

Cancels the suspension delay.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.TransientTask

**Parameters**

| Name      | Type    | Mandatory  | Description        |
| --------- | ------ | ---- | ---------- |
| requestId | number | Yes   | ID of the suspension delay request. The value is obtained by calling [requestSuspendDelay](#backgroundtaskmanagerrequestsuspenddelay).|

**Example**

  ```js
  let delayInfo = backgroundTaskManager.requestSuspendDelay("test", () => {});
  backgroundTaskManager.cancelSuspendDelay(delayInfo.requestId);
  ```


## backgroundTaskManager.startBackgroundRunning<sup>8+</sup>

startBackgroundRunning(context: Context, bgMode: BackgroundMode, wantAgent: WantAgent, callback: AsyncCallback&lt;void&gt;): void

Requests a continuous task from the system. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.KEEP_BACKGROUND_RUNNING

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.ContinuousTask

**Parameters**

| Name   | Type                                         | Mandatory| Description                                                        |
| --------- | --------------------------------------------- | ---- | ------------------------------------------------------------ |
| context   | Context                                       | Yes  | Application context.<br>For details about the application context of the FA model, see [Context](js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](js-apis-inner-application-context.md).|
| bgMode    | [BackgroundMode](#backgroundmode8)            | Yes  | Background mode requested.                                      |
| wantAgent | [WantAgent](js-apis-app-ability-wantAgent.md) | Yes  | Notification parameter, which is used to specify the target page that is redirected to when a continuous task notification is clicked.            |
| callback  | AsyncCallback&lt;void&gt;                     | Yes  | Callback used to return the result.                        |

**Example**

FA model:

```js
import backgroundTaskManager from '@ohos.backgroundTaskManager';
import featureAbility from '@ohos.ability.featureAbility';
import wantAgent from '@ohos.wantAgent';

function callback(err, data) {
    if (err) {
        console.error("Operation startBackgroundRunning failed Cause: " + err);
    } else {
        console.info("Operation startBackgroundRunning succeeded");
    }
}

let wantAgentInfo = {
    wants: [
        {
            bundleName: "com.example.myapplication",
            abilityName: "com.example.myapplication.MainAbility"
        }
    ],
    operationType: wantAgent.OperationType.START_ABILITY,
    requestCode: 0,
    wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

wantAgent.getWantAgent(wantAgentInfo).then((wantAgentObj) => {
    backgroundTaskManager.startBackgroundRunning(featureAbility.getContext(),
        backgroundTaskManager.BackgroundMode.LOCATION, wantAgentObj, callback)
});

```

Stage model:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import backgroundTaskManager from '@ohos.backgroundTaskManager';
import wantAgent from '@ohos.app.ability.wantAgent';

function callback(err, data) {
    if (err) {
        console.error("Operation startBackgroundRunning failed Cause: " + err);
    } else {
        console.info("Operation startBackgroundRunning succeeded");
    }
}

export default class EntryAbility extends UIAbility {
    onCreate(want, launchParam) {
        let wantAgentInfo = {
            wants: [
                {
                    bundleName: "com.example.myapplication",
                    abilityName: "EntryAbility"
                }
            ],
            operationType: wantAgent.OperationType.START_ABILITY,
            requestCode: 0,
            wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
        };

        wantAgent.getWantAgent(wantAgentInfo).then((wantAgentObj) => {
            backgroundTaskManager.startBackgroundRunning(this.context,
                backgroundTaskManager.BackgroundMode.LOCATION, wantAgentObj, callback)
        });
    }
};
```

## backgroundTaskManager.startBackgroundRunning<sup>8+</sup>

startBackgroundRunning(context: Context, bgMode: BackgroundMode, wantAgent: WantAgent): Promise&lt;void&gt;

Requests a continuous task from the system. This API uses a promise to return the result.

**Required permissions**: ohos.permission.KEEP_BACKGROUND_RUNNING

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.ContinuousTask

**Parameters**

| Name   | Type                                         | Mandatory| Description                                                        |
| --------- | --------------------------------------------- | ---- | ------------------------------------------------------------ |
| context   | Context                                       | Yes  | Application context.<br>For details about the application context of the FA model, see [Context](js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](js-apis-inner-application-context.md).|
| bgMode    | [BackgroundMode](#backgroundmode8)            | Yes  | Background mode requested.                                      |
| wantAgent | [WantAgent](js-apis-app-ability-wantAgent.md) | Yes  | Notification parameter, which is used to specify the target page that is redirected to when a continuous task notification is clicked.              |

**Return value**

| Type            | Description              |
| -------------- | ---------------- |
| Promise\<void> | Promise used to return the result.|

**Example**

FA model:

```js
import backgroundTaskManager from '@ohos.backgroundTaskManager';
import featureAbility from '@ohos.ability.featureAbility';
import wantAgent from '@ohos.wantAgent';

let wantAgentInfo = {
    wants: [
        {
            bundleName: "com.example.myapplication",
            abilityName: "com.example.myapplication.MainAbility"
        }
    ],
    operationType: wantAgent.OperationType.START_ABILITY,
    requestCode: 0,
    wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

wantAgent.getWantAgent(wantAgentInfo).then((wantAgentObj) => {
    backgroundTaskManager.startBackgroundRunning(featureAbility.getContext(),
        backgroundTaskManager.BackgroundMode.LOCATION, wantAgentObj).then(() => {
        console.info("Operation startBackgroundRunning succeeded");
    }).catch((err) => {
        console.error("Operation startBackgroundRunning failed Cause: " + err);
    });
});
```

Stage model:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import backgroundTaskManager from '@ohos.backgroundTaskManager';
import wantAgent from '@ohos.app.ability.wantAgent';

export default class EntryAbility extends UIAbility {
    onCreate(want, launchParam) {
        let wantAgentInfo = {
            wants: [
                {
                    bundleName: "com.example.myapplication",
                    abilityName: "EntryAbility"
                }
            ],
            operationType: wantAgent.OperationType.START_ABILITY,
            requestCode: 0,
            wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
        };

        wantAgent.getWantAgent(wantAgentInfo).then((wantAgentObj) => {
            backgroundTaskManager.startBackgroundRunning(this.context,
                backgroundTaskManager.BackgroundMode.LOCATION, wantAgentObj).then(() => {
                console.info("Operation startBackgroundRunning succeeded");
            }).catch((err) => {
                console.error("Operation startBackgroundRunning failed Cause: " + err);
            });
        });
    }
};
```

## backgroundTaskManager.stopBackgroundRunning<sup>8+</sup>

stopBackgroundRunning(context: Context, callback: AsyncCallback&lt;void&gt;): void

Requests to cancel a continuous task. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.ContinuousTask

**Parameters**

| Name     | Type                       | Mandatory  | Description                                      |
| -------- | ------------------------- | ---- | ---------------------------------------- |
| context  | Context                   | Yes   | Application context.<br>For details about the application context of the FA model, see [Context](js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](js-apis-inner-application-context.md).|
| callback | AsyncCallback&lt;void&gt; | Yes   | Callback used to return the result.                  |

**Example**

FA model:

```js
import backgroundTaskManager from '@ohos.backgroundTaskManager';
import featureAbility from '@ohos.ability.featureAbility';

function callback(err, data) {
    if (err) {
        console.error("Operation stopBackgroundRunning failed Cause: " + err);
    } else {
        console.info("Operation stopBackgroundRunning succeeded");
    }
}

backgroundTaskManager.stopBackgroundRunning(featureAbility.getContext(), callback);

```

Stage model:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import backgroundTaskManager from '@ohos.backgroundTaskManager';

function callback(err, data) {
    if (err) {
        console.error("Operation stopBackgroundRunning failed Cause: " + err);
    } else {
        console.info("Operation stopBackgroundRunning succeeded");
    }
}

export default class EntryAbility extends UIAbility {
    onCreate(want, launchParam) {
        backgroundTaskManager.stopBackgroundRunning(this.context, callback);
    }
};
```

## backgroundTaskManager.stopBackgroundRunning<sup>8+</sup>

stopBackgroundRunning(context: Context): Promise&lt;void&gt;

Requests to cancel a continuous task. This API uses a promise to return the result.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.ContinuousTask

**Parameters**

| Name    | Type     | Mandatory  | Description                                      |
| ------- | ------- | ---- | ---------------------------------------- |
| context | Context | Yes   | Application context.<br>For details about the application context of the FA model, see [Context](js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](js-apis-inner-application-context.md).|

**Return value**

| Type            | Description              |
| -------------- | ---------------- |
| Promise\<void> | Promise used to return the result.|

**Example**

FA model:

```js
import backgroundTaskManager from '@ohos.backgroundTaskManager';
import featureAbility from '@ohos.ability.featureAbility';

backgroundTaskManager.stopBackgroundRunning(featureAbility.getContext()).then(() => {
    console.info("Operation stopBackgroundRunning succeeded");
}).catch((err) => {
    console.error("Operation stopBackgroundRunning failed Cause: " + err);
});

```

Stage model:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import backgroundTaskManager from '@ohos.backgroundTaskManager';

export default class EntryAbility extends UIAbility {
    onCreate(want, launchParam) {
        backgroundTaskManager.stopBackgroundRunning(this.context).then(() => {
            console.info("Operation stopBackgroundRunning succeeded");
        }).catch((err) => {
            console.error("Operation stopBackgroundRunning failed Cause: " + err);
        });
    }
};
```

## DelaySuspendInfo

Provides the information about the suspension delay.

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.TransientTask

| Name            | Type    | Mandatory  | Description                                      |
| --------------- | ------ | ---- | ---------------------------------------- |
| requestId       | number | Yes   | ID of the suspension delay request.                              |
| actualDelayTime | number | Yes   | Actual suspension delay duration of the application, in milliseconds.<br>The default duration is 180000 when the battery level is higher than or equal to the broadcast low battery level and 60000 when the battery level is lower than the broadcast low battery level.|


## BackgroundMode<sup>8+</sup>

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.ContinuousTask

| Name                    | Value | Description                   |
| ----------------------- | ---- | --------------------- |
| DATA_TRANSFER           | 1    | Data transfer.                 |
| AUDIO_PLAYBACK          | 2    | Audio playback.                 |
| AUDIO_RECORDING         | 3    | Audio recording.                   |
| LOCATION                | 4    | Positioning and navigation.                 |
| BLUETOOTH_INTERACTION   | 5    | Bluetooth-related task.                 |
| MULTI_DEVICE_CONNECTION | 6    | Multi-device connection.                |
| WIFI_INTERACTION        | 7    | WLAN-related.<br>This is a system API.|
| VOIP                    | 8    | Audio and video calls.<br>This is a system API. |
| TASK_KEEPING            | 9    | Computing task (effective only for specific devices).       |
