# ModuleInfo

The **ModuleInfo** module provides module information of an application.

> **NOTE**
>
> The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## ModuleInfo<sup>(deprecated)<sup>
> This API is deprecated since API version 9. You are advised to use [bundleManager-HapModuleInfo](js-apis-bundleManager-hapModuleInfo.md) instead.

**System capability**: SystemCapability.BundleManager.BundleFramework

| Name           | Type  | Readable| Writable| Description    |
| --------------- | ------ | ---- | ---- | -------- |
| moduleName      | string | Yes  | No  | Module name.|
| moduleSourceDir | string | Yes  | No  | Installation directory. A resource file cannot be accessed by combining paths. Use [Resource Manager](js-apis-resource-manager.md) to access it. |
