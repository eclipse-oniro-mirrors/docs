# @ohos.app.ability.quickFixManager (quickFixManager) (System API)

The **quickFixManager** module provides APIs for quick fix. With quick fix, you can fix bugs in your application by applying patches, which is more efficient than by updating the entire application.

> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version. 
> The APIs of this module are system APIs and cannot be called by third-party applications.

## Modules to Import

```ts
import quickFixManager from '@ohos.app.ability.quickFixManager';
```

## HapModuleQuickFixInfo

Defines the quick fix information at the HAP file level.

**System capability**: SystemCapability.Ability.AbilityRuntime.QuickFix

**System API**: This is a system API and cannot be called by third-party applications.

| Name       | Type                | Read-only| Mandatory| Description                                                        |
| ----------- | -------------------- | ---- | ---- | ------------------------------------------------------------ |
| moduleName    | string               | Yes|  Yes  | Name of the HAP file.                              |
| originHapHash    | string            | Yes| Yes  | Hash value of the HAP file.                              |
| quickFixFilePath    | string         | Yes| Yes  | Installation path of the quick fix patch file.                              |

## ApplicationQuickFixInfo

Defines the quick fix information at the application level.

**System capability**: SystemCapability.Ability.AbilityRuntime.QuickFix

**System API**: This is a system API and cannot be called by third-party applications.

