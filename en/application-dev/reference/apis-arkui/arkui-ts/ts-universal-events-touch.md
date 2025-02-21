# Touch Event

A touch event is triggered when a finger is pressed against, swipes on, or is lifted from a component.

> **NOTE**
>
> This event is supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.

## onTouch

onTouch(event: (event: TouchEvent) => void): T

Invoked when a touch event is triggered.

**Widget capability**: Since API version 9, this feature is supported in ArkTS widgets.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type                             | Mandatory| Description                |
| ------ | --------------------------------- | ---- | -------------------- |
| event  | [TouchEvent](#touchevent) | Yes  | **TouchEvent** object.|

**Return value**

| Type| Description|
| -------- | -------- |
| T | Current component.|

## TouchEvent

| Name               | Type                                      | Description          |
| ------------------- | ---------------------------------------- | ------------ |
| type                | [TouchType](ts-appendix-enums.md#touchtype)      | Type of the touch event.    |
| touches             | Array&lt;[TouchObject](#touchobject)&gt; | All finger information.     |
| changedTouches      | Array&lt;[TouchObject](#touchobject)&gt; | Finger information changed.|
| stopPropagation      | () => void | Stops the event from bubbling upwards or downwards.|
| timestamp<sup>8+</sup> | number | Timestamp of the event. It is the interval between the time when the event is triggered and the time when the system starts.<br>For example, if the system starts at 2023/10/12 11:33 and the touch event is triggered at 2023/10/12 11:34, then the returned timestamp value is 60,000,000,000 ns.<br>Unit: ns|
| target<sup>8+</sup> | [EventTarget](ts-universal-events-click.md#eventtarget8) | Display area of the element that triggers the gesture event.|
| source<sup>8+</sup> | [SourceType](ts-gesture-settings.md#sourcetype)| Event input device.|


### getHistoricalPoints<sup>10+</sup>

getHistoricalPoints(): Array&lt;HistoricalPoint&gt;

Obtains all historical points of the current frame. The touch event frequency of a frame varies by device, and all touch events of the current frame are referred to as its historical points. This API can be called only in [TouchEvent](#touchevent). You can use this API to obtain the historical points of the current frame when [onTouch](#ontouch) is invoked. [onTouch](#ontouch) is invoked only once for a frame. If the value of [TouchEvent](#touchevent) received by the current frame is greater than 1, the last point of the frame is returned through [onTouch](#ontouch). The remaining points are regarded as historical points.

**Return value**

| Type    | Description                     |
| ------ | ----------------------- |
| Array&lt;[HistoricalPoint](#historicalpoint10)&gt;| Array of historical points.|


## TouchObject

| Name   | Type                                       | Description                                 |
| ------- | ------------------------------------------- | ------------------------------------- |
| type    | [TouchType](ts-appendix-enums.md#touchtype) | Type of the touch event.                     |
| id      | number                                      | Unique identifier of a finger.                     |
| x       | number                                      | X coordinate of the touch point relative to the upper left corner of the event responding component.<br>Unit: vp|
| y       | number                                      | Y coordinate of the touch point relative to the upper left corner of the event responding component.<br>Unit: vp|
| windowX<sup>10+</sup>  | number                       | X coordinate of the touch point relative to the upper left corner of the application window.<br>Unit: vp  |
| windowY<sup>10+</sup>  | number                       | Y coordinate of the touch point relative to the upper left corner of the application window.<br>Unit: vp  |
| displayX<sup>10+</sup> | number                       | X coordinate of the touch point relative to the upper left corner of the application screen.<br>Unit: vp  |
| displayY<sup>10+</sup> | number                       | Y coordinate of the touch point relative to the upper left corner of the application screen.<br>Unit: vp  |
| screenX<sup>(deprecated)</sup> | number               | X coordinate of the touch point relative to the upper left corner of the application window.<br>Unit: vp<br>This API is deprecated since API version 10. You are advised to use **windowX** instead.  |
| screenY<sup>(deprecated)</sup> | number               | Y coordinate of the touch point relative to the upper left corner of the application window.<br>Unit: vp<br>This API is deprecated since API version 10. You are advised to use **windowY** instead.  |

## HistoricalPoint<sup>10+</sup>

| Name        | Type                                | Description                                                                        |
| ----------- | ----------------------------------- | ----------------------------------------------------------------------------- |
| touchObject | [TouchObject](#touchobject)  | Basic information of the historical point.                                                  |
| size        | number                              | Size of the contact area between the finger and screen for the historical point.<br>Default value: **0**                                    |
| force       | number                              | Touch force of the historical point.<br>Default value: **0**<br>Value range: [0,1]. A larger value indicates a greater touch force.<br>The support for this API varies by device. Currently, it is only available on tablets.|
| timestamp   | number                              | Timestamp of the historical point. It is the interval between the time when the event is triggered and the time when the system starts.<br>Unit: ns          |
## Example

```ts
// xxx.ets
@Entry
@Component
struct TouchExample {
  @State text: string = ''
  @State eventType: string = ''

  build() {
    Column() {
      Button('Touch').height(40).width(100)
        .onTouch((event?: TouchEvent) => {
          if(event){
            if (event.type === TouchType.Down) {
              this.eventType = 'Down'
            }
            if (event.type === TouchType.Up) {
              this.eventType = 'Up'
            }
            if (event.type === TouchType.Move) {
              this.eventType = 'Move'
            }
            this.text = 'TouchType:' + this.eventType + '\nDistance between touch point and touch element:\nx: '
            + event.touches[0].x + '\n' + 'y: ' + event.touches[0].y + '\nComponent globalPos:('
            + event.target.area.globalPosition.x + ',' + event.target.area.globalPosition.y + ')\nwidth:'
            + event.target.area.width + '\nheight:' + event.target.area.height
          }
        })
      Button('Touch').height(50).width(200).margin(20)
        .onTouch((event?: TouchEvent) => {
          if(event){
            if (event.type === TouchType.Down) {
              this.eventType = 'Down'
            }
            if (event.type === TouchType.Up) {
              this.eventType = 'Up'
            }
            if (event.type === TouchType.Move) {
              this.eventType = 'Move'
            }
            this.text = 'TouchType:' + this.eventType + '\nDistance between touch point and touch element:\nx: '
            + event.touches[0].x + '\n' + 'y: ' + event.touches[0].y + '\nComponent globalPos:('
            + event.target.area.globalPosition.x + ',' + event.target.area.globalPosition.y + ')\nwidth:'
            + event.target.area.width + '\nheight:' + event.target.area.height
          }
        })
      Text(this.text)
    }.width('100%').padding(30)
  }
}
```

![en-us_image_0000001209874754](figures/en-us_image_0000001209874754.gif)
