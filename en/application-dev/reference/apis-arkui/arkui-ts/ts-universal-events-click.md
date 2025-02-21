# Click Event

A click event is triggered when a component is clicked.

>  **NOTE**
>
>  The APIs of this module are supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.

## onClick

onClick(event: (event: ClickEvent) => void): T

Called when a click event occurs.

**Widget capability**: This API can be used in ArkTS widgets since API version 9.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type                             | Mandatory| Description                |
| ------ | --------------------------------- | ---- | -------------------- |
| event  | [ClickEvent](#clickevent) | Yes  | [ClickEvent](#clickevent) object.|

**Return value**

| Type| Description|
| -------- | -------- |
| T | Current component.|

## ClickEvent

This API can be used in ArkTS widgets since API version 9.

| Name           | Type                                | Description                                                    |
| ------------------- | ------------------------------------ | -------------------------------------------------------- |
| x                   | number                               | X coordinate of the click point relative to the left edge of the clicked component.<br>Unit: vp |
| y                   | number                               | Y coordinate of the click point relative to the upper edge of the clicked component.<br>Unit: vp |
| timestamp<sup>8+</sup> | number | Timestamp of the event. It is the interval between the time when the event is triggered and the time when the system starts.<br>Unit: ns|
| target<sup>8+</sup> | [EventTarget](#eventtarget8) | Display area of the object that triggers the event.|
| source<sup>8+</sup> | [SourceType](ts-gesture-settings.md#sourcetype)| Event input device.|
| windowX<sup>10+</sup> | number                             | X coordinate of the click point relative to the upper left corner of the application window.<br>Unit: vp |
| windowY<sup>10+</sup> | number                             | Y coordinate of the click point relative to the upper left corner of the application window.<br>Unit: vp |
| displayX<sup>10+</sup> | number                            | X coordinate of the click point relative to the upper left corner of the application screen.<br>Unit: vp |
| displayY<sup>10+</sup> | number                            | Y coordinate of the click relative to the upper left corner of the application screen.<br>Unit: vp|
| screenX<sup>(deprecated)</sup> | number                    | X coordinate of the click relative to the upper left corner of the application window.<br>This API is deprecated since API version 10. You are advised to use **windowX** instead. |
| screenY<sup>(deprecated)</sup> | number                    | Y coordinate of the click point relative to the upper left corner of the application window.<br>This API is deprecated since API version 10. You are advised to use **windowY** instead. |

## EventTarget<sup>8+</sup>

This API can be used in ArkTS widgets since API version 9.

| Name  | Type                     | Description        |
| ---- | ------------------------- | ---------- |
| area | [Area](ts-types.md#area8) | Area information of the target element.|

## Example

```ts
// xxx.ets
@Entry
@Component
struct ClickExample {
  @State text: string = ''

  build() {
    Column() {
      Row({ space: 20 }) {
        Button('Click').width(100).height(40)
          .onClick((event?: ClickEvent) => {
            if(event){
              this.text = 'Click Point:' + '\n  windowX:' + event.windowX + '\n  windowY:' + event.windowY
              + '\n  x:' + event.x + '\n  y:' + event.y + '\ntarget:' + '\n  component globalPos:('
              + event.target.area.globalPosition.x + ',' + event.target.area.globalPosition.y + ')\n  width:'
              + event.target.area.width + '\n  height:' + event.target.area.height + '\ntimestamp' + event.timestamp;
            }
          })
        Button('Click').width(200).height(50)
          .onClick((event?: ClickEvent) => {
            if(event){
              this.text = 'Click Point:' + '\n  windowX:' + event.windowX + '\n  windowY:' + event.windowY
              + '\n  x:' + event.x + '\n  y:' + event.y + '\ntarget:' + '\n  component globalPos:('
              + event.target.area.globalPosition.x + ',' + event.target.area.globalPosition.y + ')\n  width:'
              + event.target.area.width + '\n  height:' + event.target.area.height + '\ntimestamp' + event.timestamp;
            }
          })
      }.margin(20)

      Text(this.text).margin(15)
    }.width('100%')
  }
}
```


![en-us_image_0000001210353788](figures/en-us_image_0000001210353788.gif)
