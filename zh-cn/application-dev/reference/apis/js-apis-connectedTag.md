# @ohos.connectedTag (有源标签)

本模块提供有源标签的使用，包括初始化有源标签芯片、读取有源标签内容、写入内容到有源标签等。

> **说明：**
>
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```js
import connectedTag from '@ohos.connectedTag';
```

## connectedTag.init

init(): boolean

初始化有源标签芯片。

**需要权限**：ohos.permission.NFC_TAG

**系统能力**：SystemCapability.Communication.ConnectedTag

**返回值：**

| **类型** | **说明** |
| -------- | -------- |
| boolean | true:初始化成功，&nbsp;false:初始化失败。 |

## connectedTag.initialize<sup>9+</sup>

initialize(): void

初始化有源标签芯片。

**需要权限：** ohos.permission.NFC_TAG

**系统能力：** SystemCapability.Communication.ConnectedTag

**错误码：**
以下错误码的详细介绍请参见[NFC错误码](../errorcodes/errorcode-nfc.md)。

| 错误码ID | 错误信息|
| -------- | -------- |
| 3200101 | Connected NFC tag running state is abnormal in service. |

## connectedTag.uninit

uninit(): boolean

卸载有源标签芯片资源。

**需要权限**：ohos.permission.NFC_TAG

**系统能力**：SystemCapability.Communication.ConnectedTag

**返回值：**

| **类型** | **说明** |
| -------- | -------- |
| boolean | true:卸载操作成功，&nbsp;false:卸载操作失败。 |

## connectedTag.uninitialize<sup>9+</sup>

uninitialize(): void

卸载有源标签芯片资源。

**需要权限:** ohos.permission.NFC_TAG

**系统能力:** SystemCapability.Communication.ConnectedTag

**错误码：**
以下错误码的详细介绍请参见[NFC错误码](../errorcodes/errorcode-nfc.md)。

| 错误码ID | 错误信息|
| -------- | -------- |
| 3200101 | Connected NFC tag running state is abnormal in service. |

## connectedTag.readNdefTag

readNdefTag(): Promise&lt;string&gt;

读取有源标签内容，使用promise方式作为异步方法。

**需要权限**：ohos.permission.NFC_TAG

**系统能力**：SystemCapability.Communication.ConnectedTag

**返回值：**

| **类型** | **说明** |
| -------- | -------- |
| Promise&lt;string&gt; | 返回读取有源标签内容。 |

**示例：**

```js
import connectedTag from '@ohos.connectedTag';

connectedTag.readNdefTag().then((data) => {
    console.log("connectedTag readNdefTag Promise data = " + data);
}).catch((err)=> {
    console.log("connectedTag readNdefTag Promise err: " + err);
});
```

## connectedTag.read<sup>9+</sup>

read(): Promise&lt;number[]&gt;

读取有源标签内容，使用promise方式作为异步方法。

**需要权限：** ohos.permission.NFC_TAG

**系统能力：** SystemCapability.Communication.ConnectedTag

**返回值：**

| **类型** | **说明** |
| -------- | -------- |
| Promise&lt;number[]&gt; | 返回读取有源标签内容。 |

**错误码：**
以下错误码的详细介绍请参见[NFC错误码](../errorcodes/errorcode-nfc.md)。

| 错误码ID | 错误信息|
| -------- | -------- |
| 3200101 | Connected NFC tag running state is abnormal in service. |

**示例：**

```js
import connectedTag from '@ohos.connectedTag';

connectedTag.read().then((data) => {
    console.log("connectedTag read Promise data = " + data);
}).catch((err)=> {
    console.log("connectedTag read Promise err: " + err);
});
```

## connectedTag.readNdefTag

readNdefTag(callback: AsyncCallback&lt;string&gt;): void

读取有源标签内容，使用AsyncCallback方式作为异步方法。

**需要权限**：ohos.permission.NFC_TAG

**系统能力**：SystemCapability.Communication.ConnectedTag

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;string&gt; | 是 | 读取有源标签内容回调函数。 |

**示例：**

```js
import connectedTag from '@ohos.connectedTag';

connectedTag.readNdefTag((err, data)=> {
    if (err) {
        console.log("connectedTag readNdefTag AsyncCallback err: " + err);
    } else {
        console.log("connectedTag readNdefTag AsyncCallback data: " + data);
    }
});
```

## connectedTag.read<sup>9+</sup>

read(callback: AsyncCallback&lt;number[]&gt;): void

读取有源标签内容，使用AsyncCallback方式作为异步方法。

**需要权限：** ohos.permission.NFC_TAG

**系统能力：** SystemCapability.Communication.ConnectedTag

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;number[]&gt; | 是 | 读取有源标签内容回调函数。 |

**错误码：**
以下错误码的详细介绍请参见[NFC错误码](../errorcodes/errorcode-nfc.md)。

| 错误码ID | 错误信息|
| -------- | -------- |
| 3200101 | Connected NFC tag running state is abnormal in service. |

**示例：**

```js
import connectedTag from '@ohos.connectedTag';

connectedTag.read((err, data)=> {
    if (err) {
        console.log("connectedTag read AsyncCallback err: " + err);
    } else {
        console.log("connectedTag read AsyncCallback data: " + data);
    }
});
```

## connectedTag.writeNdefTag

writeNdefTag(data: string): Promise&lt;void&gt;

写入内容到有源标签，使用promise方式作为异步方法。

**需要权限**：ohos.permission.NFC_TAG

**系统能力**：SystemCapability.Communication.ConnectedTag

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| data | string | 是 | 有源标签内容, 长度最大是1024个字节。 |

