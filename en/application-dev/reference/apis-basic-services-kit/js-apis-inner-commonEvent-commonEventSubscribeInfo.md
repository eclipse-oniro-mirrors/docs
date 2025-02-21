# CommonEventSubscribeInfo

The **CommonEventSubscribeInfo** module provides APIs for providing subscriber information.

> **NOTE**
>
> The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Attributes

**System capability**: SystemCapability.Notification.CommonEvent

| Name               | Type          | Readable| Writable| Description                                                        |
| ------------------- | -------------- | ---- | ---- | ------------------------------------------------------------ |
| events              | Array\<string> | Yes | No | Common events to subscribe to.                                        |
| publisherPermission | string         | Yes | No | Permission of the publisher. The subscriber can receive only the events from the publisher with this permission.                                            |
| publisherDeviceId   | string         | Yes | No | Device ID. The value must be the ID of a device on the same network. Use [@ohos.deviceInfo](./js-apis-device-info.md) to obtain the UDID as the device ID of the subscriber.        |
| userId              | number         | Yes | No | User ID. If this parameter is not specified, the default value, which is the ID of the current user, will be used. The value must be an existing user ID in the system. Use [getOsAccountLocalId](./js-apis-osAccount.md#getosaccountlocalid9) to obtain the system account ID and use it as the user ID of the subscriber.|
| priority            | number         | Yes | No | Subscriber priority. The value ranges from –100 to +1000. If the value exceeds the upper or lower limit, the upper or lower limit is used.                |
| publisherBundleName<sup>11+</sup> | string         | Yes | No | Bundle name of the publisher to subscribe to.                |
