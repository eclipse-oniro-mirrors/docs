# 安全区域

安全区域是指页面的显示区域，默认不与系统设置的非安全区域比如状态栏、导航栏区域重叠，默认情况下开发者开发的界面都被布局在安全区域内。提供属性方法允许开发者设置组件绘制内容突破安全区域的限制，通过expandSafeArea属性支持组件不改变布局情况下扩展其绘制区域至安全区外，通过设置setKeyboardAvoidMode来配置虚拟键盘弹出时页面的避让模式。

> **说明：**
>
> 从API Version 10开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。
> 默认摄像头挖孔区域不为非安全区域，页面不避让挖孔。

## expandSafeArea

expandSafeArea(types?: Array&lt;SafeAreaType&gt;, edges?: Array&lt;SafeAreaEdge&gt;)

控制组件扩展其安全区域。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型                                               | 必填 | 说明                                                         |
| ------ | -------------------------------------------------- | ---- | ------------------------------------------------------------ |
| types  | Array <[SafeAreaType](ts-types.md#safeareatype10)> | 否   | 非必填，配置扩展安全区域的类型。页面不避让挖孔时, CUTOUT类型不生效。<br />默认值: <br />[SafeAreaType.SYSTEM, SafeAreaType.CUTOUT, SafeAreaType.KEYBOARD] |
| edges  | Array <[SafeAreaEdge](ts-types.md#safeareaedge10)> | 否   | 非必填，配置扩展安全区域的方向。<br /> [SafeAreaEdge.TOP, SafeAreaEdge.BOTTOM, SafeAreaEdge.START, SafeAreaEdge.END]<br />扩展至所有非安全区域。 |

>  **说明：**
>
>  设置expandSafeArea属性进行组件绘制扩展时，组件不能设置固定宽高尺寸（百分比除外）。
>
>  安全区域不会限制内部组件的布局和大小，不会裁剪内部组件。
>
>  当父容器是滚动容器时，设置expandSafeArea属性不生效。
>
>  设置expandSafeArea()时，不传参，走默认值处理；设置expandSafeArea([],[])时，相当于入参是空数组，此时设置expandSafeArea属性不生效。

## setKeyboardAvoidMode<sup>11+</sup>

setKeyboardAvoidMode(value: KeyboardAvoidMode): void

控制虚拟键盘抬起时页面的避让模式。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型                                                 | 必填 | 说明                                                         |
| ------ | ---------------------------------------------------- | ---- | ------------------------------------------------------------ |
| value  | [KeyboardAvoidMode](ts-types.md#keyboardavoidmode11) | 是   | 控制虚拟键盘抬起时页面的避让模式。<br />默认值: KeyboardAvoidMode.OFFSET <br />键盘抬起时默认页面避让模式为上抬模式。<br />必填，配置虚拟键盘避让时的页面避让模式。 |

>  **说明：**
>  KeyboardAvoidMode.RESIZE是压缩Page的大小，Page下设置百分比宽高的组件会跟随Page压缩，直接设置宽高的组件会按设置的固定大小布局。
>
>  设置KeyboardAvoidMode.RESIZE时，expandSafeArea([SafeAreaType.KEYBOARD],[SafeAreaEdge.BOTTOM])不生效。

## getKeyboardAvoidMode

getKeyboardAvoidMode(): KeyboardAvoidMode

返回虚拟键盘抬起时的页面避让模式。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**返回值：** 

| 名称                                                 | 说明                               |
| ---------------------------------------------------- | ---------------------------------- |
| [KeyboardAvoidMode](ts-types.md#keyboardavoidmode11) | 返回虚拟键盘抬起时的页面避让模式。 |

## 示例

### 示例1

```ts
// xxx.ets
@Entry
@Component
struct SafeAreaExample1 {
  @State text: string = ''
  controller: TextInputController = new TextInputController()

  build() {
    Row() {
        Column()
          .height('100%').width('100%')
          .backgroundImage($r('app.media.bg')).backgroundImageSize(ImageSize.Cover)
          .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.BOTTOM])
    }.height('100%')
  }
}
```

![expandSafeArea1](figures/expandSafeArea1.png)

### 示例2

```ts
// xxx.ets
@Entry
@Component
struct SafeAreaExample {
  @State text: string = ''
  controller: TextInputController = new TextInputController()

  build() {
    Row() {
      Stack() {
        Column()
          .height('100%').width('100%')
          .backgroundImage($r('app.media.bg')).backgroundImageSize(ImageSize.Cover)
          .expandSafeArea([SafeAreaType.KEYBOARD, SafeAreaType.SYSTEM])
        Column() {
          Button('Set caretPosition 1')
            .onClick(() => {
              this.controller.caretPosition(1)
            })
          TextInput({ text: this.text, placeholder: 'input your word...', controller: this.controller })
            .placeholderFont({ size: 14, weight: 400 })
            .width(320).height(40).offset({y: 120})
            .fontSize(14).fontColor(Color.Black)
            .backgroundColor(Color.White)
        }.width('100%').alignItems(HorizontalAlign.Center)
      }
    }.height('100%')
  }
}
```

![expandSafeArea2](figures/expandSafeArea2.png)

### 示例3

```ts
// EntryAbility.ets
import { KeyboardAvoidMode } from '@ohos.arkui.UIContext';

  onWindowStageCreate(windowStage: window.WindowStage) {
    // Main window is created, set main page for this ability
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onWindowStageCreate');

    windowStage.loadContent('pages/Index', (err, data) => {
      let keyboardAvoidMode  = windowStage.getMainWindowSync().getUIContext().getKeyboardAvoidMode();
     // 设置虚拟键盘抬起时压缩页面大小为减去键盘的高度
  windowStage.getMainWindowSync().getUIContext().setKeyboardAvoidMode(KeyboardAvoidMode.RESIZE);
      if (err.code) {
        hilog.error(0x0000, 'testTag', 'Failed to load the content. Cause: %{public}s', JSON.stringify(err) ?? '');
        return;
      }
      hilog.info(0x0000, 'testTag', 'Succeeded in loading the content. Data: %{public}s', JSON.stringify(data) ?? '');
    });
  }

// xxx.ets
@Entry
@Component
struct KeyboardAvoidExample {
    build() {
    Column() {
      Row().height("30%").width("100%").backgroundColor(Color.Gray)
      TextArea().width("100%").borderWidth(1)
      Text("I can see the bottom of the page").width("100%").textAlign(TextAlign.Center).backgroundColor(Color.Pink).layoutWeight(1)
    }.width('100%').height("100%")
  }
}
```

![keyboardAvoidMode1](figures/keyboardAvoidMode1.jpg)

### 示例4

```ts
// EntryAbility.ets
import { KeyboardAvoidMode } from '@ohos.arkui.UIContext';

  onWindowStageCreate(windowStage: window.WindowStage) {
    // Main window is created, set main page for this ability
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onWindowStageCreate');

    windowStage.loadContent('pages/Index', (err, data) => {
      let keyboardAvoidMode  = windowStage.getMainWindowSync().getUIContext().getKeyboardAvoidMode();
     // 设置虚拟键盘抬起时把页面上抬直到露出光标
  windowStage.getMainWindowSync().getUIContext().setKeyboardAvoidMode(KeyboardAvoidMode.OFFSET);
      if (err.code) {
        hilog.error(0x0000, 'testTag', 'Failed to load the content. Cause: %{public}s', JSON.stringify(err) ?? '');
        return;
      }
      hilog.info(0x0000, 'testTag', 'Succeeded in loading the content. Data: %{public}s', JSON.stringify(data) ?? '');
    });
  }

// xxx.ets
@Entry
@Component
struct KeyboardAvoidExample {
    build() {
    Column() {
      Row().height("30%").width("100%").backgroundColor(Color.Gray)
      TextArea().width("100%").borderWidth(1)
      Text("I can see the bottom of the page").width("100%").textAlign(TextAlign.Center).backgroundColor(Color.Pink).layoutWeight(1)
    }.width('100%').height("100%")
  }
}
```

![keyboardAvoidMode1](figures/keyboardAvoidMode2.jpg)