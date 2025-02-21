# @ohos.app.ability.dialogRequest (dialogRequest)

The **dialogRequest** module provides APIs related to modal dialog box processing, including obtaining the request information (used to bind a modal dialog box) and request callback (used to set the request result).
A modal dialog box is a system pop-up box that intercepts events (such as mouse, keyboard, and touchscreen events) triggered for the page displayed under it. The page can be operated only after the modal dialog box is destroyed.

> **NOTE**
>
>  - The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>  - The APIs provided by this module are used in ServiceExtensionAbilities. For a ServiceExtensionAbility that implements modal dialog boxes, you can use the APIs to obtain the request information and request callback and return the request result.

## Modules to Import

```ts
import dialogRequest from '@ohos.app.ability.dialogRequest';
```

## dialogRequest.getRequestInfo

getRequestInfo(want: Want): RequestInfo

> **NOTE**
>
>  This API can be used by a ServiceExtensionAbility. If the ServiceExtensionAbility implements modal dialog boxes, the request information can be obtained from Want. If this API is used in other scenarios, no return value is obtained.

Obtains the request information from Want.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name| Type  | Mandatory| Description                       |
| ---- | ------ | ---- | --------------------------- |
| want  | [Want](js-apis-app-ability-want.md) | Yes  | Want passed in the request for a modal dialog box.|

**Return value**

| Type  | Description                    |
| ------ | ------------------------ |
| [RequestInfo](#requestinfo) | **RequestInfo** object obtained, which is used to bind a modal dialog box.|

**Example**

```ts
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import UIAbility from '@ohos.app.ability.UIAbility';
import Want from '@ohos.app.ability.Want';
import dialogRequest from '@ohos.app.ability.dialogRequest';

export default class EntryAbility extends UIAbility {
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    try {
      let requestInfo = dialogRequest.getRequestInfo(want);
    } catch (err) {
      console.error(`getRequestInfo err= ${JSON.stringify(err)}`);
    }
  }
}
```

## dialogRequest.getRequestCallback

getRequestCallback(want: Want): RequestCallback

Obtains the request callback from Want.

> **NOTE**
>
>  This API can be used by a ServiceExtensionAbility. If the ServiceExtensionAbility implements modal dialog boxes, the request callback can be obtained from Want. If this API is used in other scenarios, no return value is obtained.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name| Type  | Mandatory| Description                       |
| ---- | ------ | ---- | --------------------------- |
| want  | [Want](js-apis-app-ability-want.md) | Yes  | Want passed in the request for a modal dialog box.|

**Return value**

| Type  | Description                    |
| ------ | ------------------------ |
| [RequestCallback](#requestcallback) | **RequestCallback** object obtained, which is used to set the return result.|

**Example**

```ts
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import UIAbility from '@ohos.app.ability.UIAbility';
import Want from '@ohos.app.ability.Want';
import dialogRequest from '@ohos.app.ability.dialogRequest';

export default class EntryAbility extends UIAbility {
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    try {
      let requestCallback = dialogRequest.getRequestCallback(want);
    } catch(err) {
      console.error(`getRequestInfo err= ${JSON.stringify(err)}`);
    }
  }
}
```

## WindowRect<sup>10+</sup>

Defines the location attributes of a modal dialog box.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name| Type  | Mandatory| Description                       |
| ---- | ------ | ---- | --------------------------- |
| left  | number | Yes  | X-coordinate of the upper left corner of the dialog box.|
| top  | number | Yes  | Y-coordinate of the upper left corner of the dialog box.|
| width  | number | Yes  | Width of the dialog box.|
| height  | number | Yes  | Height of the dialog box.|

## RequestInfo

Defines the request information, which is used as an input parameter for binding the modal dialog box.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name     | Type      | Mandatory  | Description    |
| ------------ | ------------------| ------ | ---------------------- |
| windowRect<sup>10+</sup>            | [WindowRect](#windowrect10)    | No  | Location attributes of a modal dialog box.         |

**Example**

```ts
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import UIAbility from '@ohos.app.ability.UIAbility';
import Want from '@ohos.app.ability.Want';
import dialogRequest from '@ohos.app.ability.dialogRequest';

export default class EntryAbility extends UIAbility {
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    try {
      let requestInfo = dialogRequest.getRequestInfo(want);
      console.info(`getRequestInfo windowRect=, ${JSON.stringify(requestInfo.windowRect)}` );
    } catch(err) {
      console.error(`getRequestInfo err= ${JSON.stringify(err)}`);
    }
  }
}
```

## ResultCode

Enumerates the result codes of the request for the modal dialog box.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name     | Value         | Description    |
| ------------ | ------------------ | ---------------------- |
| RESULT_OK            | 0          | The request succeeds.         |
| RESULT_CANCEL        | 1          | The request fails.         |

## RequestResult
Defines the result of the request for the modal dialog box. It contains **ResultCode** and **ResultWant**.

### Attributes

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name| Type| Read-only| Mandatory| Description|
| -------- | -------- | -------- | -------- | -------- |
| result | [ResultCode](#resultcode) | No| Yes| Result code of the request.|
| want<sup>10+</sup> | [ResultWant](js-apis-app-ability-want.md)  | No| No| Want information, such as the ability name and bundle name.|

## RequestCallback

Provides a callback for setting the modal dialog box request result.

**Model restriction**: This API can be used only in the stage model.

### RequestCallback.setRequestResult

setRequestResult(result: RequestResult): void

Sets the result of the request for the modal dialog box.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| result | [RequestResult](#requestresult) | Yes| Request result to set.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 401 | If the input parameter is not valid parameter. |

For details about the error codes, see [Ability Error Codes](errorcode-ability.md).

**Example**

```ts
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import UIAbility from '@ohos.app.ability.UIAbility';
import Want from '@ohos.app.ability.Want';
import dialogRequest from '@ohos.app.ability.dialogRequest';

export default class EntryAbility extends UIAbility {
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    try {
      let requestCallback = dialogRequest.getRequestCallback(want);
      let myResult: dialogRequest.RequestResult = {
        result : dialogRequest.ResultCode.RESULT_CANCEL,
      };
      requestCallback.setRequestResult(myResult);
    } catch(err) {
      console.error(`getRequestInfo err= ${JSON.stringify(err)}`);
    }
  }
}
```
