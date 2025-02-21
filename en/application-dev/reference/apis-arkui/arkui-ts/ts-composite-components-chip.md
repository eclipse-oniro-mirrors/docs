#  @ohos.arkui.advanced.Chip (Chip)

The chip component is typically used in the search box history or email address list.

> **NOTE**
>
> This component is supported since API version 11. Updates will be marked with a superscript to indicate their earliest API version.

## Child Components

Not supported

## Chip

Chip({options:ChipOptions})

**Decorator**: @Builder

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name   | Type                       | Mandatory| Decorator| Description                |
| ------- | --------------------------- | ---- | ---------- | -------------------- |
| options | [ChipOptions](#chipoptions) | Yes  | @Builder   | Parameters of the chip.|

## ChipOptions

Defines the type and style parameters of the chip.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name           | Type                                                        | Mandatory| Description                                                        |
| --------------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| size            | [ChipSize](#chipsize) \| [SizeOptions](ts-types.md#sizeoptions) | No  | Size of the chip.<br>Default value: **ChipSize**: **ChipSize.NORMAL**<br>   If of the SizeOptions type, this parameter cannot be set in percentage.|
| enabled         | boolean                                                      | No  | Whether the chip can be selected.<br>Default value: **true**                        |
| prefixIcon      | [PrefixIconOptions](#prefixiconoptions)                      | No  | Prefix icon of the chip.                                              |
| label           | [LabelOptions](#labeloptions)                                | Yes  | Text of the chip.                                                  |
| suffixIcon      | [SuffixIconOptions](#suffixiconoptions)                      | No  | Suffix icon of the chip.                                              |
| backgroundColor | [ResourceColor](ts-types.md#resourcecolor)                   | No  | Background color of the chip.<br>Default value: **$r('sys.float.ohos_id_color_button_normal')**|
| borderRadius    | [Dimension](ts-types.md#dimension10)                         | No  | Border radius of the chip. This parameter cannot be set in percentage.<br>Default value: **$r('sys.float.ohos_id_corner_radius_button')**|
| allowClose      | boolean                                                      | No  | Whether to show the deletion icon.<br>Default value: **true**                       |
| onClose         | ()=>void                                                     | No  | Event triggered when the close icon is clicked.                                      |

> **NOTE**
>
> 1. If the width set for the chip is less than the minimum width, the chip is displayed at the minimum width.
>
> 2. If **suffixIcon** is specified, **allowClose** has no effect.
>
> 3. If **undefined** is assigned to **backgroundColor**, the default background color is used. If an invalid value is assigned to **backgroundColor**, the background color is transparent.
>
> 4. The default value of **fillColor** is **$r('sys.color.ohos_id_color_secondary')** for **prefixIcon** and **$r('sys.color.ohos_id_color_primary')** for **suffixIcon**. The color parsing of **fillColor** is the same as that of the **\<Image>** component.

## ChipSize

Defines the size type of the chip.

| Name  | Value      | Description              |
| ------ | -------- | ------------------ |
| NORMAL | "NORMAL" | Normal size.|
| SMALL  | "SMALL"  | Small size. |

## IconCommonOptions

Defines the common icon attributes of the chip.

| Name     | Type                                      | Mandatory| Description                                                        |
| --------- | ------------------------------------------ | ---- | ------------------------------------------------------------ |
| src       | [ResourceStr](ts-types.md#resourcestr)     | Yes  | Icon source, which can be a specific image path or an image reference.                                    |
| size      | [SizeOptions](ts-types.md#sizeoptions)     | No  | Icon size. This parameter cannot be set in percentage.<br>Default value: **{width: 16,height: 16}**|
| fillColor | [ResourceColor](ts-types.md#resourcecolor) | No  | Icon fill color.                                              |

> **NOTE**
>
> **fillColor** takes effect only when the icon format is **svg**.


## PrefixIconOptions

Defines the attributes of the prefix icon.

Inherits from [IconCommonOptions](#iconcommonoptions).

## SuffixIconOptions

Defines the attributes of the suffix icon.

Inherits from [IconCommonOptions](#iconcommonoptions).

| Name  | Type      | Mandatory| Description              |
| ------ | ---------- | ---- | ------------------ |
| action | () => void | No  | Action of the suffix icon.|

## LabelOptions

Defines the text attributes of the chip.

| Name       | Type                                      | Mandatory| Description                                                        |
| ----------- | ------------------------------------------ | ---- | ------------------------------------------------------------ |
| text        | string                                     | Yes  | Text content.                                              |
| fontSize    | [Dimension](ts-types.md#dimension10)       | No  | Font size. This parameter cannot be set in percentage.<br>Default value: **$r('sys.float.ohos_id_text_size_button3')**|
| fontColor   | [ResourceColor](ts-types.md#resourcecolor) | No  | Font color.<br>Default value: **$r('sys.color.ohos_id_color_text_primary')**|
| fontFamily  | string                                     | No  | Font family.<br>Default value: **"HarmonyOS Sans"**                   |
| labelMargin | [LabelMarginOptions](#labelmarginoptions)  | No  | Spacing between the text and the left and right icons.                                  |

## LabelMarginOptions

Defines the spacing between the text and the left and right icons.

| Name | Type                                | Mandatory| Description                                                    |
| ----- | ------------------------------------ | ---- | -------------------------------------------------------- |
| left  | [Dimension](ts-types.md#dimension10) | No  | Spacing between the text and the left icon. This parameter cannot be set in percentage.<br>Default value: **6vp**|
| right | [Dimension](ts-types.md#dimension10) | No  | Spacing between the text and the right icon. This parameter cannot be set in percentage.<br>Default value: **6vp**|


## Example

### Example 1

```ts
import { Chip, ChipSize } from '@ohos.arkui.advanced.Chip';

@Entry
@Component
struct Index {
  build() {
    Column({ space: 10 }) {
      Chip({
        prefixIcon: {
          src: $r('app.media.chips'),
          size: { width: 16, height: 16 },
          fillColor: Color.Red,
        },
        label: {
          text: "Chip",
          fontSize: 12,
          fontColor: Color.Blue,
          fontFamily: "HarmonyOS Sans",
          labelMargin: { left: 20, right: 30 },
        },
        suffixIcon: {
          src: $r('app.media.close'),
          size: { width: 16, height: 16 },
          fillColor: Color.Red,
        },
        size: ChipSize.NORMAL,
        allowClose: false,
        enabled: true,
        backgroundColor: $r('sys.color.ohos_id_color_button_normal'),
        borderRadius: $r('sys.float.ohos_id_corner_radius_button')
      })
    }
  }
}
```


![](figures/chip1.png)

### Example 2

```ts
import { Chip, ChipSize } from '@ohos.arkui.advanced.Chip';

@Entry
@Component
struct Index {
  build() {
    Column({ space: 10 }) {
      Chip({
        prefixIcon: {
          src: $r('app.media.chips'),
          size: { width: 16, height: 16 },
          fillColor: Color.Blue,
        },
        label: {
          text: "Chip",
          fontSize: 12,
          fontColor: Color.Blue,
          fontFamily: "HarmonyOS Sans",
          labelMargin: { left: 20, right: 30 },
        },
        size: ChipSize.NORMAL,
        allowClose: true,
        enabled: true,
        backgroundColor: $r('sys.color.ohos_id_color_button_normal'),
        borderRadius: $r('sys.float.ohos_id_corner_radius_button')
      })
    }
  }
}
```


![](figures/chip2.png)

### Example 3

```ts
import { Chip, ChipSize } from '@ohos.arkui.advanced.Chip';

@Entry
@Component
struct Index {
  build() {
    Column({ space: 10 }) {
      Chip({
        prefixIcon: {
          src: $r('app.media.chips'),
          size: { width: 16, height: 16 },
          fillColor: Color.Blue,
        },
        label: {
          text: "Chip",
          fontSize: 12,
          fontColor: Color.Blue,
          fontFamily: "HarmonyOS Sans",
          labelMargin: { left: 20, right: 30 },
        },
        size: ChipSize.SMALL,
        allowClose: false,
        enabled: true,
        backgroundColor: $r('sys.color.ohos_id_color_button_normal'),
        borderRadius: $r('sys.float.ohos_id_corner_radius_button'),
        onClose:()=>{
          console.log("chip on close")
      }
      })
    }
  }
}
```


![](figures/chip3.png)
