# Tabs

The **\<Tabs>** component is a container component that allows users to switch between content views through tabs. Each tab page corresponds to a content view.

>  **NOTE**
>
>  This component is supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.
>
>  Since API version 11, this component supports the safe area attribute by default, with the default attribute value being **expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.BOTTOM]))**. You can override this attribute to change the default behavior. In earlier versions, you need to use the [expandSafeArea](ts-universal-attributes-expand-safe-area.md) attribute to implement the safe area feature.


## Child Components

Custom components cannot be used as child components. Only the [\<TabContent>](ts-container-tabcontent.md) child component is allowed, with support for [if/else](../../../quick-start/arkts-rendering-control-ifelse.md) and [ForEach](../../../quick-start/arkts-rendering-control-foreach.md) rendering control. In addition, the **if/else** and **ForEach** statements support **\<TabContent>** components only, but not custom components.

>  **NOTE**
>
>  If the child component has the **visibility** attribute set to **None** or **Hidden**, it is hidden but takes up space in the layout.


## APIs

Tabs(value?: {barPosition?: BarPosition, index?: number, controller?: TabsController})

**Parameters**

| Name        | Type                             | Mandatory  | Description                                    |
| ----------- | --------------------------------- | ---- | ---------------------------------------- |
| barPosition | [BarPosition](#barposition)| No   | Position of the **\<Tabs>** component.<br>Default value: **BarPosition.Start**  |
| index       | number                            | No   | Index of the currently displayed tab.<br>Default value: **0**<br>**NOTE**<br>A value less than 0 evaluates to the default value.<br>The value ranges from 0 to the number of **\<TabContent>** subnodes minus 1.<br>When the tab is switched by changing the index, the tab switching animation does not take effect. When **changeIndex** of **TabController** is used for tab switching, the tab switching animation is enabled by default. You can disable the animation by setting **animationDuration** to **0**.<br>Since API version 10, this parameter supports two-way binding through [$$](../../../quick-start/arkts-two-way-sync.md).|
| controller  | [TabsController](#tabscontroller) | No   | Tab controller.                              |

## BarPosition

| Name   | Description                                      |
| ----- | ---------------------------------------- |
| Start | If the **vertical** attribute is set to **true**, the tab is on the left of the container. If the **vertical** attribute is set to **false**, the tab is on the top of the container.|
| End   | If the **vertical** attribute is set to **true**, the tab is on the right of the container. If the **vertical** attribute is set to **false**, the tab is at the bottom of the container.|


## Attributes

In addition to the [universal attributes](ts-universal-attributes-size.md), the following attributes are supported.

| Name                              | Type                                    | Description                                      |
| -------------------------------- | ---------------------------------------- | ---------------------------------------- |
| vertical                         | boolean                                  | Whether to use vertical tabs. The value **true** means to use vertical tabs, and **false** means to use horizontal tabs.<br>Default value: **false**|
| scrollable                       | boolean                                  | Whether the tabs are scrollable. The value **true** means that the tabs are scrollable, and **false** means the opposite.<br>Default value: **true**|
| barMode                          | [BarMode](#barmode),[ScrollableBarModeOptions](#scrollablebarmodeoptions10) | Tab bar layout mode. **BarMode** is mandatory, and **ScrollableBarModeOptions** is optional. For details, see **BarMode** and **ScrollableBarModeOptions**. Since API version 10, the optional **ScrollableBarModeOptions** parameter is supported. It is effective only when the tab bar is in scrollable mode.<br>Default value: **BarMode.Fixed**|
| barWidth                         | number \| Length<sup>8+</sup>  | Width of the tab bar.<br>The default value varies.<br>If the tab bar has the **vertical** attribute set to **false** and does not have [SubTabBarStyle](ts-container-tabcontent.md#subtabbarstyle9) or [BottomTabBarStyle](ts-container-tabcontent.md#bottomtabbarstyle9) specified, the default value is the width of the **\<Tabs>** component.<br>If the tab bar has the **vertical** attribute set to **true** and does not have [SubTabBarStyle](ts-container-tabcontent.md#subtabbarstyle9) or [BottomTabBarStyle](ts-container-tabcontent.md#bottomtabbarstyle9) specified, the default value is **56vp**.<br>If the tab bar has the **vertical** attribute set to **false** and **SubTabbarStyle** specified, the default value is the width of the **\<Tabs>** component.<br>If the tab bar has the **vertical** attribute set to **true** and **SubTabbarStyle** specified, the default value is **56vp**.<br>If the tab bar has the **vertical** attribute set to **true** and **BottomTabbarStyle** specified, the default value is **96vp**.<br>If the tab bar has the **vertical** attribute set to **false** and **BottomTabbarStyle** specified, the default value is the width of the **\<Tabs>** component.<br>**NOTE**<br><br>A value less than 0 or greater than the width of the **\<Tabs>** component evaluates to the default value.|
| barHeight                        | number \| Length<sup>8+</sup>  | Height of the tab bar.<br>The default value varies.<br>If the tab bar has the **vertical** attribute set to **false** and does not have a style specified, the default value is **56vp**.<br>If the tab bar has the **vertical** attribute set to **true** and does not have a style specified, the default value is the height of the **\<Tabs>** component.<br>If the tab bar has the **vertical** attribute set to **false** and **SubTabbarStyle** specified, the default value is **56vp**.<br>If the tab bar has the **vertical** attribute set to **true** and **SubTabbarStyle** specified, the default value is the height of the **\<Tabs>** component.<br>If the tab bar has the **vertical** attribute set to **true** and **BottomTabbarStyle** specified, the default value is the height of the **\<Tabs>** component.<br>If the tab bar has the **vertical** attribute set to **false** and **BottomTabbarStyle** specified, the default value is **56vp**.<br>**NOTE**<br><br>A value less than 0 or greater than the height of the **\<Tabs>** component evaluates to the default value.|
| animationDuration                | number                                   | Length of time required to complete the tab switching animation, which is initiated by clicking a specific tab or by calling the **changeIndex** API of **TabsController**.<br>The default value varies.<br>API version 10 and earlier versions: If this parameter is set to **null** or is not set, the default value 0 ms is used, which means that no tab switching animation is displayed when a specific tab is clicked or the **changeIndex** API of **TabsController** is called. If this parameter is set to **undefined** or a value less than 0, the default value 300 ms is used.<br>API version 11 and later versions: If this parameter is set to an invalid value or is not set, the default value 0 ms is used when the tab bar is set to **BottomTabBarStyle**; and 300 ms is used when the tab bar is set to other styles.<br>**NOTE**<br>This parameter cannot be set in percentage.|
| divider<sup>10+</sup>            | [DividerStyle](#dividerstyle10) \| null | Whether the divider is displayed for the **\<TabBar>** and **\<TabContent>** components and the divider style. By default, the divider is not displayed.<br> **DividerStyle**: divider style.<br> **null**: The divider is not displayed.|
| fadingEdge<sup>10+</sup>         | boolean                                  | Whether the tab fades out when it exceeds the container width.<br>Default value: **true**<br>**NOTE**<br>It is recommended that this attribute be used together with the **barBackgroundColor** attribute. If the **barBackgroundColor** attribute is not defined, the tab fades out in white when it exceeds the container width by default.|
| barOverlap<sup>10+</sup>         | boolean                                  | Whether the tab bar is superimposed on the **\<TabContent>** component after having its background blurred.<br>Default value: **false**|
| barBackgroundColor<sup>10+</sup> | [ResourceColor](ts-types.md#resourcecolor) | Background color of the tab bar.<br>Default value: transparent              |
| barBackgroundBlurStyle<sup>11+</sup> | [BlurStyle](ts-appendix-enums.md#blurstyle9) | Background blur style of the tab bar.<br>Default value: **BlurStyle.NONE**             |
| barGridAlign<sup>10+</sup> | [BarGridColumnOptions](#bargridcolumnoptions10) | Visible area of the tab bar in grid mode. For details, see **BarGridColumnOptions**. This attribute is effective only in horizontal mode. It is not applicable to [XS, XL, and XXL devices](../../../ui/arkts-layout-development-grid-layout.md#grid-breakpoints).             |

## DividerStyle<sup>10+</sup>

| Name         | Type                                    | Mandatory  | Description                                      |
| ----------- | ---------------------------------------- | ---- | ---------------------------------------- |
| strokeWidth | [Length](ts-types.md#length)             | Yes   | Width of the divider. It cannot be set in percentage.<br>Default value: **0.0**<br>Unit: vp                      |
| color       | [ResourceColor](ts-types.md#resourcecolor) | No   | Color of the divider.<br>Default value: **#33182431**               |
| startMargin | [Length](ts-types.md#length)             | No   | Distance between the divider and the top of the sidebar. It cannot be set in percentage.<br>Default value: **0.0**<br>Unit: vp|
| endMargin   | [Length](ts-types.md#length)             | No   | Distance between the divider and the bottom of the sidebar. It cannot be set in percentage.<br>Default value: **0.0**<br>Unit: vp|

## BarGridColumnOptions<sup>10+</sup>

| Name         | Type                                    | Mandatory  | Description                                      |
| ----------- | ---------------------------------------- | ---- | ---------------------------------------- |
| margin | [Dimension](ts-types.md#dimension10)             | No   | Column margin in grid mode. It cannot be set in percentage.<br>Default value: **24.0**<br>Unit: vp                       |
| gutter      | [Dimension](ts-types.md#dimension10) | No   | Column gutter (that is, gap between columns) in grid mode. It cannot be set in percentage.<br>Default value: **24.0**<br>Unit: vp                    |
| sm | number            | No   | Number of columns occupied by a tab on a screen whose width is greater than or equal to 320 vp but less than 600 vp.<br>The value must be a non-negative even number. The default value is **-1**, indicating that the tab takes up the entire width of the tab bar.|
| md   | number          | No   | Number of columns occupied by a tab on a screen whose width is greater than or equal to 600 vp but less than 800 vp.<br>The value must be a non-negative even number. The default value is **-1**, indicating that the tab takes up the entire width of the tab bar.|
| lg   | number           | No   | Number of columns occupied by a tab on a screen whose width is greater than or equal to 840 vp but less than 1024 vp.<br>The value must be a non-negative even number. The default value is **-1**, indicating that the tab takes up the entire width of the tab bar.|

## ScrollableBarModeOptions<sup>10+</sup>

| Name         | Type                                    | Mandatory  | Description                                      |
| ----------- | ---------------------------------------- | ---- | ---------------------------------------- |
| margin | [Dimension](ts-types.md#dimension10)          | No   | Left and right margin of the tab bar in scrollable mode. It cannot be set in percentage.<br>Default value: **0.0**<br>Unit: vp                   |
| nonScrollableLayoutStyle      | [LayoutStyle](#layoutstyle10) | No   | Tab layout mode of the tab bar when not scrolling in scrollable mode.<br>Default value: **LayoutStyle.ALWAYS_CENTER**          |

## BarMode

| Name        | Description                                      |
| ---------- | ---------------------------------------- |
| Scrollable | The width of each tab is determined by the actual layout. The tabs are scrollable in the following case: In horizontal layout, the total width exceeds the tab bar width; in horizontal layout, the total height exceeds the tab bar height.|
| Fixed      | The width of each tab is determined by equally dividing the number of tabs by the bar width (or bar height in the vertical layout).|

## LayoutStyle<sup>10+</sup>

| Name        | Description                                      |
| ---------- | ---------------------------------------- |
| ALWAYS_CENTER | When the tab content exceeds the tab bar width, the tabs are scrollable.<br>Otherwise, the tabs are compactly centered and not scrollable.|
| ALWAYS_AVERAGE_SPLITE      | When the tab content exceeds the tab bar width, the tabs are scrollable.<br>Otherwise, the tabs are not scrollable, and the tab bar width is distributed evenly between all tabs.<br>This option is valid only in horizontal mode, and is equivalent to **LayoutStyle.ALWAYS_CENTER** otherwise.|
| SPACE_BETWEEN_OR_CENTER      | When the tab content exceeds the tab bar width, the tabs are scrollable.<br>When the tab content exceeds half of the tab bar width but still within the tab bar width, the tabs are compactly centered and not scrollable.<br>When the tab content does not exceed half of the tab bar width, the tabs are centered within half of the tab bar width, with even spacing between, and not scrollable.|

## Events

In addition to the [universal events](ts-universal-events-click.md), the following events are supported.

| Name                                      | Description                                    |
| ---------------------------------------- | ---------------------------------------- |
| onChange(event: (index: number) =&gt; void) | Triggered when a tab is switched.<br>- **index**: index of the active tab. The index starts from 0.<br>This event is triggered when any of the following conditions is met:<br>1. The **\<TabContent>** component supports sliding, and the user slides on the tab bar.<br>2. The [Controller](#tabscontroller) API is called.<br>3. The attribute value is updated using a [state variable](../../../quick-start/arkts-state.md).<br>4. A tab is clicked.<br/>**NOTE**<br/>Since this API is also called when the layout changes, do not update state variables in this callback, so as to avoid cyclic updates of the layout, which may result in performance issues or other unexpected behaviors. To update state variables, you can use asynchronous tasks instead, for example, [setTimeout](../../common/js-apis-timer.md#settimeout).|
| onTabBarClick(event: (index: number) =&gt; void)<sup>10+</sup> | Triggered when a tab is clicked.<br>- **index**: index of the clicked tab. The index starts from 0.|
| onAnimationStart<sup>11+</sup>(handler: (index: number, targetIndex: number, event: [TabsAnimationEvent](ts-types.md#tabsanimationevent11)) => void) | Triggered when the tab switching animation starts.<br>- **index**: index of the currently displayed element.<br>- **targetIndex**: index of the target element to switch to.<br>- **event**: animation-related information, including the offset of the currently displayed element and target element relative to the start position of the **\<Tabs>** along the main axis, and the hands-off velocity.<br>**NOTE**<br>The **index** parameter indicates the index before the animation starts (not the one after).|
| onAnimationEnd<sup>11+</sup>(handler: (index: number, event: [TabsAnimationEvent](ts-types.md#tabsanimationevent11)) => void) | Triggered when the tab switching animation ends.<br>- **index**: index of the currently displayed element.<br>- **event**: animation-related information, including the offset of the currently displayed element relative to the start position of the **\<Tabs>** along the main axis.<br>**NOTE**<br>This event is triggered when the tab switching animation ends, whether it is caused by gesture interruption or not. The **index** parameter indicates the index after the animation ends.|
| onGestureSwipe<sup>11+</sup>(handler: (index: number, event: [TabsAnimationEvent](ts-types.md#tabsanimationevent11)) => void) | Triggered on a frame-by-frame basis when the tab is switched by a swipe.<br>- **index**: index of the currently displayed element.<br>- **event**: animation-related information, including the offset of the currently displayed element relative to the start position of the **\<Tabs>** along the main axis.|
| customContentTransition<sup>11+</sup>(delegate: (from: number, to: number) => [TabContentAnimatedTransition](ts-types.md#tabcontentanimatedtransition11) \| undefined) | Custom tab switching animation. **from** and **to** indicate the return values.<br> - **from**: index of the currently displayed tab before the animation starts.<br>- **to**: index of the target tab before the animation starts.<br> Instructions:<br>  1. When the custom tab switching animation is used, the default switching animation of the **\<Tabs>** component is disabled, and tabs cannot be switched through swiping.<br> 2. The value **undefined** means not to use the custom tab switching animation, in which case the default switching animation is used.<br> 3. The custom tab switching animation cannot be interrupted.<br> 4. Currently, the custom tab switching animation can be triggered only by clicking a tab or by calling the **TabsController.changeIndex()** API.<br> 5. When the custom tab switching animation is used, the **\<Tabs>** component supports all events except **onGestureSwipe**.<br> 6. Notes about the **onChange** and **onAnimationEnd** events: If the second custom animation is triggered during the execution of the first custom animation, the **onChange** and **onAnimationEnd** events of the first custom animation will be triggered when the second custom animation starts.<br> 7. When the custom animation is used, the stack layout is used for pages involved in the animation. If the **zIndex** attribute is not set for related pages, the **zIndex** values of all pages are the same. In this case, the pages are rendered in the order in which they are added to the component tree (that is, the sequence of page indexes). In light of this, to control the rendering levels of pages, set the **zIndex** attribute of the pages.<br>|


## TabsController

Defines a tab controller, which is used to control switching of tabs. One **TabsController** cannot control multiple **\<Tabs>** components.

### Objects to Import

```ts
let controller: TabsController = new TabsController()
```

### changeIndex

changeIndex(value: number): void

Switches to the specified tab.

**Parameters**

| Name  | Type  | Mandatory  | Description                                    |
| ----- | ------ | ---- | ---------------------------------------- |
| value | number | Yes   | Index of the tab. The value starts from 0.<br>**NOTE**<br>If this parameter is set to a value less than 0 or greater than the maximum number, the default value **0** is used.|


## Example

### Example 1

This example uses **onChange** to implement the linkage between **tabBar** and **\<TabContent>**.

```ts
// xxx.ets
@Entry
@Component
struct TabsExample {
  @State fontColor: string = '#182431'
  @State selectedFontColor: string = '#007DFF'
  @State currentIndex: number = 0
  private controller: TabsController = new TabsController()

  @Builder tabBuilder(index: number, name: string) {
    Column() {
      Text(name)
        .fontColor(this.currentIndex === index ? this.selectedFontColor : this.fontColor)
        .fontSize(16)
        .fontWeight(this.currentIndex === index ? 500 : 400)
        .lineHeight(22)
        .margin({ top: 17, bottom: 7 })
      Divider()
        .strokeWidth(2)
        .color('#007DFF')
        .opacity(this.currentIndex === index ? 1 : 0)
    }.width('100%')
  }

  build() {
    Column() {
      Tabs({ barPosition: BarPosition.Start, index: this.currentIndex, controller: this.controller }) {
        TabContent() {
          Column().width('100%').height('100%').backgroundColor('#00CB87')
        }.tabBar(this.tabBuilder(0, 'green'))

        TabContent() {
          Column().width('100%').height('100%').backgroundColor('#007DFF')
        }.tabBar(this.tabBuilder(1, 'blue'))

        TabContent() {
          Column().width('100%').height('100%').backgroundColor('#FFBF00')
        }.tabBar(this.tabBuilder(2, 'yellow'))

        TabContent() {
          Column().width('100%').height('100%').backgroundColor('#E67C92')
        }.tabBar(this.tabBuilder(3, 'pink'))
      }
      .vertical(false)
      .barMode(BarMode.Fixed)
      .barWidth(360)
      .barHeight(56)
      .animationDuration(400)
      .onChange((index: number) => {
        this.currentIndex = index
      })
      .width(360)
      .height(296)
      .margin({ top: 52 })
      .backgroundColor('#F1F3F5')
    }.width('100%')
  }
}
```

![tabs2](figures/tabs2.gif)

### Example 2

This example uses **divider** to present dividers in different styles.

```ts
// xxx.ets
@Entry
@Component
struct TabsDivider1 {
  private controller1: TabsController = new TabsController()
  @State dividerColor: string = 'red'
  @State strokeWidth: number = 2
  @State startMargin: number = 0
  @State endMargin: number = 0
  @State nullFlag: boolean = false

  build() {
    Column() {
      Tabs({ controller: this.controller1 }) {
        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Pink)
        }.tabBar('pink')

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Yellow)
        }.tabBar('yellow')

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Blue)
        }.tabBar('blue')

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Green)
        }.tabBar('green')

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Red)
        }.tabBar('red')
      }
      .vertical(true)
      .scrollable(true)
      .barMode(BarMode.Fixed)
      .barWidth(70)
      .barHeight(200)
      .animationDuration(400)
      .onChange((index: number) => {
        console.info(index.toString())
      })
      .height('200vp')
      .margin({ bottom: '12vp' })
      .divider(this.nullFlag ? null : {
        strokeWidth: this.strokeWidth,
        color: this.dividerColor,
        startMargin: this.startMargin,
        endMargin: this.endMargin
      })

      Button('Regular Divider').width('100%').margin({ bottom: '12vp' })
        .onClick(() => {
          this.nullFlag = false;
          this.strokeWidth = 2;
          this.dividerColor = 'red';
          this.startMargin = 0;
          this.endMargin = 0;
        })
      Button('Empty Divider').width('100%').margin({ bottom: '12vp' })
        .onClick(() => {
          this.nullFlag = true
        })
      Button('Change to Blue').width('100%').margin({ bottom: '12vp'})
        .onClick(() => {
          this.dividerColor = 'blue'
        })
      Button('Increase Width').width('100%').margin({ bottom: '12vp' })
        .onClick(() => {
          this.strokeWidth += 2
        })
      Button('Decrease Width').width('100%').margin({ bottom: '12vp'})
        .onClick(() => {
          if (this.strokeWidth > 2) {
            this.strokeWidth -= 2
          }
        })
      Button('Increase Top Margin').width ('100%').margin ({ bottom:'12vp'})
        .onClick(() => {
          this.startMargin += 2
        })
      Button('Decrease Top Margin').width ('100%').margin ({ bottom:'12vp' })
        .onClick(() => {
          if (this.startMargin > 2) {
            this.startMargin -= 2
          }
        })
      Button('Increase Bottom Margin').width ('100%').margin ({ bottom:'12vp'})
        .onClick(() => {
          this.endMargin += 2
        })
      Button('Decrease Bottom Margin').width ('100%').margin ({ bottom:'12vp' })
        .onClick(() => {
          if (this.endMargin > 2) {
            this.endMargin -= 2
          }
        })
    }.padding({ top: '24vp', left: '24vp', right: '24vp' })
  }
}
```

![tabs3](figures/tabs3.gif)

### Example 3

This example uses **fadingEdge** to specify whether to fade out tabs.

```ts
// xxx.ets
@Entry
@Component
struct TabsOpaque {
  @State message: string = 'Hello World'
  private controller: TabsController = new TabsController()
  private controller1: TabsController = new TabsController()
  @State selfFadingFade: boolean = true;

  build() {
    Column() {
      Button('Set Tab to Fade').width('100%').margin({ bottom: '12vp' })
        .onClick((event?: ClickEvent) => {
          this.selfFadingFade = true;
        })
      Button('Set Tab Not to Fade').width('100%').margin({ bottom: '12vp' })
        .onClick((event?: ClickEvent) => {
          this.selfFadingFade = false;
        })
      Tabs({ barPosition: BarPosition.End, controller: this.controller }) {
        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Pink)
        }.tabBar('pink')

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Yellow)
        }.tabBar('yellow')

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Blue)
        }.tabBar('blue')

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Green)
        }.tabBar('green')

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Green)
        }.tabBar('green')

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Green)
        }.tabBar('green')

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Green)
        }.tabBar('green')

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Green)
        }.tabBar('green')
      }
      .vertical(false)
      .scrollable(true)
      .barMode(BarMode.Scrollable)
      .barHeight(80)
      .animationDuration(400)
      .onChange((index: number) => {
        console.info(index.toString())
      })
      .fadingEdge(this.selfFadingFade)
      .height('30%')
      .width('100%')

      Tabs({ barPosition: BarPosition.Start, controller: this.controller1 }) {
        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Pink)
        }.tabBar('pink')

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Yellow)
        }.tabBar('yellow')

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Blue)
        }.tabBar('blue')

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Green)
        }.tabBar('green')

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Green)
        }.tabBar('green')

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Green)
        }.tabBar('green')
      }
      .vertical(true)
      .scrollable(true)
      .barMode(BarMode.Scrollable)
      .barHeight(200)
      .barWidth(80)
      .animationDuration(400)
      .onChange((index: number) => {
        console.info(index.toString())
      })
      .fadingEdge(this.selfFadingFade)
      .height('30%')
      .width('100%')
    }
    .padding({ top: '24vp', left: '24vp', right: '24vp' })
  }
}
```

![tabs4](figures/tabs4.gif)

### Example 4

This example uses **barOverlap** to specify whether the tab bar is superimposed on the **\<TabContent>** component after having its background blurred.

```ts
// xxx.ets
@Entry
@Component
struct barBackgroundColorTest {
  private controller: TabsController = new TabsController()
  @State barOverlap: boolean = true;
  @State barBackgroundColor: string = '#88888888';

  build() {
    Column() {
      Button("Change barOverlap").width('100%').margin({ bottom: '12vp' })
        .onClick((event?: ClickEvent) => {
          if (this.barOverlap) {
            this.barOverlap = false;
          } else {
            this.barOverlap = true;
          }
        })

      Tabs({ barPosition: BarPosition.Start, index: 0, controller: this.controller }) {
        TabContent() {
          Column() {
            Text(`barOverlap ${this.barOverlap}`).fontSize(16).margin({ top: this.barOverlap ? '56vp' : 0 })
            Text(`barBackgroundColor ${this.barBackgroundColor}`).fontSize(16)
          }.width('100%').width('100%').height('100%')
          .backgroundColor(Color.Pink)
        }
        .tabBar(new BottomTabBarStyle($r('sys.media.ohos_app_icon'), "1"))

        TabContent() {
          Column() {
            Text(`barOverlap ${this.barOverlap}`).fontSize(16).margin({ top: this.barOverlap ? '56vp' : 0 })
            Text(`barBackgroundColor ${this.barBackgroundColor}`).fontSize(16)
          }.width('100%').width('100%').height('100%')
          .backgroundColor(Color.Yellow)
        }
        .tabBar(new BottomTabBarStyle($r('sys.media.ohos_app_icon'), "2"))

        TabContent() {
          Column() {
            Text(`barOverlap ${this.barOverlap}`).fontSize(16).margin({ top: this.barOverlap ? '56vp' : 0 })
            Text(`barBackgroundColor ${this.barBackgroundColor}`).fontSize(16)
          }.width('100%').width('100%').height('100%')
          .backgroundColor(Color.Green)
        }
        .tabBar(new BottomTabBarStyle($r('sys.media.ohos_app_icon'), "3"))
      }
      .vertical(false)
      .barMode(BarMode.Fixed)
      .height('60%')
      .barOverlap(this.barOverlap)
      .scrollable(true)
      .animationDuration(10)
      .barBackgroundColor(this.barBackgroundColor)
    }
    .height(500)
    .padding({ top: '24vp', left: '24vp', right: '24vp' })
  }
}
```

![tabs5](figures/tabs5.gif)

### Example 5

This example uses **barGridAlign** to set the visible area of the tab bar in grid mode.

```ts
// xxx.ets
@Entry
@Component
struct TabsExample5 {
  private controller: TabsController = new TabsController()
  @State gridMargin: number = 10
  @State gridGutter: number = 10
  @State sm: number = -2
  @State clickedContent: string = "";

  build() {
    Column() {
      Row() {
        Button("gridMargin+10 " + this.gridMargin)
          .width('47%')
          .height(50)
          .margin({ top: 5 })
          .onClick((event?: ClickEvent) => {
            this.gridMargin += 10
          })
          .margin({ right: '6%', bottom: '12vp' })
        Button("gridMargin-10 " + this.gridMargin)
          .width('47%')
          .height(50)
          .margin({ top: 5 })
          .onClick((event?: ClickEvent) => {
            this.gridMargin -= 10
          })
          .margin({ bottom: '12vp' })
      }

      Row() {
        Button("gridGutter+10 " + this.gridGutter)
          .width('47%')
          .height(50)
          .margin({ top: 5 })
          .onClick((event?: ClickEvent) => {
            this.gridGutter += 10
          })
          .margin({ right: '6%', bottom: '12vp' })
        Button("gridGutter-10 " + this.gridGutter)
          .width('47%')
          .height(50)
          .margin({ top: 5 })
          .onClick((event?: ClickEvent) => {
            this.gridGutter -= 10
          })
          .margin({ bottom: '12vp' })
      }

      Row() {
        Button("sm+2 " + this.sm)
          .width('47%')
          .height(50)
          .margin({ top: 5 })
          .onClick((event?: ClickEvent) => {
            this.sm += 2
          })
          .margin({ right: '6%' })
        Button("sm-2 " + this.sm).width('47%').height(50).margin({ top: 5 })
          .onClick((event?: ClickEvent) => {
            this.sm -= 2
          })
      }

      Text("Clicked content: " + this.clickedContent).width('100%').height(200).margin({ top: 5 })


      Tabs({ barPosition: BarPosition.End, controller: this.controller }) {
        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Pink)
        }.tabBar(BottomTabBarStyle.of($r("sys.media.ohos_app_icon"), "1"))

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Green)
        }.tabBar(BottomTabBarStyle.of($r("sys.media.ohos_app_icon"), "2"))

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Blue)
        }.tabBar(BottomTabBarStyle.of($r("sys.media.ohos_app_icon"), "3"))
      }
      .width('350vp')
      .animationDuration(300)
      .height('60%')
      .barGridAlign({ sm: this.sm, margin: this.gridMargin, gutter: this.gridGutter })
      .backgroundColor(0xf1f3f5)
      .onTabBarClick((index: number) => {
        this.clickedContent += "now index " + index + " is clicked\n";
      })
    }
    .width('100%')
    .height(500)
    .margin({ top: 5 })
    .padding('10vp')
  }
}
```

![tabs5](figures/tabs6.gif)

### Example 6

This example implements the **ScrollableBarModeOptions** parameter of **barMode**. This parameter is effective only in **Scrollable** mode.

```ts
// xxx.ets
@Entry
@Component
struct TabsExample6 {
  private controller: TabsController = new TabsController()
  @State scrollMargin: number = 0
  @State layoutStyle: LayoutStyle = LayoutStyle.ALWAYS_CENTER
  @State text: string = "Text"

  build() {
    Column() {
      Row() {
        Button("scrollMargin+10 " + this.scrollMargin)
          .width('47%')
          .height(50)
          .margin({ top: 5 })
          .onClick((event?: ClickEvent) => {
            this.scrollMargin += 10
          })
          .margin({ right: '6%', bottom: '12vp' })
        Button("scrollMargin-10 " + this.scrollMargin)
          .width('47%')
          .height(50)
          .margin({ top: 5 })
          .onClick((event?: ClickEvent) => {
            this.scrollMargin -= 10
          })
          .margin({ bottom: '12vp' })
      }

      Row() {
        Button ("Add Text")
          .width('47%')
          .height(50)
          .margin({ top: 5 })
          .onClick((event?: ClickEvent) => {
            this.text += 'Add Text'
          })
          .margin({ right: '6%', bottom: '12vp' })
        Button ("Reset Text")
          .width('47%')
          .height(50)
          .margin({ top: 5 })
          .onClick((event?: ClickEvent) => {
            this.text = "Text"
          })
          .margin({ bottom: '12vp' })
      }

      Row() {
        Button("layoutStyle.ALWAYS_CENTER")
          .width('100%')
          .height(50)
          .margin({ top: 5 })
          .fontSize(15)
          .onClick((event?: ClickEvent) => {
            this.layoutStyle = LayoutStyle.ALWAYS_CENTER;
          })
          .margin({ bottom: '12vp' })
      }

      Row() {
        Button("layoutStyle.ALWAYS_AVERAGE_SPLIT")
          .width('100%')
          .height(50)
          .margin({ top: 5 })
          .fontSize(15)
          .onClick((event?: ClickEvent) => {
            this.layoutStyle = LayoutStyle.ALWAYS_AVERAGE_SPLIT;
          })
          .margin({ bottom: '12vp' })
      }

      Row() {
        Button("layoutStyle.SPACE_BETWEEN_OR_CENTER")
          .width('100%')
          .height(50)
          .margin({ top: 5 })
          .fontSize(15)
          .onClick((event?: ClickEvent) => {
            this.layoutStyle = LayoutStyle.SPACE_BETWEEN_OR_CENTER;
          })
          .margin({ bottom: '12vp' })
      }

      Tabs({ barPosition: BarPosition.End, controller: this.controller }) {
        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Pink)
        }.tabBar(SubTabBarStyle.of(this.text))

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Green)
        }.tabBar(SubTabBarStyle.of(this.text))

        TabContent() {
          Column().width('100%').height('100%').backgroundColor(Color.Blue)
        }.tabBar(SubTabBarStyle.of(this.text))
      }
      .animationDuration(300)
      .height('60%')
      .backgroundColor(0xf1f3f5)
      .barMode(BarMode.Scrollable, { margin: this.scrollMargin, nonScrollableLayoutStyle: this.layoutStyle })
    }
    .width('100%')
    .height(500)
    .margin({ top: 5 })
    .padding('24vp')
  }
}
```

![tabs5](figures/tabs7.gif)

### Example 7

This example uses **customContentTransition** to implement a custom tab switching animation.

```ts
// xxx.ets
interface itemType {
  text: string,
  backgroundColor: Color
}

@Entry
@Component
struct TabsCustomAnimationExample {
  @State data: itemType[] = [
    {
      text: 'Red',
      backgroundColor: Color.Red
    },
    {
      text: 'Yellow',
      backgroundColor: Color.Yellow
    },
    {
      text: 'Blue',
      backgroundColor: Color.Blue
    }]
  @State opacityList: number[] = []
  @State scaleList: number[] = []

  private durationList: number[] = []
  private timeoutList: number[] = []
  private customContentTransition: (from: number, to: number) => TabContentAnimatedTransition = (from: number, to: number) => {
    let tabContentAnimatedTransition = {
      timeout: this.timeoutList[from],
      transition: (proxy: TabContentTransitionProxy) => {
        this.scaleList[from] = 1.0
        this.scaleList[to] = 0.5
        this.opacityList[from] = 1.0
        this.opacityList[to] = 0.5
        animateTo({
          duration: this.durationList[from],
          onFinish: () => {
            proxy.finishTransition()
          }
        }, () => {
          this.scaleList[from] = 0.5
          this.scaleList[to] = 1.0
          this.opacityList[from] = 0.5
          this.opacityList[to] = 1.0
        })
      }
    } as TabContentAnimatedTransition
    return tabContentAnimatedTransition
  }

  aboutToAppear(): void {
    let duration = 1000
    let timeout = 1000
    for (let i = 1; i <= this.data.length; i++) {
      this.opacityList.push(1.0)
      this.scaleList.push(1.0)
      this.durationList.push(duration * i)
      this.timeoutList.push(timeout * i)
    }
  }

  build() {
    Column() {
      Tabs() {
        ForEach(this.data, (item: itemType, index: number) => {
          TabContent() {}
          .tabBar(item.text)
          .backgroundColor(item.backgroundColor)
          // Customize the opacity and scale animation.
          .opacity(this.opacityList[index])
          .scale({ x: this.scaleList[index], y: this.scaleList[index] })
        })
      }
      .backgroundColor(0xf1f3f5)
      .width('100%')
      .height(500)
      .customContentTransition(this.customContentTransition)
    }
  }
}
```

![tabs5](figures/tabs8.gif)

### Example 9

This example uses **onChange**, **onAnimationStart**, **onAnimationEnd**, and **onGestureSwipe** APIs to customize the tab bar switching animation.

```ts
@Entry
@Component
struct TabsExample {
  @State currentIndex: number = 0
  @State animationDuration: number = 300
  @State indicatorLeftMargin: number = 0
  @State indicatorWidth: number = 0
  private tabsWidth: number = 0
  private textInfos: [number, number][] = []
  private isStartAnimateTo: boolean = false

  @Builder
  tabBuilder(index: number, name: string) {
    Column() {
      Text(name)
        .fontSize(16)
        .fontColor(this.currentIndex === index ? '#007DFF' : '#182431')
        .fontWeight(this.currentIndex === index ? 500 : 400)
        .id(index.toString())
        .onAreaChange((oldValue: Area, newValue: Area) => {
          this.textInfos[index] = [newValue.globalPosition.x as number, newValue.width as number]
          if (this.currentIndex === index && !this.isStartAnimateTo) {
            this.indicatorLeftMargin = this.textInfos[index][0]
            this.indicatorWidth = this.textInfos[index][1]
          }
        })
    }.width('100%')
  }

  build() {
    Stack({ alignContent: Alignment.TopStart }) {
      Tabs({ barPosition: BarPosition.Start }) {
        TabContent() {
          Column().width('100%').height('100%').backgroundColor('#00CB87')
        }.tabBar(this.tabBuilder(0, 'green'))

        TabContent() {
          Column().width('100%').height('100%').backgroundColor('#007DFF')
        }.tabBar(this.tabBuilder(1, 'blue'))

        TabContent() {
          Column().width('100%').height('100%').backgroundColor('#FFBF00')
        }.tabBar(this.tabBuilder(2, 'yellow'))

        TabContent() {
          Column().width('100%').height('100%').backgroundColor('#E67C92')
        }.tabBar(this.tabBuilder(3, 'pink'))
      }
      .onAreaChange((oldValue: Area, newValue: Area)=> {
        this.tabsWidth = newValue.width as number
      })
      .barWidth('100%')
      .barHeight(56)
      .width('100%')
      .height(296)
      .backgroundColor('#F1F3F5')
      .animationDuration(this.animationDuration)
      .onChange((index: number) => {
        this.currentIndex = index // Listen for index changes to switch between tab pages.
      })
      .onAnimationStart((index: number, targetIndex: number, event: TabsAnimationEvent) => {
        // Triggered when the tab switching animation starts. The underline moves with the active tab, along with a width gradient.
        this.currentIndex = targetIndex
        this.startAnimateTo(this.animationDuration, this.textInfos[targetIndex][0], this.textInfos[targetIndex][1])
      })
      .onAnimationEnd((index: number, event: TabsAnimationEvent) => {
        // Triggered when the tab switching animation ends. The underline animation stops.
        let currentIndicatorInfo = this.getCurrentIndicatorInfo(index, event)
        this.startAnimateTo(0, currentIndicatorInfo.left, currentIndicatorInfo.width)
      })
      .onGestureSwipe((index: number, event: TabsAnimationEvent) => {
        // Triggered on a frame-by-frame basis when the tab is switched by a swipe.
        let currentIndicatorInfo = this.getCurrentIndicatorInfo(index, event)
        this.currentIndex = currentIndicatorInfo.index
        this.indicatorLeftMargin = currentIndicatorInfo.left
        this.indicatorWidth = currentIndicatorInfo.width
      })

      Column()
        .height(2)
        .width(this.indicatorWidth)
        .margin({ left: this.indicatorLeftMargin, top:48})
        .backgroundColor('#007DFF')
    }.width('100%')
  }

  private getCurrentIndicatorInfo(index: number, event: TabsAnimationEvent): Record<string, number> {
    let nextIndex = index
    if (index > 0 && event.currentOffset > 0) {
      nextIndex--
    } else if (index < 3 && event.currentOffset < 0) {
      nextIndex++
    }
    let indexInfo = this.textInfos[index]
    let nextIndexInfo = this.textInfos[nextIndex]
    let swipeRatio = Math.abs(event.currentOffset / this.tabsWidth)
    let currentIndex = swipeRatio > 0.5 ? nextIndex : index  // When the scroll distance exceeds half of the page, the tab bar switches to the next page.
    let currentLeft = indexInfo[0] + (nextIndexInfo[0] - indexInfo[0]) * swipeRatio
    let currentWidth = indexInfo[1] + (nextIndexInfo[1] - indexInfo[1]) * swipeRatio
    return { 'index': currentIndex, 'left': currentLeft, 'width': currentWidth }
  }

  private startAnimateTo(duration: number, leftMargin: number, width: number) {
    this.isStartAnimateTo = true
    animateTo({
      duration: duration, // Animation duration.
      curve: Curve.Linear, // Animation curve.
      iterations: 1, // Number of playback times.
      playMode: PlayMode.Normal, // Animation playback mode.
      onFinish: () => {
        this.isStartAnimateTo = false
        console.info('play end')
      }
    }, () => {
      this.indicatorLeftMargin = leftMargin
      this.indicatorWidth = width
    })
  }
}
```

![tabs10](figures/tabs10.gif)
