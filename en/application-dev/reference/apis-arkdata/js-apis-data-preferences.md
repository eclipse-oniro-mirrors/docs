# @ohos.data.preferences (User Preferences)

The **Preferences** module provides APIs for processing data in the form of key-value (KV) pairs, including querying, modifying, and persisting KV pairs.

The key is of the string type, and the value can be a number, a string, a Boolean value, or an array of numbers, strings, or Boolean values.


> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```ts
import dataPreferences from '@ohos.data.preferences';
```

## Constants

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

| Name            | Type| Readable| Writable| Description                                   |
| ---------------- | -------- | ---- | ---- | --------------------------------------- |
| MAX_KEY_LENGTH   | number   | Yes  | No  | Maximum length of a key, which is 80 bytes.    |
| MAX_VALUE_LENGTH | number   | Yes  | No  | Maximum length of a value, which is 8192 bytes.|


## dataPreferences.getPreferences

getPreferences(context: Context, name: string, callback: AsyncCallback&lt;Preferences&gt;): void

Obtains a **Preferences** instance. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name  | Type                                            | Mandatory| Description                                                        |
| -------- | ------------------------------------------------ | ---- | ------------------------------------------------------------ |
| context  | Context            | Yes  | Application context.<br>For details about the application context of the FA model, see [Context](../apis-ability-kit/js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md).                                                |
| name     | string                                           | Yes  | Name of the **Preferences** instance.                                     |
| callback | AsyncCallback&lt;[Preferences](#preferences)&gt; | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined** and the **Preferences** instance obtained is returned. Otherwise, **err** is an error object.|

**Example**

FA model:

```ts
import featureAbility from '@ohos.ability.featureAbility';
import { BusinessError } from '@ohos.base';

let context = featureAbility.getContext();
let preferences: dataPreferences.Preferences | null = null;

dataPreferences.getPreferences(context, 'myStore', (err: BusinessError, val: dataPreferences.Preferences) => {
  if (err) {
    console.error("Failed to get preferences. code =" + err.code + ", message =" + err.message);
    return;
  }
  preferences = val;
  console.info("Succeeded in getting preferences.");
})
```

Stage model:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import { BusinessError } from '@ohos.base';
import window from '@ohos.window';

let preferences: dataPreferences.Preferences | null = null;

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    dataPreferences.getPreferences(this.context, 'myStore', (err: BusinessError, val: dataPreferences.Preferences) => {
      if (err) {
        console.error("Failed to get preferences. code =" + err.code + ", message =" + err.message);
        return;
      }
      preferences = val;
      console.info("Succeeded in getting preferences.");
    })
  }
}
```

## dataPreferences.getPreferences

getPreferences(context: Context, name: string): Promise&lt;Preferences&gt;

Obtains a **Preferences** instance. This API uses a promise to return the result.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name | Type                                 | Mandatory| Description                   |
| ------- | ------------------------------------- | ---- | ----------------------- |
| context | Context | Yes  | Application context.<br>For details about the application context of the FA model, see [Context](../apis-ability-kit/js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md).           |
| name    | string                                | Yes  | Name of the **Preferences** instance.|

**Return value**

| Type                                      | Description                              |
| ------------------------------------------ | ---------------------------------- |
| Promise&lt;[Preferences](#preferences)&gt; | Promise used to return the **Preferences** instance obtained.|

**Example**

FA model:

```ts
// Obtain the context.
import featureAbility from '@ohos.ability.featureAbility';
import { BusinessError } from '@ohos.base'

let context = featureAbility.getContext();

let preferences: dataPreferences.Preferences | null = null;
let promise = dataPreferences.getPreferences(context, 'myStore');
promise.then((object: dataPreferences.Preferences) => {
  preferences = object;
  console.info("Succeeded in getting preferences.");
}).catch((err: BusinessError) => {
  console.error("Failed to get preferences. code =" + err.code + ", message =" + err.message);
})
```

Stage model:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import { BusinessError } from '@ohos.base'
import window from '@ohos.window';

let preferences: dataPreferences.Preferences | null = null;

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    let promise = dataPreferences.getPreferences(this.context, 'myStore');
    promise.then((object: dataPreferences.Preferences) => {
      preferences = object;
      console.info("Succeeded in getting preferences.");
    }).catch((err: BusinessError) => {
      console.error("Failed to get preferences. code =" + err.code + ", message =" + err.message);
    })
  }
}
```

## dataPreferences.getPreferences<sup>10+</sup>

getPreferences(context: Context, options: Options, callback: AsyncCallback&lt;Preferences&gt;): void

Obtains a **Preferences** instance. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name  | Type                                         | Mandatory| Description                                                                                                                                                                          |
| -------- | --------------------------------------------- | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| context  | Context                                       | Yes  | Application context.<br>For details about the application context of the FA model, see [Context](../apis-ability-kit/js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md).|
| options  | [Options](#options10)                              | Yes  | Configuration options of the **Preferences** instance.                                                                                                                                             |
| callback | AsyncCallback&lt;[Preferences](#preferences)&gt; | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined** and the **Preferences** instance obtained is returned. Otherwise, **err** is an error object.                                                                                   |

**Error codes**

For details about the error codes, see [User Preference Error Codes](errorcode-preferences.md).

| ID| Error Message                      |
| -------- | ------------------------------ |
| 15501001 | Only supported in stage mode. |
| 15501002 | The data group id is not valid.     |

**Example**

FA model:

```ts
// Obtain the context.
import featureAbility from '@ohos.ability.featureAbility';
import { BusinessError } from '@ohos.base'

let context = featureAbility.getContext();
let preferences: dataPreferences.Preferences | null = null;

let options: dataPreferences.Options = { name: 'myStore' };
dataPreferences.getPreferences(context, options, (err: BusinessError, val: dataPreferences.Preferences) => {
  if (err) {
    console.error("Failed to get preferences. code =" + err.code + ", message =" + err.message);
    return;
  }
  preferences = val;
  console.info("Succeeded in getting preferences.");
})
```


Stage model:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import { BusinessError } from '@ohos.base'
import window from '@ohos.window';

let preferences: dataPreferences.Preferences | null = null;

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    let options: dataPreferences.Options = { name: 'myStore', dataGroupId: 'myId' };
    dataPreferences.getPreferences(this.context, options, (err: BusinessError, val: dataPreferences.Preferences) => {
      if (err) {
        console.error("Failed to get preferences. code =" + err.code + ", message =" + err.message);
        return;
      }
      preferences = val;
      console.info("Succeeded in getting preferences.");
    })
  }
}
```

## dataPreferences.getPreferences<sup>10+</sup>

getPreferences(context: Context, options: Options): Promise&lt;Preferences&gt;

Obtains a **Preferences** instance. This API uses a promise to return the result.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name | Type            | Mandatory| Description                                                                                                                                                                          |
| ------- | ---------------- | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| context | Context          | Yes  | Application context.<br>For details about the application context of the FA model, see [Context](../apis-ability-kit/js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md).|
| options | [Options](#options10) | Yes  | Configuration options of the **Preferences** instance.                                                                                                                                             |

**Return value**

| Type                                   | Description                              |
| --------------------------------------- | ---------------------------------- |
| Promise&lt;[Preferences](#preferences)&gt; | Promise used to return the **Preferences** instance obtained.|

**Error codes**

For details about the error codes, see [User Preference Error Codes](errorcode-preferences.md).

| ID| Error Message                      |
| -------- | ------------------------------ |
| 15501001 | Only supported in stage mode. |
| 15501002 | The data group id is not valid.     |

**Example**

FA model:

```ts
// Obtain the context.
import featureAbility from '@ohos.ability.featureAbility';
import { BusinessError } from '@ohos.base'

