# BundleInstaller

The **BundleInstaller** module provides APIs for you to install, uninstall, and recover bundles on devices.

> **NOTE**
>
> The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## BundleInstaller.install<sup>(deprecated)<sup>

> This API is deprecated since API version 9. You are advised to use [@ohos.bundle.installer.install](js-apis-installer.md) instead.

install(bundleFilePaths: Array&lt;string&gt;, param: InstallParam, callback: AsyncCallback&lt;InstallStatus&gt;): void;

Installs a bundle. Multiple HAP files can be installed. This API uses an asynchronous callback to return the result.

**Required permissions**

ohos.permission.INSTALL_BUNDLE

**System capability**

SystemCapability.BundleManager.BundleFramework

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name         | Type                                                        | Mandatory| Description                                                        |
| --------------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| bundleFilePaths | Array&lt;string&gt;                                          | Yes  | Sandbox path where the HAP files of the bundle are stored. For details about how to obtain the sandbox path, see [Obtaining the Sandbox Path](#obtaining-the-sandbox-path).|
| param           | [InstallParam](#installparamdeprecated)                      | Yes  | Parameters required for bundle installation.                                    |
| callback        | AsyncCallback&lt;[InstallStatus](#installstatusdeprecated)&gt; | Yes  | Callback used to return the installation status.              |

**Example**

```ts
import bundle from '@ohos.bundle';
let hapFilePaths = ['/data/storage/el2/base/haps/entry/files/'];
let installParam = {
    userId: 100,
    isKeepData: false,
    installFlag: 1,
};

bundle.getBundleInstaller().then(installer => {
    installer.install(hapFilePaths, installParam, err => {
        if (err) {
            console.error('install failed:' + JSON.stringify(err));
        } else {
            console.info('install successfully.');
        }
    });
}).catch(error => {
    console.error('getBundleInstaller failed. Cause: ' + error.message);
});
```

## BundleInstaller.uninstall<sup>(deprecated)<sup>

> This API is deprecated since API version 9. You are advised to use [uninstall](js-apis-installer.md) instead.

uninstall(bundleName: string, param: InstallParam, callback: AsyncCallback&lt;InstallStatus&gt;): void;

Uninstalls a bundle. This API uses an asynchronous callback to return the result.

**Required permissions**

ohos.permission.INSTALL_BUNDLE

**System capability**

SystemCapability.BundleManager.BundleFramework

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                                                        | Mandatory| Description                                          |
| ---------- | ------------------------------------------------------------ | ---- | ---------------------------------------------- |
| bundleName | string                                                       | Yes  | Bundle name.                              |
| param      | [InstallParam](#installparamdeprecated)                      | Yes  | Parameters required for bundle uninstall.                      |
| callback   | AsyncCallback&lt;[InstallStatus](#installstatusdeprecated)&gt; | Yes  | Callback used to return the installation status.|

**Example**

```ts
import bundle from '@ohos.bundle';
let bundleName = 'com.example.myapplication';
let installParam = {
    userId: 100,
    isKeepData: false,
    installFlag: 1,
};

bundle.getBundleInstaller().then(installer => {
    installer.uninstall(bundleName, installParam, err => {
        if (err) {
            console.error('uninstall failed:' + JSON.stringify(err));
        } else {
            console.info('uninstall successfully.');
        }
    });
}).catch(error => {
    console.error('getBundleInstaller failed. Cause: ' + error.message);
});
```
## BundleInstaller.recover<sup>(deprecated)<sup>

> This API is deprecated since API version 9. You are advised to use [recover](js-apis-installer.md) instead.

recover(bundleName: string, param: InstallParam, callback: AsyncCallback&lt;InstallStatus&gt;): void;

Recovers a bundle. This API uses an asynchronous callback to return the result. After a pre-installed bundle is uninstalled, you can call this API to recover it.

**Required permissions**

ohos.permission.INSTALL_BUNDLE

**System capability**

SystemCapability.BundleManager.BundleFramework

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name    | Type                                                        | Mandatory| Description                                              |
| ---------- | ------------------------------------------------------------ | ---- | -------------------------------------------------- |
| bundleName | string                                                       | Yes  | Bundle name.                                  |
| param      | [InstallParam](#installparamdeprecated)                      | Yes  | Parameters required for bundle recovery.                      |
| callback   | AsyncCallback&lt;[InstallStatus](#installstatusdeprecated)&gt; | Yes  | Callback used to return the recovery status.|

**Example**

```ts
import bundle from '@ohos.bundle';

let bundleName = 'com.example.myapplication';
let installParam = {
    userId: 100,
    isKeepData: false,
    installFlag: 1,
};

bundle.getBundleInstaller().then(installer => {
    installer.recover(bundleName, installParam, err => {
        if (err) {
            console.error('recover failed:' + JSON.stringify(err));
        } else {
            console.info('recover successfully.');
        }
    });
}).catch(error => {
    console.error('getBundleInstaller failed. Cause: ' + error.message);
});
```

## InstallParam<sup>(deprecated)<sup>

Describes the parameters required for bundle installation, recovery, or uninstall.

**System capability**: SystemCapability.BundleManager.BundleFramework

**System API**: This is a system API and cannot be called by third-party applications.

| Name       | Type   | Readable| Writable| Description              |
| ----------- | ------- | ---- | ---- | ------------------ |
| userId      | number  | Yes  | Yes  | User ID. The default value is the user ID of the caller.|
| installFlag | number  | Yes  | Yes  | Installation flag.<br>**1** (default): overwrite installation.<br>**16**: installation-free.|
| isKeepData  | boolean | Yes  | Yes  | Whether data is kept. The default value is **false**.|

## InstallStatus<sup>(deprecated)<sup>

Describes the bundle installation or uninstall status.

**System capability**: SystemCapability.BundleManager.BundleFramework

**System API**: This is a system API and cannot be called by third-party applications.

| Name         | Type                                                        | Readable| Writable| Description                          |
| ------------- | ------------------------------------------------------------ | ---- | ---- | ------------------------------ |
| status        | bundle.[InstallErrorCode](js-apis-Bundle.md#installerrorcode) | Yes  | No  | Installation or uninstall error code. The value must be defined in [InstallErrorCode](js-apis-Bundle.md#installerrorcode)|
| statusMessage | string                                                       | Yes  | No  | Installation or uninstall status message.  <br>**SUCCESS**: install_succeed<br>**STATUS_INSTALL_FAILURE**: Installation failed (no installation file exists).<br>**STATUS_INSTALL_FAILURE_ABORTED**: Installation aborted.<br>**STATUS_INSTALL_FAILURE_INVALID**: Invalid installation parameter.<br>**STATUS_INSTALL_FAILURE_CONFLICT**: Installation conflict. (The basic information of the application to update is inconsistent with that of the existing application.)<br>**STATUS_INSTALL_FAILURE_STORAGE**: Failed to store the bundle information.<br>**STATUS_INSTALL_FAILURE_INCOMPATIBLE**: Installation incompatibility. (A downgrade occurs or the signature information is incorrect.)<br>**STATUS_UNINSTALL_FAILURE**: Uninstallation failed. (The application to be uninstalled is not found.)<br>**STATUS_UNINSTALL_FAILURE_ABORTED**: Uninstallation aborted. (This error code is not in use.)<br>**STATUS_UNINSTALL_FAILURE_ABORTED**: Uninstallation conflict. (Failed to uninstall a system application or end the application process.)<br>**STATUS_INSTALL_FAILURE_DOWNLOAD_TIMEOUT**: Installation failed. (Download timed out.)<br>**STATUS_INSTALL_FAILURE_DOWNLOAD_FAILED**: Installation failed. (Download failed.)<br>**STATUS_RECOVER_FAILURE_INVALID**: Failed to restore the pre-installed application.<br>**STATUS_ABILITY_NOT_FOUND**: Ability not found.<br>**STATUS_BMS_SERVICE_ERROR**: BMS service error.<br>**STATUS_FAILED_NO_SPACE_LEFT**: Insufficient device space.<br>**STATUS_GRANT_REQUEST_PERMISSIONS_FAILED**: Application authorization failed.<br>**STATUS_INSTALL_PERMISSION_DENIED**: No installation permission.<br>**STATUS_UNINSTALL_PERMISSION_DENIED**: No uninstallation permission. |

## Obtaining the Sandbox Path
For the FA model, the sandbox path of a bundle can be obtained using the APIs in [Context](js-apis-inner-app-context.md). For the stage model, the sandbox path can be obtained using the attribute in [Context](js-apis-inner-application-uiAbilityContext.md#abilitycontext). The following describes how to obtain the sandbox path.

**Example**
``` ts
// Stage model
import UIAbility from '@ohos.app.ability.UIAbility';
export default class EntryAbility extends UIAbility {
    onWindowStageCreate(windowStage) {
        let context = this.context;
        let pathDir = context.filesDir;
        console.info('sandbox path is ' + pathDir);
    }
}

// FA model
import featureAbility from '@ohos.ability.featureAbility';
let context = featureAbility.getContext();
context.getFilesDir().then((data) => {
    let pathDir = data;
    console.info('sandbox path is ' + pathDir);
});
```
