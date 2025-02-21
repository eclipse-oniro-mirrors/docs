# Slider

The **\<Slider>** component is used to quickly adjust settings, such as the volume and brightness.

>  **NOTE**
>
>  This component is supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.


## Child Components

Not supported


## APIs

Slider(options?: SliderOptions)

**Widget capability**: This API can be used in ArkTS widgets since API version 9.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name | Type                                   | Mandatory| Description              |
| ------- | --------------------------------------- | ---- | ------------------ |
| options | [SliderOptions](#slideroptions) | No  | Parameters of the slider.|

## SliderOptions

This API can be used in ArkTS widgets since API version 9.

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | number | No| Current progress.<br>Default value: value of **min**<br>Since API version 10, this parameter supports two-way binding through [$$](../../../quick-start/arkts-two-way-sync.md).|
| min | number | No| Minimum value.<br>Default value: **0**|
| max | number | No| Maximum value.<br>Default value: **100**<br>**NOTE**<br>If the value of **min** is greater than or equal to the value of **max**, the default value **0** is used for **min** and the default value **100** is used for **max**.<br>If the value is not within the [min, max] range, the value of **min** or **max** is used, whichever is closer.|
| step | number | No| Step of the slider.<br>Default value: **1**<br>Value range: [0.01, max]<br>**NOTE**<br>If this parameter is set to a value less than 0 or greater than the value of **max**, the default value is used.|
| style | [SliderStyle](#sliderstyle) | No| Style of the slider thumb and track.<br>Default value: **SliderStyle.OutSet**|
| direction<sup>8+</sup> | [Axis](ts-appendix-enums.md#axis) | No| Whether the slider moves horizontally or vertically.<br>Default value: **Axis.Horizontal**|
| reverse<sup>8+</sup> | boolean | No| Whether the slider values are reversed. By default, the values increase from left to right for a horizontal slider and from top to bottom for a vertical slider.<br>Default value: **false**|

## SliderStyle

This API can be used in ArkTS widgets since API version 9.

| Name| Description|
| -------- | -------- |
| OutSet | The thumb is on the track.|
| InSet  | The thumb is in the track.|

## Attributes

All the [universal attributes](ts-universal-attributes-size.md) except **responseRegion** are supported 

| Name| Type| Description|
| -------- | -------- | -------- |
| blockColor | [ResourceColor](ts-types.md#resourcecolor) | Color of the thumb.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>Default value: **'#ffffff'**<br>When **SliderBlockType.DEFAULT** is used, **blockColor** sets the color of the round slider.<br>When **SliderBlockType.IMAGE** is used, `blockColor` does not work as the slider has no fill color.<br>When **SliderBlockType.SHAPE** is used, **blockColor** sets the color of the slider in a custom shape.|
| trackColor | [ResourceColor](ts-types.md#resourcecolor) | Background color of the track.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>Default value: **'#19182431'**|
| selectedColor | [ResourceColor](ts-types.md#resourcecolor) | Color of the portion of the track between the minimum value and the thumb.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>Default value: **'#007dff'**|
| showSteps | boolean | Whether to display the current step.<br>Default value: **false**<br>This API can be used in ArkTS widgets since API version 9.|
| showTips | value: boolean,<br>content<sup>10+</sup>?: [ResourceStr](ts-types.md#resourcestr) | **value**: whether to display a tooltip when the user drags the slider.<br>Default value: **false**<br>**content**: content of the tooltip. By default, the tooltip shows the current percentage value.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>When **direction** is set to **Axis.Horizontal**, the tooltip is displayed right above the slider. When **direction** is set to **Axis.Vertical**, the tooltip is displayed on the left of the slider.<br>The drawing area of the tooltip is the overlay of the slider.<br>If no margin is set for the slider or the margin is not large enough, the tooltip will be clipped.|
| trackThickness<sup>8+</sup> | [Length](ts-types.md#length) | Track thickness of the slider.<br>Default value: **4.0vp** when **style** is set to **[SliderStyle](#sliderstyle).OutSet**; **20.0vp** when **style** is set to **[SliderStyle](#sliderstyle).InSet**<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>If the value is less than or equal to 0, the default value is used.<br>To ensure [SliderStyle](#sliderstyle) works as expected for the thumb and track, **blockSize** should increase or decrease proportionally with **trackThickness**. Specially, when **style** is **[SliderStyle](#sliderstyle).OutSet**, **trackThickness**: **blockSize** = 1:4; when **style** is **[SliderStyle](#sliderstyle).InSet**, **trackThickness**: **blockSize** = 5:3.<br>In changing the value of **trackThickness**, if it or the value of **blockSize** exceeds the width or height of the slider, the default value is used. (When **style** is **[SliderStyle](#sliderstyle).OutSet**, it is possible that only the value of **blockSize** exceeds the height of the slider.)|
| blockBorderColor<sup>10+</sup> | [ResourceColor](ts-types.md#resourcecolor) | Border color of the slider in the block direction.<br>**NOTE**<br>Default value: **'#00000000'**<br>When **SliderBlockType.DEFAULT** is used, **blockBorderColor** sets the border color of the round slider.<br>When **SliderBlockType.IMAGE** is used, **blockBorderColor** does not work as the slider has no border.<br>When **SliderBlockType.SHAPE** is used, **blockBorderColor** sets the border color of the slider in a custom shape.|
| blockBorderWidth<sup>10+</sup> | [Length](ts-types.md#length) | Border width of the slider in the block direction.<br>**NOTE**<br>When **SliderBlockType.DEFAULT** is used, **blockBorderWidth** sets the border width of the round slider.<br>When **SliderBlockType.IMAGE** is used, **blockBorderWidth** does not work as the slider has no border.<br>WWhen **SliderBlockType.SHAPE** is used, **blockBorderWidth** sets the border width of the slider in a custom shape.|
| stepColor<sup>10+</sup> | [ResourceColor](ts-types.md#resourcecolor) | Step color.<br>**NOTE**<br>Default value: **'#19182431'**|
| trackBorderRadius<sup>10+</sup> | [Length](ts-types.md#length) | Radius of the rounded corner of the slider track.<br>**NOTE**<br>Default value: **'2vp'**|
| blockSize<sup>10+</sup> | [SizeOptions](ts-types.md#sizeoptions) | Size of the slider in the block direction.<br>**NOTE**<br>Default value:<br>**{width: 16, height: 16}** when **style** is set to [SliderStyle](#sliderstyle).OutSet<br>{width: 16, height: 16} when **style** is set to [SliderStyle](#sliderstyle).InSet<br>If the width and height of **bolckSize** are different, the smaller value is used. If one or both of the width and height are less than or equal to 0, the default value is used.|
| blockStyle<sup>10+</sup> | [SliderBlockStyle](#sliderblockstyle10) | Style of the slider in the block direction.<br>**NOTE**<br>Default value: **SliderBlockType.DEFAULT**, indicating the round slider.|
| stepSize<sup>10+</sup> | [Length](ts-types.md#length) | Step size (diameter).<br>**NOTE**<br>Default value: **'4vp'**<br>If the value is 0, the step size is not displayed. If the value is less than 0, the default value is used.|
| minLabel<sup>deprecated</sup> | string | Minimum value.<br>This API is deprecated since API version 9. You are advised to use **min** instead.|
| maxLabel<sup>deprecated</sup> | string | Maximum value.<br>This API is deprecated since API version 9. You are advised to use **max** instead.|

>  **NOTE**
>
>  - By default, the slider has no padding.
>  - For a horizontal slider, the default height is 40 vp, the width equals that of the parent container, the slider track is displayed in the center, and the left and right margins are 10 vp and not covered by the paddings (if set).
>  - For a vertical slider, the default width is 40 vp, the height equals that of the parent container, the slider track is displayed in the center, and the top and bottom margins are 6 vp and not covered by the paddings (if set).

## SliderBlockStyle<sup>10+</sup>

Describes the style of the slider in the block direction.

| Name | Type                                                        | Mandatory| Description                                                        |
| ----- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| type  | [SliderBlockType](#sliderblocktype10)                | Yes  | Type of the slider in the block direction.<br>Default value: **SliderBlockType.DEFAULT**, indicating the round slider.|
| image | [ResourceStr](ts-types.md#resourcestr)                       | No  | Image resource of the slider.<br>The area size for displaying the image is subject to the **blockSize** attribute. Be mindful of the image size when selecting an image.|
| shape | [Circle](ts-drawing-components-circle.md) \| [Ellipse](ts-drawing-components-ellipse.md) \| [Path](ts-drawing-components-path.md) \| [Rect](ts-drawing-components-rect.md)  | No  | Custom shape of the slider.                                  |

## SliderBlockType<sup>10+</sup>

Enumerates the types of the slider in the block direction.

| Name   | Description                  |
| ------- | ---------------------- |
| DEFAULT | Round slider.  |
| IMAGE   | Slider with an image background.  |
| SHAPE   | Slider in a custom shape.|

## Events

In addition to the [universal events](ts-universal-events-click.md), the following attributes are supported.

| Name| Description|
| -------- | -------- |
| onChange(callback: (value: number, mode: SliderChangeMode) =&gt; void) | Invoked when the slider is dragged or clicked.<br>**value**: current slider value. If the return value contains decimals, you can use the **number.toFixed()** API to process the data to the expected precision.<br>**mode**: state triggered by the event.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>The **Begin** and **End** states are triggered when the slider is clicked with a gesture. The **Moving** and **Click** states are triggered when the value of **value** changes.<br>If the coherent action is a drag action, the **Click** state will not be triggered.<br>The value range of **value** is the **steps** value array.|

## SliderChangeMode

This API can be used in ArkTS widgets since API version 9.

| Name| Value| Description|
| -------- | -------- | -------- |
| Begin | 0 | The user touches or presses the slider with a gesture or mouse.|
| Moving | 1 | The user is dragging the slider.|
| End | 2 | The user stops dragging the slider by lifting their finger or releasing the mouse.|
| Click    | 3    | The user moves the slider by touching the slider track.|

## Example

### Example 1

```ts
// xxx.ets
@Entry
@Component
struct SliderExample {
  @State outSetValueOne: number = 40
  @State inSetValueOne: number = 40
  @State outSetValueTwo: number = 40
  @State inSetValueTwo: number = 40
  @State vOutSetValueOne: number = 40
  @State vInSetValueOne: number = 40
  @State vOutSetValueTwo: number = 40
  @State vInSetValueTwo: number = 40

  build() {
    Column({ space: 8 }) {
      Text('outset slider').fontSize(9).fontColor(0xCCCCCC).width('90%').margin(15)
      Row() {
        Slider({
          value: this.outSetValueOne,
          min: 0,
          max: 100,
          style: SliderStyle.OutSet
        })
          .showTips(true)
          .onChange((value: number, mode: SliderChangeMode) => {
            this.outSetValueOne = value
            console.info('value:' + value + 'mode:' + mode.toString())
          })
        // toFixed(0) converts the return value of the slider to an integer.
        Text(this.outSetValueOne.toFixed(0)).fontSize(12)
      }
      .width('80%')
      Row() {
        Slider({
          value: this.outSetValueTwo,
          step: 10,
          style: SliderStyle.OutSet
        })
          .showSteps(true)
          .onChange((value: number, mode: SliderChangeMode) => {
            this.outSetValueTwo = value
            console.info('value:' + value + 'mode:' + mode.toString())
          })
        Text(this.outSetValueTwo.toFixed(0)).fontSize(12)
      }
      .width('80%')

      Text('inset slider').fontSize(9).fontColor(0xCCCCCC).width('90%').margin(15)
      Row() {
        Slider({
          value: this.inSetValueOne,
          min: 0,
          max: 100,
          style: SliderStyle.InSet
        })
          .blockColor('#191970')
          .trackColor('#ADD8E6')
          .selectedColor('#4169E1')
          .showTips(true)
          .onChange((value: number, mode: SliderChangeMode) => {
            this.inSetValueOne = value
            console.info('value:' + value + 'mode:' + mode.toString())
          })
        Text(this.inSetValueOne.toFixed(0)).fontSize(12)
      }
      .width('80%')
      Row() {
        Slider({
          value: this.inSetValueTwo,
          step: 10,
          style: SliderStyle.InSet
        })
          .blockColor('#191970')
          .trackColor('#ADD8E6')
          .selectedColor('#4169E1')
          .showSteps(true)
          .onChange((value: number, mode: SliderChangeMode) => {
            this.inSetValueTwo = value
            console.info('value:' + value + 'mode:' + mode.toString())
          })
        Text(this.inSetValueTwo.toFixed(0)).fontSize(12)
      }
      .width('80%')

      Row() {
        Column() {
          Text('vertical outset slider').fontSize(9).fontColor(0xCCCCCC).width('50%').margin(15)
          Row() {
            Text().width('10%')
            Slider({
              value: this.vOutSetValueOne,
              style: SliderStyle.OutSet,
              direction: Axis.Vertical
            })
              .blockColor('#191970')
              .trackColor('#ADD8E6')
              .selectedColor('#4169E1')
              .showTips(true)
              .onChange((value: number, mode: SliderChangeMode) => {
                this.vOutSetValueOne = value
                console.info('value:' + value + 'mode:' + mode.toString())
              })
            Slider({
              value: this.vOutSetValueTwo,
              step: 10,
              style: SliderStyle.OutSet,
              direction: Axis.Vertical
            })
              .blockColor('#191970')
              .trackColor('#ADD8E6')
              .selectedColor('#4169E1')
              .showSteps(true)
              .onChange((value: number, mode: SliderChangeMode) => {
                this.vOutSetValueTwo = value
                console.info('value:' + value + 'mode:' + mode.toString())
              })
          }
        }.width('50%').height(300)

        Column() {
          Text('vertical inset slider').fontSize(9).fontColor(0xCCCCCC).width('50%').margin(15)
          Row() {
            Slider({
              value: this.vInSetValueOne,
              style: SliderStyle.InSet,
              direction: Axis.Vertical,
              reverse: true // By default, at the top of the vertical slider is the min value and at the bottom is the max value. Therefore, if you want to slide from bottom to top, set reverse to true.
            })
              .showTips(true)
              .onChange((value: number, mode: SliderChangeMode) => {
                this.vInSetValueOne = value
                console.info('value:' + value + 'mode:' + mode.toString())
              })
            Slider({
              value: this.vInSetValueTwo,
              step: 10,
              style: SliderStyle.InSet,
              direction: Axis.Vertical,
              reverse: true
            })
              .showSteps(true)
              .onChange((value: number, mode: SliderChangeMode) => {
                this.vInSetValueTwo = value
                console.info('value:' + value + 'mode:' + mode.toString())
              })
          }
        }.width('50%').height(300)
      }
    }.width('100%')
  }
}
```

![en-us_image_0000001179613854](figures/en-us_image_0000001179613854.gif)

### Example 2

```ts
@Entry
@Component
struct SliderExample {
  @State tipsValue: number = 40

  build() {
    Column({ space: 8 }) {
      Text('block').fontSize(9).fontColor(0xCCCCCC).margin(15).width('90%')
      Slider({ style: SliderStyle.OutSet, value: 40 })
        .blockSize({ width: 40, height: 40 })
        .blockBorderColor(Color.Red)
        .blockBorderWidth(5)
      Divider()
      Text('step').fontSize(9).fontColor(0xCCCCCC).margin(15).width('90%')
      Slider({ style: SliderStyle.InSet, value: 40, step: 10 })
        .showSteps(true)
        .stepSize(8)
        .stepColor(Color.Yellow)
      Divider()
      Text('track').fontSize(9).fontColor(0xCCCCCC).margin(15).width('90%')
      Slider({ style: SliderStyle.InSet, value: 40 })
        .trackBorderRadius(2)
      Divider()
      Text('blockStyle').fontSize(9).fontColor(0xCCCCCC).margin(15).width('90%')
      Slider({ style: SliderStyle.OutSet, value: 40 })
        .blockStyle({ type: SliderBlockType.DEFAULT })
      Slider({ style: SliderStyle.OutSet, value: 40 })
        .blockStyle({ type: SliderBlockType.IMAGE, image: $r('sys.media.ohos_app_icon') })
      Slider({ style: SliderStyle.OutSet, value: 40 })
        .blockSize({ width: '60px', height: '60px' })
        .blockColor(Color.Red)
        .blockStyle({ type: SliderBlockType.SHAPE, shape: new Path({ commands: 'M60 60 M30 30 L15 56 L45 56 Z' }) })
      Divider()
      Text('tips').fontSize(9).fontColor(0xCCCCCC).margin(15).width('90%')
      Slider({ style: SliderStyle.InSet, value: this.tipsValue })
        .showTips(true, this.tipsValue.toFixed())
        .onChange(value => {
          this.tipsValue = value
        })
    }
  }
}
```

![](figures/slider_2.png)
