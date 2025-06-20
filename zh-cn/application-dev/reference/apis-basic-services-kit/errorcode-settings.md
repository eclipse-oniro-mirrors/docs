# 设置数据项错误码

> **说明：**
>
> 以下仅介绍本模块特有错误码，通用错误码请参考[通用错误码说明文档](../errorcode-universal.md)。

## 14800000 参数检查失败

**错误信息**

Parameter error. Possible causes: 1. Parameter verification failed.

**错误描述**

1. 空参数错误。

2. 参数解析错误。

**可能原因**

1. 空参数错误 (Null Argument Error)。

2. 参数值范围错误 (Value Range Error)。

**处理步骤**

请检查必选参数是否传入。如果参数校验失败，请阅读参数规格约束，并根据可能原因进行排查。

## 14800010 上下文参数不是UIAbility类型

**错误信息**

Original service error.

**错误描述**

原始服务错误。

**可能原因**

当前上下文环境非UIAbility界面。

**处理步骤**

切换当前上下文环境，使用UIAbility模型。