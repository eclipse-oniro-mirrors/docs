# oh_display_info.h


## Overview

The **oh_display_info.h** file declares the common enums and definitions of the display.

**File to include**: &lt;window_manager/oh_display_info.h&gt;

**Library**: libnative_display_manager.so

**System capability**: SystemCapability.WindowManager.WindowManager.Core

**Since**: 12

**Related module**: [OH_DisplayManager](_o_h___display_manager.md)


## Summary


### Structs

| Name| Description| 
| -------- | -------- |
| struct  [NativeDisplayManager_Rect](_native_display_manager___rect.md) | Describes a rectangle.| 
| struct  [NativeDisplayManager_WaterfallDisplayAreaRects](ive_display_manager___waterfall_display_area_rects.md) | Describes the curved area on a waterfall display.| 
| struct  [NativeDisplayManager_CutoutInfo](_native_display_manager___cutout_info.md) | Describes the unusable area of a display, including punch hole, notch, and curved area of a waterfall display.| 
| struct  [NativeDisplayManager_DisplayHdrFormat](_native_display_manager___display_hdr_format.md) | Encapsulates all the HDR formats supported by a display.| 
| struct  [NativeDisplayManager_DisplayColorSpace](_native_display_manager___display_color_space.md) | Encapsulates all the color spaces supported by a display.| 
| struct  [NativeDisplayManager_DisplayInfo](_native_display_manager___display_info.md) | Encapsulates the information about a display.| 
| struct  [NativeDisplayManager_DisplaysInfo](_native_display_manager___displays_info.md) | Encapsulates the information about displays of a device with multiple screens.| 


### Types

