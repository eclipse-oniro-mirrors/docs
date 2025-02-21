# CommonEventSubscriber

描述公共事件的订阅者。

> **说明：**
>
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 使用说明

在使用CommonEventSubscriber的功能前，需要通过CommonEvent.createSubscriber获取subscriber对象。

```ts
import CommonEvent from '@ohos.commonEvent';
import CommonEventManager from '@ohos.commonEventManager';
import Base from '@ohos.base';
let subscriber:CommonEventManager.CommonEventSubscriber; // 用于保存创建成功的订阅者对象，后续使用其完成订阅及退订的动作

// 订阅者信息
let subscribeInfo:CommonEventManager.CommonEventSubscribeInfo = {
	events: ["event"]
};

// 创建订阅者回调
function createCB(err:Base.BusinessError, commonEventSubscriber:CommonEventManager.CommonEventSubscriber) {
    if (err.code !== undefined && err.code != null) {
        console.error(`createSubscriber failed, code is ${err.code}`);
    } else {
        console.info("createSubscriber success");
        subscriber = commonEventSubscriber;
    }
}

// 创建订阅者
CommonEvent.createSubscriber(subscribeInfo, createCB);
```

## getCode

getCode(callback: AsyncCallback\<number>): void

获取有序公共事件代码。使用callback异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                   | 必填 | 说明               |
| -------- | ---------------------- | ---- | ------------------ |
| callback | AsyncCallback\<number\> | 是   | 公共事件代码。 |

**示例：**

```ts
//获取有序公共事件代码回调
function getCodeCallback(err:Base.BusinessError, code:number) {
    if (err.code !== undefined && err.code != null) {
        console.error(`getCode failed, code is ${err.code}, message is ${err.message}`);
    } else {
        console.info("getCode " + JSON.stringify(code));
    }
}
subscriber.getCode(getCodeCallback);
```

## getCode

getCode(): Promise\<number>

获取有序公共事件代码。使用Promise异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型             | 说明                 |
| ---------------- | -------------------- |
| Promise\<number> | 公共事件代码。 |

**示例：**

```ts
subscriber.getCode().then((code:number) => {
    console.info("getCode " + JSON.stringify(code));
}).catch((err:Base.BusinessError) => {
    console.error(`getCode failed, code is ${err.code}, message is ${err.message}`);
});
```

## getCodeSync<sup>10+</sup>

getCodeSync(): number

获取有序公共事件代码。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型             | 说明                 |
| ---------------- | -------------------- |
| number | 公共事件代码。 |

**示例：**

```ts
let code = subscriber.getCodeSync();
console.info("getCodeSync " + JSON.stringify(code));
```

## setCode

setCode(code: number, callback: AsyncCallback\<void>): void

设置有序公共事件的代码。使用callback异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                 | 必填 | 说明                   |
| -------- | -------------------- | ---- | ---------------------- |
| code     | number               | 是   | 公共事件的代码。   |
| callback | AsyncCallback\<void> | 是   | 表示被指定的回调方法。 |

**示例：**

```ts
//设置有序公共事件的代码回调
function setCodeCallback(err:Base.BusinessError) {
    if (err.code !== undefined && err.code != null) {
        console.error(`setCode failed, code is ${err.code}, message is ${err.message}`);
    } else {
        console.info("setCode success");
    }
}
subscriber.setCode(1, setCodeCallback);
```

## setCode

setCode(code: number): Promise\<void>

设置有序公共事件的代码。使用Promise异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名 | 类型   | 必填 | 说明               |
| ------ | ------ | ---- | ------------------ |
| code   | number | 是   | 公共事件的代码。 |

**返回值：**

| 类型             | 说明                 |
| ---------------- | -------------------- |
| Promise\<void>   | 返回一个Promise的结果。 |

**示例：**

