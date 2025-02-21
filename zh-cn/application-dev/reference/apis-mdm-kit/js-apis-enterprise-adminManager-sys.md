# @ohos.enterprise.adminManager (企业设备管理)(系统接口)

本模块提供企业设备管理能力，使设备具备企业场景下所需的定制能力。

> **说明：**
>
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>
> 本模块接口仅对[设备管理应用](enterpriseDeviceManagement-overview.md#基本概念)开放，实现相应功能。
> 
> 本模块接口均为系统接口。

## 导入模块

```ts
import adminManager from '@ohos.enterprise.adminManager';
```

## adminManager.enableAdmin

enableAdmin(admin: Want, enterpriseInfo: EnterpriseInfo, type: AdminType, callback: AsyncCallback\<void>): void

激活当前用户下指定的设备管理应用，其中超级设备管理应用仅能在管理员用户下被激活。使用callback异步回调。

**需要权限：** ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数**：

| 参数名            | 类型                                  | 必填   | 说明                 |
| -------------- | ----------------------------------- | ---- | ------------------ |
| admin          | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 设备管理应用。            |
| enterpriseInfo | [EnterpriseInfo](#enterpriseinfo)   | 是    | 设备管理应用的企业信息。      |
| type           | [AdminType](#admintype)             | 是    | 激活的设备管理应用类型。         |
| callback       | AsyncCallback\<void>                | 是    | 回调函数，当接口调用成功，err为null，否则为错误对象。 |

**错误码**：

以下错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)。

| 错误码ID | 错误信息                                                         |
| ------- | --------------------------------------------------------------- |
| 9200003 | the administrator ability component is invalid.                 |
| 9200004 | failed to enable the administrator application of the device.   |
| 9200007 | the system ability work abnormally.                             |

**示例**：

```ts
import Want from '@ohos.app.ability.Want';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};
let enterpriseInfo: adminManager.EnterpriseInfo = {
  name: 'enterprise name',
  description: 'enterprise description'
}

adminManager.enableAdmin(wantTemp, enterpriseInfo, adminManager.AdminType.ADMIN_TYPE_SUPER, (err) => {
  if (err) {
    console.error(`Failed to enable admin. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info('Succeeded in enabling admin');
});
```

## adminManager.enableAdmin

enableAdmin(admin: Want, enterpriseInfo: EnterpriseInfo, type: AdminType, userId: number, callback: AsyncCallback\<void>): void

激活指定用户（通过userId指定）下指定的设备管理应用，其中超级管理应用仅能在管理员用户下被激活。使用callback异步回调。

**需要权限：** ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数**：

| 参数名            | 类型                                  | 必填   | 说明                           |
| -------------- | ----------------------------------- | ---- | ---------------------------- |
| admin          | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 设备管理应用。                      |
| enterpriseInfo | [EnterpriseInfo](#enterpriseinfo)   | 是    | 设备管理应用的企业信息。                 |
| type           | [AdminType](#admintype)             | 是    | 激活的设备管理应用类型。                  |
| userId         | number                              | 是    | 用户ID，指定具体用户，取值范围：大于等于0。<br>默认值：调用方所在用户。 |
| callback       | AsyncCallback\<void>                | 是    | 回调函数，当接口调用成功，err为null，否则为错误对象。       |

**错误码**:

以下错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)。

| 错误码ID | 错误信息                                                         |
| ------- | --------------------------------------------------------------- |
| 9200003 | the administrator ability component is invalid.                 |
| 9200004 | failed to enable the administrator application of the device.   |
| 9200007 | the system ability work abnormally.                             |

**示例**：

```ts
import Want from '@ohos.app.ability.Want';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};
let enterpriseInfo: adminManager.EnterpriseInfo = {
  name: 'enterprise name',
  description: 'enterprise description'
}

