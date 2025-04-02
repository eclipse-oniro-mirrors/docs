# XML解析


对于以XML作为载体传递的数据，实际使用中需要对相关的节点进行解析，一般包括[解析XML标签和标签值](#解析xml标签和标签值)、[解析XML属性和属性值](#解析xml属性和属性值)、[解析XML事件类型和元素深度](#解析xml事件类型和元素深度)三类操作。如在Web服务中，XML是SOAP（Simple Object Access Protocol）协议的基础，SOAP消息通常以XML格式封装，包含请求和响应参数，通过解析这些XML消息，Web服务可以处理来自客户端的请求并生成相应的响应。


XML模块提供XmlPullParser类对XML文件解析，输入为含有XML文本的ArrayBuffer或DataView，输出为解析得到的信息。


  **表1** XML解析选项，其详细介绍请参见[ParseOptions](../reference/apis-arkts/js-apis-xml.md#parseoptions)。

| 名称 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| supportDoctype | boolean | 否 | 是否解析文档类型，false表示不解析文档类型，true表示解析文档类型，默认false。 |
| ignoreNameSpace | boolean | 否 | 是否忽略命名空间，忽略命名空间后，将不会对其进行解析。true表示忽略命名空间，false表示不忽略命名空间，默认false。|
| tagValueCallbackFunction | (name: string, value: string) =&gt; boolean | 否 | 获取tagValue回调函数，打印标签及标签值。默认为null，表示不进行XML标签和标签值的解析。 |
| attributeValueCallbackFunction | (name: string, value: string) =&gt; boolean | 否 | 获取attributeValue回调函数，打印属性及属性值。默认为null，表示不进行XML属性和属性值的解析。 |
| tokenValueCallbackFunction | (eventType: EventType, value: ParseInfo) =&gt; boolean | 否 | 获取tokenValue回调函数，打印标签事件类型及parseInfo对应属性。默认为null，表示不进行XML事件类型解析。 |


## 注意事项

- XML解析及转换需要确保传入的XML数据符合标准格式。

- XML解析目前不支持按指定节点解析对应的节点值。


## 解析XML标签和标签值

1. 引入模块。

    ```ts
    import { xml, util } from '@kit.ArkTS'; // 需要使用util模块函数对文件编码
    ```

2. 对XML文件编码后调用XmlPullParser。

   可以基于ArrayBuffer构造XmlPullParser对象，也可以基于DataView构造XmlPullParser对象（两种构造方式返回结果无区别可任选一种）。

    ```ts
    let strXml: string =
    '<?xml version="1.0" encoding="utf-8"?>' +
      '<note importance="high" logged="true">' +
      '<title>Play</title>' +
      '<lens>Work</lens>' +
      '</note>';
    let textEncoder: util.TextEncoder = new util.TextEncoder();
    let arrBuffer: Uint8Array = textEncoder.encodeInto(strXml); // 对数据编码，防止包含中文字符乱码
    // 方式1：基于ArrayBuffer构造XmlPullParser对象
    let that: xml.XmlPullParser = new xml.XmlPullParser(arrBuffer.buffer as object as ArrayBuffer, 'UTF-8');
   
    // 方式2：基于DataView构造XmlPullParser对象
    // let dataView: DataView = new DataView(arrBuffer.buffer as object as ArrayBuffer);
    // let that: xml.XmlPullParser = new xml.XmlPullParser(dataView, 'UTF-8');
    ```

3. 自定义回调函数，本例直接打印出标签及标签值。

    ```ts
    function func(name: string, value: string): boolean {
      if (name == 'note') {
        console.info(name);
      }
      if (value == 'Play' || value == 'Work') {
        console.info('    ' + value);
      }
      if (name == 'title' || name == 'lens') {
        console.info('  ' + name);
      }
      return true; //true:继续解析 false:停止解析
    }
    ```

4. 设置解析选项，调用parse函数。

    ```ts
    let options: xml.ParseOptions = {supportDoctype:true, ignoreNameSpace:true, tagValueCallbackFunction:func};
    that.parse(options);
    ```

	输出结果如下所示：

	```
	note
	  title
	    Play
	  title
	  lens
	    Work
	  lens
	note
	```




## 解析XML属性和属性值

1. 引入模块。

    ```ts
    import { xml, util } from '@kit.ArkTS'; // 需要使用util模块函数对文件编码
    ```

2. 对XML文件编码后调用XmlPullParser。

    ```ts
    let strXml: string =
      '<?xml version="1.0" encoding="utf-8"?>' +
        '<note importance="high" logged="true">' +
        '    <title>Play</title>' +
        '    <title>Happy</title>' +
        '    <lens>Work</lens>' +
        '</note>';
    let textEncoder: util.TextEncoder = new util.TextEncoder();
    let arrBuffer: Uint8Array = textEncoder.encodeInto(strXml); // 对数据编码，防止包含中文字符乱码
    let that: xml.XmlPullParser = new xml.XmlPullParser(arrBuffer.buffer as object as ArrayBuffer, 'UTF-8');
    ```

3. 自定义回调函数，本例直接打印出属性及属性值。

    ```ts
    let str: string = '';
    function func(name: string, value: string): boolean {
      str += name + ' ' + value + ' ';
      return true; // true:继续解析 false:停止解析
    }
    ```

4. 设置解析选项，调用parse函数。

    ```ts
    let options: xml.ParseOptions = {supportDoctype:true, ignoreNameSpace:true, attributeValueCallbackFunction:func};
    that.parse(options);
    console.info(str); // 一次打印出所有的属性及其值
    ```

   输出结果如下所示：
   ```
   importance high logged true // note节点的属性及属性值
   ```


## 解析XML事件类型和元素深度

1. 引入模块。

    ```ts
    import { xml, util } from '@kit.ArkTS'; // 需要使用util模块函数对文件编码
    ```

2. 对XML文件编码后调用XmlPullParser。

    ```ts
    let strXml: string =
      '<?xml version="1.0" encoding="utf-8"?>' +
      '<note importance="high" logged="true">' +
      '<title>Play</title>' +
      '</note>';
    let textEncoder: util.TextEncoder = new util.TextEncoder();
    let arrBuffer: Uint8Array = textEncoder.encodeInto(strXml); // 对数据编码，防止包含中文字符乱码
    let that: xml.XmlPullParser = new xml.XmlPullParser(arrBuffer.buffer as object as ArrayBuffer, 'UTF-8');
    ```

3. 自定义回调函数，本例直接打印元素事件类型及元素深度。

    ```ts
    let str: string  = '';
    function func(name: xml.EventType, value: xml.ParseInfo): boolean {
      str = name + ' ' + value.getDepth(); // getDepth 获取元素的当前深度
      console.info(str)
      return true; //true:继续解析 false:停止解析
    }
    ```

4. 设置解析选项，调用parse函数。

     ```ts
     let options: xml.ParseOptions = {supportDoctype:true, ignoreNameSpace:true, tokenValueCallbackFunction:func};
     that.parse(options);
     ```

   输出结果如下所示：

	```
	 0 0 // 0：<?xml version="1.0" encoding="utf-8"?> 对应事件类型		START_DOCUMENT值为0  0：起始深度为0
	 2 1 // 2：<note importance="high" logged="true"> 对应事件类型START_TAG值为2       1：深度为1
	 2 2 // 2：<title>对应事件类型START_TAG值为2                                       2：深度为2
	 4 2 // 4：Play对应事件类型TEXT值为4                                               2：深度为2
	 3 2 // 3：</title>对应事件类型END_TAG值为3                                        2：深度为2
	 3 1 // 3：</note>对应事件类型END_TAG值为3                                         1：深度为1（与<note对应>）
	 1 0 // 1：对应事件类型END_DOCUMENT值为1                                           0：深度为0
	```




## 场景示例

此处以调用所有解析选项为例，提供解析XML标签、属性和事件类型的开发示例。


```ts
import { xml, util } from '@kit.ArkTS';

let strXml: string =
  '<?xml version="1.0" encoding="UTF-8"?>' +
    '<book category="COOKING">' +
    '<title lang="en">Everyday</title>' +
    '<author>Giana</author>' +
    '</book>';
let textEncoder: util.TextEncoder = new util.TextEncoder();
let arrBuffer: Uint8Array = textEncoder.encodeInto(strXml);
let that: xml.XmlPullParser = new xml.XmlPullParser(arrBuffer.buffer as object as ArrayBuffer, 'UTF-8');
let str: string = '';

function tagFunc(name: string, value: string): boolean {
  str = name + value;
  console.info('tag-' + str);
  return true;
}

function attFunc(name: string, value: string): boolean {
  str = name + ' ' + value;
  console.info('attri-' + str);
  return true;
}

function tokenFunc(name: xml.EventType, value: xml.ParseInfo): boolean {
  str = name + ' ' + value.getDepth();
  console.info('token-' + str);
  return true;
}

let options: xml.ParseOptions = {
  supportDoctype: true,
  ignoreNameSpace: true,
  tagValueCallbackFunction: tagFunc,
  attributeValueCallbackFunction: attFunc,
  tokenValueCallbackFunction: tokenFunc
};
that.parse(options);
```

输出结果如下所示：

   ```
   tag-
   token-0 0
   tag-book
   attri-category COOKING
   token-2 1
   tag-title
   attri-lang en
   token-2 2
   tag-Everyday
   token-4 2
   tag-title
   token-3 2
   tag-author
   token-2 2
   tag-Giana
   token-4 2
   tag-author
   token-3 2
   tag-book
   token-3 1
   tag-
   token-1 0
   ```
