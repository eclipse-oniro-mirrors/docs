# Menu Control

A context menu – a vertical list of items – can be bound to a component and displayed by long-pressing, clicking, or right-clicking the component.

>  **NOTE**
>
>  - The APIs of this module are supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.
>
>  - **CustomBuilder** does not support the use of **bindMenu** and **bindContextMenu** methods. To display a multi-level menu, use the [\<Menu>](ts-basic-components-menu.md) component instead.
>
>  - The text in the context menu cannot be selected by long-pressing.

## bindMenu

bindMenu(content: Array<MenuElement&gt; | CustomBuilder, options?: MenuOptions)

Menu bound to the component, which is displayed when the user clicks the component. A menu item can be a combination of text and icons or a custom component.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name | Type                                                        | Mandatory| Description                                        |
| ------- | ------------------------------------------------------------ | ---- | -------------------------------------------- |
| content | Array<[MenuElement](#menuelement)&gt; \| [CustomBuilder](ts-types.md#custombuilder8) | Yes  | Array of menu item icons and text, or custom component.|
| options | [MenuOptions](#menuoptions10)                                | No  | Parameters of the context menu.                        |

## bindMenu<sup>11+</sup>

bindMenu(isShow: boolean, content: Array<MenuElement&gt; | CustomBuilder, options?: MenuOptions)

Menu bound to the component, which is displayed when the user clicks the component. A menu item can be a combination of text and icons or a custom component.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name              | Type                                                        | Mandatory| Description                                                        |
| -------------------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| isShow<sup>11+</sup> | boolean                                                      | Yes  | Whether to show the menu. The default value is **false**. Menus can be displayed only after all pages are constructed. Therefore, this parameter cannot be set to **true** during page construction. Otherwise, display position and shape errors will occur. Two-way binding is not supported.|
| content              | Array<[MenuElement](#menuelement)&gt; \| [CustomBuilder](ts-types.md#custombuilder8) | Yes  | Array of menu item icons and text, or custom component.                |
| options              | [MenuOptions](#menuoptions10)                                | No  | Parameters of the context menu.                                        |

## bindContextMenu<sup>8+</sup>

bindContextMenu(content: CustomBuilder, responseType: ResponseType, options?: ContextMenuOptions)

Context menu bound to the component, which is displayed when the user long-presses or right-clicks the component. Only custom menu items are supported.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name      | Type                                              | Mandatory| Description                                        |
| ------------ | -------------------------------------------------- | ---- | -------------------------------------------- |
| content      | [CustomBuilder](ts-types.md#custombuilder8)        | Yes  | Array of menu item icons and text, or custom component.|
| responseType | [ResponseType](ts-appendix-enums.md#responsetype8) | Yes  | How the context menu is triggered, which can be long-press or right-click. Long pressing with a mouse device is not supported.           |
| options      | [ContextMenuOptions](#contextmenuoptions10)        | No   | Parameters of the context menu.                        |

## MenuElement

| Name                 | Type                                  | Mandatory| Description                                                        |
| --------------------- | -------------------------------------- | ---- | ------------------------------------------------------------ |
| value                 | [ResourceStr](ts-types.md#resourcestr) | Yes  | Menu item text.                                                |
| icon<sup>10+</sup>    | [ResourceStr](ts-types.md#resourcestr) | No  | Menu item icon.                                                |
| enabled<sup>11+</sup> | boolean                                | No  | Whether to enable interactions with the menu item.<br>Default value: **true**, indicating that interactions with the menu item are enabled.|
| action                | () =&gt; void                | Yes  | Action triggered when a menu item is clicked.                                      |

## MenuOptions<sup>10+</sup>

Inherited from [ContextMenuOptions](#contextmenuoptions10).

| Name                         | Type                                  | Mandatory| Description                                                        |
| ----------------------------- | -------------------------------------- | ---- | ------------------------------------------------------------ |
| title                         | [ResourceStr](ts-types.md#resourcestr) | No  | Menu title.<br>**NOTE**<br>This parameter is effective only when **content** is set to Array<[MenuElement](#menuelement)>.|
| showInSubWindow<sup>11+</sup> | boolean                                | No  | Whether to show the menu in a subwindow.<br>Default value: **true** for 2-in-1 devices and **false** for other devices                    |

## ContextMenuOptions<sup>10+</sup>

| Name                 | Type                                                        | Mandatory| Description                                                        |
| --------------------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| offset                | [Position](ts-types.md#position)                            | No  | Offset for showing the context menu, which should not cause the menu to extend beyond the screen.<br>**NOTE**<br>When the menu is displayed relative to the parent component area, the width or height of the area is automatically counted into the offset based on the **placement** attribute of the menu.<br>When the menu is displayed above the parent component (that is, **placement** is set to **Placement.TopLeft**, **Placement.Top**, or **Placement.TopRight**), a positive value of **x** indicates rightward movement relative to the parent component, and a positive value of **y** indicates upward movement.<br>When the menu is displayed below the parent component (that is, **placement** is set to **Placement.BottomLeft**, **Placement.Bottom**, or **Placement.BottomRight**), a positive value of **x** indicates rightward movement relative to the parent component, and a positive value of **y** indicates downward movement.<br>When the menu is displayed on the left of the parent component (that is, **placement** is set to **Placement.LeftTop**, **Placement.Left**, or **Placement.LeftBottom**), a positive value of **x** indicates leftward movement relative to the parent component, and a positive value of **y** indicates downward movement.<br>When the menu is displayed on the right of the parent component (that is, **placement** is set to **Placement.RightTop**, **Placement.RightTop**, or **Placement.RightBottom**), a positive value of **x** indicates rightward movement relative to the parent component, and a positive value of **y** indicates downward movement.<br>If the display position of the menu is adjusted (different from the main direction of the initial **placement** value), the offset value is invalid.|
| placement             | [Placement](ts-appendix-enums.md#placement8)                 | No  | Preferred position of the context menu. If the set position is insufficient for holding the component, it will be automatically adjusted.<br>**NOTE**<br>Setting **placement** to **undefined** or **null** is equivalent to not setting it at all. In this case, if [bindContextMenu<sup>8+</sup>](#bindcontextmenu8) is used, the menu is displayed at the clicked position.|
| enableArrow           | boolean                                                      | No  | Whether to display an arrow. If the size and position of the context menu are insufficient for holding an arrow, no arrow is displayed.<br>Default value: **false**, indicating that no arrow is displayed<br>**NOTE**<br>When **enableArrow** is **true**, an arrow is displayed in the position specified by **placement**. If **placement** is not set or its value is invalid, the arrow is displayed above the target. If the position is insufficient for holding the arrow, it is automatically adjusted. When **enableArrow** is **undefined**, no arrow is displayed.|
| arrowOffset           | [Length](ts-types.md#length)                                 | No  | Offset of the arrow relative to the context menu. When the arrow is placed in a horizontal position with the context menu: The value indicates the distance from the arrow to the leftmost; the arrow is centered by default. When the arrow is placed in a vertical position with the context menu: The value indicates the distance from the arrow to the top; the arrow is centered by default. The offset settings take effect only when the value is valid, can be converted to a number greater than 0, and does not cause the arrow to extend beyond the safe area of the context menu. The value of **placement** determines whether the offset is horizontal or vertical.|
| preview<sup>11+</sup> | [MenuPreviewMode](ts-appendix-enums.md#menupreviewmode11)\| [CustomBuilder](ts-types.md#custombuilder8) | No  | Preview displayed when the context menu is triggered by a long-press. It can be a screenshot of the target component or custom content.<br>Default value: **MenuPreviewMode.NONE**, indicating no preview.<br>**NOTE**<br>- This parameter has no effect when **responseType** is set to **ResponseType.RightClick**.<br>- If **preview** is set to **MenuPreviewMode.NONE** or is not set, the **enableArrow** parameter is effective.<br>- If **preview** is set to **MenuPreviewMode.IMAGE** or **CustomBuilder**, no arrow will be displayed even when **enableArrow** is **true**.|
| previewAnimationOptions<sup>11+</sup> | [ContextMenuAnimationOptions](#contextmenuanimationoptions11) | No   | Start scale ratio and end scale ratio (relative to the original preview image) of the preview animation displayed when the component is long pressed<br>Default value: **{scale: [0.95, 1.1]}**<br>**NOTE**<br>- If the value of this parameter is less than or equal to 0, this parameter does not take effect.<br>- This parameter takes effect only when **preview** is set to **MenuPreviewMode.IMAGE.**|
| onAppear              | () =&gt; void                                      | No  | Callback triggered when the menu is displayed.                                      |
| onDisappear           | () =&gt; void                                      | No  | Callback triggered when the menu is hidden.                                      |
| aboutToAppear              | () =&gt; void                                      | No  | Callback triggered when the menu is about to appear.                                      |
| aboutToDisappear           | () =&gt; void                                      | No  | Callback triggered when the menu is about to disappear.                                      |
| backgroundColor<sup>11+</sup> | [ResourceColor](ts-types.md#resourcecolor)  | No| Backplane color of the dialog box.<br>Default value: **Color.Transparent**|
| backgroundBlurStyle<sup>11+</sup> | [BlurStyle](ts-appendix-enums.md#blurstyle9) | No| Background blur style of the dialog box.<br>Default value: **BlurStyle.COMPONENT_ULTRA_THICK**|

## ContextMenuAnimationOptions<sup>11+</sup>

| Name | Type                                      | Mandatory| Description                                |
| ----- | ------------------------------------------ | ---- | ------------------------------------ |
| scale | [AnimationRange](#animationrange11)\<number> | No  | Scale ratio of the preview image when the animation starts and scale ratio when the animation ends.|

## AnimationRange<sup>11+</sup>

Describes the scale ratio of the preview image when the animation starts and scale ratio when the animation ends.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Value Range        | Description                                                                          |
| ---------------- | ------------------------------------------------------------------------------ |
| [from: T, to: T] | **from** indicates the scale ratio of the preview image when the animation starts, and **to** indicates the scale ratio when the animation ends.|

## Example

### Example 1

Menu with textual menu items:

```ts
// xxx.ets
@Entry
@Component
struct MenuExample {
  build() {
    Column() {
      Text('click for Menu')
    }
    .width('100%')
    .margin({ top: 5 })
    .bindMenu([
      {
        value: 'Menu1',
        action: () => {
          console.info('handle Menu1 select')
        }
      },
      {
        value: 'Menu2',
        action: () => {
          console.info('handle Menu2 select')
        }
      },
    ])
  }
}
```

![en-us_image_0000001174582862](figures/en-us_image_0000001174582862.gif)

### Example 2

Menu with custom menu items:

```ts
@Entry
@Component
struct MenuExample {
  @State listData: number[] = [0, 0, 0]

  @Builder MenuBuilder() {
    Flex({ direction: FlexDirection.Column, justifyContent: FlexAlign.Center, alignItems: ItemAlign.Center }) {
      ForEach(this.listData, (item:number, index) => {
        Column() {
          Row() {
            Image($r("app.media.icon")).width(20).height(20).margin({ right: 5 })
            Text(`Menu${index as number + 1}`).fontSize(20)
          }
          .width('100%')
          .height(30)
          .justifyContent(FlexAlign.Center)
          .align(Alignment.Center)
          .onClick(() => {
            console.info(`Menu${index as number + 1} Clicked!`)
          })

          if (index != this.listData.length - 1) {
            Divider().height(10).width('80%').color('#ccc')
          }
        }.padding(5).height(40)
      })
    }.width(100)
  }

  build() {
    Column() {
      Text('click for menu')
        .fontSize(20)
        .margin({ top: 20 })
        .bindMenu(this.MenuBuilder)
    }
    .height('100%')
    .width('100%')
    .backgroundColor('#f0f0f0')
  }
}
```

![en-us_image_0000001186807708](figures/en-us_image_0000001186807708.gif)

### Example 3

Context menu displayed upon long-press:

```ts
// xxx.ets
@Entry
@Component
struct ContextMenuExample {
  @Builder MenuBuilder() {
    Flex({ direction: FlexDirection.Column, justifyContent: FlexAlign.Center, alignItems: ItemAlign.Center }) {
      Text('Test menu item 1')
        .fontSize(20)
        .width(100)
        .height(50)
        .textAlign(TextAlign.Center)
      Divider().height(10)
      Text('Test menu item 2')
        .fontSize(20)
        .width(100)
        .height(50)
        .textAlign(TextAlign.Center)
    }.width(100)
  }

  build() {
    Column() {
      Text('LongPress for menu')
    }
    .width('100%')
    .margin({ top: 5 })
    .bindContextMenu(this.MenuBuilder, ResponseType.LongPress)
  }
}
```

![longMenu](figures/longMenu.gif)

### Example 4

Directive menu displayed upon right-click:

```ts
// xxx.ets
@Entry
@Component
struct DirectiveMenuExample {
  @Builder MenuBuilder() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Text('Options')
      Divider().strokeWidth(2).margin(5).color('#F0F0F0')
      Text('Hide')
      Divider().strokeWidth(2).margin(5).color('#F0F0F0')
      Text('Exit')
    }
    .width(200)
  }

  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Column() {
        Text("DirectiveMenuExample")
          .fontSize(20)
          .width('100%')
          .height("25%")
          .backgroundColor('#F0F0F0')
          .textAlign(TextAlign.Center)
          .bindContextMenu(this.MenuBuilder, ResponseType.RightClick, {
            enableArrow: true,
            placement: Placement.Bottom
          })
      }
    }
    .width('100%')
    .height('100%')
  }
}
```

![en-us_image_0000001689126950](figures/en-us_image_0000001689126950.png)

### Example 5

Context menu displayed upon long-pressing (with preview of component screenshot):

```ts
// xxx.ets
@Entry
@Component
struct Index {
  private iconStr: ResourceStr = $r("app.media.icon")

  @Builder
  MyMenu() {
    Menu() {
      MenuItem({ startIcon: this.iconStr, content: "Menu option" })
      MenuItem({ startIcon: this.iconStr, content: "Menu option" })
      MenuItem({ startIcon: this.iconStr, content: "Menu option" })
    }
  }

  build() {
    Column({ space: 50 }) {
      Column() {
        Column() {
          Text('preview-image')
            .width(200)
            .height(100)
            .textAlign(TextAlign.Center)
            .margin(100)
            .fontSize(30)
            .bindContextMenu(this.MyMenu, ResponseType.LongPress,
              { preview: MenuPreviewMode.IMAGE,
                previewAnimationOptions: {scale: [0.8, 1.0]},
              })
            .backgroundColor("#ff3df2f5")
        }
      }.width('100%')
    }
  }
}
```

![preview-image](figures/preview-image.png)

### Example 6

Context menu displayed upon long-pressing (with preview of custom content):

```ts
// xxx.ets
@Entry
@Component
struct Index {
  private iconStr: ResourceStr = $r("app.media.icon")

  @Builder
  MyMenu() {
    Menu() {
      MenuItem({ startIcon: this.iconStr, content: "Menu option" })
      MenuItem({ startIcon: this.iconStr, content: "Menu option" })
      MenuItem({ startIcon: this.iconStr, content: "Menu option" })
    }
  }

  @Builder
  MyPreview() {
    Column() {
      Image($r('app.media.icon'))
        .width(200)
        .height(200)
    }
  }

  build() {
    Column({ space: 50 }) {
      Column() {
        Column() {
          Text('preview-builder')
            .width(200)
            .height(100)
            .textAlign(TextAlign.Center)
            .margin(100)
            .fontSize(30)
            .bindContextMenu(this.MyMenu, ResponseType.LongPress,
              {
                preview: this.MyPreview
              })
        }
      }.width('100%')
    }
  }
}
```

![preview-builder](figures/preview-builder.png)

### Example 7

Context menu displayed upon setting isShown (with preview of custom content):

```ts
// xxx.ets
@Entry
@Component
struct Index {
  private iconStr: ResourceStr = $r("app.media.icon")
  @State isShown: boolean = false

  @Builder
  MyMenu() {
    Menu() {
      MenuItem({ startIcon: this.iconStr, content: "Menu option" })
      MenuItem({ startIcon: this.iconStr, content: "Menu option" })
      MenuItem({ startIcon: this.iconStr, content: "Menu option" })
    }
  }

  @Builder
  MyPreview() {
    Column() {
      Image($r('app.media.icon'))
        .width(200)
        .height(200)
    }
  }

  build() {
    Column({ space: 50 }) {
      Column() {
        Column() {
          Text('preview-builder')
            .width(200)
            .height(100)
            .textAlign(TextAlign.Center)
            .margin(100)
            .fontSize(30)
            .bindContextMenu(this.isShown, this.MyMenu,
              {
                preview: this.MyPreview,
                onDisappear: ()=>{
                    this.isShown = false;
                }
              })
          Button('click')
            .onClick(()=>{
                this.isShown = true;
             })
        }
      }.width('100%')
    }
  }
}
```
