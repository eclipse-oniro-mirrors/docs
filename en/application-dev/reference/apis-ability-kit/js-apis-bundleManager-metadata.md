# Metadata

The **Metadata** module defines a metadata object. An application can obtain the metadata through [bundleManager.getBundleInfoForSelf](js-apis-bundleManager.md#bundlemanagergetbundleinfoforself), with **GET_BUNDLE_INFO_WITH_METADATA** passed in for [bundleFlags](js-apis-bundleManager.md#bundleflag). This object is contained in [ApplicationInfo](js-apis-bundleManager-applicationInfo.md), [HapModuleInfo](js-apis-bundleManager-hapModuleInfo.md), [AbilityInfo](js-apis-bundleManager-abilityInfo.md), and [ExtensionAbilityInfo](js-apis-bundleManager-extensionAbilityInfo.md).

The **Metadata** module provides the configuration about the module, UIAbility, and ExtensionAbility. The value is of the array type. The configuration is valid only for the current module, UIAbility, or ExtensionAbility.

> **NOTE**
> 
The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Metadata

**System capability**: SystemCapability.BundleManager.BundleFramework.Core
| Name    | Type  | Readable| Writable| Description      |
| -------- | ------ | ---- | ---- | ---------- |
| name     | string | Yes  | Yes  | Metadata name.|
| value    | string | Yes  | Yes  | Metadata value.  |
| resource | string | Yes  | Yes  | Metadata resource.|
