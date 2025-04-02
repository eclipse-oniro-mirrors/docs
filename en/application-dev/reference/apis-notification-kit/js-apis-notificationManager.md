# @ohos.notificationManager (NotificationManager)

The **NotificationManager** module provides notification management capabilities, covering notifications, notification slots, notification enabled status, and notification badge status.

> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```ts
import { notificationManager } from '@kit.NotificationKit';
```

## notificationManager.publish

publish(request: NotificationRequest, callback: AsyncCallback\<void\>): void

Publish a notification. This API uses an asynchronous callback to return the result.

If the ID and label of the new notification are the same as that of the previous notification, the new one replaces the previous one.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                                       | Mandatory| Description                                       |
| -------- | ------------------------------------------- | ---- | ------------------------------------------- |
| request  | [NotificationRequest](js-apis-inner-notification-notificationRequest.md#notificationrequest) | Yes  | Content and related configuration of the notification to publish.|
| callback | AsyncCallback\<void\>                       | Yes  | Callback used to return the result.                       |

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                                             |
| -------- | ---------------------------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.    | 
| 1600001  | Internal error.                                      |
| 1600002  | Marshalling or unmarshalling error.                  |
| 1600003  | Failed to connect to the service.                    |
| 1600004  | Notification disabled.                               |
| 1600005  | Notification slot disabled.                          |
| 1600007  | The notification does not exist.                     |
| 1600009  | The notification sending frequency reaches the upper limit.            |
| 1600012  | No memory space.                                     |
| 1600014  | No permission.                                       |
| 1600015  | The current notification status does not support duplicate configurations. |
| 1600016  | The notification version for this update is too low. |
| 2300007  | Network unreachable.                                 |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

// publish callback
let publishCallback = (err: BusinessError): void => {
  if (err) {
    console.error(`publish failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("publish success");
  }
}
// NotificationRequest object
let notificationRequest: notificationManager.NotificationRequest = {
  id: 1,
  content: {
    notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT,
    normal: {
      title: "test_title",
      text: "test_text",
      additionalText: "test_additionalText"
    }
  }
};
notificationManager.publish(notificationRequest, publishCallback);
```

## notificationManager.publish

publish(request: NotificationRequest): Promise\<void\>

Publish a notification. This API uses a promise to return the URI of the file in the destination directory.

If the ID and label of the new notification are the same as that of the previous notification, the new one replaces the previous one.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                                       | Mandatory| Description                                       |
| -------- | ------------------------------------------- | ---- | ------------------------------------------- |
| request  | [NotificationRequest](js-apis-inner-notification-notificationRequest.md#notificationrequest) | Yes  | Content and related configuration of the notification to publish.|

**Return value**

| Type    | Description| 
| ------- |--|
| Promise\<void\> | Promise that returns no value.| 

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                                             |
| -------- | ---------------------------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.    | 
| 1600001  | Internal error.                                      |
| 1600002  | Marshalling or unmarshalling error.                  |
| 1600003  | Failed to connect to the service.                    |
| 1600004  | Notification disabled.                               |
| 1600005  | Notification slot disabled.                          |
| 1600007  | The notification does not exist.                     |
| 1600009  | The notification sending frequency reaches the upper limit.            |
| 1600012  | No memory space.                                     |
| 1600014  | No permission.                                       |
| 1600015  | The current notification status does not support duplicate configurations. |
| 1600016  | The notification version for this update is too low. |
| 2300007  | Network unreachable.                                 |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

// NotificationRequest object
let notificationRequest: notificationManager.NotificationRequest = {
  id: 1,
  content: {
    notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT,
    normal: {
      title: "test_title",
      text: "test_text",
      additionalText: "test_additionalText"
    }
  }
};
notificationManager.publish(notificationRequest).then(() => {
  console.info("publish success");
}).catch((err: BusinessError) => {
  console.error(`publish fail: ${JSON.stringify(err)}`);
});

```

## notificationManager.cancel

cancel(id: number, label: string, callback: AsyncCallback\<void\>): void

Cancels a notification with the specified ID and label. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                 | Mandatory| Description                |
| -------- | --------------------- | ---- | -------------------- |
| id       | number                | Yes  | Notification ID.              |
| label    | string                | Yes  | Notification label.            |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |
| 1600007  | The notification does not exist.      |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

// cancel callback
let cancelCallback = (err: BusinessError): void => {
  if (err) {
    console.error(`cancel failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("cancel success");
  } 
}
notificationManager.cancel(0, "label", cancelCallback);
```

## notificationManager.cancel

cancel(id: number, label?: string): Promise\<void\>

Cancels a notification with the specified ID and optional label. This API uses a promise to return the URI of the file in the destination directory.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name | Type  | Mandatory| Description    |
| ----- | ------ | ---- | -------- |
| id    | number | Yes  | Notification ID.  |
| label | string | No  | Notification label. This parameter is left empty by default.|

**Return value**

| Type    | Description       | 
| ------- |-----------|
| Promise\<void\> | Promise that returns no value.| 

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |
| 1600007  | The notification does not exist.      |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

notificationManager.cancel(0).then(() => {
  console.info("cancel success");
}).catch((err: BusinessError) => {
  console.error(`cancel fail: ${JSON.stringify(err)}`);
});
```

## notificationManager.cancel

cancel(id: number, callback: AsyncCallback\<void\>): void

Cancels a notification with the specified ID. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                 | Mandatory| Description                |
| -------- | --------------------- | ---- | -------------------- |
| id       | number                | Yes  | Notification ID.              |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |
| 1600007  | The notification does not exist.      |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

// cancel callback
let cancelCallback = (err: BusinessError): void => {
  if (err) {
    console.error(`cancel failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("cancel success");
  }
}
notificationManager.cancel(0, cancelCallback);
```

## notificationManager.cancelAll

cancelAll(callback: AsyncCallback\<void\>): void

Cancels all notifications of this application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                 | Mandatory| Description                |
| -------- | --------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

// cancel callback
let cancelAllCallback = (err: BusinessError): void => {
  if (err) {
    console.error(`cancelAll failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("cancelAll success");
  }
}
notificationManager.cancelAll(cancelAllCallback);
```

## notificationManager.cancelAll

cancelAll(): Promise\<void\>

Cancels all notifications of this application. This API uses a promise to return the URI of the file in the destination directory.

**System capability**: SystemCapability.Notification.Notification

**Return value**

| Type    | Description       | 
| ------- |-----------|
| Promise\<void\> | Promise that returns no value.| 

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

notificationManager.cancelAll().then(() => {
  console.info("cancelAll success");
}).catch((err: BusinessError) => {
  console.error(`cancelAll fail: ${JSON.stringify(err)}`);
});
```

## notificationManager.addSlot

addSlot(type: SlotType, callback: AsyncCallback\<void\>): void

Adds a notification slot of a specified type. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                 | Mandatory| Description                  |
| -------- | --------------------- | ---- | ---------------------- |
| type     | [SlotType](#slottype)              | Yes  | Type of the notification slot to add.|
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.  |

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |
| 1600012  | No memory space.                    |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

// addSlot callback
let addSlotCallBack = (err: BusinessError): void => {
  if (err) {
    console.error(`addSlot failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("addSlot success");
  }
}
notificationManager.addSlot(notificationManager.SlotType.SOCIAL_COMMUNICATION, addSlotCallBack);
```

## notificationManager.addSlot

addSlot(type: SlotType): Promise\<void\>

Adds a notification slot of a specified type. This API uses a promise to return the URI of the file in the destination directory.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name| Type    | Mandatory| Description                  |
| ---- | -------- | ---- | ---------------------- |
| type | [SlotType](#slottype) | Yes  | Type of the notification slot to add.|

**Return value**

| Type    | Description       | 
| ------- |-----------|
| Promise\<void\> | Promise that returns no value.| 

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |
| 1600012  | No memory space.                    |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

notificationManager.addSlot(notificationManager.SlotType.SOCIAL_COMMUNICATION).then(() => {
  console.info("addSlot success");
}).catch((err: BusinessError) => {
  console.error(`addSlot fail: ${JSON.stringify(err)}`);
});
```

## notificationManager.getSlot

getSlot(slotType: SlotType, callback: AsyncCallback\<NotificationSlot\>): void

Obtains a notification slot of a specified type. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                             | Mandatory| Description                                                       |
| -------- | --------------------------------- | ---- | ----------------------------------------------------------- |
| slotType | [SlotType](#slottype)                          | Yes  | Type of a notification slot, including social communication, service notification, and content consultation.|
| callback | AsyncCallback\<[NotificationSlot](js-apis-inner-notification-notificationSlot.md)\> | Yes  | Callback used to return the result.                                       |

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

// getSlot callback
let getSlotCallback = (err: BusinessError, data: notificationManager.NotificationSlot): void => {
  if (err) {
    console.error(`getSlot failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info(`getSlot success, data is ${JSON.stringify(data)}`);
  }
}
let slotType: notificationManager.SlotType = notificationManager.SlotType.SOCIAL_COMMUNICATION;
notificationManager.getSlot(slotType, getSlotCallback);
```

## notificationManager.getSlot

getSlot(slotType: SlotType): Promise\<NotificationSlot\>

Obtains a notification slot of a specified type. This API uses a promise to return the URI of the file in the destination directory.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type    | Mandatory| Description                                                       |
| -------- | -------- | ---- | ----------------------------------------------------------- |
| slotType | [SlotType](#slottype) | Yes  | Type of a notification slot, including social communication, service notification, and content consultation.|

**Return value**

| Type                                                       | Description                                                        |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<[NotificationSlot](js-apis-inner-notification-notificationSlot.md)\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

let slotType: notificationManager.SlotType = notificationManager.SlotType.SOCIAL_COMMUNICATION;
notificationManager.getSlot(slotType).then((data: notificationManager.NotificationSlot) => {
  console.info("getSlot success, data: " + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error(`getSlot fail: ${JSON.stringify(err)}`);
});
```

## notificationManager.getSlots

getSlots(callback: AsyncCallback\<Array\<NotificationSlot>>): void

Obtains all notification slots of this application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                             | Mandatory| Description                |
| -------- | --------------------------------- | ---- | -------------------- |
| callback | AsyncCallback\<Array\<[NotificationSlot](js-apis-inner-notification-notificationSlot.md)\>\> | Yes  | Callback used to return all notification slots of the current application.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).


| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

// getSlots callback
let getSlotsCallback = (err: BusinessError, data: Array<notificationManager.NotificationSlot>): void => {
  if (err) {
    console.error(`getSlots failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info(`getSlots success, data is ${JSON.stringify(data)}`);
  }
}
notificationManager.getSlots(getSlotsCallback);
```

## notificationManager.getSlots

getSlots(): Promise\<Array\<NotificationSlot>>

Obtains all notification slots of this application. This API uses a promise to return the URI of the file in the destination directory.

**System capability**: SystemCapability.Notification.Notification

**Return value**

| Type                                                       | Description                                                        |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<Array\<[NotificationSlot](js-apis-inner-notification-notificationSlot.md)\>\> | Promise used to return all notification slots of the current application.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

notificationManager.getSlots().then((data: Array<notificationManager.NotificationSlot>) => {
  console.info("getSlots success, data: " + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error(`getSlots fail: ${JSON.stringify(err)}`);
});
```

## notificationManager.removeSlot

removeSlot(slotType: SlotType, callback: AsyncCallback\<void\>): void

Removes a notification slot of a specified type for this application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                 | Mandatory| Description                                                       |
| -------- | --------------------- | ---- | ----------------------------------------------------------- |
| slotType | [SlotType](#slottype)              | Yes  | Type of a notification slot, including social communication, service notification, and content consultation.|
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.                                       |

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

// removeSlot callback
let removeSlotCallback = (err: BusinessError): void => {
  if (err) {
    console.error(`removeSlot failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("removeSlot success");
  }
}
let slotType = notificationManager.SlotType.SOCIAL_COMMUNICATION;
notificationManager.removeSlot(slotType, removeSlotCallback);
```

## notificationManager.removeSlot

removeSlot(slotType: SlotType): Promise\<void\>

Removes a notification slot of a specified type for this application. This API uses a promise to return the URI of the file in the destination directory.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type    | Mandatory| Description                                                       |
| -------- | -------- | ---- | ----------------------------------------------------------- |
| slotType | [SlotType](#slottype) | Yes  | Type of a notification slot, including social communication, service notification, and content consultation.|

**Return value**

| Type     | Description       | 
|---------|-----------|
| Promise\<void\> | Promise that returns no value.| 

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

let slotType: notificationManager.SlotType = notificationManager.SlotType.SOCIAL_COMMUNICATION;
notificationManager.removeSlot(slotType).then(() => {
  console.info("removeSlot success");
}).catch((err: BusinessError) => {
  console.error(`removeSlot fail: ${JSON.stringify(err)}`);
});
```

## notificationManager.removeAllSlots

removeAllSlots(callback: AsyncCallback\<void\>): void

Removes all notification slots for this application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                 | Mandatory| Description                |
| -------- | --------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

let removeAllSlotsCallback = (err: BusinessError): void => {
  if (err) {
    console.error(`removeAllSlots failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("removeAllSlots success");
  }
}
notificationManager.removeAllSlots(removeAllSlotsCallback);
```

## notificationManager.removeAllSlots

removeAllSlots(): Promise\<void\>

Removes all notification slots for this application. This API uses a promise to return the URI of the file in the destination directory.

**System capability**: SystemCapability.Notification.Notification

**Return value**

| Type     | Description       | 
|---------|-----------|
| Promise\<void\> | Promise that returns no value.| 

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

notificationManager.removeAllSlots().then(() => {
  console.info("removeAllSlots success");
}).catch((err: BusinessError) => {
  console.error(`removeAllSlots fail: ${JSON.stringify(err)}`);
});
```

## notificationManager.isNotificationEnabled<sup>11+</sup>

isNotificationEnabled(callback: AsyncCallback\<boolean\>): void

Checks whether notification is enabled for the specified application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                 | Mandatory| Description                    |
| -------- | --------------------- | ---- | ------------------------ |
| callback | AsyncCallback\<boolean\> | Yes  | Callback used to return the result. The value **true** means that the notification is enabled, and **false** means the opposite.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                                 |
| -------- | ---------------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      |
| 1600001  | Internal error.                          |
| 1600002  | Marshalling or unmarshalling error.      |
| 1600003  | Failed to connect to the service.               |
| 1600008  | The user does not exist.                   |
| 17700001 | The specified bundle name was not found. |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

let isNotificationEnabledCallback = (err: BusinessError, data: boolean): void => {
  if (err) {
    console.error(`isNotificationEnabled failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info(`isNotificationEnabled success, data is ${JSON.stringify(data)}`);
  }
}

notificationManager.isNotificationEnabled(isNotificationEnabledCallback);
```

## notificationManager.isNotificationEnabled<sup>11+</sup>

isNotificationEnabled(): Promise\<boolean\>

Checks whether notification is enabled for the specified application. This API uses a promise to return the URI of the file in the destination directory.

**System capability**: SystemCapability.Notification.Notification

**Return value**

| Type                                                       | Description                                                        |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| Promise\<boolean\> | Promise used to return the result. The value **true** means that the notification is enabled, and **false** means the opposite.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                                |
| -------- | ---------------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      |
| 1600001  | Internal error.                          |
| 1600002  | Marshalling or unmarshalling error.      |
| 1600003  | Failed to connect to the service.               |
| 1600008  | The user does not exist.                   |
| 17700001 | The specified bundle name was not found. |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

notificationManager.isNotificationEnabled().then((data: boolean) => {
  console.info("isNotificationEnabled success, data: " + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error(`isNotificationEnabled fail: ${JSON.stringify(err)}`);
});
```

## notificationManager.isNotificationEnabledSync<sup>12+</sup>

isNotificationEnabledSync(): boolean

Synchronously checks whether notification is enabled for the specified application.

**System capability**: SystemCapability.Notification.Notification

**Return value**

| Type                                                       | Description                                                    |
| ----------------------------------------------------------- |--------------------------------------------------------- |
| boolean | Returned result. **true**: enabled; **false**: returned.|

**Error codes**

For details about the error codes, see [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                                |
| -------- | ---------------------------------------- |
| 1600001  | Internal error.                          |
| 1600002  | Marshalling or unmarshalling error.      |
| 1600003  | Failed to connect to the service.               |

**Example**

```ts
let enabled = notificationManager.isNotificationEnabledSync();
console.info(`isNotificationEnabledSync success, data is : ${JSON.stringify(enabled)}`);
```

## notificationManager.setBadgeNumber<sup>10+</sup>

setBadgeNumber(badgeNumber: number): Promise\<void\>

Sets the notification badge number. This API uses a promise to return the URI of the file in the destination directory.

If the **badgeNumber** is set to **0**, badges are cleared; if the value is greater than **99**, **99+** is displayed on the badge.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name     | Type  | Mandatory| Description      |
| ----------- | ------ | ---- | ---------- |
| badgeNumber | number | Yes  | Notification badge number to set.|

**Return value**

| Type     | Description       | 
|---------|-----------|
| Promise\<void\> | Promise that returns no value.| 

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |
| 1600012  | No memory space.                          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

let badgeNumber: number = 10;
notificationManager.setBadgeNumber(badgeNumber).then(() => {
  console.info("setBadgeNumber success");
}).catch((err: BusinessError) => {
  console.error(`setBadgeNumber fail: ${JSON.stringify(err)}`);
});
```

## notificationManager.setBadgeNumber<sup>10+</sup>

setBadgeNumber(badgeNumber: number, callback: AsyncCallback\<void\>): void

Sets the notification badge number. This API uses an asynchronous callback to return the result.

If the **badgeNumber** is set to **0**, badges are cleared; if the value is greater than **99**, **99+** is displayed on the badge.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name     | Type                 | Mandatory| Description              |
| ----------- | --------------------- | ---- | ------------------ |
| badgeNumber | number                | Yes  | Notification badge number to set.        |
| callback    | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |
| 1600012  | No memory space.                          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

let setBadgeNumberCallback = (err: BusinessError): void => {
  if (err) {
    console.error(`setBadgeNumber failed code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("setBadgeNumber success");
  }
}
let badgeNumber: number = 10;
notificationManager.setBadgeNumber(badgeNumber, setBadgeNumberCallback);
```

## notificationManager.getActiveNotificationCount

getActiveNotificationCount(callback: AsyncCallback\<number\>): void

Obtains the number of active notifications of this application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                  | Mandatory| Description                  |
| -------- | ---------------------- | ---- | ---------------------- |
| callback | AsyncCallback\<number\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

let getActiveNotificationCountCallback = (err: BusinessError, data: number): void => {
  if (err) {
    console.error(`getActiveNotificationCount failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info(`getActiveNotificationCount success, data is ${JSON.stringify(data)}`);
  }
}

notificationManager.getActiveNotificationCount(getActiveNotificationCountCallback);
```

## notificationManager.getActiveNotificationCount

getActiveNotificationCount(): Promise\<number\>

Obtains the number of active notifications of this application. This API uses a promise to return the URI of the file in the destination directory.

**System capability**: SystemCapability.Notification.Notification

**Return value**

| Type             | Description                                       |
| ----------------- | ------------------------------------------- |
| Promise\<number\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

notificationManager.getActiveNotificationCount().then((data: number) => {
  console.info("getActiveNotificationCount success, data: " + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error(`getActiveNotificationCount fail: ${JSON.stringify(err)}`);
});
```

## notificationManager.getActiveNotifications

getActiveNotifications(callback: AsyncCallback\<Array\<NotificationRequest>>): void

Obtains the active notifications of this application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name    | Type                                                        | Mandatory| Description                          |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------ |
| callback | AsyncCallback\<Array\<[NotificationRequest](js-apis-inner-notification-notificationRequest.md#notificationrequest)>> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

let getActiveNotificationsCallback = (err: BusinessError, data: Array<notificationManager.NotificationRequest>): void => {
  if (err) {
    console.error(`getActiveNotifications failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("getActiveNotifications success" + JSON.stringify(data));
  }
}
notificationManager.getActiveNotifications(getActiveNotificationsCallback);
```

## notificationManager.getActiveNotifications

getActiveNotifications(): Promise\<Array\<NotificationRequest\>\>

Obtains the active notifications of this application. This API uses a promise to return the URI of the file in the destination directory.

**System capability**: SystemCapability.Notification.Notification

**Return value**

| Type                                                        | Description                                   |
| ------------------------------------------------------------ | --------------------------------------- |
| Promise\<Array\<[NotificationRequest](js-apis-inner-notification-notificationRequest.md#notificationrequest)\>\> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

notificationManager.getActiveNotifications().then((data: Array<notificationManager.NotificationRequest>) => {
  console.info("getActiveNotifications success, data: " + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error(`getActiveNotifications fail: ${JSON.stringify(err)}`);
});
```

## notificationManager.cancelGroup

cancelGroup(groupName: string, callback: AsyncCallback\<void\>): void

Cancels notifications under a notification group of this application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name     | Type                 | Mandatory| Description                        |
| --------- | --------------------- | ---- | ---------------------------- |
| groupName | string                | Yes  | Name of the notification group, which is specified through [NotificationRequest](js-apis-inner-notification-notificationRequest.md#notificationrequest) when the notification is published.|
| callback  | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

let cancelGroupCallback = (err: BusinessError): void => {
  if (err) {
    console.error(`cancelGroup failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("cancelGroup success");
  }
}
let groupName: string = "GroupName";
notificationManager.cancelGroup(groupName, cancelGroupCallback);
```

## notificationManager.cancelGroup

cancelGroup(groupName: string): Promise\<void\>

Cancels notifications under a notification group of this application. This API uses a promise to return the URI of the file in the destination directory.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name     | Type  | Mandatory| Description          |
| --------- | ------ | ---- | -------------- |
| groupName | string | Yes  | Name of the notification group, which is specified through [NotificationRequest](js-apis-inner-notification-notificationRequest.md#notificationrequest) when the notification is published.|

**Return value**

| Type     | Description       | 
|---------|-----------|
| Promise\<void\> | Promise that returns no value.| 

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

let groupName: string = "GroupName";
notificationManager.cancelGroup(groupName).then(() => {
  console.info("cancelGroup success");
}).catch((err: BusinessError) => {
  console.error(`cancelGroup fail: ${JSON.stringify(err)}`);
});
```

## notificationManager.isSupportTemplate

isSupportTemplate(templateName: string, callback: AsyncCallback\<boolean\>): void

Checks whether a specified template is supported. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name      | Type                    | Mandatory| Description                      |
| ------------ | ------------------------ | ---- | -------------------------- |
| templateName | string                   | Yes  | Template name. Currently, only **downloadTemplate** is supported.                  |
| callback     | AsyncCallback\<boolean\> | Yes  | Callback used to return the result. The value **true** means that the specified template is supported, and **false** means the opposite.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

let templateName: string = 'downloadTemplate';
let isSupportTemplateCallback = (err: BusinessError, data: boolean): void => {
  if (err) {
    console.error(`isSupportTemplate failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("isSupportTemplate success, data: " + JSON.stringify(data));
  }
}
notificationManager.isSupportTemplate(templateName, isSupportTemplateCallback);
```

## notificationManager.isSupportTemplate

isSupportTemplate(templateName: string): Promise\<boolean\>

Checks whether a specified template is supported. This API uses a promise to return the URI of the file in the destination directory.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name      | Type  | Mandatory| Description    |
| ------------ | ------ | ---- | -------- |
| templateName | string | Yes  | Template name. Currently, only **downloadTemplate** is supported.|

**Return value**

| Type              | Description           |
| ------------------ | --------------- |
| Promise\<boolean\> | Promise used to return the result. The value **true** means that the specified template is supported, and **false** means the opposite.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

let templateName: string = 'downloadTemplate';
notificationManager.isSupportTemplate(templateName).then((data: boolean) => {
  console.info("isSupportTemplate success, data: " + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error(`isSupportTemplate fail: ${JSON.stringify(err)}`);
});
```

## notificationManager.requestEnableNotification<sup>(deprecated)</sup>

requestEnableNotification(callback: AsyncCallback\<void\>): void

Requests notification to be enabled for this application. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is deprecated since API version 12. You are advised to use [requestEnableNotification](#notificationmanagerrequestenablenotification10) with **context** input parameters instead.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name  | Type                    | Mandatory| Description                      |
| -------- | ------------------------ | ---- | -------------------------- |
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |
| 1600004  | Notification disabled.          |
| 1600013  | A notification dialog box is already displayed.           |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

let requestEnableNotificationCallback = (err: BusinessError): void => {
  if (err) {
    console.error(`requestEnableNotification failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("requestEnableNotification success");
  }
};
notificationManager.requestEnableNotification(requestEnableNotificationCallback);
```

## notificationManager.requestEnableNotification<sup>(deprecated)</sup>

requestEnableNotification(): Promise\<void\>

Requests notification to be enabled for this application. This API uses a promise to return the URI of the file in the destination directory.

> **NOTE**
>
> This API is deprecated since API version 12. You are advised to use [requestEnableNotification](#notificationmanagerrequestenablenotification10-1) with **context** input parameters instead.

**System capability**: SystemCapability.Notification.Notification

**Return value**

| Type     | Description       | 
|---------|-----------|
| Promise\<void\> | Promise that returns no value.| 

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |
| 1600004  | Notification disabled.          |
| 1600013  | A notification dialog box is already displayed.           |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

notificationManager.requestEnableNotification().then(() => {
  console.info("requestEnableNotification success");
}).catch((err: BusinessError) => {
  console.error(`requestEnableNotification fail: ${JSON.stringify(err)}`);
});
```

## notificationManager.requestEnableNotification<sup>10+</sup>

requestEnableNotification(context: UIAbilityContext, callback: AsyncCallback\<void\>): void

Requests notification to be enabled for this application in a modal. This API uses an asynchronous callback to return the result.

This API can be called only after the application UI is loaded (that is, [loadContent](../apis-ability-kit/js-apis-app-ability-uiExtensionContentSession.md#uiextensioncontentsessionloadcontent) is successfully called).

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name  | Type                    | Mandatory| Description                |
| -------- | ------------------------ | ---- |--------------------|
| context | [UIAbilityContext](../../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md) | Yes  | Ability context bound to the notification dialog box.|
| callback | AsyncCallback\<void\> | Yes  | Callback used to return the result.    |

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      |
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |
| 1600004  | Notification disabled.          |
| 1600013  | A notification dialog box is already displayed.           |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';
import { UIAbility } from '@kit.AbilityKit';
import { window } from '@kit.ArkUI';
import { hilog } from '@kit.PerformanceAnalysisKit';

class MyAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
  hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onWindowStageCreate');
    windowStage.loadContent('pages/Index', (err, data) => {
      if (err.code) {
        hilog.error(0x0000, 'testTag', 'Failed to load the content. Cause: %{public}s', JSON.stringify(err) ?? '');
        return;
      }
      hilog.info(0x0000, 'testTag', 'Succeeded in loading the content. Data: %{public}s', JSON.stringify(data) ?? '');
      let requestEnableNotificationCallback = (err: BusinessError): void => {
        if (err) {
          hilog.error(0x0000, 'testTag', `[ANS] requestEnableNotification failed, code is ${err.code}, message is ${err.message}`);
        } else {
          hilog.info(0x0000, 'testTag', `[ANS] requestEnableNotification success`);
        }
      };
      notificationManager.requestEnableNotification(this.context, requestEnableNotificationCallback);
    });
  }
}
```

## notificationManager.requestEnableNotification<sup>10+</sup>

requestEnableNotification(context: UIAbilityContext): Promise\<void\>

Requests notification to be enabled for this application in a modal. This API uses a promise to return the URI of the file in the destination directory.

This API can be called only after the application UI is loaded (that is, [loadContent](../apis-ability-kit/js-apis-app-ability-uiExtensionContentSession.md#uiextensioncontentsessionloadcontent) is successfully called).

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name  | Type                    | Mandatory| Description                |
| -------- | ------------------------ | ---- |--------------------|
| context | [UIAbilityContext](../../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md) | Yes  | Ability context bound to the notification dialog box.|

**Return value**

| Type     | Description       | 
|---------|-----------|
| Promise\<void\> | Promise that returns no value.| 

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |
| 1600004  | Notification disabled.          |
| 1600013  | A notification dialog box is already displayed.           |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';
import { UIAbility } from '@kit.AbilityKit';
import { window } from '@kit.ArkUI';
import { hilog } from '@kit.PerformanceAnalysisKit';

class MyAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onWindowStageCreate');
    windowStage.loadContent('pages/Index', (err, data) => {
      if (err.code) {
        hilog.error(0x0000, 'testTag', 'Failed to load the content. Cause: %{public}s', JSON.stringify(err) ?? '');
        return;
      }
      hilog.info(0x0000, 'testTag', 'Succeeded in loading the content. Data: %{public}s', JSON.stringify(data) ?? '');
      notificationManager.requestEnableNotification(this.context).then(() => {
        hilog.info(0x0000, 'testTag', `[ANS] requestEnableNotification success`);
      }).catch((err: BusinessError) => {
        hilog.error(0x0000, 'testTag', `[ANS] requestEnableNotification failed, code is ${err.code}, message is ${err.message}`);
      });
    });
  }
}
```

## notificationManager.isDistributedEnabled   

isDistributedEnabled(callback: AsyncCallback\<boolean>): void

Checks whether distributed notification is enabled on this device. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.Notification

**Parameters**

| Name  | Type                    | Mandatory| Description                      |
| -------- | ------------------------ | ---- | -------------------------- |
| callback | AsyncCallback\<boolean\> | Yes  | Callback used to return the result. The value **true** means that distributed notification is enabled, and **false** means the opposite.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |
| 1600010  | Distributed operation failed.       |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

let isDistributedEnabledCallback = (err: BusinessError, data: boolean): void => {
  if (err) {
    console.error(`isDistributedEnabled failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("isDistributedEnabled success " + JSON.stringify(data));
  }
};
notificationManager.isDistributedEnabled(isDistributedEnabledCallback);
```

## notificationManager.isDistributedEnabled

isDistributedEnabled(): Promise\<boolean>

Checks whether distributed notification is enabled on this device. This API uses a promise to return the URI of the file in the destination directory.

**System capability**: SystemCapability.Notification.Notification

**Return value**

| Type              | Description                                         |
| ------------------ | --------------------------------------------- |
| Promise\<boolean\> | Promise used to return the result. The value **true** means that distributed notification is enabled, and **false** means the opposite.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 401     | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3.Parameter verification failed.      | 
| 1600001  | Internal error.                     |
| 1600002  | Marshalling or unmarshalling error. |
| 1600003  | Failed to connect to the service.          |
| 1600010  | Distributed operation failed.       |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';

notificationManager.isDistributedEnabled().then((data: boolean) => {
  console.info("isDistributedEnabled success, data: " + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error(`isDistributedEnabled fail: ${JSON.stringify(err)}`);
});
```

## notificationManager.openNotificationSettings<sup>13+</sup>

openNotificationSettings(context: UIAbilityContext): Promise\<void\>

Opens the notification settings page of the application, which is displayed in semi-modal mode and can be used to set the notification enabling and notification mode. This API uses a promise to return the URI of the file in the destination directory.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.Notification.NotificationSettings

**Parameters**

| Name  | Type                    | Mandatory| Description                |
| -------- | ------------------------ | ---- |--------------------|
| context | [UIAbilityContext](../../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md) | Yes  | Ability context bound to the notification settings page.|

**Return value**

| Type     | Description       | 
|---------|-----------|
| Promise\<void\> | Promise that returns no value.| 

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md) and [Notification Error Codes](./errorcode-notification.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 1600001  | Internal error.                     |
| 1600003  | Failed to connect to the service.          |
| 1600018  | the notification settings window is already displayed.           |

**Example**

```ts
import { BusinessError } from '@kit.BasicServicesKit';
import { UIAbility } from '@kit.AbilityKit';
import { window } from '@kit.ArkUI';
import { hilog } from '@kit.PerformanceAnalysisKit';

class MyAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onWindowStageCreate');
    windowStage.loadContent('pages/Index', (err, data) => {
      if (err.code) {
        hilog.error(0x0000, 'testTag', 'Failed to load the content. Cause: %{public}s', JSON.stringify(err) ?? '');
        return;
      }
      hilog.info(0x0000, 'testTag', 'Succeeded in loading the content. Data: %{public}s', JSON.stringify(data) ?? '');
      notificationManager.openNotificationSettings(this.context).then(() => {
        hilog.info(0x0000, 'testTag', `[ANS] openNotificationSettings success`);
      }).catch((err: BusinessError) => {
        hilog.error(0x0000, 'testTag', `[ANS] openNotificationSettings failed, code is ${err.code}, message is ${err.message}`);
      });
    });
  }
}
```

## ContentType

Enumerates the notification content types.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Notification.Notification

| Name                             | Value         | Description              |
| --------------------------------- | ----------- |------------------|
| NOTIFICATION_CONTENT_BASIC_TEXT   | 0          | Normal text notification.         |
| NOTIFICATION_CONTENT_LONG_TEXT    | 1          | Long text notification.        |
| NOTIFICATION_CONTENT_PICTURE      | 2          | Picture-attached notification.         |
| NOTIFICATION_CONTENT_CONVERSATION | 3          | Conversation notification. Not supported currently.|
| NOTIFICATION_CONTENT_MULTILINE    | 4          | Multi-line text notification.       |
| NOTIFICATION_CONTENT_SYSTEM_LIVE_VIEW<sup>11+</sup>    | 5 | Live view notification. A third-party application cannot directly create a notification of this type. After the system proxy creates a system live view, the third-party application releases a notification with the same ID to update the specified content.|
| NOTIFICATION_CONTENT_LIVE_VIEW<sup>11+</sup>    | 6 | Common live view notification. Only system applications are supported. |

## SlotLevel

Enumerates the notification level.

**System capability**: SystemCapability.Notification.Notification

| Name                             | Value         | Description              |
| --------------------------------- | ----------- | ------------------ |
| LEVEL_NONE                        | 0           | Notification is disabled.    |
| LEVEL_MIN                         | 1           | Notification is enabled, but the notification icon is not displayed in the status bar, with no banner or alert tone.|
| LEVEL_LOW                         | 2           | Notification is enabled, and the notification icon is displayed in the status bar, with no banner or alert tone.|
| LEVEL_DEFAULT                     | 3           | Notification is enabled, and the notification icon is displayed in the status bar, with an alert tone but no banner.|
| LEVEL_HIGH                        | 4           | Notification is enabled, and the notification icon is displayed in the status bar, with an alert tone and banner.|


## SlotType

Enumerates the notification slot types.

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Notification.Notification

| Name                | Value      | Description      |
| -------------------- | -------- | ---------- |
| UNKNOWN_TYPE         | 0 | Unknown type. This type corresponds to [SlotLevel](#slotlevel) being **LEVEL_MIN**.|
| SOCIAL_COMMUNICATION | 1 | Notification slot for social communication. This type corresponds to [SlotLevel](#slotlevel) being **LEVEL_HIGH**.|
| SERVICE_INFORMATION  | 2 | Notification slot for service information. This type corresponds to [SlotLevel](#slotlevel) being **LEVEL_HIGH**.|
| CONTENT_INFORMATION  | 3 | Notification slot for content consultation. This type corresponds to [SlotLevel](#slotlevel) being **LEVEL_MIN**.|
| LIVE_VIEW<sup>11+</sup>            | 4 | Live view. A third-party application cannot directly create a notification of this slot type. After the system proxy creates a system live view, the third-party application releases a notification with the same ID to update the specified content. This type corresponds to [SlotLevel](#slotlevel) being **LEVEL_DEFAULT**.|
| CUSTOMER_SERVICE<sup>11+</sup>     | 5 | Customer service message. This type is used for messages between users and customer service providers. The messages must be initiated by users. This type corresponds to [SlotLevel](#slotlevel) being **LEVEL_DEFAULT**. |
| OTHER_TYPES          | 0xFFFF | Notification slot for other purposes. This type corresponds to [SlotLevel](#slotlevel) being **LEVEL_MIN**.|
