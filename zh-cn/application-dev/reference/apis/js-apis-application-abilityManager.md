# @ohos.application.abilityManager (AbilityManager)

AbilityManager模块提供对Ability相关信息和状态信息进行获取、新增、修改等能力。

> **说明：**
>
> 本模块首批接口从API version 8开始支持，从API version 9废弃，替换模块为[@ohos.app.ability.abilityManager](js-apis-app-ability-abilityManager.md)。后续版本的新增接口，采用上角标单独标记接口的起始版本。  
> 本模块接口均为系统接口，三方应用不支持调用。


## 导入模块

```ts
import AbilityManager from '@ohos.application.abilityManager';
```

## AbilityState

Ability的状态信息。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

**系统API**: 此接口为系统接口，三方应用不支持调用。

| 名称 | 值 | 说明 | 
| -------- | -------- | -------- |
| INITIAL | 0 | 表示ability为initial状态。| 
| FOREGROUND | 9 | 表示ability为foreground状态。  | 
| BACKGROUND | 10 | 表示ability为background状态。  | 
| FOREGROUNDING | 11 | 表示ability为foregrounding状态。  | 
| BACKGROUNDING | 12 | 表示ability为backgrounding状态。  | 

## updateConfiguration

updateConfiguration(config: Configuration, callback: AsyncCallback\<void>): void

通过修改配置来更新配置（callback形式）。

**需要权限**: ohos.permission.UPDATE_CONFIGURATION

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core
 
**参数**：

| 参数名        | 类型                                       | 必填   | 说明             |
| --------- | ---------------------------------------- | ---- | -------------- |
| config    | [Configuration](js-apis-application-configuration.md)   | 是    | 新的配置项。 |
| callback  | AsyncCallback\<void>                   | 是    | 被指定的回调方法。      |

**示例**：

```ts
import abilitymanager from '@ohos.application.abilityManager';

let config = {
  language: 'chinese' 
};

abilitymanager.updateConfiguration(config, () => {
    console.log('------------ updateConfiguration -----------');
})
```

## updateConfiguration

updateConfiguration(config: Configuration): Promise\<void>

通过修改配置来更新配置（Promise形式）。

**需要权限**: ohos.permission.UPDATE_CONFIGURATION

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

**参数**：

| 参数名        | 类型                                       | 必填   | 说明             |
| --------- | ---------------------------------------- | ---- | -------------- |
| config    | [Configuration](js-apis-application-configuration.md)   | 是    | 新的配置项。 |

**返回值：**

| 类型                                       | 说明      |
| ---------------------------------------- | ------- |
| Promise\<void> | 返回执行结果。 |

**示例**：

```ts
import abilitymanager from '@ohos.application.abilityManager';

let config = {
  language: 'chinese' 
};

abilitymanager.updateConfiguration(config).then(() => {
  console.log('updateConfiguration success');
}).catch((err) => {
  console.log('updateConfiguration fail');
})
```

## getAbilityRunningInfos

getAbilityRunningInfos(callback: AsyncCallback\<Array\<AbilityRunningInfo>>): void

获取Ability运行相关信息（callback形式）。

**需要权限**: ohos.permission.GET_RUNNING_INFO

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

**参数**：

| 参数名        | 类型                                       | 必填   | 说明             |
| --------- | ---------------------------------------- | ---- | -------------- |
| callback  | AsyncCallback\<Array\<[AbilityRunningInfo](js-apis-inner-application-abilityRunningInfo.md)>>  | 是    | 被指定的回调方法。      |

**示例**：

```ts
import abilityManager from '@ohos.application.abilityManager';
import { BusinessError } from '@ohos.base';

abilityManager.getAbilityRunningInfos((err: BusinessError, data) => { 
    console.log(`getAbilityRunningInfos err: ${err}, data: ${JSON.stringify(data)}`);
});
```

## getAbilityRunningInfos

getAbilityRunningInfos(): Promise\<Array\<AbilityRunningInfo>>

获取Ability运行相关信息（Promise形式）。

**需要权限**: ohos.permission.GET_RUNNING_INFO

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

| 类型                                       | 说明      |
| ---------------------------------------- | ------- |
| Promise\<Array\<[AbilityRunningInfo](js-apis-inner-application-abilityRunningInfo.md)>> | 返回执行结果。 |

**示例**：

```ts
import abilityManager from '@ohos.application.abilityManager';
import { BusinessError } from '@ohos.base';

abilityManager.getAbilityRunningInfos().then((data) => {
    console.log(`getAbilityRunningInfos  data: ${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
  console.error(`getAbilityRunningInfos err: ${JSON.stringify(err)}`);
});
```