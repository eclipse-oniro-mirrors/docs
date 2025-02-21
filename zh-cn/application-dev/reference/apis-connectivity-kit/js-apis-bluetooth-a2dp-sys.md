# @ohos.bluetooth.a2dp (蓝牙a2dp模块)（系统接口）

a2dp模块提供了访问蓝牙音频接口的方法。

> **说明：**
>
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> 当前页面仅包含本模块的系统接口，其他公开接口参见[@ohos.bluetooth.a2dp (蓝牙a2dp模块)](js-apis-bluetooth-a2dp.md)


## 导入模块

```js
import a2dp from '@ohos.bluetooth.a2dp';
```


### connect

connect(deviceId: string): void

发起设备的A2dp服务连接请求。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名    | 类型     | 必填   | 说明      |
| ------ | ------ | ---- | ------- |
| deviceId | string | 是    | 远端设备地址。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.               |
|2900003 | Bluetooth switch is off.       |
|2900004 | Profile is not supported.      |
|2900099 | Operation failed.              |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let a2dpSrc = a2dp.createA2dpSrcProfile();
    a2dpSrc.connect('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


### disconnect

disconnect(deviceId: string): void

断开设备的a2dp服务连接。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名    | 类型     | 必填   | 说明      |
| ------ | ------ | ---- | ------- |
| deviceId | string | 是    | 远端设备地址。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900004 | Profile is not supported.                |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let a2dpSrc = a2dp.createA2dpSrcProfile();
    a2dpSrc.disconnect('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```


### isAbsoluteVolumeSupported<sup>11+</sup>

isAbsoluteVolumeSupported(deviceId: string, callback: AsyncCallback&lt;boolean&gt;): void

获取设备是否支持绝对音量能力。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名    | 类型     | 必填   | 说明      |
| ------ | ------ | ---- | ------- |
| deviceId | string | 是    | 远端设备地址。 |
| callback | AsyncCallback&lt;boolean&gt; | 是 | 通过注册回调函数获取设备是否支持绝对音量。如果成功，值在supported中返回。 |


**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let a2dpSrc = a2dp.createA2dpSrcProfile();
    a2dpSrc.isAbsoluteVolumeSupported('XX:XX:XX:XX:XX:XX', (err, supported) => {
        console.info('device support absolute volume ' + supported);
    });
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```

### isAbsoluteVolumeSupported<sup>11+</sup>

isAbsoluteVolumeSupported(deviceId: string): Promise&lt;boolean&gt;

获取设备是否支持绝对音量能力。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名    | 类型     | 必填   | 说明      |
| ------ | ------ | ---- | ------- |
| deviceId | string | 是    | 远端设备地址。 |

**返回值：**

| 类型                            | 说明         |
| ----------------------------- | ---------- |
| Promise&lt;boolean&gt; | 通过promise形式获取设备是否支持绝对音量。如果成功，值在supported中返回。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let a2dpSrc = a2dp.createA2dpSrcProfile();
    a2dpSrc.isAbsoluteVolumeSupported('XX:XX:XX:XX:XX:XX').then((supported) => {
        console.info('device support absolute volume ' + supported);
    });
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```

### isAbsoluteVolumeEnabled<sup>11+</sup>

isAbsoluteVolumeEnabled(deviceId: string, callback: AsyncCallback&lt;boolean&gt;): void

获取设备绝对音量能力是否开启。需要在设备支持绝对音量的情况下（参考[isAbsoluteVolumeSupported](#isabsolutevolumesupported11)），再获取设备绝对音量能力是否开启。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名    | 类型     | 必填   | 说明      |
| ------ | ------ | ---- | ------- |
| deviceId | string | 是    | 远端设备地址。 |
| callback | AsyncCallback&lt;boolean&gt; | 是 | 通过注册回调函数获取设备绝对音量是否开启。如果成功，值在enabled中返回。 |


**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let a2dpSrc = a2dp.createA2dpSrcProfile();
    a2dpSrc.isAbsoluteVolumeEnabled('XX:XX:XX:XX:XX:XX', (err, enabled) => {
        console.info('device absolute volume enable ' + enabled);
    });
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```

### isAbsoluteVolumeEnabled<sup>11+</sup>

isAbsoluteVolumeEnabled(deviceId: string): Promise&lt;boolean&gt;

获取设备绝对音量能力是否开启。需要在设备支持绝对音量的情况下（参考[isAbsoluteVolumeSupported](#isabsolutevolumesupported11)），再获取设备绝对音量能力是否开启。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名    | 类型     | 必填   | 说明      |
| ------ | ------ | ---- | ------- |
| deviceId | string | 是    | 远端设备地址。 |

**返回值：**

| 类型                            | 说明         |
| ----------------------------- | ---------- |
| Promise&lt;boolean&gt; | 通过promise形式获取设备绝对音量是否开启。如果成功，值在enabled中返回。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let a2dpSrc = a2dp.createA2dpSrcProfile();
    a2dpSrc.isAbsoluteVolumeEnabled('XX:XX:XX:XX:XX:XX').then((enabled) => {
        console.info('device absolute volume enable ' + enabled);
    });
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```

### enableAbsoluteVolume<sup>11+</sup>

enableAbsoluteVolume(deviceId: string, callback: AsyncCallback&lt;void&gt;): void

开启设备绝对音量能力。需要在设备支持绝对音量的情况下（参考[isAbsoluteVolumeSupported](#isabsolutevolumesupported11)），再开启设备绝对音量能力。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH 和 ohos.permission.MANAGE_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名    | 类型     | 必填   | 说明      |
| ------ | ------ | ---- | ------- |
| deviceId | string | 是    | 远端设备地址。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。如果成功，err为undefined，否则为错误对象。 |


**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let a2dpSrc = a2dp.createA2dpSrcProfile();
    a2dpSrc.enableAbsoluteVolume('XX:XX:XX:XX:XX:XX', (err) => {
        if (err) {
            console.error("enableAbsoluteVolume error");
        }
    });
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```

### enableAbsoluteVolume<sup>11+</sup>

enableAbsoluteVolume(deviceId: string): Promise&lt;void&gt;

开启设备绝对音量能力。需要在设备支持绝对音量的情况下（参考[isAbsoluteVolumeSupported](#isabsolutevolumesupported11)），再开启设备绝对音量能力。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH 和 ohos.permission.MANAGE_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名    | 类型     | 必填   | 说明      |
| ------ | ------ | ---- | ------- |
| deviceId | string | 是    | 远端设备地址。 |

**返回值：**

| 类型                            | 说明         |
| ----------------------------- | ---------- |
| Promise&lt;void&gt; | 以Promise的形式返回结果。如果成功，err为undefined，否则为错误对象。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let a2dpSrc = a2dp.createA2dpSrcProfile();
    a2dpSrc.enableAbsoluteVolume('XX:XX:XX:XX:XX:XX').then(() => {
            console.info("enableAbsoluteVolume");
        }
    );
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```

### disableAbsoluteVolume<sup>11+</sup>

disableAbsoluteVolume(deviceId: string, callback: AsyncCallback&lt;void&gt;): void

关闭设备绝对音量能力。需要在设备支持绝对音量的情况下（参考[isAbsoluteVolumeSupported](#isabsolutevolumesupported11)），再关闭设备绝对音量能力。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH 和 ohos.permission.MANAGE_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名    | 类型     | 必填   | 说明      |
| ------ | ------ | ---- | ------- |
| deviceId | string | 是    | 远端设备地址。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数。如果成功，err为undefined，否则为错误对象。 |


**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let a2dpSrc = a2dp.createA2dpSrcProfile();
    a2dpSrc.disableAbsoluteVolume('XX:XX:XX:XX:XX:XX', (err) => {
        if (err) {
            console.error("disableAbsoluteVolume error");
        }
    });
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```

### disableAbsoluteVolume<sup>11+</sup>

disableAbsoluteVolume(deviceId: string): Promise&lt;void&gt;

关闭设备绝对音量能力。需要在设备支持绝对音量的情况下（参考[isAbsoluteVolumeSupported](#isabsolutevolumesupported11)），再关闭设备绝对音量能力。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH 和 ohos.permission.MANAGE_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名    | 类型     | 必填   | 说明      |
| ------ | ------ | ---- | ------- |
| deviceId | string | 是    | 远端设备地址。 |

**返回值：**

| 类型                            | 说明         |
| ----------------------------- | ---------- |
| Promise&lt;void&gt; | 以Promise的形式返回结果。如果成功，err为undefined，否则为错误对象。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let a2dpSrc = a2dp.createA2dpSrcProfile();
    a2dpSrc.disableAbsoluteVolume('XX:XX:XX:XX:XX:XX').then(() => {
        console.info("disableAbsoluteVolume");
    });
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```

### getCurrentCodecInfo<sup>11+</sup>

getCurrentCodecInfo(deviceId: string): CodecInfo

获取当前编码器信息。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名    | 类型     | 必填   | 说明      |
| ------ | ------ | ---- | ------- |
| deviceId | string | 是    | 远端设备地址。 |

**返回值：**

| 类型                            | 说明         |
| ----------------------------- | ---------- |
| [CodecInfo](js-apis-bluetooth-a2dp#codecinfo11)| 当前编码器信息。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let a2dpSrc = a2dp.createA2dpSrcProfile();
    let codecInfo : a2dp.CodecInfo = a2dpSrc.getCurrentCodecInfo('XX:XX:XX:XX:XX:XX');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```

### setCurrentCodecInfo<sup>11+</sup>

setCurrentCodecInfo(deviceId: string, codecInfo: CodecInfo): void

设置当前编码器信息。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.ACCESS_BLUETOOTH 和 ohos.permission.MANAGE_BLUETOOTH

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**参数：**

| 参数名    | 类型     | 必填   | 说明      |
| ------ | ------ | ---- | ------- |
| deviceId | string | 是    | 远端设备地址。 |
| codecInfo | [CodecInfo](js-apis-bluetooth-a2dp.md#codecinfo11) | 是    | 编码器信息。 |

**错误码**：

以下错误码的详细介绍请参见[蓝牙服务子系统错误码](errorcode-bluetoothManager.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------- |
|2900001 | Service stopped.                         |
|2900003 | Bluetooth switch is off.                 |
|2900099 | Operation failed.                        |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let a2dpSrc = a2dp.createA2dpSrcProfile();
    let codecInfo : a2dp.CodecInfo = {
        codecType: 0,
        codecBitsPerSample: 1,
        codecChannelMode: 2,
        codecSampleRate: 1,
    }
    a2dpSrc.setCurrentCodecInfo('XX:XX:XX:XX:XX:XX', codecInfo);
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```

