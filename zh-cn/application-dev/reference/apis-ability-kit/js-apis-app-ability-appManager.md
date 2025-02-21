# @ohos.app.ability.appManager (appManager)

appManager模块提供App管理的能力，包括查询当前是否处于稳定性测试场景、查询是否为ram受限设备、获取应用程序的内存大小、获取有关运行进程的信息等。

> **说明：**
> 
> 本模块首批接口从API version 9 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import appManager from '@ohos.app.ability.appManager';
```

## appManager.isRunningInStabilityTest

isRunningInStabilityTest(callback: AsyncCallback&lt;boolean&gt;): void

查询当前是否处于稳定性测试场景。使用callback异步回调。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

  | 参数名 | 类型 | 必填 | 说明 | 
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 |以回调方式返回接口运行结果及当前是否处于稳定性测试场景，可进行错误处理或其他自定义处理。true: 处于稳定性测试场景，false：处于非稳定性测试场景。  | 

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[元能力子系统错误码](errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

appManager.isRunningInStabilityTest((err, flag) => {
    if (err) {
        console.error(`isRunningInStabilityTest fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log(`The result of isRunningInStabilityTest is: ${JSON.stringify(flag)}`);
    }
});  
```


## appManager.isRunningInStabilityTest

isRunningInStabilityTest(): Promise&lt;boolean&gt;

查询当前是否处于稳定性测试场景。使用Promise异步回调。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

  | 类型 | 说明 | 
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 以Promise方式返回接口运行结果及当前是否处于稳定性测试场景，可进行错误处理或其他自定义处理。true: 处于稳定性测试场景，false：处于非稳定性测试场景。 | 

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[元能力子系统错误码](errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';
import { BusinessError } from '@ohos.base';

appManager.isRunningInStabilityTest().then((flag) => {
    console.log(`The result of isRunningInStabilityTest is: ${JSON.stringify(flag)}`);
}).catch((error: BusinessError) => {
    console.error(`error: ${JSON.stringify(error)}`);
});
```


## appManager.isRamConstrainedDevice

isRamConstrainedDevice(): Promise\<boolean>

查询是否为ram受限设备。使用Promise异步回调。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

  | 类型 | 说明 | 
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 以Promise方式返回接口运行结果及当前设备是否为ram受限设备，可进行错误处理或其他自定义处理。true：当前设备为ram受限设备，false：当前设备为非ram受限设备。 | 

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[元能力子系统错误码](errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';
import { BusinessError } from '@ohos.base';

appManager.isRamConstrainedDevice().then((data) => {
    console.log(`The result of isRamConstrainedDevice is: ${JSON.stringify(data)}`);
}).catch((error: BusinessError) => {
    console.error(`error: ${JSON.stringify(error)}`);
});
```

## appManager.isRamConstrainedDevice

isRamConstrainedDevice(callback: AsyncCallback\<boolean>): void

查询是否为ram受限设备。使用callback异步回调。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

  | 参数名 | 类型 | 必填 | 说明 | 
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 |以回调方式返回接口运行结果及当前设备是否为ram受限设备，可进行错误处理或其他自定义处理。true：当前设备为ram受限设备，false：当前设备为非ram受限设备。  | 

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[元能力子系统错误码](errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

appManager.isRamConstrainedDevice((err, data) => {
    if (err) {
        console.error(`isRamConstrainedDevice fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log(`The result of isRamConstrainedDevice is: ${JSON.stringify(data)}`);
    }
});
```

## appManager.getAppMemorySize

getAppMemorySize(): Promise\<number>

获取当前应用程序可以使用的内存的值。使用Promise异步回调。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

  | 类型 | 说明 | 
  | -------- | -------- |
  | Promise&lt;number&gt; | 获取当前应用程序可以使用的内存的值，可根据此值进行错误处理或其他自定义处理，单位是M。使用Promise异步回调。| 

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[元能力子系统错误码](errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';
import { BusinessError } from '@ohos.base';

appManager.getAppMemorySize().then((data) => {
    console.log(`The size of app memory is: ${JSON.stringify(data)}`);
}).catch((error: BusinessError) => {
    console.error(`error: ${JSON.stringify(error)}`);
});
```

## appManager.getAppMemorySize

getAppMemorySize(callback: AsyncCallback\<number>): void

获取当前应用程序可以使用的内存的值。使用callback异步回调。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

  | 参数名 | 类型 | 必填 | 说明 | 
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;number&gt; | 是 |获取当前应用程序可以使用的内存的值，可根据此值进行错误处理或其他自定义处理，单位是M。使用callback异步回调。| 

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[元能力子系统错误码](errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';

appManager.getAppMemorySize((err, data) => {
    if (err) {
        console.error(`getAppMemorySize fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log(`The size of app memory is: ${JSON.stringify(data)}`);
    }
});
```

## appManager.getRunningProcessInformation

getRunningProcessInformation(): Promise\<Array\<ProcessInformation>>

获取当前运行进程的有关信息。使用Promise异步回调。

> **说明：**
>
> API version 11之前的版本，该接口需要申请权限ohos.permission.GET_RUNNING_INFO（该权限仅系统应用可申请）。从API version 11开始，该接口不再需要申请权限。

**元服务API：** 从API version 11开始，该接口支持在元服务中使用。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise\<Array\<[ProcessInformation](js-apis-inner-application-processInformation.md)>> | 以Promise方式返回接口运行结果及有关运行进程的信息，可进行错误处理或其他自定义处理。 |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[元能力子系统错误码](errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';
import { BusinessError } from '@ohos.base';

appManager.getRunningProcessInformation().then((data) => {
    console.log(`The running process information is: ${JSON.stringify(data)}`);
}).catch((error: BusinessError) => {
    console.error(`error: ${JSON.stringify(error)}`);
});
```

## appManager.getRunningProcessInformation

getRunningProcessInformation(callback: AsyncCallback<Array\<ProcessInformation>>): void

获取当前运行进程的有关信息。使用callback异步回调。

**需要权限**：ohos.permission.GET_RUNNING_INFO

> **说明：**
>
> 从API version 11开始，该接口不再需要ohos.permission.GET_RUNNING_INFO权限。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 | 
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;Array\<[ProcessInformation](js-apis-inner-application-processInformation.md)>&gt; | 是 | 以回调方式返回接口运行结果及有关运行进程的信息，可进行错误处理或其他自定义处理。 | 

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 16000050 | Internal error. |

以上错误码详细介绍请参考[元能力子系统错误码](errorcode-ability.md)。

**示例：**

```ts
import appManager from '@ohos.app.ability.appManager';
import { BusinessError } from '@ohos.base';

appManager.getRunningProcessInformation((err, data) => {
    if (err) {
        console.error(`getRunningProcessInformation fail, err: ${JSON.stringify(err)}`);
    } else {
        console.log(`ProcessInformation: ${JSON.stringify(data)}`);
    }
});
```

## ProcessState<sup>10+</sup>

表示进程状态的枚举。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

| 名称                 | 值  | 说明                               |
| -------------------- | --- | --------------------------------- |
| STATE_CREATE    | 0   |      当进程在创建中的时候处于的状态。       |
| STATE_FOREGROUND          | 1   |            当进程切换到前台的时候处于的状态。      |
| STATE_ACTIVE  | 2   |          当进程在获焦的时候处于的状态。   |
| STATE_BACKGROUND        | 3   |       当进程处于后台不可见时处于的状态。           |
| STATE_DESTROY        | 4   |         当进程在销毁的时候处于的状态。         |