let context = featureAbility.getContext();

let preferences: dataPreferences.Preferences | null = null;
let options: dataPreferences.Options = { name: 'myStore' };
let promise = dataPreferences.getPreferences(context, options);
promise.then((object: dataPreferences.Preferences) => {
  preferences = object;
  console.info("Succeeded in getting preferences.");
}).catch((err: BusinessError) => {
  console.error("Failed to get preferences. code =" + err.code + ", message =" + err.message);
})
```

Stage model:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import { BusinessError } from '@ohos.base'
import window from '@ohos.window';

let preferences: dataPreferences.Preferences | null = null;

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    let options: dataPreferences.Options = { name: 'myStore', dataGroupId: 'myId' };
    let promise = dataPreferences.getPreferences(this.context, options);
    promise.then((object: dataPreferences.Preferences) => {
      preferences = object;
      console.info("Succeeded in getting preferences.");
    }).catch((err: BusinessError) => {
      console.error("Failed to get preferences. code =" + err.code + ", message =" + err.message);
    })
  }
}
```

## dataPreferences.getPreferencesSync<sup>10+</sup>

getPreferencesSync(context: Context, options: Options): Preferences

Obtains a **Preferences** instance. This API returns the result synchronously.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name | Type                 | Mandatory| Description                                                        |
| ------- | --------------------- | ---- | ------------------------------------------------------------ |
| context | Context               | Yes  | Application context.<br>For details about the application context of the FA model, see [Context](../apis-ability-kit/js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md).|
| options | [Options](#options10) | Yes  | Configuration options of the **Preferences** instance.                           |

**Return value**

| Type                       | Description                 |
| --------------------------- | --------------------- |
| [Preferences](#preferences) | **Preferences** instance obtained.|

**Error codes**

For details about the error codes, see [User Preference Error Codes](errorcode-preferences.md).

| ID| Error Message                       |
| -------- | ------------------------------- |
| 15501001 | Only supported in stage mode.   |
| 15501002 | The data group id is not valid. |

**Example**

FA model:

```ts
// Obtain the context.
import featureAbility from '@ohos.ability.featureAbility';

let context = featureAbility.getContext();
let preferences: dataPreferences.Preferences | null = null;

let options: dataPreferences.Options = { name: 'myStore' };
preferences = dataPreferences.getPreferencesSync(context, options);
```

Stage model:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';

let preferences: dataPreferences.Preferences | null = null;

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    let options: dataPreferences.Options = { name: 'myStore', dataGroupId: 'myId' };
    preferences = dataPreferences.getPreferencesSync(this.context, options);
  }
}
```

## dataPreferences.deletePreferences

deletePreferences(context: Context, name: string, callback: AsyncCallback&lt;void&gt;): void

Deletes a **Preferences** instance from the cache. If the **Preferences** instance has a persistent file, the persistent file will also be deleted. This API uses an asynchronous callback to return the result.

Avoid using a deleted **Preferences** instance to perform data operations, which may cause data inconsistency. Instead, set the deleted **Preferences** instance to null. The system will reclaim them in a unified manner.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name  | Type                                 | Mandatory| Description                                                |
| -------- | ------------------------------------- | ---- | ---------------------------------------------------- |
| context  | Context | Yes  | Application context.<br>For details about the application context of the FA model, see [Context](../apis-ability-kit/js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md).                                        |
| name     | string                                | Yes  | Name of the **Preferences** instance.                             |
| callback | AsyncCallback&lt;void&gt;             | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [User Preference Error Codes](errorcode-preferences.md).

| ID| Error Message                      |
| -------- | ------------------------------|
| 15500010 | Failed to delete preferences file. |

**Example**

FA model:

```ts
// Obtain the context.
import featureAbility from '@ohos.ability.featureAbility';
import { BusinessError } from '@ohos.base'

let context = featureAbility.getContext();

dataPreferences.deletePreferences(context, 'myStore', (err: BusinessError) => {
  if (err) {
    console.error("Failed to delete preferences. code =" + err.code + ", message =" + err.message);
    return;
  }
  console.info("Succeeded in deleting preferences.");
})
```

Stage model:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import { BusinessError } from '@ohos.base'
import window from '@ohos.window';

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    dataPreferences.deletePreferences(this.context, 'myStore', (err: BusinessError) => {
      if (err) {
        console.error("Failed to delete preferences. code =" + err.code + ", message =" + err.message);
        return;
      }
      console.info("Succeeded in deleting preferences.");
    })
  }
}
```

## dataPreferences.deletePreferences

deletePreferences(context: Context, name: string): Promise&lt;void&gt;

Deletes a **Preferences** instance from the cache. If the **Preferences** instance has a persistent file, the persistent file will also be deleted. This API uses a promise to return the result.

Avoid using a deleted **Preferences** instance to perform data operations, which may cause data inconsistency. Instead, set the deleted **Preferences** instance to null. The system will reclaim them in a unified manner.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name | Type                                 | Mandatory| Description                   |
| ------- | ------------------------------------- | ---- | ----------------------- |
| context | Context | Yes  | Application context.<br>For details about the application context of the FA model, see [Context](../apis-ability-kit/js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md).           |
| name    | string                                | Yes  | Name of the **Preferences** instance.|

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [User Preference Error Codes](errorcode-preferences.md).

