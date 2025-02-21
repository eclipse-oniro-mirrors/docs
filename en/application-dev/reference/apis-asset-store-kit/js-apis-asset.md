# @ohos.security.asset (Asset Store Service)

The asset store service (ASSET) provides secure storage and management of sensitive data less than 1024 bytes in size, including passwords, app tokens, and other critical data (such as bank card numbers).

>  **NOTE**
>
> The initial APIs of this module are supported since API version 11. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```typescript
import { asset } from '@kit.AssetStoreKit';
```

## asset.add

add(attributes: AssetMap): Promise\<void>

Add an asset. This API uses a promise to return the result.

**System capability**: SystemCapability.Security.Asset

| Name    | Type    | Mandatory| Description                                                        |
| ---------- | -------- | ---- | ------------------------------------------------------------ |
| attributes | [AssetMap](#assetmap) | Yes  | Attributes of the asset to add, including the asset plaintext, access control attributes, and custom data.|

**Return value**

| Type         | Description                   |
| ------------- | ----------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Asset Store Service Error Codes](errorcode-asset.md).

| ID| Error Message                                                  |
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

**Example**

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

Removes one or more assets. This API uses a promise to return the result.

**System capability**: SystemCapability.Security.Asset

| Name| Type    | Mandatory| Description                                                  |
| ------ | -------- | ---- | ------------------------------------------------------ |
| query  | [AssetMap](#assetmap) | Yes  | Attributes of the asset to remove, such as the asset alias, access control attributes, and custom data.|

**Return value**

| Type         | Description                   |
| ------------- | ----------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Asset Store Service Error Codes](errorcode-asset.md).

| ID| Error Message                                                  |
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

**Example**

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

Updates an asset. This API uses a promise to return the result.

**System capability**: SystemCapability.Security.Asset

