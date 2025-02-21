# Text

The **\<Text>** component is used to display a piece of textual information.

>  **NOTE**
>
>  This component is supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.


## Child Components

This component can contain the [\<Span>](ts-basic-components-span.md), [\<ImageSpan>](ts-basic-components-imagespan.md), [\<SymbolSpan>](ts-basic-components-symbolSpan.md), and [\<ContainerSpan>](ts-basic-components-containerspan.md) child components.

## APIs

Text(content?: string | Resource, value?: TextOptions)

This API can be used in ArkTS widgets since API version 9.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| content | string \| [Resource](ts-types.md#resource) | No| Text content. The content and style set for the **\<Text>** component do not take effect when it contains the **\<Span>** child component.<br>Default value: **' '**|
| value<sup>11+</sup> | [TextOptions](#textoptions11) | No| Initialization options of the component.|

## Attributes

In addition to the [universal attributes](ts-universal-attributes-size.md) and [universal text attributes](ts-universal-attributes-text-style.md), the following attributes are supported.

| Name                      | Type                           | Description                                              |
| ----------------------- | ----------------------------------- | ------------------------------------------- |
| textAlign               | [TextAlign](ts-appendix-enums.md#textalign) | Horizontal alignment mode of the text.<br>Default value: **TextAlign.Start**<br>**NOTE**<br/>The text takes up the full width of the **\<Text>** component. To set vertical alignment for the text, use the [align](ts-universal-attributes-location.md) attribute. The **align** attribute alone does not control the horizontal position of the text. In other words, **Alignment.TopStart**, **Alignment.Top**, and **Alignment.TopEnd** produce the same effect, top-aligning the text; **Alignment.Start**, **Alignment.Center**, and **Alignment.End** produce the same effect, centered-aligning the text vertically; **Alignment.BottomStart**, **Alignment.Bottom**, and **Alignment.BottomEnd** produce the same effect, bottom-aligning the text. Yet, it can work with the **textAlign** attribute to jointly determine the horizontal position of the text.<br>When **textAlign** is set to **TextAlign.JUSTIFY**, the text in the last line is horizontally aligned with the start edge.<br>This API can be used in ArkTS widgets since API version 9.|
| textOverflow            | {overflow: [TextOverflow](ts-appendix-enums.md#textoverflow)} | Display mode when the text is too long.<br>Default value: **{overflow: TextOverflow.Clip}**<br>**NOTE**<br>Text is clipped at the transition between words. To clip text in the middle of a word, add **\u200B** between characters. Since API version 11, you are advised to use this attribute with the **wordBreak** attribute set to **WordBreak.BREAK_ALL** so that word breaks can occur between any two characters when overflow occurs. For details, see [Example](#example-4).<br>If **overflow** is set to **TextOverflow.None**, **TextOverflow.Clip**, or **TextOverflow.Ellipsis**, this attribute must be used with **maxLines** for the settings to take effect. **TextOverflow.None** produces the same effect as **TextOverflow.Clip**.<br>If **overflow** is set to **TextOverflow.MARQUEE**, the text scrolls in a line, and neither **maxLines** nor **copyOption** takes effect. In this case, the **\<ImageSpan>** component is not supported, and **textAlign** takes effect only when the text is not scrollable.<br>This API can be used in ArkTS widgets since API version 9.|
| maxLines                | number | Maximum number of lines in the text.<br>**NOTE**<br>By default, text is automatically folded. If this attribute is specified, the text will not exceed the specified number of lines. If there is extra text, you can use **textOverflow** to specify how it is displayed.<br>This API can be used in ArkTS widgets since API version 9.|
| lineHeight              | string \| number \| [Resource](ts-types.md#resource)  | Text line height. If the value is less than or equal to **0**, the line height is not limited and the font size is adaptive. If the value of the number type, the unit fp is used.<br>This API can be used in ArkTS widgets since API version 9.|
| decoration              | {<br>type: [TextDecorationType](ts-appendix-enums.md#textdecorationtype),<br>color?: [ResourceColor](ts-types.md#resourcecolor)<br>} | Style and color of the text decorative line.<br>Default value: {<br>type: TextDecorationType.None,<br>color: Color.Black<br>} <br>This API can be used in ArkTS widgets since API version 9.|
| baselineOffset          | number \| string | Baseline offset of the text. The default value is **0**.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>If this attribute is set to a percentage, the default value is used.|
| letterSpacing           | number \| string | Letter spacing.<br>This API can be used in ArkTS widgets since API version 9.<br>**NOTE**<br>If this attribute is set to a percentage, the default value is used.<br> If this attribute is set to a negative value, the letters will overlap each other.|
| minFontSize             | number \| string \| [Resource](ts-types.md#resource)      | Minimum font size.<br>For the setting to take effect, this attribute must be used together with **maxFontSize** and **maxLines**, or layout constraint settings. It has no effect on child components.<br>When the adaptive font size is used, the **fontSize** settings do not take effect.<br>If the value of **minFontSize** is less than or equal to 0, the adaptive font size does not take effect.<br>This API can be used in ArkTS widgets since API version 9.|
| maxFontSize             | number \| string \| [Resource](ts-types.md#resource)      | Maximum font size.<br>For the setting to take effect, this attribute must be used together with **minFontSize** and **maxLines**, or layout constraint settings. It has no effect on child components.<br>When the adaptive font size is used, the **fontSize** settings do not take effect.<br>This API can be used in ArkTS widgets since API version 9.|
| textCase                | [TextCase](ts-appendix-enums.md#textcase) | Text case.<br>Default value: **TextCase.Normal**<br>This API can be used in ArkTS widgets since API version 9.|
| copyOption<sup>9+</sup> | [CopyOptions](ts-appendix-enums.md#copyoptions9) | Whether copy and paste is allowed.<br>Default value: **CopyOptions.None**<br>This API is supported in ArkTS widgets.<br>**NOTE**<br>When this attribute is set to **CopyOptions.InApp** or **CopyOptions.LocalDevice**, a long press on the text will display a context menu that offers the copy and select-all options.|
| draggable<sup>9+</sup>  | boolean | Drag effect of the selected text.<br>This attribute cannot be used with the [onDragStart](ts-universal-events-drag-drop.md) event.<br>It must be used together with **copyOption**. When it is set to **true** and **copyOptions** is set to **CopyOptions.InApp** or **CopyOptions.LocalDevice**, the selected text can be dragged and copied to the text box.<br>Default value: **false**<br>**NOTE**<br>This API is supported since API version 9.|
| font<sup>10+</sup>  | [Font](ts-types.md#font) | Text style, covering the font size, font width, Font family, and font style.|
| textShadow<sup>10+</sup> | [ShadowOptions](ts-universal-attributes-image-effect.md#shadowoptions) \| Array&lt;[ShadowOptions](ts-universal-attributes-image-effect.md#shadowoptions)&gt;<sup>11+</sup>  | Text shadow.<br>**NOTE**<br>This API does not work with the **fill** attribute or coloring strategy.<br>If the **\<Text>** component's **clip** attribute is set to true (default), the content (for example, text shadow) outside of the component's content area is clipped. Therefore, to fully show the text shadow when the content exceeds the component's content area, set the **clip** attribute to **false**.<br>Since API version 11, this API supports input parameters in an array to implement multiple text shadows.|
| heightAdaptivePolicy<sup>10+</sup> | [TextHeightAdaptivePolicy](ts-appendix-enums.md#textheightadaptivepolicy10) | How the adaptive height is determined for the text.<br>Default value: **TextHeightAdaptivePolicy.MAX_LINES_FIRST**<br>**NOTE**<br/>When this attribute is set to **TextHeightAdaptivePolicy.MAX_LINES_FIRST**, the **maxLines** attribute takes precedence for adjusting the text height. If the **maxLines** setting results in a layout beyond the layout constraints, the text will shrink to a font size between `minFontSize` and `maxFontSize` to allow for more content to be shown.<br>When this attribute is set to **TextHeightAdaptivePolicy.MIN_FONT_SIZE_FIRST**, the **minFontSize** attribute takes precedence for adjusting the text height. If the text can fit in one line with the **minFontSize** setting, the text will enlarge to the largest possible font size between **minFontSize** and **maxFontSize**.<br>When this attribute is set to **TextHeightAdaptivePolicy.LAYOUT_CONSTRAINT_FIRST**, the layout constraints take precedence for adjusting the text height. If the resultant layout is beyond the layout constraints, the text will shrink to a font size between **minFontSize** and **maxFontSize** to respect the layout constraints. If the layout still exceeds the layout constraints after the font size is reduced to **minFontSize**, the lines that exceed the layout constraints are deleted.|
| textIndent<sup>10+</sup> | [Length](ts-types.md#length) | Indentation of the first line.<br>Default value: **0**|
| font<sup>10+</sup> | [Font](ts-types.md#font) | Text style, covering the font size, font width, Font family, and font style.|
| wordBreak<sup>11+</sup> | [WordBreak](ts-appendix-enums.md#wordbreak11) | Line break rule.<br>Default value: **WordBreak.BREAK_WORD**<br>**NOTE**<br>This API can be used in ArkTS widgets since API version 11.<br>When used with **{overflow: TextOverflow.Ellipsis}** and **maxLines**, **WordBreak.BREAK_ALL** can insert line breaks between letters when overflow occurs and display excess content with an ellipsis (...).|
| selection<sup>11+</sup> |(selectionStart: number, selectionEnd: number)| Text selection. The selected text is highlighted, and a selection handle is displayed together with a menu of available actions.<br>Default value: (-1, -1)<br>**NOTE**<br>This API can be used in ArkTS widgets since API version 11.<br>When **copyOption** is set to **CopyOptions.None**, the **selection** attribute is not effective.<br>When **overflow** is set to **TextOverflow.MARQUEE**, the **selection** attribute is not effective.<br>If the value of **selectionStart** is greater than or equal to that of **selectionEnd**, no text will be selected. The value range is [0, textSize], where **textSize** indicates the maximum number of characters in the text content. If the value is less than 0, the value **0** will be used. If the value is greater than **textSize**, **textSize** will be used.<br>If value of **selectionStart** or **selectionEnd** falls within the invisible area, no text will be selected. If clipping is disabled, the text selection outside of the parent component takes effect.|
| ellipsisMode<sup>11+</sup> |[EllipsisMode](ts-appendix-enums.md#ellipsismode11)| Ellipsis position.<br>Default value: **EllipsisMode.END**<br>**NOTE**<br/>This API can be used in ArkTS widgets since API version 11.<br>For the settings to work, **overflow** must be set to **TextOverflow.Ellipsis** and **maxLines** must be specified. Setting **ellipsisMode** alone does not take effect.<br>**EllipsisMode.START** and **EllipsisMode.CENTER** take effect only when text overflows in a single line. |
| enableDataDetector<sup>11+</sup> |boolean| Whether to enable text recognition.<br>Default value: **false**<br>**NOTE**<br>The recognized entity is in the following style settings:<br>fontColor: Color.Blue<br>decoration: {<br>type: TextDecorationType.Underline,<br>color: Color.Blue<br>}<br>For this API to work, the target device must provide the text recognition capability.<br>When **enableDataDetector** is set to **true** and **dataDetectorConfig** is not set, all types of entities are recognized by default.<br>When **copyOption** is set to **CopyOptions.None**, this API does not take effect.|
| dataDetectorConfig<sup>11+</sup> | [TextDataDetectorConfig](#textdatadetectorconfig11) | Text recognition configuration.<br>Default value: {<br>types: [ ],<br>onDetectResultUpdate: null<br>} <br>**NOTE**<br>This API must be used together with **enableDataDetector**. It takes effect only when **enableDataDetector** is set to **true**.<br>When entities A and B overlap, the following rules are followed:<br>1. If A  ⊂ B, retain B. Otherwise, retain A.<br>2. When A ⊄ B and B ⊄ A: If A.start < B.start, retain A; otherwise, retain B.|
| bindSelectionMenu<sup>11+</sup> | {<br>spantype: [TextSpanType](ts-appendix-enums.md#textspantype11),<br>content: [CustomBuilder](ts-types.md#custombuilder8),<br>responseType: [TextResponseType](ts-appendix-enums.md#textresponsetype11) \,<br>options?: [SelectionMenuOptions](ts-appendix-enums.md#selectionmenuoptions11)<br>} | Custom context menu on text selection.<br> Default value: {<br>  spanType: TextSpanType.TEXT<br>**content**: null<br>responseType: TextResponseType.LONG_PRESS <br>}<br>**NOTE**<br/>The duration required for a long-press gesture is 600 ms for **bindSelectionMenu** and 800 ms for **bindContextMenu**. When both **bindSelectionMenu** and **bindContextMenu** are set and both are configured to be triggered by a long-press gesture, **bindSelectionMenu** is triggered first.<br>If the custom menu is too long, embed a [\<Scroll>](./ts-container-scroll.md) component to prevent the keyboard from being blocked. |

>  **NOTE**
>
>  The **\<Text>** component cannot contain both text and the child component **\<Span>** or **\<ImageSpan>**. If both of them exist, only the content in **\<Span>** or **\<ImageSpan>** is displayed.
>
>  The typesetting engine rounds down the value of [width](ts-universal-attributes-size.md#width) to ensure that the value is an integer. If the typesetting engine rounds up the value instead, the right side of the text may be clipped.
>
> When multiple **\<Text>** components are placed in the [\<Row>](ts-container-row.md) container with no specific layout or space allocation settings configured, the components are laid out based on the maximum size of the container. To make sure the sum of the components' main axis sizes does not exceed the main axis size of the container, you can set [layoutWeight](ts-universal-attributes-size.md#layoutweight) or use the [flex layout](ts-universal-attributes-flex-layout.md).

## TextDataDetectorConfig<sup>11+</sup>
| Name| Type | Mandatory| Description |
| ------ | -------- | ---- | ------------------------------------------- |
| types   | [TextDataDetectorType](ts-appendix-enums.md#textdatadetectortype11) | Yes  | Entity types for text recognition. Values **null** and **[]** indicate that all types of entities can be recognized.|
| onDetectResultUpdate   | (callback:(result: string) => void) | Yes  | Callback invoked when text recognition succeeds.<br>- **result**: text recognition result, in JSON format.|

## Events

In addition to the [universal events](ts-universal-events-click.md), the following events are supported.

| Name                                                        | Description                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| onCopy(callback:(value: string) =&gt; void)<sup>11+</sup> | Triggered when data is copied to the pasteboard, which is displayed when the text box is long pressed.<br>**value**: text to be copied.<br>**NOTE**<br>This API can be used in ArkTS widgets since API version 11.<br>Currently, only text can be copied.|
| onTextSelectionChange(callback: (selectionStart: number, selectionEnd: number) => void)<sup>11+</sup> | Triggered when the text selection position changes.<br>**selectionStart**: start position of the text selection area. The start position of text in the text box is **0**.<br>**selectionEnd**: end position of the text selection area.|

## TextOptions<sup>11+</sup>

Describes the initialization options of the **\<Text>** component.

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| controller | [TextController](#textcontroller11)  | Yes| Text controller.|

## TextController<sup>11+</sup>

Defines the controller of the **\<Text>** component.

### Objects to Import

```
controller: TextController = new TextController()
```

### closeSelectionMenu

closeSelectionMenu(): void

Closes the custom or default context menu on selection.

## Example

### Example 1

This example shows how to set the **textAlign**, **maxLines**, **textOverflow**, and **lineHeight** attributes.

```ts
// xxx.ets
@Extend(Text)
function style(TextAlign: TextAlign) {
  .textAlign(TextAlign)
  .fontSize(12)
  .border({ width: 1 })
  .padding(10)
  .width('100%')
}

@Entry
@Component
struct TextExample1 {
  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Start, justifyContent: FlexAlign.SpaceBetween }) {
      // Set the horizontal alignment for the text.
      // Single-line text
      Text('textAlign').fontSize(9).fontColor(0xCCCCCC)
      Text('TextAlign set to Center.')
        .style(TextAlign.Center)
      Text('TextAlign set to Start.')
        .style(TextAlign.Start)
      Text('TextAlign set to End.')
        .style(TextAlign.End)

      // Multi-line text
      Text('This is the text content with textAlign set to Center.')
        .style(TextAlign.Center)
      Text('This is the text content with textAlign set to Start.')
        .style(TextAlign.Start)
      Text('This is the text content with textAlign set to End.')
        .style(TextAlign.End)


      // Set the display mode when the text is too long.
      Text('TextOverflow+maxLines').fontSize(9).fontColor(0xCCCCCC)
      // Clip the text when the value of maxLines is exceeded.
      Text('This is the setting of textOverflow to Clip text content This is the setting of textOverflow to None text content. This is the setting of textOverflow to Clip text content This is the setting of textOverflow to None text content.')
        .textOverflow({ overflow: TextOverflow.Clip })
        .maxLines(1)
        .style(TextAlign.Start)

      // Show an ellipsis (...) when the value of maxLines is exceeded.
      Text('This is set textOverflow to Ellipsis text content This is set textOverflow to Ellipsis text content.')
        .textOverflow({ overflow: TextOverflow.Ellipsis })
        .maxLines(1)
        .style(TextAlign.Start)

      Text('lineHeight').fontSize(9).fontColor(0xCCCCCC)
      Text('This is the text with the line height set. This is the text with the line height set.')
        .style(TextAlign.Start)
      Text('This is the text with the line height set. This is the text with the line height set.')
        .style(TextAlign.Start)
        .lineHeight(20)
    }.height(600).width(340).padding({ left: 35, right: 35, top: 35 })
  }
}
```
![textExp1](figures/textExp1.png)

### Example 2

This example shows how to set the **decoration**, **baselineOffset**, **letterSpacing**, and **textCase** attributes.

```ts
@Extend(Text)
function style() {
  .fontSize(12)
  .border({ width: 1 })
  .padding(10)
  .width('100%')
}

@Entry
@Component
struct TextExample2 {
  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Start, justifyContent: FlexAlign.SpaceBetween }) {
      Text('decoration').fontSize(9).fontColor(0xCCCCCC)
      Text('This is the text content with the decoration set to LineThrough and the color set to Red.')
        .decoration({
          type: TextDecorationType.LineThrough,
          color: Color.Red
        })
        .style()

      Text('This is the text content with the decoration set to Overline and the color set to Red.')
        .decoration({
          type: TextDecorationType.Overline,
          color: Color.Red,
          style: TextDecorationStyle.DOTTED
        })
        .style()

      Text('This is the text content with the decoration set to Underline and the color set to Red.')
        .decoration({
          type: TextDecorationType.Underline,
          color: Color.Red,
          style: TextDecorationStyle.WAVY
        })
        .style()

      // Set the offset of the text baseline.
      Text('baselineOffset').fontSize(9).fontColor(0xCCCCCC)
      Text('This is the text content with baselineOffset 0.')
        .baselineOffset(0)
        .style()
      Text('This is the text content with baselineOffset 30.')
        .baselineOffset(30)
        .style()
      Text('This is the text content with baselineOffset -20.')
        .baselineOffset(-20)
        .style()

      // Set the letter spacing.
      Text('letterSpacing').fontSize(9).fontColor(0xCCCCCC)
      Text('This is the text content with letterSpacing 0.')
        .letterSpacing(0)
        .style()
      Text('This is the text content with letterSpacing 3.')
        .letterSpacing(3)
        .style()
      Text('This is the text content with letterSpacing -1.')
        .letterSpacing(-1)
        .style()

      Text('textCase').fontSize(9).fontColor(0xCCCCCC)
      Text('This is the text content with textCase set to Normal.')
        .textCase(TextCase.Normal)
        .style()
      // Display the text in lowercase.
      Text('This is the text content with textCase set to LowerCase.')
        .textCase(TextCase.LowerCase)
        .style()
      // Display the text in uppercase.
      Text('This is the text content with textCase set to UpperCase.')
        .textCase(TextCase.UpperCase)
        .style()

    }.height(700).width(350).padding({ left: 35, right: 35, top: 35 })
  }
}
```
![textExp1](figures/textExp2.png)

### Example 3

This example shows how to use **textShadow**, **heightAdaptivePolicy**, and **TextOverflow.MARQUEE**.

```ts
@Extend(Text)
function style(HeightAdaptivePolicy: TextHeightAdaptivePolicy) {
  .width('80%')
  .height(90)
  .borderWidth(1)
  .minFontSize(10)
  .maxFontSize(30)
  .maxLines(2)
  .textOverflow({ overflow: TextOverflow.Ellipsis })
  .heightAdaptivePolicy(HeightAdaptivePolicy)
}

@Entry
@Component
struct TextExample3 {
  build() {
    Column({ space: 8 }) {
      Text('textShadow').fontSize(9).fontColor(0xCCCCCC).margin(15).width('90%')
      // Set the text shadow.
      Text('textShadow')
        .width('80%')
        .height(55)
        .fontSize(40)
        .lineHeight(55)
        .textAlign(TextAlign.Center)
        .textShadow({
          radius: 10,
          color: Color.Black,
          offsetX: 0,
          offsetY: 0
        })
        .borderWidth(1)
      Divider()
      // Set how the adaptive height is determined for the text.
      Text('heightAdaptivePolicy').fontSize(9).fontColor(0xCCCCCC).margin(15).width('90%')
      Text('This is the text with the height adaptive policy set')
        .style(TextHeightAdaptivePolicy.MAX_LINES_FIRST)
      Text('This is the text with the height adaptive policy set')
        .style(TextHeightAdaptivePolicy.MIN_FONT_SIZE_FIRST)
      Text('This is the text with the height adaptive policy set')
        .style(TextHeightAdaptivePolicy.LAYOUT_CONSTRAINT_FIRST)
      Divider()
      Text('marquee').fontSize(9).fontColor(0xCCCCCC).margin(15).width('90%')
      // Set the text to continuously scroll when text overflow occurs.
      Text('This is the text with the text overflow set marquee')
        .width(300)
        .borderWidth(1)
        .textOverflow({ overflow: TextOverflow.MARQUEE })
    }
  }
}
```

![](figures/text_3.gif)

### Example 4
This example shows how to use **ellipsisMode** and **wordBreak**.

```ts
// xxx.ets
@Entry
@Component
struct TextExample4 {
  @State text: string =
    'The text component is used to display a piece of textual information.Support universal attributes and universal text attributes.'
  @State ellipsisModeIndex: number = 0;
  @State ellipsisMode: EllipsisMode[] = [EllipsisMode.START, EllipsisMode.CENTER, EllipsisMode.END]
  @State ellipsisModeStr: string[] = ['START', 'CENTER', 'END']
  @State wordBreakIndex: number = 0;
  @State wordBreak: WordBreak[] = [WordBreak.NORMAL, WordBreak.BREAK_ALL, WordBreak.BREAK_WORD]
  @State wordBreakStr: string[] = ['NORMAL', 'BREAK_ALL', 'BREAK_WORD']
  @State textClip: boolean = false

  build() {
    Column({ space: 10 }) {
      Text(this.text)
        .fontSize(16)
        .border({ width: 1 })
        .lineHeight(20)
        .maxLines(1)
        .textOverflow({ overflow: TextOverflow.Ellipsis })
        .ellipsisMode(this.ellipsisMode[this.ellipsisModeIndex])
        .width(300)
        .margin({ left: 20, top: 20 })

      Row() {
        Button('Change Ellipsis Position:' + this.ellipsisModeStr[this.ellipsisModeIndex]).onClick (() => {
          this.ellipsisModeIndex++
          if (this.ellipsisModeIndex > (this.ellipsisModeStr.length - 1)) {
            this.ellipsisModeIndex = 0
          }
        })
      }

      Text('This is set wordBreak to WordBreak text Taumatawhakatangihangakoauauotamateaturipukakapikimaungahoronukupokaiwhenuakitanatahu.')
        .fontSize(12)
        .border({ width: 1 })
        .wordBreak(WordBreak.NORMAL)
        .lineHeight(20)
        .maxLines(2)
        .clip(this.textClip)
        .width(260)
      Row() {
        Button('Change Clip Mode: ' + this.textClip).onClick(() => {
          this.textClip = !this.textClip
        })
      }

      Text(this.text)
        .fontSize(12)
        .border({ width: 1 })
        .maxLines(2)
        .textOverflow({ overflow: TextOverflow.Ellipsis })
        .wordBreak(this.wordBreak[this.wordBreakIndex])
        .lineHeight(20)
        .width(260)
      Row() {
        Button('Change wordBreak Mode: ' + this.wordBreakStr[this.wordBreakIndex]).onClick(() => {
          this.wordBreakIndex++
          if (this.wordBreakIndex > (this.wordBreakStr.length - 1)) {
            this.wordBreakIndex = 0
          }
        })
      }
    }
  }
}
```
![](figures/textExample4.gif)

### Example 5
This example shows how to use **selection** and **onCopy**.

```ts
@Entry
@Component
struct TextExample5 {
  @State onCopy: string = ''
  @State text: string = 'This is set selection to Selection text content This is set selection to Selection text content.'
  @State start: number = 0
  @State end: number = 20

  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Start, justifyContent: FlexAlign.Start }) {
      Text(this.text)
        .fontSize(12)
        .border({ width: 1 })
        .lineHeight(20)
        .margin(30)
        .copyOption(CopyOptions.InApp)
        .selection(this.start, this.end)
        .onCopy((value: string) => {
          this.onCopy = value
        })
      Button('Set text selection')
        .margin({left:20})
        .onClick(() => {
          // Change the start point and end point of the text selection.
          this.start = 10
          this.end = 30
        })
      Text(this.onCopy).fontSize(12).margin(10).key('copy')
    }.height(600).width(335).padding({ left: 35, right: 35, top: 35 })
  }
}
```
![](figures/textExample5.png)

### Example 6
This example shows how to use **enableDataDetector** and **dataDetectorConfig**.

```ts
@Entry
@Component
struct TextExample6 {
  @State phoneNumber: string = '(86) (755) ********';
  @State url: string = 'www.********.com';
  @State email: string = '***@example.com';
  @State address: string = 'XX (province) XX (city) XX (county) XXXX';
  @State enableDataDetector: boolean = true;
  @State types: TextDataDetectorType[] = [];

  build() {
    Row() {
      Column() {
        Text(
          'Phone number:' + this.phoneNumber + '\n' +
          'URL:' + this.url + '\n' +
          'Email:' + this.email + '\n' +
          'Address:' + this.address
        )
          .fontSize(16)
          .copyOption(CopyOptions.InApp)
          .enableDataDetector(this.enableDataDetector)
          .dataDetectorConfig({types : this.types, onDetectResultUpdate: (result: string)=>{}})
          .textAlign(TextAlign.Center)
          .borderWidth(1)
          .padding(10)
          .width('100%')
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

![](figures/text7.png)

### Example 7
This example shows how to use **bindSelectionMenu**, **onTextSelectionChange**, and **closeSelectionMenu**.

```ts
@Entry
@Component
struct TextExample7 {
  controller: TextController = new TextController();
  options: TextOptions = { controller: this.controller };

  build() {
    Column() {
      Column() {
        Text(undefined, this.options) {
          Span('Hello World')
          ImageSpan($r('app.media.icon'))
            .width('100px')
            .height('100px')
            .objectFit(ImageFit.Fill)
            .verticalAlign(ImageSpanAlignment.CENTER)
        }
        .copyOption(CopyOptions.InApp)
        .bindSelectionMenu(TextSpanType.IMAGE, this.LongPressImageCustomMenu, TextResponseType.LONG_PRESS, {
          onDisappear: () => {
            console.info(`Triggered when the custom context menu on selection is closed.`);
          },
          onAppear: () => {
            console.info(`Triggered when the custom context menu on selection is displayed`);
          }
        })
        .bindSelectionMenu(TextSpanType.TEXT, this.RightClickTextCustomMenu, TextResponseType.RIGHT_CLICK)
        .bindSelectionMenu(TextSpanType.MIXED, this.SelectMixCustomMenu, TextResponseType.SELECT)
        .onTextSelectionChange((selectionStart: number, selectionEnd: number) => {
          console.info(`Triggered when the text selection position changes, selectionStart: ${selectionStart}, selectionEnd: ${selectionEnd}`);
        })
        .borderWidth(1)
        .borderColor(Color.Red)
        .width(200)
        .height(100)
      }
      .width('100%')
      .backgroundColor(Color.White)
      .alignItems(HorizontalAlign.Start)
      .padding(25)
    }
    .height('100%')
  }

  @Builder
  RightClickTextCustomMenu() {
    Column() {
      Menu() {
        MenuItemGroup() {
          MenuItem({ startIcon: $r('app.media.app_icon'), content: "Right Click Menu 1", labelInfo: "" })
            .onClick((event) => {
              this.controller.closeSelectionMenu();
            })
          MenuItem({ startIcon: $r('app.media.app_icon'), content: "Right Click Menu 2", labelInfo: "" })
          MenuItem({ startIcon: $r('app.media.app_icon'), content: "Right Click Menu 3", labelInfo: "" })
        }
      }
      .MenuStyles()
    }
  }

  @Builder
  LongPressImageCustomMenu() {
    Column() {
      Menu() {
        MenuItemGroup() {
          MenuItem({ startIcon: $r('app.media.app_icon'), content: "Long Press Image Menu 1", labelInfo: "" })
            .onClick((event) => {
              this.controller.closeSelectionMenu();
            })
          MenuItem({ startIcon: $r('app.media.app_icon'), content: "Long Press Image Menu 2", labelInfo: "" })
          MenuItem({ startIcon: $r('app.media.app_icon'), content: "Long Press Image Menu 3", labelInfo: "" })
        }
      }
      .MenuStyles()
    }
  }

  @Builder
  SelectMixCustomMenu() {
    Column() {
      Menu() {
        MenuItemGroup() {
          MenuItem({ startIcon: $r('app.media.app_icon'), content: "Select Mixed Menu 1", labelInfo: "" })
            .onClick((event) => {
              this.controller.closeSelectionMenu();
            })
          MenuItem({ startIcon: $r('app.media.app_icon'), content: "Select Mixed Menu 2", labelInfo: "" })
          MenuItem({ startIcon: $r('app.media.app_icon'), content: "Select Mixed Menu 3", labelInfo: "" })
        }
      }
      .MenuStyles()
    }
  }
}

@Extend(Menu)
function MenuStyles() {
  .radius($r('sys.float.ohos_id_corner_radius_card'))
  .clip(true)
  .backgroundColor('#F0F0F0')
}
```

![](figures/textBindSelectionMenu.gif)