| ID| Error Message                      |
| -------- | ------------------------------|
| 15500010 | Failed to delete preferences file. |

**Example**

FA model:

```ts
// Obtain the context.
import featureAbility from '@ohos.ability.featureAbility';
import { BusinessError } from '@ohos.base'

let context = featureAbility.getContext();

let promise = dataPreferences.deletePreferences(context, 'myStore');
promise.then(() => {
  console.info("Succeeded in deleting preferences.");
}).catch((err: BusinessError) => {
  console.error("Failed to delete preferences. code =" + err.code + ", message =" + err.message);
})
```

Stage model:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import { BusinessError } from '@ohos.base'
import window from '@ohos.window';

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    let promise = dataPreferences.deletePreferences(this.context, 'myStore');
    promise.then(() => {
      console.info("Succeeded in deleting preferences.");
    }).catch((err: BusinessError) => {
      console.error("Failed to delete preferences. code =" + err.code + ", message =" + err.message);
    })
  }
}
```

## dataPreferences.deletePreferences<sup>10+</sup>

deletePreferences(context: Context, options: Options, callback: AsyncCallback&lt;void&gt;): void

Deletes a **Preferences** instance from the cache. If the **Preferences** instance has a persistent file, the persistent file will also be deleted. This API uses an asynchronous callback to return the result.

Avoid using a deleted **Preferences** instance to perform data operations, which may cause data inconsistency. Instead, set the deleted **Preferences** instance to null. The system will reclaim them in a unified manner.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name  | Type                     | Mandatory| Description                                                                                                                                                                          |
| -------- | ------------------------- | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| context  | Context                   | Yes  | Application context.<br>For details about the application context of the FA model, see [Context](../apis-ability-kit/js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md).|
| options  | [Options](#options10)          | Yes  | Configuration options of the **Preferences** instance.                                                                                                                                             |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**. Otherwise, **err** is an error object.                                                                                                                          |

**Error codes**

For details about the error codes, see [User Preference Error Codes](errorcode-preferences.md).

| ID| Error Message                          |
| -------- | ---------------------------------- |
| 15500010 | Failed to delete preferences file. |
| 15501001 | Only supported in stage mode. |
| 15501002 | The data group id is not valid. |

**Example**

FA model:

```ts
// Obtain the context.
import featureAbility from '@ohos.ability.featureAbility';
import { BusinessError } from '@ohos.base'

let context = featureAbility.getContext();

let options: dataPreferences.Options = { name: 'myStore' };
dataPreferences.deletePreferences(context, options, (err: BusinessError) => {
  if (err) {
    console.error("Failed to delete preferences. code =" + err.code + ", message =" + err.message);
    return;
  }
  console.info("Succeeded in deleting preferences.");
})
```

Stage model:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import { BusinessError } from '@ohos.base'
import window from '@ohos.window';

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    let options: dataPreferences.Options = { name: 'myStore', dataGroupId: 'myId' };
    dataPreferences.deletePreferences(this.context, options, (err: BusinessError) => {
      if (err) {
        console.error("Failed to delete preferences. code =" + err.code + ", message =" + err.message);
        return;
      }
      console.info("Succeeded in deleting preferences.");
    })
  }
}
```


## dataPreferences.deletePreferences<sup>10+</sup>

deletePreferences(context: Context, options: Options): Promise&lt;void&gt;

Deletes a **Preferences** instance from the cache. If the **Preferences** instance has a persistent file, the persistent file will also be deleted. This API uses a promise to return the result.

Avoid using a deleted **Preferences** instance to perform data operations, which may cause data inconsistency. Instead, set the deleted **Preferences** instance to null. The system will reclaim them in a unified manner.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name | Type            | Mandatory| Description                                                                                                                                                                          |
| ------- | ---------------- | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| context | Context          | Yes  | Application context.<br>For details about the application context of the FA model, see [Context](../apis-ability-kit/js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md).|
| options | [Options](#options10) | Yes  | Configuration options of the **Preferences** instance.                                                                                                                                             |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [User Preference Error Codes](errorcode-preferences.md).

| ID| Error Message                          |
| -------- | ---------------------------------- |
| 15500010 | Failed to delete preferences file. |
| 15501001 | Only supported in stage mode. |
| 15501002 | The data group id is not valid. |

**Example**

FA model:

```ts
// Obtain the context.
import featureAbility from '@ohos.ability.featureAbility';
import { BusinessError } from '@ohos.base'

let context = featureAbility.getContext();

let options: dataPreferences.Options = { name: 'myStore' };
let promise = dataPreferences.deletePreferences(context, options);
promise.then(() => {
  console.info("Succeeded in deleting preferences.");
}).catch((err: BusinessError) => {
  console.error("Failed to delete preferences. code =" + err.code + ", message =" + err.message);
})
```

Stage model:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import { BusinessError } from '@ohos.base'
import window from '@ohos.window';

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    let options: dataPreferences.Options = { name: 'myStore', dataGroupId: 'myId' };
    let promise = dataPreferences.deletePreferences(this.context, options);
    promise.then(() => {
      console.info("Succeeded in deleting preferences.");
    }).catch((err: BusinessError) => {
      console.error("Failed to delete preferences. code =" + err.code + ", message =" + err.message);
    })
  }
}
```


## dataPreferences.removePreferencesFromCache

removePreferencesFromCache(context: Context, name: string, callback: AsyncCallback&lt;void&gt;): void

Removes a **Preferences** instance from the cache. This API uses an asynchronous callback to return the result.

After an application calls [getPreferences](#datapreferencesgetpreferences) for the first time to obtain a **Preferences** instance, the obtained **Preferences** instance is cached. When the application calls [getPreferences](#datapreferencesgetpreferences) again, the **Preferences** instance will be read from the cache instead of from the persistent file. After this API is called to remove the instance from the cache, calling **getPreferences** again will read data from the persistent file and create a new **Preferences** instance.

Avoid using a removed **Preferences** instance to perform data operations, which may cause data inconsistency. Instead, set the removed **Preferences** instance to null. The system will reclaim them in a unified manner.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name  | Type                                 | Mandatory| Description                                                |
| -------- | ------------------------------------- | ---- | ---------------------------------------------------- |
| context  | Context | Yes  | Application context.<br>For details about the application context of the FA model, see [Context](../apis-ability-kit/js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md).                                        |
| name     | string                                | Yes  | Name of the **Preferences** instance.                             |
| callback | AsyncCallback&lt;void&gt;             | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**. Otherwise, **err** is an error object.|

**Example**

FA model:

```ts
// Obtain the context.
import featureAbility from '@ohos.ability.featureAbility';
import { BusinessError } from '@ohos.base'

