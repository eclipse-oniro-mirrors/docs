# @ohos.ability.particleAbility (ParticleAbility)

The **particleAbility** module provides APIs for operating a DataAbility and ServiceAbility. You can use the APIs to start and terminate a ParticleAbility, obtain a **dataAbilityHelper** object, and connect to or disconnect from a ServiceAbility.

> **NOTE**
> 
> The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version. 
> The APIs of this module can be used only in the FA model.

## Constraints

The ParticleAbility module is used to perform operations on abilities of the Data and Service types.

## Modules to Import

```ts
import particleAbility from '@ohos.ability.particleAbility';
```

## particleAbility.startAbility

startAbility(parameter: StartAbilityParameter, callback: AsyncCallback\<void>): void

Starts a ParticleAbility. This API uses an asynchronous callback to return the result.

Observe the following when using this API:
 - If an application running in the background needs to call this API to start an ability, it must have the **ohos.permission.START_ABILITIES_FROM_BACKGROUND** permission.
 - If **visible** of the target ability is **false**, the caller must have the **ohos.permission.START_INVISIBLE_ABILITY** permission.
 - For details about the startup rules for the components in the FA model, see [Component Startup Rules (FA Model)](../../application-models/component-startup-rules-fa.md).

**System capability**: SystemCapability.Ability.AbilityRuntime.FAModel

**Parameters**

| Name     | Type                                           | Mandatory| Description             |
| --------- | ----------------------------------------------- | ---- | ----------------- |
| parameter | [StartAbilityParameter](js-apis-inner-ability-startAbilityParameter.md) | Yes  | Ability to start.|
| callback  | AsyncCallback\<void>                            | Yes  | Callback used to return the result. |

**Example**

```ts
import particleAbility from '@ohos.ability.particleAbility';
import wantConstant from '@ohos.app.ability.wantConstant';

particleAbility.startAbility(
    {
        want:
        {
            action: 'ohos.want.action.home',
            entities: ['entity.system.home'],
            type: 'MIMETYPE',
            flags: wantConstant.Flags.FLAG_AUTH_READ_URI_PERMISSION,
            deviceId: '',
            bundleName: 'com.example.Data',
            abilityName: 'com.example.Data.MainAbility',
            uri: ''
        },
    },
    (error, result) => {
        console.log('particleAbility startAbility errCode:' + error + 'result:' + result);
    },
);
```

## particleAbility.startAbility

startAbility(parameter: StartAbilityParameter): Promise\<void>

Starts a ParticleAbility. This API uses a promise to return the result.

Observe the following when using this API:
 - If an application running in the background needs to call this API to start an ability, it must have the **ohos.permission.START_ABILITIES_FROM_BACKGROUND** permission.
 - If **visible** of the target ability is **false**, the caller must have the **ohos.permission.START_INVISIBLE_ABILITY** permission.
 - For details about the startup rules for the components in the FA model, see [Component Startup Rules (FA Model)](../../application-models/component-startup-rules-fa.md).

**System capability**: SystemCapability.Ability.AbilityRuntime.FAModel

**Parameters**

| Name     | Type                                           | Mandatory| Description             |
| --------- | ----------------------------------------------- | ---- | ----------------- |
| parameter | [StartAbilityParameter](js-apis-inner-ability-startAbilityParameter.md) | Yes  | Ability to start.|

**Return value**

| Type          | Description                     |
| -------------- | ------------------------- |
| Promise\<void> | Promise that returns no value.|

**Example**

```ts
import particleAbility from '@ohos.ability.particleAbility';
import wantConstant from '@ohos.app.ability.wantConstant';

particleAbility.startAbility(
    {
        want:
        {
            action: 'ohos.want.action.home',
            entities: ['entity.system.home'],
            type: 'MIMETYPE',
            flags: wantConstant.Flags.FLAG_AUTH_READ_URI_PERMISSION,
            deviceId: '',
            bundleName: 'com.example.Data',
            abilityName: 'com.example. Data.MainAbility',
            uri: ''
        },
    },
).then((data) => {
    console.info('particleAbility startAbility');
});
```

