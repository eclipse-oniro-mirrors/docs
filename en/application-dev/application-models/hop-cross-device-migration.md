# Cross-Device Migration

## Overview

When the environment changes, for example, when a user goes outdoors or when a more appropriate device is detected, the user can migrate an ongoing task to another device for better experience. The application on the source device can automatically exit, depending on the setting. A typical cross-device migration scenario is as follows: You migrate a video playback task from a tablet to a smart TV. The video application on the tablet exits. From the perspective of application development, cross-device migration enables the UIAbility component running on device A to migrate to and keep running on device B. After the migration is complete, the UIAbility component on device A automatically exits (depending on the setting).

The core task of cross-device migration is to migrate the status (including page components and status variables) of an application to the target device so that users can have continuous application experience on that device. This means that operations performed by a user on one device can be quickly switched and seamlessly connected in the same application on another device.

Cross-device migration supports the following features:

- Saving and restoring custom data

- Saving and restoring page routing information and page component status data

- Checking application compatibility

- Dynamically setting the migration state (**ACTIVE** by default)

  For example, for an editing application, only the text editing page needs to be migrated to the target device. In this case, you can call [setMissionContinueState](../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md#uiabilitycontextsetmissioncontinuestate10) for precise control.

- Determining whether to restore the page stack (restored by default)

 If an application wants to customize the page to be displayed after being migrated to the target device, you can use [SUPPORT_CONTINUE_PAGE_STACK_KEY](../reference/apis-ability-kit/js-apis-app-ability-wantConstant.md#wantconstantparams) for precise control.

- Determining whether to exit the application on the source device after a successful migration (application exit by default)

 You can use [SUPPORT_CONTINUE_SOURCE_EXIT_KEY](../reference/apis-ability-kit/js-apis-app-ability-wantConstant.md#wantconstantparams) for precise control.

  > **NOTE**
  >
  > You only need to develop an application with the migration capabilities. System applications will trigger cross-device migration.


## Working Principles

![hop-cross-device-migration](figures/hop-cross-device-migration.png)

1. On the source device, the UIAbility uses the [onContinue()](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityoncontinue) callback to save service data to be continued. For example, to complete cross-device migration, a browser application uses the [onContinue()](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityoncontinue) callback to save service data such as the page URL. The system automatically saves the page status, such as the current browsing progress.
2. The distributed framework provides a mechanism for saving and restoring application UI, page stacks, and service data across devices. It sends the data from the source device to the target device.
3. On the target device, the same UIAbility uses the [onCreate()](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityoncreate) callback (in the case of cold start) or [onNewWant()](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityonnewwant) callback (in the case of hot start) to restore the service data.

## Cross-Device Migration Process

The following figure shows the cross-device migration process when a migration request is initiated from the migration entry of the peer device.

![hop-cross-device-migration](figures/hop-cross-device-migration7.png)



## Constraints

- Cross-device migration must be performed between the same UIAbility component. In other words, **bundleName**, **abilityName**, and **signature** of the component on the two devices must be the same.
- For better user experience, the data to be transmitted using the **wantParam** parameter must be less than 100 KB.

## How to Develop

1. Configure the **continuable** tag under **abilities** in the [module.json5 file](../quick-start/module-configuration-file.md).

   ```json
   {
     "module": {
       // ...
       "abilities": [
         {
           // ...
           "continuable": true, // Configure the UIAbility to support migration.
         }
       ]
     }
   }
   ```

   > **NOTE**
   >
   > Configure the application launch type. For details, see [UIAbility Component Launch Type](uiability-launch-type.md).

2. Implement [onContinue()](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityoncontinue) in the UIAbility on the source device.

   When a migration is triggered for the UIAbility, [onContinue()](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityoncontinue) is called on the source device. You can use either synchronous or asynchronous mode to save the data in this method to implement application compatibility check and migration decision.

   - Saving data to migrate: You can save the data to migrate in key-value pairs in **wantParam**.
   - Checking application compatibility: You can obtain the application version on the target device from **wantParam.version** in the [onContinue()](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityoncontinue) callback and compare it with the application version on the source device.
   - Making a migration decision: You can determine whether migration is supported based on the return value of [onContinue()](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityoncontinue). For details about the return values, see [AbilityConstant.OnContinueResult](../reference/apis-ability-kit/js-apis-app-ability-abilityConstant.md#abilityconstantoncontinueresult).

   ```ts
   import AbilityConstant from '@ohos.app.ability.AbilityConstant';
   import hilog from '@ohos.hilog';
   import UIAbility from '@ohos.app.ability.UIAbility';
   
   const TAG: string = '[MigrationAbility]';
   const DOMAIN_NUMBER: number = 0xFF00;
   
   export default class MigrationAbility extends UIAbility {
     onContinue(wantParam: Record<string, Object>):AbilityConstant.OnContinueResult {
       let version = wantParam.version;
       let targetDevice = wantParam.targetDevice;
       hilog.info(DOMAIN_NUMBER, TAG, `onContinue version = ${version}, targetDevice: ${targetDevice}`); // Prepare data to migrate.
   
       // Obtain the application version on the source device.
       let versionSrc: number = -1; // Enter the version number obtained.
   
       // Compatibility verification
       if (version !== versionSrc) {
         // Return MISMATCH when the compatibility check fails.
         return AbilityConstant.OnContinueResult.MISMATCH;
       }
   
       // Save the data to migrate in the custom field (for example, data) of wantParam.
       const continueInput = 'Data to migrate';
       wantParam['data'] = continueInput;
   
       return AbilityConstant.OnContinueResult.AGREE;
     }
   }
   ```

3. On the source device, call APIs to restore data and load the UI. The APIs vary according to the cold or hot start mode in use. For the UIAbility on the target device, implement [onCreate()](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityoncreate) or [onNewWant()](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityonnewwant) to restore the data.
   

In the stage model, applications with different launch types can call different APIs to restore data and load the UI, as shown below.

![hop-cross-device-migration](figures/hop-cross-device-migration8.png)

   - The **launchReason** parameter in the [onCreate()](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityoncreate) or [onNewWant()](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityonnewwant) callback specifies whether the launch is triggered by migration.
   - You can obtain the saved data from the **want** parameter.
   - After data restoration is complete, call **restoreWindowStage()** to trigger page restoration, including page stack information.

   ```ts
   import AbilityConstant from '@ohos.app.ability.AbilityConstant';
   import hilog from '@ohos.hilog';
   import UIAbility from '@ohos.app.ability.UIAbility';
   import type Want from '@ohos.app.ability.Want';
   
   const TAG: string = '[MigrationAbility]';
   const DOMAIN_NUMBER: number = 0xFF00;
   
   export default class MigrationAbility extends UIAbility {
     storage : LocalStorage = new LocalStorage();
   
     onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
       hilog.info(DOMAIN_NUMBER, TAG, '%{public}s', 'Ability onCreate');
       if (launchParam.launchReason === AbilityConstant.LaunchReason.CONTINUATION) {
         // Restore the saved data from want.parameters.
         let continueInput = '';
         if (want.parameters !== undefined) {
           continueInput = JSON.stringify(want.parameters.data);
           hilog.info(DOMAIN_NUMBER, TAG, `continue input ${continueInput}`);
         }
         // Trigger page restoration.
         this.context.restoreWindowStage(this.storage);
       }
     }
   
     onNewWant(want: Want, launchParam: AbilityConstant.LaunchParam): void {
        hilog.info(DOMAIN_NUMBER, TAG, 'onNewWant');
        if (launchParam.launchReason === AbilityConstant.LaunchReason.CONTINUATION) {
          // Restore the saved data from want.parameters.
          let continueInput = '';
          if (want.parameters !== undefined) {
            continueInput = JSON.stringify(want.parameters.data);
            hilog.info(DOMAIN_NUMBER, TAG, `continue input ${continueInput}`);
          }
          // Trigger page restoration. 
          this.context.restoreWindowStage(this.storage);
        }
      }
   }
   ```

## Configuring Optional Migration Features

### Dynamically Setting the Migration State

Since API version 10, you can dynamically set the migration state. Specifically, you can enable or disable migration as required by calling [setMissionContinueState()](../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md#uiabilitycontextsetmissioncontinuestate10). By default, **ACTIVE** is set for an application, indicating that migration is enabled.

**Time for Setting the Migration State**

The change of the migration state can be implemented based on service requirements. Typical methods are as follows:

Call the API in the [onCreate()](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityoncreate) callback of the UIAbility to set the migration state when the application is created.

```ts
// MigrationAbility.ets
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import hilog from '@ohos.hilog';
import UIAbility from '@ohos.app.ability.UIAbility';
import type Want from '@ohos.app.ability.Want';

const TAG: string = '[MigrationAbility]';
const DOMAIN_NUMBER: number = 0xFF00;

export default class MigrationAbility extends UIAbility {
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    // ...
    this.context.setMissionContinueState(AbilityConstant.ContinueState.INACTIVE, (result) => {
      hilog.info(DOMAIN_NUMBER, TAG, `setMissionContinueState: ${JSON.stringify(result)}`);
    });
    // ...
  }
}
```

Call the API in the **onPageShow()** callback of the page to set the migration state when a single page is displayed.

```ts
// Page_MigrationAbilityFirst.ets
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import common from '@ohos.app.ability.common';
import hilog from '@ohos.hilog';

const TAG: string = '[MigrationAbility]';
const DOMAIN_NUMBER: number = 0xFF00;

@Entry
@Component
struct Page_MigrationAbilityFirst {
  private context = getContext(this) as common.UIAbilityContext;
  build() {
    // ...
  }
  // ...
  onPageShow(){
    // When the page is displayed, set the migration state to ACTIVE.
    this.context.setMissionContinueState(AbilityConstant.ContinueState.ACTIVE, (result) => {
      hilog.info(DOMAIN_NUMBER, TAG, '%{public}s', `setMissionContinueState ACTIVE result: ${JSON.stringify(result)}`);
    });
  }
}
```

Set the migration state in the event of a component.

```ts
// Page_MigrationAbilityFirst.ets
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import common from '@ohos.app.ability.common';
import hilog from '@ohos.hilog';
import promptAction from '@ohos.promptAction';

const TAG: string = '[MigrationAbility]';
const DOMAIN_NUMBER: number = 0xFF00;

@Entry
@Component
struct Page_MigrationAbilityFirst {
  private context = getContext(this) as common.UIAbilityContext;
  build() {
    // ...
    Button() {
      // ...
    }
    .onClick(()=>{
      // When the button is clicked, set the migration state to ACTIVE.
      this.context.setMissionContinueState(AbilityConstant.ContinueState.ACTIVE, (result) => {
        hilog.info(DOMAIN_NUMBER, TAG, '%{public}s', `setMissionContinueState ACTIVE result: ${JSON.stringify(result)}`);
      });
    })
  }
}
```

### Ensuring Migration Continuity

During UI page loading, the application on the target device may have executed the command to set its own migration state (for example, set the state to **INACTIVE** in [onCreate()](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityoncreate) during cold start or to **INACTIVE** during hot start since the application has opened a page that cannot be migrated). To ensure a migration back to the source device, you must set the migration state to **ACTIVE** in [onCreate()](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityoncreate) or [onNewWant()](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityonnewwant).

```ts
// MigrationAbility.ets
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import hilog from '@ohos.hilog';
import UIAbility from '@ohos.app.ability.UIAbility';
import type Want from '@ohos.app.ability.Want';

const TAG: string = '[MigrationAbility]';
const DOMAIN_NUMBER: number = 0xFF00;

export default class MigrationAbility extends UIAbility {
  // ...
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    // ...
    // Set the migration state to ACTIVE when the launch is caused by migration. This setting copes with cold start.
    if (launchParam.launchReason == AbilityConstant.LaunchReason.CONTINUATION) {
      this.context.setMissionContinueState(AbilityConstant.ContinueState.ACTIVE, (result) => {
        hilog.info(`setMissionContinueState ACTIVE result: ${JSON.stringify(result)}`);
      });
    }
  }
  
  onNewWant(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    // ...
    // Set the migration state to ACTIVE when the launch is caused by migration. This setting copes with hot start.
    if (launchParam.launchReason == AbilityConstant.LaunchReason.CONTINUATION) {
      this.context.setMissionContinueState(AbilityConstant.ContinueState.ACTIVE, (result) => {
        hilog.info(DOMAIN_NUMBER, TAG, `setMissionContinueState ACTIVE result: ${JSON.stringify(result)}`);
      });
    }
  }
  // ...
}
```

### Migrating the Page Stack on Demand

Configure whether to restore the page stack. By default, the page stack is restored. If an application does not want to use the page stack restored by the system, you can set the page to be displayed on the target device in **onWindowStageRestore()**. For details about the configuration, see [SUPPORT_CONTINUE_PAGE_STACK_KEY](../reference/apis-ability-kit/js-apis-app-ability-wantConstant.md#wantconstantparams).

The index and second routes exist in the page stack of the application on the source device. However, the application on the target device wants to display a specified page, rather than that on the source device.

Example: A UIAbility does not want automatically restored page stack information.

```ts
// MigrationAbility.ets
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import hilog from '@ohos.hilog';
import UIAbility from '@ohos.app.ability.UIAbility';
import wantConstant from '@ohos.app.ability.wantConstant';
import type window from '@ohos.window';

const TAG: string = '[MigrationAbility]';
const DOMAIN_NUMBER: number = 0xFF00;

export default class MigrationAbility extends UIAbility {
  // ...
  onContinue(wantParam: Record<string, Object>):AbilityConstant.OnContinueResult {
    hilog.info(DOMAIN_NUMBER, TAG, `onContinue version = ${wantParam.version}, targetDevice: ${wantParam.targetDevice}`);
    wantParam[wantConstant.Params.SUPPORT_CONTINUE_PAGE_STACK_KEY] = false;
    return AbilityConstant.OnContinueResult.AGREE;
  }

  onWindowStageRestore(windowStage: window.WindowStage) : void {
    // Set the page to be displayed after the migration.
    windowStage.loadContent('pages/page_migrationability/Page_MigrationAbilityThird', (err, data) => {
      if (err.code) {
        hilog.error(DOMAIN_NUMBER, TAG, 'Failed to load the content. Cause: %{public}s', JSON.stringify(err) ?? '');
        return;
      }
    });
  }
}
```

### Exiting the Application on Demand

Configure whether to exit the application on the source device after a successful migration. By default, the application on the source device exits by default. If you do not want the application on the source device to automatically exit after a successful migration, set the [SUPPORT_CONTINUE_SOURCE_EXIT_KEY](../reference/apis-ability-kit/js-apis-app-ability-wantConstant.md#wantconstantparams) parameter.

Example: A UIAbility on the source device does not exit after a successful migration.

```ts
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import hilog from '@ohos.hilog';
import UIAbility from '@ohos.app.ability.UIAbility';
import wantConstant from '@ohos.app.ability.wantConstant';

const TAG: string = '[MigrationAbility]';
const DOMAIN_NUMBER: number = 0xFF00;

export default class MigrationAbility extends UIAbility {
  // ...
  onContinue(wantParam: Record<string, Object>):AbilityConstant.OnContinueResult {
    hilog.info(DOMAIN_NUMBER, TAG, `onContinue version = ${wantParam.version}, targetDevice: ${wantParam.targetDevice}`);
    wantParam[wantConstant.Params.SUPPORT_CONTINUE_SOURCE_EXIT_KEY] = false;
    return AbilityConstant.OnContinueResult.AGREE;
  }
}
```

## Cross-Device Data Migration
Three data migration modes are provided. You can select them as required.
  > **NOTE**
  >
  > Through the configuration of **restoreId**, certain ArkUI components can be restored to a given state on the target device after migration. For details, see [restoreId](../../application-dev/reference/apis-arkui/arkui-ts/ts-universal-attributes-restoreId.md).
  >
  > If distributed objects and files need to be migrated, you must
  > 1. Declare the **ohos.permission.DISTRIBUTED_DATASYNC** permission. For details, see [Declaring Permissions](../security/AccessToken/declare-permissions.md).
  > 2. Display a dialog box to ask for authorization from the user when the application is started for the first time. For details, see [Requesting User Authorization](../security/AccessToken/request-user-authorization.md).

### Using wantParam for Data Migration

If the size of the data to migrate is less than 100 KB, you can add fields to **wantParam** for data migration. An example is as follows:

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import Want from '@ohos.app.ability.Want';

const TAG: string = '[MigrationAbility]';
const DOMAIN_NUMBER: number = 0xFF00;

export default class MigrationAbility extends UIAbility {
  // Save the data on the source device.
  onContinue(wantParam: Record<string, Object>):AbilityConstant.OnContinueResult {
    // Save the data to migrate in the custom field (for example, data) of wantParam.
    const continueInput = 'Data to migrate';
    wantParam['data'] = continueInput;
    return AbilityConstant.OnContinueResult.AGREE;
  }

  // Restore the data on the target device.
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    if (launchParam.launchReason === AbilityConstant.LaunchReason.CONTINUATION) {
      // Obtain the data saved.
      let continueInput = '';
      if (want.parameters !== undefined) {
        continueInput = JSON.stringify(want.parameters.data);
        hilog.info(DOMAIN_NUMBER, TAG, `continue input ${continueInput}`);
      }
      // Trigger page restoration.
      this.context.restoreWindowStage(this.storage);
    }
  }

  onNewWant(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    if (launchParam.launchReason == AbilityConstant.LaunchReason.CONTINUATION) {
      let continueInput = '';
      if (want.parameters !== undefined) {
        continueInput = JSON.stringify(want.parameters.data);
        hilog.info(DOMAIN_NUMBER, TAG, `continue input ${JSON.stringify(continueInput)}`);
      }
      // Trigger page restoration.
      this.context.restoreWindowStage(this.storage);
    }
  }
}
```
### Using Distributed Data Objects for Data Migration

If the size of the data to migrate is greater than 100 KB, you can use a [distributed data object](../../application-dev/reference/apis-arkdata/js-apis-data-distributedobject.md) for data migration.

1. First, create a distributed [data object](../../application-dev/reference/apis-arkdata/js-apis-data-distributedobject.md#dataobject) in the **onContinue()** callback for the application on the source device, fill the data to migrate into this object, and send the generated session ID to the peer through **want**.
2. During data restoration initiated by **onCreate()** or **onNewWant()**, the peer reads the session ID from **want** and restore data through the distributed object.

For details, see [Cross-Device Synchronization of Distributed Data Objects](../../application-dev/database/data-sync-of-distributed-data-object.md).

### Using Distributed Files For Data Migration
If the size of the data to migrate is greater than 100 KB, you can also use a distributed file for data migration. Compared with distributed data objects, distributed files are more suitable when files are to be transmitted. After data is written to the distributed file path on the source device, the application started on the target device can access the file in this path after the migration.

For details, see [Accessing Files Across Devices](../../application-dev/file-management/file-access-across-devices.md).

## Verification Guide

A mission center demo is provided for you to verify the migration capability of your application. The following walks you through on how to verify migration by using the demo.

### Compiling and Installing the Demo

#### Environment Configuration

[Switch to the full SDK](../../application-dev/faqs/full-sdk-switch-guide.md) in DevEco Studio. This is because the mission center uses the system API [@ohos.distributedDeviceManager](../../application-dev/reference/apis-distributedservice-kit/js-apis-distributedDeviceManager.md), which is not provided in the public SDK.

> **NOTE**
>
> The screenshots in this section are for reference only. The DevEco Studio and SDK versions in use prevail.

#### Demo Download

Download the mission center demo from [Sample Code](https://gitee.com/openharmony/ability_dmsfwk/tree/master/services/dtbschedmgr/test/missionCenterDemo/dmsDemo/entry/src/main).

#### Building Project Files

1. Create an empty project and replace the corresponding folders with the downloaded files.

   ![hop-cross-device-migration](figures/hop-cross-device-migration1.png)

2. Complete the signature, build, and installation.

   The default signature permission provided by the automatic signature template of DevEco Studio is normal. The mission center demo requires the **ohos.permission.MANAGE_MISSIONS** permission, which is at the system_core level. Therefore, you must escalate the permission to the system_core level. ​Specifically, change **"apl":"normal"** to **"apl":"system_core"** in the **UnsignedReleasedProfileTemplate.json** file in **openharmony\*apiVersion*\toolchains\lib**. Then sign the files as follows:

   1. Choose **File > Project Structure**.

      ![hop-cross-device-migration](figures/hop-cross-device-migration2.png)

   2. Click **Signing Configs** and click **OK**.

      ![hop-cross-device-migration](figures/hop-cross-device-migration3.png)

   3. Connect to the developer board and run the demo.

### Device Networking

1. Open the calculators of devices A and B.
2. Click the arrow in the upper right corner to select device B.
3. Select a trusted device on device B. The PIN is displayed.
4. Enter the PIN on device A.
5. Verify the networking. Enter a number on device A. If the number is displayed on device B, the networking is successful.

### Initiation Migration

1. Open your application on device B, and open the mission center demo on device A. The name of device A (Local: OpenHarmony 3.2) and the name of device B (OpenHarmony 3.2) are displayed on device A.

   ![hop-cross-device-migration](figures/hop-cross-device-migration4.png)

2. Click the name of device B. The application of device B is displayed.

   ![hop-cross-device-migration](figures/hop-cross-device-migration5.png)

3. Drag the application to the name of device A. The application on device A is started, and the application on device B exits.

   ![hop-cross-device-migration](figures/hop-cross-device-migration6.png)

