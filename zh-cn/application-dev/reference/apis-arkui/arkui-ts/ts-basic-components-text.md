# Text

显示一段文本的组件。

>  **说明：**
>
>  该组件从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


## 子组件

可以包含[Span](ts-basic-components-span.md)、[ImageSpan](ts-basic-components-imagespan.md)、[SymbolSpan](ts-basic-components-symbolSpan.md)和[ContainerSpan](ts-basic-components-containerspan.md)子组件。

## 接口

Text(content?: string | Resource, value?: TextOptions)

从API version 9开始，该接口支持在ArkTS卡片中使用。

**参数：**

| 参数名 | 参数类型 | 必填 | 参数描述 |
| -------- | -------- | -------- | -------- |
| content | string \| [Resource](ts-types.md#resource) | 否 | 文本内容。包含子组件Span时不生效，显示Span内容，并且此时text组件的样式不生效。<br/>默认值：' ' |
| value<sup>11+</sup> | [TextOptions](#textoptions11) | 否 | 文本组件初始化选项。|

## 属性

除支持[通用属性](ts-universal-attributes-size.md)和[文本通用属性](ts-universal-attributes-text-style.md)外，还支持以下属性：

| 名称                       | 参数类型                            | 描述                                               |
| ----------------------- | ----------------------------------- | ------------------------------------------- |
| textAlign               | [TextAlign](ts-appendix-enums.md#textalign) | 设置文本段落在水平方向的对齐方式。<br/>默认值：TextAlign.Start<br/>**说明：**<br/>文本段落宽度占满Text组件宽度；可通过[align](ts-universal-attributes-location.md)属性控制文本段落在垂直方向上的位置，此组件中不可通过align属性控制文本段落在水平方向上的位置，即align属性中Alignment.TopStart、Alignment.Top、Alignment.TopEnd效果相同，控制内容在顶部，Alignment.Start、Alignment.Center、Alignment.End效果相同，控制内容垂直居中，Alignment.BottomStart、Alignment.Bottom、Alignment.BottomEnd效果相同，控制内容在底部。结合TextAlign属性可控制内容在水平方向的位置。<br/>当`textAlign`属性设置为TextAlign.JUSTIFY时，最后一行文本不参与两端对齐，为水平对齐首部效果。<br/>从API version 9开始，该接口支持在ArkTS卡片中使用。 |
| textOverflow            | {overflow:&nbsp;[TextOverflow](ts-appendix-enums.md#textoverflow)} | 设置文本超长时的显示方式。<br/>默认值：{overflow:&nbsp;TextOverflow.Clip}<br/>**说明：**<br/>文本截断是按字截断。例如，英文以单词为最小单位进行截断，若需要以字母为单位进行截断，可在字母间添加零宽空格：\u200B。从API version 11开始，建议优先组合`wordBreak`属性设置为WordBreak.BREAK_ALL方式实现字母为单位进行截断，使用[示例](#示例4)。<br />当`overflow`设置为TextOverflow.None、TextOverflow.Clip、TextOverflow.Ellipsis时，需配合`maxLines`使用，单独设置不生效。设置TextOverflow.None与TextOverflow.Clip效果一样。<br/>当`overflow`设置为TextOverflow.MARQUEE时，文本在一行内滚动显示，设置`maxLines`及`copyOption`属性均不生效，此时不支持ImageSpan组件，并且在文本不可滚动时，设置`textAlign`属性生效；在文本可滚动时，设置`textAlign`属性不生效。在跑马灯模式下，Text组件clip属性默认为true。<br/>从API version 9开始，该接口支持在ArkTS卡片中使用。 |
| maxLines                | number | 设置文本的最大行数。<br />**说明：** <br />默认情况下，文本是自动折行的，如果指定此参数，则文本最多不会超过指定的行。如果有多余的文本，可以通过        `textOverflow`来指定截断方式。<br/>从API version 9开始，该接口支持在ArkTS卡片中使用。 |
| lineHeight              | string&nbsp;\|&nbsp;number&nbsp;\|&nbsp;[Resource](ts-types.md#resource)  | 设置文本的文本行高，设置值不大于0时，不限制文本行高，自适应字体大小，Length为number类型时单位为fp。<br/>从API version 9开始，该接口支持在ArkTS卡片中使用。 |
| decoration              | {<br/>type:&nbsp;[TextDecorationType](ts-appendix-enums.md#textdecorationtype),<br/>color?:&nbsp;[ResourceColor](ts-types.md#resourcecolor)<br/>} | 设置文本装饰线样式及其颜色。<br />默认值：{<br/>type:&nbsp;TextDecorationType.None,<br/>color：Color.Black<br/>} <br/>从API version 9开始，该接口支持在ArkTS卡片中使用。|
| baselineOffset          | number&nbsp;\|&nbsp;string | 设置文本基线的偏移量，默认值0。  <br/>从API version 9开始，该接口支持在ArkTS卡片中使用。<br/>**说明：** <br/>设置该值为百分比时，按默认值显示。 |
| letterSpacing           | number&nbsp;\|&nbsp;string | 设置文本字符间距。<br/>从API version 9开始，该接口支持在ArkTS卡片中使用。<br/>**说明：** <br/>设置该值为百分比时，按默认值显示。<br /> 当取值为负值时，文字会发生压缩，负值过小时会将组件内容区大小压缩为0，导致无内容显示。 |
| minFontSize             | number&nbsp;\|&nbsp;string&nbsp;\|&nbsp;[Resource](ts-types.md#resource)      | 设置文本最小显示字号。<br/>需配合maxFontSize以及maxline或布局大小限制使用，单独设置不生效，对子组件不生效。<br/>自适应字号生效时，fontSize设置不生效。<br/>minFontSize小于或等于0时，自适应字号不生效。<br/>从API version 9开始，该接口支持在ArkTS卡片中使用。|
| maxFontSize             | number&nbsp;\|&nbsp;string&nbsp;\|&nbsp;[Resource](ts-types.md#resource)      | 设置文本最大显示字号。<br/>需配合minFontSize以及maxline或布局大小限制使用，单独设置不生效，对子组件不生效。<br/>自适应字号生效时，fontSize设置不生效。 <br/>从API version 9开始，该接口支持在ArkTS卡片中使用。|
| textCase                | [TextCase](ts-appendix-enums.md#textcase) | 设置文本大小写。<br />默认值：TextCase.Normal <br/>从API version 9开始，该接口支持在ArkTS卡片中使用。|
| copyOption<sup>9+</sup> | [CopyOptions](ts-appendix-enums.md#copyoptions9) | 组件支持设置文本是否可复制粘贴。<br />默认值：CopyOptions.None <br/>该接口支持在ArkTS卡片中使用。<br>**说明：** <br/>设置copyOptions为CopyOptions.InApp或者CopyOptions.LocalDevice，长按文本，会弹出文本选择菜单，可选中文本并进行复制、全选操作。<br/>由于卡片没有长按事件，此场景下长按文本，不会弹出文本选择菜单。 |
| draggable<sup>9+</sup>  | boolean | 设置选中文本拖拽效果。<br/>不能和[onDragStart](ts-universal-events-drag-drop.md)事件同时使用；<br/>需配合copyOption一起使用，设置copyOptions为CopyOptions.InApp或者CopyOptions.LocalDevice，并且draggable设置为true时，支持对选中文本的拖拽以及选中内容复制到输入框。<br/>默认值：false <br />**说明：**<br />从 API version 9 开始支持。 |
| font<sup>10+</sup>  | [Font](ts-types.md#font) | 设置文本样式。包括字体大小、字体粗细、字体族和字体风格。 |
| textShadow<sup>10+</sup> | [ShadowOptions](ts-universal-attributes-image-effect.md#shadowoptions对象说明)&nbsp;\|&nbsp;Array&lt;[ShadowOptions](ts-universal-attributes-image-effect.md#shadowoptions对象说明)&gt;<sup>11+</sup>  | 设置文字阴影效果。<br/>**说明：**<br/>不支持fill字段,不支持智能取色模式。<br/>从API version 11开始，该接口支持以数组形式入参，实现多重文字阴影。|
| heightAdaptivePolicy<sup>10+</sup> | [TextHeightAdaptivePolicy](ts-appendix-enums.md#textheightadaptivepolicy10) | 设置文本自适应高度的方式。<br/>默认值：TextHeightAdaptivePolicy.MAX_LINES_FIRST。<br/>**说明：**<br/>当设置为TextHeightAdaptivePolicy.MAX_LINES_FIRST时，优先使用`maxLines`属性来调整文本高度。如果使用`maxLines`属性的布局大小超过了布局约束，则尝试在`minFontSize`和`maxFontSize`的范围内缩小字体以显示更多文本。<br/>当设置为TextHeightAdaptivePolicy.MIN_FONT_SIZE_FIRST时，优先使用`minFontSize`属性来调整文本高度。如果使用`minFontSize`属性可以将文本布局在一行中，则尝试在`minFontSize`和`maxFontSize`的范围内增大字体并使用最大可能的字体大小。<br/>当设置为TextHeightAdaptivePolicy.LAYOUT_CONSTRAINT_FIRST时，优先使用布局约束来调整文本高度。如果布局大小超过布局约束，则尝试在`minFontSize`和`maxFontSize`的范围内缩小字体以满足布局约束。如果将字体大小缩小到`minFontSize`后，布局大小仍然超过布局约束，则删除超过布局约束的行。|
| textIndent<sup>10+</sup> | [Length](ts-types.md#length) | 设置首行文本缩进，默认值0。 |
| font<sup>10+</sup> | [Font](ts-types.md#font) | 设置文本样式。包括字体大小、字体粗细、字体族和字体风格。 |
| wordBreak<sup>11+</sup> | [WordBreak](ts-appendix-enums.md#wordbreak11) | 设置断行规则。 <br />默认值：WordBreak.BREAK_WORD <br/>**说明：**<br/>WordBreak.BREAK_ALL与{overflow:&nbsp;TextOverflow.Ellipsis}，`maxLines`组合使用可实现英文单词按字母截断，超出部分以省略号显示|
| selection<sup>11+</sup> |(selectionStart:&nbsp;number, selectionEnd:&nbsp;number)| 设置选中区域。选中区域高亮且显示手柄和文本选择菜单。 <br />默认值：（-1，-1） <br/>**说明：**<br/>当`copyOption`设置为CopyOptions.None时，设置`selection`属性不生效。<br/>当`overflow`设置为TextOverflow.MARQUEE时，设置`selection`属性不生效。<br/>当`selectionStart`大于等于`selectionEnd`时不选中。可选范围为[0, textSize],textSize为文本内容最大字符数，入参小于0处理为0，大于textSize处理为textSize。<br/>当`selectionStart`或`selectionEnd`在截断不可见区域时不选中。截断为false时超出父组件的文本选中区域生效。|
| ellipsisMode<sup>11+</sup> |[EllipsisMode](ts-appendix-enums.md#ellipsismode11)| 设置省略位置。 <br />默认值：EllipsisMode.END <br/>**说明：**<br/>该接口在API version 11版本不生效。<br/>`ellipsisMode`属性需要配合`overflow`设置为TextOverflow.Ellipsis以及maxLines使用，单独设置`ellipsisMode`属性不生效。<br/>EllipsisMode.START和EllipsisMode.CENTER仅在单行超长文本生效。|
| enableDataDetector<sup>11+</sup> |boolean| 使能文本识别。<br/>默认值： false<br/>**说明：**<br/>所识别实体的`fontColor`和`decoration`会被更改为如下样式：<br/>fontColor：Color.Blue<br/>decoration:&nbsp;{<br/>type:&nbsp;TextDecorationType.Underline,<br/>color:&nbsp;Color.Blue<br/>}<br/>该接口依赖设备底层应具有文本识别能力，否则设置不会生效。<br/>当`enableDataDetector`设置为true，同时不设置`dataDetectorConfig`属性时，默认识别所有类型的实体。<br/>当`copyOption`设置为CopyOptions.None时，该功能不会生效。 |
| dataDetectorConfig<sup>11+</sup> | [TextDataDetectorConfig](#textdatadetectorconfig11对象说明) | 文本识别配置。 <br/>默认值：{<br/>types:&nbsp;[ ],<br/>onDetectResultUpdate:&nbsp;null<br/>} <br />**说明：**<br/>需配合`enableDataDetector`一起使用，设置`enableDataDetector`为true时，`dataDetectorConfig`的配置才能生效。<br/>当有两个实体A、B重叠时，按以下规则保留实体：<br/>1.&nbsp;若A&nbsp;⊂&nbsp;B，则保留B，反之则保留A。<br/>2.&nbsp;当A&nbsp;⊄&nbsp;B且B&nbsp;⊄&nbsp;A时，若A.start&nbsp;<&nbsp;B.start，则保留A，反之则保留B。|
| bindSelectionMenu<sup>11+</sup> | {<br/>spantype:&nbsp;[TextSpanType](ts-appendix-enums.md#textspantype11),<br/>content:&nbsp;[CustomBuilder](ts-types.md#custombuilder8),<br/>responseType:&nbsp;[TextResponseType](ts-appendix-enums.md#textresponsetype11)&nbsp;\,<br/>options?:&nbsp;[SelectionMenuOptions](ts-appendix-enums.md#selectionmenuoptions11)<br/>} | 设置自定义选择菜单。<br/> 默认值：{<br/>  spanType:&nbsp;TextSpanType.TEXT<br/>content：空<br/>responseType:&nbsp;TextResponseType.LONG_PRESS <br/>}<br />**说明：**<br/>`bindSelectionMenu`长按响应时长为600ms，`bindContextMenu`长按响应时长为800ms，同时绑定且触发方式均为长按时，优先响应`bindSelectionMenu`。<br/>自定义菜单超长时，建议内部嵌套[Scroll](./ts-container-scroll.md)组件使用，避免键盘被遮挡。 |

>  **说明：**
>
>  不支持Text内同时存在文本内容和Span或ImageSpan子组件。如果同时存在，只显示Span或ImageSpan内的内容。
>
>  字体排版引擎会对开发者传入的宽度[width](ts-universal-attributes-size.md#width)进行向下取整，保证是整型像素后进行排版。如果字体排版引擎向上取整，可能会出现文字右侧被截断。
>
>  当多个Text组件在[Row](ts-container-row.md)容器内布局且没有设置具体的布局分配信息时，Text会以Row的最大尺寸进行布局。如果需要子组件主轴累加的尺寸不超过Row容器主轴的尺寸，可以设置[layoutWeight](ts-universal-attributes-size.md#layoutweight)或者是以[Flex](ts-universal-attributes-flex-layout.md)布局来约束子组件的主轴尺寸。

## TextDataDetectorConfig<sup>11+</sup>对象说明
| 参数名 | 类型  | 必填 | 说明  |
| ------ | -------- | ---- | ------------------------------------------- |
| types   | [TextDataDetectorType](ts-appendix-enums.md#textdatadetectortype11) | 是   | 设置文本识别的实体类型。设置types为null或者[]时，识别所有类型的实体，否则只识别指定类型的实体。 |
| onDetectResultUpdate   | (callback:(result: string) => void) | 是   | 文本识别成功后，触发onDetectResultUpdate回调。<br/>-&nbsp;result：文本识别的结果，Json格式。 |

## 事件

除支持[通用事件](ts-universal-events-click.md)外，还支持以下事件：

| 名称                                                         | 功能描述                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| onCopy(callback:(value:&nbsp;string)&nbsp;=&gt;&nbsp;void)<sup>11+</sup> | 长按文本内部区域弹出剪贴板后，点击剪切板复制按钮，触发该回调。<br/>value：复制的文本内容。 <br/>**说明：**<br/>目前文本复制仅支持文本。|
| onTextSelectionChange(callback: (selectionStart: number, selectionEnd: number) => void)<sup>11+</sup> | 文本选择的位置发生变化时，触发该回调。<br/>**说明：**<br />selectionStart：文本选择区域起始位置，文本框中文字的起始位置为0。<br />selectionEnd：文本选择区域结束位置。 |

## TextOptions<sup>11+</sup>

Text初始化参数。

| 名称 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| controller | [TextController](#textcontroller11)  | 是 | 文本控制器。 |

## TextController<sup>11+</sup>

Text组件的控制器。

### 导入对象

```
controller: TextController = new TextController()
```

### closeSelectionMenu

closeSelectionMenu(): void

关闭自定义选择菜单或系统默认选择菜单。

## 示例

### 示例1

textAlign、maxLines、textOverflow、lineHeight属性接口使用示例

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
      // 文本水平方向对齐方式设置
      // 单行文本
      Text('textAlign').fontSize(9).fontColor(0xCCCCCC)
      Text('TextAlign set to Center.')
        .style(TextAlign.Center)
      Text('TextAlign set to Start.')
        .style(TextAlign.Start)
      Text('TextAlign set to End.')
        .style(TextAlign.End)

      // 多行文本
      Text('This is the text content with textAlign set to Center.')
        .style(TextAlign.Center)
      Text('This is the text content with textAlign set to Start.')
        .style(TextAlign.Start)
      Text('This is the text content with textAlign set to End.')
        .style(TextAlign.End)


      // 文本超长时显示方式
      Text('TextOverflow+maxLines').fontSize(9).fontColor(0xCCCCCC)
      // 超出maxLines截断内容展示
      Text('This is the setting of textOverflow to Clip text content This is the setting of textOverflow to None text content. This is the setting of textOverflow to Clip text content This is the setting of textOverflow to None text content.')
        .textOverflow({ overflow: TextOverflow.Clip })
        .maxLines(1)
        .style(TextAlign.Start)

      // 超出maxLines展示省略号
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

### 示例2

decoration、baselineOffset、letterSpacing、textCase属性接口使用示例

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

      // 文本基线偏移
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

      // 文本字符间距
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
      // 文本全小写展示
      Text('This is the text content with textCase set to LowerCase.')
        .textCase(TextCase.LowerCase)
        .style()
      // 文本全大写展示
      Text('This is the text content with textCase set to UpperCase.')
        .textCase(TextCase.UpperCase)
        .style()

    }.height(700).width(350).padding({ left: 35, right: 35, top: 35 })
  }
}
```
![textExp1](figures/textExp2.png)

### 示例3

textShadow，heightAdaptivePolicy，TextOverflow.MARQUEE使用示例：

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
      // 设置文字阴影效果
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
      // 设置文本自适应高度的方式
      Text('heightAdaptivePolicy').fontSize(9).fontColor(0xCCCCCC).margin(15).width('90%')
      Text('This is the text with the height adaptive policy set')
        .style(TextHeightAdaptivePolicy.MAX_LINES_FIRST)
      Text('This is the text with the height adaptive policy set')
        .style(TextHeightAdaptivePolicy.MIN_FONT_SIZE_FIRST)
      Text('This is the text with the height adaptive policy set')
        .style(TextHeightAdaptivePolicy.LAYOUT_CONSTRAINT_FIRST)
      Divider()
      Text('marquee').fontSize(9).fontColor(0xCCCCCC).margin(15).width('90%')
      // 设置文本超长时以跑马灯的方式展示
      Text('This is the text with the text overflow set marquee')
        .width(300)
        .borderWidth(1)
        .textOverflow({ overflow: TextOverflow.MARQUEE })
    }
  }
}
```

![](figures/text_3.gif)

### 示例4
ellipsisMode和wordBreak使用示例

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
        Button('更改省略号位置：' + this.ellipsisModeStr[this.ellipsisModeIndex]).onClick(() => {
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
        Button('切换clip：' + this.textClip).onClick(() => {
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
        Button('更改wordBreak模式：' + this.wordBreakStr[this.wordBreakIndex]).onClick(() => {
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

### 示例5
selection, onCopy使用示例

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
          // 变更文本选中起始点、终点
          this.start = 10
          this.end = 30
        })
      Text(this.onCopy).fontSize(12).margin(10).key('copy')
    }.height(600).width(335).padding({ left: 35, right: 35, top: 35 })
  }
}
```
![](figures/textExample5.png)

### 示例6
enableDataDetector和dataDetectorConfig使用示例

```ts
@Entry
@Component
struct TextExample6 {
  @State phoneNumber: string = '(86) (755) ********';
  @State url: string = 'www.********.com';
  @State email: string = '***@example.com';
  @State address: string = 'XX省XX市XX区XXXX';
  @State enableDataDetector: boolean = true;
  @State types: TextDataDetectorType[] = [];

  build() {
    Row() {
      Column() {
        Text(
          '电话号码：' + this.phoneNumber + '\n' +
          '链接：' + this.url + '\n' +
          '邮箱：' + this.email + '\n' +
          '地址：' + this.address
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

### 示例7
bindSelectionMenu，onTextSelectionChange及closeSelectionMenu使用示例

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
            console.info(`自定义选择菜单关闭时回调`);
          },
          onAppear: () => {
            console.info(`自定义选择菜单弹出时回调`);
          }
        })
        .bindSelectionMenu(TextSpanType.TEXT, this.RightClickTextCustomMenu, TextResponseType.RIGHT_CLICK)
        .bindSelectionMenu(TextSpanType.MIXED, this.SelectMixCustomMenu, TextResponseType.SELECT)
        .onTextSelectionChange((selectionStart: number, selectionEnd: number) => {
          console.info(`文本选中区域变化回调, selectionStart: ${selectionStart}, selectionEnd: ${selectionEnd}`);
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
