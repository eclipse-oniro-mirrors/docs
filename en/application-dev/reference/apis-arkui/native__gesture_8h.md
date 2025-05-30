# native_gesture.h


## Overview

Declares the APIs of **NativeGesture**.

**Library**: libace_ndk.z.so

**File to include**: <arkui/native_gesture.h>

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Since**: 12

**Related module**: [ArkUI_NativeModule](_ark_u_i___native_module.md)


## Summary


### Structs

| Name| Description| 
| -------- | -------- |
| struct  [ArkUI_NativeGestureAPI_1](_ark_u_i___native_gesture_a_p_i__1.md) | Defines a struct for the gesture APIs. | 
| struct  [ArkUI_NativeGestureAPI_2](_ark_u_i___native_gesture_a_p_i__2.md) | Defines a struct for the gesture APIs.|


### Types

| Name| Description| 
| -------- | -------- |
| typedef uint32_t [ArkUI_GestureEventActionTypeMask](_ark_u_i___native_module.md#arkui_gestureeventactiontypemask) | Defines a set of gesture event types. | 
| typedef uint32_t [ArkUI_GestureDirectionMask](_ark_u_i___native_module.md#arkui_gesturedirectionmask) | Defines a set of gesture directions. | 
| typedef ArkUI_GestureRecognizer \* [ArkUI_GestureRecognizerHandle](_ark_u_i___native_module.md#arkui_gesturerecognizerhandle) | Defines the gesture recognizer handle. | 
| typedef [ArkUI_GestureRecognizerHandle](_ark_u_i___native_module.md#arkui_gesturerecognizerhandle) \* [ArkUI_GestureRecognizerHandleArray](_ark_u_i___native_module.md#arkui_gesturerecognizerhandlearray) | Defines the gesture recognizer handle array. | 
| typedef ArkUI_TouchRecognizer \* [ArkUI_TouchRecognizerHandle](_ark_u_i___native_module.md#arkui_touchrecognizerhandle) | Defines the gesture recognizer handle. | 
| typedef [ArkUI_TouchRecognizerHandle](_ark_u_i___native_module.md#arkui_touchrecognizerhandle) \* [ArkUI_TouchRecognizerHandleArray](_ark_u_i___native_module.md#arkui_touchrecognizerhandlearray) | Defines an array of gesture recognizer handles. | 
| typedef struct [ArkUI_GestureEventTargetInfo](_ark_u_i___native_module.md#arkui_gestureeventtargetinfo) [ArkUI_GestureEventTargetInfo](_ark_u_i___native_module.md#arkui_gestureeventtargetinfo) | Defines a **GestureEventTargetInfo** object that provides information about a gesture event target. | 
| typedef struct [ArkUI_ParallelInnerGestureEvent](_ark_u_i___native_module.md#arkui_parallelinnergestureevent) [ArkUI_ParallelInnerGestureEvent](_ark_u_i___native_module.md#arkui_parallelinnergestureevent) | Defines a parallel internal gesture event. | 
| typedef struct [ArkUI_GestureInterruptInfo](_ark_u_i___native_module.md#arkui_gestureinterruptinfo) [ArkUI_GestureInterruptInfo](_ark_u_i___native_module.md#arkui_gestureinterruptinfo) | Obtains the custom data from a gesture interruption event.|
| typedef void(\* [ArkUI_GestureRecognizerDestructNotifyCallback](_ark_u_i___native_module.md#arkui_gesturerecognizerdestructnotifycallback)) (ArkUI_GestureRecognizer \*recognizer, void \*userData) | Defines a callback function for notifying gesture recognizer destruction. | 


### Enums

| Name| Description| 
| -------- | -------- |
| [ArkUI_GestureEventActionType](_ark_u_i___native_module.md#arkui_gestureeventactiontype) { [GESTURE_EVENT_ACTION_ACCEPT](_ark_u_i___native_module.md) = 0x01, [GESTURE_EVENT_ACTION_UPDATE](_ark_u_i___native_module.md) = 0x02, [GESTURE_EVENT_ACTION_END](_ark_u_i___native_module.md) = 0x04, [GESTURE_EVENT_ACTION_CANCEL](_ark_u_i___native_module.md) = 0x08 } | Enumerates gesture event types. | 
| [ArkUI_GesturePriority](_ark_u_i___native_module.md#arkui_gesturepriority) { [NORMAL](_ark_u_i___native_module.md) = 0, [PRIORITY](_ark_u_i___native_module.md) = 1, [PARALLEL](_ark_u_i___native_module.md) = 2 } | Enumerates gesture event modes. | 
| [ArkUI_GroupGestureMode](_ark_u_i___native_module.md#arkui_groupgesturemode) { [SEQUENTIAL_GROUP](_ark_u_i___native_module.md) = 0, [PARALLEL_GROUP](_ark_u_i___native_module.md) = 1, [EXCLUSIVE_GROUP](_ark_u_i___native_module.md) = 2 } | Enumerates gesture group modes. | 
| [ArkUI_GestureDirection](_ark_u_i___native_module.md#arkui_gesturedirection) {<br>[GESTURE_DIRECTION_ALL](_ark_u_i___native_module.md) = 0b1111, [GESTURE_DIRECTION_HORIZONTAL](_ark_u_i___native_module.md) = 0b0011, [GESTURE_DIRECTION_VERTICAL](_ark_u_i___native_module.md) = 0b1100, [GESTURE_DIRECTION_LEFT](_ark_u_i___native_module.md) = 0b0001,<br>[GESTURE_DIRECTION_RIGHT](_ark_u_i___native_module.md) = 0b0010, [GESTURE_DIRECTION_UP](_ark_u_i___native_module.md) = 0b0100, [GESTURE_DIRECTION_DOWN](_ark_u_i___native_module.md) = 0b1000, [GESTURE_DIRECTION_NONE](_ark_u_i___native_module.md) = 0<br>} | Enumerates gesture directions. | 
| [ArkUI_GestureMask](_ark_u_i___native_module.md#arkui_gesturemask) { [NORMAL_GESTURE_MASK](_ark_u_i___native_module.md) = 0, [IGNORE_INTERNAL_GESTURE_MASK](_ark_u_i___native_module.md) } | Enumerates gesture masking modes. | 
| [ArkUI_GestureRecognizerType](_ark_u_i___native_module.md#arkui_gesturerecognizertype) {<br>[TAP_GESTURE](_ark_u_i___native_module.md) = 0, [LONG_PRESS_GESTURE](_ark_u_i___native_module.md), [PAN_GESTURE](_ark_u_i___native_module.md), [PINCH_GESTURE](_ark_u_i___native_module.md),<br>[ROTATION_GESTURE](_ark_u_i___native_module.md), [SWIPE_GESTURE](_ark_u_i___native_module.md), [GROUP_GESTURE](_ark_u_i___native_module.md)<br>} | Enumerates gesture recognizer types. | 
| [ArkUI_GestureInterruptResult](_ark_u_i___native_module.md#arkui_gestureinterruptresult) { [GESTURE_INTERRUPT_RESULT_CONTINUE](_ark_u_i___native_module.md) = 0, [GESTURE_INTERRUPT_RESULT_REJECT](_ark_u_i___native_module.md) } | Enumerates gesture interruption results. | 
| [ArkUI_GestureRecognizerState](_ark_u_i___native_module.md#arkui_gesturerecognizerstate) {<br>[ARKUI_GESTURE_RECOGNIZER_STATE_REDAY](_ark_u_i___native_module.md) = 0, [ARKUI_GESTURE_RECOGNIZER_STATE_DETECTING](_ark_u_i___native_module.md) = 1, [ARKUI_GESTURE_RECOGNIZER_STATE_PENDING](_ark_u_i___native_module.md) = 2, [ARKUI_GESTURE_RECOGNIZER_STATE_BLOCKED](_ark_u_i___native_module.md) = 3,<br>[ARKUI_GESTURE_RECOGNIZER_STATE_SUCCESSFUL](_ark_u_i___native_module.md) = 4, [ARKUI_GESTURE_RECOGNIZER_STATE_FAILED](_ark_u_i___native_module.md) = 5<br>} | Enumerates the gesture recognizer states. | 


### Functions

| Name| Description| 
| -------- | -------- |
| bool [OH_ArkUI_GestureInterruptInfo_GetSystemFlag](_ark_u_i___native_module.md#oh_arkui_gestureinterruptinfo_getsystemflag) (const ArkUI_GestureInterruptInfo \*event) | Checks whether a gesture is a built-in gesture of the component. | 
| ArkUI_GestureRecognizer \* [OH_ArkUI_GestureInterruptInfo_GetRecognizer](_ark_u_i___native_module.md#oh_arkui_gestureinterruptinfo_getrecognizer) (const ArkUI_GestureInterruptInfo \*event) | Returns the pointer to interrupted gesture recognizer. | 
| ArkUI_GestureEvent \* [OH_ArkUI_GestureInterruptInfo_GetGestureEvent](_ark_u_i___native_module.md#oh_arkui_gestureinterruptinfo_getgestureevent) (const ArkUI_GestureInterruptInfo \*event) | Obtains the pointer to the interrupted gesture event. | 
| int32_t [OH_ArkUI_GestureInterruptInfo_GetSystemRecognizerType](_ark_u_i___native_module.md#oh_arkui_gestureinterruptinfo_getsystemrecognizertype) (const ArkUI_GestureInterruptInfo \*event) | Obtains the type of the system gesture to trigger. | 
| int32_t [OH_ArkUI_GestureInterruptInfo_GetTouchRecognizers](_ark_u_i___native_module.md#oh_arkui_gestureinterruptinfo_gettouchrecognizers) (const ArkUI_GestureInterruptInfo\* info, ArkUI_TouchRecognizerHandleArray\* recognizers, int32_t\* size) | Obtains touch recognizers from gesture interruption information. | 
| int32_t [OH_ArkUI_TouchRecognizer_GetNodeHandle](_ark_u_i___native_module.md#oh_arkui_touchrecognizer_getnodehandle) (const ArkUI_TouchRecognizerHandle recognizer) | Obtains the component handle corresponding to a touch recognizer. |
| int32_t [OH_ArkUI_TouchRecognizer_CancelTouch](_ark_u_i___native_module.md#oh_arkui_touchrecognizer_canceltouch) (ArkUI_TouchRecognizerHandle recognizer, ArkUI_GestureInterruptInfo\* info) | Sends a cancel touch event to a touch recognizer in a gesture interruption callback. |
| [ArkUI_GestureEventActionType](_ark_u_i___native_module.md#arkui_gestureeventactiontype) [OH_ArkUI_GestureEvent_GetActionType](_ark_u_i___native_module.md#oh_arkui_gestureevent_getactiontype) (const ArkUI_GestureEvent \*event) | Obtains the gesture event type. | 
| [ArkUI_NodeHandle](_ark_u_i___native_module.md#arkui_nodehandle) [OH_ArkUI_GestureEvent_GetResponseNode](_ark_u_i___native_module.md#oh_arkui_gestureevent_getresponsenode) (ArkUI_GestureEvent \*event) | Obtains the node that responds to the gesture. | 
| const [ArkUI_UIInputEvent](_ark_u_i___event_module.md#arkui_uiinputevent) \* [OH_ArkUI_GestureEvent_GetRawInputEvent](_ark_u_i___native_module.md#oh_arkui_gestureevent_getrawinputevent) (const ArkUI_GestureEvent \*event) | Obtains gesture input. | 
| int32_t [OH_ArkUI_LongPress_GetRepeatCount](_ark_u_i___native_module.md#oh_arkui_longpress_getrepeatcount) (const ArkUI_GestureEvent \*event) | Obtains the number of times that a long press gesture is triggered periodically. | 
| float [OH_ArkUI_PanGesture_GetVelocity](_ark_u_i___native_module.md#oh_arkui_pangesture_getvelocity) (const ArkUI_GestureEvent \*event) | Obtains the velocity of a pan gesture along the main axis. | 
| float [OH_ArkUI_PanGesture_GetVelocityX](_ark_u_i___native_module.md#oh_arkui_pangesture_getvelocityx) (const ArkUI_GestureEvent \*event) | Obtains the velocity of a pan gesture along the x-axis. | 
| float [OH_ArkUI_PanGesture_GetVelocityY](_ark_u_i___native_module.md#oh_arkui_pangesture_getvelocityy) (const ArkUI_GestureEvent \*event) | Obtains the velocity of a pan gesture along the y-axis. | 
| float [OH_ArkUI_PanGesture_GetOffsetX](_ark_u_i___native_module.md#oh_arkui_pangesture_getoffsetx) (const ArkUI_GestureEvent \*event) | Obtains the relative offset of a pan gesture along the x-axis. | 
| float [OH_ArkUI_PanGesture_GetOffsetY](_ark_u_i___native_module.md#oh_arkui_pangesture_getoffsety) (const ArkUI_GestureEvent \*event) | Obtains the relative offset of a pan gesture along the y-axis. | 
| float [OH_ArkUI_SwipeGesture_GetAngle](_ark_u_i___native_module.md#oh_arkui_swipegesture_getangle) (const ArkUI_GestureEvent \*event) | Obtains the angle information of the swipe gesture. | 
| float [OH_ArkUI_SwipeGesture_GetVelocity](_ark_u_i___native_module.md#oh_arkui_swipegesture_getvelocity) (const ArkUI_GestureEvent \*event) | Obtains the average velocity of all fingers used in the swipe gesture. | 
| float [OH_ArkUI_RotationGesture_GetAngle](_ark_u_i___native_module.md#oh_arkui_rotationgesture_getangle) (const ArkUI_GestureEvent \*event) | Obtains the angle information of a rotation gesture. | 
| float [OH_ArkUI_PinchGesture_GetScale](_ark_u_i___native_module.md#oh_arkui_pinchgesture_getscale) (const ArkUI_GestureEvent \*event) | Obtains the scale ratio of a pinch gesture. | 
| float [OH_ArkUI_PinchGesture_GetCenterX](_ark_u_i___native_module.md#oh_arkui_pinchgesture_getcenterx) (const ArkUI_GestureEvent \*event) | Obtains the X coordinate of the center of the pinch gesture, in vp, relative to the upper left corner of the current component. | 
| float [OH_ArkUI_PinchGesture_GetCenterY](_ark_u_i___native_module.md#oh_arkui_pinchgesture_getcentery) (const ArkUI_GestureEvent \*event) | Obtains the Y coordinate of the center of the pinch gesture, in vp, relative to the upper left corner of the current component. | 
| [ArkUI_NodeHandle](_ark_u_i___native_module.md#arkui_nodehandle) [OH_ArkUI_GestureEvent_GetNode](_ark_u_i___native_module.md#oh_arkui_gestureevent_getnode) (const ArkUI_GestureEvent \*event) | Obtains the ArkUI component to which the gesture is bound. | 
| int32_t [OH_ArkUI_GetResponseRecognizersFromInterruptInfo](_ark_u_i___native_module.md#oh_arkui_getresponserecognizersfrominterruptinfo) (const ArkUI_GestureInterruptInfo \*event, [ArkUI_GestureRecognizerHandleArray](_ark_u_i___native_module.md#arkui_gesturerecognizerhandlearray) \*responseChain, int32_t \*count) | Obtains information about a gesture response chain. | 
| int32_t [OH_ArkUI_SetGestureRecognizerEnabled](_ark_u_i___native_module.md#oh_arkui_setgesturerecognizerenabled) (ArkUI_GestureRecognizer \*recognizer, bool enabled) | Sets the enabled state of a gesture recognizer. | 
| int32_t(\* [OH_ArkUI_SetGestureRecognizerLimitFingerCount](_ark_u_i___native_module.md#oh_arkui_setgesturerecognizerlimitfingercount) )(ArkUI_GestureRecognizer \*recognizer, bool limitFingerCount) | Sets whether to check the number of fingers touching the screen. | 
| bool [OH_ArkUI_GetGestureRecognizerEnabled](_ark_u_i___native_module.md#oh_arkui_getgesturerecognizerenabled) (ArkUI_GestureRecognizer \*recognizer) | Obtains the enabled state of a gesture recognizer. | 
| int32_t [OH_ArkUI_GetGestureRecognizerState](_ark_u_i___native_module.md#oh_arkui_getgesturerecognizerstate) (ArkUI_GestureRecognizer \*recognizer, [ArkUI_GestureRecognizerState](_ark_u_i___native_module.md#arkui_gesturerecognizerstate) \*state) | Obtains the state of a gesture recognizer. | 
| int32_t [OH_ArkUI_GetGestureEventTargetInfo](_ark_u_i___native_module.md#oh_arkui_getgestureeventtargetinfo) (ArkUI_GestureRecognizer \*recognizer, [ArkUI_GestureEventTargetInfo](_ark_u_i___native_module.md#arkui_gestureeventtargetinfo) \*\*info) | Obtains the information about a gesture event target. | 
| int32_t [OH_ArkUI_GestureEventTargetInfo_IsScrollBegin](_ark_u_i___native_module.md#oh_arkui_gestureeventtargetinfo_isscrollbegin) ([ArkUI_GestureEventTargetInfo](_ark_u_i___native_module.md#arkui_gestureeventtargetinfo) \*info, bool \*ret) | Obtains whether this scroll container is scrolled to the top. | 
| int32_t [OH_ArkUI_GestureEventTargetInfo_IsScrollEnd](_ark_u_i___native_module.md#oh_arkui_gestureeventtargetinfo_isscrollend) ([ArkUI_GestureEventTargetInfo](_ark_u_i___native_module.md#arkui_gestureeventtargetinfo) \*info, bool \*ret) | Obtains whether this scroll container is scrolled to the bottom. | 
| int32_t [OH_ArkUI_GetPanGestureDirectionMask](_ark_u_i___native_module.md#oh_arkui_getpangesturedirectionmask) (ArkUI_GestureRecognizer \*recognizer, [ArkUI_GestureDirectionMask](_ark_u_i___native_module.md#arkui_gesturedirectionmask) \*directionMask) | Obtains the direction of a pan gesture. | 
| bool [OH_ArkUI_IsBuiltInGesture](_ark_u_i___native_module.md#oh_arkui_isbuiltingesture) (ArkUI_GestureRecognizer \*recognizer) | Obtains whether a gesture is a built-in gesture. | 
| int32_t [OH_ArkUI_GetGestureTag](_ark_u_i___native_module.md#oh_arkui_getgesturetag) (ArkUI_GestureRecognizer \*recognizer, char \*buffer, int32_t bufferSize, int32_t \*result) | Obtains the tag of a gesture recognizer. | 
| int32_t [OH_ArkUI_GetGestureBindNodeId](_ark_u_i___native_module.md#oh_arkui_getgesturebindnodeid) (ArkUI_GestureRecognizer \*recognizer, char \*nodeId, int32_t size, int32_t \*result) | Obtains the ID of the component linked to a gesture recognizer. | 
| bool [OH_ArkUI_IsGestureRecognizerValid](_ark_u_i___native_module.md#oh_arkui_isgesturerecognizervalid) (ArkUI_GestureRecognizer \*recognizer) | Obtains whether a gesture recognizer is valid. | 
| void \* [OH_ArkUI_ParallelInnerGestureEvent_GetUserData](_ark_u_i___native_module.md#oh_arkui_parallelinnergestureevent_getuserdata) ([ArkUI_ParallelInnerGestureEvent](_ark_u_i___native_module.md#arkui_parallelinnergestureevent) \*event) | Obtains custom data in the parallel internal gesture event. | 
| void* [OH_ArkUI_GestureInterrupter_GetUserData](_ark_u_i___native_module.md#oh_arkui_gestureinterrupter_getuserdata)([ArkUI_GestureInterruptInfo](_ark_u_i___native_module.md#arkui_gestureinterruptinfo)* event) | Obtains the custom data from a gesture interruption event.|
| ArkUI_GestureRecognizer \* [OH_ArkUI_ParallelInnerGestureEvent_GetCurrentRecognizer](_ark_u_i___native_module.md#oh_arkui_parallelinnergestureevent_getcurrentrecognizer) ([ArkUI_ParallelInnerGestureEvent](_ark_u_i___native_module.md#arkui_parallelinnergestureevent) \*event) | Obtains the current gesture recognizer in a parallel internal gesture event. | 
| int32_t [OH_ArkUI_ParallelInnerGestureEvent_GetConflictRecognizers](_ark_u_i___native_module.md#oh_arkui_parallelinnergestureevent_getconflictrecognizers) ([ArkUI_ParallelInnerGestureEvent](_ark_u_i___native_module.md#arkui_parallelinnergestureevent) \*event, [ArkUI_GestureRecognizerHandleArray](_ark_u_i___native_module.md#arkui_gesturerecognizerhandlearray) \*array, int32_t \*size) | Obtains the conflicting gesture recognizers in a parallel internal gesture event. | 
| int32_t [OH_ArkUI_SetArkUIGestureRecognizerDisposeNotify](_ark_u_i___native_module.md#oh_arkui_setarkuigesturerecognizerdisposenotify) (ArkUI_GestureRecognizer \*recognizer, [ArkUI_GestureRecognizerDestructNotifyCallback](_ark_u_i___native_module.md#arkui_gesturerecognizerdestructnotifycallback) callback, void \*userData) | Sets a callback function for notifying gesture recognizer destruction. | 
| int32_t [OH_ArkUI_GetGestureParam_DirectMask](_ark_u_i___native_module.md#oh_arkui_getgestureparam_directmask) (ArkUI_GestureRecognizer \*recognizer, [ArkUI_GestureDirectionMask](_ark_u_i___native_module.md#arkui_gesturedirectionmask) \*directMask) | Obtains the swipe direction of a gesture recognizer. | 
| int32_t [OH_ArkUI_GetGestureParam_FingerCount](_ark_u_i___native_module.md#oh_arkui_getgestureparam_fingercount) (ArkUI_GestureRecognizer \*recognizer, int \*finger) | Obtains the number of fingers used by a gesture recognizer. | 
| int32_t [OH_ArkUI_GetGestureParam_limitFingerCount](_ark_u_i___native_module.md#oh_arkui_getgestureparam_limitfingercount) (ArkUI_GestureRecognizer \*recognizer, bool \*isLimited) | Checks whether a gesture recognizer has a finger count limit. | 
| int32_t [OH_ArkUI_GetGestureParam_repeat](_ark_u_i___native_module.md#oh_arkui_getgestureparam_repeat) (ArkUI_GestureRecognizer \*recognizer, bool \*isRepeat) | Checks whether a gesture recognizer supports repeated event callbacks. | 
| int32_t [OH_ArkUI_GetGestureParam_distance](_ark_u_i___native_module.md#oh_arkui_getgestureparam_distance) (ArkUI_GestureRecognizer \*recognizer, double \*distance) | Obtains the allowed movement distance range for a gesture recognizer. | 
| int32_t [OH_ArkUI_GetGestureParam_speed](_ark_u_i___native_module.md#oh_arkui_getgestureparam_speed) (ArkUI_GestureRecognizer \*recognizer, double \*speed) | Obtains the minimum swipe speed recognized by a gesture recognizer. | 
| int32_t [OH_ArkUI_GetGestureParam_duration](_ark_u_i___native_module.md#oh_arkui_getgestureparam_duration) (ArkUI_GestureRecognizer \*recognizer, int \*duration) | Obtains the minimum duration required to trigger a long press by a gesture recognizer. | 
| int32_t [OH_ArkUI_GetGestureParam_angle](_ark_u_i___native_module.md#oh_arkui_getgestureparam_angle) (ArkUI_GestureRecognizer \*recognizer, double \*angle) | Obtains the minimum angle change required for a rotation gesture to be recognized by a gesture recognizer. | 
| int32_t [OH_ArkUI_GetGestureParam_distanceThreshold](_ark_u_i___native_module.md#oh_arkui_getgestureparam_distancethreshold) (ArkUI_GestureRecognizer \*recognizer, double \*distanceThreshold) | Obtains the movement threshold for gestures to be recognized by a gesture recognizer. | 
