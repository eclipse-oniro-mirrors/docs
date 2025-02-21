# Removing Assets (C/C++)

## Available APIs

For details about the APIs, see:

[int32_t OH_Asset_Remove(const Asset_Attr *query, uint32_t queryCnt)](../../reference/apis-asset-store-kit/_asset_api.md#oh_asset_remove)

The following table describes the parameters.

| Attribute Name (Asset_Tag)           | Attribute Content (Asset_Value)                                      | Mandatory| Description                                            |
| ------------------------------- | ------------------------------------------------------------ | -------- | ------------------------------------------------ |
| ASSET_TAG_ALIAS                 | Type: uint8[]<br>Length: 1-256 bytes                              | No    | Asset alias, which uniquely identifies an asset.           |
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

## Example

Remove asset **demo_alias**.

1. Add the dynamic library in the CMake script.
   ```txt
   target_link_libraries(entry PUBLIC libasset_ndk.z.so)
   ```

2. Add an asset.
   ```c
   #include <string.h>

   #include "asset/asset_api.h"

   void RemoveAsset() {
      static const char *ALIAS = "demo_alias";
      Asset_Blob alias = { (uint32_t)(strlen(ALIAS)), (uint8_t *)ALIAS };

      Asset_Attr attr[] = {
         {.tag = ASSET_TAG_ALIAS, .value.blob = alias}, // Specify the alias of the asset to remove. If no alias is specified, all assets will be removed.
      };

      int32_t ret = OH_Asset_Remove(attr, sizeof(attr) / sizeof(attr[0]));
      if (ret == ASSET_SUCCESS) {
         // Asset removed successfully.
      } else {
         // Failed to remove Asset.
      }
   }
   ```

## Constraints

N/A.