let context = featureAbility.getContext();
dataPreferences.removePreferencesFromCache(context, 'myStore', (err: BusinessError) => {
  if (err) {
    console.error("Failed to remove preferences. code =" + err.code + ", message =" + err.message);
    return;
  }
  console.info("Succeeded in removing preferences.");
})
```

Stage model:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import { BusinessError } from '@ohos.base'
import window from '@ohos.window';

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    dataPreferences.removePreferencesFromCache(this.context, 'myStore', (err: BusinessError) => {
      if (err) {
        console.error("Failed to remove preferences. code =" + err.code + ", message =" + err.message);
        return;
      }
      console.info("Succeeded in removing preferences.");
    })
  }
}
```

## dataPreferences.removePreferencesFromCache

removePreferencesFromCache(context: Context, name: string): Promise&lt;void&gt;

Removes a **Preferences** instance from the cache. This API uses a promise to return the result.

After an application calls [getPreferences](#datapreferencesgetpreferences) for the first time to obtain a **Preferences** instance, the obtained **Preferences** instance is cached. When the application calls [getPreferences](#datapreferencesgetpreferences) again, the **Preferences** instance will be read from the cache instead of from the persistent file. After this API is called to remove the instance from the cache, calling **getPreferences** again will read data from the persistent file and create a new **Preferences** instance.

Avoid using a removed **Preferences** instance to perform data operations, which may cause data inconsistency. Instead, set the removed **Preferences** instance to null. The system will reclaim them in a unified manner.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name | Type                                 | Mandatory| Description                   |
| ------- | ------------------------------------- | ---- | ----------------------- |
| context | Context | Yes  | Application context.<br>For details about the application context of the FA model, see [Context](../apis-ability-kit/js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md).           |
| name    | string                                | Yes  | Name of the **Preferences** instance.|

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

FA model:

```ts
// Obtain the context.
import featureAbility from '@ohos.ability.featureAbility';
import { BusinessError } from '@ohos.base'

let context = featureAbility.getContext();
let promise = dataPreferences.removePreferencesFromCache(context, 'myStore');
promise.then(() => {
  console.info("Succeeded in removing preferences.");
}).catch((err: BusinessError) => {
  console.error("Failed to remove preferences. code =" + err.code + ", message =" + err.message);
})
```

Stage model:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import { BusinessError } from '@ohos.base'
import window from '@ohos.window';

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    let promise = dataPreferences.removePreferencesFromCache(this.context, 'myStore');
    promise.then(() => {
      console.info("Succeeded in removing preferences.");
    }).catch((err: BusinessError) => {
      console.error("Failed to remove preferences. code =" + err.code + ", message =" + err.message);
    })
  }
}
```

## dataPreferences.removePreferencesFromCacheSync<sup>10+</sup>

removePreferencesFromCacheSync(context: Context, name: string): void

Removes a **Preferences** instance from the cache. This API returns the result synchronously.

After an application calls [getPreferences](#datapreferencesgetpreferences) for the first time to obtain a **Preferences** instance, the obtained **Preferences** instance is cached. When the application calls [getPreferences](#datapreferencesgetpreferences) again, the **Preferences** instance will be read from the cache instead of from the persistent file. After this API is called to remove the instance from the cache, calling **getPreferences** again will read data from the persistent file and create a new **Preferences** instance.

Avoid using a removed **Preferences** instance to perform data operations, which may cause data inconsistency. Instead, set the removed **Preferences** instance to null. The system will reclaim them in a unified manner.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name | Type                                 | Mandatory| Description                   |
| ------- | ------------------------------------- | ---- | ----------------------- |
| context | Context | Yes  | Application context.<br>For details about the application context of the FA model, see [Context](../apis-ability-kit/js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md).           |
| name    | string                                | Yes  | Name of the **Preferences** instance.|

**Example**

FA model:

```ts
// Obtain the context.
import featureAbility from '@ohos.ability.featureAbility';
let context = featureAbility.getContext();
dataPreferences.removePreferencesFromCacheSync(context, 'myStore');
```

Stage model:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    dataPreferences.removePreferencesFromCacheSync(this.context, 'myStore');
  }
}
```

## dataPreferences.removePreferencesFromCache<sup>10+</sup>

removePreferencesFromCache(context: Context, options: Options, callback: AsyncCallback&lt;void&gt;): void

Removes a **Preferences** instance from the cache. This API uses an asynchronous callback to return the result.

After an application calls [getPreferences](#datapreferencesgetpreferences) for the first time to obtain a **Preferences** instance, the obtained **Preferences** instance is cached. When the application calls [getPreferences](#datapreferencesgetpreferences) again, the **Preferences** instance will be read from the cache instead of from the persistent file. After this API is called to remove the instance from the cache, calling **getPreferences** again will read data from the persistent file and create a new **Preferences** instance.

Avoid using a removed **Preferences** instance to perform data operations, which may cause data inconsistency. Instead, set the removed **Preferences** instance to null. The system will reclaim them in a unified manner.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name  | Type                     | Mandatory| Description                                                                                                                                                                          |
| -------- | ------------------------- | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| context  | Context                   | Yes  | Application context.<br>For details about the application context of the FA model, see [Context](../apis-ability-kit/js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md).|
| options  | [Options](#options10)          | Yes  | Configuration options of the **Preferences** instance.                                                                                                                                             |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**. Otherwise, **err** is an error object.                                                                                                                          |

**Error codes**

For details about the error codes, see [User Preference Error Codes](errorcode-preferences.md).

| ID| Error Message                      |
| -------- | ------------------------------ |
| 15501001 | Only supported in stage mode. |
| 15501002 | The data group id is not valid.     |

**Example**

FA model:

```ts
// Obtain the context.
import featureAbility from '@ohos.ability.featureAbility';
import { BusinessError } from '@ohos.base'

let context = featureAbility.getContext();
let options: dataPreferences.Options = { name: 'myStore' };
dataPreferences.removePreferencesFromCache(context, options, (err: BusinessError) => {
  if (err) {
    console.error("Failed to remove preferences. code =" + err.code + ", message =" + err.message);
    return;
  }
  console.info("Succeeded in removing preferences.");
})
```

Stage model:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import { BusinessError } from '@ohos.base'
import window from '@ohos.window';

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    let options: dataPreferences.Options = { name: 'myStore', dataGroupId: 'myId' };
    dataPreferences.removePreferencesFromCache(this.context, options, (err: BusinessError) => {
      if (err) {
        console.error("Failed to remove preferences. code =" + err.code + ", message =" + err.message);
        return;
      }
      console.info("Succeeded in removing preferences.");
    })
  }
}
```

## dataPreferences.removePreferencesFromCache<sup>10+</sup>

removePreferencesFromCache(context: Context, options: Options): Promise&lt;void&gt;

Removes a **Preferences** instance from the cache. This API uses a promise to return the result.

After an application calls [getPreferences](#datapreferencesgetpreferences) for the first time to obtain a **Preferences** instance, the obtained **Preferences** instance is cached. When the application calls [getPreferences](#datapreferencesgetpreferences) again, the **Preferences** instance will be read from the cache instead of from the persistent file. After this API is called to remove the instance from the cache, calling **getPreferences** again will read data from the persistent file and create a new **Preferences** instance.

Avoid using a removed **Preferences** instance to perform data operations, which may cause data inconsistency. Instead, set the removed **Preferences** instance to null. The system will reclaim them in a unified manner.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name | Type            | Mandatory| Description                                                                                                                                                                          |
| ------- | ---------------- | ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| context | Context          | Yes  | Application context.<br>For details about the application context of the FA model, see [Context](../apis-ability-kit/js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md).|
| options | [Options](#options10) | Yes  | Configuration options of the **Preferences** instance.                                                                                                                                             |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [User Preference Error Codes](errorcode-preferences.md).

| ID| Error Message                      |
| -------- | ------------------------------ |
| 15501001 | Only supported in stage mode. |
| 15501002 | The data group id is not valid.     |

**Example**

FA model:

```ts
// Obtain the context.
import featureAbility from '@ohos.ability.featureAbility';
import { BusinessError } from '@ohos.base'

