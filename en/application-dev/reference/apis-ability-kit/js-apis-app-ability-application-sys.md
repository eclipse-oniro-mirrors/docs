#  @ohos.app.ability.application (Application) (System API)
You can use this module to create a [Context](../../application-models/application-context-stage.md).

> **NOTE**
>
> The initial APIs of this module are supported since API version 12. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> The APIs of this module can be used only in the stage model.

## Modules to Import

```ts
import { application } from '@kit.AbilityKit';
```
## application.createModuleContext<sup>12+</sup>

createModuleContext(context: Context, bundleName: string, moduleName: string): Promise\<Context>

Creates the context for a module.


**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API.

**Parameters**

| Name       | Type                                      | Mandatory  | Description            |
| --------- | ---------------------------------------- | ---- | -------------- |
| context | [Context](../../reference/apis-ability-kit/js-apis-inner-application-context.md) | Yes| Application context.| 
| bundleName | string   | Yes   | Bundle name of the application. If an empty string is passed in, the current application is used by default.|
| moduleName | string | Yes| Module name.|

**Return value**

| Type              | Description               |
| ------------------ | ------------------- |
| Promise\<[Context](../../reference/apis-ability-kit/js-apis-inner-application-context.md)> | Promise used to return the context created.|

**Error codes**

For details about the error codes, see [Ability Error Codes](errorcode-ability.md).

| ID| Error Message       |
| -------- | --------------- |
| 201 | Permission denied. |
| 202 | Permission denied, non-system app called system api.|
| 401 | Parameter error. Possible causes: 1.Mandatory parameters are left unspecified. 2.Incorrect parameter types. |

**Example**

```ts
import { UIAbility, application, common } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';

export default class EntryAbility extends UIAbility {
  onCreate() {
    let moduleContext: common.Context;
    try {
      application.createModuleContext(this.context, 'bundlename', 'entry').then((data: Context)=>{
        moduleContext = data;
        console.info('createModuleContext success!');
      }).catch((error : BusinessError)=>{
        console.error(`createModuleContext failed, error.code: ${(error as BusinessError).code}, error.message: ${(error as BusinessError).message}`);
      })
    } catch (error) {
      console.error(`createModuleContext failed, error.code: ${(error as BusinessError).code}, error.message: ${(error as BusinessError).message}`);
    }
  }
}
```

## application.createBundleContext<sup>12+</sup>

createBundleContext(context: Context, bundleName: string): Promise\<Context>

Creates the context for an application.


**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API.

**Parameters**

| Name       | Type                                      | Mandatory  | Description            |
| --------- | ---------------------------------------- | ---- | -------------- |
| context | [Context](../../reference/apis-ability-kit/js-apis-inner-application-context.md) | Yes| Application context.| 
| bundleName | string   | Yes   | Bundle name of the application.|

**Return value**

| Type              | Description               |
| ------------------ | ------------------- |
| Promise\<[Context](../../reference/apis-ability-kit/js-apis-inner-application-context.md)> | Promise used to return the context created.|

**Error codes**

For details about the error codes, see [Ability Error Codes](errorcode-ability.md).

| ID| Error Message       |
| -------- | --------------- |
| 201 | Permission denied. |
| 202 | Permission denied, non-system app called system api.|
| 401 | Parameter error. Possible causes: 1.Mandatory parameters are left unspecified. 2.Incorrect parameter types. |


**Example**

```ts
import { UIAbility, application, common } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';

export default class EntryAbility extends UIAbility {
  onCreate() {
    let moduleContext: common.Context;
    try {
      application.createBundleContext(this.context, 'bundlename').then((data: Context)=>{
        moduleContext = data;
        console.info('createBundleContext success!');
      }).catch((error : BusinessError)=>{
        console.error(`createBundleContext failed, error.code: ${(error as BusinessError).code}, error.message: ${(error as BusinessError).message}`);
      })
    } catch (error) {
      console.error(`createBundleContext failed, error.code: ${(error as BusinessError).code}, error.message: ${(error as BusinessError).message}`);
    }
  }
}
```
