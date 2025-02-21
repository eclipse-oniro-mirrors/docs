# @ohos.notification (Notification)

The **Notification** module provides notification management capabilities, covering notifications, notification slots, notification subscription, notification enabled status, and notification badge status.

> **NOTE**
>
> The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
> Notification subscription and unsubscription APIs are available only to system applications.

## Modules to Import

```js
import Notification from '@ohos.notification';
```

## Notification.publish

publish(request: NotificationRequest, callback: AsyncCallback\<void\>): void

Publishes a notification. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                                       | Mandatory| Description                                       |
| -------- | ------------------------------------------- | ---- | ------------------------------------------- |
| request  | [NotificationRequest](#notificationrequest) | Yes  | Content and related configuration of the notification to publish.|
| callback | AsyncCallback\<void\>                       | Yes  | Callback used to return the result.                       |

**Example**

```js
// publish callback
function publishCallback(err) {
    if (err.code) {
        console.info("publish failed " + JSON.stringify(err));
    } else {
        console.info("publish success");
    }
}
// NotificationRequest object
let notificationRequest = {
    id: 1,
    content: {
        contentType: Notification.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT,
        normal: {
            title: "test_title",
            text: "test_text",
            additionalText: "test_additionalText"
        }
    }
};
Notification.publish(notificationRequest, publishCallback);
```



## Notification.publish

publish(request: NotificationRequest): Promise\<void\>

Publishes a notification. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                                       | Mandatory| Description                                       |
| -------- | ------------------------------------------- | ---- | ------------------------------------------- |
| request  | [NotificationRequest](#notificationrequest) | Yes  | Content and related configuration of the notification to publish.|

**Example**

```js
// NotificationRequest object
let notificationRequest = {
    id: 1,
    content: {
        contentType: Notification.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT,
        normal: {
            title: "test_title",
            text: "test_text",
            additionalText: "test_additionalText"
        }
    }
};
Notification.publish(notificationRequest).then(() => {
	console.info("publish success");
});

```

## Notification.publish<sup>8+</sup>

publish(request: NotificationRequest, userId: number, callback: AsyncCallback\<void\>): void

Publishes a notification to a specified user. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                                       | Mandatory| Description                                       |
| -------- | ----------------------------------------- | ---- | ------------------------------------------- |
| request  | [NotificationRequest](#notificationrequest) | Yes  | Content and related configuration of the notification to publish.|
| userId   | number                                      | Yes  | User ID.                          |
| callback | AsyncCallback\<void\>                       | Yes  | Callback used to return the result.                          |

**Example**

```js
// publish callback
function publishCallback(err) {
    if (err.code) {
        console.info("publish failed " + JSON.stringify(err));
    } else {
        console.info("publish success");
    }
}
// User ID
let userId = 1;
// NotificationRequest object
let notificationRequest = {
    id: 1,
    content: {
        contentType: Notification.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT,
        normal: {
            title: "test_title",
            text: "test_text",
            additionalText: "test_additionalText"
        }
    }
};
Notification.publish(notificationRequest, userId, publishCallback);
```

## Notification.publish<sup>8+</sup>

publish(request: NotificationRequest, userId: number): Promise\<void\>

Publishes a notification to a specified user. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    |  Type                                       | Mandatory| Description                                       |
| -------- | ----------------------------------------- | ---- | ------------------------------------------- |
| request  | [NotificationRequest](#notificationrequest) | Yes  | Content and related configuration of the notification to publish.|
| userId   | number                                      | Yes  | User ID.                          |

**Example**

```js
let notificationRequest = {
    id: 1,
    content: {
        contentType: Notification.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT,
        normal: {
            title: "test_title",
            text: "test_text",
            additionalText: "test_additionalText"
        }
    }
};

let userId = 1;

Notification.publish(notificationRequest, userId).then(() => {
	console.info("publish success");
});
```


## Notification.cancel

cancel(id: number, label: string, callback: AsyncCallback\<void\>): void

Cancels a notification with the specified ID and label. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                 | Mandatory| Description                |
| -------- | --------------------- | ---- | -------------------- |
| id       | number                | Yes  | Notification ID.              |
| label    | string                | Yes  | Notification label.            |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```js
// cancel callback
function cancelCallback(err) {
    if (err.code) {
        console.info("cancel failed " + JSON.stringify(err));
    } else {
        console.info("cancel success");
    }
}
Notification.cancel(0, "label", cancelCallback);
```



## Notification.cancel

cancel(id: number, label?: string): Promise\<void\>

Cancels a notification with the specified ID and optional label. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name | Type  | Mandatory| Description    |
| ----- | ------ | ---- | -------- |
| id    | number | Yes  | Notification ID.  |
| label | string | No  | Notification label.|

**Example**

```js
Notification.cancel(0).then(() => {
	console.info("cancel success");
});
```



## Notification.cancel

cancel(id: number, callback: AsyncCallback\<void\>): void

Cancels a notification with the specified ID. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                 | Mandatory| Description                |
| -------- | --------------------- | ---- | -------------------- |
| id       | number                | Yes  | Notification ID.              |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```js
// cancel callback
function cancelCallback(err) {
    if (err.code) {
        console.info("cancel failed " + JSON.stringify(err));
    } else {
        console.info("cancel success");
    }
}
Notification.cancel(0, cancelCallback);
```



## Notification.cancelAll

cancelAll(callback: AsyncCallback\<void\>): void

Cancels all notifications. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                 | Mandatory| Description                |
| -------- | --------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```js
// cancel callback
function cancelAllCallback(err) {
    if (err.code) {
        console.info("cancelAll failed " + JSON.stringify(err));
    } else {
        console.info("cancelAll success");
    }
}
Notification.cancelAll(cancelAllCallback);
```



## Notification.cancelAll

cancelAll(): Promise\<void\>

Cancels all notifications. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Example**

```js
Notification.cancelAll().then(() => {
	console.info("cancelAll success");
});
```



## Notification.addSlot

addSlot(slot: NotificationSlot, callback: AsyncCallback\<void\>): void

Adds a notification slot. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                 | Mandatory| Description                |
| -------- | --------------------- | ---- | -------------------- |
| slot     | [NotificationSlot](#notificationslot)       | Yes  | Notification slot to add.|
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```js
// addSlot callback
function addSlotCallBack(err) {
    if (err.code) {
        console.info("addSlot failed " + JSON.stringify(err));
    } else {
        console.info("addSlot success");
    }
}
// NotificationSlot object
let notificationSlot = {
    type: Notification.SlotType.SOCIAL_COMMUNICATION
};
Notification.addSlot(notificationSlot, addSlotCallBack);
```



## Notification.addSlot

addSlot(slot: NotificationSlot): Promise\<void\>

Adds a notification slot. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type            | Mandatory| Description                |
| ---- | ---------------- | ---- | -------------------- |
| slot | [NotificationSlot](#notificationslot) | Yes  | Notification slot to add.|

**Example**

```js
// NotificationSlot object
let notificationSlot = {
    type: Notification.SlotType.SOCIAL_COMMUNICATION
};
Notification.addSlot(notificationSlot).then(() => {
	console.info("addSlot success");
});
```



## Notification.addSlot

addSlot(type: SlotType, callback: AsyncCallback\<void\>): void

Adds a notification slot of a specified type. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                 | Mandatory| Description                  |
| -------- | --------------------- | ---- | ---------------------- |
| type     | [SlotType](#slottype)              | Yes  | Type of the notification slot to add.|
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.  |

**Example**

```js
// addSlot callback
function addSlotCallBack(err) {
    if (err.code) {
        console.info("addSlot failed " + JSON.stringify(err));
    } else {
        console.info("addSlot success");
    }
}
Notification.addSlot(Notification.SlotType.SOCIAL_COMMUNICATION, addSlotCallBack);
```



## Notification.addSlot

addSlot(type: SlotType): Promise\<void\>

Adds a notification slot of a specified type. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name| Type    | Mandatory| Description                  |
| ---- | -------- | ---- | ---------------------- |
| type | [SlotType](#slottype) | Yes  | Type of the notification slot to add.|

**Example**

```js
Notification.addSlot(Notification.SlotType.SOCIAL_COMMUNICATION).then(() => {
	console.info("addSlot success");
});
```



## Notification.addSlots

addSlots(slots: Array\<NotificationSlot\>, callback: AsyncCallback\<void\>): void

Adds an array of notification slots. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                     | Mandatory| Description                    |
| -------- | ------------------------- | ---- | ------------------------ |
| slots    | Array\<[NotificationSlot](#notificationslot)\> | Yes  | Notification slots to add.|
| callback | AsyncCallback\<void\>     | Yes  | Callback used to return the result.    |

**Example**

```js
// addSlots callback
function addSlotsCallBack(err) {
    if (err.code) {
        console.info("addSlots failed " + JSON.stringify(err));
    } else {
        console.info("addSlots success");
    }
}
// NotificationSlot object
let notificationSlot = {
    type: Notification.SlotType.SOCIAL_COMMUNICATION
};
// NotificationSlotArray object
let notificationSlotArray = new Array();
notificationSlotArray[0] = notificationSlot;

Notification.addSlots(notificationSlotArray, addSlotsCallBack);
```



## Notification.addSlots

addSlots(slots: Array\<NotificationSlot\>): Promise\<void\>

Adds an array of notification slots. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name | Type                     | Mandatory| Description                    |
| ----- | ------------------------- | ---- | ------------------------ |
| slots | Array\<[NotificationSlot](#notificationslot)\> | Yes  | Notification slots to add.|

**Example**

```js
// NotificationSlot object
let notificationSlot = {
    type: Notification.SlotType.SOCIAL_COMMUNICATION
};
// NotificationSlotArray object
let notificationSlotArray = new Array();
notificationSlotArray[0] = notificationSlot;

Notification.addSlots(notificationSlotArray).then(() => {
	console.info("addSlots success");
});
```



## Notification.getSlot

getSlot(slotType: SlotType, callback: AsyncCallback\<NotificationSlot\>): void

Obtains a notification slot of a specified type. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                             | Mandatory| Description                                                       |
| -------- | --------------------------------- | ---- | ----------------------------------------------------------- |
| slotType | [SlotType](#slottype)                          | Yes  | Type of the notification slot, which can be used for social communication, service information, content consultation, and other purposes.|
| callback | AsyncCallback\<[NotificationSlot](#notificationslot)\> | Yes  | Callback used to return the result.                                       |

**Example**

```js
// getSlot callback
function getSlotCallback(err, data) {
    if (err.code) {
        console.info("getSlot failed " + JSON.stringify(err));
    } else {
        console.info("getSlot success");
    }
}
let slotType = Notification.SlotType.SOCIAL_COMMUNICATION;
Notification.getSlot(slotType, getSlotCallback);
```



## Notification.getSlot

getSlot(slotType: SlotType): Promise\<NotificationSlot\>

Obtains a notification slot of a specified type. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type    | Mandatory| Description                                                       |
| -------- | -------- | ---- | ----------------------------------------------------------- |
| slotType | [SlotType](#slottype) | Yes  | Type of the notification slot, which can be used for social communication, service information, content consultation, and other purposes.|

**Return value**

| Type                                                       | Description                                                        |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<NotificationSlot\> | Promise used to return the result.|

**Example**

```js
let slotType = Notification.SlotType.SOCIAL_COMMUNICATION;
Notification.getSlot(slotType).then((data) => {
	console.info("getSlot success, data: " + JSON.stringify(data));
});
```



## Notification.getSlots

getSlots(callback: AsyncCallback\<Array\<NotificationSlot>>): void

Obtains all notification slots. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                             | Mandatory| Description                |
| -------- | --------------------------------- | ---- | -------------------- |
| callback | AsyncCallback\<Array\<[NotificationSlot](#notificationslot)>> | Yes  | Callback used to return the result.|

**Example**

```js
// getSlots callback
function getSlotsCallback(err, data) {
    if (err.code) {
        console.info("getSlots failed " + JSON.stringify(err));
    } else {
        console.info("getSlots success");
    }
}
Notification.getSlots(getSlotsCallback);
```



## Notification.getSlots

getSlots(): Promise\<Array\<NotificationSlot\>>

Obtains all notification slots of this application. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Return value**

| Type                                                       | Description                                                        |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<Array\<[NotificationSlot](#notificationslot)\>\> | Promise used to return the result.|

**Example**

```js
Notification.getSlots().then((data) => {
	console.info("getSlots success, data: " + JSON.stringify(data));
});
```



## Notification.removeSlot

removeSlot(slotType: SlotType, callback: AsyncCallback\<void\>): void

Removes a notification slot of a specified type. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                 | Mandatory| Description                                                       |
| -------- | --------------------- | ---- | ----------------------------------------------------------- |
| slotType | [SlotType](#slottype)              | Yes  | Type of the notification slot, which can be used for social communication, service information, content consultation, and other purposes.|
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.                                       |

**Example**

```js
// removeSlot callback
function removeSlotCallback(err) {
    if (err.code) {
        console.info("removeSlot failed " + JSON.stringify(err));
    } else {
        console.info("removeSlot success");
    }
}
let slotType = Notification.SlotType.SOCIAL_COMMUNICATION;
Notification.removeSlot(slotType,removeSlotCallback);
```



## Notification.removeSlot

removeSlot(slotType: SlotType): Promise\<void\>

Removes a notification slot of a specified type. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type    | Mandatory| Description                                                       |
| -------- | -------- | ---- | ----------------------------------------------------------- |
| slotType | [SlotType](#slottype) | Yes  | Type of the notification slot, which can be used for social communication, service information, content consultation, and other purposes.|

**Example**

```js
let slotType = Notification.SlotType.SOCIAL_COMMUNICATION;
Notification.removeSlot(slotType).then(() => {
	console.info("removeSlot success");
});
```



## Notification.removeAllSlots

removeAllSlots(callback: AsyncCallback\<void\>): void

Removes all notification slots. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                 | Mandatory| Description                |
| -------- | --------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```js
function removeAllCallBack(err) {
    if (err.code) {
        console.info("removeAllSlots failed " + JSON.stringify(err));
    } else {
        console.info("removeAllSlots success");
    }
}
Notification.removeAllSlots(removeAllCallBack);
```



## Notification.removeAllSlots

removeAllSlots(): Promise\<void\>

Removes all notification slots. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Example**

```js
Notification.removeAllSlots().then(() => {
	console.info("removeAllSlots success");
});
```



## Notification.subscribe

subscribe(subscriber: NotificationSubscriber, info: NotificationSubscribeInfo, callback: AsyncCallback\<void\>): void

Subscribes to a notification with the subscription information specified. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name      | Type                     | Mandatory| Description            |
| ---------- | ------------------------- | ---- | ---------------- |
| subscriber | [NotificationSubscriber](#notificationsubscriber)    | Yes  | Notification subscriber.    |
| info       | [NotificationSubscribeInfo](#notificationsubscribeinfo) | Yes  | Notification subscription information.|
| callback   | AsyncCallback\<void\>     | Yes  | Callback used to return the result.|

**Example**

```js
// subscribe callback
function subscribeCallback(err) {
    if (err.code) {
        console.info("subscribe failed " + JSON.stringify(err));
    } else {
        console.info("subscribe success");
    }
}
function onConsumeCallback(data) {
	console.info("Consume callback: " + JSON.stringify(data));
}
let subscriber = {
    onConsume: onConsumeCallback
};
let info = {
    bundleNames: ["bundleName1", "bundleName2"]
};
Notification.subscribe(subscriber, info, subscribeCallback);
```



## Notification.subscribe

subscribe(subscriber: NotificationSubscriber, callback: AsyncCallback\<void\>): void

Subscribes to notifications of all applications under this user. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name      | Type                  | Mandatory| Description            |
| ---------- | ---------------------- | ---- | ---------------- |
| subscriber | [NotificationSubscriber](#notificationsubscriber) | Yes  | Notification subscriber.    |
| callback   | AsyncCallback\<void\>  | Yes  | Callback used to return the result.|

**Example**

```js
function subscribeCallback(err) {
    if (err.code) {
        console.info("subscribe failed " + JSON.stringify(err));
    } else {
        console.info("subscribe success");
    }
}
function onConsumeCallback(data) {
	console.info("Consume callback: " + JSON.stringify(data));
}
let subscriber = {
    onConsume: onConsumeCallback
};
Notification.subscribe(subscriber, subscribeCallback);
```



## Notification.subscribe

subscribe(subscriber: NotificationSubscriber, info?: NotificationSubscribeInfo): Promise\<void\>

Subscribes to a notification with the subscription information specified. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name      | Type                     | Mandatory| Description        |
| ---------- | ------------------------- | ---- | ------------ |
| subscriber | [NotificationSubscriber](#notificationsubscriber)    | Yes  | Notification subscriber.|
| info       | [NotificationSubscribeInfo](#notificationsubscribeinfo) | No  | Notification subscription information.  |

**Example**

```js
function onConsumeCallback(data) {
    console.info("Consume callback: " + JSON.stringify(data));
}
let subscriber = {
    onConsume: onConsumeCallback
};
Notification.subscribe(subscriber).then(() => {
	console.info("subscribe success");
});
```



## Notification.unsubscribe

unsubscribe(subscriber: NotificationSubscriber, callback: AsyncCallback\<void\>): void

Unsubscribes from a notification. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name      | Type                  | Mandatory| Description                |
| ---------- | ---------------------- | ---- | -------------------- |
| subscriber | [NotificationSubscriber](#notificationsubscriber) | Yes  | Notification subscriber.        |
| callback   | AsyncCallback\<void\>  | Yes  | Callback used to return the result.|

**Example**

```js
function unsubscribeCallback(err) {
    if (err.code) {
        console.info("unsubscribe failed " + JSON.stringify(err));
    } else {
        console.info("unsubscribe success");
    }
}
function onDisconnectCallback() {
	console.info("subscribe disconnect");
}
let subscriber = {
    onDisconnect: onDisconnectCallback
};
Notification.unsubscribe(subscriber, unsubscribeCallback);
```



## Notification.unsubscribe

unsubscribe(subscriber: NotificationSubscriber): Promise\<void\>

Unsubscribes from a notification. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name      | Type                  | Mandatory| Description        |
| ---------- | ---------------------- | ---- | ------------ |
| subscriber | [NotificationSubscriber](#notificationsubscriber) | Yes  | Notification subscriber.|

**Example**

```js
function onDisconnectCallback() {
	console.info("subscribe disconnect");
}
let subscriber = {
    onDisconnect: onDisconnectCallback
};
Notification.unsubscribe(subscriber).then(() => {
	console.info("unsubscribe success");
});
```



## Notification.enableNotification

enableNotification(bundle: BundleOption, enable: boolean, callback: AsyncCallback\<void\>): void

Sets whether to enable notification for a specified application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                 | Mandatory| Description                |
| -------- | --------------------- | ---- | -------------------- |
| bundle   | [BundleOption](#bundleoption)          | Yes  | Bundle information of the application.       |
| enable   | boolean               | Yes  | Whether to enable notification.            |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```js
function enableNotificationCallback(err) {
    if (err.code) {
        console.info("enableNotification failed " + JSON.stringify(err));
    } else {
        console.info("enableNotification success");
    }
}
let bundle = {
    bundle: "bundleName1",
};
Notification.enableNotification(bundle, false, enableNotificationCallback);
```



## Notification.enableNotification

enableNotification(bundle: BundleOption, enable: boolean): Promise\<void\>

Sets whether to enable notification for a specified application. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type        | Mandatory| Description      |
| ------ | ------------ | ---- | ---------- |
| bundle | [BundleOption](#bundleoption) | Yes  | Bundle information of the application.|
| enable | boolean      | Yes  | Whether to enable notification.  |

**Example**

```js
let bundle = {
    bundle: "bundleName1",
};
Notification.enableNotification(bundle, false).then(() => {
	console.info("enableNotification success");
});
```



## Notification.isNotificationEnabled

isNotificationEnabled(bundle: BundleOption, callback: AsyncCallback\<boolean\>): void

Checks whether notification is enabled for a specified application. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**Parameters**

| Name    | Type                 | Mandatory| Description                    |
| -------- | --------------------- | ---- | ------------------------ |
| bundle   | [BundleOption](#bundleoption)          | Yes  | Bundle information of the application.           |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```js
function isNotificationEnabledCallback(err, data) {
    if (err.code) {
        console.info("isNotificationEnabled failed " + JSON.stringify(err));
    } else {
        console.info("isNotificationEnabled success");
    }
}
let bundle = {
    bundle: "bundleName1",
};
Notification.isNotificationEnabled(bundle, isNotificationEnabledCallback);
```



## Notification.isNotificationEnabled

isNotificationEnabled(bundle: BundleOption): Promise\<boolean\>

Checks whether notification is enabled for a specified application. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type        | Mandatory| Description      |
| ------ | ------------ | ---- | ---------- |
| bundle | [BundleOption](#bundleoption) | Yes  | Bundle information of the application.|

**Return value**

| Type              | Description                                               |
| ------------------ | --------------------------------------------------- |
| Promise\<boolean\> | Promise used to return the result.|

**Example**

```js
let bundle = {
    bundle: "bundleName1",
};
Notification.isNotificationEnabled(bundle).then((data) => {
	console.info("isNotificationEnabled success, data: " + JSON.stringify(data));
});
```



## Notification.isNotificationEnabled

isNotificationEnabled(callback: AsyncCallback\<boolean\>): void

Checks whether notification is enabled for this application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                 | Mandatory| Description                    |
| -------- | --------------------- | ---- | ------------------------ |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```js
function isNotificationEnabledCallback(err, data) {
    if (err.code) {
        console.info("isNotificationEnabled failed " + JSON.stringify(err));
    } else {
        console.info("isNotificationEnabled success");
    }
}

Notification.isNotificationEnabled(isNotificationEnabledCallback);
```



## Notification.isNotificationEnabled

isNotificationEnabled(): Promise\<boolean\>

Checks whether notification is enabled for this application. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type        | Mandatory| Description      |
| ------ | ------------ | ---- | ---------- |
| bundle | [BundleOption](#bundleoption) | Yes  | Bundle information of the application.|

**Return value**

| Type                                                       | Description                                                        |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<boolean\> | Promise used to return the result.|

**Example**

```js
Notification.isNotificationEnabled().then((data) => {
	console.info("isNotificationEnabled success, data: " + JSON.stringify(data));
});
```



## Notification.displayBadge

displayBadge(bundle: BundleOption, enable: boolean, callback: AsyncCallback\<void\>): void

Sets whether to enable the notification badge for a specified application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                 | Mandatory| Description                |
| -------- | --------------------- | ---- | -------------------- |
| bundle   | [BundleOption](#bundleoption)          | Yes  | Bundle information of the application.          |
| enable   | boolean               | Yes  | Whether to enable notification.            |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```js
function displayBadgeCallback(err) {
    if (err.code) {
        console.info("displayBadge failed " + JSON.stringify(err));
    } else {
        console.info("displayBadge success");
    }
}
let bundle = {
    bundle: "bundleName1",
};
Notification.displayBadge(bundle, false, displayBadgeCallback);
```



## Notification.displayBadge

displayBadge(bundle: BundleOption, enable: boolean): Promise\<void\>

Sets whether to enable the notification badge for a specified application. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type        | Mandatory| Description      |
| ------ | ------------ | ---- | ---------- |
| bundle | [BundleOption](#bundleoption) | Yes  | Bundle information of the application.|
| enable | boolean      | Yes  | Whether to enable notification.  |

**Example**

```js
let bundle = {
    bundle: "bundleName1",
};
Notification.displayBadge(bundle, false).then(() => {
	console.info("displayBadge success");
});
```



## Notification.isBadgeDisplayed

isBadgeDisplayed(bundle: BundleOption, callback: AsyncCallback\<boolean\>): void

Checks whether the notification badge is enabled for a specified application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                 | Mandatory| Description                    |
| -------- | --------------------- | ---- | ------------------------ |
| bundle   | [BundleOption](#bundleoption)          | Yes  | Bundle information of the application.              |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```js
function isBadgeDisplayedCallback(err, data) {
    if (err.code) {
        console.info("isBadgeDisplayed failed " + JSON.stringify(err));
    } else {
        console.info("isBadgeDisplayed success");
    }
}
let bundle = {
    bundle: "bundleName1",
};
Notification.isBadgeDisplayed(bundle, isBadgeDisplayedCallback);
```



## Notification.isBadgeDisplayed

isBadgeDisplayed(bundle: BundleOption): Promise\<boolean\>

Checks whether the notification badge is enabled for a specified application. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type        | Mandatory| Description      |
| ------ | ------------ | ---- | ---------- |
| bundle | [BundleOption](#bundleoption) | Yes  | Bundle information of the application.|

**Return value**

| Type                                                       | Description                                                        |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<boolean\> | Promise used to return the result.|

**Example**

```js
let bundle = {
    bundle: "bundleName1",
};
Notification.isBadgeDisplayed(bundle).then((data) => {
	console.info("isBadgeDisplayed success, data: " + JSON.stringify(data));
});
```



## Notification.setSlotByBundle

setSlotByBundle(bundle: BundleOption, slot: NotificationSlot, callback: AsyncCallback\<void\>): void

Sets the notification slot for a specified application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                 | Mandatory| Description                |
| -------- | --------------------- | ---- | -------------------- |
| bundle   | [BundleOption](#bundleoption)          | Yes  | Bundle information of the application.          |
| slot     | [NotificationSlot](#notificationslot)      | Yes  | Notification slot.            |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```js
function setSlotByBundleCallback(err) {
    if (err.code) {
        console.info("setSlotByBundle failed " + JSON.stringify(err));
    } else {
        console.info("setSlotByBundle success");
    }
}
let bundle = {
    bundle: "bundleName1",
};
let notificationSlot = {
    type: Notification.SlotType.SOCIAL_COMMUNICATION
};
Notification.setSlotByBundle(bundle, notificationSlot, setSlotByBundleCallback);
```



## Notification.setSlotByBundle

setSlotByBundle(bundle: BundleOption, slot: NotificationSlot): Promise\<void\>

Sets the notification slot for a specified application. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type        | Mandatory| Description      |
| ------ | ------------ | ---- | ---------- |
| bundle | [BundleOption](#bundleoption) | Yes  | Bundle information of the application.|
| slot   | [NotificationSlot](#notificationslot) | Yes  | Notification slot.|

**Example**

```js
let bundle = {
    bundle: "bundleName1",
};
let notificationSlot = {
    type: Notification.SlotType.SOCIAL_COMMUNICATION
};
Notification.setSlotByBundle(bundle, notificationSlot).then(() => {
	console.info("setSlotByBundle success");
});
```



## Notification.getSlotsByBundle

getSlotsByBundle(bundle: BundleOption, callback: AsyncCallback\<Array\<NotificationSlot>>): void

Obtains the notification slots of a specified application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                                    | Mandatory| Description                |
| -------- | ---------------------------------------- | ---- | -------------------- |
| bundle   | [BundleOption](#bundleoption)                             | Yes  | Bundle information of the application.          |
| callback | AsyncCallback\<Array\<[NotificationSlot](#notificationslot)>> | Yes  | Callback used to return the result.|

**Example**

```js
function getSlotsByBundleCallback(err, data) {
    if (err.code) {
        console.info("getSlotsByBundle failed " + JSON.stringify(err));
    } else {
        console.info("getSlotsByBundle success");
    }
}
let bundle = {
    bundle: "bundleName1",
};
Notification.getSlotsByBundle(bundle, getSlotsByBundleCallback);
```



## Notification.getSlotsByBundle

getSlotsByBundle(bundle: BundleOption): Promise\<Array\<NotificationSlot>>

Obtains the notification slots of a specified application. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type        | Mandatory| Description      |
| ------ | ------------ | ---- | ---------- |
| bundle | [BundleOption](#bundleoption) | Yes  | Bundle information of the application.|

**Return value**

| Type                                                       | Description                                                        |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<Array\<[NotificationSlot](#notificationslot)>> | Promise used to return the result.|

**Example**

```js
let bundle = {
    bundle: "bundleName1",
};
Notification.getSlotsByBundle(bundle).then((data) => {
	console.info("getSlotsByBundle success, data: " + JSON.stringify(data));
});
```



## Notification.getSlotNumByBundle

getSlotNumByBundle(bundle: BundleOption, callback: AsyncCallback\<number\>): void

Obtains the number of notification slots of a specified application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                     | Mandatory| Description                  |
| -------- | ------------------------- | ---- | ---------------------- |
| bundle   | [BundleOption](#bundleoption)              | Yes  | Bundle information of the application.            |
| callback | AsyncCallback\<number\> | Yes  | Callback used to return the result.|

**Example**

```js
function getSlotNumByBundleCallback(err, data) {
    if (err.code) {
        console.info("getSlotNumByBundle failed " + JSON.stringify(err));
    } else {
        console.info("getSlotNumByBundle success");
    }
}
let bundle = {
    bundle: "bundleName1",
};
Notification.getSlotNumByBundle(bundle, getSlotNumByBundleCallback);
```



## Notification.getSlotNumByBundle

getSlotNumByBundle(bundle: BundleOption): Promise\<number\>

Obtains the number of notification slots of a specified application. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type        | Mandatory| Description      |
| ------ | ------------ | ---- | ---------- |
| bundle | [BundleOption](#bundleoption) | Yes  | Bundle information of the application.|

**Return value**

| Type                                                       | Description                                                        |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<number\> | Promise used to return the result.|

**Example**

```js
let bundle = {
    bundle: "bundleName1",
};
Notification.getSlotNumByBundle(bundle).then((data) => {
	console.info("getSlotNumByBundle success, data: " + JSON.stringify(data));
});
```



## Notification.remove

remove(bundle: BundleOption, notificationKey: NotificationKey, reason: RemoveReason, callback: AsyncCallback\<void\>): void

Removes a notification for a specified bundle. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name           | Type                               | Mandatory| Description                |
| --------------- |   ----------------------------------| ---- | -------------------- |
| bundle          | [BundleOption](#bundleoption)       | Yes  | Bundle information of the application.          |
| notificationKey | [NotificationKey](#notificationkey) | Yes  | Notification key.            |
| reason          | [RemoveReason](#removereason9)      | Yes  | Indicates the reason for deleting a notification.        |
| callback        | AsyncCallback\<void\>               | Yes  | Callback used to return the result.|

**Example**

```js
function removeCallback(err) {
    if (err.code) {
        console.info("remove failed " + JSON.stringify(err));
    } else {
        console.info("remove success");
    }
}
let bundle = {
    bundle: "bundleName1",
};
let notificationKey = {
    id: 0,
    label: "label",
};
let reason = Notification.RemoveReason.CLICK_REASON_REMOVE;
Notification.remove(bundle, notificationKey, reason, removeCallback);
```



## Notification.remove

remove(bundle: BundleOption, notificationKey: NotificationKey, reason: RemoveReason): Promise\<void\>

Removes a notification for a specified bundle. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name           | Type           | Mandatory| Description      |
| --------------- | --------------- | ---- | ---------- |
| bundle          | [BundleOption](#bundleoption)    | Yes  | Bundle information of the application.|
| notificationKey | [NotificationKey](#notificationkey) | Yes  | Notification key.  |
| reason          | [RemoveReason](#removereason9) | Yes  | Reason for deleting the notification.        |

**Example**

```js
let bundle = {
    bundle: "bundleName1",
};
let notificationKey = {
    id: 0,
    label: "label",
};
let reason = Notification.RemoveReason.CLICK_REASON_REMOVE;
Notification.remove(bundle, notificationKey, reason).then(() => {
	console.info("remove success");
});
```



## Notification.remove

remove(hashCode: string, reason: RemoveReason, callback: AsyncCallback\<void\>): void

Removes a notification for a specified bundle. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                 | Mandatory| Description                |
| -------- | --------------------- | ---- | -------------------- |
| hashCode | string                | Yes  | Unique notification ID. It is the **hashCode** in the [NotificationRequest](#notificationrequest) object of [SubscribeCallbackData](#subscribecallbackdata) of the [onConsume](#onconsume) callback.|
| reason   | [RemoveReason](#removereason9) | Yes  | Indicates the reason for deleting a notification.        |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```js
let hashCode = 'hashCode';

function removeCallback(err) {
    if (err.code) {
        console.info("remove failed " + JSON.stringify(err));
    } else {
        console.info("remove success");
    }
}
let reason = Notification.RemoveReason.CANCEL_REASON_REMOVE;
Notification.remove(hashCode, reason, removeCallback);
```



## Notification.remove

remove(hashCode: string, reason: RemoveReason): Promise\<void\>

Removes a notification for a specified bundle. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type      | Mandatory| Description      |
| -------- | ---------- | ---- | ---------- |
| hashCode | string | Yes  | Unique notification ID.|
| reason   | [RemoveReason](#removereason9) | Yes  | Reason for deleting the notification.        |

**Example**

```js
let hashCode = 'hashCode';
let reason = Notification.RemoveReason.CLICK_REASON_REMOVE;
Notification.remove(hashCode, reason).then(() => {
	console.info("remove success");
});
```



## Notification.removeAll

removeAll(bundle: BundleOption, callback: AsyncCallback\<void\>): void

Removes all notifications for a specified application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**Parameters**

| Name    | Type                 | Mandatory| Description                        |
| -------- | --------------------- | ---- | ---------------------------- |
| bundle   | [BundleOption](#bundleoption)          | Yes  | Bundle information of the application.                  |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```js
function removeAllCallback(err) {
    if (err.code) {
        console.info("removeAll failed " + JSON.stringify(err));
    } else {
        console.info("removeAll success");
    }
}
let bundle = {
    bundle: "bundleName1",
};
Notification.removeAll(bundle, removeAllCallback);
```



## Notification.removeAll

removeAll(callback: AsyncCallback\<void\>): void

Removes all notifications. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                 | Mandatory| Description                |
| -------- | --------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```js
function removeAllCallback(err) {
    if (err.code) {
        console.info("removeAll failed " + JSON.stringify(err));
    } else {
        console.info("removeAll success");
    }
}

Notification.removeAll(removeAllCallback);
```



## Notification.removeAll

removeAll(bundle?: BundleOption): Promise\<void\>

Removes all notifications for a specified application. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type        | Mandatory| Description      |
| ------ | ------------ | ---- | ---------- |
| bundle | [BundleOption](#bundleoption) | No  | Bundle information of the application.|

**Example**

```js
// If no application is specified, notifications of all applications are deleted.
Notification.removeAll().then(() => {
	console.info("removeAll success");
});
```

## Notification.removeAll<sup>8+</sup>

removeAll(userId: number, callback: AsyncCallback\<void>): void

Removes all notifications for a specified user. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type        | Mandatory| Description      |
| ------ | ------------ | ---- | ---------- |
| userId | number | Yes  | User ID.|
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```js
function removeAllCallback(err) {
    if (err.code) {
        console.info("removeAll failed " + JSON.stringify(err));
    } else {
        console.info("removeAll success");
    }
}

let userId = 1;
Notification.removeAll(userId, removeAllCallback);
```

## Notification.removeAll<sup>8+</sup>

removeAll(userId: number): Promise\<void>

Removes all notifications for a specified user. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type        | Mandatory| Description      |
| ------ | ------------ | ---- | ---------- |
| userId | number | Yes  | User ID.|

**Example**

```js
let userId = 1;
Notification.removeAll(userId).then(() => {
	console.info("removeAll success");
});
```


## Notification.getAllActiveNotifications

getAllActiveNotifications(callback: AsyncCallback\<Array\<NotificationRequest>>): void

Obtains all active notifications. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                                                        | Mandatory| Description                |
| -------- | ------------------------------------------------------------ | ---- | -------------------- |
| callback | AsyncCallback\<Array\<[NotificationRequest](#notificationrequest)>> | Yes  | Callback used to return the result.|

**Example**

```js
function getAllActiveNotificationsCallback(err, data) {
    if (err.code) {
        console.info("getAllActiveNotifications failed " + JSON.stringify(err));
    } else {
        console.info("getAllActiveNotifications success");
    }
}

Notification.getAllActiveNotifications(getAllActiveNotificationsCallback);
```



## Notification.getAllActiveNotifications

getAllActiveNotifications(): Promise\<Array\<[NotificationRequest](#notificationrequest)>>

Obtains all active notifications. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Return value**

| Type                                                       | Description                                                        |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<Array\<[NotificationRequest](#notificationrequest)>> | Promise used to return the result.|

**Example**

```js
Notification.getAllActiveNotifications().then((data) => {
	console.info("getAllActiveNotifications success, data: " + JSON.stringify(data));
});
```



## Notification.getActiveNotificationCount

getActiveNotificationCount(callback: AsyncCallback\<number\>): void

Obtains the number of active notifications of this application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                  | Mandatory| Description                  |
| -------- | ---------------------- | ---- | ---------------------- |
| callback | AsyncCallback\<number\> | Yes  | Callback used to return the result.|

**Example**

```js
function getActiveNotificationCountCallback(err, data) {
    if (err.code) {
        console.info("getActiveNotificationCount failed " + JSON.stringify(err));
    } else {
        console.info("getActiveNotificationCount success");
    }
}

Notification.getActiveNotificationCount(getActiveNotificationCountCallback);
```



## Notification.getActiveNotificationCount

getActiveNotificationCount(): Promise\<number\>

Obtains the number of active notifications of this application. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Return value**

| Type             | Description                                       |
| ----------------- | ------------------------------------------- |
| Promise\<number\> | Promise used to return the result.|

**Example**

```js
Notification.getActiveNotificationCount().then((data) => {
	console.info("getActiveNotificationCount success, data: " + JSON.stringify(data));
});
```



## Notification.getActiveNotifications

getActiveNotifications(callback: AsyncCallback<Array\<NotificationRequest\>>): void

Obtains active notifications of this application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                                                        | Mandatory| Description                          |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------ |
| callback | AsyncCallback<Array\<[NotificationRequest](#notificationrequest)\>> | Yes  | Callback used to return the result.|

**Example**

```js
function getActiveNotificationsCallback(err, data) {
    if (err.code) {
        console.info("getActiveNotifications failed " + JSON.stringify(err));
    } else {
        console.info("getActiveNotifications success");
    }
}

Notification.getActiveNotifications(getActiveNotificationsCallback);
```



## Notification.getActiveNotifications

getActiveNotifications(): Promise\<Array\<[NotificationRequest](#notificationrequest)\>\>

Obtains active notifications of this application. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Return value**

| Type                                                        | Description                                   |
| ------------------------------------------------------------ | --------------------------------------- |
| Promise\<Array\<[NotificationRequest](#notificationrequest)\>\> | Promise used to return the result.|

**Example**

```js
Notification.getActiveNotifications().then((data) => {
	console.info("removeGroupByBundle success, data: " + JSON.stringify(data));
});
```



## Notification.cancelGroup<sup>8+</sup>

cancelGroup(groupName: string, callback: AsyncCallback\<void\>): void

Cancels notifications under a notification group of this application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name     | Type                 | Mandatory| Description                        |
| --------- | --------------------- | ---- | ---------------------------- |
| groupName | string                | Yes  | Name of the notification group, which is specified through [NotificationRequest](#notificationrequest) when the notification is published.|
| callback  | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```js
function cancelGroupCallback(err) {
    if (err.code) {
        console.info("cancelGroup failed " + JSON.stringify(err));
    } else {
        console.info("cancelGroup success");
    }
}

let groupName = "GroupName";

Notification.cancelGroup(groupName, cancelGroupCallback);
```



## Notification.cancelGroup<sup>8+</sup>

cancelGroup(groupName: string): Promise\<void\>

Cancels notifications under a notification group of this application. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name     | Type  | Mandatory| Description          |
| --------- | ------ | ---- | -------------- |
| groupName | string | Yes  | Name of the notification group.|

**Example**

```js
let groupName = "GroupName";
Notification.cancelGroup(groupName).then(() => {
	console.info("cancelGroup success");
});
```



## Notification.removeGroupByBundle<sup>8+</sup>

removeGroupByBundle(bundle: BundleOption, groupName: string, callback: AsyncCallback\<void\>): void

Removes notifications under a notification group of a specified application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name     | Type                 | Mandatory| Description                        |
| --------- | --------------------- | ---- | ---------------------------- |
| bundle    | [BundleOption](#bundleoption)          | Yes  | Bundle information of the application.                  |
| groupName | string                | Yes  | Name of the notification group.              |
| callback  | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```js
function removeGroupByBundleCallback(err) {
    if (err.code) {
        console.info("removeGroupByBundle failed " + JSON.stringify(err));
    } else {
        console.info("removeGroupByBundle success");
    }
}

let bundleOption = {bundle: "Bundle"};
let groupName = "GroupName";

Notification.removeGroupByBundle(bundleOption, groupName, removeGroupByBundleCallback);
```



## Notification.removeGroupByBundle<sup>8+</sup>

removeGroupByBundle(bundle: BundleOption, groupName: string): Promise\<void\>

Removes notifications under a notification group of a specified application. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name     | Type        | Mandatory| Description          |
| --------- | ------------ | ---- | -------------- |
| bundle    | [BundleOption](#bundleoption) | Yes  | Bundle information of the application.    |
| groupName | string       | Yes  | Name of the notification group.|

**Example**

```js
let bundleOption = {bundle: "Bundle"};
let groupName = "GroupName";
Notification.removeGroupByBundle(bundleOption, groupName).then(() => {
	console.info("removeGroupByBundle success");
});
```



## Notification.setDoNotDisturbDate<sup>8+</sup>

setDoNotDisturbDate(date: DoNotDisturbDate, callback: AsyncCallback\<void\>): void

Sets the DND time. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                 | Mandatory| Description                  |
| -------- | --------------------- | ---- | ---------------------- |
| date     | [DoNotDisturbDate](#donotdisturbdate8)      | Yes  | DND time to set.        |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```js
function setDoNotDisturbDateCallback(err) {
    if (err.code) {
        console.info("setDoNotDisturbDate failed " + JSON.stringify(err));
    } else {
        console.info("setDoNotDisturbDate success");
    }
}

let doNotDisturbDate = {
    type: Notification.DoNotDisturbType.TYPE_ONCE,
    begin: new Date(),
    end: new Date(2021, 11, 15, 18, 0)
};

Notification.setDoNotDisturbDate(doNotDisturbDate, setDoNotDisturbDateCallback);
```



## Notification.setDoNotDisturbDate<sup>8+</sup>

setDoNotDisturbDate(date: DoNotDisturbDate): Promise\<void\>

Sets the DND time. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type            | Mandatory| Description          |
| ---- | ---------------- | ---- | -------------- |
| date | [DoNotDisturbDate](#donotdisturbdate8) | Yes  | DND time to set.|

**Example**

```js
let doNotDisturbDate = {
    type: Notification.DoNotDisturbType.TYPE_ONCE,
    begin: new Date(),
    end: new Date(2021, 11, 15, 18, 0)
};
Notification.setDoNotDisturbDate(doNotDisturbDate).then(() => {
	console.info("setDoNotDisturbDate success");
});
```


## Notification.setDoNotDisturbDate<sup>8+</sup>

setDoNotDisturbDate(date: DoNotDisturbDate, userId: number, callback: AsyncCallback\<void\>): void

Sets the DND time for a specified user. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                 | Mandatory| Description                  |
| -------- | --------------------- | ---- | ---------------------- |
| date     | [DoNotDisturbDate](#donotdisturbdate8)      | Yes  | DND time to set.        |
| userId   | number                | Yes  | ID of the user for whom you want to set the DND time.|
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```js
function setDoNotDisturbDateCallback(err) {
    if (err.code) {
        console.info("setDoNotDisturbDate failed " + JSON.stringify(err));
    } else {
        console.info("setDoNotDisturbDate success");
    }
}

let doNotDisturbDate = {
    type: Notification.DoNotDisturbType.TYPE_ONCE,
    begin: new Date(),
    end: new Date(2021, 11, 15, 18, 0)
};

let userId = 1
Notification.setDoNotDisturbDate(doNotDisturbDate, userId, setDoNotDisturbDateCallback);
```



## Notification.setDoNotDisturbDate<sup>8+</sup>

setDoNotDisturbDate(date: DoNotDisturbDate, userId: number): Promise\<void\>

Sets the DND time for a specified user. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type            | Mandatory| Description          |
| ------ | ---------------- | ---- | -------------- |
| date   | [DoNotDisturbDate](#donotdisturbdate8) | Yes  | DND time to set.|
| userId | number           | Yes  | ID of the user for whom you want to set the DND time.|

**Example**

```js
let doNotDisturbDate = {
    type: Notification.DoNotDisturbType.TYPE_ONCE,
    begin: new Date(),
    end: new Date(2021, 11, 15, 18, 0)
};

let userId = 1;

Notification.setDoNotDisturbDate(doNotDisturbDate, userId).then(() => {
	console.info("setDoNotDisturbDate success");
});
```


## Notification.getDoNotDisturbDate<sup>8+</sup>

getDoNotDisturbDate(callback: AsyncCallback\<DoNotDisturbDate\>): void

Obtains the DND time. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                             | Mandatory| Description                  |
| -------- | --------------------------------- | ---- | ---------------------- |
| callback | AsyncCallback\<[DoNotDisturbDate](#donotdisturbdate8)\> | Yes  | Callback used to return the result.|

**Example**

```js
function getDoNotDisturbDateCallback(err, data) {
    if (err.code) {
        console.info("getDoNotDisturbDate failed " + JSON.stringify(err));
    } else {
        console.info("getDoNotDisturbDate success");
    }
}

Notification.getDoNotDisturbDate(getDoNotDisturbDateCallback);
```



## Notification.getDoNotDisturbDate<sup>8+</sup>

getDoNotDisturbDate(): Promise\<DoNotDisturbDate\>

Obtains the DND time. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Return value**

| Type                                             | Description                                     |
| ------------------------------------------------- | ----------------------------------------- |
| Promise\<[DoNotDisturbDate](#donotdisturbdate8)\> | Promise used to return the result.|

**Example**

```js
Notification.getDoNotDisturbDate().then((data) => {
	console.info("getDoNotDisturbDate success, data: " + JSON.stringify(data));
});
```


## Notification.getDoNotDisturbDate<sup>8+</sup>

getDoNotDisturbDate(userId: number, callback: AsyncCallback\<DoNotDisturbDate\>): void

Obtains the DND time of a specified user. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                             | Mandatory| Description                  |
| -------- | --------------------------------- | ---- | ---------------------- |
| callback | AsyncCallback\<[DoNotDisturbDate](#donotdisturbdate8)\> | Yes  | Callback used to return the result.|
| userId   | number                            | Yes  | User ID.|

**Example**

```js
function getDoNotDisturbDateCallback(err,data) {
    if (err.code) {
        console.info("getDoNotDisturbDate failed " + JSON.stringify(err));
    } else {
        console.info("getDoNotDisturbDate success");
    }
}

let userId = 1;

Notification.getDoNotDisturbDate(userId, getDoNotDisturbDateCallback);
```



## Notification.getDoNotDisturbDate<sup>8+</sup>

getDoNotDisturbDate(userId: number): Promise\<DoNotDisturbDate\>

Obtains the DND time of a specified user. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                             | Mandatory| Description                  |
| -------- | --------------------------------- | ---- | ---------------------- |
| userId   | number                            | Yes  | User ID.|

**Return value**

| Type                                             | Description                                     |
| ------------------------------------------------- | ----------------------------------------- |
| Promise\<[DoNotDisturbDate](#donotdisturbdate8)\> | Promise used to return the result.|

**Example**

```js
let userId = 1;

Notification.getDoNotDisturbDate(userId).then((data) => {
	console.info("getDoNotDisturbDate success, data: " + JSON.stringify(data));
});
```


## Notification.supportDoNotDisturbMode<sup>8+</sup>

supportDoNotDisturbMode(callback: AsyncCallback\<boolean\>): void

Checks whether DND mode is supported. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                    | Mandatory| Description                            |
| -------- | ------------------------ | ---- | -------------------------------- |
| callback | AsyncCallback\<boolean\> | Yes  | Callback used to return the result.|

**Example**

```js
function supportDoNotDisturbModeCallback(err,data) {
    if (err.code) {
        console.info("supportDoNotDisturbMode failed " + JSON.stringify(err));
    } else {
        console.info("supportDoNotDisturbMode success");
    }
}

Notification.supportDoNotDisturbMode(supportDoNotDisturbModeCallback);
```



## Notification.supportDoNotDisturbMode<sup>8+</sup>

supportDoNotDisturbMode(): Promise\<boolean\>

Checks whether DND mode is supported. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Return value**

| Type                                                       | Description                                                        |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<boolean\> | Promise used to return the result.|

**Example**

```js
Notification.supportDoNotDisturbMode().then((data) => {
	console.info("supportDoNotDisturbMode success, data: " + JSON.stringify(data));
});
```



## Notification.isSupportTemplate<sup>8+</sup>

isSupportTemplate(templateName: string, callback: AsyncCallback\<boolean\>): void

Checks whether a specified template exists. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name      | Type                    | Mandatory| Description                      |
| ------------ | ------------------------ | ---- | -------------------------- |
| templateName | string                   | Yes  | Template name.                  |
| callback     | AsyncCallback\<boolean\> | Yes  | Callback used to return the result.|

**Example**

```javascript
let templateName = 'process';
function isSupportTemplateCallback(err, data) {
    if (err.code) {
        console.info("isSupportTemplate failed " + JSON.stringify(err));
    } else {
        console.info("isSupportTemplate success");
    }
}

Notification.isSupportTemplate(templateName, isSupportTemplateCallback);
```



## Notification.isSupportTemplate<sup>8+</sup>

isSupportTemplate(templateName: string): Promise\<boolean\>

Checks whether a specified template exists. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name      | Type  | Mandatory| Description    |
| ------------ | ------ | ---- | -------- |
| templateName | string | Yes  | Template name.|

**Return value**

| Type              | Description           |
| ------------------ | --------------- |
| Promise\<boolean\> | Promise used to return the result.|

**Example**

```javascript
let templateName = 'process';

Notification.isSupportTemplate(templateName).then((data) => {
    console.info("isSupportTemplate success, data: " + JSON.stringify(data));
});
```



## Notification.requestEnableNotification<sup>8+</sup>

requestEnableNotification(callback: AsyncCallback\<void\>): void

Requests notification to be enabled for this application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name  | Type                    | Mandatory| Description                      |
| -------- | ------------------------ | ---- | -------------------------- |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```javascript
function requestEnableNotificationCallback(err) {
    if (err.code) {
        console.info("requestEnableNotification failed " + JSON.stringify(err));
    } else {
        console.info("requestEnableNotification success");
    }
};

Notification.requestEnableNotification(requestEnableNotificationCallback);
```



## Notification.requestEnableNotification<sup>8+</sup>

requestEnableNotification(): Promise\<void\>

Requests notification to be enabled for this application. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Example**

```javascript
Notification.requestEnableNotification().then(() => {
    console.info("requestEnableNotification success");
});
```


## Notification.enableDistributed<sup>8+</sup>

enableDistributed(enable: boolean, callback: AsyncCallback\<void\>): void

Sets whether this device supports distributed notifications. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type                    | Mandatory| Description                      |
| -------- | ------------------------ | ---- | -------------------------- |
| enable   | boolean                  | Yes  | Whether the device supports distributed notifications.|
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```javascript
function enabledNotificationCallback(err) {
    if (err.code) {
        console.info("enableDistributed failed " + JSON.stringify(err));
    } else {
        console.info("enableDistributed success");
    }
};

let enable = true;

Notification.enableDistributed(enable, enabledNotificationCallback);
```



## Notification.enableDistributed<sup>8+</sup>

enableDistributed(enable: boolean): Promise\<void>

Sets whether this device supports distributed notifications. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type                    | Mandatory| Description                      |
| -------- | ------------------------ | ---- | -------------------------- |
| enable   | boolean                  | Yes  | Whether the device supports distributed notifications.|

**Example**

```javascript
let enable = true;
Notification.enableDistributed(enable).then(() => {
    console.info("enableDistributed success");
});
```


## Notification.isDistributedEnabled<sup>8+</sup>

isDistributedEnabled(callback: AsyncCallback\<boolean>): void

Checks whether this device supports distributed notifications. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name  | Type                    | Mandatory| Description                      |
| -------- | ------------------------ | ---- | -------------------------- |
| callback | AsyncCallback\<boolean\> | Yes  | Callback used to return the result.|

**Example**

```javascript
function isDistributedEnabledCallback(err, data) {
    if (err.code) {
        console.info("isDistributedEnabled failed " + JSON.stringify(err));
    } else {
        console.info("isDistributedEnabled success " + JSON.stringify(data));
    }
};

Notification.isDistributedEnabled(isDistributedEnabledCallback);
```



## Notification.isDistributedEnabled<sup>8+</sup>

isDistributedEnabled(): Promise\<boolean>

Checks whether this device supports distributed notifications. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Return value**

| Type              | Description                                         |
| ------------------ | --------------------------------------------- |
| Promise\<boolean\> | Promise used to return the result.|

**Example**

```javascript
Notification.isDistributedEnabled().then((data) => {
    console.info("isDistributedEnabled success, data: " + JSON.stringify(data));
});
```


## Notification.enableDistributedByBundle<sup>8+</sup>

enableDistributedByBundle(bundle: BundleOption, enable: boolean, callback: AsyncCallback\<void>): void

Sets whether a specified application supports distributed notifications. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type                    | Mandatory| Description                      |
| -------- | ------------------------ | ---- | -------------------------- |
| bundle   | [BundleOption](#bundleoption)             | Yes  | Bundle information of the application.                  |
| enable   | boolean                  | Yes  | Whether the device supports distributed notifications.                      |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Example**

```javascript
function enableDistributedByBundleCallback(err) {
    if (err.code) {
        console.info("enableDistributedByBundle failed " + JSON.stringify(err));
    } else {
        console.info("enableDistributedByBundle success");
    }
};

let bundle = {
    bundle: "bundleName1",
};

let enable = true;

Notification.enableDistributedByBundle(bundle, enable, enableDistributedByBundleCallback);
```



## Notification.enableDistributedByBundle<sup>8+</sup>

enableDistributedByBundle(bundle: BundleOption, enable: boolean): Promise\<void>

Sets whether a specified application supports distributed notifications. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type                    | Mandatory| Description                      |
| -------- | ------------------------ | ---- | -------------------------- |
| bundle   | [BundleOption](#bundleoption)             | Yes  | Application bundle.               |
| enable   | boolean                  | Yes  | Whether the device supports distributed notifications.                 |

**Example**

```javascript
let bundle = {
    bundle: "bundleName1",
};

let enable = true;
Notification.enableDistributedByBundle(bundle, enable).then(() => {
    console.info("enableDistributedByBundle success");
});
```

## Notification.isDistributedEnabledByBundle<sup>8+</sup>

isDistributedEnabledByBundle(bundle: BundleOption, callback: AsyncCallback\<boolean>): void

Obtains whether an application supports distributed notifications based on the bundle. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type                    | Mandatory| Description                      |
| -------- | ------------------------ | ---- | -------------------------- |
| bundle   | [BundleOption](#bundleoption)             | Yes  | Application bundle.                    |
| callback | AsyncCallback\<boolean\> | Yes  | Callback used to return the result.|

**Example**

```javascript
function isDistributedEnabledByBundleCallback(err, data) {
    if (err.code) {
        console.info("isDistributedEnabledByBundle failed " + JSON.stringify(err));
    } else {
        console.info("isDistributedEnabledByBundle success" + JSON.stringify(data));
    }
};

let bundle = {
    bundle: "bundleName1",
};

Notification.isDistributedEnabledByBundle(bundle, isDistributedEnabledByBundleCallback);
```



## Notification.isDistributedEnabledByBundle<sup>8+</sup>

isDistributedEnabledByBundle(bundle: BundleOption): Promise\<boolean>

Checks whether a specified application supports distributed notifications. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type                    | Mandatory| Description                      |
| -------- | ------------------------ | ---- | -------------------------- |
| bundle   | [BundleOption](#bundleoption)             | Yes  | Application bundle.               |

**Return value**

| Type              | Description                                             |
| ------------------ | ------------------------------------------------- |
| Promise\<boolean\> | Promise used to return the result.|

**Example**

```javascript
let bundle = {
    bundle: "bundleName1",
};

Notification.isDistributedEnabledByBundle(bundle).then((data) => {
    console.info("isDistributedEnabledByBundle success, data: " + JSON.stringify(data));
});
```


## Notification.getDeviceRemindType<sup>8+</sup>

getDeviceRemindType(callback: AsyncCallback\<DeviceRemindType\>): void

Obtains the notification reminder type. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type                              | Mandatory| Description                      |
| -------- | --------------------------------- | ---- | -------------------------- |
| callback | AsyncCallback\<[DeviceRemindType](#deviceremindtype8)\> | Yes  | Callback used to return the result.|

**Example**

```javascript
function getDeviceRemindTypeCallback(err,data) {
    if (err.code) {
        console.info("getDeviceRemindType failed " + JSON.stringify(err));
    } else {
        console.info("getDeviceRemindType success");
    }
};

Notification.getDeviceRemindType(getDeviceRemindTypeCallback);
```



## Notification.getDeviceRemindType<sup>8+</sup>

getDeviceRemindType(): Promise\<DeviceRemindType\>

Obtains the notification reminder type. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.Notification

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System API**: This is a system API and cannot be called by third-party applications.

**Return value**

| Type              | Description           |
| ------------------ | --------------- |
| Promise\<[DeviceRemindType](#deviceremindtype8)\> | Promise used to return the result.|

**Example**

```javascript
Notification.getDeviceRemindType().then((data) => {
    console.info("getDeviceRemindType success, data: " + JSON.stringify(data));
});
```

## NotificationSubscriber

Provides callbacks for receiving or removing notifications and serves as the input parameter of [subscribe](#notificationsubscribe).

**System API**: This is a system API and cannot be called by third-party applications.

### onConsume

onConsume?: (data: [SubscribeCallbackData](#subscribecallbackdata)) => void

Callback for receiving notifications.

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| ------------ | ------------------------ | ---- | -------------------------- |
| data | [SubscribeCallbackData](#subscribecallbackdata) | Yes| Information about the notification received.|

**Example**

```javascript
function subscribeCallback(err) {
    if (err.code) {
        console.info("subscribe failed " + JSON.stringify(err));
    } else {
        console.info("subscribeCallback");
    }
};

function onConsumeCallback(data) {
    let req = data.request;
    console.info('===> onConsume callback req.id:' + req.id);
};

let subscriber = {
    onConsume: onConsumeCallback
};

Notification.subscribe(subscriber, subscribeCallback);
```

### onCancel

onCancel?:(data: [SubscribeCallbackData](#subscribecallbackdata)) => void

Callback for canceling notifications.

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| ------------ | ------------------------ | ---- | -------------------------- |
| data | [SubscribeCallbackData](#subscribecallbackdata) | Yes| Information about the notification to cancel.|

**Example**

```javascript
function subscribeCallback(err) {
    if (err.code) {
        console.info("subscribe failed " + JSON.stringify(err));
    } else {
        console.info("subscribeCallback");
    }
};

function onCancelCallback(data) {
    let req = data.request;
    console.info('===> onCancel callback req.id:' + req.id);
}

let subscriber = {
    onCancel: onCancelCallback
};

Notification.subscribe(subscriber, subscribeCallback);
```

### onUpdate

onUpdate?:(data: [NotificationSortingMap](#notificationsortingmap)) => void

Callback for notification sorting updates.

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| ------------ | ------------------------ | ---- | -------------------------- |
| data | [NotificationSortingMap](#notificationsortingmap) | Yes| Latest notification sorting list.|

**Example**

```javascript
function subscribeCallback(err) {
    if (err.code) {
        console.info("subscribe failed " + JSON.stringify(err));
    } else {
        console.info("subscribeCallback");
    }
};

function onUpdateCallback(map) {
    console.info('===> onUpdateCallback map:' + JSON.stringify(map));
}

let subscriber = {
    onUpdate: onUpdateCallback
};

Notification.subscribe(subscriber, subscribeCallback);
```

### onConnect

onConnect?:() => void

Callback for subscription.

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

**Example**

```javascript
function subscribeCallback(err) {
    if (err.code) {
        console.info("subscribe failed " + JSON.stringify(err));
    } else {
        console.info("subscribeCallback");
    }
};

function onConnectCallback() {
    console.info('===> onConnect in test');
}

let subscriber = {
    onConnect: onConnectCallback
};

Notification.subscribe(subscriber, subscribeCallback);
```

### onDisconnect

onDisconnect?:() => void

Callback for unsubscription.

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

**Example**

```javascript
function subscribeCallback(err) {
    if (err.code) {
        console.info("subscribe failed " + JSON.stringify(err));
    } else {
        console.info("subscribeCallback");
    }
};
function unsubscribeCallback(err) {
    if (err.code) {
        console.info("unsubscribe failed " + JSON.stringify(err));
    } else {
        console.info("unsubscribeCallback");
    }
};

function onConnectCallback() {
    console.info('===> onConnect in test');
}
function onDisconnectCallback() {
    console.info('===> onDisconnect in test');
}

let subscriber = {
    onConnect: onConnectCallback,
    onDisconnect: onDisconnectCallback
};

// The onConnect callback is invoked when subscription to the notification is complete.
Notification.subscribe(subscriber, subscribeCallback);
// The onDisconnect callback is invoked when unsubscription to the notification is complete.
Notification.unsubscribe(subscriber, unsubscribeCallback);
```

### onDestroy

onDestroy?:() => void

Callback for service disconnection.

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

**Example**

```javascript
function subscribeCallback(err) {
    if (err.code) {
        console.info("subscribe failed " + JSON.stringify(err));
    } else {
        console.info("subscribeCallback");
    }
};

function onDestroyCallback() {
    console.info('===> onDestroy in test');
}

let subscriber = {
    onDestroy: onDestroyCallback
};

Notification.subscribe(subscriber, subscribeCallback);
```

### onDoNotDisturbDateChange<sup>8+</sup>

onDoNotDisturbDateChange?:(mode: notification.[DoNotDisturbDate](#donotdisturbdate8)) => void

Callback for DND time setting updates.

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| ------------ | ------------------------ | ---- | -------------------------- |
| mode | notification.[DoNotDisturbDate](#donotdisturbdate8) | Yes| DND time setting updates.|

**Example**
```javascript
function subscribeCallback(err) {
    if (err.code) {
        console.info("subscribe failed " + JSON.stringify(err));
    } else {
        console.info("subscribeCallback");
    }
};

function onDoNotDisturbDateChangeCallback(mode) {
    console.info('===> onDoNotDisturbDateChange:' + mode);
}

let subscriber = {
    onDoNotDisturbDateChange: onDoNotDisturbDateChangeCallback
};
Notification.subscribe(subscriber, subscribeCallback);

let doNotDisturbDate = {
    type: Notification.DoNotDisturbType.TYPE_ONCE,
    begin: new Date(),
    end: new Date(2021, 11, 15, 18, 0)
}
// Set the onDoNotDisturbDateChange callback for DND time setting updates.
Notification.setDoNotDisturbDate(doNotDisturbDate).then(() => {
	console.info("setDoNotDisturbDate sucess");
});
```


### onEnabledNotificationChanged<sup>8+</sup>

onEnabledNotificationChanged?:(callbackData: [EnabledNotificationCallbackData](#enablednotificationcallbackdata8)) => void

Listens for the notification enabled status changes. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| ------------ | ------------------------ | ---- | -------------------------- |
| callback | AsyncCallback\<[EnabledNotificationCallbackData](#enablednotificationcallbackdata8)\> | Yes| Callback used to return the result.|

**Example**

```javascript
function subscribeCallback(err) {
    if (err.code) {
        console.info("subscribe failed " + JSON.stringify(err));
    } else {
        console.info("subscribeCallback");
    }
};

function onEnabledNotificationChangedCallback(callbackData) {
    console.info("bundle: " + callbackData.bundle);
    console.info("uid: " + callbackData.uid);
    console.info("enable: " + callbackData.enable);
};

let subscriber = {
    onEnabledNotificationChanged: onEnabledNotificationChangedCallback
};
Notification.subscribe(subscriber, subscribeCallback);

let bundle = {
    bundle: "bundleName1",
}
// Set the onEnabledNotificationChanged callback that is triggered when the notification enabled status changes.
Notification.enableNotification(bundle, false).then(() => {
	console.info("enableNotification sucess");
});
```

## SubscribeCallbackData

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

| Name           | Type                                             | Readable| Writable| Description    |
| --------------- | ------------------------------------------------- | ---- | --- | -------- |
| request         | [NotificationRequest](#notificationrequest)       | Yes | No | Notification content.|
| sortingMap      | [NotificationSortingMap](#notificationsortingmap) | Yes | No | Notification sorting information.|
| reason          | number                                            | Yes | No | Reason for deletion.|
| sound           | string                                            | Yes | No | Sound used for notification.|
| vibrationValues | Array\<number\>                                   | Yes | No | Vibration used for notification.|


## EnabledNotificationCallbackData<sup>8+</sup>

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

| Name  | Type   | Readable| Writable| Description            |
| ------ | ------- | ---- | --- | ---------------- |
| bundle | string  | Yes | No | Bundle name of the application.      |
| uid    | number  | Yes | No | UID of the application.       |
| enable | boolean | Yes | No | Notification enabled status of the application.|


## DoNotDisturbDate<sup>8+</sup>

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

| Name | Type                                  | Readable| Writable| Description                  |
| ----- | -------------------------------------- | ---- | ---- | ---------------------- |
| type  | [DoNotDisturbType](#donotdisturbtype8) | Yes  | Yes  | DND time type.|
| begin | Date                                   | Yes  | Yes  | DND start time.|
| end   | Date                                   | Yes  | Yes  | DND end time.|

## DoNotDisturbType<sup>8+</sup>

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

| Name        | Value              | Description                                      |
| ------------ | ---------------- | ------------------------------------------ |
| TYPE_NONE    | 0 | Non-DND.                          |
| TYPE_ONCE    | 1 | One-shot DND at the specified time segment (only considering the hour and minute).|
| TYPE_DAILY   | 2 | Daily DND at the specified time segment (only considering the hour and minute).|
| TYPE_CLEARLY | 3 | DND at the specified time segment (considering the year, month, day, hour, and minute).    |


## ContentType

**System capability**: SystemCapability.Notification.Notification

| Name                             | Value         | Description              |
| --------------------------------- | ----------- | ------------------ |
| NOTIFICATION_CONTENT_BASIC_TEXT   | NOTIFICATION_CONTENT_BASIC_TEXT | Normal text notification.    |
| NOTIFICATION_CONTENT_LONG_TEXT    | NOTIFICATION_CONTENT_LONG_TEXT | Long text notification.  |
| NOTIFICATION_CONTENT_PICTURE      | NOTIFICATION_CONTENT_PICTURE | Picture-attached notification.    |
| NOTIFICATION_CONTENT_CONVERSATION | NOTIFICATION_CONTENT_CONVERSATION | Conversation notification.    |
| NOTIFICATION_CONTENT_MULTILINE    | NOTIFICATION_CONTENT_MULTILINE | Multi-line text notification.|

## SlotLevel

**System capability**: SystemCapability.Notification.Notification

| Name                             | Value         | Description              |
| --------------------------------- | ----------- | ------------------ |
| LEVEL_NONE                        | 0           | The notification function is disabled.    |
| LEVEL_MIN                         | 1           | The notification function is enabled, but the notification icon is not displayed in the status bar, with no banner or alert tone.|
| LEVEL_LOW                         | 2           | The notification function is enabled, and the notification icon is displayed in the status bar, with no banner or alert tone.|
| LEVEL_DEFAULT                     | 3           | The notification feature is enabled, and the notification icon is displayed in the status bar, with an alert tone but no banner.|
| LEVEL_HIGH                        | 4           | The notification feature is enabled, and the notification icon is displayed in the status bar, with an alert tone and banner.|


## BundleOption

**System capability**: SystemCapability.Notification.Notification

| Name  | Type  | Readable| Writable| Description  |
| ------ | ------ |---- | --- |  ------ |
| bundle | string | Yes | Yes | Bundle information of the application.|
| uid    | number | Yes | Yes | User ID.|



## NotificationKey

**System capability**: SystemCapability.Notification.Notification

| Name | Type  | Readable| Writable| Description    |
| ----- | ------ | ---- | --- | -------- |
| id    | number | Yes | Yes | Notification ID.  |
| label | string | Yes | Yes | Notification label.|


## SlotType

**System capability**: SystemCapability.Notification.Notification

| Name                | Value      | Description      |
| -------------------- | -------- | ---------- |
| UNKNOWN_TYPE         | 0 | Unknown type.|
| SOCIAL_COMMUNICATION | 1 | Notification slot for social communication.|
| SERVICE_INFORMATION  | 2 | Notification slot for service information.|
| CONTENT_INFORMATION  | 3 | Notification slot for content consultation.|
| OTHER_TYPES          | 0xFFFF | Notification slot for other purposes.|


## NotificationActionButton

Describes the button displayed in the notification.

**System capability**: SystemCapability.Notification.Notification

| Name     | Type                                           | Readable| Writable| Description                     |
| --------- | ----------------------------------------------- | --- | ---- | ------------------------- |
| title     | string                                          | Yes | Yes | Button title.                 |
| wantAgent | [WantAgent](js-apis-app-ability-wantAgent.md)   | Yes | Yes | **WantAgent** of the button.|
| extras    | { [key: string]: any }                          | Yes | Yes | Extra information of the button.             |
| userInput<sup>8+</sup> | [NotificationUserInput](#notificationuserinput8) | Yes | Yes | User input object.         |


## NotificationBasicContent

Describes the normal text notification.

**System capability**: SystemCapability.Notification.Notification

| Name          | Type  | Readable| Writable| Description                              |
| -------------- | ------ | ---- | ---- | ---------------------------------- |
| title          | string | Yes  | Yes  | Notification title.                        |
| text           | string | Yes  | Yes  | Notification content.                        |
| additionalText | string | Yes  | Yes  | Additional information of the notification.|


## NotificationLongTextContent

Describes the long text notification.

**System capability**: SystemCapability.Notification.Notification

| Name          | Type  | Readable| Writable| Description                            |
| -------------- | ------ | ---- | --- | -------------------------------- |
| title          | string | Yes | Yes | Notification title.                        |
| text           | string | Yes | Yes | Notification content.                        |
| additionalText | string | Yes | Yes | Additional information of the notification.|
| longText       | string | Yes | Yes | Long text of the notification.                    |
| briefText      | string | Yes | Yes | Brief text of the notification.|
| expandedTitle  | string | Yes | Yes | Title of the notification in the expanded state.                |


## NotificationMultiLineContent

Describes the multi-line text notification.

**System capability**: SystemCapability.Notification.Notification

| Name          | Type           | Readable| Writable| Description                            |
| -------------- | --------------- | --- | --- | -------------------------------- |
| title          | string          | Yes | Yes | Notification title.                        |
| text           | string          | Yes | Yes | Notification content.                        |
| additionalText | string          | Yes | Yes | Additional information of the notification.|
| briefText      | string          | Yes | Yes | Brief text of the notification.|
| longTitle      | string          | Yes | Yes | Title of the notification in the expanded state.                |
| lines          | Array\<string\> | Yes | Yes | Multi-line text of the notification.                  |


## NotificationPictureContent

Describes the picture-attached notification.

**System capability**: SystemCapability.Notification.Notification

| Name          | Type          | Readable| Writable| Description                            |
| -------------- | -------------- | ---- | --- | -------------------------------- |
| title          | string         | Yes | Yes | Notification title.                        |
| text           | string         | Yes | Yes | Notification content.                        |
| additionalText | string         | Yes | Yes | Additional information of the notification.|
| briefText      | string         | Yes | Yes | Brief text of the notification.|
| expandedTitle  | string         | Yes | Yes | Title of the notification in the expanded state.                |
| picture        | [image.PixelMap](js-apis-image.md#pixelmap7) | Yes | Yes | Picture attached to the notification.                  |


## NotificationContent

Describes the notification content.

**System capability**: SystemCapability.Notification.Notification

| Name       | Type                                                        | Readable| Writable| Description              |
| ----------- | ------------------------------------------------------------ | ---- | --- | ------------------ |
| contentType | [ContentType](#contenttype)                                  | Yes | Yes | Notification content type.      |
| normal      | [NotificationBasicContent](#notificationbasiccontent)        | Yes | Yes | Normal text.  |
| longText    | [NotificationLongTextContent](#notificationlongtextcontent)  | Yes | Yes | Long text.|
| multiLine   | [NotificationMultiLineContent](#notificationmultilinecontent) | Yes | Yes | Multi-line text.  |
| picture     | [NotificationPictureContent](#notificationpicturecontent)    | Yes | Yes | Picture-attached.  |


## NotificationFlagStatus<sup>8+</sup>

Describes the notification flag status.

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

| Name          | Value | Description                              |
| -------------- | --- | --------------------------------- |
| TYPE_NONE      | 0   | The default flag is used.                        |
| TYPE_OPEN      | 1   | The notification flag is enabled.                    |
| TYPE_CLOSE     | 2   | The notification flag is disabled.                    |


## NotificationFlags<sup>8+</sup>

Enumerates notification flags.

**System capability**: SystemCapability.Notification.Notification

| Name            | Type                   | Readable| Writable| Description                              |
| ---------------- | ---------------------- | ---- | ---- | --------------------------------- |
| soundEnabled     | [NotificationFlagStatus](#notificationflagstatus8) | Yes  | No  | Whether to enable the sound alert for the notification.                 |
| vibrationEnabled | [NotificationFlagStatus](#notificationflagstatus8) | Yes  | No  | Whether to enable vibration for the notification.              |


## NotificationRequest

Describes the notification request.

**System capability**: SystemCapability.Notification.Notification

| Name                 | Type                                         | Readable| Writable| Description                      |
| --------------------- | --------------------------------------------- | ---- | --- | -------------------------- |
| content               | [NotificationContent](#notificationcontent)   | Yes | Yes | Notification content.                  |
| id                    | number                                        | Yes | Yes | Notification ID.                    |
| slotType              | [SlotType](#slottype)                         | Yes | Yes | Slot type.                  |
| isOngoing             | boolean                                       | Yes | Yes | Whether the notification is an ongoing notification.            |
| isUnremovable         | boolean                                       | Yes | Yes | Whether the notification can be removed.                |
| deliveryTime          | number                                        | Yes | Yes | Time when the notification is sent.              |
| tapDismissed          | boolean                                       | Yes | Yes | Whether the notification is automatically cleared.          |
| autoDeletedTime       | number                                        | Yes | Yes | Time when the notification is automatically cleared.            |
| wantAgent             | [WantAgent](js-apis-app-ability-wantAgent.md) | Yes | Yes | **WantAgent** instance to which the notification will be redirected after being clicked. |
| extraInfo             | {[key: string]: any}                          | Yes | Yes | Extended parameters.                  |
| color                 | number                                        | Yes | Yes | Background color of the notification. Not supported currently.|
| colorEnabled          | boolean                                       | Yes | Yes | Whether the notification background color is enabled. Not supported currently.|
| isAlertOnce           | boolean                                       | Yes | Yes | Whether the notification triggers an alert only once.|
| isStopwatch           | boolean                                       | Yes | Yes | Whether to display the stopwatch.          |
| isCountDown           | boolean                                       | Yes | Yes | Whether to display the countdown time.        |
| isFloatingIcon        | boolean                                       | Yes | Yes | Whether the notification is displayed as a floating icon in the status bar.        |
| label                 | string                                        | Yes | Yes | Notification label.                  |
| badgeIconStyle        | number                                        | Yes | Yes | Notification badge type.              |
| showDeliveryTime      | boolean                                       | Yes | Yes | Whether to display the time when the notification is delivered.          |
| actionButtons         | Array\<[NotificationActionButton](#notificationactionbutton)\>             | Yes | Yes | Buttons in the notification. Up to two buttons are allowed.    |
| smallIcon             | [image.PixelMap](js-apis-image.md#pixelmap7) | Yes | Yes | Small notification icon. This field is optional, and the icon size cannot exceed 30 KB.|
| largeIcon             | [image.PixelMap](js-apis-image.md#pixelmap7) | Yes | Yes | Large notification icon. This field is optional, and the icon size cannot exceed 30 KB.|
| creatorBundleName     | string                                        | Yes | No | Name of the bundle that creates the notification.            |
| creatorUid            | number                                        | Yes | No | UID used for creating the notification.             |
| creatorPid            | number                                        | Yes | No | PID used for creating the notification.             |
| creatorUserId<sup>8+</sup>| number                                    | Yes | No | ID of the user who creates the notification.          |
| hashCode              | string                                        | Yes | No | Unique ID of the notification.              |
| classification        | string                                        | Yes | Yes | Notification category.<br>**System API**: This is a system API and cannot be called by third-party applications.                  |
| groupName<sup>8+</sup>| string                                        | Yes | Yes | Notification group name.                |
| template<sup>8+</sup> | [NotificationTemplate](#notificationtemplate8) | Yes | Yes | Notification template.                  |
| isRemoveAllowed<sup>8+</sup> | boolean                                | Yes | No | Whether the notification can be removed.<br>**System API**: This is a system API and cannot be called by third-party applications.                  |
| source<sup>8+</sup>   | number                                        | Yes | No | Notification source.<br>**System API**: This is a system API and cannot be called by third-party applications.                  |
| distributedOption<sup>8+</sup>   | [DistributedOptions](#distributedoptions8)                 | Yes | Yes | Distributed notification options.         |
| deviceId<sup>8+</sup> | string                                        | Yes | No | Device ID of the notification source.<br>**System API**: This is a system API and cannot be called by third-party applications.         |
| notificationFlags<sup>8+</sup> | [NotificationFlags](#notificationflags8)                    | Yes | No | Notification flags.         |
| removalWantAgent<sup>9+</sup> | [WantAgent](js-apis-app-ability-wantAgent.md) | Yes | Yes | **WantAgent** instance to which the notification will be redirected when it is removed.         |
| badgeNumber<sup>9+</sup> | number                    | Yes | Yes | Number of notifications displayed on the application icon.         |

## DistributedOptions<sup>8+</sup>

Describes distributed notifications options.

**System capability**: SystemCapability.Notification.Notification

| Name                  | Type           | Readable| Writable| Description                              |
| ---------------------- | -------------- | ---- | ---- | ---------------------------------- |
| isDistributed          | boolean        | Yes  | Yes  | Whether the notification is a distributed notification.                 |
| supportDisplayDevices  | Array\<string> | Yes  | Yes  | List of the devices to which the notification can be synchronized.        |
| supportOperateDevices  | Array\<string> | Yes  | Yes  | List of the devices on which the notification can be opened.             |
| remindType             | number         | Yes  | No  | Notification reminder type.<br>**System API**: This is a system API and cannot be called by third-party applications.                   |


## NotificationSlot

Describes the notification slot.

**System capability**: SystemCapability.Notification.Notification

| Name                | Type                 | Readable| Writable| Description                                      |
| -------------------- | --------------------- | ---- | --- | ------------------------------------------ |
| type                 | [SlotType](#slottype) | Yes | Yes | Slot type.                                  |
| level                | number                | Yes | Yes | Notification level. If this parameter is not set, the default value is used based on the notification slot type.|
| desc                 | string                | Yes | Yes | Notification slot description.                          |
| badgeFlag            | boolean               | Yes | Yes | Whether to display the badge.                              |
| bypassDnd            | boolean               | Yes | Yes | Whether to bypass DND mode in the system.              |
| lockscreenVisibility | number                | Yes | Yes | Mode for displaying the notification on the lock screen.                |
| vibrationEnabled     | boolean               | Yes | Yes | Whether vibration is enabled for the notification.                                |
| sound                | string                | Yes | Yes | Notification alert tone.                                |
| lightEnabled         | boolean               | Yes | Yes | Whether the indicator blinks for the notification.                                  |
| lightColor           | number                | Yes | Yes | Indicator color of the notification.                                |
| vibrationValues      | Array\<number\>       | Yes | Yes | Vibration mode of the notification.                              |
| enabled<sup>9+</sup> | boolean               | Yes | No | Whether the notification slot is enabled.                     |


## NotificationSorting

Provides sorting information of active notifications.

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

| Name    | Type                                 | Readable| Writable| Description        |
| -------- | ------------------------------------- | ---- | --- | ------------ |
| slot     | [NotificationSlot](#notificationslot) | Yes | No | Notification slot content.|
| hashCode | string                                | Yes | No | Unique ID of the notification.|
| ranking  | number                                | Yes | No | Notification sequence number.|


## NotificationSortingMap

Provides sorting information of active notifications in all subscribed notifications.

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

| Name          | Type                                                        | Readable| Writable| Description            |
| -------------- | ------------------------------------------------------------ | ---- | --- | ---------------- |
| sortings       | {[key: string]: [NotificationSorting](#notificationsorting)} | Yes | No | Array of notification sorting information.|
| sortedHashCode | Array\<string\>                                              | Yes | No | Array of unique notification IDs.|


## NotificationSubscribeInfo

Provides the information about the publisher for notification subscription.

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

| Name       | Type           | Readable| Writable| Description                           |
| ----------- | --------------- | --- | ---- | ------------------------------- |
| bundleNames | Array\<string\> | Yes | Yes | Bundle names of the applications whose notifications are to be subscribed to.|
| userId      | number          | Yes | Yes | User whose notifications are to be subscribed to.   |


## NotificationTemplate<sup>8+</sup>

Describes the notification template.

**System capability**: SystemCapability.Notification.Notification

| Name| Type                   | Readable| Writable| Description      |
| ---- | ---------------------- | ---- | ---- | ---------- |
| name | string                 | Yes  | Yes  | Template name.|
| data | {[key:string]: Object} | Yes  | Yes  | Template data.|


## NotificationUserInput<sup>8+</sup>

Provides the notification user input.

**System capability**: SystemCapability.Notification.Notification

| Name    | Type  | Readable| Writable| Description                         |
| -------- | ------ | --- | ---- | ----------------------------- |
| inputKey | string | Yes | Yes | Key to identify the user input.|


## DeviceRemindType<sup>8+</sup>

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

| Name                | Value | Description                              |
| -------------------- | --- | --------------------------------- |
| IDLE_DONOT_REMIND    | 0   | The device is not in use. No notification is required.           |
| IDLE_REMIND          | 1   | The device is not in use.                |
| ACTIVE_DONOT_REMIND  | 2   | The device is in use. No notification is required.           |
| ACTIVE_REMIND        | 3   | The device is in use.                |


## SourceType<sup>8+</sup>

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

| Name                | Value | Description                 |
| -------------------- | --- | -------------------- |
| TYPE_NORMAL          | 0   | Normal notification.           |
| TYPE_CONTINUOUS      | 1   | Continuous notification.           |
| TYPE_TIMER           | 2   | Timed notification.           |

## RemoveReason<sup>9+</sup>

**System capability**: SystemCapability.Notification.Notification

**System API**: This is a system API and cannot be called by third-party applications.

| Name                | Value | Description                 |
| -------------------- | --- | -------------------- |
| CLICK_REASON_REMOVE<sup>9+</sup>  | 1   | The notification is removed after a click on it.   |
| CANCEL_REASON_REMOVE<sup>9+</sup> | 2   | The notification is removed by the user.        |