let context = featureAbility.getContext();
let options: dataPreferences.Options = { name: 'myStore' };
let promise = dataPreferences.removePreferencesFromCache(context, options);
promise.then(() => {
  console.info("Succeeded in removing preferences.");
}).catch((err: BusinessError) => {
  console.error("Failed to remove preferences. code =" + err.code + ", message =" + err.message);
})
```

Stage model:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import { BusinessError } from '@ohos.base'
import window from '@ohos.window';

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    let options: dataPreferences.Options = { name: 'myStore', dataGroupId: 'myId' };
    let promise = dataPreferences.removePreferencesFromCache(this.context, options);
    promise.then(() => {
      console.info("Succeeded in removing preferences.");
    }).catch((err: BusinessError) => {
      console.error("Failed to remove preferences. code =" + err.code + ", message =" + err.message);
    })
  }
}
```

## dataPreferences.removePreferencesFromCacheSync<sup>10+</sup>

removePreferencesFromCacheSync(context: Context, options: Options):void

Removes a **Preferences** instance from the cache. This API returns the result synchronously.

After an application calls [getPreferences](#datapreferencesgetpreferences) for the first time to obtain a **Preferences** instance, the obtained **Preferences** instance is cached. When the application calls [getPreferences](#datapreferencesgetpreferences) again, the **Preferences** instance will be read from the cache instead of from the persistent file. After this API is called to remove the instance from the cache, calling **getPreferences** again will read data from the persistent file and create a new **Preferences** instance.

Avoid using a removed **Preferences** instance to perform data operations, which may cause data inconsistency. Instead, set the removed **Preferences** instance to null. The system will reclaim them in a unified manner.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name | Type                 | Mandatory| Description                                                        |
| ------- | --------------------- | ---- | ------------------------------------------------------------ |
| context | Context               | Yes  | Application context.<br>For details about the application context of the FA model, see [Context](../apis-ability-kit/js-apis-inner-app-context.md).<br>For details about the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-uiAbilityContext.md).|
| options | [Options](#options10) | Yes  | Configuration options of the **Preferences** instance.                           |

**Error codes**

For details about the error codes, see [User Preference Error Codes](errorcode-preferences.md).

| ID| Error Message                       |
| -------- | ------------------------------- |
| 15501001 | Only supported in stage mode.   |
| 15501002 | The data group id is not valid. |

**Example**

FA model:

```ts
// Obtain the context.
import featureAbility from '@ohos.ability.featureAbility';
let context = featureAbility.getContext();
let options: dataPreferences.Options = { name: 'myStore' };
dataPreferences.removePreferencesFromCacheSync(context, options);
```

Stage model:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    let options: dataPreferences.Options = { name: 'myStore', dataGroupId: 'myId' };
    dataPreferences.removePreferencesFromCacheSync(this.context, options);
  }
}
```

## Options<sup>10+</sup>

Represents the configuration of a **Preferences** instance.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

| Name       | Type  | Mandatory| Description                                                        |
| ----------- | ------ | ---- | ------------------------------------------------------------ |
| name        | string | Yes  | Name of the **Preferences** instance.                                     |
| dataGroupId | string\|null\|undefined | No  | Application group ID, which needs to be obtained from the AppGallery.<br>This parameter is optional. A **Preferences** instance will be created in the sandbox path corresponding to the specified **dataGroupId**. If this parameter is not specified, the **Preferences** instance is created in the sandbox directory of the application.<br>**Model restriction**: This attribute can be used only in the stage model.|


## Preferences

Provides APIs for obtaining and modifying the stored data.

Before calling any API of **Preferences**, you must obtain a **Preferences** instance by using [dataPreferences.getPreferences](#datapreferencesgetpreferences).


### get

get(key: string, defValue: ValueType, callback: AsyncCallback&lt;ValueType&gt;): void

Obtains the value of a key from this **Preferences** instance. This API uses an asynchronous callback to return the result. If the value is null or is not of the default value type, **defValue** is returned.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name  | Type                                        | Mandatory| Description                                                        |
| -------- | -------------------------------------------- | ---- | ------------------------------------------------------------ |
| key      | string                                       | Yes  | Key of the data to obtain. It cannot be empty.                             |
| defValue | [ValueType](#valuetype)                      | Yes  | Default value to be returned. The value supports the following types: number, string, boolean, Array\<number>, Array\<string>, Array\<boolean>, and Uint8Array.|
| callback | AsyncCallback&lt;[ValueType](#valuetype)&gt; | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined** and **data** is the value obtained. Otherwise, **err** is an error object.|

**Example**

```ts
import {BusinessError} from '@ohos.base';

