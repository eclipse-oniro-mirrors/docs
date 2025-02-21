# @ohos.data.commonType (Common Data Types)

The **commonType** module defines common data types in data management.

> **NOTE**
>
> The initial APIs of this module are supported since API version 11. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```ts
import commonType from '@ohos.data.commonType';
```

## AssetStatus

Enumerates the asset statuses. Use the enum name rather than the enum value.

**System capability**: SystemCapability.DistributedDataManager.CommonType

| Name             | Value | Description                        |
| ----------------- | --- | ---------------------------- |
| ASSET_NORMAL      | 1   | The asset is in normal status.          |
| ASSET_INSERT      | 2   | The asset is to be inserted to the cloud.    |
| ASSET_UPDATE      | 3   | The asset is to be updated to the cloud.    |
| ASSET_DELETE      | 4   | The asset is to be deleted from the cloud.    |
| ASSET_ABNORMAL    | 5   | The asset is in abnormal status.          |
| ASSET_DOWNLOADING | 6   | The asset is being downloaded to a local device.|

## Asset

Defines information about an asset (such as a document, image, and video).

**System capability**: SystemCapability.DistributedDataManager.CommonType

| Name      | Type                       | Mandatory| Description                              |
| ---------- | --------------------------- | ---- | ---------------------------------- |
| name       | string                      | Yes  | Asset name.                      |
| uri        | string                      | Yes  | Asset URI, which is an absolute path in the system.   |
| path       | string                      | Yes  | Application sandbox path of the asset.          |
| createTime | string                      | Yes  | Time when the asset was created.            |
| modifyTime | string                      | Yes  | Time when the asset was last modified.        |
| size       | string                      | Yes  | Size of the asset.              |
| status     | [AssetStatus](#assetstatus) | No  | Asset status. The default value is **ASSET_NORMAL**.|

## Assets

Represents an array of [Assets](#asset).

**System capability**: SystemCapability.DistributedDataManager.CommonType

| Type                        | Description                 |
| ---------------------------- | --------------------- |
| Array&lt;[Asset](#asset)&gt; | Array of assets.|

## ValueType

Enumerates the value types, which vary with the parameter function.

**System capability**: SystemCapability.DistributedDataManager.CommonType

| Type      | Description                                   |
| ---------- | --------------------------------------- |
| null       | The value is null.                       |
| number     | The value is a number.                     |
| string     | The value is a string.                   |
| boolean    | The value is true or false.                   |
| Uint8Array | The value is a Uint8 array.          |
| Asset      | The value is an [Asset](#asset).      |
| Assets     | The value is an [Asset array](#assets).|

## ValuesBucket

Defines the types of the key and value in a KV pair. This type is not multi-thread safe. If a **ValuesBucket** instance is operated by multiple threads at the same time in an application, use a lock for the instance.

**System capability**: SystemCapability.DistributedDataManager.CommonType

| Key Type| Value Type                 |
| ------ | ----------------------- |
| string | [ValueType](#valuetype) |