adminManager.enableAdmin(wantTemp, enterpriseInfo, adminManager.AdminType.ADMIN_TYPE_NORMAL, 100, (err) => {
  if (err) {
    console.error(`Failed to enable admin. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info('Succeeded in enabling admin');
});
```

## adminManager.enableAdmin

enableAdmin(admin: Want, enterpriseInfo: EnterpriseInfo, type: AdminType, userId?: number): Promise\<void>

激活当前/指定用户下指定的设备管理应用，其中超级管理应用仅能在管理员用户下被激活。使用promise异步回调。

**需要权限：** ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数**：

| 参数名            | 类型                                  | 必填   | 说明                           |
| -------------- | ----------------------------------- | ---- | ---------------------------- |
| admin          | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 设备管理应用。                      |
| enterpriseInfo | [EnterpriseInfo](#enterpriseinfo)   | 是    | 设备管理应用的企业信息。                 |
| type           | [AdminType](#admintype)             | 是    | 激活的设备管理应用类型。                   |
| userId         | number                              | 否    | 用户ID，取值范围：大于等于0。<br> - 调用接口时，若传入userId，表示指定用户。<br> - 调用接口时，若未传入userId，表示当前用户。|

**返回值：**

| 类型                | 说明                |
| ----------------- | ----------------- |
| Promise\<void>    | 无返回结果的Promise对象。当激活设备管理应用失败时，会抛出错误对象。 |

**错误码**：

以下错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)。

| 错误码ID | 错误信息                                                         |
| ------- | --------------------------------------------------------------- |
| 9200003 | the administrator ability component is invalid.                 |
| 9200004 | failed to enable the administrator application of the device.   |
| 9200007 | the system ability work abnormally.                             |

**示例**：

```ts
import Want from '@ohos.app.ability.Want';
import { BusinessError } from '@ohos.base';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};
let enterpriseInfo: adminManager.EnterpriseInfo = {
  name: 'enterprise name',
  description: 'enterprise description'
}

adminManager.enableAdmin(wantTemp, enterpriseInfo, adminManager.AdminType.ADMIN_TYPE_NORMAL, 100).catch(
  (err: BusinessError) => {
    console.error(`Failed to enable admin. Code: ${err.code}, message: ${err.message}`);
  });
```

## adminManager.disableAdmin

disableAdmin(admin: Want, callback: AsyncCallback\<void>): void

将当前用户下指定的普通设备管理应用去激活。使用callback异步回调。

**需要权限：** ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数**：

| 参数名      | 类型                                  | 必填   | 说明                  |
| -------- | ----------------------------------- | ---- | ------------------- |
| admin    | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 普通设备管理应用。           |
| callback | AsyncCallback\<void>                | 是    | 回调函数，当接口调用成功，err为null，否则为错误对象。 |

**错误码**:

以下的错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)。

| 错误码ID | 错误信息                                                           |
| ------- | ----------------------------------------------------------------- |
| 9200005 | failed to disable the administrator application of the device.    |

**示例**：

```ts
import Want from '@ohos.app.ability.Want';
let wantTemp: Want = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

adminManager.disableAdmin(wantTemp, (err) => {
  if (err) {
    console.error(`Failed to disable admin. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info('Succeeded in disabling admin');
});
```

## adminManager.disableAdmin

disableAdmin(admin: Want, userId: number, callback: AsyncCallback\<void>): void

将指定用户（通过userId指定）下指定的普通管理应用去激活。使用callback异步回调。

**需要权限：** ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数**：

| 参数名      | 类型                                  | 必填   | 说明                           |
| -------- | ----------------------------------- | ---- | ---------------------------- |
| admin    | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 普通设备管理应用。                    |
| userId   | number                              | 是    | 用户ID，指定具体用户，取值范围：大于等于0。<br>默认值：当前用户。 |
| callback | AsyncCallback\<void>                | 是    | 回调函数，当接口调用成功，err为null，否则为错误对象。        |

**错误码**:

以下错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)。

| 错误码ID | 错误信息                                                           |
| ------- | ----------------------------------------------------------------- |
| 9200005 | failed to disable the administrator application of the device.    |

**示例**：

```ts
import Want from '@ohos.app.ability.Want';
let wantTemp: Want = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

adminManager.disableAdmin(wantTemp, 100, (err) => {
  if (err) {
    console.error(`Failed to disable admin. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info('Succeeded in disabling admin');
});
```

## adminManager.disableAdmin

disableAdmin(admin: Want, userId?: number): Promise\<void>

将当前/指定用户下指定的普通管理应用去激活。使用promise异步回调。

**需要权限：** ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数**：

| 参数名    | 类型                                  | 必填   | 说明                           |
| ------ | ----------------------------------- | ---- | ---------------------------- |
| admin  | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 普通设备管理应用。                    |
| userId | number                              | 否    | 用户ID， 取值范围：大于等于0。<br> - 调用接口时，若传入userId，表示指定用户。<br> - 调用接口时，若未传入userId，表示当前用户。|

**返回值：**

| 类型                | 说明                |
| ----------------- | ----------------- |
| Promise\<void>    | 无返回结果的Promise对象。当去激活普通管理应用失败时，会抛出错误对象。 |

**错误码**:

以下错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)。

| 错误码ID | 错误信息                                                           |
| ------- | ----------------------------------------------------------------- |
| 9200005 | failed to disable the administrator application of the device.    |

**示例**：

```ts
import Want from '@ohos.app.ability.Want';
import { BusinessError } from '@ohos.base';
let wantTemp: Want = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

adminManager.disableAdmin(wantTemp, 100).catch((err: BusinessError) => {
  console.error(`Failed to disable admin. Code: ${err.code}, message: ${err.message}`);
});
```

## adminManager.disableSuperAdmin

disableSuperAdmin(bundleName: String, callback: AsyncCallback\<void>): void

根据bundleName将管理员用户下的超级设备管理应用去激活。使用callback异步回调。

**需要权限：** ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数**：

| 参数名        | 类型                      | 必填   | 说明                  |
| ---------- | ----------------------- | ---- | ------------------- |
| bundleName | String                  | 是    | 超级设备管理应用的包名。        |
| callback   | AsyncCallback\<void>    | 是    | 回调函数，当接口调用成功，err为null，否则为错误对象。 |

**错误码**:

以下的错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)。

| 错误码ID | 错误信息                                                           |   
| ------- | ----------------------------------------------------------------- |
| 9200005 | failed to disable the administrator application of the device.    |

**示例**：

```ts
import Want from '@ohos.app.ability.Want';
let bundleName: string = 'com.example.myapplication';

adminManager.disableSuperAdmin(bundleName, (err) => {
  if (err) {
    console.error(`Failed to disable super admin. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info('Succeeded in disabling super admin');
});
```

## adminManager.disableSuperAdmin

disableSuperAdmin(bundleName: String): Promise\<void>

根据bundleName将管理员用户下的超级设备管理应用去激活。使用promise异步回调。

**需要权限：** ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数**：

| 参数名        | 类型     | 必填   | 说明           |
| ---------- | ------ | ---- | ------------ |
| bundleName | String | 是    | 超级设备管理应用的包名。 |

**返回值：**

| 类型                | 说明                |
| ----------------- | ----------------- |
| Promise\<void>    | 无返回结果的Promise对象。当去激活超级设备管理应用失败时，会抛出错误对象。 |

**错误码**:

以下错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)。

| 错误码ID | 错误信息                                                           |
| ------- | ----------------------------------------------------------------- |
| 9200005 | failed to disable the administrator application of the device.    |

**示例**：

```ts
import Want from '@ohos.app.ability.Want';
import { BusinessError } from '@ohos.base';
let bundleName: string = 'com.example.myapplication';

adminManager.disableSuperAdmin(bundleName).catch((err: BusinessError) => {
  console.error(`Failed to disable super admin. Code: ${err.code}, message: ${err.message}`);
});
```

## adminManager.isAdminEnabled

isAdminEnabled(admin: Want, callback: AsyncCallback\<boolean>): void

查询当前用户下指定的设备管理应用是否被激活。使用callback异步回调。

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数**：

| 参数名      | 类型                                  | 必填   | 说明                   |
| -------- | ----------------------------------- | ---- | -------------------- |
| admin    | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 设备管理应用。             |
| callback | AsyncCallback\<boolean>             | 是    | 回调函数，当接口调用成功，err为null，data为boolean值，true表示当前用户下指定的设备管理应用被激活，false表示当前用户下指定的设备管理应用未激活，否则err为错误对象。 |

**示例**：

```ts
import Want from '@ohos.app.ability.Want';
let wantTemp: Want = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

adminManager.isAdminEnabled(wantTemp, (err, result) => {
  if (err) {
    console.error(`Failed to query admin is enabled or not. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info(`Succeeded in querying admin is enabled or not, result : ${result}`);
});
```

## adminManager.isAdminEnabled

isAdminEnabled(admin: Want, userId: number, callback: AsyncCallback\<boolean>): void

查询指定用户（通过userId指定）下指定的设备管理应用是否被激活。使用callback异步回调。

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数**：

| 参数名      | 类型                                  | 必填   | 说明                           |
| -------- | ----------------------------------- | ---- | ---------------------------- |
| admin    | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 设备管理应用。                      |
| userId   | number                              | 是    | 用户ID，指定具体用户，取值范围：大于等于0。<br> 默认值：当前用户。 |
| callback | AsyncCallback\<boolean>             | 是    | 回调函数，当接口调用成功，err为null，data为boolean值，true表示当前用户下指定的设备管理应用被激活，false表示当前用户下指定的设备管理应用未激活，否则err为错误对象。      |

**示例**：

```ts
import Want from '@ohos.app.ability.Want';
let wantTemp: Want = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

adminManager.isAdminEnabled(wantTemp, 100, (err, result) => {
  if (err) {
    console.error(`Failed to query admin is enabled. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info(`Succeeded in querying admin is enabled or not, result : ${result}`);
});
```

## adminManager.isAdminEnabled

isAdminEnabled(admin: Want, userId?: number): Promise\<boolean>

查询当前/指定用户下指定的设备管理应用是否被激活。使用promise异步回调。

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数**：

| 参数名    | 类型                                  | 必填   | 说明                           |
| ------ | ----------------------------------- | ---- | ---------------------------- |
| admin  | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 设备管理应用。                      |
| userId | number                              | 否    | 用户ID，取值范围：大于等于0。<br> - 调用接口时，若传入userId，表示指定用户。<br> - 调用接口时，若未传入userId，表示当前用户。 |

**返回值：**

| 类型               | 说明                |
| ----------------- | ------------------- |
| Promise\<boolean> | Promise对象, 返回true表示指定的设备管理应用被激活，返回false表示指定的设备管理应用未激活。|

**示例**：

```ts
import Want from '@ohos.app.ability.Want';
import { BusinessError } from '@ohos.base';
let wantTemp: Want = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

adminManager.isAdminEnabled(wantTemp, 100).then((result) => {
  console.info(`Succeeded in querying admin is enabled or not, result : ${result}`);
}).catch((err: BusinessError) => {
  console.error(`Failed to query admin is enabled or not. Code: ${err.code}, message: ${err.message}`);
});
```

## adminManager.isSuperAdmin

isSuperAdmin(bundleName: String, callback: AsyncCallback\<boolean>): void

根据bundleName查询管理员用户下的超级设备管理应用是否被激活。使用callback异步回调。

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数**：

| 参数名        | 类型                      | 必填   | 说明                   |
| ---------- | ----------------------- | ---- | -------------------- |
| bundleName | String                  | 是    | 超级设备管理应用。              |
| callback   | AsyncCallback\<boolean> | 是    | 回调函数，当接口调用成功，err为null，data为boolean类型值，true表示当前用户下指定的设备管理应用被激活，false表示当前用户下指定的设备管理应用未激活，否则err为错误对象。 |

**示例**：

```ts
import Want from '@ohos.app.ability.Want';
let bundleName: string = 'com.example.myapplication';

adminManager.isSuperAdmin(bundleName, (err, result) => {
  if (err) {
    console.error(`Failed to query admin is super admin or not. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info(`Succeeded in querying admin is super admin or not, result : ${result}`);
});
```

## adminManager.isSuperAdmin

isSuperAdmin(bundleName: String): Promise\<boolean>

根据bundleName查询管理员用户下的超级设备管理应用是否被激活。使用promise异步回调。

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数**：

| 参数名        | 类型     | 必填   | 说明        |
| ---------- | ------ | ---- | --------- |
| bundleName | String | 是    | 超级设备管理应用。 |

**返回值：**

| 错误码ID           | 错误信息               |
| ----------------- | ------------------- |
| Promise\<boolean> | Promise对象, 返回true表示指定的超级设备管理应用被激活，返回false表示指定的超级设备管理应用未激活。 |

**示例**：

```ts
import Want from '@ohos.app.ability.Want';
import { BusinessError } from '@ohos.base';
let bundleName: string = 'com.example.myapplication';

adminManager.isSuperAdmin(bundleName).then((result) => {
  console.info(`Succeeded in querying admin is super admin or not, result : ${result}`);
}).catch((err: BusinessError) => {
  console.error(`Failed to query admin is super admin or not. Code: ${err.code}, message: ${err.message}`);
});
```

## adminManager.setEnterpriseInfo

setEnterpriseInfo(admin: Want, enterpriseInfo: EnterpriseInfo, callback: AsyncCallback\<void>): void

设置指定的设备管理应用的企业信息。使用callback异步回调。

**需要权限：** ohos.permission.SET_ENTERPRISE_INFO

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数：**

| 参数名            | 类型                                  | 必填   | 说明                     |
| -------------- | ----------------------------------- | ---- | ---------------------- |
| admin          | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 设备管理应用。                |
| enterpriseInfo | [EnterpriseInfo](#enterpriseinfo)   | 是    | 设备管理应用的企业信息。           |
| callback       | AsyncCallback\<void>              | 是    | 回调函数，当接口调用成功，err为null，否则为错误对象。 |

**错误码**：

以下错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)。

| 错误码ID | 错误信息                                               |
| ------- | ----------------------------------------------------- |
| 9200001 | the application is not an administrator of the device. |

**示例：**

```ts
import Want from '@ohos.app.ability.Want';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};
let enterpriseInfo: adminManager.EnterpriseInfo = {
  name: 'enterprise name',
  description: 'enterprise description'
}

adminManager.setEnterpriseInfo(wantTemp, enterpriseInfo, (err) => {
  if (err) {
    console.error(`Failed to set enterprise info. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info('Succeeded in setting enterprise info');
});
```

## adminManager.setEnterpriseInfo

setEnterpriseInfo(admin: Want, enterpriseInfo: EnterpriseInfo): Promise\<void>

设置指定的设备管理应用的企业信息。使用promise异步回调。

**需要权限：** ohos.permission.SET_ENTERPRISE_INFO

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数：**

| 参数名            | 类型                                  | 必填   | 说明           |
| -------------- | ----------------------------------- | ---- | ------------ |
| admin          | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 设备管理应用      |
| enterpriseInfo | [EnterpriseInfo](#enterpriseinfo)   | 是    | 设备管理应用的企业信息 |

**返回值：**

| 类型                | 说明                    |
| ----------------- | --------------------- |
| Promise\<void>    | 无返回结果的Promise对象。当设置设备管理应用企业信息失败时，会抛出错误对象。 |

**错误码**：

以下错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)。

| 错误码ID | 错误信息                                               |
| ------- | ----------------------------------------------------- |
| 9200001 | the application is not an administrator of the device. |

**示例：**

```ts
import Want from '@ohos.app.ability.Want';
import { BusinessError } from '@ohos.base';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};
let enterpriseInfo: adminManager.EnterpriseInfo = {
  name: 'enterprise name',
  description: 'enterprise description'
}

adminManager.setEnterpriseInfo(wantTemp, enterpriseInfo).catch((err: BusinessError) => {
  console.error(`Failed to set enterprise info. Code: ${err.code}, message: ${err.message}`);
});
```

## adminManager.getEnterpriseInfo

getEnterpriseInfo(admin: Want, callback: AsyncCallback&lt;EnterpriseInfo&gt;): void

获取指定的设备管理应用的企业信息。使用callback异步回调。

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                       |
| -------- | ---------------------------------------- | ---- | ------------------------ |
| admin    | [Want](../apis-ability-kit/js-apis-app-ability-want.md)      | 是    | 设备管理应用                  |
| callback | AsyncCallback&lt;[EnterpriseInfo](#enterpriseinfo)&gt; | 是    | 回调函数，当接口调用成功，err为null，data为设备管理应用的企业信息，否则err为错误对象。 |

**错误码**：

以下错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)。

| 错误码ID | 错误信息                                               |
| ------- | ----------------------------------------------------- |
| 9200001 | the application is not an administrator of the device. |

**示例：**

```ts
import Want from '@ohos.app.ability.Want';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};

adminManager.getEnterpriseInfo(wantTemp, (err, result) => {
  if (err) {
    console.error(`Failed to get enterprise info. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info(`Succeeded in getting enterprise info, enterprise name : ${result.name}, enterprise description : ${result.description}`);
});
```

## adminManager.getEnterpriseInfo

getEnterpriseInfo(admin: Want): Promise&lt;EnterpriseInfo&gt;

获取指定的设备管理应用的企业信息，使用promise异步回调。

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数：**

| 参数名   | 类型                                  | 必填   | 说明      |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 设备管理应用 |

**返回值：**

| 类型                                       | 说明                        |
| ---------------------------------------- | ------------------------- |
| Promise&lt;[EnterpriseInfo](#enterpriseinfo)&gt; | Promise对象，返回指定的设备管理应用的企业信息。 |

**错误码**：

以下错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)。

| 错误码ID | 错误信息                                               |
| ------- | ----------------------------------------------------- |
| 9200001 | the application is not an administrator of the device. |

**示例：**

```ts
import Want from '@ohos.app.ability.Want';
import { BusinessError } from '@ohos.base';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};

adminManager.getEnterpriseInfo(wantTemp).then((result) => {
  console.info(`Succeeded in getting enterprise info, enterprise name : ${result.name}, enterprise description : ${result.description}`);
}).catch((err: BusinessError) => {
  console.error(`Failed to get enterprise info. Code: ${err.code}, message: ${err.message}`);
});
```

## adminManager.subscribeManagedEvent

subscribeManagedEvent(admin: Want, managedEvents: Array\<ManagedEvent>, callback: AsyncCallback\<void>): void

指定的设备管理应用订阅系统管理事件。使用callback异步回调。

**需要权限：** ohos.permission.ENTERPRISE_SUBSCRIBE_MANAGED_EVENT

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数：**

| 参数名   | 类型                                  | 必填   | 说明      |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 设备管理应用。 |
| managedEvents  | Array\<[ManagedEvent](#managedevent)> | 是 | 订阅事件数组。 |
| callback | AsyncCallback\<void> | 是 | 回调函数，当接口调用成功，err为null，否则为错误对象。 |

**错误码**：

以下错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)。

|错误码ID | 错误信息                                                |
| ------- | ----------------------------------------------------- |
| 9200001 | the application is not an administrator of the device. |
| 9200008 | the specified system events enum is invalid.          |

**示例：**

```ts
import Want from '@ohos.app.ability.Want';
let wantTemp: Want = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};
let events: Array<adminManager.ManagedEvent> = [adminManager.ManagedEvent.MANAGED_EVENT_BUNDLE_ADDED, adminManager.ManagedEvent.MANAGED_EVENT_BUNDLE_REMOVED];

adminManager.subscribeManagedEvent(wantTemp, events, (err) => {
  if (err) {
    console.error(`Failed to subscribe managed event. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info('Succeeded in subscribe managed event');
});
```

## adminManager.subscribeManagedEvent

subscribeManagedEvent(admin: Want, managedEvents: Array\<ManagedEvent>): Promise\<void>

指定的设备管理应用订阅系统管理事件。使用Promise异步回调。

**需要权限：** ohos.permission.ENTERPRISE_SUBSCRIBE_MANAGED_EVENT

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数：**

| 参数名   | 类型                                  | 必填   | 说明      |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 设备管理应用。 |
| managedEvents  | Array\<[ManagedEvent](#managedevent)> | 是 | 订阅事件数组。 |

**返回值：**

| 类型   | 说明                                  |
| ----- | ----------------------------------- |
| Promise\<void> | 无返回结果的Promise对象。当指定的设备管理应用订阅系统事件失败时，会抛出错误对象。 |

**错误码**：

以下错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)。

| 错误码ID | 错误信息                                               |
| ------- | ----------------------------------------------------- |
| 9200001 | the application is not an administrator of the device. |
| 9200008 | the specified system events enum is invalid.          |

**示例：**

```ts
import Want from '@ohos.app.ability.Want';
import { BusinessError } from '@ohos.base';
let wantTemp: Want = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};
let events: Array<adminManager.ManagedEvent> = [adminManager.ManagedEvent.MANAGED_EVENT_BUNDLE_ADDED, adminManager.ManagedEvent.MANAGED_EVENT_BUNDLE_REMOVED];

adminManager.subscribeManagedEvent(wantTemp, events).then(() => {
}).catch((err: BusinessError) => {
  console.error(`Failed to subscribe managed event. Code: ${err.code}, message: ${err.message}`);
})
```

## adminManager.unsubscribeManagedEvent

unsubscribeManagedEvent(admin: Want, managedEvents: Array\<ManagedEvent>, callback: AsyncCallback\<void>): void

指定的设备管理应用取消订阅系统管理事件。使用callback异步回调。

**需要权限：** ohos.permission.ENTERPRISE_SUBSCRIBE_MANAGED_EVENT

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数：**

| 参数名   | 类型                                  | 必填   | 说明      |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 设备管理应用。 |
| managedEvents  | Array\<[ManagedEvent](#managedevent)> | 是 | 取消订阅事件数组。 |
| callback | AsyncCallback\<void> | 是 | 回调函数，当接口调用成功，err为null，否则为错误对象。 |

**错误码**：

以下错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)。

| 错误码ID | 错误信息                                               |
| ------- | ----------------------------------------------------- |
| 9200001 | the application is not an administrator of the device. |
| 9200008 | the specified system events enum is invalid.          |

**示例：**

```ts
import Want from '@ohos.app.ability.Want';
let wantTemp: Want = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};
let events: Array<adminManager.ManagedEvent> = [adminManager.ManagedEvent.MANAGED_EVENT_BUNDLE_ADDED, adminManager.ManagedEvent.MANAGED_EVENT_BUNDLE_REMOVED];

adminManager.unsubscribeManagedEvent(wantTemp, events, (err) => {
  if (err) {
    console.error(`Failed to unsubscribe managed event. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info('Succeeded in unsubscribe managed event');
});
```

## adminManager.unsubscribeManagedEvent

unsubscribeManagedEvent(admin: Want, managedEvents: Array\<ManagedEvent>): Promise\<void>

指定的设备管理应用取消订阅系统管理事件。使用promise异步回调。

**需要权限：** ohos.permission.ENTERPRISE_SUBSCRIBE_MANAGED_EVENT

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数：**

| 参数名   | 类型                                  | 必填   | 说明      |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 设备管理应用。 |
| managedEvents  | Array\<[ManagedEvent](#managedevent)> | 是 | 取消订阅事件数组。 |

**返回值：**

| 类型   | 说明                                  |
| ----- | ----------------------------------- |
| Promise\<void> | 无返回结果的Promise对象。当指定设备管理应用取消订阅系统管理事件失败时，会抛出错误对象。 |

**错误码**：

以下错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)。

| 错误码ID | 错误信息                                               |
| ------- | ----------------------------------------------------- |
| 9200001 | the application is not an administrator of the device. |
| 9200008 | the specified system events enum is invalid.          |

**示例：**

```ts
import Want from '@ohos.app.ability.Want';
import { BusinessError } from '@ohos.base';
let wantTemp: Want = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};
let events: Array<adminManager.ManagedEvent> = [adminManager.ManagedEvent.MANAGED_EVENT_BUNDLE_ADDED, adminManager.ManagedEvent.MANAGED_EVENT_BUNDLE_REMOVED];

adminManager.unsubscribeManagedEvent(wantTemp, events).then(() => {
}).catch((err: BusinessError) => {
  console.error(`Failed to unsubscribe managed event. Code: ${err.code}, message: ${err.message}`);
})
```

## adminManager.authorizeAdmin<sup>10+</sup>

authorizeAdmin(admin: Want, bundleName: string, callback: AsyncCallback&lt;void&gt;): void

设备管理应用授予指定应用管理员权限。使用callback异步回调。

**需要权限：** ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数：**

| 参数名   | 类型                                  | 必填   | 说明      |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 设备管理应用。 |
| bundleName  | string | 是 | 被授予管理员权限应用的包名。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数，当接口调用成功，err为null，否则为错误对象。 |

**错误码**：

以下的错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)

| 错误码ID | 错误信息                                               |
| ------- | ----------------------------------------------------- |
| 9200001 | the application is not an administrator of the device. |
| 9200002 | the administrator application does not have permission to manage the device.          |
| 9200009 | authorize permission to the application failed.          |

**示例：**

```ts
import Want from '@ohos.app.ability.Want';
let wantTemp: Want = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};
let bundleName: string = "com.example.application";

adminManager.authorizeAdmin(wantTemp, bundleName, (err) => {
  if (err) {
    console.error(`Failed to authorize permission to the application. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info('Successfully authorized permission to the application');
});
```

## adminManager.authorizeAdmin<sup>10+</sup>

authorizeAdmin(admin: Want, bundleName: string): Promise&lt;void&gt;

设备管理应用授予指定应用管理员权限。使用Promise异步回调。

**需要权限：** ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**模型约束**: 此接口仅可在Stage模型下使用。

**参数：**

| 参数名   | 类型                                  | 必填   | 说明      |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 设备管理应用。 |
| bundleName  | string | 是 | 被授予管理员权限应用的包名。 |

**返回值：**

| 类型   | 说明                                  |
| ----- | ----------------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。当设备管理应用授予指定应用管理员权限失败时，抛出错误对象。 |

**错误码**：

以下的错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)

| 错误码ID | 错误信息                                               |
| ------- | ----------------------------------------------------- |
| 9200001 | the application is not an administrator of the device. |
| 9200002 | the administrator application does not have permission to manage the device.          |
| 9200009 | authorize permission to the application failed.          |

**示例：**

```ts
import Want from '@ohos.app.ability.Want';
import { BusinessError } from '@ohos.base';
let wantTemp: Want = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};
let bundleName: string = "com.example.application";

adminManager.authorizeAdmin(wantTemp, bundleName).then(() => {
}).catch((err: BusinessError) => {
  console.error(`Failed to authorize permission to the application. Code: ${err.code}, message: ${err.message}`);
})
```

## EnterpriseInfo

设备管理应用的企业信息。

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



| 名称         | 类型     | 必填 | 说明                            |
| ----------- | --------| ---- | ------------------------------- |
| name        | string   | 是   | 表示设备管理应用所属企业的名称。 |
| description | string   | 是   | 表示设备管理应用所属企业的描述。 |

## AdminType

设备管理应用的类型。 

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



| 名称                | 值  | 说明    |
| ----------------- | ---- | ----- |
| ADMIN_TYPE_NORMAL | 0x00 | 普通设备管理应用。 |
| ADMIN_TYPE_SUPER  | 0x01 | 超级设备管理应用。 |

## ManagedEvent

可订阅的系统管理事件。

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



| 名称                        | 值  | 说明           |
| -------------------------- | ---- | ------------- |
| MANAGED_EVENT_BUNDLE_ADDED | 0    | 应用安装事件。 |
| MANAGED_EVENT_BUNDLE_REMOVED | 1  | 应用卸载事件。 |
| MANAGED_EVENT_APP_START<sup>10+</sup> | 2    | 应用启动事件。 |
| MANAGED_EVENT_APP_STOP<sup>10+</sup> | 3  | 应用停止事件。 |
| MANAGED_EVENT_SYSTEM_UPDATE<sup>11+</sup> | 4   | 系统更新事件。 |