preferences.get('startup', 'default', (err: BusinessError, val: dataPreferences.ValueType) => {
  if (err) {
    console.error("Failed to get value of 'startup'. code =" + err.code + ", message =" + err.message);
    return;
  }
  console.info("Obtained the value of 'startup' successfully. val: " + val);
})
```

### get

get(key: string, defValue: ValueType): Promise&lt;ValueType&gt;

Obtains the value of a key from this **Preferences** instance. This API uses a promise to return the result. If the value is null or is not of the default value type, **defValue** is returned.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

 **Parameters**

| Name  | Type                   | Mandatory| Description                                                        |
| -------- | ----------------------- | ---- | ------------------------------------------------------------ |
| key      | string                  | Yes  | Key of the data to obtain. It cannot be empty.                             |
| defValue | [ValueType](#valuetype) | Yes  | Default value to be returned. The value supports the following types: number, string, boolean, Array\<number>, Array\<string>, Array\<boolean>, and Uint8Array.|

**Return value**

| Type                               | Description                         |
| ----------------------------------- | ----------------------------- |
| Promise<[ValueType](#valuetype)&gt; | Promise used to return the value obtained.|

**Example**

```ts
import {BusinessError} from '@ohos.base';

let promise = preferences.get('startup', 'default');
promise.then((data: dataPreferences.ValueType) => {
  console.info("Got the value of 'startup'. Data: " + data);
}).catch((err: BusinessError) => {
  console.error("Failed to get value of 'startup'. code =" + err.code + ", message =" + err.message);
})
```

### getSync<sup>10+</sup>

getSync(key: string, defValue: ValueType): ValueType

Obtains the value of a key from this **Preferences** instance. This API returns the result synchronously. If the value is null or is not of the default value type, **defValue** is returned.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name  | Type                   | Mandatory| Description                                                        |
| -------- | ----------------------- | ---- | ------------------------------------------------------------ |
| key      | string                  | Yes  | Key of the data to obtain. It cannot be empty.                             |
| defValue | [ValueType](#valuetype) | Yes  | Default value to be returned. The value supports the following types: number, string, boolean, Array\<number>, Array\<string>, Array\<boolean>, and Uint8Array.|

**Return value**

| Type                               | Description                         |
| ----------------------------------- | ----------------------------- |
| [ValueType](#valuetype) | Returns the value obtained.|

**Example**

```ts
let value: dataPreferences.ValueType = preferences.getSync('startup', 'default');
```

### getAll

getAll(callback: AsyncCallback&lt;Object&gt;): void;

Obtains all KV pairs from this **Preferences** instance. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name  | Type                       | Mandatory| Description                                                        |
| -------- | --------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback&lt;Object&gt; | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined** and **value** provides all KV pairs obtained. Otherwise, **err** is an error object.|

**Example**

```ts
import {BusinessError} from '@ohos.base';

// There is no Object.keys in ArkTS, and the for..in... syntax cannot be used.
// If an error is reported, extract this API to a .ts file and expose it. Then import the API to the .ets file when required.
function getObjKeys(obj: Object): string[] {
  let keys = Object.keys(obj);
  return keys;
}

preferences.getAll((err: BusinessError, value: Object) => {
  if (err) {
    console.error("Failed to get all key-values. code =" + err.code + ", message =" + err.message);
    return;
  }
  let allKeys = getObjKeys(value);
  console.info("getAll keys = " + allKeys);
  console.info("getAll object = " + JSON.stringify(value));
})
```


### getAll

getAll(): Promise&lt;Object&gt;

Obtains all KV pairs from this **Preferences** instance. This API uses a promise to return the result.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Return value**

| Type                 | Description                                       |
| --------------------- | ------------------------------------------- |
| Promise&lt;Object&gt; | Promise used to return the KV pairs obtained.|

**Example**

```ts
import {BusinessError} from '@ohos.base';

// There is no Object.keys in ArkTS, and the for..in... syntax cannot be used.
// If an error is reported, extract this API to a .ts file and expose it. Then import the API to the .ets file when required.
function getObjKeys(obj: Object): string[] {
  let keys = Object.keys(obj);
  return keys;
}

let promise = preferences.getAll();
promise.then((value: Object) => {
  let allKeys = getObjKeys(value);
  console.info('getAll keys = ' + allKeys);
  console.info("getAll object = " + JSON.stringify(value));
}).catch((err: BusinessError) => {
  console.error("Failed to get all key-values. code =" + err.code + ", message =" + err.message);
})
```

### getAllSync<sup>10+</sup>

getAllSync(): Object

Obtains all KV pairs from this **Preferences** instance. This API returns the result synchronously.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Return value**

| Type                 | Description                                       |
| --------------------- | ------------------------------------------- |
| Object | Returns all KV pairs obtained.|

**Example**

```ts
// There is no Object.keys in ArkTS, and the for..in... syntax cannot be used.
// If an error is reported, extract this API to a .ts file and expose it. Then import the API to the .ets file when required.
function getObjKeys(obj: Object): string[] {
  let keys = Object.keys(obj);
  return keys;
}

let value = preferences.getAllSync();
let allKeys = getObjKeys(value);
console.info('getAll keys = ' + allKeys);
console.info("getAll object = " + JSON.stringify(value));
```

### put

put(key: string, value: ValueType, callback: AsyncCallback&lt;void&gt;): void

Writes data to this **Preferences** instance. This API uses an asynchronous callback to return the result. You can use [flush](#flush) to persist the **Preferences** instance.

  > **NOTE**
  >
  > If the key already exists, **put()** overwrites the value. You can use **hasSync()** to check whether the KV pair exists.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name  | Type                     | Mandatory| Description                                                        |
| -------- | ------------------------- | ---- | ------------------------------------------------------------ |
| key      | string                    | Yes  | Key of the data. It cannot be empty.                               |
| value    | [ValueType](#valuetype)   | Yes  | Value to write. The value supports the following types: number, string, boolean, Array\<number>, Array\<string>, Array\<boolean>, and Uint8Array.|
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**. Otherwise, **err** is an error object.  |

**Example**

```ts
import {BusinessError} from '@ohos.base';

