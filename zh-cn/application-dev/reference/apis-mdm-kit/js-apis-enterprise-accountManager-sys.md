# @ohos.enterprise.accountManager（帐户管理）(系统接口)

本模块提供设备帐户管理能力，包括禁止创建本地用户等。

> **说明：**
>
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>
> 本模块接口仅可在Stage模型下使用。
>
> 本模块接口仅对[设备管理应用](enterpriseDeviceManagement-overview.md#基本概念)开放，需将[设备管理应用激活](js-apis-enterprise-adminManager-sys.md#adminmanagerenableadmin)后调用，实现相应功能。
> 
> 本模块接口均为系统接口。

## 导入模块

```ts
import accountManager from '@ohos.enterprise.accountManager';
```

## accountManager.disallowAddLocalAccount

disallowAddLocalAccount(admin: Want, disallow: boolean, callback: AsyncCallback&lt;void&gt;): void

指定设备管理应用禁止设备创建本地用户。使用callback异步回调。

**需要权限：** ohos.permission.ENTERPRISE_SET_ACCOUNT_POLICY

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**参数：**

| 参数名      | 类型                                       | 必填   | 说明                       |
| -------- | ---------------------------------------- | ---- | ------------------------------- |
| admin    | [Want](../apis-ability-kit/js-apis-app-ability-want.md)     | 是    | 设备管理应用。                  |
| disallow    | boolean     | 是    | 是否禁止创建本地用户，true表示禁止创建，false表示允许创建。                  |
| callback | AsyncCallback&lt;void&gt;            | 是    | 回调函数。当接口调用成功，err为null，否则为错误对象。       |

**错误码**：

以下错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)

| 错误码ID | 错误信息                                                                       |          
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | the application is not an administrator of the device.                        |
| 9200002 | the administrator application does not have permission to manage the device. |

**示例：**

```ts
import Want from '@ohos.app.ability.Want';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};

accountManager.disallowAddLocalAccount(wantTemp, true, (err) => {
  if (err) {
    console.error(`Failed to disallow add local account. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info('Succeeded in disallowing add local account');
});
```

## accountManager.disallowAddLocalAccount

disallowAddLocalAccount(admin: Want, disallow: boolean): Promise&lt;void&gt;

指定设备管理应用禁止设备创建本地用户。使用promise异步回调。

**需要权限：** ohos.permission.ENTERPRISE_SET_ACCOUNT_POLICY

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**参数：**

| 参数名   | 类型                                  | 必填   | 说明      |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是    | 设备管理应用。 |
| disallow    | boolean     | 是    | 是否禁止创建本地用户，true表示禁止创建，false表示允许创建。                  |

**返回值：**

| 类型                   | 说明                      |
| --------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。当禁止创建本地用户失败时，抛出错误对象。 |

**错误码**：

以下错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)

| 错误码ID | 错误信息                                                                     |          
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | the application is not an administrator of the device.                        |
| 9200002 | the administrator application does not have permission to manage the device. |

**示例：**

```ts
import Want from '@ohos.app.ability.Want';
import { BusinessError } from '@ohos.base';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};

accountManager.disallowAddLocalAccount(wantTemp, true).then(() => {
  console.info('Succeeded in disallowing add local account');
}).catch((err: BusinessError) => {
  console.error(`Failed to disallow add local account. Code: ${err.code}, message: ${err.message}`);
});
```

## accountManager.disallowAddOsAccountByUser<sup>11+</sup>

disallowAddOsAccountByUser(admin: Want, userId: number, disallow: boolean): void

指定设备管理应用禁止用户添加账号。

**需要权限：** ohos.permission.ENTERPRISE_SET_ACCOUNT_POLICY

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**参数：**

| 参数名   | 类型                                | 必填 | 说明                                                        |
| -------- | ----------------------------------- | ---- | ----------------------------------------------------------- |
| admin    | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是   | 设备管理应用。                                              |
| userId   | number                              | 是   | 用户ID，指定具体用户，取值范围：大于等于0。                 |
| disallow | boolean                             | 是   | 是否禁止用户添加账号，true表示禁止添加，false表示允许添加。 |

**错误码**：

以下错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 9200001  | the application is not an administrator of the device.       |
| 9200002  | the administrator application does not have permission to manage the device. |

**示例：**

```ts
import Want from '@ohos.app.ability.Want';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};

