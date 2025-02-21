# @ohos.enterprise.wifiManager（WiFi管理）(系统接口)

本模块提供企业设备WiFi管理能力，包括查询WiFi开启状态等。

> **说明：**
>
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>
> 本模块接口仅可在Stage模型下使用。
>
> 本模块接口仅对[设备管理应用](../../mdm/mdm-kit-guide.md#功能介绍)开放，需将[设备管理应用激活](js-apis-enterprise-adminManager-sys.md#adminmanagerenableadmin)后调用，实现相应功能。
>
> 当前页面仅包含本模块的系统接口，其他公开接口参见。其他公开接口参见[@ohos.enterprise.wifiManager](js-apis-enterprise-wifiManager.md)。

## 导入模块

```ts
import { wifiManager } from '@kit.MDMKit';
```

## wifiManager.isWifiActive

isWifiActive(admin: Want, callback: AsyncCallback&lt;boolean&gt;): void

指定设备管理应用查询wifi开启状态。使用callback异步回调。

**需要权限：** ohos.permission.ENTERPRISE_SET_WIFI

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**参数：**

| 参数名      | 类型                                       | 必填   | 说明                       |
| -------- | ---------------------------------------- | ---- | ------------------------------- |
| admin    | [Want](../apis-ability-kit/js-apis-app-ability-want.md)     | 是    | 设备管理应用。                  |
| callback | AsyncCallback&lt;boolean&gt;            | 是    | 回调函数，当接口调用成功，err为null，data为boolean值，true表示wifi开启，false表示wifi关闭，否则err为错误对象。       |

**错误码**：

以下的错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)和[通用错误码](../errorcode-universal.md)。

| 错误码ID | 错误信息                                                                       |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | The application is not an administrator application of the device.            |
| 9200002 | The administrator application does not have permission to manage the device. |
| 201 | Permission verification failed. The application does not have the permission required to call the API. |
| 202 | Permission verification failed. A non-system application calls a system API. |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |

**示例：**

```ts
import { Want } from '@kit.AbilityKit';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};

wifiManager.isWifiActive(wantTemp, (err, result) => {
  if (err) {
    console.error(`Failed to query is wifi active or not. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info(`Succeeded in query is wifi active or not, result : ${result}`);
});
```

## wifiManager.isWifiActive

isWifiActive(admin: Want): Promise&lt;boolean&gt;

指定设备管理应用获取wifi开启状态。使用Promise异步回调。

**需要权限：** ohos.permission.ENTERPRISE_SET_WIFI

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**参数：**

| 参数名   | 类型                                  | 必填   | 说明      |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 设备管理应用。 |

**返回值：**

| 类型                   | 说明                      |
| --------------------- | ------------------------- |
| Promise&lt;boolean&gt; | Promise结果，返回wifi开启状态，true表示wifi开启，false表示wifi关闭。  |

**错误码**：

以下的错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)和[通用错误码](../errorcode-universal.md)。

| 错误码ID | 错误信息                                                                     |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | The application is not an administrator application of the device.            |
| 9200002 | The administrator application does not have permission to manage the device. |
| 201 | Permission verification failed. The application does not have the permission required to call the API. |
| 202 | Permission verification failed. A non-system application calls a system API. |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |

**示例：**

```ts
import { Want } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};

wifiManager.isWifiActive(wantTemp).then((result) => {
  console.info(`Succeeded in query is wifi active or not, result : ${result}`);
}).catch((err: BusinessError) => {
  console.error(`Failed to query is wifi active or not. Code: ${err.code}, message: ${err.message}`);
});
```

## wifiManager.setWifiProfile

setWifiProfile(admin: Want, profile: WifiProfile, callback: AsyncCallback&lt;void&gt;): void

指定设备管理应用为设备配置wifi，使连接到指定网络。使用callback异步回调。

**需要权限：** ohos.permission.ENTERPRISE_SET_WIFI

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**参数：**

| 参数名      | 类型                                       | 必填   | 说明                       |
| -------- | ---------------------------------------- | ---- | ------------------------------- |
| admin    | [Want](../apis-ability-kit/js-apis-app-ability-want.md)     | 是    | 设备管理应用。                  |
| profile    | [WifiProfile](js-apis-enterprise-wifiManager.md#wifiprofile) | 是    | WLAN配置信息。                  |
| callback | AsyncCallback&lt;void&gt;            | 是    | 回调函数，当接口调用成功，err为null，否则为错误对象。      |

**错误码**：

以下的错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)和[通用错误码](../errorcode-universal.md)。

| 错误码ID | 错误信息                                                                       |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | The application is not an administrator application of the device.            |
| 9200002 | The administrator application does not have permission to manage the device. |
| 201 | Permission verification failed. The application does not have the permission required to call the API. |
| 202 | Permission verification failed. A non-system application calls a system API. |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |

**示例：**

```ts
import { Want } from '@kit.AbilityKit';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};
let profile: wifiManager.WifiProfile = {
  'ssid': 'name',
  'preSharedKey': 'passwd',
  'securityType': wifiManager.WifiSecurityType.WIFI_SEC_TYPE_PSK
};