## particleAbility.terminateSelf

terminateSelf(callback: AsyncCallback\<void>): void

Terminates this ParticleAbility. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.FAModel

**Parameters**

| Name    | Type                | Mandatory| Description                |
| -------- | -------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void> | Yes  | Callback used to return the result.|

**Example**

```ts
import particleAbility from '@ohos.ability.particleAbility';

particleAbility.terminateSelf(
    (error, result) => {
        console.log('particleAbility terminateSelf errCode:' + error + 'result:' + result);
    }
);
```

## particleAbility.terminateSelf

terminateSelf(): Promise\<void>

Terminates this ParticleAbility. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.FAModel

**Return value**

| Type          | Description                     |
| -------------- | ------------------------- |
| Promise\<void> | Promise that returns no value.|

**Example**

```ts
import particleAbility from '@ohos.ability.particleAbility';

particleAbility.terminateSelf().then((data) => {
	console.info('particleAbility terminateSelf');
});
```



## particleAbility.acquireDataAbilityHelper

acquireDataAbilityHelper(uri: string): DataAbilityHelper

Obtains a **dataAbilityHelper** object.

**System capability**: SystemCapability.Ability.AbilityRuntime.FAModel

**Parameters**

| Name| Type  | Mandatory| Description                    |
| :--- | ------ | ---- | ------------------------ |
| uri  | string | Yes  | URI of the file to open.|

**Return value**

| Type             | Description                                        |
| ----------------- | -------------------------------------------- |
| [DataAbilityHelper](js-apis-inner-ability-dataAbilityHelper.md) | A utility class used to help other abilities access a DataAbility.|

**Example**

```ts
import particleAbility from '@ohos.ability.particleAbility';

let uri = '';
particleAbility.acquireDataAbilityHelper(uri);
```


## particleAbility.startBackgroundRunning<sup>(deprecated)</sup>

startBackgroundRunning(id: number, request: NotificationRequest, callback: AsyncCallback&lt;void&gt;): void

