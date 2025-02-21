# RotationGesture

用于触发旋转手势事件，触发旋转手势的最少手指为2指，最大为5指，最小改变度数为1度。

>  **说明：**
>
>  从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


## 接口

RotationGesture(value?: { fingers?: number, angle?: number })

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**参数：**

| 参数名称 | 参数类型 | 必填 | 参数描述 |
| -------- | -------- | -------- | -------- |
| fingers | number | 否 | 触发旋转的最少手指数,&nbsp;最小为2指，最大为5指。<br/>默认值：2 <br/>触发手势手指可以多于fingers数目，但只有先落下的两指参与手势计算。|
| angle | number | 否 | 触发旋转手势的最小改变度数，单位为deg。<br/>默认值：1 <br/>**说明：** <br/>当改变度数的值小于等于0或大于360时，会被转化为默认值。|


## 事件

| 名称 | 功能描述 |
| -------- | -------- |
| onActionStart(event:(event:&nbsp;[GestureEvent](ts-gesture-settings.md#gestureevent对象说明))&nbsp;=&gt;&nbsp;void) | Rotation手势识别成功回调。 <br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。|
| onActionUpdate(event:(event:&nbsp;[GestureEvent](ts-gesture-settings.md#gestureevent对象说明))&nbsp;=&gt;&nbsp;void) | Rotation手势移动过程中回调。 <br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。|
| onActionEnd(event:(event:&nbsp;[GestureEvent](ts-gesture-settings.md#gestureevent对象说明))&nbsp;=&gt;&nbsp;void) | Rotation手势识别成功，手指抬起后触发回调。 <br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。|
| onActionCancel(event:&nbsp;()&nbsp;=&gt;&nbsp;void) | Rotation手势识别成功，接收到触摸取消事件触发回调。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。|

## 属性

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

| 名称 | 类型    |描述                                        |
| ----  | ------  | ---------------------------------------- |
| tag<sup>11+</sup>   | string  | 设置Rotation手势标志，用于自定义手势判定时区分绑定的手势。|

## 示例

该示例通过配置RotationGesture实现了双指旋转手势的识别。

```ts
// xxx.ets
@Entry
@Component
struct RotationGestureExample {
  @State angle: number = 0
  @State rotateValue: number = 0

  build() {
    Column() {
      Column() {
        Text('RotationGesture angle:' + this.angle)
      }
      .height(200)
      .width(300)
      .padding(20)
      .border({ width: 3 })
      .margin(80)
      .rotate({ angle: this.angle })
      // 双指旋转触发该手势事件
      .gesture(
      RotationGesture()
        .onActionStart((event: GestureEvent) => {
          console.info('Rotation start')
        })
        .onActionUpdate((event: GestureEvent) => {
          if (event) {
            this.angle = this.rotateValue + event.angle
          }
        })
        .onActionEnd((event: GestureEvent) => {
          this.rotateValue = this.angle
          console.info('Rotation end')
        })
      )
    }.width('100%')
  }
}
```

 ![zh-cn_image_0000001174264372](figures/zh-cn_image_0000001174264372.png ) 