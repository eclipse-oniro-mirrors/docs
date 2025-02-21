# Application Window Development (FA Model)

## Basic Concepts

Immersive window: a window display mode where the system windows (generally the status bar and navigation bar) are hidden to allow users to fully engage with the content.

The immersive window feature is applicable only to the main window of an application in full-screen mode. It does not apply to a main window in any other mode or a subwindow (for example, a dialog box or a floating window).

## When to Use

In the FA model, you can perform the following operations during application window development:

- Setting the properties and content of the subwindow of an application

- Experiencing the immersive window feature


## Available APIs

The table below lists the common APIs used for application window development. For details about more APIs, see [Window](../reference/apis-arkui/js-apis-window.md).

| Instance        | API                                                      | Description                                                        |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Window static method| createWindow(config: Configuration, callback: AsyncCallback\<Window>): void | Creates a subwindow.<br>**config**: parameters used for creating the window.              |
| Window static method| findWindow(name: string): Window                             | Finds a window based on the name.                                    |
| Window         | setUIContent(path: string, callback: AsyncCallback&lt;void&gt;): void | Loads the content of a page, with its path in the current project specified, to this window.<br>**path**: path of the page from which the content will be loaded. The path is configured in the **config.json** file of the project in the FA model.                                |
| Window         | moveWindowTo(x: number, y: number, callback: AsyncCallback&lt;void&gt;): void | Moves this window.                                              |
| Window         | setWindowBrightness(brightness: number, callback: AsyncCallback&lt;void&gt;): void | Sets the brightness for this window.                                            |
| Window         | resize(width: number, height: number, callback: AsyncCallback&lt;void&gt;): void | Changes the window size.                                          |
| Window         | setWindowLayoutFullScreen(isLayoutFullScreen: boolean, callback: AsyncCallback&lt;void&gt;): void | Sets whether to enable the full-screen mode for the window layout.                                 |
| Window         | setWindowSystemBarEnable(names: Array&lt;'status'\|'navigation'&gt;): Promise&lt;void&gt; | Sets whether to display the status bar and navigation bar in this window.                                |
| Window         | setWindowSystemBarProperties(systemBarProperties: SystemBarProperties, callback: AsyncCallback&lt;void&gt;): void | Sets the properties of the status bar and navigation bar in this window.<br>**systemBarProperties**: properties of the status bar and navigation bar.|
| Window         | showWindow(callback: AsyncCallback\<void>): void             | Shows this window.                                              |
| Window         | on(type: 'touchOutside', callback: Callback&lt;void&gt;): void | Enables listening for touch events outside this window.                          |
| Window         | destroyWindow(callback: AsyncCallback&lt;void&gt;): void     | Destroys this window.                                              |


## Setting the Subwindow of an Application

You can create a subwindow, such as a dialog box, and set its properties.


### How to Develop

1. Create or obtain a subwindow.

   - Call **window.createWindow** to create a subwindow.
   - Call **window.findWindow** to find an available subwindow.

   ```ts
   import window from '@ohos.window';
   import { BusinessError } from '@ohos.base';
   
   let windowClass: window.Window | null = null;
   // Method 1: Create a subwindow.
   let config: window.Configuration = { name: "subWindow", windowType: window.WindowType.TYPE_APP };
   window.createWindow(config, (err: BusinessError, data) => {
     let errCode: number = err.code;
     if (errCode) {
       console.error('Failed to create the subWindow. Cause: ' + JSON.stringify(err));
       return;
     }
     console.info('Succeeded in creating subWindow. Data: ' + JSON.stringify(data));
     windowClass = data;
   });
   // Method 2: Find a subwindow.
   try {
     windowClass = window.findWindow('subWindow');
   } catch (exception) {
     console.error('Failed to find the Window. Cause: ' + JSON.stringify(exception));
   }
   ```

2. Set the properties of the subwindow.

   After the subwindow is created, you can set its properties, such as the size, position, background color, and brightness.

   ```ts
   // Move the subwindow.
   let windowClass: window.Window = window.findWindow("test");
   windowClass.moveWindowTo(300, 300, (err: BusinessError) => {
     let errCode: number = err.code;
     if (errCode) {
       console.error('Failed to move the window. Cause:' + JSON.stringify(err));
       return;
     }
     console.info('Succeeded in moving the window.');
   });
   // Change the size of the subwindow.
   windowClass.resize(500, 500, (err: BusinessError) => {
     let errCode: number = err.code;
     if (errCode) {
       console.error('Failed to change the window size. Cause:' + JSON.stringify(err));
       return;
     }
     console.info('Succeeded in changing the window size.');
   });
   ```

3. Load content to and show the subwindow.

   Call **setUIContent** to load content to the subwindow and **showWindow** to show the subwindow.

   ```ts
   // Load content to the subwindow.
   let windowClass: window.Window = window.findWindow("test");
   windowClass.setUIContent("pages/page2", (err: BusinessError) => {
     let errCode: number = err.code;
     if (errCode) {
       console.error('Failed to load the content. Cause: ' + JSON.stringify(err));
       return;
     }
     console.info('Succeeded in loading the content.');
     // Show the subwindow.
     windowClass.showWindow((err: BusinessError) => {
       let errCode: number = err.code;
       if (errCode) {
         console.error('Failed to show the window. Cause: ' + JSON.stringify(err));
         return;
       }
       console.info('Succeeded in showing the window.');
     });
   });
   ```

