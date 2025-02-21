# @ohos.power (系统电源管理)

该模块主要提供重启、关机、查询屏幕状态等接口。

> **说明：**
>
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```js
import power from '@ohos.power';
```

## power.shutdown

shutdown(reason: string): void

系统关机。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.REBOOT

**系统能力：** SystemCapability.PowerManager.PowerManager.Core

**参数：**

| 参数名    | 类型     | 必填   | 说明    |
| ------ | ------ | ---- | ----- |
| reason | string | 是    | 关机原因。 |

**错误码：**

以下错误码的详细介绍请参见[系统电源管理错误码](../errorcodes/errorcode-power.md)。

| 错误码ID   | 错误信息    |
|---------|---------|
| 4900101 | If connecting to the service failed. |

**示例：**

```js
try {
    power.shutdown('shutdown_test');
} catch(err) {
    console.error('shutdown failed, err: ' + err);
}
```

## power.reboot<sup>9+</sup>

reboot(reason: string): void

重启设备。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.REBOOT

**系统能力：** SystemCapability.PowerManager.PowerManager.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明       |
| ------ | ------ | ---- | ---------- |
| reason | string | 是   | 重启原因。 |

**错误码：**

以下错误码的详细介绍请参见[系统电源管理错误码](../errorcodes/errorcode-power.md)。

| 错误码ID   | 错误信息    |
|---------|---------|
| 4900101 | If connecting to the service failed. |

**示例：**

```js
try {
    power.reboot('reboot_test');
} catch(err) {
    console.error('reboot failed, err: ' + err);
}
```

## power.isActive<sup>9+</sup>

isActive(): boolean

检测当前设备是否处于活动状态。

**系统能力：** SystemCapability.PowerManager.PowerManager.Core

**错误码：**

以下错误码的详细介绍请参见[系统电源管理错误码](../errorcodes/errorcode-power.md)。

| 错误码ID   | 错误信息    |
|---------|---------|
| 4900101 | If connecting to the service failed. |

**示例：**

```js
try {
    var isActive = power.isActive();
    console.info('power is active: ' + isActive);
} catch(err) {
    console.error('check active status failed, err: ' + err);
}
```

## power.wakeup<sup>9+</sup>

wakeup(detail: string): void

唤醒设备。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.PowerManager.PowerManager.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明       |
| ------ | ------ | ---- | ---------- |
| detail | string | 是   | 唤醒原因。 |

**错误码：**

以下错误码的详细介绍请参见[系统电源管理错误码](../errorcodes/errorcode-power.md)。

| 错误码ID   | 错误信息    |
|---------|---------|
| 4900101 | If connecting to the service failed. |

**示例：**

```js
try {
    power.wakeup('wakeup_test');
} catch(err) {
    console.error('wakeup failed, err: ' + err);
}
```

## power.suspend<sup>9+</sup>

suspend(): void

休眠设备。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.PowerManager.PowerManager.Core

**错误码：**

以下错误码的详细介绍请参见[系统电源管理错误码](../errorcodes/errorcode-power.md)。

| 错误码ID   | 错误信息    |
|---------|---------|
| 4900101 | If connecting to the service failed. |

**示例：**

```js
try {
    power.suspend();
} catch(err) {
    console.error('suspend failed, err: ' + err);
}
```

## power.getPowerMode<sup>9+</sup>

getPowerMode(): DevicePowerMode

获取当前设备的电源模式。

**系统能力：** SystemCapability.PowerManager.PowerManager.Core

**返回值：**

