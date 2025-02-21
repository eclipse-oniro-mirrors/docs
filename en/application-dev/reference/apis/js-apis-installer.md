# @ohos.bundle.installer (installer)

The **bundle.installer** module provides APIs for you to install, uninstall, and recover bundles on devices.

> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```js
import installer from '@ohos.bundle.installer';
```

## Required Permissions

| Permission                          | Permission Level   | Description            |
| ------------------------------ | ----------- | ---------------- |
| ohos.permission.INSTALL_BUNDLE | system_core | Permission to install or uninstall bundles.|

For details, see [Permission Levels](../../security/accesstoken-overview.md#permission-levels).

## BundleInstaller.getBundleInstaller

getBundleInstaller(callback: AsyncCallback\<BundleInstaller>): void

Obtains a **BundleInstaller** object. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.BundleManager.BundleFramework.Core

**Parameters**

| Name  | Type                                                        | Mandatory| Description                                                        |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback\<BundleInstaller> | Yes  | Callback used to return the result. If the operation is successful, **err** is **null** and **data** is the **BundleInstaller** object obtained; otherwise, **err** is an error object.|

**Example**

```ts
import installer from '@ohos.bundle.installer';

try {
    installer.getBundleInstaller((err, data) => {
        if (err) {
            console.error('getBundleInstaller failed:' + err.message);
        } else {
            console.info('getBundleInstaller successfully');
        }
    });
} catch (error) {
    console.error('getBundleInstaller failed:' + error.message);
}
```

## BundleInstaller.getBundleInstaller

getBundleInstaller(): Promise\<BundleInstaller>

Obtains a **BundleInstaller** object. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.BundleManager.BundleFramework.Core

**Return value**
| Type                                                        | Description                                |
| ------------------------------------------------------------ | ------------------------------------ |
| Promise\<BundleInstaller> | Promise used to return the **BundleInstaller** object obtained.|

**Example**

```ts
import installer from '@ohos.bundle.installer';

try {
    installer.getBundleInstaller().then((data) => {
        console.info('getBundleInstaller successfully.');
    }).catch((error) => {
        console.error('getBundleInstaller failed. Cause: ' + error.message);
    });
} catch (error) {
    console.error('getBundleInstaller failed. Cause: ' + error.message);
}
```

## BundleInstaller.install
install(hapFilePaths: Array&lt;string&gt;, installParam: InstallParam, callback: AsyncCallback&lt;void&gt;): void

Installs a bundle. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.INSTALL_BUNDLE

**System capability**: SystemCapability.BundleManager.BundleFramework.Core

**Parameters**

| Name          | Type                                                | Mandatory| Description                                                        |
| --------------- | ---------------------------------------------------- | ---- | ------------------------------------------------------------ |
| hapFilePaths | Array&lt;string&gt;                                  | Yes  | Paths where the HAP files of the bundle are stored, which are the data directories. If only one directory is passed, the HAP files in the directory must belong to the same bundle and have the same signature.|
| installParam           | [InstallParam](#installparam)                        | Yes  | Parameters required for the installation.                                    |
| callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result. If the operation is successful, **err** is **null**; otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Bundle Error Codes](../errorcodes/errorcode-bundle.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17700004 | The specified user ID is not found.                          |
| 17700010 | Failed to install the HAP because the HAP fails to be parsed. |
| 17700011 | Failed to install the HAP because the HAP signature fails to be verified. |
| 17700012 | Failed to install the HAP because the HAP path is invalid or the HAP is too large. |
| 17700015 | Failed to install the HAPs because they have different configuration information. |
| 17700016 | Failed to install the HAP because of insufficient system disk space. |
| 17700017 | Failed to install the HAP since the version of the HAP to install is too early. |
| 17700018 | Failed to install because the dependent module does not exist. |

**Example**

```ts
import installer from '@ohos.bundle.installer';
let hapFilePaths = ['/data/storage/el2/base/haps/entry/files/'];
let installParam = {
    userId: 100,
    isKeepData: false,
    installFlag: 1,
};

try {
    installer.getBundleInstaller().then(data => {
        data.install(hapFilePaths, installParam, err => {
            if (err) {
                console.error('install failed:' + err.message);
            } else {
                console.info('install successfully.');
            }
        });
    }).catch(error => {
        console.error('getBundleInstaller failed. Cause: ' + error.message);
    });
} catch (error) {
    console.error('getBundleInstaller failed. Cause: ' + error.message);
}
```

## BundleInstaller.install

install(hapFilePaths: Array\<string\>, installParam?: InstallParam) : Promise\<void\>

Installs a bundle. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.INSTALL_BUNDLE

**System capability**: SystemCapability.BundleManager.BundleFramework.Core

**Parameters**

| Name      | Type                         | Mandatory| Description                                                        |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| hapFilePaths | Array\<string\>               | Yes  | Paths where the HAP files of the bundle are stored, which are the data directories. If only one directory is passed, the HAP files in the directory must belong to the same bundle and have the same signature.|
| installParam | [InstallParam](#installparam) | No  | Parameters required for the installation.                                    |

**Return value**

| Type           | Description                                  |
| --------------- | -------------------------------------- |
| Promise\<void\> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Bundle Error Codes](../errorcodes/errorcode-bundle.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17700004 | The specified user ID is not found.                          |
| 17700010 | Failed to install the HAP because the HAP fails to be parsed. |
| 17700011 | Failed to install the HAP because the HAP signature fails to be verified. |
| 17700012 | Failed to install the HAP because the HAP path is invalid or the HAP is too large. |
| 17700015 | Failed to install the HAPs because they have different configuration information. |
| 17700016 | Failed to install the HAP because of insufficient system disk space. |
| 17700017 | Failed to install the HAP since the version of the HAP to install is too early. |
| 17700018 | Failed to install because the dependent module does not exist. |

**Example**

```ts
import installer from '@ohos.bundle.installer';
let hapFilePaths = ['/data/storage/el2/base/haps/entry/files/'];
let installParam = {
    userId: 100,
    isKeepData: false,
    installFlag: 1,
};

try {
    installer.getBundleInstaller().then(data => {
        data.install(hapFilePaths, installParam)
            .then((data) => {
                console.info('install successfully: ' + JSON.stringify(data));
        }).catch((error) => {
            console.error('install failed:' + error.message);
        });
    }).catch(error => {
        console.error('getBundleInstaller failed. Cause: ' + error.message);
    });
} catch (error) {
    console.error('getBundleInstaller failed. Cause: ' + error.message);
}
```

## BundleInstaller.uninstall

uninstall(bundleName: string, installParam: InstallParam, callback: AsyncCallback&lt;void&gt;): void

Uninstalls a bundle. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.INSTALL_BUNDLE

**System capability**: SystemCapability.BundleManager.BundleFramework.Core

**Parameters**

| Name     | Type                                                | Mandatory| Description                                          |
| ---------- | ---------------------------------------------------- | ---- | ---------------------------------------------- |
| bundleName | string                                               | Yes  | Name of the target bundle.                                          |
| installParam      | [InstallParam](#installparam)                        | Yes  | Parameters required for the uninstall.                      |
| callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result. If the operation is successful, **err** is **null**; otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Bundle Error Codes](../errorcodes/errorcode-bundle.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17700001 | The specified bundle name is not found. |
| 17700004 | The specified user ID is not found.                          |
| 17700020 | The specified bundle is pre-installed bundle which cannot be uninstalled. |

**Example**

```ts
import installer from '@ohos.bundle.installer';
let bundleName = 'com.ohos.demo';
let installParam = {
    userId: 100,
    isKeepData: false,
    installFlag: 1
};

try {
    installer.getBundleInstaller().then(data => {
        data.uninstall(bundleName, installParam, err => {
            if (err) {
                console.error('uninstall failed:' + err.message);
            } else {
                console.info('uninstall successfully.');
            }
        });
    }).catch(error => {
        console.error('getBundleInstaller failed. Cause: ' + error.message);
    });
} catch (error) {
    console.error('getBundleInstaller failed. Cause: ' + error.message);
}
```
## BundleInstaller.uninstall

uninstall(bundleName: string, installParam?: InstallParam) : Promise\<void\>

Uninstalls a bundle. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.INSTALL_BUNDLE

**System capability**: SystemCapability.BundleManager.BundleFramework.Core

**Parameters**

| Name      | Type                         | Mandatory| Description                                                        |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| bundleName | string                          | Yes  | Name of the target bundle.                                          |
| installParam | [InstallParam](#installparam) | No  | Parameters required for the uninstall.                                    |

**Return value**

| Type           | Description                                  |
| --------------- | -------------------------------------- |
| Promise\<void\> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Bundle Error Codes](../errorcodes/errorcode-bundle.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 17700001 | The specified bundle name is not found. |
| 17700004 | The specified user ID is not found.                          |
| 17700020 | The specified bundle is pre-installed bundle which cannot be uninstalled. |

**Example**
```ts
import installer from '@ohos.bundle.installer';
let bundleName = 'com.ohos.demo';
let installParam = {
    userId: 100,
    isKeepData: false,
    installFlag: 1,
};

try {
    installer.getBundleInstaller().then(data => {
        data.uninstall(bundleName, installParam)
            .then((data) => {
                console.info('uninstall successfully: ' + JSON.stringify(data));
        }).catch((error) => {
            console.error('uninstall failed:' + error.message);
        });
    }).catch(error => {
        console.error('getBundleInstaller failed. Cause: ' + error.message);
    });
} catch (error) {
    console.error('getBundleInstaller failed. Cause: ' + error.message);
}
```

## BundleInstaller.recover

recover(bundleName: string, installParam: InstallParam, callback: AsyncCallback&lt;void&gt;): void

Rolls back a bundle to the initial installation state. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.INSTALL_BUNDLE

**System capability**: SystemCapability.BundleManager.BundleFramework.Core

**Parameters**

| Name     | Type                                                | Mandatory| Description                                          |
| ---------- | ---------------------------------------------------- | ---- | ---------------------------------------------- |
| bundleName | string                                               | Yes  | Name of the target bundle.                                          |
| installParam      | [InstallParam](#installparam)                        | Yes  | Parameters required for the recovery.                      |
| callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result. If the operation is successful, **err** is **null**; otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Bundle Error Codes](../errorcodes/errorcode-bundle.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 17700001 | The specified bundle name is not found. |
| 17700004 | The specified user ID is not found. |

**Example**

```ts
import installer from '@ohos.bundle.installer';
let bundleName = 'com.ohos.demo';
let installParam = {
    userId: 100,
    isKeepData: false,
    installFlag: 1
};

try {
    installer.getBundleInstaller().then(data => {
        data.recover(bundleName, installParam, err => {
            if (err) {
                console.error('recover failed:' + err.message);
            } else {
                console.info('recover successfully.');
            }
        });
    }).catch(error => {
        console.error('getBundleInstaller failed. Cause: ' + error.message);
    });
} catch (error) {
    console.error('getBundleInstaller failed. Cause: ' + error.message);
}
```
## BundleInstaller.recover

recover(bundleName: string, installParam?: InstallParam) : Promise\<void\>

Rolls back a bundle to the initial installation state. This API uses a promise to return the result.

**System API**: This is a system API.

**Required permissions**: ohos.permission.INSTALL_BUNDLE

**System capability**: SystemCapability.BundleManager.BundleFramework.Core

**Parameters**

| Name      | Type                         | Mandatory| Description                                                        |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| bundleName | string                          | Yes  | Name of the target bundle.                                          |
| installParam | [InstallParam](#installparam) | No  | Parameters required for the recovery.                                    |

**Return value**

| Type           | Description                                  |
| --------------- | -------------------------------------- |
| Promise\<void\> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Bundle Error Codes](../errorcodes/errorcode-bundle.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 17700001 | The specified bundle name is not found. |
| 17700004 | The specified user ID is not found. |

**Example**
```ts
import installer from '@ohos.bundle.installer';
let bundleName = 'com.ohos.demo';
let installParam = {
    userId: 100,
    isKeepData: false,
    installFlag: 1,
};

try {
    installer.getBundleInstaller().then(data => {
        data.recover(bundleName, installParam)
            .then((data) => {
                console.info('recover successfully: ' + JSON.stringify(data));
        }).catch((error) => {
            console.error('recover failed:' + error.message);
        });
    }).catch(error => {
        console.error('getBundleInstaller failed. Cause: ' + error.message);
    });
} catch (error) {
    console.error('getBundleInstaller failed. Cause: ' + error.message);
}
```
## HashParam

Defines the hash parameters for bundle installation and uninstall.

 **System capability**: SystemCapability.BundleManager.BundleFramework.Core

 **System API**: This is a system API.

| Name    | Type  | Mandatory| Description            |
| ---------- | ------ | ---------------- | ---------------- |
| moduleName | string | Yes| Module name of the bundle.|
| hashValue  | string | Yes| Hash value.          |

## InstallParam

Defines the parameters that need to be specified for bundle installation, uninstall, or recovering.

 **System capability**: SystemCapability.BundleManager.BundleFramework.Core

 **System API**: This is a system API.

| Name                       | Type                          | Mandatory                        | Description              |
| ------------------------------ | ------------------------------ | ------------------ | ------------------ |
| userId                         | number                         | No                       | User ID. You can use [queryOsAccountLocalIdFromProcess](js-apis-osAccount.md#getOsAccountLocalId) to obtain the user of the current process.|
| installFlag                    | number                         | No                       | Installation flag. The value **0x00** means initial installation, **0x01** means overwrite installation, and **0x10** means installation-free. The default value is **0x00**.|
| isKeepData                     | boolean                        | No                      | Whether to retain the data directory during bundle uninstall.|
| hashParams        | Array<[HashParam](#hashparam)> | No| Hash parameters.        |
| crowdtestDeadline| number                         | No                       | End date of crowdtesting. The default value is **-1**, indicating that no end date is specified for crowdtesting.|
