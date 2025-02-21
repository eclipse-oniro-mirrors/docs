# @ohos.app.ability.AbilityConstant (AbilityConstant)

The **AbilityConstant** module defines the UIAbility-related enums, including the initial launch reasons, reasons for the last exit, ability continuation results, and window modes.

> **NOTE**
> 
> - The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> 
> - The APIs of this module can be used only in the stage model.

## Modules to Import

```ts
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
```

## AbilityConstant.LaunchParam

Defines the parameters for starting an ability. The parameter values are automatically passed in by the system when the ability is started. You do not need to change the values.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name| Type| Read-only| Mandatory| Description|
| -------- | -------- | -------- | -------- | -------- |
| launchReason | [LaunchReason](#abilityconstantlaunchreason)| No| Yes| Ability launch reason, which is an enumerated type.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| lastExitReason | [LastExitReason](#abilityconstantlastexitreason) | No| Yes| Reason for the last exit, which is an enumerated type.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|

## AbilityConstant.LaunchReason

Enumerates the initial ability launch reasons. You can use it together with the value of **launchParam.launchReason** in [onCreate(want, launchParam)](js-apis-app-ability-uiAbility.md#uiabilityoncreate) of the UIAbility to complete different operations.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name                         | Value  | Description                                                        |
| ----------------------------- | ---- | ------------------------------------------------------------ |
| UNKNOWN          | 0    | Unknown reason.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| START_ABILITY          | 1    | The ability is started by calling [startAbility](js-apis-inner-application-uiAbilityContext.md#uiabilitycontextstartability).<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| CALL | 2    | The ability is started by calling [startAbilityByCall](js-apis-inner-application-uiAbilityContext.md#uiabilitycontextstartabilitybycall).<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| CONTINUATION           | 3    | The ability is started by means of cross-device migration.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| APP_RECOVERY           | 4    | The ability is automatically started when the application is restored from a fault.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| SHARE<sup>10+</sup>           | 5    | The ability is started by means of atomic service sharing.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| AUTO_STARTUP<sup>11+</sup>           | 8    | The ability is automatically started upon system boot.|
| INSIGHT_INTENT<sup>11+</sup>           | 9    | The ability is started by the InsightIntent framework.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import Want from '@ohos.app.ability.Want';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';

class MyAbility extends UIAbility {
    onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
        if (launchParam.launchReason === AbilityConstant.LaunchReason.START_ABILITY) {
            console.log('The ability has been started by the way of startAbility.');
        }
    }
}
```

## AbilityConstant.LastExitReason

Enumerates the reasons for the last exit. You can use it together with the value of **launchParam.lastExitReason** in [onCreate(want, launchParam)](js-apis-app-ability-uiAbility.md#uiabilityoncreate) of the UIAbility to complete different operations.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name                         | Value  | Description                                                        |
| ----------------------------- | ---- | ------------------------------------------------------------ |
| UNKNOWN          | 0    | Unknown reason.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| ABILITY_NOT_RESPONDING<sup>(deprecated)</sup> | 1    | The ability does not respond.<br>**NOTE**<br>This enum is supported since API version 9 and deprecated since API version 10. You are advised to use **APP_FREEZE**.|
| NORMAL | 2    | The ability exits normally because the user closes the application.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| CPP_CRASH<sup>10+</sup>  | 3    | The ability exits due to abnormal signals on the local host.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| JS_ERROR<sup>10+</sup>  | 4    | The ability exits due to a JS_ERROR fault triggered when an application has a JS syntax error that is not captured by developers.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| APP_FREEZE<sup>10+</sup>  | 5    | The ability exits because watchdog detects that the application is frozen.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| PERFORMANCE_CONTROL<sup>10+</sup>  | 6    | The ability exits due to system performance problems, for example, insufficient device memory.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| RESOURCE_CONTROL<sup>10+</sup>  | 7    | The ability exits because the system resource usage (CPU, I/O, or memory usage) exceeds the upper limit.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| UPGRADE<sup>10+</sup>  | 8    | The ability exits due to an update.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import Want from '@ohos.app.ability.Want';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';

class MyAbility extends UIAbility {
    onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
        if (launchParam.lastExitReason === AbilityConstant.LastExitReason.APP_FREEZE) {
            console.log('The ability has exit last because the ability was not responding.');
        }
    }
}
```

## AbilityConstant.OnContinueResult 

Enumerates the ability continuation results. You can use it together with [onContinue(wantParam)](js-apis-app-ability-uiAbility.md#uiabilityoncontinue) of the UIAbility to complete different operations.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name                         | Value  | Description                                                        |
| ----------------------------- | ---- | ------------------------------------------------------------ |
| AGREE           | 0    | The ability continuation is accepted.|
| REJECT           | 1    | The ability continuation is rejected. If the application is abnormal in [onContinue](js-apis-app-ability-uiAbility.md#uiabilityoncontinue), which results in abnormal display during data restoration, this error code is returned.|
| MISMATCH  | 2    | The version does not match. The application on the initiator can obtain the version of the target application from [onContinue](js-apis-app-ability-uiAbility.md#uiabilityoncontinue). If the ability continuation cannot be performed due to version mismatch, this error code is returned.|

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';

class MyAbility extends UIAbility {
    onContinue(wantParam: Record<string, Object>) {
        return AbilityConstant.OnContinueResult.AGREE;
    }
}
```

## AbilityConstant.MemoryLevel

Enumerates the memory levels. You can use it in [onMemoryLevel(level)](js-apis-app-ability-ability.md#abilityonmemorylevel) of the UIAbility to complete different operations.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name                        | Value| Description               |
| ---                         | --- | ---           |
| MEMORY_LEVEL_MODERATE       | 0   | Moderate memory usage.|
| MEMORY_LEVEL_LOW            | 1   | Low memory usage.  |
| MEMORY_LEVEL_CRITICAL       | 2   | High memory usage.  |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';

class MyAbility extends UIAbility {
    onMemoryLevel(level: AbilityConstant.MemoryLevel) {
        if (level === AbilityConstant.MemoryLevel.MEMORY_LEVEL_CRITICAL) {
            console.log('The memory of device is critical, please release some memory.');
        }
    }
}
```

## AbilityConstant.OnSaveResult

Enumerates the result types for the operation of saving application data. You can use it in [onSaveState(reason, wantParam)](js-apis-app-ability-uiAbility.md#uiabilityonsavestate) of the UIAbility to complete different operations.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name                         | Value  | Description                                                        |
| ----------------------------- | ---- | ------------------------------------------------------------ |
| ALL_AGREE           | 0    | Always agreed to save the status.|
| CONTINUATION_REJECT           | 1    | Rejected to save the status in continuation.|
| CONTINUATION_MISMATCH  | 2    | Continuation mismatch.|
| RECOVERY_AGREE           | 3    | Agreed to restore the saved status.|
| RECOVERY_REJECT  | 4    | Rejected to restore the saved status.|
| ALL_REJECT  | 5    | Always rejected to save the status.|

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';

class MyAbility extends UIAbility {
    onSaveState(reason: AbilityConstant.StateType, wantParam: Record<string, Object>) {
        return AbilityConstant.OnSaveResult.ALL_AGREE;
    }
}
```

## AbilityConstant.StateType

Enumerates the scenarios for saving application data. You can use it in [onSaveState(reason, wantParam)](js-apis-app-ability-uiAbility.md#uiabilityonsavestate) of the UIAbility to complete different operations.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name                         | Value  | Description                                                        |
| ----------------------------- | ---- | ------------------------------------------------------------ |
| CONTINUATION           | 0    | Saving the status in continuation.|
| APP_RECOVERY           | 1    | Saving the status in application recovery.|

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';

class MyAbility extends UIAbility {
    onSaveState(reason: AbilityConstant.StateType, wantParam: Record<string, Object>) {
        if (reason === AbilityConstant.StateType.CONTINUATION) {
            console.log('Save the ability data when the ability continuation.');
        } 
        return AbilityConstant.OnSaveResult.ALL_AGREE;
    }
}
```

## AbilityConstant.ContinueState<sup>10+</sup>

Enumerates the mission continuation states of the application. It is used in the [setMissionContinueState](js-apis-inner-application-uiAbilityContext.md#uiabilitycontextsetmissioncontinuestate10) API of [UIAbilityContext](js-apis-inner-application-uiAbilityContext.md).

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name          | Value      | Description                                                        |
| ------------- | --------- | ------------------------------------------------------------ |
| ACTIVE        | 0         | Mission continuation is activated for the current application.                             |
| INACTIVE      | 1         | Mission continuation is not activated for the current application.                           |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import Want from '@ohos.app.ability.Want';
import { BusinessError } from '@ohos.base';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';

class MyAbility extends UIAbility {
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam) {
    this.context.setMissionContinueState(AbilityConstant.ContinueState.INACTIVE, (result: BusinessError) => {
      console.info(`setMissionContinueState: ${JSON.stringify(result)}`);
    });
  }
}
```
