# IAllInOneExecutor


## 概述

定义全功能执行器标准API接口。接口可用于获取执行器信息，获取凭据模版信息，注册口令，认证口令，删除口令等。

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
| [SetData](#setdata) ([in] unsigned long scheduleId, [in] unsigned long authSubType, [in] unsigned char[] data, [in] int resultCode) | 设置口令数据，口令认证驱动处理注册或认证口令请求时，如果口令数据由口令认证服务获取，需要通过该接口将口令数据传给口令认证驱动。 | 
| [Enroll](#enroll) ([in] unsigned long scheduleId, [in] unsigned char[] extraInfo, [in] [IExecutorCallback](interface_i_executor_callback_v20.md) callbackObj) | 注册口令。 | 
| [Authenticate](#authenticate) ([in] unsigned long scheduleId, [in] unsigned long[] templateIdList, [in] unsigned char[] extraInfo, [in] [IExecutorCallback](interface_i_executor_callback_v20.md) callbackObj) | 认证口令。 | 
| [Delete](#delete) ([in] unsigned long templateId) | 删除口令。 | 
| [GetProperty](#getproperty) ([in] unsigned long[] templateIdList, [in] int[] propertyTypes, [out] struct [Property](_property_v20.md) property) | 获取属性。 | 


## 成员函数说明


### Authenticate()

```
IAllInOneExecutor::Authenticate ([in] unsigned long scheduleId, [in] unsigned long[] templateIdList, [in] unsigned char[] extraInfo, [in] IExecutorCallback callbackObj )
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
IAllInOneExecutor::Cancel ([in] unsigned long scheduleId)
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


### Delete()

```
IAllInOneExecutor::Delete ([in] unsigned long templateId)
```

**描述**

删除口令。

**起始版本：** 5.0

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| templateId | 模版ID。 | 

**返回：**

0 表示操作成功。

非0 表示操作失败。


### Enroll()

```
IAllInOneExecutor::Enroll ([in] unsigned long scheduleId, [in] unsigned char[] extraInfo, [in] IExecutorCallback callbackObj )
```

**描述**

注册口令。

**起始版本：** 5.0

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| scheduleId | 调度ID，用于标识一次操作请求的调度过程。 | 
| extraInfo | 其他相关信息，用于支持信息扩展。 | 
| callbackObj | 回调对象[IExecutorCallback](interface_i_executor_callback_v20.md)。 | 

**返回：**

0 表示操作成功。

非0 表示操作失败。


### GetExecutorInfo()

```
IAllInOneExecutor::GetExecutorInfo ([out] struct ExecutorInfo executorInfo)
```

**描述**

获取执行器信息。

**起始版本：** 5.0

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| executorInfo | 标识执行器信息[ExecutorInfo](_executor_info_v20.md)。 | 

**返回：**

0 表示操作成功。

非0 表示操作失败。


### GetProperty()

```
IAllInOneExecutor::GetProperty ([in] unsigned long[] templateIdList, [in] int[] propertyTypes, [out] struct Property property )
```

**描述**

获取属性。

**起始版本：** 5.0

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| templateIdList | 标识需要处理的模板。 | 
| propertyTypes | 标识需要获取的属性类型[GetPropertyType](_hdf_pin_auth_v20.md#getpropertytype)。 | 
| property | 标识获取的属性[Property](_property_v20.md)。 | 

**返回：**

0 表示操作成功。

非0 表示操作失败。


### OnRegisterFinish()

```
IAllInOneExecutor::OnRegisterFinish ([in] unsigned long[] templateIdList, [in] unsigned char[] frameworkPublicKey, [in] unsigned char[] extraInfo )
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
IAllInOneExecutor::SendMessage ([in] unsigned long scheduleId, [in] int srcRole, [in] unsigned char[] msg )
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


### SetData()

```
IAllInOneExecutor::SetData ([in] unsigned long scheduleId, [in] unsigned long authSubType, [in] unsigned char[] data, [in] int resultCode )
```

**描述**

设置口令数据，口令认证驱动处理注册或认证口令请求时，如果口令数据由口令认证服务获取，需要通过该接口将口令数据传给口令认证驱动。

**起始版本：** 5.0

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| scheduleId | 调度ID，用于标识一次操作请求的调度过程。 | 
| authSubType | 口令子类型，如六位数字PIN码等[PinAuthTypes](_pin_auth_types_8idl_v20.md)。 | 
| data | 口令数据。 | 
| resultCode | 返回结果状态码。 | 

**返回：**

0 表示操作成功。

非0 表示操作失败。
