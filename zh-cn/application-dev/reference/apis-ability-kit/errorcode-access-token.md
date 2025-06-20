# 访问控制错误码

> **说明：**
>
> 以下仅介绍本模块特有错误码，通用错误码请参考[通用错误码说明文档](../errorcode-universal.md)。

## 12100001 入参错误

**错误信息**

Invalid Parameter. Error message: ${messageInfo}.

**可能原因**

该错误码表示参数校验出现错误，可能原因如下。
1. tokenId值为0。
2. 指定的权限名为空或者权限名长度大于256。
3. 请求授权/撤销权限的flag取值非法。
4. 注册监听的参数检查错误。
5. 指定的Context不属于当前应用。
6. 请求的权限不属于同一个权限组。
7. 请求的权限中存在应用未声明的权限。
8. 请求的全局开关类型非法。

**处理步骤**

检查入参，修正参数值为合法值。

<!--Del-->
## 12100002 tokenId不存在

**错误信息**

TokenId does not exist.

**可能原因**

1. 指定的tokenid不存在。
2. 指定的tokenId对应的进程非应用进程。

**处理步骤**

检查入参，修正参数值为有效值，有效值请参考[权限列表](../../security/AccessToken/app-permissions.md)。
<!--DelEnd-->

<!--Del-->
## 12100003 权限名不存在

**错误信息**

Permission does not exist.

**可能原因**

1. 指定的permissionName不存在。
2. 请求授权/撤销权限场景下，指定的应用tokenid未申请过指定的permissionName。
3. 权限使用记录场景下，指定的permissionName非用户授权的敏感权限。

**处理步骤**

检查入参，修正参数值为有效值，有效值请参考[权限列表](../../security/AccessToken/app-permissions.md)。
<!--DelEnd-->

## 12100004 接口未配套使用

**错误信息**

The API is not used in pair with others.

**可能原因**

该错误码表示监听器接口未配套使用，可能原因如下。
1. 当前接口再未配套使用的情况下，重复调用。
2. 当前接口再未配套使用的情况下，单独调用。

**处理步骤**

1. 检查当前接口是否有配套使用，如调用启动记录的接口后，在未调用停止记录的接口前，不可再次使用相同的入参调用启动记录接口。
2. 检查当前接口是否有配套使用，如停止记录的接口需要在启动记录的接口调用之后方可调用，注销监听接口需要在注册监听接口调用之后方可调用。


## 12100005 监听器数量超过限制

**错误信息**

The number of listeners exceeds the limit.

**可能原因**

该错误码表示当前监听器数量超过限制200个。

**处理步骤**

及时释放已注册的无用的监听器。

<!--Del-->
## 12100006 指定的应用不支持被授予或被取消授予指定的权限

**错误信息**

The specified application does not support the permissions granted or ungranted as specified.

**可能原因**

1. 输入的tokenid是远端设备的身份标识，尚未支持分布式授权和取消授权。
2. 入参指定的tokenid为沙箱应用，被禁止申请指定的权限。

**处理步骤**

1. 请确认tokenid的获取方式是否正确。
2. 确认待授权的沙箱应用是否为特殊的受限沙箱应用进程，部分模式下的沙箱应用被禁止授予大部分权限。
<!--DelEnd-->

## 12100007 系统服务工作异常

**错误信息**

The service is abnormal.

**可能原因**

该错误码表示系统服务工作异常。
1. 权限管理服务无法正常启动。
2. IPC数据读取写入失败。

**处理步骤**

系统服务内部工作异常，请稍后重试，或者重启设备。

<!--Del-->
## 12100008 内存申请失败

**错误信息**

Out of memory.

**可能原因**

系统内存不足。

**处理步骤**

系统内存不足，请稍后重试，或者重启设备。
<!--DelEnd-->

## 12100009 服务内部错误

**错误信息**

Common inner error.

**可能原因**

系统服务内部错误。

**处理步骤**

系统内部逻辑错误，需要结合故障日志进一步分析。

## 12100010 存在未被处理的请求

**错误信息**

The request already exists.

**可能原因**

上一次请求未被处理。

**处理步骤**

请处理完上次请求。


## 12100011 输入的所有权限均已被授权

**错误信息**

All permissions in the permission list have been granted.

**可能原因**

所有权限均已被授权。

**处理步骤**

无需处理，返回此错误码表示申请权限已被授权，不会拉起权限设置弹框。


## 12100012 输入的权限中存在未被用户拒绝过的权限

**错误信息**

The permission list contains the permission that has not been revoked by the user.

**可能原因**

存在未被用户拒绝过的权限。

**处理步骤**

请先调用requestPermissionsFromUser向用户申请权限。


## 12100013 全局开关已开启

**错误信息**

The specific global switch is already open.

**可能原因**

全局开关已开启。

**处理步骤**

无需处理，返回此错误码表示全局开关已开启，不会拉起全局开关设置弹框。