| Name       | Type                | Read-only| Mandatory| Description                                                        |
| ----------- | -------------------- | ---- | ---- | ------------------------------------------------------------ |
| bundleName    | string               | Yes| Yes  | Bundle name.                      |
| bundleVersionCode    | number        | Yes| Yes  | Internal version number of the application.                              |
| bundleVersionName    | string        | Yes| Yes  | Version number of the application that is shown to users.                              |
| quickFixVersionCode    | number      | Yes| Yes  | Version code of the quick fix patch package.                              |
| quickFixVersionName    | string      | Yes| Yes  | Text description of the version number of the quick fix patch package.                              |
| hapModuleQuickFixInfo    | Array\<[HapModuleQuickFixInfo](#hapmodulequickfixinfo)>   | Yes| Yes  | Quick fix information at the HAP file level.    |

## quickFixManager.applyQuickFix

applyQuickFix(hapModuleQuickFixFiles: Array\<string>, callback: AsyncCallback\<void>): void;

Applies a quick fix patch. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INSTALL_BUNDLE

**System capability**: SystemCapability.Ability.AbilityRuntime.QuickFix

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Parameter| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| hapModuleQuickFixFiles | Array\<string> | Yes| Quick fix patch files, each of which must contain a valid file path.|
| callback | AsyncCallback\<void> | Yes| Callback used to return the result. If the quick fix patch is installed, **err** is **undefined**. Otherwise, **err** is an error object.|

**Error codes**

If an error occurs during patch installation, the error code and message are returned through the common event [COMMON_EVENT_QUICK_FIX_APPLY_RESULT](../apis-basic-services-kit/common_event/commonEvent-definitions.md#common_event_quick_fix_apply_result9).

| ID| Error Message|
| ------- | -------- |
| 18500002 | The specified quick fix is invalid. It may not exist or inaccessible. |
| 18500008 | Internal error. |

For details about the error codes, see [Ability Error Codes](errorcode-ability.md).

> **NOTE**
>
> The file path passed in the API must be an application sandbox path. For details about how to obtain the sandbox path, see [Obtaining the Sandbox Path](js-apis-bundle-BundleInstaller-sys.md#obtaining-the-sandbox-path). The path mapped to the device is **/proc/<*applicationProcessId*>/root/*sandboxPath***.

**Example**

```ts
import quickFixManager from '@ohos.app.ability.quickFixManager';

  try {
    let hapModuleQuickFixFiles = ['/data/storage/el2/base/entry.hqf'];
    quickFixManager.applyQuickFix(hapModuleQuickFixFiles, (error) => {
      if (error) {
          console.error( `applyQuickFix failed with error: ${error}`);
      } else {
          console.info( 'applyQuickFix success');
      }
    });
  } catch (paramError) {
    console.error(`error.code: ${paramError.code}, error.message: ${paramError.message}`);
  }
```

## quickFixManager.applyQuickFix

applyQuickFix(hapModuleQuickFixFiles: Array\<string>): Promise\<void>;

Applies a quick fix patch. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INSTALL_BUNDLE

**System capability**: SystemCapability.Ability.AbilityRuntime.QuickFix

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Parameter| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| hapModuleQuickFixFiles | Array\<string> | Yes| Quick fix patch files, each of which must contain a valid file path.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

If an error occurs during patch installation, the error code and message are returned through the common event [COMMON_EVENT_QUICK_FIX_APPLY_RESULT](../apis-basic-services-kit/common_event/commonEvent-definitions.md#common_event_quick_fix_apply_result9).

| ID| Error Message|
| ------- | -------- |
| 18500002 | The specified quick fix is invalid. It may not exist or inaccessible. |
| 18500008 | Internal error. |

For details about the error codes, see [Ability Error Codes](errorcode-ability.md).

**Example**

```ts
import quickFixManager from '@ohos.app.ability.quickFixManager';
import { BusinessError } from '@ohos.base';

  let hapModuleQuickFixFiles = ['/data/storage/el2/base/entry.hqf'];
  try {
    quickFixManager.applyQuickFix(hapModuleQuickFixFiles).then(() => {
      console.info('applyQuickFix success');
    }).catch((error: BusinessError) => {
      console.error(`applyQuickFix err: ${error}`);
    });
  } catch (paramError) {
    console.error(`error: ${paramError.code}, ${paramError.message}`);
  }
```

## quickFixManager.getApplicationQuickFixInfo

getApplicationQuickFixInfo(bundleName: string, callback: AsyncCallback\<ApplicationQuickFixInfo>): void;

Obtains the quick fix information of the application. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**System capability**: SystemCapability.Ability.AbilityRuntime.QuickFix

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Parameter| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| bundleName | string | Yes|Bundle name. |
| callback | AsyncCallback\<[ApplicationQuickFixInfo](#applicationquickfixinfo)> | Yes| Callback used to return the quick fix information.|

**Error codes**

| ID| Error Message|
| ------- | -------- |
| 18500001 | The specified bundleName is invalid. |
| 18500008 | Internal error. |

For details about the error codes, see [Ability Error Codes](errorcode-ability.md).

**Example**

```ts
import quickFixManager from '@ohos.app.ability.quickFixManager';

  try {
    let bundleName = 'bundleName';
    quickFixManager.getApplicationQuickFixInfo(bundleName, (error, data) => {
      if (error) {
        console.error(`getApplicationQuickFixInfo error: ${error}`);
      } else {
        console.info(`getApplicationQuickFixInfo success: ${data}`);
      }
    });
  } catch (paramError) {
    console.error(`error: ${paramError.code}, ${paramError.message}`);
  }
```

## quickFixManager.getApplicationQuickFixInfo

getApplicationQuickFixInfo(bundleName: string): Promise\<ApplicationQuickFixInfo>;

Obtains the quick fix information of the application. This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**System capability**: SystemCapability.Ability.AbilityRuntime.QuickFix

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Parameter| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| bundleName | string | Yes| Bundle name.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise\<[ApplicationQuickFixInfo](#applicationquickfixinfo)> | Promise used to return the quick fix information.|

**Error codes**

| ID| Error Message|
| ------- | -------- |
| 18500001 | The specified bundleName is invalid. |
| 18500008 | Internal error. |

For details about the error codes, see [Ability Error Codes](errorcode-ability.md).

**Example**

  ```ts
import quickFixManager from '@ohos.app.ability.quickFixManager';
import { BusinessError } from '@ohos.base';

  try {
    let bundleName = 'bundleName';
    quickFixManager.getApplicationQuickFixInfo(bundleName).then((data) => {
      console.info(`getApplicationQuickFixInfo success: ${data}`);
    }).catch((error: BusinessError) => {
      console.error(`getApplicationQuickFixInfo err: ${error}`);
    });
  } catch (paramError) {
    console.error(`error: ${paramError.code}, ${paramError.message}`);
  }
  ```

## quickFixManager.revokeQuickFix<sup>10+<sup>

revokeQuickFix(bundleName: string, callback: AsyncCallback\<void>): void;

Revokes quick fix. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_BUNDLE_INFO_PRIVILEGED and ohos.permission.INSTALL_BUNDLE

**System capability**: SystemCapability.Ability.AbilityRuntime.QuickFix

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Parameter| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| bundleName | string | Yes| Name of the bundle for which the patch needs to be revoked.|
| callback | AsyncCallback\<void> | Yes| Callback used to return the result. If quick fix is revoked, **err** is **undefined**. Otherwise, **err** is an error object.|

**Error codes**

| ID| Error Message|
| ------- | -------- |
| 18500001 | The bundle is not exist or no patch has applied. |
| 18500009 | The application has a apply quick fix task that is being processed. |

If an error occurs during patch installation, the error code and message are returned through the common event [COMMON_EVENT_QUICK_FIX_REVOKE_RESULT](../apis-basic-services-kit/common_event/commonEvent-ability.md#common_event_quick_fix_revoke_result10).



**Example**

```ts
import quickFixManager from '@ohos.app.ability.quickFixManager';

  let bundleName = "com.example.myapplication";
  quickFixManager.revokeQuickFix(bundleName, (err) => {
    console.info("revokeQuickFix " + bundleName + " " + JSON.stringify(err));
  });
```

## quickFixManager.revokeQuickFix<sup>10+<sup>

revokeQuickFix(bundleName: string): Promise\<void>;

Revokes quick fix. This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_BUNDLE_INFO_PRIVILEGED and ohos.permission.INSTALL_BUNDLE

**System capability**: SystemCapability.Ability.AbilityRuntime.QuickFix

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Parameter| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| bundleName | string | Yes| Name of the bundle for which the patch needs to be revoked.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Ability Error Codes](errorcode-ability.md).

| ID| Error Message|
| ------- | -------- |
| 18500001 | The bundle is not exist or no patch has applied. |
| 18500009 | The application has a apply quick fix task that is being processed. |

If an error occurs during patch installation, the error code and message are returned through the common event [COMMON_EVENT_QUICK_FIX_REVOKE_RESULT](../apis-basic-services-kit/common_event/commonEvent-ability.md#common_event_quick_fix_revoke_result10). The table below lists the possible error codes and messages.

**Example**

```ts
import quickFixManager from '@ohos.app.ability.quickFixManager';
import { BusinessError } from '@ohos.base';

  let bundleName = "com.example.myapplication";
  quickFixManager.revokeQuickFix(bundleName).then(() => {
    console.info("revokeQuickFix " + bundleName +" ok");
  }).catch((err: BusinessError) => {
    console.info("revokeQuickFix " + bundleName +" failed, error code is ", JSON.stringify((err)));
  });
```

   