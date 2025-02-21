#  Select

The **<Select\>** component provides a drop-down list box that allows users to select among multiple options.

>  **NOTE**
>
>  This component is supported since API version 8. Updates will be marked with a superscript to indicate their earliest API version.

## Child Components

Not supported

## APIs

Select(options: Array\<[SelectOption](#selectoption)\>)

**Parameters**

| Name | Type                                      | Mandatory| Description      |
| ------- | ---------------------------------------------- | ---- | -------------- |
| options | Array\<[SelectOption](#selectoption)\> | Yes  | Options in the drop-down list box.|

## SelectOption

| Name| Type                           | Mandatory| Description      |
| ------ | ----------------------------------- | ---- | -------------- |
| value  | [ResourceStr](ts-types.md#resourcestr) | Yes  | Value of an option in the drop-down list box.|
| icon   | [ResourceStr](ts-types.md#resourcestr) | No  | Icon of an option in the drop-down list box.|

## Attributes

In addition to the [universal attributes](ts-universal-attributes-size.md), the following attributes are supported.

| Name                   | Type                             | Description                                         |
| ----------------------- | ------------------------------------- | --------------------------------------------- |
| selected                | number \| [Resource](ts-types.md#resource)<sup>11+</sup>    | Index of the initial selected option in the drop-down list box. The index of the first option is **0**.<br>If this attribute is set to an invalid value or is not set, the default value **-1** will be used, which means that no option will be selected. If this attribute is set to **undefined** or **null**, the first option will be selected.<br>Since API version 10, this attribute supports two-way binding through [$$](../../../quick-start/arkts-two-way-sync.md).|
| value                   | [ResourceStr](ts-types.md#resourcestr)<sup>11+</sup> | Text of the drop-down button. By default, it will be replaced by the content of the selected option.<br>Since API version 10, this attribute supports two-way binding through [$$](../../../quick-start/arkts-two-way-sync.md).|
| font                    | [Font](ts-types.md#font)          | Text font of the drop-down button.<br>Default value:<br>{<br>size: '16fp',<br>weight: FontWeight.Medium<br>} <br>**NOTE**<br>When **size** is set to **0**, the text is not displayed. When **size** is set to a negative value, the text is displayed at its default size.|
| fontColor               | [ResourceColor](ts-types.md#resourcecolor) | Text color of the drop-down button.<br>Default value: **'\#E5182431'**|
| selectedOptionBgColor   | [ResourceColor](ts-types.md#resourcecolor) | Background color of the selected option in the drop-down list box.<br>Default value: **'\#33007DFF'**|
| selectedOptionFont      | [Font](ts-types.md#font)          | Text font of the selected option in the drop-down list box.<br>Default value:<br>{<br>size: '16fp',<br>weight: FontWeight.Regular<br>} <br>**NOTE**<br>When **size** is set to **0**, the text is not displayed. When **size** is set to a negative value, the text is displayed at its default size.|
| selectedOptionFontColor | [ResourceColor](ts-types.md#resourcecolor) | Text color of the selected option in the drop-down list box.<br>Default value: **'\#ff007dff'**|
| optionBgColor           | [ResourceColor](ts-types.md#resourcecolor) | Background color of an option in the drop-down list box.<br>Default value: **'\#ffffffff'**|
| optionFont              | [Font](ts-types.md#font)          | Text font of an option in the drop-down list box.<br>Default value:<br>{<br>size: '16fp',<br>weight: FontWeight.Regular<br>}<br>**NOTE**<br>When **size** is set to **0**, the text is not displayed. When **size** is set to a negative value, the text is displayed at its default size.|
| optionFontColor         | [ResourceColor](ts-types.md#resourcecolor) | Text color of an option in the drop-down list box.<br>Default value: **'\#ff182431'**|
| space<sup>10+</sup>         | [Length](ts-types.md#length)               | Spacing between the text and arrow of an option.<br>**NOTE**<br>This attribute cannot be set in percentage.<br>Default value: **8**<br>If this attribute to **null**, **undefined**, or a value less than or equal to 8, the default value is used.|
| arrowPosition<sup>10+</sup> | [ArrowPosition](#arrowposition10)                  | Alignment between the text and arrow of an option.<br>Default value: **ArrowPosition.END**|
| menuAlign<sup>10+</sup> | alignType: [MenuAlignType](#menualigntype10),<br> offset?: [Offset](ts-types.md#offset)    | Alignment between the drop-down button and the drop-down menu.<br> - **alignType**: alignment type. Mandatory.<br>Default value: **MenuAlignType.START**<br> - **offset**: offset of the drop-down menu relative to the drop-down button after alignment based on the specified alignment type.<br> Default value: **{dx: 0, dy: 0}**|
| optionWidth<sup>11+</sup> | [Dimension](ts-types.md#dimension10) \| [OptionWidthMode](#optionwidthmode11) | Width of the option in the drop-down list box. **OptionWidthMode** specifies whether to inherit the width of the drop-down list button.<br>If set to **undefined**, null, or a negative number, this attribute does not take effect. In this case, the default width of two columns is used.<br>If the value is less than the minimum width 56 vp, the default width of two columns is used. The value must be greater than or equal to 0.<br>**NOTE**<br>This attribute cannot be set in percentage.|
| optionHeight<sup>11+</sup> | [Dimension](ts-types.md#dimension10) | Maximum height of the option in the drop-down list box. The default and maximum value is 80% of the available height of the screen.<br>If set to **undefined**, null, or a negative number, this attribute does not take effect. In this case, the default value is used.<br>The value must be greater than 0 If the actual height of all options in the drop-down list box is less than the preset height, the options are displayed at their actual height.<br>**NOTE**<br>This attribute cannot be set in percentage.|
| menuBackgroundColor<sup>11+</sup> | [ResourceColor](ts-types.md#resourcecolor) | Background color of the drop-down list box.<br>Default value: **Color.Transparent**|
| menuBackgroundBlurStyle<sup>11+</sup> | [BlurStyle](ts-appendix-enums.md#blurstyle9) |  Background blur style of the drop-down list box.<br>Default value: **BlurStyle.COMPONENT_ULTRA_THICK**|

## OptionWidthMode<sup>11+</sup>

| Name       | Description                          |
| ----------- | ------------------------------ |
| FIT_CONTENT | Uses the default width, that is, width of two columns.           |
| FIT_TRIGGER | Inherits the width of the drop-down list button.|

## ArrowPosition<sup>10+</sup>

| Name               | Description              |
| ------------------- | ------------------ |
| END<sup>10+</sup>   | The text is in front of the arrow.|
| START<sup>10+</sup> | The arrow is in front of the text.|


## MenuAlignType<sup>10+</sup>

| Name               | Description              |
| ------------------- | ------------------ |
| START               | Aligned with the start edge in the same direction as the language in use.|
| CENTER              | Aligned with the center.|
| END                 | Aligned with the end edge in the same direction as the language in use.|

## Events

| Name                                                        | Description                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| onSelect(callback: (index: number, value: string) => void) | Invoked when an option in the drop-down list box is selected.<br>**index**: index of the selected option.<br>**value**: value of the selected option.|

##  Example

```ts
// xxx.ets
@Entry
@Component
struct SelectExample {
  @State text: string = "TTTTT"
  @State index: number = 2
  @State space: number = 8
  @State arrowPosition: ArrowPosition = ArrowPosition.END
  build() {
    Column() {
      Select([{ value: 'aaa', icon: $r("app.media.selecticon") },
        { value: 'bbb', icon: $r("app.media.selecticon") },
        { value: 'ccc', icon: $r("app.media.selecticon") },
        { value: 'ddd', icon: $r("app.media.selecticon") }])
        .selected(this.index)
        .value(this.text)
        .font({ size: 16, weight: 500 })
        .fontColor('#182431')
        .selectedOptionFont({ size: 16, weight: 400 })
        .optionFont({ size: 16, weight: 400 })
        .space(this.space)
        .arrowPosition(this.arrowPosition)
        .menuAlign(MenuAlignType.START, {dx:0, dy:0})
        .optionWidth(200)
        .optionHeight(300)
        .onSelect((index:number, text?: string | undefined)=>{
          console.info('Select:' + index)
          this.index = index;
          if(text){
            this.text = text;
          }
        })
    }.width('100%')
  }
}
```

![](figures/selectExample.png)
