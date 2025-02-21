# AbilityRunningInfo (System API)

The **AbilityRunningInfo** module defines the running information and state of an ability.

> **NOTE**
> 
> The initial APIs of this module are supported since API version 8. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> The APIs provided by this module are system APIs.

## Modules to Import

```ts
import abilitymanager from '@ohos.app.ability.abilityManager';
```

## Usage

The ability running information is obtained by calling [getAbilityRunningInfos](js-apis-app-ability-abilityManager-sys.md#getabilityrunninginfos) in **abilityManager**.

## Attributes

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

| Name| Type| Readable| Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| ability | ElementName | Yes| No| Information that matches an ability. |
| pid | number | Yes| No| Process ID.|
| uid | number | Yes| No| User ID. |
| processName | string | Yes| No| Process name. |
| startTime | number | Yes| No| Ability start time. |
| abilityState | [abilityManager.AbilityState](js-apis-app-ability-abilityManager-sys.md#abilitystate) | Yes| No| Ability state. |

**Example**

```ts
import abilitymanager from '@ohos.app.ability.abilityManager';

abilitymanager.getAbilityRunningInfos((error, data) => { 
    if (error) {
        console.error(`getAbilityRunningInfos fail, error: ${JSON.stringify(error)}`);
    } else {
        console.log(`getAbilityRunningInfos success, data: ${JSON.stringify(data)}`);
        for (let i = 0; i < data.length; i++) {
            let abilityinfo = data[i];
            console.log(`abilityinfo.ability: ${JSON.stringify(abilityinfo.ability)}`);
            console.log(`abilityinfo.pid: ${JSON.stringify(abilityinfo.pid)}`);
            console.log(`abilityinfo.uid: ${JSON.stringify(abilityinfo.uid)}`);
            console.log(`abilityinfo.processName: ${JSON.stringify(abilityinfo.processName)}`);
            console.log(`abilityinfo.startTime: ${JSON.stringify(abilityinfo.startTime)}`);
            console.log(`abilityinfo.abilityState: ${JSON.stringify(abilityinfo.abilityState)}`);
        }
    }
});
```