| Name| Description| 
| -------- | -------- |
| typedef enum [NativeDisplayManager_Rotation](_o_h___display_manager.md#nativedisplaymanager_rotation) [NativeDisplayManager_Rotation](_o_h___display_manager.md#nativedisplaymanager_rotation) | Defines an enum for the clockwise rotation angles of a display.| 
| typedef enum [NativeDisplayManager_Orientation](_o_h___display_manager.md#nativedisplaymanager_orientation) [NativeDisplayManager_Orientation](_o_h___display_manager.md#nativedisplaymanager_orientation) | Defines an enum for the orientations of a display.| 
| typedef enum [NativeDisplayManager_ErrorCode](_o_h___display_manager.md#nativedisplaymanager_errorcode) [NativeDisplayManager_ErrorCode](_o_h___display_manager.md#nativedisplaymanager_errorcode) | Defines an enum for the status codes returned by the display manager interface.| 
| typedef enum [NativeDisplayManager_FoldDisplayMode](_o_h___display_manager.md#nativedisplaymanager_folddisplaymode) [NativeDisplayManager_FoldDisplayMode](_o_h___display_manager.md#nativedisplaymanager_folddisplaymode) | Defines an enum for the display modes of a foldable device.| 
| typedef struct [NativeDisplayManager_Rect](_native_display_manager___rect.md) [NativeDisplayManager_Rect](_o_h___display_manager.md#nativedisplaymanager_rect) | Defines a struct for a rectangle.| 
| typedef struct [NativeDisplayManager_WaterfallDisplayAreaRects](ive_display_manager___waterfall_display_area_rects.md) [NativeDisplayManager_WaterfallDisplayAreaRects](_o_h___display_manager.md#nativedisplaymanager_waterfalldisplayarearects) | Defines a struct for the curved area on a waterfall display.| 
| typedef struct [NativeDisplayManager_CutoutInfo](_native_display_manager___cutout_info.md) [NativeDisplayManager_CutoutInfo](_o_h___display_manager.md#nativedisplaymanager_cutoutinfo) | Defines a struct for the unusable area of a display, including punch hole, notch, and curved area of a waterfall display.| 
| typedef enum [NativeDisplayManager_DisplayState](_o_h___display_manager.md#nativedisplaymanager_displaystate) [NativeDisplayManager_DisplayState](_o_h___display_manager.md#nativedisplaymanager_displaystate) | Defines an enum for the states of a display.| 
| typedef struct [NativeDisplayManager_DisplayHdrFormat](_native_display_manager___display_hdr_format.md) [NativeDisplayManager_DisplayHdrFormat](_o_h___display_manager.md#nativedisplaymanager_displayhdrformat) | Defines a struct that encapsulates all the HDR formats supported by a display.| 
| typedef struct [NativeDisplayManager_DisplayColorSpace](_native_display_manager___display_color_space.md) [NativeDisplayManager_DisplayColorSpace](_o_h___display_manager.md#nativedisplaymanager_displaycolorspace) | Defines a struct that encapsulates all the color spaces supported by a display.| 
| typedef struct [NativeDisplayManager_DisplayInfo](_native_display_manager___display_info.md) [NativeDisplayManager_DisplayInfo](_o_h___display_manager.md#nativedisplaymanager_displayinfo) | Defines a struct that encapsulates the information about a display.| 
| typedef struct [NativeDisplayManager_DisplaysInfo](_native_display_manager___displays_info.md) [NativeDisplayManager_DisplaysInfo](_o_h___display_manager.md#nativedisplaymanager_displaysinfo) | Defines a struct that encapsulates the information about displays of a device with multiple screens.| 


### Enums

| Name| Description| 
| -------- | -------- |
| [NativeDisplayManager_Rotation](_o_h___display_manager.md#nativedisplaymanager_rotation-1) { DISPLAY_MANAGER_ROTATION_0 = 0, DISPLAY_MANAGER_ROTATION_90 = 1, DISPLAY_MANAGER_ROTATION_180 = 2, DISPLAY_MANAGER_ROTATION_270 = 3 } | Enumerates the clockwise rotation angles of a display.| 
| [NativeDisplayManager_Orientation](_o_h___display_manager.md#nativedisplaymanager_orientation-1) {<br>DISPLAY_MANAGER_PORTRAIT = 0, DISPLAY_MANAGER_LANDSCAPE = 1, DISPLAY_MANAGER_PORTRAIT_INVERTED = 2, DISPLAY_MANAGER_LANDSCAPE_INVERTED = 3,<br>DISPLAY_MANAGER_UNKNOWN<br>} | Enumerates the orientations of a display.| 
| [NativeDisplayManager_ErrorCode](_o_h___display_manager.md#nativedisplaymanager_errorcode-1) {<br>DISPLAY_MANAGER_OK = 0, DISPLAY_MANAGER_ERROR_NO_PERMISSION = 201, DISPLAY_MANAGER_ERROR_NOT_SYSTEM_APP = 202, DISPLAY_MANAGER_ERROR_INVALID_PARAM = 401,<br>DISPLAY_MANAGER_ERROR_DEVICE_NOT_SUPPORTED = 801, DISPLAY_MANAGER_ERROR_INVALID_SCREEN = 1400001, DISPLAY_MANAGER_ERROR_INVALID_CALL = 1400002, DISPLAY_MANAGER_ERROR_SYSTEM_ABNORMAL = 1400003<br>} | Enumerates the status codes returned by the display manager interface.| 
| [NativeDisplayManager_FoldDisplayMode](_o_h___display_manager.md#nativedisplaymanager_folddisplaymode-1) {<br>DISPLAY_MANAGER_FOLD_DISPLAY_MODE_UNKNOWN = 0, DISPLAY_MANAGER_FOLD_DISPLAY_MODE_FULL = 1, DISPLAY_MANAGER_FOLD_DISPLAY_MODE_MAIN = 2, DISPLAY_MANAGER_FOLD_DISPLAY_MODE_SUB = 3,<br>DISPLAY_MANAGER_FOLD_DISPLAY_MODE_COORDINATION = 4<br>} | Enumerates the display modes of a foldable device.| 
| [NativeDisplayManager_DisplayState](_o_h___display_manager.md#nativedisplaymanager_displaystate-1) {<br>DISPLAY_MANAGER_DISPLAY_STATE_UNKNOWN = 0, DISPLAY_MANAGER_DISPLAY_STATE_OFF = 1, DISPLAY_MANAGER_DISPLAY_STATE_ON = 2, DISPLAY_MANAGER_DISPLAY_STATE_DOZE = 3,<br>DISPLAY_MANAGER_DISPLAY_STATE_DOZE_SUSPEND = 4, DISPLAY_MANAGER_DISPLAY_STATE_VR = 5, DISPLAY_MANAGER_DISPLAY_STATE_ON_SUSPEND = 6<br>} | Enumerates the states of a display.| 
