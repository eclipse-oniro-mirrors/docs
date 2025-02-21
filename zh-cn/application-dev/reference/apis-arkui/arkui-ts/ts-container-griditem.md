# GridItem

网格容器中单项内容容器。

>  **说明：**
>
>  * 该组件从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。
>  * 仅支持作为[Grid](ts-container-grid.md)组件的子组件使用。
>  * 当GridItem配合LazyForEach使用时，GridItem子组件在GridItem创建时创建。配合if/else、ForEach使用时，或父组件为Grid时，GridItem子组件在GridItem布局时创建。


## 子组件

可以包含单个子组件。

## 接口

GridItem(value?: GridItemOptions)

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                      | 必填 | 说明                                                     |
| ------ | --------------------------------------------- | ---- | ------------------------------------------------------------ |
| value<sup>11+</sup>  | [GridItemOptions](#griditemoptions11对象说明) | 否   | 为GridItem提供可选参数, 该对象内含有[GridItemStyle](#griditemstyle11枚举说明)枚举类型的style参数。 |

## 属性

### rowStart

rowStart(value: number)

设置当前元素起始行号。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明               |
| ------ | ------ | ---- | ------------------ |
| value  | number | 是   | 当前元素起始行号。<br/>需要指定GridItem起始行列号和所占行列数的场景推荐使用[Grid的layoutOptions参数](ts-container-grid.md#gridlayoutoptions10)，详细可参考[Grid的示例1](ts-container-grid.md#示例1固定行列grid)和[Grid的示例3](ts-container-grid.md#示例3可滚动grid设置跨行跨列节点)。 |

### rowEnd

rowEnd(value: number)

设置当前元素终点行号。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明               |
| ------ | ------ | ---- | ------------------ |
| value  | number | 是   | 当前元素终点行号。<br/>需要指定GridItem起始行列号和所占行列数的场景推荐使用[Grid的layoutOptions参数](ts-container-grid.md#gridlayoutoptions10)，详细可参考[Grid的示例1](ts-container-grid.md#示例1固定行列grid)和[Grid的示例3](ts-container-grid.md#示例3可滚动grid设置跨行跨列节点)。 |

### columnStart

columnStart(value: number)

设置当前元素起始列号。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明               |
| ------ | ------ | ---- | ------------------ |
| value  | number | 是   | 当前元素起始列号。<br/>需要指定GridItem起始行列号和所占行列数的场景推荐使用[Grid的layoutOptions参数](ts-container-grid.md#gridlayoutoptions10)，详细可参考[Grid的示例1](ts-container-grid.md#示例1固定行列grid)和[Grid的示例3](ts-container-grid.md#示例3可滚动grid设置跨行跨列节点)。 |

### columnEnd

columnEnd(value: number)

设置当前元素终点列号。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明               |
| ------ | ------ | ---- | ------------------ |
| value  | number | 是   | 当前元素终点列号。<br/>需要指定GridItem起始行列号和所占行列数的场景推荐使用[Grid的layoutOptions参数](ts-container-grid.md#gridlayoutoptions10)，详细可参考[Grid的示例1](ts-container-grid.md#示例1固定行列grid)和[Grid的示例3](ts-container-grid.md#示例3可滚动grid设置跨行跨列节点)。 |

>  **说明：**
>
>  需要指定GridItem起始行列号和所占行列数的场景推荐使用[Grid的layoutOptions参数](ts-container-grid.md#gridlayoutoptions10)，详细可参考[Grid的示例1](ts-container-grid.md#示例1固定行列grid)和[Grid的示例3](ts-container-grid.md#示例3可滚动grid设置跨行跨列节点)。
>
>  起始行号、终点行号、起始列号、终点列号生效规则如下：
>
>  rowStart/rowEnd合理取值范围为0\~总行数-1，columnStart/columnEnd合理取值范围为0\~总列数-1。
>
>  如果设置了rowStart/rowEnd/columnStart/columnEnd，GridItem会占据指定的行数(rowEnd-rowStart+1)或列数(columnEnd-columnStart+1)。
>
>  只有在设置columnTemplate和rowTemplate的Grid中，设置合理的rowStart/rowEnd/columnStart/columnEnd四个属性的GridItem才能按照指定的行列号布局。
>
>  在设置columnTemplate和rowTemplate的Grid中，单独设置行号rowStart/rowEnd或列号columnStart/columnEnd的GridItem会按照一行一列进行布局。
>
>  在只设置columnTemplate的Grid中设置列号columnStart/columnEnd的GridItem按照列数布局。在该区域位置存在GridItem布局，则直接换行进行放置。
>
>  在只设置rowTemplate的Grid中设置行号rowStart/rowEnd的GridItem按照行数布局。在该区域位置存在GridItem布局，则直接换列进行放置。
>
>  在只设置columnTemplate的Grid中，在GridItem上设置了不合理的值，GridItem按照一行一列进行布局。
>
>  columnTemplate和rowTemplate都不设置的Grid中GridItem的行列号属性无效。

### forceRebuild<sup>(deprecated)</sup>

forceRebuild(value: boolean)

设置在触发组件build时是否重新创建此节点。GridItem会根据自身属性和子组件变化自行决定是否需要重新创建，无需设置。

从API version9开始废弃。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                                                    |
| ------ | ------- | ---- | ------------------------------------------------------- |
| value  | boolean | 是   | 在触发组件build时是否重新创建此节点。<br/>默认值：false |

### selectable<sup>8+</sup>

selectable(value: boolean)

设置当前GridItem元素是否可以被鼠标框选。外层Grid容器的鼠标框选开启时，GridItem的框选才生效。

该属性需要在设置[选中态样式](./ts-universal-attributes-polymorphic-style.md#statestyles接口说明)前使用才能生效选中态样式。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                                                  |
| ------ | ------- | ---- | ----------------------------------------------------- |
| value  | boolean | 是   | 当前GridItem元素是否可以被鼠标框选。<br/>默认值：true |

### selected<sup>10+</sup>

selected(value: boolean)

设置当前GridItem选中状态。该属性支持[$$](../../../quick-start/arkts-two-way-sync.md)双向绑定变量。

该属性需要在设置[选中态样式](./ts-universal-attributes-polymorphic-style.md#statestyles接口说明)前使用才能生效选中态样式。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                                     |
| ------ | ------- | ---- | ---------------------------------------- |
| value  | boolean | 是   | 当前GridItem选中状态。<br/>默认值：false |

## GridItemOptions<sup>11+</sup>对象说明

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称  | 类型                  | 必填 | 说明                         |
| ----- | -------------------- | ---- | ---------------------------- |
| style | [GridItemStyle](#griditemstyle11枚举说明) | 否   | 设置GridItem样式。<br/>默认值: GridItemStyle.NONE<br/>设置为GridItemStyle.NONE时无样式。<br/>设置为GridItemStyle.PLAIN时，显示Hover、Press态样式。 |

## GridItemStyle<sup>11+</sup>枚举说明

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称  |枚举值| 描述                     |
| ----- |----| ------------------------ |
| NONE  |  0 | 无样式。                 |
| PLAIN |  1 | 显示Hover、Press态样式。 |

> **说明：**
>
> GridItem焦点态样式设置：Grid组件需要设置4vp规格以上的内边距，用于显示GridItem的焦点框。

## 事件

### onSelect<sup>8+</sup>

onSelect(event:&nbsp;(isSelected:&nbsp;boolean)&nbsp;=&gt;&nbsp;void)

GridItem元素被鼠标框选的状态改变时触发回调。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名     | 类型    | 必填 | 说明                                                         |
| ---------- | ------- | ---- | ------------------------------------------------------------ |
| isSelected | boolean | 是   | 进入鼠标框选范围即被选中返回true，&nbsp;移出鼠标框选范围即未被选中返回false。 |

## 示例

### 示例1（GridItem设置自身位置）
GridItem通过设置合理的ColumnStart、ColumnEnd、RowStart、RowEnd属性来设置自身位置。需要指定GridItem起始行列号和所占行列数的场景推荐使用[Grid的layoutOptions参数](ts-container-grid.md#gridlayoutoptions10)，详细可参考[Grid的示例1](ts-container-grid.md#示例1固定行列grid)和[Grid的示例3](ts-container-grid.md#示例3可滚动grid设置跨行跨列节点)。

```ts
// xxx.ets
@Entry
@Component
struct GridItemExample {
  @State numbers: string[] = ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "10", "11", "12", "13", "14", "15"]

  build() {
    Column() {
      Grid() {
        GridItem() {
          Text('4')
            .fontSize(16)
            .backgroundColor(0xFAEEE0)
            .width('100%')
            .height('100%')
            .textAlign(TextAlign.Center)
        }.rowStart(1).rowEnd(2).columnStart(1).columnEnd(2) // 同时设置合理的行列号

        ForEach(this.numbers, (item: string) => {
          GridItem() {
            Text(item)
              .fontSize(16)
              .backgroundColor(0xF9CF93)
              .width('100%')
              .height('100%')
              .textAlign(TextAlign.Center)
          }
        }, (item: string) => item)

        GridItem() {
          Text('5')
            .fontSize(16)
            .backgroundColor(0xDBD0C0)
            .width('100%')
            .height('100%')
            .textAlign(TextAlign.Center)
        }.columnStart(1).columnEnd(4) // 只设置列号，不会从第1列开始布局
      }
      .columnsTemplate('1fr 1fr 1fr 1fr 1fr')
      .rowsTemplate('1fr 1fr 1fr 1fr 1fr')
      .width('90%').height(300)
    }.width('100%').margin({ top: 5 })
  }
}
```

![zh-cn_image_0000001174582870](figures/zh-cn_image_0000001174582870.gif)

### 示例2（设置GridItem样式）

使用GridItemOptions设置GridItem样式。

```ts
// xxx.ets
@Entry
@Component
struct GridItemExample {
  @State numbers: String[] = ['0', '1', '2']

  build() {
    Column({ space: 5 }) {
      Grid() {
        ForEach(this.numbers, (day: string) => {
          ForEach(this.numbers, (day: string) => {
            GridItem({style:GridItemStyle.NONE}) {
              Text(day)
                .fontSize(16)
                .width('100%')
                .height('100%')
                .textAlign(TextAlign.Center)
                .focusable(true)
            }
            .backgroundColor(0xF9CF93)
          }, (day: string) => day)
        }, (day: string) => day)
      }
      .columnsTemplate('1fr 1fr 1fr')
      .rowsTemplate('1fr 1fr')
      .columnsGap(4)
      .rowsGap(4)
      .width('60%')
      .backgroundColor(0xFAEEE0)
      .height(150)
      .padding('4vp')

      Grid() {
        ForEach(this.numbers, (day: string) => {
          ForEach(this.numbers, (day: string) => {
            GridItem({style:GridItemStyle.PLAIN}) {
              Text(day)
                .fontSize(16)
                .width('100%')
                .height('100%')
                .textAlign(TextAlign.Center)
                .focusable(true)
            }
            .backgroundColor(0xF9CF93)
          }, (day: string) => day)
        }, (day: string) => day)
      }
      .columnsTemplate('1fr 1fr 1fr')
      .rowsTemplate('1fr 1fr')
      .columnsGap(4)
      .rowsGap(4)
      .width('60%')
      .backgroundColor(0xFAEEE0)
      .height(150)
      .padding('4vp')
    }.width('100%').margin({ top: 5 })
  }
}
```

![zh-ch_image_griditem_griditemoptions](figures/zh-ch_image_griditem_griditemoptions.png)
