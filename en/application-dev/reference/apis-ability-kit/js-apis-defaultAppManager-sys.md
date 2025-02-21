# @ohos.bundle.defaultAppManager (Default Application Management) (System API)

The **DefaultAppManager** module provides APIs to query whether the current application is the default application of a specific type.

> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
> This topic describes only system APIs provided by the module. For details about its public APIs, see [@ohos.bundle.defaultAppManager](js-apis-defaultAppManager.md).

## Modules to Import

```ts
import defaultAppMgr from '@ohos.bundle.defaultAppManager';
```

## Required Permissions

| Permission                                   | APL   | Description            |
| --------------------------------------- | ----------- | ---------------- |
| ohos.permission.GET_DEFAULT_APPLICATION | system_core | Permission related to the default application.|

For details, see [Permission APL](../../security/AccessToken/app-permission-mgmt-overview.md#permission-apl).

## defaultAppMgr.getDefaultApplication

getDefaultApplication(type: string, userId?: number): Promise\<BundleInfo>

Obtains the default application based on a system-defined application type or a file type that complies with the media type format (either specified by **type** or **subtype**). This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework.DefaultApp

**System API**: This is a system API.

**Parameters**

| Name        | Type    | Mandatory  | Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type  | string | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](js-apis-defaultAppManager.md#defaultappmgrapplicationtype) or a file type that complies with the media type format.      |
| userId  | number | No   | User ID. The default value is the user ID of the caller.                        |

**Return value**

| Type                       | Description                |
| ------------------------- | ------------------ |
| Promise\<[BundleInfo](js-apis-bundle-BundleInfo.md)> | Promise used to return the default application.|

**Error codes**

For details about the error codes, see [Bundle Error Codes](errorcode-bundle.md).

| ID| Error Message                                 |
| -------- | ----------------------------------------- |
| 17700004 | The specified user ID is not found.       |
| 17700023 | The specified default app does not exist. |
| 17700025 | The specified type is invalid.            |

**Example**

```ts
import defaultAppMgr from '@ohos.bundle.defaultAppManager';
import { BusinessError } from '@ohos.base';

defaultAppMgr.getDefaultApplication(defaultAppMgr.ApplicationType.BROWSER)
  .then((data) => {
    console.info('Operation successful. bundleInfo: ' + JSON.stringify(data));
  })
  .catch((error: BusinessError) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
  });

defaultAppMgr.getDefaultApplication("image/png")
  .then((data) => {
    console.info('Operation successful. bundleInfo: ' + JSON.stringify(data));
  })
  .catch((error: BusinessError) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
  });
```

## defaultAppMgr.getDefaultApplication

getDefaultApplication(type: string, userId: number, callback: AsyncCallback\<BundleInfo>) : void

Obtains the default application of a user based on a system-defined application type or a file type that complies with the media type format (either specified by **type** or **subtype**). This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework.DefaultApp

**System API**: This is a system API.

**Parameters**

| Name        | Type    | Mandatory  | Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type  | string | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](js-apis-defaultAppManager.md#defaultappmgrapplicationtype) or a file type that complies with the media type format.      |
| userId  | number | Yes   | User ID.                          |
| callback    | AsyncCallback\<[BundleInfo](js-apis-bundle-BundleInfo.md)> | Yes   | Callback used to return the default application.                   |

**Error codes**

For details about the error codes, see [Bundle Error Codes](errorcode-bundle.md).

| ID| Error Message                                 |
| -------- | ----------------------------------------- |
| 17700004 | The specified user ID is not found.       |
| 17700023 | The specified default app does not exist. |
| 17700025 | The specified type is invalid.            |

**Example**

```ts
import defaultAppMgr from '@ohos.bundle.defaultAppManager';
import { BusinessError } from '@ohos.base';

let userId = 100;
defaultAppMgr.getDefaultApplication(defaultAppMgr.ApplicationType.BROWSER, userId, (err: BusinessError, data) => {
  if (err) {
    console.error('Operation failed. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Operation successful. bundleInfo:' + JSON.stringify(data));
});

defaultAppMgr.getDefaultApplication("image/png", userId, (err: BusinessError, data) => {
  if (err) {
    console.error('Operation failed. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Operation successful. bundleInfo:' + JSON.stringify(data));
});
```

## defaultAppMgr.getDefaultApplication

getDefaultApplication(type: string, callback: AsyncCallback\<BundleInfo>) : void

Obtains the default application based on a system-defined application type or a file type that complies with the media type format (either specified by **type** or **subtype**). This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework.DefaultApp

**System API**: This is a system API.

**Parameters**

| Name        | Type    | Mandatory  | Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type  | string | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](js-apis-defaultAppManager.md#defaultappmgrapplicationtype) or a file type that complies with the media type format.      |
| callback    | AsyncCallback\<[BundleInfo](js-apis-bundle-BundleInfo.md)> | Yes   | Callback used to return the default application.                   |

**Error codes**

For details about the error codes, see [Bundle Error Codes](errorcode-bundle.md).

| ID| Error Message                                 |
| -------- | ----------------------------------------- |
| 17700023 | The specified default app does not exist. |
| 17700025 | The specified type is invalid.            |

**Example**

```ts
import defaultAppMgr from '@ohos.bundle.defaultAppManager';
import { BusinessError } from '@ohos.base';

defaultAppMgr.getDefaultApplication(defaultAppMgr.ApplicationType.BROWSER, (err: BusinessError, data) => {
  if (err) {
    console.error('Operation failed. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Operation successful. bundleInfo:' + JSON.stringify(data));
});
defaultAppMgr.getDefaultApplication("image/png", (err: BusinessError, data) => {
  if (err) {
    console.error('Operation failed. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Operation successful. bundleInfo:' + JSON.stringify(data));
});
```

## defaultAppMgr.getDefaultApplicationSync<sup>10+</sup>

getDefaultApplicationSync(type: string, userId?: number): BundleInfo

Obtains the default application based on a system-defined application type or a file type that complies with the media type format (either specified by **type** or **subtype**). This API is a synchronous API.

**Required permissions**: ohos.permission.GET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework.DefaultApp

**System API**: This is a system API.

**Parameters**

| Name| Type  | Mandatory| Description                                   |
| -------| ------ | ---- | --------------------------------------- |
| type   | string | Yes  | Type of the target application. It must be set to a value defined by [ApplicationType](js-apis-defaultAppManager.md#defaultappmgrapplicationtype) or a file type that complies with the media type format.|
| userId | number | No  | User ID. The default value is the user ID of the caller.         |

**Return value**

| Type                                      | Description                |
| ------------------------------------------ | -------------------- |
| [BundleInfo](js-apis-bundle-BundleInfo.md) | Bundle information of the default application.|

**Error codes**

For details about the error codes, see [Bundle Error Codes](errorcode-bundle.md).

| ID| Error Message                                 |
| -------- | ----------------------------------------- |
| 17700004 | The specified user ID is not found.       |
| 17700023 | The specified default app does not exist. |
| 17700025 | The specified type is invalid.            |

**Example**

```ts
import defaultAppMgr from '@ohos.bundle.defaultAppManager';
try {
  let data = defaultAppMgr.getDefaultApplicationSync(defaultAppMgr.ApplicationType.BROWSER)
  console.info('Operation successful. bundleInfo: ' + JSON.stringify(data));
} catch(error) {
  console.error('Operation failed. Cause: ' + JSON.stringify(error));
};

try {
  let data = defaultAppMgr.getDefaultApplicationSync("image/png")
  console.info('Operation successful. bundleInfo: ' + JSON.stringify(data));
} catch(error) {
  console.error('Operation failed. Cause: ' + JSON.stringify(error));
};
```

## defaultAppMgr.setDefaultApplication

setDefaultApplication(type: string, elementName: ElementName, userId?: number): Promise\<void>

Sets the default application based on a system-defined application type or a file type that complies with the media type format (either specified by **type** or **subtype**). This API uses a promise to return the result.

**Required permissions**: ohos.permission.SET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework.DefaultApp

**System API**: This is a system API.

**Parameters**

| Name        | Type    | Mandatory  | Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type  | string | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](js-apis-defaultAppManager.md#defaultappmgrapplicationtype) or a file type that complies with the media type format.      |
| elementName  | [ElementName](js-apis-bundle-ElementName.md) | Yes   | Information about the element to be set as the default application.                          |
| userId  | number | No   | User ID. The default value is the user ID of the caller.                           |

**Return value**

| Type          | Description                              |
| -------------- | ---------------------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Bundle Error Codes](errorcode-bundle.md).

| ID| Error Message                                      |
| -------- | ---------------------------------------------- |
| 17700004 | The specified user ID is not found.            |
| 17700025 | The specified type is invalid.                 |
| 17700028 | The specified ability does not match the type. |

**Example**

```ts
import defaultAppMgr from '@ohos.bundle.defaultAppManager';
import { BusinessError } from '@ohos.base';

defaultAppMgr.setDefaultApplication(defaultAppMgr.ApplicationType.BROWSER, {
  bundleName: "com.example.myapplication",
  moduleName: "module01",
  abilityName: "EntryAbility"
}).then((data) => {
  console.info('Operation successful.');
}).catch((error: BusinessError) => {
  console.error('Operation failed. Cause: ' + JSON.stringify(error));
});

let userId = 100;
defaultAppMgr.setDefaultApplication(defaultAppMgr.ApplicationType.BROWSER, {
  bundleName: "com.example.myapplication",
  moduleName: "module01",
  abilityName: "EntryAbility"
}, userId).then((data) => {
  console.info('Operation successful.');
}).catch((error: BusinessError) => {
  console.error('Operation failed. Cause: ' + JSON.stringify(error));
});

defaultAppMgr.setDefaultApplication("image/png", {
  bundleName: "com.example.myapplication",
  moduleName: "module01",
  abilityName: "EntryAbility"
}, userId).then((data) => {
  console.info('Operation successful.');
}).catch((error: BusinessError) => {
  console.error('Operation failed. Cause: ' + JSON.stringify(error));
});
```

## defaultAppMgr.setDefaultApplication

setDefaultApplication(type: string, elementName: ElementName, userId: number, callback: AsyncCallback\<void>) : void

Sets the default application for a user based on a system-defined application type or a file type that complies with the media type format (either specified by **type** or **subtype**). This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.SET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework.DefaultApp

**System API**: This is a system API.

**Parameters**

| Name        | Type    | Mandatory  | Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type  | string | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](js-apis-defaultAppManager.md#defaultappmgrapplicationtype) or a file type that complies with the media type format.      |
| elementName  | [ElementName](js-apis-bundle-ElementName.md) | Yes   | Information about the element to be set as the default application.                          |
| userId  | number | Yes   | User ID.                          |
| callback    | AsyncCallback\<void> | Yes   | Callback used to return the result.                   |

**Error codes**

For details about the error codes, see [Bundle Error Codes](errorcode-bundle.md).

| ID| Error Message                                      |
| -------- | ---------------------------------------------- |
| 17700004 | The specified user ID is not found.            |
| 17700025 | The specified type is invalid.                 |
| 17700028 | The specified ability does not match the type. |

**Example**

```ts
import defaultAppMgr from '@ohos.bundle.defaultAppManager';
import { BusinessError } from '@ohos.base';

let userId = 100;
defaultAppMgr.setDefaultApplication(defaultAppMgr.ApplicationType.BROWSER, {
  bundleName: "com.example.myapplication",
  moduleName: "module01",
  abilityName: "EntryAbility"
}, userId, (err: BusinessError, data) => {
  if (err) {
    console.error('Operation failed. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Operation successful.');
});

defaultAppMgr.setDefaultApplication("image/png", {
  bundleName: "com.example.myapplication",
  moduleName: "module01",
  abilityName: "EntryAbility"
}, userId, (err: BusinessError, data) => {
  if (err) {
    console.error('Operation failed. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Operation successful.');
});
```

## defaultAppMgr.setDefaultApplication

setDefaultApplication(type: string, elementName: ElementName, callback: AsyncCallback\<void>) : void

Sets the default application based on a system-defined application type or a file type that complies with the media type format (either specified by **type** or **subtype**). This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.SET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework.DefaultApp

**System API**: This is a system API.

**Parameters**

| Name        | Type    | Mandatory  | Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type  | string | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](js-apis-defaultAppManager.md#defaultappmgrapplicationtype) or a file type that complies with the media type format.      |
| elementName  | [ElementName](js-apis-bundle-ElementName.md) | Yes   | Information about the element to be set as the default application.                          |
| callback    | AsyncCallback\<void> | Yes   | Callback used to return the result.                   |

**Error codes**

For details about the error codes, see [Bundle Error Codes](errorcode-bundle.md).

| ID| Error Message                                      |
| -------- | ---------------------------------------------- |
| 17700025 | The specified type is invalid.                 |
| 17700028 | The specified ability does not match the type. |

**Example**

```ts
import defaultAppMgr from '@ohos.bundle.defaultAppManager';
import { BusinessError } from '@ohos.base';

defaultAppMgr.setDefaultApplication(defaultAppMgr.ApplicationType.BROWSER, {
  bundleName: "com.example.myapplication",
  moduleName: "module01",
  abilityName: "EntryAbility"
}, (err: BusinessError, data) => {
  if (err) {
    console.error('Operation failed. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Operation successful.');
});

defaultAppMgr.setDefaultApplication("image/png", {
  bundleName: "com.example.myapplication",
  moduleName: "module01",
  abilityName: "EntryAbility"
}, (err: BusinessError, data) => {
  if (err) {
    console.error('Operation failed. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Operation successful.');
});
```

## defaultAppMgr.setDefaultApplicationSync<sup>10+</sup>

setDefaultApplicationSync(type: string, elementName: ElementName, userId?: number): void

Sets the default application based on the application type defined in the system or the file type that complies with the media type format (type/subtype). This API is a synchronous API.

**Required permissions**: ohos.permission.SET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework.DefaultApp

**System API**: This is a system API.

**Parameters**

| Name     | Type  | Mandatory| Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type        | string | Yes  | Type of the target application. It must be set to a value defined by [ApplicationType](js-apis-defaultAppManager.md#defaultappmgrapplicationtype) or a file type that complies with the media type format.|
| elementName | [ElementName](js-apis-bundle-ElementName.md) | Yes| Information about the element to be set as the default application.                          |
| userId      | number | No  | User ID. The default value is the user ID of the caller.                           |

**Error codes**

For details about the error codes, see [Bundle Error Codes](errorcode-bundle.md).

| ID| Error Message                                      |
| -------- | ---------------------------------------------- |
| 17700004 | The specified user ID is not found.            |
| 17700025 | The specified type is invalid.                 |
| 17700028 | The specified ability does not match the type. |

**Example**

```ts
import defaultAppMgr from '@ohos.bundle.defaultAppManager';
try {
  defaultAppMgr.setDefaultApplicationSync(defaultAppMgr.ApplicationType.BROWSER, {
  bundleName: "com.example.myapplication",
  moduleName: "module01",
  abilityName: "EntryAbility"
});
  console.info('Operation successful.');
} catch(error) {
  console.error('Operation failed. Cause: ' + JSON.stringify(error));
};

let userId = 100;
try {
  defaultAppMgr.setDefaultApplicationSync(defaultAppMgr.ApplicationType.BROWSER, {
  bundleName: "com.example.myapplication",
  moduleName: "module01",
  abilityName: "EntryAbility"
}, userId);
  console.info('Operation successful.');
} catch(error) {
  console.error('Operation failed. Cause: ' + JSON.stringify(error));
};

try {
  defaultAppMgr.setDefaultApplicationSync("image/png", {
  bundleName: "com.example.myapplication",
  moduleName: "module01",
  abilityName: "EntryAbility"
}, userId);
  console.info('Operation successful.');
} catch(error) {
  console.error('Operation failed. Cause: ' + JSON.stringify(error));
};
```

## defaultAppMgr.resetDefaultApplication

resetDefaultApplication(type: string, userId?: number): Promise\<void>

Resets the default application based on a system-defined application type or a file type that complies with the media type format (either specified by **type** or **subtype**). This API uses a promise to return the result.

**Required permissions**: ohos.permission.SET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework.DefaultApp

**System API**: This is a system API.

**Parameters**

| Name        | Type    | Mandatory  | Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type  | string | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](js-apis-defaultAppManager.md#defaultappmgrapplicationtype) or a file type that complies with the media type format.      |
| userId  | number | No   | User ID. The default value is the user ID of the caller.                           |

**Error codes**

For details about the error codes, see [Bundle Error Codes](errorcode-bundle.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 17700004 | The specified user ID is not found. |
| 17700025 | The specified type is invalid.      |

**Example**

```ts
import defaultAppMgr from '@ohos.bundle.defaultAppManager';
import { BusinessError } from '@ohos.base';

let userId = 100;
defaultAppMgr.resetDefaultApplication(defaultAppMgr.ApplicationType.BROWSER, userId)
  .then((data) => {
    console.info('Operation successful.');
  })
  .catch((error: BusinessError) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
  });

defaultAppMgr.resetDefaultApplication("image/png", userId)
  .then((data) => {
    console.info('Operation successful.');
  })
  .catch((error: BusinessError) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
  });
```

## defaultAppMgr.resetDefaultApplication

resetDefaultApplication(type: string, userId: number, callback: AsyncCallback\<void>) : void

Resets the default application for a user based on a system-defined application type or a file type that complies with the media type format (either specified by **type** or **subtype**). This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.SET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework.DefaultApp

**System API**: This is a system API.

**Parameters**

| Name        | Type    | Mandatory  | Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type  | string | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](js-apis-defaultAppManager.md#defaultappmgrapplicationtype) or a file type that complies with the media type format.      |
| userId  | number | Yes   | User ID.                         |
| callback    | AsyncCallback\<void> | Yes   | Callback used to return the result.                   |

**Error codes**

For details about the error codes, see [Bundle Error Codes](errorcode-bundle.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 17700004 | The specified user ID is not found. |
| 17700025 | The specified type is invalid.      |

**Example**

```ts
import defaultAppMgr from '@ohos.bundle.defaultAppManager';
import { BusinessError } from '@ohos.base';

let userId = 100;
defaultAppMgr.resetDefaultApplication(defaultAppMgr.ApplicationType.BROWSER, userId, (err: BusinessError, data) => {
  if (err) {
    console.error('Operation failed. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Operation successful.');
});

defaultAppMgr.resetDefaultApplication("image/png", userId, (err: BusinessError, data) => {
  if (err) {
    console.error('Operation failed. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Operation successful.');
});
```

## defaultAppMgr.resetDefaultApplication

resetDefaultApplication(type: string, callback: AsyncCallback\<void>) : void

Resets the default application based on a system-defined application type or a file type that complies with the media type format (either specified by **type** or **subtype**). This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.SET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework.DefaultApp

**System API**: This is a system API.

**Parameters**

| Name        | Type    | Mandatory  | Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type  | string | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](js-apis-defaultAppManager.md#defaultappmgrapplicationtype) or a file type that complies with the media type format.      |
| callback    | AsyncCallback\<void> | Yes   | Callback used to return the result.                   |

**Error codes**

For details about the error codes, see [Bundle Error Codes](errorcode-bundle.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 17700025 | The specified type is invalid.      |

**Example**

```ts
import defaultAppMgr from '@ohos.bundle.defaultAppManager';
import { BusinessError } from '@ohos.base';

defaultAppMgr.resetDefaultApplication(defaultAppMgr.ApplicationType.BROWSER, (err: BusinessError, data) => {
  if (err) {
    console.error('Operation failed. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Operation successful.');
});

defaultAppMgr.resetDefaultApplication("image/png", (err: BusinessError, data) => {
  if (err) {
    console.error('Operation failed. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Operation successful.');
});
```

## defaultAppMgr.resetDefaultApplicationSync<sup>10+</sup>

resetDefaultApplicationSync(type: string, userId?: number): void

Resets the default application based on the application type defined in the system or the file type that complies with the media type format (type/subtype). This API is a synchronous API.

**Required permissions**: ohos.permission.SET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework.DefaultApp

**System API**: This is a system API.

**Parameters**

| Name| Type  | Mandatory| Description                                   |
| ------ | ------ | ---- | --------------------------------------- |
| type   | string | Yes  | Type of the target application. It must be set to a value defined by [ApplicationType](js-apis-defaultAppManager.md#defaultappmgrapplicationtype) or a file type that complies with the media type format.|
| userId | number | No  | User ID. The default value is the user ID of the caller.                           |

**Error codes**

For details about the error codes, see [Bundle Error Codes](errorcode-bundle.md).

| ID| Error Message                           |
| -------- | ----------------------------------- |
| 17700004 | The specified user ID is not found. |
| 17700025 | The specified type is invalid.      |

**Example**

```ts
import defaultAppMgr from '@ohos.bundle.defaultAppManager';

let userId = 100;
try {
  defaultAppMgr.resetDefaultApplicationSync(defaultAppMgr.ApplicationType.BROWSER, userId);
  console.info('Operation successful.');
} catch(error) {
  console.error('Operation failed. Cause: ' + JSON.stringify(error));
};

try {
  defaultAppMgr.resetDefaultApplicationSync("image/png", userId);
  console.info('Operation successful.');
} catch(error) {
  console.error('Operation failed. Cause: ' + JSON.stringify(error));
};
```
