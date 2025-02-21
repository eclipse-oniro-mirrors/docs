# Intra-Device Interaction Between UIAbility Components


UIAbility is the minimum unit that can be scheduled by the system. Redirection between functional modules in a device involves starting of specific UIAbility components, which belong to the same or a different application (for example, starting UIAbility of a third-party payment application).


This topic describes the UIAbility interaction modes in the following scenarios. For details about cross-device application component interaction, see [Inter-Device Application Component Interaction (Hopping)](inter-device-interaction-hop-overview.md).


- [Starting UIAbility in the Same Application](#starting-uiability-in-the-same-application)

- [Starting UIAbility in the Same Application and Obtaining the Return Result](#starting-uiability-in-the-same-application-and-obtaining-the-return-result)

- [Starting UIAbility of Another Application](#starting-uiability-of-another-application)

- [Starting UIAbility of Another Application and Obtaining the Return Result](#starting-uiability-of-another-application-and-obtaining-the-return-result)

- [Starting UIAbility with Window Mode Specified (for System Applications Only)](#starting-uiability-with-window-mode-specified-for-system-applications-only)

- [Starting a Specified Page of UIAbility](#starting-a-specified-page-of-uiability)

- [Using Call to Implement UIAbility Interaction (for System Applications Only)](#using-call-to-implement-uiability-interaction-for-system-applications-only)


## Starting UIAbility in the Same Application

This scenario is possible when an application contains multiple UIAbility components. For example, in a payment application, you may need to start the payment UIAbility from the entry UIAbility.

Assume that your application has two UIAbility components: EntryAbility and FuncAbility, either in the same module or different modules. To start FuncAbility from EntryAbility, proceed as follows:

1. In EntryAbility, call [startAbility()](../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md#uiabilitycontextstartability) and pass the [want](../reference/apis-ability-kit/js-apis-app-ability-want.md) parameter to start the UIAbility instance. In the **want** parameter, **bundleName** indicates the bundle name of the application to start; **abilityName** indicates the name of the UIAbility to start; **moduleName** is required only when the target UIAbility belongs to a different module from EntryAbility; **parameters** is used to carry custom information. For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](uiability-usage.md#obtaining-the-context-of-uiability).

   ```ts
   import common from '@ohos.app.ability.common';
   import Want from '@ohos.app.ability.Want';
   import { BusinessError } from '@ohos.base';
   import hilog from '@ohos.hilog';
   
   const TAG: string = '[Page_UIAbilityComponentsInteractive]';
   const DOMAIN_NUMBER: number = 0xFF00;
   
   @Entry
   @Component
   struct Page_UIAbilityComponentsInteractive {
     private context = getContext(this) as common.UIAbilityContext;
   
     build() {
       // ...
       Button()
         .onClick(() => {
	   // Context is a member of the ability object and is required for invoking inside a non-ability object.
           // Pass in the Context object.
           let wantInfo: Want = {
             deviceId: '', // An empty deviceId indicates the local device.
             bundleName: 'com.samples.myapplication',
             moduleName: 'entry', // moduleName is optional.
             abilityName: 'FuncAbilityA',
             parameters: { // Custom information.
               info: 'From the UIAbilityComponentsInteractive page of EntryAbility',
             },
           }
           // context is the UIAbilityContext of the initiator UIAbility.
           this.context.startAbility(wantInfo).then(() => {
             hilog.info(DOMAIN_NUMBER, TAG, 'startAbility success.');
           }).catch((error: BusinessError) => {
             hilog.error(DOMAIN_NUMBER, TAG, 'startAbility failed.');
           });
         })
     }
   }
   ```

2. In FuncAbility, use [onCreate()](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityoncreate) or [onNewWant()](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityonnewwant) to receive the parameters passed in by EntryAbility.

   ```ts
   import UIAbility from '@ohos.app.ability.UIAbility';
   import AbilityConstant from '@ohos.app.ability.AbilityConstant';
   import Want from '@ohos.app.ability.Want';

   export default class FuncAbility extends UIAbility {
     onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
       // Receive the parameters passed by the initiator UIAbility.
       let funcAbilityWant = want;
       let info = funcAbilityWant?.parameters?.info;
       // ...
     }
   }
   ```

   > **NOTE**
   >
   > In FuncAbility started, you can obtain the PID and bundle name of the UIAbility through **parameters** in the passed **want** parameter.

3. To stop the **UIAbility** instance after the FuncAbility service is not needed, call [terminateSelf()](../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md#uiabilitycontextterminateself) in FuncAbility.

   ```ts
   import common from '@ohos.app.ability.common';
   import hilog from '@ohos.hilog';
   
   const TAG: string = '[Page_UIAbilityComponentsInteractive]';
   const DOMAIN_NUMBER: number = 0xFF00;
   
   @Entry
   @Component
   struct Page_UIAbilityComponentsInteractive {
     build() {
       // ...
       Button()
         .onClick(() => {
           let context: common.UIAbilityContext = getContext(this) as common.UIAbilityContext; // UIAbilityContext
           // context is the UIAbilityContext of the UIAbility instance to stop.
           context.terminateSelf((err) => {
             if (err.code) {
               hilog.error(DOMAIN_NUMBER, TAG, `Failed to terminate Self. Code is ${err.code}, message is ${err.message}`);
               return;
             }
           });
         })
     }
   }
   ```

   > **NOTE**
   >
   > When [terminateSelf()](../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md#uiabilitycontextterminateself) is called to stop the **UIAbility** instance, the snapshot of the instance is retained by default. That is, the mission corresponding to the instance is still displayed in Recents. If you do not want to retain the snapshot, set **removeMissionAfterTerminate** under the [abilities](../quick-start/module-configuration-file.md#abilities) tag to **true** in the [module.json5 file](../quick-start/module-configuration-file.md) of the corresponding UIAbility.

4. To stop all UIAbility instances of the application, call [killAllProcesses()](../reference/apis-ability-kit/js-apis-inner-application-applicationContext.md#applicationcontextkillallprocesses) of [ApplicationContext](../reference/apis-ability-kit/js-apis-inner-application-applicationContext.md).


## Starting UIAbility in the Same Application and Obtaining the Return Result

When starting FuncAbility from EntryAbility, you may want the result to be returned after the FuncAbility service is finished. For example, after the sign-in operation is finished in the sign-in UIAbility of your application, you want the sign-in result to be returned to the entry UIAbility.

1. In EntryAbility, call [startAbilityForResult()](../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md#uiabilitycontextterminateselfwithresult) to start FuncAbility. Use **data** in the asynchronous callback to receive information returned after FuncAbility stops itself. For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](uiability-usage.md#obtaining-the-context-of-uiability).

   ```ts
   import common from '@ohos.app.ability.common';
   import hilog from '@ohos.hilog';
   import Want from '@ohos.app.ability.Want';
   import { BusinessError } from '@ohos.base';
   
   const TAG: string = '[Page_UIAbilityComponentsInteractive]';
   const DOMAIN_NUMBER: number = 0xFF00;
   
   @Entry
   @Component
   struct Page_UIAbilityComponentsInteractive {
     build() {
       Button()
         .onClick(() => {
           let context: common.UIAbilityContext = getContext(this) as common.UIAbilityContext; // UIAbilityContext
   
           let want: Want = {
             deviceId: '', // An empty deviceId indicates the local device.
             bundleName: 'com.samples.stagemodelabilitydevelop',
             moduleName: 'entry', // moduleName is optional.
             abilityName: 'FuncAbilityA',
             parameters: { // Custom information.
               info: 'From the UIAbilityComponentsInteractive page of EntryAbility',
             }
           };
           context.startAbilityForResult(want).then((data) => {
             // ...
           }).catch((err: BusinessError) => {
             hilog.error(DOMAIN_NUMBER, TAG, `Failed to start ability for result. Code is ${err.code}, message is ${err.message}`);
           });
         })
     }
   }
   ```

2. Call [terminateSelfWithResult()](../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md#uiabilitycontextterminateselfwithresult) to stop FuncAbility. Use the input parameter **abilityResult** to carry the information that FuncAbility needs to return to EntryAbility.

   ```ts
   import common from '@ohos.app.ability.common';
   import hilog from '@ohos.hilog';
   
   const TAG: string = '[Page_FuncAbilityA]';
   const DOMAIN_NUMBER: number = 0xFF00;
   
   @Entry
   @Component
   struct Page_FuncAbilityA {
     build() {
       Button()
         .onClick(() => {
           let context: common.UIAbilityContext = getContext(this) as common.UIAbilityContext; // UIAbilityContext
           const RESULT_CODE: number = 1001;
           let abilityResult: common.AbilityResult = {
             resultCode: RESULT_CODE,
             want: {
               bundleName: 'com.samples.stagemodelabilitydevelop',
               moduleName: 'entry', // moduleName is optional.
               abilityName: 'FuncAbilityB',
               parameters: {
                 info: 'From the Index page of FuncAbility',
               },
             },
           };
           context.terminateSelfWithResult(abilityResult, (err) => {
             if (err.code) {
               hilog.error(DOMAIN_NUMBER, TAG, `Failed to terminate self with result. Code is ${err.code}, message is ${err.message}`);
               return;
             }
           });
         })
     }
   }
   ```

3. After FuncAbility stops itself, EntryAbility uses [startAbilityForResult()](../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md#uiabilitycontextterminateselfwithresult) to receive the information returned by FuncAbility. The value of **RESULT_CODE** must be the same as that specified in the preceding step.

   ```ts
   import common from '@ohos.app.ability.common';
   import hilog from '@ohos.hilog';
   import Want from '@ohos.app.ability.Want';
   import { BusinessError } from '@ohos.base';
   import promptAction from '@ohos.promptAction';
   
   const TAG: string = '[EntryAbility]';
   const DOMAIN_NUMBER: number = 0xFF00;
   
   @Entry
   @Component
   struct Page_UIAbilityComponentsInteractive {
     build() {
       Button()
         .onClick(() => {
           let context: common.UIAbilityContext = getContext(this) as common.UIAbilityContext; // UIAbilityContext
           const RESULT_CODE: number = 1001;
   
           let want: Want = {
             deviceId: '', // An empty deviceId indicates the local device.
             bundleName: 'com.samples.stagemodelabilitydevelop',
             moduleName: 'entry', // moduleName is optional.
             abilityName: 'FuncAbilityA',
             parameters: { // Custom information.
               info: 'From the UIAbilityComponentsInteractive page of EntryAbility',
             }
           };
           context.startAbilityForResult(want).then((data) => {
             if (data?.resultCode === RESULT_CODE) {
               // Parse the information returned by the target UIAbility.
               let info = data.want?.parameters?.info;
               hilog.info(DOMAIN_NUMBER, TAG, JSON.stringify(info) ?? '');
               if (info !== null) {
                 promptAction.showToast({
                   message: JSON.stringify(info)
                 });
               }
             }
             hilog.info(DOMAIN_NUMBER, TAG, JSON.stringify(data.resultCode) ?? '');
           }).catch((err: BusinessError) => {
             hilog.error(DOMAIN_NUMBER, TAG, `Failed to start ability for result. Code is ${err.code}, message is ${err.message}`);
           });
         })
     }
   }
   
   ```



## Starting UIAbility of Another Application

Generally, the user only needs to perform a general operation (for example, selecting a document application to view the document content) to start the UIAbility of another application. In this case, the [implicit Want launch mode](want-overview.md#types-of-want) is recommended. In this mode, the system identifies a matched UIAbility and starts it based on the **want** parameter of the initiator UIAbility.

There are two ways to start **UIAbility**: [explicit and implicit](want-overview.md).

- Explicit Want launch is used to start a determined UIAbility component of an application. You need to set **bundleName** and **abilityName** of the target application in the **want** parameter.

- Implicit Want launch is used to start a UIAbility based on the matching conditions. That is, the UIAbility to start is not determined (the **abilityName** parameter is not specified). When [startAbility()](../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md#uiabilitycontextstartability) is called, the **want** parameter specifies a series of parameters such as **entities** and **actions**. **entities** provides category information of the target UIAbility, such as the browser or video player. **actions** specifies the common operations to perform, such as viewing and sharing. Then the system analyzes the **want** parameter to find the right UIAbility to start. If you are not sure about whether the target application is installed and what **bundleName** and **abilityName** of the target application are, consider using implicit Want launch.

The following example describes how to start the UIAbility of another application through implicit Want.

1. Install multiple document applications on your device. In the [module.json5 file](../quick-start/module-configuration-file.md) of each UIAbility component, configure **entities** and **actions** under **skills**.

  ```json
   {
     "module": {
       "abilities": [
         {
           ...
           "skills": [
             {
               "entities": [
                 ...
                 "entity.system.default"
               ],
               "actions": [
                 ...
                 "ohos.want.action.viewData"
               ]
             }
           ]
         }
       ]
     }
   }
  ```

2. Include **entities** and **actions** of the initiator UIAbility's **want** parameter into **entities** and **actions** under **skills** of the target UIAbility. After the system identifies the UIAbility instances that match the **entities** and **actions** information, a dialog box is displayed, showing the list of matching UIAbility instances for users to select. For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](uiability-usage.md#obtaining-the-context-of-uiability).

   ```ts
   import common from '@ohos.app.ability.common';
   import Want from '@ohos.app.ability.Want';
   import { BusinessError } from '@ohos.base';
   import hilog from '@ohos.hilog';
   
   const TAG: string = '[Page_UIAbilityComponentsInteractive]';
   const DOMAIN_NUMBER: number = 0xFF00;
   
   @Entry
   @Component
   struct Page_UIAbilityComponentsInteractive {
     build() {
       Button()
         .onClick(() => {
           let context: common.UIAbilityContext = getContext(this) as common.UIAbilityContext; // UIAbilityContext
           let want: Want = {
             deviceId: '', // An empty deviceId indicates the local device.
             // Uncomment the line below if you want to implicitly query data only in the specific bundle.
             // bundleName: 'com.samples.stagemodelabilityinteraction',
             action: 'ohos.want.action.viewData',
             // entities can be omitted.
             entities: ['entity.system.default']
           };
           // context is the UIAbilityContext of the initiator UIAbility.
           context.startAbility(want).then(() => {
             hilog.info(DOMAIN_NUMBER, TAG, 'Succeeded in starting FuncAbility.');
           }).catch((err: BusinessError) => {
             hilog.error(DOMAIN_NUMBER, TAG, `Failed to start FuncAbility. Code is ${err.code}, message is ${err.message}`);
           });
         })
     }
   }
   ```

   The following figure shows the effect. When you click **Open PDF**, a dialog box is displayed for you to select the application to use.
   ![](figures/uiability-intra-device-interaction.png)

3. To stop the **UIAbility** instance when the document application is not in use, call [terminateSelf()](../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md#uiabilitycontextterminateself).

   ```ts
   import common from '@ohos.app.ability.common';
   import hilog from '@ohos.hilog';
   
   const TAG: string = '[Page_FromStageModel]';
   const DOMAIN_NUMBER: number = 0xFF00;
   
   @Entry
   @Component
   struct Page_FromStageModel {
     @State message: string = 'Hello World'
   
     build() {
       Button()
         .onClick(() => {
           let context: common.UIAbilityContext = getContext(this) as common.UIAbilityContext; // UIAbilityContext
           // context is the UIAbilityContext of the UIAbility instance to stop.
           context.terminateSelf((err) => {
             if (err.code) {
               hilog.error(DOMAIN_NUMBER, TAG, `Failed to terminate self. Code is ${err.code}, message is ${err.message}`);
               return;
             }
           });
         })
     }
   }
   ```



## Starting UIAbility of Another Application and Obtaining the Return Result

If you want to obtain the return result when using implicit Want to start the UIAbility of another application, use [startAbilityForResult()](../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md#uiabilitycontextterminateselfwithresult). An example scenario is that your application needs to start a third-party payment application and obtain the payment result.

1. In the [module.json5 file](../quick-start/module-configuration-file.md) of the UIAbility corresponding to the payment application, set **entities** and **actions** under **skills**.

   ```json
   {
     "module": {
       "abilities": [
         {
           ...
           "skills": [
             {
               "entities": [
                 ...
                 "entity.system.default"
               ],
               "actions": [
                 ...
                 "ohos.want.action.editData"
               ]
             }
           ]
         }
       ]
     }
   }
   ```

2. Call [startAbilityForResult()](../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md#uiabilitycontextterminateselfwithresult) to start the UIAbility of the payment application. Include **entities** and **actions** of the initiator UIAbility's **want** parameter into **entities** and **actions** under **skills** of the target UIAbility. Use **data** in the asynchronous callback to receive the information returned to the initiator UIAbility after the payment UIAbility stops itself. After the system identifies the UIAbility instances that match the **entities** and **actions** information, a dialog box is displayed, showing the list of matching UIAbility instances for users to select.

   ```ts
   import common from '@ohos.app.ability.common';
   import hilog from '@ohos.hilog';
   import Want from '@ohos.app.ability.Want';
   import { BusinessError } from '@ohos.base';
   
   const TAG: string = '[Page_UIAbilityComponentsInteractive]';
   const DOMAIN_NUMBER: number = 0xFF00;
   
   @Entry
   @Component
   struct Page_UIAbilityComponentsInteractive {
     build() {
       Button()
         .onClick(() => {
           let context: common.UIAbilityContext = getContext(this) as common.UIAbilityContext; // UIAbilityContext
   
           let want: Want = {
             deviceId: '', // An empty deviceId indicates the local device.
             bundleName: 'com.samples.stagemodelabilitydevelop',
             moduleName: 'entry', // moduleName is optional.
             abilityName: 'FuncAbilityA',
             parameters: { // Custom information.
               info: 'From the UIAbilityComponentsInteractive page of EntryAbility',
             }
           };
           context.startAbilityForResult(want).then((data) => {
             // ...
           }).catch((err: BusinessError) => {
             hilog.error(DOMAIN_NUMBER, TAG, `Failed to start ability for result. Code is ${err.code}, message is ${err.message}`);
           });
         })
     }
   }
   ```

3. After the payment is finished, call [terminateSelfWithResult()](../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md#uiabilitycontextterminateselfwithresult) to stop the payment UIAbility and return the **abilityResult** parameter.

   ```ts
   import common from '@ohos.app.ability.common';
   import hilog from '@ohos.hilog';
   
   const TAG: string = '[Page_FuncAbilityA]';
   const DOMAIN_NUMBER: number = 0xFF00;
   
   @Entry
   @Component
   struct Page_FuncAbilityA {
     build() {
       Button()
         .onClick(() => {
           let context: common.UIAbilityContext = getContext(this) as common.UIAbilityContext; // UIAbilityContext
           const RESULT_CODE: number = 1001;
           let abilityResult: common.AbilityResult = {
             resultCode: RESULT_CODE,
             want: {
               bundleName: 'com.samples.stagemodelabilitydevelop',
               moduleName: 'entry', // moduleName is optional.
               abilityName: 'FuncAbilityB',
               parameters: {
                 info: 'From the Index page of FuncAbility',
               },
             },
           };
           context.terminateSelfWithResult(abilityResult, (err) => {
             if (err.code) {
               hilog.error(DOMAIN_NUMBER, TAG, `Failed to terminate self with result. Code is ${err.code}, message is ${err.message}`);
               return;
             }
           });
         })
     }
   }
   ```

4. Receive the information returned by the payment application in the callback of the [startAbilityForResult()](../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md#uiabilitycontextterminateselfwithresult) method. The value of **RESULT_CODE** must be the same as that returned by [terminateSelfWithResult()](../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md#uiabilitycontextterminateselfwithresult).

   ```ts
   import common from '@ohos.app.ability.common';
   import hilog from '@ohos.hilog';
   import Want from '@ohos.app.ability.Want';
   import { BusinessError } from '@ohos.base';
   import promptAction from '@ohos.promptAction';
   
   const TAG: string = '[EntryAbility]';
   const DOMAIN_NUMBER: number = 0xFF00;
   
   @Entry
   @Component
   struct Page_UIAbilityComponentsInteractive {
     build() {
       Button()
         .onClick(() => {
           let context: common.UIAbilityContext = getContext(this) as common.UIAbilityContext; // UIAbilityContext
           const RESULT_CODE: number = 1001;
   
           let want: Want = {
             deviceId: '', // An empty deviceId indicates the local device.
             bundleName: 'com.samples.stagemodelabilitydevelop',
             moduleName: 'entry', // moduleName is optional.
             abilityName: 'FuncAbilityA',
             parameters: { // Custom information.
               info: 'From the UIAbilityComponentsInteractive page of EntryAbility',
             }
           };
           context.startAbilityForResult(want).then((data) => {
             if (data?.resultCode === RESULT_CODE) {
               // Parse the information returned by the target UIAbility.
               let info = data.want?.parameters?.info;
               hilog.info(DOMAIN_NUMBER, TAG, JSON.stringify(info) ?? '');
               if (info !== null) {
                 promptAction.showToast({
                   message: JSON.stringify(info)
                 });
               }
             }
             hilog.info(DOMAIN_NUMBER, TAG, JSON.stringify(data.resultCode) ?? '');
           }).catch((err: BusinessError) => {
             hilog.error(DOMAIN_NUMBER, TAG, `Failed to start ability for result. Code is ${err.code}, message is ${err.message}`);
           });
         })
     }
   }
   ```

## Starting UIAbility with Window Mode Specified (for System Applications Only)

By specifying the window mode when starting the UIAbility of an application, you can have the application displayed in the specified window mode, which can be full-screen, floating window, or split-screen.

In full-screen mode, an application occupies the entire screen after being started. Users cannot view other windows or applications. This mode is suitable for an application that requires users to focus on a specific task or UI.

In floating window mode, an application is displayed on the screen as a floating window after being started. Users can easily switch to other windows or applications. This mode is suitable for an application that allows users to process multiple tasks at the same time.

In split-screen mode, two applications occupy the entire screen, side by side, horizontally or vertically. This mode helps users improve multi-task processing efficiency.

The window mode is specified by the **windowMode** field in the [StartOptions](../reference/apis-ability-kit/js-apis-app-ability-startOptions.md) parameter of [startAbility()](../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md#uiabilitycontextstartability).

> **NOTE**
>
> - If the **windowMode** field is not specified, the UIAbility is started in the default window mode.
> - To ensure that the application can be displayed in the required window mode, check the **supportWindowMode** field under [abilities](../quick-start/module-configuration-file.md#abilities) in the [module.json5 file](../quick-start/module-configuration-file.md) of the UIAbility and make sure the specified window mode is supported.

The following describes how to start the FuncAbility from the EntryAbility page and display it in floating window mode.

1. Add the [StartOptions](../reference/apis-ability-kit/js-apis-app-ability-startOptions.md) parameter in [startAbility()](../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md#uiabilitycontextstartability).
2. Set the **windowMode** field in the [StartOptions](../reference/apis-ability-kit/js-apis-app-ability-startOptions.md) parameter to **WINDOW_MODE_FLOATING**. This setting applies only to a system application.
3. In the case of a third-party application, set the **displayId** field instead.

For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](uiability-usage.md#obtaining-the-context-of-uiability).

```ts
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import common from '@ohos.app.ability.common';
import hilog from '@ohos.hilog';
import StartOptions from '@ohos.app.ability.StartOptions';
import Want from '@ohos.app.ability.Want';
import { BusinessError } from '@ohos.base';

const TAG: string = '[Page_UIAbilityComponentsInteractive]';
const DOMAIN_NUMBER: number = 0xFF00;

@Entry
@Component
struct Page_UIAbilityComponentsInteractive {
  build() {
    Button()
      .onClick(() => {
        let context: common.UIAbilityContext = getContext(this) as common.UIAbilityContext; // UIAbilityContext
        let want: Want = {
          deviceId: '', // An empty deviceId indicates the local device.
          bundleName: 'com.samples.stagemodelabilitydevelop',
          moduleName: 'entry', // moduleName is optional.
          abilityName: 'FuncAbilityB',
          parameters: { // Custom information.
            info: 'From the Index page of EntryAbility',
          }
        };
        let options: StartOptions = {
          windowMode: AbilityConstant.WindowMode.WINDOW_MODE_FLOATING
        };
        // context is the UIAbilityContext of the initiator UIAbility.
        context.startAbility(want, options).then(() => {
          hilog.info(DOMAIN_NUMBER, TAG, 'Succeeded in starting ability.');
        }).catch((err: BusinessError) => {
          hilog.error(DOMAIN_NUMBER, TAG, `Failed to start ability. Code is ${err.code}, message is ${err.message}`);
        });
      })
  }
}
```

The display effect is shown below.

![](figures/start-uiability-floating-window.png)

## Starting a Specified Page of UIAbility

### Overview

A UIAbility component can have multiple pages that each display in specific scenarios.

A UIAbility component can be started in two modes:

- Cold start: The UIAbility instance is totally closed before being started. This requires that the code and resources of the UIAbility instance be completely loaded and initialized.
- Hot start: The UIAbility instance has been started, running in the foreground, and then switched to the background before being started again. In this case, the status of the UIAbility instance can be quickly restored.

This section describes how to start a specified page in both modes: [cold start](#cold-starting-uiability) and [hot start](#hot-starting-uiability). Before starting a specified page, you will learn how to specify a startup page on the initiator UIAbility.


### Specifying a Startup Page

When the initiator UIAbility starts another UIAbility, it usually needs to redirect to a specified page of the target UIAbility. For example, with FuncAbility, which contains two pages, starting FuncAbility means to redirect to either of the pages: Index (corresponding to the home page) and Second (corresponding to feature A page). You can configure the specified page URL in the **want** parameter by adding a custom parameter to **parameters** in **want**. For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](uiability-usage.md#obtaining-the-context-of-uiability).


```ts
import common from '@ohos.app.ability.common';
import hilog from '@ohos.hilog';
import Want from '@ohos.app.ability.Want';
import { BusinessError } from '@ohos.base';

const TAG: string = '[Page_UIAbilityComponentsInteractive]';
const DOMAIN_NUMBER: number = 0xFF00;

@Entry
@Component
struct Page_UIAbilityComponentsInteractive {
  build() {
    Button()
      .onClick(() => {
        let context: common.UIAbilityContext = getContext(this) as common.UIAbilityContext; // UIAbilityContext
        let want: Want = {
          deviceId: '', // An empty deviceId indicates the local device.
          bundleName: 'com.samples.stagemodelabilityinteraction',
          moduleName: 'entry', // moduleName is optional.
          abilityName: 'FuncAbility',
          parameters: { // Custom parameter used to pass the page information.
            router: 'FuncA'
          }
        };
        // context is the UIAbilityContext of the initiator UIAbility.
        context.startAbility(want).then(() => {
          hilog.info(DOMAIN_NUMBER, TAG, 'Succeeded in starting ability.');
        }).catch((err: BusinessError) => {
          hilog.error(DOMAIN_NUMBER, TAG, `Failed to start ability. Code is ${err.code}, message is ${err.message}`);
        });
      })
  }
}
```


### Cold Starting UIAbility

In cold start mode, obtain the parameters from the initiator UIAbility through the **onCreate()** callback of the target UIAbility. Then, in the **onWindowStageCreate()** callback of the target UIAbility, parse the **want** parameter passed by the EntryAbility to obtain the URL of the page to be loaded, and pass the URL to the **windowStage.loadContent()** method.


```ts
import AbilityConstant from '@ohos.app.ability.AbilityConstant';
import UIAbility from '@ohos.app.ability.UIAbility';
import Want from '@ohos.app.ability.Want';
import window from '@ohos.window';

export default class FuncAbility extends UIAbility {
  funcAbilityWant: Want | undefined = undefined;

  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    // Receive the parameters passed by the initiator UIAbility.
    this.funcAbilityWant = want;
  }

  onWindowStageCreate(windowStage: window.WindowStage) {
    // Main window is created. Set a main page for this UIAbility.
    let url = 'pages/Index';
    if (this.funcAbilityWant?.parameters?.router && this.funcAbilityWant.parameters.router === 'funcA') {
      url = 'pages/Page_ColdStartUp';
    }
    windowStage.loadContent(url, (err, data) => {
      // ...
    });
  }
}
```

### Hot Starting UIAbility

If the target UIAbility has been started, the initialization logic is not executed again. Instead, the **onNewWant()** lifecycle callback is directly triggered. To implement redirection, parse the required parameters in **onNewWant()**.

An example scenario is as follows:

1. A user opens the SMS application. The UIAbility instance of the SMS application is started, and the home page of the application is displayed.
2. The user returns to the home screen, and the SMS application switches to the background.
3. The user opens the Contacts application and finds a contact.
4. The user touches the SMS button next to the contact. The UIAbility instance of the SMS application is restarted.
5. Since the UIAbility instance of the SMS application has been started, the **onNewWant()** callback of the UIAbility is triggered, and the initialization logic such as **onCreate()** and **onWindowStageCreate()** is skipped.

**Figure 1** Hot starting the target UIAbility

![](figures/uiability-hot-start.png)

The development procedure is as follows:

1. When the UIAbility instance of the SMS application is cold started, call [getUIContext()](../reference/apis-arkui/js-apis-window.md#getuicontext10) in the **onWindowStageCreate()** lifecycle callback to obtain the [UIContext](../reference/apis-arkui/js-apis-arkui-UIContext.md).

   ```ts
   import hilog from '@ohos.hilog';
   import UIAbility from '@ohos.app.ability.UIAbility';
   import Want from '@ohos.app.ability.Want';
   import window from '@ohos.window';
   
   import { UIContext } from '@ohos.arkui.UIContext';
   
   const DOMAIN_NUMBER: number = 0xFF00;
   const TAG: string = '[EntryAbility]';
   
   export default class EntryAbility extends UIAbility {
     funcAbilityWant: Want | undefined = undefined;
     uiContext: UIContext | undefined = undefined;
   
     // ...
   
     onWindowStageCreate(windowStage: window.WindowStage): void {
       // Main window is created. Set a main page for this UIAbility.
       let url = 'pages/Index';
       if (this.funcAbilityWant?.parameters?.router && this.funcAbilityWant.parameters.router === 'funcA') {
         url = 'pages/Page_ColdStartUp';
       }
   
       windowStage.loadContent(url, (err, data) => {
         if (err.code) {
           return;
         }
   
         let windowClass: window.Window;
         windowStage.getMainWindow((err, data) => {
           if (err.code) {
             hilog.error(DOMAIN_NUMBER, TAG, `Failed to obtain the main window. Code is ${err.code}, message is ${err.message}`);
             return;
           }
           windowClass = data;
           this.uiContext = windowClass.getUIContext();
         })
       });
     }
   }
   ```

2. Parse the **want** parameter passed in the **onNewWant()** callback of the UIAbility of the SMS application, call [getRouter()](../reference/apis-arkui/js-apis-arkui-UIContext.md#getrouter) in the **UIContext** class to obtain a [Router](../reference/apis-arkui/js-apis-arkui-UIContext.md#router) instance, and specify the target page. When the UIAbility instance of the SMS application is started again, the specified page of the UIAbility instance of the SMS application is displayed.

   ```ts
   import AbilityConstant from '@ohos.app.ability.AbilityConstant';
   import hilog from '@ohos.hilog';
   import UIAbility from '@ohos.app.ability.UIAbility';
   import Want from '@ohos.app.ability.Want';
   import { BusinessError } from '@ohos.base';

   import { Router, UIContext } from '@ohos.arkui.UIContext';
   
   const DOMAIN_NUMBER: number = 0xFF00;
   const TAG: string = '[EntryAbility]';
   
   export default class EntryAbility extends UIAbility {
     funcAbilityWant: Want | undefined = undefined;
     uiContext: UIContext | undefined = undefined;
   
     onNewWant(want: Want, launchParam: AbilityConstant.LaunchParam): void {
       if (want?.parameters?.router && want.parameters.router === 'funcB') {
         let funcAUrl = 'pages/Page_HotStartUp';
         if (this.uiContext) {
           let router: Router = this.uiContext.getRouter();
           router.pushUrl({
             url: funcAUrl
           }).catch((err: BusinessError) => {
          hilog.error(DOMAIN_NUMBER, TAG, `Failed to push url. Code is ${err.code}, message is ${err.message}`);
           });
         }
       }
     }
     // ...
   }
   ```

> **NOTE**
>
> When the [launch type of the target UIAbility](uiability-launch-type.md) is set to **multiton**, a new instance is created each time the target UIAbility is started. In this case, the [onNewWant()](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityonnewwant) callback will not be invoked.


## Using Call to Implement UIAbility Interaction (for System Applications Only)

Call is an extension of the UIAbility capability. It enables the UIAbility to be invoked by and communicate with external systems. The UIAbility invoked can be either started in the foreground or created and run in the background. You can use the call to implement data sharing between two UIAbility instances (CallerAbility and CalleeAbility) through IPC.

The core API used for the call is **startAbilityByCall()**, which differs from **startAbility()** in the following ways:

- **startAbilityByCall()** supports UIAbility launch in the foreground and background, whereas **startAbility()** supports UIAbility launch in the foreground only.

- The CallerAbility can use the caller object returned by **startAbilityByCall()** to communicate with the CalleeAbility, but **startAbility()** does not provide the communication capability.

Call is usually used in the following scenarios:

- Communicating with the CalleeAbility

- Starting the CalleeAbility in the background


**Table 1** Terms used in the call

| **Term**| Description|
| -------- | -------- |
| CallerAbility| UIAbility that triggers the call.|
| CalleeAbility | UIAbility invoked by the call.|
| Caller | Object returned by **startAbilityByCall** and used by the CallerAbility to communicate with the CalleeAbility.|
| Callee | Object held by the CalleeAbility to communicate with the CallerAbility.|

The following figure shows the call process.

**Figure 1** Call process
![call](figures/call.png)

- The CallerAbility uses **startAbilityByCall** to obtain a caller object and uses **call()** of the caller object to send data to the CalleeAbility.

- The CalleeAbility, which holds a callee object, uses **on()** of the callee object to register a callback. This callback is invoked when the CalleeAbility receives data from the CallerAbility.

> **NOTE**
> Currently, only system applications can use the call.
>
> The launch type of the CalleeAbility must be **singleton**.
>
> Both local (intra-device) and cross-device calls are supported. The following describes how to initiate a local call. For details about how to initiate a cross-device call, see [Using Cross-Device Call](hop-multi-device-collaboration.md#using-cross-device-call).


### Available APIs

The following table describes the main APIs used for the call. For details, see [AbilityContext](../reference/apis-ability-kit/js-apis-app-ability-uiAbility.md#caller).

**Table 2** Call APIs

| API| Description|
| -------- | -------- |
| startAbilityByCall(want: Want): Promise&lt;Caller&gt; | Starts a UIAbility in the foreground (through the **want** configuration) or background (default) and obtains the caller object for communication with the UIAbility. For details, see [AbilityContext](../reference/apis-ability-kit/js-apis-inner-application-uiAbilityContext.md#abilitycontextstartabilitybycall) or **ServiceExtensionContext**. |
| on(method: string, callback: CalleeCallBack): void | Callback invoked when the CalleeAbility registers a method.|
| off(method: string): void | Callback invoked when the CalleeAbility deregisters a method.|
| call(method: string, data: rpc.Parcelable): Promise&lt;void&gt; | Sends agreed parcelable data to the CalleeAbility.|
| callWithResult(method: string, data: rpc.Parcelable): Promise&lt;rpc.MessageSequence&gt; | Sends agreed parcelable data to the CalleeAbility and obtains the agreed parcelable data returned by the CalleeAbility.|
| release(): void | Releases the caller object.|
| on(type: "release", callback: OnReleaseCallback): void| Callback invoked when the caller object is released.|

The implementation of using the call for UIAbility interaction involves two parts:

- [Creating a CalleeAbility](#creating-a-calleeability)

- [Accessing the CalleeAbility](#accessing-the-calleeability)


### Creating a CalleeAbility

For the CalleeAbility, implement the callback to receive data and the methods to marshal and unmarshal data. When data needs to be received, use **on()** to register a listener. When data does not need to be received, use **off()** to deregister the listener.

1. Configure the launch type of the CalleeAbility.

   For example, set the launch type of the CalleeAbility to **singleton**. For details, see [UIAbility Component Launch Type](uiability-launch-type.md).

2. Import the **UIAbility** module.

   ```ts
   import UIAbility from '@ohos.app.ability.UIAbility';
   ```

3. Define the agreed parcelable data.

   The data formats sent and received by the CallerAbility and CalleeAbility must be consistent. In the following example, the data formats are number and string.


   ```ts
   import type rpc from '@ohos.rpc';
   
   class MyParcelable {
     num: number = 0;
     str: string = '';
   
     constructor(num: number, string: string) {
       this.num = num;
       this.str = string;
     };
   
     mySequenceable(num: number, string: string): void {
       this.num = num;
       this.str = string;
     };
   
     marshalling(messageSequence: rpc.MessageSequence): boolean {
       messageSequence.writeInt(this.num);
       messageSequence.writeString(this.str);
       return true;
     };
   
     unmarshalling(messageSequence: rpc.MessageSequence): boolean {
       this.num = messageSequence.readInt();
       this.str = messageSequence.readString();
       return true;
     };
   }
   ```

4. Implement **Callee.on** and **Callee.off**.

   The time to register a listener for the CalleeAbility depends on your application. The data sent and received before the listener is registered and that after the listener is deregistered are not processed. In the following example, the **MSG_SEND_METHOD** listener is registered in **onCreate** of the UIAbility and deregistered in **onDestroy**. After receiving parcelable data, the application processes the data and returns the data result. You need to implement processing based on service requirements. The sample code is as follows:


   ```ts
   import type AbilityConstant from '@ohos.app.ability.AbilityConstant';
   import UIAbility from '@ohos.app.ability.UIAbility';
   import type Want from '@ohos.app.ability.Want';
   import hilog from '@ohos.hilog';
   import type rpc from '@ohos.rpc';
   import type { Caller } from '@ohos.app.ability.UIAbility';

   const MSG_SEND_METHOD: string = 'CallSendMsg';
   const DOMAIN_NUMBER: number = 0xFF00;
   const TAG: string = '[CalleeAbility]';
   
   class MyParcelable {
     num: number = 0;
     str: string = '';
   
     constructor(num: number, string: string) {
       this.num = num;
       this.str = string;
     }
   
     mySequenceable(num: number, string: string): void {
       this.num = num;
       this.str = string;
     }
   
     marshalling(messageSequence: rpc.MessageSequence): boolean {
       messageSequence.writeInt(this.num);
       messageSequence.writeString(this.str);
       return true;
     };
   
     unmarshalling(messageSequence: rpc.MessageSequence): boolean {
       this.num = messageSequence.readInt();
       this.str = messageSequence.readString();
       return true;
     };
   };

   function sendMsgCallback(data: rpc.MessageSequence): rpc.Parcelable {
     hilog.info(DOMAIN_NUMBER, TAG, '%{public}s', 'CalleeSortFunc called');

     // Obtain the parcelable data sent by the CallerAbility.
     let receivedData: MyParcelable = new MyParcelable(0, '');
     data.readParcelable(receivedData);
     hilog.info(DOMAIN_NUMBER, TAG, '%{public}s', `receiveData[${receivedData.num}, ${receivedData.str}]`);
     let num: number = receivedData.num;

     // Process the data.
     // Return the parcelable data result to the CallerAbility.
     return new MyParcelable(num + 1, `send ${receivedData.str} succeed`) as rpc.Parcelable;
   }

   export default class CalleeAbility extends UIAbility {
     caller: Caller | undefined;
     onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
       try {
         this.callee.on(MSG_SEND_METHOD, sendMsgCallback);
       } catch (error) {
         hilog.error(DOMAIN_NUMBER, TAG, '%{public}s', `Failed to register. Error is ${error}`);
       };
     }
     releaseCall(): void {
       try {
         if (this.caller) {
           this.caller.release();
           this.caller = undefined;
         }
         hilog.info(DOMAIN_NUMBER, TAG, '%{public}s', 'caller release succeed');
       } catch (error) {
         hilog.info(DOMAIN_NUMBER, TAG, '%{public}s', `caller release failed with ${error}`);
       };
     }
     onDestroy(): void {
       try {
         this.callee.off(MSG_SEND_METHOD);
         hilog.info(DOMAIN_NUMBER, TAG, '%{public}s', 'Callee OnDestroy');
         this.releaseCall();
       } catch (error) {
         hilog.error(DOMAIN_NUMBER, TAG, '%{public}s', `Failed to register. Error is ${error}`);
       };
     }
   }
   ```


### Accessing the CalleeAbility

1. Import the **UIAbility** module.

   ```ts
   import UIAbility from '@ohos.app.ability.UIAbility';
   ```

2. Obtain the caller interface.

   The **UIAbilityContext** attribute implements **startAbilityByCall** to obtain the caller object for communication. The following example uses **this.context** to obtain the **UIAbilityContext**, uses **startAbilityByCall** to start the CalleeAbility, obtain the caller object, and register the **onRelease** listener of the CallerAbility. You need to implement processing based on service requirements.


   ```ts
   import { Caller } from '@ohos.app.ability.UIAbility';
   import { BusinessError } from '@ohos.base';
   import common from '@ohos.app.ability.common';
   import promptAction from '@ohos.promptAction';
   import hilog from '@ohos.hilog';
   import Want from '@ohos.app.ability.Want';
   
   const DOMAIN_NUMBER: number = 0xFF00;
   const TAG: string = '[Page_UIAbilityComponentsInteractive]';
   
   @Entry
   @Component
   struct Page_UIAbilityComponentsInteractive {
     caller: Caller | undefined = undefined;
   
     // Register the onRelease() listener of the CallerAbility.
     private regOnRelease(caller: Caller): void {
       hilog.info(DOMAIN_NUMBER, TAG, `caller is ${caller}`);
       try {
         caller.on('release', (msg: string) => {
           hilog.info(DOMAIN_NUMBER, TAG, `caller onRelease is called ${msg}`);
         })
         hilog.info(DOMAIN_NUMBER, TAG, 'succeeded in registering on release.');
       } catch (err) {
         let code = (err as BusinessError).code;
         let message = (err as BusinessError).message;
         hilog.error(DOMAIN_NUMBER, TAG, `Failed to caller register on release. Code is ${code}, message is ${message}`);
       }
     }
   
     build() {
       Button('StartAbilityByCall')
         .onClick(() => {
           let context: common.UIAbilityContext = getContext(this) as common.UIAbilityContext; // UIAbilityContext
           let want: Want = {
             bundleName: 'com.samples.stagemodelabilityinteraction',
             abilityName: 'CalleeAbility',
             parameters: { // Custom information.
               info: 'CallSendMsg'
             }
           };
   
           context.startAbilityByCall(want).then((caller: Caller) => {
             hilog.info(DOMAIN_NUMBER, TAG, `Succeeded in starting ability.Code is ${caller}`);
             if (caller === undefined) {
               hilog.info(DOMAIN_NUMBER, TAG, 'get caller failed');
               return;
             }
             else {
               hilog.info(DOMAIN_NUMBER, TAG, 'get caller success');
               this.regOnRelease(caller);
               promptAction.showToast({
                 message: 'caller success'
               });
             }
           }).catch((err: BusinessError) => {
             hilog.error(DOMAIN_NUMBER, TAG, `Failed to start ability. Code is ${err.code}, message is ${err.message}`);
           });
         })
     }
   }
   ```

