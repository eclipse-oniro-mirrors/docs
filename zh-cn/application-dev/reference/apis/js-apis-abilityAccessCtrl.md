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
| permissionName | Permissions | 是   | 需要校验的权限名称，合法的权限名取值可在[系统权限定义列表](../../security/permission-list.md)中查询。 |

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| Promise&lt;GrantStatus&gt; | Promise对象。返回授权状态结果。 |

**错误码：**

以下错误码的详细介绍请参见[程序访问控制错误码](../errorcodes/errorcode-access-token.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 12100001 | The parameter is invalid. The tokenID is 0, or the string size of permissionName is larger than 256. |

**示例：**

```ts
import abilityAccessCtrl from '@ohos.abilityAccessCtrl';
import { BusinessError } from '@ohos.base';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let tokenID: number = 0; // 系统应用可以通过bundleManager.getApplicationInfo获取,普通应用可以通过bundleManager.getBundleInfoForSelf获取
try {
    atManager.checkAccessToken(tokenID, "ohos.permission.GRANT_SENSITIVE_PERMISSIONS").then((data: abilityAccessCtrl.GrantStatus) => {
        console.log(`checkAccessToken success, data->${JSON.stringify(data)}`);
    }).catch((err: BusinessError) => {
        console.log(`checkAccessToken fail, err->${JSON.stringify(err)}`);
    });
} catch(err) {
    console.log(`catch err->${JSON.stringify(err)}`);
}
```

### verifyAccessTokenSync<sup>9+</sup>

verifyAccessTokenSync(tokenID: number, permissionName: Permissions): GrantStatus

校验应用是否被授予权限，同步返回结果。

**系统能力：** SystemCapability.Security.AccessToken

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                       |
| -------- | -------------------  | ---- | ------------------------------------------ |
| tokenID   |  number   | 是   | 要校验应用的身份标识。可通过应用的[ApplicationInfo](js-apis-bundleManager-applicationInfo.md)获得。              |
| permissionName | Permissions | 是   | 需要校验的权限名称，合法的权限名取值可在[系统权限定义列表](../../security/permission-list.md)中查询。 |

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| [GrantStatus](#grantstatus) | 枚举实例，返回授权状态。 |

**错误码：**

以下错误码的详细介绍请参见[程序访问控制错误码](../errorcodes/errorcode-access-token.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 12100001 | The parameter is invalid. The tokenID is 0, or the string size of permissionName is larger than 256. |

**示例：**

```ts
import abilityAccessCtrl from '@ohos.abilityAccessCtrl';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let tokenID: number = 0; // 系统应用可以通过bundleManager.getApplicationInfo获取,普通应用可以通过bundleManager.getBundleInfoForSelf获取
let data: abilityAccessCtrl.GrantStatus = atManager.verifyAccessTokenSync(tokenID, "ohos.permission.GRANT_SENSITIVE_PERMISSIONS");
console.log(`data->${JSON.stringify(data)}`);
```

### grantUserGrantedPermission

grantUserGrantedPermission(tokenID: number, permissionName: Permissions, permissionFlags: number): Promise&lt;void&gt;

授予应用user grant权限。使用Promise异步回调。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.GRANT_SENSITIVE_PERMISSIONS，仅系统应用可用。

**系统能力：** SystemCapability.Security.AccessToken

**参数：**

| 参数名    | 类型                | 必填 | 说明                                                         |
| --------- | ------------------- | ---- | ------------------------------------------------------------ |
| tokenID      | number              | 是   | 目标应用的身份标识。可通过应用的[ApplicationInfo](js-apis-bundleManager-applicationInfo.md)获得。            |
| permissionName | Permissions              | 是   | 被授予的权限名称，合法的权限名取值可在[系统权限定义列表](../../security/permission-list.md)中查询。 |
| permissionFlags  | number | 是   | 授权选项<br>- 0表示权限未经过用户主动设置。<br>- 1表示当次用户若选择禁止该权限，下次权限弹窗仍可以弹出申请用户授权。<br>- 2表示当次用户若选择禁止该权限，下次不会再弹出权限弹窗，需要用户在setting的权限管理中进行授权。<br>- 4表示当次权限设置为系统授权，用户不可更改这个权限授权状态。 |

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| Promise&lt;void&gt; | Promise对象。无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[程序访问控制错误码](../errorcodes/errorcode-access-token.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 12100001 | The parameter is invalid. The tokenID is 0, or the string size of permissionName is larger than 256, or the flags value is invalid. |
| 12100002 | The specified tokenID does not exist. |
| 12100003 | The specified permission does not exist. |
| 12100006 | The application specified by the tokenID is not allowed to be granted with the specified permission. Either the application is a sandbox or the tokenID is from a remote device. |
| 12100007 | Service is abnormal. |

**示例：**

```ts
import abilityAccessCtrl from '@ohos.abilityAccessCtrl';
import { BusinessError } from '@ohos.base';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let tokenID: number = 0; // 系统应用可以通过bundleManager.getApplicationInfo获取,普通应用可以通过bundleManager.getBundleInfoForSelf获取
let permissionFlags: number = 1;
try {
    atManager.grantUserGrantedPermission(tokenID, "ohos.permission.GRANT_SENSITIVE_PERMISSIONS", permissionFlags).then(() => {
        console.log('grantUserGrantedPermission success');
    }).catch((err: BusinessError) => {
        console.log(`grantUserGrantedPermission fail, err->${JSON.stringify(err)}`);
    });
} catch(err) {
    console.log(`catch err->${JSON.stringify(err)}`);
}
```

### grantUserGrantedPermission

grantUserGrantedPermission(tokenID: number, permissionName: Permissions, permissionFlags: number, callback: AsyncCallback&lt;void&gt;): void

授予应用user grant权限。使用callback异步回调。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.GRANT_SENSITIVE_PERMISSIONS，仅系统应用可用。

**系统能力：** SystemCapability.Security.AccessToken

**参数：**

| 参数名    | 类型                | 必填 | 说明                          |
| --------- | ------------------- | ---- | ------------------------------------------------------------ |
| tokenID      | number              | 是   | 目标应用的身份标识。可通过应用的[ApplicationInfo](js-apis-bundleManager-applicationInfo.md)获得。|
| permissionName | Permissions              | 是   | 被授予的权限名称，合法的权限名取值可在[系统权限定义列表](../../security/permission-list.md)中查询。 |
| permissionFlags  | number | 是   | 授权选项<br>- 0表示权限未经过用户主动设置。<br>- 1表示当次用户若选择禁止该权限，下次权限弹窗仍可以弹出申请用户授权。<br>- 2表示当次用户若选择禁止该权限，下次不会再弹出权限弹窗，需要用户在setting的权限管理中进行授权。<br>- 4表示当次权限设置为系统授权，用户不可更改这个权限授权状态。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 授予应用user grant权限。当授予权限成功时，err为undefined；否则为错误对象。 |

**错误码：**

以下错误码的详细介绍请参见[程序访问控制错误码](../errorcodes/errorcode-access-token.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 12100001 | The parameter is invalid. The tokenID is 0, or the string size of permissionName is larger than 256, or the flags value is invalid. |
| 12100002 | TokenId does not exist. |
| 12100003 | Permission does not exist. |
| 12100006 | The application specified by the tokenID is not allowed to be granted with the specified permission. Either the application is a sandbox or the tokenID is from a remote device. |
| 12100007 | Service is abnormal. |

**示例：**

```ts
import abilityAccessCtrl from '@ohos.abilityAccessCtrl';
import { BusinessError } from '@ohos.base';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let tokenID: number = 0; // 系统应用可以通过bundleManager.getApplicationInfo获取,普通应用可以通过bundleManager.getBundleInfoForSelf获取
let permissionFlags: number = 1;
try {
    atManager.grantUserGrantedPermission(tokenID, "ohos.permission.GRANT_SENSITIVE_PERMISSIONS", permissionFlags, (err: BusinessError, data: void) => {
        if (err) {
            console.log(`grantUserGrantedPermission fail, err->${JSON.stringify(err)}`);
        } else {
            console.log('grantUserGrantedPermission success');
        }
    });
} catch(err) {
    console.log(`catch err->${JSON.stringify(err)}`);
}
```

### revokeUserGrantedPermission

revokeUserGrantedPermission(tokenID: number, permissionName: Permissions, permissionFlags: number): Promise&lt;void&gt;

撤销应用user grant权限。使用Promise异步回调。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.REVOKE_SENSITIVE_PERMISSIONS，仅系统应用可用。

**系统能力：** SystemCapability.Security.AccessToken

**参数：**

| 参数名    | 类型                | 必填 | 说明                                                         |
| --------- | ------------------- | ---- | ------------------------------------------------------------ |
| tokenID      | number              | 是   | 目标应用的身份标识。可通过应用的[ApplicationInfo](js-apis-bundleManager-applicationInfo.md)获得。           |
| permissionName | Permissions              | 是   | 被撤销的权限名称，合法的权限名取值可在[系统权限定义列表](../../security/permission-list.md)中查询。 |
| permissionFlags  | number | 是   | 授权选项<br>- 0表示权限未经过用户主动设置。<br>- 1表示当次用户若选择禁止该权限，下次权限弹窗仍可以弹出申请用户授权。<br>- 2表示当次用户若选择禁止该权限，下次不会再弹出权限弹窗，需要用户在setting的权限管理中进行授权。<br>- 4表示当次权限设置为系统授权，用户不可更改这个权限授权状态。 |

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| Promise&lt;void&gt; | Promise对象。无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[程序访问控制错误码](../errorcodes/errorcode-access-token.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 12100001 | The parameter is invalid. The tokenID is 0, or the string size of permissionName is larger than 256, or the flags value is invalid. |
| 12100002 | The specified tokenID does not exist. |
| 12100003 | The specified permission does not exist. |
| 12100006 | The application specified by the tokenID is not allowed to be revoked with the specified permission. Either the application is a sandbox or the tokenID is from a remote device. |
| 12100007 | Service is abnormal. |

**示例：**

```ts
import abilityAccessCtrl from '@ohos.abilityAccessCtrl';
import { BusinessError } from '@ohos.base';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let tokenID: number = 0; // 系统应用可以通过bundleManager.getApplicationInfo获取,普通应用可以通过bundleManager.getBundleInfoForSelf获取
let permissionFlags: number = 1;
try {
    atManager.revokeUserGrantedPermission(tokenID, "ohos.permission.GRANT_SENSITIVE_PERMISSIONS", permissionFlags).then(() => {
        console.log('revokeUserGrantedPermission success');
    }).catch((err: BusinessError) => {
        console.log(`revokeUserGrantedPermission fail, err->${JSON.stringify(err)}`);
    });
} catch(err) {
    console.log(`catch err->${JSON.stringify(err)}`);
}
```

### revokeUserGrantedPermission

revokeUserGrantedPermission(tokenID: number, permissionName: Permissions, permissionFlags: number, callback: AsyncCallback&lt;void&gt;): void

撤销应用user grant权限。使用callback异步回调。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.REVOKE_SENSITIVE_PERMISSIONS，仅系统应用可用。

**系统能力：** SystemCapability.Security.AccessToken

**参数：**

| 参数名    | 类型                | 必填 | 说明                          |
| --------- | ------------------- | ---- | ------------------------------------------------------------ |
| tokenID      | number              | 是   | 目标应用的身份标识。可通过应用的[ApplicationInfo](js-apis-bundleManager-applicationInfo.md)获得。           |
| permissionName | Permissions              | 是   | 被撤销的权限名称，合法的权限名取值可在[系统权限定义列表](../../security/permission-list.md)中查询。 |
| permissionFlags  | number | 是   | 授权选项<br>- 0表示权限未经过用户主动设置。<br>- 1表示当次用户若选择禁止该权限，下次权限弹窗仍可以弹出申请用户授权。<br>- 2表示当次用户若选择禁止该权限，下次不会再弹出权限弹窗，需要用户在setting的权限管理中进行授权。<br>- 4表示当次权限设置为系统授权，用户不可更改这个权限授权状态。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 撤销应用user grant权限。当撤销权限成功时，err为undefined；否则为错误对象。 |

**错误码：**

以下错误码的详细介绍请参见[程序访问控制错误码](../errorcodes/errorcode-access-token.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 12100001 | The parameter is invalid. The tokenID is 0, or the string size of permissionName is larger than 256, or the flags value is invalid. |
| 12100002 | TokenId does not exist. |
| 12100003 | Permission does not exist. |
| 12100006 | The application specified by the tokenID is not allowed to be revoked with the specified permission. Either the application is a sandbox or the tokenID is from a remote device. |
| 12100007 | Service is abnormal. |

**示例：**

```ts
import abilityAccessCtrl from '@ohos.abilityAccessCtrl';
import { BusinessError } from '@ohos.base';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let tokenID: number = 0; // 系统应用可以通过bundleManager.getApplicationInfo获取,普通应用可以通过bundleManager.getBundleInfoForSelf获取
let permissionFlags: number = 1;
try {
    atManager.revokeUserGrantedPermission(tokenID, "ohos.permission.GRANT_SENSITIVE_PERMISSIONS", permissionFlags, (err: BusinessError, data: void) => {
        if (err) {
            console.log(`revokeUserGrantedPermission fail, err->${JSON.stringify(err)}`);
        } else {
            console.log('revokeUserGrantedPermission success');
        }
    });
} catch(err) {
    console.log(`catch err->${JSON.stringify(err)}`);
}
```

### getPermissionFlags

getPermissionFlags(tokenID: number, permissionName: Permissions): Promise&lt;number&gt;

获取指定应用的指定权限的flag。使用Promise异步回调。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.GET_SENSITIVE_PERMISSIONS or ohos.permission.GRANT_SENSITIVE_PERMISSIONS or ohos.permission.REVOKE_SENSITIVE_PERMISSIONS，仅系统应用可用。

**系统能力：** SystemCapability.Security.AccessToken

**参数：**

| 参数名    | 类型                | 必填 | 说明                          |
| --------- | ------------------- | ---- | ------------------------------------------------------------ |
| tokenID      | number              | 是   | 目标应用的身份标识。可通过应用的[ApplicationInfo](js-apis-bundleManager-applicationInfo.md)获得。            |
| permissionName | Permissions              | 是   | 查询的权限名称，合法的权限名取值可在[系统权限定义列表](../../security/permission-list.md)中查询。 |

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| Promise&lt;number&gt; | Promise对象。返回查询结果。 |

**错误码：**

以下错误码的详细介绍请参见[程序访问控制错误码](../errorcodes/errorcode-access-token.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 12100001 | The parameter is invalid. The tokenID is 0, or the string size of permissionName is larger than 256. |
| 12100002 | The specified tokenID does not exist. |
| 12100003 | The specified permission does not exist. |
| 12100006 | The operation is not allowed. Either the application is a sandbox or the tokenID is from a remote device. |
| 12100007 | Service is abnormal. |

**示例：**

```ts
import abilityAccessCtrl from '@ohos.abilityAccessCtrl';
import { BusinessError } from '@ohos.base';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let tokenID: number = 0; // 系统应用可以通过bundleManager.getApplicationInfo获取,普通应用可以通过bundleManager.getBundleInfoForSelf获取
try {
    atManager.getPermissionFlags(tokenID, "ohos.permission.GRANT_SENSITIVE_PERMISSIONS").then((data: number) => {
        console.log(`getPermissionFlags success, data->${JSON.stringify(data)}`);
    }).catch((err: BusinessError) => {
        console.log(`getPermissionFlags fail, err->${JSON.stringify(err)}`);
    });
} catch(err) {
    console.log(`catch err->${JSON.stringify(err)}`);
}
```

### getVersion<sup>9+</sup>

getVersion(): Promise&lt;number&gt;

获取当前权限管理的数据版本。使用Promise异步回调。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.Security.AccessToken

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| Promise&lt;number&gt; | Promise对象。返回查询到的版本号。 |

**示例：**

```ts
import abilityAccessCtrl from '@ohos.abilityAccessCtrl';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let promise = atManager.getVersion();
promise.then((data: number) => {
    console.log(`promise: data->${JSON.stringify(data)}`);
});
```

### on<sup>9+</sup>

on(type: 'permissionStateChange', tokenIDList: Array&lt;number&gt;, permissionList: Array&lt;Permissions&gt;, callback: Callback&lt;PermissionStateChangeInfo&gt;): void;

订阅指定tokenId列表与权限列表的权限状态变更事件。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.GET_SENSITIVE_PERMISSIONS，仅系统应用可用。

**系统能力：** SystemCapability.Security.AccessToken

**参数：**

| 参数名             | 类型                   | 必填 | 说明                                                          |
| ------------------ | --------------------- | ---- | ------------------------------------------------------------ |
| type               | string                | 是   | 订阅事件类型，固定为'permissionStateChange'，权限状态变更事件。  |
| tokenIDList        | Array&lt;number&gt;   | 是   | 订阅的tokenId列表，为空时表示订阅所有的应用的权限状态变化。        |
| permissionList | Array&lt;Permissions&gt;   | 是   | 订阅的权限名列表，为空时表示订阅所有的权限状态变化。               |
| callback | Callback&lt;[PermissionStateChangeInfo](#permissionstatechangeinfo9)&gt; | 是 | 订阅指定tokenId与指定权限名状态变更事件的回调。|

**错误码：**

以下错误码的详细介绍请参见[程序访问控制错误码](../errorcodes/errorcode-access-token.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 12100001 | The parameter is invalid. The tokenID is 0, or the string size of permissionName is larger than 256. |
| 12100004 | The interface is called repeatedly with the same input. |
| 12100005 | The registration time has exceeded the limitation. |
| 12100007 | Service is abnormal. |
| 12100008 | Out of memory. |

**示例：**

```ts
import abilityAccessCtrl, { Permissions } from '@ohos.abilityAccessCtrl';
import bundleManager from '@ohos.bundle.bundleManager';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let appInfo: bundleManager.ApplicationInfo = bundleManager.getApplicationInfoSync('com.example.myapplication', 0, 100);
let tokenIDList: Array<number> = [appInfo.accessTokenId];
let permissionList: Array<Permissions> = ["ohos.permission.DISTRIBUTED_DATASYNC"];
try {
    atManager.on('permissionStateChange', tokenIDList, permissionList, (data: abilityAccessCtrl.PermissionStateChangeInfo) => {
        console.debug("receive permission state change, data:" + JSON.stringify(data));
    });
} catch(err) {
    console.log(`catch err->${JSON.stringify(err)}`);
}
```

### off<sup>9+</sup>

off(type: 'permissionStateChange', tokenIDList: Array&lt;number&gt;, permissionList: Array&lt;Permissions&gt;, callback?: Callback&lt;PermissionStateChangeInfo&gt;): void;

取消订阅指定tokenId列表与权限列表的权限状态变更事件，使用callback回调异步返回结果。

**系统接口：** 此接口为系统接口。

**需要权限：** ohos.permission.GET_SENSITIVE_PERMISSIONS，仅系统应用可用。

**系统能力：** SystemCapability.Security.AccessToken

**参数：**

| 参数名             | 类型                   | 必填 | 说明                                                          |
| ------------------ | --------------------- | ---- | ------------------------------------------------------------ |
| type               | string                | 是   | 订阅事件类型，固定为'permissionStateChange'，权限状态变更事件。  |
| tokenIDList        | Array&lt;number&gt;   | 是   | 订阅的tokenId列表，为空时表示订阅所有的应用的权限状态变化，必须与on的输入一致。 |
| permissionList | Array&lt;Permissions&gt;   | 是   | 订阅的权限名列表，为空时表示订阅所有的权限状态变化，必须与on的输入一致。 |
| callback | Callback&lt;[PermissionStateChangeInfo](#permissionstatechangeinfo9)&gt; | 否 | 取消订阅指定tokenId与指定权限名状态变更事件的回调。|

**错误码：**

以下错误码的详细介绍请参见[程序访问控制错误码](../errorcodes/errorcode-access-token.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 12100001 | The parameter is invalid. The tokenID in list is all invalid, or the permissionName in list is all invalid. |
| 12100004 | The interface is not used together with "on". |
| 12100007 | Service is abnormal. |
| 12100008 | Out of memory. |

**示例：**

```ts
import abilityAccessCtrl, { Permissions } from '@ohos.abilityAccessCtrl';
import bundleManager from '@ohos.bundle.bundleManager';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
let appInfo: bundleManager.ApplicationInfo = bundleManager.getApplicationInfoSync('com.example.myapplication', 0, 100);
let tokenIDList: Array<number> = [appInfo.accessTokenId];
let permissionList: Array<Permissions> = ["ohos.permission.DISTRIBUTED_DATASYNC"];
try {
    atManager.off('permissionStateChange', tokenIDList, permissionList);
} catch(err) {
    console.log(`catch err->${JSON.stringify(err)}`);
}
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
| permissionName | Permissions | 是   | 需要校验的权限名称，合法的权限名取值可在[系统权限定义列表](../../security/permission-list.md)中查询。 |

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
try {
    atManager.verifyAccessToken(tokenID, permissionName).then((data: abilityAccessCtrl.GrantStatus) => {
        console.log(`promise: data->${JSON.stringify(data)}`);
    }).catch((err: BusinessError) => {
        console.log(`verifyAccessToken fail, err->${JSON.stringify(err)}`);
    });
}catch(err) {
    console.log(`catch err->${JSON.stringify(err)}`);
}
```

### requestPermissionsFromUser<sup>9+</sup>

requestPermissionsFromUser(context: Context, permissionList: Array&lt;Permissions&gt;, requestCallback: AsyncCallback&lt;PermissionRequestResult&gt;) : void;

用于UIAbility拉起弹框请求用户授权。使用callback异步回调。
> **说明：**
>
> 非UIAbility不支持调用本函数。

**模型约束**：此接口仅可在Stage模型下使用。

**系统能力**: SystemCapability.Security.AccessToken

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| context | Context | 是 | 请求权限的UIAbility的UIAbilityContext。 |
| permissionList | Array&lt;Permissions&gt; | 是 | 权限名列表，合法的权限名取值可在[系统权限定义列表](../../security/permission-list.md)中查询。 |
| callback | AsyncCallback&lt;[PermissionRequestResult](js-apis-permissionrequestresult.md)&gt; | 是 | 回调函数，返回接口调用是否成功的结果。 |

**错误码：**

以下错误码的详细介绍请参见[程序访问控制错误码](../errorcodes/errorcode-access-token.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 12100001 | The parameter is invalid. The context is invalid when it does not belong to the application itself. |

**示例：**

ArkTS语法不支持直接使用globalThis，需要通过一个单例的map来做中转。开发者需要：

   a. 在EntryAbility.ets中导入构建的单例对象GlobalThis。
      ```ts
       import { GlobalThis } from '../utils/globalThis'; // 需要根据globalThis.ets的路径自行适配
      ```
   b. 在onCreate中添加:
      ```ts
       GlobalThis.getInstance().setContext('context', this.context);
      ```

   > **说明：**
   >
   > 由于在ts中引入ets文件会有告警提示，需要将EntryAbility.ts的文件后缀修改为EntryAbility.ets，并在module.json5中同步修改。

**globalThis.ets示例代码如下：**
```ts
import { Context } from '@ohos.abilityAccessCtrl';

// 构造单例对象
export class GlobalThis {
    private constructor() {}
    private static instance: GlobalThis;
    private _uiContexts = new Map<string, Context>();

    public static getInstance(): GlobalThis {
    if (!GlobalThis.instance) {
        GlobalThis.instance = new GlobalThis();
    }
    return GlobalThis.instance;
    }

    getContext(key: string): Context | undefined {
    return this._uiContexts.get(key);
    }

    setContext(key: string, value: Context): void {
    this._uiContexts.set(key, value);
    }

    // 其他需要传递的内容依此扩展
}
```

```ts
import abilityAccessCtrl, { Context, PermissionRequestResult } from '@ohos.abilityAccessCtrl';
import { BusinessError } from '@ohos.base';
import common from '@ohos.app.ability.common';
import { GlobalThis } from '../utils/globalThis';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
try {
    let context: Context = GlobalThis.getInstance().getContext('context');
    atManager.requestPermissionsFromUser(context, ['ohos.permission.CAMERA'], (err: BusinessError, data: PermissionRequestResult)=>{
        console.info('data:' + JSON.stringify(data));
        console.info('data permissions:' + data.permissions);
        console.info('data authResults:' + data.authResults);
} catch(err) {
    console.log(`catch err->${JSON.stringify(err)}`);
}
```

### requestPermissionsFromUser<sup>9+</sup>

requestPermissionsFromUser(context: Context, permissionList: Array&lt;Permissions&gt;) : Promise&lt;PermissionRequestResult&gt;;

用于UIAbility拉起弹框请求用户授权。使用promise异步回调。

> **说明：**
>
> 非UIAbility不支持调用本函数。

**模型约束**：此接口仅可在Stage模型下使用。

**系统能力**: SystemCapability.Security.AccessToken

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| context | Context | 是 | 请求权限的UIAbility的UIAbilityContext。 |
| permissionList | Array&lt;Permissions&gt; | 是 | 需要校验的权限名称，合法的权限名取值可在[系统权限定义列表](../../security/permission-list.md)中查询。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;[PermissionRequestResult](js-apis-permissionrequestresult.md)&gt; | 返回一个Promise，包含接口的结果。 |

**错误码：**

以下错误码的详细介绍请参见[程序访问控制错误码](../errorcodes/errorcode-access-token.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 12100001 | The parameter is invalid. The context is invalid when it does not belong to the application itself. |

**示例：**

修改EntryAbility.ets和导入GlobalThis等步骤同上，此处不再重复

```ts
import abilityAccessCtrl, { Context, PermissionRequestResult } from '@ohos.abilityAccessCtrl';
import { BusinessError } from '@ohos.base';
import { GlobalThis } from '../utils/globalThis';

let atManager: abilityAccessCtrl.AtManager = abilityAccessCtrl.createAtManager();
try {
    let context: Context = GlobalThis.getInstance().getContext('context');
    atManager.requestPermissionsFromUser(context, ['ohos.permission.CAMERA']).then((data: PermissionRequestResult) => {
        console.info("data:" + JSON.stringify(data));
        console.info("data permissions:" + data.permissions);
        console.info("data authResults:" + data.authResults);
    }).catch((err: BusinessError) => {
        console.info("data:" + JSON.stringify(err));
    })
} catch(err) {
    console.log(`catch err->${JSON.stringify(err)}`);
}
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
| permissionName | string | 是   | 需要校验的权限名称。 |

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
try {
    atManager.verifyAccessToken(tokenID, 'ohos.permission.GRANT_SENSITIVE_PERMISSIONS').then((data: abilityAccessCtrl.GrantStatus) => {
        console.log(`promise: data->${JSON.stringify(data)}`);
    }).catch((err: BusinessError) => {
        console.log(`verifyAccessToken fail, err->${JSON.stringify(err)}`);
    });
}catch(err) {
    console.log(`catch err->${JSON.stringify(err)}`);
}
```

### GrantStatus

表示授权状态的枚举。

**系统能力：** SystemCapability.Security.AccessToken

| 名称               |    值 | 说明        |
| ------------------ | ----- | ----------- |
| PERMISSION_DENIED  | -1    | 表示未授权。 |
| PERMISSION_GRANTED | 0     | 表示已授权。 |

### PermissionStateChangeType<sup>9+</sup>

表示权限授权状态变化操作类型的枚举。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.Security.AccessToken

| 名称                     |    值 | 说明              |
| ----------------------- | ------ | ----------------- |
| PERMISSION_REVOKED_OPER | 0      | 表示权限取消操作。 |
| PERMISSION_GRANTED_OPER | 1      | 表示权限授予操作。 |

### PermissionStateChangeInfo<sup>9+</sup>

表示某次权限授权状态变化的详情。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.Security.AccessToken

| 名称           | 类型                       | 可读 | 可写 | 说明                |
| -------------- | ------------------------- | ---- | ---- | ------------------ |
| change         | [PermissionStateChangeType](#permissionstatechangetype9) | 是   | 否   | 权限授权状态变化类型。        |
| tokenID        | number                    | 是   | 否   | 被订阅的应用身份标识。 |
| permissionName | Permissions                    | 是   | 否   | 当前授权状态发生变化的权限名，合法的权限名取值可在[系统权限定义列表](../../security/permission-list.md)中查询。 |
