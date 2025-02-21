# Querying Assets (ArkTS)

## Available APIs

For details about the API, see:

[query(query: AssetMap): Promise\<Array\<AssetMap>>](../../reference/apis-asset-store-kit/js-apis-asset.md#assetquery)

The following table describes the parameters of **AssetMap**.

| Attribute Name (Tag)       | Attribute Content (Value)                    | Mandatory | Description                                                        |
| --------------------- | ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
| ALIAS                 | Type: Uint8Array<br>Length: 1-256 bytes                           | No    | Asset alias, which uniquely identifies an asset.                       |
| ACCESSIBILITY         | Type: number<br>Value range: see [Accessibility](../../reference/apis-asset-store-kit/js-apis-asset.md#accessibility)| No    | Access control based on the lock screen status.                                                |
| REQUIRE_PASSWORD_SET  | Type: bool                                                  | No    | Whether the asset is accessible only when a lock screen password is set.                |
| AUTH_TYPE             | Type: number<br>Value range: see [AuthType](../../reference/apis-asset-store-kit/js-apis-asset.md#authtype)| No    | Type of user authentication required for accessing the asset.                              |
| SYNC_TYPE             | Type: number<br>Value range: see [SyncType](../../reference/apis-asset-store-kit/js-apis-asset.md#synctype)| No    | Type of sync supported by the asset.                                      |
| IS_PERSISTENT         | Type: bool                                                  | No    | Whether to retain the asset when the application is uninstalled.                            |
| DATA_LABEL_CRITICAL_1 | Type: Uint8Array<br>Length: 1-512 bytes                           | No    | Additional asset data customized by the service with integrity protection.            |
| DATA_LABEL_CRITICAL_2 | Type: Uint8Array<br>Length: 1-512 bytes                           | No    | Additional asset data customized by the service with integrity protection.            |
| DATA_LABEL_CRITICAL_3 | Type: Uint8Array<br>Length: 1-512 bytes                           | No    | Additional asset data customized by the service with integrity protection.            |
| DATA_LABEL_CRITICAL_4 | Type: Uint8Array<br>Length: 1-512 bytes                           | No    | Additional asset data customized by the service with integrity protection.            |
| DATA_LABEL_NORMAL_1   | Type: Uint8Array<br>Length: 1-512 bytes                           | No    | Additional asset data customized by the service without integrity protection.            |
| DATA_LABEL_NORMAL_2   | Type: Uint8Array<br>Length: 1-512 bytes                           | No    | Additional asset data customized by the service without integrity protection.            |
| DATA_LABEL_NORMAL_3   | Type: Uint8Array<br>Length: 1-512 bytes                           | No    | Additional asset data customized by the service without integrity protection.            |
| DATA_LABEL_NORMAL_4   | Type: Uint8Array<br>Length: 1-512 bytes                           | No    | Additional asset data customized by the service without integrity protection.            |
| RETURN_TYPE           | Type: number<br>Value range: see [ReturnType](../../reference/apis-asset-store-kit/js-apis-asset.md#returntype)| No    | Type of the asset query result to return.                                        |
| RETURN_LIMIT          | Type: number                                                | No    | Maximum number of asset records to return.                                        |
| RETURN_OFFSET         | Type: number<br>Value range: 1-65536                             | No    | Offset of the asset query result.<br>**NOTE**: This parameter specifies the starting asset record to return in batch asset query.                                |
| RETURN_ORDERED_BY     | Type: number<br>Value: asset.Tag.DATA_LABEL_xxx.            | No    | How the query results are sorted. Currently, the results can be sorted only by **DATA_LABEL**.<br>**NOTE**: By default, assets are returned in the order in which they are added.|

## Example

### Querying the Plaintext of an Asset

Query the plaintext of asset **demo_alias**.

```typescript
import { asset } from '@kit.AssetStoreKit';
import { util } from '@kit.ArkTS';
import { BusinessError } from '@kit.BasicServicesKit';

function stringToArray(str: string): Uint8Array {
  let textEncoder = new util.TextEncoder();
  return textEncoder.encodeInto(str);
}

function arrayToString(arr: Uint8Array): string {
  let textDecoder = util.TextDecoder.create("utf-8", { ignoreBOM: true });
  let str = textDecoder.decodeWithStream(arr, { stream: false })
  return str;
}

let query: asset.AssetMap = new Map();
query.set(asset.Tag.ALIAS, stringToArray('demo_alias')); // Specify the alias of the asset to query.
query.set(asset.Tag.RETURN_TYPE, asset.ReturnType.ALL); // Return all asset information, including attributes and asset plaintext.
try {
  asset.query(query).then((res: Array<asset.AssetMap>) => {
    for (let i = 0; i < res.length; i++) {
      // Parse the secret.
      let secret: Uint8Array = res[i].get(asset.Tag.SECRET) as Uint8Array;
      // Convert uint8array to string
      let secretStr: string = arrayToString(secret);
    }
  }).catch ((err: BusinessError) => {
    console.error(`Failed to query Asset. Code is ${err.code}, message is ${err.message}`);
  });
} catch (error) {
  let err = error as BusinessError;
  console.error(`Failed to query Asset. Code is ${err.code}, message is ${err.message}`);
}
```

### Querying Attributes of an Asset

Query attributes of asset **demo_alias**.

```typescript
import { asset } from '@kit.AssetStoreKit';
import { util } from '@kit.ArkTS';
import { BusinessError } from '@kit.BasicServicesKit';

function stringToArray(str: string): Uint8Array {
  let textEncoder = new util.TextEncoder();
  return textEncoder.encodeInto(str);
}

let query: asset.AssetMap = new Map();
query.set(asset.Tag.ALIAS, stringToArray('demo_alias')); // Specify the alias of the asset to query.
query.set(asset.Tag.RETURN_TYPE, asset.ReturnType.ATTRIBUTES); // Return only the attributes of the asset, that is, the result does not include the asset plaintext.
try {
  asset.query(query).then((res: Array<asset.AssetMap>) => {
    for (let i = 0; i < res.length; i++) {
      // Parse the attributes.
      let accessibility: number = res[i].get(asset.Tag.ACCESSIBILITY) as number;
    }
  }).catch ((err: BusinessError) => {
    console.error(`Failed to query Asset. Code is ${err.code}, message is ${err.message}`);
  });
} catch (error) {
  let err = error as BusinessError;
  console.error(`Failed to query Asset. Code is ${err.code}, message is ${err.message}`);
}
```

### Querying Attributes of Assets

Query attributes of assets with tag 1 of **demo_label** and return a total of 10 records sorted by **DATA_LABEL_NORMAL_1** starting from the fifth record that matches the search criteria.

```typescript
import { asset } from '@kit.AssetStoreKit';
import { util } from '@kit.ArkTS';
import { BusinessError } from '@kit.BasicServicesKit';

function stringToArray(str: string): Uint8Array {
  let textEncoder = new util.TextEncoder();
  return textEncoder.encodeInto(str);
}

let query: asset.AssetMap = new Map();
query.set(asset.Tag.RETURN_TYPE, asset.ReturnType.ATTRIBUTES); // Return only the attributes of the asset, that is, the return result does not include the plaintext of the asset.
query.set(asset.Tag.DATA_LABEL_NORMAL_1, stringToArray('demo_label'));
query.set(asset.Tag.RETURN_OFFSET, 5); // Return results from the fifth asset that matches the search criteria.
query.set(asset.Tag.RETURN_LIMIT, 10); // Return information about 10 assets that match the search criteria.
query.set(asset.Tag.RETURN_ORDERED_BY, asset.Tag.DATA_LABEL_NORMAL_1); // Sort the query results by DATA_LABEL_NORMAL_1.
try {
  asset.query(query).then((res: Array<asset.AssetMap>) => {
    for (let i = 0; i < res.length; i++) {
      // Parse the attributes.
      let accessibility: number = res[i].get(asset.Tag.ACCESSIBILITY) as number;
    }
  }).catch ((err: BusinessError) => {
    console.error(`Failed to query Asset. Code is ${err.code}, message is ${err.message}`);
  });
} catch (error) {
  let err = error as BusinessError;
  console.error(`Failed to query Asset. Code is ${err.code}, message is ${err.message}`);
}
```

## Constraints

* Batch asset query

  The assets queried are transmitted to the service through an IPC channel. Due to the limitation of the IPC buffer size, the maximum number of assets to be queried at a time cannot exceed 40.