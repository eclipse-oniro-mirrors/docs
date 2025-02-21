# Marquee

跑马灯组件，用于滚动展示一段单行文本。仅当文本内容宽度超过跑马灯组件宽度时滚动，不超过时不滚动。


>  **说明：**
>
>  该组件从API Version 8开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。
>
>  为了不影响滚动帧率，建议在滚动类组件中Marquee的个数不超过4个，或者使用[Text](ts-basic-components-text.md)组件的[TextOverflow.MARQUEE](ts-appendix-enums.md#textoverflow)替代。

## 子组件

无


## 接口

Marquee(value: { start: boolean, step?: number, loop?: number, fromStart?: boolean, src: string })

从API version 9开始，该接口支持在ArkTS卡片中使用。

**参数：**

| 参数名 | 参数类型 | 必填 | 参数描述 |
| -------- | -------- | -------- | -------- |
| start | boolean | 是 | 控制跑马灯是否进入播放状态。<br/>**说明：**<br/>有限的滚动次数播放完毕后，不可以通过改变start重置滚动次数重新开始播放。 |
| step | number | 否 | 滚动动画文本滚动步长，当step大于Marquee的文本宽度时，取默认值。<br/>默认值：6，单位vp |
| loop | number | 否 | 设置重复滚动的次数，小于等于零时无限循环。<br/>默认值：-1<br/>**说明：**<br/>ArkTS卡片上该参数设置任意值都仅在可见时滚动一次。 |
| fromStart | boolean | 否 | 设置文本从头开始滚动或反向滚动。<br/>默认值：true |
| src | string | 是 | 需要滚动的文本。 |

## 属性
除支持文本通用属性：fontColor、fontSize、fontWeight、fontFamily外，还支持以下属性：
| 名称       | 参数类型 | 描述                                                         |
| ---------- | -------- | ------------------------------------------------------------ |
| allowScale | boolean  | 是否允许文本缩放。<br/>默认值：false<br/>**说明：**<br/>仅当fontSize为fp单位时生效。 |

## 事件

| 名称 | 功能描述 |
| -------- | -------- |
| onStart(event:&nbsp;()&nbsp;=&gt;&nbsp;void) | 当滚动的文本内容变化或者开始滚动时触发回调。<br/>从API version 9开始，该接口支持在ArkTS卡片中使用。 |
| onBounce(event:&nbsp;()&nbsp;=&gt;&nbsp;void) | 完成一次滚动时触发，若循环次数不为1，则该事件会多次触发。<br/>从API version 9开始，该接口支持在ArkTS卡片中使用。 |
| onFinish(event:&nbsp;()&nbsp;=&gt;&nbsp;void) | 滚动全部循环次数完成时触发回调。<br/>从API version 9开始，该接口支持在ArkTS卡片中使用。 |


## 示例


```ts
// xxx.ets
@Entry
@Component
struct MarqueeExample {
  @State start: boolean = false
  private fromStart: boolean = true
  private step: number = 50
  private loop: number = Number.POSITIVE_INFINITY
  private src: string = "Running Marquee starts rolling"

  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Marquee({
        start: this.start,
        step: this.step,
        loop: this.loop,
        fromStart: this.fromStart,
        src: this.src
      })
        .width(360)
        .height(80)
        .fontColor('#FFFFFF')
        .fontSize(48)
        .fontWeight(700)
        .backgroundColor('#182431')
        .margin({ bottom: 40 })
        .onStart(() => {
          console.info('Marquee animation complete onStart')
        })
        .onBounce(() => {
          console.info('Marquee animation complete onBounce')
        })
        .onFinish(() => {
          console.info('Marquee animation complete onFinish')
        })
      Button('Start')
        .onClick(() => {
          this.start = true
        })
        .width(120)
        .height(40)
        .fontSize(16)
        .fontWeight(500)
        .backgroundColor('#007DFF')
    }
    .width('100%')
    .height('100%')
  }
}
```

![marquee](figures/marquee.gif)