# @ohos.app.ability.appRecovery (appRecovery)

appRecovery模块提供了应用在故障状态下的恢复能力。

> **说明：**
> 
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。当前版本仅支持单进程中单Ability的应用恢复。

## 导入模块
```ts
import appRecovery from '@ohos.app.ability.appRecovery';
```

## appRecovery.RestartFlag

应用重启标志，[enableAppRecovery](#apprecoveryenableapprecovery)接口重启选项参数，该类型为枚举。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

| 名称       | 值   | 说明       |
| ---------- | ---- | ---------- |
| ALWAYS_RESTART   | 0    | 总是重启应用。 |
| RESTART_WHEN_JS_CRASH   | 0x0001    | 发生JS_CRASH时重启应用。 |
| RESTART_WHEN_APP_FREEZE   | 0x0002    | 发生APP_FREEZE时重启应用。 |
| NO_RESTART           | 0xFFFF    | 总是不重启应用。 |

## appRecovery.SaveOccasionFlag

保存条件标志，[enableAppRecovery](#apprecoveryenableapprecovery)接口状态保存时的选项参数，该类型为枚举。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

| 名称                          | 值   | 说明                                                         |
| ----------------------------- | ---- | ------------------------------------------------------------ |
| SAVE_WHEN_ERROR            | 0x0001    | 当发生应用故障时保存。 |
| SAVE_WHEN_BACKGROUND            | 0x0002    | 当应用切入后台时保存。 |

## appRecovery.SaveModeFlag  

状态保存标志，[enableAppRecovery](#apprecoveryenableapprecovery)接口状态保存方式的参数，该类型为枚举。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

| 名称                          | 值   | 说明                                                         |
| ----------------------------- | ---- | ------------------------------------------------------------ |
| SAVE_WITH_FILE             | 0x0001    | 每次状态保存都会写入到本地文件缓存。 |
| SAVE_WITH_SHARED_MEMORY             | 0x0002    | 状态先保存在内存中，应用故障退出时写入到本地文件缓存。 |

## appRecovery.enableAppRecovery

enableAppRecovery(restart?: [RestartFlag](#apprecoveryrestartflag), saveOccasion?: [SaveOccasionFlag](#apprecoverysaveoccasionflag), saveMode?: [SaveModeFlag](#apprecoverysavemodeflag)) : void;

使能应用恢复功能，参数按顺序填入。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| restart | [RestartFlag](#apprecoveryrestartflag) | 否 | 枚举类型，发生对应故障时是否重启，默认为重启。 |
| saveOccasion | [SaveOccasionFlag](#apprecoverysaveoccasionflag) | 否 | 枚举类型，状态保存时机，默认为故障时保存。 |
| saveMode | [SaveModeFlag](#apprecoverysavemodeflag) | 否 | 枚举类型，状态保存方式， 默认为文件缓存。 |

**示例：**
    
```ts
import appRecovery from '@ohos.app.ability.appRecovery';
import AbilityStage from '@ohos.app.ability.AbilityStage';

export default class MyAbilityStage extends AbilityStage {
    onCreate() {
        appRecovery.enableAppRecovery(
            appRecovery.RestartFlag.ALWAYS_RESTART,
            appRecovery.SaveOccasionFlag.SAVE_WHEN_ERROR,
            appRecovery.SaveModeFlag.SAVE_WITH_FILE
        );
    }
}
```

## appRecovery.restartApp

restartApp(): void;

重启当前App进程，可以配合[errorManager](js-apis-app-ability-errorManager.md)相关接口使用。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core


**示例：**
    
```ts
import appRecovery from '@ohos.app.ability.appRecovery';
import errorManager from '@ohos.app.ability.errorManager';

let observer = {
    onUnhandledException(errorMsg) {
        console.log('onUnhandledException, errorMsg: ', errorMsg);
        appRecovery.restartApp();
    }
};

try {
    errorManager.on('error', observer);
} catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
}
```

## appRecovery.saveAppState

saveAppState(): boolean;

保存当前App状态，可以配合[errorManager](js-apis-app-ability-errorManager.md)相关接口使用

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| context | [UIAbilityContext](js-apis-inner-application-uiAbilityContext.md)| 否 | 需要保存状态的UIAbility所对应的context。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 保存成功与否。true：保存成功，false：保存失败。 |

**示例：**
    
```ts
import appRecovery from '@ohos.app.ability.appRecovery';
import errorManager from '@ohos.app.ability.errorManager';

let observer = {
    onUnhandledException(errorMsg) {
        console.log('onUnhandledException, errorMsg: ', errorMsg);
        appRecovery.saveAppState();
    }
};

try {
    errorManager.on('error', observer);
} catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
}
```
