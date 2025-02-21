# Application Window Development (Stage Model)


## Basic Concepts

- Immersive window: a window display mode where the system windows (generally the status bar and navigation bar) are hidden to allow users to fully engage with the content.
  The immersive window feature is applicable only to the main window of an application in full-screen mode. It does not apply to a main window in freeform window mode or a subwindow (for example, a dialog box or a floating window).

- Floating window: a special application window that can still be displayed in the foreground when the main window and corresponding ability are running in the background.
  The floating window can be used to continue playing a video after the application is switched to the background, or offer a quick entry (for example, bubbles) to the application. Before creating a floating window, an application must apply for the required permission.


## When to Use

In the stage model, you can perform the following operations during application window development:

- Setting the properties and content of the main window of an application

- Setting the properties and content of the subwindow of an application

- Experiencing the immersive window feature

- Setting a floating window

 


## Available APIs

The table below lists the common APIs used for application window development. For details about more APIs, see [Window](../reference/apis/js-apis-window.md).

| Instance| API| Description|
| -------- | -------- | -------- |
| WindowStage | getMainWindow(callback: AsyncCallback&lt;Window&gt;): void | Obtains the main window of this window stage.<br>This API can be used only in the stage model.|
| WindowStage | loadContent(path: string, callback: AsyncCallback&lt;void&gt;): void | Loads content to the main window in this window stage.<br>**path**: path of the page from which the content will be loaded. The path is configured in the **main_pages.json** file of the project.<br>This API can be used only in the stage model.|
| WindowStage | createSubWindow(name: string, callback: AsyncCallback&lt;Window&gt;): void | Creates a subwindow.<br>This API can be used only in the stage model.|
| Window static method| createWindow(config: Configuration, callback: AsyncCallback\<Window>): void | Creates a system window.<br>**config**: parameters used for creating the window.|
| Window | setUIContent(path: string, callback: AsyncCallback&lt;void&gt;): void | Loads content to this window.<br>**path**: path of the page from which the content will be loaded. The path is configured in the **main_pages.json** file of the project in the stage model.|
| Window | setWindowBrightness(brightness: number, callback: AsyncCallback&lt;void&gt;): void | Sets the brightness for this window.|
| Window | setWindowTouchable(isTouchable: boolean, callback: AsyncCallback&lt;void&gt;): void | Sets whether this window is touchable.|
| Window | moveWindowTo(x: number, y: number, callback: AsyncCallback&lt;void&gt;): void | Moves this window.|
| Window | resize(width: number, height: number, callback: AsyncCallback&lt;void&gt;): void | Changes the window size.|
| Window | setWindowLayoutFullScreen(isLayoutFullScreen: boolean, callback: AsyncCallback&lt;void&gt;): void | Sets whether to enable the full-screen mode for the window layout. |
| Window | setWindowSystemBarEnable(names: Array&lt;'status'\|'navigation'&gt;): Promise&lt;void&gt; | Sets whether to display the status bar and navigation bar in this window.|
| Window | setWindowSystemBarProperties(systemBarProperties: SystemBarProperties, callback: AsyncCallback&lt;void&gt;): void | Sets the properties of the status bar and navigation bar in this window.<br>**systemBarProperties**: properties of the status bar and navigation bar.|
| Window | showWindow(callback: AsyncCallback\<void>): void | Shows this window.|
| Window | on(type: 'touchOutside', callback: Callback&lt;void&gt;): void | Subscribes to touch events outside this window.|
| Window | destroyWindow(callback: AsyncCallback&lt;void&gt;): void | Destroys this window.|


## Setting the Main Window of an Application

