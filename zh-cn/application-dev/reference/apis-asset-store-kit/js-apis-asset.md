# @ohos.security.asset (关键资产存储服务)

关键资产存储服务提供了用户短敏感数据的安全存储及管理能力。其中，短敏感数据可以是密码类（账号/密码）、Token类（应用凭据）、其他关键明文（如银行卡号）等长度较短的用户敏感数据。

>  **说明：**
>
> 本模块首批接口从API version 11 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```typescript
import { asset } from '@kit.AssetStoreKit';
```

## asset.add

add(attributes: AssetMap): Promise\<void>

新增一条关键资产，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Security.Asset

| 参数名     | 类型     | 必填 | 说明                                                         |
| ---------- | -------- | ---- | ------------------------------------------------------------ |
| attributes | [AssetMap](#assetmap) | 是   | 待新增关键资产的属性集合，包括关键资产明文、访问控制属性、自定义数据等。 |

**返回值：**

| 类型          | 说明                    |
| ------------- | ----------------------- |
| Promise\<void> | Promise对象，无返回值。 |

**错误码：**

以下错误码的详细介绍请参见[关键资产存储服务错误码](errorcode-asset.md)

| 错误码ID | 错误信息                                                   |
| -------- | ---------------------------------------------------------- |
| 201      | The caller doesn't have the permission.                    |
| 401      | The argument is invalid.                                   |
| 24000001 | The ASSET Service is unavailable.                          |
| 24000003 | The Asset already exists.                                  |
| 24000005 | The screen lock status mismatches.                         |
| 24000006 | Insufficient memory.                                       |
| 24000007 | The Asset is corrupted.                                    |
| 24000008 | The database operation is failed.                          |
| 24000009 | The cryptography operation is failed.                      |
| 24000010 | IPC communication is failed                                |
| 24000011 | The operation of calling Bundle Manager Service is failed. |
| 24000012 | The operation of calling OS Account Service is failed.     |
| 24000013 | The operation of calling Access Token Service is failed.   |
| 24000014 | The operation of file is failed.                           |
| 24000015 | The operation of getting system time is failed.            |

**示例代码：**

```typescript
import { asset } from '@kit.AssetStoreKit';
import { util } from '@kit.ArkTS';
import { BusinessError } from '@kit.BasicServicesKit';

function stringToArray(str: string): Uint8Array {
  let textEncoder = new util.TextEncoder();
  return textEncoder.encodeInto(str);
}

let attr: asset.AssetMap = new Map();
attr.set(asset.Tag.SECRET, stringToArray('demo_pwd'));
attr.set(asset.Tag.ALIAS, stringToArray('demo_alias'));
attr.set(asset.Tag.ACCESSIBILITY, asset.Accessibility.DEVICE_FIRST_UNLOCKED);
attr.set(asset.Tag.DATA_LABEL_NORMAL_1, stringToArray('demo_label'));
try {
  asset.add(attr).then(() => {
    console.info(`Asset added successfully.`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to add Asset. Code is ${err.code}, message is ${err.message}`);
  })
} catch (error) {
  let err = error as BusinessError;
  console.error(`Failed to add Asset. Code is ${err.code}, message is ${err.message}`);
}
```

## asset.remove

remove(query: AssetMap): Promise\<void>

删除符合条件的一条或多条关键资产，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Security.Asset

| 参数名 | 类型     | 必填 | 说明                                                   |
| ------ | -------- | ---- | ------------------------------------------------------ |
| query  | [AssetMap](#assetmap) | 是   | 待删除关键资产的搜索条件，如别名、访问控制属性、自定义数据等。 |

**返回值：**

| 类型          | 说明                    |
| ------------- | ----------------------- |
| Promise\<void> | Promise对象，无返回值。 |

**错误码：**

以下错误码的详细介绍请参见[关键资产存储服务错误码](errorcode-asset.md)

| 错误码ID | 错误信息                                                   |
| -------- | ---------------------------------------------------------- |
| 401      | The argument is invalid.                                   |
| 24000001 | The ASSET Service is unavailable.                          |
| 24000002 | The queried Asset can not be found.                        |
| 24000006 | Insufficient memory.                                       |
| 24000007 | The Asset is corrupted.                                    |
| 24000008 | The database operation is failed.                          |
| 24000009 | The cryptography operation is failed.                      |
| 24000010 | IPC communication is failed                                |
| 24000011 | The operation of calling Bundle Manager Service is failed. |
| 24000012 | The operation of calling OS Account Service is failed.     |
| 24000013 | The operation of calling Access Token Service is failed.   |

**示例代码：**

```typescript
import { asset } from '@kit.AssetStoreKit';
import { util } from '@kit.ArkTS';
import { BusinessError } from '@kit.BasicServicesKit';

