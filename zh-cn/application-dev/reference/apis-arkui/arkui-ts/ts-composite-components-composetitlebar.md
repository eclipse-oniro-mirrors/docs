# @ohos.arkui.advanced.ComposeTitleBar (头像和单双行文本标题栏)


一种普通标题栏，支持设置标题、头像（可选）和副标题（可选），可用于一级页面、二级及其以上界面配置返回键。


> **说明：**
>
> 该组件从API Version 10开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


## 导入模块

```
import { ComposeTitleBar } from "@ohos.arkui.advanced.ComposeTitleBar"
```


## 子组件

无

## 属性
不支持[通用属性](ts-universal-attributes-size.md)


## ComposeTitleBar

ComposeTitleBar({item?: ComposeTitleBarMenuItem, title: ResourceStr, subtitle?: ResourceStr, menuItems?: Array&lt;ComposeTitleBarMenuItem&gt;})

**装饰器类型：**\@Component

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 名称 | 参数类型 | 必填 | 说明 | 
| -------- | -------- | -------- | -------- |
| item | [ComposeTitleBarMenuItem](#composetitlebarmenuitem) | 否 | 用于左侧头像的单个菜单项目。 | 
| title | [ResourceStr](ts-types.md#resourcestr) | 是 | 标题。 | 
| subtitle | [ResourceStr](ts-types.md#resourcestr) | 否 | 副标题。 | 
| menuItems | Array&lt;[ComposeTitleBarMenuItem](#composetitlebarmenuitem)&gt; | 否 | 右侧菜单项目列表。 | 


## ComposeTitleBarMenuItem

| 名称 | 类型 | 必填 | 说明 | 
| -------- | -------- | -------- | -------- |
| value | [ResourceStr](ts-types.md#resourcestr) | 是 | 图标资源。 | 
| isEnabled | boolean | 否 | 是否启用，默认禁用。<br> isEnabled为true时，表示为启用。<br> isEnabled为false时，表示为禁用。 | 
| action | ()&nbsp;=&gt;&nbsp;void | 否 | 触发时的动作闭包，item属性不支持触发action事件。 | 

## 事件
不支持[通用事件](ts-universal-events-click.md)

## 示例

```ts
import { ComposeTitleBar } from "@ohos.arkui.advanced.ComposeTitleBar"
import promptAction from '@ohos.promptAction'

interface menuItem {
  value: Resource;
  isEnabled?: boolean;
  action?: () => void
}

@Entry
@Component
struct Index {
  private menuItems: Array<menuItem> = [
    {
      value: $r('app.media.ic_public_save'),
      isEnabled: true,
      action: () => promptAction.showToast({ message: "show toast index 1" })
    },
    {
      value: $r('app.media.ic_public_save'),
      isEnabled: true,
      action: () => promptAction.showToast({ message: "show toast index 1" })
    },
    {
      value: $r('app.media.ic_public_save'),
      isEnabled: true,
      action: () => promptAction.showToast({ message: "show toast index 1" })
    },
    {
      value: $r('app.media.ic_public_save'),
      isEnabled: true,
      action: () => promptAction.showToast({ message: "show toast index 1" })
    },
  ]

  build() {
    Row() {
      Column() {
        Divider().height(2).color(0xCCCCCC)
        ComposeTitleBar({
          title: "标题",
          subtitle: "副标题",
          menuItems: this.menuItems.slice(0, 1),
        })
        Divider().height(2).color(0xCCCCCC)
        ComposeTitleBar({
          title: "标题",
          subtitle: "副标题",
          menuItems: this.menuItems.slice(0, 2),
        })
        Divider().height(2).color(0xCCCCCC)
        ComposeTitleBar({
          title: "标题",
          subtitle: "副标题",
          menuItems: this.menuItems,
        })
        Divider().height(2).color(0xCCCCCC)
        ComposeTitleBar({
          menuItems: [{ isEnabled: true, value: $r('app.media.ic_public_save'),
            action: () => promptAction.showToast({ message: "show toast index 1" })
          }],
          title: "标题",
          subtitle: "副标题",
          item: { isEnabled: true, value: $r('app.media.app_icon') }
        })
        Divider().height(2).color(0xCCCCCC)
      }
    }.height('100%')
  }
}
```

![zh-cn_image_0000001616913438](figures/zh-cn_image_0000001616913438.jpg)
