# @ohos.abilityAccessCtrl (Application Access Control)

The **abilityAccessCtrl** module provides APIs for application permission management, including authentication, authorization, and revocation.

> **NOTE**
>
> The initial APIs of this module are supported since API version 8. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```ts
import abilityAccessCtrl from '@ohos.abilityAccessCtrl'
```

## abilityAccessCtrl.createAtManager

createAtManager(): AtManager

Creates an **AtManager** instance, which is used for application access control.

**System capability**: SystemCapability.Security.AccessToken


**Return value**

| Type| Description|
| -------- | -------- |
| [AtManager](#atmanager) | **AtManager** instance created.|

**Example**

```ts
let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
```

## AtManager

Provides APIs for application access control.

### checkAccessToken<sup>9+</sup>

checkAccessToken(tokenID: number, permissionName: Permissions): Promise&lt;GrantStatus&gt;

Checks whether a permission is granted to an application. This API uses a promise to return the result.

**System capability**: SystemCapability.Security.AccessToken

**Parameters**

| Name  | Type                | Mandatory| Description                                      |
| -------- | -------------------  | ---- | ------------------------------------------ |
| tokenID   |  number   | Yes  | Application token ID, which can be obtained from [ApplicationInfo](js-apis-bundleManager-applicationInfo.md).            |
| permissionName | Permissions | Yes  | Permission to check. For details about the permissions, see [Permissions for All Applications](../../security/AccessToken/permissions-for-all.md).|

**Return value**

| Type         | Description                               |
| :------------ | :---------------------------------- |
| Promise&lt;GrantStatus&gt; | Promise used to return the permission grant state.|

**Error codes**

For details about the error codes, see [Access Control Error Codes](errorcode-access-token.md).

| ID| Error Message|
| -------- | -------- |
| 12100001 | The parameter is invalid. The tokenID is 0, or permissionName exceeds 256 bytes.|

**Example**

```ts
import abilityAccessCtrl from '@ohos.abilityAccessCtrl';
import { BusinessError } from '@ohos.base';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let tokenID: number = 0; // Use bundleManager.getApplicationInfo() to obtain the token ID for a system application, and use bundleManager.getBundleInfoForSelf() to obtain the token ID for a non-system application.
atManager.checkAccessToken(tokenID, 'ohos.permission.GRANT_SENSITIVE_PERMISSIONS').then((data: abilityAccessCtrl.GrantStatus) => {
  console.log(`checkAccessToken success, data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
  console.log(`checkAccessToken fail, err->${JSON.stringify(err)}`);
});
```

### verifyAccessTokenSync<sup>9+</sup>

verifyAccessTokenSync(tokenID: number, permissionName: Permissions): GrantStatus

Verifies whether a permission is granted to an application. This API returns the result synchronously.

**System capability**: SystemCapability.Security.AccessToken

**Parameters**

| Name  | Type                | Mandatory| Description                                      |
| -------- | -------------------  | ---- | ------------------------------------------ |
| tokenID   |  number   | Yes  | Application token ID, which can be obtained from [ApplicationInfo](js-apis-bundleManager-applicationInfo.md).             |
| permissionName | Permissions | Yes  | Permission to verify. For details about the permissions, see [Permissions for All Applications](../../security/AccessToken/permissions-for-all.md).|

**Return value**

| Type         | Description                               |
| :------------ | :---------------------------------- |
| [GrantStatus](#grantstatus) | Permission grant state.|

**Error codes**

For details about the error codes, see [Access Control Error Codes](errorcode-access-token.md).

| ID| Error Message|
| -------- | -------- |
| 12100001 | The parameter is invalid. The tokenID is 0, or permissionName exceeds 256 bytes.|

**Example**

```ts
import abilityAccessCtrl from '@ohos.abilityAccessCtrl';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let tokenID: number = 0; // Use bundleManager.getApplicationInfo() to obtain the token ID for a system application, and use bundleManager.getBundleInfoForSelf() to obtain the token ID for a non-system application.
let data: abilityAccessCtrl.GrantStatus = atManager.verifyAccessTokenSync(tokenID, 'ohos.permission.GRANT_SENSITIVE_PERMISSIONS');
console.log(`data->${JSON.stringify(data)}`);
```

### verifyAccessToken<sup>9+</sup>

verifyAccessToken(tokenID: number, permissionName: Permissions): Promise&lt;GrantStatus&gt;

Verifies whether a permission is granted to an application. This API uses a promise to return the result.

> **NOTE**
>
> You are advised to use [checkAccessToken](#checkaccesstoken9).

**System capability**: SystemCapability.Security.AccessToken

**Parameters**

| Name  | Type                | Mandatory| Description                                      |
| -------- | -------------------  | ---- | ------------------------------------------ |
| tokenID   |  number   | Yes  | Application token ID, which can be obtained from [ApplicationInfo](js-apis-bundleManager-applicationInfo.md).            |
| permissionName | Permissions | Yes  | Permission to verify. For details about the permissions, see [Permissions for All Applications](../../security/AccessToken/permissions-for-all.md).|

**Return value**

| Type         | Description                               |
| :------------ | :---------------------------------- |
| Promise&lt;GrantStatus&gt; | Promise used to return the permission grant state.|

**Example**

```ts
import abilityAccessCtrl, { Permissions } from '@ohos.abilityAccessCtrl';
import { BusinessError } from '@ohos.base';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let tokenID: number = 0; // Use bundleManager.getApplicationInfo() to obtain the token ID for a system application, and use bundleManager.getBundleInfoForSelf() to obtain the token ID for a non-system application.
let permissionName: Permissions = 'ohos.permission.GRANT_SENSITIVE_PERMISSIONS';
atManager.verifyAccessToken(tokenID, permissionName).then((data: abilityAccessCtrl.GrantStatus) => {
  console.log(`promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
  console.log(`verifyAccessToken fail, err->${JSON.stringify(err)}`);
});
```

### requestPermissionsFromUser<sup>9+</sup>

requestPermissionsFromUser(context: Context, permissionList: Array&lt;Permissions&gt;, requestCallback: AsyncCallback&lt;PermissionRequestResult&gt;) : void

Requests user authorization in a dialog box opened by a UIAbility. This API uses an asynchronous callback to return the result.

If the user rejects to grant the permission, the authorization dialog box cannot be displayed again. If required, the user can manually grant the permission on the **Settings** page.

> **NOTE**
>
> Only UIAbility is supported.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.Security.AccessToken

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| context | Context | Yes| Context of the UIAbility.|
| permissionList | Array&lt;Permissions&gt; | Yes| Permissions requested. For details about the permissions, see [Permissions for All Applications](../../security/AccessToken/permissions-for-all.md).|
| requestCallback | AsyncCallback&lt;[PermissionRequestResult](js-apis-permissionrequestresult.md)&gt; | Yes| Callback invoked to return the result.|

**Error codes**

For details about the error codes, see [Access Control Error Codes](errorcode-access-token.md).

| ID| Error Message|
| -------- | -------- |
| 12100001 | The parameter is invalid. The context is invalid when it does not belong to the application itself. |

**Example**
For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

```ts
import abilityAccessCtrl, { Context, PermissionRequestResult } from '@ohos.abilityAccessCtrl';
import { BusinessError } from '@ohos.base';
import common from '@ohos.app.ability.common';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let context: Context = getContext(this) as common.UIAbilityContext;
atManager.requestPermissionsFromUser(context, ['ohos.permission.CAMERA'], (err: BusinessError, data: PermissionRequestResult)=>{
  if (err) {
    console.log(`requestPermissionsFromUser fail, err->${JSON.stringify(err)}`);
  } else {
    console.info('data:' + JSON.stringify(data));
    console.info('data permissions:' + data.permissions);
    console.info('data authResults:' + data.authResults);
  }
});
```

### requestPermissionsFromUser<sup>9+</sup>

requestPermissionsFromUser(context: Context, permissionList: Array&lt;Permissions&gt;) : Promise&lt;PermissionRequestResult&gt;

Requests user authorization in a dialog box opened by a UIAbility. This API uses a promise to return the result.

If the user rejects to grant the permission, the authorization dialog box cannot be displayed again. If required, the user can manually grant the permission on the **Settings** page.

> **NOTE**
>
> Only UIAbility is supported.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.Security.AccessToken

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| context | Context | Yes| Context of the UIAbility.|
| permissionList | Array&lt;Permissions&gt; | Yes| Permissions requested. For details about the permissions, see [Permissions for All Applications](../../security/AccessToken/permissions-for-all.md).|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;[PermissionRequestResult](js-apis-permissionrequestresult.md)&gt; | Promise used to return the result.|

**Error codes**

For details about the error codes, see [Access Control Error Codes](errorcode-access-token.md).

| ID| Error Message|
| -------- | -------- |
| 12100001 | The parameter is invalid. The context is invalid when it does not belong to the application itself. |

**Example**
For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

```ts
import abilityAccessCtrl, { Context, PermissionRequestResult } from '@ohos.abilityAccessCtrl';
import { BusinessError } from '@ohos.base';
import common from '@ohos.app.ability.common';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let context: Context = getContext(this) as common.UIAbilityContext;
atManager.requestPermissionsFromUser(context, ['ohos.permission.CAMERA']).then((data: PermissionRequestResult) => {
  console.info('data:' + JSON.stringify(data));
  console.info('data permissions:' + data.permissions);
  console.info('data authResults:' + data.authResults);
}).catch((err: BusinessError) => {
  console.info('data:' + JSON.stringify(err));
});
```

### verifyAccessToken<sup>(deprecated)</sup>

verifyAccessToken(tokenID: number, permissionName: string): Promise&lt;GrantStatus&gt;

Verifies whether a permission is granted to an application. This API uses a promise to return the result.

> **NOTE**
>
> This API is no longer maintained since API version 9. Use [checkAccessToken](#checkaccesstoken9) instead.

**System capability**: SystemCapability.Security.AccessToken

**Parameters**

| Name  | Type                | Mandatory| Description                                      |
| -------- | -------------------  | ---- | ------------------------------------------ |
| tokenID   |  number   | Yes  | Application token ID, which can be obtained from [ApplicationInfo](js-apis-bundleManager-applicationInfo.md).            |
| permissionName | string | Yes  | Permission to verify. For details about the permissions, see [Permissions for All Applications](../../security/AccessToken/permissions-for-all.md).|

**Return value**

| Type         | Description                               |
| :------------ | :---------------------------------- |
| Promise&lt;GrantStatus&gt; | Promise used to return the permission grant state.|

**Example**

```ts
import abilityAccessCtrl from '@ohos.abilityAccessCtrl';
import { BusinessError } from '@ohos.base';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let tokenID: number = 0; // Use bundleManager.getApplicationInfo() to obtain the token ID for a system application, and use bundleManager.getBundleInfoForSelf() to obtain the token ID for a non-system application.
atManager.verifyAccessToken(tokenID, 'ohos.permission.GRANT_SENSITIVE_PERMISSIONS').then((data: abilityAccessCtrl.GrantStatus) => {
  console.log(`promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
  console.log(`verifyAccessToken fail, err->${JSON.stringify(err)}`);
});
```

### checkAccessTokenSync<sup>10+</sup>

checkAccessTokenSync(tokenID: number, permissionName: Permissions): GrantStatus

Checks whether a permission is granted to an application. This API returns the result synchronously.

**System capability**: SystemCapability.Security.AccessToken

**Parameters**

| Name  | Type                | Mandatory| Description                                      |
| -------- | -------------------  | ---- | ------------------------------------------ |
| tokenID   |  number   | Yes  | Application token ID, which can be obtained from [ApplicationInfo](js-apis-bundleManager-applicationInfo.md).             |
| permissionName | Permissions | Yes  | Permission to check. For details about the permissions, see [Permissions for All Applications](../../security/AccessToken/permissions-for-all.md).|

**Return value**

| Type         | Description                               |
| :------------ | :---------------------------------- |
| [GrantStatus](#grantstatus) | Permission grant state.|

**Error codes**

For details about the error codes, see [Access Control Error Codes](errorcode-access-token.md).

| ID| Error Message|
| -------- | -------- |
| 12100001 | The parameter is invalid. The tokenID is 0, or permissionName exceeds 256 bytes.|

**Example**

```ts
import abilityAccessCtrl, { Permissions } from '@ohos.abilityAccessCtrl';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let tokenID: number = 0; // Use bundleManager.getApplicationInfo() to obtain the token ID for a system application, and use bundleManager.getBundleInfoForSelf() to obtain the token ID for a non-system application.
let permissionName: Permissions = 'ohos.permission.GRANT_SENSITIVE_PERMISSIONS';
let data: abilityAccessCtrl.GrantStatus = atManager.checkAccessTokenSync(tokenID, permissionName);
console.log(`data->${JSON.stringify(data)}`);
```

### GrantStatus

Enumerates the permission grant states.

**System capability**: SystemCapability.Security.AccessToken

| Name              |    Value| Description       |
| ------------------ | ----- | ----------- |
| PERMISSION_DENIED  | -1    | Permission denied.|
| PERMISSION_GRANTED | 0     | Permission granted.|
