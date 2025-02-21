# @ohos.ability.ability (Ability)

Ability模块将二级模块API组织在一起方便开发者进行导出。

> **说明：**
> 
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> 本模块接口仅可在FA模型下使用

## 导入模块

```ts
import ability from '@ohos.ability.ability';
```

## 属性

**系统能力：** SystemCapability.Ability.AbilityRuntime.AbilityCore

| 名称         | 类型                 | 描述                                                         |
| ----------- | -------------------- | ------------------------------------------------------------ |
| DataAbilityHelper    | [DataAbilityHelper](js-apis-inner-ability-dataAbilityHelper.md)               | DataAbilityHelper二级模块。<br/>**系统能力**：SystemCapability.Ability.AbilityRuntime.FAModel |
| PacMap   | [PacMap](js-apis-inner-ability-dataAbilityHelper.md#pacmap)               | PacMap二级模块。<br/>**系统能力**：SystemCapability.Ability.AbilityRuntime.FAModel |
| DataAbilityOperation   | [DataAbilityOperation](js-apis-inner-ability-dataAbilityOperation.md)               | DataAbilityOperation二级模块。<br/>**系统能力**：SystemCapability.Ability.AbilityRuntime.FAModel |
| DataAbilityResult   | [DataAbilityResult](js-apis-inner-ability-dataAbilityResult.md)               | DataAbilityResult二级模块。<br/>**系统能力**：SystemCapability.Ability.AbilityRuntime.FAModel |
| AbilityResult   | [AbilityResult](js-apis-inner-ability-abilityResult.md)               | AbilityResult二级模块。<br/>**系统能力**：SystemCapability.Ability.AbilityBase |
| ConnectOptions   | [ConnectOptions](js-apis-inner-ability-connectOptions.md)               | ConnectOptions二级模块。<br/>**系统能力**：SystemCapability.Ability.AbilityRuntime.Core |
| StartAbilityParameter   | [StartAbilityParameter](js-apis-inner-ability-startAbilityParameter.md)               | StartAbilityParameter二级模块。<br/>**系统能力**：SystemCapability.Ability.AbilityRuntime.FAModel |

**示例：**
```ts
import ability from '@ohos.ability.ability';

let dataAbilityHelper: ability.DataAbilityHelper;
let pacMap: ability.PacMap;
let dataAbilityOperation: ability.DataAbilityOperation;
let dataAbilityResult: ability.DataAbilityResult;
let abilityResult: ability.AbilityResult;
let connectOptions: ability.ConnectOptions;  
let startAbilityParameter: ability.StartAbilityParameter;
```