# 尺寸设置

用于设置组件的宽高、边距。

>  **说明：**
>
>  从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


## 属性


| 名称           | 参数说明                                                     | 描述                                                         |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| width          | [Length](ts-types.md#length)                                 | 设置组件自身的宽度，缺省时使用元素自身内容需要的宽度。若子组件的宽大于父组件的宽，则会画出父组件的范围。<br/>单位：vp<br/>从API version 9开始，该接口支持在ArkTS卡片中使用。 |
| height         | [Length](ts-types.md#length)                                 | 设置组件自身的高度，缺省时使用元素自身内容需要的高度。若子组件的高大于父组件的高，则会画出父组件的范围。<br/>从API version 9开始，该接口支持在ArkTS卡片中使用。 |
| size           | {<br/>width?:&nbsp;[Length](ts-types.md#length),<br/>height?:&nbsp;[Length](ts-types.md#length)<br/>} | 设置高宽尺寸。<br/>单位：vp<br/>从API version 9开始，该接口支持在ArkTS卡片中使用。 |
| padding        | [Padding](ts-types.md#padding)&nbsp;\|&nbsp;[Length](ts-types.md#length) | 设置内边距属性。<br/>参数为Length类型时，四个方向内边距同时生效。<br>默认值：0 <br>单位：vp<br/>padding设置百分比时，上下左右内边距均以父容器的width作为基础值。<br/>从API version 9开始，该接口支持在ArkTS卡片中使用。 |
| margin         | [Margin](ts-types.md#margin)&nbsp;\|&nbsp;[Length](ts-types.md#length) | 设置外边距属性。<br/>参数为Length类型时，四个方向外边距同时生效。<br>默认值：0 <br>单位：vp<br/>margin设置百分比时，上下左右外边距均以父容器的width作为基础值。<br/>从API version 9开始，该接口支持在ArkTS卡片中使用。 |
| layoutWeight   | number&nbsp;\|&nbsp;string                                   | 父容器尺寸确定时，设置了layoutWeight属性的子元素与兄弟元素占主轴尺寸按照权重进行分配，忽略元素本身尺寸设置，表示自适应占满剩余空间。<br/>默认值：0<br/>从API version 9开始，该接口支持在ArkTS卡片中使用。<br/>**说明：** <br/>仅在Row/Column/Flex布局中生效。<br/>可选值为大于等于0的数字，或者可以转换为数字的字符串。 |
| constraintSize | {<br/>minWidth?:&nbsp;[Length](ts-types.md#length),<br/>maxWidth?:&nbsp;[Length](ts-types.md#length),<br/>minHeight?:&nbsp;[Length](ts-types.md#length),<br/>maxHeight?:&nbsp;[Length](ts-types.md#length)<br/>} | 设置约束尺寸，组件布局时，进行尺寸范围限制。constraintSize的优先级高于Width和Height。若设置的minWidth大于maxWidth，则minWidth生效，minHeight与maxHeight同理。<br>默认值：<br>{<br/>minWidth:&nbsp;0,<br/>maxWidth:&nbsp;Infinity,<br/>minHeight:&nbsp;0,<br/>maxHeight:&nbsp;Infinity<br/>}<br/>从API version 9开始，该接口支持在ArkTS卡片中使用。 |

>  **说明：**
>
>  在Row、Column、RelativeContainer组件中，width、height设置auto表示自适应子组件。在TextInput组件中，width设置auto表示自适应文本宽度。

## 示例

```ts
// xxx.ets
@Entry
@Component
struct SizeExample {
  build() {
    Column({ space: 10 }) {
      Text('margin and padding:').fontSize(12).fontColor(0xCCCCCC).width('90%')
      Row() {
        // 宽度80 ,高度80 ,外边距20(蓝色区域），上下左右的内边距分别为5、15、10、20（白色区域）
        Row() {
          Row().size({ width: '100%', height: '100%' }).backgroundColor(Color.Yellow)
        }
        .width(80)
        .height(80)
        .padding({ top: 5, left: 10, bottom: 15, right: 20 })
        .margin(20)
        .backgroundColor(Color.White)
      }.backgroundColor(Color.Blue)

      Text('constraintSize').fontSize(12).fontColor(0xCCCCCC).width('90%')
      Text('this is a Text.this is a Text.this is a Text.this is a Text.this is a Text.this is a Text.this is a Text.this is a Text.this is a Text.this is a Text.this is a Text.this is a Text.this is a Text.this is a Text.this is a Text')
        .width('90%')
        .constraintSize({ maxWidth: 200 })

      Text('layoutWeight').fontSize(12).fontColor(0xCCCCCC).width('90%')
      // 父容器尺寸确定时，设置了layoutWeight的子元素在主轴布局尺寸按照权重进行分配，忽略本身尺寸设置。
      Row() {
        // 权重1，占主轴剩余空间1/3
        Text('layoutWeight(1)')
          .size({ width: '30%', height: 110 }).backgroundColor(0xFFEFD5).textAlign(TextAlign.Center)
          .layoutWeight(1)
        // 权重2，占主轴剩余空间2/3
        Text('layoutWeight(2)')
          .size({ width: '30%', height: 110 }).backgroundColor(0xF5DEB3).textAlign(TextAlign.Center)
          .layoutWeight(2)
        // 未设置layoutWeight属性，组件按照自身尺寸渲染
        Text('no layoutWeight')
          .size({ width: '30%', height: 110 }).backgroundColor(0xD2B48C).textAlign(TextAlign.Center)
      }.size({ width: '90%', height: 140 }).backgroundColor(0xAFEEEE)
    }.width('100%').margin({ top: 5 })
  }
}
```

![size](figures/size.png)
