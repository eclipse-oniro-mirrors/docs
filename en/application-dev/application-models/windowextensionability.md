# WindowExtensionAbility (for System Applications Only)


[WindowExtensionAbility](../reference/apis/js-apis-application-windowExtensionAbility.md) is a type of ExtensionAbility component that allows a system application to be embedded in and displayed over another application.


The WindowExtensionAbility component must be used together with the [AbilityComponent](../reference/arkui-ts/ts-container-ability-component.md) to process services of the started application. WindowExtensionAbility is run in connection mode. A system application must use the AbilityComponent to start the WindowExtensionAbility component.

Each ExtensionAbility has its own context. For WindowExtensionAbility,
the context is [WindowExtensionContext](../reference/apis/js-apis-inner-application-windowExtensionContext.md).  

> **NOTE**
>
> **WindowExtensionAbility** is a system API. To embed a third-party application in another application and display it over the application, switch to the full SDK by following the instructions provided in [Guide to Switching to Full SDK](../../application-dev/quick-start/full-sdk-switch-guide.md).


## Setting an Embedded UIAbility

The **WindowExtensionAbility** class provides **onConnect()**, **onDisconnect()**, and **onWindowReady()** lifecycle callbacks, which can be overridden.

- The **onWindowReady()** callback is invoked when a window is created for the ability.

- The **onConnect()** callback is invoked when the AbilityComponent corresponding to the window connects to the ability.

- The **onDisconnect()** callback is invoked when the AbilityComponent disconnects from the ability.


**How to Develop**

To implement an embedded application, manually create a WindowExtensionAbility in DevEco Studio as follows:

1. In the **ets** directory of the **Module** project, right-click and choose **New > Directory** to create a directory named **WindowExtAbility**.

2. Right-click the **WindowExtAbility** directory, and choose **New > TypeScript File** to create a file named **WindowExtAbility.ts**.

3. Open the **WindowExtAbility.ts** file and import the dependency package of **WindowExtensionAbility**. Customize a class that inherits from **WindowExtensionAbility** and implement the **onWindowReady()**, **onConnect()**, and **onDisconnect()** lifecycle callbacks.

   ```ts
   import Extension from '@ohos.application.WindowExtensionAbility'

    export default class WindowExtAbility extends Extension {
        onWindowReady(window) {
            window.loadContent('WindowExtAbility/pages/index1').then(() => {
                window.getProperties().then((pro) => {
                    console.info("WindowExtension " + JSON.stringify(pro));
                })
                window.show();
            })
        }

        onConnect(want) {
            console.info('JSWindowExtension onConnect ' + want.abilityName);
        }

        onDisconnect(want) {
            console.info('JSWindowExtension onDisconnect ' + want.abilityName);
        }
    }
   ```

4. Register the WindowExtensionAbility in the [module.json5 file](../quick-start/module-configuration-file.md) corresponding to the **Module** project. Set **type** to **"window"** and **srcEntry** to the code path of the ExtensionAbility component.

   ```json
   {
     "module": {
       "extensionAbilities": [
            {
                "name": "WindowExtAbility",
                "srcEntry": "./ets/WindowExtAbility/WindowExtAbility.ts",
                "icon": "$media:icon",
                "description": "WindowExtension",
                "type": "window",
                "exported": true,
            }
        ],
     }
   }
   ```


## Starting an Embedded UIAbility

System applications can load the created WindowExtensionAbility through the AbilityComponent.

**How to Develop**

1. To connect to an embedded application, add the AbilityComponent to the corresponding pages in the DevEco Studio project.

2. Set **bundleName** and **abilityName** in the AbilityComponent.

3. Set the width and height. The sample code is as follows:

   ```ts
   @Entry
   @Component
   struct Index {
     @State message: string = 'Hello World'
   
     build() {
       Row() {
         Column() {
           AbilityComponent({ abilityName: "WindowExtAbility", bundleName: "com.example.WindowExtAbility"})
             .width(500)
             .height(500)
         }
         .width('100%')
       }
       .height('100%')
       .backgroundColor(0x64BB5c)
     }
   }
   ```

