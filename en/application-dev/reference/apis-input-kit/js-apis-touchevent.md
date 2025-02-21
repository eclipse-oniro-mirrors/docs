# @ohos.multimodalInput.touchEvent (Touch Event)

The **touchEvent** module provides touchscreen events reported by a device. It is inherited from [InputEvent](./js-apis-inputevent.md).

>  **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```js
import {Action,ToolType,SourceType,Touch,TouchEvent} from '@ohos.multimodalInput.touchEvent';
```

## Action

Enumerates touch event types.

**System capability**: SystemCapability.MultimodalInput.Input.Core

| Name    | Value  | Description  |
| ------ | ------ | ---- |
| CANCEL | 0 | Cancellation of touch.|
| DOWN   | 1 | Pressing of touch.|
| MOVE   | 2 | Moving of touch.|
| UP     | 3 | Lifting of touch.|

## ToolType

Enumerates touch tool types.

**System capability**: SystemCapability.MultimodalInput.Input.Core

| Name      | Value  | Description  |
| -------- | ------ | ---- |
| FINGER   | 0 | Finger  |
| PEN      | 1 | Stylus   |
| RUBBER   | 2 | Eraser |
| BRUSH    | 3 | Brush  |
| PENCIL   | 4 | Pencil  |
| AIRBRUSH | 5 | Air brush  |
| MOUSE    | 6 | Mouse  |
| LENS     | 7 | Lens  |

## SourceType 

Enumerates touch source types.

**System capability**: SystemCapability.MultimodalInput.Input.Core

| Name          | Value | Description  |
| ------------ | ------ | ---- |
| TOUCH_SCREEN | 0 | Touchscreen |
| PEN          | 1 | Stylus |
| TOUCH_PAD    | 2 | Touchpad |

## Touch

Defines the touch point information.

**System capability**: SystemCapability.MultimodalInput.Input.Core

| Name         | Type  | Readable  | Writable  | Description                                 |
| ----------- | ------ | ---- | ---- | ----------------------------------- |
| id          | number | Yes   | No   | Touch event ID.                               |
| pressedTime | number | Yes   | No   | Press timestamp, in μs.                            |
| screenX     | number | Yes   | No   | X coordinate of the touch position on the screen.                       |
| screenY     | number | Yes   | No   | Y coordinate of the touch position on the screen.                       |
| windowX     | number | Yes   | No   | X coordinate of the touch position in the window.                       |
| windowY     | number | Yes   | No   | Y coordinate of the touch position in the window.                       |
| pressure    | number | Yes   | No   | Pressure value. The value range is [0.0, 1.0]. The value 0.0 indicates that the pressure is not supported.      |
| width       | number | Yes   | No   | Width of the touch area.                          |
| height      | number | Yes   | No   | Height of the touch area.                          |
| tiltX       | number | Yes   | No   | Angle relative to the YZ plane. The value range is [-90, 90]. A positive value indicates a rightward tilt.|
| tiltY       | number | Yes   | No   | Angle relative to the XZ plane. The value range is [-90, 90]. A positive value indicates a downward tilt.|
| toolX       | number | Yes   | No   | X coordinate of the center point of the tool area.                          |
| toolY       | number | Yes   | No   | Y coordinate of the center point of the tool area.                          |
| toolWidth   | number | Yes   | No   | Width of the tool area.                             |
| toolHeight  | number | Yes   | No   | Height of the tool area.                             |
| rawX        | number | Yes   | No   | X coordinate of the input device.                          |
| rawY        | number | Yes   | No   | Y coordinate of the input device.                          |
| toolType    | [ToolType](#tooltype) | Yes   | No   | Tool type.                               |

## TouchEvent

Defines a touch event.

**System capability**: SystemCapability.MultimodalInput.Input.Core

| Name        | Type      | Readable  | Writable  | Description       |
| ---------- | ---------- | ---- | ---- | --------- |
| action     | [Action](#action)     | Yes   | No   | Touch event type.    |
| touch      | [Touch](#touch)      | Yes   | No   | Current touch point.  |
| touches    | [Touch](#touch)[]    | Yes   | No   | All touch points.    |
| sourceType | [SourceType](#sourcetype) | Yes   | No   | Touch source type.|
