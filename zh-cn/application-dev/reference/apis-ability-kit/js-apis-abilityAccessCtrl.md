# @ohos.abilityAccessCtrl (程序访问控制管理)

程序访问控制提供程序的权限管理能力，包括鉴权、授权和取消授权等。

> **说明：**
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import abilityAccessCtrl from '@ohos.abilityAccessCtrl'
```

## abilityAccessCtrl.createAtManager

createAtManager(): AtManager

访问控制管理：获取访问控制模块对象。

**系统能力：** SystemCapability.Security.AccessToken


**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [AtManager](#atmanager) | 获取访问控制模块的实例。 |

**示例：**

```ts
let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
```

## AtManager

管理访问控制模块的实例。

### checkAccessToken<sup>9+</sup>

checkAccessToken(tokenID: number, permissionName: Permissions): Promise&lt;GrantStatus&gt;

校验应用是否授予权限。使用Promise异步回调。

**系统能力：** SystemCapability.Security.AccessToken

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                       |
| -------- | -------------------  | ---- | ------------------------------------------ |
| tokenID   |  number   | 是   | 要校验的目标应用的身份标识。可通过应用的[ApplicationInfo](js-apis-bundleManager-applicationInfo.md)获得。             |
| permissionName | Permissions | 是   | 需要校验的权限名称，合法的权限名取值可在[应用权限列表](../../security/AccessToken/permissions-for-all.md)中查询。 |

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| Promise&lt;GrantStatus&gt; | Promise对象。返回授权状态结果。 |

**错误码：**

以下错误码的详细介绍请参见[访问控制错误码](errorcode-access-token.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 12100001 | The parameter is invalid. The tokenID is 0, or the string size of permissionName is larger than 256. |

**示例：**

```ts
import abilityAccessCtrl from '@ohos.abilityAccessCtrl';
import { BusinessError } from '@ohos.base';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let tokenID: number = 0; // 系统应用可以通过bundleManager.getApplicationInfo获取,普通应用可以通过bundleManager.getBundleInfoForSelf获取
atManager.checkAccessToken(tokenID, 'ohos.permission.GRANT_SENSITIVE_PERMISSIONS').then((data: abilityAccessCtrl.GrantStatus) => {
  console.log(`checkAccessToken success, data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
  console.log(`checkAccessToken fail, err->${JSON.stringify(err)}`);
});
```

### verifyAccessTokenSync<sup>9+</sup>

verifyAccessTokenSync(tokenID: number, permissionName: Permissions): GrantStatus

校验应用是否被授予权限，同步返回结果。

**系统能力：** SystemCapability.Security.AccessToken

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                       |
| -------- | -------------------  | ---- | ------------------------------------------ |
| tokenID   |  number   | 是   | 要校验应用的身份标识。可通过应用的[ApplicationInfo](js-apis-bundleManager-applicationInfo.md)获得。              |
| permissionName | Permissions | 是   | 需要校验的权限名称，合法的权限名取值可在[应用权限列表](../../security/AccessToken/permissions-for-all.md)中查询。 |

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| [GrantStatus](#grantstatus) | 枚举实例，返回授权状态。 |

**错误码：**

以下错误码的详细介绍请参见[访问控制错误码](errorcode-access-token.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 12100001 | The parameter is invalid. The tokenID is 0, or the string size of permissionName is larger than 256. |

**示例：**

```ts
import abilityAccessCtrl from '@ohos.abilityAccessCtrl';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let tokenID: number = 0; // 系统应用可以通过bundleManager.getApplicationInfo获取,普通应用可以通过bundleManager.getBundleInfoForSelf获取
let data: abilityAccessCtrl.GrantStatus = atManager.verifyAccessTokenSync(tokenID, 'ohos.permission.GRANT_SENSITIVE_PERMISSIONS');
console.log(`data->${JSON.stringify(data)}`);
```

### verifyAccessToken<sup>9+</sup>

verifyAccessToken(tokenID: number, permissionName: Permissions): Promise&lt;GrantStatus&gt;

校验应用是否授予权限。使用Promise异步回调。

> **说明：**
>
> 建议使用[checkAccessToken](#checkaccesstoken9)替代。

**系统能力：** SystemCapability.Security.AccessToken

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                       |
| -------- | -------------------  | ---- | ------------------------------------------ |
| tokenID   |  number   | 是   | 要校验的目标应用的身份标识。可通过应用的[ApplicationInfo](js-apis-bundleManager-applicationInfo.md)获得。             |
| permissionName | Permissions | 是   | 需要校验的权限名称，合法的权限名取值可在[应用权限列表](../../security/AccessToken/permissions-for-all.md)中查询。 |

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| Promise&lt;GrantStatus&gt; | Promise对象。返回授权状态结果。 |

**示例：**

```ts
import abilityAccessCtrl, { Permissions } from '@ohos.abilityAccessCtrl';
import { BusinessError } from '@ohos.base';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let tokenID: number = 0; // 系统应用可以通过bundleManager.getApplicationInfo获取,普通应用可以通过bundleManager.getBundleInfoForSelf获取
let permissionName: Permissions = 'ohos.permission.GRANT_SENSITIVE_PERMISSIONS';
atManager.verifyAccessToken(tokenID, permissionName).then((data: abilityAccessCtrl.GrantStatus) => {
  console.log(`promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
  console.log(`verifyAccessToken fail, err->${JSON.stringify(err)}`);
});
```

### requestPermissionsFromUser<sup>9+</sup>

requestPermissionsFromUser(context: Context, permissionList: Array&lt;Permissions&gt;, requestCallback: AsyncCallback&lt;PermissionRequestResult&gt;) : void

用于UIAbility拉起弹框请求用户授权。使用callback异步回调。

如果用户拒绝授权，将无法再次拉起弹框，需要用户在系统应用“设置”的界面中，手动授予权限。

> **说明：**
>
> 仅支持UIAbility。

**模型约束**：此接口仅可在Stage模型下使用。

**系统能力**: SystemCapability.Security.AccessToken

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| context | Context | 是 | 请求权限的UIAbility的Context。 |
| permissionList | Array&lt;Permissions&gt; | 是 | 权限名列表，合法的权限名取值可在[应用权限列表](../../security/AccessToken/permissions-for-all.md)中查询。 |
| requestCallback | AsyncCallback&lt;[PermissionRequestResult](js-apis-permissionrequestresult.md)&gt; | 是 | 回调函数，返回接口调用是否成功的结果。 |

**错误码：**

以下错误码的详细介绍请参见[访问控制错误码](errorcode-access-token.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 12100001 | The parameter is invalid. The context is invalid when it does not belong to the application itself. |

**示例：**
示例中context的获取方式请参见[获取UIAbility的上下文信息](../../application-models/uiability-usage.md#获取uiability的上下文信息)。

```ts
import abilityAccessCtrl, { Context, PermissionRequestResult } from '@ohos.abilityAccessCtrl';
import { BusinessError } from '@ohos.base';
import common from '@ohos.app.ability.common';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let context: Context = getContext(this) as common.UIAbilityContext;
atManager.requestPermissionsFromUser(context, ['ohos.permission.CAMERA'], (err: BusinessError, data: PermissionRequestResult)=>{
  if (err) {
    console.log(`requestPermissionsFromUser fail, err->${JSON.stringify(err)}`);
  } else {
    console.info('data:' + JSON.stringify(data));
    console.info('data permissions:' + data.permissions);
    console.info('data authResults:' + data.authResults);
  }
});
```

### requestPermissionsFromUser<sup>9+</sup>

requestPermissionsFromUser(context: Context, permissionList: Array&lt;Permissions&gt;) : Promise&lt;PermissionRequestResult&gt;

用于UIAbility拉起弹框请求用户授权。使用promise异步回调。

如果用户拒绝授权，将无法再次拉起弹框，需要用户在系统应用“设置”的界面中，手动授予权限。

> **说明：**
>
> 仅支持UIAbility。

**模型约束**：此接口仅可在Stage模型下使用。

**系统能力**: SystemCapability.Security.AccessToken

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| context | Context | 是 | 请求权限的UIAbility的Context。 |
| permissionList | Array&lt;Permissions&gt; | 是 | 需要校验的权限名称，合法的权限名取值可在[应用权限列表](../../security/AccessToken/permissions-for-all.md)中查询。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;[PermissionRequestResult](js-apis-permissionrequestresult.md)&gt; | 返回一个Promise，包含接口的结果。 |

**错误码：**

以下错误码的详细介绍请参见[访问控制错误码](errorcode-access-token.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 12100001 | The parameter is invalid. The context is invalid when it does not belong to the application itself. |

**示例：**
示例中context的获取方式请参见[获取UIAbility的上下文信息](../../application-models/uiability-usage.md#获取uiability的上下文信息)。

```ts
import abilityAccessCtrl, { Context, PermissionRequestResult } from '@ohos.abilityAccessCtrl';
import { BusinessError } from '@ohos.base';
import common from '@ohos.app.ability.common';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let context: Context = getContext(this) as common.UIAbilityContext;
atManager.requestPermissionsFromUser(context, ['ohos.permission.CAMERA']).then((data: PermissionRequestResult) => {
  console.info('data:' + JSON.stringify(data));
  console.info('data permissions:' + data.permissions);
  console.info('data authResults:' + data.authResults);
}).catch((err: BusinessError) => {
  console.info('data:' + JSON.stringify(err));
});
```

### verifyAccessToken<sup>(deprecated)</sup>

verifyAccessToken(tokenID: number, permissionName: string): Promise&lt;GrantStatus&gt;

校验应用是否授予权限。使用Promise异步回调。

> **说明：**
>
> 从API version 9开始不再维护，建议使用[checkAccessToken](#checkaccesstoken9)替代。

**系统能力：** SystemCapability.Security.AccessToken

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                       |
| -------- | -------------------  | ---- | ------------------------------------------ |
| tokenID   |  number   | 是   | 要校验的目标应用的身份标识。可通过应用的[ApplicationInfo](js-apis-bundleManager-applicationInfo.md)获得。             |
| permissionName | string | 是   | 需要校验的权限名称，合法的权限名取值可在[应用权限列表](../../security/AccessToken/permissions-for-all.md)中查询。 |

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| Promise&lt;GrantStatus&gt; | Promise对象。返回授权状态结果。 |

**示例：**

```ts
import abilityAccessCtrl from '@ohos.abilityAccessCtrl';
import { BusinessError } from '@ohos.base';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let tokenID: number = 0; // 系统应用可以通过bundleManager.getApplicationInfo获取,普通应用可以通过bundleManager.getBundleInfoForSelf获取
atManager.verifyAccessToken(tokenID, 'ohos.permission.GRANT_SENSITIVE_PERMISSIONS').then((data: abilityAccessCtrl.GrantStatus) => {
  console.log(`promise: data->${JSON.stringify(data)}`);
}).catch((err: BusinessError) => {
  console.log(`verifyAccessToken fail, err->${JSON.stringify(err)}`);
});
```

### checkAccessTokenSync<sup>10+</sup>

checkAccessTokenSync(tokenID: number, permissionName: Permissions): GrantStatus

校验应用是否被授予权限，同步返回结果。

**系统能力：** SystemCapability.Security.AccessToken

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                       |
| -------- | -------------------  | ---- | ------------------------------------------ |
| tokenID   |  number   | 是   | 要校验应用的身份标识。可通过应用的[ApplicationInfo](js-apis-bundleManager-applicationInfo.md)获得。              |
| permissionName | Permissions | 是   | 需要校验的权限名称，合法的权限名取值可在[应用权限列表](../../security/AccessToken/permissions-for-all.md)中查询。 |

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| [GrantStatus](#grantstatus) | 枚举实例，返回授权状态。 |

**错误码：**

以下错误码的详细介绍请参见[访问控制错误码](errorcode-access-token.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 12100001 | The parameter is invalid. The tokenID is 0, or the string size of permissionName is larger than 256. |

**示例：**

```ts
import abilityAccessCtrl, { Permissions } from '@ohos.abilityAccessCtrl';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let tokenID: number = 0; // 系统应用可以通过bundleManager.getApplicationInfo获取,普通应用可以通过bundleManager.getBundleInfoForSelf获取
let permissionName: Permissions = 'ohos.permission.GRANT_SENSITIVE_PERMISSIONS';
let data: abilityAccessCtrl.GrantStatus = atManager.checkAccessTokenSync(tokenID, permissionName);
console.log(`data->${JSON.stringify(data)}`);
```

### GrantStatus

表示授权状态的枚举。

**系统能力：** SystemCapability.Security.AccessToken

| 名称               |    值 | 说明        |
| ------------------ | ----- | ----------- |
| PERMISSION_DENIED  | -1    | 表示未授权。 |
| PERMISSION_GRANTED | 0     | 表示已授权。 |