| 类型                                 | 说明       |
| ------------------------------------ | ---------- |
| [DevicePowerMode](#devicepowermode9) | 电源模式。 |

**错误码：**

以下错误码的详细介绍请参见[系统电源管理错误码](../errorcodes/errorcode-power.md)。

| 错误码ID   | 错误信息    |
|---------|---------|
| 4900101 | If connecting to the service failed. |

**示例：**

```js
try {
    var mode = power.getPowerMode();
    console.info('power mode: ' + mode);
} catch(err) {
    console.error('get power mode failed, err: ' + err);
}
```

## power.setPowerMode<sup>9+</sup>

setPowerMode(mode: DevicePowerMode, callback: AsyncCallback&lt;void&gt;): void

设置当前设备的电源模式。使用callback异步回调。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.POWER_OPTIMIZATION

**系统能力：** SystemCapability.PowerManager.PowerManager.Core

**参数：**

| 参数名   | 类型                                 | 必填 | 说明                                                         |
| -------- | ------------------------------------ | ---- | ------------------------------------------------------------ |
| mode     | [DevicePowerMode](#devicepowermode9) | 是   | 电源模式。                                                   |
| callback | AsyncCallback&lt;void&gt;            | 是   | 回调函数。当设置电源模式成功，err为undefined，否则为错误对象。 |

**错误码：**

以下错误码的详细介绍请参见[系统电源管理错误码](../errorcodes/errorcode-power.md)。

| 错误码ID   | 错误信息    |
|---------|---------|
| 4900101 | If connecting to the service failed. |

**示例：**

```js
power.setPowerMode(power.DevicePowerMode.MODE_PERFORMANCE, err => {
    if (typeof err === 'undefined') {
        console.info('set power mode to MODE_PERFORMANCE');
    } else {
        console.error('set power mode failed, err: ' + err);
    }
});
```

## power.setPowerMode<sup>9+</sup>

setPowerMode(mode: DevicePowerMode): Promise&lt;void&gt;

设置当前设备的电源模式。使用Promise异步回调。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.POWER_OPTIMIZATION

**系统能力：** SystemCapability.PowerManager.PowerManager.Core

**参数：**

| 参数名 | 类型                                 | 必填 | 说明       |
| ------ | ------------------------------------ | ---- | ---------- |
| mode   | [DevicePowerMode](#devicepowermode9) | 是   | 电源模式。 |

**返回值：**

| 类型                | 说明                                   |
| ------------------- | -------------------------------------- |
| Promise&lt;void&gt; | Promise对象。无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[系统电源管理错误码](../errorcodes/errorcode-power.md)。

| 错误码ID   | 错误信息    |
|---------|---------|
| 4900101 | If connecting to the service failed. |

**示例：**

```js
power.setPowerMode(power.DevicePowerMode.MODE_PERFORMANCE)
.then(() => {
    console.info('set power mode to MODE_PERFORMANCE');
})
.catch(err => {
    console.error('set power mode failed, err: ' + err);
});
```

## power.rebootDevice<sup>(deprecated)</sup>

rebootDevice(reason: string): void

> **说明：**<br>从API version 7开始支持，从API version 9开始不再维护。建议使用[power.reboot](#powerreboot9)替代，替代接口能力仅对系统应用开放。

重启设备。

**需要权限：** ohos.permission.REBOOT

**系统能力：** SystemCapability.PowerManager.PowerManager.Core

**参数：**

| 参数名    | 类型     | 必填   | 说明    |
| ------ | ------ | ---- | ----- |
| reason | string | 是    | 重启原因。 |

**示例：**

```js
power.rebootDevice('reboot_test');
```

## power.isScreenOn<sup>(deprecated)</sup>

isScreenOn(callback: AsyncCallback&lt;boolean&gt;): void

> **说明：**<br>从API version 9开始不再维护，建议使用[power.isActive](#powerisactive9)替代。

检测当前设备的亮灭屏状态。使用callback异步回调。

**系统能力：** SystemCapability.PowerManager.PowerManager.Core

**参数：**

| 参数名   | 类型                         | 必填 | 说明                                                         |
| -------- | ---------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback&lt;boolean&gt; | 是   | 回调函数。当检测成功，err为undefined，data为获取到的亮灭屏状态，返回true表示亮屏，返回false表示灭屏；否则为错误对象。 |

**示例：**

```js
power.isScreenOn((err, data) => {
    if (typeof err === 'undefined') {
        console.info('screen on status is ' + data);
    } else {
        console.error('check screen status failed, err: ' + err);
    }
})
```

## power.isScreenOn<sup>(deprecated)</sup>

isScreenOn(): Promise&lt;boolean&gt;

> **说明：**<br>从API version 9开始不再维护，建议使用[power.isActive](#powerisactive9)替代。

检测当前设备的亮灭屏状态。使用Promise异步回调。

**系统能力：** SystemCapability.PowerManager.PowerManager.Core

**返回值：**
| 类型                   | 说明                                               |
| ---------------------- | -------------------------------------------------- |
| Promise&lt;boolean&gt; | Promise对象。返回true表示亮屏；返回false表示灭屏。 |

**示例：**

```js
power.isScreenOn()
.then(data => {
    console.info('screen on status is ' + data);
})
.catch(err => {
    console.error('check screen status failed, err: ' + err);
})
```

## DevicePowerMode<sup>9+</sup>

表示电源模式的枚举值。

**系统能力：** SystemCapability.PowerManager.PowerManager.Core

| 名称                    | 值   | 说明                   |
| ----------------------- | ---- | ---------------------- |
| MODE_NORMAL             | 600  | 表示标准模式，默认值。 |
| MODE_POWER_SAVE         | 601  | 表示省电模式。         |
| MODE_PERFORMANCE        | 602  | 表示性能模式。         |
| MODE_EXTREME_POWER_SAVE | 603  | 表示超级省电模式。     |
