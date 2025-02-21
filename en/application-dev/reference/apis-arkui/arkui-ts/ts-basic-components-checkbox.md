# Checkbox

The **\<Checkbox>** component is used to enable or disable an option.

>  **NOTE**
>
>  Since API version 11, the default style of the **\<Checkbox>** component is changed from rounded square to circle.
>
>  This component is supported since API version 8. Updates will be marked with a superscript to indicate their earliest API version.

## Child Components

Not supported

## APIs

Checkbox(options?: CheckboxOptions)

Creates a check box.

**Widget capability**: Since API version 9, this feature is supported in ArkTS widgets.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name | Type                                       | Mandatory| Description              |
| ------- | ------------------------------------------- | ---- | ------------------ |
| options | [CheckboxOptions](#checkboxoptions) | No  | Check box parameters.|

## CheckboxOptions

| Name | Type| Mandatory | Description|
| --------| --------| ------ | -------- |
| name    | string | No| Name of the check box.|
| group   | string | No| Group name of the check box (that is, the name of the check box group to which the check box belongs).<br>**NOTE**<br>For the settings to take effect, this parameter must be used with the [CheckboxGroup](ts-basic-components-checkboxgroup.md) component.|

## Attributes

In addition to the [universal attributes](ts-universal-attributes-size.md), the following attributes are supported.


| Name         | Type| Description|
| ------------- | ------- | -------- |
| select        | boolean | Whether the check box is selected.<br>Default value: **false**<br>This API can be used in ArkTS widgets since API version 9.<br>Since API version 10, this attribute supports two-way binding through [$$](../../../quick-start/arkts-two-way-sync.md).|
| selectedColor | [ResourceColor](ts-types.md#resourcecolor) | Color of the check box when it is selected.<br>Default value: **$r('sys.color.ohos_id_color_text_primary_activated')**<br>An invalid value is handled as the default value.<br>This API can be used in ArkTS widgets since API version 9.|
| unselectedColor<sup>10+</sup> | [ResourceColor](ts-types.md#resourcecolor) | Border color of the check box when it is not selected.<br>Default value: **'#33ffffff'**|
| mark<sup>10+</sup> | [MarkStyle](#markstyle10) | Internal icon style of the check box.|
| shape<sup>11+</sup> | [CheckBoxShape](#checkboxshape11) | Shape of the check box.<br>Default value: **CheckBoxShape.CIRCLE**|

## Events

In addition to the [universal events](ts-universal-events-click.md), the following attributes are supported.

| Name                                        | Description                                                    |
| -------------------------------------------- | ------------------------------------------------------------ |
| onChange(callback: (value: boolean) => void) | Triggered when the selected status of the check box changes.<br>- The value **true** means that the check box is selected.<br>- The value **false** means that the check box is not selected.<br>This API can be used in ArkTS widgets since API version 9.|

## MarkStyle<sup>10+</sup>

| Name       | Type                                      | Mandatory| Default Value     | Description                                                        |
| ----------- | ------------------------------------------ | ---- | ----------- | ------------------------------------------------------------ |
| strokeColor | [ResourceColor](ts-types.md#resourcecolor) | No  | Color.White | Color of the internal mark.                                              |
| size        | [Length](ts-types.md#length)               | No  | -           | Size of the internal mark, in vp. The default size is the same as the width of the check box.<br>This parameter cannot be set in percentage. If it is set to an invalid value, the default value is used.|
| strokeWidth | [Length](ts-types.md#length)               | No  | 2           | Stroke width of the internal mark, in vp. This parameter cannot be set in percentage. If it is set to an invalid value, the default value is used.|

## CheckBoxShape<sup>11+</sup>

| Name      | Value| Description    |
| -------------- | ------ | -------- |
| CIRCLE         | 0      | Circle.    |
| ROUNDED_SQUARE | 1      | Rounded square.|

## Example

### Example 1

```ts
// xxx.ets
@Entry
@Component
struct CheckboxExample {
  build() {
    Flex({ justifyContent: FlexAlign.SpaceAround }) {
      Checkbox({ name: 'checkbox1', group: 'checkboxGroup' })
        .select(true)
        .selectedColor(0xed6f21)
        .shape(CheckBoxShape.CIRCLE)
        .onChange((value: boolean) => {
          console.info('Checkbox1 change is' + value)
        })
      Checkbox({ name: 'checkbox2', group: 'checkboxGroup' })
        .select(false)
        .selectedColor(0x39a2db)
        .shape(CheckBoxShape.ROUNDED_SQUARE)
        .onChange((value: boolean) => {
          console.info('Checkbox2 change is' + value)
        })
    }
  }
}
```


![](figures/checkbox.gif)

### Example 2

```ts
// xxx.ets
@Entry
@Component
struct Index {

  build() {
    Row() {
      Column() {
        Flex({ justifyContent: FlexAlign.Center, alignItems: ItemAlign.Center }) {
          Checkbox({ name: 'checkbox1', group: 'checkboxGroup' })
            .selectedColor(0x39a2db)
            .shape(CheckBoxShape.ROUNDED_SQUARE)
            .onChange((value: boolean) => {
              console.info('Checkbox1 change is'+ value)
            })
            .mark({
              strokeColor:Color.Black,
              size: 50,
              strokeWidth: 5
            })
            .unselectedColor(Color.Red)
            .width(30)
            .height(30)
          Text('Checkbox1').fontSize(20)
        }
        Flex({ justifyContent: FlexAlign.Center, alignItems: ItemAlign.Center }) {
          Checkbox({ name: 'checkbox2', group: 'checkboxGroup' })
            .selectedColor(0x39a2db)
            .shape(CheckBoxShape.ROUNDED_SQUARE)
            .onChange((value: boolean) => {
              console.info('Checkbox2 change is' + value)
            })
            .width(30)
            .height(30)
          Text('Checkbox2').fontSize(20)
        }
      }
      .width('100%')
    }
    .height('100%')
  }
}
```


![](figures/checkbox2.gif)
