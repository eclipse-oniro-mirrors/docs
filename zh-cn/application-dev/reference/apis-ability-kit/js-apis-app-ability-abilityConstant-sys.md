# @ohos.app.ability.AbilityConstant (AbilityConstant)(系统接口)

提供UIAbility中窗口类型的枚举。

> **说明：**
> 
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>
> 本模块接口仅可在Stage模型下使用。
>
> 当前页面仅包含本模块的系统接口，其他公开接口参见[@ohos.app.ability.AbilityConstant (AbilityConstant)](js-apis-app-ability-abilityConstant.md)。

## 导入模块

```ts
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
```

## AbilityConstant.WindowMode

启动Ability时的窗口模式，该类型为枚举，可配合startAbility使用指定启动Ability的窗口模式。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口。

| 名称                        | 值 | 说明                 |
| ---                         | --- | ---                  |
| WINDOW_MODE_UNDEFINED       | 0   | 未定义窗口模式。       |
| WINDOW_MODE_FULLSCREEN      | 1   | 全屏模式。            |
| WINDOW_MODE_SPLIT_PRIMARY   | 100 | 屏幕如果是水平方向表示左分屏，屏幕如果是竖直方向表示上分屏。   |
| WINDOW_MODE_SPLIT_SECONDARY | 101 | 屏幕如果是水平方向表示右分屏，屏幕如果是竖直方向表示下分屏。   |
| WINDOW_MODE_FLOATING        | 102 | 自由悬浮形式窗口模式。 |

**示例：**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import StartOptions from '@ohos.app.ability.StartOptions';
import Want from '@ohos.app.ability.Want';
import { BusinessError } from '@ohos.base';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';

let want: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};
let option: StartOptions = {
  windowMode: AbilityConstant.WindowMode.WINDOW_MODE_FULLSCREEN
};

// 确保从上下文获取到context
class MyAbility extends UIAbility {
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
    this.context.startAbility(want, option).then(()=>{
      console.log('Succeed to start ability.');
    }).catch((error: BusinessError)=>{
      console.error('Failed to start ability with error: ${JSON.stringify(error)}');
    });
  }
}
```
