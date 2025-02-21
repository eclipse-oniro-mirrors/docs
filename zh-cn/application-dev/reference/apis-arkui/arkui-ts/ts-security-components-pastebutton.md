# PasteButton


安全控件的粘贴按钮，用户通过点击该粘贴按钮，可以临时获取读取剪贴板权限。


> **说明：**
>
> 该组件从API Version 10开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


## 子组件

不支持。


## 接口
### PasteButton
PasteButton()

默认创建带有图标、文本、背景的粘贴按钮。

### PasteButton
PasteButton(option:PasteButtonOptions)

创建包含指定元素的粘贴按钮。

**参数：**

| 参数名 | 参数类型 | 必填 | 参数描述 |
| -------- | -------- | -------- | -------- |
| option | [PasteButtonOptions](#pastebuttonoptions) | 否 | 创建包含指定元素的粘贴按钮。<br/>默认值：<br/>{<br/>icon: PasteIconStyle.LINES,<br/>text: PasteDescription.PASTE,<br/>buttonType: ButtonType.Capsule <br/>} |

## PasteButtonOptions

| 名称 | 类型 | 必填 | 描述 |
| -------- | -------- | -------- | -------- |
| icon | [PasteIconStyle](#pasteiconstyle枚举说明) | 否 | 设置粘贴按钮的图标风格。<br/>不传入该参数表示没有图标，icon和text至少存在一个。 |
| text | [PasteDescription](#pastedescription枚举说明) | 否 | 设置粘贴按钮的文本描述。<br/>不传入该参数表示没有文字描述，icon和text至少存在一个。 |
| buttonType | [ButtonType](ts-basic-components-button.md#buttontype枚举说明) | 否 | 设置粘贴按钮的背景样式。<br/>不传入该参数表示没有背景。 |


## 属性

不支持通用属性，仅继承[安全控件通用属性](ts-securitycomponent-attributes.md#属性)。


## PasteIconStyle枚举说明

| 名称 | 枚举值 | 描述 |
| -------- | -------- | -------- |
| LINES | 0 | 粘贴按钮展示线条样式图标。 |


## PasteDescription枚举说明

| 名称 | 枚举值 | 描述 |
| -------- | -------- | -------- |
| PASTE | 0 | 粘贴按钮的文字描述为“粘贴”。 |


## PasteButtonOnClickResult枚举说明

| 名称 | 枚举值 | 描述 |
| -------- | -------- | -------- |
| SUCCESS | 0 | 粘贴按钮点击成功。 |
| TEMPORARY_AUTHORIZATION_FAILED | 1 | 粘贴按钮点击后权限授权失败。 |


## 事件

不支持通用事件，仅支持以下事件：

| 名称 | 功能描述 |
| -------- | -------- |
| onClick(event: (event: [ClickEvent](ts-universal-events-click.md#clickevent对象说明), result: [PasteButtonOnClickResult](#pastebuttononclickresult枚举说明)) =&gt; void) | 点击动作触发该回调。<br/>result：剪贴板权限的授权结果，授权后可以读取当前剪贴板内容。<br/>event：见ClickEvent对象说明。 |


## 示例

```
// xxx.ets
@Entry
@Component
struct Index {
  build() {
    Row() {
      Column({space:10}) {
        // 默认参数下，图标、文字、背景都存在
        PasteButton().onClick((event: ClickEvent, result: PasteButtonOnClickResult)=>{
          console.info("result " + result)
        })
        // 传入参数即表示元素存在，不传入的参数表示元素不存在，例如：只显示图标
        PasteButton({icon:PasteIconStyle.LINES})
        // 只显示图标+背景
        PasteButton({icon:PasteIconStyle.LINES, buttonType:ButtonType.Capsule})
        // 图标、文字、背景都存在
        PasteButton({icon:PasteIconStyle.LINES, text:PasteDescription.PASTE, buttonType:ButtonType.Capsule})
      }.width('100%')
    }.height('100%')
  }
}
```

![zh-cn_image_0000001593677984](figures/zh-cn_image_0000001593677984.png)