Requests a continuous task from the system. This API uses an asynchronous callback to return the result. You are advised to use the new API [backgroundTaskManager.startBackgroundRunning](js-apis-backgroundTaskManager.md#backgroundtaskmanagerstartbackgroundrunning8).

**Required permissions**: ohos.permission.KEEP_BACKGROUND_RUNNING

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.ContinuousTask

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | id | number | Yes| Notification ID of a continuous task.|
  | request | [NotificationRequest](js-apis-notification.md#notificationrequest) | Yes| Notification parameter, which is used to display information in the notification bar.|
  | callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

 **Example**

```ts
import notification from '@ohos.notification';
import particleAbility from '@ohos.ability.particleAbility';
import wantAgent from '@ohos.wantAgent';

function callback(err, data) {
    if (err) {
        console.error('Operation failed cause: ' + JSON.stringify(err));
    } else {
        console.info('Operation succeeded');
    }
}

let wantAgentInfo = {
    wants: [
        {
            bundleName: 'com.example.myapplication',
            abilityName: 'com.example.myapplication.MainAbility'
        }
    ],
    operationType: wantAgent.OperationType.START_ABILITY,
    requestCode: 0,
    wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

wantAgent.getWantAgent(wantAgentInfo).then((wantAgentObj) => {
    let basicContent = {
        title: 'title',
        text: 'text'
    };
    let notificationContent = {
        contentType: notification.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT,
        normal: basicContent
    };
    let request = {
        content: notificationContent,
        wantAgent: wantAgentObj
    };
    let id = 1;
    particleAbility.startBackgroundRunning(id, request, callback);
});

```

## particleAbility.startBackgroundRunning<sup>(deprecated)</sup>

startBackgroundRunning(id: number, request: NotificationRequest): Promise&lt;void&gt;

**Required permissions**: ohos.permission.KEEP_BACKGROUND_RUNNING

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.ContinuousTask

Requests a continuous task from the system. This API uses a promise to return the result. You are advised to use the new API [backgroundTaskManager.startBackgroundRunning](js-apis-backgroundTaskManager.md#backgroundtaskmanagerstartbackgroundrunning8-1).

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| id | number | Yes| Notification ID of a continuous task.|
| request | [NotificationRequest](js-apis-notification.md#notificationrequest) | Yes| Notification parameter, which is used to display information in the notification bar.|

**Return value**

| Type          | Description                     |
| -------------- | ------------------------- |
| Promise\<void> | Promise that returns no value.|

**Example**

```ts
import notification from '@ohos.notification';
import particleAbility from '@ohos.ability.particleAbility';
import wantAgent from '@ohos.wantAgent';

let wantAgentInfo = {
    wants: [
        {
            bundleName: 'com.example.myapplication',
            abilityName: 'com.example.myapplication.MainAbility'
        }
    ],
    operationType: wantAgent.OperationType.START_ABILITY,
    requestCode: 0,
    wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
};

wantAgent.getWantAgent(wantAgentInfo).then((wantAgentObj) => {
    let basicContent = {
        title: 'title',
        text: 'text'
    };
    let notificationContent = {
        contentType: notification.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT,
        normal: basicContent
    };
    let request = {
        content: notificationContent,
        wantAgent: wantAgentObj
    };
    let id = 1;
    particleAbility.startBackgroundRunning(id, request).then(() => {
        console.info('Operation succeeded');
    }).catch((err) => {
        console.error('Operation failed cause: ' + JSON.stringify(err));
    });
});

```

## particleAbility.cancelBackgroundRunning<sup>(deprecated)</sup>

cancelBackgroundRunning(callback: AsyncCallback&lt;void&gt;): void

Requests to cancel a continuous task from the system. This API uses an asynchronous callback to return the result. You are advised to use the new API [backgroundTaskManager.stopBackgroundRunning](js-apis-backgroundTaskManager.md#backgroundtaskmanagerstopbackgroundrunning8).

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.ContinuousTask

 **Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

 **Example**

```ts
import particleAbility from '@ohos.ability.particleAbility';

function callback(err, data) {
    if (err) {
        console.error('Operation failed cause: ' + JSON.stringify(err));
    } else {
        console.info('Operation succeeded');
    }
}

particleAbility.cancelBackgroundRunning(callback);

```

## particleAbility.cancelBackgroundRunning<sup>(deprecated)</sup>

cancelBackgroundRunning(): Promise&lt;void&gt;

Requests to cancel a continuous task from the system. This API uses a promise to return the result. You are advised to use the new API [backgroundTaskManager.stopBackgroundRunning](js-apis-backgroundTaskManager.md#backgroundtaskmanagerstopbackgroundrunning8-1).

**System capability**: SystemCapability.ResourceSchedule.BackgroundTaskManager.ContinuousTask

**Return value**

| Type          | Description                     |
| -------------- | ------------------------- |
| Promise\<void> | Promise that returns no value.|

 **Example**

```ts
import particleAbility from '@ohos.ability.particleAbility';
import { BusinessError } from '@ohos.base';

particleAbility.cancelBackgroundRunning().then(() => {
    console.info('Operation succeeded');
}).catch((err) => {
    console.error('Operation failed cause: ' + JSON.stringify(err));
});

```

## particleAbility.connectAbility

connectAbility(request: Want, options:ConnectOptions): number

Connects this ability to a specific ServiceAbility.

**System capability**: SystemCapability.Ability.AbilityRuntime.FAModel

**Parameters**

| Name   | Type          | Mandatory| Description                        |
| ------- | -------------- | ---- | ---------------------------- |
| request | [Want](js-apis-application-want.md)           | Yes  | ServiceAbility to connect.|
| options | [ConnectOptions](js-apis-inner-ability-connectOptions.md) | Yes  | Connection options.          |

**Return value**

| Type    | Description                  |
| ------ | -------------------- |
| number | ID of the connected ServiceAbility. The ID starts from 0 and is incremented by 1 each time a connection is set up.|


**Example**

```ts
import particleAbility from '@ohos.ability.particleAbility';
import rpc from '@ohos.rpc';
import { BusinessError } from '@ohos.base';

function onConnectCallback(element, remote) {
    console.log('ConnectAbility onConnect remote is proxy:' + (remote instanceof rpc.RemoteProxy));
}

function onDisconnectCallback(element) {
    console.log('ConnectAbility onDisconnect element.deviceId : ' + element.deviceId);
}

function onFailedCallback(code) {
    console.log('particleAbilityTest ConnectAbility onFailed errCode : ' + code);
}

let connId = particleAbility.connectAbility(
    {
        bundleName: 'com.ix.ServiceAbility',
        abilityName: 'ServiceAbilityA',
    },
    {
        onConnect: onConnectCallback,
        onDisconnect: onDisconnectCallback,
        onFailed: onFailedCallback,
    },
);

particleAbility.disconnectAbility(connId).then((data) => {
    console.log(' data: ' + data);
}).catch((error) => {
    console.log('particleAbilityTest result errCode : ' + error.code);
});
```

## particleAbility.disconnectAbility

disconnectAbility(connection: number, callback:AsyncCallback\<void>): void

Disconnects this ability from a specific ServiceAbility. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.FAModel

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | connection | number               | Yes   | ID of the ServiceAbility to disconnect.|
  | callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

**Example**

```ts
import particleAbility from '@ohos.ability.particleAbility';
import rpc from '@ohos.rpc';

function onConnectCallback(element, remote) {
    console.log('ConnectAbility onConnect remote is proxy:' + (remote instanceof rpc.RemoteProxy));
}

function onDisconnectCallback(element) {
    console.log('ConnectAbility onDisconnect element.deviceId : ' + element.deviceId);
}

function onFailedCallback(code) {
    console.log('particleAbilityTest ConnectAbility onFailed errCode : ' + code);
}

let connId = particleAbility.connectAbility(
    {
        bundleName: 'com.ix.ServiceAbility',
        abilityName: 'ServiceAbilityA',
    },
    {
        onConnect: onConnectCallback,
        onDisconnect: onDisconnectCallback,
        onFailed: onFailedCallback,
    },
);

particleAbility.disconnectAbility(connId, (err) => {
    console.log('particleAbilityTest disconnectAbility err====>'
    + ('json err=') + JSON.stringify(err));
});
```


## particleAbility.disconnectAbility

disconnectAbility(connection: number): Promise\<void>

Disconnects this ability from a specific ServiceAbility. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.FAModel

**Return value**

| Type          | Description                     |
| -------------- | ------------------------- |
| connection | number               | Yes   | ID of the ServiceAbility to disconnect.|
| Promise\<void> | Promise that returns no value.|

**Example**

```ts
import particleAbility from '@ohos.ability.particleAbility';
import rpc from '@ohos.rpc';

function onConnectCallback(element, remote) {
    console.log('ConnectAbility onConnect remote is proxy:' + (remote instanceof rpc.RemoteProxy));
}

function onDisconnectCallback(element) {
    console.log('ConnectAbility onDisconnect element.deviceId : ' + element.deviceId);
}

function onFailedCallback(code) {
    console.log('particleAbilityTest ConnectAbility onFailed errCode : ' + code);
}

let connId = particleAbility.connectAbility(
    {
        bundleName: 'com.ix.ServiceAbility',
        abilityName: 'ServiceAbilityA',
    },
    {
        onConnect: onConnectCallback,
        onDisconnect: onDisconnectCallback,
        onFailed: onFailedCallback,
    },
);

particleAbility.disconnectAbility(connId).then((data) => {
    console.log(' data: ' + data);
}).catch((error) => {
    console.log('particleAbilityTest result errCode : ' + error.code);
});

```

## ErrorCode

Enumerates the error codes.

**System capability**: SystemCapability.Ability.AbilityRuntime.FAModel

| Name                         | Value  | Description                                                        |
| ----------------------------- | ---- | ------------------------------------------------------------ |
| INVALID_PARAMETER         | -1    | Invalid parameter.|
