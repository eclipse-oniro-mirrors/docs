#  @ohos.multimodalInput.shortKey (Shortcut Key) (System API)

The **shortKey** module provides APIs to set the delay for starting an ability using a shortcut key. For example, you can set the delay to 3 seconds so that a screenshot is taken when you press and hold the shortcut key for 3 seconds.

> **NOTE**
>
> - The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
> - The APIs provided by this module are system APIs.

##  Modules to Import

```js
import shortKey from '@ohos.multimodalInput.shortKey';
```

##  shortKey.setKeyDownDuration

setKeyDownDuration(businessKey: string, delay: number, callback: AsyncCallback&lt;void&gt;): void

Sets the delay for starting an ability using shortcut keys. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.ShortKey

**Parameters**

| Name    | Type               | Mandatory| Description                                                        |
| ---------- | ------------------- | ---- | ------------------------------------------------------------ |
| businessKey| string              | Yes  | Unique service ID registered on the multimodal side. It corresponds to **businessId** in the **ability_launch_config.json** file.|
| delay      | number              | Yes  | Delay for starting an ability using shortcut keys, in milliseconds. This field is invalid only when shortcut keys are used.|
| callback   | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**. Otherwise, **err** is an error object. |                                               

**Example**

```js
import shortKey from '@ohos.multimodalInput.shortKey';
try {
  shortKey.setKeyDownDuration("screenshot", 500, (error) => {
    if (error) {
      console.log(`Set key down duration failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Set key down duration success`);
  });
} catch (error) {
  console.log(`Set key down duration failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## shortKey.setKeyDownDuration

setKeyDownDuration(businessKey: string, delay: number): Promise&lt;void&gt;

Sets the delay for starting an ability using shortcut keys. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.ShortKey

**Parameters**

| Name    | Type  | Mandatory| Description                                                        |
| ---------- | ------ | ---- | ------------------------------------------------------------ |
| businessKey| string | Yes  | Unique service ID registered on the multimodal side. It corresponds to **businessId** in the **ability_launch_config.json** file.|
| delay      | number | Yes  | Delay for starting an ability using shortcut keys, in milliseconds. This field is invalid only when shortcut keys are used.|

**Return value**

| Parameters         | Description         |
| ------------- | ------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```js
import shortKey from '@ohos.multimodalInput.shortKey';
try {
  shortKey.setKeyDownDuration("screenshot", 500).then(() => {
    console.log(`Set key down duration success`);
  });
} catch (error) {
  console.log(`Set key down duration failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```