wifiManager.setWifiProfile(wantTemp, profile, (err) => {
  if (err) {
    console.error(`Failed to set wifi profile. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info('Succeeded in setting wifi profile');
});
```

## wifiManager.setWifiProfile

setWifiProfile(admin: Want, profile: WifiProfile): Promise&lt;void&gt;

指定设备管理应用为设备配置wifi，使连接到指定网络。使用Promise异步回调。

**需要权限：** ohos.permission.ENTERPRISE_SET_WIFI

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**参数：**

| 参数名   | 类型                                  | 必填   | 说明      |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 设备管理应用。 |
| profile    | [WifiProfile](js-apis-enterprise-wifiManager.md#wifiprofile) | 是    | WLAN配置信息。                  |

**返回值：**

| 类型                   | 说明                      |
| --------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。当配置wifi连接到指定网络失败时会抛出错误对象。 |

**错误码**：

以下的错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)和[通用错误码](../errorcode-universal.md)。

| 错误码ID | 错误信息                                                                     |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | The application is not an administrator application of the device.            |
| 9200002 | The administrator application does not have permission to manage the device. |
| 201 | Permission verification failed. The application does not have the permission required to call the API. |
| 202 | Permission verification failed. A non-system application calls a system API. |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |

**示例：**

```ts
import { Want } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};
let profile: wifiManager.WifiProfile = {
  'ssid': 'name',
  'preSharedKey': 'passwd',
  'securityType': wifiManager.WifiSecurityType.WIFI_SEC_TYPE_PSK
};

wifiManager.setWifiProfile(wantTemp, profile).then(() => {
  console.info('Succeeded in setting wifi profile');
}).catch((err: BusinessError) => {
  console.error(`Failed to set wifi profile. Code: ${err.code}, message: ${err.message}`);
});
```

## wifiManager.isWifiDisabled<sup>11+</sup>

isWifiDisabled(admin: Want): boolean

指定设备管理应用查询wifi是否被禁用。

**需要权限：** ohos.permission.ENTERPRISE_MANAGE_WIFI

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager

**系统API：** 此接口为系统接口。

**参数：**

| 参数名   | 类型                                  | 必填   | 说明      |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 设备管理应用。 |

**返回值：**

| 类型                   | 说明                      |
| --------------------- | ------------------------- |
| boolean | 返回wifi禁用状态，true表示wifi被禁用，false表示wifi未被禁用。 |

**错误码：**

以下的错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)和[通用错误码](../errorcode-universal.md)。

| 错误码ID | 错误信息                                                                     |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | The application is not an administrator application of the device.            |
| 9200002 | The administrator application does not have permission to manage the device. |
| 201 | Permission verification failed. The application does not have the permission required to call the API. |
| 202 | Permission verification failed. A non-system application calls a system API. |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |

**示例：**

```ts
import { Want } from '@kit.AbilityKit';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};
try {
  let result: boolean = wifiManager.isWifiDisabled(wantTemp);
  console.info(`Succeeded in query the wifi is disabled or not, result : ${result}`);
} catch (err) {
  console.error(`Failed to query the wifi is disabled or not. Code: ${err.code}, message: ${err.message}`);
};
```

## wifiManager.setWifiDisabled<sup>11+</sup>

setWifiDisabled(admin: Want, disabled: boolean): void

指定设备管理应用设置禁用wifi策略。

**需要权限：** ohos.permission.ENTERPRISE_MANAGE_WIFI

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager

**系统API：** 此接口为系统接口。

**参数：**

| 参数名     | 类型                                | 必填 | 说明                                      |
| ---------- | ----------------------------------- | ---- | ----------------------------------------- |
| admin      | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是   | 设备管理应用。                            |
| disabled   | boolean                             | 是   | true表示禁用wifi，false表示解除wifi禁用。 |

**错误码：**

以下的错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)和[通用错误码](../errorcode-universal.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 9200001  | The application is not an administrator application of the device. |
| 9200002  | The administrator application does not have permission to manage the device. |
| 201      | Permission verification failed. The application does not have the permission required to call the API. |
| 202      | Permission verification failed. A non-system application calls a system API. |
| 401      | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |

**示例：**

```ts
import { Want } from '@kit.AbilityKit';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};

try {
  wifiManager.setWifiDisabled(wantTemp, true);
  console.info('Succeeded in set the wifi disabled');
} catch (err) {
  console.error(`Failed to set the wifi disabled. Code: ${err.code}, message: ${err.message}`);
};
```