preferences.put('startup', 'auto', (err: BusinessError) => {
  if (err) {
    console.error("Failed to put value of 'startup'. code =" + err.code + ", message =" + err.message);
    return;
  }
  console.info("Successfully put the value of 'startup'.");
})
```


### put

put(key: string, value: ValueType): Promise&lt;void&gt;

Writes data to this **Preferences** instance. This API uses a promise to return the result. You can use [flush](#flush) to persist the **Preferences** instance.

  > **NOTE**
  >
  > If the key already exists, **put()** overwrites the value. You can use **hasSync()** to check whether the KV pair exists.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name| Type                   | Mandatory| Description                                                        |
| ------ | ----------------------- | ---- | ------------------------------------------------------------ |
| key    | string                  | Yes  | Key of the data. It cannot be empty.                               |
| value  | [ValueType](#valuetype) | Yes  | Value to write. The value supports the following types: number, string, boolean, Array\<number>, Array\<string>, Array\<boolean>, and Uint8Array.|

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
import {BusinessError} from '@ohos.base';

let promise = preferences.put('startup', 'auto');
promise.then(() => {
  console.info("Successfully put the value of 'startup'.");
}).catch((err: BusinessError) => {
  console.error("Failed to put value of 'startup'. code =" + err.code + ", message =" + err.message);
})
```


### putSync<sup>10+</sup>

putSync(key: string, value: ValueType): void

