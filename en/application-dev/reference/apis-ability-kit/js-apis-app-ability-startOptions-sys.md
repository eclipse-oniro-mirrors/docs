# @ohos.app.ability.StartOptions (StartOptions) (System API)

**StartOptions** is used as an input parameter of [startAbility()](js-apis-inner-application-uiAbilityContext.md#uiabilitycontextstartability-1) to specify the window mode of an ability.

> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
> The APIs of this module can be used only in the stage model.
>
> This topic describes only system APIs provided by the module. For details about its public APIs, see [@ohos.app.ability.StartOptions (StartOptions)](js-apis-app-ability-startOptions.md).

## Modules to Import

```ts
import StartOptions from '@ohos.app.ability.StartOptions';
```

## Attributes

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name| Type| Read-only| Mandatory| Description|
| -------- | -------- | -------- | -------- | -------- |
| [windowMode](js-apis-app-ability-abilityConstant-sys.md#abilityconstantwindowmode) | number | No| No| Window mode.<br>**System API**: This is a system API and cannot be called by third-party applications.|

**Example**

  ```ts
  import UIAbility from '@ohos.app.ability.UIAbility';
  import Want from '@ohos.app.ability.Want';
  import StartOptions from '@ohos.app.ability.StartOptions';
  import { BusinessError } from '@ohos.base';

  export default class EntryAbility extends UIAbility {

    onForeground() {
      let want: Want = {
        deviceId: '',
        bundleName: 'com.example.myapplication',
        abilityName: 'EntryAbility'
      };
      let options: StartOptions = {
        displayId: 0
      };

      try {
        this.context.startAbility(want, options, (err: BusinessError) => {
          if (err.code) {
            // Process service logic errors.
            console.error(`startAbility failed, code is ${err.code}, message is ${err.message}`);
            return;
          }
          // Carry out normal service processing.
          console.info('startAbility succeed');
        });
      } catch (err) {
        // Process input parameter errors.
        let code = (err as BusinessError).code;
        let message = (err as BusinessError).message;
        console.error(`startAbility failed, code is ${code}, message is ${message}`);
      }
    }
  }
  ```
