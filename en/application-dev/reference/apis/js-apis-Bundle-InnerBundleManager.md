# @ohos.bundle.innerBundleManager (innerBundleManager)

The **innerBundleManager** module provides APIs for the **Home Screen** application.

>
> The initial APIs of this module are supported since API version 8. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> This module is deprecated since API version 9. You are advised to use [launcherBundleManager](js-apis-launcherBundleManager.md) and [bundleMonitor](js-apis-bundleMonitor.md) instead.

## Modules to Import

```typescript
import innerBundleManager from '@ohos.bundle.innerBundleManager';
```

## System Capability

SystemCapability.BundleManager.BundleFramework


## innerBundleManager.getLauncherAbilityInfos<sup>(deprecated)</sup>

getLauncherAbilityInfos(bundleName: string, userId: number, callback: AsyncCallback&lt;Array&lt;LauncherAbilityInfo&gt;&gt;) : void

Obtains the launcher ability information based on a given bundle name. This API uses an asynchronous callback to return the result.
> This API is deprecated since API version 9. You are advised to use [launcherBundleManager.getLauncherAbilityInfo](js-apis-launcherBundleManager.md#launcherbundlemanagergetlauncherabilityinfo9) instead.

**Required permissions**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**System capability**

SystemCapability.BundleManager.BundleFramework

**System API**

This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                                                        | Mandatory| Description                                      |
| ---------- | ------------------------------------------------------------ | ---- | ------------------------------------------ |
| bundleName | string                                                       | Yes  | Bundle name.                  |
| userId     | number                                                       | Yes  | User ID. The value must be greater than or equal to 0.             |
| callback   | AsyncCallback\<Array<[LauncherAbilityInfo](js-apis-bundle-LauncherAbilityInfo.md)>> | Yes  | Callback used to return an array of the launcher ability information.|


## innerBundleManager.getLauncherAbilityInfos<sup>(deprecated)</sup>

getLauncherAbilityInfos(bundleName: string, userId: number) : Promise&lt;Array&lt;LauncherAbilityInfo&gt;&gt;

Obtains the launcher ability information based on a given bundle name. This API uses a promise to return the result.
> This API is deprecated since API version 9. You are advised to use [launcherBundleManager.getLauncherAbilityInfo](js-apis-launcherBundleManager.md#launcherbundlemanagergetlauncherabilityinfo9) instead.

**Required permissions**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**System capability**

SystemCapability.BundleManager.BundleFramework

**System API**

This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type  | Mandatory| Description                         |
| ---------- | ------ | ---- | ----------------------------- |
| bundleName | string | Yes  | Bundle name.     |
| userId     | number | Yes  | User ID. The value must be greater than or equal to 0.|

**Return value**

| Type                                                        | Description                     |
| ------------------------------------------------------------ | ------------------------- |
| Promise\<Array<[LauncherAbilityInfo](js-apis-bundle-LauncherAbilityInfo.md)>> | Promise used to return an array of the launcher ability information.|

## innerBundleManager.on<sup>(deprecated)</sup>

on(type:"BundleStatusChange", bundleStatusCallback : BundleStatusCallback, callback: AsyncCallback&lt;string&gt;) : void

Registers a callback to receive bundle status changes. This API uses an asynchronous callback to return the result.
> This API is deprecated since API version 9. You are advised to use [bundleMonitor.on](js-apis-bundleMonitor.md#bundlemonitoron) instead.

**Required permissions**

ohos.permission.LISTEN_BUNDLE_CHANGE

**System capability**

SystemCapability.BundleManager.BundleFramework

**System API**

This is a system API and cannot be called by third-party applications.

**Parameters**

| Name             | Type                 | Mandatory| Description                                              |
| -------------------- | --------------------- | ---- | ---------------------------------------------------- |
| type                 | string | Yes  | Event type. Only **BundleStatusChange** is supported.            |
| bundleStatusCallback | [BundleStatusCallback](js-apis-Bundle-BundleStatusCallback.md) | Yes  | Callback to register.                                  |
| callback             | AsyncCallback\<string> | Yes  | Callback used to return a successful result or error information.|

## innerBundleManager.on<sup>(deprecated)</sup>

on(type:"BundleStatusChange", bundleStatusCallback : BundleStatusCallback) : Promise&lt;string&gt;

Registers a callback to receive bundle status changes. This API uses a promise to return the result.
> This API is deprecated since API version 9. You are advised to use [bundleMonitor.on](js-apis-bundleMonitor.md#bundlemonitoron) instead.

**Required permissions**

ohos.permission.LISTEN_BUNDLE_CHANGE

**System capability**

SystemCapability.BundleManager.BundleFramework

**System API**

This is a system API and cannot be called by third-party applications.

**Parameters**

| Name              | Type                                                        | Mandatory| Description                                      |
| -------------------- | ------------------------------------------------------------ | ---- | ------------------------------------------ |
| type                 | string                                                       | Yes  | Event type. Only **BundleStatusChange** is supported.|
| bundleStatusCallback | [BundleStatusCallback](js-apis-Bundle-BundleStatusCallback.md) | Yes  | Callback to register.                        |

**Return value**

| Type           | Description                               |
| --------------- | ----------------------------------- |
| Promise\<string> | Promise used to return a successful result or error information.|

## innerBundleManager.off<sup>(deprecated)</sup>

off(type:"BundleStatusChange", callback: AsyncCallback&lt;string&gt;) : void

Deregisters the callback that receives bundle status changes. This API uses an asynchronous callback to return the result.
> This API is deprecated since API version 9. You are advised to use [bundleMonitor.off](js-apis-bundleMonitor.md#bundlemonitoroff) instead.

**Required permissions**

ohos.permission.LISTEN_BUNDLE_CHANGE

**System capability**

SystemCapability.BundleManager.BundleFramework

**System API**

This is a system API and cannot be called by third-party applications.

**Parameters**

| Name | Type                 | Mandatory| Description                                              |
| -------- | --------------------- | ---- | ---------------------------------------------------- |
| type     | string | Yes  | Event type. Only **BundleStatusChange** is supported.              |
| callback | AsyncCallback\<string> | Yes  | Callback used to return a successful result or error information.|

## innerBundleManager.off<sup>(deprecated)</sup>

off(type:"BundleStatusChange") : Promise&lt;string&gt;

Deregisters the callback that receives bundle status changes. This API uses a promise to return the result.
> This API is deprecated since API version 9. You are advised to use [bundleMonitor.off](js-apis-bundleMonitor.md#bundlemonitoroff) instead.

**Required permissions**

ohos.permission.LISTEN_BUNDLE_CHANGE

**System capability**

SystemCapability.BundleManager.BundleFramework

**System API**

This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type  | Mandatory| Description                                      |
| ------ | ------ | ---- | ------------------------------------------ |
| type   | string | Yes  | Event type. Only **BundleStatusChange** is supported.|

**Return value**

| Type           | Description                               |
| --------------- | ----------------------------------- |
| Promise\<string> | Promise used to return a successful result or error information.|

## innerBundleManager.getAllLauncherAbilityInfos<sup>(deprecated)</sup>

getAllLauncherAbilityInfos(userId: number, callback: AsyncCallback&lt;Array&lt;LauncherAbilityInfo&gt;&gt;) : void

Obtains the information about all launcher abilities. This API uses an asynchronous callback to return the result.
> This API is deprecated since API version 9. You are advised to use [launcherBundleManager.getAllLauncherAbilityInfo](js-apis-launcherBundleManager.md#launcherbundlemanagergetalllauncherabilityinfo9) instead.

**Required permissions**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**System capability**

SystemCapability.BundleManager.BundleFramework

**System API**

This is a system API and cannot be called by third-party applications.

**Parameters**

| Name  | Type                                                        | Mandatory| Description                                                 |
| -------- | ------------------------------------------------------------ | ---- | ----------------------------------------------------- |
| userId   | number                                                       | Yes  | User ID. The value must be greater than or equal to 0.|
| callback | AsyncCallback\<Array<[LauncherAbilityInfo](js-apis-bundle-LauncherAbilityInfo.md)>> | Yes  | Callback used to return an array of the launcher ability information.           |

## innerBundleManager.getAllLauncherAbilityInfos<sup>(deprecated)</sup>

getAllLauncherAbilityInfos(userId: number) : Promise&lt;Array&lt;LauncherAbilityInfo&gt;&gt;

Obtains the information about all launcher abilities. This API uses a promise to return the result.
> This API is deprecated since API version 9. You are advised to use [launcherBundleManager.getAllLauncherAbilityInfo](js-apis-launcherBundleManager.md#launcherbundlemanagergetalllauncherabilityinfo9) instead.

**Required permissions**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**System capability**

SystemCapability.BundleManager.BundleFramework

**System API**

This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type  | Mandatory| Description                                                 |
| ------ | ------ | ---- | ----------------------------------------------------- |
| userId | number | Yes  | User ID. The value must be greater than or equal to 0.|

**Return value**

| Type                                                        | Description                     |
| ------------------------------------------------------------ | ------------------------- |
| Promise\<Array<[LauncherAbilityInfo](js-apis-bundle-LauncherAbilityInfo.md)>> | Promise used to return an array of the launcher ability information.|

## innerBundleManager.getShortcutInfos<sup>(deprecated)</sup>

getShortcutInfos(bundleName :string, callback: AsyncCallback&lt;Array&lt;ShortcutInfo&gt;&gt;) : void

Obtains the shortcut information based on a given bundle name. This API uses an asynchronous callback to return the result.
> This API is deprecated since API version 9. You are advised to use [launcherBundleManager.getShortcutInfo](js-apis-launcherBundleManager.md#launcherbundlemanagergetshortcutinfo9) instead.

**Required permissions**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**System capability**

SystemCapability.BundleManager.BundleFramework

**System API**

This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                                                        | Mandatory| Description                                          |
| ---------- | ------------------------------------------------------------ | ---- | ---------------------------------------------- |
| bundleName | string                                                       | Yes  | Bundle name.                      |
| callback   | AsyncCallback\<Array<[ShortcutInfo](js-apis-bundle-ShortcutInfo.md)>> | Yes  | Callback used to return an array of the shortcut information.|

## innerBundleManager.getShortcutInfos<sup>(deprecated)</sup>

getShortcutInfos(bundleName : string) : Promise&lt;Array&lt;ShortcutInfo&gt;&gt;

Obtains the shortcut information based on a given bundle name. This API uses a promise to return the result.
> This API is deprecated since API version 9. You are advised to use [launcherBundleManager.getShortcutInfo](js-apis-launcherBundleManager.md#launcherbundlemanagergetshortcutinfo9) instead.

**Required permissions**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**System capability**

SystemCapability.BundleManager.BundleFramework

**System API**

This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type  | Mandatory| Description                    |
| ---------- | ------ | ---- | ------------------------ |
| bundleName | string | Yes  | Bundle name.|

**Return value**

| Type                                                    | Description                         |
| -------------------------------------------------------- | ----------------------------- |
| Promise\<Array<[ShortcutInfo](js-apis-bundle-ShortcutInfo.md)>> | Promise used to return an array of the shortcut information.|
