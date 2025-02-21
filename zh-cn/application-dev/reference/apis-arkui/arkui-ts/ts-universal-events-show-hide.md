# 挂载卸载事件

挂载卸载事件指组件从组件树上挂载、卸载时触发的事件。

> **说明：**
>
> 从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。

## onAppear

onAppear(event: () => void): T

组件挂载显示时触发此回调。

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| T | 返回当前组件。 |

**卡片能力：** 从API version 9开始，该接口支持在ArkTS卡片中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

## onDisAppear

onDisAppear(event: () => void): T

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| T | 返回当前组件。 |

组件卸载消失时触发此回调。

**卡片能力：** 从API version 9开始，该接口支持在ArkTS卡片中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full


## 示例

```ts
// xxx.ets
import promptAction from '@ohos.promptAction'

@Entry
@Component
struct AppearExample {
  @State isShow: boolean = true
  @State changeAppear: string = '点我卸载挂载组件'
  private myText: string = 'Text for onAppear'

  build() {
    Column() {
      Button(this.changeAppear)
        .onClick(() => {
          this.isShow = !this.isShow
        }).margin(15)
      if (this.isShow) {
        Text(this.myText).fontSize(26).fontWeight(FontWeight.Bold)
          .onAppear(() => {
            promptAction.showToast({
              message: 'The text is shown',
              duration: 2000,
              bottom: 500
            })
          })
          .onDisAppear(() => {
            promptAction.showToast({
              message: 'The text is hidden',
              duration: 2000,
              bottom: 500
            })
          })
      }
    }.padding(30).width('100%')
  }
}
```

![zh-cn_image_0000001219864151](figures/zh-cn_image_0000001219864151.gif)