```ts
subscriber.setCode(1).then(() => {
    console.info("setCode success");
}).catch((err:Base.BusinessError) => {
    console.error(`setCode failed, code is ${err.code}, message is ${err.message}`);
});
```

## setCodeSync<sup>10+</sup>

setCodeSync(code: number): void

设置有序公共事件的代码。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名 | 类型   | 必填 | 说明               |
| ------ | ------ | ---- | ------------------ |
| code   | number | 是   | 公共事件的代码。 |


**示例：**

```ts

try {
    subscriber.setCodeSync(1);
} catch (error) {
    let err:Base.BusinessError = error as Base.BusinessError;
    console.error(`setCodeSync failed, code is ${err.code}, message is ${err.message}`);
}
```

## getData

getData(callback: AsyncCallback\<string>): void

获取有序公共事件的数据。使用callback异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                   | 必填 | 说明                 |
| -------- | ---------------------- | ---- | -------------------- |
| callback | AsyncCallback\<string> | 是   | 公共事件的数据。 |

**示例：**

```ts
//获取有序公共事件代码数据回调
function getDataCallback(err:Base.BusinessError, data:string) {
    if (err.code !== undefined && err.code != null) {
        console.error(`getData failed, code is ${err.code}, message is ${err.message}`);
    } else {
        console.info("getData " + JSON.stringify(data));
    }
}
subscriber.getData(getDataCallback);
```

## getData

getData(): Promise\<string>

获取有序公共事件的数据。使用Promise异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型             | 说明               |
| ---------------- | ------------------ |
| Promise\<string> | 公共事件的数据。 |

**示例：**

```ts
subscriber.getData().then((data:string) => {
    console.info("getData " + JSON.stringify(data));
}).catch((err:Base.BusinessError) => {
    console.error(`getData failed, code is ${err.code}, message is ${err.message}`);
});
```

## getDataSync<sup>10+</sup>

getDataSync(): string

获取有序公共事件的数据。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型             | 说明               |
| ---------------- | ------------------ |
| string | 公共事件的数据。 |

**示例：**

```ts
let data = subscriber.getDataSync();
console.info("getDataSync " + JSON.stringify(data));
```

## setData

setData(data: string, callback: AsyncCallback\<void>): void

设置有序公共事件的数据。使用callback异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                 | 必填 | 说明                 |
| -------- | -------------------- | ---- | -------------------- |
| data     | string               | 是   | 公共事件的数据。   |
| callback | AsyncCallback\<void> | 是   | 表示被指定的回调方法。 |

**示例：**

```ts
//设置有序公共事件的结果数据回调
function setDataCallback(err:Base.BusinessError) {
    if (err.code !== undefined && err.code != null) {
        console.error(`setData failed, code is ${err.code}, message is ${err.message}`);
    } else {
        console.info("setData success");
    }
}
subscriber.setData("publish_data_changed", setDataCallback);
```

## setData

setData(data: string): Promise\<void>

设置有序公共事件的数据。使用Promise异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名 | 类型   | 必填 | 说明                 |
| ------ | ------ | ---- | -------------------- |
| data   | string | 是   | 公共事件的数据。 |

**返回值：**

| 类型             | 说明                 |
| ---------------- | -------------------- |
| Promise\<void>   | 返回一个Promise的结果。 |

**示例：**

```ts
subscriber.setData("publish_data_changed").then(() => {
    console.info("setData success");
}).catch((err:Base.BusinessError) => {
    console.error(`setData failed, code is ${err.code}, message is ${err.message}`);
});
```

## setDataSync<sup>10+</sup>

setDataSync(data: string): void

设置有序公共事件的数据。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名 | 类型   | 必填 | 说明                 |
| ------ | ------ | ---- | -------------------- |
| data   | string | 是   | 公共事件的数据。 |

**示例：**

```ts
try {
    subscriber.setDataSync("publish_data_changed");
} catch (error) {
    let err:Base.BusinessError = error as Base.BusinessError;
    console.error(`setDataSync failed, code is ${err.code}, message is ${err.message}`);
}
```

