# @ohos.app.ability.wantConstant (wantConstant) (System API)

The **wantConstant** module provides the actions, entities, and flags used in **Want** objects.

> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
> This topic describes only system APIs provided by the module. For details about its public APIs, see [@ohos.app.ability.wantConstant (wantConstant)](js-apis-app-ability-wantConstant.md).

## Modules to Import

```ts
import wantConstant from '@ohos.app.ability.wantConstant';
```

## wantConstant.Params

Defines **Params** (specifying the action that can be performed) in the Want.

**System capability**: SystemCapability.Ability.AbilityBase

| Name                   | Value                                | Description                                                                          |
| ----------------------- | ---------------------------------- | ------------------------------------------------------------------------------ |
| DLP_PARAMS_SANDBOX      | ohos.dlp.params.sandbox            | Action of obtaining the sandbox flag.<br>**System API**: This is a system API and cannot be called by third-party applications.|
| DLP_PARAMS_BUNDLE_NAME  | ohos.dlp.params.bundleName         | Action of obtaining the DLP bundle name.<br>**System API**: This is a system API and cannot be called by third-party applications.|
| DLP_PARAMS_MODULE_NAME  | ohos.dlp.params.moduleName         | Action of obtaining the DLP module name.<br>**System API**: This is a system API and cannot be called by third-party applications.|
| DLP_PARAMS_ABILITY_NAME | ohos.dlp.params.abilityName        | Action of obtaining the DLP ability name.<br>**System API**: This is a system API and cannot be called by third-party applications.|
| DLP_PARAMS_INDEX        | ohos.dlp.params.index              | Action of obtaining the DLP index.<br>**System API**: This is a system API and cannot be called by third-party applications.|


## wantConstant.Flags

 Enumerates the flags that specify how the Want will be handled.

**System capability**: SystemCapability.Ability.AbilityBase

| Name                                | Value      | Description                                                        |
| ------------------------------------ | ---------- | ------------------------------------------------------------ |
| FLAG_AUTH_PERSISTABLE_URI_PERMISSION<sup>10+</sup> | 0x00000040 | Indicates the permanent permission of the URI. This flag is valid only for 2-in-1 applications.<br>**System API**: This is a system API and cannot be called by third-party applications.<br>If this flag is used together with **FLAG_AUTH_READ_URI_PERMISSION**, the permanent read permission is granted.<br>If this flag is used together with **FLAG_AUTH_WRITE_URI_PERMISSION**, the permanent write permission is granted.<br>The flag takes effect only when the **PERMISSION_PROXY_AUTHORIZATION_URI** permission is configured for the application.|
