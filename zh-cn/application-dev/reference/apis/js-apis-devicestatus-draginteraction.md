# @ohos. deviceStatus.dragInteraction (拖拽)

 拖拽功能模块，提供注册和取消拖拽状态监听的能力。 

> **说明**
>
>   - 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>
>  - 本模块接口均为系统接口。

## 导入模块

```js
import dragInteraction from '@ohos.deviceStatus.dragInteraction'
```

## dragInteraction.on

on(type: 'drag', callback: Callback&lt;DragState&gt;): void;

注册监听拖拽状态。

**系统能力**：SystemCapability.Msdp.DeviceStatus.Drag

**参数**：

| 参数名                | 类型                                                             | 必填 | 说明                            |
| --------             | ----------------------------                                    | ---- | ----------------------------   |
| type                 | string                                                          |  是  | 监听类型，固定取值为 'drag' |
| callback             | Callback&lt;[DragState](#dragstate)&gt; |  是  | 回调函数，异步返回拖拽状态消息 |

**示例**：

```js
try {
  dragInteraction.on('drag', (data) => {
    console.log(`Drag interaction event: ${JSON.stringify(data)}`);
  });
} catch (error) {
  console.log(`Register failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## dragInteraction.off

off(type: 'drag', callback?: Callback&lt;DragState&gt;): void;

取消监听拖拽状态。

**系统能力**：SystemCapability.Msdp.DeviceStatus.Drag

**参数**：

| 参数名                | 类型                                                              | 必填    | 说明                           |
| --------             | ----------------------------                                     | ----   | ----------------------------   |
| type                 | string                                                           |  是    | 监听类型，固定取值为 'drag' |
| callback             | Callback&lt;[DragState](#dragstate)> |  否  | 需要取消注册的回调函数，若无此参数，则取消当前应用注册的所有回调函数。 |

**示例**：

```js
// 取消注册单个回调函数
function callback(event) {
  console.log(`Drag interaction event: ${JSON.stringify(event)}`);
  return false;
}
try {
  dragInteraction.on('drag', callback);
  dragInteraction.off("drag", callback);
} catch (error) {
  console.log(`Execute failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```
```js
// 取消注册所有回调函数
function callback(event) {
  console.log(`Drag interaction event: ${JSON.stringify(event)}`);
  return false;
}
try {
  dragInteraction.on('drag', callback);
  dragInteraction.off("drag");
} catch (error) {
  console.log(`Execute failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

##  DragState

拖拽状态。

**系统能力**：SystemCapability.Msdp.DeviceStatus.Drag

| 名称                       | 值                             | 说明                              |
| --------                     |  -----------------               |  -----------------               |
| MSG_DRAG_STATE_START |  1   | 表示开始拖拽。 |
| MSG_DRAG_STATE_STOP |  2  |  表示结束拖拽。  |
| MSG_DRAG_STATE_CANCEL |  3  |  表示取消拖拽。  |