try {
  accountManager.disallowAddOsAccountByUser(wantTemp, 100, true);
  console.info(`Succeeded in disallowing user add os account`);
} catch (err) {
  console.error(`Failed to disallow user add os account. Code: ${err.code}, message: ${err.message}`);
}
```

## accountManager.isAddOsAccountByUserDisallowed<sup>11+</sup>

isAddOsAccountByUserDisallowed(admin: Want, userId: number): boolean

指定设备管理应用查询是否禁止某用户添加账号。

**需要权限：** ohos.permission.ENTERPRISE_SET_ACCOUNT_POLICY

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**参数：**

| 参数名 | 类型                                | 必填 | 说明                                        |
| ------ | ----------------------------------- | ---- | ------------------------------------------- |
| admin  | [Want](../apis-ability-kit/js-apis-app-ability-want.md) | 是   | 设备管理应用。                              |
| userId | number                              | 是   | 用户ID，指定具体用户，取值范围：大于等于0。 |

**返回值：**

| 类型    | 说明                                                         |
| ------- | ------------------------------------------------------------ |
| boolean | 返回true表示该用户禁止添加账号，<br/>返回false表示该用户允许添加账号。 |

**错误码**：

以下错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 9200001  | the application is not an administrator of the device.       |
| 9200002  | the administrator application does not have permission to manage the device. |

**示例：**

```ts
import Want from '@ohos.app.ability.Want';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};

try {
  let isDisallowed: boolean = accountManager.isAddOsAccountByUserDisallowed(wantTemp, 100);
  console.info(`Succeeded in querying the user can add os account or not: ${isDisallowed}`);
} catch (err) {
  console.error(`Failed to query the user can add os account or not. Code: ${err.code}, message: ${err.message}`);
}
```

## accountManager.addOsAccount<sup>11+</sup>

addOsAccount(admin: Want, name: string, type: osAccount.OsAccountType): osAccount.OsAccountInfo

指定设备管理应用后台添加账号。

**需要权限：** ohos.permission.ENTERPRISE_SET_ACCOUNT_POLICY

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager



**参数：**

| 参数名 | 类型                                                         | 必填 | 说明                                                         |
| ------ | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| admin  | [Want](../apis-ability-kit/js-apis-app-ability-want.md)                          | 是   | 设备管理应用。                                               |
| name   | string                                                       | 是   | 用户ID，指定具体用户，取值范围：大于等于0。                  |
| type   | [osAccount.OsAccountType](../apis-basic-services-kit/js-apis-osAccount.md#osaccounttype) | 是   | 要添加的账号的类型。<br/>取值范围：ADMIN、NORMAL、GUEST。<br/>· ADMIN：管理员帐号。<br/>· NORMAL：普通账号。<br/>· GUEST：访客账号。 |

**返回值：**

| 类型                                                         | 说明                 |
| ------------------------------------------------------------ | -------------------- |
| [osAccount.OsAccountInfo](../apis-basic-services-kit/js-apis-osAccount.md#osaccounttype) | 返回添加的账号信息。 |

**错误码**：

以下错误码的详细介绍请参见[企业设备管理错误码](errorcode-enterpriseDeviceManager.md)

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 9200001  | the application is not an administrator of the device.       |
| 9200002  | the administrator application does not have permission to manage the device. |
| 9201003  | failed to add an OS account.                                 |

**示例：**

```ts
import Want from '@ohos.app.ability.Want';
import osAccount from '@ohos.account.osAccount';
let wantTemp: Want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};

try {
  let info: osAccount.OsAccountInfo = accountManager.addOsAccount(wantTemp, "TestAccountName", osAccount.OsAccountType.NORMAL);
  console.info(`Succeeded in creating os account: ${JSON.stringify(info)}`);
} catch (err) {
  console.error(`Failed to creating os account. Code: ${err.code}, message: ${err.message}`);
}
```

