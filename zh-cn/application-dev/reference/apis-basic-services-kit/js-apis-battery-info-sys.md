# @ohos.batteryInfo (电量信息)(系统接口)

该模块主要提供电池状态和充放电状态的查询接口。

> **说明：**
>
> 本模块首批接口从API version 6开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>
>当前页面仅包含本模块的系统接口，其他公开接口参见[@ohos.batteryInfo (电量信息)](js-apis-battery-info.md)。


## 导入模块

```js
import batteryInfo from '@ohos.batteryInfo';
```

## batteryInfo.setBatteryConfig<sup>11+</sup>

setBatteryConfig(sceneName: string, sceneValue: string): number

按场景名称设置电池配置。

**系统接口：** 此接口为系统接口。

**系统能力:** SystemCapability.PowerManager.BatteryManager.Core

**参数**：

| 参数名     | 类型   | 必填 | 说明         |
| ---------- | ------ | ---- | ------------ |
| sceneName  | string | 是   | 设置场景名称 |
| sceneValue | string | 是   | 设置场景的值 |

**返回值**：

| 类型   | 说明                                                       |
| ------ | ---------------------------------------------------------- |
| number | 返回设置充电结果。返回0表示设置成功，返回非0表示设置失败。 |

**错误码：**

以下错误码的详细介绍请参见[电量信息错误码](errorcode-battery-info.md)。

| 错误码ID   | 错误信息    |
|---------|---------|
| 4900101 | If connecting to the service failed. |

**示例**：

  ```ts
  import batteryInfo from '@ohos.batteryInfo';

  let sceneName = 'xxx';
  let sceneValue = '0';
  let result = batteryInfo.setBatteryConfig(sceneName, sceneValue);

  console.info("The result is: " + result);
  ```

## batteryInfo.getBatteryConfig<sup>11+</sup>

getBatteryConfig(sceneName: string): string

按场景名称查询电池配置。

**系统接口：** 此接口为系统接口。

**系统能力:** SystemCapability.PowerManager.BatteryManager.Core

**参数**：

| 参数名    | 类型   | 必填 | 说明         |
| --------- | ------ | ---- | ------------ |
| sceneName | string | 是   | 设置场景名称 |

**返回值**：

| 类型   | 说明                           |
| ------ | ------------------------------ |
| string | 返回电池充电配置，否则返回""。 |

**错误码：**

以下错误码的详细介绍请参见[电量信息错误码](errorcode-battery-info.md)。

| 错误码ID   | 错误信息    |
|---------|---------|
| 4900101 | If connecting to the service failed. |

**示例**：

  ```ts
  import batteryInfo from '@ohos.batteryInfo';

  let sceneName = 'xxx';
  let result = batteryInfo.getBatteryConfig(sceneName);

  console.info("The result is: " + result);
  ```

## batteryInfo.isBatteryConfigSupported<sup>11+</sup>

isBatteryConfigSupported(sceneName: string): boolean

检查是否按场景名称启用电池配置。

**系统接口：** 此接口为系统接口。

**系统能力:** SystemCapability.PowerManager.BatteryManager.Core

**参数**：

| 参数名    | 类型   | 必填 | 说明         |
| --------- | ------ | ---- | ------------ |
| sceneName | string | 是   | 设置场景名称 |

**返回值**：

| 类型    | 说明                                              |
| ------- | ------------------------------------------------- |
| boolean | 如果设备支持充电场景，则返回true，否则返回false。 |

**错误码：**

以下错误码的详细介绍请参见[电量信息错误码](errorcode-battery-info.md)。

| 错误码ID   | 错误信息    |
|---------|---------|
| 4900101 | If connecting to the service failed. |

**示例**：

  ```ts
  import batteryInfo from '@ohos.batteryInfo';

  let sceneName = 'xxx';
  let result = batteryInfo.isBatteryConfigSupported(sceneName);

  console.info("The result is: " + result);
  ```

## 属性

描述电池信息。

**系统能力**：SystemCapability.PowerManager.BatteryManager.Core

| 名称      | 类型        | 可读 | 可写 |  说明     |
| --------------- | ------------------- | ---- | ---- | ---------------------|
| estimatedRemainingChargeTime<sup>9+</sup> | number                                         | 是   | 否   | 表示当前设备充满电的预估时间，单位毫秒。此接口为系统接口。          |
| totalEnergy<sup>9+</sup>                  | number                                         | 是   | 否   | 表示当前设备电池的总容量，单位毫安时。此接口为系统接口。   |
| nowCurrent<sup>9+</sup>                   | number                                         | 是   | 否   | 表示当前设备电池的电流，单位毫安。此接口为系统接口。       |
| remainingEnergy<sup>9+</sup>              | number                                         | 是   | 否   | 表示当前设备电池的剩余容量，单位毫安时。此接口为系统接口。 |

