# 图像效果

设置组件的模糊、阴影、球面效果以及设置图片的图像效果。

>  **说明：**
>
>  从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。

## blur

blur(value: number, options?: BlurOptions)

为组件添加内容模糊效果。

**卡片能力：** 从API version 9开始，该接口支持在ArkTS卡片中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名                | 类型                                              | 必填 | 说明                                                         |
| --------------------- | ------------------------------------------------- | ---- | ------------------------------------------------------------ |
| value                 | number                                            | 是   | 当前组件添加内容模糊效果，入参为模糊半径，模糊半径越大越模糊，为0时不模糊。 |
| options<sup>11+</sup> | [BlurOptions](ts-appendix-enums.md#bluroptions11) | 否   | 灰阶梯参数。                                                 |

## backdropBlur

backdropBlur(value: number, options?: BlurOptions)

为组件添加背景模糊效果。

**卡片能力：** 从API version 9开始，该接口支持在ArkTS卡片中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名                | 类型                                              | 必填 | 说明                                                         |
| --------------------- | ------------------------------------------------- | ---- | ------------------------------------------------------------ |
| value                 | number                                            | 是   | 为当前组件添加背景模糊效果，入参为模糊半径，模糊半径越大越模糊，为0时不模糊。 |
| options<sup>11+</sup> | [BlurOptions](ts-appendix-enums.md#bluroptions11) | 否   | 灰阶梯参数。                                                 |

>  **说明：**
>
>  blur和backdropBlur是实时模糊接口，会每帧进行实时渲染，性能负载较高。当模糊内容和模糊半径都不需要变化时，建议使用[静态模糊接口](../../apis-arkgraphics2d/js-apis-effectKit.md#blur)。

## shadow

shadow(value: ShadowOptions | ShadowStyle)

为组件添加阴影效果。

**卡片能力：** 从API version 9开始，该接口支持在ArkTS卡片中使用，ArkTS卡片上不支持参数为 [ShadowStyle](ts-universal-attributes-image-effect.md#shadowstyle10枚举说明)类型。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                         | 必填 | 说明                                                         |
| ------ | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| value  | [ShadowOptions](#shadowoptions对象说明)&nbsp;\|&nbsp;[ShadowStyle](#shadowstyle10枚举说明)<sup>10+</sup> | 是   | 为当前组件添加阴影效果。<br/>入参类型为ShadowOptions时，可以指定模糊半径、阴影的颜色、X轴和Y轴的偏移量。<br/>入参类型为ShadowStyle时，可指定不同阴影样式。 |

## grayscale

grayscale(value: number)

为组件添加灰度效果。

**卡片能力：** 从API version 9开始，该接口支持在ArkTS卡片中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| value  | number | 是   | 为当前组件添加灰度效果。值定义为灰度转换的比例，入参1.0则完全转为灰度图像，入参0.0则图像无变化，入参在0.0和1.0之间时，效果呈线性变化。（百分比)<br/>默认值：0.0<br/>取值范围：[0.0, 1.0]<br/>**说明：**<br/>设置小于0.0的值时，按值为0.0处理，设置大于1.0的值时，按值为1.0处理。 |

## brightness

brightness(value: number)

为组件添加高光效果。

**卡片能力：** 从API version 9开始，该接口支持在ArkTS卡片中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| value  | number | 是   | 为当前组件添加高光效果，入参为高光比例，值为1时没有效果，小于1时亮度变暗，0为全黑，大于1时亮度增加，数值越大亮度越大，但大于2后亮度效果变化不明显。<br/>默认值：1.0<br/>推荐取值范围：[0, 2]<br/>**说明：**<br/>设置小于0的值时，按值为0处理。<br/>从API version 9开始，该接口支持在ArkTS卡片中使用。 |

## saturate

saturate(value: number)

为组件添加饱和度效果。

**卡片能力：** 从API version 9开始，该接口支持在ArkTS卡片中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| value  | number | 是   | 为当前组件添加饱和度效果，饱和度为颜色中的含色成分和消色成分(灰)的比例，入参为1时，显示原图像，大于1时含色成分越大，饱和度越大，小于1时消色成分越大，饱和度越小。（百分比）<br/>默认值：1.0<br/>推荐取值范围：[0, 50)<br/>**说明：**<br/>设置小于0的值时，按值为0处理。 |

## contrast

contrast(value: number)

为组件添加对比度效果。

**卡片能力：** 从API version 9开始，该接口支持在ArkTS卡片中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| value  | number | 是   | 为当前组件添加对比度效果，入参为对比度的值。值为1时，显示原图，大于1时，值越大对比度越高，图像越清晰醒目，小于1时，值越小对比度越低，当对比度为0时，图像变为全灰。（百分比）<br/>默认值：1.0<br/>推荐取值范围：[0, 10)<br/>**说明：**<br/>设置小于0的值时，按值为0处理。 |

## invert

invert(value: number | InvertOptions)

反转输入的图像。

**卡片能力：** 从API version 9开始，该接口支持在ArkTS卡片中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                         | 必填 | 说明                                                         |
| ------ | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| value  | number&nbsp;\|&nbsp;[InvertOptions](#invertoptions11对象说明)<sup>11+</sup> | 是   | 反转输入的图像。<br/>入参对象为number时,入参为图像反转的比例，值为1时完全反转，值为0则图像无变化。（百分比）<br/>取值范围：[0, 1]<br/>设置小于0的值时，按值为0处理。<br/>入参对象为 InvertOptions时，对比背景颜色灰度值和阈值区间，背景颜色灰度值小于阈值区间时反色取high值，当背景颜色灰度值大于阈值区间时反色取low值，背景颜色灰度值在阈值区间内取值由high线性渐变到low。 |

## sepia

sepia(value: number)

将图像转换为深褐色。

**卡片能力：** 从API version 9开始，该接口支持在ArkTS卡片中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| value  | number | 是   | 将图像转换为深褐色。入参为图像反转的比例，值为1则完全是深褐色的，值为0图像无变化。 （百分比） |

## hueRotate

hueRotate(value: number | string)

色相旋转效果。

**卡片能力：** 从API version 9开始，该接口支持在ArkTS卡片中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                       | 必填 | 说明                                                         |
| ------ | -------------------------- | ---- | ------------------------------------------------------------ |
| value  | number&nbsp;\|&nbsp;string | 是   | 色相旋转效果，输入参数为旋转角度。<br/>默认值：'0deg'<br/>取值范围：(-∞, +∞)<br/>**说明：**<br/>色调旋转360度会显示原始颜色。先将色调旋转180 度，然后再旋转-180度会显示原始颜色。数据类型为number时，值为90和'90deg'效果一致。 |

## colorBlend<sup>7+</sup>

colorBlend(value: Color | string | Resource)

为组件添加颜色叠加效果。

**卡片能力：** 从API version 9开始，该接口支持在ArkTS卡片中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                         | 必填 | 说明                                           |
| ------ | ------------------------------------------------------------ | ---- | ---------------------------------------------- |
| value  | [Color](ts-appendix-enums.md#color)&nbsp;\|&nbsp;string&nbsp;\|&nbsp;[Resource](ts-types.md#resource) | 是   | 为当前组件添加颜色叠加效果，入参为叠加的颜色。 |

## linearGradientBlur<sup>10+</sup> 

linearGradientBlur(value: number, options: LinearGradientBlurOptions)

为组件添加内容线性渐变模糊效果。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名  | 类型                                                         | 必填 | 说明                                                         |
| ------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| value   | number                                                       | 是   | 为模糊半径，模糊半径越大越模糊，为0时不模糊。<br/>取值范围：[0, 60]<br/>线性梯度模糊包含两个部分fractionStops和direction。 |
| options | [LinearGradientBlurOptions](#lineargradientbluroptions10对象说明) | 是   | 设置线性渐变模糊效果。                                       |

## renderGroup<sup>10+</sup>

renderGroup(value: boolean)

设置当前控件和子控件是否先整体离屏渲染绘制后再与父控件融合绘制。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                                                         |
| ------ | ------- | ---- | ------------------------------------------------------------ |
| value  | boolean | 是   | 设置当前控件和子控件是否先整体离屏渲染绘制后再与父控件融合绘制。当前控件的不透明度不为1时绘制效果可能有差异。<br/>默认值：false |

## blendMode<sup>11+</sup> 

blendMode(value: BlendMode, type?: BlendApplyType)

将当前控件的内容（包含子节点内容）与下方画布（可能为离屏画布）已有内容进行混合。

**卡片能力：** 从API version 11开始，该接口支持在ArkTS卡片中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                            | 必填 | 说明                                                         |
| ------ | ------------------------------- | ---- | ------------------------------------------------------------ |
| value  | [BlendMode](#blendmode11枚举说明)  | 是   | 混合模式。<br/>默认值：BlendMode.NONE   |
| type   | [BlendApplyType](ts-appendix-enums.md#blendapplytype11)  |    否    | blendMode实现方式是否离屏。<br/>默认值：BlendApplyType.FAST<br/>**说明：**<br/>1. 设置BlendApplyType.FAST时，不离屏。<br/>2. 设置BlendApplyType.OFFSCREEN时，会创建当前组件大小的离屏画布，再将当前组件（含子组件）的内容绘制到离屏画布上，再用指定的混合模式与下方画布已有内容进行混合。     |

## useShadowBatching<sup>11+</sup> 

useShadowBatching(value: boolean)

控件内部子节点的阴影进行同层绘制，同层元素阴影重叠。

**卡片能力：** 从API version 11开始，该接口支持在ArkTS卡片中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                                                         |
| ------ | ------- | ---- | ------------------------------------------------------------ |
| value  | boolean | 是   | 控件内部子节点的阴影进行同层绘制，同层元素阴影重叠。<br/>默认值：false<br/>**说明：**<br/>1. 默认不开启，如果子节点的阴影半径较大，节点各自的阴影会互相重叠。 当开启时，元素的阴影将不会重叠。<br/>2. 不推荐useShadowBatching嵌套使用，如果嵌套使用，只会对当前的子节点生效，无法递推。 |

## ShadowOptions对象说明

阴影属性集合，用于设置阴影的模糊半径、阴影的颜色、X轴和Y轴的偏移量。

从API version 9开始，该接口支持在ArkTS卡片中使用。

| 名称      | 类型                                       | 必填   | 说明                                       |
| ------- | ---------------------------------------- | ---- | ---------------------------------------- |
| radius  | number \| [Resource](ts-types.md#resource) | 是    | 阴影模糊半径。<br/>取值范围：[0, +∞)<br/>单位：px<br/>**说明：**  <br/>设置小于0的值时，按值为0处理。<br/>如需使用vp单位的数值可用[vp2px](ts-pixel-units.md#像素单位转换)进行转换。<br/>如果radius为Resource类型，则传入的值需为number类型。<br/> |
| type<sup>10+</sup> | [ShadowType<sup>10+</sup>](ts-appendix-enums.md#shadowtype10)  |      否    | 阴影类型。<br/>默认为COLOR。        |
| color   | [Color](ts-appendix-enums.md#color) \| string \| [Resource](ts-types.md#resource)\| [ColoringStrategy<sup>10+</sup> ](ts-types.md#coloringstrategy10) | 否    | 阴影的颜色。<br/>默认为黑色。 <br/>**说明：** <br/>从API version 11开始，该接口支持使用ColoringStrategy实现智能取色，智能取色功能不支持在ArkTS卡片、[textShadow](ts-basic-components-text.md#属性)中使用。<br/>当前仅支持平均取色和主色取色，智能取色区域为shadow绘制区域。<br/>支持使用'average'字符串触发智能平均取色模式，支持使用'primary'字符串触发智能主色模式。                       |
| offsetX | number \| [Resource](ts-types.md#resource) | 否    | 阴影的X轴偏移量。<br/>默认值：0<br/>单位：px<br/>**说明：** <br/>如需使用vp单位的数值可用[vp2px](ts-pixel-units.md#像素单位转换)进行转换。<br/>如果offsetX为Resource类型，则传入的值需为number类型。<br/> |
| offsetY | number \| [Resource](ts-types.md#resource) | 否    | 阴影的Y轴偏移量。<br/>默认值：0<br/>单位：px<br/>**说明：** <br/>如需使用vp单位的数值可用[vp2px](ts-pixel-units.md#像素单位转换)进行转换。<br/>如果offsetY为Resource类型，则传入的值需为number类型。<br/> |
| fill<sup>11+</sup>     | boolean                                    | 否    | 阴影是否内部填充。<br/>默认为false。<br/>**说明：**<br/>[textShadow](ts-basic-components-text.md#属性)中该字段不生效。                 |

## ShadowStyle<sup>10+</sup>枚举说明

| 名称                | 描述     |
| ----------------- | ------ |
| OUTER_DEFAULT_XS  | 超小阴影。  |
| OUTER_DEFAULT_SM  | 小阴影。   |
| OUTER_DEFAULT_MD  | 中阴影。   |
| OUTER_DEFAULT_LG  | 大阴影。   |
| OUTER_FLOATING_SM | 浮动小阴影。 |
| OUTER_FLOATING_MD | 浮动中阴影。 |

## BlendMode<sup>11+</sup>枚举说明

>  **说明：**
>
>  blendMode枚举中，s表示源像素，d表示目标像素，sa表示原像素透明度，da表示目标像素透明度，r表示混合后像素，ra表示混合后像素透明度。

| 名称           | 描述                                                             |
| ---------------| ------                                                        |
| NONE            | 将上层图像直接覆盖到下层图像上，不进行任何混合操作。              |
| CLEAR           | 将源像素覆盖的目标像素清除为完全透明。                      |
| SRC             | r = s，只显示源像素。                    |
| DST             | r = d，只显示目标像素。                  |
| SRC_OVER        | r = s + (1 - sa) * d，将源像素按照透明度进行混合，覆盖在目标像素上。                 |
| DST_OVER        | r = d + (1 - da) * s，将目标像素按照透明度进行混合，覆盖在源像素上。                 |
| SRC_IN          | r = s * da，只显示源像素中与目标像素重叠的部分。                        |
| DST_IN          | r = d * sa，只显示目标像素中与源像素重叠的部分。                        |
| SRC_OUT         | r = s * (1 - da)，只显示源像素中与目标像素不重叠的部分。                |
| DST_OUT         | r = d * (1 - sa)，只显示目标像素中与源像素不重叠的部分。                |
| SRC_ATOP        | r = s * da + d * (1 - sa)，在源像素和目标像素重叠的地方绘制源像素，在源像素和目标像素不重叠的地方绘制目标像素。                 |
| DST_ATOP        | r = d * sa + s * (1 - da)，在源像素和目标像素重叠的地方绘制目标像素，在源像素和目标像素不重叠的地方绘制源像素。                 |
| XOR             | r = s * (1 - da) + d * (1 - sa)，只显示源像素与目标像素不重叠的部分。                     |
| PLUS            | r = min(s + d, 1)，将源像素值与目标像素值相加，并将结果作为新的像素值。                     |
| MODULATE        | r = s * d，将源像素与目标像素进行乘法运算，并将结果作为新的像素值。                          |
| SCREEN          | r = s + d - s * d，将两个图像的像素值相加，然后减去它们的乘积来实现混合。                    |
| OVERLAY         | 根据目标像素来决定使用MULTIPLY混合模式还是SCREEN混合模式。                                  |
| DARKEN          | rc = s + d - max(s * da, d * sa), ra = kSrcOver，当两个颜色重叠时，较暗的颜色会覆盖较亮的颜色。                 |
| LIGHTEN         | rc = s + d - min(s * da, d * sa), ra = kSrcOver，将源图像和目标图像中的像素进行比较，选取两者中较亮的像素作为最终的混合结果。            |
| COLOR_DODGE     | 使目标像素变得更亮来反映源像素。                     |
| COLOR_BURN      | 使目标像素变得更暗来反映源像素。                     |
| HARD_LIGHT      | 根据源像素的值来决定目标像素变得更亮或者更暗。根据源像素来决定使用MULTIPLY混合模式还是SCREEN混合模式。                  |
| SOFT_LIGHT      | 根据源像素来决定使用LIGHTEN混合模式还是DARKEN混合模式。                                                             |
| DIFFERENCE      | rc = s + d - 2 * (min(s * da, d * sa)), ra = kSrcOver，对比源像素和目标像素，亮度更高的像素减去亮度更低的像素，产生高对比度的效果。                      |
| EXCLUSION       | rc = s + d - two(s * d), ra = kSrcOver，对比源像素和目标像素，亮度更高的像素减去亮度更低的像素，产生柔和的效果。          |
| MULTIPLY        | r = s * (1 - da) + d * (1 - sa) + s * d，将源图像与目标图像进行乘法混合，得到一张新的图像。                           |
| HUE             | 保留源图像的亮度和饱和度，但会使用目标图像的色调来替换源图像的色调。                                   |
| SATURATION      | 保留目标像素的亮度和色调，但会使用源像素的饱和度来替换目标像素的饱和度。                                |
| COLOR           | 保留源像素的饱和度和色调，但会使用目标像素的亮度来替换源像素的亮度。                                   |
| LUMINOSITY      | 保留目标像素的色调和饱和度，但会用源像素的亮度替换目标像素的亮度。                                     |

## LinearGradientBlurOptions<sup>10+</sup>对象说明

| 名称          | 类型                                                        | 必填  | 说明                                                         |
| ------------- | ----------------------------------------------------------- | ----- | ------------------------------------------------------------ |
| fractionStops | Array\<[FractionStop](#fractionstop)>                                    | 是    | 数组中保存的每一个二元数组（取值0-1，小于0则为0，大于0则为1）表示[模糊程度, 模糊位置]；模糊位置需严格递增，开发者传入的数据不符合规范会记录日志，渐变模糊数组中二元数组个数必须大于等于2，否则渐变模糊不生效。 |
| direction     | [GradientDirection](ts-appendix-enums.md#gradientdirection) | 是    | 渐变模糊方向。<br/>默认值：<br/>GradientDirection.Bottom |

## FractionStop

FractionStop = [ number, number ]

定义模糊段。元组中的第一个元素表示分数。该值的范围为[0,1]。值1表示不透明，0表示完全透明。第二个元素表示停止位置。该值的范围为[0,1]。值1表示区域结束位置，0表示区域开始位置。

## InvertOptions<sup>11+</sup>对象说明

前景智能取反色。

| 名称            |  类型  | 必填  | 说明                                       |
| -------------- | ------ | ----- | ------------------------------------------ |
| low            | number | 是    | 背景颜色灰度值大于阈值区间时的取值。                  |
| high           | number | 是    | 背景颜色灰度值小于阈值区间时的取值。              |
| threshold      | number | 是    | 灰度阈值。                                  |
| thresholdRange | number | 是    | 阈值范围。<br/>**说明：**<br/>灰度阈值上下偏移thresholdRange构成阈值区间，背景颜色灰度值在区间内取值由high线性渐变到low。|

## 示例

### 示例1
模糊属性的用法，blur内容模糊，backdropBlur背景模糊。
```ts
// xxx.ets
@Entry
@Component
struct BlurEffectsExample {
  build() {
    Column({ space: 10 }) {
      // 对字体进行模糊
      Text('font blur').fontSize(15).fontColor(0xCCCCCC).width('90%')
      Flex({ alignItems: ItemAlign.Center }) {
        Text('original text').margin(10)
        Text('blur text')
          .blur(5).margin(10)
        Text('blur text')
          .blur(10).margin(10)
        Text('blur text')
          .blur(15).margin(10)
      }.width('90%').height(40)
      .backgroundColor(0xF9CF93)


      // 对背景进行模糊
      Text('backdropBlur').fontSize(15).fontColor(0xCCCCCC).width('90%')
      Text()
        .width('90%')
        .height(40)
        .fontSize(16)
        .backdropBlur(3)
        .backgroundImage($r('app.media.image'))
        .backgroundImageSize({ width: 1200, height: 160 })
    }.width('100%').margin({ top: 5 })
  }
}
```

![textblur](figures/textblur.png)

### 示例2
设置图片的效果，包括阴影，灰度，高光，饱和度，对比度，图像反转，叠色，色相旋转等。
```ts
// xxx.ets
@Entry
@Component
struct ImageEffectsExample {
  build() {
    Column({ space: 5 }) {
      // 添加阴影效果，图片效果不变
      Text('shadow').fontSize(15).fontColor(0xCCCCCC).width('90%')
      Image($r('app.media.image'))
        .width('90%')
        .height(30)
        .shadow({ radius: 10, color: Color.Green, offsetX: 20, offsetY: 20 })

      // 添加内部阴影效果
      Text('shadow').fontSize(15).fontColor(0xCCCCCC).width('90%')
      Image($r('app.media.image'))
        .width('90%')
        .height(30)
        .shadow({ radius: 5, color: Color.Green, offsetX: 20, offsetY: 20,fill:true }).opacity(0.5)

      // 灰度效果0~1，越接近1，灰度越明显
      Text('grayscale').fontSize(15).fontColor(0xCCCCCC).width('90%')
      Image($r('app.media.image')).width('90%').height(30).grayscale(0.3)
      Image($r('app.media.image')).width('90%').height(30).grayscale(0.8)

      // 高光效果，1为正常图片，<1变暗，>1亮度增大
      Text('brightness').fontSize(15).fontColor(0xCCCCCC).width('90%')
      Image($r('app.media.image')).width('90%').height(30).brightness(1.2)

      // 饱和度，原图为1
      Text('saturate').fontSize(15).fontColor(0xCCCCCC).width('90%')
      Image($r('app.media.image')).width('90%').height(30).saturate(2.0)
      Image($r('app.media.image')).width('90%').height(30).saturate(0.7)

      // 对比度，1为原图，>1值越大越清晰，<1值越小越模糊
      Text('contrast').fontSize(15).fontColor(0xCCCCCC).width('90%')
      Image($r('app.media.image')).width('90%').height(30).contrast(2.0)
      Image($r('app.media.image')).width('90%').height(30).contrast(0.8)

      // 图像反转比例
      Text('invert').fontSize(15).fontColor(0xCCCCCC).width('90%')
      Image($r('app.media.image')).width('90%').height(30).invert(0.2)
      Image($r('app.media.image')).width('90%').height(30).invert(0.8)

      // 叠色添加
      Text('colorBlend').fontSize(15).fontColor(0xCCCCCC).width('90%')
      Image($r('app.media.image')).width('90%').height(30).colorBlend(Color.Green)
      Image($r('app.media.image')).width('90%').height(30).colorBlend(Color.Blue)

      // 深褐色
      Text('sepia').fontSize(15).fontColor(0xCCCCCC).width('90%')
      Image($r('app.media.image')).width('90%').height(30).sepia(0.8)

      // 色相旋转
      Text('hueRotate').fontSize(15).fontColor(0xCCCCCC).width('90%')
      Image($r('app.media.image')).width('90%').height(30).hueRotate(90)
    }.width('100%').margin({ top: 5 })
  }
}
```

![imageeffect](figures/imageeffect.png)


### 示例3

设置组件的内容线性渐变模糊效果。

```ts
// xxx.ets
@Entry
@Component
struct ImageExample1 {
  private_resource1:Resource = $r('app.media.testlinearGradientBlurOrigin')
  @State image_src: Resource = this.private_resource1
  build() {
    Column() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Start }) {
        Row({ space: 5 }) {
          Image(this.image_src)
            .linearGradientBlur(60, { fractionStops: [[0,0],[0,0.33],[1,0.66],[1,1]], direction: GradientDirection.Bottom })
        }
      }
    }
  }
}

```

![testlinearGradientBlur](figures/testlinearGradientBlur.png)

### 示例4
renderGroup示例
```ts
// xxx.ets
@Component
struct Component1 {
  @Prop renderGroupValue: boolean;
  build() {
    Row() {
      Row() {
        Row()
          .backgroundColor(Color.Black)
          .width(100)
          .height(100)
          .opacity(1)
      }
      .backgroundColor(Color.White)
      .width(150)
      .height(150)
      .justifyContent(FlexAlign.Center)
      .opacity(0.6)
      .renderGroup(this.renderGroupValue)
    }
    .backgroundColor(Color.Black)
    .width(200)
    .height(200)
    .justifyContent(FlexAlign.Center)
    .opacity(1)
  }
}
@Entry
@Component
struct RenderGroupExample {
  build() {
    Column() {
      Component1({renderGroupValue: true})
        .margin(20)
      Component1({renderGroupValue: false})
        .margin(20)
    }
    .width("100%")
    .height("100%")
    .alignItems(HorizontalAlign.Center)
  }
}
```

![renderGroup](figures/renderGroup.png)

### 示例5
单独使用blendMode
```ts
// xxx.ets
@Entry
@Component
struct Index {
  build() {
    Column() {
      Text("blendMode")
        .fontSize(20)
        .fontWeight(FontWeight.Bold)
        .fontColor('#ffff0101')
      Row() {
        Circle()
          .width(200)
          .height(200)
          .fill(Color.Green)
          .position({ x: 50, y: 50 })
        Circle()
          .width(200)
          .height(200)
          .fill(Color.Blue)
          .position({ x: 150, y: 50 })
      }
      .blendMode(BlendMode.OVERLAY,BlendApplyType.OFFSCREEN)
      .alignItems(VerticalAlign.Center)
      .height(300)
      .width('100%')
    }
    .height('100%')
    .width('100%')
    .backgroundImage($r('app.media.image'))
    .backgroundImageSize(ImageSize.Cover)
  }
}
```

<br/>BlendMode.OVERLAY,BlendApplyType.OFFSCREEN<br/>
![zh-cn_image_effect_blendMode2](figures/zh-cn_image_effect_blendMode.png)
<br/>不同的混合模式搭配是否需要离屏从而产生不同的效果。

### 示例6

blendMode搭配backgroundEffect实现文字异形模糊效果。<br/>
如果出现漏线问题，开发者应首先确保两个blendMode所在组件大小严格相同。如果确认相同，可能是组件边界落在浮点数坐标上导致，可尝试设置[pixelRound](ts-universal-attributes-layout-constraints.md#pixelRound11)通用属性，使产生的白线、暗线两侧的组件边界对齐到整数像素坐标上。

```ts
// xxx.ets
@Entry
@Component
struct Index {
  @State shColor: Color = Color.White;
  @State sizeDate: number = 20;
  @State rVal: number = 255;
  @State gVal: number = 255;
  @State bVal: number = 255;
  @State aVal: number = 0.1;
  @State rad: number = 40;
  @State satVal: number = 0.8;
  @State briVal: number = 1.5;
  build() {
    Stack() {
      Image($r('app.media.image'))
      Column() {
        Column({ space: 0 }) {
          Column() {
            Text('11')
              .fontSize(144)
              .fontWeight(FontWeight.Bold)
              .fontColor('rgba(255,255,255,1)')
              .fontFamily('HarmonyOS-Sans-Digit')
              .maxLines(1)
              .lineHeight(120 * 1.25)
              .height(120 * 1.25)
              .letterSpacing(4 * 1.25)
            Text('42')
              .fontSize(144)
              .fontWeight(FontWeight.Bold)
              .fontColor('rgba(255,255,255,1)')
              .fontFamily('HarmonyOS-Sans-Digit')
              .maxLines(1)
              .lineHeight(120 * 1.25)
              .height(120 * 1.25)
              .letterSpacing(4 * 1.25)
              .shadow({
                color: 'rgba(0,0,0,0)',
                radius: 20,
                offsetX: 0,
                offsetY: 0
              })
            Row() {
              Text('10月16日')
                .fontSize(this.sizeDate)
                .height(22)
                .fontWeight('medium')
                .fontColor('rgba(255,255,255,1)')
              Text('星期一')
                .fontSize(this.sizeDate)
                .height(22)
                .fontWeight('medium')
                .fontColor('rgba(255,255,255,1)')
            }
          }
          .blendMode(BlendMode.DST_IN, BlendApplyType.OFFSCREEN)
          .pixelRound({
            start: PixelRoundCalcPolicy.FORCE_FLOOR ,
            top: PixelRoundCalcPolicy.FORCE_FLOOR ,
            end: PixelRoundCalcPolicy.FORCE_CEIL,
            bottom: PixelRoundCalcPolicy.FORCE_CEIL
          })
        }
        .blendMode(BlendMode.SRC_OVER, BlendApplyType.OFFSCREEN)
        .backgroundEffect({
          radius: this.rad,
          saturation: this.satVal,
          brightness: this.briVal,
          color: this.getVolumeDialogWindowColor()
        })
        .justifyContent(FlexAlign.Center)
        .pixelRound({
          start: PixelRoundCalcPolicy.FORCE_FLOOR ,
          top: PixelRoundCalcPolicy.FORCE_FLOOR ,
          end: PixelRoundCalcPolicy.FORCE_CEIL,
          bottom: PixelRoundCalcPolicy.FORCE_CEIL
        })
      }
    }
  }
  getVolumeDialogWindowColor(): ResourceColor | string {
    return `rgba(${this.rVal.toFixed(0)}, ${this.gVal.toFixed(0)}, ${this.bVal.toFixed(0)}, ${this.aVal.toFixed(0)})`;
  }
}
```

![testDestinationIn_lockDemo](figures/testDestinationIn_lockDemo.jpeg)

### 示例7
通过 InvertOptions 实现反色。
```ts
// xxx.ets
 @Entry
 @Component
 struct Index {
   build() {
    Stack() {
      Column()
        Stack(){
          Image($r('app.media.r')).width('100%')
         Column(){
           Column().width("100%").height(30).invert({
             low:0,
             high:1,
             threshold:0.5,
             thresholdRange:0.2
           })
           Column().width("100%").height(30).invert({
             low:0.2,
             high:0.5,
             threshold:0.3,
             thresholdRange:0.2
           })
         }
        }
        .width('100%')
        .height('100%')
    }
  }
 }

```

![testDestinationIn_lockDemo](figures/testInvertOptions.png)

### 示例8
useShadowBatching搭配shadow实现同层阴影不重叠效果。
```ts
// xxx.ets
@Entry
@Component
struct UseShadowBatchingExample {
  build() {
    Column() {
      Column({ space: 10 }) {
        Stack() {

        }.width('90%').height(50).margin({ top: 5 }).backgroundColor(0xFFE4C4)
        .shadow({ radius: 120, color: Color.Green, offsetX: 0, offsetY: 0 })
        .align(Alignment.TopStart).shadow({ radius: 120, color: Color.Green, offsetX: 0, offsetY: 0 })

        Stack() {

        }.width('90%').height(50).margin({ top: 5 }).backgroundColor(0xFFE4C4)
        .align(Alignment.TopStart).shadow({ radius: 120, color: Color.Red, offsetX: 0, offsetY: 0 })
        .width('90%')
        .backgroundColor(Color.White)

        Column() {
          Text()
            .fontWeight(FontWeight.Bold)
            .fontSize(20)
            .fontColor(Color.White)
        }
        .justifyContent(FlexAlign.Center)
        .width(150)
        .height(150)
        .borderRadius(10)
        .backgroundColor(0xf56c6c)
        .shadow({ radius: 300, color: Color.Yellow, offsetX: 0, offsetY: 0 })

        Column() {
          Text()
            .fontWeight(FontWeight.Bold)
            .fontSize(20)
            .fontColor(Color.White)
        }
        .justifyContent(FlexAlign.Center)
        .width(150)
        .height(150)
        .backgroundColor(0x67C23A)
        .borderRadius(10)
        .translate({ y: -50})
        .shadow({ radius: 220, color: Color.Blue, offsetX: 0, offsetY: 0 })
      }
      .useShadowBatching(true)
    }
    .width('100%').margin({ top: 5 })
  }
}
```

![testUseShadowBatchingDemo](figures/testUseShadowBatching.png)
