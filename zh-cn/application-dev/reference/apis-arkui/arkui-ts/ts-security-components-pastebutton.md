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

为避免控件样式不合法导致授权失败，请开发者先了解安全控件样式的[约束与限制](../../../security/AccessToken/security-component-overview.md#约束与限制)。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### PasteButton

PasteButton(options: PasteButtonOptions)

创建包含指定元素的粘贴按钮。

为避免控件样式不合法导致授权失败，请开发者先了解安全控件样式的[约束与限制](../../../security/AccessToken/security-component-overview.md#约束与限制)。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| options | [PasteButtonOptions](#pastebuttonoptions) | 是 | 创建包含指定元素的粘贴按钮。<br/>默认值：<br/>{<br/>icon: PasteIconStyle.LINES,<br/>text: PasteDescription.PASTE,<br/>buttonType: ButtonType.Capsule <br/>} |

## PasteButtonOptions

用于指定粘贴按钮的图标、文本等指定元素。

> **说明：**
> 
> - icon或text需至少传入一个。<br>
> - 如果icon、text都不传入，[PasteButton](#pastebutton-1)中的options参数不起效，创建的PasteButton为默认样式，默认样式：
>
>   PasteIconStyle默认样式为LINES；
>
>   PasteDescription默认样式为PASTE；
>
>   ButtonType默认样式为Capsule。
> - icon、text、buttonType不支持动态修改。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| icon | [PasteIconStyle](#pasteiconstyle枚举说明) | 否 | 设置粘贴按钮的图标风格。<br/>不传入该参数表示没有图标。 |
| text | [PasteDescription](#pastedescription枚举说明) | 否 | 设置粘贴按钮的文本描述。<br/>不传入该参数表示没有文字描述。 |
| buttonType | [ButtonType](ts-basic-components-button.md#buttontype枚举说明) | 否 | 设置粘贴按钮的背景样式。<br/>不传入该参数，系统默认提供Capsule类型按钮。 |

## 属性

不支持通用属性，仅继承[安全控件通用属性](ts-securitycomponent-attributes.md#属性)。

## PasteIconStyle枚举说明

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| LINES | 0 | 粘贴按钮展示线条样式图标。 |

## PasteDescription枚举说明

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| PASTE | 0 | 粘贴按钮的文字描述为“粘贴”。 |

## PasteButtonOnClickResult枚举说明

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| SUCCESS | 0 | 粘贴按钮点击成功。 |
| TEMPORARY_AUTHORIZATION_FAILED | 1 | 粘贴按钮点击后权限授权失败。 |

## 事件

不支持通用事件，仅支持以下事件：

### onClick

onClick(event: (event: ClickEvent, result: PasteButtonOnClickResult) =&gt; void)

点击动作触发该回调。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型                   | 必填 | 说明                   |
|------------|------|-------|---------|
| event  | [ClickEvent](ts-universal-events-click.md#clickevent对象说明) |是 |见ClickEvent对象说明。|
| result | [PasteButtonOnClickResult](#pastebuttononclickresult枚举说明)| 是 | 剪贴板权限的授权结果，授权后可以读取当前剪贴板内容。|

## 示例

```ts
// xxx.ets
@Entry
@Component
struct Index {
  build() {
    Row() {
      Column({ space: 10 }) {
        // 默认参数下，图标、文字、背景都存在。
        PasteButton().onClick((event: ClickEvent, result: PasteButtonOnClickResult) => {
          console.info("result " + result)
        })
        // 传入参数即表示元素存在，不传入的参数表示元素不存在，如果不传入buttonType，会默认添加ButtonType.Capsule配置，显示图标+背景。
        PasteButton({ icon: PasteIconStyle.LINES })
        // 只显示图标+背景，如果设置背景色高八位的α值低于0x1A，则会被系统强制调整为0xFF。
        PasteButton({ icon: PasteIconStyle.LINES, buttonType: ButtonType.Capsule })
          .backgroundColor(0x10007dff)
        // 图标、文字、背景都存在，如果设置背景色高八位的α值低于0x1A，则会被系统强制调整为0xFF。
        PasteButton({ icon: PasteIconStyle.LINES, text: PasteDescription.PASTE, buttonType: ButtonType.Capsule })
        // 图标、文字、背景都存在，如果设置宽度小于当前属性组合下允许的最小宽度时，宽度仍为设置值，此时按钮文本信息会自动换行，以保证安全控件显示的完整性。
        PasteButton({ icon: PasteIconStyle.LINES, text: PasteDescription.PASTE, buttonType: ButtonType.Capsule })
          .fontSize(16)
          .width(30)
        // 图标、文字、背景都存在，如果设置宽度小于当前属性组合下允许的最小宽度时，宽度仍为设置值，此时按钮文本信息会自动换行，以保证安全控件显示的完整性。
        PasteButton({ icon: PasteIconStyle.LINES, text: PasteDescription.PASTE, buttonType: ButtonType.Capsule })
          .fontSize(16)
          .size({ width: 30, height: 30 })
        // 图标、文字、背景都存在，如果设置宽度小于当前属性组合下允许的最小宽度时，宽度仍为设置值，此时按钮文本信息会自动换行，以保证安全控件显示的完整性。
        PasteButton({ icon: PasteIconStyle.LINES, text: PasteDescription.PASTE, buttonType: ButtonType.Capsule })
          .fontSize(16)
          .constraintSize({
            minWidth: 0,
            maxWidth: 30,
            minHeight: 0,
            maxHeight: 30
          })
      }.width('100%')
    }.height('100%')
  }
}
```

![zh-cn_image_0000001593677984](figures/zh-cn_image_0000001593677984.png)
