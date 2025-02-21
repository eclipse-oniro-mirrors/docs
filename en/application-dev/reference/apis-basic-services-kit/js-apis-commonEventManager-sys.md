# @ohos.commonEventManager (Common Event) (System API)

The **CommonEventManager** module provides common event capabilities, including the capabilities to publish, subscribe to, and unsubscribe from common events.

> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
> This topic describes only system APIs provided by the module. For details about its public APIs, see [CommonEventManager](./js-apis-commonEventManager.md).

## Modules to Import

```ts
import CommonEventManager from '@ohos.commonEventManager';
```

## Support

A system common event is an event that is published by a system service or system application and requires specific permissions to subscribe to. To publish or subscribe to this type of event, you must follow the event-specific definitions.

For details about the enumerations of all system common events, see [System Common Events](./common_event/commonEventManager-definitions.md).

## CommonEventManager.publishAsUser<sup>

publishAsUser(event: string, userId: number, callback: AsyncCallback\<void>): void

Publishes a common event to a specific user. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.CommonEvent

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                | Mandatory| Description                              |
| -------- | -------------------- | ---- | ---------------------------------- |
| event    | string               | Yes  | Name of the common event to publish. For details, see [System Common Events](./common_event/commonEventManager-definitions.md).            |
| userId   | number               | Yes  | User ID.|
| callback | AsyncCallback\<void> | Yes  | Callback used to return the result.            |

**Error codes**

