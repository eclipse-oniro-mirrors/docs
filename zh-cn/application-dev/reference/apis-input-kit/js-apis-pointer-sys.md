# @ohos.multimodalInput.pointer (鼠标指针)(系统接口)

鼠标指针管理模块，用于查询和设置鼠标指针相关属性。

> **说明**：
>
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>
> 当前页面仅包含本模块的系统接口，其他公开接口参见[@ohos.multimodalInput.pointer (鼠标指针)](js-apis-pointer.md)。

## 导入模块

```js
import pointer from '@ohos.multimodalInput.pointer';
```

## pointer.setPointerSpeed

setPointerSpeed(speed: number, callback: AsyncCallback&lt;void&gt;): void

设置鼠标移动速度，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                        | 必填   | 说明                                    |
| -------- | ------------------------- | ---- | ------------------------------------- |
| speed    | number                    | 是    | 鼠标移动速度，范围1-11，默认为7。   |
| callback | AsyncCallback&lt;void&gt; | 是    | 回调函数。 |

**示例**：

```js
try {
  pointer.setPointerSpeed(5, (error: Error) => {
    if (error) {
      console.log(`Set pointer speed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Set pointer speed success`);
  });
} catch (error) {
  console.log(`Set pointer speed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setPointerSpeed

setPointerSpeed(speed: number): Promise&lt;void&gt;

设置鼠标移动速度，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名    | 类型     | 必填   | 说明                                  |
| ----- | ------ | ---- | ----------------------------------- |
| speed | number | 是    | 鼠标移动速度，范围1-11，默认为7。 |

**返回值**：

| 参数                  | 说明               |
| ------------------- | ---------------- |
| Promise&lt;void&gt; | Promise对象。 |

**示例**：

```js
try {
  pointer.setPointerSpeed(5).then(() => {
    console.log(`Set pointer speed success`);
  });
} catch (error) {
  console.log(`Set pointer speed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setPointerSpeedSync<sup>10+</sup>

setPointerSpeedSync(speed: number): void

使用同步方式设置鼠标移动速度。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名    | 类型     | 必填   | 说明                                  |
| ----- | ------ | ---- | ----------------------------------- |
| speed | number | 是    | 鼠标移动速度，范围1-11，默认为7。 |

**示例**：

```js
try {
  let speed = pointer.setPointerSpeedSync(5);
  console.log(`Set pointer speed success`);
} catch (error) {
  console.log(`Set pointer speed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getPointerSpeed

getPointerSpeed(callback: AsyncCallback&lt;number&gt;): void

获取鼠标移动速度，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                          | 必填   | 说明             |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback&lt;number&gt; | 是    | 回调函数，异步返回鼠标移动速度。 |

**示例**：

```js
try {
  pointer.getPointerSpeed((error: Error, speed: number) => {
    if (error) {
      console.log(`Get pointer speed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Get pointer speed success, speed: ${JSON.stringify(speed)}`);
  });
} catch (error) {
  console.log(`Get pointer speed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getPointerSpeed

getPointerSpeed(): Promise&lt;number&gt;

获取当前鼠标移动速度，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**返回值**：

| 参数                    | 说明                  |
| --------------------- | ------------------- |
| Promise&lt;number&gt; | Promise实例，异步返回鼠标移动速度。 |

**示例**：

```js
try {
  pointer.getPointerSpeed().then(speed => {
    console.log(`Get pointer speed success, speed: ${JSON.stringify(speed)}`);
  });
} catch (error) {
  console.log(`Get pointer speed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getPointerSpeedSync<sup>10+</sup>

getPointerSpeedSync(): number

使用同步方式获取当前鼠标移动速度。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**返回值**：

| 参数                    | 说明                  |
| --------------------- | ------------------- |
| number | 返回鼠标移动速度。 |

**示例**：

```js
try {
  let speed = pointer.getPointerSpeedSync();
  console.log(`Get pointer speed success, speed: ${JSON.stringify(speed)}`);
} catch (error) {
  console.log(`Get pointer speed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setHoverScrollState<sup>10+</sup>

setHoverScrollState(state: boolean, callback: AsyncCallback&lt;void&gt;): void

设置鼠标悬停滚动开关状态，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                        | 必填   | 说明                                    |
| -------- | ------------------------- | ---- | ------------------------------------- |
| state    | boolean                    | 是    | 鼠标悬停滚动开关状态。true代表开关开启，false代表开关关闭，默认开启。   |
| callback | AsyncCallback&lt;void&gt; | 是    | 回调函数。 |

**示例**：

```js
try {
  pointer.setHoverScrollState(true, (error: Error) => {
    if (error) {
      console.log(`Set the mouse hover scroll failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Set the mouse hover scroll success`);
  });
} catch (error) {
  console.log(`Set the mouse hover scroll failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setHoverScrollState<sup>10+</sup>

setHoverScrollState(state: boolean): Promise&lt;void&gt;