function stringToArray(str: string): Uint8Array {
  let textEncoder = new util.TextEncoder();
  return textEncoder.encodeInto(str);
}

let query: asset.AssetMap = new Map();
query.set(asset.Tag.ALIAS, stringToArray('demo_alias'));
try {
  asset.remove(query).then(() => {
    console.info(`Asset removed successfully.`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to remove Asset. Code is ${err.code}, message is ${err.message}`);
  });
} catch (error) {
  let err = error as BusinessError;
  console.error(`Failed to remove Asset. Code is ${err.code}, message is ${err.message}`);
}
```

## asset.update

update(query: AssetMap, attributesToUpdate: AssetMap): Promise\<void>

更新符合条件的一条关键资产，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Security.Asset

| 参数名             | 类型     | 必填 | 说明                                                         |
| ------------------ | -------- | ---- | ------------------------------------------------------------ |
| query              | [AssetMap](#assetmap) | 是   | 待更新关键资产的搜索条件，如关键资产别名、访问控制属性、自定义数据等。 |
| attributesToUpdate | [AssetMap](#assetmap) | 是   | 待更新关键资产的属性集合，如关键资产明文、自定义数据等。       |

**返回值：**

| 类型          | 说明                    |
| ------------- | ----------------------- |
| Promise\<void> | Promise对象，无返回值。 |

**错误码：**

以下错误码的详细介绍请参见[关键资产存储服务错误码](errorcode-asset.md)

| 错误码ID | 错误信息                                                   |
| -------- | ---------------------------------------------------------- |
| 401      | The argument is invalid.                                   |
| 24000001 | The ASSET Service is unavailable.                          |
| 24000002 | The queried Asset can not be found.                        |
| 24000005 | The screen lock status mismatches.                         |
| 24000006 | Insufficient memory.                                       |
| 24000007 | The Asset is corrupted.                                    |
| 24000008 | The database operation is failed.                          |
| 24000009 | The cryptography operation is failed.                      |
| 24000010 | IPC communication is failed                                |
| 24000011 | The operation of calling Bundle Manager Service is failed. |
| 24000012 | The operation of calling OS Account Service is failed.     |
| 24000013 | The operation of calling Access Token Service is failed.   |
| 24000015 | The operation of getting system time is failed.            |

**示例代码：**

```typescript
import { asset } from '@kit.AssetStoreKit';
import { util } from '@kit.ArkTS';
import { BusinessError } from '@kit.BasicServicesKit';

function stringToArray(str: string): Uint8Array {
  let textEncoder = new util.TextEncoder();
  return textEncoder.encodeInto(str);
}

let query: asset.AssetMap = new Map();
query.set(asset.Tag.ALIAS, stringToArray('demo_alias'));
let attrsToUpdate: asset.AssetMap = new Map();
attrsToUpdate.set(asset.Tag.SECRET, stringToArray('demo_pwd_new'));
try {
  asset.update(query, attrsToUpdate).then(() => {
    console.info(`Asset updated successfully.`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to update Asset. Code is ${err.code}, message is ${err.message}`);
  });
} catch (error) {
  let err = error as BusinessError;
  console.error(`Failed to update Asset. Code is ${err.code}, message is ${err.message}`);
}
```

## asset.preQuery

preQuery(query: AssetMap): Promise\<Uint8Array>

查询的预处理，用于需要用户认证的关键资产。在用户认证成功后，应当随后调用[asset.query](#assetquery)、[asset.postQuery](#assetpostquery)。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Security.Asset

| 参数名 | 类型     | 必填 | 说明                                                   |
| ------ | -------- | ---- | ------------------------------------------------------ |
| query  | [AssetMap](#assetmap) | 是   | 关键资产的查询条件，如别名、访问控制属性、自定义数据等。 |

**返回值：**

| 类型                | 说明                                                  |
| ------------------- | ----------------------------------------------------- |
| Promise\<Uint8Array> | Promise对象，返回挑战值。<br>**说明：** 挑战值用于后续用户认证。 |

**错误码：**

以下错误码的详细介绍请参见[关键资产存储服务错误码](errorcode-asset.md)

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401      | The argument is invalid.                                     |
| 24000001 | The ASSET Service is unavailable.                            |
| 24000002 | The queried Asset can not be found.                          |
| 24000005 | The screen lock status mismatches.                           |
| 24000006 | Insufficient memory.                                         |
| 24000007 | The Asset is corrupted.                                      |
| 24000008 | The database operation is failed.                            |
| 24000009 | The cryptography operation is failed.                        |
| 24000010 | IPC communication is failed                                  |
| 24000011 | The operation of calling Bundle Manager Service is failed.   |
| 24000012 | The operation of calling OS Account Service is failed.       |
| 24000013 | The operation of calling Access Token Service is failed.     |
| 24000016 | The cache exceeds the limit.                                 |
| 24000017 | The capability is not supported.                             |

**示例代码：**

```typescript
import { asset } from '@kit.AssetStoreKit';
import { util } from '@kit.ArkTS';
import { BusinessError } from '@kit.BasicServicesKit';

function stringToArray(str: string): Uint8Array {
  let textEncoder = new util.TextEncoder();
  return textEncoder.encodeInto(str);
}

let query: asset.AssetMap = new Map();
query.set(asset.Tag.ALIAS, stringToArray('demo_alias'));
try {
  asset.preQuery(query).then((challenge: Uint8Array) => {
    console.info(`Succeeded in pre-querying Asset.`);
  }).catch ((err: BusinessError) => {
    console.error(`Failed to pre-query Asset. Code is ${err.code}, message is ${err.message}`);
  });
} catch (error) {
  let err = error as BusinessError;
  console.error(`Failed to pre-query Asset. Code is ${err.code}, message is ${err.message}`);
}
```

## asset.query

query(query: AssetMap): Promise\<Array\<AssetMap>>

查询一条或多条符合条件的关键资产。若查询需要用户认证的关键资产，则需要在本函数前调用[asset.preQuery](#assetprequery)，在本函数后调用[asset.postQuery](#assetpostquery)，开发步骤请参考[开发指导](../../security/AssetStoreKit/asset-js-query-auth.md)。使用Promise回调异步返回结果。

**系统能力：** SystemCapability.Security.Asset

| 参数名   | 类型                            | 必填 | 说明                                                         |
| -------- | ------------------------------- | ---- | ------------------------------------------------------------ |
| query    | [AssetMap](#assetmap)           | 是   | 关键资产的查询条件，如别名、访问控制属性、自定义数据等。       |

**返回值：**

| 类型                     | 说明                                  |
| ------------------------ | ------------------------------------- |
| Promise\<Array\<AssetMap>> | Promise对象，返回查询结果列表。 |

**错误码：**

以下错误码的详细介绍请参见[关键资产存储服务错误码](errorcode-asset.md)

| 错误码ID | 错误信息                                                   |
| -------- | ---------------------------------------------------------- |
| 401      | The argument is invalid.                                   |
| 24000001 | The ASSET Service is unavailable.                          |
| 24000002 | The queried Asset can not be found.                        |
| 24000004 | The access to Asset is denied.                             |
| 24000005 | The screen lock status mismatches.                         |
| 24000006 | Insufficient memory.                                       |
| 24000007 | The Asset is corrupted.                                    |
| 24000008 | The database operation is failed.                          |
| 24000009 | The cryptography operation is failed.                      |
| 24000010 | IPC communication is failed                                |
| 24000011 | The operation of calling Bundle Manager Service is failed. |
| 24000012 | The operation of calling OS Account Service is failed.     |
| 24000013 | The operation of calling Access Token Service is failed.   |
| 24000017 | The capability is not supported.                           |

**示例代码：**

```typescript
import { asset } from '@kit.AssetStoreKit';
import { util } from '@kit.ArkTS';
import { BusinessError } from '@kit.BasicServicesKit';

function stringToArray(str: string): Uint8Array {
  let textEncoder = new util.TextEncoder();
  return textEncoder.encodeInto(str);
}

let query: asset.AssetMap = new Map();
query.set(asset.Tag.ALIAS, stringToArray('demo_alias'));
try {
  asset.query(query).then((res: Array<asset.AssetMap>) => {
    for (let i = 0; i < res.length; i++) {
      // parse the attribute.
      let accessibility: number = res[i].get(asset.Tag.ACCESSIBILITY) as number;
    }
    console.info(`Asset query succeeded.`);
  }).catch ((err: BusinessError) => {
    console.error(`Failed to query Asset. Code is ${err.code}, message is ${err.message}`);
  });
} catch (error) {
  let err = error as BusinessError;
  console.error(`Failed to query Asset. Code is ${err.code}, message is ${err.message}`);
}
```

## asset.postQuery

postQuery(handle: AssetMap): Promise\<void>

查询的后置处理，用于需要用户认证的关键资产。需与[asset.preQuery](#assetprequery)函数成对出现。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Security.Asset

| 参数名 | 类型     | 必填 | 说明                                                         |
| ------ | -------- | ---- | ------------------------------------------------------------ |
| handle | [AssetMap](#assetmap) | 是   | 待处理的查询句柄，当前包含[asset.preQuery](#assetprequery)执行成功返回的挑战值。 |

**返回值：**

| 类型          | 说明                    |
| ------------- | ----------------------- |
| Promise\<void> | Promise对象，无返回值。 |

**错误码：**

以下错误码的详细介绍请参见[关键资产存储服务错误码](errorcode-asset.md)

| 错误码ID | 错误信息                                                   |
| -------- | ---------------------------------------------------------- |
| 401      | The argument is invalid.                                   |
| 24000001 | The ASSET Service is unavailable.                          |
| 24000006 | Insufficient memory.                                       |
| 24000010 | IPC communication is failed                                |
| 24000011 | The operation of calling Bundle Manager Service is failed. |
| 24000012 | The operation of calling OS Account Service is failed.     |
| 24000013 | The operation of calling Access Token Service is failed.   |

**示例代码：**

```typescript
import { asset } from '@kit.AssetStoreKit';
import { BusinessError } from '@kit.BasicServicesKit';

let handle: asset.AssetMap = new Map();
// 此处传入的new Uint8Array(32)仅作为示例，实际应传入asset.preQuery执行成功返回的挑战值
handle.set(asset.Tag.AUTH_CHALLENGE, new Uint8Array(32));
try {
  asset.postQuery(handle).then(() => {
    console.info(`Succeeded in post-querying Asset.`);
  }).catch ((err: BusinessError) => {
    console.error(`Failed to post-query Asset. Code is ${err.code}, message is ${err.message}`);
  });
} catch (error) {
  let err = error as BusinessError;
  console.error(`Failed to post-query Asset. Code is ${err.code}, message is ${err.message}`);
}
```

## TagType

枚举，关键资产属性支持的数据类型。

**系统能力：** SystemCapability.Security.Asset

| 名称   | 值         | 说明                                     |
| ------ | ---------- | ---------------------------------------- |
| BOOL   | 0x01 << 28 | 标识关键资产属性对应的数据类型是布尔     |
| NUMBER | 0x02 << 28 | 标识关键资产属性对应的数据类型是整型     |
| BYTES  | 0x03 << 28 | 标识关键资产属性对应的数据类型是字节数组 |

## Tag

枚举，关键资产支持的属性名称类型，用作[AssetMap](#assetmap)的键。

**系统能力：** SystemCapability.Security.Asset

| 名称 | 值                                  | 说明                                                         |
| ------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| SECRET                    | TagType.BYTES &#124; 0x01  | 关键资产明文                                                 |
| ALIAS                     | TagType.BYTES &#124; 0x02 | 关键资产别名，每条关键资产的唯一索引                         |
| ACCESSIBILITY             | TagType.NUMBER &#124; 0x03 | 基于锁屏状态的访问控制                                       |
| REQUIRE_PASSWORD_SET      | TagType.BOOL &#124; 0x04                   | 是否仅在设置了锁屏密码的情况下，可访问关键资产                 |
| AUTH_TYPE                 | TagType.NUMBER &#124; 0x05 | 访问关键资产所需的用户认证类型                               |
| AUTH_VALIDITY_PERIOD      | TagType.NUMBER &#124; 0x06 | 用户认证的有效期                                             |
| AUTH_CHALLENGE            | TagType.BYTES &#124; 0x07     | 用户认证的挑战值                                         |
| AUTH_TOKEN                | TagType.BYTES &#124; 0x08    | 用户认证通过的授权令牌                                           |
| SYNC_TYPE                 | TagType.NUMBER &#124; 0x10 | 关键资产支持的同步类型                                       |
| IS_PERSISTENT             | TagType.BOOL &#124; 0x11                         | 在应用卸载时是否需要保留关键资产<br>**需要权限：** ohos.permission.STORE_PERSISTENT_DATA<br/>**备注：** 仅在调用[asset.add](#assetadd)函数并传入该属性时需要校验权限 |
| DATA_LABEL_CRITICAL_1     | TagType.BYTES &#124; 0x20 | 关键资产附属信息，内容由业务自定义且**有完整性保护**             |
| DATA_LABEL_CRITICAL_2 | TagType.BYTES &#124; 0x21 | 关键资产附属信息，内容由业务自定义且**有完整性保护** |
| DATA_LABEL_CRITICAL_3 | TagType.BYTES &#124; 0x22 | 关键资产附属信息，内容由业务自定义且**有完整性保护** |
| DATA_LABEL_CRITICAL_4 | TagType.BYTES &#124; 0x23  | 关键资产附属信息，内容由业务自定义且**有完整性保护** |
| DATA_LABEL_NORMAL_1       | TagType.BYTES &#124; 0x30 | 关键资产附属信息，内容由业务自定义且**无完整性保护**             |
| DATA_LABEL_NORMAL_2 | TagType.BYTES &#124; 0x31 | 关键资产附属信息，内容由业务自定义且**无完整性保护** |
| DATA_LABEL_NORMAL_3 | TagType.BYTES &#124; 0x32 | 关键资产附属信息，内容由业务自定义且**无完整性保护** |
| DATA_LABEL_NORMAL_4 | TagType.BYTES &#124; 0x33  | 关键资产附属信息，内容由业务自定义且**无完整性保护** |
| RETURN_TYPE               | TagType.NUMBER &#124; 0x40 | 关键资产查询返回的结果类型                                         |
| RETURN_LIMIT              | TagType.NUMBER &#124; 0x41                      | 关键资产查询返回的结果数量                                         |
| RETURN_OFFSET             | TagType.NUMBER &#124; 0x42   | 关键资产查询返回的结果偏移量<br>**说明：** 用于分批查询场景，指定从第几个开始返回                                 |
| RETURN_ORDERED_BY         | TagType.NUMBER &#124; 0x43 | 关键资产查询返回的结果排序依据，仅支持按照附属信息排序<br>**说明：** 默认按照关键资产新增的顺序返回。 |
| CONFLICT_RESOLUTION       | TagType.NUMBER &#124; 0x44 | 新增关键资产时的冲突（如：别名相同）处理策略                             |

## Value

type Value = boolean | number | Uint8Array;

关键资产属性的内容，用作[AssetMap](#assetmap)的值。

**系统能力：** SystemCapability.Security.Asset

## AssetMap

type AssetMap = Map\<Tag, Value>

关键资产属性的键-值对集合。

**系统能力：** SystemCapability.Security.Asset

## Accessibility

枚举，关键资产基于锁屏状态的访问控制类型。

**系统能力：** SystemCapability.Security.Asset

| 名称                  | 值   | 说明                                                         |
| --------------------- | ---- | ------------------------------------------------------------ |
| DEVICE_POWERED_ON     | 0    | 开机后可访问                                   |
| DEVICE_FIRST_UNLOCKED | 1    | 首次解锁后可访问<br>**备注：** 未设置锁屏密码时，等同于开机后可访问 |
| DEVICE_UNLOCKED       | 2    | 解锁状态时可访问<br/>**备注：** 未设置锁屏密码时，等同于开机后可访问 |

## AuthType

枚举，关键资产支持的用户认证类型。

**系统能力：** SystemCapability.Security.Asset

| 名称 | 值   | 说明                                                         |
| ---- | ---- | ------------------------------------------------------------ |
| NONE | 0    | 访问关键资产前无需用户认证。                                 |
| ANY  | 255  | 任意一种用户认证方式（PIN码、人脸、指纹等）通过后，均可访问关键资产。 |

## SyncType

枚举，关键资产支持的同步类型。

> **说明：**
>
> 本字段属于能力预埋，当前不支持同步。

**系统能力：** SystemCapability.Security.Asset

| 名称           | 值     | 说明                                             |
| -------------- | ------ | ------------------------------------------------ |
| NEVER          | 0      | 不允许同步关键资产。                             |
| THIS_DEVICE    | 1 << 0 | 只在本设备进行同步，如仅在本设备还原的备份场景。 |
| TRUSTED_DEVICE | 1 << 1 | 只在可信设备间进行同步，如克隆场景。             |

## ReturnType

枚举，关键资产查询返回的结果类型。

**系统能力：** SystemCapability.Security.Asset

| 名称       | 值   | 说明                                                         |
| ---------- | ---- | ------------------------------------------------------------ |
| ALL        | 0    | 返回关键资产明文及属性。<br/>**说明：** 查询单条关键资产明文时，需设置此类型。 |
| ATTRIBUTES | 1    | 返回关键资产属性，不含关键资产明文。<br>**备注：** 批量查询关键资产属性时，需设置此类型。 |

## ConflictResolution

枚举，新增关键资产时的冲突（如：别名相同）处理策略。

**系统能力：** SystemCapability.Security.Asset

| 名称        | 值   | 说明                         |
| ----------- | ---- | ---------------------------- |
| OVERWRITE   | 0    | 覆盖原有的关键资产。    |
| THROW_ERROR | 1    | 抛出异常，由业务进行后续处理。 |
