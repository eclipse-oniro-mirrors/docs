# TimePicker

时间选择组件，根据指定参数创建选择器，支持选择小时及分钟。

>  **说明：**
>
>  该组件从API Version 8开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


## 子组件

无


## 接口

TimePicker(options?: TimePickerOptions)

默认以24小时的时间区间创建滑动选择器。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名  | 类型                                            | 必填 | 说明                     |
| ------- | ----------------------------------------------- | ---- | ------------------------ |
| options | [TimePickerOptions](#timepickeroptions对象说明) | 否   | 配置时间选择组件的参数。 |

## TimePickerOptions对象说明

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称                 | 类型                                            | 必填 | 说明                                                         |
| -------------------- | ----------------------------------------------- | ---- | ------------------------------------------------------------ |
| selected             | Date                                            | 否   | 设置选中项的时间。<br/>默认值：当前系统时间<br />从API version 10开始，该参数支持[$$](../../../quick-start/arkts-two-way-sync.md)双向绑定变量。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| format<sup>11+</sup> | [TimePickerFormat](#timepickerformat11枚举说明) | 否   | 指定需要显示的TimePicker的格式。<br/>默认值：TimePickerFormat.HOUR_MINUTE <br/>**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。|

## TimePickerFormat<sup>11+</sup>枚举说明

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称               | 说明                     |
| ------------------ | ------------------------ |
| HOUR_MINUTE        | 按照小时和分显示。       |
| HOUR_MINUTE_SECOND | 按照小时、分钟和秒显示。 |

## 属性

除支持[通用属性](ts-universal-attributes-size.md)外，还支持以下属性：

### useMilitaryTime

useMilitaryTime(value: boolean)

设置展示时间是否为24小时制。当展示时间为12小时制时，上下午与小时无联动关系。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                                       |
| ------ | ------- | ---- | ------------------------------------------ |
| value  | boolean | 是   | 展示时间是否为24小时制。<br/>默认值：false |

### disappearTextStyle<sup>10+</sup>

disappearTextStyle(value: PickerTextStyle)

设置所有选项中最上和最下两个选项的文本颜色、字号、字体粗细。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                         | 必填 | 说明                                                         |
| ------ | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| value  | [PickerTextStyle](ts-basic-components-datepicker.md#pickertextstyle10类型说明) | 是   | 所有选项中最上和最下两个选项的文本颜色、字号、字体粗细。<br/>默认值：<br/>{<br/>color: '#ff182431',<br/>font: {<br/>size: '14fp', <br/>weight: FontWeight.Regular<br/>}<br/>} |

### textStyle<sup>10+</sup>

textStyle(value: PickerTextStyle)

设置所有选项中除了最上、最下及选中项以外的文本颜色、字号、字体粗细。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                         | 必填 | 说明                                                         |
| ------ | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| value  | [PickerTextStyle](ts-basic-components-datepicker.md#pickertextstyle10类型说明) | 是   | 所有选项中除了最上、最下及选中项以外的文本颜色、字号、字体粗细。<br/>默认值：<br/>{<br/>color: '#ff182431',<br/>font: {<br/>size: '16fp', <br/>weight: FontWeight.Regular<br/>}<br/>} |

### selectedTextStyle<sup>10+</sup>

selectedTextStyle(value: PickerTextStyle)

设置选中项的文本颜色、字号、字体粗细。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                         | 必填 | 说明                                                         |
| ------ | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| value  | [PickerTextStyle](ts-basic-components-datepicker.md#pickertextstyle10类型说明) | 是   | 选中项的文本颜色、字号、字体粗细。<br/>默认值：<br/>{<br/>color: '#ff007dff',<br/>font: {<br/>size: '20vp', <br/>weight: FontWeight.Medium<br/>}<br/>} |

### loop<sup>11+</sup>

loop(value: boolean)

设置是否启用循环模式。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                                                         |
| ------ | ------- | ---- | ------------------------------------------------------------ |
| value  | boolean | 是   | 是否启用循环模式。<br/>默认值：true，true表示启用循环模式，false表示不启用循环模式。 |

### dateTimeOptions<sup>12+</sup>

dateTimeOptions(value: DateTimeOptions)

设置时分秒是否显示前置0。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                                         | 必填 | 说明                                                         |
| ------ | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| value  | [DateTimeOptions](../../apis-localization-kit/js-apis-intl.md#datetimeoptions) | 是   | 设置时分秒是否显示前置0，目前只支持设置hour、minute和second参数。<br/>默认值：<br/>hour: 24小时制默认为"2-digit"，即有前置0；12小时制默认为"numeric"，即没有前置0。<br/>minute: 默认为"2-digit"，即有前置0。<br/>second: 默认为"2-digit"，即有前置0。<br/> |

### enableHapticFeedback<sup>12+</sup>

enableHapticFeedback(enable: boolean)

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 参数名 | 类型                                          | 必填  | 说明                                                                                  |
| ------ | --------------------------------------------- |-----|-------------------------------------------------------------------------------------|
| enable  | boolean | 是   | 是否支持触控反馈。<br/>默认值：true，true表示开启触控反馈，false表示不开启触控反馈。<br/>设置为true后是否生效，还取决于系统的硬件是否支持。 |

>  **说明：**
>
>  开启触控反馈时，需要在工程的module.json5中配置requestPermissions字段开启振动权限，配置如下：
>  ```json
>  "requestPermissions": [
>  {
>   "name": "ohos.permission.VIBRATE",
>  }
>  ]
>  ```

## 事件

除支持[通用事件](ts-universal-events-click.md)外，还支持以下事件：

### onChange

onChange(callback:&nbsp;(value:&nbsp;TimePickerResult )&nbsp;=&gt;&nbsp;void)

选择时间时触发该事件。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                          | 必填 | 说明           |
| ------ | --------------------------------------------- | ---- | -------------- |
| value  | [TimePickerResult](#timepickerresult对象说明) | 是   | 24小时制时间。 |

## TimePickerResult对象说明

返回值为24小时制时间。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称                 | 类型   | 只读 | 可选 | 说明                                |
| -------------------- | ------ | ---- | ---- | ----------------------------------- |
| hour                 | number | 否   | 否   | 选中时间的时。<br/>取值范围：[0-23] |
| minute               | number | 否   | 否   | 选中时间的分。<br/>取值范围：[0-59] |
| second<sup>11+</sup> | number | 否   | 否   | 选中时间的秒。<br/>取值范围：[0-59] |

## 示例

该示例实现了时间选择组件，根据指定参数创建选择器。

```ts
// xxx.ets
@Entry
@Component
struct TimePickerExample {
  @State isMilitaryTime: boolean = false
  private selectedTime: Date = new Date('2022-07-22T08:00:00')

  build() {
    Column() {
      Button('切换12小时制/24小时制')
        .margin(30)
        .onClick(() => {
          this.isMilitaryTime = !this.isMilitaryTime
        })
      TimePicker({
        selected: this.selectedTime,
      })
        .useMilitaryTime(this.isMilitaryTime)
        .onChange((value: TimePickerResult) => {
          if(value.hour >= 0) {
            this.selectedTime.setHours(value.hour, value.minute)
            console.info('select current date is: ' + JSON.stringify(value))
          }
        })
        .disappearTextStyle({color: Color.Red, font: {size: 15, weight: FontWeight.Lighter}})
        .textStyle({color: Color.Black, font: {size: 20, weight: FontWeight.Normal}})
        .selectedTextStyle({color: Color.Blue, font: {size: 30, weight: FontWeight.Bolder}})
    }.width('100%')
  }
}
```

![timePicker](figures/timePicker.gif)