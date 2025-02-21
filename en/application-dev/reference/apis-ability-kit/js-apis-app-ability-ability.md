# @ohos.app.ability.Ability (Ability Base Class)

This is the base class of [UIAbility](js-apis-app-ability-uiAbility.md) and [ExtensionAbility](js-apis-app-ability-extensionAbility.md). It provides the callbacks for system configuration updates and memory level updates. You cannot inherit from this base class.

> **NOTE**
> 
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
> The APIs of this module can be used only in the stage model.

## Modules to Import

```ts
import Ability from '@ohos.app.ability.Ability';
```

## Ability.onConfigurationUpdate

onConfigurationUpdate(newConfig: Configuration): void

Called when the configuration of the environment where the ability is running is updated.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| newConfig | [Configuration](js-apis-app-ability-configuration.md) | Yes| New configuration.|

**Example**
  ```ts
// You are not allowed to inherit from the top-level base class Ability. Therefore, the derived class UIAbility is used as an example.
import UIAbility from '@ohos.app.ability.UIAbility';
import { Configuration } from '@ohos.app.ability.Configuration';

class MyUIAbility extends UIAbility {
    onConfigurationUpdate(config: Configuration) {
        console.log(`onConfigurationUpdate, config: ${JSON.stringify(config)}`);
    }
}
  ```

## Ability.onMemoryLevel

onMemoryLevel(level: AbilityConstant.MemoryLevel): void

Called when the system adjusts the memory level.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| level | [AbilityConstant.MemoryLevel](js-apis-app-ability-abilityConstant.md#abilityconstantmemorylevel) | Yes| New memory level.|

**Example**

  ```ts
// You are not allowed to inherit from the top-level base class Ability. Therefore, the derived class UIAbility is used as an example.
import UIAbility from '@ohos.app.ability.UIAbility';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';

class MyUIAbility extends UIAbility {
    onMemoryLevel(level: AbilityConstant.MemoryLevel) {
        console.log(`onMemoryLevel, level: ${JSON.stringify(level)}`);
    } 
}
  ```
