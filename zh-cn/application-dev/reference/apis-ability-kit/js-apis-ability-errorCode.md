# @ohos.ability.errorCode (ErrorCode)

ErrorCode定义启动Ability时返回的错误码，包括无效的参数、权限拒绝等。

> **说明：**
> 
> 本模块首批接口从API version 6开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import errorCode from '@ohos.ability.errorCode';
```

## ErrorCode

定义启动Ability时返回的错误码。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

| 名称                             | 值    | 说明                                       |
| ------------------------------ | ---- | ---------------------------------------- |
| NO_ERROR         | 0    | 没有异常。   |
| INVALID_PARAMETER | -1   | 无效的参数。 |
| ABILITY_NOT_FOUND | -2   | 找不到ABILITY。 |
| PERMISSION_DENY   | -3   | 权限拒绝。   |