# @ohos. deviceStatus.dragInteraction (Drag)

 The **dragInteraction** module provides the APIs to enable and disable listening for dragging status changes.

> **NOTE**
>
>   - The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
>  - The APIs provided by this module are system APIs.

## Modules to Import

```js
import dragInteraction from '@ohos.deviceStatus.dragInteraction'
```

## dragInteraction.on

on(type: 'drag', callback: Callback&lt;DragState&gt;): void;

Enables listening for dragging status changes.

**System capability**: SystemCapability.Msdp.DeviceStatus.Drag

**Parameters**

| Name               | Type                                                            | Mandatory| Description                           |
| --------             | ----------------------------                                    | ---- | ----------------------------   |
| type                 | string                                                          |  Yes | Event type. This field has a fixed value of **drag**.|
| callback             | Callback&lt;[DragState](#dragstate)&gt; |  Yes | Callback used to return the dragging status.|

**Example**

```js
try {
  dragInteraction.on('drag', (data) => {
    console.log(`Drag interaction event: ${JSON.stringify(data)}`);
  });
} catch (error) {
  console.log(`Register failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## dragInteraction.off

off(type: 'drag', callback?: Callback&lt;DragState&gt;): void;

Disables listening for dragging status changes.

**System capability**: SystemCapability.Msdp.DeviceStatus.Drag

**Parameters**

| Name               | Type                                                             | Mandatory   | Description                          |
| --------             | ----------------------------                                     | ----   | ----------------------------   |
| type                 | string                                                           |  Yes   | Event type. This field has a fixed value of **drag**.|
| callback             | Callback&lt;[DragState](#dragstate)> |  No | Callback to be unregistered. If this parameter is not specified, all callbacks registered by the current application will be unregistered.|

**Example**

```js
// Unregister a single callback.
function callback(event) {
  console.log(`Drag interaction event: ${JSON.stringify(event)}`);
  return false;
}
try {
  dragInteraction.on('drag', callback);
  dragInteraction.off("drag", callback);
} catch (error) {
  console.log(`Execute failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```
```js
// Unregister all callbacks.
function callback(event) {
  console.log(`Drag interaction event: ${JSON.stringify(event)}`);
  return false;
}
try {
  dragInteraction.on('drag', callback);
  dragInteraction.off("drag");
} catch (error) {
  console.log(`Execute failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

##  DragState

Enumerates dragging states.

**System capability**: SystemCapability.Msdp.DeviceStatus.Drag

| Name                      | Value                            | Description                             |
| --------                     |  -----------------               |  -----------------               |
| MSG_DRAG_STATE_START |  1   | Dragging starts.|
| MSG_DRAG_STATE_STOP |  2  |  Dragging is ended. |
| MSG_DRAG_STATE_CANCEL |  3  |  Dragging is canceled. |