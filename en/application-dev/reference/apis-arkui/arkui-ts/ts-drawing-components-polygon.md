# Polygon

The **\<Polygon>** component is used to draw a polygon.

>  **NOTE**
>
>  This component is supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.


## Child Components

Not supported


## APIs

Polygon(value?: {width?: string | number, height?: string | number})

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
| points | Array&lt;[Point](ts-drawing-components-polygon.md#point)&gt; | [] | Vertex coordinates of the polygon.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>An invalid value is handled as the default value.|
| fill | [ResourceColor](ts-types.md#resourcecolor) | Color.Black | Color of the fill area.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>An invalid value is handled as the default value.|
| fillOpacity | [Length](ts-types.md#length) | 1 | Opacity of the fill area.<br>The value range is [0.0, 1.0]. A value less than 0.0 evaluates to the value **0.0**. A value greater than 1.0 evaluates to the value **1.0**. Any other value evaluates to the value **1.0**.<br>This API can be used in ArkTS widgets since API version 9.|
| stroke | [ResourceColor](ts-types.md#resourcecolor) | - | Stroke color. If this attribute is not set, the component does not have any stroke.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>If the value is invalid, no stroke will be drawn.|
| strokeDashArray | Array&lt;[Length](ts-types.md#length)&gt; | [] | Stroke dashes.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>Line segments may overlap when they intersect. An invalid value is handled as the default value.|
| strokeDashOffset | number \| string | 0 | Offset of the start point for drawing the stroke.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>An invalid value is handled as the default value.|
| strokeLineCap | [LineCapStyle](ts-appendix-enums.md#linecapstyle) | LineCapStyle.Butt | Cap style of the stroke.<br>This API can be used in ArkTS widgets since API version 9.|
| strokeLineJoin | [LineJoinStyle](ts-appendix-enums.md#linejoinstyle) | LineJoinStyle.Miter | Join style of the stroke.<br>This API can be used in ArkTS widgets since API version 9.|
| strokeMiterLimit | number \| string | 4 | Limit on the ratio of the miter length to the value of **strokeWidth** used to draw a miter join. The miter length indicates the distance from the outer tip to the inner corner of the miter.<br>**NOTE**<br>This attribute works only when **strokeLineJoin** is set to **LineJoinStyle.Miter**.<br>The value must be greater than or equal to 1.0. If the value is in the [0, 1) range, the value **1.0** will be used. In other cases, the default value will be used.<br>This API can be used in ArkTS widgets since API version 9.|
| strokeOpacity | [Length](ts-types.md#length) | 1 | Stroke opacity.<br>**NOTE**<br>The value range is [0.0, 1.0]. A value less than 0.0 evaluates to the value **0.0**. A value greater than 1.0 evaluates to the value **1.0**. Any other value evaluates to the value **1.0**.<br>This API can be used in ArkTS widgets since API version 9.|
| strokeWidth | [Length](ts-types.md#length) | 1 | Stroke width.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>If of the string type, this parameter cannot be set in percentage. A percentage is processed as 1px.|
| antiAlias | boolean | true | Whether anti-aliasing is enabled.<br>This API can be used in ArkTS widgets since API version 9.|

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
struct PolygonExample {
  build() {
    Column({ space: 10 }) {
      // Draw a triangle in a 100 x 100 rectangle. The start point is (0, 0), the end point is (100, 0), and the passing point is (50, 100).
      Polygon({ width: 100, height: 100 })
        .points([[0, 0], [50, 100], [100, 0]])
        .fill(Color.Green)
      // Draw a quadrilateral in a 100 x 100 rectangle. The start point is (0, 0), the end point is (100, 0), and the passing points are (0, 100) and (100, 100).
      Polygon().width(100).height(100)
        .points([[0, 0], [0, 100], [100, 100], [100, 0]])
        .fillOpacity(0)
        .strokeWidth(5)
        .stroke(Color.Blue)
      // Draw a pentagon in a 100 x 100 rectangle. The start point is (50, 0), the end point is (100, 50), and the passing points are (0, 50), (20, 100), and (80, 100).
      Polygon().width(100).height(100)
        .points([[50, 0], [0, 50], [20, 100], [80, 100], [100, 50]])
        .fill(Color.Red)
        .fillOpacity(0.6)
    }.width('100%').margin({ top: 10 })
  }
}
```

![en-us_image_0000001174582856](figures/en-us_image_0000001174582856.png)