In the stage model, the main window of an application is created and maintained by a **UIAbility** instance. In the **onWindowStageCreate** callback of the **UIAbility** instance, use **WindowStage** to obtain the main window of the application and set its properties. You can also set the properties (for example, **maxWindowWidth**) in the [module.json5 file](../quick-start/module-configuration-file.md#abilities).

### How to Develop

1. Obtain the main window.

   Call **getMainWindow** to obtain the main window of the application.

2. Set the properties of the main window.

   You can set multiple properties of the main window, such as the background color, brightness, and whether the main window is touchable. The code snippet below uses the **touchable** property as an example.

3. Load content to the main window.

   Call **loadContent** to load content to the main window.

```ts
import UIAbility from '@ohos.app.ability.UIAbility';

export default class EntryAbility extends UIAbility {
    onWindowStageCreate(windowStage) {
        // 1. Obtain the main window of the application.
        let windowClass = null;
        windowStage.getMainWindow((err, data) => {
            if (err.code) {
                console.error('Failed to obtain the main window. Cause: ' + JSON.stringify(err));
                return;
            }
            windowClass = data;
            console.info('Succeeded in obtaining the main window. Data: ' + JSON.stringify(data));
            // 2. Set the touchable property of the main window.
            let isTouchable = true;
            windowClass.setWindowTouchable(isTouchable, (err) => {
                if (err.code) {
                    console.error('Failed to set the window to be touchable. Cause:' + JSON.stringify(err));
                    return;
                }
                console.info('Succeeded in setting the window to be touchable.');
            })
        })
        // 3. Load content to the main window.
        windowStage.loadContent("pages/page2", (err) => {
            if (err.code) {
                console.error('Failed to load the content. Cause:' + JSON.stringify(err));
                return;
            }
            console.info('Succeeded in loading the content.');
        });
    }
};
```

## Setting a Subwindow of an Application

You can create an application subwindow, such as a dialog box, and set its properties.

### How to Develop

1. Create a subwindow.

   Call **createSubWindow** to create a subwindow.

2. Set the properties of the subwindow.

   After the subwindow is created, you can set its properties, such as the size, position, background color, and brightness.

3. Load content to and show the subwindow.

   Call **setUIContent** to load content to the subwindow and **showWindow** to show the subwindow.

4. Destroy the subwindow.

   When the subwindow is no longer needed, you can call **destroyWindow** to destroy it.

```ts
import UIAbility from '@ohos.app.ability.UIAbility';

let windowStage_ = null;
let sub_windowClass = null;

export default class EntryAbility extends UIAbility {
  showSubWindow() {
    // 1. Create a subwindow.
    windowStage_.createSubWindow("mySubWindow", (err, data) => {
      if (err.code) {
        console.error('Failed to create the subwindow. Cause: ' + JSON.stringify(err));
        return;
      }
      sub_windowClass = data;
      console.info('Succeeded in creating the subwindow. Data: ' + JSON.stringify(data));
      // 2. Set the position, size, and other properties of the subwindow.
      sub_windowClass.moveWindowTo(300, 300, (err) => {
        if (err.code) {
          console.error('Failed to move the window. Cause:' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in moving the window.');
      });
      sub_windowClass.resize(500, 500, (err) => {
        if (err.code) {
          console.error('Failed to change the window size. Cause:' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in changing the window size.');
      });
      // 3. Load content to the subwindow.
      sub_windowClass.setUIContent("pages/page3", (err) => {
        if (err.code) {
          console.error('Failed to load the content. Cause:' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in loading the content.');
        // 3. Show the subwindow.
        sub_windowClass.showWindow((err) => {
          if (err.code) {
            console.error('Failed to show the window. Cause: ' + JSON.stringify(err));
            return;
          }
          console.info('Succeeded in showing the window.');
        });
      });
    })
  }

  destroySubWindow() {
    // 4. Destroy the subwindow when it is no longer needed (depending on the service logic).
    sub_windowClass.destroyWindow((err) => {
      if (err.code) {
        console.error('Failed to destroy the window. Cause: ' + JSON.stringify(err));
        return;
      }
      console.info('Succeeded in destroying the window.');
    });
  }

  onWindowStageCreate(windowStage) {
    windowStage_ = windowStage;
    // Create a subwindow when it is needed, for example, when a touch event occurs in the main window. Calling onWindowStageCreate is not always necessary. The code here is for reference only.
    this.showSubWindow();
  }

  onWindowStageDestroy() {
    // Destroy the subwindow when it is no longer needed, for example, when the Close button in the subwindow is touched. Calling onWindowStageDestroy is not always necessary. The code here is for reference only.
    this.destroySubWindow();
  }
};
```

## Experiencing the Immersive Window Feature

To create a better video watching and gaming experience, you can use the immersive window feature to hide the status bar and navigation bar. This feature is available only for the main window of an application.


### How to Develop

1. Obtain the main window.

   Call **getMainWindow** to obtain the main window of the application.

2. Implement the immersive effect. You can use either of the following methods:

   - Method 1: Call **setWindowSystemBarEnable** to hide the navigation bar and status bar.

   - Method 2: Call **setWindowLayoutFullScreen** to enable the full-screen mode for the main window layout. Call **setWindowSystemBarProperties** to set the opacity, background color, text color, and highlighted icon of the status bar and navigation bar to create a display effect consistent with that of the main window.
 
3. Load content to the immersive window.

   Call **loadContent** to load content to the immersive window.

```ts
import UIAbility from '@ohos.app.ability.UIAbility';

export default class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage) {
    // 1. Obtain the main window of the application.
    let windowClass = null;
    windowStage.getMainWindow((err, data) => {
      if (err.code) {
        console.error('Failed to obtain the main window. Cause: ' + JSON.stringify(err));
        return;
      }
      windowClass = data;
      console.info('Succeeded in obtaining the main window. Data: ' + JSON.stringify(data));

      // 2. Implement the immersive effect by hiding the status bar and navigation bar.
      let names = [];
      windowClass.setWindowSystemBarEnable(names, (err) => {
        if (err.code) {
          console.error('Failed to set the system bar to be visible. Cause:' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in setting the system bar to be visible.');
      });
      // 2. Alternatively, implement the immersive effect by setting the properties of the status bar and navigation bar.
      let isLayoutFullScreen = true;
      windowClass.setWindowLayoutFullScreen(isLayoutFullScreen, (err) => {
        if (err.code) {
          console.error('Failed to set the window layout to full-screen mode. Cause:' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in setting the window layout to full-screen mode.');
      });
      let sysBarProps = {
        statusBarColor: '#ff00ff',
        navigationBarColor: '#00ff00',
        // The following properties are supported since API version 8.
        statusBarContentColor: '#ffffff',
        navigationBarContentColor: '#ffffff'
      };
      windowClass.setWindowSystemBarProperties(sysBarProps, (err) => {
        if (err.code) {
          console.error('Failed to set the system bar properties. Cause: ' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in setting the system bar properties.');
      });
    })
    // 3. Load content to the immersive window.
    windowStage.loadContent("pages/page2", (err) => {
      if (err.code) {
        console.error('Failed to load the content. Cause:' + JSON.stringify(err));
        return;
      }
      console.info('Succeeded in loading the content.');
    });
  }
};
```

## Setting a Floating Window

A floating window is created based on an existing task. It is always displayed in the foreground, even if the task used for creating the floating window is switched to the background. Generally, the floating window is above all application windows. You can create a floating window and set its properties.


### How to Develop

**Prerequisites**: To create a floating window (a window of the type **WindowType.TYPE_FLOAT**), you must request the **ohos.permission.SYSTEM_FLOAT_WINDOW** permission. For details, see [Declaring Permissions in the Configuration File](../security/accesstoken-guidelines.md#declaring-permissions-in-the-configuration-file).

1. Create a floating window.

   Call **window.createWindow** to create a floating window.

2. Set properties of the floating window.

   After the floating window is created, you can set its properties, such as the size, position, background color, and brightness.

3. Load content to and show the floating window.

   Call **setUIContent** to load content to the floating window and **showWindow** to show the window.

4. Destroy the floating window.

   When the floating window is no longer needed, you can call **destroyWindow** to destroy it.

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';

export default class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage) {
    // 1. Create a floating window.
    let windowClass = null;
    let config = {name: "floatWindow", windowType: window.WindowType.TYPE_FLOAT, ctx: this.context};
    window.createWindow(config, (err, data) => {
      if (err.code) {
        console.error('Failed to create the floatWindow. Cause: ' + JSON.stringify(err));
        return;
      }
      console.info('Succeeded in creating the floatWindow. Data: ' + JSON.stringify(data));
      windowClass = data;
      // 2. Set the position, size, and other properties of the floating window.
      windowClass.moveWindowTo(300, 300, (err) => {
        if (err.code) {
          console.error('Failed to move the window. Cause:' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in moving the window.');
      });
      windowClass.resize(500, 500, (err) => {
        if (err.code) {
          console.error('Failed to change the window size. Cause:' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in changing the window size.');
      });
      // 3. Load content to the floating window.
      windowClass.setUIContent("pages/page4", (err) => {
        if (err.code) {
          console.error('Failed to load the content. Cause:' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in loading the content.');
        // 3. Show the floating window.
        windowClass.showWindow((err) => {
          if (err.code) {
            console.error('Failed to show the window. Cause: ' + JSON.stringify(err));
            return;
          }
          console.info('Succeeded in showing the window.');
        });
      });
      // 4. Destroy the floating window when it is no longer needed (depending on the service logic).
      windowClass.destroyWindow((err) => {
        if (err.code) {
          console.error('Failed to destroy the window. Cause: ' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in destroying the window.');
      });
    });
  }
};
```

