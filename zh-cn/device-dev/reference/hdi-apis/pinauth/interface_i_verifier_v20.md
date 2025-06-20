# IVerifier


## 概述

定义认证器标准API接口。接口可用于获取执行器信息，取消认证，口令认证，发送消息等。

**起始版本：** 5.0

**相关模块：**[HdfPinAuth](_hdf_pin_auth_v20.md)


## 汇总


### Public 成员函数

| 名称 | 描述 | 
| -------- | -------- |
| [GetExecutorInfo](#getexecutorinfo) ([out] struct [ExecutorInfo](_executor_info_v20.md) executorInfo) | 获取执行器信息。 | 
| [OnRegisterFinish](#onregisterfinish) ([in] unsigned long[] templateIdList, [in] unsigned char[] frameworkPublicKey, [in] unsigned char[] extraInfo) | 完成执行器注册，对口令模版信息进行对账，用于删除无效的口令模板及相关信息。 | 
| [Cancel](#cancel) ([in] unsigned long scheduleId) | 取消操作请求。 | 
| [SendMessage](#sendmessage) ([in] unsigned long scheduleId, [in] int srcRole, [in] unsigned char[] msg) | 发送消息。 | 
| [Authenticate](#authenticate) ([in] unsigned long scheduleId, [in] unsigned long[] templateIdList, [in] unsigned char[] extraInfo, [in] [IExecutorCallback](interface_i_executor_callback_v20.md) callbackObj) | 认证口令。 | 
| [NotifyCollectorReady](#notifycollectorready) ([in] unsigned long scheduleId) | 通知收集器准备就绪。 | 


## 成员函数说明


### Authenticate()

```
IVerifier::Authenticate ([in] unsigned long scheduleId, [in] unsigned long[] templateIdList, [in] unsigned char[] extraInfo, [in] IExecutorCallback callbackObj )
```

**描述**

认证口令。

**起始版本：** 5.0

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| scheduleId | 调度ID，用于标识一次操作请求的调度过程。 | 
| templateIdList | 指定要认证的模版ID列表。 | 
| extraInfo | 其他相关信息，用于支持信息扩展。 | 
| callbackObj | 回调对象[IExecutorCallback](interface_i_executor_callback_v20.md)。 | 

**返回：**

0 表示操作成功。

非0 表示操作失败。


### Cancel()

```
IVerifier::Cancel ([in] unsigned long scheduleId)
```

**描述**

取消操作请求。

**起始版本：** 5.0

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| scheduleId | 调度ID，用于标识一次操作请求的调度过程。 | 

**返回：**

0 表示操作成功。

非0 表示操作失败。


### GetExecutorInfo()

```
IVerifier::GetExecutorInfo ([out] struct ExecutorInfo executorInfo)
```

**描述**

获取执行器信息。

**起始版本：** 5.0

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| executorInfo | 执行器信息[ExecutorInfo](_executor_info_v20.md)。 | 

**返回：**

0 表示操作成功。

非0 表示操作失败。


### NotifyCollectorReady()

```
IVerifier::NotifyCollectorReady ([in] unsigned long scheduleId)
```

**描述**

通知收集器准备就绪。

**起始版本：** 5.0

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| scheduleId | 调度ID，用于标识一次操作请求的调度过程。 | 

**返回：**

0 表示操作成功。

非0 表示操作失败。


### OnRegisterFinish()

```
IVerifier::OnRegisterFinish ([in] unsigned long[] templateIdList, [in] unsigned char[] frameworkPublicKey, [in] unsigned char[] extraInfo )
```

**描述**

完成执行器注册，对口令模版信息进行对账，用于删除无效的口令模板及相关信息。

**起始版本：** 5.0

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| templateIdList | 用户认证框架内由该执行器注册的口令凭据模版ID列表。 | 
| frameworkPublicKey | 用户认证框架的公钥，用于校验用户认证框架私钥签名的信息。 | 
| extraInfo | 其他相关信息，用于支持信息扩展。 | 

**返回：**

0 表示操作成功。

非0 表示操作失败。


### SendMessage()

```
IVerifier::SendMessage ([in] unsigned long scheduleId, [in] int srcRole, [in] unsigned char[] msg )
```

**描述**

发送消息。

**起始版本：** 5.0

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| scheduleId | 标识消息的调度ID。 | 
| srcRole | 源执行器角色[ExecutorRole](_hdf_pin_auth_v20.md#executorrole)。 | 
| msg | 消息。 | 

**返回：**

0 表示操作成功。

非0 表示操作失败。
