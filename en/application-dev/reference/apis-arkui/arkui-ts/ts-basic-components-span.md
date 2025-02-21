# Span

As a child of the [\<Text>](ts-basic-components-text.md) and [\<ContainerSpan>](ts-basic-components-containerspan.md) components, the \<Span> component is used to display inline text.

>  **NOTE**
>
>  This component is supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.
>
>  Since API version 10, this component can inherit the attributes of the **\<Text>** parent component. That is, if no attribute is set for this component, it inherits the attributes (if set) of its parent component. Only the following attributes can be inherited: **fontColor**, **fontSize**, **fontStyle**, **fontWeight**, **decoration**, **letterSpacing**, **textCase**, **fontfamily**, and **textShadow**.


## Child Components

Not supported


## APIs

Span(value: string | Resource)

This API can be used in ArkTS widgets since API version 9.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | string \| [Resource](ts-types.md#resource) | Yes| Plain text.|


## Attributes

Only the [universal text attributes](ts-universal-attributes-text-style.md) are supported.

| Name| Type| Description|
| -------- | -------- | -------- |
| decoration | {<br>type: [TextDecorationType](ts-appendix-enums.md#textdecorationtype),<br>color?: [ResourceColor](ts-types.md#resourcecolor)<br>} | Style and color of the text decorative line.<br>Default value: {<br>type: TextDecorationType.None<br>color: Color.Black<br>} <br>This API can be used in ArkTS widgets since API version 9.|
| letterSpacing       | number \| string  | Letter spacing. A negative value tightens the spacing; a positive value loosens the spacing, and the letters are spread farther apart with the value.<br>This API can be used in ArkTS widgets since API version 9.                               |
| textCase | [TextCase](ts-appendix-enums.md#textcase) | Text case.<br>Default value: **TextCase.Normal**<br>This API can be used in ArkTS widgets since API version 9.|
| lineHeight<sup>10+</sup> | [Length](ts-types.md#length) | Line height of the text.|
| font<sup>10+</sup> | [Font](ts-types.md#font) | Text style, covering the font size, font width, Font family, and font style.|
| textShadow<sup>11+</sup>  |  [ShadowOptions](ts-universal-attributes-image-effect.md#shadowoptions) \| Array&lt;[ShadowOptions](ts-universal-attributes-image-effect.md#shadowoptions)> | Text shadow. It supports input parameters in an array to implement multiple text shadows.<br>**NOTE**<br>This API does not work with the **fill** attribute or coloring strategy.|
| textBackgroundStyle<sup>11+</sup> | [TextBackgroundStyle](ts-basic-components-containerspan.md#textbackgroundstyle)                                                                                           | Background style.<br>Default value:<br>{<br>  color: Color.Transparent,<br>  radius: 0<br>} <br>**NOTE**<br>This attribute prioritizes the value separately set for the component. If it is not set, the component can inherit the settings from its parent [\<ContainerSpan>](ts-basic-components-containerspan.md).|


## Events

Among all the universal events, only the [click event](ts-universal-events-click.md) is supported.

>  **NOTE**
>
>  As the **\<Span>** component does not include size information, the **target** attribute of the **ClickEvent** object returned by the click event is invalid.


## Example
### Example 1
```ts
// xxx.ets
@Entry
@Component
struct SpanExample {
  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Start, justifyContent: FlexAlign.SpaceBetween }) {
      Text('Basic Usage').fontSize(9).fontColor(0xCCCCCC)
      Text() {
        Span('In Line')
        Span(' Component')
        Span(' !')
      }

      Text() {
        Span('This is the Span component').fontSize(12).textCase(TextCase.Normal)
          .decoration({ type: TextDecorationType.None, color: Color.Red })
      }

      // Add a line under the text.
      Text('Text Decoration').fontSize(9).fontColor(0xCCCCCC)
      Text() {
        Span('I am Underline-span').decoration({ type: TextDecorationType.Underline, color: Color.Red }).fontSize(12)
      }

      Text() {
        Span('I am LineThrough-span')
          .decoration({ type: TextDecorationType.LineThrough, color: Color.Red })
          .fontSize(12)
      }

      Text() {
        Span('I am Overline-span').decoration({ type: TextDecorationType.Overline, color: Color.Red }).fontSize(12)
      }

      // Set the letter spacing.
      Text('LetterSpacing').fontSize(9).fontColor(0xCCCCCC)
      Text() {
        Span('span letter spacing')
          .letterSpacing(0)
          .fontSize(12)
      }

      Text() {
        Span('span letter spacing')
          .letterSpacing(-2)
          .fontSize(12)
      }

      Text() {
        Span('span letter spacing')
          .letterSpacing(3)
          .fontSize(12)
      }


      // Set the text case.
      Text('Text Case').fontSize(9).fontColor(0xCCCCCC)
      Text() {
        Span('I am Lower-span').fontSize(12)
          .textCase(TextCase.LowerCase)
          .decoration({ type: TextDecorationType.None })
      }

      Text() {
        Span('I am Upper-span').fontSize(12)
          .textCase(TextCase.UpperCase)
          .decoration({ type: TextDecorationType.None })
      }
    }.width('100%').height(250).padding({ left: 35, right: 35, top: 35 })
  }
}
```

![Span](figures/span.png)

### Example 2
``` ts
@Entry
@Component
struct TextSpanExample {
  @State textShadows : ShadowOptions | Array<ShadowOptions> = [{ radius: 10, color: Color.Red, offsetX: 10, offsetY: 0 },{ radius: 10, color: Color.Black, offsetX: 20, offsetY: 0 },
      { radius: 10, color: Color.Brown, offsetX: 30, offsetY: 0 },{ radius: 10, color: Color.Green, offsetX: 40, offsetY: 0 },
      { radius: 10, color: Color.Yellow, offsetX: 100, offsetY: 0 }]
  build() {
    Column({ space: 8 }) {
      Text() {
        Span('123456789').fontSize(50).textShadow(this.textShadows)
      }
      Text() {
        Span('123456789') // span can inherit text shadow & font size from outer text
      }.fontSize(50).textShadow(this.textShadows)
    }
  }
}
```
![TextshadowExample](figures/text_span_textshadow.png)

### Example 3
``` ts
// xxx.ets
@Component
@Entry
struct Index {
  build() {
    Column() {
      Text() {
        Span('   Hello World !   ')
          .fontSize('20fp')
          .textBackgroundStyle({color: "#7F007DFF", radius: "5vp"})
          .fontColor(Color.White)
      }
    }.width('100%').margin({bottom: '5vp'}).alignItems(HorizontalAlign.Center)
  }
}
```
![TextBackgroundStyleExample](figures/span_textbackgroundstyle.png)