## setCodeAndData

setCodeAndData(code: number, data: string, callback:AsyncCallback\<void>): void

设置有序公共事件代码和数据。使用callback异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                 | 必填 | 说明                   |
| -------- | -------------------- | ---- | ---------------------- |
| code     | number               | 是   | 公共事件的代码。   |
| data     | string               | 是   | 公共事件的数据。   |
| callback | AsyncCallback\<void> | 是   | 表示被指定的回调方法。 |

**示例：**

```ts
//设置有序公共事件的代码和数据回调
function setCodeAndDataCallback(err:Base.BusinessError) {
    if (err.code !== undefined && err.code != null) {
        console.error(`setCodeAndData failed, code is ${err.code}, message is ${err.message}`);
    } else {
        console.info("setCodeAndData success");
    }
}
subscriber.setCodeAndData(1, "publish_data_changed", setCodeAndDataCallback);
```

## setCodeAndData

setCodeAndData(code: number, data: string): Promise\<void>

设置有序公共事件的代码和数据。使用Promise异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名 | 类型   | 必填 | 说明                 |
| ------ | ------ | ---- | -------------------- |
| code   | number | 是   | 公共事件的代码。 |
| data   | string | 是   | 公共事件的数据。 |

**返回值：**

| 类型             | 说明                 |
| ---------------- | -------------------- |
| Promise\<void>   | 返回一个Promise。 |

**示例：**

```ts
subscriber.setCodeAndData(1, "publish_data_changed").then(() => {
    console.info("setCodeAndData success");
}).catch((err:Base.BusinessError) => {
    console.error(`setCodeAndData failed, code is ${err.code}, message is ${err.message}`);
});
```

## setCodeAndDataSync<sup>10+</sup>

setCodeAndDataSync(code: number, data: string): void

设置有序公共事件的代码和数据。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名 | 类型   | 必填 | 说明                 |
| ------ | ------ | ---- | -------------------- |
| code   | number | 是   | 公共事件的代码。 |
| data   | string | 是   | 公共事件的数据。 |

**示例：**

```ts
try {
    subscriber.setCodeAndDataSync(1, "publish_data_changed");
} catch (error) {
    let err:Base.BusinessError = error as Base.BusinessError;
    console.error(`setCodeAndDataSync failed, code is ${err.code}, message is ${err.message}`);
}

```

## isOrderedCommonEvent

isOrderedCommonEvent(callback: AsyncCallback\<boolean>): void

查询当前公共事件是否为有序公共事件。使用callback异步回调。

返回true代表是有序公共事件，false代表不是有序公共事件。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                    | 必填 | 说明                               |
| -------- | ----------------------- | ---- | ---------------------------------- |
| callback | AsyncCallback\<boolean> | 是   | 当前公共事件是否为有序公共事件。 |

**示例：**

```ts
//获取当前公共事件是否为有序事件的回调
function isOrderedCommonEventCallback(err:Base.BusinessError, isOrdered:boolean) {
    if (err.code !== undefined && err.code != null) {
        console.error(`isOrderedCommonEvent failed, code is ${err.code}, message is ${err.message}`);
    } else {
        console.info("isOrderedCommonEvent " + JSON.stringify(isOrdered));
    }
}
subscriber.isOrderedCommonEvent(isOrderedCommonEventCallback);
```

## isOrderedCommonEvent

isOrderedCommonEvent(): Promise\<boolean>

查询当前公共事件是否为有序公共事件。使用Promise异步回调。

返回true代表是有序公共事件，false代表不是有序公共事件。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型              | 说明                             |
| ----------------- | -------------------------------- |
| Promise\<boolean> | 当前公共事件是否为有序公共事件。 |

**示例：**

