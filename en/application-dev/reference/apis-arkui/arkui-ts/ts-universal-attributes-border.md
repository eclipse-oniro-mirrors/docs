# Border

The border attributes are used to set border styles for components.

>  **NOTE**
>
>  The APIs of this module are supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.
>

## border

border(value: BorderOptions)

Sets the border.

**Widget capability**: Since API version 9, this feature is supported in ArkTS widgets.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type                                   | Mandatory| Description                                                        |
| ------ | --------------------------------------- | ---- | ------------------------------------------------------------ |
| value  | [BorderOptions](#borderoptions) | Yes  | Unified border style.<br>**NOTE**<br>The default value is **0**, indicating that the border is not displayed.<br>The border of a component is displayed above the content of its child components since API version 9.|

## borderStyle

borderStyle(value: BorderStyle | EdgeStyles)

Sets the border style.

**Widget capability**: Since API version 9, this feature is supported in ArkTS widgets.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type                                                        | Mandatory| Description                                              |
| ------ | ------------------------------------------------------------ | ---- | -------------------------------------------------- |
| value  | [BorderStyle](ts-appendix-enums.md#borderstyle) \| [EdgeStyles](#edgestyles9)<sup>9+</sup>| Yes  | Border style.<br>Default value: **BorderStyle.Solid**|

## borderWidth

borderWidth(value: Length | EdgeWidths)

Sets the border width.

**Widget capability**: This API can be used in ArkTS widgets since API version 9.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type                                                        | Mandatory| Description                              |
| ------ | ------------------------------------------------------------ | ---- | ---------------------------------- |
| value  | [Length](ts-types.md#length) \| [EdgeWidths](#edgewidths9)<sup>9+</sup> | Yes  | Border width. The percentage format is not supported.|

## borderColor

borderColor(value: ResourceColor | EdgeColors)

Sets the border color.

**Widget capability**: This API can be used in ArkTS widgets since API version 9.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type                                                        | Mandatory| Description                                        |
| ------ | ------------------------------------------------------------ | ---- | -------------------------------------------- |
| value  | [ResourceColor](ts-types.md#resourcecolor) \| [EdgeColors](#edgecolors9)<sup>9+</sup> | Yes  | Border color.<br>Default value: **Color.Black**|

## borderRadius

borderRadius(value: Length | BorderRadiuses)

Sets the radius of the border rounded corners. The radius is restricted by the component size. The maximum value is half of the component width or height.

**Widget capability**: This API can be used in ArkTS widgets since API version 9.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name| Type                                                        | Mandatory| Description                                  |
| ------ | ------------------------------------------------------------ | ---- | -------------------------------------- |
| value  | [Length](ts-types.md#length) \| [BorderRadiuses](#borderradiuses9)<sup>9+</sup> | Yes  | Border radius. The percentage format is not supported.|

## BorderOptions

| Name  | Type                                                    | Mandatory| Description              |
| ------ | ------------------------------------------------------------ | ---- | ------------------ |
| width  | [Length](ts-types.md#length) \| [EdgeWidths](#edgewidths9)<sup>9+</sup> | No  | Border width.    |
| color  | [ResourceColor](ts-types.md#resourcecolor) \| [EdgeColors](#edgecolors9)<sup>9+</sup> | No  | Border color.    |
| radius | [Length](ts-types.md#length) \| [BorderRadiuses](#borderradiuses9)<sup>9+</sup> | No  | Radius of the border rounded corners.|
| style  | [BorderStyle](ts-appendix-enums.md#borderstyle) \| [EdgeStyles](#edgestyles9)<sup>9+</sup>| No  | Border style.    |

## EdgeWidths<sup>9+</sup>

To reference this object, at least one parameter must be passed.

| Name    | Type                        | Mandatory  | Description     |
| ------ | ---------------------------- | ---- | ------- |
| left   | [Length](ts-types.md#length) | No   | Width of the left border.|
| right  | [Length](ts-types.md#length) | No   | Width of the right border.|
| top    | [Length](ts-types.md#length) | No   | Width of the top border.|
| bottom | [Length](ts-types.md#length) | No   | Width of the bottom border.|

## EdgeColors<sup>9+</sup>

To reference this object, at least one parameter must be passed.

| Name    | Type                                    | Mandatory  | Description     |
| ------ | ---------------------------------------- | ---- | ------- |
| left   | [ResourceColor](ts-types.md#resourcecolor) | No   | Color of the left border.|
| right  | [ResourceColor](ts-types.md#resourcecolor) | No   | Color of the right border.|
| top    | [ResourceColor](ts-types.md#resourcecolor) | No   | Color of the top border.|
| bottom | [ResourceColor](ts-types.md#resourcecolor) | No   | Color of the bottom border.|

## BorderRadiuses<sup>9+</sup>

To reference this object, at least one parameter must be passed.

| Name         | Type                        | Mandatory  | Description      |
| ----------- | ---------------------------- | ---- | -------- |
| topLeft     | [Length](ts-types.md#length) | No   | Radius of the upper-left rounded corner.|
| topRight    | [Length](ts-types.md#length) | No   | Radius of the upper-right rounded corner.|
| bottomLeft  | [Length](ts-types.md#length) | No   | Radius of the lower-left rounded corner.|
| bottomRight | [Length](ts-types.md#length) | No   | Radius of the lower-right rounded corner.|

## EdgeStyles<sup>9+</sup>

To reference this object, at least one parameter must be passed.

| Name    | Type                                    | Mandatory  | Description     |
| ------ | ---------------------------------------- | ---- | ------- |
| left   | [BorderStyle](ts-appendix-enums.md#borderstyle) | No   | Style of the left border.|
| right  | [BorderStyle](ts-appendix-enums.md#borderstyle) | No   | Style of the right border.|
| top    | [BorderStyle](ts-appendix-enums.md#borderstyle) | No   | Style of the top border.|
| bottom | [BorderStyle](ts-appendix-enums.md#borderstyle) | No   | Style of the bottom border.|

## Example

```ts
// xxx.ets
@Entry
@Component
struct BorderExample {
  build() {
    Column() {
      Flex({ justifyContent: FlexAlign.SpaceAround, alignItems: ItemAlign.Center }) {
        // Dashed border
        Text('dashed')
          .borderStyle(BorderStyle.Dashed).borderWidth(5).borderColor(0xAFEEEE).borderRadius(10)
          .width(120).height(120).textAlign(TextAlign.Center).fontSize(16)
        // Dotted border
        Text('dotted')
          .border({ width: 5, color: 0x317AF7, radius: 10, style: BorderStyle.Dotted })
          .width(120).height(120).textAlign(TextAlign.Center).fontSize(16)
      }.width('100%').height(150)

      Text('.border')
        .fontSize(50)
        .width(300)
        .height(300)
        .border({
          width: { left: 3, right: 6, top: 10, bottom: 15 },
          color: { left: '#e3bbbb', right: Color.Blue, top: Color.Red, bottom: Color.Green },
          radius: { topLeft: 10, topRight: 20, bottomLeft: 40, bottomRight: 80 },
          style: {
            left: BorderStyle.Dotted,
            right: BorderStyle.Dotted,
            top: BorderStyle.Solid,
            bottom: BorderStyle.Dashed
          }
        }).textAlign(TextAlign.Center)
    }
  }
}
```

![en-us_image_0000001211898466](figures/en-us_image_0000001211898466.gif)