| Name            | Type    | Mandatory| Description                                                        |
| ------------------ | -------- | ---- | ------------------------------------------------------------ |
| query              | [AssetMap](#assetmap) | Yes  | Attributes of the asset to update, such as the asset alias, access control attributes, and custom data.|
| attributesToUpdate | [AssetMap](#assetmap) | Yes  | New attributes of the asset, such as the asset plaintext and custom data.      |

**Return value**

| Type         | Description                   |
| ------------- | ----------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Asset Store Service Error Codes](errorcode-asset.md).

| ID| Error Message                                                  |
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

**Example**

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

Performs preprocessing for the asset query. This API is used when user authentication is required for the access to the asset. After the user authentication is successful, call [asset.query](#assetquery) and [asset.postQuery](#assetpostquery). This API uses a promise to return the result.

**System capability**: SystemCapability.Security.Asset

| Name| Type    | Mandatory| Description                                                  |
| ------ | -------- | ---- | ------------------------------------------------------ |
| query  | [AssetMap](#assetmap) | Yes  | Attributes of the asset to query, such as the asset alias, access control attributes, and custom data.|

**Return value**

| Type               | Description                                                 |
| ------------------- | ----------------------------------------------------- |
| Promise\<Uint8Array> | Promise used to return a challenge value.<br>**NOTE**: The challenge value is used for subsequent user authentication.|

**Error codes**

For details about the error codes, see [Asset Store Service Error Codes](errorcode-asset.md).

| ID| Error Message                                                    |
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

**Example**

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

Queries one or more assets. If user authentication is required for the access to the asset, call [asset.preQuery](#assetprequery) before this API and call [asset.postQuery](#assetpostquery) after this API. For details about the development procedure, see [Querying an Asset with User Authentication](../../security/AssetStoreKit/asset-js-query-auth.md). This API uses a promise to return the result.

**System capability**: SystemCapability.Security.Asset

| Name  | Type                           | Mandatory| Description                                                        |
| -------- | ------------------------------- | ---- | ------------------------------------------------------------ |
| query    | [AssetMap](#assetmap)           | Yes  | Attributes of the asset to query, such as the asset alias, access control attributes, and custom data.      |

**Return value**

| Type                    | Description                                 |
| ------------------------ | ------------------------------------- |
| Promise\<Array\<AssetMap>> | Promise used to return the result obtained.|

**Error codes**

For details about the error codes, see [Asset Store Service Error Codes](errorcode-asset.md).

| ID| Error Message                                                  |
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

**Example**

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

Performs postprocessing for the asset query. This API is used when user authentication is required for the access to the asset. This API must be used with [asset.preQuery](#assetprequery) together. This API uses a promise to return the result.

**System capability**: SystemCapability.Security.Asset

| Name| Type    | Mandatory| Description                                                        |
| ------ | -------- | ---- | ------------------------------------------------------------ |
| handle | [AssetMap](#assetmap) | Yes  | Handle of the query operation, including the challenge value returned by [asset.preQuery](#assetprequery).|

**Return value**

| Type         | Description                   |
| ------------- | ----------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Asset Store Service Error Codes](errorcode-asset.md).

| ID| Error Message                                                  |
| -------- | ---------------------------------------------------------- |
| 401      | The argument is invalid.                                   |
| 24000001 | The ASSET Service is unavailable.                          |
| 24000006 | Insufficient memory.                                       |
| 24000010 | IPC communication is failed                                |
| 24000011 | The operation of calling Bundle Manager Service is failed. |
| 24000012 | The operation of calling OS Account Service is failed.     |
| 24000013 | The operation of calling Access Token Service is failed.   |

**Example**

```typescript
import { asset } from '@kit.AssetStoreKit';
import { BusinessError } from '@kit.BasicServicesKit';

let handle: asset.AssetMap = new Map();
// The new Uint8Array(32) is only an example. Pass in the challenge value returned by asset.preQuery.
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

Enumerates the types of the keys of asset attributes.

**System capability**: SystemCapability.Security.Asset

| Name  | Value        | Description                                    |
| ------ | ---------- | ---------------------------------------- |
| BOOL   | 0x01 << 28 | Boolean.    |
| NUMBER | 0x02 << 28 | Number.    |
| BYTES  | 0x03 << 28 | Byte array.|

## Tag

Enumerate the keys of asset attributes ([AssetMap](#assetmap)), which are in key-value (KV) pairs.

**System capability**: SystemCapability.Security.Asset

| Name| Value                                 | Description                                                        |
| ------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| SECRET                    | TagType.BYTES &#124; 0x01  | Asset plaintext.                                                |
| ALIAS                     | TagType.BYTES &#124; 0x02 | Asset alias, which uniquely identifies an asset.                        |
| ACCESSIBILITY             | TagType.NUMBER &#124; 0x03 | Access control based on the lock screen status.                                      |
| REQUIRE_PASSWORD_SET      | TagType.BOOL &#124; 0x04                   | Whether the asset is accessible only when a lock screen password is set.                |
| AUTH_TYPE                 | TagType.NUMBER &#124; 0x05 | Type of user authentication required for accessing the asset.                              |
| AUTH_VALIDITY_PERIOD      | TagType.NUMBER &#124; 0x06 | Validity period of the user authentication.                                            |
| AUTH_CHALLENGE            | TagType.BYTES &#124; 0x07     | Challenge for the user authentication.                                        |
| AUTH_TOKEN                | TagType.BYTES &#124; 0x08    | Authorization token obtained after the user authentication is successful.                                          |
| SYNC_TYPE                 | TagType.NUMBER &#124; 0x10 | Type of sync supported by the asset.                                      |
| IS_PERSISTENT             | TagType.BOOL &#124; 0x11                         | Whether to retain the asset when the application is uninstalled.<br>**Required permissions**: ohos.permission.STORE_PERSISTENT_DATA<br>**NOTE**: Permission verification is required only when [asset.add](#assetadd) is called with this attribute passed in.|
| DATA_LABEL_CRITICAL_1     | TagType.BYTES &#124; 0x20 | Additional asset data customized by the service with integrity protection.            |
| DATA_LABEL_CRITICAL_2 | TagType.BYTES &#124; 0x21 | Additional asset data customized by the service with integrity protection.|
| DATA_LABEL_CRITICAL_3 | TagType.BYTES &#124; 0x22 | Additional asset data customized by the service with integrity protection.|
| DATA_LABEL_CRITICAL_4 | TagType.BYTES &#124; 0x23  | Additional asset data customized by the service with integrity protection.|
| DATA_LABEL_NORMAL_1       | TagType.BYTES &#124; 0x30 | Additional data of the asset customized by the service without integrity protection.            |
| DATA_LABEL_NORMAL_2 | TagType.BYTES &#124; 0x31 | Additional data of the asset customized by the service without integrity protection.|
| DATA_LABEL_NORMAL_3 | TagType.BYTES &#124; 0x32 | Additional data of the asset customized by the service without integrity protection.|
| DATA_LABEL_NORMAL_4 | TagType.BYTES &#124; 0x33  | Additional data of the asset customized by the service without integrity protection.|
| RETURN_TYPE               | TagType.NUMBER &#124; 0x40 | Type of the asset query result to return.                                        |
| RETURN_LIMIT              | TagType.NUMBER &#124; 0x41                      | Maximum number of asset records to return.                                        |
| RETURN_OFFSET             | TagType.NUMBER &#124; 0x42   | Offset of the asset query result.<br>**NOTE**: This parameter specifies the starting asset record to return in batch asset query.                                |
| RETURN_ORDERED_BY         | TagType.NUMBER &#124; 0x43 | How the query results are sorted. Currently, the results can be sorted only by **DATA_LABEL**.<br>**NOTE**: By default, assets are returned in the order in which they are added.|
| CONFLICT_RESOLUTION       | TagType.NUMBER &#124; 0x44 | Policy for resolving the conflict (for example, a duplicate alias).                            |

## Value

type Value = boolean | number | Uint8Array;

Represents the value of each attribute in [AssetMap](#assetmap).

**System capability**: SystemCapability.Security.Asset

## AssetMap

type AssetMap = Map\<Tag, Value>

Represents a set of asset attributes in KV pairs.

**System capability**: SystemCapability.Security.Asset

## Accessibility

Enumerates the types of access control based on the lock screen status.

**System capability**: SystemCapability.Security.Asset

| Name                 | Value  | Description                                                        |
| --------------------- | ---- | ------------------------------------------------------------ |
| DEVICE_POWERED_ON     | 0    | The asset can be accessed after the device is powered on.                                  |
| DEVICE_FIRST_UNLOCKED | 1    | The asset can be accessed only after the device is unlocked for the first time.<br>**NOTE**: If no lock screen password is set, this option is equivalent to **DEVICE_POWERED_ON**.|
| DEVICE_UNLOCKED       | 2    | The asset can be accessed only when the device is unlocked.<br>**NOTE**: If no lock screen password is set, this option is equivalent to **DEVICE_POWERED_ON**.|

## AuthType

Enumerates the types of user authentication supported by an asset.

**System capability**: SystemCapability.Security.Asset

| Name| Value  | Description                                                        |
| ---- | ---- | ------------------------------------------------------------ |
| NONE | 0    | No user authentication is required before the asset is accessed.                                |
| ANY  | 255  | The asset can be accessed if any user authentication (such as PIN, facial, or fingerprint authentication) is successful.|

## SyncType

Enumerates the sync types supported by an asset.

> **NOTE**
>
> This field is an embedded parameter. Currently, asset sync is not supported.

**System capability**: SystemCapability.Security.Asset

| Name          | Value    | Description                                            |
| -------------- | ------ | ------------------------------------------------ |
| NEVER          | 0      | Asset sync is not allowed.                            |
| THIS_DEVICE    | 1 << 0 | Asset sync is allowed only on the local device, for example, in data restore on the local device.|
| TRUSTED_DEVICE | 1 << 1 | Asset sync is allowed only between trusted devices, for example, in the case of cloning.            |

## ReturnType

Enumerates the type of information returned by an asset query operation.

**System capability**: SystemCapability.Security.Asset

| Name      | Value  | Description                                                        |
| ---------- | ---- | ------------------------------------------------------------ |
| ALL        | 0    | The query result contains the asset plaintext and its attributes.<br>**NOTE**: Use this option when you need to query the plaintext of a single asset.|
| ATTRIBUTES | 1    | The query result contains only the asset attributes.<br>**NOTE**: Use this option when you need to query attributes of multiple assets.|

## ConflictResolution

Enumerates the policies for resolving conflicts (for example, a duplicate alias) when an asset is added.

**System capability**: SystemCapability.Security.Asset

| Name       | Value  | Description                        |
| ----------- | ---- | ---------------------------- |
| OVERWRITE   | 0    | Overwrite the original asset.   |
| THROW_ERROR | 1    | Throw an exception for the service to perform subsequent processing.|
