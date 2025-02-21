# Context (System API)

The **Context** module provides context for abilities or applications. It allows access to application-specific resources.

> **NOTE**
>
>  - The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>  - The APIs of this module can be used only in the stage model.
>  - The APIs provided by this module are system APIs.

## Modules to Import

```ts
import common from '@ohos.app.ability.common';
```

## Context.createBundleContext

createBundleContext(bundleName: string): Context

Creates the context based on the bundle name.

**System API**: This is a system API.

**Required permissions**: ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name      | Type                    | Mandatory  | Description           |
| -------- | ---------------------- | ---- | ------------- |
| bundleName | string | Yes   | Bundle name.|

**Return value**

| Type| Description|
| -------- | -------- |
| Context | Context created.|

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import common from '@ohos.app.ability.common';

export default class EntryAbility extends UIAbility {
  onCreate() {
    console.log('MyAbility onCreate');
    let bundleContext: common.Context;
    try {
      bundleContext = this.context.createBundleContext('com.example.test');
    } catch (error) {
      console.error(`createBundleContext failed, error.code: ${error.code}, error.message: ${error.message}`);
    }
  }
}
```

## Context.createModuleContext

createModuleContext(bundleName: string, moduleName: string): Context

Creates the context based on the bundle name and module name.

**System API**: This is a system API.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name      | Type                    | Mandatory  | Description           |
| -------- | ---------------------- | ---- | ------------- |
| bundleName | string | Yes   | Bundle name.|
| moduleName | string | Yes   | Module name.|

**Return value**

| Type| Description|
| -------- | -------- |
| Context | Context created.|

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import common from '@ohos.app.ability.common';

export default class EntryAbility extends UIAbility {
  onCreate() {
    console.log('MyAbility onCreate');
    let moduleContext: common.Context;
    try {
      moduleContext = this.context.createModuleContext('com.example.test', 'entry');
    } catch (error) {
      console.error(`createModuleContext failed, error.code: ${error.code}, error.message: ${error.message}`);
    }
  }
}
```

## Context.createModuleResourceManager<sup>11+</sup>

createModuleResourceManager(bundleName: string, moduleName: string): resmgr.ResourceManager

Creates a resource management object for a module.

**System API**: This is a system API.

**Required permissions**: ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name      | Type                    | Mandatory  | Description           |
| -------- | ---------------------- | ---- | ------------- |
| bundleName | string | Yes   | Bundle name.|
| moduleName | string | Yes   | Module name.|

**Return value**

| Type| Description|
| -------- | -------- |
| resmgr.ResourceManager | Object for resource management.|

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import common from '@ohos.app.ability.common';
import resourceManager from '@ohos.resourceManager';
export default class EntryAbility extends UIAbility {
  onCreate() {
    console.log('MyAbility onCreate');
    let ModuleResourceManager: resourceManager.ResourceManager;
    try {
      ModuleResourceManager = this.context.createModuleResourceManager('com.example.test', 'entry');
    } catch (error) {
      console.error(`createModuleResourceManager failed, error.code: ${error.code}, error.message: ${error.message}`);
    }
  }
}
```