For details about the error codes, see [Event Error Codes](./errorcode-CommonEventService.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 1500004  | not System services.                |
| 1500007  | error sending message to Common Event Service. |
| 1500008  | Common Event Service does not complete initialization. |
| 1500009  | error obtaining system parameters.  |

**Example**

```ts
import Base from '@ohos.base';

// Callback for common event publication
function publishCB(err:Base.BusinessError) {
	if (err) {
        console.error(`publishAsUser failed, code is ${err.code}, message is ${err.message}`);
    } else {
        console.info("publishAsUser");
    }
}

// Specify the user to whom the common event will be published.
let userId = 100;

// Publish a common event.
try {
    CommonEventManager.publishAsUser("event", userId, publishCB);
} catch (error) {
    let err:Base.BusinessError = error as Base.BusinessError;
    console.error(`publishAsUser failed, code is ${err.code}, message is ${err.message}`);
}
```

## CommonEventManager.publishAsUser

publishAsUser(event: string, userId: number, options: CommonEventPublishData, callback: AsyncCallback\<void>): void

Publishes a common event with given attributes to a specific user. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.CommonEvent

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                  | Mandatory| Description                  |
| -------- | ---------------------- | ---- | ---------------------- |
| event    | string                 | Yes  | Name of the common event to publish. For details, see [System Common Events](./common_event/commonEventManager-definitions.md). |
| userId   | number | Yes| User ID.|
| options  | [CommonEventPublishData](./js-apis-inner-commonEvent-commonEventPublishData.md) | Yes  | Attributes of the common event to publish.|
| callback | AsyncCallback\<void>   | Yes  | Callback used to return the result. |

**Error codes**

For details about the error codes, see [Event Error Codes](./errorcode-CommonEventService.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 1500004  | not System services or System app.                |
| 1500007  | error sending message to Common Event Service. |
| 1500008  | Common Event Service does not complete initialization. |
| 1500009  | error obtaining system parameters.  |

**Example**


```ts
import Base from '@ohos.base';

// Attributes of a common event.
let options:CommonEventManager.CommonEventPublishData = {
	code: 0,			 // Result code of the common event.
	data: "initial data",// Result data of the common event.
}

// Callback for common event publication
function publishCB(err:Base.BusinessError) {
	if (err) {
        console.error(`publishAsUser failed, code is ${err.code}, message is ${err.message}`);
    } else {
        console.info("publishAsUser");
    }
}

// Specify the user to whom the common event will be published.
let userId = 100;

// Publish a common event.
try {
    CommonEventManager.publishAsUser("event", userId, options, publishCB);
} catch (error) {
    let err:Base.BusinessError = error as Base.BusinessError;
    console.error(`publishAsUser failed, code is ${err.code}, message is ${err.message}`);
}
```

## CommonEventManager.removeStickyCommonEvent<sup>10+</sup>

removeStickyCommonEvent(event: string, callback: AsyncCallback\<void>): void

Removes a sticky common event. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.CommonEvent

**Required permissions**: ohos.permission.COMMONEVENT_STICKY

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type                | Mandatory| Description                            |
| -------- | -------------------- | ---- | -------------------------------- |
| event    | string               | Yes  | Sticky common event to remove. For details, see [System Common Events](./common_event/commonEventManager-definitions.md).      |
| callback | AsyncCallback\<void> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Event Error Codes](./errorcode-CommonEventService.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 1500004  | not system service.                 |
| 1500007  | error sending message to Common Event Service.             |
| 1500008  | Common Event Service does not complete initialization.     |

**Example**


```ts
import Base from '@ohos.base';

CommonEventManager.removeStickyCommonEvent("sticky_event", (err:Base.BusinessError) => {
    if (err) {
        console.info(`removeStickyCommonEvent failed, errCode: ${err.code}, errMes: ${err.message}`);
        return;
    }
    console.info(`removeStickyCommonEvent success`);
});
```

## CommonEventManager.removeStickyCommonEvent<sup>10+</sup>

removeStickyCommonEvent(event: string): Promise\<void>

Removes a sticky common event. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.CommonEvent

**Required permissions**: ohos.permission.COMMONEVENT_STICKY

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type  | Mandatory| Description                      |
| ------ | ------ | ---- | -------------------------- |
| event  | string | Yes  | Sticky common event to remove. For details, see [System Common Events](./common_event/commonEventManager-definitions.md).|

**Return value**

| Type          | Description                        |
| -------------- | ---------------------------- |
| Promise\<void> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Event Error Codes](./errorcode-CommonEventService.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 1500004  | not system service.                 |
| 1500007  | error sending message to Common Event Service.             |
| 1500008  | Common Event Service does not complete initialization.     |

**Example**


```ts
import Base from '@ohos.base';

CommonEventManager.removeStickyCommonEvent("sticky_event").then(() => {
    console.info(`removeStickyCommonEvent success`);
}).catch ((err:Base.BusinessError) => {
    console.info(`removeStickyCommonEvent failed, errCode: ${err.code}, errMes: ${err.message}`);
});
```

## CommonEventManager.setStaticSubscriberState<sup>10+</sup>

setStaticSubscriberState(enable: boolean, callback: AsyncCallback\<void>): void;

Enables or disables static subscription for the current application. This API uses an asynchronous callback to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.Notification.CommonEvent

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type  | Mandatory| Description                      |
| ------ | ------ | ---- | -------------------------- |
| enable  | boolean | Yes  | Whether static subscription is enabled.<br> **true**: enabled.<br>**false**: disabled.|
| callback  | AsyncCallback\<void> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Event Error Codes](./errorcode-CommonEventService.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 1500007  | error sending message to Common Event Service.             |
| 1500008  | Common Event Service does not complete initialization.     |

**Example**


```ts
import Base from '@ohos.base';

CommonEventManager.setStaticSubscriberState(true, (err:Base.BusinessError) => {
    if (!err) {
        console.info(`setStaticSubscriberState failed, err is null.`);
        return;
    }
    if (err.code !== undefined && err.code != null) {
        console.info(`setStaticSubscriberState failed, errCode: ${err.code}, errMes: ${err.message}`);
        return;
    }
    console.info(`setStaticSubscriberState success`);
});
```

## CommonEventManager.setStaticSubscriberState<sup>10+</sup>

setStaticSubscriberState(enable: boolean): Promise\<void>;

Enables or disables static subscription for the current application. This API uses a promise to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.Notification.CommonEvent

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type  | Mandatory| Description                      |
| ------ | ------ | ---- | -------------------------- |
| enable  | boolean | Yes  | Whether static subscription is enabled.<br> **true**: enabled.<br>**false**: disabled.|

**Return value**

| Type          | Description                        |
| -------------- | ---------------------------- |
| Promise\<void> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Event Error Codes](./errorcode-CommonEventService.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 1500007  | error sending message to Common Event Service.             |
| 1500008  | Common Event Service does not complete initialization.     |

**Example**


```ts
import Base from '@ohos.base';

CommonEventManager.setStaticSubscriberState(false).then(() => {
    console.info(`setStaticSubscriberState success`);
}).catch ((err:Base.BusinessError) => {
    console.info(`setStaticSubscriberState failed, errCode: ${err.code}, errMes: ${err.message}`);
});
```
