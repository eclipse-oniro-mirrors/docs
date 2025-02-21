# @ohos.continuation.continuationManager (continuationManager)

continuationManager模块提供了流转/协同入口管理服务能力，包括连接/取消流转管理服务，注册/解注册设备连接变化监听，拉起设备选择模块，更新连接状态。

本模块接口用于拉起系统中的设备选择模块，由于该模块功能暂不完备，因此流转能力整体暂不支持用于应用开发。

> **说明：**
> 
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import continuationManager from '@ohos.continuation.continuationManager'
```

## continuationManager.register<sup>(deprecated)</sup>

register(callback: AsyncCallback\<number>): void;

注册流转管理服务，并获取对应的注册token，无过滤条件，使用AsyncCallback方式作为异步方法。

> 从API version 9开始不再维护，建议使用[registerContinuation](#continuationmanagerregistercontinuation9)替代。

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback\<number> | 是 | AsyncCallback形式返回流转管理服务连接后生成的token。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 3 | Failed to flatten the object. |
| 7 | The object is null. |
| 29360207 | The number of registrations has reached the upper limit. |

**示例：**

  ```ts
  let token = -1;
  continuationManager.register((err, data) => {
    if (err.code != 0) {
      console.error('register failed, cause: ' + JSON.stringify(err));
      return;
    }
    console.info('register finished, ' + JSON.stringify(data));
    token = data;
  });
  ```

## continuationManager.register<sup>(deprecated)</sup>

register(options: ContinuationExtraParams, callback: AsyncCallback\<number>): void;

连接流转管理服务，并获取对应的注册token，使用AsyncCallback方式作为异步方法。

> 从API version 9开始不再维护，建议使用[registerContinuation](#continuationmanagerregistercontinuation9)替代。

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | options | [ContinuationExtraParams](js-apis-continuation-continuationExtraParams.md) | 是 | 过滤可选择设备列表的额外参数。 |
  | callback | AsyncCallback\<number> | 是 | AsyncCallback形式返回流转管理服务连接后生成的token。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 3 | Failed to flatten the object. |
| 7 | The object is null. |
| 29360207 | The number of registrations has reached the upper limit. |
| 29360216 | Invalid continuation mode. |

**示例：**

  ```ts
  let token = -1;
  let continuationExtraParams = {
    deviceType: ["00E"]
  };
  continuationManager.register(continuationExtraParams, (err, data) => {
    if (err.code != 0) {
      console.error('register failed, cause: ' + JSON.stringify(err));
      return;
    }
    console.info('register finished, ' + JSON.stringify(data));
    token = data;
  });
  ```

## continuationManager.register<sup>(deprecated)</sup>

register(options?: ContinuationExtraParams): Promise\<number>;

连接流转管理服务，并获取对应的注册token，使用Promise方式作为异步方法。

> 从API version 9开始不再维护，建议使用[registerContinuation](#continuationmanagerregistercontinuation9)替代。

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | options | [ContinuationExtraParams](js-apis-continuation-continuationExtraParams.md) | 否 | 过滤可选择设备列表的额外参数，该参数可缺省|

**返回值：**

| 类型                        | 说明                 |
| ------------------------- | ------------------ |
| Promise\<number> | Promise形式返回流转管理服务连接后生成的token。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 3 | Failed to flatten the object |
| 7 | The object is null. |
| 29360207 | The number of registrations has reached the upper limit. |
| 29360216 | Invalid continuation mode. |

**示例：**

  ```ts
  let token = -1;
  let continuationExtraParams = {
    deviceType: ["00E"]
  };
  continuationManager.register(continuationExtraParams)
    .then((data) => {
      console.info('register finished, ' + JSON.stringify(data));
      token = data;
    })
    .catch((err) => {
      console.error('register failed, cause: ' + JSON.stringify(err));
    });
  ```

## continuationManager.registerContinuation<sup>9+</sup>

registerContinuation(callback: AsyncCallback\<number>): void;

注册流转管理服务，并获取对应的注册token，无过滤条件，使用AsyncCallback方式作为异步方法。

**需要权限**：ohos.permission.DISTRIBUTED_DATASYNC

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback\<number> | 是 | AsyncCallback形式返回流转管理服务连接后生成的token。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 16600001 | The system ability works abnormally. |
| 16600003 | The number of token registration times has reached the upper limit. |

**示例：**

  ```ts
  let token = -1;
  try {
    continuationManager.registerContinuation((err, data) => {
      if (err.code != 0) {
        console.error('registerContinuation failed, cause: ' + JSON.stringify(err));
        return;
      }
      console.info('registerContinuation finished, ' + JSON.stringify(data));
      token = data;
    });
  } catch (err) {
    console.error('registerContinuation failed, cause: ' + JSON.stringify(err));
  }
  ```

## continuationManager.registerContinuation<sup>9+</sup>

registerContinuation(options: ContinuationExtraParams, callback: AsyncCallback\<number>): void;

连接流转管理服务，并获取对应的注册token，使用AsyncCallback方式作为异步方法。

**需要权限**：ohos.permission.DISTRIBUTED_DATASYNC

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | options | [ContinuationExtraParams](js-apis-continuation-continuationExtraParams.md) | 是 | 过滤可选择设备列表的额外参数。 |
  | callback | AsyncCallback\<number> | 是 | AsyncCallback形式返回流转管理服务连接后生成的token。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 16600001 | The system ability works abnormally. |
| 16600003 | The number of token registration times has reached the upper limit. |

**示例：**

  ```ts
  let token = -1;
  let continuationExtraParams = {
    deviceType: ["00E"]
  };
  try {
    continuationManager.registerContinuation(continuationExtraParams, (err, data) => {
      if (err.code != 0) {
        console.error('registerContinuation failed, cause: ' + JSON.stringify(err));
        return;
      }
      console.info('registerContinuation finished, ' + JSON.stringify(data));
      token = data;
    });
  } catch (err) {
    console.error('registerContinuation failed, cause: ' + JSON.stringify(err));
  }
  ```

## continuationManager.registerContinuation<sup>9+</sup>

registerContinuation(options?: ContinuationExtraParams): Promise\<number>;

连接流转管理服务，并获取对应的注册token，使用Promise方式作为异步方法。

**需要权限**：ohos.permission.DISTRIBUTED_DATASYNC

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | options | [ContinuationExtraParams](js-apis-continuation-continuationExtraParams.md) | 否 | 过滤可选择设备列表的额外参数，该参数可缺省|

**返回值：**

| 类型                        | 说明                 |
| ------------------------- | ------------------ |
| Promise\<number> | Promise形式返回流转管理服务连接后生成的token。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 16600001 | The system ability works abnormally. |
| 16600003 | The number of token registration times has reached the upper limit. |

**示例：**

  ```ts
  let token = -1;
  let continuationExtraParams = {
    deviceType: ["00E"]
  };
  try {
    continuationManager.register(continuationExtraParams)
      .then((data) => {
        console.info('registerContinuation finished, ' + JSON.stringify(data));
        token = data;
      })
      .catch((err) => {
        console.error('registerContinuation failed, cause: ' + JSON.stringify(err));
      });
  } catch (err) {
    console.error('registerContinuation failed, cause: ' + JSON.stringify(err));
  }
  ```


## continuationManager.on("deviceConnect")<sup>(deprecated)</sup>

on(type: "deviceConnect", callback: Callback\<ContinuationResult>): void;

异步方法，监听设备连接状态，使用Callback形式返回连接的设备信息。

> 从API version 9开始不再维护，建议使用[on](#continuationmanagerondeviceselected9)替代。

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 监听的事件类型，固定值"deviceConnect"。 |
  | callback | Callback\<[ContinuationResult](js-apis-continuation-continuationResult.md)> | 是 | 当用户从设备选择模块中选择设备时调用，返回设备ID、设备类型和设备名称供开发者使用。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 3 | Failed to flatten the object |
| 7 | The object is null | 7 |
| 29360208 | The token is not registered. |
| 29360209 | The callback has been registered. |
| 29360214 | The type of callback is not supported. |

**示例：**

  ```ts
  continuationManager.on("deviceConnect", (data) => {
    console.info('onDeviceConnect deviceId: ' + JSON.stringify(data.id));
    console.info('onDeviceConnect deviceType: ' + JSON.stringify(data.type));
    console.info('onDeviceConnect deviceName: ' + JSON.stringify(data.name));
  });
  ```

## continuationManager.on("deviceDisconnect")<sup>(deprecated)</sup>

on(type: "deviceDisconnect", callback: Callback\<string>): void;

异步方法，监听设备断开状态，使用Callback形式返回断开的设备信息。

> 从API version 9开始不再维护，建议使用[on](#continuationmanagerondeviceunselected9)替代。

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 监听的事件类型，固定值"deviceDisconnect"。 |
  | callback | Callback\<string> | 是 | 当用户从设备选择模块中断开设备时调用，返回设备ID供开发者使用。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 3 | Failed to flatten the object. |
| 7 | The object is null. |
| 29360208 | The token is not registered. |
| 29360209 | The callback has been registered. |
| 29360214 | The type of callback is not supported. |

**示例：**

  ```ts
  continuationManager.on("deviceDisconnect", (data) => {
    console.info('onDeviceDisconnect deviceId: ' + JSON.stringify(data));
  });
  ```

## continuationManager.off("deviceConnect")<sup>(deprecated)</sup>

off(type: "deviceConnect", callback?: Callback\<ContinuationResult>): void;

异步方法，取消监听设备连接状态，使用Callback形式返回连接的设备信息。

> 从API version 9开始不再维护，建议使用[off](#continuationmanageroffdeviceselected9)替代。

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 取消监听的事件类型，固定值"deviceConnect"。 |
  | callback | Callback\<[ContinuationResult](js-apis-continuation-continuationResult.md)> | 否 | 当用户从设备选择模块中选择设备时调用，返回设备ID、设备类型和设备名称供开发者使用。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 3 | Failed to flatten the object. |
| 7 | The object is null. |
| 29360208 | The token is not registered. |
| 29360210 | The callback is not registered. |
| 29360214 | The type of callback is not supported. |

**示例：**

  ```ts
  continuationManager.off("deviceConnect", (data) => {
    console.info('onDeviceConnect deviceId: ' + JSON.stringify(data.id));
    console.info('onDeviceConnect deviceType: ' + JSON.stringify(data.type));
    console.info('onDeviceConnect deviceName: ' + JSON.stringify(data.name));
  });
  ```

## continuationManager.off("deviceDisconnect")<sup>(deprecated)</sup>

off(type: "deviceDisconnect", callback?: Callback\<string>): void;

异步方法，取消监听设备断开状态，使用Callback形式返回连接的设备信息。

> 从API version 9开始不再维护，建议使用[off](#continuationmanageroffdeviceunselected9)替代。

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 取消监听的事件类型，固定值"deviceDisconnect"。 |
  | callback | Callback\<string> | 否 | 当用户从设备选择模块中断开设备时调用，返回设备ID供开发者使用。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 3 | Failed to flatten the object. |
| 7 | The object is null. |
| 29360208 | The token is not registered. |
| 29360210 | The callback is not registered. |
| 29360214 | The type of callback is not supported. |

**示例：**

  ```ts
  continuationManager.off("deviceDisconnect", (data) => {
    console.info('onDeviceDisconnect deviceId: ' + JSON.stringify(data));
  });
  ```

## continuationManager.on("deviceSelected")<sup>9+</sup>

on(type: "deviceSelected", token: number, callback: Callback\<Array\<ContinuationResult>>): void;

异步方法，监听设备连接状态，使用Callback形式返回连接的设备信息。

**需要权限**：ohos.permission.DISTRIBUTED_DATASYNC

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 监听的事件类型，固定值"deviceSelected"。 |
  | token | number | 是 | 注册后的token。 |
  | callback | Callback\<Array\<[ContinuationResult](js-apis-continuation-continuationResult.md)>> | 是 | 当用户从设备选择模块中选择设备时调用，返回设备ID、设备类型和设备名称供开发者使用。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 16600001 | The system ability works abnormally. |
| 16600002 | The specified token or callback is not registered. |
| 16600004 | The specified callback has been registered. |

**示例：**

  ```ts
  let token = 1;
  try {
    continuationManager.on("deviceSelected", token, (data) => {
      console.info('onDeviceSelected len: ' + data.length);
      for (let i = 0; i < data.length; i++) {
        console.info('onDeviceSelected deviceId: ' + JSON.stringify(data[i].id));
        console.info('onDeviceSelected deviceType: ' + JSON.stringify(data[i].type));
        console.info('onDeviceSelected deviceName: ' + JSON.stringify(data[i].name));
      }
    });
  } catch (err) {
    console.error('on failed, cause: ' + JSON.stringify(err));
  }
  ```

## continuationManager.on("deviceUnselected")<sup>9+</sup>

on(type: "deviceUnselected", token: number, callback: Callback\<Array\<ContinuationResult>>): void;

异步方法，监听设备断开状态，使用Callback形式返回断开的设备信息。

**需要权限**：ohos.permission.DISTRIBUTED_DATASYNC

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 监听的事件类型，固定值"deviceUnselected"。 |
  | token | number | 是 | 注册后的token。 |
  | callback | Callback\<Array\<[ContinuationResult](js-apis-continuation-continuationResult.md)>> | 是 | 当用户从设备选择模块中断开设备时调用，返回设备ID、设备类型和设备名称供开发者使用。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 16600001 | The system ability works abnormally. |
| 16600002 | The specified token or callback is not registered. |
| 16600004 | The specified callback has been registered. |

**示例：**

  ```ts
  let token = 1;
  try {
    continuationManager.on("deviceUnselected", token, (data) => {
      console.info('onDeviceUnselected len: ' + data.length);
      for (let i = 0; i < data.length; i++) {
        console.info('onDeviceUnselected deviceId: ' + JSON.stringify(data[i].id));
        console.info('onDeviceUnselected deviceType: ' + JSON.stringify(data[i].type));
        console.info('onDeviceUnselected deviceName: ' + JSON.stringify(data[i].name));
      }
      console.info('onDeviceUnselected finished.');
    });
  } catch (err) {
    console.error('on failed, cause: ' + JSON.stringify(err));
  }
  ```

## continuationManager.off("deviceSelected")<sup>9+</sup>

off(type: "deviceSelected", token: number): void;

取消监听设备连接状态。

**需要权限**：ohos.permission.DISTRIBUTED_DATASYNC

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 取消监听的事件类型，固定值"deviceSelected"。 |
  | token | number | 是 | 注册后的token。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 16600001 | The system ability works abnormally. |
| 16600002 | The specified token or callback is not registered. |
| 16600004 | The specified callback has been registered. |

**示例：**

  ```ts
  let token = 1;
  try {
    continuationManager.off("deviceSelected", token);
  } catch (err) {
    console.error('off failed, cause: ' + JSON.stringify(err));
  }
  ```

## continuationManager.off("deviceUnselected")<sup>9+</sup>

off(type: "deviceUnselected", token: number): void;

取消监听设备断开状态。

**需要权限**：ohos.permission.DISTRIBUTED_DATASYNC

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 取消监听的事件类型，固定值"deviceUnselected"。 |
  | token | number | 是 | 注册后的token。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 16600001 | The system ability works abnormally. |
| 16600002 | The specified token or callback is not registered. |
| 16600004 | The specified callback has been registered. |

**示例：**

  ```ts
  let token = 1;
  try {
    continuationManager.off("deviceUnselected", token);
  } catch (err) {
    console.error('off failed, cause: ' + JSON.stringify(err));
  }
  ```

## continuationManager.startDeviceManager<sup>(deprecated)</sup>

startDeviceManager(token: number, callback: AsyncCallback\<void>): void;

拉起设备选择模块，可显示组网内可选择设备列表信息，无过滤条件，使用AsyncCallback方式作为异步方法。

> 从API version 9开始不再维护，建议使用[startContinuationDeviceManager](#continuationmanagerstartcontinuationdevicemanager9)替代。

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | token | number | 是 | 注册后的token。 |
  | callback | AsyncCallback\<void> | 是 | AsyncCallback形式返回接口调用结果。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 3 | Failed to flatten the object. |
| 7 | The object is null. |
| 29360208 | The token is not registered. |
| 29360210 | The callback is not registered. |
| 29360211 | Failed to connect to the ability. |
| 29360216 | Invalid continuation mode. |

**示例：**

  ```ts
  let token = 1;
  continuationManager.startDeviceManager(token, (err, data) => {
    if (err.code != 0) {
      console.error('startDeviceManager failed, cause: ' + JSON.stringify(err));
      return;
    }
    console.info('startDeviceManager finished, ' + JSON.stringify(data));
  });
  ```

## continuationManager.startDeviceManager<sup>(deprecated)</sup>

startDeviceManager(token: number, options: ContinuationExtraParams, callback: AsyncCallback\<void>): void;

拉起设备选择模块，可显示组网内可选择设备列表信息，使用AsyncCallback方式作为异步方法。

> 从API version 9开始不再维护，建议使用[startContinuationDeviceManager](#continuationmanagerstartcontinuationdevicemanager9)替代。

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | token | number | 是 | 注册后的token。 |
  | options | [ContinuationExtraParams](js-apis-continuation-continuationExtraParams.md) | 是 | 过滤可选择设备列表的额外参数。 |
  | callback | AsyncCallback\<void> | 是 | AsyncCallback形式返回接口调用结果。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 3 | Failed to flatten the object |
| 7 | The object is null |
| 29360208 | The token is not registered. |
| 29360210 | The callback is not registered. |
| 29360211 | Failed to connect to the ability. |
| 29360216 | Invalid continuation mode. |

**示例：**

  ```ts
  let token = 1;
  let continuationExtraParams = {
    deviceType: ["00E"]
  };
  continuationManager.startDeviceManager(token, continuationExtraParams, (err, data) => {
    if (err.code != 0) {
      console.error('startDeviceManager failed, cause: ' + JSON.stringify(err));
      return;
    }
    console.info('startDeviceManager finished, ' + JSON.stringify(data));
  });
  ```

## continuationManager.startDeviceManager<sup>(deprecated)</sup>

startDeviceManager(token: number, options?: ContinuationExtraParams): Promise\<void>;

拉起设备选择模块，可显示组网内可选择设备列表信息，使用Promise方式作为异步方法。

> 从API version 9开始不再维护，建议使用[startContinuationDeviceManager](#continuationmanagerstartcontinuationdevicemanager9)替代。

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | token | number | 是 | 注册后的token。 |
  | options | [ContinuationExtraParams](js-apis-continuation-continuationExtraParams.md) | 否 | 过滤可选择设备列表的额外参数，该参数可缺省|

**返回值：**

| 类型                        | 说明                 |
| ------------------------- | ------------------ |
| Promise\<void> | Promise形式返回接口调用结果。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 3 | Failed to flatten the object |
| 7 | The object is null |
| 29360208 | The token is not registered. |
| 29360210 | The callback is not registered. |
| 29360211 | Failed to connect to the ability. |
| 29360216 | Invalid continuation mode. |

**示例：**

  ```ts
  let token = 1;
  let continuationExtraParams = {
    deviceType: ["00E"]
  };
  continuationManager.startDeviceManager(token, continuationExtraParams)
    .then((data) => {
      console.info('startDeviceManager finished, ' + JSON.stringify(data));
    })
    .catch((err) => {
      console.error('startDeviceManager failed, cause: ' + JSON.stringify(err));
    });
  ```

## continuationManager.startContinuationDeviceManager<sup>9+</sup>

startContinuationDeviceManager(token: number, callback: AsyncCallback\<void>): void;

拉起设备选择模块，可显示组网内可选择设备列表信息，无过滤条件，使用AsyncCallback方式作为异步方法。

**需要权限**：ohos.permission.DISTRIBUTED_DATASYNC

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | token | number | 是 | 注册后的token。 |
  | callback | AsyncCallback\<void> | 是 | AsyncCallback形式返回接口调用结果。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 16600001 | The system ability works abnormally. |
| 16600002 | The specified token or callback is not registered. |

**示例：**

  ```ts
  let token = 1;
  try {
    continuationManager.startContinuationDeviceManager(token, (err, data) => {
      if (err.code != 0) {
        console.error('startContinuationDeviceManager failed, cause: ' + JSON.stringify(err));
        return;
      }
      console.info('startContinuationDeviceManager finished, ' + JSON.stringify(data));
    });
  } catch (err) {
    console.error('startContinuationDeviceManager failed, cause: ' + JSON.stringify(err));
  }
  ```

## continuationManager.startContinuationDeviceManager<sup>9+</sup>

startContinuationDeviceManager(token: number, options: ContinuationExtraParams, callback: AsyncCallback\<void>): void;

拉起设备选择模块，可显示组网内可选择设备列表信息，使用AsyncCallback方式作为异步方法。

**需要权限**：ohos.permission.DISTRIBUTED_DATASYNC

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | token | number | 是 | 注册后的token。 |
  | options | [ContinuationExtraParams](js-apis-continuation-continuationExtraParams.md) | 是 | 过滤可选择设备列表的额外参数。 |
  | callback | AsyncCallback\<void> | 是 | AsyncCallback形式返回接口调用结果。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 16600001 | The system ability works abnormally. |
| 16600002 | The specified token or callback is not registered. |

**示例：**

  ```ts
  let token = 1;
  let continuationExtraParams = {
    deviceType: ["00E"]
  };
  try {
    continuationManager.startContinuationDeviceManager(token, continuationExtraParams, (err, data) => {
      if (err.code != 0) {
        console.error('startContinuationDeviceManager failed, cause: ' + JSON.stringify(err));
        return;
      }
      console.info('startContinuationDeviceManager finished, ' + JSON.stringify(data));
    });
  } catch (err) {
    console.error('startContinuationDeviceManager failed, cause: ' + JSON.stringify(err));
  }
  ```

## continuationManager.startContinuationDeviceManager<sup>9+</sup>

startContinuationDeviceManager(token: number, options?: ContinuationExtraParams): Promise\<void>;

拉起设备选择模块，可显示组网内可选择设备列表信息，使用Promise方式作为异步方法。

**需要权限**：ohos.permission.DISTRIBUTED_DATASYNC

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | token | number | 是 | 注册后的token。 |
  | options | [ContinuationExtraParams](js-apis-continuation-continuationExtraParams.md) | 否 | 过滤可选择设备列表的额外参数，该参数可缺省|

**返回值：**

| 类型                        | 说明                 |
| ------------------------- | ------------------ |
| Promise\<void> | Promise形式返回接口调用结果。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 16600001 | The system ability works abnormally. |
| 16600002 | The specified token or callback is not registered. |

**示例：**

  ```ts
  let token = 1;
  let continuationExtraParams = {
    deviceType: ["00E"]
  };
  try {
    continuationManager.startContinuationDeviceManager(token, continuationExtraParams)
      .then((data) => {
        console.info('startContinuationDeviceManager finished, ' + JSON.stringify(data));
      })
      .catch((err) => {
        console.error('startContinuationDeviceManager failed, cause: ' + JSON.stringify(err));
      });
  } catch (err) {
    console.error('startContinuationDeviceManager failed, cause: ' + JSON.stringify(err));
  }
  ```

## continuationManager.updateConnectStatus<sup>(deprecated)</sup>

updateConnectStatus(token: number, deviceId: string, status: DeviceConnectState, callback: AsyncCallback\<void>): void;

通知设备选择模块，更新当前的连接状态，使用AsyncCallback方式作为异步方法。

> 从API version 9开始不再维护，建议使用[updateContinuationState](#continuationmanagerupdatecontinuationstate9)替代。

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | token | number | 是 | 注册后的token。 |
  | deviceId | string | 是 | 设备ID。 |
  | status | [DeviceConnectState](#deviceconnectstate) | 是 | 设备连接状态。 |
  | callback | AsyncCallback\<void> | 是 | AsyncCallback形式返回接口调用结果。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 3 | Failed to flatten the object. |
| 7 | The object is null. |
| 29360208 | The token is not registered. |
| 29360210 | The callback is not registered. |
| 29360211 | Failed to connect to the ability. |
| 29360215 | Invalid connection state. |

**示例：**

  ```ts
  let token = 1;
  let deviceId: string = "test deviceId";
  continuationManager.updateConnectStatus(token, deviceId, continuationManager.DeviceConnectState.CONNECTED, (err, data) => {
    if (err.code != 0) {
      console.error('updateConnectStatus failed, cause: ' + JSON.stringify(err));
      return;
    }
    console.info('updateConnectStatus finished, ' + JSON.stringify(data));
  });
  ```

## continuationManager.updateConnectStatus<sup>(deprecated)</sup>

updateConnectStatus(token: number, deviceId: string, status: DeviceConnectState): Promise\<void>;

通知设备选择模块，更新当前的连接状态，使用Promise方式作为异步方法。

> 从API version 9开始不再维护，建议使用[updateContinuationState](#continuationmanagerupdatecontinuationstate9)替代。

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | token | number | 是 | 注册后的token。 |
  | deviceId | string | 是 | 设备ID。 |
  | status | [DeviceConnectState](#deviceconnectstate) | 是 | 设备连接状态。 |

**返回值：**

| 类型                        | 说明                 |
| ------------------------- | ------------------ |
| Promise\<void> | Promise形式返回接口调用结果。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 3 | Failed to flatten the object. |
| 7 | The object is null. |
| 29360208 | The token is not registered. |
| 29360210 | The callback is not registered. |
| 29360211 | Failed to connect to the ability. |
| 29360215 | Invalid connection state. |

**示例：**

  ```ts
  let token = 1;
  let deviceId: string = "test deviceId";
  continuationManager.updateConnectStatus(token, deviceId, continuationManager.DeviceConnectState.CONNECTED)
    .then((data) => {
      console.info('updateConnectStatus finished, ' + JSON.stringify(data));
    })
    .catch((err) => {
      console.error('updateConnectStatus failed, cause: ' + JSON.stringify(err));
    });
  ```

## continuationManager.updateContinuationState<sup>9+</sup>

updateContinuationState(token: number, deviceId: string, status: DeviceConnectState, callback: AsyncCallback\<void>): void;

通知设备选择模块，更新当前的连接状态，使用AsyncCallback方式作为异步方法。

**需要权限**：ohos.permission.DISTRIBUTED_DATASYNC

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | token | number | 是 | 注册后的token。 |
  | deviceId | string | 是 | 设备ID。 |
  | status | [DeviceConnectState](#deviceconnectstate) | 是 | 设备连接状态。 |
  | callback | AsyncCallback\<void> | 是 | AsyncCallback形式返回接口调用结果。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 16600001 | The system ability works abnormally. |
| 16600002 | The specified token or callback is not registered. |

**示例：**

  ```ts
  let token = 1;
  let deviceId: string = "test deviceId";
  try {
    continuationManager.updateContinuationState(token, deviceId, continuationManager.DeviceConnectState.CONNECTED, (err, data) => {
      if (err.code != 0) {
        console.error('updateContinuationState failed, cause: ' + JSON.stringify(err));
        return;
      }
      console.info('updateContinuationState finished, ' + JSON.stringify(data));
    });
  } catch (err) {
    console.error('updateContinuationState failed, cause: ' + JSON.stringify(err));
  }
  ```

## continuationManager.updateContinuationState<sup>9+</sup>

updateContinuationState(token: number, deviceId: string, status: DeviceConnectState): Promise\<void>;

通知设备选择模块，更新当前的连接状态，使用Promise方式作为异步方法。

**需要权限**：ohos.permission.DISTRIBUTED_DATASYNC

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | token | number | 是 | 注册后的token。 |
  | deviceId | string | 是 | 设备ID。 |
  | status | [DeviceConnectState](#deviceconnectstate) | 是 | 设备连接状态。 |

**返回值：**

| 类型                        | 说明                 |
| ------------------------- | ------------------ |
| Promise\<void> | Promise形式返回接口调用结果。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 16600001 | The system ability works abnormally. |
| 16600002 | The specified token or callback is not registered. |

**示例：**

  ```ts
  let token = 1;
  let deviceId: string = "test deviceId";
  try {
    continuationManager.updateContinuationState(token, deviceId, continuationManager.DeviceConnectState.CONNECTED)
      .then((data) => {
        console.info('updateContinuationState finished, ' + JSON.stringify(data));
      })
      .catch((err) => {
        console.error('updateContinuationState failed, cause: ' + JSON.stringify(err));
      });
  } catch (err) {
    console.error('updateContinuationState failed, cause: ' + JSON.stringify(err));
  }
  ```


## continuationManager.unregister<sup>(deprecated)</sup>

unregister(token: number, callback: AsyncCallback\<void>): void;

解注册流转管理服务，传入注册时获取的token进行解注册，使用AsyncCallback方式作为异步方法。

> 从API version 9开始不再维护，建议使用[unregisterContinuation](#continuationmanagerunregistercontinuation9)替代。

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | token | number | 是 | 注册后的token。 |
  | callback | AsyncCallback\<void> | 是 | AsyncCallback形式返回接口调用结果。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 3 | Failed to flatten the object. |
| 7 | The object is null. |
| 29360208 | The token is not registered. |

**示例：**

  ```ts
  let token = 1;
  continuationManager.unregister(token, (err, data) => {
    if (err.code != 0) {
      console.error('unregister failed, cause: ' + JSON.stringify(err));
      return;
    }
    console.info('unregister finished, ' + JSON.stringify(data));
  });
  ```

## continuationManager.unregister<sup>(deprecated)</sup>

unregister(token: number): Promise\<void>;

解注册流转管理服务，传入注册时获取的token进行解注册，使用Promise方式作为异步方法。

> 从API version 9开始不再维护，建议使用[unregisterContinuation](#continuationmanagerunregistercontinuation9)替代。

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | token | number | 是 | 注册后的token。 |

**返回值：**

| 类型                        | 说明                 |
| ------------------------- | ------------------ |
| Promise\<void> | Promise形式返回接口调用结果。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 3 | Failed to flatten the object. |
| 7 | The object is null. |
| 29360208 | The token is not registered. |

**示例：**

  ```ts
  let token = 1;
  continuationManager.unregister(token)
    .then((data) => {
      console.info('unregister finished, ' + JSON.stringify(data));
    })
    .catch((err) => {
      console.error('unregister failed, cause: ' + JSON.stringify(err));
    });
  ```

## continuationManager.unregisterContinuation<sup>9+</sup>

unregisterContinuation(token: number, callback: AsyncCallback\<void>): void;

解注册流转管理服务，传入注册时获取的token进行解注册，使用AsyncCallback方式作为异步方法。

**需要权限**：ohos.permission.DISTRIBUTED_DATASYNC

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | token | number | 是 | 注册后的token。 |
  | callback | AsyncCallback\<void> | 是 | AsyncCallback形式返回接口调用结果。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 16600001 | The system ability works abnormally. |
| 16600002 | The specified token or callback is not registered. |

**示例：**

  ```ts
  let token = 1;
  try {
    continuationManager.unregisterContinuation(token, (err, data) => {
      if (err.code != 0) {
        console.error('unregisterContinuation failed, cause: ' + JSON.stringify(err));
        return;
      }
      console.info('unregisterContinuation finished, ' + JSON.stringify(data));
    });
  } catch (err) {
    console.error('unregisterContinuation failed, cause: ' + JSON.stringify(err));
  }
  ```

## continuationManager.unregisterContinuation<sup>9+</sup>

unregisterContinuation(token: number): Promise\<void>;

解注册流转管理服务，传入注册时获取的token进行解注册，使用Promise方式作为异步方法。

**需要权限**：ohos.permission.DISTRIBUTED_DATASYNC

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | token | number | 是 | 注册后的token。 |

**返回值：**

| 类型                        | 说明                 |
| ------------------------- | ------------------ |
| Promise\<void> | Promise形式返回接口调用结果。 |

**错误码：**

以下错误码的详细介绍请参见[分布式调度错误码](../errorcodes/errorcode-DistributedSchedule.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------------------------- |
| 16600001 | The system ability works abnormally. |
| 16600002 | The specified token or callback is not registered. |

**示例：**

  ```ts
  let token = 1;
  try {
    continuationManager.unregisterContinuation(token)
      .then((data) => {
        console.info('unregisterContinuation finished, ' + JSON.stringify(data));
      })
      .catch((err) => {
        console.error('unregisterContinuation failed, cause: ' + JSON.stringify(err));
      });
  } catch (err) {
    console.error('unregisterContinuation failed, cause: ' + JSON.stringify(err));
  }
  ```


## DeviceConnectState

设备连接状态。

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| IDLE | 0 | 设备连接初始状态。 |
| CONNECTING | 1 | 设备连接中状态。 |
| CONNECTED | 2 | 设备已连接状态。 |
| DISCONNECTING | 3 | 设备断开连接状态。 |

## ContinuationMode

设备选择模块连接模式。

**系统能力**：SystemCapability.Ability.DistributedAbilityManager

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| COLLABORATION_SINGLE | 0 | 设备选择模块单选模式。 |
| COLLABORATION_MULTIPLE | 1 | 设备选择模块多选模式。 |