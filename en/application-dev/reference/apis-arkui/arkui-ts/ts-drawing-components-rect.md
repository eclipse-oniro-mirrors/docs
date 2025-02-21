# Rect

The **\<Rect>** component is used to draw a rectangle.

>  **NOTE**
>
>  This component is supported since API version 9. Updates will be marked with a superscript to indicate their earliest API version.


## Child Components

Not supported


## APIs

Rect(value?: {width?: string | number,height?: string | number,radius?: string | number | Array&lt;string | number&gt;} |
  {width?: string | number,height?: string | number,radiusWidth?: string | number,radiusHeight?: string | number})

This API can be used in ArkTS widgets since API version 9.

**Parameters**

| Name| Type| Mandatory| Default Value| Description|
| -------- | -------- | -------- | -------- | -------- |
| width | string \| number | No| 0 | Width.<br>**NOTE**<br>An invalid value is handled as the default value.|
| height | string \| number | No| 0 | Height.<br>**NOTE**<br>An invalid value is handled as the default value.|
| radius | string \| number \| Array&lt;string \| number&gt; | No| 0 | Radius of the rounded corner. You can set separate radiuses for four rounded corners.<br>This attribute works in a similar manner as **radiusWidth**/**radiusHeight**. When they are used together, it takes precedence over **radiusWidth**/**radiusHeight**.<br>**NOTE**<br>An invalid value is handled as the default value.|
| radiusWidth | string \| number | No| 0 | Width of the rounded corner.<br>**NOTE**<br>An invalid value is handled as the default value.|
| radiusHeight | string \| number | No| 0 | Height of the rounded corner.<br>**NOTE**<br>An invalid value is handled as the default value.|

## Attributes

In addition to the [universal attributes](ts-universal-attributes-size.md), the following attributes are supported.