```ts
subscriber.isOrderedCommonEvent().then((isOrdered:boolean) => {
    console.info("isOrderedCommonEvent " + JSON.stringify(isOrdered));
}).catch((err:Base.BusinessError) => {
    console.error(`isOrderedCommonEvent failed, code is ${err.code}, message is ${err.message}`);
});
```

## isOrderedCommonEventSync<sup>10+</sup>

isOrderedCommonEventSync(): boolean

查询当前公共事件是否为有序公共事件。

返回true代表是有序公共事件，false代表不是有序公共事件。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型              | 说明                             |
| ----------------- | -------------------------------- |
| boolean | 当前公共事件是否为有序公共事件。 |

**示例：**

```ts
let isOrdered  = subscriber.isOrderedCommonEventSync();
console.info("isOrderedCommonEventSync " + JSON.stringify(isOrdered));
```

## isStickyCommonEvent

isStickyCommonEvent(callback: AsyncCallback\<boolean>): void

检查当前公共事件是否为一个粘性事件。使用callback异步回调。

返回true代表是粘性公共事件，false代表不是粘性公共事件。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                    | 必填 | 说明                               |
| -------- | ----------------------- | ---- | ---------------------------------- |
| callback | AsyncCallback\<boolean> | 是   | 当前公共事件是否为粘性公共事件。 |

**示例：**

```ts
//获取当前公共事件是否为粘性事件的回调
function isStickyCommonEventCallback(err:Base.BusinessError, isSticky:boolean) {
    if (err.code !== undefined && err.code != null) {
        console.error(`isStickyCommonEvent failed, code is ${err.code}, message is ${err.message}`);
    } else {
        console.info("isStickyCommonEvent " + JSON.stringify(isSticky));
    }
}
subscriber.isStickyCommonEvent(isStickyCommonEventCallback);
```

## isStickyCommonEvent

isStickyCommonEvent(): Promise\<boolean>

检查当前公共事件是否为一个粘性事件。使用Promise异步回调。

返回true代表是粘性公共事件，false代表不是粘性公共事件。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型              | 说明                             |
| ----------------- | -------------------------------- |
| Promise\<boolean> | 当前公共事件是否为粘性公共事件。 |

**示例：**

```ts
subscriber.isStickyCommonEvent().then((isSticky:boolean) => {
    console.info("isStickyCommonEvent " + JSON.stringify(isSticky));
}).catch((err:Base.BusinessError) => {
    console.error(`isStickyCommonEvent failed, code is ${err.code}, message is ${err.message}`);
});
```

## isStickyCommonEventSync<sup>10+</sup>

isStickyCommonEventSync(): boolean

检查当前公共事件是否为一个粘性事件。

返回true代表是粘性公共事件，false代表不是粘性公共事件。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型              | 说明                             |
| ----------------- | -------------------------------- |
| boolean | 当前公共事件是否为粘性公共事件。 |

**示例：**

```ts
let isSticky  = subscriber.isStickyCommonEventSync();
console.info("isStickyCommonEventSync " + JSON.stringify(isSticky));
```

## abortCommonEvent

abortCommonEvent(callback: AsyncCallback\<void>): void

取消当前的有序公共事件，取消后，有序公共事件不再向下一个订阅者传递。使用callback异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                 | 必填 | 说明                 |
| -------- | -------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void> | 是   | 取消当前的有序公共事件。 |

**示例：**

```ts
//取消当前有序公共事件的回调
function abortCommonEventCallback(err:Base.BusinessError) {
    if (err.code !== undefined && err.code != null) {
		console.error(`abortCommonEvent failed, code is ${err.code}, message is ${err.message}`);
    } else {
        console.info("abortCommonEvent success");
    }
}
subscriber.abortCommonEvent(abortCommonEventCallback);
```

## abortCommonEvent

abortCommonEvent(): Promise\<void>

取消当前的有序公共事件，取消后，公共事件不再向下一个订阅者传递。使用Promise异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型             | 说明                 |
| ---------------- | -------------------- |
| Promise\<void>   | 返回一个Promise的结果。 |