设置鼠标悬停滚动开关状态，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名    | 类型     | 必填   | 说明                                  |
| ----- | ------ | ---- | ----------------------------------- |
| state | boolean | 是    | 鼠标悬停滚动开关状态。true代表开关开启，false代表开关关闭，默认开启。 |

**返回值**：

| 参数                  | 说明               |
| ------------------- | ---------------- |
| Promise&lt;void&gt; | Promise对象。 |

**示例**：

```js
try {
  pointer.setHoverScrollState(true).then(() => {
    console.log(`Set the mouse hover scroll success`);
  });
} catch (error) {
  console.log(`Set the mouse hover scroll failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getHoverScrollState<sup>10+</sup>

getHoverScrollState(callback: AsyncCallback&lt;boolean&gt;): void

获取鼠标悬停滚动开关状态，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                          | 必填   | 说明             |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback&lt;boolean&gt; | 是    | 回调函数，异步返回鼠标悬停滚动开关状态。true代表开关开启，false代表开关关闭，默认开启。 |

**示例**：

```js
try {
  pointer.getHoverScrollState((error: Error, state: boolean) => {
    console.log(`Get the mouse hover scroll success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`Get the mouse hover scroll failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getHoverScrollState<sup>10+</sup>

getHoverScrollState(): Promise&lt;boolean&gt;

获取当前鼠标悬停滚动开关状态，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**返回值**：

| 参数                    | 说明                  |
| --------------------- | ------------------- |
| Promise&lt;boolean&gt; | Promise实例，异步返回鼠标悬停滚动开关状态。true代表开关开启，false代表开关关闭，默认开启。 |

**示例**：

```js
try {
  pointer.getHoverScrollState().then((state: boolean) => {
    console.log(`Get the mouse hover scroll success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`Get the mouse hover scroll failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setMousePrimaryButton<sup>10+</sup>

setMousePrimaryButton(primary: PrimaryButton, callback: AsyncCallback&lt;void&gt;): void

设置鼠标主键，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名    | 类型                      | 必填  | 说明                                    |
| -------- | ------------------------- | ----  | ------------------------------------- |
| primary  | [PrimaryButton](js-apis-pointer.md#primarybutton10)   | 是    | 鼠标主键id。   |
| callback | AsyncCallback&lt;void&gt; | 是    | 回调函数。 |

**示例**：

```js
try {
  pointer.setMousePrimaryButton(pointer.PrimaryButton.RIGHT, (error: Error) => {
    if (error) {
      console.log(`Set mouse primary button failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Set mouse primary button success`);
  });
} catch (error) {
  console.log(`Set mouse primary button failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setMousePrimaryButton<sup>10+</sup>

setMousePrimaryButton(primary: PrimaryButton): Promise&lt;void&gt;

设置鼠标主键，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名    | 类型     | 必填   | 说明                                  |
| ----- | ------ | ---- | ----------------------------------- |
| primary | [PrimaryButton](js-apis-pointer.md#primarybutton10) | 是    | 鼠标主键id。 |

**返回值**：

| 参数                  | 说明               |
| ------------------- | ---------------- |
| Promise&lt;void&gt; | Promise对象。 |

**示例**：

```js
try {
  pointer.setMousePrimaryButton(pointer.PrimaryButton.RIGHT).then(() => {
    console.log(`Set mouse primary button success`);
  });
} catch (error) {
  console.log(`Set mouse primary button failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getMousePrimaryButton<sup>10+</sup>

getMousePrimaryButton(callback: AsyncCallback&lt;PrimaryButton&gt;): void

获取当前鼠标主键，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                          | 必填   | 说明             |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback&lt;[PrimaryButton](js-apis-pointer.md#primarybutton10)&gt; | 是    | 回调函数，异步返回鼠标主键。 |

**示例**：

```js
try {
  pointer.getMousePrimaryButton((error: Error, primary: pointer.PrimaryButton) => {
    console.log(`Get mouse primary button success, primary: ${JSON.stringify(primary)}`);
  });
} catch (error) {
  console.log(`Get mouse primary button failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getMousePrimaryButton<sup>10+</sup> 

getMousePrimaryButton(): Promise&lt;PrimaryButton&gt;

获取当前鼠标主键，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**返回值**：

| 参数                    | 说明                  |
| --------------------- | ------------------- |
| Promise&lt;[PrimaryButton](js-apis-pointer.md#primarybutton10)&gt; | Promise实例，异步返回鼠标主键。 |

**示例**：

```js
try {
  pointer.getMousePrimaryButton().then((primary: pointer.PrimaryButton) => {
    console.log(`Get mouse primary button success, primary: ${JSON.stringify(primary)}`);
  });
} catch (error) {
  console.log(`Get mouse primary button failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setMouseScrollRows<sup>10+</sup>

setMouseScrollRows(rows: number, callback: AsyncCallback&lt;void&gt;): void

设置鼠标滚动行数，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                        | 必填   | 说明                                    |
| -------- | ------------------------- | ---- | ------------------------------------- |
| rows     | number                    | 是    | 鼠标滚动行数，范围1-100，默认为3。   |
| callback | AsyncCallback&lt;void&gt; | 是    | 回调函数。 |

**示例**：

```js
try {
  pointer.setMouseScrollRows(1, (error: Error) => {
    if (error) {
      console.log(`setMouseScrollRows failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`setMouseScrollRows success`);
  });
} catch (error) {
  console.log(`setMouseScrollRows failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setMouseScrollRows<sup>10+</sup>

setMouseScrollRows(rows: number): Promise&lt;void&gt;

设置鼠标滚动行数，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名    | 类型     | 必填   | 说明                                  |
| ----- | ------ | ---- | ----------------------------------- |
| rows  | number | 是    | 鼠标滚动行数，范围1-100，默认为3。 |

**返回值**：

| 参数                  | 说明               |
| ------------------- | ---------------- |
| Promise&lt;void&gt; | Promise对象。 |

**示例**：

```js
try {
  pointer.setMouseScrollRows(20).then(() => {
    console.log(`setMouseScrollRows success`);
  });
} catch (error) {
  console.log(`setMouseScrollRows failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getMouseScrollRows<sup>10+</sup>

getMouseScrollRows(callback: AsyncCallback&lt;number&gt;): void

获取鼠标滚动行数，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                          | 必填   | 说明             |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback&lt;number&gt; | 是    | 回调函数，异步返回鼠标滚动行数。 |

**示例**：

```js
try {
  pointer.getMouseScrollRows((error: Error, rows: number) => {
    console.log(`getMouseScrollRows success, rows: ${JSON.stringify(rows)}`);
  });
} catch (error) {
  console.log(`getMouseScrollRows failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getMouseScrollRows<sup>10+</sup>

getMouseScrollRows(): Promise&lt;number&gt;

获取当前鼠标滚动行数，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**返回值**：

| 参数                    | 说明                  |
| --------------------- | ------------------- |
| Promise&lt;number&gt; | Promise实例，异步返回鼠标滚动行数。 |

**示例**：

```js
try {
  pointer.getMouseScrollRows().then((rows: number) => {
    console.log(`getMouseScrollRows success, rows: ${JSON.stringify(rows)}`);
  });
} catch (error) {
  console.log(`getMouseScrollRows failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadScrollSwitch<sup>10+</sup>

setTouchpadScrollSwitch(state: boolean, callback: AsyncCallback\<void>): void

设置触控板滚轴开关，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                        | 必填   | 说明                                    |
| -------- | ------------------------- | ---- | ------------------------------------- |
| state | boolean | 是    | 滚轴开关开启的状态，true代表开启，false代表关闭，默认为开启   |
| callback | AsyncCallback\<void> | 是    | 回调函数。 |

**示例**：

```js
try {
  pointer.setTouchpadScrollSwitch(true, (error: Error) => {
    if (error) {
      console.log(`setTouchpadScrollSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`setTouchpadScrollSwitch success`);
  });
} catch (error) {
  console.log(`setTouchpadScrollSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadScrollSwitch<sup>10+</sup>

setTouchpadScrollSwitch(state: boolean): Promise\<void>

设置触控板滚轴开关，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名    | 类型     | 必填   | 说明                                  |
| ----- | ------ | ---- | ----------------------------------- |
| state | boolean| 是    |  滚轴开关开启的状态，true代表开启，false代表关闭，默认为开启 |

**返回值**：

| 参数                  | 说明               |
| ------------------- | ---------------- |
| Promise\<void> | Promise对象。 |

**示例**：

```js
try {
  pointer.setTouchpadScrollSwitch(false).then(() => {
    console.log(`setTouchpadScrollSwitch success`);
  });
} catch (error) {
  console.log(`setTouchpadScrollSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadScrollSwitch<sup>10+</sup>

getTouchpadScrollSwitch(callback:  AsyncCallback\<boolean>): void

获取触控板滚轴能力开启状态，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                          | 必填   | 说明             |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback\<boolean> | 是    | 回调函数，异步返回触控板滚轴能力开启状态。true代表开启，false代表关闭，默认为开启。 |

**示例**：

```js
try {
  pointer.getTouchpadScrollSwitch((error: Error, state: boolean) => {
    console.log(`getTouchpadScrollSwitch success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadScrollSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadScrollSwitch<sup>10+</sup>

getTouchpadScrollSwitch(): Promise\<boolean>

获取触控板滚轴能力开启状态，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**返回值**：

| 参数                    | 说明                  |
| --------------------- | ------------------- |
| Promise\<boolean> | Promise实例，异步返回触控板滚轴能力开启状态。true代表开启，false代表关闭，默认为开启。 |

**示例**：

```js
try {
  pointer.getTouchpadScrollSwitch().then((state) => {
    console.log(`getTouchpadScrollSwitch success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadScrollSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadScrollDirection<sup>10+</sup>

setTouchpadScrollDirection(state: boolean, callback: AsyncCallback\<void>): void

设置触控板滚轴的方向，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                        | 必填   | 说明                                    |
| -------- | ------------------------- | ---- | ------------------------------------- |
| state | boolean | 是    | state为触控板滚轴的方向。<br>true与手指滑动的方向一致，false与手指滑动的方向相反，<br>默认为true。   |
| callback | AsyncCallback\<void> | 是    | 回调函数。 |

**示例**：

```js
try {
  pointer.setTouchpadScrollDirection(true, (error: Error) => {
    if (error) {
      console.log(`setTouchpadScrollDirection failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`setTouchpadScrollDirection success`);
  });
} catch (error) {
  console.log(`setTouchpadScrollDirection failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadScrollDirection<sup>10+</sup>

setTouchpadScrollDirection(state: boolean): Promise\<void>

设置触控板滚轴的方向，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名    | 类型     | 必填   | 说明                                  |
| ----- | ------ | ---- | ----------------------------------- |
| state | boolean| 是    |  state为触控板滚轴的方向。<br>true与手指滑动的方向一致，false与手指滑动的方向相反。<br>默认为true|

**返回值**：

| 参数                  | 说明               |
| ------------------- | ---------------- |
| Promise\<void> | Promise对象。 |

**示例**：

```js
try {
  pointer.setTouchpadScrollDirection (false).then(() => {
    console.log(`setTouchpadScrollDirection success`);
  });
} catch (error) {
  console.log(`setTouchpadScrollDirection failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadScrollDirection<sup>10+</sup>

getTouchpadScrollDirection(callback:  AsyncCallback\<boolean>): void

获取触控板滚轴方向，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                          | 必填   | 说明             |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback\<boolean> | 是    | 回调函数，异步返回触控板滚轴方向。<br>true与手指滑动的方向一致，false与手指滑动的方向相反。<br>默认为true |

**示例**：

```js
try {
  pointer.getTouchpadScrollDirection ((error: Error, state: boolean) => {
    console.log(`getTouchpadScrollDirection success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadScrollDirection failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadScrollDirection<sup>10+</sup>

getTouchpadScrollDirection(): Promise\<boolean>

获取触控板滚轴方向，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**返回值**：

| 参数                    | 说明                  |
| --------------------- | ------------------- |
| Promise\<boolean> | Promise实例，异步返回触控板滚轴方向。<br>true与手指滑动的方向一致，false与手指滑动的方向相反。<br>默认为true |

**示例**：

```js
try {
  pointer.getTouchpadScrollDirection().then((state: boolean) => {
    console.log(`getTouchpadScrollDirection success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadScrollDirection failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadTapSwitch<sup>10+</sup>

setTouchpadTapSwitch(state: boolean, callback: AsyncCallback\<void>): void

设置触控板轻触功能开关，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                        | 必填   | 说明                                    |
| -------- | ------------------------- | ---- | ------------------------------------- |
| state | boolean | 是    |触控板轻触功能开关开启状态。 true代表轻触开启，false代表轻触关闭，默认开启。   |
| callback | AsyncCallback\<void> | 是    | 回调函数。 |

**示例**：

```js
try {
  pointer.setTouchpadTapSwitch(true, (error: Error) => {
    if (error) {
      console.log(`setTouchpadTapSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`setTouchpadTapSwitch success`);
  });
} catch (error) {
  console.log(`setTouchpadTapSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadTapSwitch <sup>10+</sup>

setTouchpadTapSwitch(state: boolean): Promise\<void>

设置触控板轻触功能开关，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名    | 类型     | 必填   | 说明                                  |
| ----- | ------ | ---- | ----------------------------------- |
| state | boolean| 是    |  触控板轻触功能开关开启状态， true代表轻触开启，false代表轻触关闭，默认开启。  |

**返回值**：

| 参数                  | 说明               |
| ------------------- | ---------------- |
| Promise\<void> | Promise对象。 |

**示例**：

```js
try {
  pointer.setTouchpadTapSwitch(false).then(() => {
    console.log(`setTouchpadTapSwitch success`);
  });
} catch (error) {
  console.log(`setTouchpadTapSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadTapSwitch<sup>10+</sup>

getTouchpadTapSwitch(callback:  AsyncCallback\<boolean>): void

获取触控板轻触能力开启状态，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                          | 必填   | 说明             |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback\<boolean> | 是    | 回调函数，异步返回触控板轻触功能开启状态， true代表开启，false代表关闭，默认开启。 |

**示例**：

```js
try {
  pointer.getTouchpadTapSwitch((error: Error, state: boolean) => {
    console.log(`getTouchpadTapSwitch success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadTapSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadTapSwitch<sup>10+</sup>

getTouchpadTapSwitch(): Promise\<boolean>

获取触控板轻触功能开启状态，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**返回值**：

| 参数                    | 说明                  |
| --------------------- | ------------------- |
| Promise\<boolean> | Promise实例，异步返回触控板轻触功能开启状态，true代表开启，false代表关闭，默认开启。 |

**示例**：

```js
try {
  pointer.getTouchpadTapSwitch().then((state: boolean) => {
    console.log(`getTouchpadTapSwitch success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadTapSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadPointerSpeed<sup>10+</sup>

setTouchpadPointerSpeed(speed: number, callback: AsyncCallback\<void>): void

设置触控板光标移动速度，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                        | 必填   | 说明                                    |
| -------- | ------------------------- | ---- | ------------------------------------- |
| speed | number                    | 是    |speed代表光标移动速度。speed取值范围[1,11]，默认6。  |
| callback | AsyncCallback\<void> | 是    | 回调函数。 |

**示例**：

```js
try {
  pointer.setTouchpadPointerSpeed(1, (error: Error) => {
    if (error) {
      console.log(`setTouchpadPointerSpeedfailed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`setTouchpadPointerSpeed success`);
  });
} catch (error) {
  console.log(`setTouchpadPointerSpeed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadPointerSpeed<sup>10+</sup>

setTouchpadPointerSpeed(speed: number): Promise\<void>

设置触控板光标移动速度，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名    | 类型     | 必填   | 说明                                  |
| ----- | ------ | ---- | ----------------------------------- |
| speed| number | 是    | speed代表光标移动速度。speed取值范围[1,11]，默认6。    |

**返回值**：

| 参数                  | 说明               |
| ------------------- | ---------------- |
| Promise\<void> | Promise对象。 |

**示例**：

```js
try {
  pointer.setTouchpadPointerSpeed(10).then(() => {
    console.log(`setTouchpadPointerSpeed success`);
  });
} catch (error) {
  console.log(`setTouchpadPointerSpeed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadPointerSpeed<sup>10+</sup>

getTouchpadPointerSpeed(callback: AsyncCallback\<number>): void

获取触控板光标移动速度，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                          | 必填   | 说明             |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback\<number> | 是    | 回调函数，异步返回触控板光标移动速度。 |

**示例**：

```js
try {
  pointer.getTouchpadPointerSpeed((error: Error, speed: number) => {
    console.log(`getTouchpadPointerSpeed success, speed: ${JSON.stringify(speed)}`);
  });
} catch (error) {
  console.log(`getTouchpadPointerSpeed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadPointerSpeed<sup>10+</sup>

getTouchpadPointerSpeed(): Promise\<number>

获取触控板光标移动速度，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**返回值**：

| 参数                    | 说明                  |
| --------------------- | ------------------- |
| Promise\<number> | Promise实例，异步返回触控板光标移动速度。 |

**示例**：

```js
try {
  pointer.getTouchpadPointerSpeed().then((speed: number) => {
    console.log(`getTouchpadPointerSpeed success, speed: ${JSON.stringify(speed)}`);
  });
} catch (error) {
  console.log(`getTouchpadPointerSpeed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadPinchSwitch<sup>10+</sup>

setTouchpadPinchSwitch(state: boolean, callback: AsyncCallback\<void>): void

设置触控板双指捏合功能开关，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                        | 必填   | 说明                                    |
| -------- | ------------------------- | ---- | ------------------------------------- |
| state | boolean | 是    |触控板双指捏合功能开关开启状态。 true代表开启，false代表关闭，默认开启。   |
| callback | AsyncCallback\<void> | 是    | 回调函数。 |

**示例**：

```js
try {
  pointer.setTouchpadTapSwitch(true, (error: Error) => {
    if (error) {
      console.log(`setTouchpadPinchSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`setTouchpadPinchSwitch success`);
  });
} catch (error) {
  console.log(`setTouchpadPinchSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadPinchSwitch<sup>10+</sup>

setTouchpadPinchSwitch(state: boolean): Promise\<void>

设置触控板双指捏合功能开关，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名    | 类型     | 必填   | 说明                                  |
| ----- | ------ | ---- | ----------------------------------- |
| state | boolean| 是    |  触控板双指捏合功能开关开启状态。 true代表开启，false代表关闭，默认开启。  |

**返回值**：

| 参数                  | 说明               |
| ------------------- | ---------------- |
| Promise\<void> | Promise对象。 |

**示例**：

```js
try {
  pointer.setTouchpadPinchSwitch(false).then(() => {
    console.log(`setTouchpadPinchSwitch success`);
  });
} catch (error) {
  console.log(`setTouchpadPinchSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadPinchSwitch<sup>10+</sup>

getTouchpadPinchSwitch(callback:  AsyncCallback\<boolean>): void

获取触控板双指捏合功能开启状态，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                          | 必填   | 说明             |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback\<boolean> | 是    | 回调函数，异步返回触控板双指捏合功能开启状态。true代表功能开启，false代表功能关闭，默认开启。 |

**示例**：

```js
try {
  pointer.getTouchpadPinchSwitch((error: Error, state: boolean) => {
    console.log(`getTouchpadPinchSwitch success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadPinchSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadPinchSwitch<sup>10+</sup>

getTouchpadPinchSwitch(): Promise\<boolean>

获取触控板双指捏合功能开启状态，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**返回值**：

| 参数                    | 说明                  |
| --------------------- | ------------------- |
| Promise\<boolean> | Promise实例，异步返回触控板双指捏合功能开启状态。true代表功能开启，false代表功能关闭，默认开启。 |

**示例**：

```js
try {
  pointer.getTouchpadPinchSwitch().then((state: boolean) => {
    console.log(`getTouchpadPinchSwitch success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadPinchSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadSwipeSwitch<sup>10+</sup>

setTouchpadSwipeSwitch(state: boolean, callback: AsyncCallback\<void>): void

设置触控板多指滑动功能开关，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                        | 必填   | 说明                                    |
| -------- | ------------------------- | ---- | ------------------------------------- |
| state | boolean | 是    |触控板多指滑动开关开启状态。 true代表多指滑动开启，false代表多指滑动关闭，默认开启。   |
| callback | AsyncCallback\<void> | 是    | 回调函数。 |

**示例**：

```js
try {
  pointer.setTouchpadSwipeSwitch(true, (error: Error) => {
    if (error) {
      console.log(`setTouchpadSwipeSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`setTouchpadSwipeSwitch success`);
  });
} catch (error) {
  console.log(`setTouchpadSwipeSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadSwipeSwitch<sup>10+</sup>

setTouchpadSwipeSwitch(state: boolean): Promise\<void>

设置触控板多指滑动功能开关，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名    | 类型     | 必填   | 说明                                  |
| ----- | ------ | ---- | ----------------------------------- |
| state | boolean| 是    |  触控板多指滑动功能开关开启状态。 true代表多指滑动开启，false代表多指滑动关闭，默认开启。  |

**返回值**：

| 参数                  | 说明               |
| ------------------- | ---------------- |
| Promise\<void> | Promise对象。 |

**示例**：

```js
try {
  pointer.setTouchpadSwipeSwitch(false).then(() => {
    console.log(`setTouchpadSwipeSwitch success`);
  });
} catch (error) {
  console.log(`setTouchpadSwipeSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadSwipeSwitch<sup>10+</sup>

getTouchpadSwipeSwitch(callback:  AsyncCallback\<boolean>): void

获取触控板多指滑动功能开启状态，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                          | 必填   | 说明             |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback\<boolean> | 是    | 回调函数，异步返回触控板多指滑动功能开启状态。 true代表多指滑动开启，false代表多指滑动关闭，默认开启。 |

**示例**：

```js
try {
  pointer.getTouchpadSwipeSwitch((error: Error, state: boolean) => {
    console.log(`getTouchpadSwipeSwitch success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadSwipeSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadSwipeSwitch<sup>10+</sup>

getTouchpadSwipeSwitch(): Promise\<boolean>

获取触控板多指滑动功能开启状态，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**返回值**：

| 参数                    | 说明                  |
| --------------------- | ------------------- |
| Promise\<boolean> | Promise实例，异步返回触控板多指滑动功能开启状态。 true代表多指滑动开启，false代表多指滑动关闭，默认开启。 |

**示例**：

```js
try {
  pointer.getTouchpadSwipeSwitch().then((state: boolean) => {
    console.log(`getTouchpadSwipeSwitch success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadSwipeSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadRightClickType<sup>10+</sup>

setTouchpadRightClickType(type: RightClickType, callback: AsyncCallback\<void>): void

设置触控板右键菜单类型，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                        | 必填   | 说明                                    |
| -------- | ------------------------- | ---- | ------------------------------------- |
| type| [RightClickType](js-apis-pointer.md#rightclicktype10)| 是    |type代表触控板右键菜单类型。<br>- TOUCHPAD_RIGHT_BUTTON：触控板右键区域。<br>- TOUCHPAD_LEFT_BUTTON：触控板左键区域。<br>- TOUCHPAD_TWO_FINGER_TAP：双指轻击或按压触控板。<br>默认为TOUCHPAD_RIGHT_BUTTON 。  |
| callback | AsyncCallback\<void> | 是    | 回调函数。 |

**示例**：

```js
try {
  pointer.setTouchpadRightClickType(pointer.RightClickType.TOUCHPAD_RIGHT_BUTTON , (error: Error) => {
    if (error) {
      console.log(`setTouchpadRightClickType, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`setTouchpadRightClickType success`);
  });
} catch (error) {
  console.log(`setTouchpadRightClickType failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadRightClickType<sup>10+</sup>

setTouchpadRightClickType(type: RightClickType): Promise\<void>

设置触控板右键菜单类型，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名    | 类型     | 必填   | 说明                                  |
| ----- | ------ | ---- | ----------------------------------- |
| type| [RightClickType](js-apis-pointer.md#rightclicktype10)| 是    | type代表触控板右键菜单类型。<br>- TOUCHPAD_RIGHT_BUTTON：触控板右键区域。<br>- TOUCHPAD_LEFT_BUTTON：触控板左键区域。<br>- TOUCHPAD_TWO_FINGER_TAP：双指轻击或按压触控板。<br>默认为TOUCHPAD_RIGHT_BUTTON 。 |

**返回值**：

| 参数                  | 说明               |
| ------------------- | ---------------- |
| Promise\<void> | Promise对象。 |

**示例**：

```js
try {
  pointer.setTouchpadRightClickType(pointer.RightClickType.TOUCHPAD_RIGHT_BUTTON).then(() => {
    console.log(`setTouchpadRightClickType success`);
  });
} catch (error) {
  console.log(`setTouchpadRightClickType failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadRightClickType<sup>10+</sup>

getTouchpadRightClickType(callback: AsyncCallback\<RightClickType>): void

获取触控板右键菜单类型，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                          | 必填   | 说明             |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback\<[RightClickType](js-apis-pointer.md#rightclicktype10)> | 是    | 回调函数，异步返回触控板右键菜单类型。 |

**示例**：

```js
try {
  pointer.getTouchpadRightClickType((error: Error, type: pointer.RightClickType) => {
    console.log(`getTouchpadRightClickType success, type: ${JSON.stringify(type)}`);
  });
} catch (error) {
  console.log(`getTouchpadRightClickType failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadRightClickType<sup>10+</sup>

getTouchpadRightClickType(): Promise\<RightClickType>

获取触控板右键菜单类型，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**返回值**：

| 参数                    | 说明                  |
| --------------------- | ------------------- |
| Promise\<[RightClickType](js-apis-pointer.md#rightclicktype10) > | Promise实例，异步返回触控板右键菜单类型。 |

**示例**：

```js
try {
  pointer.getTouchpadRightClickType().then((type: pointer.RightClickType) => {
    console.log(`getTouchpadRightClickType success, typeed: ${JSON.stringify(type)}`);
  });
} catch (error) {
  console.log(`getTouchpadRightClickType failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setPointerSize<sup>10+</sup>

setPointerSize(size: number, callback: AsyncCallback&lt;void&gt;): void

设置鼠标光标大小，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                        | 必填   | 说明                                    |
| -------- | ------------------------- | ---- | ------------------------------------- |
| size     | number                    | 是    | 鼠标光标大小，范围为[1-7]，默认为1。   |
| callback | AsyncCallback&lt;void&gt; | 是    | 回调函数，当设置成功时，err为undefined，否则为错误对象。 |

**示例**：

```js
try {
  pointer.setPointerSize(1, (error: Error) => {
    if (error) {
      console.log(`setPointerSize failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`setPointerSize success`);
  });
} catch (error) {
  console.log(`setPointerSize failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setPointerSize<sup>10+</sup>

setPointerSize(size: number): Promise&lt;void&gt;

设置鼠标光标大小，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名    | 类型     | 必填   | 说明                                  |
| ----- | ------ | ---- | ----------------------------------- |
| size  | number | 是    | 鼠标光标大小，范围为[1-7]，默认为1。 |

**返回值**：

| 参数                  | 说明               |
| ------------------- | ---------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例**：

```js
try {
  pointer.setPointerSize(3).then(() => {
    console.log(`setPointerSize success`);
  });
} catch (error) {
  console.log(`setPointerSize failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setPointerSizeSync<sup>10+</sup>

setPointerSizeSync(size: number): void;

设置鼠标光标大小，使用同步方式进行设置。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名    | 类型     | 必填   | 说明                                  |
| ----- | ------ | ---- | ----------------------------------- |
| size  | number | 是    | 鼠标光标大小，范围为[1-7]，默认为1。 |

**示例**：

```js
try {
  pointer.setPointerSizeSync(5);
  console.log(`setPointerSizeSync success`);
} catch (error) {
  console.log(`setPointerSizeSync failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getPointerSize<sup>10+</sup>

getPointerSize(callback: AsyncCallback&lt;number&gt;): void

获取鼠标光标大小，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                          | 必填   | 说明             |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback&lt;number&gt; | 是    | 回调函数，异步返回鼠标光标大小。 |

**示例**：

```js
try {
  pointer.getPointerSize((error: Error, size: number) => {
    console.log(`getPointerSize success, size: ${JSON.stringify(size)}`);
  });
} catch (error) {
  console.log(`getPointerSize failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getPointerSize<sup>10+</sup>

getPointerSize(): Promise&lt;number&gt;

获取当前鼠标光标大小，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**返回值**：

| 参数                    | 说明                  |
| --------------------- | ------------------- |
| Promise&lt;number&gt; | Promise对象，异步返回鼠标光标大小。 |

**示例**：

```js
try {
  pointer.getPointerSize().then((size: number) => {
    console.log(`getPointerSize success, size: ${JSON.stringify(size)}`);
  });
} catch (error) {
  console.log(`getPointerSize failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getPointerSizeSync<sup>10+</sup>

getPointerSizeSync(): number

获取鼠标光标大小，使用同步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**返回值**：

| 参数                    | 说明                  |
| --------------------- | ------------------- |
| number | 鼠标光标大小。 |

**示例**：

```js
try {
  let pointerSize = pointer.getPointerSizeSync();
  console.log(`getPointerSizeSync success, pointerSize: ${JSON.stringify(pointerSize)}`);
} catch (error) {
  console.log(`getPointerSizeSync failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setPointerColor<sup>10+</sup>

setPointerColor(color: number, callback: AsyncCallback&lt;void&gt;): void

设置鼠标光标颜色，使用AsyncCallback异步方式返回结果。

**说明**
>
> 设置和调试时，需连接外部设备，如鼠标、蓝牙等。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                        | 必填   | 说明                                    |
| -------- | ------------------------- | ---- | ------------------------------------- |
| color     | number                    | 是    | 鼠标光标颜色，默认为黑色：0x000000。   |
| callback | AsyncCallback&lt;void&gt; | 是    | 回调函数，当设置成功时，err为undefined，否则为错误对象。 |

**示例**：

```js
try {
  pointer.setPointerColor(0xF6C800, (error: Error) => {
    if (error) {
      console.log(`setPointerColor failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`setPointerColor success`);
  });
} catch (error) {
  console.log(`setPointerColor failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setPointerColor<sup>10+</sup>

setPointerColor(color: number): Promise&lt;void&gt;

设置鼠标光标颜色，使用Promise异步方式返回结果。

**说明**
>
> 设置和调试时，需连接外部设备，如鼠标、蓝牙等。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名    | 类型     | 必填   | 说明                                  |
| ----- | ------ | ---- | ----------------------------------- |
| color  | number | 是    | 鼠标光标颜色，默认为黑色：0x000000。 |

**返回值**：

| 参数                  | 说明               |
| ------------------- | ---------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例**：

```js
try {
  pointer.setPointerColor(0xF6C800).then(() => {
    console.log(`setPointerColor success`);
  });
} catch (error) {
  console.log(`setPointerColor failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setPointerColorSync<sup>10+</sup>

setPointerColorSync(color: number): void;

设置鼠标光标颜色，使用同步方式进行设置。

**说明**
>
> 设置和调试时，需连接外部设备，如鼠标、蓝牙等。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名    | 类型     | 必填   | 说明                                  |
| ----- | ------ | ---- | ----------------------------------- |
| color  | number | 是    | 鼠标光标颜色，默认为黑色：0x000000。 |

**示例**：

```js
try {
  pointer.setPointerColorSync(0xF6C800);
  console.log(`setPointerColorSync success`);
} catch (error) {
  console.log(`setPointerColorSync failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getPointerColor<sup>10+</sup>

getPointerColor(callback: AsyncCallback&lt;number&gt;): void

获取鼠标光标颜色，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**参数**：

| 参数名       | 类型                          | 必填   | 说明             |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback&lt;number&gt; | 是    | 回调函数，异步返回鼠标光标颜色。 |

**示例**：

```js
try {
  pointer.getPointerColor((error: Error, color: number) => {
    console.log(`getPointerColor success, color: ${JSON.stringify(color)}`);
  });
} catch (error) {
  console.log(`getPointerColor failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getPointerColor<sup>10+</sup>

getPointerColor(): Promise&lt;number&gt;

获取当前鼠标光标颜色，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**返回值**：

| 参数                    | 说明                  |
| --------------------- | ------------------- |
| Promise&lt;number&gt; | Promise对象，异步返回鼠标光标颜色。 |

**示例**：

```js
try {
  pointer.getPointerColor().then((color: number) => {
    console.log(`getPointerColor success, color: ${JSON.stringify(color)}`);
  });
} catch (error) {
  console.log(`getPointerColor failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getPointerColorSync<sup>10+</sup>

getPointerColorSync(): number

获取鼠标光标颜色，使用同步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.Pointer

**系统API**: 此接口为系统接口。

**返回值**：

| 参数                    | 说明                  |
| --------------------- | ------------------- |
| number | 鼠标光标颜色。 |

**示例**：

```js
try {
  let pointerColor = pointer.getPointerColorSync();
  console.log(`getPointerColorSync success, pointerColor: ${JSON.stringify(pointerColor)}`);
} catch (error) {
  console.log(`getPointerColorSync failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```