**返回值：**

| **类型** | **说明** |
| -------- | -------- |
| Promise&lt;void&gt; | 无返回值。 |

**示例：**

```js
import connectedTag from '@ohos.connectedTag';

var rawData = "010203"; // change it tobe correct.
connectedTag.writeNdefTag(rawData).then(() => {
    console.log("connectedTag writeNdefTag Promise success.");
}).catch((err)=> {
    console.log("connectedTag writeNdefTag Promise err: " + err);
});
```

## connectedTag.write<sup>9+</sup>

write(data: number[]): Promise&lt;void&gt;

写入内容到有源标签，使用promise方式作为异步方法。

**需要权限：** ohos.permission.NFC_TAG

**系统能力：** SystemCapability.Communication.ConnectedTag

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| data | number[] | 是 | 有源标签内容, 由十六进制数字组成，范围从0x00至0xFF。 |

**返回值：**

| **类型** | **说明** |
| -------- | -------- |
| Promise&lt;void&gt; | 无返回值。 |

**错误码：**
以下错误码的详细介绍请参见[NFC错误码](../errorcodes/errorcode-nfc.md)。

| 错误码ID | 错误信息|
| -------- | -------- |
| 3200101 | Connected NFC tag running state is abnormal in service. |

**示例：**

```js
import connectedTag from '@ohos.connectedTag';

var rawData = [0x01, 0x02, 0x03]; // change it tobe correct.
connectedTag.write(rawData).then(() => {
    console.log("connectedTag write NdefTag Promise success.");
}).catch((err)=> {
    console.log("connectedTag write NdefTag Promise err: " + err);
});
```

## connectedTag.writeNdefTag

writeNdefTag(data: string, callback: AsyncCallback&lt;void&gt;): void

写入内容到有源标签，使用AsyncCallback方式作为异步方法。

**需要权限**：ohos.permission.NFC_TAG

**系统能力**：SystemCapability.Communication.ConnectedTag

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| data | string | 是 | 有源标签内容, 长度最大是1024个字节。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 读取有源标签内容回调函数。 |

**示例：**

```js
import connectedTag from '@ohos.connectedTag';

var rawData = "010203"; // change it tobe correct.
connectedTag.writeNdefTag(rawData, (err)=> {
    if (err) {
        console.log("connectedTag writeNdefTag AsyncCallback err: " + err);
    } else {
        console.log("connectedTag writeNdefTag AsyncCallback success.");
    }
});
```

## connectedTag.write<sup>9+</sup>

write(data: number[], callback: AsyncCallback&lt;void&gt;): void

写入内容到有源标签，使用AsyncCallback方式作为异步方法。

**需要权限：** ohos.permission.NFC_TAG

**系统能力：** SystemCapability.Communication.ConnectedTag

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| data | number[] | 是 | 有源标签内容, 由十六进制数字组成，范围从0x00至0xFF。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 读取有源标签内容回调函数。 |

**错误码：**
以下错误码的详细介绍请参见[NFC错误码](../errorcodes/errorcode-nfc.md)。

| 错误码ID | 错误信息|
| -------- | -------- |
| 3200101 | Connected NFC tag running state is abnormal in service. |

**示例：**

```js
import connectedTag from '@ohos.connectedTag';

var rawData = [0x01, 0x02, 0x03]; // change it tobe correct.
connectedTag.write(rawData, (err)=> {
    if (err) {
        console.log("connectedTag write NdefTag AsyncCallback err: " + err);
    } else {
        console.log("connectedTag write NdefTag AsyncCallback success.");
    }
});
```

## connectedTag.on('notify')

on(type: "notify", callback: Callback&lt;number&gt;): void

注册NFC场强状态事件。

**需要权限**：ohos.permission.NFC_TAG

**系统能力**：SystemCapability.Communication.ConnectedTag

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"notify"字符串 |
| callback | Callback&lt;number&gt; | 是 | 状态改变回调函数，返回值参见[NfcRfType](#nfcrftype)。 |

## connectedTag.off('notify')

off(type: "notify", callback?: Callback&lt;number&gt;): void

取消NFC场强状态事件的注册。

**需要权限**：ohos.permission.NFC_TAG

**系统能力**：SystemCapability.Communication.ConnectedTag

**参数：**

| **参数名** | **类型** | **必填** | **说明** |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 固定填"notify"字符串 |
| callback | Callback&lt;number&gt; | 否 | 状态改变回调函数。如果callback不填，将“去注册”该事件关联的所有回调函数。|

**示例：**

```js
import connectedTag from '@ohos.connectedTag';

// Register event
connectedTag.on("notify", (err, rfState)=> {
    if (err) {
        console.log("connectedTag on Callback err: " + err);
    } else {
        console.log("connectedTag on Callback rfState: " + rfState);
    }
});

var initStatus = connectedTag.init();
console.log("connectedTag init status: " + initStatus);

// Add nfc connecected tag business oprations here...
// connectedTag.writeNdefTag(rawData)
// connectedTag.readNdefTag()

var uninitStatus = connectedTag.uninit();
console.log("connectedTag uninit status: " + uninitStatus);

// Unregister event
connectedTag.off("notify", (err, rfState)=> {
    if (err) {
        console.log("connectedTag off Callback err: " + err);
    } else {
        console.log("connectedTag off Callback rfState: " + rfState);
    }
});
```

## NfcRfType

表示NFC场强状态的枚举。

**系统能力**：SystemCapability.Communication.ConnectedTag

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| NFC_RF_LEAVE | 0 | NFC离场事件 |
| NFC_RF_ENTER | 1 | NFC进场事件 |