Writes data to this **Preferences** instance. This API returns the result synchronously. You can use [flush](#flush) to persist the **Preferences** instance.

  > **NOTE**
  >
  > If the key already exists, **putSync()** overwrites the value. You can use **hasSync()** to check whether the KV pair exists.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name| Type                   | Mandatory| Description                                                        |
| ------ | ----------------------- | ---- | ------------------------------------------------------------ |
| key    | string                  | Yes  | Key of the data. It cannot be empty.                               |
| value  | [ValueType](#valuetype) | Yes  | Value to write. The value supports the following types: number, string, boolean, Array\<number>, Array\<string>, Array\<boolean>, and Uint8Array.|

**Example**

```ts
preferences.putSync('startup', 'auto');
```


### has

has(key: string, callback: AsyncCallback&lt;boolean&gt;): void

Checks whether this **Preferences** instance contains the KV pair of the given key. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name  | Type                        | Mandatory| Description                                                        |
| -------- | ---------------------------- | ---- | ------------------------------------------------------------ |
| key      | string                       | Yes  | Key of the data to check. It cannot be empty.                             |
| callback | AsyncCallback&lt;boolean&gt; | Yes  | Callback used to return the result. If the **Preferences** instance contains the KV pair, **true** will be returned. Otherwise, **false** will be returned.|

**Example**

```ts
import {BusinessError} from '@ohos.base';

preferences.has('startup', (err: BusinessError, val: boolean) => {
  if (err) {
    console.error("Failed to check the key 'startup'. code =" + err.code + ", message =" + err.message);
    return;
  }
  if (val) {
    console.info("The key 'startup' is contained.");
  } else {
    console.info("The key 'startup' is not contained.");
  }
})
```


### has

has(key: string): Promise&lt;boolean&gt;

Checks whether this **Preferences** instance contains the KV pair of the given key. This API uses a promise to return the result.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name| Type  | Mandatory| Description                           |
| ------ | ------ | ---- | ------------------------------- |
| key    | string | Yes  | Key of the data to check. It cannot be empty.|

**Return value**

| Type                  | Description                                                        |
| ---------------------- | ------------------------------------------------------------ |
| Promise&lt;boolean&gt; | Promise used to return the result. If the **Preferences** instance contains the KV pair, **true** will be returned. Otherwise, **false** will be returned.|

**Example**

```ts
import { BusinessError } from '@ohos.base';

let promise = preferences.has('startup');
promise.then((val: boolean) => {
  if (val) {
    console.info("The key 'startup' is contained.");
  } else {
    console.info("The key 'startup' is not contained.");
  }
}).catch((err: BusinessError) => {
  console.error("Failed to check the key 'startup'. code =" + err.code + ", message =" + err.message);
})
```


### hasSync<sup>10+</sup>

hasSync(key: string): boolean

Checks whether this **Preferences** instance contains the KV pair of the given key. This API returns the result synchronously.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name| Type  | Mandatory| Description                           |
| ------ | ------ | ---- | ------------------------------- |
| key    | string | Yes  | Key of the data to check. It cannot be empty.|

**Return value**

| Type                  | Description                                                        |
| ---------------------- | ------------------------------------------------------------ |
| boolean | If the **Preferences** instance contains the KV pair, **true** will be returned. Otherwise, **false** will be returned.|

**Example**

```ts
let isExist: boolean = preferences.hasSync('startup');
if (isExist) {
  console.info("The key 'startup' is contained.");
} else {
  console.info("The key 'startup' is not contained.");
}
```


### delete

delete(key: string, callback: AsyncCallback&lt;void&gt;): void

Deletes a KV pair from this **Preferences** instance. This API uses an asynchronous callback to return the result. You can use [flush](#flush) to persist the **Preferences** instance.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name  | Type                     | Mandatory| Description                                                |
| -------- | ------------------------- | ---- | ---------------------------------------------------- |
| key      | string                    | Yes  | Key of the KV pair to delete. It cannot be empty.                     |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**. Otherwise, **err** is an error object.|

**Example**

```ts
import {BusinessError} from '@ohos.base';

preferences.delete('startup', (err: BusinessError) => {
  if (err) {
    console.error("Failed to delete the key 'startup'. code =" + err.code + ", message =" + err.message);
    return;
  }
  console.info("Deleted the key 'startup'.");
})
```


### delete

delete(key: string): Promise&lt;void&gt;

Deletes a KV pair from this **Preferences** instance. This API uses a promise to return the result. You can use [flush](#flush) to persist the **Preferences** instance.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name| Type  | Mandatory| Description                           |
| ------ | ------ | ---- | ------------------------------- |
| key    | string | Yes  | Key of the KV pair to delete. It cannot be empty.|

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
import {BusinessError} from '@ohos.base';

let promise = preferences.delete('startup');
promise.then(() => {
  console.info("Deleted the key 'startup'.");
}).catch((err: BusinessError) => {
  console.error("Failed to delete the key 'startup'. code =" + err.code +", message =" + err.message);
})
```


### deleteSync<sup>10+</sup>

deleteSync(key: string): void

Deletes a KV pair from this **Preferences** instance. This API returns the result synchronously. You can use [flush](#flush) to persist the **Preferences** instance.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name| Type  | Mandatory| Description                           |
| ------ | ------ | ---- | ------------------------------- |
| key    | string | Yes  | Key of the KV pair to delete. It cannot be empty.|

**Example**

```ts
preferences.deleteSync('startup');
```


### flush

flush(callback: AsyncCallback&lt;void&gt;): void

Flushes the data in this **Preferences** instance to the persistent file. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name  | Type                     | Mandatory| Description                                                |
| -------- | ------------------------- | ---- | ---------------------------------------------------- |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**. Otherwise, **err** is an error object.|

**Example**

```ts
import {BusinessError} from '@ohos.base';

preferences.flush((err: BusinessError) => {
  if (err) {
    console.error("Failed to flush. code =" + err.code + ", message =" + err.message);
    return;
  }
  console.info("Successfully flushed data.");
})
```


### flush

flush(): Promise&lt;void&gt;

Flushes the data in this **Preferences** instance to the persistent file. This API uses a promise to return the result.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
import {BusinessError} from '@ohos.base';

let promise = preferences.flush();
promise.then(() => {
  console.info("Successfully flushed data.");
}).catch((err: BusinessError) => {
  console.error("Failed to flush. code =" + err.code + ", message =" + err.message);
})
```


### clear

clear(callback: AsyncCallback&lt;void&gt;): void

Clears this **Preferences** instance. This API uses an asynchronous callback to return the result. You can use [flush](#flush) to persist the **Preferences** instance.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name  | Type                     | Mandatory| Description                                                |
| -------- | ------------------------- | ---- | ---------------------------------------------------- |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**. Otherwise, **err** is an error object.|

**Example**

```ts
import {BusinessError} from '@ohos.base';

preferences.clear((err: BusinessError) =>{
  if (err) {
    console.error("Failed to clear. code =" + err.code + ", message =" + err.message);
    return;
  }
  console.info("Successfully cleared data.");
})
```


### clear

clear(): Promise&lt;void&gt;

Clears this **Preferences** instance. This API uses a promise to return the result. You can use [flush](#flush) to persist the **Preferences** instance.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
import {BusinessError} from '@ohos.base';

let promise = preferences.clear();
promise.then(() => {
  console.info("Successfully cleared data.");
}).catch((err: BusinessError) => {
  console.error("Failed to clear. code =" + err.code + ", message =" + err.message);
})
```


### clearSync<sup>10+</sup>

clearSync(): void

Clears this **Preferences** instance. This API returns the result synchronously. You can use [flush](#flush) to persist the **Preferences** instance.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Example**

```ts
preferences.clearSync();
```


### on('change')

on(type: 'change', callback: Callback&lt;string&gt;): void

Subscribes to data changes. The registered callback will be invoked to return the new value if the data change is [flushed](#flush).

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name  | Type    | Mandatory| Description                                    |
| -------- | -------- | ---- | ---------------------------------------- |
| type     | string   | Yes  | Event type. The value is **'change'**, which indicates data changes.|
| callback | Callback&lt;string&gt; | Yes  | Callback used to return the data change.    |

**Example**

```ts
import {BusinessError} from '@ohos.base';

let observer = (key: string) => {
  console.info("The key " + key + " changed.");
}
preferences.on('change', observer);
preferences.putSync('startup', 'manual');
preferences.flush((err: BusinessError) => {
  if (err) {
    console.error("Failed to flush. Cause: " + err);
    return;
  }
  console.info("Successfully flushed data.");
})
```

### on('multiProcessChange')<sup>10+</sup>

on(type: 'multiProcessChange', callback: Callback&lt;string&gt;): void

Subscribes to inter-process data changes. For the multiple processes holding the same preference file, if the value of the subscribed key changes in any process, the callback in this API will be invoked after [flush()](#flush) is executed.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name  | Type    | Mandatory| Description                                                        |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | Yes  | Event type. The value is **'multiProcessChange'**, which indicates inter-process data changes.|
| callback | Callback&lt;string&gt; | Yes  | Callback used to return the inter-process data change.                        |

**Error codes**

For details about the error codes, see [User Preference Error Codes](errorcode-preferences.md).

| ID| Error Message                              |
| -------- | -------------------------------------- |
| 15500019 | Failed to obtain subscription service. |

**Example**

```ts
import {BusinessError} from '@ohos.base';

let observer = (key: string) => {
  console.info("The key " + key + " changed.");
}
preferences.on('multiProcessChange', observer);
preferences.putSync('startup', 'manual');
preferences.flush((err: BusinessError) => {
  if (err) {
    console.error("Failed to flush. Cause: " + err);
    return;
  }
  console.info("Successfully flushed data.");
})
```

### off('change')

off(type: 'change', callback?: Callback&lt;string&gt;): void

Unsubscribes from data changes.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name  | Type    | Mandatory| Description                                                        |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | Yes  | Event type. The value is **'change'**, which indicates data changes.                    |
| callback | Callback&lt;string&gt; | No  | Callback to unregister. If this parameter is not specified, this API unregisters all callbacks for data changes.|

**Example**

```ts
import {BusinessError} from '@ohos.base';

let observer = (key: string) => {
  console.info("The key " + key + " changed.");
}
preferences.on('change', observer);
preferences.putSync('startup', 'auto');
preferences.flush((err: BusinessError) => {
  if (err) {
    console.error("Failed to flush. Cause: " + err);
    return;
  }
  console.info("Successfully flushed data.");
})
preferences.off('change', observer);
```

### off('multiProcessChange')<sup>10+</sup>

off(type: 'multiProcessChange', callback?: Callback&lt;string&gt;): void

Unsubscribes from inter-process data changes.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

**Parameters**

| Name  | Type    | Mandatory| Description                                                        |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | Yes  | Event type. The value is **'multiProcessChange'**, which indicates inter-process data changes.|
| callback | Callback&lt;string&gt; | No  | Callback to unregister. If this parameter is not specified, this API unregisters all callbacks for inter-process data changes.|

**Example**

```ts
import {BusinessError} from '@ohos.base';

let observer = (key: string) => {
  console.info("The key " + key + " changed.");
}
preferences.on('multiProcessChange', observer);
preferences.putSync('startup', 'auto');
preferences.flush((err: BusinessError) => {
  if (err) {
    console.error("Failed to flush. Cause: " + err);
    return;
  }
  console.info("Successfully flushed data.");
})
preferences.off('multiProcessChange', observer);
```
## ValueType

Enumerates the value types.

**System capability**: SystemCapability.DistributedDataManager.Preferences.Core

| Type           | Description                             |
| --------------- | --------------------------------- |
| number          | The value is a number.               |
| string          | The value is a string.             |
| boolean         | The value is true or false.             |
| Array\<number>  | The value is an array of numbers.     |
| Array\<boolean> | The value is a Boolean array.     |
| Array\<string>  | The value is an array of strings.   |
| Uint8Array<sup>11+</sup>      | The value is an array of 8-bit unsigned integers.|
