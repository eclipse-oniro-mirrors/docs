# Scroll

The **\<Scroll>** component scrolls the content when the layout size of a component exceeds the size of its parent component.

>  **NOTE**
>  - This component is supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.
>  - When nesting a **\<List>** within this component, specify the width and height for the **\<List>** under scenarios where consistently high performance is required. If the width and height are not specified, this component will load all content of the **\<List>**.
>  - This component can scroll only when the size on the main axis is less than the content size.
>  - This component can produce a bounce effect only when there is more than one screen of content.


## Child Components

This component supports only one child component.


## APIs

Scroll(scroller?: Scroller)

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| scroller | [Scroller](#scroller) | No| Scroller, which can be bound to scrollable components.|

## Attributes

In addition to the [universal attributes](ts-universal-attributes-size.md), the following attributes are supported.

| Name            | Type                                   | Description       |
| -------------- | ---------------------------------------- | --------- |
| scrollable     | [ScrollDirection](#scrolldirection)                        | Scroll direction.<br>Default value: **ScrollDirection.Vertical**|
| scrollBar      | [BarState](ts-appendix-enums.md#barstate) | Scrollbar status.<br>Default value: **BarState.Auto**<br>**NOTE**<br>If the container component cannot be scrolled, the scrollbar is not displayed. If the size of a child component of a container component is infinite, the scrollbar cannot be dragged or scrolled with the child component.<br>Since API version 10, when the scrollable component has rounded corners, to prevent the scrollbar from being cut off by the corners, the scrollbar will automatically calculate the clearance distance from the top and bottom.|
| scrollBarColor | string \| number \| [Color](ts-appendix-enums.md#color)   | Color of the scrollbar.<br/>Default value: **'\#182431'** (40% opacity)|
| scrollBarWidth | string \| number         | Width of the scrollbar. This attribute cannot be set in percentage.<br>Default value: **4**<br>Unit: vp<br>**NOTE**<br>After the width is set, the scrollbar is displayed with the set width in normal state and pressed state. If the set width exceeds the height of the **\<Scroll>** component on the main axis, the scrollbar reverts to the default width.|
| scrollSnap<sup>10+</sup>     | [ScrollSnapOptions](#scrollsnapoptions10)                     | Scroll snapping mode.|
| edgeEffect     | value:[EdgeEffect](ts-appendix-enums.md#edgeeffect),<br>options?:[EdgeEffectOptions<sup>11+</sup>](#edgeeffectoptions11)        | Effect used at the edges of the component when the boundary of the scrollable content is reached.<br>\- **value**: effect used at the edges of the **\<Scroll>** component when the boundary of the scrollable content is reached. The spring effect and shadow effect are supported.<br>Default value: **EdgeEffect.None**<br>\- **options**: whether to enable the scroll effect when the component content size is smaller than the component itself.<br>Default value: **true**|
| enableScrollInteraction<sup>10+</sup>  |  boolean  |   Whether to support scroll gestures. When this attribute is set to **false**, scrolling by finger or mouse is not supported, but the scrolling controller API is not affected.<br>Default value: **true**     |
| nestedScroll<sup>10+</sup>                 | [NestedScrollOptions](#nestedscrolloptions10)         | Nested scrolling options. You can set the nested scrolling mode in the forward and backward directions to implement scrolling linkage with the parent component.<br>Default value: **{ scrollForward: NestedScrollMode.SELF_ONLY, scrollBackward: NestedScrollMode.SELF_ONLY }**|
| friction<sup>10+</sup> | number \| [Resource](ts-types.md#resource)    | Friction coefficient. It applies only to gestures in the scrolling area, and it affects only indirectly the scroll chaining during the inertial scrolling process.<br>Default value: **0.9** for wearable devices and **0.6** for non-wearable devices<br>Since API version 11, the default value for non-wearable devices is **0.7**.<br>**NOTE**<br>A value less than or equal to 0 evaluates to the default value.|
| enablePaging<sup>11+</sup>                 | boolean  | Whether to enable the swipe-to-turn-pages feature.<br>Default value: **false**<br>**NOTE**<br>If both **enablePaging** and **scrollSnap** are set, **scrollSnap** takes effect, but **enablePaging** does not.|

### flingSpeedLimit<sup>11+</sup>

flingSpeedLimit(speedLimit: number)

Sets the maximum starting fling speed when the fling animation starts. The unit is vp/s.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name    | Type  | Mandatory| Description                           |
| ---------- | ------ | ---- | ------------------------------- |
| speedLimit | number | Yes  | Maximum starting fling speed when the fling animation starts.|

## ScrollDirection
| Name      | Description                    |
| ---------- | ------------------------ |
| Horizontal | Only horizontal scrolling is supported.    |
| Vertical   | Only vertical scrolling is supported.    |
| None       | Scrolling is disabled.              |
| Free<sup>(deprecated) </sup> | Vertical or horizontal scrolling is supported.<br> This API is deprecated since API version 9.|

## ScrollSnapOptions<sup>10+</sup>
| Name      | Type   | Mandatory  | Description      |
| ---------- | --------------------|-------------------- | -------- |
| snapAlign  | [ScrollSnapAlign](ts-container-list.md#scrollsnapalign10)   | Yes| Alignment mode for the scroll snap position.<br>Default value: **ScrollSnapAlign.NONE**|
| snapPagination | [Dimension](ts-types.md#dimension10) \| Array\<Dimension\> | No| Snap points for the **\<Scroll>** component. Each snap point defines the offset from an edge to which the **\<Scroll>** component can scroll.<br>**NOTE**<br>1. A value of the **Dimension** type indicates the size per page. The system automatically works out the position of each snap point based on the value. For example, if the value is **500**, the position of the snap point is [0,500,1000,1500, ...].<br>2. A value of the **Array\<Dimension\>** type indicates an array of snap point positions defined by **Dimension**. The range of each dimension is [0, scrollable distance]. Point 0 and the bottom of the scrollable distance automatically become the snap points.<br>3. If this attribute is not set or **Dimension** is set to a value less than or equal to 0, the value is regarded as an abnormal value. In this case, there is no scroll snapping. When the value is of the **Array\<Dimension\>** type, the items in the array must be monotonically increasing.<br>4. When the value is a percentage, the actual size is the product of the viewport of the **\<Scroll>** component and the percentage value.|
| enableSnapToStart | boolean   | No| Whether to enable the snap to start feature. When scroll snapping is defined for the **\<Scroll>** component, setting this attribute to **false** enables the component to scroll between the start edge and the first snap point.<br>**NOTE**<br>1. Default value: **true**<br>2. This attribute takes effect only when **snapPagination** is set to a value of the **Array\<Dimension\>** type; it does not work with values of the **Dimension** type.|
| enableSnapToEnd | boolean   | No| Whether to enable the snap to end feature. When scroll snapping is defined for the **\<Scroll>** component, setting this attribute to **false** enables the component to scroll between the end edge and the last snap point.<br>**NOTE**<br>1. Default value: **true**<br>2. This attribute takes effect only when **snapPagination** is set to a value of the **Array\<Dimension\>** type; it does not work with values of the **Dimension** type.|

## Events

| Name                                                        | Description                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| onScrollFrameBegin<sup>9+</sup>(event: (offset: number, state: [ScrollState](ts-container-list.md#scrollstate)) => { offsetRemain: number; }) | Triggered when each frame scrolling starts. The input parameters indicate the amount by which the **\<Scroll>** component will scroll. The event handler then works out the amount by which the component needs to scroll based on the real-world situation and returns the result.<br>\- **offset**: amount to scroll by.<br>\- **state**: current scrolling status.<br>- **offsetRemain**: actual amount by which the component scrolls.<br>**NOTE**<br>1. This event is triggered when scrolling is started by the **\<Scroll>** component or other input settings, such as keyboard and mouse operations.<br>2. This event is not triggered when the controller API is called.<br>3. This event does not support the out-of-bounds bounce effect.<br>4. This event is not triggered when the scroll bar is dragged.<br>**NOTE**<br>The value of **offsetRemain** can be a negative value.<br>If the **onScrollFrameBegin** event and **scrollBy** method are used to implement nested scrolling, set the **edgeEffect** attribute of the scrollable child component to **None**. For example, if a **\<List>** is nested in the **\<Scroll>** component, **edgeEffect** of the **\<List>** must be set to **EdgeEffect.None**.|
| onScroll(event: (xOffset: number, yOffset: number) => void)  | Triggered to return the horizontal and vertical offsets during scrolling when the specified scroll event occurs.<br>**NOTE**<br>1. This event is triggered when scrolling is started by the **\<Scroll>** component or other input settings, such as keyboard and mouse operations.<br>2. This event is triggered when the controller API is called.<br>3. This event supports the out-of-bounds bounce effect.|
| onScrollEdge(event: (side: Edge) => void)                    | Triggered when scrolling reaches the edge.<br>**NOTE**<br>1. This event is triggered when scrolling reaches the edge after being started by the **\<Scroll>** component or other input settings, such as keyboard and mouse operations.<br>2. This event is triggered when the controller API is called.<br>3. This event supports the out-of-bounds bounce effect.|
| onScrollEnd<sup>(deprecated) </sup>(event: () => void)       | Triggered when scrolling stops.<br>This event is deprecated since API version 9. Use the **onScrollStop** event instead.<br>**NOTE**<br>1. This event is triggered when scrolling is stopped by the **\<Scroll>** component or other input settings, such as keyboard and mouse operations.<br>2. This event is triggered when the controller API is called, accompanied by a transition animation.|
| onScrollStart<sup>9+</sup>(event: () => void)                | Triggered when scrolling starts and is initiated by the user's finger dragging the **\<Scroll>** component or its scrollbar. This event is also triggered when the animation contained in the scrolling triggered by [Scroller](#scroller) starts.<br>**NOTE**<br>1. This event is triggered when scrolling is started by the **\<Scroll>** component or other input settings, such as keyboard and mouse operations.<br>2. This event is triggered when the controller API is called, accompanied by a transition animation.|
| onScrollStop<sup>9+</sup>(event: () => void)                 | Triggered when scrolling stops after the user's finger leaves the screen. This event is also triggered when the animation contained in the scrolling triggered by [Scroller](#scroller) stops.<br>**NOTE**<br>1. This event is triggered when scrolling is stopped by the **\<Scroll>** component or other input settings, such as keyboard and mouse operations.<br>2. This event is triggered when the controller API is called, accompanied by a transition animation.|
| onReachStart<sup>11+</sup>(event: () => void)          | Triggered when the **\<Scroll>** component reaches the start position.<br>**NOTE**<br>This event is triggered once when the component is initialized and once when the component scrolls to the start position. When the component's edge effect is the spring effect, this event is triggered once when the component passes the start position and is triggered again when the component returns to the start position.|
| onReachEnd<sup>11+</sup>(event: () => void)            | Triggered when the **\<Scroll>** component reaches the end position.<br>**NOTE**<br>When the component's edge effect is the spring effect, this event is triggered once when the component passes the end position and is triggered again when the component returns to the end position.|

>  **NOTE**
>
>  If the **onScrollFrameBegin** event and **scrollBy** method are used to implement nested scrolling, set the **edgeEffect** attribute of the scrollable child component to **None**. For example, if a **\<List>** is nested in the **\<Scroll>** component, **edgeEffect** of the **\<List>** must be set to **EdgeEffect.None**.

## Scroller

Implements a controller for a scrollable container component. You can bind this component to a container component and use it to control the scrolling of that component. One controller can control only one container component. The supported container components are **\<List>**, **\<Scroll>**, **\<ScrollBar>**, **\<Grid>**, and **\<WaterFlow>**.


### Objects to Import

```
scroller: Scroller = new Scroller()
```


### scrollTo

scrollTo(value: { xOffset: number | string, yOffset: number | string, animation?: { duration?: number, curve?: Curve | ICurve } | boolean }): void


Scrolls to the specified position.

**Parameters**

| Name   | Type                                                    | Mandatory| Description                                                    |
| --------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| xOffset   | number \| string                                   | Yes  | Horizontal scrolling offset.<br>**NOTE**<br>This parameter cannot be set in percentage.<br>If the value is less than 0, the offset will be 0 for scrolling without animation; scrolling with animation stops when it reaches the start position.<br>This parameter takes effect only when the scroll axis is the x-axis.|
| yOffset   | number \| string                                   | Yes  | Vertical scrolling offset.<br>**NOTE**<br>This parameter cannot be set in percentage.<br>If the value is less than 0, the offset will be 0 for scrolling without animation; scrolling with animation stops when it reaches the start position.<br>This parameter takes effect only when the scroll axis is the y-axis.|
| animation | {duration?: number, curve?: [Curve](ts-appendix-enums.md#curve) \| [ICurve](../js-apis-curve.md#icurve)<sup>9+ </sup>} \| boolean<sup>10+ </sup> | No  | Animation configuration, which includes the following:<br>- **duration**: scrolling duration.<br>- **curve**: scrolling curve.<br>- **boolean**: whether to enable the default spring animation.<br>Default value:<br>{<br>duration: 1000,<br>curve: Curve.Ease<br>}<br>boolean: false<br>**NOTE**<br>A value less than 0 evaluates to the default value.<br>Currently, the **\<List>**, **\<Scroll>**, **\<Grid>**, and **\<WaterFlow>** support the **Boolean** type and **ICurve**.|


### scrollEdge

scrollEdge(value: Edge): void


Scrolls to the edge of the container, regardless of the scroll axis direction. **Edge.Top** and **Edge.Start** produce the same effect, and **Edge.Bottom** and **Edge.End** produce the same effect.

**Parameters**

| Name  | Type| Mandatory  | Description     |
| ----- | ---- | ---- | --------- |
| value | [Edge](ts-appendix-enums.md#edge) | Yes   | Edge position to scroll to.|

### scrollPage<sup>9+</sup>

scrollPage(value: { next: boolean }): void

Scrolls to the next or previous page.

**Parameters**

| Name                           | Type                         | Mandatory| Description                                                   |
| --------------------------------- | --------------------------------- | ---- | ----------------------------------------------------------- |
| next                              | boolean                           | Yes  | Whether to turn to the next page. The value **true** means to scroll to the next page, and **false** means to scroll to the previous page.        |

### scrollPage<sup>(deprecated)</sup>

scrollPage(value: { next: boolean, direction?: Axis }): void

Scrolls to the next or previous page. This API is deprecated since API version 9. You are advised to use [scrollPage<sup>9+</sup>](#scrollpage9) instead.

**Parameters**

| Name      | Type   | Mandatory  | Description                          |
| --------- | ------- | ---- | ------------------------------ |
| next      | boolean | Yes   | Whether to turn to the next page. The value **true** means to scroll to the next page, and **false** means to scroll to the previous page.|
| direction | [Axis](ts-appendix-enums.md#axis)    | No   | Scrolling direction: horizontal or vertical.              |

### currentOffset

currentOffset(): OffsetResult

| Type | Description|
| -------- | -------- |
|  [OffsetResult<sup>11+</sup>](#offsetresult11) | Obtains the scrolling offset.<br>**NOTE**<br>If **Scroller** is not bound to a container component or the container component is released abnormally, the return value for **currentOffset** is null.|

### scrollToIndex

scrollToIndex(value: number, smooth?: boolean, align?: ScrollAlign): void

Scrolls to the item with the specified index.

When **smooth** is set to **true**, all passed items are loaded and counted in layout calculation. This may result in performance issues if a large number of items are involved.


>  **NOTE**
>
>  This API only works for the **\<Grid>**, **\<List>**, and **\<WaterFlow>** components.

**Parameters**

| Name               | Type| Mandatory| Description                                                    |
| --------------------- | -------- | ---- | ------------------------------------------------------------ |
| value | number   | Yes  | Index of the item to be scrolled to in the container.<br>**NOTE**<br>If the value set is a negative value or greater than the maximum index of the items in the container, the value is deemed abnormal, and no scrolling will be performed.                    |
| smooth | boolean  | No  | Whether to enable the smooth animation for scrolling to the item with the specified index. The value **true** means to enable that the smooth animation, and **false** means the opposite.<br>Default value: **false**|
| align | [ScrollAlign](#scrollalign10)  | No  | How the list item to scroll to is aligned with the container.<br>Default value when the container is **\<List>**: **ScrollAlign.START**<br> Default value when the container is **\<Grid>**: **ScrollAlign.AUTO**<br> Default value when the container is **\<WaterFlow>**: **ScrollAlign.START**<br>**NOTE**<br>This parameter is only available for the **\<List>**, **\<Grid>**, and **\<WaterFlow>** components.|

### scrollBy<sup>9+</sup>

scrollBy(dx: Length, dy: Length): void


Scrolls by the specified amount.


>  **NOTE**
>
>  This API is available for the **\<Scroll>**, **\<List>**, **\<Grid>**, and **\<WaterFlow>** components.

**Parameters**

| Name  | Type  | Mandatory  | Description             |
| ----- | ------ | ---- | ----------------- |
| dx |  [Length](ts-types.md#length) | Yes   | Amount to scroll by in the horizontal direction. The percentage format is not supported.|
| dy |  [Length](ts-types.md#length) | Yes   | Amount to scroll by in the vertical direction. The percentage format is not supported.|

### isAtEnd<sup>10+</sup>

isAtEnd(): boolean

Checks whether the component has scrolled to the bottom.

>  **NOTE**
>
>  This API is available for the **\<Scroll>**, **\<List>**, **\<Grid>**, and **\<WaterFlow>** components.

**Return value**

| Type        | Description         |
| ------- | -------- |
| boolean | The value **true** means that the component has scrolled to the bottom, and **false** means the opposite.|

### getItemRect<sup>11+</sup>

getItemRect(index: number): RectResult

Obtains the size and position of a child component.

>  **NOTE**
>
>  This API is available for the **\<Scroll>**, **\<List>**, **\<Grid>**, and **\<WaterFlow>** components.

**Parameters**

| Name  | Type  | Mandatory  | Description             |
| ----- | ------ | ---- | ----------------- |
| index | number | Yes   | Index of the target child component.|

> **NOTE**
>
> - The value of **index** must be the index of a child component visible in the display area. Otherwise, the value is considered invalid.
> - The size and position returned for an invalid value are both **0**.

**Return value**

| Type      | Description      |
| -------------------  | -------- |
| [RectResult](ts-types.md#rectresult10) | Size and position of the child component relative to the component.<br>Unit: vp|

## OffsetResult<sup>11+</sup>

| Name| Type                                                      | Description                                                        |
| --------------|-------------------------------------------- | ------------------------------------------------------------ |
| xOffset | number | Horizontal scrolling offset.<br>The unit of the return value is vp.|
| yOffset | number | Vertical scrolling offset.<br>The unit of the return value is vp.|

## ScrollAlign<sup>10+</sup>

| Name    | Description                            |
| ------ | ------------------------------ |
| START   | The start edge of the list item is flush with the start edge of the list. |
| CENTER | The list item is centered along the main axis of the list.       |
| END  | The end edge of the list item is flush with the end edge of the list.|
| AUTO  | The list item is automatically aligned.<br>If the list item is fully contained within the display area, no adjustment is performed. Otherwise, the list item is aligned so that its start or end edge is flush with the start or end edge of the list, whichever requires a shorter scrolling distance.|

## NestedScrollOptions<sup>10+ </sup>
| Name  | Type | Mandatory| Description             |
| ----- | ------ | ------ | ----------------- |
| scrollForward | NestedScrollMode | Yes| Nested scrolling option when the component scrolls forward.|
| scrollBackward | NestedScrollMode | Yes| Nested scrolling option when the component scrolls backward.|

## NestedScrollMode<sup>10+ </sup>
| Name    | Description                            |
| ------ | ------------------------------ |
| SELF_ONLY   | The scrolling is contained within the component, and no scroll chaining occurs, that is, the parent component does not scroll when the component scrolling reaches the boundary. |
| SELF_FIRST | The component scrolls first, and when it hits the boundary, the parent component scrolls. When the parent component hits the boundary, its edge effect is displayed. If no edge effect is specified for the parent component, the edge effect of the child component is displayed instead.       |
| PARENT_FIRST  | The parent component scrolls first, and when it hits the boundary, the component scrolls. When the component hits the boundary, its edge effect is displayed. If no edge effect is specified for the component, the edge effect of the parent component is displayed instead.|
| PARALLEL  | The component and its parent component scroll at the same time. When both the component and its parent component hit the boundary, the edge effect of the component is displayed. If no edge effect is specified for the component, the edge effect of the parent component is displayed instead.|

## EdgeEffectOptions<sup>11+ </sup>
| Name  | Type | Mandatory| Description             |
| ----- | ------| ------- | ----------------- |
| alwaysEnabled | boolean | Yes| Whether to enable the scroll effect when the component content is smaller than the component itself.|


## Example
### Example 1

```ts
// xxx.ets
import Curves from '@ohos.curves'

@Entry
@Component
struct ScrollExample {
  scroller: Scroller = new Scroller()
  private arr: number[] = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

  build() {
    Stack({ alignContent: Alignment.TopStart }) {
      Scroll(this.scroller) {
        Column() {
          ForEach(this.arr, (item: number) => {
            Text(item.toString())
              .width('90%')
              .height(150)
              .backgroundColor(0xFFFFFF)
              .borderRadius(15)
              .fontSize(16)
              .textAlign(TextAlign.Center)
              .margin({ top: 10 })
          }, (item: string) => item)
        }.width('100%')
      }
      .scrollable(ScrollDirection.Vertical) // The scrollbar scrolls in the vertical direction.
      .scrollBar(BarState.On) // The scrollbar is always displayed.
      .scrollBarColor(Color.Gray) // The scrollbar color is gray.
      .scrollBarWidth(10) // The scrollbar width is 10.
      .friction(0.6)
      .edgeEffect(EdgeEffect.None)
      .onScroll((xOffset: number, yOffset: number) => {
        console.info(xOffset + ' ' + yOffset)
      })
      .onScrollEdge((side: Edge) => {
        console.info('To the edge')
      })
      .onScrollStop(() => {
        console.info('Scroll Stop')
      })

      Button('scroll 150')
        .height('5%')
        .onClick(() => { // Click to scroll down by 150.0 vp.
          this.scroller.scrollBy(0, 150)
        })
        .margin({ top: 10, left: 20 })
      Button('scroll 100')
        .height('5%')
        .onClick(() => { // Click to scroll down by 100.0 vp.
          const yOffset: number = this.scroller.currentOffset().yOffset;
          this.scroller.scrollTo({ xOffset: 0, yOffset: yOffset + 100 })
        })
        .margin({ top: 60, left: 20 })
      Button('scroll 100')
        .height('5%')
        .onClick(() => {// Click to scroll down by 100.0 vp. An animation is applied to the scrolling.
          let curve = Curves.interpolatingSpring(10, 1, 228, 30) // Create a step curve.
          const yOffset: number = this.scroller.currentOffset().yOffset;
          this.scroller.scrollTo({ xOffset: 0, yOffset: yOffset + 100, animation: { duration: 1000, curve: curve } })
        })
        .margin({ top: 110, left: 20 })
      Button('back top')
        .height('5%')
        .onClick(() => { // Click to go back to the top.
          this.scroller.scrollEdge(Edge.Top)
        })
        .margin({ top: 160, left: 20 })
      Button('next page')
        .height('5%')
        .onClick(() => { // Click to go to the next page.
          this.scroller.scrollPage({ next: true })
        })
        .margin({ top: 210, left: 20 })
    }.width('100%').height('100%').backgroundColor(0xDCDCDC)
  }
}
```

![en-us_image_0000001174104386](figures/en-us_image_0000001174104386.gif)

### Example 2
```ts
@Entry
@Component
struct NestedScroll {
  @State listPosition: number = 0; // 0 indicates scrolling to the top of the list, 1 indicates scrolling to the middle of the list, and 2 indicates scrolling to the bottom of the list.
  private arr: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
  private scrollerForScroll: Scroller = new Scroller()
  private scrollerForList: Scroller = new Scroller()

  build() {
    Flex() {
      Scroll(this.scrollerForScroll) {
        Column() {
          Text("Scroll Area")
            .width("100%")
            .height("40%")
            .backgroundColor(0X330000FF)
            .fontSize(16)
            .textAlign(TextAlign.Center)
            .onClick(() => {
              this.scrollerForList.scrollToIndex(5)
            })

          List({ space: 20, scroller: this.scrollerForList }) {
            ForEach(this.arr, (item: number) => {
              ListItem() {
                Text("ListItem" + item)
                  .width("100%")
                  .height("100%")
                  .borderRadius(15)
                  .fontSize(16)
                  .textAlign(TextAlign.Center)
                  .backgroundColor(Color.White)
              }.width("100%").height(100)
            }, (item: string) => item)
          }
          .width("100%")
          .height("50%")
          .edgeEffect(EdgeEffect.None)
          .friction(0.6)
          .onReachStart(() => {
            this.listPosition = 0
          })
          .onReachEnd(() => {
            this.listPosition = 2
          })
          .onScrollFrameBegin((offset: number) => {
            if ((this.listPosition == 0 && offset <= 0) || (this.listPosition == 2 && offset >= 0)) {
              this.scrollerForScroll.scrollBy(0, offset)
              return { offsetRemain: 0 }
            }
            this.listPosition = 1
            return { offsetRemain: offset };
          })

          Text("Scroll Area")
            .width("100%")
            .height("40%")
            .backgroundColor(0X330000FF)
            .fontSize(16)
            .textAlign(TextAlign.Center)
        }
      }
      .width("100%").height("100%")
    }.width('100%').height('100%').backgroundColor(0xDCDCDC).padding(20)
  }
}
```

![NestedScroll](figures/NestedScroll.gif)

### Example 3
```ts
@Entry
@Component
struct StickyNestedScroll {
  @State arr: number[] = []

  @Styles
  listCard() {
    .backgroundColor(Color.White)
    .height(72)
    .width("100%")
    .borderRadius(12)
  }

  build() {
    Scroll() {
      Column() {
        Text("Scroll Area")
          .width("100%")
          .height("40%")
          .backgroundColor('#0080DC')
          .textAlign(TextAlign.Center)
        Tabs({ barPosition: BarPosition.Start }) {
          TabContent() {
            List({ space: 10 }) {
              ForEach(this.arr, (item: number) => {
                ListItem() {
                  Text("item" + item)
                    .fontSize(16)
                }.listCard()
              }, (item: string) => item)
            }.width("100%")
            .edgeEffect(EdgeEffect.Spring)
            .nestedScroll({
              scrollForward: NestedScrollMode.PARENT_FIRST,
              scrollBackward: NestedScrollMode.SELF_FIRST
            })
          }.tabBar("Tab1")

          TabContent() {
          }.tabBar("Tab2")
        }
        .vertical(false)
        .height("100%")
      }.width("100%")
    }
    .edgeEffect(EdgeEffect.Spring)
    .friction(0.6)
    .backgroundColor('#DCDCDC')
    .scrollBar(BarState.Off)
    .width('100%')
    .height('100%')
  }

  aboutToAppear() {
    for (let i = 0; i < 30; i++) {
      this.arr.push(i)
    }
  }
}
```
![NestedScroll2](figures/NestedScroll2.gif)
### Example 4
```ts
@Entry
@Component
struct Index {
  scroller: Scroller = new Scroller;
  private arr: number[] = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15]
  build() {
    Scroll(this.scroller) {
      Column() {
        ForEach(this.arr, (item: number) => {
          Text(item.toString())
            .width('90%')
            .height(200)
            .backgroundColor(0xFFFFFF)
            .borderWidth(1)
            .borderColor(Color.Black)
            .borderRadius(15)
            .fontSize(16)
            .textAlign(TextAlign.Center)
        }, (item: string) => item)
      }.width('100%').backgroundColor(0xDCDCDC)
    }
    .backgroundColor(Color.Yellow)
    .height('100%')
    .edgeEffect(EdgeEffect.Spring)
    .scrollSnap({snapAlign:ScrollSnapAlign.START, snapPagination:400, enableSnapToStart:true, enableSnapToEnd:true})
  }
}
```
![NestedScrollSnap](figures/NestedScrollSnap.gif)
