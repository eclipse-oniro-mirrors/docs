# 组件内转场

组件内转场主要通过transition属性配置转场参数，在组件插入和删除时显示过渡动效，主要用于容器组件中的子组件插入和删除时，提升用户体验（需要配合[animateTo](ts-explicit-animation.md)才能生效，动效时长、曲线、延时跟随animateTo中的配置）。 

>  **说明：**
>
>  从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


## 属性


| 名称 | 参数类型 | 参数描述 |
| -------- | -------- | -------- |
| transition | [TransitionOptions](#transitionoptions参数说明) | 设置组件插入显示和删除隐藏的过渡效果。<br/>默认值：不设置任何过渡效果时，默认有透明度从0到1的过渡效果。若设置了其他过渡效果，以设置的过渡效果为准。<br/>**说明：** <br/>所有参数均为可选参数，详细描述见[TransitionOptions](#transitionoptions参数说明)参数说明。 |

## TransitionOptions参数说明

| 参数名称 | 参数类型 | 必填 | 参数描述 |
| -------- | -------- | -------- | -------- |
| type | [TransitionType](ts-appendix-enums.md#transitiontype)  | 否 | 默认包括组件新增和删除。<br/>默认值：TransitionType.All<br/>**说明：**<br/>不指定Type时说明插入删除使用同一种效果。 |
| opacity | number | 否 | 设置组件转场时的透明度效果，为插入时起点和删除时终点的值。<br/>默认值：1<br/>取值范围： [0, 1]<br/>**说明：** <br/>设置小于0或大于1的非法值时，按1处理。 |
| translate | {<br/>x?&nbsp;:&nbsp;number&nbsp;\|&nbsp;string,<br/>y?&nbsp;:&nbsp;number&nbsp;\|&nbsp;string,<br/>z?&nbsp;:&nbsp;number&nbsp;\|&nbsp;string<br/>} | 否 | 设置组件转场时的平移效果，为插入时起点和删除时终点的值。<br/>-x：横向的平移距离。<br/>-y：纵向的平移距离。<br/>-z：竖向的平移距离。|
| scale | {<br/>x?&nbsp;:&nbsp;number,<br/>y?&nbsp;:&nbsp;number,<br/>z?&nbsp;:&nbsp;number,<br/>centerX?&nbsp;:&nbsp;number&nbsp;\|&nbsp;string,<br/>centerY?&nbsp;:&nbsp;number&nbsp;\|&nbsp;string<br/>} | 否 | 设置组件转场时的缩放效果，为插入时起点和删除时终点的值。<br/>-x：横向放大倍数（或缩小比例）。<br/>-y：纵向放大倍数（或缩小比例）。<br/>-z：当前为二维显示，该参数无效 。<br/>-&nbsp;centerX、centerY指缩放中心点，centerX和centerY默认值是"50%"。<br/>-&nbsp;中心点为0时，默认的是组件的左上角。 |
| rotate | {<br/>x?:&nbsp;number,<br/>y?:&nbsp;number,<br/>z?:&nbsp;number,<br/>angle:&nbsp;number&nbsp;\|&nbsp;string,<br/>centerX?:&nbsp;number&nbsp;\|&nbsp;string,<br/>centerY?:&nbsp;number&nbsp;\|&nbsp;string<br/>} | 否 | 设置组件转场时的旋转效果，为插入时起点和删除时终点的值。<br/>-x：横向的旋转向量。<br/>-y：纵向的旋转向量。<br/>-z：竖向的旋转向量。<br/>-&nbsp;centerX,centerY指旋转中心点，centerX和centerY默认值是"50%"。<br/>-&nbsp;中心点为（0，0）时，默认的是组件的左上角。 |


## 示例

```ts
// xxx.ets
@Entry
@Component
struct TransitionExample {
  @State flag: boolean = true
  @State show: string = 'show'

  build() {
    Column() {
      Button(this.show).width(80).height(30).margin(30)
        .onClick(() => {
          // 点击Button控制Image的显示和消失
          animateTo({ duration: 1000 }, () => {
            if (this.flag) {
              this.show = 'hide'
            } else {
              this.show = 'show'
            }
            this.flag = !this.flag
          })
        })
      if (this.flag) {
        // Image的显示和消失配置为不同的过渡效果
        Image($r('app.media.testImg')).width(300).height(300)
          .transition({ type: TransitionType.Insert, scale: { x: 0, y: 1.0 } })
          .transition({ type: TransitionType.Delete, rotate: { angle: 180 } })
      }
    }.width('100%')
  }
}
```

示意图：

图片完全显示时：

![animationComponent1](figures/animationComponent1.png)

图片消失时配置顺时针旋转180°的过渡效果：

![animationComponent3](figures/animationComponent3.png)

图片完全消失时：

![animationComponent2](figures/animationComponent2.png)

图片显示时配置横向放大一倍的过渡效果：

![animationComponent4](figures/animationComponent4.png)