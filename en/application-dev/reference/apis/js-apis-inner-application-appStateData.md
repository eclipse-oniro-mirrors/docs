# AppStateData

The **AppStateData** module defines the application state data, which can be obtained through [getForegroundApplications](js-apis-app-ability-appManager.md#appmanagergetforegroundapplications).

## Modules to Import

```ts
import appManager from '@ohos.app.ability.appManager';
```

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

| Name                     | Type  | Mandatory | Description      |
| ------------------------- | ------ | ---- | --------- |
| bundleName<sup>8+</sup>   | string | No  | Bundle name.|
| uid<sup>8+</sup>          | number | No  | User ID.  |
| state<sup>8+</sup>        | number | No  | Application state.|

**Example**
```ts
import appManager from "@ohos.application.appManager";

appManager.getForegroundApplications((error, data) => {
    for (let i = 0; i < data.length; i++) {
        let appStateData = data[i];
        console.info('appStateData.bundleName: ' + appStateData.bundleName);
        console.info('appStateData.uid: ' + appStateData.uid);
        console.info('appStateData.state: ' + appStateData.state);
    }
});
```

