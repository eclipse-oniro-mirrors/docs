# @ohos.multimodalInput.inputDevice (输入设备)

输入设备管理模块，用于监听输入设备连接和断开状态，查询输入设备相关信息。

> **说明**：
>
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```js
import inputDevice from '@ohos.multimodalInput.inputDevice';
```

## inputDevice.getDeviceList<sup>9+</sup>

getDeviceList(callback: AsyncCallback&lt;Array&lt;number&gt;&gt;): void

获取所有输入设备的id列表，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**参数**：

| 参数名     | 类型                                     | 必填 | 说明                                     |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| callback | AsyncCallback&lt;Array&lt;number&gt;&gt; | 是   | 回调函数，异步返回所有输入设备的id列表。 |

**示例**：

```js
try {
  inputDevice.getDeviceList((error, ids) => {
    if (error) {
      console.log(`Failed to get device id list, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Device id list: ${JSON.stringify(ids)}`);
  });
} catch (error) {
  console.log(`Failed to get device id list, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.getDeviceList<sup>9+</sup>

getDeviceList(): Promise&lt;Array&lt;number&gt;&gt;

获取所有输入设备的id列表，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**返回值**：

| 参数                               | 说明                                        |
| ---------------------------------- | ------------------------------------------- |
| Promise&lt;Array&lt;number&gt;&gt; | Promise对象，异步返回所有输入设备的id列表。 |

**示例**：

```js
try {
  inputDevice.getDeviceList().then((ids) => {
    console.log(`Device id list: ${JSON.stringify(ids)}`);
  });
} catch (error) {
  console.log(`Failed to get device id list, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.getDeviceInfo<sup>9+</sup>

getDeviceInfo(deviceId: number, callback: AsyncCallback&lt;InputDeviceData&gt;): void

获取指定输入设备的信息，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**参数**：

