# @ohos.inputMethod (输入法框架) (系统接口)

本模块主要面向普通前台应用（备忘录、信息、设置等系统应用与三方应用），提供对输入法（输入法应用）的控制、管理能力，包括显示/隐藏输入法软键盘、切换输入法、获取所有输入法列表等等。

> **说明：**
>
> 本模块首批接口从API version 6开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```ts
import inputMethod from '@ohos.inputMethod';
```

## inputMethod.switchInputMethod<sup>11+</sup>
switchInputMethod(bundleName: string, subtypeId?: string): Promise&lt;void&gt;

切换输入法，使用promise异步回调。

**需要权限：** ohos.permission.CONNECT_IME_ABILITY

**系统能力：** SystemCapability.MiscServices.InputMethodFramework

**系统接口：** 此接口为系统接口。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  |bundleName |  string| 是 | 目标输入法包名。 |
  |subtypeId |  string| 否 | 输入法子类型。 |

**返回值：**

  | 类型           | 说明                     |
  | -------------- | ----------------------- |
  | Promise\<void> | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[输入法框架错误码](errorcode-inputmethod-framework.md)。

| 错误码ID | 错误信息                             |
| -------- | -------------------------------------- |
| 12800005 | configuration persisting error.        |
| 12800008 | input method manager service error. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let currentIme = inputMethod.getCurrentInputMethod();
try {
  inputMethod.switchInputMethod(currentIme.name).then(() => {
    console.log('Succeeded in switching inputmethod.');
  }).catch((err: BusinessError) => {
    console.error(`Failed to switchInputMethod: ${JSON.stringify(err)}`);
  })
} catch (err) {
  console.error(`Failed to switchInputMethod: ${JSON.stringify(err)}`);
}
let currentImeSubType = inputMethod.getCurrentInputMethodSubtype();
try {
  inputMethod.switchInputMethod(currentIme.name, currentImeSubType.id).then(() => {
    console.log('Succeeded in switching inputmethod.');
  }).catch((err: BusinessError) => {
    console.error(`Failed to switchInputMethod: ${JSON.stringify(err)}`);
  })
} catch (err) {
  console.error(`Failed to switchInputMethod: ${JSON.stringify(err)}`);
}
```

## InputMethodSetting<sup>8+</sup>

下列API均需使用[getSetting](./js-apis-inputmethod.md#inputmethodgetsetting9)获取到InputMethodSetting实例后，通过实例调用。

### on('imeShow')<sup>10+</sup>

on(type: 'imeShow', callback: (info: Array\<InputWindowInfo>) => void): void

订阅输入法[Panel](js-apis-inputmethodengine.md#panel10)固定态软键盘显示事件。使用callback异步回调。

**系统接口**：此接口为系统接口。

**系统能力：** SystemCapability.MiscServices.InputMethodFramework

**参数：**

| 参数名   | 类型 | 必填 | 说明 |
| -------- | ---- | ---- | ---- |
| type     | string | 是 | 设置监听类型，固定取值为'imeShow'。 |
| callback | (info: Array<[InputWindowInfo](js-apis-inputmethod.md#inputwindowinfo10)>) => void | 是 | 回调函数，返回输入法固定态软键盘信息。 |

**示例：**

```ts
try {
  inputMethodSetting.on('imeShow', (info: Array<inputMethod.InputWindowInfo>) => {
    console.info('Succeeded in subscribing imeShow event.');
  });
} catch(err) {
  console.error(`Failed to unsubscribing imeShow. err: ${JSON.stringify(err)}`);
}
```

### on('imeHide')<sup>10+</sup>

on(type: 'imeHide', callback: (info: Array\<InputWindowInfo>) => void): void

订阅输入法[Panel](js-apis-inputmethodengine.md#panel10)固定态软键盘隐藏事件。使用callback异步回调。

**系统接口**：此接口为系统接口。

**系统能力：** SystemCapability.MiscServices.InputMethodFramework

**参数：**

| 参数名   | 类型 | 必填 | 说明 |
| -------- | ---- | ---- | ---- |
| type     | string | 是 | 设置监听类型，固定取值为'imeHide'。 |
| callback | (info: Array<[InputWindowInfo](js-apis-inputmethod.md#inputwindowinfo10)>) => void | 是 | 回调函数，返回输入法固定态软键盘信息。 |

**示例：**

```ts
try {
  inputMethodSetting.on('imeHide', (info: Array<inputMethod.InputWindowInfo>) => {
    console.info('Succeeded in subscribing imeHide event.');
  });
} catch(err) {
  console.error(`Failed to unsubscribing imeHide. err: ${JSON.stringify(err)}`);
}
```

### off('imeShow')<sup>10+</sup>

off(type: 'imeShow', callback?: (info: Array\<InputWindowInfo>) => void): void

取消订阅输入法[Panel](js-apis-inputmethodengine.md#panel10)固定态软键盘显示事件。

**系统接口**：此接口为系统接口。

**系统能力：** SystemCapability.MiscServices.InputMethodFramework

**参数：**

| 参数名   | 类型 | 必填 | 说明   |
| -------- | ---- | ---- | ------ |
| type     | string | 是 | 设置监听类型，固定取值`imeShow`。 |
| callback | (info: Array<[InputWindowInfo](js-apis-inputmethod.md#inputwindowinfo10)>) => void  | 否 | 取消订阅的回调函数。<br>参数不填写时，取消订阅type对应的所有回调事件。 |

**示例：**

```ts
try {
  inputMethodSetting.off('imeShow');
} catch(err) {
  console.error(`Failed to unsubscribing imeShow. err: ${JSON.stringify(err)}`);
}
```

### off('imeHide')<sup>10+</sup>

off(type: 'imeHide', callback?: (info: Array\<InputWindowInfo>) => void): void

取消订阅输入法[Panel](js-apis-inputmethodengine.md#panel10)固定态软键盘隐藏事件。

**系统接口**：此接口为系统接口。

**系统能力：** SystemCapability.MiscServices.InputMethodFramework

**参数：**

| 参数名   | 类型 | 必填 | 说明   |
| -------- | ---- | ---- | ------ |
| type     | string | 是 | 设置监听类型，固定取值'imeHide'。 |
| callback | (info: Array<[InputWindowInfo](js-apis-inputmethod.md#inputwindowinfo10)>) => void  | 否 | 取消订阅的回调函数。<br>参数不填写时，取消订阅type对应的所有回调事件。 |

**示例：**

```ts
try {
  inputMethodSetting.off('imeHide');
} catch(err) {
  console.error(`Failed to unsubscribing imeHide. err: ${JSON.stringify(err)}`);
}
```

### isPanelShown<sup>11+</sup>

isPanelShown(panelInfo: PanelInfo): boolean

查询指定类型的输入法面板是否处于显示状态。

**系统接口**：此接口为系统接口。

**系统能力：** SystemCapability.MiscServices.InputMethodFramework

**参数：**

| 参数名    | 类型                                                  | 必填 | 说明               |
| --------- | ----------------------------------------------------- | ---- | ------------------ |
| panelInfo | [PanelInfo](./js-apis-inputmethod-panel.md#panelinfo) | 是   | 输入法面板的属性。 |

**返回值：**

| 类型    | 说明                                                         |
| ------- | ------------------------------------------------------------ |
| boolean | 面板显隐状态查询结果。<br/>- true表示被查询的输入法面板处于显示状态。<br/>- false表示被查询的输入法面板处于隐藏状态。 |

**错误码：**

以下错误码的详细介绍请参见[输入法框架错误码](errorcode-inputmethod-framework.md)。

| 错误码ID | 错误信息                            |
| -------- | ----------------------------------- |
| 12800008 | input method manager service error. |

**示例：**

```ts
import { PanelInfo, PanelType, PanelFlag } from '@ohos.inputMethod.Panel';

let info: PanelInfo = {
  type: PanelType.SOFT_KEYBOARD,
  flag: PanelFlag.FLAG_FIXED
}
try {
  let result = inputMethodSetting.isPanelShown(info);
  console.log('Succeeded in querying isPanelShown, result: ' + result);
} catch (err) {
  console.error(`Failed to query isPanelShown: ${JSON.stringify(err)}`);
}
```
