# @ohos.data.uniformDataStruct (标准化数据结构)

本模块为统一数据管理框架（Unified Data Management Framework，UDMF）的组成部分，针对多对多跨应用数据共享的不同业务场景提供了部分标准化数据类型[UniformDataType](js-apis-data-uniformTypeDescriptor.md#uniformdatatype)对应的数据结构，方便不同应用间进行数据交互，减少数据类型适配的工作量。

> **说明：**
>
> 本模块首批接口从API version 12开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```js
import { uniformDataStruct } from '@kit.ArkData';
```

## PlainText

纯文本类型数据，用于描述纯文本类型数据。

**系统能力**：SystemCapability.DistributedDataManager.UDMF.Core

| 名称        | 类型   | 只读 | 可选 | 说明                    |
| ----------- | ------ | ---- | ---- |-----------------------|
| uniformDataType | 'general.plain-text'| 是   | 否   | 统一数据类型标识，标识为纯文本类型数据，固定为“general.plain-text”，数据类型描述信息见[UniformDataType](js-apis-data-uniformTypeDescriptor.md#uniformdatatype)。                |
| textContent | string | 否   | 否   | 纯文本内容。                |
| abstract    | string | 否   | 是   | 纯文本摘要，非必填字段，默认值为空字符串。 |
| details | Record<string, string> | 否   | 是 | 是一个字典类型对象，key和value都是string类型，用于描述文本内容详细属性。例如，可生成一个details内容为<br />{<br />"title":"标题",<br />"content":"内容"<br />}<br />的数据对象，用于描述一篇文章的详细属性。非必填字段，默认值为空字典对象。 |

**示例：**

```ts
let plainTextDetails : Record<string, string> = {
  'attr1': 'value1',
  'attr2': 'value2',
}
let plainText : uniformDataStruct.PlainText = {
  uniformDataType: 'general.plain-text',
  textContent : 'This is plainText textContent example',
  abstract : 'this is abstract',
  details : plainTextDetails,
}
console.info('plainText.uniformDataType: ' + plainText.uniformDataType);
if(plainText.details != undefined){
  let plainTextDetailsObj : Record<string, string> = plainText.details;
  for(let kv of Object.entries(plainTextDetailsObj)) {
    console.info('plainText.details.attr: ' + kv[0] + ', value:' + kv[1]);
  }
}
```

## Hyperlink

超链接类型数据，用于描述超链接类型数据。

**系统能力**：SystemCapability.DistributedDataManager.UDMF.Core

| 名称        | 类型   | 只读 | 可选 | 说明           |
| ----------- | ------ | ---- | ---- |--------------|
| uniformDataType | 'general.hyperlink'| 是   | 否   | 统一数据类型标识为超链接类型数据，固定为“general.hyperlink”，数据类型描述信息见[UniformDataType](js-apis-data-uniformTypeDescriptor.md#uniformdatatype)。
| url         | string | 否   | 否   | 链接url。       |
| description | string | 否   | 是   | 链接内容描述，非必填字段，默认值为空字符串。 |
| details | Record<string, string> | 否   | 是  | 是一个字典类型对象，key和value都是string类型，用于描述Hyperlink的详细属性内容。例如，可生成一个details内容为<br />{<br />"title":"标题",<br />"content":"内容"<br />}<br />的数据对象。非必填字段，默认值为空字典对象。 |

**示例：**

```ts
let hyperlinkDetails : Record<string, string> = {
  'attr1': 'value1',
  'attr2': 'value2',
}
let hyperlink : uniformDataStruct.Hyperlink = {
  uniformDataType:'general.hyperlink',
  url : 'www.XXX.com',
  description : 'This is the description of this hyperlink',
  details : hyperlinkDetails,
}
console.info('hyperlink.uniformDataType: ' + hyperlink.uniformDataType);
```

## HTML

HTML类型数据，用于描述超文本标记语言数据。

**系统能力**：SystemCapability.DistributedDataManager.UDMF.Core

| 名称         | 类型   | 只读 | 可选 | 说明                    |
| ------------ | ------ | ---- | ---- |-----------------------|
| uniformDataType | 'general.html'| 是   | 否   | 统一数据类型标识为html类型数据，固定为“general.html”，数据类型描述信息见[UniformDataType](js-apis-data-uniformTypeDescriptor.md#uniformdatatype)。
| htmlContent  | string | 否   | 否   | html格式内容。             |
| plainContent | string | 否   | 是   | 去除html标签后的纯文本内容，非必填字段，默认值为空字符串。 |
| details | Record<string, string> | 否   | 是   | 是一个字典类型对象，key和value都是string类型，用于描述HTML的详细属性内容。例如，可生成一个details内容为<br />{<br />"title":"标题",<br />"content":"内容"<br />}<br />的数据对象。非必填字段，默认值为空字典对象。 |

**示例：**

```ts
let htmlObjDetails : Record<string, string> = {
  'attr1': 'value1',
  'attr2': 'value2',
}
let htmlObj : uniformDataStruct.HTML = {
  uniformDataType :'general.html',
  htmlContent : '<div><p>标题</p></div>',
  plainContent : 'this is plainContent',
  details : htmlObjDetails,
}
console.info('htmlObj.uniformDataType: ' + htmlObj.uniformDataType);
```

## OpenHarmonyAppItem

系统定义的桌面图标类型数据。

**系统能力**：SystemCapability.DistributedDataManager.UDMF.Core

| 名称        | 类型   | 只读 | 可选 | 说明              |
| ----------- | ------ | ---- | ---- |-----------------|
| uniformDataType | 'openharmony.app-item'| 是   | 否   | 统一数据类型标识为桌面图标类型数据，固定为“openharmony.app-item”，数据类型描述信息见[UniformDataType](js-apis-data-uniformTypeDescriptor.md#uniformdatatype)。
| appId       | string | 否   | 否   | 图标对应的应用id。      |
| appName     | string | 否   | 否   | 图标对应的应用名。       |
| appIconId   | string | 否   | 否   | 图标的图片id。        |
| appLabelId  | string | 否   | 否   | 图标名称对应的标签id。    |
| bundleName  | string | 否   | 否   | 图标对应的应用bundle名。 |
| abilityName | string | 否   | 否   | 图标对应的应用ability名。 |
| details | Record<string, number \| string \| Uint8Array> | 否   | 是   | 是一个字典类型对象，key是string类型，value可以写入number（数值类型）、string（字符串类型）、Uint8Array（二进制字节数组）类型数据。非必填字段，默认值为空字典对象。|


**示例：**

```ts
let u8Array = new Uint8Array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10]);
let appItemDetails : Record<string, number | string | Uint8Array> = {
  'appItemKey1': 123,
  'appItemKey2': 'appItemValue',
  'appItemKey3': u8Array,
}
let appItem : uniformDataStruct.OpenHarmonyAppItem = {
  uniformDataType:'openharmony.app-item',
  appId : 'MyAppId',
  appName : 'MyAppName',
  appIconId : 'MyAppIconId',
  appLabelId : 'MyAppLabelId',
  bundleName : 'MyBundleName',
  abilityName : 'MyAbilityName',
  details : appItemDetails,
}
console.info('appItem.uniformDataType: ' + appItem.uniformDataType);
```