| 参数名     | 类型                                                     | 必填 | 说明                                    |
| -------- | -------------------------------------------------------- | ---- | --------------------------------------- |
| deviceId | number                                                   | 是   | 输入设备id。                  |
| callback | AsyncCallback&lt;[InputDeviceData](#inputdevicedata)&gt; | 是   | 回调函数，异步返回输入设备信息。 |

**示例**：

```js
// 获取输入设备id为1的设备信息。
try {
  inputDevice.getDeviceInfo(1, (error, deviceData) => {
    if (error) {
      console.log(`Failed to get device info, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Device info: ${JSON.stringify(deviceData)}`);
  });
} catch (error) {
  console.log(`Failed to get device info, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.getDeviceInfo<sup>9+</sup>

getDeviceInfo(deviceId: number): Promise&lt;InputDeviceData&gt;

获取指定输入设备的信息，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**参数**：

| 参数名     | 类型   | 必填 | 说明                   |
| -------- | ------ | ---- | ---------------------- |
| deviceId | number | 是   | 输入设备id。 |

**返回值**：

| 参数                                               | 说明                            |
| -------------------------------------------------- | ------------------------------- |
| Promise&lt;[InputDeviceData](#inputdevicedata)&gt; | Promise对象，异步返回输入设备信息。 |

**示例**：

```js
// 获取输入设备id为1的设备信息。
try {
  inputDevice.getDeviceInfo(1).then((deviceData) => {
    console.log(`Device info: ${JSON.stringify(deviceData)}`);
  });
} catch (error) {
  console.log(`Failed to get device info, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.on<sup>9+</sup>

on(type: "change", listener: Callback&lt;DeviceListener&gt;): void

监听输入设备的热插拔事件。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**参数**：

| 参数名       | 类型                                       | 必填   | 说明          |
| -------- | ---------------------------------------- | ---- | ----------- |
| type     | string                                   | 是    | 输入设备的事件类型。  |
| listener | Callback&lt;[DeviceListener](#devicelistener9)&gt; | 是    | 回调函数，异步上报输入设备热插拔事件。 |

**示例**：

```js
let isPhysicalKeyboardExist = true;
try {
  inputDevice.on("change", (data) => {
    console.log(`Device event info: ${JSON.stringify(data)}`);
    inputDevice.getKeyboardType(data.deviceId, (err, type) => {
      console.log("The keyboard type is: " + type);
      if (type == inputDevice.KeyboardType.ALPHABETIC_KEYBOARD && data.type == 'add') {
        // 监听物理键盘已连接。
        isPhysicalKeyboardExist = true;
      } else if (type == inputDevice.KeyboardType.ALPHABETIC_KEYBOARD && data.type == 'remove') {
        // 监听物理键盘已断开。
        isPhysicalKeyboardExist = false;
      }
    });
  });
  // 根据isPhysicalKeyboardExist的值决定软键盘是否弹出。
} catch (error) {
  console.log(`Get device info failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.off<sup>9+</sup>

off(type: "change", listener?: Callback&lt;DeviceListener&gt;): void

取消监听输入设备的热插拔事件。在应用退出前调用，取消监听。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**参数**：

| 参数名       | 类型                                       | 必填   | 说明          |
| -------- | ---------------------------------------- | ---- | ----------- |
| type     | string                                   | 是    | 输入设备的事件类型。  |
| listener | Callback&lt;[DeviceListener](#devicelistener9)&gt; | 否    | 取消监听的回调函数。 |

**示例**：

```js
function callback(data) {
  console.log(`Report device event info: ${JSON.stringify(data, [`type`, `deviceId`])}`);
};

try {
  inputDevice.on("change", callback);
} catch (error) {
  console.log(`Listen device event failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}

// 取消指定的监听。
try {
  inputDevice.off("change", callback);
} catch (error) {
  console.log(`Cancel listening device event failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}

// 取消所有监听。
try {
  inputDevice.off("change");
} catch (error) {
  console.log(`Cancel all listening device event failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.getDeviceIds<sup>(deprecated)</sup>

getDeviceIds(callback: AsyncCallback&lt;Array&lt;number&gt;&gt;): void

获取所有输入设备的id列表，使用AsyncCallback异步方式返回结果。

从API version 9 开始不再维护，建议使用[inputDevice.getDeviceList](#inputdevicegetdevicelist9)代替。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**参数**：

| 参数名     | 类型                                     | 必填 | 说明                                     |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| callback | AsyncCallback&lt;Array&lt;number&gt;&gt; | 是   | 回调函数，异步返回所有输入设备的id列表。 |

**示例**：

```js
inputDevice.getDeviceIds((error, ids) => {
  if (error) {
    console.log(`Failed to get device id list, error: ${JSON.stringify(error, [`code`, `message`])}`);
    return;
  }
  console.log(`Device id list: ${JSON.stringify(ids)}`);
});
```

## inputDevice.getDeviceIds<sup>(deprecated)</sup>

getDeviceIds(): Promise&lt;Array&lt;number&gt;&gt;

获取所有输入设备的id列表，使用Promise异步方式返回结果。

从API version 9 开始不再维护，建议使用[inputDevice.getDeviceList](#inputdevicegetdevicelist9)代替。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**返回值**：

| 参数                               | 说明                                        |
| ---------------------------------- | ------------------------------------------- |
| Promise&lt;Array&lt;number&gt;&gt; | Promise对象，异步返回所有输入设备的id列表。 |

**示例**：

```js
inputDevice.getDeviceIds().then((ids) => {
  console.log(`Device id list: ${JSON.stringify(ids)}`);
});
```

## inputDevice.getDevice<sup>(deprecated)</sup>

getDevice(deviceId: number, callback: AsyncCallback&lt;InputDeviceData&gt;): void

获取指定输入设备的信息，使用AsyncCallback异步方式返回结果。

从API version 9 开始不再维护，建议使用[inputDevice.getDeviceInfo](#inputdevicegetdeviceinfo9)代替。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**参数**：

| 参数名     | 类型                                                     | 必填 | 说明                             |
| -------- | -------------------------------------------------------- | ---- | -------------------------------- |
| deviceId | number                                                   | 是   | 输入设备id。                     |
| callback | AsyncCallback&lt;[InputDeviceData](#inputdevicedata)&gt; | 是   | 回调函数，异步返回输入设备信息。 |

**示例**：

```js
// 获取输入设备id为1的设备信息。
inputDevice.getDevice(1, (error, deviceData) => {
  if (error) {
    console.log(`Failed to get device info, error: ${JSON.stringify(error, [`code`, `message`])}`);
    return;
  }
  console.log(`Device info: ${JSON.stringify(deviceData)}`);
});
```

## inputDevice.getDevice<sup>(deprecated)</sup>

getDevice(deviceId: number): Promise&lt;InputDeviceData&gt;

获取指定输入设备的信息，使用Promise异步方式返回结果。

从API version 9 开始不再维护，建议使用[inputDevice.getDeviceInfo](#inputdevicegetdeviceinfo9)代替。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**参数**：

| 参数名     | 类型   | 必填 | 说明         |
| -------- | ------ | ---- | ------------ |
| deviceId | number | 是   | 输入设备id。 |

**返回值**：

| 参数                                               | 说明                                |
| -------------------------------------------------- | ----------------------------------- |
| Promise&lt;[InputDeviceData](#inputdevicedata)&gt; | Promise对象，异步返回输入设备信息。 |

**示例**：

```js
// 获取输入设备id为1的设备信息。
inputDevice.getDevice(1).then((deviceData) => {
  console.log(`Device info: ${JSON.stringify(deviceData)}`);
});
```

## inputDevice.supportKeys<sup>9+</sup>

supportKeys(deviceId: number, keys: Array&lt;KeyCode&gt;, callback: AsyncCallback &lt;Array&lt;boolean&gt;&gt;): void

获取输入设备是否支持指定的键码值，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**参数**：

| 参数名     | 类型                                      | 必填 | 说明                                                   |
| -------- | ----------------------------------------- | ---- | ------------------------------------------------------ |
| deviceId | number                                    | 是   | 输入设备id，同一个物理设备反复插拔，设备id会发生变化。 |
| keys     | Array&lt;KeyCode&gt;                      | 是   | 需要查询的键码值，最多支持5个按键查询。                |
| callback | AsyncCallback&lt;Array&lt;boolean&gt;&gt; | 是   | 回调函数，异步返回查询结果。                           |

**示例**：

```js
// 查询id为1的输入设备对于17、22和2055按键的支持情况。
try {
  inputDevice.supportKeys(1, [17, 22, 2055], (error, supportResult) => {
    console.log(`Query result: ${JSON.stringify(supportResult)}`);
  });
} catch (error) {
  console.log(`Query failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.supportKeys<sup>9+</sup>

supportKeys(deviceId: number, keys: Array&lt;KeyCode&gt;): Promise&lt;Array&lt;boolean&gt;&gt;

获取输入设备是否支持指定的键码值，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**参数**：

| 参数名     | 类型                 | 必填 | 说明                                                   |
| -------- | -------------------- | ---- | ------------------------------------------------------ |
| deviceId | number               | 是   | 输入设备id，同一个物理设备反复插拔，设备id会发生变化。 |
| keys     | Array&lt;KeyCode&gt; | 是   | 需要查询的键码值，最多支持5个按键查询。                |

**返回值**：

| 参数                                | 说明                            |
| ----------------------------------- | ------------------------------- |
| Promise&lt;Array&lt;boolean&gt;&gt; | Promise对象，异步返回查询结果。 |

**示例**：

```js
// 查询id为1的输入设备对于17、22和2055按键的支持情况。
try {
  inputDevice.supportKeys(1, [17, 22, 2055]).then((supportResult) => {
    console.log(`Query result: ${JSON.stringify(supportResult)}`);
  });
} catch (error) {
  console.log(`Query failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.getKeyboardType<sup>9+</sup>

getKeyboardType(deviceId: number, callback: AsyncCallback&lt;KeyboardType&gt;): void

获取输入设备的键盘类型，使用AsyncCallback异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**参数**：

| 参数名     | 类型                                                | 必填 | 说明                                                         |
| -------- | --------------------------------------------------- | ---- | ------------------------------------------------------------ |
| deviceId | number                                              | 是   | 输入设备的唯一标识，同一个物理设备反复插拔，设备id会发生变化。 |
| callback | AsyncCallback&lt;[KeyboardType](#keyboardtype9)&gt; | 是   | 回调函数，异步返回查询结果。                                 |

**示例**：

```js
// 查询id为1的输入设备的键盘类型。
try {
  inputDevice.getKeyboardType(1, (error, type) => {
    if (error) {
      console.log(`Failed to get keyboard type, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Keyboard type: ${JSON.stringify(type)}`);
  });
} catch (error) {
  console.log(`Failed to get keyboard type, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.getKeyboardType<sup>9+</sup>

getKeyboardType(deviceId: number): Promise&lt;KeyboardType&gt;

获取输入设备的键盘类型，使用Promise异步方式返回结果。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

**参数**：

| 参数名     | 类型   | 必填 | 说明                                                         |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| deviceId | number | 是   | 输入设备的唯一标识，同一个物理设备反复插拔，设备id会发生变化。 |

**返回值**：

| 参数                                          | 说明                            |
| --------------------------------------------- | ------------------------------- |
| Promise&lt;[KeyboardType](#keyboardtype9)&gt; | Promise对象，异步返回查询结果。 |

**示例**：

```js
// 示例查询设备id为1的设备键盘类型。
try {
  inputDevice.getKeyboardType(1).then((type) => {
    console.log(`Keyboard type: ${JSON.stringify(type)}`);
  });
} catch (error) {
  console.log(`Failed to get keyboard type, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## DeviceListener<sup>9+</sup>

输入设备热插拔的描述信息。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

| 名称        | 类型   | 可读   | 可写   | 说明      |
| --------- | ------ | ---- | ---- | ------- |
| type     | [ChangedType](#changedtype) | 是 | 否 | 输入设备插入或者移除。|
| deviceId | number                      | 是 | 否 | 输入设备的唯一标识，同一个物理设备反复插拔，设备id会发生变化。 |

## InputDeviceData

输入设备的描述信息。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

| 名称        | 类型   | 可读   | 可写   | 说明      |
| --------- | ------ | ---- | ---- | ------- |
| id                   | number                                 | 是 | 否 | 输入设备的唯一标识，同一个物理设备反复插拔，设备id会发生变化。 |
| name                 | string                                 | 是 | 否 | 输入设备的名字。                                             |
| sources              | Array&lt;[SourceType](#sourcetype)&gt; | 是 | 否 | 输入设备支持的源类型。比如有的键盘上附带触摸板，则此设备有keyboard和touchpad两种输入源。 |
| axisRanges           | Array&lt;[AxisRange](#axisrange)&gt;  | 是 | 否 | 输入设备的轴信息。                                           |
| bus<sup>9+</sup>     | number                                 | 是 | 否 | 输入设备的总线类型。                                         |
| product<sup>9+</sup> | number                                 | 是 | 否 | 输入设备的产品信息。                                         |
| vendor<sup>9+</sup>  | number                                 | 是 | 否 | 输入设备的厂商信息。                                         |
| version<sup>9+</sup> | number                                 | 是 | 否 | 输入设备的版本信息。                                         |
| phys<sup>9+</sup>    | string                                 | 是 | 否 | 输入设备的物理地址。                                         |
| uniq<sup>9+</sup>    | string                                 | 是 | 否 | 输入设备的唯一标识。                                         |

## AxisType<sup>9+</sup>

输入设备的轴类型。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

| 名称        | 类型   | 可读   | 可写   | 说明      |
| --------- | ------ | ---- | ---- | ------- |
| touchMajor  | string | 是 | 否 | 表示touchMajor轴。  |
| touchMinor  | string | 是 | 否 | 表示touchMinor轴。  |
| toolMinor   | string | 是 | 否 | 表示toolMinor轴。   |
| toolMajor   | string | 是 | 否 | 表示toolMajor轴。   |
| orientation | string | 是 | 否 | 表示orientation轴。 |
| pressure    | string | 是 | 否 | 表示pressure轴。    |
| x           | string | 是 | 否 | 表示x轴。           |
| y           | string | 是 | 否 | 表示y轴。           |
| NULL        | string | 是 | 否 | 无。              |

## AxisRange

输入设备的轴信息。

**系统能力**： SystemCapability.MultimodalInput.Input.InputDevice

| 名称        | 类型   | 可读   | 可写   | 说明      |
| --------- | ------ | ---- | ---- | ------- |
| source                  | [SourceType](#sourcetype) | 是 | 否 | 轴的输入源类型。 |
| axis                    | [AxisType](#axistype9)    | 是 | 否 | 轴的类型。    |
| max                     | number                    | 是 | 否 | 轴的最大值。   |
| min                     | number                    | 是 | 否 | 轴的最小值。   |
| fuzz<sup>9+</sup>       | number                    | 是 | 否 | 轴的模糊值。   |
| flat<sup>9+</sup>       | number                    | 是 | 否 | 轴的基准值。   |
| resolution<sup>9+</sup> | number                    | 是 | 否 | 轴的分辨率。   |

## SourceType<sup>9+</sup>

轴的输入源类型。比如鼠标设备可上报x轴事件，则x轴的输入源就是鼠标。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

| 名称        | 类型   | 可读   | 可写   | 说明      |
| --------- | ------ | ---- | ---- | ------- |
| keyboard    | string | 是 | 否 | 表示输入设备是键盘。  |
| touchscreen | string | 是 | 否 | 表示输入设备是触摸屏。 |
| mouse       | string | 是 | 否 | 表示输入设备是鼠标。  |
| trackball   | string | 是 | 否 | 表示输入设备是轨迹球。 |
| touchpad    | string | 是 | 否 | 表示输入设备是触摸板。 |
| joystick    | string | 是 | 否 | 表示输入设备是操纵杆。 |

## ChangedType<sup>9+</sup>

定义监听设备热插拔事件。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

| 名称        | 类型   | 可读   | 可写   | 说明      |
| --------- | ------ | ---- | ---- | ------- |
| add    | string | 是 | 否 | 表示输入设备插入。 |
| remove | string | 是 | 否 | 表示输入设备移除。 |

## KeyboardType<sup>9+</sup>

定义键盘输入设备的类型。

**系统能力**：SystemCapability.MultimodalInput.Input.InputDevice

| 名称                  | 值    | 说明        |
| ------------------- | ---- | --------- |
| NONE                | 0    | 表示无按键设备。  |
| UNKNOWN             | 1    | 表示未知按键设备。 |
| ALPHABETIC_KEYBOARD | 2    | 表示全键盘设备。  |
| DIGITAL_KEYBOARD    | 3    | 表示小键盘设备。  |
| HANDWRITING_PEN     | 4    | 表示手写笔设备。  |
| REMOTE_CONTROL      | 5    | 表示遥控器设备。  |