**示例：**

```ts
subscriber.abortCommonEvent().then(() => {
    console.info("abortCommonEvent success");
}).catch((err:Base.BusinessError) => {
    console.error(`abortCommonEvent failed, code is ${err.code}, message is ${err.message}`);
});
```

## abortCommonEventSync<sup>10+</sup>

abortCommonEventSync(): void

取消当前的有序公共事件，取消后，公共事件不再向下一个订阅者传递。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**示例：**

```ts
subscriber.abortCommonEventSync();
```

## clearAbortCommonEvent

clearAbortCommonEvent(callback: AsyncCallback\<void>): void

清除当前有序公共事件。使用callback异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                 | 必填 | 说明                 |
| -------- | -------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void> | 是   | 表示被指定的回调方法。 |

**示例：**

```ts
//清除当前公共事件取消状态的回调
function clearAbortCommonEventCallback(err:Base.BusinessError) {
    if (err.code !== undefined && err.code != null) {
        console.error(`clearAbortCommonEvent failed, code is ${err.code}, message is ${err.message}`);
    } else {
        console.info("clearAbortCommonEvent success");
    }
}
subscriber.clearAbortCommonEvent(clearAbortCommonEventCallback);
```

## clearAbortCommonEvent

clearAbortCommonEvent(): Promise\<void>

清除当前有序公共事件。使用Promise异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型             | 说明                 |
| ---------------- | -------------------- |
| Promise\<void>   | 返回一个Promise的结果。 |

**示例：**

```ts
subscriber.clearAbortCommonEvent().then(() => {
    console.info("clearAbortCommonEvent success");
}).catch((err:Base.BusinessError) => {
    console.error(`clearAbortCommonEvent failed, code is ${err.code}, message is ${err.message}`);
});
```

## clearAbortCommonEventSync<sup>10+</sup>

clearAbortCommonEventSync(): void

清除当前有序公共事件。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**示例：**

```ts
subscriber.clearAbortCommonEventSync();
```

## getAbortCommonEvent

getAbortCommonEvent(callback: AsyncCallback\<boolean>): void

获取当前有序公共事件是否取消的状态。使用callback异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                    | 必填 | 说明                               |
| -------- | ----------------------- | ---- | ---------------------------------- |
| callback | AsyncCallback\<boolean> | 是   | 表示当前有序公共事件是否取消的状态。 |

**示例：**

```ts
//获取当前有序公共事件是否取消的回调
function getAbortCommonEventCallback(err:Base.BusinessError, abortEvent:boolean) {
    if (err.code !== undefined && err.code != null) {
        console.error(`getAbortCommonEvent failed, code is ${err.code}, message is ${err.message}`);
    } else {
        console.info("getAbortCommonEvent " + JSON.stringify(abortEvent));
    }
}
subscriber.getAbortCommonEvent(getAbortCommonEventCallback);
```

## getAbortCommonEvent

getAbortCommonEvent(): Promise\<boolean>

获取当前有序公共事件是否取消的状态。使用Promise异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型              | 说明                               |
| ----------------- | ---------------------------------- |
| Promise\<boolean> | 表示当前有序公共事件是否取消的状态。 |

**示例：**

```ts
subscriber.getAbortCommonEvent().then((abortEvent:boolean) => {
    console.info("getAbortCommonEvent " + JSON.stringify(abortEvent));
}).catch((err:Base.BusinessError) => {
    console.error(`getAbortCommonEvent failed, code is ${err.code}, message is ${err.message}`);
});
```

## getAbortCommonEventSync<sup>10+</sup>

getAbortCommonEventSync(): boolean

获取当前有序公共事件是否取消的状态。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型              | 说明                               |
| ----------------- | ---------------------------------- |
| boolean | 表示当前有序公共事件是否取消的状态。 |

**示例：**

