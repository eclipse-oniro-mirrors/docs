# ImageSpan


As a child of the [\<Text>](ts-basic-components-text.md) and [\<ContainerSpan>](ts-basic-components-containerspan.md) components, the **\<ImageSpan>** component is used to display inline images.

>  **NOTE**
>
>  This component is supported since API version 10. Updates will be marked with a superscript to indicate their earliest API version.


## Child Components

Not supported


## APIs

ImageSpan(value: ResourceStr | PixelMap)

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| value | [ResourceStr](ts-types.md#resourcestr) \| [PixelMap](../../apis-image-kit/js-apis-image.md#pixelmap7)  | Yes| Image source. Both local and online images are supported.<br>When using an image referenced using a relative path, for example, **ImageSpan("common/test.jpg")**, the **\<ImageSpan>** component cannot be called across bundles or modules. Therefore, you are advised to use **\$r** to reference image resources that need to be used globally.<br>\- The following image formats are supported: PNG, JPG, BMP, SVG, GIF.<br>\- Base64 strings are supported. The value format is data:image/[png\|jpeg\|bmp\|webp];base64,[base64 data], where [base64 data] is a Base64 string.<br>\- Strings with the **file:///data/storage** prefix are supported, which are used to read image resources in the **files** folder in the installation directory of the application. Ensure that the application has the read permission to the files in the specified path.|


## Attributes

The [universal attribute](ts-universal-attributes-size.md) methods can be used to set the size, background, and border.

| Name| Type| Description|
| -------- | -------- | -------- |
| verticalAlign | [ImageSpanAlignment](#imagespanalignment) | Alignment mode of the image with the text.<br>Default value: **ImageSpanAlignment.BOTTOM**|
| objectFit | [ImageFit](ts-appendix-enums.md#imagefit) | Image scale type.<br>Default value: **ImageFit.Cover**|
| textBackgroundStyle<sup>11+</sup> | [TextBackgroundStyle](ts-basic-components-containerspan.md#textbackgroundstyle)                                                                                           | Background style.<br>Default value:<br> {<br>  color: Color.Transparent,<br>  radius: 0<br>} <br>**NOTE**<br>This attribute prioritizes the value separately set for the component. If it is not set, the component can inherit the settings from its parent [\<ContainerSpan>](ts-basic-components-containerspan.md). |

## ImageSpanAlignment

| Name    | Description                          |
| -------- | ------------------------------ |
| TOP      | The image is aligned with the top edge of the line box.  |
| CENTER   | The image is aligned with the center of the line box.      |
| BOTTOM   | The image is aligned with the bottom edge of the line box.  |
| BASELINE | The image is bottom aligned with the text baseline.|

## Events

Among all the universal events, only the [click event](ts-universal-attributes-click.md) is supported.

## Example

### Example 1
```ts
// xxx.ets
@Entry
@Component
struct SpanExample {
  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Text() {
        Span('This is the Span and ImageSpan component').fontSize(25).textCase(TextCase.Normal)
          .decoration({ type: TextDecorationType.None, color: Color.Pink })
      }.width('100%').textAlign(TextAlign.Center)

      Text() {
        ImageSpan($r('app.media.icon'))
          .width('200px')
          .height('200px')
          .objectFit(ImageFit.Fill)
          .verticalAlign(ImageSpanAlignment.CENTER)
        Span('I am LineThrough-span')
          .decoration({ type: TextDecorationType.LineThrough, color: Color.Red }).fontSize(25)
        ImageSpan($r('app.media.icon'))
          .width('50px')
          .height('50px')
          .verticalAlign(ImageSpanAlignment.TOP)
        Span('I am Underline-span')
          .decoration({ type: TextDecorationType.Underline, color: Color.Red }).fontSize(25)
        ImageSpan($r('app.media.icon'))
          .size({ width: '100px', height: '100px' })
          .verticalAlign(ImageSpanAlignment.BASELINE)
        Span('I am Underline-span')
          .decoration({ type: TextDecorationType.Underline, color: Color.Red }).fontSize(25)
        ImageSpan($r('app.media.icon'))
          .width('70px')
          .height('70px')
          .verticalAlign(ImageSpanAlignment.BOTTOM)
        Span('I am Underline-span')
          .decoration({ type: TextDecorationType.Underline, color: Color.Red }).fontSize(50)
      }
      .width('100%')
      .textIndent(50)
    }.width('100%').height('100%').padding({ left: 0, right: 0, top: 0 })
  }
}
```

![imagespan](figures/imagespan.png)

### Example 2
```ts
// xxx.ets
@Component
@Entry
struct Index {
  build() {
    Column() {
      Text() {
        ImageSpan($r('app.media.app_icon'))
          .width('60vp')
          .height('60vp')
          .verticalAlign(ImageSpanAlignment.CENTER)
          .textBackgroundStyle({color: Color.Green, radius: "5vp"})
      }
    }.width('100%').alignItems(HorizontalAlign.Center)
  }
}
```
![imagespan](figures/image_span_textbackgroundstyle.png)
