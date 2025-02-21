# @ohos.app.ability.abilityLifecycleCallback (AbilityLifecycleCallback)

The **AbilityLifecycleCallback** module defines the callbacks to receive lifecycle changes of [ApplicationContext](js-apis-inner-application-applicationContext.md).

> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
> The APIs of this module can be used only in the stage model.

## Modules to Import

```ts
import AbilityLifecycleCallback from '@ohos.app.ability.AbilityLifecycleCallback';
```

## AbilityLifecycleCallback.onAbilityCreate

onAbilityCreate(ability: UIAbility): void

Called when an ability is created.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | ability | [UIAbility](js-apis-app-ability-uiAbility.md) | Yes| **Ability** object.|

**Example**

See [Usage of AbilityLifecycleCallback](#usage-of-abilitylifecyclecallback).

## AbilityLifecycleCallback.onWindowStageCreate

onWindowStageCreate(ability: UIAbility, windowStage: window.WindowStage): void

Called when the window stage of an ability is created.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | ability | [UIAbility](js-apis-app-ability-uiAbility.md) | Yes| **Ability** object.|
  | windowStage | [window.WindowStage](../apis-arkui/js-apis-window.md#windowstage9) | Yes| **WindowStage** object.|

**Example**

See [Usage of AbilityLifecycleCallback](#usage-of-abilitylifecyclecallback).

## AbilityLifecycleCallback.onWindowStageActive

onWindowStageActive(ability: UIAbility, windowStage: window.WindowStage): void

Called when the window stage of an ability gains focus.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | ability | [UIAbility](js-apis-app-ability-uiAbility.md) | Yes| **Ability** object.|
  | windowStage | [window.WindowStage](../apis-arkui/js-apis-window.md#windowstage9) | Yes| **WindowStage** object.|

**Example**

See [Usage of AbilityLifecycleCallback](#usage-of-abilitylifecyclecallback).

## AbilityLifecycleCallback.onWindowStageInactive

onWindowStageInactive(ability: UIAbility, windowStage: window.WindowStage): void

Called when the window stage of an ability loses focus.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | ability | [UIAbility](js-apis-app-ability-uiAbility.md) | Yes| **Ability** object.|
  | windowStage | [window.WindowStage](../apis-arkui/js-apis-window.md#windowstage9) | Yes| **WindowStage** object.|

**Example**

See [Usage of AbilityLifecycleCallback](#usage-of-abilitylifecyclecallback).

## AbilityLifecycleCallback.onWindowStageDestroy

onWindowStageDestroy(ability: UIAbility, windowStage: window.WindowStage): void

Called when the window stage of an ability is destroyed.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | ability | [UIAbility](js-apis-app-ability-uiAbility.md) | Yes| **Ability** object.|
  | windowStage | [window.WindowStage](../apis-arkui/js-apis-window.md#windowstage9) | Yes| **WindowStage** object.|

**Example**

See [Usage of AbilityLifecycleCallback](#usage-of-abilitylifecyclecallback).

## AbilityLifecycleCallback.onAbilityDestroy

onAbilityDestroy(ability: UIAbility): void

Called when an ability is destroyed.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | ability | [UIAbility](js-apis-app-ability-uiAbility.md) | Yes| **Ability** object.|

**Example**

See [Usage of AbilityLifecycleCallback](#usage-of-abilitylifecyclecallback).

## AbilityLifecycleCallback.onAbilityForeground

onAbilityForeground(ability: UIAbility): void

Called when an ability is switched from the background to the foreground.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | ability | [UIAbility](js-apis-app-ability-uiAbility.md) | Yes| **Ability** object.|

**Example**

See [Usage of AbilityLifecycleCallback](#usage-of-abilitylifecyclecallback).

## AbilityLifecycleCallback.onAbilityBackground

onAbilityBackground(ability: UIAbility): void

Called when an ability is switched from the foreground to the background.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | ability | [UIAbility](js-apis-app-ability-uiAbility.md) | Yes| **Ability** object.|

**Example**

See [Usage of AbilityLifecycleCallback](#usage-of-abilitylifecyclecallback).

## AbilityLifecycleCallback.onAbilityContinue

onAbilityContinue(ability: UIAbility): void

Called when an ability is continued on another device.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | ability | [UIAbility](js-apis-app-ability-uiAbility.md) | Yes| **Ability** object.|

**Example**

See [Usage of AbilityLifecycleCallback](#usage-of-abilitylifecyclecallback).

## Usage of AbilityLifecycleCallback

**Example**
GlobalContext.ts
Global context
```ts
// Construct a singleton object.
export class GlobalContext {
  private constructor() {}
  private static instance: GlobalContext;
  private _objects = new Map<string, Object>();

  public static getContext(): GlobalContext {
    if (!GlobalContext.instance) {
      GlobalContext.instance = new GlobalContext();
    }
    return GlobalContext.instance;
  }

  getObject(value: string): Object | undefined {
    return this._objects.get(value);
  }

  setObject(key: string, objectClass: Object): void {
    this._objects.set(key, objectClass);
  }
}
```

MyFirstAbility.ts
First ability of the application
```ts
import AbilityLifecycleCallback from '@ohos.app.ability.AbilityLifecycleCallback';
import UIAbility from '@ohos.app.ability.UIAbility';

// Import GlobalContext. Use the actual path declared.
import { GlobalContext } from '../GlobalContext'

// Declare the ability lifecycle callbacks. A listener can be registered in applicationContext only after all the callbacks are configured.
let abilityLifecycleCallback: AbilityLifecycleCallback = {
    onAbilityCreate(ability){
        console.log('AbilityLifecycleCallback onAbilityCreate.');
    },
    onWindowStageCreate(ability, windowStage){
        console.log('AbilityLifecycleCallback onWindowStageCreate.');
    },
    onWindowStageActive(ability, windowStage){
        console.log('AbilityLifecycleCallback onWindowStageActive.');
    },
    onWindowStageInactive(ability, windowStage){
        console.log('AbilityLifecycleCallback onWindowStageInactive.');
    },
    onWindowStageDestroy(ability, windowStage){
        console.log('AbilityLifecycleCallback onWindowStageDestroy.');
    },
    onAbilityDestroy(ability){
        console.log('AbilityLifecycleCallback onAbilityDestroy.');
    },
    onAbilityForeground(ability){
        console.log('AbilityLifecycleCallback onAbilityForeground.');
    },
    onAbilityBackground(ability){
        console.log('AbilityLifecycleCallback onAbilityBackground.');
    },
    onAbilityContinue(ability){
        console.log('AbilityLifecycleCallback onAbilityContinue.');
    }
};

export default class MyFirstAbility extends UIAbility {
    onCreate() {
        console.log('MyAbilityStage onCreate');
        // 1. Obtain applicationContext through the context attribute.
        let applicationContext = this.context.getApplicationContext();
        // 2. Register the listener for the ability lifecycle changes through the applicationContext object.
        try {
            let lifecycleId = applicationContext.on('abilityLifecycle', abilityLifecycleCallback);
            GlobalContext.getContext().setObject("lifecycleId", lifecycleId);
            console.log(`registerAbilityLifecycleCallback lifecycleId: ${GlobalContext.getContext().getObject('lifecycleId')}`);
        } catch (paramError) {
            console.error(`error: ${paramError.code}, ${paramError.message}`);
        }
    }
}
```

MySecondAbility.ts
Second ability of the application
```ts
import UIAbility from '@ohos.app.ability.UIAbility';

// Import GlobalContext. Use the actual path declared.
import { GlobalContext } from '../GlobalContext'

export default class MySecondAbility extends UIAbility {
    onDestroy() {
        let applicationContext = this.context.getApplicationContext();
        let lifecycleId = GlobalContext.getContext().getObject("lifecycleId") as number;
        // 3. Deregister the listener for the ability lifecycle changes through the applicationContext object.
        applicationContext.off('abilityLifecycle', lifecycleId, (error) => {
            if (error && error.code !== 0) {
                console.error(`unregisterAbilityLifecycleCallback fail, error: ${JSON.stringify(error)}`);
            } else {
                console.log('unregisterAbilityLifecycleCallback success.');
            }
        });
    }
}
```
