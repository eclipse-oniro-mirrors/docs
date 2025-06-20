# Window Subsystem Changelog

## cl.window.1 Changed the Return Values of getWindowStatus and on('windowStatusChange') on 2-in-1 Devices When the Window Is Maximized

**Access Level**

Public API

**Reason for Change**

When the window is maximized, the **getWindowStatus** and **on('windowStatusChange')** APIs return **WindowStatusType::FULL_SCREEN**.

The application cannot tell whether the window is in the maximized state or full-screen mode on 2-in-1 devices from the return values.

**Change Impact**

This change is a non-compatible change.

Before change: When **getWindowStatus** and **on('windowStatusChange')** are called on 2-in-1 devices, the return value is **WindowStatusType::FULL_SCREEN** when the window is maximized.

After change: When **getWindowStatus** and **on('windowStatusChange')** are called on 2-in-1 devices, the return value is **WindowStatusType::MAXIMIZE** when the window is maximized.

**Start API Level**

11 for **on('windowStatusChange')**

12 for **getWindowStatus interface** on 2-in-1 devices

**Change Since**

OpenHarmony SDK 5.0.1.45

**Key API/Component Changes**

@ohos.window.d.ts

System capability: SystemCapability.Window.SessionManager

APIs: getWindowStatus and on('windowStatusChange')

**Adaptation Guide**

To distinguish whether the window is maximized or in full-screen mode on 2-in-1 devices, implement as follows:

- In API version 13 and earlier, in the case that **WindowStatusType::FULL_SCREEN** is returned, call [getImmersiveModeEnabledState()](../../../application-dev/reference/apis-arkui/js-apis-window.md#getimmersivemodeenabledstate12). If **true** is returned, the window is in full-screen mode. If **false** is returned, the window is maximized.

- In API version 14 and later, you can directly call **getWindowStatus** and **on('windowStatusChange')** to distinguish the maximized state from full-screen mode.

  However, you must adjust the code to match the return value. If the same code logic is used for **WindowStatusType::FULL_SCREEN** and **WindowStatusType::MAXIMIZE**, just append a check for **WindowStatusType::MAXIMIZE** (using a logical OR) within the existing logic. If different logic is used for **WindowStatusType::FULL_SCREEN** and **WindowStatusType::MAXIMIZE**, you must introduce a separate condition for **WindowStatusType::MAXIMIZE** to manage the window maximization logic.

The following example uses the **on('windowStatusChange')** API as an example to describe how to distinguish the maximized state and full-screen mode on 2-in-1 devices.

```ts
// API version 13 and earlier versions
// EntryAbility.ets
import { BusinessError } from '@kit.BasicServicesKit';

export default class EntryAbility extends UIAbility {
  // ...
  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    try {
      let windowClass = windowStage.getMainWindowSync();
      windowClass?.on("windowStatusChange", (windowStatusType: window.WindowStatusType) => {
        if (windowStatusType == window.WindowStatusType.FULL_SCREEN) {
          // If isFullScreen is true, the window is in full-screen mode; if it is false, the window is maximized.
          let isFullScreen: boolean = windowClass.getImmersiveModeEnabledState();
        } else {
          // ...
        }
      })
    } catch (exception) {
      console.error(`Failed to obtain the main window. Cause code: ${exception.code}, message: ${exception.message}`);
    }
  }
}
```

```ts
// API version 14 or later
// EntryAbility.ets
import { BusinessError } from '@kit.BasicServicesKit';

export default class EntryAbility extends UIAbility {
  // ...
  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    try {
      let windowClass = windowStage.getMainWindowSync();
      windowClass?.on("windowStatusChange", (windowStatusType: window.WindowStatusType) => {
        // Different logic is used for the full-screen mode and maximized state. Add a separate condition for window.WindowStatusType.MAXIMIZE.
        if (windowStatusType == window.WindowStatusType.FULL_SCREEN) {
          // ....
        } else if (windowStatusType == window.WindowStatusType.MAXIMIZE) {
          // ...
        } else {
          // ...
        }
      })
    } catch (exception) {
      console.error(`Failed to obtain the main window. Cause code: ${exception.code}, message: ${exception.message}`);
    }
  }
}
```

```ts
// API version 14 or later
// EntryAbility.ets
import { BusinessError } from '@kit.BasicServicesKit';

export default class EntryAbility extends UIAbility {
  // ...
  onWindowStageCreate(windowStage: window.WindowStage) {
    console.info('onWindowStageCreate');
    try {
      let windowClass = windowStage.getMainWindowSync();
      windowClass?.on("windowStatusChange", (windowStatusType: window.WindowStatusType) => {
        // The same logic is used for the full-screen mode and maximized state. Add a check using OR for window.WindowStatusType.MAXIMIZE.
        if (windowStatusType == window.WindowStatusType.FULL_SCREEN ||
            windowStatusType == window.WindowStatusType.MAXIMIZE) {
          // ....
        } else {
          // ...
        }
      })
    } catch (exception) {
      console.error(`Failed to obtain the main window. Cause code: ${exception.code}, message: ${exception.message}`);
    }
  }
}
```
