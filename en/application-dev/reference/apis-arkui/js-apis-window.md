# @ohos.window (Window)

The **Window** module provides basic window management capabilities, such as creating and destroying the current window, setting properties for the current window, and managing and scheduling windows.

This module provides the following common window-related functions:

- [Window](#window): window instance, which is the basic unit managed by the window manager.
- [WindowStage](#windowstage9): window manager that manages windows.

> **NOTE**
>
> The initial APIs of this module are supported since API version 6. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```ts
import window from '@ohos.window';
```

## WindowType<sup>7+</sup>

Enumerates the window types.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

| Name                                 | Value | Description                                                                                    |
|-------------------------------------| ------ |----------------------------------------------------------------------------------------|
| TYPE_APP                            | 0      | Application subwindow.<br>**Model restriction**: This API can be used only in the FA model.                                                  |
| TYPE_SYSTEM_ALERT                   | 1      | System alert window.<br>**NOTE**<br>This property is supported since API version 7 and deprecated since API version 11.                               |
| TYPE_FLOAT<sup>9+</sup>             | 8      | Floating window.<br>**Model restriction**: This API can be used only in the stage model.<br>**Required permissions**: ohos.permission.SYSTEM_FLOAT_WINDOW |
| TYPE_DIALOG<sup>10+</sup>           | 16      | Modal window.<br>**Model restriction**: This API can be used only in the stage model.                                                |

## Configuration<sup>9+</sup>

Defines the parameters for creating a subwindow or system window.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

| Name | Type | Mandatory | Description                                                                         |
| ---------- | -------------------------- | -- |-----------------------------------------------------------------------------|
| name       | string                     | Yes | Name of the window.                                                                      |
| windowType | [WindowType](#windowtype7) | Yes | Window type.                                                                      |
| ctx        | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md) | No | Current application context. If no value is passed, no context is used.<br>In the FA model, do not pass in this parameter when creating a subwindow. Otherwise, an error is reported.<br>In the stage model, you must pass in this parameter when creating a floating window, modal window, or system window. |
| displayId  | number                     | No | ID of the current physical screen. If no value is passed, the default value **-1** is used. The value must be an integer.                                            |
| parentId   | number                     | No | ID of the parent window. If no value is passed, the default value **-1** is used. The value must be an integer.                                                          |

## AvoidAreaType<sup>7+</sup>

Enumerates the types of the area where the window cannot be displayed.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

| Name                            | Value  | Description                                                        |
| -------------------------------- | ---- | ------------------------------------------------------------ |
| TYPE_SYSTEM                      | 0    | Default area of the system. Generally, the status bar and navigation bar are included. The default area may vary according to the device in use. |
| TYPE_CUTOUT                      | 1    | Notch.                                            |
| TYPE_SYSTEM_GESTURE<sup>9+</sup> | 2    | Gesture area.                                              |
| TYPE_KEYBOARD<sup>9+</sup>       | 3    | Soft keyboard area.                                            |
| TYPE_NAVIGATION_INDICATOR<sup>11+</sup> | 4    | Navigation bar area.                                     |

## SystemBarProperties

Describes the properties of the status bar and navigation bar.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

| Name                                  | Type |  Mandatory | Description                                                        |
| -------------------------------------- | -------- | ---- | ------------------------------------------------------------ |
| statusBarColor                         | string   |  No  | Background color of the status bar. The value is a hexadecimal RGB or ARGB color code and is case insensitive, for example, **'#00FF00'** or **'#FF00FF00'**. The default value is **'#0x66000000'**. |
| isStatusBarLightIcon<sup>7+</sup>      | boolean  |  No  | Whether any icon on the status bar is highlighted. The value **true** means that the icon is highlighted, and **false** means the opposite. The default value is **false**. |
| statusBarContentColor<sup>8+</sup>     | string   |  No  | Color of the text on the status bar. After this property is set, the setting of **isStatusBarLightIcon** is invalid. The default value is **'#0xE5FFFFFF'**. |
| navigationBarColor                     | string   |  No  | Background color of the navigation bar. The value is a hexadecimal RGB or ARGB color code and is case insensitive, for example, **'#00FF00'** or **'#FF00FF00'**. The default value is **'#0x66000000'**. |
| isNavigationBarLightIcon<sup>7+</sup>  | boolean  |  No  | Whether any icon on the navigation bar is highlighted. The value **true** means that the icon is highlighted, and **false** means the opposite. The default value is **false**. |
| navigationBarContentColor<sup>8+</sup> | string   |  No  | Color of the text on the navigation bar. After this property is set, the setting of **isNavigationBarLightIcon** is invalid. The default value is **'#0xE5FFFFFF'**. |

## Orientation<sup>9+</sup>

Enumerates the window orientations.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

| Name                                 | Value  | Description                         |
| ------------------------------------- | ---- | ----------------------------- |
| UNSPECIFIED                           | 0    | Unspecified. The orientation is determined by the system. |
| PORTRAIT                              | 1    | Portrait.            |
| LANDSCAPE                             | 2    | Landscape.  |
| PORTRAIT_INVERTED                     | 3    | Reverse portrait.  |
| LANDSCAPE_INVERTED                    | 4    | Reverse landscape. |
| AUTO_ROTATION                         | 5    | Automatically rotates with the sensor. The orientation can be portrait, landscape, reverse portrait, or reverse landscape. |
| AUTO_ROTATION_PORTRAIT                | 6    | Automatically rotates with the sensor in the vertical direction. The orientation can be portrait or reverse portrait. |
| AUTO_ROTATION_LANDSCAPE               | 7    | Automatically rotates with the sensor in the horizontal direction. The orientation can be landscape or reverse landscape. |
| AUTO_ROTATION_RESTRICTED              | 8    | Automatically rotates with the sensor, under the restriction of the rotation switch in the Control Panel. The orientation can be portrait, landscape, reverse portrait, or reverse landscape. |
| AUTO_ROTATION_PORTRAIT_RESTRICTED     | 9    | Automatically rotates with the sensor, under the restriction of the rotation switch in the Control Panel. The orientation can be portrait or reverse portrait. |
| AUTO_ROTATION_LANDSCAPE_RESTRICTED    | 10   | Automatically rotates with the sensor, under the restriction of the rotation switch in the Control Panel. The orientation can be landscape or reverse landscape. |
| LOCKED                                | 11   | Locked. |

## Rect<sup>7+</sup>

Describes the rectangular area of the window.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

| Name  | Type | Readable | Writable | Description              |
| ------ | -------- | ---- | ---- | ------------------ |
| left   | number   | Yes  | Yes  | Left boundary of the rectangle, in px. The value must be an integer. |
| top    | number   | Yes  | Yes  | Top boundary of the rectangle, in px. The value must be an integer. |
| width  | number   | Yes  | Yes  | Width of the rectangle, in px. The value must be an integer. |
| height | number   | Yes  | Yes  | Height of the rectangle, in px. The value must be an integer. |

## AvoidArea<sup>7+</sup>

Describes the area where the window cannot be displayed, for example, the system bar area, notch, gesture area, and soft keyboard area. Touch events will not be responded in this area. 
 
Pay attention to the following restrictions on this area: 

- The non-navigation bar area in the gesture area at the bottom supports transparent transmission of touch events, touch and hold events, but not drag events. 

- The gesture area on the left and right sides supports transparent transmission of touch events, touch and hold events, and swipe up and down events, but not drag events. 

- The navigation bar area supports responding to touch events, touch and hold events, and drag events. However, it does not support transparent transmission of events. 

**System capability**: SystemCapability.WindowManager.WindowManager.Core

| Name      | Type     | Readable | Writable | Description              |
| ---------- | ------------- | ---- | ---- | ------------------ |
| visible<sup>9+</sup>    | boolean       | Yes  | Yes  | Whether the window can be displayed in the area. The value **true** means that the window can be displayed in the area, and **false** means the opposite. |
| leftRect   | [Rect](#rect7) | Yes  | Yes  | Rectangle on the left of the screen. |
| topRect    | [Rect](#rect7) | Yes  | Yes  | Rectangle at the top of the screen. |
| rightRect  | [Rect](#rect7) | Yes  | Yes  | Rectangle on the right of the screen. |
| bottomRect | [Rect](#rect7) | Yes  | Yes  | Rectangle at the bottom of the screen. |

## Size<sup>7+</sup>

Describes the window size.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

| Name  | Type | Readable | Writable | Description      |
| ------ | -------- | ---- | ---- | ---------- |
| width  | number   | Yes  | Yes  | Window width, in px. The value must be an integer. |
| height | number   | Yes  | Yes  | Window height, in px. The value must be an integer. |

## WindowProperties

Describes the window properties.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

| Name                                 | Type                 | Readable | Writable | Description                                                                                                    |
| ------------------------------------- | ------------------------- | ---- | ---- |--------------------------------------------------------------------------------------------------------|
| windowRect<sup>7+</sup>               | [Rect](#rect7)             | Yes  | Yes  | Window size.                                                                                                 |
| drawableRect<sup>11+</sup>            | [Rect](#rect7)             | Yes  | Yes  | Size of the rectangle that can be drawn in the window. The upper boundary and left boundary are calculated relative to the window.                                                                                                 |
| type<sup>7+</sup>                     | [WindowType](#windowtype7) | Yes  | Yes  | Window type.                                                                                                 |
| isFullScreen                          | boolean                   | Yes  | Yes  | Whether the window is displayed in full-screen mode. The default value is **false**. The value **true** means that the window is displayed in full-screen mode, and **false** means the opposite.                                                                    |
| isLayoutFullScreen<sup>7+</sup>       | boolean                   | Yes  | Yes  | Whether the window layout is in full-screen mode (whether the window is immersive). The default value is **false**. The value **true** means that the window is immersive, and **false** means the opposite.                                                              |
| focusable<sup>7+</sup>                | boolean                   | Yes  | No  | Whether the window can gain focus. The default value is **true**. The value **true** means that the window can gain focus, and **false** means the opposite.                                                                |
| touchable<sup>7+</sup>                | boolean                   | Yes  | No  | Whether the window is touchable. The default value is **true**. The value **true** means that the window is touchable, and **false** means the opposite.                                                                |
| brightness                            | number                    | Yes  | Yes  | Screen brightness. The value is a floating point number in the range [0.0, 1.0], and the value **1.0** means the brightest. If no value is passed, the brightness follows the system. In this case, the obtained brightness value is **-1**.                     |
| dimBehindValue<sup>(deprecated)</sup> | number                    | Yes  | Yes  | Dimness of the window that is not on top. The value is a floating point number in the range [0.0, 1.0], and the value **1.0** means the dimmest.<br>**NOTE**<br>This property is supported since API version 7 and deprecated since API version 9.  |
| isKeepScreenOn                        | boolean                   | Yes  | Yes  | Whether the screen is always on. The default value is **false**. The value **true** means that the screen is always on, and **false** means the opposite.                                                                  |
| isPrivacyMode<sup>7+</sup>            | boolean                   | Yes  | Yes  | Whether the window is in privacy mode. The default value is **false**. The value **true** means that the window is in privacy mode, and **false** means the opposite.                                                                 |
| isRoundCorner<sup>(deprecated)</sup>  | boolean                   | Yes  | Yes  | Whether the window has rounded corners. The default value is **false**. The value **true** means that the window has rounded corners, and **false** means the opposite.<br>**NOTE**<br>This property is supported since API version 7 and deprecated since API version 9.      |
| isTransparent<sup>7+</sup>            | boolean                   | Yes  | Yes  | Whether the window is transparent. The default value is **false**. The value **true** means that the window is transparent, and **false** means the opposite.                                                                  |
| id<sup>9+</sup>                       | number                    | Yes  | No  | Window ID. The default value is **0**. The value must be an integer.                                                                                   |

## ColorSpace<sup>8+</sup>

Enumerates the color spaces.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

| Name      | Value | Description          |
| ---------- | ------ | -------------- |
| DEFAULT    | 0      | Default SRGB gamut. |
| WIDE_GAMUT | 1      | Wide-gamut.  |

## WindowEventType<sup>10+</sup>

Enumerates the window lifecycle states.

| Name      | Value | Description      |
| ---------- | ------ | ---------- |
| WINDOW_SHOWN      | 1      | The window is running in the foreground.<br>**System capability**: SystemCapability.WindowManager.WindowManager.Core|
| WINDOW_ACTIVE     | 2      | The window gains focus.<br>**System capability**: SystemCapability.WindowManager.WindowManager.Core|
| WINDOW_INACTIVE   | 3      | The window loses focus.<br>**System capability**: SystemCapability.WindowManager.WindowManager.Core|
| WINDOW_HIDDEN     | 4      | The window is running in the background.<br>**System capability**: SystemCapability.WindowManager.WindowManager.Core|
| WINDOW_DESTROYED<sup>11+</sup>  | 7      | The window is destroyed.<br>**System capability**: SystemCapability.Window.SessionManager|

## WindowLimits<sup>11+</sup>

Defines the window size limits. You can call [setWindowLimits](#setwindowlimits11) to set the window size limits and call [getWindowLimits](#getwindowlimits11) to obtain the current window size limits.

**System capability**: SystemCapability.Window.SessionManager

| Name     | Type  | Readable | Writable | Description                                                        |
| :-------- | :----- | :--- | :--- | :----------------------------------------------------------- |
| maxWidth  | number | Yes  | Yes  | Maximum window width, in px. The value must be an integer. The default value is **0**, indicating that the property does not change. The lower limit is **0**, and the upper limit is the maximum width specified by the system. |
| maxHeight | number | Yes  | Yes  | Maximum window height, in px. The value must be an integer. The default value is **0**, indicating that the property does not change. The lower limit is **0**, and the upper limit is the maximum height specified by the system. |
| minWidth  | number | Yes  | Yes  | Minimum window width, in px. The value must be an integer. The default value is **0**, indicating that the property does not change. The lower limit is **0**, and the upper limit is the minimum width specified by the system. |
| minHeight | number | Yes  | Yes  | Minimum window height, in px. The value must be an integer. The default value is **0**, indicating that the property does not change. The lower limit is **0**, and the upper limit is the minimum height specified by the system. |

## WindowStatusType<sup>11+</sup>

Enumerates the window modes.

**System capability**: SystemCapability.Window.SessionManager

| Name      | Value  | Description                         |
| ---------- | ---- | ----------------------------- |
| UNDEFINED  | 0    | The window mode is not defined by the application.      |
| FULL_SCREEN | 1    | The application is displayed in full screen.            |
| MAXIMIZE    | 2    | The application window is maximized.  |
| MINIMIZE    | 3    | The application window is minimized.  |
| FLOATING    | 4    | The application is displayed in a floating window.  |
| SPLIT_SCREEN  | 5    | The application is displayed in split-screen mode.  |

## TitleButtonRect<sup>11+</sup>

Defines the rectangle used to hold the minimize, maximize, and close buttons on the title bar. This rectangle is located in the upper right corner of the window.

**System capability**: SystemCapability.Window.SessionManager

| Name  | Type  | Readable | Writable | Description                                      |
| ------ | ------ | ---- | ---- | ------------------------------------------ |
| right  | number | Yes  | Yes  | Right boundary of the rectangle, in vp. The value must be an integer. |
| top    | number | Yes  | Yes  | Top boundary of the rectangle, in vp. The value must be an integer. |
| width  | number | Yes  | Yes  | Width of the rectangle, in vp. The value must be an integer.  |
| height | number | Yes  | Yes  | Height of the rectangle, in vp. The value must be an integer.  |

## window.createWindow<sup>9+</sup>

createWindow(config: Configuration, callback: AsyncCallback&lt;Window&gt;): void

Creates a subwindow or system window. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| -------- | -------------------------------------- | -- | --------------------------------- |
| config   | [Configuration](#configuration9)       | Yes | Parameters used for creating the window.  |
| callback | AsyncCallback&lt;[Window](#window)&gt; | Yes | Callback used to return the window created. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------- |
| 1300001 | Repeated operation. |
| 1300006 | This window context is abnormal. |
| 1300008 | The operation is on invalid display. |
| 1300009 | The parent window is invalid. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
let config: window.Configuration = {
  name: "test",
  windowType: window.WindowType.TYPE_DIALOG,
  ctx: this.context
};
try {
  window.createWindow(config, (err: BusinessError, data) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to create the window. Cause: ' + JSON.stringify(err));
      return;
    }
    windowClass = data;
    console.info('Succeeded in creating the window. Data: ' + JSON.stringify(data));
    windowClass.resize(500, 1000);
  });
} catch (exception) {
  console.error('Failed to create the window. Cause: ' + JSON.stringify(exception));
}
```

## window.createWindow<sup>9+</sup>

createWindow(config: Configuration): Promise&lt;Window&gt;

Creates a subwindow or system window. This API uses a promise to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| ------ | -------------------------------- | -- | ------------------ |
| config | [Configuration](#configuration9) | Yes | Parameters used for creating the window. |

**Return value**

| Type | Description |
| -------------------------------- | ------------------------------------ |
| Promise&lt;[Window](#window)&gt; | Promise used to return the window created. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------- |
| 1300001 | Repeated operation. |
| 1300006 | This window context is abnormal. |
| 1300008 | The operation is on invalid display. |
| 1300009 | The parent window is invalid. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
let config: window.Configuration = {
  name: "test",
  windowType: window.WindowType.TYPE_DIALOG,
  ctx: this.context
};
try {
  let promise = window.createWindow(config);
  promise.then((data) => {
    windowClass = data;
    console.info('Succeeded in creating the window. Data:' + JSON.stringify(data));
  }).catch((err: BusinessError) => {
    console.error('Failed to create the Window. Cause:' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to create the window. Cause: ' + JSON.stringify(exception));
}
```

## window.findWindow<sup>9+</sup>

findWindow(name: string): Window

Finds a window based on the name.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type  | Mandatory | Description    |
| ------ | ------ | ---- | -------- |
| name   | string | Yes  | Window name, that is, the value of **name** in [Configuration](#configuration9). |

**Return value**

| Type | Description |
| ----------------- | ------------------- |
| [Window](#window) | Window found. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------- |
| 1300002 | This window state is abnormal. |

**Example**

```ts
let windowClass: window.Window | undefined = undefined;
try {
  windowClass = window.findWindow('test');
} catch (exception) {
  console.error('Failed to find the Window. Cause: ' + JSON.stringify(exception));
}
```

## window.getLastWindow<sup>9+</sup>

getLastWindow(ctx: BaseContext, callback: AsyncCallback&lt;Window&gt;): void

Obtains the top window of the current application. This API uses an asynchronous callback to return the result. If no subwindow is available, the main window of the application is returned.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| -------- | -------------------------------------- | -- | ---------------------------------------- |
| ctx      | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md) | Yes | Current application context. |
| callback | AsyncCallback&lt;[Window](#window)&gt; | Yes | Callback used to return the top window obtained. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------- |
| 1300002 | This window state is abnormal.   |
| 1300006 | This window context is abnormal. |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...
  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    try {
      window.getLastWindow(this.context, (err: BusinessError, data) => {
        const errCode: number = err.code;
        if (errCode) {
          console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(err));
          return;
        }
        windowClass = data;
        console.info('Succeeded in obtaining the top window. Data: ' + JSON.stringify(data));
      });
    } catch (exception) {
      console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(exception));
    }
  }
}
```

## window.getLastWindow<sup>9+</sup>

getLastWindow(ctx: BaseContext): Promise&lt;Window&gt;

Obtains the top window of the current application. This API uses a promise to return the result. If no subwindow is available, the main window of the application is returned.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| ------ | ----------- | ---- | ------------------------------------------------------------ |
| ctx    | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md) | Yes  | Current application context. |

**Return value**

| Type | Description |
| -------------------------------- | ------------------------------------------- |
| Promise&lt;[Window](#window)&gt; | Promise used to return the top window obtained. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------- |
| 1300002 | This window state is abnormal.   |
| 1300006 | This window context is abnormal. |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...
  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    try {
      let promise = window.getLastWindow(this.context);
      promise.then((data) => {
        windowClass = data;
        console.info('Succeeded in obtaining the top window. Data: ' + JSON.stringify(data));
      }).catch((err: BusinessError) => {
        console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(err));
      });
    } catch (exception) {
      console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(exception));
    }
  }
}
```

## window.shiftAppWindowFocus<sup>11+</sup>
shiftAppWindowFocus(sourceWindowId: number, targetWindowId: number): Promise&lt;void&gt;

Shifts the window focus from the source window to the target window in the same application. The window focus can be shifted between the main window and a subwindow.

**System capability**: SystemCapability.Window.SessionManager

**Parameters**

| Name         | Type  | Mandatory | Description                   |
| -------------- | ------ | ----- | ----------------------- |
| sourceWindowId | number | Yes   | ID of the source window, which is having the focus.|
| targetWindowId | number | Yes   | ID of the target window.            |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message                                     |
| ------- | --------------------------------------------- |
| 1300002 | This window state is abnormal.                |
| 1300003 | This window manager service works abnormally. |
| 1300004 | Unauthorized operation.                       |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    // ...
    console.info('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    let subWindowClass: window.Window | undefined = undefined;
    let windowClassId: number = -1;
    let subWindowClassId: number = -1;

    // Obtain the main window and ID of the application.
    try {
      let promise = windowStage.getMainWindow();
      promise.then((data) => {
        if (data == null) {
          console.error("Failed to obtaining the window. Cause: The data is empty");
          return;
        }
        windowClass = data;
        windowClass.setUIContent("pages/Index");
        try {
          windowClassId = windowClass.getWindowProperties().id;
        } catch (exception) {
          console.error('Failed to obtain the window. Cause: ' + JSON.stringify(exception))
        }
        console.info('Succeeded in obtaining the window')
      }).catch((err: BusinessError) => {
        console.error('Failed to obtaining the window. Cause: ' + JSON.stringify(err))
      })
    } catch (exception) {
      console.error('Failed to obtain the window. Cause: ' + JSON.stringify(exception))
    }

    // Create or obtain a subwindow and its ID. In this case, the subwindow has focus.
    try {
      let promise = windowStage.createSubWindow("testSubWindow");
      promise.then((data) => {
        if (data == null) {
          console.error("Failed to obtaining the window. Cause: The data is empty");
          return;
        }
        subWindowClass = data;
        try {
          subWindowClassId = subWindowClass.getWindowProperties().id;
        } catch (exception) {
          console.error('Failed to obtain the window. Cause: ' + JSON.stringify(exception))
        }
        subWindowClass.resize(500, 500);
        subWindowClass.setUIContent("pages/Index2");
        subWindowClass.showWindow();

        // Listen for the window status and ensure that the window is ready.
        subWindowClass.on("windowEvent", (windowEvent) => {
          if (windowEvent == window.WindowEventType.WINDOW_ACTIVE) {
            // Switch the focus.
            try {
              let promise = window.shiftAppWindowFocus(subWindowClassId, windowClassId);
              promise.then(() => {
                console.info('Succeeded in shifting app window focus');
              }).catch((err: BusinessError) => {
                console.error('Failed to shift app window focus. Cause: ' + JSON.stringify(err));
              })
            } catch (exception) {
              console.error('Failed to shift app window focus. Cause: ' + JSON.stringify(exception));
            }
          }
        })
      })
    } catch (exception) {
      console.error('Failed to create the subWindow. Cause: ' + JSON.stringify(exception));
    }
  }
}
```

## window.create<sup>(deprecated)</sup>

create(id: string, type: WindowType, callback: AsyncCallback&lt;Window&gt;): void

Creates a subwindow. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [createWindow()](#windowcreatewindow9) instead.

**Model restriction**: This API can be used only in the FA model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                  | Mandatory | Description                                |
| -------- | -------------------------------------- | ---- | ------------------------------------ |
| id       | string                                 | Yes  | Window name, that is, the value of **name** in [Configuration](#configuration9).|
| type     | [WindowType](#windowtype7)              | Yes  | Window type.                          |
| callback | AsyncCallback&lt;[Window](#window)&gt; | Yes  | Callback used to return the subwindow created. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
window.create('test', window.WindowType.TYPE_APP, (err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to create the subWindow. Cause: ' + JSON.stringify(err));
    return;
  }
  windowClass = data;
  console.info('Succeeded in creating the subWindow. Data: ' + JSON.stringify(data));
});
```

## window.create<sup>(deprecated)</sup>

create(id: string, type: WindowType): Promise&lt;Window&gt;

Creates a subwindow. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [createWindow()](#windowcreatewindow9-1) instead.

**Model restriction**: This API can be used only in the FA model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type                     | Mandatory | Description      |
| ------ | ------------------------- | ---- | ---------- |
| id     | string                    | Yes  | Window name, that is, the value of **name** in [Configuration](#configuration9).  |
| type   | [WindowType](#windowtype7) | Yes  | Window type. |

**Return value**

| Type                            | Description                                   |
| -------------------------------- | --------------------------------------- |
| Promise&lt;[Window](#window)&gt; | Promise used to return the subwindow created. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
let promise = window.create('test', window.WindowType.TYPE_APP);
promise.then((data) => {
  windowClass = data;
  console.info('Succeeded in creating the subWindow. Data: ' + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error('Failed to create the subWindow. Cause: ' + JSON.stringify(err));
});
```

## window.create<sup>(deprecated)</sup>

create(ctx: BaseContext, id: string, type: WindowType, callback: AsyncCallback&lt;Window&gt;): void

Creates a system window. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [createWindow()](#windowcreatewindow9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                                   | Mandatory | Description                                |
| -------- | ------------------------------------------------------- | ---- | ------------------------------------ |
| ctx      | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md) | Yes  | Current application context.                |
| id       | string                                                  | Yes  | Window name, that is, the value of **name** in [Configuration](#configuration9).  |
| type     | [WindowType](#windowtype7)                              | Yes  | Window type.                          |
| callback | AsyncCallback&lt;[Window](#window)&gt;                  | Yes  | Callback used to return the subwindow created. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
window.create('test', window.WindowType.TYPE_SYSTEM_ALERT, (err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to create the window. Cause: ' + JSON.stringify(err));
    return;
  }
  windowClass = data;
  console.info('Succeeded in creating the window. Data: ' + JSON.stringify(data));
  windowClass.resetSize(500, 1000);
});
```

## window.create<sup>(deprecated)</sup>

create(ctx: BaseContext, id: string, type: WindowType): Promise&lt;Window&gt;

Creates a system window. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [createWindow()](#windowcreatewindow9-1) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type                     | Mandatory | Description                                                        |
| ------ | ------------------------- | ---- | ------------------------------------------------------------ |
| ctx    | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md) | Yes  | Current application context. |
| id     | string                    | Yes  | Window name, that is, the value of **name** in [Configuration](#configuration9). |
| type   | [WindowType](#windowtype7) | Yes  | Window type.                                                  |

**Return value**

| Type                            | Description                                   |
| -------------------------------- | --------------------------------------- |
| Promise&lt;[Window](#window)&gt; | Promise used to return the subwindow created. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
let promise = window.create('test', window.WindowType.TYPE_SYSTEM_ALERT);
promise.then((data) => {
  windowClass = data;
  console.info('Succeeded in creating the window. Data:' + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error('Failed to create the Window. Cause:' + JSON.stringify(err));
});
```

## window.find<sup>(deprecated)</sup>

find(id: string, callback: AsyncCallback&lt;Window&gt;): void

Finds a window based on the ID. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [findWindow()](#windowfindwindow9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                  | Mandatory | Description                                |
| -------- | -------------------------------------- | ---- | ------------------------------------ |
| id       | string                                 | Yes  | Window name, that is, the value of **name** in [Configuration](#configuration9). |
| callback | AsyncCallback&lt;[Window](#window)&gt; | Yes  | Callback used to return the window found. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
window.find('test', (err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to find the Window. Cause: ' + JSON.stringify(err));
    return;
  }
  windowClass = data;
  console.info('Succeeded in finding the window. Data: ' + JSON.stringify(data));
});
```

## window.find<sup>(deprecated)</sup>

find(id: string): Promise&lt;Window&gt;

Finds a window based on the ID. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [findWindow()](#windowfindwindow9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type  | Mandatory | Description    |
| ------ | ------ | ---- | -------- |
| id     | string | Yes  | Window name, that is, the value of **name** in [Configuration](#configuration9). |

**Return value**

| Type                            | Description                                 |
| -------------------------------- | ------------------------------------- |
| Promise&lt;[Window](#window)&gt; | Promise used to return the window found. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
let promise = window.find('test');
promise.then((data) => {
  windowClass = data;
  console.info('Succeeded in finding the window. Data: ' + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error('Failed to find the Window. Cause: ' + JSON.stringify(err));
});
```

## window.getTopWindow<sup>(deprecated)</sup>

getTopWindow(callback: AsyncCallback&lt;Window&gt;): void

Obtains the top window of the current application. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 6 and deprecated since API version 9. You are advised to use [getLastWindow()](#windowgetlastwindow9) instead.

**Model restriction**: This API can be used only in the FA model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                  | Mandatory | Description                                        |
| -------- | -------------------------------------- | ---- | -------------------------------------------- |
| callback | AsyncCallback&lt;[Window](#window)&gt; | Yes  | Callback used to return the top window obtained. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
window.getTopWindow((err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(err));
    return;
  }
  windowClass = data;
  console.info('Succeeded in obtaining the top window. Data: ' + JSON.stringify(data));
});
```

## window.getTopWindow<sup>(deprecated)</sup>

getTopWindow(): Promise&lt;Window&gt;

Obtains the top window of the current application. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 6 and deprecated since API version 9. You are advised to use [getLastWindow()](#windowgetlastwindow9-1) instead.

**Model restriction**: This API can be used only in the FA model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Return value**

| Type                            | Description                                           |
| -------------------------------- | ----------------------------------------------- |
| Promise&lt;[Window](#window)&gt; | Promise used to return the top window obtained. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let windowClass: window.Window | undefined = undefined;
let promise = window.getTopWindow();
promise.then((data)=> {
  windowClass = data;
  console.info('Succeeded in obtaining the top window. Data: ' + JSON.stringify(data));
}).catch((err: BusinessError)=>{
  console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(err));
});
```

## window.getTopWindow<sup>(deprecated)</sup>

getTopWindow(ctx: BaseContext, callback: AsyncCallback&lt;Window&gt;): void

Obtains the top window of the current application. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [getLastWindow()](#windowgetlastwindow9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                  | Mandatory | Description                                                        |
| -------- | -------------------------------------- | ---- | ------------------------------------------------------------ |
| ctx      | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md)                            | Yes  | Current application context. |
| callback | AsyncCallback&lt;[Window](#window)&gt; | Yes  | Callback used to return the top window obtained.                |

**Example**

```ts
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage:window.WindowStage){
    console.info('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    try {
      window.getTopWindow(this.context, (err: BusinessError, data) => {
        const errCode: number = err.code;
        if(errCode){
          console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(err));
          return ;
        }
        windowClass = data;
        console.info('Succeeded in obtaining the top window. Data: ' + JSON.stringify(data));
      });
    } catch(error){
      console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(error));
    }
  }
}
```

## window.getTopWindow<sup>(deprecated)</sup>

getTopWindow(ctx: BaseContext): Promise&lt;Window&gt;

Obtains the top window of the current application. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [getLastWindow()](#windowgetlastwindow9-1) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type   | Mandatory | Description                                                        |
| ------ | ----------- | ---- | ------------------------------------------------------------ |
| ctx    | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md) | Yes  | Current application context. |

**Return value**

| Type                            | Description                                           |
| -------------------------------- | ----------------------------------------------- |
| Promise&lt;[Window](#window)&gt; | Promise used to return the top window obtained. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage:window.WindowStage) {
    console.info('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    let promise = window.getTopWindow(this.context);
    promise.then((data) => {
      windowClass = data;
      console.info('Succeeded in obtaining the top window. Data: ' + JSON.stringify(data));
    }).catch((error: BusinessError) => {
      console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(error));
    });
  }
}
```

## SpecificSystemBar<sup>11+</sup>

Enumerates the types of system bars that can be displayed or hidden.

**System capability**: SystemCapability.Window.SessionManager

| Type      | Description    |
|------------|--------|
| 'status'   | Status bar.  |
| 'navigation'  | Navigation bar.  |
| 'navigationIndicator'  | Bottom navigation bar. |

## Window

Represents a window instance, which is the basic unit managed by the window manager.

In the following API examples, you must use [getLastWindow()](#windowgetlastwindow9), [createWindow()](#windowcreatewindow9), or [findWindow()](#windowfindwindow9) to obtain a **Window** instance (named windowClass in this example) and then call a method in this instance.

### showWindow<sup>9+</sup>

showWindow(callback: AsyncCallback&lt;void&gt;): void

Shows this window. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| -------- | ------------------------- | -- | --------- |
| callback | AsyncCallback&lt;void&gt; | Yes | Callback used to return the result. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

windowClass.showWindow((err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to show the window. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in showing the window.');
});
```

### showWindow<sup>9+</sup>

showWindow(): Promise&lt;void&gt;

Shows this window. This API uses a promise to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Return value**

| Type | Description |
| ------------------- | ----------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.showWindow();
promise.then(() => {
  console.info('Succeeded in showing the window.');
}).catch((err: BusinessError) => {
  console.error('Failed to show the window. Cause: ' + JSON.stringify(err));
});
```

### destroyWindow<sup>9+</sup>

destroyWindow(callback: AsyncCallback&lt;void&gt;): void

Destroys this window. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| -------- | ------------------------- | -- | --------- |
| callback | AsyncCallback&lt;void&gt; | Yes | Callback used to return the result. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

windowClass.destroyWindow((err) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to destroy the window. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in destroying the window.');
});
```

### destroyWindow<sup>9+</sup>

destroyWindow(): Promise&lt;void&gt;

Destroys this window. This API uses a promise to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Return value**

| Type | Description |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.destroyWindow();
promise.then(() => {
  console.info('Succeeded in destroying the window.');
}).catch((err: BusinessError) => {
  console.error('Failed to destroy the window. Cause: ' + JSON.stringify(err));
});
```

### moveWindowTo<sup>9+</sup>

moveWindowTo(x: number, y: number, callback: AsyncCallback&lt;void&gt;): void

Moves this window. This API uses an asynchronous callback to return the result.

This operation is not supported in a window in full-screen mode.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| -------- | ------------------------- | -- | --------------------------------------------- |
| x        | number                    | Yes | Distance that the window moves along the x-axis, in px. A positive value indicates that the window moves to the right. The value must be an integer. If a floating point number is passed in, the value is rounded down. |
| y        | number                    | Yes | Distance that the window moves along the y-axis, in px. A positive value indicates that the window moves downwards. The value must be an integer. If a floating point number is passed in, the value is rounded down. |
| callback | AsyncCallback&lt;void&gt; | Yes | Callback used to return the result.                                    |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

try {
  windowClass.moveWindowTo(300, 300, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to move the window. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in moving the window.');
  });
} catch (exception) {
  console.error('Failed to move the window. Cause:' + JSON.stringify(exception));
}
```

### moveWindowTo<sup>9+</sup>

moveWindowTo(x: number, y: number): Promise&lt;void&gt;

Moves this window. This API uses a promise to return the result.

This operation is not supported in a window in full-screen mode.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| -- | ----- | -- | --------------------------------------------- |
| x | number | Yes | Distance that the window moves along the x-axis, in px. A positive value indicates that the window moves to the right. The value must be an integer. If a floating point number is passed in, the value is rounded down. |
| y | number | Yes | Distance that the window moves along the y-axis, in px. A positive value indicates that the window moves downwards. The value must be an integer. If a floating point number is passed in, the value is rounded down. |

**Return value**

| Type | Description |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

try {
  let promise = windowClass.moveWindowTo(300, 300);
  promise.then(() => {
    console.info('Succeeded in moving the window.');
  }).catch((err: BusinessError) => {
    console.error('Failed to move the window. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to move the window. Cause:' + JSON.stringify(exception));
}
```

### resize<sup>9+</sup>

resize(width: number, height: number, callback: AsyncCallback&lt;void&gt;): void

Changes the size of this window. This API uses an asynchronous callback to return the result.

The main window and subwindow have the following default size limits: [320, 1920] in width and [240, 1920] in height, both in units of vp.
The minimum width and height of the main window and subwindow of the application depends on the configuration on the product side. You can call [getWindowLimits](#getwindowlimits11) to obtain size limits.

The system window has the following size limits: [0, 1920] in width and [0, 1920] in height, both in units of vp.

The window width and height you set must meet the limits. The rules are as follows:
- If the window width or height you set is less than the minimum width or height limit, then the minimum width or height limit takes effect.
- If the window width or height you set is greater than the maximum width or height limit, then the maximum width or height limit takes effect.

This operation is not supported in a window in full-screen mode.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| -------- | ------------------------- | -- | ------------------------ |
| width    | number                    | Yes | New width of the window, in px. The value must be an integer. If a floating point number is passed in, the value is rounded down. A negative value is invalid. |
| height   | number                    | Yes | New height of the window, in px. The value must be an integer. If a floating point number is passed in, the value is rounded down. A negative value is invalid. |
| callback | AsyncCallback&lt;void&gt; | Yes | Callback used to return the result.               |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

try {
  windowClass.resize(500, 1000, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to change the window size. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in changing the window size.');
  });
} catch (exception) {
  console.error('Failed to change the window size. Cause:' + JSON.stringify(exception));
}
```

### resize<sup>9+</sup>

resize(width: number, height: number): Promise&lt;void&gt;

Changes the size of this window. This API uses a promise to return the result.

The main window and subwindow have the following default size limits: [320, 1920] in width and [240, 1920] in height, both in units of vp.
The minimum width and height of the main window and subwindow of the application depends on the configuration on the product side. You can call [getWindowLimits](#getwindowlimits11) to obtain size limits.

The system window has the following size limits: [0, 1920] in width and [0, 1920] in height, both in units of vp.

The window width and height you set must meet the limits. The rules are as follows:
- If the window width or height you set is less than the minimum width or height limit, then the minimum width or height limit takes effect.
- If the window width or height you set is greater than the maximum width or height limit, then the maximum width or height limit takes effect.

This operation is not supported in a window in full-screen mode.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| ------ | ------ | -- | ------------------------ |
| width  | number | Yes | New width of the window, in px. The value must be an integer. If a floating point number is passed in, the value is rounded down. A negative value is invalid. |
| height | number | Yes | New height of the window, in px. The value must be an integer. If a floating point number is passed in, the value is rounded down. A negative value is invalid. |

**Return value**

| Type | Description |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

try {
  let promise = windowClass.resize(500, 1000);
  promise.then(() => {
    console.info('Succeeded in changing the window size.');
  }).catch((err: BusinessError) => {
    console.error('Failed to change the window size. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to change the window size. Cause: ' + JSON.stringify(exception));
}
```

### getWindowProperties<sup>9+</sup>

getWindowProperties(): WindowProperties

Obtains the properties of this window.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Return value**

| Type | Description |
| ------------------------------------- | ------------- |
| [WindowProperties](#windowproperties) | Window properties obtained. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**Example**

```ts
try {
  let properties = windowClass.getWindowProperties();
} catch (exception) {
  console.error('Failed to obtain the window properties. Cause: ' + JSON.stringify(exception));
}
```

### getWindowAvoidArea<sup>9+</sup>

getWindowAvoidArea(type: AvoidAreaType): AvoidArea

Obtains the area where this window cannot be displayed, for example, the system bar area, notch, gesture area, and soft keyboard area. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| ---- |----------------------------------| -- | ------------------------------------------------------------ |
| type | [AvoidAreaType](#avoidareatype7) | Yes | Type of the area. |

**Return value**

| Type | Description |
|--------------------------| ----------------- |
| [AvoidArea](#avoidarea7) | Area where the window cannot be displayed. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**Example**

```ts
let type = window.AvoidAreaType.TYPE_SYSTEM;
try {
  let avoidArea = windowClass.getWindowAvoidArea(type);
} catch (exception) {
  console.error('Failed to obtain the area. Cause:' + JSON.stringify(exception));
}
```

### setWindowLayoutFullScreen<sup>9+</sup>

setWindowLayoutFullScreen(isLayoutFullScreen: boolean, callback: AsyncCallback&lt;void&gt;): void

Sets whether the main window layout or the subwindow layout is immersive. This API uses an asynchronous callback to return the result.
An immersive layout means that the layout does not avoid the status bar and navigation bar, and components may overlap with them.
A non-immersive layout means that the layout avoids the status bar and navigation bar, and components do not overlap with them.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| ------------------ | ------------------------- | -- | --------- |
| isLayoutFullScreen | boolean                   | Yes | Whether the window layout is immersive. (The status bar and navigation bar of the immersive layout are still displayed.) The value **true** means that the window layout is immersive, and **false** means the opposite. |
| callback           | AsyncCallback&lt;void&gt; | Yes | Callback used to return the result. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isLayoutFullScreen = true;
try {
  windowClass.setWindowLayoutFullScreen(isLayoutFullScreen, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the window layout to full-screen mode. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the window layout to full-screen mode.');
  });
} catch (exception) {
  console.error('Failed to set the window layout to full-screen mode. Cause:' + JSON.stringify(exception));
}
```

### setWindowLayoutFullScreen<sup>9+</sup>

setWindowLayoutFullScreen(isLayoutFullScreen: boolean): Promise&lt;void&gt;

Sets whether the main window layout or the subwindow layout is immersive. This API uses a promise to return the result.
An immersive layout means that the layout does not avoid the status bar and navigation bar, and components may overlap with them.
A non-immersive layout means that the layout avoids the status bar and navigation bar, and components do not overlap with them.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| ------------------ | ------- | -- | ------------------------------------------------------------------------------------------------ |
| isLayoutFullScreen | boolean | Yes | Whether the window layout is immersive. (The status bar and navigation bar of the immersive layout are still displayed.) The value **true** means that the window layout is immersive, and **false** means the opposite. |

**Return value**

| Type | Description |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isLayoutFullScreen = true;
try {
  let promise = windowClass.setWindowLayoutFullScreen(isLayoutFullScreen);
  promise.then(() => {
    console.info('Succeeded in setting the window layout to full-screen mode.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the window layout to full-screen mode. Cause:' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the window layout to full-screen mode. Cause:' + JSON.stringify(exception));
}
```

### setWindowSystemBarEnable<sup>9+</sup>

setWindowSystemBarEnable(names: Array<'status' | 'navigation'>, callback: AsyncCallback&lt;void&gt;): void

Sets whether to display the status bar and navigation bar when the window is in full-screen mode. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| -------- | ---------------------------- | -- | --------- |
| names    | Array<'status'\|'navigation'> | Yes | Whether to display the status bar and navigation bar when the window is in full-screen mode.<br>For example, to display the status bar and navigation bar, set this parameter to **['status', 'navigation']**. By default, they are not displayed. |
| callback | AsyncCallback&lt;void&gt; | Yes | Callback used to return the result. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
// In this example, the status bar and navigation bar are not displayed.
import { BusinessError } from '@ohos.base';

let names: Array<'status' | 'navigation'> = [];
try {
  windowClass.setWindowSystemBarEnable(names, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the system bar to be invisible. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the system bar to be invisible.');
  });
} catch (exception) {
  console.error('Failed to set the system bar to be invisible. Cause:' + JSON.stringify(exception));
}
```

### setWindowSystemBarEnable<sup>9+</sup>

setWindowSystemBarEnable(names: Array<'status' | 'navigation'>): Promise&lt;void&gt;

Sets whether to display the status bar and navigation bar when the window is in full-screen mode. This API uses a promise to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| ----- | ---------------------------- | -- | --------------------------------- |
| names | Array<'status'\|'navigation'> | Yes | Whether to display the status bar and navigation bar when the window is in full-screen mode.<br>For example, to display the status bar and navigation bar, set this parameter to **['status', 'navigation']**. By default, they are not displayed. |

**Return value**

| Type | Description |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
// In this example, the status bar and navigation bar are not displayed.
import { BusinessError } from '@ohos.base';

let names: Array<'status' | 'navigation'> = [];
try {
  let promise = windowClass.setWindowSystemBarEnable(names);
  promise.then(() => {
    console.info('Succeeded in setting the system bar to be invisible.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the system bar to be invisible. Cause:' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the system bar to be invisible. Cause:' + JSON.stringify(exception));
}
```

### setSpecificSystemBarEnabled<sup>11+</sup>

setSpecificSystemBarEnabled(name: SpecificSystemBar, enable: boolean): Promise&lt;void&gt;

Sets whether to show the navigation bar, status bar, or bottom navigation bar in full-screen mode. This API uses a promise to return the result.

**System capability**: SystemCapability.Window.SessionManager

**Parameters**

| Name | Type | Mandatory | Description |
| ----- | ---------------------------- | -- | --------------------------------- |
| name  | [SpecificSystemBar](#specificsystembar11) | Yes | Type of the system bar to be shown or hidden. |
| enable  | boolean | Yes | Whether to show the status bar, navigation bar, or bottom navigation bar. The value **true** means to show them, and **false** means to hide them.|

**Return value**

| Type | Description |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
// Hide the bottom navigation bar.
import { BusinessError } from '@ohos.base';

try {
  let promise = windowClass.setSpecificSystemBarEnabled('navigationIndicator', false);
  promise.then(() => {
    console.info('Succeeded in setting the system bar to be invisible.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the system bar to be invisible. Cause:' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the system bar to be invisible. Cause:' + JSON.stringify(exception));
}
```

### setWindowSystemBarProperties<sup>9+</sup>

setWindowSystemBarProperties(systemBarProperties: SystemBarProperties, callback: AsyncCallback&lt;void&gt;): void

Sets the properties of the status bar and navigation bar when the main window is in full-screen mode. This API uses an asynchronous callback to return the result. The setting does not take effect for 2-in-1 devices.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name             | Type                                       | Mandatory | Description                  |
| ------------------- | ------------------------------------------- | ---- | ---------------------- |
| systemBarProperties | [SystemBarProperties](#systembarproperties) | Yes  | Properties of the status bar and navigation bar. |
| callback            | AsyncCallback&lt;void&gt;                   | Yes  | Callback used to return the result.            |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let SystemBarProperties: window.SystemBarProperties = {
  statusBarColor: '#ff00ff',
  navigationBarColor: '#00ff00',
  // The following properties are supported since API version 8.
  statusBarContentColor: '#ffffff',
  navigationBarContentColor: '#00ffff'
};
try {
  windowClass.setWindowSystemBarProperties(SystemBarProperties, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the system bar properties. Cause: ' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the system bar properties.');
  });
} catch (exception) {
  console.error('Failed to set the system bar properties. Cause: ' + JSON.stringify(exception));
}
```

### setWindowSystemBarProperties<sup>9+</sup>

setWindowSystemBarProperties(systemBarProperties: SystemBarProperties): Promise&lt;void&gt;

Sets the properties of the status bar and navigation bar when the main window is in full-screen mode. This API uses a promise to return the result. The setting does not take effect for 2-in-1 devices.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name             | Type                                       | Mandatory | Description                  |
| ------------------- | ------------------------------------------- | ---- | ---------------------- |
| systemBarProperties | [SystemBarProperties](#systembarproperties) | Yes  | Properties of the status bar and navigation bar. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let SystemBarProperties: window.SystemBarProperties = {
  statusBarColor: '#ff00ff',
  navigationBarColor: '#00ff00',
  // The following properties are supported since API version 8.
  statusBarContentColor: '#ffffff',
  navigationBarContentColor: '#00ffff'
};
try {
  let promise = windowClass.setWindowSystemBarProperties(SystemBarProperties);
  promise.then(() => {
    console.info('Succeeded in setting the system bar properties.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the system bar properties. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the system bar properties. Cause: ' + JSON.stringify(exception));
}
```

### setPreferredOrientation<sup>9+</sup>

setPreferredOrientation(orientation: Orientation, callback: AsyncCallback&lt;void&gt;): void

Sets the preferred orientation for this window. This API uses an asynchronous callback to return the result. It takes effect only on the device that supports rotation with the sensor.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name             | Type                                       | Mandatory | Description                  |
| ------------------- | ------------------------------------------- | ---- | ---------------------- |
| orientation         | [Orientation](#orientation9)                | Yes  | Orientation to set.        |
| callback            | AsyncCallback&lt;void&gt;                   | Yes  | Callback used to return the result.            |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let orientation = window.Orientation.AUTO_ROTATION;
try {
  windowClass.setPreferredOrientation(orientation, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set window orientation. Cause: ' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting window orientation.');
  });
} catch (exception) {
  console.error('Failed to set window orientation. Cause: ' + JSON.stringify(exception));
}
```

### setPreferredOrientation<sup>9+</sup>

setPreferredOrientation(orientation: Orientation): Promise&lt;void&gt;

Sets the preferred orientation for this window. This API uses a promise to return the result. It takes effect only on the device that supports rotation with the sensor.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name             | Type                                       | Mandatory | Description                  |
| ------------------- | ------------------------------------------- | ---- | ---------------------- |
| orientation         | [Orientation](#orientation9)                | Yes  | Orientation to set.      |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let orientation = window.Orientation.AUTO_ROTATION;
try {
  let promise = windowClass.setPreferredOrientation(orientation);
  promise.then(() => {
    console.info('Succeeded in setting the window orientation.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the window orientation. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set window orientation. Cause: ' + JSON.stringify(exception));
}
```

### getUIContext<sup>10+</sup>

getUIContext(): UIContext

Obtain a **UIContext** instance.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Return value**

| Type      | Description                  |
| ---------- | ---------------------- |
| [UIContext](js-apis-arkui-UIContext.md#uicontext) | **UIContext** instance obtained. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';
import { UIContext } from '@ohos.arkui.UIContext';

export default class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    // Load content for the main window.
    windowStage.loadContent("pages/page2", (err: BusinessError) => {
      let errCode: number = err.code;
      if (errCode) {
        console.error('Failed to load the content. Cause:' + JSON.stringify(err));
        return;
      }
      console.info('Succeeded in loading the content.');
      // Obtain the main window.
      let windowClass: window.Window | undefined = undefined;
      windowStage.getMainWindow((err: BusinessError, data) => {
        let errCode: number = err.code;
        if (errCode) {
          console.error('Failed to obtain the main window. Cause: ' + JSON.stringify(err));
          return;
        }
        windowClass = data;
        console.info('Succeeded in obtaining the main window. Data: ' + JSON.stringify(data));
        // Obtain a UIContext instance.
        let uiContext: UIContext | null = null;
        uiContext = windowClass.getUIContext();
      })
    });
  }
};
```

### setUIContent<sup>9+</sup>

setUIContent(path: string, callback: AsyncCallback&lt;void&gt;): void

Loads the content of a page, with its path in the current project specified, to this window. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| -------- | ------------------------- | -- | -------------------- |
| path     | string                    | Yes | Path of the page from which the content will be loaded. In the stage model, the path is configured in the **main_pages.json** file of the project. In the FA model, the path is configured in the **config.json** file of the project. |
| callback | AsyncCallback&lt;void&gt; | Yes | Callback used to return the result.         |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

try {
  windowClass.setUIContent('pages/page2/page3', (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in loading the content.');
  });
} catch (exception) {
  console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
}
```

### setUIContent<sup>9+</sup>

setUIContent(path: string): Promise&lt;void&gt;

Loads the content of a page, with its path in the current project specified, to this window. This API uses a promise to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| ---- | ------ | -- | ------------------ |
| path | string | Yes | Path of the page from which the content will be loaded. In the stage model, the path is configured in the **main_pages.json** file of the project. In the FA model, the path is configured in the **config.json** file of the project. |

**Return value**

| Type | Description |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

try {
  let promise = windowClass.setUIContent('pages/page2/page3');
  promise.then(() => {
    console.info('Succeeded in loading the content.');
  }).catch((err: BusinessError) => {
    console.error('Failed to load the content. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to load the content. Cause: ' + JSON.stringify(exception));
}
```

### loadContent<sup>9+</sup>

loadContent(path: string, storage: LocalStorage, callback: AsyncCallback&lt;void&gt;): void

Loads the content of a page, with its path in the current project specified, to this window, and transfers the state attribute to the page through a local storage. This API uses an asynchronous callback to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                           | Mandatory | Description                                                        |
| -------- | ----------------------------------------------- | ---- | ------------------------------------------------------------ |
| path     | string                                          | Yes  | Path of the page from which the content will be loaded. The path is configured in the **main_pages.json** file of the project. |
| storage  | [LocalStorage](../../quick-start/arkts-localstorage.md) | Yes  | Page-level UI state storage unit, which is used to transfer the state attribute for the page. |
| callback | AsyncCallback&lt;void&gt;                       | Yes  | Callback used to return the result.                                                  |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    let storage: LocalStorage = new LocalStorage();
    storage.setOrCreate('storageSimpleProp', 121);
    try {
      if (!windowClass) {
        console.info('Failed to load the content. Cause: windowClass is null');
      }
      else {
        (windowClass as window.Window).loadContent('pages/page2', storage, (err: BusinessError) => {
          const errCode: number = err.code;
          if (errCode) {
            console.error('Failed to load the content. Cause:' + JSON.stringify(err));
            return;
          }
          console.info('Succeeded in loading the content.');
        });
      }
    } catch (exception) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
    }
  }
};
```

### loadContent<sup>9+</sup>

loadContent(path: string, storage: LocalStorage): Promise&lt;void&gt;

Loads the content of a page, with its path in the current project specified, to this window, and transfers the state attribute to the page through a local storage. This API uses a promise to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type                                           | Mandatory | Description                                                        |
| ------- | ----------------------------------------------- | ---- | ------------------------------------------------------------ |
| path    | string                                          | Yes  | Path of the page from which the content will be loaded. The path is configured in the **main_pages.json** file of the project. |
| storage | [LocalStorage](../../quick-start/arkts-localstorage.md) | Yes  | Page-level UI state storage unit, which is used to transfer the state attribute for the page. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    let storage: LocalStorage = new LocalStorage();
    storage.setOrCreate('storageSimpleProp', 121);
    try {
      if (!windowClass) {
        console.info('Failed to load the content. Cause: windowClass is null');
      }
      else {
        let promise = (windowClass as window.Window).loadContent('pages/page2', storage);
        promise.then(() => {
          console.info('Succeeded in loading the content.');
        }).catch((err: BusinessError) => {
          console.error('Failed to load the content. Cause:' + JSON.stringify(err));
        });
      }
    } catch (exception) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
    }
  }
};
```

### loadContentByName<sup>11+</sup>

loadContentByName(name: string, storage: LocalStorage, callback: AsyncCallback&lt;void&gt;): void

Loads the content of a [named route](../../ui/arkts-routing.md#named-route) page to this window, and transfers the state attribute to the page through a local storage. This API uses an asynchronous callback to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                                   | Mandatory | Description                                                        |
| -------- | ------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| name     | string                                                  | Yes  | Name of the named route page.                                            |
| storage  | [LocalStorage](../../quick-start/arkts-localstorage.md) | Yes  | Page-level UI state storage unit, which is used to transfer the state attribute for the page. |
| callback | AsyncCallback&lt;void&gt;                               | Yes  | Callback used to return the result.                                                  |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message                                     |
| -------- | --------------------------------------------- |
| 1300002  | This window state is abnormal.                |
| 1300003  | This window manager service works abnormally. |

**Example**

```ts
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';
import * as Index from '../pages/Index'; // Import the named route page.

console.info('onWindowStageCreate');
let storage: LocalStorage = new LocalStorage();
storage.setOrCreate('storageSimpleProp', 121);
try {
  (windowClass as window.Window).loadContentByName(Index.entryName, storage, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error(`Failed to load the content. Cause code: ${err.code}, message: ${err.message}`);
      return;
    }
    console.info('Succeeded in loading the content.');
  });
} catch (exception) {
  console.error(`Failed to load the content. Cause code: ${exception.code}, message: ${exception.message}`);
}
```
```ts
// ets/pages/Index.ets
export const entryName : string = 'Index';
@Entry({routeName: entryName, storage : LocalStorage.getShared()})
@Component
export struct Index {
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

### loadContentByName<sup>11+</sup>

loadContentByName(name: string, callback: AsyncCallback&lt;void&gt;): void

Loads the content of a [named route](../../ui/arkts-routing.md#named-route) page to this window. This API uses an asynchronous callback to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                     | Mandatory | Description            |
| -------- | ------------------------- | ---- | ---------------- |
| name     | string                    | Yes  | Name of the named route page. |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.      |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message                                     |
| -------- | --------------------------------------------- |
| 1300002  | This window state is abnormal.                |
| 1300003  | This window manager service works abnormally. |

**Example**

```ts
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';
import * as Index from '../pages/Index'; // Import the named route page.

try {  
  (windowClass as window.Window).loadContentByName(Index.entryName, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error(`Failed to load the content. Cause code: ${err.code}, message: ${err.message}`);
      return;
    }
    console.info('Succeeded in loading the content.');
  });
} catch (exception) {
  console.error(`Failed to load the content. Cause code: ${exception.code}, message: ${exception.message}`);
}
```
```ts
// ets/pages/Index.ets
export const entryName : string = 'Index';
@Entry({routeName: entryName})
@Component
export struct Index {
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

### loadContentByName<sup>11+</sup>

loadContentByName(name: string, storage?: LocalStorage): Promise&lt;void&gt;

Loads the content of a [named route](../../ui/arkts-routing.md#named-route) page to this window, and transfers the state attribute to the page through a local storage. This API uses a promise to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type                                                   | Mandatory | Description                                                        |
| ------- | ------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| name    | string                                                  | Yes  | Name of the named route page.                                            |
| storage | [LocalStorage](../../quick-start/arkts-localstorage.md) | No  | Page-level UI state storage unit, which is used to transfer the state attribute for the page. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message                                     |
| -------- | --------------------------------------------- |
| 1300002  | This window state is abnormal.                |
| 1300003  | This window manager service works abnormally. |

**Example**

```ts
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';
import * as Index from '../pages/Index'; // Import the named route page.

let storage: LocalStorage = new LocalStorage();
storage.setOrCreate('storageSimpleProp', 121);
try {
  let promise = (windowClass as window.Window).loadContentByName(Index.entryName, storage);
  promise.then(() => {
    console.info('Succeeded in loading the content.');
  }).catch((err: BusinessError) => {
    console.error(`Failed to load the content. Cause code: ${err.code}, message: ${err.message}`);
  });
} catch (exception) {
  console.error(`Failed to load the content. Cause code: ${exception.code}, message: ${exception.message}`);
}
```
```ts
// ets/pages/Index.ets
export const entryName : string = 'Index';
@Entry({routeName: entryName, storage : LocalStorage.getShared()})
@Component
export struct Index {
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

### isWindowShowing<sup>9+</sup>

isWindowShowing(): boolean

Checks whether this window is displayed.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Return value**

| Type | Description |
| ------- | ------------------------------------------------------------------ |
| boolean | Whether the window is displayed. The value **true** means that the window is displayed, and **false** means the opposite. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**Example**

```ts
try {
  let data = windowClass.isWindowShowing();
  console.info('Succeeded in checking whether the window is showing. Data: ' + JSON.stringify(data));
} catch (exception) {
  console.error('Failed to check whether the window is showing. Cause: ' + JSON.stringify(exception));
}
```

### on('windowSizeChange')<sup>7+</sup>

on(type:  'windowSizeChange', callback: Callback&lt;Size&gt;): void

Subscribes to the window size change event.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                          | Mandatory | Description                                                    |
| -------- | ------------------------------ | ---- | -------------------------------------------------------- |
| type     | string                         | Yes  | Event type. The value is fixed at **'windowSizeChange'**, indicating the window size change event. |
| callback | Callback&lt;[Size](#size7)&gt; | Yes  | Callback used to return the window size.                          |

**Example**

```ts
try {
  windowClass.on('windowSizeChange', (data) => {
    console.info('Succeeded in enabling the listener for window size changes. Data: ' + JSON.stringify(data));
  });
} catch (exception) {
  console.error('Failed to enable the listener for window size changes. Cause: ' + JSON.stringify(exception));
}
```

### off('windowSizeChange')<sup>7+</sup>

off(type: 'windowSizeChange', callback?: Callback&lt;Size&gt;): void

Unsubscribes from the window size change event.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                         | Mandatory | Description                                                    |
| -------- | ----------------------------- | ---- | -------------------------------------------------------- |
| type     | string                        | Yes  | Event type. The value is fixed at **'windowSizeChange'**, indicating the window size change event. |
| callback | Callback&lt;[Size](#size7)&gt; | No  | Callback used to return the window size. If a value is passed in, the corresponding subscription is canceled. If no value is passed in, all subscriptions to the specified event are canceled.                          |

**Example**

```ts
try {
  windowClass.off('windowSizeChange');
} catch (exception) {
  console.error('Failed to disable the listener for window size changes. Cause: ' + JSON.stringify(exception));
}
```

### on('avoidAreaChange')<sup>9+</sup>

on(type: 'avoidAreaChange', callback: Callback&lt;{ type: AvoidAreaType, area: AvoidArea}&gt;): void

Subscribes to the event indicating changes to the area where the window cannot be displayed.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                                              | Mandatory | Description                                  |
| -------- |------------------------------------------------------------------| ---- |--------------------------------------|
| type     | string                                                           | Yes  | Event type. The value is fixed at **'avoidAreaChange'**, indicating the event of changes to the area where the window cannot be displayed. |
| callback | Callback&lt;{ type: [AvoidAreaType](#avoidareatype7), area: [AvoidArea](#avoidarea7) }&gt; | Yes  | Callback used to return the area and area type.|

**Example**

```ts
try {
  windowClass.on('avoidAreaChange', (data) => {
    console.info('Succeeded in enabling the listener for system avoid area changes. type:' +
    JSON.stringify(data.type) + ', area: ' + JSON.stringify(data.area));
  });
} catch (exception) {
  console.error('Failed to enable the listener for system avoid area changes. Cause: ' + JSON.stringify(exception));
}
```

### off('avoidAreaChange')<sup>9+</sup>

off(type: 'avoidAreaChange', callback?: Callback&lt;{ type: AvoidAreaType, area: AvoidArea }&gt;): void

Unsubscribes from the event indicating changes to the area where the window cannot be displayed.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                                                         | Mandatory | Description                                |
| -------- |-----------------------------------------------------------------------------|-----|------------------------------------|
| type     | string                                                                      | Yes  | Event type. The value is fixed at **'avoidAreaChange'**, indicating the event of changes to the area where the window cannot be displayed. |
| callback | Callback&lt;{ type: [AvoidAreaType](#avoidareatype7), area: [AvoidArea](#avoidarea7) }&gt; | No  | Callback used to return the area and area type. If a value is passed in, the corresponding subscription is canceled. If no value is passed in, all subscriptions to the specified event are canceled.|

**Example**

```ts
try {
  windowClass.off('avoidAreaChange');
} catch (exception) {
  console.error('Failed to disable the listener for system avoid area changes. Cause: ' + JSON.stringify(exception));
}
```

### on('keyboardHeightChange')<sup>7+</sup>

on(type: 'keyboardHeightChange', callback: Callback&lt;number&gt;): void

Subscribes to the event indicating soft keyboard height changes in fixed state. The system notifies the keyboard height change when the soft keyboard overlaps with the window. Since API version 10, the input method panel can be set to the fixed or floating state. For details, see [Input Method Service](../apis-ime-kit/js-apis-inputmethodengine.md#changeflag10).

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type               | Mandatory | Description                                       |
| -------- | ------------------- | ---- |-------------------------------------------|
| type     | string              | Yes  | Event type. The value is fixed at **'keyboardHeightChange'**, indicating the keyboard height change event. |
| callback | Callback&lt;number&gt; | Yes  | Callback used to return the current keyboard height, which is an integer, in px.    |

**Example**

```ts
try {
  windowClass.on('keyboardHeightChange', (data) => {
    console.info('Succeeded in enabling the listener for keyboard height changes. Data: ' + JSON.stringify(data));
  });
} catch (exception) {
  console.error('Failed to enable the listener for keyboard height changes. Cause: ' + JSON.stringify(exception));
}
```

### off('keyboardHeightChange')<sup>7+</sup>

off(type: 'keyboardHeightChange', callback?: Callback&lt;number&gt;): void

Unsubscribes from the event indicating soft keyboard height changes in fixed state. Since API version 10, the input method panel can be set to the fixed or floating state. For details, see [Input Method Service](../apis-ime-kit/js-apis-inputmethodengine.md#changeflag10).

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                  | Mandatory | Description                                                        |
| -------- | ---------------------- | ---- | ------------------------------------------------------------ |
| type     | string                 | Yes  | Event type. The value is fixed at **'keyboardHeightChange'**, indicating the keyboard height change event. |
| callback | Callback&lt;number&gt; | No  | Callback used to return the current keyboard height, which is an integer, in px. If a value is passed in, the corresponding subscription is canceled. If no value is passed in, all subscriptions to the specified event are canceled.                              |

**Example**

```ts
try {
  windowClass.off('keyboardHeightChange');
} catch (exception) {
  console.error('Failed to disable the listener for keyboard height changes. Cause: ' + JSON.stringify(exception));
}
```

### on('touchOutside')<sup>11+</sup>

on(type: 'touchOutside', callback: Callback&lt;void&gt;): void

Subscribes to the touch event outside this window.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type               | Mandatory | Description                                                        |
| -------- | ------------------- | ---- | ------------------------------------------------------------ |
| type     | string              | Yes  | Event type. The value is fixed at **'touchOutside'**, indicating the touch event outside this window. |
| callback | Callback&lt;void&gt; | Yes  | Callback used to return the touch event outside this window.                              |

**Example**

```ts
try {
  windowClass.on('touchOutside', () => {
    console.info('touch outside');
  });
} catch (exception) {
  console.error('Failed to register callback. Cause: ' + JSON.stringify(exception));
}
```

### off('touchOutside')<sup>11+</sup>

off(type: 'touchOutside', callback?: Callback&lt;void&gt;): void

Unsubscribes from the touch event outside this window.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                  | Mandatory | Description                                  |
| -------- |----------------------| ---- |--------------------------------------|
| type     | string               | Yes  | Event type. The value is fixed at **'touchOutside'**, indicating the touch event outside this window. |
| callback | Callback&lt;void&gt; | No  | Callback used to return the touch event outside this window. If a value is passed in, the corresponding subscription is canceled. If no value is passed in, all subscriptions to the specified event are canceled.           |

**Example**

```ts
try {
  windowClass.off('touchOutside');
} catch (exception) {
  console.error('Failed to unregister callback. Cause: ' + JSON.stringify(exception));
}
```

### on('screenshot')<sup>9+</sup>

on(type: 'screenshot', callback: Callback&lt;void&gt;): void

Subscribes to the screenshot event.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type               | Mandatory | Description                                                        |
| -------- | ------------------- | ---- | ------------------------------------------------------------ |
| type     | string              | Yes  | Event type. The value is fixed at **'screenshot'**, indicating the screenshot event, which can be initiated from the Control Panel, by running hdc commands, or by calling the screenshot interfaces. |
| callback | Callback&lt;void&gt; | Yes  | Callback invoked when a screenshot event occurs.                              |

**Example**

```ts
try {
  windowClass.on('screenshot', () => {
    console.info('screenshot happened');
  });
} catch (exception) {
  console.error('Failed to register callback. Cause: ' + JSON.stringify(exception));
}
```

### off('screenshot')<sup>9+</sup>

off(type: 'screenshot', callback?: Callback&lt;void&gt;): void

Unsubscribes from the screenshot event.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                  | Mandatory | Description                                                        |
| -------- | ---------------------- | ---- | ------------------------------------------------------------ |
| type     | string                 | Yes  | Event type. The value is fixed at **'screenshot'**, indicating the screenshot event. |
| callback | Callback&lt;void&gt; | No  | Callback invoked when a screenshot event occurs. If a value is passed in, the corresponding subscription is canceled. If no value is passed in, all subscriptions to the specified event are canceled. |

**Example**

```ts
let callback = () => {
  console.info('screenshot happened');
};
try {
  windowClass.on('screenshot', callback);
} catch (exception) {
  console.error('Failed to register callback. Cause: ' + JSON.stringify(exception));
}
try {
  windowClass.off('screenshot', callback);
  // Unregister all the callbacks that have been registered through on().
  windowClass.off('screenshot');
} catch (exception) {
  console.error('Failed to unregister callback. Cause: ' + JSON.stringify(exception));
}
```

### on('dialogTargetTouch')<sup>10+</sup>

on(type: 'dialogTargetTouch', callback: Callback&lt;void&gt;): void

Subscribes to click or touch events in a window covered by a modal window.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                | Mandatory | Description                                                         |
| -------- | ------------------- | ---- | ------------------------------------------------------------ |
| type     | string              | Yes  | Event type. The value is fixed at **'dialogTargetTouch'**, indicating the click or touch event in a window covered by a modal window. |
| callback | Callback&lt;void&gt;| Yes  | Callback invoked when a click or touch event occurs in the window covered by the modal window. |

**Example**

```ts
try {
  windowClass.on('dialogTargetTouch', () => {
    console.info('touch dialog target');
  });
} catch (exception) {
  console.error('Failed to register callback. Cause: ' + JSON.stringify(exception));
}
```

### off('dialogTargetTouch')<sup>10+</sup>

off(type: 'dialogTargetTouch', callback?: Callback&lt;void&gt;): void

Unsubscribes from the touch event of the target window in the modal window mode.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                   | Mandatory | Description                                                         |
| -------- | ---------------------- | ---- | ------------------------------------------------------------ |
| type     | string                 | Yes  | Event type. The value is fixed at **'dialogTargetTouch'**, indicating the touch event of the target window in the modal window mode. |
| callback | Callback&lt;void&gt;      | No  | Callback invoked when the touch event occurs in the target window of the modal window mode. If a value is passed in, the corresponding subscription is canceled. If no value is passed in, all subscriptions to the specified event are canceled. |

**Example**

```ts
try {
  windowClass.off('dialogTargetTouch');
} catch (exception) {
  console.error('Failed to unregister callback. Cause: ' + JSON.stringify(exception));
}
```

### on('windowEvent')<sup>10+</sup>

on(type: 'windowEvent', callback: Callback&lt;WindowEventType&gt;): void

Subscribes to the window lifecycle change event.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                                      | Mandatory | Description                                                        |
| -------- | ---------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                                                     | Yes  | Event type. The value is fixed at **'windowEvent'**, indicating the window lifecycle change event. |
| callback | Callback&lt;[WindowEventType](#windoweventtype10)&gt; | Yes  | Callback used to return the window lifecycle state.                |

**Example**

```ts
try {
  windowClass.on('windowEvent', (data) => {
    console.info('Window event happened. Event:' + JSON.stringify(data));
  });
} catch (exception) {
  console.error('Failed to register callback. Cause: ' + JSON.stringify(exception));
}
```

### off('windowEvent')<sup>10+</sup>

off(type: 'windowEvent', callback?: Callback&lt;WindowEventType &gt;): void

Unsubscribes from the window lifecycle change event.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                                      | Mandatory | Description                                                        |
| -------- | ---------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                                                     | Yes  | Event type. The value is fixed at **'windowEvent'**, indicating the window lifecycle change event. |
| callback | Callback&lt;[WindowEventType](#windoweventtype10)&gt; | No  | Callback used to return the window lifecycle state. If a value is passed in, the corresponding subscription is canceled. If no value is passed in, all subscriptions to the specified event are canceled.                |

**Example**

```ts
try {
  windowClass.off('windowEvent');
} catch (exception) {
  console.error('Failed to unregister callback. Cause: ' + JSON.stringify(exception));
}
```

### on('windowVisibilityChange')<sup>11+</sup>

on(type: 'windowVisibilityChange', callback: Callback&lt;boolean&gt;): void

Subscribes to the visibility status change event of this window.

**System capability**: SystemCapability.Window.SessionManager

**Parameters**

| Name  | Type                      | Mandatory | Description                                                        |
| -------- | --------------------------| ---- | ------------------------------------------------------------ |
| type     | string                    | Yes  | Event type. The value is fixed at **'windowVisibilityChange'**, indicating the visibility status change event. |
| callback | Callback&lt;boolean&gt;   | Yes  | Callback used to return the visibility status of the window, which is a Boolean value. The value **true** means that the window is visible, and **false** means the opposite.                              |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal.                |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
try {
  windowClass.on('windowVisibilityChange', (boolean) => {
    console.info('Window visibility changed, isVisible=' + boolean);
  });
} catch (exception) {
  console.error('Failed to register callback. Cause: ' + JSON.stringify(exception));
}
```

### off('windowVisibilityChange')<sup>11+</sup>

off(type: 'windowVisibilityChange', callback?: Callback&lt;boolean&gt;): void

Unsubscribes from the visibility status change event of this window.

**System capability**: SystemCapability.Window.SessionManager

**Parameters**

| Name  | Type                       | Mandatory | Description                                  |
| -------- |----------------------------| ---- |--------------------------------------|
| type     | string                     | Yes  | Event type. The value is fixed at **'windowVisibilityChange'**, indicating the visibility status change event. |
| callback | Callback&lt;boolean&gt;    | No  | Callback used to return the visibility status of the window. If a value is passed in, the corresponding subscription is canceled. If no value is passed in, all subscriptions to the specified event are canceled.           |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal.                |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
try {
  windowClass.off('windowVisibilityChange');
} catch (exception) {
  console.error('Failed to unregister callback. Cause: ' + JSON.stringify(exception));
}
```

### on('windowStatusChange')<sup>11+</sup>

on(type:  'windowStatusChange', callback: Callback&lt;WindowStatusType&gt;): void

Subscribes to the window status change event.

**System capability**: SystemCapability.Window.SessionManager

**Parameters**

| Name  | Type                          | Mandatory | Description                                                    |
| -------- | ------------------------------ | ---- | -------------------------------------------------------- |
| type     | string                         | Yes  | Event type. The value is fixed at **'windowStatusChange'**, indicating the window status change event. |
| callback | Callback&lt;[WindowStatusType](#windowstatustype11)&gt; | Yes  | Callback used to return the window status.                          |

**Example**

```ts
try {
  windowClass.on('windowStatusChange', (WindowStatusType) => {
    console.info('Succeeded in enabling the listener for window status changes. Data: ' + JSON.stringify(WindowStatusType));
  });
} catch (exception) {
  console.error('Failed to enable the listener for window status changes. Cause: ' + JSON.stringify(exception));
}
```

### off('windowStatusChange')<sup>11+</sup>

off(type: 'windowStatusChange', callback?: Callback&lt;WindowStatusType&gt;): void

Unsubscribes from the window status change event.

**System capability**: SystemCapability.Window.SessionManager

**Parameters**

| Name  | Type                         | Mandatory | Description                                                    |
| -------- | ----------------------------- | ---- | -------------------------------------------------------- |
| type     | string                        | Yes  | Event type. The value is fixed at **'windowStatusChange'**, indicating the window status change event. |
| callback | Callback&lt;[WindowStatusType](#windowstatustype11)&gt; | No  | Callback used to return the window status. If a value is passed in, the corresponding subscription is canceled. If no value is passed in, all subscriptions to the specified event are canceled.                          |

**Example**

```ts
try {
  windowClass.off('windowStatusChange');
} catch (exception) {
  console.error('Failed to disable the listener for window status changes. Cause: ' + JSON.stringify(exception));
}
```

### on('windowTitleButtonRectChange')<sup>11+</sup>

on(type: 'windowTitleButtonRectChange', callback: Callback&lt;TitleButtonRect&gt;): void

Subscribes to the change event of the rectangle that holds the minimize, maximize, and close buttons on the title bar.

**System capability**: SystemCapability.Window.SessionManager

**Parameters**

| Name  | Type                                                 | Mandatory | Description                                                        |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                                                | Yes  | Event type. The value is fixed at **'windowTitleButtonRectChange'**, indicating that the change event of the rectangle that holds the minimize, maximize, and close buttons. |
| callback | Callback&lt;[TitleButtonRect](#titlebuttonrect11)&gt; | Yes  | Callback used to return the new rectangle. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message                      |
| -------- | ------------------------------ |
| 1300002  | This window state is abnormal. |

**Example**

```ts
try {
  windowClass.on('windowTitleButtonRectChange', (titleButtonRect) => {
    console.info('Succeeded in enabling the listener for window title buttons area changes. Data: ' + JSON.stringify(titleButtonRect));
  });
} catch (exception) {
  console.error('Failed to enable the listener for window title buttons area changes. Cause: ' + JSON.stringify(exception));
}
```

### off('windowTitleButtonRectChange')<sup>11+</sup>

off(type: 'windowTitleButtonRectChange', callback?: Callback&lt;TitleButtonRect&gt;): void

Unsubscribes from the change event of the rectangle that holds the minimize, maximize, and close buttons on the title bar.

**System capability**: SystemCapability.Window.SessionManager

**Parameters**

| Name  | Type                                                 | Mandatory | Description                                                        |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                                                | Yes  | Event type. The value is fixed at **'windowTitleButtonRectChange'**, indicating that the change event of the rectangle that holds the minimize, maximize, and close buttons. |
| callback | Callback&lt;[TitleButtonRect](#titlebuttonrect11)&gt; | No  | Callback used to return the new rectangle. If a value is passed in, the corresponding subscription is canceled. If no value is passed in, all subscriptions to the specified event are canceled. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message                      |
| -------- | ------------------------------ |
| 1300002  | This window state is abnormal. |

**Example**

```ts
try {
  windowClass.off('windowTitleButtonRectChange');
} catch (exception) {
  console.error('Failed to disable the listener for window title buttons area changes. Cause: ' + JSON.stringify(exception));
}
```

### isWindowSupportWideGamut<sup>9+</sup>

isWindowSupportWideGamut(callback: AsyncCallback&lt;boolean&gt;): void

Checks whether this window supports the wide-gamut color space. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| -------- | ---------------------------- | -- | -------------------------------------------------------------------------------- |
| callback | AsyncCallback&lt;boolean&gt; | Yes | Callback used to return the result. The value **true** means that the wide-gamut color space is supported, and **false** means the opposite. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

windowClass.isWindowSupportWideGamut((err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to check whether the window support WideGamut. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in checking whether the window support WideGamut Data: ' + JSON.stringify(data));
});
```

### isWindowSupportWideGamut<sup>9+</sup>

isWindowSupportWideGamut(): Promise&lt;boolean&gt;

Checks whether this window supports the wide-gamut color space. This API uses a promise to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Return value**

| Type | Description |
| ---------------------- | ------------------------------------------------------------------------------------ |
| Promise&lt;boolean&gt; | Promise used to return the result. The value **true** means that the wide-gamut color space is supported, and **false** means the opposite. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.isWindowSupportWideGamut();
promise.then((data) => {
  console.info('Succeeded in checking whether the window support WideGamut. Data: ' + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error('Failed to check whether the window support WideGamut. Cause: ' + JSON.stringify(err));
});
```

### setWindowColorSpace<sup>9+</sup>

setWindowColorSpace(colorSpace:ColorSpace, callback: AsyncCallback&lt;void&gt;): void

Sets a color space for this window. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| ---------- | ------------------------- | -- | ----------- |
| colorSpace | [ColorSpace](#colorspace8) | Yes | Color space to set. |
| callback   | AsyncCallback&lt;void&gt; | Yes | Callback used to return the result.  |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

try {
  windowClass.setWindowColorSpace(window.ColorSpace.WIDE_GAMUT, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set window colorspace. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting window colorspace.');
  });
} catch (exception) {
  console.error('Failed to set window colorspace. Cause:' + JSON.stringify(exception));
}
```

### setWindowColorSpace<sup>9+</sup>

setWindowColorSpace(colorSpace:ColorSpace): Promise&lt;void&gt;

Sets a color space for this window. This API uses a promise to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| ---------- | ------------------------- | -- | ------------- |
| colorSpace | [ColorSpace](#colorspace8) | Yes | Color space to set. |

**Return value**

| Type | Description |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

try {
  let promise = windowClass.setWindowColorSpace(window.ColorSpace.WIDE_GAMUT);
  promise.then(() => {
    console.info('Succeeded in setting window colorspace.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set window colorspace. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set window colorspace. Cause:' + JSON.stringify(exception));
}
```

### getWindowColorSpace<sup>9+</sup>

getWindowColorSpace(): ColorSpace

Obtains the color space of this window.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Return value**

| Type | Description |
| ------------------------- | ------------- |
| [ColorSpace](#colorspace8) | Color space obtained. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**Example**

```ts
let colorSpace = windowClass.getWindowColorSpace();
```

### setWindowBackgroundColor<sup>9+</sup>

setWindowBackgroundColor(color: string): void

Sets the background color for this window. In the stage model, this API must be used after the call of [loadContent](#loadcontent9) or [setUIContent()](#setuicontent9) takes effect.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| ----- | ------ | -- | ----------------------------------------------------------------------- |
| color | string | Yes | Background color to set. The value is a hexadecimal RGB or ARGB color code and is case insensitive, for example, **'#00FF00'** or **'#FF00FF00'**. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

private SetUIContent(windowClass: window.Window) {
  windowClass.setUIContent("pages/ButtonWindow",(err: BusinessError) => {
    if (err.code) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in loading the content.');
    let color: string = '#00ff33';
    try {
      windowClass.setWindowBackgroundColor(color);
    } catch (exception) {
      console.error('Failed to set the background color. Cause: ' + JSON.stringify(exception));
    };
  });
}
```

### setWindowBrightness<sup>9+</sup>

setWindowBrightness(brightness: number, callback: AsyncCallback&lt;void&gt;): void

Sets the screen brightness for this window. This API uses an asynchronous callback to return the result.

When the screen brightness setting for the window takes effect, Control Panel cannot adjust the system screen brightness. It can do so only after the window screen brightness is restored to the default value.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description                                       |
| ---------- | ------------------------- | -- |-------------------------------------------|
| brightness | number                    | Yes | Brightness to set. The value is a floating point number in the range [0.0, 1.0] or **-1.0**. The value **1.0** means the brightest, and **-1.0** means the default brightness. |
| callback   | AsyncCallback&lt;void&gt; | Yes | Callback used to return the result.                                    |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let brightness: number = 1;
try {
  windowClass.setWindowBrightness(brightness, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the brightness. Cause: ' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the brightness.');
  });
} catch (exception) {
  console.error('Failed to set the brightness. Cause: ' + JSON.stringify(exception));
}
```

### setWindowBrightness<sup>9+</sup>

setWindowBrightness(brightness: number): Promise&lt;void&gt;

Sets the screen brightness for this window. This API uses a promise to return the result.

When the screen brightness setting for the window takes effect, Control Panel cannot adjust the system screen brightness. It can do so only after the window screen brightness is restored to the default value.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description                                    |
| ---------- | ------ | -- |----------------------------------------|
| brightness | number | Yes | Brightness to set. The value is a floating point number in the range [0.0, 1.0] or **-1.0**. The value **1.0** means the brightest, and **-1.0** means the default brightness. |

**Return value**

| Type | Description |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let brightness: number = 1;
try {
  let promise = windowClass.setWindowBrightness(brightness);
  promise.then(() => {
    console.info('Succeeded in setting the brightness.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the brightness. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the brightness. Cause: ' + JSON.stringify(exception));
}
```

### setWindowFocusable<sup>9+</sup>

setWindowFocusable(isFocusable: boolean, callback: AsyncCallback&lt;void&gt;): void

Sets whether this window is focusable, that is, whether the window can gain focus after it is being clicked or using other methods. This API uses an asynchronous callback to return the result.


**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| ----------- | ------------------------- | -- | ------------------------------------------------------- |
| isFocusable | boolean                   | Yes | Whether the window can gain focus. The value **true** means that the window can gain focus, and **false** means the opposite. |
| callback    | AsyncCallback&lt;void&gt; | Yes | Callback used to return the result.                                              |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isFocusable: boolean = true;
try {
  windowClass.setWindowFocusable(isFocusable, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the window to be focusable. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the window to be focusable.');
  });
} catch (exception) {
  console.error('Failed to set the window to be focusable. Cause:' + JSON.stringify(exception));
}
```

### setWindowFocusable<sup>9+</sup>

setWindowFocusable(isFocusable: boolean): Promise&lt;void&gt;

Sets whether this window is focusable, that is, whether the window can gain focus after it is being clicked or using other methods. This API uses a promise to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| ----------- | ------- | -- | -------------------------------------------------------- |
| isFocusable | boolean | Yes | Whether the window can gain focus. The value **true** means that the window can gain focus, and **false** means the opposite. |

**Return value**

| Type | Description |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isFocusable: boolean = true;
try {
  let promise = windowClass.setWindowFocusable(isFocusable);
  promise.then(() => {
    console.info('Succeeded in setting the window to be focusable.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the window to be focusable. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the window to be focusable. Cause:' + JSON.stringify(exception));
}
```

### setWindowKeepScreenOn<sup>9+</sup>

setWindowKeepScreenOn(isKeepScreenOn: boolean, callback: AsyncCallback&lt;void&gt;): void

Sets whether to keep the screen always on. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| -------------- | ------------------------- | -- | ---------------------------------------------------- |
| isKeepScreenOn | boolean                   | Yes | Whether to keep the screen always on. The value **true** means to keep the screen always on, and **false** means the opposite. |
| callback       | AsyncCallback&lt;void&gt; | Yes | Callback used to return the result.                                           |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isKeepScreenOn: boolean = true;
try {
  windowClass.setWindowKeepScreenOn(isKeepScreenOn, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the screen to be always on. Cause: ' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the screen to be always on.');
  });
} catch (exception) {
  console.error('Failed to set the screen to be always on. Cause: ' + JSON.stringify(exception));
}
```

### setWindowKeepScreenOn<sup>9+</sup>

setWindowKeepScreenOn(isKeepScreenOn: boolean): Promise&lt;void&gt;

Sets whether to keep the screen always on. This API uses a promise to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| -------------- | ------- | -- | --------------------------------------------------- |
| isKeepScreenOn | boolean | Yes | Whether to keep the screen always on. The value **true** means to keep the screen always on, and **false** means the opposite. |

**Return value**

| Type | Description |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isKeepScreenOn: boolean = true;
try {
  let promise = windowClass.setWindowKeepScreenOn(isKeepScreenOn);
  promise.then(() => {
    console.info('Succeeded in setting the screen to be always on.');
  }).catch((err: BusinessError) => {
    console.info('Failed to set the screen to be always on. Cause:  ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the screen to be always on. Cause: ' + JSON.stringify(exception));
}
```

### setWindowPrivacyMode<sup>9+</sup>

setWindowPrivacyMode(isPrivacyMode: boolean, callback: AsyncCallback&lt;void&gt;): void

Sets whether this window is in privacy mode. This API uses an asynchronous callback to return the result.

A window in privacy mode cannot be captured or recorded. This API can be used in scenarios where screen capture or recording is disabled.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Required permissions**: ohos.permission.PRIVACY_WINDOW

**Parameters**

| Name | Type | Mandatory | Description |
| ------------- | ------------------------- | -- | ------------------------------------------------------ |
| isPrivacyMode | boolean                   | Yes | Whether the window is in privacy mode. The value **true** means that the window is in privacy mode, and **false** means the opposite. |
| callback      | AsyncCallback&lt;void&gt; | Yes | Callback used to return the result.                                             |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isPrivacyMode: boolean = true;
try {
  windowClass.setWindowPrivacyMode(isPrivacyMode, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the window to privacy mode. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the window to privacy mode.');
  });
} catch (exception) {
  console.error('Failed to set the window to privacy mode. Cause:' + JSON.stringify(exception));
}
```

### setWindowPrivacyMode<sup>9+</sup>

setWindowPrivacyMode(isPrivacyMode: boolean): Promise&lt;void&gt;

Sets whether this window is in privacy mode. This API uses a promise to return the result.

A window in privacy mode cannot be captured or recorded. This API can be used in scenarios where screen capture or recording is disabled.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Required permissions**: ohos.permission.PRIVACY_WINDOW

**Parameters**

| Name | Type | Mandatory | Description |
| ------------- | ------- | -- | ----------------------------------------------------- |
| isPrivacyMode | boolean | Yes | Whether the window is in privacy mode. The value **true** means that the window is in privacy mode, and **false** means the opposite. |

**Return value**

| Type | Description |
| ------------------- | ------------------------ |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isPrivacyMode: boolean = true;
try {
  let promise = windowClass.setWindowPrivacyMode(isPrivacyMode);
  promise.then(() => {
    console.info('Succeeded in setting the window to privacy mode.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the window to privacy mode. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the window to privacy mode. Cause:' + JSON.stringify(exception));
}
```

### setWindowTouchable<sup>9+</sup>

setWindowTouchable(isTouchable: boolean, callback: AsyncCallback&lt;void&gt;): void

Sets whether this window is touchable. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| ----------- | ------------------------- | -- | ----------------------------------------------- |
| isTouchable | boolean                   | Yes | Whether the window is touchable. The value **true** means that the window is touchable, and **false** means the opposite. |
| callback    | AsyncCallback&lt;void&gt; | Yes | Callback used to return the result.                                       |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isTouchable = true;
try {
  windowClass.setWindowTouchable(isTouchable, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the window to be touchable. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the window to be touchable.');
  });
} catch (exception) {
  console.error('Failed to set the window to be touchable. Cause:' + JSON.stringify(exception));
}
```

### setWindowTouchable<sup>9+</sup>

setWindowTouchable(isTouchable: boolean): Promise&lt;void&gt;

Sets whether this window is touchable. This API uses a promise to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description |
| ----------- | ------- | -- | ----------------------------------------------- |
| isTouchable | boolean | Yes | Whether the window is touchable. The value **true** means that the window is touchable, and **false** means the opposite. |

**Return value**

| Type | Description |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300003 | This window manager service works abnormally. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isTouchable: boolean = true;
try {
  let promise = windowClass.setWindowTouchable(isTouchable);
  promise.then(() => {
    console.info('Succeeded in setting the window to be touchable.');
  }).catch((err: BusinessError) => {
    console.error('Failed to set the window to be touchable. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to set the window to be touchable. Cause:' + JSON.stringify(exception));
}
```

### snapshot<sup>9+</sup>

snapshot(callback: AsyncCallback&lt;image.PixelMap&gt;): void

Captures this window. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name     | Type                     | Mandatory | Description                |
| ----------- | ------------------------- | ---- | -------------------- |
| callback    | AsyncCallback&lt;[image.PixelMap](../apis-image-kit/js-apis-image.md#pixelmap7)&gt; | Yes  | Callback used to return the result. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import image from '@ohos.multimedia.image';

windowClass.snapshot((err: BusinessError, pixelMap: image.PixelMap) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to snapshot window. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in snapshotting window. Pixel bytes number: ' + pixelMap.getPixelBytesNumber());
  pixelMap.release(); // Release the memory in time after the PixelMap is used.
});
```

### snapshot<sup>9+</sup>

snapshot(): Promise&lt;image.PixelMap&gt;

Captures this window. This API uses a promise to return the result.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;[image.PixelMap](../apis-image-kit/js-apis-image.md#pixelmap7)&gt; | Promise used to return the window screenshot. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |

**Example**

```ts
import { BusinessError } from '@ohos.base';
import image from '@ohos.multimedia.image';

let promise = windowClass.snapshot();
promise.then((pixelMap: image.PixelMap) => {
  console.info('Succeeded in snapshotting window. Pixel bytes number: ' + pixelMap.getPixelBytesNumber());
  pixelMap.release(); // Release the memory in time after the PixelMap is used.
}).catch((err: BusinessError) => {
  console.error('Failed to snapshot window. Cause:' + JSON.stringify(err));
});
```

### setAspectRatio<sup>10+</sup>

setAspectRatio(ratio: number): Promise&lt;void&gt;

Sets the aspect ratio of the window content layout. This API uses a promise to return the result.

This API is available only for the main window of the application. The aspect ratio will be saved permanently and takes effect even after the application is closed or the device is restarted.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name            | Type   | Mandatory | Description                                       |
| ------------------ | ------- | ---- |-------------------------------------------|
| ratio | number | Yes  | Aspect ratio of the window content layout except border decoration. The value is a floating point number greater than or equal to 0.0. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300004 | Unauthorized operation.                      |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {

  // ...
  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    let windowClass: window.Window = windowStage.getMainWindowSync(); // Obtain the main window of the application.
    if (!windowClass) {
      console.info('windowClass is null');
    }
    try {
      let ratio = 1.0;
      let promise = windowClass.setAspectRatio(ratio);
      promise.then(() => {
        console.info('Succeeded in setting aspect ratio of window.');
      }).catch((err: BusinessError) => {
        console.error(`Failed to set the aspect ratio of window. Cause code: ${err.code}, message: ${err.message}`);
      });
    } catch (exception) {
      console.error(`Failed to set the aspect ratio of window. Cause code: ${exception.code}, message: ${exception.message}`);
    }
  }
}
```

### setAspectRatio<sup>10+</sup>

setAspectRatio(ratio: number, callback: AsyncCallback&lt;void&gt;): void

Sets the aspect ratio of the window content layout. This API uses an asynchronous callback to return the result.

This API is available only for the main window of the application. The aspect ratio will be saved permanently and takes effect even after the application is closed or the device is restarted.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name            | Type   | Mandatory | Description                                        |
| ------------------ | ------- | ---- |--------------------------------------------|
| ratio | number | Yes  | Aspect ratio of the window content layout except border decoration. The value is a floating point number greater than or equal to 0.0. |
| callback    | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.                                     |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300004 | Unauthorized operation.                      |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {

  // ...
  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    let windowClass: window.Window = windowStage.getMainWindowSync(); // Obtain the main window of the application.
    if (!windowClass) {
      console.info('Failed to load the content. Cause: windowClass is null');
    }
    try {
      let ratio = 1.0;
      windowClass.setAspectRatio(ratio, (err: BusinessError) => {
        const errCode: number = err.code;
        if (errCode) {
          console.error(`Failed to set the aspect ratio of window. Cause code: ${err.code}, message: ${err.message}`);
          return;
        }
        console.info('Succeeded in setting the aspect ratio of window.');
      });
    } catch (exception) {
      console.error(`Failed to set the aspect ratio of window. Cause code: ${exception.code}, message: ${exception.message}`);
    }
  }
}
```

### resetAspectRatio<sup>10+</sup>

resetAspectRatio(): Promise&lt;void&gt;

Resets the aspect ratio of the window content layout. This API uses a promise to return the result.

This API is available only for the main window of the application. After this API is called, the persistently stored aspect ratio is cleared.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300004 | Unauthorized operation.                      |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {

  // ...
  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    let windowClass: window.Window = windowStage.getMainWindowSync(); // Obtain the main window of the application.
    if (!windowClass) {
      console.info('Failed to load the content. Cause: windowClass is null');
    }
    try {
      let promise = windowClass.resetAspectRatio();
      promise.then(() => {
        console.info('Succeeded in resetting aspect ratio of window.');
      }).catch((err: BusinessError) => {
        console.error(`Failed to reset the aspect ratio of window. Cause code: ${err.code}, message: ${err.message}`);
      });
    } catch (exception) {
      console.error(`Failed to reset the aspect ratio of window. Cause code: ${exception.code}, message: ${exception.message}`);
    }
  }
}
```

### resetAspectRatio<sup>10+</sup>

resetAspectRatio(callback: AsyncCallback&lt;void&gt;): void

Resets the aspect ratio of the window content layout. This API uses an asynchronous callback to return the result.

This API is available only for the main window of the application. After this API is called, the persistently stored aspect ratio is cleared.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name            | Type   | Mandatory | Description                                                        |
| ------------------ | ------- | ---- | ------------------------------------------------------------ |
| callback    | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.          |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | -------------------------------------------- |
| 1300002 | This window state is abnormal.               |
| 1300004 | Unauthorized operation.                      |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {

  // ...
  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    let windowClass: window.Window = windowStage.getMainWindowSync(); // Obtain the main window of the application.
    if (!windowClass) {
      console.info('Failed to load the content. Cause: windowClass is null');
    }
    try {
      windowClass.resetAspectRatio((err: BusinessError) => {
        const errCode: number = err.code;
        if (errCode) {
          console.error(`Failed to reset the aspect ratio of window. Cause code: ${err.code}, message: ${err.message}`);
          return;
        }
        console.info('Succeeded in resetting aspect ratio of window.');
      });
    } catch (exception) {
      console.error(`Failed to reset the aspect ratio of window. Cause code: ${exception.code}, message: ${exception.message}`);
    }
  }
}
```

### minimize<sup>11+</sup>

minimize(callback: AsyncCallback&lt;void&gt;): void

Implements different functionalities based on the caller:

Minimizes the main window if the caller is the main window. The main window can be restored in the dock bar.

Hides the subwindow if the caller is a subwindow. The subwindow cannot be restored in the dock bar.

This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Window.SessionManager

**Parameters**

| Name  | Type                     | Mandatory | Description      |
| -------- | ------------------------- | ---- | ---------- |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300003 | This window manager service works abnormally. |

**Example**

```js
import { BusinessError } from '@ohos.base';

windowClass.minimize((err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to minimize the window. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in minimizing the window.');
});
```

### minimize<sup>11+</sup>

minimize(): Promise&lt;void&gt;

Implements different functionalities based on the caller:

Minimizes the main window if the caller is the main window. The main window can be restored in the dock bar.

Hides the subwindow if the caller is a subwindow. The subwindow cannot be restored in the dock bar.

This API uses a promise to return the result.

**System capability**: SystemCapability.Window.SessionManager

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300003 | This window manager service works abnormally. |

**Example**

```js
import { BusinessError } from '@ohos.base';

let promise = windowClass.minimize();
promise.then(() => {
  console.info('Succeeded in minimizing the window.');
}).catch((err: BusinessError) => {
  console.error('Failed to minimize the window. Cause: ' + JSON.stringify(err));
});
```

### recover<sup>11+</sup>

recover(): Promise&lt;void&gt;

Restores the main window from the full-screen, maximized, or split-screen mode to a floating window, and restores the window size and position to those before the full-screen, maximized, or split-screen mode is entered. If the main window is already in the floating window mode, nothing will happen. This API uses a promise to return the result. It takes effect only in the multi-window cascade layout.

**System capability**: SystemCapability.Window.SessionManager

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300001 | Repeated operation. |
| 1300002 | This window state is abnormal. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.recover();
promise.then(() => {
  console.info('Succeeded in recovering the window.');
}).catch((err: BusinessError) => {
  console.error('Failed to recover the window. Cause: ' + JSON.stringify(err));
});
```

### getWindowLimits<sup>11+</sup>

getWindowLimits(): WindowLimits

Obtains the size limits of this window.

**System capability**: SystemCapability.Window.SessionManager

**Return value**

| Type                         | Description          |
| ----------------------------- | ------------------ |
| [WindowLimits](#windowlimits11) | Window size limits. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message                      |
| :------- | :----------------------------- |
| 1300002  | This window state is abnormal. |

**Example**

```ts
try {
  let windowLimits = windowClass.getWindowLimits();
} catch (exception) {
  console.error('Failed to obtain the window limits of window. Cause: ' + JSON.stringify(exception));
}
```

### setWindowLimits<sup>11+</sup>

setWindowLimits(windowLimits: WindowLimits): Promise&lt;WindowLimits&gt;

Sets the size limits for this window. This API uses a promise to return the result.

**System capability**: SystemCapability.Window.SessionManager

**Parameters**

| Name      | Type                         | Mandatory | Description                          |
| :----------- | :---------------------------- | :--- | :----------------------------- |
| windowLimits | [WindowLimits](#windowlimits11) | Yes  | Target size limits, in px. |

**Return value**

| Type                                        | Description                               |
| :------------------------------------------- | :---------------------------------- |
| Promise&lt;[WindowLimits](#windowlimits11)&gt; | Promise used to return the new size limits. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message                                     |
| :------- | :-------------------------------------------- |
| 1300002  | This window state is abnormal.                |
| 1300003  | This window manager service works abnormally. |
| 1300004 | Unauthorized operation.                |

**Example**

```ts
import { BusinessError } from '@ohos.base';
try {
  let windowLimits: window.WindowLimits = {
    maxWidth: 1500,
    maxHeight: 1000,
    minWidth: 500,
    minHeight: 400
  };
  let promise = windowClass.setWindowLimits(windowLimits);
    promise.then((data) => {
    console.info('Succeeded in changing the window limits. Cause:' + JSON.stringify(data));
  }).catch((err: BusinessError) => {
    console.error('Failed to change the window limits. Cause: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to change the window limits. Cause:' + JSON.stringify(exception));
}
```

### keepKeyboardOnFocus<sup>11+</sup>

keepKeyboardOnFocus(keepKeyboardFlag: boolean): void

Sets whether to keep the soft keyboard created by others when a window has focus. This API can be called only by a system window or an application subwindow.

**System capability**: SystemCapability.Window.SessionManager

**Parameters**

| Name          | Type   | Mandatory | Description                                                        |
| ---------------- | ------- | ---- | ------------------------------------------------------------ |
| keepKeyboardFlag | boolean | Yes  | Whether to keep the soft keyboard created by others. The value **true** means to keep the soft keyboard, and **false** means the opposite.|

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ---------------------------------------- |
| 1300002 | This window state is abnormal.           |
| 1300004 | Unauthorized operation.                  |

**Example**

```ts
try {
  windowClass.keepKeyboardOnFocus(true);
} catch (exception) {
  console.error('Failed to keep keyboard onFocus. Cause: ' + JSON.stringify(exception));
}
```

### setWindowDecorVisible<sup>11+</sup>

setWindowDecorVisible(isVisible: boolean): void

Sets whether the title bar is visible in the main window.

**System capability**: SystemCapability.Window.SessionManager

**Parameters**

| Name   | Type   | Mandatory | Description                                         |
| --------- | ------- | ---- | --------------------------------------------- |
| isVisible | boolean | Yes  | Whether the title bar is visible. The value **true** means that the title bar is visible and **false** means the opposite. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message                      |
| -------- | ------------------------------ |
| 1300002  | This window state is abnormal. |
| 1300004  | Unauthorized operation.        |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    // Load content for the main window.
    windowStage.loadContent("pages/page2", (err: BusinessError) => {
      let errCode: number = err.code;
      if (errCode) {
        console.error('Failed to load the content. Cause:' + JSON.stringify(err));
        return;
      }
      console.info('Succeeded in loading the content.');
      // Obtain the main window.
      let mainWindow: window.Window | undefined = undefined;
      windowStage.getMainWindow((err: BusinessError, data) => {
        let errCode: number = err.code;
        if (errCode) {
          console.error('Failed to obtain the main window. Cause: ' + JSON.stringify(err));
          return;
        }
        mainWindow = data;
        console.info('Succeeded in obtaining the main window. Data: ' + JSON.stringify(data));
        let isVisible = false;
        // Call setWindowDecorVisible.
        try {
          mainWindow.setWindowDecorVisible(isVisible);
        } catch (exception) {
          console.error('Failed to set the visibility of window decor. Cause: ' + JSON.stringify(exception));
        }
      })
    });
  }
};
```

### setWindowDecorHeight<sup>11+</sup>

setWindowDecorHeight(height: number): void

Sets the title bar height of the main window or the decorated subwindow. This API can be used only on 2-in-1 devices.

**System capability**: SystemCapability.Window.SessionManager

**Parameters**

| Name | Type  | Mandatory | Description                                                        |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| height | number | Yes  | Height of the title bar. It takes effect only for the window with the title bar. The value is an integer in the range [37,112]. The unit is vp. If a floating point number is passed in, the value is rounded down. A value outside the range is invalid.|

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message                      |
| -------- | ------------------------------ |
| 1300002  | This window state is abnormal. |

**Example**

```ts
let height: number = 50;
try {
  windowClass.setWindowDecorHeight(height);
} catch (exception) {
  console.error('Failed to set the height of window decor. Cause: ' + JSON.stringify(exception));
}
```

### getWindowDecorHeight<sup>11+</sup>

getWindowDecorHeight(): number

Obtains the title bar height of the main window or the decorated subwindow. This API can be used only on 2-in-1 devices.

**System capability**: SystemCapability.Window.SessionManager

**Return value**

| Type  | Description                                                        |
| ------ | ------------------------------------------------------------ |
| number | Height of the title bar. The value is an integer in the range [48,112]. The unit is vp. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message                      |
| -------- | ------------------------------ |
| 1300002  | This window state is abnormal. |

**Example**

```ts
try {
  let height = windowClass.getWindowDecorHeight();
} catch (exception) {
  console.error('Failed to get the height of window decor. Cause: ' + JSON.stringify(exception));
}
```

### getTitleButtonRect<sup>11+</sup>

getTitleButtonRect(): TitleButtonRect

Obtains the rectangle that holds the minimize, maximize, and close buttons on the title bar of the main window or the decorated subwindow. This API can be used only on 2-in-1 devices.

**System capability**: SystemCapability.Window.SessionManager

**Return value**

| Type                                 | Description                                                        |
| ------------------------------------- | ------------------------------------------------------------ |
| [TitleButtonRect](#titlebuttonrect11) | Rectangle obtained, which is located in the upper right corner of the window. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message                      |
| -------- | ------------------------------ |
| 1300002  | This window state is abnormal. |

**Example**

```ts
try {
  let titleButtonArea = windowClass.getTitleButtonRect();
  console.info('Succeeded in obtaining the area of title buttons. Data: ' + JSON.stringify(titleButtonArea));
} catch (exception) {
  console.error('Failed to get the area of title buttons. Cause: ' + JSON.stringify(exception));
}
```

### show<sup>(deprecated)</sup>

show(callback: AsyncCallback&lt;void&gt;): void

Shows this window. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [showWindow()](#showwindow9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                     | Mandatory | Description      |
| -------- | ------------------------- | ---- | ---------- |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

windowClass.show((err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to show the window. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in showing the window.');
});
```

### show<sup>(deprecated)</sup>

show(): Promise&lt;void&gt;

Shows this window. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [showWindow()](#showwindow9-1) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.show();
promise.then(() => {
  console.info('Succeeded in showing the window.');
}).catch((err: BusinessError) => {
  console.error('Failed to show the window. Cause: ' + JSON.stringify(err));
});
```

### destroy<sup>(deprecated)</sup>

destroy(callback: AsyncCallback&lt;void&gt;): void

Destroys this window. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [destroyWindow()](#destroywindow9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                     | Mandatory | Description      |
| -------- | ------------------------- | ---- | ---------- |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

windowClass.destroy((err: BusinessError) => {
  const errCode: number = err.code;
  if (err.code) {
    console.error('Failed to destroy the window. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in destroying the window.');
});
```

### destroy<sup>(deprecated)</sup>

destroy(): Promise&lt;void&gt;

Destroys this window. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [destroyWindow()](#destroywindow9-1) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.destroy();
promise.then(() => {
  console.info('Succeeded in destroying the window.');
}).catch((err: BusinessError) => {
  console.error('Failed to destroy the window. Cause: ' + JSON.stringify(err));
});
```

### moveTo<sup>(deprecated)</sup>

moveTo(x: number, y: number, callback: AsyncCallback&lt;void&gt;): void

Moves this window. This API uses an asynchronous callback to return the result.

This operation is not supported in a window in full-screen mode.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [moveWindowTo()](#movewindowto9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                     | Mandatory | Description                                             |
| -------- | ------------------------- | ---- | ------------------------------------------------- |
| x        | number                    | Yes  | Distance that the window moves along the x-axis, in px. A positive value indicates that the window moves to the right. The value must be an integer. If a floating point number is passed in, the value is rounded down. |
| y        | number                    | Yes  | Distance that the window moves along the y-axis, in px. A positive value indicates that the window moves downwards. The value must be an integer. If a floating point number is passed in, the value is rounded down. |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.                                       |

**Example**

```ts
import { BusinessError } from '@ohos.base';

windowClass.moveTo(300, 300, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to move the window. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in moving the window.');
});
```

### moveTo<sup>(deprecated)</sup>

moveTo(x: number, y: number): Promise&lt;void&gt;

Moves this window. This API uses a promise to return the result.

This operation is not supported in a window in full-screen mode.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [moveWindowTo()](#movewindowto9-1) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type  | Mandatory | Description                                             |
| ------ | ------ | ---- | ------------------------------------------------- |
| x      | number | Yes  | Distance that the window moves along the x-axis, in px. A positive value indicates that the window moves to the right. The value must be an integer. If a floating point number is passed in, the value is rounded down. |
| y      | number | Yes  | Distance that the window moves along the y-axis, in px. A positive value indicates that the window moves downwards. The value must be an integer. If a floating point number is passed in, the value is rounded down. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.moveTo(300, 300);
promise.then(() => {
  console.info('Succeeded in moving the window.');
}).catch((err: BusinessError) => {
  console.error('Failed to move the window. Cause: ' + JSON.stringify(err));
});
```

### resetSize<sup>(deprecated)</sup>

resetSize(width: number, height: number, callback: AsyncCallback&lt;void&gt;): void

Changes the size of this window. This API uses an asynchronous callback to return the result.

The main window and subwindow have the following default size limits: [320, 1920] in width and [240, 1920] in height, both in units of vp.
The minimum width and height of the main window and subwindow of the application depends on the configuration on the product side. You can call [getWindowLimits](#getwindowlimits11) to obtain size limits.

The system window has the following size limits: [0, 1920] in width and [0, 1920] in height, both in units of vp.

The window width and height you set must meet the limits. The rules are as follows:
- If the window width or height you set is less than the minimum width or height limit, then the minimum width or height limit takes effect.
- If the window width or height you set is greater than the maximum width or height limit, then the maximum width or height limit takes effect.

This operation is not supported in a window in full-screen mode.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [resize()](#resize9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                     | Mandatory | Description                      |
| -------- | ------------------------- | ---- | -------------------------- |
| width    | number                    | Yes  | New width of the window, in px. The value must be an integer. If a floating point number is passed in, the value is rounded down. A negative value is invalid. |
| height   | number                    | Yes  | New height of the window, in px. The value must be an integer. If a floating point number is passed in, the value is rounded down. A negative value is invalid. |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.                |

**Example**

```ts
import { BusinessError } from '@ohos.base';

windowClass.resetSize(500, 1000, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to change the window size. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in changing the window size.');
});
```

### resetSize<sup>(deprecated)</sup>

resetSize(width: number, height: number): Promise&lt;void&gt;

Changes the size of this window. This API uses a promise to return the result.

The main window and subwindow have the following default size limits: [320, 1920] in width and [240, 1920] in height, both in units of vp.
The minimum width and height of the main window and subwindow of the application depends on the configuration on the product side. You can call [getWindowLimits](#getwindowlimits11) to obtain size limits.

The system window has the following size limits: [0, 1920] in width and [0, 1920] in height, both in units of vp.

The window width and height you set must meet the limits. The rules are as follows:
- If the window width or height you set is less than the minimum width or height limit, then the minimum width or height limit takes effect.
- If the window width or height you set is greater than the maximum width or height limit, then the maximum width or height limit takes effect.

This operation is not supported in a window in full-screen mode.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [resize()](#resize9-1) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type  | Mandatory | Description                      |
| ------ | ------ | ---- | -------------------------- |
| width  | number | Yes  | New width of the window, in px. The value must be an integer. If a floating point number is passed in, the value is rounded down. A negative value is invalid. |
| height | number | Yes  | New height of the window, in px. The value must be an integer. If a floating point number is passed in, the value is rounded down. A negative value is invalid. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.resetSize(500, 1000);
promise.then(() => {
  console.info('Succeeded in changing the window size.');
}).catch((err: BusinessError) => {
  console.error('Failed to change the window size. Cause: ' + JSON.stringify(err));
});
```

### getProperties<sup>(deprecated)</sup>

getProperties(callback: AsyncCallback&lt;WindowProperties&gt;): void

Obtains the properties of this window. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 6 and deprecated since API version 9. You are advised to use [getWindowProperties()](#getwindowproperties9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                                      | Mandatory | Description                        |
| -------- | ---------------------------------------------------------- | ---- | ---------------------------- |
| callback | AsyncCallback&lt;[WindowProperties](#windowproperties)&gt; | Yes  | Callback used to return the window properties. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

windowClass.getProperties((err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to obtain the window properties. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in obtaining the window properties. Data: ' + JSON.stringify(data));
});
```

### getProperties<sup>(deprecated)</sup>

getProperties(): Promise&lt;WindowProperties&gt;

Obtains the properties of this window. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 6 and deprecated since API version 9. You are advised to use [getWindowProperties()](#getwindowproperties9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Return value**

| Type                                                | Description                           |
| ---------------------------------------------------- | ------------------------------- |
| Promise&lt;[WindowProperties](#windowproperties)&gt; | Promise used to return the window properties. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.getProperties();
promise.then((data) => {
  console.info('Succeeded in obtaining the window properties. Data: ' + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error('Failed to obtain the window properties. Cause: ' + JSON.stringify(err));
});
```

### getAvoidArea<sup>(deprecated)</sup>

getAvoidArea(type: [AvoidAreaType](#avoidareatype7), callback: AsyncCallback&lt;[AvoidArea](#avoidarea7)&gt;): void

Obtains the area where this window cannot be displayed, for example, the system bar area, notch, gesture area, and soft keyboard area. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [getWindowAvoidArea()](#getwindowavoidarea9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                           | Mandatory | Description                                                        |
| -------- |-----------------------------------------------| ---- | ------------------------------------------------------------ |
| type     | [AvoidAreaType](#avoidareatype7)              | Yes  | Type of the area.|
| callback | AsyncCallback&lt;[AvoidArea](#avoidarea7)&gt; | Yes  | Callback used to return the area.                            |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let type = window.AvoidAreaType.TYPE_SYSTEM;
windowClass.getAvoidArea(type, (err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to obtain the area. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in obtaining the area. Data:' + JSON.stringify(data));
});
```

### getAvoidArea<sup>(deprecated)</sup>

getAvoidArea(type: [AvoidAreaType](#avoidareatype7)): Promise&lt;[AvoidArea](#avoidarea7)&gt;

Obtains the area where this window cannot be displayed, for example, the system bar area, notch, gesture area, and soft keyboard area. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [getWindowAvoidArea()](#getwindowavoidarea9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type                              | Mandatory | Description                                                        |
| ------ |----------------------------------| ---- | ------------------------------------------------------------ |
| type   | [AvoidAreaType](#avoidareatype7) | Yes  | Type of the area. |

**Return value**

| Type                                     | Description                               |
|-----------------------------------------| ----------------------------------- |
| Promise&lt;[AvoidArea](#avoidarea7)&gt; | Promise used to return the area. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let type = window.AvoidAreaType.TYPE_SYSTEM;
let promise = windowClass.getAvoidArea(type);
promise.then((data) => {
  console.info('Succeeded in obtaining the area. Data:' + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error('Failed to obtain the area. Cause:' + JSON.stringify(err));
});
```

### setFullScreen<sup>(deprecated)</sup>

setFullScreen(isFullScreen: boolean, callback: AsyncCallback&lt;void&gt;): void

Sets whether the main window or the subwindow is in full-screen mode. This API uses an asynchronous callback to return the result.
- In full-screen mode, the layout does not avoid the status bar and navigation bar, and components may overlap with them.
- In non-full-screen mode, the layout avoids the status bar and navigation bar, and components do not overlap with them.

> **NOTE**
>
> This API is supported since API version 6 and deprecated since API version 9. You are advised to use [setWindowSystemBarEnable()](#setwindowsystembarenable9) and [setWindowLayoutFullScreen()](#setwindowlayoutfullscreen9) to implement the full-screen mode.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name      | Type                     | Mandatory | Description                                          |
| ------------ | ------------------------- | ---- | ---------------------------------------------- |
| isFullScreen | boolean                   | Yes  | Whether to set full-screen mode. This setting affects the display of the status bar and navigation bar. The value **true** means to set full-screen mode, and **false** means the opposite. |
| callback     | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.                                    |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isFullScreen: boolean = true;
windowClass.setFullScreen(isFullScreen, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to enable the full-screen mode. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in enabling the full-screen mode.');
});
```

### setFullScreen<sup>(deprecated)</sup>

setFullScreen(isFullScreen: boolean): Promise&lt;void&gt;

Sets whether the main window or the subwindow is in full-screen mode. This API uses a promise to return the result.
- In full-screen mode, the layout does not avoid the status bar and navigation bar, and components may overlap with them.
- In non-full-screen mode, the layout avoids the status bar and navigation bar, and components do not overlap with them.

> **NOTE**
>
> This API is supported since API version 6 and deprecated since API version 9. You are advised to use [setWindowSystemBarEnable()](#setwindowsystembarenable9-1) and [setWindowLayoutFullScreen()](#setwindowlayoutfullscreen9-1) to implement the full-screen mode.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name      | Type   | Mandatory | Description                                          |
| ------------ | ------- | ---- | ---------------------------------------------- |
| isFullScreen | boolean | Yes  | Whether to set full-screen mode. This setting affects the display of the status bar and navigation bar. The value **true** means to set full-screen mode, and **false** means the opposite. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isFullScreen: boolean = true;
let promise = windowClass.setFullScreen(isFullScreen);
promise.then(() => {
  console.info('Succeeded in enabling the full-screen mode.');
}).catch((err: BusinessError) => {
  console.error('Failed to enable the full-screen mode. Cause: ' + JSON.stringify(err));
});
```

### setLayoutFullScreen<sup>(deprecated)</sup>

setLayoutFullScreen(isLayoutFullScreen: boolean, callback: AsyncCallback&lt;void&gt;): void

Sets whether the main window layout or the subwindow layout is immersive. This API uses an asynchronous callback to return the result.
An immersive layout means that the layout does not avoid the status bar and navigation bar, and components may overlap with them.
A non-immersive layout means that the layout avoids the status bar and navigation bar, and components do not overlap with them.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [setWindowLayoutFullScreen()](#setwindowlayoutfullscreen9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name            | Type                     | Mandatory | Description                                                        |
| ------------------ | ------------------------- | ---- | ------------------------------------------------------------ |
| isLayoutFullScreen | boolean                   | Yes  | Whether the window layout is immersive. This setting does not affect the display of the status bar and navigation bar. The value **true** means that the window layout is immersive, and **false** means the opposite. |
| callback           | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.                                                  |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isLayoutFullScreen: boolean = true;
windowClass.setLayoutFullScreen(isLayoutFullScreen, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set the window layout to full-screen mode. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting the window layout to full-screen mode.');
});
```

### setLayoutFullScreen<sup>(deprecated)</sup>

setLayoutFullScreen(isLayoutFullScreen: boolean): Promise&lt;void&gt;

Sets whether the main window layout or the subwindow layout is immersive. This API uses a promise to return the result.
An immersive layout means that the layout does not avoid the status bar and navigation bar, and components may overlap with them.
A non-immersive layout means that the layout avoids the status bar and navigation bar, and components do not overlap with them.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [setWindowLayoutFullScreen()](#setwindowlayoutfullscreen9-1) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name            | Type   | Mandatory | Description                                                        |
| ------------------ | ------- | ---- | ------------------------------------------------------------ |
| isLayoutFullScreen | boolean | Yes  | Whether the window layout is immersive. This setting does not affect the display of the status bar and navigation bar. The value **true** means that the window layout is immersive, and **false** means the opposite. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isLayoutFullScreen: boolean = true;
let promise = windowClass.setLayoutFullScreen(isLayoutFullScreen);
promise.then(() => {
  console.info('Succeeded in setting the window layout to full-screen mode.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the window layout to full-screen mode. Cause:' + JSON.stringify(err));
});
```

### setSystemBarEnable<sup>(deprecated)</sup>

setSystemBarEnable(names: Array<'status' | 'navigation'>, callback: AsyncCallback&lt;void&gt;): void

Sets whether to display the status bar and navigation bar when the window is in full-screen mode. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [setWindowSystemBarEnable()](#setwindowsystembarenable9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                     | Mandatory | Description                                                        |
| -------- | ---------------------------- | ---- | ------------------------------------------------------------ |
| names    | Array<'status'\|'navigation'> | Yes  | Whether to display the status bar and navigation bar when the window is in full-screen mode.<br>For example, to display the status bar and navigation bar, set this parameter to **['status', 'navigation']**. By default, they are not displayed. |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.                                                  |

**Example**

```ts
// In this example, the status bar and navigation bar are not displayed.
import { BusinessError } from '@ohos.base';

let names: Array<'status' | 'navigation'> = [];
windowClass.setSystemBarEnable(names, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set the system bar to be invisible. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting the system bar to be invisible.');
});
```

### setSystemBarEnable<sup>(deprecated)</sup>

setSystemBarEnable(names: Array<'status' | 'navigation'>): Promise&lt;void&gt;

Sets whether to display the status bar and navigation bar when the window is in full-screen mode. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [setWindowSystemBarEnable()](#setwindowsystembarenable9-1) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type | Mandatory | Description                                                        |
| ------ | ---------------------------- | ---- | ------------------------ |
| names  | Array<'status'\|'navigation'> | Yes  | Whether to display the status bar and navigation bar when the window is in full-screen mode.<br>For example, to display the status bar and navigation bar, set this parameter to **['status', 'navigation']**. By default, they are not displayed. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Example**

```ts
// In this example, the status bar and navigation bar are not displayed.
import { BusinessError } from '@ohos.base';

let names: Array<'status' | 'navigation'> = [];
let promise = windowClass.setSystemBarEnable(names);
promise.then(() => {
  console.info('Succeeded in setting the system bar to be invisible.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the system bar to be invisible. Cause:' + JSON.stringify(err));
});
```

### setSystemBarProperties<sup>(deprecated)</sup>

setSystemBarProperties(systemBarProperties: SystemBarProperties, callback: AsyncCallback&lt;void&gt;): void

Sets the properties of the status bar and navigation bar when the main window is in full-screen mode. This API uses an asynchronous callback to return the result. The setting does not take effect for 2-in-1 devices.

> **NOTE**
>
> This API is supported since API version 6 and deprecated since API version 9. You are advised to use [setWindowSystemBarProperties()](#setwindowsystembarproperties9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name             | Type                                       | Mandatory | Description                  |
| ------------------- | ------------------------------------------- | ---- | ---------------------- |
| systemBarProperties | [SystemBarProperties](#systembarproperties) | Yes  | Properties of the status bar and navigation bar. |
| callback            | AsyncCallback&lt;void&gt;                   | Yes  | Callback used to return the result.            |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let SystemBarProperties: window.SystemBarProperties = {
  statusBarColor: '#ff00ff',
  navigationBarColor: '#00ff00',
  // The following properties are supported since API version 8.
  statusBarContentColor: '#ffffff',
  navigationBarContentColor: '#00ffff'
};
windowClass.setSystemBarProperties(SystemBarProperties, (err) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set the system bar properties. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting the system bar properties.');
});
```

### setSystemBarProperties<sup>(deprecated)</sup>

setSystemBarProperties(systemBarProperties: SystemBarProperties): Promise&lt;void&gt;

Sets the properties of the status bar and navigation bar when the main window is in full-screen mode. This API uses a promise to return the result. The setting does not take effect for 2-in-1 devices.

> **NOTE**
>
> This API is supported since API version 6 and deprecated since API version 9. You are advised to use [setWindowSystemBarProperties()](#setwindowsystembarproperties9-1) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name             | Type                                       | Mandatory | Description                  |
| ------------------- | ------------------------------------------- | ---- | ---------------------- |
| systemBarProperties | [SystemBarProperties](#systembarproperties) | Yes  | Properties of the status bar and navigation bar. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let SystemBarProperties: window.SystemBarProperties = {
  statusBarColor: '#ff00ff',
  navigationBarColor: '#00ff00',
  // The following properties are supported since API version 8.
  statusBarContentColor: '#ffffff',
  navigationBarContentColor: '#00ffff'
};
let promise = windowClass.setSystemBarProperties(SystemBarProperties);
promise.then(() => {
  console.info('Succeeded in setting the system bar properties.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the system bar properties. Cause: ' + JSON.stringify(err));
});
```

### loadContent<sup>(deprecated)</sup>

loadContent(path: string, callback: AsyncCallback&lt;void&gt;): void

Loads content from a page to this window. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [setUIContent()](#setuicontent9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                     | Mandatory | Description                |
| -------- | ------------------------- | ---- | -------------------- |
| path     | string                    | Yes  | Path of the page from which the content will be loaded. In the stage model, the path is configured in the **main_pages.json** file of the project. In the FA model, the path is configured in the **config.json** file of the project. |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.          |

**Example**

```ts
import { BusinessError } from '@ohos.base';

windowClass.loadContent('pages/page2/page3', (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to load the content. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in loading the content.');
});
```

### loadContent<sup>(deprecated)</sup>

loadContent(path: string): Promise&lt;void&gt;

Loads content from a page to this window. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [setUIContent()](#setuicontent9-1) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type  | Mandatory | Description                |
| ------ | ------ | ---- | -------------------- |
| path   | string | Yes  | Path of the page from which the content will be loaded. In the stage model, the path is configured in the **main_pages.json** file of the project. In the FA model, the path is configured in the **config.json** file of the project. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.loadContent('pages/page2/page3');
promise.then(() => {
  console.info('Succeeded in loading the content.');
}).catch((err: BusinessError) => {
  console.error('Failed to load the content. Cause: ' + JSON.stringify(err));
});
```

### isShowing<sup>(deprecated)</sup>

isShowing(callback: AsyncCallback&lt;boolean&gt;): void

Checks whether this window is displayed. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [isWindowShowing()](#iswindowshowing9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                        | Mandatory | Description                                                        |
| -------- | ---------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback&lt;boolean&gt; | Yes  | Callback used to return the result. The value **true** means that the window is displayed, and **false** means the opposite. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

windowClass.isShowing((err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to check whether the window is showing. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in checking whether the window is showing. Data: ' + JSON.stringify(data));
});
```

### isShowing<sup>(deprecated)</sup>

isShowing(): Promise&lt;boolean&gt;

Checks whether this window is displayed. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [isWindowShowing()](#iswindowshowing9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Return value**

| Type                  | Description                                                        |
| ---------------------- | ------------------------------------------------------------ |
| Promise&lt;boolean&gt; | Promise used to return the result. The value **true** means that the window is displayed, and **false** means the opposite. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.isShowing();
promise.then((data) => {
  console.info('Succeeded in checking whether the window is showing. Data: ' + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error('Failed to check whether the window is showing. Cause: ' + JSON.stringify(err));
});
```

### on('systemAvoidAreaChange')<sup>(deprecated)</sup>

on(type: 'systemAvoidAreaChange', callback: Callback&lt;AvoidArea&gt;): void

Subscribes to the event indicating changes to the area where the window cannot be displayed.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. Use [on('avoidAreaChange')](#onavoidareachange9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                      | Mandatory | Description                                                   |
| -------- |------------------------------------------| ---- | ------------------------------------------------------- |
| type     | string                                   | Yes  | Event type. The value is fixed at **'systemAvoidAreaChange'**, indicating the event of changes to the area where the window cannot be displayed. |
| callback | Callback&lt;[AvoidArea](#avoidarea7)&gt; | Yes  | Callback used to return the area.                            |

**Example**

```ts
windowClass.on('systemAvoidAreaChange', (data) => {
  console.info('Succeeded in enabling the listener for system avoid area changes. Data: ' + JSON.stringify(data));
});
```

### off('systemAvoidAreaChange')<sup>(deprecated)</sup>

off(type: 'systemAvoidAreaChange', callback?: Callback&lt;AvoidArea&gt;): void

Unsubscribes from the event indicating changes to the area where the window cannot be displayed.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. Use [off('avoidAreaChange')](#offavoidareachange9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                      | Mandatory | Description                                                   |
| -------- |------------------------------------------| ---- | ------------------------------------------------------- |
| type     | string                                   | Yes  | Event type. The value is fixed at **'systemAvoidAreaChange'**, indicating the event of changes to the area where the window cannot be displayed. |
| callback | Callback&lt;[AvoidArea](#avoidarea7)&gt; | No  | Callback used to return the area. If a value is passed in, the corresponding subscription is canceled. If no value is passed in, all subscriptions to the specified event are canceled.          |

**Example**

```ts
windowClass.off('systemAvoidAreaChange');
```

### isSupportWideGamut<sup>(deprecated)</sup>

isSupportWideGamut(callback: AsyncCallback&lt;boolean&gt;): void

Checks whether this window supports the wide-gamut color space. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [isWindowSupportWideGamut()](#iswindowsupportwidegamut9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                        | Mandatory | Description                                                        |
| -------- | ---------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback&lt;boolean&gt; | Yes  | Callback used to return the result. The value **true** means that the wide-gamut color space is supported, and **false** means the opposite. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

windowClass.isSupportWideGamut((err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to check whether the window support WideGamut. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in checking whether the window support WideGamut Data: ' + JSON.stringify(data));
});
```

### isSupportWideGamut<sup>(deprecated)</sup>

isSupportWideGamut(): Promise&lt;boolean&gt;

Checks whether this window supports the wide-gamut color space. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [isWindowSupportWideGamut()](#iswindowsupportwidegamut9-1) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Return value**

| Type                  | Description                                                        |
| ---------------------- | ------------------------------------------------------------ |
| Promise&lt;boolean&gt; | Promise used to return the result. The value **true** means that the wide-gamut color space is supported, and **false** means the opposite. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.isSupportWideGamut();
promise.then((data) => {
  console.info('Succeeded in checking whether the window support WideGamut. Data: ' + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error('Failed to check whether the window support WideGamut. Cause: ' + JSON.stringify(err));
});
```

### setColorSpace<sup>(deprecated)</sup>

setColorSpace(colorSpace:ColorSpace, callback: AsyncCallback&lt;void&gt;): void

Sets a color space for this window. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [setWindowColorSpace()](#setwindowcolorspace9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name    | Type                     | Mandatory | Description        |
| ---------- | ------------------------- | ---- | ------------ |
| colorSpace | [ColorSpace](#colorspace8) | Yes  | Color space to set. |
| callback   | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.  |

**Example**

```ts
import { BusinessError } from '@ohos.base';

windowClass.setColorSpace(window.ColorSpace.WIDE_GAMUT, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set window colorspace. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting window colorspace.');
});
```

### setColorSpace<sup>(deprecated)</sup>

setColorSpace(colorSpace:ColorSpace): Promise&lt;void&gt;

Sets a color space for this window. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [setWindowColorSpace()](#setwindowcolorspace9-1) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name    | Type                     | Mandatory | Description          |
| ---------- | ------------------------- | ---- | -------------- |
| colorSpace | [ColorSpace](#colorspace8) | Yes  | Color space to set. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.setColorSpace(window.ColorSpace.WIDE_GAMUT);
promise.then(() => {
  console.info('Succeeded in setting window colorspace.');
}).catch((err: BusinessError) => {
  console.error('Failed to set window colorspace. Cause: ' + JSON.stringify(err));
});
```

### getColorSpace<sup>(deprecated)</sup>

getColorSpace(callback: AsyncCallback&lt;ColorSpace&gt;): void

Obtains the color space of this window. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [getWindowColorSpace()](#getwindowcolorspace9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                          | Mandatory | Description                                                      |
| -------- | ---------------------------------------------- | ---- | ---------------------------------------------------------- |
| callback | AsyncCallback&lt;[ColorSpace](#colorspace8)&gt; | Yes  | Callback used to return the result. When the color space is obtained successfully, **err** is **undefined**, and **data** is the current color space. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

windowClass.getColorSpace((err: BusinessError, data) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to get window colorspace. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in getting window colorspace. Cause:' + JSON.stringify(data));
});
```

### getColorSpace<sup>(deprecated)</sup>

getColorSpace(): Promise&lt;ColorSpace&gt;

Obtains the color space of this window. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [getWindowColorSpace()](#getwindowcolorspace9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Return value**

| Type                                    | Description                           |
| ---------------------------------------- | ------------------------------- |
| Promise&lt;[ColorSpace](#colorspace8)&gt; | Promise used to return the current color space. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.getColorSpace();
promise.then((data) => {
  console.info('Succeeded in getting window color space. Cause:' + JSON.stringify(data));
}).catch((err: BusinessError) => {
  console.error('Failed to get window colorspace. Cause: ' + JSON.stringify(err));
});
```

### setBackgroundColor<sup>(deprecated)</sup>

setBackgroundColor(color: string, callback: AsyncCallback&lt;void&gt;): void

Sets the background color for this window. This API uses an asynchronous callback to return the result. In the stage model, this API must be used after the call of [loadContent](#loadcontent9) or [setUIContent()](#setuicontent9) takes effect.

> **NOTE**
>
> This API is supported since API version 6 and deprecated since API version 9. You are advised to use [setWindowBackgroundColor()](#setwindowbackgroundcolor9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                     | Mandatory | Description                                                        |
| -------- | ------------------------- | ---- | ------------------------------------------------------------ |
| color    | string                    | Yes  | Background color to set. The value is a hexadecimal RGB or ARGB color code and is case insensitive, for example, **'#00FF00'** or **'#FF00FF00'**. |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.                                                  |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let color: string = '#00ff33';
windowClass.setBackgroundColor(color, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set the background color. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting the background color.');
});
```

### setBackgroundColor<sup>(deprecated)</sup>

setBackgroundColor(color: string): Promise&lt;void&gt;

Sets the background color for this window. This API uses a promise to return the result. In the stage model, this API must be used after the call of [loadContent](#loadcontent9) or [setUIContent()](#setuicontent9) takes effect.

> **NOTE**
>
> This API is supported since API version 6 and deprecated since API version 9. You are advised to use [setWindowBackgroundColor()](#setwindowbackgroundcolor9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type  | Mandatory | Description                                                        |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| color  | string | Yes  | Background color to set. The value is a hexadecimal RGB or ARGB color code and is case insensitive, for example, **'#00FF00'** or **'#FF00FF00'**. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let color: string = '#00ff33';
let promise = windowClass.setBackgroundColor(color);
promise.then(() => {
  console.info('Succeeded in setting the background color.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the background color. Cause: ' + JSON.stringify(err));
});
```

### setBrightness<sup>(deprecated)</sup>

setBrightness(brightness: number, callback: AsyncCallback&lt;void&gt;): void

Sets the screen brightness for this window. This API uses an asynchronous callback to return the result.

When the screen brightness setting for the window takes effect, Control Panel cannot adjust the system screen brightness. It can do so only after the window screen brightness is restored to the default value.

> **NOTE**
>
> This API is supported since API version 6 and deprecated since API version 9. You are advised to use [setWindowBrightness()](#setwindowbrightness9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name    | Type                     | Mandatory | Description                                   |
| ---------- | ------------------------- | ---- |---------------------------------------|
| brightness | number                    | Yes  | Brightness to set. The value is a floating point number in the range [0.0, 1.0] or **-1.0**. The value **1.0** means the brightest, and **-1.0** means the default brightness. |
| callback   | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.                                |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let brightness: number = 1;
windowClass.setBrightness(brightness, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set the brightness. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting the brightness.');
});
```

### setBrightness<sup>(deprecated)</sup>

setBrightness(brightness: number): Promise&lt;void&gt;

Sets the screen brightness for this window. This API uses a promise to return the result.

When the screen brightness setting for the window takes effect, Control Panel cannot adjust the system screen brightness. It can do so only after the window screen brightness is restored to the default value.

> **NOTE**
>
> This API is supported since API version 6 and deprecated since API version 9. You are advised to use [setWindowBrightness()](#setwindowbrightness9-1) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name    | Type  | Mandatory | Description                                      |
| ---------- | ------ | ---- |------------------------------------------|
| brightness | number | Yes  | Brightness to set. The value is a floating point number in the range [0.0, 1.0] or **-1.0**. The value **1.0** means the brightest, and **-1.0** means the default brightness. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let brightness: number = 1;
let promise = windowClass.setBrightness(brightness);
promise.then(() => {
  console.info('Succeeded in setting the brightness.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the brightness. Cause: ' + JSON.stringify(err));
});
```

### setDimBehind<sup>(deprecated)</sup>

setDimBehind(dimBehindValue: number, callback: AsyncCallback&lt;void&gt;): void

Sets the dimness of the window that is not on top. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API cannot be used. This API is supported since API version 7 and deprecated since API version 9.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name        | Type                     | Mandatory | Description                                    |
| -------------- | ------------------------- | ---- |----------------------------------------|
| dimBehindValue | number                    | Yes  | Dimness of the window to set. The value range is [0.0, 1.0], and the value **1.0** means the dimmest. |
| callback       | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.                                 |

**Example**

```ts
import { BusinessError } from '@ohos.base';

windowClass.setDimBehind(0.5, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set the dimness. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting the dimness.');
});
```

### setDimBehind<sup>(deprecated)</sup>

setDimBehind(dimBehindValue: number): Promise&lt;void&gt;

Sets the dimness of the window that is not on top. This API uses a promise to return the result.

> **NOTE**
>
> This API cannot be used. This API is supported since API version 7 and deprecated since API version 9.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name        | Type  | Mandatory | Description                                              |
| -------------- | ------ | ---- | -------------------------------------------------- |
| dimBehindValue | number | Yes  | Dimness of the window to set. The value ranges from 0 to 1. The value **1** indicates the dimmest. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let promise = windowClass.setDimBehind(0.5);
promise.then(() => {
  console.info('Succeeded in setting the dimness.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the dimness. Cause: ' + JSON.stringify(err));
});
```

### setFocusable<sup>(deprecated)</sup>

setFocusable(isFocusable: boolean, callback: AsyncCallback&lt;void&gt;): void

Sets whether this window is focusable, that is, whether the window can gain focus after it is being clicked or using other methods. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [setWindowFocusable()](#setwindowfocusable9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name     | Type                     | Mandatory | Description                        |
| ----------- | ------------------------- | ---- | ---------------------------- |
| isFocusable | boolean                   | Yes  | Whether the window can gain focus. The value **true** means that the window can gain focus, and **false** means the opposite. |
| callback    | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.                  |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isFocusable: boolean = true;
windowClass.setFocusable(isFocusable, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set the window to be focusable. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting the window to be focusable.');
});
```

### setFocusable<sup>(deprecated)</sup>

setFocusable(isFocusable: boolean): Promise&lt;void&gt;

Sets whether this window is focusable, that is, whether the window can gain focus after it is being clicked or using other methods. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [setWindowFocusable()](#setwindowfocusable9-1) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name     | Type   | Mandatory | Description                        |
| ----------- | ------- | ---- | ---------------------------- |
| isFocusable | boolean | Yes  | Whether the window can gain focus. The value **true** means that the window can gain focus, and **false** means the opposite. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isFocusable: boolean = true;
let promise = windowClass.setFocusable(isFocusable);
promise.then(() => {
  console.info('Succeeded in setting the window to be focusable.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the window to be focusable. Cause: ' + JSON.stringify(err));
});
```

### setKeepScreenOn<sup>(deprecated)</sup>

setKeepScreenOn(isKeepScreenOn: boolean, callback: AsyncCallback&lt;void&gt;): void

Sets whether to keep the screen always on. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 6 and deprecated since API version 9. You are advised to use [setWindowKeepScreenOn()](#setwindowkeepscreenon9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name        | Type                     | Mandatory | Description                    |
| -------------- | ------------------------- | ---- | ------------------------ |
| isKeepScreenOn | boolean                   | Yes  | Whether to keep the screen always on. The value **true** means to keep the screen always on, and **false** means the opposite. |
| callback       | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.              |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isKeepScreenOn: boolean = true;
windowClass.setKeepScreenOn(isKeepScreenOn, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set the screen to be always on. Cause: ' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting the screen to be always on.');
});
```

### setKeepScreenOn<sup>(deprecated)</sup>

setKeepScreenOn(isKeepScreenOn: boolean): Promise&lt;void&gt;

Sets whether to keep the screen always on. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 6 and deprecated since API version 9. You are advised to use [setWindowKeepScreenOn()](#setwindowkeepscreenon9-1) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name        | Type   | Mandatory | Description                    |
| -------------- | ------- | ---- | ------------------------ |
| isKeepScreenOn | boolean | Yes  | Whether to keep the screen always on. The value **true** means to keep the screen always on, and **false** means the opposite. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isKeepScreenOn: boolean = true;
let promise = windowClass.setKeepScreenOn(isKeepScreenOn);
promise.then(() => {
  console.info('Succeeded in setting the screen to be always on.');
}).catch((err: BusinessError) => {
  console.info('Failed to set the screen to be always on. Cause:  ' + JSON.stringify(err));
});
```

### setOutsideTouchable<sup>(deprecated)</sup>

setOutsideTouchable(touchable: boolean, callback: AsyncCallback&lt;void&gt;): void

Sets whether the area outside the subwindow is touchable. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9.
> 
> Since API version 9, the area outside the subwindow is touchable by default. This API is no longer supported and no substitute API is provided.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name   | Type                     | Mandatory | Description            |
| --------- | ------------------------- | ---- | ---------------- |
| touchable | boolean                   | Yes  | Whether the area outside the subwindow is touchable. The value **true** means the area outside the subwindow is touchable, and **false** means the opposite. |
| callback  | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.      |

**Example**

```ts
import { BusinessError } from '@ohos.base';

if (!windowClass) {
  console.info('Failed to load the content. Cause: windowClass is null');
}
else {
  (windowClass as window.Window).setOutsideTouchable(true, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the area to be touchable. Cause: ' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the area to be touchable.');
  });
}
```

### setOutsideTouchable<sup>(deprecated)</sup>

setOutsideTouchable(touchable: boolean): Promise&lt;void&gt;

Sets whether the area outside the subwindow is touchable. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9.
> 
> Since API version 9, the area outside the subwindow is touchable by default. This API is no longer supported and no substitute API is provided.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name   | Type   | Mandatory | Description            |
| --------- | ------- | ---- | ---------------- |
| touchable | boolean | Yes  | Whether the area outside the subwindow is touchable. The value **true** means the area outside the subwindow is touchable, and **false** means the opposite. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

if (!windowClass) {
  console.info('Failed to load the content. Cause: windowClass is null');
}
else {
let promise = (windowClass as window.Window).setOutsideTouchable(true);
promise.then(() => {
  console.info('Succeeded in setting the area to be touchable.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the area to be touchable. Cause: ' + JSON.stringify(err));
});
}
```

### setPrivacyMode<sup>(deprecated)</sup>

setPrivacyMode(isPrivacyMode: boolean, callback: AsyncCallback&lt;void&gt;): void

Sets whether this window is in privacy mode. This API uses an asynchronous callback to return the result.

A window in privacy mode cannot be captured or recorded. This API can be used in scenarios where screen capture or recording is disabled.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [setWindowPrivacyMode()](#setwindowprivacymode9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name       | Type                     | Mandatory | Description                |
| ------------- | ------------------------- | ---- | -------------------- |
| isPrivacyMode | boolean                   | Yes  | Whether the window is in privacy mode. The value **true** means that the window is in privacy mode, and **false** means the opposite. |
| callback      | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.          |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isPrivacyMode: boolean = true;
windowClass.setPrivacyMode(isPrivacyMode, (err: BusinessError) => {
  const errCode: number = err.code;
  if (errCode) {
    console.error('Failed to set the window to privacy mode. Cause:' + JSON.stringify(err));
    return;
  }
  console.info('Succeeded in setting the window to privacy mode.');
});
```

### setPrivacyMode<sup>(deprecated)</sup>

setPrivacyMode(isPrivacyMode: boolean): Promise&lt;void&gt;

Sets whether this window is in privacy mode. This API uses a promise to return the result.

A window in privacy mode cannot be captured or recorded. This API can be used in scenarios where screen capture or recording is disabled.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [setWindowPrivacyMode()](#setwindowprivacymode9-1) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name       | Type   | Mandatory | Description                |
| ------------- | ------- | ---- | -------------------- |
| isPrivacyMode | boolean | Yes  | Whether the window is in privacy mode. The value **true** means that the window is in privacy mode, and **false** means the opposite. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isPrivacyMode: boolean = true;
let promise = windowClass.setPrivacyMode(isPrivacyMode);
promise.then(() => {
  console.info('Succeeded in setting the window to privacy mode.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the window to privacy mode. Cause: ' + JSON.stringify(err));
});
```

### setTouchable<sup>(deprecated)</sup>

setTouchable(isTouchable: boolean, callback: AsyncCallback&lt;void&gt;): void

Sets whether this window is touchable. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [setWindowTouchable()](#setwindowtouchable9) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name     | Type                     | Mandatory | Description                |
| ----------- | ------------------------- | ---- | -------------------- |
| isTouchable | boolean                   | Yes  | Whether the window is touchable. The value **true** means that the window is touchable, and **false** means the opposite. |
| callback    | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.          |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isTouchable = true;
if (!windowClass) {
  console.info('Failed to load the content. Cause: windowClass is null');
}
else {
  (windowClass as window.Window).setTouchable(isTouchable, (err: BusinessError) => {
    const errCode: number = err.code;
    if (errCode) {
      console.error('Failed to set the window to be touchable. Cause:' + JSON.stringify(err));
      return;
    }
    console.info('Succeeded in setting the window to be touchable.');
  });
}
```

### setTouchable<sup>(deprecated)</sup>

setTouchable(isTouchable: boolean): Promise&lt;void&gt;

Sets whether this window is touchable. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [setWindowTouchable()](#setwindowtouchable9-1) instead.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name     | Type   | Mandatory | Description                |
| ----------- | ------- | ---- | -------------------- |
| isTouchable | boolean | Yes  | Whether the window is touchable. The value **true** means that the window is touchable, and **false** means the opposite. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let isTouchable = true;
let promise = windowClass.setTouchable(isTouchable);
promise.then(() => {
  console.info('Succeeded in setting the window to be touchable.');
}).catch((err: BusinessError) => {
  console.error('Failed to set the window to be touchable. Cause: ' + JSON.stringify(err));
});
```

## WindowStageEventType<sup>9+</sup>

Describes the lifecycle of a window stage.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

| Name      | Value | Description      |
| ---------- | ------ | ---------- |
| SHOWN      | 1      | The window stage is running in the foreground. |
| ACTIVE     | 2      | The window stage gains focus. |
| INACTIVE   | 3      | The window stage loses focus. |
| HIDDEN     | 4      | The window stage is running in the background. |
| RESUMED<sup>11+</sup> | 5      | The window stage is interactive in the foreground. If the user opens the Recents screen when an application is running in the foreground, the application becomes non-interactive. When the user switches back to the application, the application becomes interactive. |
| PAUSED<sup>11+</sup>  | 6      | The window stage is non-interactive in the foreground. If the user opens the Recents screen when an application is running in the foreground, the application becomes non-interactive. When the user switches back to the application, the application becomes interactive. |

## SubWindowOptions<sup>11+</sup>

Describes the parameters used for creating a subwindow.

**System capability**: SystemCapability.Window.SessionManager

| Name     | Type | Read Only | Mandatory | Description        |
| ---------- | ---- | ---- | ---- | ----------- |
| title    | string | No | Yes | Title of the subwindow.      |
| decorEnabled | boolean | No | Yes | Whether decorations are displayed in the subwindow. The value **true** means that decorations are displayed, and **false** means the opposite.      |

## WindowStage<sup>9+</sup>

Implements a window manager, which manages each basic window unit, that is, [Window](#window) instance.

Before calling any of the following APIs, you must use [onWindowStageCreate()](../apis-ability-kit/js-apis-app-ability-uiAbility.md#uiabilityonwindowstagecreate) to create a **WindowStage** instance.

### getMainWindow<sup>9+</sup>

getMainWindow(callback: AsyncCallback&lt;Window&gt;): void

Obtains the main window of this window stage. This API uses an asynchronous callback to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                  | Mandatory | Description                                         |
| -------- | -------------------------------------- | ---- | --------------------------------------------- |
| callback | AsyncCallback&lt;[Window](#window)&gt; | Yes  | Callback used to return the main window. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    windowStage.getMainWindow((err: BusinessError, data) => {
      const errCode: number = err.code;
      if (errCode) {
        console.error('Failed to obtain the main window. Cause: ' + JSON.stringify(err));
        return;
      }
      windowClass = data;
      console.info('Succeeded in obtaining the main window. Data: ' + JSON.stringify(data));
    });
  }
};
```

### getMainWindow<sup>9+</sup>

getMainWindow(): Promise&lt;Window&gt;

Obtains the main window of this window stage. This API uses a promise to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Return value**

| Type                            | Description                                            |
| -------------------------------- | ------------------------------------------------ |
| Promise&lt;[Window](#window)&gt; | Promise used to return the main window. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    let promise = windowStage.getMainWindow();
    promise.then((data) => {
      windowClass = data;
      console.info('Succeeded in obtaining the main window. Data: ' + JSON.stringify(data));
    }).catch((err: BusinessError) => {
      console.error('Failed to obtain the main window. Cause: ' + JSON.stringify(err));
    });
  }
};
```

### getMainWindowSync<sup>9+</sup>

getMainWindowSync(): Window

Obtains the main window of this window stage.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Return value**

| Type | Description |
| ----------------- | --------------------------------- |
| [Window](#window) | return the main window. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    try {
      let windowClass = windowStage.getMainWindowSync();
    } catch (exception) {
      console.error('Failed to obtain the main window. Cause: ' + JSON.stringify(exception));
    }
  }
};
```

### createSubWindow<sup>9+</sup>

createSubWindow(name: string, callback: AsyncCallback&lt;Window&gt;): void

Creates a subwindow for this window stage. This API uses an asynchronous callback to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                  | Mandatory | Description                                         |
| -------- | -------------------------------------- | ---- | --------------------------------------------- |
| name     | string                                 | Yes  | Name of the subwindow.                               |
| callback | AsyncCallback&lt;[Window](#window)&gt; | Yes  | Callback used to return the subwindow. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    try {
      windowStage.createSubWindow('mySubWindow', (err: BusinessError, data) => {
        const errCode: number = err.code;
        if (errCode) {
          console.error('Failed to create the subwindow. Cause: ' + JSON.stringify(err));
          return;
        }
        windowClass = data;
        console.info('Succeeded in creating the subwindow. Data: ' + JSON.stringify(data));
        if (!windowClass) {
          console.info('Failed to load the content. Cause: windowClass is null');
        }
        else {
          (windowClass as window.Window).resize(500, 1000);
        }
      });

    } catch (exception) {
      console.error('Failed to create the subwindow. Cause: ' + JSON.stringify(exception));
    }
  }
};
```

### createSubWindow<sup>9+</sup>

createSubWindow(name: string): Promise&lt;Window&gt;

Creates a subwindow for this window stage. This API uses a promise to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type  | Mandatory | Description          |
| ------ | ------ | ---- | -------------- |
| name   | string | Yes  | Name of the subwindow. |

**Return value**

| Type                            | Description                                            |
| -------------------------------- | ------------------------------------------------ |
| Promise&lt;[Window](#window)&gt; | Promise used to return the subwindow. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    try {
      let promise = windowStage.createSubWindow('mySubWindow');
      promise.then((data) => {
        windowClass = data;
        console.info('Succeeded in creating the subwindow. Data: ' + JSON.stringify(data));
      }).catch((err: BusinessError) => {
        console.error('Failed to create the subwindow. Cause: ' + JSON.stringify(err));
      });
    } catch (exception) {
      console.error('Failed to create the subwindow. Cause: ' + JSON.stringify(exception));
    }
  }
};
```

### createSubWindowWithOptions<sup>11+</sup>

createSubWindowWithOptions(name: string, options: SubWindowOptions): Promise&lt;Window&gt;

Creates a subwindow for this window stage. This API uses a promise to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.Window.SessionManager

**Parameters**

| Name | Type  | Mandatory | Description          |
| ------ | ------ | ---- | -------------- |
| name   | string | Yes  | Name of the subwindow. |
| options  | [SubWindowOptions](#subwindowoptions11) | Yes  |  Parameters used for creating the subwindow. |

**Return value**

| Type                            | Description                                            |
| -------------------------------- | ------------------------------------------------ |
| Promise&lt;[Window](#window)&gt; | Promise used to return the subwindow created. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    let windowClass: window.Window | undefined = undefined;
    try {
      let options : window.SubWindowOptions = {
        title: 'title',
        decorEnabled: true
      };
      let promise = windowStage.createSubWindowWithOptions('mySubWindow', options);
      promise.then((data) => {
        windowClass = data;
        console.info('Succeeded in creating the subwindow. Data: ' + JSON.stringify(data));
      }).catch((err: BusinessError) => {
        console.error('Failed to create the subwindow. Cause: ' + JSON.stringify(err));
      });
    } catch (exception) {
      console.error('Failed to create the subwindow. Cause: ' + JSON.stringify(exception));
    }
  }
};
```

### getSubWindow<sup>9+</sup>

getSubWindow(callback: AsyncCallback&lt;Array&lt;Window&gt;&gt;): void

Obtains all the subwindows of this window stage. This API uses an asynchronous callback to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                               | Mandatory | Description                                             |
| -------- | --------------------------------------------------- | ---- | ------------------------------------------------- |
| callback | AsyncCallback&lt;Array&lt;[Window](#window)&gt;&gt; | Yes  | Callback used to return all the subwindows. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300005 | This window stage is abnormal. |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    let windowClass: window.Window[] = [];
    windowStage.getSubWindow((err: BusinessError, data) => {
      const errCode: number = err.code;
      if (errCode) {
        console.error('Failed to obtain the subwindow. Cause: ' + JSON.stringify(err));
        return;
      }
      windowClass = data;
      console.info('Succeeded in obtaining the subwindow. Data: ' + JSON.stringify(data));
    });
  }
};
```

### getSubWindow<sup>9+</sup>

getSubWindow(): Promise&lt;Array&lt;Window&gt;&gt;

Obtains all the subwindows of this window stage. This API uses a promise to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Return value**

| Type                                         | Description                                                |
| --------------------------------------------- | ---------------------------------------------------- |
| Promise&lt;Array&lt;[Window](#window)&gt;&gt; | Promise used to return all the subwindows. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300005 | This window stage is abnormal. |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    let windowClass: window.Window[] = [];
    let promise = windowStage.getSubWindow();
    promise.then((data) => {
      windowClass = data;
      console.info('Succeeded in obtaining the subwindow. Data: ' + JSON.stringify(data));
    }).catch((err: BusinessError) => {
      console.error('Failed to obtain the subwindow. Cause: ' + JSON.stringify(err));
    })
  }
};
```

### loadContent<sup>9+</sup>

loadContent(path: string, storage: LocalStorage, callback: AsyncCallback&lt;void&gt;): void

Loads the content of a page, with its path in the current project specified, to the main window of this window stage, and transfers the state attribute to the page through a local storage. This API uses an asynchronous callback to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                           | Mandatory | Description                                                        |
| -------- | ----------------------------------------------- | ---- | ------------------------------------------------------------ |
| path     | string                                          | Yes  | Path of the page from which the content will be loaded. The path is configured in the **main_pages.json** file of the project. |
| storage  | [LocalStorage](../../quick-start/arkts-localstorage.md) | Yes  | Page-level UI state storage unit, which is used to transfer the state attribute for the page. |
| callback | AsyncCallback&lt;void&gt;                       | Yes  | Callback used to return the result.                                                  |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  storage: LocalStorage = new LocalStorage();

  onWindowStageCreate(windowStage: window.WindowStage) {
    this.storage.setOrCreate('storageSimpleProp', 121);
    console.log('onWindowStageCreate');
    try {
      windowStage.loadContent('pages/page2', this.storage, (err: BusinessError) => {
        const errCode: number = err.code;
        if (errCode) {
          console.error('Failed to load the content. Cause:' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in loading the content.');
      });
    } catch (exception) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
    }
  }
};
```

### loadContent<sup>9+</sup>

loadContent(path: string, storage?: LocalStorage): Promise&lt;void&gt;

Loads the content of a page, with its path in the current project specified, to the main window of this window stage, and transfers the state attribute to the page through a local storage. This API uses a promise to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type                                           | Mandatory | Description                                                        |
| ------- | ----------------------------------------------- | ---- | ------------------------------------------------------------ |
| path    | string                                          | Yes  | Path of the page from which the content will be loaded. The path is configured in the **main_pages.json** file of the project. |
| storage | [LocalStorage](../../quick-start/arkts-localstorage.md) | No  | Page-level UI state storage unit, which is used to transfer the state attribute for the page. |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  storage: LocalStorage = new LocalStorage();

  onWindowStageCreate(windowStage: window.WindowStage) {
    this.storage.setOrCreate('storageSimpleProp', 121);
    console.log('onWindowStageCreate');
    try {
      let promise = windowStage.loadContent('pages/page2', this.storage);
      promise.then(() => {
        console.info('Succeeded in loading the content.');
      }).catch((err: BusinessError) => {
        console.error('Failed to load the content. Cause:' + JSON.stringify(err));
      });
    } catch (exception) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
    }
    ;
  }
};
```

### loadContent<sup>9+</sup>

loadContent(path: string, callback: AsyncCallback&lt;void&gt;): void

Loads content from a page to this window stage. This API uses an asynchronous callback to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                     | Mandatory | Description                |
| -------- | ------------------------- | ---- | -------------------- |
| path     | string                    | Yes  | Path of the page from which the content will be loaded. The path is configured in the **main_pages.json** file of the project. |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.          |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    try {
      windowStage.loadContent('pages/page2', (err: BusinessError) => {
        const errCode: number = err.code;
        if (errCode) {
          console.error('Failed to load the content. Cause:' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in loading the content.');
      });
    } catch (exception) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
    }
  }
};
```

### loadContentByName<sup>11+</sup>

loadContentByName(name: string, storage: LocalStorage, callback: AsyncCallback&lt;void&gt;): void

Loads the content of a [named route](../../ui/arkts-routing.md#named-route) page to this window stage, and transfers the state attribute to the page through a local storage. This API uses an asynchronous callback to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                                   | Mandatory | Description                                                        |
| -------- | ------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| name     | string                                                  | Yes  | Name of the named route page.                                            |
| storage  | [LocalStorage](../../quick-start/arkts-localstorage.md) | Yes  | Page-level UI state storage unit, which is used to transfer the state attribute for the page. |
| callback | AsyncCallback&lt;void&gt;                               | Yes  | Callback used to return the result.                                                  |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message                                     |
| -------- | --------------------------------------------- |
| 1300002  | This window state is abnormal.                |
| 1300003  | This window manager service works abnormally. |

**Example**

```ts
// ets/entryability/EntryAbility.ets
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';
import * as Index from '../pages/Index'; // Import the named route page.

export default class EntryAbility extends UIAbility {
  // ...

  storage: LocalStorage = new LocalStorage();

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    this.storage.setOrCreate('storageSimpleProp', 121);
    try {
      windowStage.loadContentByName(Index.entryName, this.storage, (err: BusinessError) => {
        const errCode: number = err.code;
        if (errCode) {
          console.error('Failed to load the content. Cause:' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in loading the content.');
      });
    } catch (exception) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
    }
  }
};
```
```ts
// ets/pages/Index.ets
export const entryName : string = 'Index';
@Entry({routeName: entryName, storage : LocalStorage.getShared()})
@Component
export struct Index {
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

### loadContentByName<sup>11+</sup>

loadContentByName(name: string, callback: AsyncCallback&lt;void&gt;): void

Loads the content of a [named route](../../ui/arkts-routing.md#named-route) page to this window stage. This API uses an asynchronous callback to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                     | Mandatory | Description            |
| -------- | ------------------------- | ---- | ---------------- |
| name     | string                    | Yes  | Name of the named route page. |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.      |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message                                     |
| -------- | --------------------------------------------- |
| 1300002  | This window state is abnormal.                |
| 1300003  | This window manager service works abnormally. |

**Example**

```ts
// ets/entryability/EntryAbility.ets
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';
import * as Index from '../pages/Index'; // Import the named route page.

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    try {
      windowStage.loadContentByName(Index.entryName, (err: BusinessError) => {
        const errCode: number = err.code;
        if (errCode) {
          console.error('Failed to load the content. Cause:' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in loading the content.');
      });
    } catch (exception) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
    }
  }
};
```
```ts
// ets/pages/Index.ets
export const entryName : string = 'Index';
@Entry({routeName: entryName})
@Component
export struct Index {
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

### loadContentByName<sup>11+</sup>

loadContentByName(name: string, storage?: LocalStorage): Promise&lt;void&gt;;

Loads the content a [named route](../../ui/arkts-routing.md#named-route) page to this window stage, and transfers the state attribute to the page through a local storage. This API uses a promise to return the result.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name | Type        | Mandatory | Description                                                        |
| ------- | ------------ | ---- | ------------------------------------------------------------ |
| name    | string       | Yes  | Name of the named route page.                                            |
| storage | LocalStorage | No  | Page-level UI state storage unit, which is used to transfer the state attribute for the page. |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message                                     |
| -------- | --------------------------------------------- |
| 1300002  | This window state is abnormal.                |
| 1300003  | This window manager service works abnormally. |

**Example**

```ts
// ets/entryability/EntryAbility.ets
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';
import { BusinessError } from '@ohos.base';
import * as Index from '../pages/Index'; // Import the named route page.

export default class EntryAbility extends UIAbility {
  // ...

  storage: LocalStorage = new LocalStorage();

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    this.storage.setOrCreate('storageSimpleProp', 121);
    try {
      let promise = windowStage.loadContentByName(Index.entryName, this.storage);
      promise.then(() => {
        console.info('Succeeded in loading the content.');
      }).catch((err: BusinessError) => {
        console.error('Failed to load the content. Cause:' + JSON.stringify(err));
      });
    } catch (exception) {
      console.error('Failed to load the content. Cause:' + JSON.stringify(exception));
    }
  }
};
```
```ts
// ets/pages/Index.ets
export const entryName : string = 'Index';
@Entry({routeName: entryName, storage : LocalStorage.getShared()})
@Component
export struct Index {
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

### on('windowStageEvent')<sup>9+</sup>

on(eventType: 'windowStageEvent', callback: Callback&lt;WindowStageEventType&gt;): void

Subscribes to the window stage lifecycle change event.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                                        | Mandatory | Description                                                        |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| eventType  | string                                                       | Yes  | Event type. The value is fixed at **'windowStageEvent'**, indicating the window stage lifecycle change event. |
| callback | Callback&lt;[WindowStageEventType](#windowstageeventtype9)&gt; | Yes  | Callback used to return the window stage lifecycle state.               |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    try {
      windowStage.on('windowStageEvent', (data) => {
        console.info('Succeeded in enabling the listener for window stage event changes. Data: ' +
        JSON.stringify(data));
      });
    } catch (exception) {
      console.error('Failed to enable the listener for window stage event changes. Cause:' +
      JSON.stringify(exception));
    }
  }
};
```

### off('windowStageEvent')<sup>9+</sup>

off(eventType: 'windowStageEvent', callback?: Callback&lt;WindowStageEventType&gt;): void

Unsubscribes from the window stage lifecycle change event.

**Model restriction**: This API can be used only in the stage model.

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Parameters**

| Name  | Type                                                        | Mandatory | Description                                                        |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| eventType  | string                                                       | Yes  | Event type. The value is fixed at **'windowStageEvent'**, indicating the window stage lifecycle change event. |
| callback | Callback&lt;[WindowStageEventType](#windowstageeventtype9)&gt; | No  | Callback used to return the window stage lifecycle state. If a value is passed in, the corresponding subscription is canceled. If no value is passed in, all subscriptions to the specified event are canceled.               |

**Error codes**

For details about the error codes, see [Window Error Codes](errorcode-window.md).

| ID | Error Message |
| ------- | ------------------------------ |
| 1300002 | This window state is abnormal. |
| 1300005 | This window stage is abnormal. |

**Example**

```ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';

export default class EntryAbility extends UIAbility {
  // ...

  onWindowStageCreate(windowStage: window.WindowStage) {
    console.log('onWindowStageCreate');
    try {
      windowStage.off('windowStageEvent');
    } catch (exception) {
      console.error('Failed to disable the listener for window stage event changes. Cause:' +
      JSON.stringify(exception));
    }
  }
};
```
