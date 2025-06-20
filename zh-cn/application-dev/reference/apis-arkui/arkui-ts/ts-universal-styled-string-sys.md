# 属性字符串 (系统接口)

方便灵活应用文本样式的对象，可通过TextController中的[setStyledString](./ts-basic-components-text.md#setstyledstring12)方法与Text组件绑定，可通过RichEditorStyledStringController中的[setStyledString](ts-basic-components-richeditor.md#setstyledstring12)方法与RichEditor组件绑定。

>  **说明：**
>
>  该组件从API version 13开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。
>
>  当前页面仅包含本模块的系统接口，其他公开接口参见[属性字符串](ts-universal-styled-string.md)。

## StyledString

### marshalling

static marshalling(styledString: StyledString): ArrayBuffer

序列化属性字符串。

**系统接口：** 此接口为系统接口。

**原子化服务API：** 从API version 13开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ----- | ----- | ---- | ---- |
| styledString | [StyledString](ts-universal-styled-string.md) | 是  | 属性字符串参数。 |

**返回值：**

| 类型              |说明       |
| ------- | --------------------------------- | 
| ArrayBuffer | 序列化后的buffer信息。<br/>**说明：** <br/>目前支持文本和图片。 |

### unmarshalling

static unmarshalling(buffer: ArrayBuffer): Promise\<StyledString>

反序列化后得到属性字符串。

**系统接口：** 此接口为系统接口。

**原子化服务API：** 从API version 13开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ----- | ----- | ---- | ---- |
| buffer | ArrayBuffer | 是  | 属性字符串序列化后的数据。 |

**返回值：**

| 类型                             | 说明                  |
| -------------------------------- | --------------------- |
| Promise\<[StyledString](ts-universal-styled-string.md)> |Promise对象，返回属性字符串。 |

## 示例

### 示例1 (属性字符串序列化和反序列化)

该示例通过marshalling、unmarshalling属性实现了属性字符串序列化和反序列化的功能。

```ts
// xxx.ets
import { LengthMetrics } from '@kit.ArkUI';

@Entry
@Component
struct Index {
  @State textTitle: string = "序列化和反序列化接口";
  @State textResult: string = "Hello world";
  @State serializeStr: string = "序列化";
  @State flag: boolean = false;
  private textAreaController: TextAreaController = new TextAreaController();
  private buff: Uint8Array = new Uint8Array();
  fontStyle: TextStyle = new TextStyle({
    fontWeight: FontWeight.Lighter,
    fontFamily: 'HarmonyOS Sans',
    fontColor: Color.Green,
    fontSize: LengthMetrics.vp(30),
    fontStyle: FontStyle.Normal
  });
  // 创建属性字符串对象
  styledString: StyledString = new StyledString("Hello world",
    [{
      start: 0,
      length: 11,
      styledKey: StyledStringKey.FONT,
      styledValue: this.fontStyle
    }]);

  @Builder
  controllableBuild() {
    Column() {
      TextArea({
        text: this.textResult,
        controller: this.textAreaController
      }).width('95%').height('40%').enableKeyboardOnFocus(false)

      Button(this.serializeStr)
        .margin(5)
        .onClick(async () => {
          this.flag = !this.flag;
          if (!this.flag) {
            console.info("Debug: 反序列化");
            let styles: StyledString = await StyledString.unmarshalling(this.buff.buffer);
            this.textTitle = "调取decodeTlv接口后，反序列化的结果显示：";
            if (styles == undefined) {
              console.error("Debug: styledString 获取失败！！！");
              return;
            }
            this.textResult = styles.getString();
            console.info("Debug: this.textResult = " + this.textResult);
            let stylesArr = styles.getStyles(0, this.textResult.length, StyledStringKey.FONT);
            console.info("Debug: stylesArr.length = " + stylesArr.length);
            for (let i = 0; i < stylesArr.length; ++i) {
              console.info("Debug: style.start = " + stylesArr[i].start);
              console.info("Debug: style.length = " + stylesArr[i].length);
              console.info("Debug: style.styledKey = " + stylesArr[i].styledKey);
              let font = stylesArr[i].styledValue as TextStyle;
              console.info("Debug: style.fontColor = " + font.fontColor);
              console.info("Debug: style.fontSize = " + font.fontSize);
              console.info("Debug: style.fontFamily = " + font.fontFamily);
              console.info("Debug: style.fontStyle = " + font.fontStyle);
            }
            let subStr = styles.subStyledString(0, 2);
            console.info("Debug: subStr = " + subStr.getString());
            this.serializeStr = "序列化";
          } else {
            console.info("Debug: 序列化");
            let resultBuffer = StyledString.marshalling(this.styledString);
            this.buff = new Uint8Array(resultBuffer);
            this.textTitle = "调取encodeTlv接口后，序列化的结果显示：";
            this.textResult = this.buff.toString();
            console.info("Debug: buff = " + this.buff.toString());
            this.serializeStr = "反序列化";
          }
        })
    }.margin(10)
  }

  build() {
    Column() {
      Blank().margin(30)
      Text(this.textTitle)
      this.controllableBuild()
    }
  }
}
```

### 示例2 (带UserDataSpan的属性字符串序列化和反序列化)

该示例通过marshalling、unmarshalling函数实现了属性字符串及其UserDataSpan序列化和反序列化的功能。

```ts
enum MyUserDataType {
  TYPE1 = 0,
  TYPE2
}

class MyUserData extends UserDataSpan {
  constructor() {
    super();
  }

  marshalling() {
    console.log("MyUserData marshalling...");
    const text = "MyUserData1";
    const buffer = new ArrayBuffer(text.length + 1);
    const uint8View = new Uint8Array(buffer);
    // 写入类型
    uint8View[0] = MyUserDataType.TYPE1;
    for (let i = 1; i < text.length; i++) {
      uint8View[i] = text.charCodeAt(i);
    }
    return uint8View.buffer;
  }

  unmarshalling() {
    console.log("MyUserData unmarshalling...");
    return new MyUserData();
  }
}

class MyUserData2 extends UserDataSpan {
  marshalling() {
    console.log("MyUserData2 marshalling...");
    const text = "MyUserData2";
    const buffer = new ArrayBuffer(text.length + 1);
    const uint8View = new Uint8Array(buffer);
    uint8View[0] = MyUserDataType.TYPE2;
    for (let i = 1; i < text.length; i++) {
      uint8View[i] = text.charCodeAt(i);
    }
    return uint8View.buffer;
  }

  unmarshalling() {
    console.log("MyUserData2 unmarshalling...");
    return new MyUserData2();
  }
}

@Entry
@Component
struct MarshallExample1 {
  controller: TextController = new TextController();

  build() {
    Column() {
      Text(undefined, { controller: this.controller })
      Button("Marshall&UnMarshall")
        .onClick(async () => {
          let myData = new MyUserData();
          let myData2 = new MyUserData2();
          let myStyledString = new MutableStyledString("12345", [{
            start: 0,
            length: 3,
            styledKey: StyledStringKey.USER_DATA,
            styledValue: myData
          }, {
            start: 3,
            length: 1,
            styledKey: StyledStringKey.USER_DATA,
            styledValue: myData2
          }]);

          let buffer = StyledString.marshalling(myStyledString, (marshallingValue: StyledStringMarshallingValue) => {
            // 根据类型选择对应的序列化接口
            if (marshallingValue instanceof MyUserData) {
              console.log("StyledString.marshalling MyUserData");
              let value = marshallingValue as MyUserData;
              return value.marshalling();
            } else if (marshallingValue instanceof MyUserData2) {
              console.log("StyledString.marshalling MyUserData2");
              let value = marshallingValue as MyUserData2;
              return value.marshalling();
            }
            console.log("StyledString.marshalling default");
            return new ArrayBuffer(10);
          });

          let newStyledString = await StyledString.unmarshalling(buffer, (value: ArrayBuffer) => {
            // 1. 读取 type 类型，
            // 2. 根据类型，选择对应的接口解析这个 buffer
            const uint8View = new Uint8Array(value);
            let type = uint8View[0];
            console.log("unmarshalling length:" + uint8View.length);
            if (type == MyUserDataType.TYPE1) {
              console.log("unmarshalling type1:" + type);
              let myUserData = new MyUserData();
              return myUserData.unmarshalling();
            } else if (type == MyUserDataType.TYPE2) {
              console.log("unmarshalling type2:" + type);
              let myUserData = new MyUserData2();
              return myUserData.unmarshalling();
            }
            return new ArrayBuffer(0);
          });
          this.controller.setStyledString(newStyledString);
        })
        .fontSize(20)
        .margin(10)
    }
    .justifyContent(FlexAlign.Center)
    .width('100%')
    .height('100%')
  }
}
```