# HdfPinAuth


## **概述**

提供口令认证驱动的标准API接口。

口令认证驱动为口令认证服务提供统一的访问接口。获取口令认证驱动代理后，口令认证服务可以调用相关接口获取执行器，获取口令认证执行器后， 口令认证服务可以调用相关接口获取执行器信息，获取凭据模版信息，注册口令，认证口令，删除口令等。

**Since：**

3.2


## **汇总**


### 文件

  | 名称 | 描述 | 
| -------- | -------- |
| [IExecutor.idl](pin__auth_2_i_executor_8idl.md) | 定义执行器标准API接口。接口可用于获取执行器信息，获取凭据模版信息，注册口令，认证口令，删除口令等。 | 
| [IExecutorCallback.idl](pin__auth_2_i_executor_callback_8idl.md) | 定义异步API接口回调，用于返回异步接口的请求处理结果和获取信息。 | 
| [IPinAuthInterface.idl](_i_pin_auth_interface_8idl.md) | 定义获取口令认证驱动的执行器列表接口，用于从口令认证驱动获取执行器对象列表。 | 
| [PinAuthTypes.idl](_pin_auth_types_8idl.md) | 定义口令认证驱动的枚举类和数据结构。 | 


### 类

  | 名称 | 描述 | 
| -------- | -------- |
| [IExecutor](interface_pin_i_executor.md) | 定义执行器标准API接口。接口可用于获取执行器信息，获取凭据模版信息，注册口令，认证口令，删除口令等。 | 
| [IExecutorCallback](interface_pin_i_executor_callback.md) | 定义异步API接口回调，用于返回异步接口的请求处理结果和信息。使用细节见[IExecutor](interface_pin_i_executor.md)。 | 
| [IPinAuthInterface](interface_i_pin_auth_interface.md) | 定义获取口令认证驱动的执行器列表接口。 | 
| [ExecutorInfo](_executor_info.md) | 执行器信息。 | 
| [TemplateInfo](_template_info.md) | 凭据模版信息。 | 


### 枚举

  | 名称 | 描述 | 
| -------- | -------- |
| [AuthType](#authtype):&nbsp;int&nbsp;{&nbsp;&nbsp;&nbsp;PIN&nbsp;=&nbsp;1,&nbsp;FACE&nbsp;=&nbsp;2,&nbsp;FINGERPRINT&nbsp;=&nbsp;4&nbsp;} | 枚举用户认证凭据类型。 | 
| [ExecutorRole](#executorrole):&nbsp;int&nbsp;{&nbsp;&nbsp;&nbsp;COLLECTOR&nbsp;=&nbsp;1,&nbsp;VERIFIER&nbsp;=&nbsp;2,&nbsp;ALL_IN_ONE&nbsp;=&nbsp;3&nbsp;} | 枚举执行器角色。 | 
| [ExecutorSecureLevel](#executorsecurelevel):&nbsp;int&nbsp;{&nbsp;&nbsp;&nbsp;ESL0&nbsp;=&nbsp;0,&nbsp;ESL1&nbsp;=&nbsp;1,&nbsp;ESL2&nbsp;=&nbsp;2,&nbsp;ESL3&nbsp;=&nbsp;3&nbsp;} | 枚举执行器安全等级。 | 
| [CommandId](#commandid):&nbsp;int&nbsp;{&nbsp;DEFAULT&nbsp;=&nbsp;0&nbsp;} | 枚举口令认证相关功能操作命令。 | 


### 关键字

  | 名称 | 描述 | 
| -------- | -------- |
| package&nbsp;ohos.hdi.pin_auth.v1_0 | 口令认证接口的包路径 | 


## **枚举类型说明**


### AuthType

  
```
enum AuthType : int
```

**描述：**

枚举用户认证凭据类型。

  | 枚举值 | 描述 | 
| -------- | -------- |
| PIN | 认证凭据类型为口令。 | 
| FACE | 认证凭据类型为人脸。 | 
| FINGERPRINT | 认证凭据类型为指纹。 | 


### CommandId

  
```
enum CommandId : int
```

**描述：**

枚举口令认证相关功能操作命令。

  | 枚举值 | 描述 | 
| -------- | -------- |
| DEFAULT | 默认无效操作命令。 | 


### ExecutorRole

  
```
enum ExecutorRole : int
```

**描述：**

枚举执行器角色。

  | 枚举值 | 描述 | 
| -------- | -------- |
| COLLECTOR | 执行器角色为采集器，提供用户认证时的数据采集能力，需要和认证器配合完成用户认证。 | 
| VERIFIER | 执行器角色为认证器，提供用户认证时数据处理能力，读取存储凭据模板信息并完成比对。 | 
| ALL_IN_ONE | 执行器角色为全功能执行器，可提供用户认证数据采集、处理、储存及比对能力。 | 


### ExecutorSecureLevel

  
```
enum ExecutorSecureLevel : int
```

**描述：**

枚举执行器安全等级。

  | 枚举值 | 描述 | 
| -------- | -------- |
| ESL0 | 执行器安全级别为0，关键操作在无访问控制执行环境中完成。 | 
| ESL1 | 执行器安全级别为1，关键操作在有访问控制的执行环境中完成。 | 
| ESL2 | 执行器安全级别为2，关键操作在可信执行环境中完成。 | 
| ESL3 | 执行器安全级别为3，关键操作在高安环境如独立安全芯片中完成。 | 