4. Destroy the subwindow.

   When the subwindow is no longer needed, you can call **destroyWindow** to destroy it.

   ```ts
   // Call destroy() to destroy the subwindow when it is no longer needed.
   let windowClass: window.Window = window.findWindow("test");
   windowClass.destroyWindow((err: BusinessError) => {
     let errCode: number = err.code;
     if (errCode) {
       console.error('Failed to destroy the subwindow. Cause:' + JSON.stringify(err));
       return;
     }
     console.info('Succeeded in destroying the subwindow.');
   });
   ```

## Experiencing the Immersive Window Feature

To create a better video watching and gaming experience, you can use the immersive window feature to hide the status bar and navigation bar. This feature is available only for the main window of an application. Since API version 10, the immersive window has the same size as the full screen by default; its layout is controlled by the component module; the background color of its status bar and navigation bar is transparent, and the text color is black. When an application window calls **setWindowLayoutFullScreen**, with **true** passed in, an immersive window layout is used. If **false** is passed in, a non-immersive window layout is used.


### How to Develop

1. Obtain the main window.

   > **NOTE**
   >
   > The immersive window feature can be implemented only after the main window is obtained.
   >
   > Ensure that the top window of the application is the main window. You can use **window.getLastWindow** to obtain the main window.

   ```ts
   import window from '@ohos.window';
   import { BusinessError } from '@ohos.base';
   
   let mainWindowClass: window.Window | null = null;
   
   // Obtain the main window.
   class BaseContext {
     stageMode: boolean = false;
   }
   
   let context: BaseContext = { stageMode: false };
   window.getLastWindow(context, (err: BusinessError, data) => {
     let errCode: number = err.code;
     if (errCode) {
       console.error('Failed to get the subWindow. Cause: ' + JSON.stringify(err));
       return;
     }
     console.info('Succeeded in getting subWindow. Data: ' + JSON.stringify(data));
     mainWindowClass = data;
   });
   ```

2. Implement the immersive effect. You can use either of the following methods:

   - Method 1: When the main window of the application is a full-screen window, call **setWindowSystemBarEnable** to hide the status bar and navigation bar.
   - Method 2: Call **setWindowLayoutFullScreen** to enable the full-screen mode for the main window layout. Call **setWindowSystemBarProperties** to set the opacity, background color, text color, and highlighted icon of the status bar and navigation bar to create a display effect consistent with that of the main window.

   ```ts
   // Implement the immersive effect by hiding the status bar and navigation bar.
   let names: Array<'status' | 'navigation'> = [];
   let mainWindowClass: window.Window = window.findWindow("test");
   mainWindowClass.setWindowSystemBarEnable(names, (err: BusinessError) => {
     let errCode: number = err.code;
     if (errCode) {
       console.error('Failed to set the system bar to be visible. Cause:' + JSON.stringify(err));
       return;
     }
     console.info('Succeeded in setting the system bar to be visible.');
   });
   // Implement the immersive effect by setting the properties of the status bar and navigation bar.
    
   let isLayoutFullScreen: boolean = true;
   mainWindowClass.setWindowLayoutFullScreen(isLayoutFullScreen, (err: BusinessError) => {
     let errCode: number = err.code;
     if (errCode) {
       console.error('Failed to set the window layout to full-screen mode. Cause:' + JSON.stringify(err));
       return;
     }
     console.info('Succeeded in setting the window layout to full-screen mode.');
   });
   let sysBarProps: window.SystemBarProperties = {
     statusBarColor: '#ff00ff',
     navigationBarColor: '#00ff00',
     // The following properties are supported since API version 8.
     statusBarContentColor: '#ffffff',
     navigationBarContentColor: '#ffffff'
   };
   mainWindowClass.setWindowSystemBarProperties(sysBarProps, (err: BusinessError) => {
     let errCode: number = err.code;
     if (errCode) {
       console.error('Failed to set the system bar properties. Cause: ' + JSON.stringify(err));
       return;
     }
     console.info('Succeeded in setting the system bar properties.');
   });
   ```

3. Load content to and show the immersive window.

   Call **setUIContent** to load content to the immersive window and **showWindow** to show the window.

   ```ts
   // Load content to the immersive window.
   let mainWindowClass: window.Window = window.findWindow("test");
   mainWindowClass.setUIContent("pages/page3", (err: BusinessError) => {
     let errCode: number = err.code;
     if (errCode) {
       console.error('Failed to load the content. Cause: ' + JSON.stringify(err));
       return;
     }
     console.info('Succeeded in loading the content.');
     // Show the immersive window.
     mainWindowClass.showWindow((err: BusinessError) => {
       let errCode: number = err.code;
       if (errCode) {
         console.error('Failed to show the window. Cause: ' + JSON.stringify(err));
         return;
       }
       console.info('Succeeded in showing the window.');
     });
   });
   ```
