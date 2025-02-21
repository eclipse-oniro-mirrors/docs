# 单选框（Radio）


Radio是单选框组件，通常用于提供相应的用户交互选择项，同一组的Radio中只有一个可以被选中。具体用法请参考[Radio](../reference/arkui-ts/ts-basic-components-radio.md)。


## 创建单选框

Radio通过调用接口来创建，接口调用形式如下：


```ts
Radio(options: {value: string, group: string})
```

  该接口用于创建一个单选框，其中value是单选框的名称，group是单选框的所属群组名称。checked属性可以设置单选框的状态，状态分别为false和true时，设置为true时表示单选框被选中。Radio仅支持选中和未选中两种样式，不支持自定义颜色和形状。

```ts
Radio({ value: 'Radio1', group: 'radioGroup' })
  .checked(false)
Radio({ value: 'Radio2', group: 'radioGroup' })
  .checked(true)
```


![zh-cn_image_0000001562820821](figures/zh-cn_image_0000001562820821.png)


## 添加事件

除支持[通用事件](../reference/arkui-ts/ts-universal-events-click.md)外，Radio通常用于选中后触发某些操作，可以绑定onChange事件来响应选中操作后的自定义行为。



```ts
  Radio({ value: 'Radio1', group: 'radioGroup' })
    .onChange((isChecked: boolean) => {
      if(isChecked) {
        //需要执行的操作
      }
    })
  Radio({ value: 'Radio2', group: 'radioGroup' })
    .onChange((isChecked: boolean) => {
      if(isChecked) {
        //需要执行的操作
      }
    })
```


## 场景示例

通过点击Radio切换声音模式。


```ts
// xxx.ets
import promptAction from '@ohos.promptAction';
@Entry
@Component
struct RadioExample {
  build() {
    Row() {
      Column() {
        Radio({ value: 'Radio1', group: 'radioGroup' }).checked(true)
          .height(50)
          .width(50)
          .onChange((isChecked: boolean) => {
            if(isChecked) {
              // 切换为响铃模式
              promptAction.showToast({ message: 'Ringing mode.' })
            }
          })
        Text('Ringing')
      }
      Column() {
        Radio({ value: 'Radio2', group: 'radioGroup' })
          .height(50)
          .width(50)
          .onChange((isChecked: boolean) => {
            if(isChecked) {
              // 切换为振动模式
              promptAction.showToast({ message: 'Vibration mode.' })
            }
          })
        Text('Vibration')
      }
      Column() {
        Radio({ value: 'Radio3', group: 'radioGroup' })
          .height(50)
          .width(50)
          .onChange((isChecked: boolean) => {
            if(isChecked) {
              // 切换为静音模式
              promptAction.showToast({ message: 'Silent mode.' })
            }
          })
        Text('Silent')
      }
    }.height('100%').width('100%').justifyContent(FlexAlign.Center)
  }
}
```


![zh-cn_image_0000001562700457](figures/zh-cn_image_0000001562700457.png)
