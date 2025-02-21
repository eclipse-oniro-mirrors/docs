# Polyline

The **\<Polyline>** component is used to draw a polyline.

>  **NOTE**
>
>  This component is supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.


## Child Components

Not supported


## APIs

Polyline(value?: {width?: string | number, height?: string | number})

This API can be used in ArkTS widgets since API version 9.

**Parameters**

| Name| Type| Mandatory| Default Value| Description|
| -------- | -------- | -------- | -------- | -------- |
| width | string \| number | No| 0 | Width.<br>**NOTE**<br>An invalid value is handled as the default value.|
| height | string \| number | No| 0 | Height.<br>**NOTE**<br>An invalid value is handled as the default value.|



## Attributes

In addition to the [universal attributes](ts-universal-attributes-size.md), the following attributes are supported.

| Name| Type| Default Value| Description|
| -------- | -------- | -------- | -------- |
| points | Array&lt;[Point](ts-drawing-components-polyline.md#point)&gt; | [] | List of coordinates that the polyline passes through.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>An invalid value is handled as the default value.|
| fill | [ResourceColor](ts-types.md#resourcecolor) | Color.Black | Color of the fill area.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>An invalid value is handled as the default value.|
| fillOpacity | [Length](ts-types.md#length) | 1 | Opacity of the fill area.<br>The value range is [0.0, 1.0]. A value less than 0.0 evaluates to the value **0.0**. A value greater than 1.0 evaluates to the value **1.0**. Any other value evaluates to the value **1.0**.<br>This API can be used in ArkTS widgets since API version 9.|
| stroke | [ResourceColor](ts-types.md#resourcecolor) | - | Stroke color. If this attribute is not set, the component does not have any stroke.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>If the value is invalid, no stroke will be drawn.|
| strokeDashArray | Array&lt;[Length](ts-types.md#length)&gt; | [] | Stroke dashes.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>Line segments may overlap when they intersect. An invalid value is handled as the default value.|
| strokeDashOffset | number \| string | 0 | Offset of the start point for drawing the stroke.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>An invalid value is handled as the default value.|
| strokeLineCap | [LineCapStyle](ts-appendix-enums.md#linecapstyle) | LineCapStyle.Butt | Cap style of the stroke.<br>This API can be used in ArkTS widgets since API version 9.|
| strokeLineJoin | [LineJoinStyle](ts-appendix-enums.md#linejoinstyle) | LineJoinStyle.Miter | Join style of the stroke.<br>This API can be used in ArkTS widgets since API version 9.|
| strokeMiterLimit | number \| string | 4 | Limit on the ratio of the miter length to the value of **strokeWidth** used to draw a miter join. The miter length indicates the distance from the outer tip to the inner corner of the miter.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>This attribute works only when **strokeLineJoin** is set to **LineJoinStyle.Miter**.<br>The value must be greater than or equal to 1.0. If the value is in the [0, 1) range, the value **1.0** will be used. In other cases, the default value will be used.<br>This API can be used in ArkTS widgets since API version 9.|
| strokeOpacity | [Length](ts-types.md#length) | 1 | Stroke opacity.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>The value range is [0.0, 1.0]. A value less than 0.0 evaluates to the value **0.0**. A value greater than 1.0 evaluates to the value **1.0**. Any other value evaluates to the value **1.0**.|
| strokeWidth | [Length](ts-types.md#length) | 1 | Stroke width.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>If of the string type, this parameter cannot be set in percentage. A percentage is processed as 1px.|
| antiAlias | boolean | true | Whether anti-aliasing is enabled.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>An invalid value is handled as the default value.|



## Point

Describes the coordinates of a point.

This API can be used in ArkTS widgets since API version 9.

| Name     | Type            | Description                                                        |
| --------- | -------------------- | ------------------------------------------------------------ |
| Point | [number, number] | Coordinates of a point. The first parameter is the x-coordinate, and the second parameter is the y-coordinate (relative coordinate).|

## Example

```ts
// xxx.ets
@Entry
@Component
struct PolylineExample {
  build() {
    Column({ space: 10 }) {
      // Draw a polyline in a 100 x 100 rectangle. The start point is (0, 0), the end point is (100, 100), and the passing point is (20,60).
      Polyline({ width: 100, height: 100 })
        .points([[0, 0], [20, 60], [100, 100]])
        .fillOpacity(0)
        .stroke(Color.Blue)
        .strokeWidth(3)
      // Draw a polyline in a 100 x 100 rectangle. The start point is (20, 0), the end point is (100, 90), and the passing point is (0,100).
      Polyline()
        .width(100)
        .height(100)
        .fillOpacity(0)
        .stroke(Color.Red)
        .strokeWidth(8)
        .points([[20, 0], [0, 100], [100, 90]])
          // Set the join style of the stroke to a round corner.
        .strokeLineJoin(LineJoinStyle.Round)
          // Set the cap style of the stroke to a half circle.
        .strokeLineCap(LineCapStyle.Round)
    }.width('100%')
  }
}
```

![en-us_image_0000001219744185](figures/en-us_image_0000001219744185.png)
