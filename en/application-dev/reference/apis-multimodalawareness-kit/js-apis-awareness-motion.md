# @ohos.multimodalawareness.motion (Motion Sensing)

The **motion** module provides the capability of sensing user motions, including user gestures and actions.

> **NOTE**
>
> The initial APIs of this module are supported since API version 15. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```ts
import { motion } from '@kit.MultimodalAwarenessKit';
```

## OperatingHandStatus

Defines the status of the operating hand.

**System capability**: SystemCapability.MultimodalAwareness.Motion

| Name               | Value  | Description                  |
| ------------------- | ---- | ---------------------- |
| UNKNOWN_STATUS  | 0    | Unknown status.|
| LEFT_HAND_OPERATED  | 1    | Left hand in use.|
| RIGHT_HAND_OPERATED | 2    | Right hand in use.|




## motion.on('operatingHandChanged')

 on(type: 'operatingHandChanged', callback: Callback&lt;OperatingHandStatus&gt;): void;

Subscribes to operating hand change events.

**Required permissions**: ohos.permission.ACTIVITY_MOTION

**System capability**: SystemCapability.MultimodalAwareness.Motion

**Parameters**

| Name  | Type                            | Mandatory| Description                                                        |
| -------- | -------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                           | Yes  | Event type. This parameter has a fixed value of **operatingHandChanged**.|
| callback | Callback&lt;[OperatingHandStatus](#operatinghandstatus)&gt; | Yes  | Callback used to return the operating hand status.                                  |

**Error codes**

For details about the error codes, see [Motion Sensing Error Codes](errorcode-motion.md) and [Universal Error Codes](../errorcode-universal.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 201      | Permission denied. An attempt was made to subscribe operatingHandChanged event forbidden by permission: ohos.permission.ACTIVITY_MOTION. |
| 401      | Parameter error. Parameter verification failed. |
| 801      | Capability not supported. Function can not work correctly due to limited device capabilities. |
| 31500001 | Service exception. |
| 31500002 | Subscribe Failed. |

**Example**

```ts
motion.on('operatingHandChanged', (data:motion.OperatingHandStatus) => {
    console.info('on success' + data);
})
```



## motion.off('operatingHandChanged')

off(type: 'operatingHandChanged', callback?: Callback&lt;OperatingHandStatus&gt;): void;

Unsubscribes from operating hand change events.

**Required permissions**: ohos.permission.ACTIVITY_MOTION

**System capability**: SystemCapability.MultimodalAwareness.Motion

**Parameters**

| Name  | Type                            | Mandatory| Description                                                        |
| -------- | -------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                           | Yes  | Event type. This parameter has a fixed value of **operatingHandChanged**.|
| callback | Callback&lt;[OperatingHandStatus](#operatinghandstatus)&gt; | No  | Callback used to return the operating hand status.                                  |

**Error codes**

For details about the error codes, see [Motion Sensing Error Codes](errorcode-motion.md) and [Universal Error Codes](../errorcode-universal.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 201      | Permission denied. An attempt was made to unsubscribe operatingHandChanged event forbidden by permission: ohos.permission.ACTIVITY_MOTION. |
| 401      | Parameter error. Parameter verification failed. |
| 801      | Capability not supported. Function can not work correctly due to limited device capabilities. |
| 31500001 | Service exception. |
| 31500003 | Unsubscribe Failed. |

**Example**

```ts
motion.off('operatingHandChanged', (data:motion.OperatingHandStatus) => {
    console.info('off success' + data);
})
```



## motion.getRecentOperatingHandStatus()

getRecentOperatingHandStatus(): OperatingHandStatus;

Obtains the latest operating hand status.

**Required permissions**: ohos.permission.ACTIVITY_MOTION

**System capability**: SystemCapability.MultimodalAwareness.Motion

**Return value**

| Type                         | Description                                |
| ----------------------------- | ------------------------------------ |
| [OperatingHandStatus](#operatinghandstatus) | Status of the operating hand.|

**Error codes**

For details about the error codes, see [Motion Sensing Error Codes](errorcode-motion.md) and [Universal Error Codes](../errorcode-universal.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 201      | Permission denied. An attempt was made to get the recent operating hand status forbidden by permission: ohos.permission.ACTIVITY_MOTION. |
| 801      | Capability not supported. Function can not work correctly due to limited device capabilities. |
| 31500001 | Service exception. |

**Example**

```ts
let data:motion.OperatingHandStatus = motion.getRecentOperatingHandStatus();
console.info('get success' + data);
```
