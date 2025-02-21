# Popup控制

给组件绑定popup弹窗，并设置弹窗内容，交互逻辑和显示状态。

>  **说明：**
>
> - 从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。
>  
> - popup弹窗的显示状态在onStateChange事件回调中反馈，其显隐与组件的创建或销毁无强对应关系。


## 接口


| 名称        | 参数类型                                     | 描述                                       |
| --------- | ---------------------------------------- | ---------------------------------------- |
| bindPopup | show:&nbsp;boolean,<br/>popup:&nbsp;[PopupOptions](#popupoptions类型说明)&nbsp;\|&nbsp;[CustomPopupOptions](#custompopupoptions8类型说明)<sup>8+</sup> | 给组件绑定Popup弹窗，设置参数show为true弹出弹框。<br/>show:&nbsp;弹窗显示状态，默认值为false，隐藏弹窗。popup弹窗必须等待页面全部构建完成才能展示，因此show不能在页面构建中设置为true，否则会导致popup弹窗显示位置及形状错误。<br/>popup:&nbsp;配置当前弹窗提示的参数。 |

## PopupOptions类型说明

| 名称                           | 类型                                       | 必填   | 描述                                       |
| ---------------------------- | ---------------------------------------- | ---- | ---------------------------------------- |
| message                      | string                                   | 是    | 弹窗信息内容。                                  |
| placementOnTop               | boolean                                  | 否    | 是否在组件上方显示，默认值为false。                     |
| primaryButton                | {<br/>value:&nbsp;string,<br/>action:&nbsp;()&nbsp;=&gt;&nbsp;void<br/>} | 否    | 第一个按钮。<br/>value:&nbsp;弹窗里主按钮的文本。<br/>action:&nbsp;点击主按钮的回调函数。 |
| secondaryButton              | {<br/>value:&nbsp;string,<br/>action:&nbsp;()&nbsp;=&gt;&nbsp;void<br/>} | 否    | 第二个按钮。<br/>value:&nbsp;弹窗里辅助按钮的文本。<br/>action:&nbsp;点击辅助按钮的回调函数。 |
| onStateChange                | (event:&nbsp;{&nbsp;isVisible:&nbsp;boolean&nbsp;})&nbsp;=&gt;&nbsp;void | 否    | 弹窗状态变化事件回调，参数isVisible为弹窗当前的显示状态。        |
| arrowOffset<sup>9+</sup>     | [Length](ts-types.md#length)             | 否    | popup箭头在弹窗处的偏移。箭头在气泡上下方时，数值为0表示箭头居最左侧，偏移量为箭头至最左侧的距离，默认居中。箭头在气泡左右侧时，偏移量为箭头至最上侧的距离，默认居中。如果显示在屏幕边缘，气泡会自动左右偏移，数值为0时箭头始终指向绑定组件。 |
| showInSubWindow<sup>9+</sup> | boolean                                  | 否    | 是否在子窗口显示气泡，默认值为false。                    |

## CustomPopupOptions<sup>8+</sup>类型说明

| 名称                         | 类型                                                         | 必填 | 描述                                                         |
| ---------------------------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| builder                      | [CustomBuilder](ts-types.md#custombuilder8)                  | 是   | 提示气泡内容的构造器。<br />**说明：**<br />popup为通用属性，自定义popup中不支持再次弹出popup。对builder下的第一层容器组件不支持使用position属性，如果使用将导致气泡不显示。builder中若使用自定义组件，自定义组件的aboutToAppear和aboutToDisappear生命周期与popup弹窗的显隐无关，不能使用其生命周期判断popup弹窗的显隐。 |
| placement                    | [Placement](ts-appendix-enums.md#placement8)                 | 否   | 气泡组件优先显示的位置，当前位置显示不下时，会自动调整位置。<br/>默认值：Placement.Bottom |
| popupColor                   | [ResourceColor](ts-types.md#resourcecolor)                   | 否   | 提示气泡的颜色。                                             |
| enableArrow                  | boolean                                                      | 否   | 是否显示箭头。<br/>从API Version 9开始，如果箭头所在方位侧的气泡长度不足以显示下箭头，则会默认不显示箭头。比如：placement设置为Left，此时如果气泡高度小于箭头的宽度（32vp）与气泡圆角两倍（48vp）之和（80vp），则实际不会显示箭头。<br/>默认值：true |
| autoCancel                   | boolean                                                      | 否   | 页面有操作时，是否自动关闭气泡。<br/>默认值：true            |
| onStateChange                | (event:&nbsp;{&nbsp;isVisible:&nbsp;boolean&nbsp;})&nbsp;=&gt;&nbsp;void | 否   | 弹窗状态变化事件回调，参数为弹窗当前的显示状态。             |
| maskColor                    | [Color](ts-appendix-enums.md#color)&nbsp;\|&nbsp;number&nbsp;\|&nbsp;string&nbsp;\|&nbsp;[Resource](#resource) | 否   | 设置气泡遮罩层颜色。                                         |
| arrowOffset<sup>9+</sup>     | [Length](ts-types.md#length)                                 | 否   | popup箭头在弹窗处的偏移。箭头在气泡上下方时，数值为0表示箭头居最左侧，偏移量为箭头至最左侧的距离，默认居中。箭头在气泡左右侧时，偏移量为箭头至最上侧的距离，默认居中。如果显示在屏幕边缘，气泡会自动左右偏移，数值为0时箭头始终指向绑定组件。 |
| showInSubWindow<sup>9+</sup> | boolean                                                      | 否   | 是否在子窗口显示气泡，默认值为false。                        |


## 示例
```ts
// xxx.ets
@Entry
@Component
struct PopupExample {
  @State handlePopup: boolean = false
  @State customPopup: boolean = false

  // popup构造器定义弹框内容
  @Builder popupBuilder() {
    Row({ space: 2 }) {
      Image($r("app.media.icon")).width(24).height(24).margin({ left: -5 })
      Text('Custom Popup').fontSize(10)
    }.width(100).height(50).padding(5)
  }

  build() {
    Flex({ direction: FlexDirection.Column }) {
      // PopupOptions 类型设置弹框内容
      Button('PopupOptions')
        .onClick(() => {
          this.handlePopup = !this.handlePopup
        })
        .bindPopup(this.handlePopup, {
          message: 'This is a popup with PopupOptions',
          placementOnTop: true,
          showInSubWindow:false,
          primaryButton: {
            value: 'confirm',
            action: () => {
              this.handlePopup = !this.handlePopup
              console.info('confirm Button click')
            }
          },
          // 第二个按钮
          secondaryButton: {
            value: 'cancel',
            action: () => {
              this.handlePopup = !this.handlePopup
              console.info('cancel Button click')
            }
          },
          onStateChange: (e) => {
            console.info(JSON.stringify(e.isVisible))
            if (!e.isVisible) {
              this.handlePopup = false
            }
          }
        })
        .position({ x: 100, y: 50 })


      // CustomPopupOptions 类型设置弹框内容
      Button('CustomPopupOptions')
        .onClick(() => {
          this.customPopup = !this.customPopup
        })
        .bindPopup(this.customPopup, {
          builder: this.popupBuilder,
          placement: Placement.Top,
          maskColor: '0x33000000',
          popupColor: Color.Yellow,
          enableArrow: true,
          showInSubWindow: false,
          onStateChange: (e) => {
            if (!e.isVisible) {
              this.customPopup = false
            }
          }
        })
        .position({ x: 80, y: 200 })
    }.width('100%').padding({ top: 5 })
  }
}
```

![figures/popup.gif](figures/popup.gif)