```ts
let abortEvent = subscriber.getAbortCommonEventSync();
console.info("getAbortCommonEventSync " + JSON.stringify(abortEvent));
```

## getSubscribeInfo

getSubscribeInfo(callback: AsyncCallback\<CommonEventSubscribeInfo>): void

获取订阅者的订阅信息。使用callback异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                   |
| -------- | ------------------------------------------------------------ | ---- | ---------------------- |
| callback | AsyncCallback\<[CommonEventSubscribeInfo](./js-apis-inner-commonEvent-commonEventSubscribeInfo.md)> | 是   | 表示订阅者的订阅信息。 |

**示例：**

```ts
//获取订阅者信息回调
function getSubscribeInfoCallback(err:Base.BusinessError, subscribeInfo:CommonEventManager.CommonEventSubscribeInfo) {
    if (err.code !== undefined && err.code != null) {
        console.error(`getSubscribeInfo failed, code is ${err.code}, message is ${err.message}`);
    } else {
        console.info("getSubscribeInfo " + JSON.stringify(subscribeInfo));
    }
}
subscriber.getSubscribeInfo(getSubscribeInfoCallback);
```

## getSubscribeInfo

getSubscribeInfo(): Promise\<CommonEventSubscribeInfo>

获取订阅者的订阅信息。使用Promise异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型                                                         | 说明                   |
| ------------------------------------------------------------ | ---------------------- |
| Promise\<[CommonEventSubscribeInfo](./js-apis-inner-commonEvent-commonEventSubscribeInfo.md)> | 表示订阅者的订阅信息。 |

**示例：**

```ts
subscriber.getSubscribeInfo().then((subscribeInfo:CommonEventManager.CommonEventSubscribeInfo) => {
    console.info("getSubscribeInfo " + JSON.stringify(subscribeInfo));
}).catch((err:Base.BusinessError) => {
    console.error(`getSubscribeInfo failed, code is ${err.code}, message is ${err.message}`);
});
```

## getSubscribeInfoSync<sup>10+</sup>

getSubscribeInfoSync(): CommonEventSubscribeInfo

获取订阅者的订阅信息。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型                                                         | 说明                   |
| ------------------------------------------------------------ | ---------------------- |
| [CommonEventSubscribeInfo](./js-apis-inner-commonEvent-commonEventSubscribeInfo.md) | 表示订阅者的订阅信息。 |

**示例：**

```ts
let subscribeInfo = subscriber.getSubscribeInfoSync();
console.info("getSubscribeInfoSync " + JSON.stringify(subscribeInfo));
```

## finishCommonEvent<sup>9+</sup>

finishCommonEvent(callback: AsyncCallback\<void>): void

结束当前有序公共事件。使用callback异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**参数：**

| 参数名   | 类型                  | 必填 | 说明                              |
| -------- | -------------------- | ---- | -------------------------------- |
| callback | AsyncCallback\<void> | 是   | 表示有序公共事件结束后的回调函数。 |

**示例：**

```ts
//结束当前有序公共事件的回调
function finishCommonEventCallback(err:Base.BusinessError) {
  if (err.code !== undefined && err.code != null) {
    console.error(`finishCommonEvent failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("finishCommonEvent success");
  }
}
subscriber.finishCommonEvent(finishCommonEventCallback);
```

## finishCommonEvent<sup>9+</sup>

finishCommonEvent(): Promise\<void>

结束当前有序公共事件。使用Promise异步回调。

**系统能力**：`SystemCapability.Notification.CommonEvent`

**返回值：**

| 类型             | 说明                 |
| ---------------- | -------------------- |
| Promise\<void>   | 返回一个Promise的结果。 |

**示例：**

```ts
subscriber.finishCommonEvent().then(() => {
    console.info("finishCommonEvent success");
}).catch((err:Base.BusinessError) => {
    console.error(`finishCommonEvent failed, code is ${err.code}, message is ${err.message}`);
});
```