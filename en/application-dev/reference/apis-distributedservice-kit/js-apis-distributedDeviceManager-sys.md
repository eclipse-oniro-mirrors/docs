# @ohos.distributedDeviceManager (Device Management) (System API)

The **distributedDeviceManager** module provides APIs for distributed device management.

Applications can call the APIs to:

- Subscribe to or unsubscribe from device state changes.
- Discover untrusted devices nearby.
- Authenticate or deauthenticate a device.
- Query the trusted device list.
- Query local device information, including the device name, type, and ID.


> **NOTE**
>
> The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> This topic describes only the system APIs provided by the module. For details about its public APIs, see [@ohos.distributedDeviceManager](js-apis-distributedDeviceManager.md).


## Modules to Import

```ts
import deviceManager from '@ohos.distributedDeviceManager';
```

## DeviceManager

Provides APIs to obtain information about trusted devices and local devices. Before calling any API of **DeviceManager**, you need to use **createDeviceManager** to create a **DeviceManager** instance, for example, **dmInstance**.

### replyUiAction

replyUiAction(action: number, actionResult: string): void;

Replies to the user's UI operation. This API can be used only by the PIN HAP of the **deviceManager**.

**Required permissions**: ohos.permission.ACCESS_SERVICE_DM

**System capability**: SystemCapability.DistributedHardware.DeviceManager

**System API**: This is a system API.

**Parameters**

  | Name      | Type           | Mandatory | Description               |
  | ------------- | --------------- | ---- | ------------------- |
  | action        | number          | Yes   | User operation.      |
  | actionResult        | string          | Yes   | Operation result.|

**Example**

For details about how to initialize **dmInstance** in the example, see [deviceManager.createDeviceManager](js-apis-distributedDeviceManager.md#devicemanagercreatedevicemanager).
  ```ts
  import { BusinessError } from '@ohos.base';

 try {
    /*
      action = 0 - Grant the permission.
      action = 1 - Revoke the permission.
      action = 2 - The user operation in the permission request dialog box times out.
      action = 3 - Cancel the display of the PIN box.
      action = 4 - Cancel the display of the PIN input box.
      action = 5 - Confirm the input in the PIN input box.
    */
    let operation = 0;
    dmInstance.replyUiAction(operation, 'extra');
  } catch (err) {
    let e: BusinessError = err as BusinessError;
    console.error('replyUiAction errCode:' + e.code + ',errMessage:' + e.message);
  }
  ```

### on('replyResult')

on(type: 'replyResult', callback: Callback&lt;{ param: string}&gt;): void;

Subscribes to the reply to the UI operation result.

**Required permissions**: ohos.permission.ACCESS_SERVICE_DM

**System capability**: SystemCapability.DistributedHardware.DeviceManager

**System API**: This is a system API.

**Parameters**

  | Name     | Type                            | Mandatory| Description                           |
  | -------- | ------------------------------------ | ---- | ------------------------------ |
  | type     | string                                | Yes | Event type, which has a fixed value of **replyResult**.|
  | callback | Callback&lt;{&nbsp;param:&nbsp;string}&gt; | Yes | Callback invoked to return the UI status change.       |

**Example**

For details about how to initialize **dmInstance** in the example, see [deviceManager.createDeviceManager](js-apis-distributedDeviceManager.md#devicemanagercreatedevicemanager).
  ```ts
  import { BusinessError } from '@ohos.base';

  class Data {
    param: string = '';
  }

  interface TmpStr {
    verifyFailed: boolean;
  }

  try {
    dmInstance.on('replyResult', (data: Data) => {
      console.log('replyResult executed, dialog closed' + JSON.stringify(data));
      let tmpStr: TmpStr = JSON.parse(data.param);
      let isShow = tmpStr.verifyFailed;
      console.log('replyResult executed, dialog closed' + isShow);
    });
  } catch (err) {
    let e: BusinessError = err as BusinessError;
    console.error('replyResult errCode:' + e.code + ',errMessage:' + e.message);
  }
  ```

### off('replyResult')

off(type: 'replyResult', callback?: Callback&lt;{ param: string}&gt;): void;

Unsubscribes from the reply to the UI operation result.

**Required permissions**: ohos.permission.ACCESS_SERVICE_DM

**System capability**: SystemCapability.DistributedHardware.DeviceManager

**System API**: This is a system API.

**Parameters**

  | Name     | Type                             | Mandatory| Description                           |
  | -------- | ------------------------------------- | ---- | ------------------------------ |
  | type     | string                                | Yes  | Event type, which has a fixed value of **replyResult**.|
  | callback | Callback&lt;{&nbsp;param:&nbsp;string}&gt; | No  | Callback to unregister.|

**Example**

For details about how to initialize **dmInstance** in the example, see [deviceManager.createDeviceManager](js-apis-distributedDeviceManager.md#devicemanagercreatedevicemanager).
  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    dmInstance.off('replyResult');
  } catch (err) {
    let e: BusinessError = err as BusinessError;
    console.error('replyResult errCode:' + e.code + ',errMessage:' + e.message);
  }
  ```
