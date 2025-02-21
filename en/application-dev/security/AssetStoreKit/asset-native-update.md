# Update an Asset (C/C++)

## Available APIs

For details about the API, see:

[int32_t OH_Asset_Update(const Asset_Attr *query, uint32_t queryCnt, const Asset_Attr *attributesToUpdate, uint32_t updateCnt)](../../reference/apis-asset-store-kit/_asset_api.md#oh_asset_update)

Attributes in **query**:

| Attribute Name (Asset_Tag)           | Attribute Content (Asset_Value)                                      | Mandatory| Description                                            |
| ------------------------------- | ------------------------------------------------------------ | -------- | ------------------------------------------------ |
| ASSET_TAG_ALIAS                 | Type: uint8[]<br>Length: 1-256 bytes                              | Yes    | Asset alias, which uniquely identifies an asset.           |
| ASSET_TAG_ACCESSIBILITY         | Type: uint32_t<br>Value range: see [Asset_Accessibility](../../reference/apis-asset-store-kit/_asset_type.md#asset_accessibility)| No    | Access control based on the lock screen status.                                    |
| ASSET_TAG_REQUIRE_PASSWORD_SET  | Type: bool                                                  | No    | Whether the asset is accessible only when a lock screen password is set.    |
| ASSET_TAG_AUTH_TYPE             | Type: uint32_t<br>Value range: see [Asset_AuthType](../../reference/apis-asset-store-kit/_asset_type.md#asset_authtype)| No    | Type of user authentication required for accessing the asset.                  |
| ASSET_TAG_SYNC_TYPE             | Type: uint32_t<br>Value range: see [Asset_SyncType](../../reference/apis-asset-store-kit/_asset_type.md#asset_synctype)| No    | Type of sync supported by the asset.                          |
| ASSET_TAG_IS_PERSISTENT         | Type: bool                                                  | No    | Whether to retain the asset when the application is uninstalled.                |
| ASSET_TAG_DATA_LABEL_CRITICAL_1 | Type: uint8[]<br>Length: 1-512 bytes                              | No    | Additional asset data customized by the service with integrity protection.|
| ASSET_TAG_DATA_LABEL_CRITICAL_2 | Type: uint8[]<br>Length: 1-512 bytes                              | No    | Additional asset data customized by the service with integrity protection.|
| ASSET_TAG_DATA_LABEL_CRITICAL_3 | Type: uint8[]<br>Length: 1-512 bytes                              | No    | Additional asset data customized by the service with integrity protection.|
| ASSET_TAG_DATA_LABEL_CRITICAL_4 | Type: uint8[]<br>Length: 1-512 bytes                              | No    | Additional asset data customized by the service with integrity protection.|
| ASSET_TAG_DATA_LABEL_NORMAL_1   | Type: uint8[]<br>Length: 1-512 bytes                              | No    | Additional asset data customized by the service without integrity protection.|
| ASSET_TAG_DATA_LABEL_NORMAL_2   | Type: uint8[]<br>Length: 1-512 bytes                              | No    | Additional asset data customized by the service without integrity protection.|
| ASSET_TAG_DATA_LABEL_NORMAL_3   | Type: uint8[]<br>Length: 1-512 bytes                              | No    | Additional asset data customized by the service without integrity protection.|
| ASSET_TAG_DATA_LABEL_NORMAL_4   | Type: uint8[]<br>Length: 1-512 bytes                              | No    | Additional asset data customized by the service without integrity protection.|


Attributes in **attributesToUpdate**:


| Attribute Name (Asset_Tag)| Attribute Content (Asset_Value)         | Mandatory| Description                                            |
| ------------------- | ------------------------------- | -------- | ------------------------------------------------ |
| SECRET              | Type: uint8[]<br>Length: 1-1024 bytes| No    | New asset plaintext.                                    |
| DATA_LABEL_NORMAL_1 | Type: uint8[]<br>Length: 1-512 bytes | No    | Additional data of the new asset customized by the service without integrity protection.|
| DATA_LABEL_NORMAL_2 | Type: uint8[]<br>Length: 1-512 bytes | No    | Additional data of the new asset customized by the service without integrity protection.|
| DATA_LABEL_NORMAL_3 | Type: uint8[]<br>Length: 1-512 bytes | No    | Additional data of the new asset customized by the service without integrity protection.|
| DATA_LABEL_NORMAL_4 | Type: uint8[]<br>Length: 1-512 bytes | No    | Additional data of the new asset customized by the service without integrity protection.|

## Example

Update asset **demo_alias** as follows: change the asset plaintext to **demo_pwd_new** and additional attribute to **demo_label_new**.

1. Add the dynamic library in the CMake script.
   ```txt
   target_link_libraries(entry PUBLIC libasset_ndk.z.so)
   ```

2. Add an asset.
   ```c
   #include <string.h>

   #include "asset/asset_api.h"

   void UpdateAsset() {
      static const char *ALIAS = "demo_alias";
      static const char *SECRET = "demo_pwd_new";
      static const char *LABEL = "demo_label_new";

      Asset_Blob alias = { (uint32_t)(strlen(ALIAS)), (uint8_t *)ALIAS };
      Asset_Blob new_secret = { (uint32_t)(strlen(SECRET)), (uint8_t *)SECRET };
      Asset_Blob new_label = { (uint32_t)(strlen(LABEL)), (uint8_t *)LABEL };
      Asset_Attr query[] = { { .tag = ASSET_TAG_ALIAS, .value.blob = alias } };
      Asset_Attr attributesToUpdate[] = {
         { .tag = ASSET_TAG_SECRET, .value.blob = new_secret },
         { .tag = ASSET_TAG_DATA_LABEL_NORMAL_1, .value.blob = new_label },
      };

      int32_t ret = OH_Asset_Update(query, sizeof(query) / sizeof(query[0]), attributesToUpdate,
                                    sizeof(attributesToUpdate) / sizeof(attributesToUpdate[0]));
      if (ret == ASSET_SUCCESS) {
         // Asset updated successfully.
      } else {
         // Failed to update Asset.
      }
   }
   ```

## Constraints

N/A.
