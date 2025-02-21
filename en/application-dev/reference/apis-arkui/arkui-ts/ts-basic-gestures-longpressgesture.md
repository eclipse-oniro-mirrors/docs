# LongPressGesture

**LongPressGesture** is used to trigger a long press gesture, which requires one or more fingers with a minimum 500 ms hold-down time.

>  **NOTE**
>
>  This gesture is supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.


## APIs

LongPressGesture(value?: { fingers?: number, repeat?: boolean, duration?: number })

Triggers a long press gesture. In components that support drag actions by default, such as **Text**, **TextInput**, **TextArea**, **HyperLink**, **Image**, and **RichEditor**, the long press gesture may conflict with the drag action. If this occurs, they are handled as follows:

If the minimum duration of the long press gesture is less than 500 ms, the long press gesture receives a higher response priority than the drag action.

If the minimum duration of the long press gesture is greater than or equal to 500 ms, the drag action receives a higher response priority than the long press gesture.

**Atomic service API**: This API can be used in atomic services since API version 11.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| fingers | number | No| Minimum number of fingers to trigger a long press gesture. The value ranges from 1 to 10.<br>Default value: **1**<br> **NOTE**<br>If a finger moves more than 15 px after being pressed, the gesture recognition fails.|
| repeat | boolean | No| Whether to continuously trigger the event callback.<br>Default value: **false**|
| duration | number | No| Minimum hold-down time, in ms.<br>Default value: **500**<br>**NOTE**<br>If the value is less than or equal to 0, the default value **500** will be used.|


## Events

| Name| Description|
| -------- | -------- |
| onAction(event:(event: [GestureEvent](ts-gesture-settings.md#gestureevent)) =&gt; void) | Invoked when a long press gesture is recognized.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| onActionEnd(event:(event: [GestureEvent](ts-gesture-settings.md#gestureevent)) =&gt; void) | Invoked when the last finger is lifted after the long press gesture is recognized.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| onActionCancel(event: () =&gt; void) | Invoked when a tap cancellation event is received after the long press gesture is recognized.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|

## Attributes

**Atomic service API**: This API can be used in atomic services since API version 11.

| Name| Type   |Description                                       |
| ----  | ------  | ---------------------------------------- |
| tag<sup>11+</sup>   | string  | Tag for the long press gesture. It is used to distinguish the gesture during custom gesture judgment.|

## Example

```ts
// xxx.ets
@Entry
@Component
struct LongPressGestureExample {
  @State count: number = 0

  build() {
    Column() {
      Text('LongPress onAction:' + this.count).fontSize(28)
        // Touch and hold the text with one finger to trigger the gesture event.
        .gesture(
        LongPressGesture({ repeat: true })
          // When repeat is set to true, the event callback is triggered continuously when the gesture is detected. The triggering interval is specified by duration (500 ms by default).
          .onAction((event: GestureEvent) => {
            if (event && event.repeat) {
              this.count++
            }
          })
            // Triggered when the long press gesture ends.
          .onActionEnd((event: GestureEvent) => {
            this.count = 0
          })
        )
    }
    .height(200)
    .width(300)
    .padding(20)
    .border({ width: 3 })
    .margin(30)
  }
}
```

![en-us_image_0000001257058425](figures/en-us_image_0000001257058425.gif)
