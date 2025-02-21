# @ohos.multimodalInput.inputDevice (输入设备)(系统接口)


输入设备管理模块，用于监听输入设备连接和断开状态，查询输入设备相关信息。


> **说明**：
>
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>
> 当前页面仅包含模块的系统接口，其他公开接口请参考[@ohos.multimodalInput.inputDevice (输入设备)](js-apis-inputdevice.md)。


## 导入模块

```js
import inputDevice from '@ohos.multimodalInput.inputDevice';
```

## inputDevice.setKeyboardRepeatDelay<sup>10+</sup>

setKeyboardRepeatDelay(delay: number, callback: AsyncCallback&lt;void&gt;): void

设置键盘按键的重复时延，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**系统API**：此接口为系统接口。

**参数**：

| 参数名     | 类型   | 必填 | 说明                                                         |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| delay    | number                    | 是    | 键盘按键重复延迟时间，默认值500ms，调节范围[300ms，1000ms]。 |
| callback | AsyncCallback&lt;void&gt; | 是    | 回调函数。 |

**示例**：

```js
try {
  inputDevice.setKeyboardRepeatDelay(350, (error: Error) => {
    if (error) {
      console.log(`Set keyboard repeat delay failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Set keyboard repeat delay success`);
  });
} catch (error) {
  console.log(`Set keyboard repeat delay failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.setKeyboardRepeatDelay<sup>10+</sup>

setKeyboardRepeatDelay(delay: number): Promise&lt;void&gt;

设置键盘按键的重复时延，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**系统API**：此接口为系统接口。

**参数**：

| 参数名    | 类型     | 必填   | 说明                                  |
| ----- | ------ | ---- | ----------------------------------- |
| delay | number | 是    | 键盘按键重复延迟时间，默认值500ms，调节范围[300ms，1000ms]。 |

**返回值**：

| 参数                  | 说明               |
| ------------------- | ---------------- |
| Promise&lt;void&gt; | Promise对象。 |

**示例**：

```js
try {
  inputDevice.setKeyboardRepeatDelay(350).then(() => {
    console.log(`Set keyboard repeat delay success`);
  });
} catch (error) {
  console.log(`Set keyboard repeat delay failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.getKeyboardRepeatDelay<sup>10+</sup>

getKeyboardRepeatDelay(callback: AsyncCallback&lt;number&gt;): void

获取键盘按键的重复时延，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**系统API**：此接口为系统接口。

**参数**：

| 参数名     | 类型   | 必填 | 说明                                                         |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| callback   | AsyncCallback&lt;number&gt;                    | 是    | 回调函数，异步返回键盘按键重复延迟时间。 |

**示例**：

```js
try {
  inputDevice.getKeyboardRepeatDelay((error: Error, delay: Number) => {
    if (error) {
      console.log(`Get keyboard repeat delay failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Get keyboard repeat delay success`);
  });
} catch (error) {
  console.log(`Get keyboard repeat delay failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.getKeyboardRepeatDelay<sup>10+</sup>

getKeyboardRepeatDelay(): Promise&lt;number&gt;

获取键盘按键的重复时延，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**系统API**：此接口为系统接口。

**返回值**：

| 参数                    | 说明                  |
| --------------------- | ------------------- |
| Promise&lt;number&gt; | Promise实例，异步返回键盘按键的重复时延。 |

**示例**：

```js
try {
  inputDevice.getKeyboardRepeatDelay().then((delay: Number) => {
    console.log(`Get keyboard repeat delay success`);
  });
} catch (error) {
  console.log(`Get keyboard repeat delay failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.setKeyboardRepeatRate<sup>10+</sup>

setKeyboardRepeatRate(rate: number, callback: AsyncCallback&lt;void&gt;): void

设置键盘按键的重复速率，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**系统API**：此接口为系统接口。

**参数**：

| 参数名     | 类型   | 必填 | 说明                                                         |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| rate    | number                    | 是    | 键盘按键重复速率，默认值50ms/次，调节范围[36ms/次，100ms/次]。 |
| callback | AsyncCallback&lt;void&gt; | 是    | 回调函数。 |

**示例**：

```js
try {
  inputDevice.setKeyboardRepeatRate(60, (error: Error) => {
    if (error) {
      console.log(`Set keyboard repeat rate failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Set keyboard repeat rate success`);
  });
} catch (error) {
  console.log(`Set keyboard repeat rate failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.setKeyboardRepeatRate<sup>10+</sup>

setKeyboardRepeatRate(rate: number): Promise&lt;void&gt;

设置键盘按键的重复速率，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**系统API**：此接口为系统接口。

**参数**：

| 参数名    | 类型     | 必填   | 说明                                  |
| ----- | ------ | ---- | ----------------------------------- |
| rate | number | 是    | 键盘按键重复速率，默认值50ms/次，调节范围[36ms/次，100ms/次]。 |

**返回值**：

| 参数                  | 说明               |
| ------------------- | ---------------- |
| Promise&lt;void&gt; | Promise对象。 |

**示例**：

```js
try {
  inputDevice.setKeyboardRepeatRate(60).then(() => {
    console.log(`Set keyboard repeat rate success`);
  });
} catch (error) {
  console.log(`Set keyboard repeat rate failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.getKeyboardRepeatRate<sup>10+</sup>

getKeyboardRepeatRate(callback: AsyncCallback&lt;number&gt;): void

获取键盘按键的重复速率，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**系统API**：此接口为系统接口。

**参数**：

| 参数名       | 类型                          | 必填   | 说明             |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback&lt;number&gt; | 是    | 回调函数，异步返回键盘按键的重复速率。 |

**示例**：

```js
try {
  inputDevice.getKeyboardRepeatRate((error: Error, rate: Number) => {
    if (error) {
      console.log(`Get keyboard repeat rate failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Get keyboard repeat rate success`);
  });
} catch (error) {
  console.log(`Get keyboard repeat rate failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.getKeyboardRepeatRate<sup>10+</sup>

getKeyboardRepeatRate(): Promise&lt;number&gt;

获取键盘按键的重复速率，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**系统API**：此接口为系统接口。

**返回值**：

| 参数                    | 说明                  |
| --------------------- | ------------------- |
| Promise&lt;number&gt; | Promise实例，异步返回键盘按键的重复速率。 |

**示例**：

```js
try {
  inputDevice.getKeyboardRepeatRate().then((rate: Number) => {
    console.log(`Get keyboard repeat rate success`);
  });
} catch (error) {
  console.log(`Get keyboard repeat rate failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```