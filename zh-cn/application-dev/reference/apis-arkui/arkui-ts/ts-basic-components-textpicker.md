# TextPicker

滑动选择文本内容的组件。

>  **说明：**
>
>  该组件从API Version 8开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


## 子组件

无


## 接口

TextPicker(options?: TextPickerOptions)

根据range指定的选择范围创建文本选择器。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名  | 类型                                            | 必填 | 说明                   |
| ------- | ----------------------------------------------- | ---- | ---------------------- |
| options | [TextPickerOptions](#textpickeroptions对象说明) | 否   | 配置文本选择器的参数。 |

## TextPickerOptions对象说明

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| range | string[]&nbsp;\|&nbsp;string[] []<sup>10+</sup> \| [Resource](ts-types.md#resource类型)&nbsp;\|<br/>[TextPickerRangeContent](#textpickerrangecontent10对象说明)[]<sup>10+</sup>&nbsp;\|&nbsp;[TextCascadePickerRangeContent](#textcascadepickerrangecontent10对象说明)[]<sup>10+</sup> | 是 | 选择器的数据选择列表。不可设置为空数组，若设置为空数组，则不显示；若动态变化为空数组，则保持当前正常值显示。<br/>**说明**：单列数据选择器使用string[]，Resource，TextPickerRangeContent[]类型。<br/>多列数据选择器使用string[][]类型。 <br/>多列联动数据选择器使用TextCascadePickerRangeContent[]类型。<br/>Resource类型只支持[strarray.json](../../../quick-start/resource-categories-and-access.md#资源组目录)。<br>range的类型及列数不可以动态修改。|
| selected | number&nbsp;\|&nbsp;number[]<sup>10+</sup> | 否 | 设置默认选中项在数组中的索引值，索引从0开始。<br/>默认值：0 <br/>**说明**：单列数据选择器使用number类型。<br/>多列、多列联动数据选择器使用number[]类型。<br />从API version 10开始，该参数支持[$$](../../../quick-start/arkts-two-way-sync.md)双向绑定变量。|
| value | string&nbsp;\|&nbsp;string[]<sup>10+</sup> | 否 | 设置默认选中项的值，优先级低于selected。<br/>默认值：第一个元素值<br/>**说明**：只有显示文本列表时该值有效。显示图片或图片加文本的列表时，该值无效。 <br/>单列数据选择器使用string类型。<br/>多列、多列联动数据选择器使用string[]类型。<br />从API version 10开始，该参数支持[$$](../../../quick-start/arkts-two-way-sync.md)双向绑定变量。|

## TextPickerRangeContent<sup>10+</sup>对象说明

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称 | 类型                                                 | 必填 | 说明       |
| ---- | ---------------------------------------------------- | ---- | ---------- |
| icon | string&nbsp;\|&nbsp;[Resource](ts-types.md#resource) | 是   | 图片资源。 icon是string类型时，表示图片存放的路径，例如"/common/hello.png"。 |
| text | string&nbsp;\|&nbsp;[Resource](ts-types.md#resource) | 否   | 文本信息。<br/>默认值：空字符串<br/>**说明**：如果文本长度大于列宽时，本文被截断。 |

## TextCascadePickerRangeContent<sup>10+</sup>对象说明

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称 | 类型                                                 | 必填 | 说明   |
| ------ | -------------------------------------------------------- | ---- | ---------- |
| text   | string&nbsp;\|&nbsp;[Resource](ts-types.md#resource) | 是   | 文本信息。<br/>**说明**：如果文本长度大于列宽时，本文被截断。 |
| children   | [TextCascadePickerRangeContent](#textcascadepickerrangecontent10对象说明)[] | 否   | 联动数据。 |
## DividerOptions<sup>12+</sup>对象说明

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称        | 类型                                 | 必填 | 说明                                                         |
| ----------- | ------------------------------------ | ---- | ------------------------------------------------------------ |
| strokeWidth | [Dimension](ts-types.md#dimension10) | 否   | 分割线的线宽（默认单位vp），也可指定单位为px，不支持"百分比"类型。<br/>取值范围：strokeWidth小于0取默认值，最大不得超过列高的一半。<br/>默认值：2.0px |
| startMargin | [Dimension](ts-types.md#dimension10) | 否   | 分割线与TextPicker侧边起始端的距离（默认单位vp），也可指定单位为px，不支持“百分比”类型。<br/>取值范围：startMargin小于0无效，最大不得超过TextPicker列宽。<br/>默认值：0 |
| endMargin   | [Dimension](ts-types.md#dimension10) | 否   | 分割线与TextPicker侧边结束端的距离（默认单位vp），也可指定单位为px，不支持“百分比”类型。<br/>取值范围：startMargin小于0无效，最大不得超过TextPicker列宽。<br/>默认值：0 |
| color       | [ResourceColor](ts-types.md#resourcecolor)  | 否   | 分割线的颜色。<br/>默认值：'#33000000'

## 属性

除支持[通用属性](ts-component-general-attributes.md)外，还支持以下属性：

### defaultPickerItemHeight

defaultPickerItemHeight(value: number | string)

设置Picker各选择项的高度。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                       | 必填 | 说明                   |
| ------ | -------------------------- | ---- | ---------------------- |
| value  | number&nbsp;\|&nbsp;string | 是   | Picker各选择项的高度。number类型取值范围：[0, +∞]，string类型仅支持number类型取值的字符串形式，例如"56"。<br/>默认值：选中项56vp，非选中项36vp。<br />**说明：**<br />设置该参数后，选中项与非选中项的高度均为所设置的值。 |

### disappearTextStyle<sup>10+</sup>

disappearTextStyle(value: PickerTextStyle)

设置所有选项中最上和最下两个选项的文本颜色、字号、字体粗细。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                         | 必填 | 说明                                                         |
| ------ | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| value  | [PickerTextStyle](ts-basic-components-datepicker.md#pickertextstyle10类型说明) | 是   | 所有选项中最上和最下两个选项的文本颜色、字号、字体粗细。<br/>默认值：<br/>{<br/>color: '#ff182431',<br/>font: {<br/>size: '14fp', <br/>weight: FontWeight.Regular<br/>}<br/>} |

### textStyle<sup>10+</sup>

textStyle(value: PickerTextStyle)

设置所有选项中除了最上、最下及选中项以外的文本颜色、字号、字体粗细。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                         | 必填 | 说明                                                         |
| ------ | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| value  | [PickerTextStyle](ts-basic-components-datepicker.md#pickertextstyle10类型说明) | 是   | 所有选项中除了最上、最下及选中项以外的文本颜色、字号、字体粗细。<br/>默认值：<br/>{<br/>color: '#ff182431',<br/>font: {<br/>size: '16fp', <br/>weight: FontWeight.Regular<br/>}<br/>} |

### selectedTextStyle<sup>10+</sup>

selectedTextStyle(value: PickerTextStyle)

设置选中项的文本颜色、字号、字体粗细。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                         | 必填 | 说明                                                         |
| ------ | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| value  | [PickerTextStyle](ts-basic-components-datepicker.md#pickertextstyle10类型说明) | 是   | 选中项的文本颜色、字号、字体粗细。<br/>默认值：<br/>{<br/>color: '#ff007dff',<br/>font: {<br/>size: '20vp', <br/>weight: FontWeight.Medium<br/>}<br/>} |

### selectedIndex<sup>10+</sup>

selectedIndex(value: number | number[])

设置默认选中项在数组中的索引值，优先级高于options中的选中值。单列数据选择器使用number类型。多列、多列联动数据选择器使用number[]类型。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                         | 必填 | 说明                         |
| ------ | ---------------------------- | ---- | ---------------------------- |
| value  | number&nbsp;\|&nbsp;number[] | 是   | 默认选中项在数组中的索引值，索引从0开始。<br/>默认值：0 <br/> |

### canLoop<sup>10+</sup>

canLoop(value: boolean)

设置是否可循环滚动。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                                                         |
| ------ | ------- | ---- | ------------------------------------------------------------ |
| value  | boolean | 是   | 是否可循环滚动。<br/>true：可循环，false：不可循环。<br/>默认值：true |

### divider<sup>12+</sup>

divider(value: DividerOptions | null)

设置分割线样式，不设置该属性则按“默认值”展示分割线。

startMargin + endMargin 超过组件宽度后startMargin和endMargin会被置0。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**
| 参数名 | 类型    | 必填 | 说明                                                                  |
| ------ | ------- | ---- | --------------------------------------------------------------------- |
| value | [DividerOptions](#divideroptions12对象说明) \| null | 是   | 1.设置DividerOptions，则按设置的样式显示分割线。<br/>默认值：<br/>{<br/>strokeWidth: '2px', <br/>startMargin: 0, <br/>endMargin: 0, <br/>color: '#33000000'<br/>}<br/>2.设置为null不显示分割线。 |

### gradientHeight<sup>12+</sup>

gradientHeight(value: Dimension)

设置渐隐效果高度，不设置该属性则显示默认渐隐效果。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型    | 必填 | 说明                                                         |
| ------ | ------- | ---- | ------------------------------------------------------------ |
| value  | [Dimension](ts-types.md#dimension10) | 是   | 内容区上下边缘的渐隐高度（支持百分比，100%为TextPicker高度的一半即最大值），设置为0时不显示渐隐效果，负数等非法值显示默认渐隐效果。默认值为36vp。|

### disableTextStyleAnimation<sup>15+</sup>

disableTextStyleAnimation(disabled: boolean)

设置滑动过程中是否有文本样式变化动效。设置为true时，滑动过程中无字号、字重、字体颜色等变化动效，且文本均显示为[defaultTextStyle](#defaulttextstyle15)属性设置样式。如未设置defaultTextStyle，则显示为Text组件默认样式。

**原子化服务API：** 从API version 15开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型    | 必填 | 说明                                                         |
| ------ | ------- | ---- | ------------------------------------------------------------ |
| disabled  | boolean | 是   | 设置滑动过程中是否有文本样式变化动效。<br/>true：无文本样式变化动效，false：有文本样式变化动效。<br/>默认值：false |

### defaultTextStyle<sup>15+</sup>

defaultTextStyle(style: TextPickerTextStyle)

设置关闭滑动过程中文本样式变化动效时，各个选项文本的样式。

**原子化服务API：** 从API version 15开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型                                                         | 必填 | 说明                                                         |
| ------ | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| style  | [TextPickerTextStyle](#textpickertextstyle15类型说明) | 是   | 设置关闭滑动过程中文本样式变化动效时的各个选项文本的样式，仅当disableTextStyleAnimation为true时生效。<br/>默认值：与[Text](ts-basic-components-text.md)组件默认值相同。 |

> **说明：**
>
> 该组件不建议开发者在动效过程中修改属性数据。

## 事件

除支持[通用事件](ts-component-general-events.md)外，还支持以下事件：

### onAccept<sup>(deprecated) </sup>

onAccept(callback: (value: string, index: number) => void)

点击弹窗中的“确定”按钮时触发该回调。该事件仅在[文本滑动选择器弹窗](ts-methods-textpicker-dialog.md)中生效。

从API version 10开始废弃。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明                 |
| ------ | ------ | ---- | -------------------- |
| value  | string | 是   | 当前选中项的文本。   |
| index  | number | 是   | 当前选中项的索引值，索引从0开始。 |

### onCancel<sup>(deprecated) </sup>

onCancel(callback: () => void)

点击弹窗中的“取消”按钮时触发该回调。该事件仅在[文本滑动选择器弹窗](ts-methods-textpicker-dialog.md)中生效。

从API version 10开始废弃。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### onChange

onChange(callback:&nbsp;(value:&nbsp;string&nbsp;\|&nbsp;string[],&nbsp;index:&nbsp;number&nbsp;\|&nbsp;number[])&nbsp;=&gt;&nbsp;void)

滑动选中TextPicker文本内容后，触发该回调。当显示文本或图片加文本列表时，value值为选中项中的文本值，当显示图片列表时，value值为空。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                       | 必填 | 说明                                              |
| ------ | ------------------------------------------ | ---- | ------------------------------------------------- |
| value  | string&nbsp;\|&nbsp;string[]<sup>10+</sup> | 是   | 当前选中项的文本。多列的情况，value为数组类型。   |
| index  | number&nbsp;\|&nbsp;number[]<sup>10+</sup> | 是   | 当前选中项的索引值，索引从0开始。多列的情况，index为数组类型。 |

### onScrollStop<sup>14+</sup>

onScrollStop(callback: TextPickerScrollStopCallback)

文本选择器的选项列滑动停止时触发该事件。

手指拖动选项列触发的滑动，手指离开屏幕且滑动停止时会触发该事件。

当显示文本或图片加文本列表时，value值为选中项中的文本值，当显示图片列表时，value值为空。

**原子化服务API：** 从API version 14开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                       | 必填 | 说明                                              |
| ------ | ------------------------------------------ | ---- | ------------------------------------------------- |
| callback | [TextPickerScrollStopCallback](#textpickerscrollstopcallback14) | 是   | 文本选择器的选项列滑动停止时触发该事件。 |

## TextPickerScrollStopCallback<sup>14+</sup>

type TextPickerScrollStopCallback = (value: string | string[], index: number | number[]) => void

文本选择器的选项列滑动停止时触发该事件。

**卡片能力：** 从API version 14开始，该接口支持在ArkTS卡片中使用。

**原子化服务API：** 从API version 14开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                       | 必填 | 说明                                              |
| ------ | ------------------------------------------ | ---- | ------------------------------------------------- |
| value  | string&nbsp;\|&nbsp;string[] | 是   | 当前选中项的文本。多列的情况，value为数组类型。   |
| index  | number&nbsp;\|&nbsp;number[] | 是   | 当前选中项的索引值，索引从0开始。多列的情况，index为数组类型。 |

## TextPickerTextStyle<sup>15+</sup>类型说明

文本样式选项，继承自[PickerTextStyle](ts-basic-components-datepicker.md#pickertextstyle10类型说明)。

**原子化服务API：** 从API version 15开始，该接口支持在原子化服务中使用。

| 参数名   | 类型                                     | 必填   | 说明                      |
| ----- | ---------------------------------------- | ---- | ------------------------- |
| color | [ResourceColor](ts-types.md#resourcecolor) | 否    | 文本颜色。                     |
| font  | [Font](ts-types.md#font)                 | 否    | 文本样式。 |
| minFontSize  | number&nbsp;\|&nbsp;string&nbsp;\|&nbsp;[Resource](ts-types.md#resource) | 否    | 文本最小显示字号，与maxFontSize配合使用，当设置minFontSize与maxFontSize时，font中的size设置不生效，默认最大行数为1，默认自适应高度方式为MIN_FONT_SIZE_FIRST。                     |
| maxFontSize  | number&nbsp;\|&nbsp;string&nbsp;\|&nbsp;[Resource](ts-types.md#resource) | 否    | 文本最大显示字号。                     |
|  overflow   |   [TextOverflow](ts-appendix-enums.md#textoverflow) | 否    | 文本截断方式，设置为MARQUEE时不生效。                     |

## 示例

### 示例1（设置选择器列数）

该示例通过配置range实现单列或多列文本选择器。

```ts
// xxx.ets
class bottom {
  bottom:number = 50
}
let bott:bottom = new bottom()
@Entry
@Component
struct TextPickerExample {
  private select: number = 1
  private apfruits: string[] = ['apple1', 'apple2', 'apple3', 'apple4']
  private orfruits: string[] = ['orange1', 'orange2', 'orange3', 'orange4']
  private pefruits: string[] = ['peach1', 'peach2', 'peach3', 'peach4']
  private multi: string[][] = [this.apfruits, this.orfruits, this.pefruits]
  private cascade: TextCascadePickerRangeContent[] = [
    {
      text: '辽宁省',
      children: [{ text: '沈阳市', children: [{ text: '沈河区' }, { text: '和平区' }, { text: '浑南区' }] },
        { text: '大连市', children: [{ text: '中山区' }, { text: '金州区' }, { text: '长海县' }] }]
    },
    {
      text: '吉林省',
      children: [{ text: '长春市', children: [{ text: '南关区' }, { text: '宽城区' }, { text: '朝阳区' }] },
        { text: '四平市', children: [{ text: '铁西区' }, { text: '铁东区' }, { text: '梨树县' }] }]
    },
    {
      text: '黑龙江省',
      children: [{ text: '哈尔滨市', children: [{ text: '道里区' }, { text: '道外区' }, { text: '南岗区' }] },
        { text: '牡丹江市', children: [{ text: '东安区' }, { text: '西安区' }, { text: '爱民区' }] }]
    }
  ]

  build() {
    Column() {

      TextPicker({ range: this.apfruits, selected: this.select })
        .onChange((value: string | string[], index: number | number[]) => {
          console.info('Picker item changed, value: ' + value + ', index: ' + index)
        })
        .onScrollStop((value: string | string[], index: number | number[]) => {
          console.info('Picker scroll stopped, value: ' + value + ', index: ' + index)
        }).margin(bott)

      TextPicker({ range: this.multi })
        .onChange((value: string | string[], index: number | number[]) => {
          console.info('TextPicker 多列:onChange ' + JSON.stringify(value) + ', ' + 'index: ' + JSON.stringify(index))
        })
        .onScrollStop((value: string | string[], index: number | number[]) => {
          console.info('TextPicker 多列:onScrollStop ' + JSON.stringify(value) + ', ' + 'index: ' + JSON.stringify(index))
        }).margin(bott)

      TextPicker({ range: this.cascade })
        .onChange((value: string | string[], index: number | number[]) => {
          console.info('TextPicker 多列联动:onChange ' + JSON.stringify(value) + ', ' + 'index: ' + JSON.stringify(index))
        })
        .onScrollStop((value: string | string[], index: number | number[]) => {
          console.info('TextPicker 多列联动:onScrollStop ' + JSON.stringify(value) + ', ' + 'index: ' + JSON.stringify(index))
        })
    }
  }
}
```

![textpicker](figures/textpicker.gif)

### 示例2（设置文本样式）

该示例通过配置disappearTextStyle、textStyle、selectedTextStyle实现文本选择器中的文本样式。

```ts
// xxx.ets
@Entry
@Component
struct TextPickerExample {
  private select: number = 1
  private fruits: string[] = ['apple1', 'orange2', 'peach3', 'grape4']

  build() {
    Column() {
      TextPicker({ range: this.fruits, selected: this.select })
        .onChange((value: string | string[], index: number | number[]) => {
          console.info('Picker item changed, value: ' + value + ', index: ' + index)
        })
        .onScrollStop((value: string | string[], index: number | number[]) => {
          console.info('Picker scroll stopped, value: ' + value + ', index: ' + index)
        })
        .disappearTextStyle({color: Color.Red, font: {size: 15, weight: FontWeight.Lighter}})
        .textStyle({color: Color.Black, font: {size: 20, weight: FontWeight.Normal}})
        .selectedTextStyle({color: Color.Blue, font: {size: 30, weight: FontWeight.Bolder}})
    }.width('100%').height('100%')
  }
}
```

![textpicker](figures/textpicker1.gif)

### 示例3（设置无分割线样式）

该示例通过配置divider为null实现无分割线样式的文本选择器。

```ts
// xxx.ets
@Entry
@Component
struct TextPickerExample {
  private select: number = 1
  private fruits: string[] = ['apple1', 'orange2', 'peach3', 'grape4']

  build() {
    Column() {
      TextPicker({ range: this.fruits, selected: this.select })
        .onChange((value: string | string[], index: number | number[]) => {
          console.info('Picker item changed, value: ' + value + ', index: ' + index)
        })
        .onScrollStop((value: string | string[], index: number | number[]) => {
          console.info('Picker scroll stopped, value: ' + value + ', index: ' + index)
        })
        .disappearTextStyle({color: Color.Red, font: {size: 15, weight: FontWeight.Lighter}})
        .textStyle({color: Color.Black, font: {size: 20, weight: FontWeight.Normal}})
        .selectedTextStyle({color: Color.Blue, font: {size: 30, weight: FontWeight.Bolder}})
        .divider(null)
    }.width('100%').height('100%')
  }
}
```
![textpicker](figures/textpicker2.gif)

### 示例4（设置分割线样式）

该示例通过配置divider的DividerOptions类型实现分割线样式的文本选择器。

```ts
// xxx.ets
@Entry
@Component
struct TextPickerExample {
  private select: number = 1
  private fruits: string[] = ['apple1', 'orange2', 'peach3', 'grape4']

  build() {
    Column() {
      TextPicker({ range: this.fruits, selected: this.select })
        .onChange((value: string | string[], index: number | number[]) => {
          console.info('Picker item changed, value: ' + value + ', index: ' + index)
        })
        .onScrollStop((value: string | string[], index: number | number[]) => {
          console.info('Picker scroll stopped, value: ' + value + ', index: ' + index)
        })
        .disappearTextStyle({color: Color.Red, font: {size: 15, weight: FontWeight.Lighter}})
        .textStyle({color: Color.Black, font: {size: 20, weight: FontWeight.Normal}})
        .selectedTextStyle({color: Color.Blue, font: {size: 30, weight: FontWeight.Bolder}})
        .divider({
          strokeWidth: 10,
          color: Color.Red,
          startMargin: 10,
          endMargin: 20
        } as DividerOptions)
    }.width('100%').height('100%')
  }
}
```
![textpicker](figures/textpicker3.gif)
### 示例5（设置渐隐效果）

该示例通过gradientHeight自定义TextPicker的渐隐效果高度。

```ts
// xxx.ets 
@Entry
@Component
struct TextPickerExample {
  private select: number = 1
  private fruits: string[] = ['apple1', 'orange2', 'peach3', 'grape4']

  build() {
    Column() {
      TextPicker({ range: this.fruits, selected: this.select })
        .onChange((value: string | string[], index: number | number[]) => {
          console.info('Picker item changed, value: ' + value + ', index: ' + index)
        })
        .onScrollStop((value: string | string[], index: number | number[]) => {
          console.info('Picker scroll stopped, value: ' + value + ', index: ' + index)
        })
        .disappearTextStyle({color: Color.Red, font: {size: 15, weight: FontWeight.Lighter}})
        .textStyle({color: Color.Black, font: {size: 20, weight: FontWeight.Normal}})
        .selectedTextStyle({color: Color.Blue, font: {size: 30, weight: FontWeight.Bolder}})
        .gradientHeight(100)
    }.width('100%').height('100%')
  }
}
```

![textpicker](figures/textpicker4.gif)

### 示例6（设置禁用文本样式变化动效与对应文本样式）

该示例通过配置disableTextStyleAnimation、defaultTextStyle实现文本选择器禁用文本样式变化动效与此时的文本样式。

```ts
// xxx.ets
@Entry
@Component
struct TextPickerExample {
  private select: number = 1
  private fruits: string[] = ['AAAAA', 'BBBBBBBBBBBBB', 'CCCC', 'DDDDDDDD', 'EEE']

  build() {
    Column() {
      TextPicker({
        range: this.fruits,
        selected: this.select,
        value: this.fruits[this.select]
      })
        .disableTextStyleAnimation(true)
        .margin({ bottom: 30 })
      TextPicker({
        range: this.fruits,
        selected: this.select,
        value: this.fruits[this.select]
      })
        .disableTextStyleAnimation(true)
        .defaultTextStyle({ minFontSize: 18, maxFontSize: 28, overflow: TextOverflow.Ellipsis })
    }.width('100%').height('100%')
  }
}
```

![textpicker](figures/TextPickerDemo9.jpeg)
