# NotificationFlags

The **NotificationFlags** module implements a **NotificationFlags** instance.

> **NOTE**
>
> The initial APIs of this module are supported since API version 8. Newly added APIs will be marked with a superscript to indicate their earliest API version.

**System capability**: SystemCapability.Notification.Notification

## Attributes

| Name            | Type                   | Mandatory| Description                              |
| ---------------- | ---------------------- | ---- | --------------------------------- |
| soundEnabled     | [NotificationFlagStatus](#notificationflagstatus) | No  | Whether to enable the sound alert for the notification.                 |
| vibrationEnabled | [NotificationFlagStatus](#notificationflagstatus) | No  | Whether to enable vibration for the notification.              |


## NotificationFlagStatus

Describes the notification flag status.

**System capability**: SystemCapability.Notification.Notification

| Name          | Value | Description                              |
| -------------- | --- | --------------------------------- |
| TYPE_NONE      | 0   | The default flag is used.                        |
| TYPE_OPEN      | 1   | The notification flag is enabled.                    |
| TYPE_CLOSE     | 2   | The notification flag is disabled.                    |
