# Building the First ArkTS Application in Stage Model


> **NOTE**
> 
> For best possible results, use [DevEco Studio 3.1 Beta2](https://developer.harmonyos.com/cn/develop/deveco-studio) for your development.


## Creating an ArkTS Project

1. If you are opening DevEco Studio for the first time, click **Create Project**. If a project is already open, choose **File** > **New** > **Create Project** from the menu bar. On the **Choose Your Ability Template** page, select **Application** (or **Atomic Service**, depending on your project), select **Empty Ability** as the template, and click **Next**.

   ![createProject](figures/createProject.png)

2. On the project configuration page, set **Compile SDK** to **9**, **Model** to **Stage**, and retain the default values for other parameters.

   ![chooseStageModel](figures/chooseStageModel.png)

   > **NOTE**
   >
   > You can use the low-code development mode apart from the traditional coding approach.
   >
   > On the low-code development pages, you can design your application UI in an efficient, intuitive manner, with a wide array of UI editing features.
   >
   > To use the low-code development mode, turn on **Enable Super Visual** on the page shown above.
   
3. Click **Finish**. DevEco Studio will automatically generate the sample code and resources that match your project type. Wait until the project is created.

4. After the project is created, in the **entry** > **build-profile.json5** file, change **runtimeOS** under **targets** to **OpenHarmony**, and click **Sync Now** in the upper right corner to start development.


## ArkTS Project Directory Structure (Stage Model)

![en-us_image_0000001364054489](figures/en-us_image_0000001364054489.png)

- **AppScope** > **app.json5**: global configuration of your application.
- **entry**: OpenHarmony project module, which can be built into an OpenHarmony Ability Package ([HAP](../../glossary.md#hap)).
  - **src > main > ets**: a collection of ArkTS source code.
  - **src > main > ets > entryability**: entry to your application/service.
  - **src > main > ets > pages**: pages included in your application/service.
  - **src > main > resources**: a collection of resource files used by your application/service, such as graphics, multimedia, character strings, and layout files. For details about resource files, see [Resource Categories and Access](resource-categories-and-access.md#resource-categories).
  - **src > main > module.json5**: module configuration file. This file describes the global configuration information of the application/service, the device-specific configuration information, and the configuration information of the HAP file. For details, see [module.json5 Configuration File](module-configuration-file.md).
  - **build-profile.json5**: current module information and build configuration options, including **buildOption** and **targets**. Under **targets**, you can set **runtimeOS** to **HarmonyOS** (default) or **OpenHarmony**, depending on the OS of your application.
  - **hvigorfile.ts**: module-level build script. You can customize related tasks and code implementation.
- **oh_modules**: third-party library dependency information. For details about how to adapt a historical npm project to ohpm, see [Manually Migrating Historical Projects](https://developer.harmonyos.com/cn/docs/documentation/doc-guides-V3/project_overview-0000001053822398-V3#section108143331212).
- **build-profile.json5**: application-level configuration information, including the signature and product configuration.
- **hvigorfile.ts**: application-level build script.


## Building the First Page

1. Use the **\<Text>** component.

   After the project synchronization is complete, choose **entry** > **src** > **main** > **ets** > **pages** in the **Project** window and open the **Index.ets** file. You can see that the file contains a **\<Text>** component. The sample code in the **Index.ets** file is shown below:
   
   ```ts
   // Index.ets
   @Entry
   @Component
   struct Index {
     @State message: string = 'Hello World'
   
     build() {
       Row() {
         Column() {
           Text(this.message)
             .fontSize(50)
             .fontWeight(FontWeight.Bold)
         }
         .width('100%')
       }
       .height('100%')
     }
   }
   ```

2. Add a **\<Button>** component.

   On the default page, add a **\<Button>** component to respond to user clicks and implement redirection to another page. The sample code in the **Index.ets** file is shown below:
   
   ```ts
   // Index.ets
   @Entry
   @Component
   struct Index {
     @State message: string = 'Hello World'
   
     build() {
       Row() {
         Column() {
           Text(this.message)
             .fontSize(50)
             .fontWeight(FontWeight.Bold)
           // Add a button to respond to user clicks.
           Button() {
             Text('Next')
               .fontSize(30)
               .fontWeight(FontWeight.Bold)
           }
           .type(ButtonType.Capsule)
           .margin({
             top: 20
           })
           .backgroundColor('#0D9FFB')
           .width('40%')
           .height('5%')
         }
         .width('100%')
       }
       .height('100%')
     }
   }
   ```

3. On the toolbar in the upper right corner of the editing window, click **Previewer**. Below is how the first page looks in the Previewer.

   ![en-us_image_0000001311334976](figures/en-us_image_0000001311334976.png)


## Building the Second Page

1. Create the second page.

   - Create the second page file: In the **Project** window, choose **entry** > **src** > **main** > **ets**. Right-click the **pages** folder, choose **New** > **ArkTS File**, name the page **Second**, and click **Finish**. Below is the structure of the **Second** folder.

      ![secondPage](figures/secondPage.png)

      > **NOTE**
      >
      > You can also right-click the **pages** folder and choose **New** > **Page** from the shortcut menu. In this scenario, you do not need to manually configure page routes.
   - Configure the route for the second page: In the **Project** window, choose **entry** > **src** > **main** > **resources** > **base** > **profile**. In the **main_pages.json** file, set **pages/Second** under **src**. The sample code is as follows:
     
      ```json
      {
        "src": [
          "pages/Index",
          "pages/Second"
        ]
      }
      ```

2. Add **\<Text>** and **\<Button>** components.

   Add **\<Text>** and **\<Button>** components and set their styles, by referring to the first page. The sample code in the **Second.ets** file is shown below:
   
   ```ts
   // Second.ets
   @Entry
   @Component
   struct Second {
     @State message: string = 'Hi there'
   
     build() {
       Row() {
         Column() {
           Text(this.message)
             .fontSize(50)
             .fontWeight(FontWeight.Bold)
           Button() {
             Text('Back')
               .fontSize(25)
               .fontWeight(FontWeight.Bold)
           }
           .type(ButtonType.Capsule)
           .margin({
             top: 20
           })
           .backgroundColor('#0D9FFB')
           .width('40%')
           .height('5%')
         }
         .width('100%')
       }
       .height('100%')
     }
   }
   ```


## Implementing Page Redirection

You can implement page redirection through the [page router](../reference/apis/js-apis-router.md), which finds the target page based on the page URL. Import the **router** module and then perform the steps below:

1. Implement redirection from the first page to the second page.

   In the **index.ets** file of the first page, bind the **onClick** event to the **Next** button so that clicking the button redirects the user to the second page. The sample code in the **Index.ets** file is shown below:
   
   ```ts
   // Index.ets
   // Import the router module.
   import router from '@ohos.router';
   
   @Entry
   @Component
   struct Index {
     @State message: string = 'Hello World'
   
     build() {
       Row() {
         Column() {
           Text(this.message)
             .fontSize(50)
             .fontWeight(FontWeight.Bold)
           // Add a button to respond to user clicks.
           Button() {
             Text('Next')
               .fontSize(30)
               .fontWeight(FontWeight.Bold)
           }
           .type(ButtonType.Capsule)
           .margin({
             top: 20
           })
           .backgroundColor('#0D9FFB')
           .width('40%')
           .height('5%')
           // Bind the onClick event to the Next button so that clicking the button redirects the user to the second page.
           .onClick(() => {
             console.info(`Succeeded in clicking the 'Next' button.`)
            // Go to the second page.
              router.pushUrl({ url: 'pages/Second' }).then(() => {
                console.info('Succeeded in jumping to the second page.')
              }).catch((err) => {
                console.error(`Failed to jump to the second page.Code is ${err.code}, message is ${err.message}`)
              })
           })
         }
         .width('100%')
       }
       .height('100%')
     }
   }
   ```

2. Implement redirection from the second page to the first page.

   In the **Second.ets** file of the second page, bind the **onClick** event to the **Back** button so that clicking the button redirects the user back to the first page. The sample code in the **Second.ets** file is shown below:
   
   ```ts
   // Second.ets
   // Import the router module.
   import router from '@ohos.router';
   
   @Entry
   @Component
   struct Second {
     @State message: string = 'Hi there'
   
     build() {
       Row() {
         Column() {
           Text(this.message)
             .fontSize(50)
             .fontWeight(FontWeight.Bold)
           Button() {
             Text('Back')
               .fontSize(25)
               .fontWeight(FontWeight.Bold)
           }
           .type(ButtonType.Capsule)
           .margin({
             top: 20
           })
           .backgroundColor('#0D9FFB')
           .width('40%')
           .height('5%')
           // Bind the onClick event to the Back button so that clicking the button redirects the user back to the first page.
           .onClick(() => {
             console.info(`Succeeded in clicking the 'Back' button.`)
             try {
               // Return to the first page.
               router.back()
               console.info('Succeeded in returning to the first page.')
             } catch (err) {
               console.error(`Failed to return to the first page.Code is ${err.code}, message is ${err.message}`)
             }
           })
         }
         .width('100%')
       }
       .height('100%')
     }
   }
   ```

3. Open the **Index.ets** file and click ![en-us_image_0000001311015192](figures/en-us_image_0000001311015192.png) in the Previewer to refresh the file. The display effect is shown in the figure below.

   ![en-us_image_0000001364254729](figures/en-us_image_0000001364254729.png)


## Running the Application on a Real Device

1. Connect the development board running the OpenHarmony standard system to the computer.

2. Choose **File** > **Project Structure...** > **Project** > **SigningConfigs**, and select **Automatically generate signature**. Wait until the automatic signing is complete, and click **OK**. See the following figure.

   ![signConfig](figures/signConfig.png)

3. On the toolbar in the upper right corner of the editing window, click ![en-us_image_0000001364054485](figures/en-us_image_0000001364054485.png). The display effect is shown in the figure below.

   ![en-us_image_0000001364254729](figures/en-us_image_0000001364254729.png)

Congratulations! You have finished developing your OpenHarmony application in ArkTS in the stage model. To learn more about OpenHarmony application development, see [Application Development Overview](../application-dev-guide.md).