| Name| Type| Default Value| Description|
| -------- | -------- | -------- | -------- |
| radiusWidth | string \| number | 0 | Width of the rounded corner. The width and height are the same when only the width is set.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>An invalid value is handled as the default value.|
| radiusHeight | string \| number | 0 | Height of the rounded corner. The width and height are the same only when the height is set.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>An invalid value is handled as the default value.|
| radius | string \| number \| Array&lt;string \| number&gt; | 0 | Radius of the rounded corner. You can set separate radiuses for four rounded corners.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>An invalid value is handled as the default value.|
| fill | [ResourceColor](ts-types.md#resourcecolor) | Color.Black | Color of the fill area.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>An invalid value is handled as the default value.|
| fillOpacity | [Length](ts-types.md#length) | 1 | Opacity of the fill area.<br>The value range is [0.0, 1.0]. A value less than 0.0 evaluates to the value **0.0**. A value greater than 1.0 evaluates to the value **1.0**. Any other value evaluates to the value **1.0**.<br>This API can be used in ArkTS widgets since API version 9.|
| stroke | [ResourceColor](ts-types.md#resourcecolor) | - | Stroke color. If this attribute is not set, the component does not have any stroke.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>If the value is invalid, no stroke will be drawn.|
| strokeDashArray | Array&lt;[Length](ts-types.md#length)&gt; | [] | Stroke dashes.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>Line segments may overlap when they intersect. An invalid value is handled as the default value.|
| strokeDashOffset | number \| string | 0 | Offset of the start point for drawing the stroke.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>An invalid value is handled as the default value.|
| strokeLineCap | [LineCapStyle](ts-appendix-enums.md#linecapstyle) | LineCapStyle.Butt | Cap style of the stroke.<br>This API can be used in ArkTS widgets since API version 9.|
| strokeLineJoin | [LineJoinStyle](ts-appendix-enums.md#linejoinstyle) | LineJoinStyle.Miter | Join style of the stroke.<br>This API can be used in ArkTS widgets since API version 9.|
| strokeMiterLimit | number \| string | 4 | Limit on the ratio of the miter length to the value of **strokeWidth** used to draw a miter join. The miter length indicates the distance from the outer tip to the inner corner of the miter.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>This attribute works only when **strokeLineJoin** is set to **LineJoinStyle.Miter**.<br>The value must be greater than or equal to 1.0. If the value is in the [0, 1) range, the value **1.0** will be used. In other cases, the default value will be used.|
| strokeOpacity | [Length](ts-types.md#length) | 1 | Stroke opacity.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>The value range is [0.0, 1.0]. A value less than 0.0 evaluates to the value **0.0**. A value greater than 1.0 evaluates to the value **1.0**. Any other value evaluates to the value **1.0**.|
| strokeWidth | [Length](ts-types.md#length) | 1 | Stroke width.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>If of the string type, this parameter cannot be set in percentage. A percentage is processed as 1px.|
| antiAlias | boolean | true | Whether anti-aliasing is enabled.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>An invalid value is handled as the default value.|

## Example
### Example 1

```ts
// xxx.ets
@Entry
@Component
struct RectExample {
  build() {
    Column({ space: 10 }) {
      Text('normal').fontSize(11).fontColor(0xCCCCCC).width('90%')
      // Draw a 90% x 50 rectangle.
      Column({ space: 5 }) {
        Text('normal').fontSize(9).fontColor(0xCCCCCC).width('90%')
        // Draw a 90% x 50 rectangle.
        Rect({ width: '90%', height: 50 })
          .fill(Color.Pink)
        // Draw a 90% x 50 rectangle.
        Rect()
          .width('90%')
          .height(50)
          .fillOpacity(0)
          .stroke(Color.Red)
          .strokeWidth(3)

        Text('with rounded corners').fontSize(11).fontColor(0xCCCCCC).width('90%')
        // Draw a 90% x 80 rectangle, with the width and height of its rounded corners being 40 and 20, respectively.
        Rect({ width: '90%', height: 80 })
          .radiusHeight(20)
          .radiusWidth(40)
          .fill(Color.Pink)
        // Draw a 90% x 80 rectangle, with the width and height of its rounded corners being both 20.
        Rect({ width: '90%', height: 80 })
          .radius(20)
          .fill(Color.Pink)
          .stroke(Color.Transparent)
      }.width('100%').margin({ top: 10 })
      // Draw a 90% x 50 rectangle, with the width and height of its rounded corners as follows: 40 for the upper left rounded corner, 20 for the upper right rounded corner, 40 for the lower right rounded corner, and 20 for the lower left rounded corner.
      Rect({ width: '90%', height: 80 })
        .radius([[40, 40], [20, 20], [40, 40], [20, 20]])
        .fill(Color.Pink)
    }.width('100%').margin({ top: 5 })
  }
}
```

![en-us_image_0000001174264386](figures/en-us_image_0000001174264386.png)

### Example 2

```ts
// xxx.ets
@Entry
@Component
struct RectExample {
  build() {
    Column({ space: 10 }) {
      Column()
        .width(100)
        .height(100)
        .linearGradient({
          direction: GradientDirection.Right,
          colors: [[0xff0000, 0.0], [0x0000ff, 0.3], [0xffff00, 1.0]]
        })
        .clip(new Rect({ width: 100, height: 100, radius: 40 }))
      Rect()
        .width(100)
        .height(100)
        // Set the color of the fill area. To display the color gradient of the background, set .fillOpacity(0.0).
        .fill(Color.Pink)
        // Set the radius of the rounded corner to 40.
        .radius(40)
        .stroke(Color.Black)
        // Set the color gradient. It takes effect only for a 100 x 100 rectangular area. The boundary of the gradient does not contain rounded corners.
        .linearGradient({
          direction: GradientDirection.Right,
          colors: [[0xff0000, 0.0], [0x0000ff, 0.3], [0xffff00, 1.0]]
        })
    }
  }
}
```

![en-us_image_0000001174264386](figures/en-us_image_0000001174264387.jpeg)
