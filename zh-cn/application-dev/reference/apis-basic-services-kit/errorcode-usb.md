# USB服务错误码

> **说明：**
>
> 以下仅介绍本模块特有错误码，通用错误码请参考[通用错误码说明文档](../errorcode-universal.md)。

## 14400001 连接USB设备被拒绝

**错误信息**

Access right denied. Call requestRight to get the USBDevicePipe access right first.

**错误描述**

当调用USB模块部分接口时，如果没有相关权限，会报此错误码。

**可能原因**

没有获取到设备的使用权限。

**处理步骤**

调用requestRight方法申请设备的使用权限。
<!--Del-->
## 14400002 HDC功能被禁用

**错误信息**

Permission denied. The HDC is disabled by the system.

**错误描述**

HDC被系统禁用。

**可能原因**

没有申请USB调试权限。

**处理步骤**

申请USB调试权限。

## 14400003 不支持的端口角色切换

**错误信息**

Unsupported operation. The current device does not support port role switching.

**错误描述**

不支持的操作。当前设备不支持端口角色切换。

**可能原因**

不是正确的端口角色。

**处理步骤**

使用正确的端口角色。
<!--DelEnd-->
## 14400004 服务异常

**错误信息**

Service exception. Possible causes: No accessory is plugged in.

**错误描述**

服务异常。

**可能原因：**

没有配件插入。

**处理步骤**

插入配件。

## 14400005 数据库操作异常

**错误信息**

Database operation exception.

**错误描述**

数据库操作异常。

**处理步骤**

尝试重新调用接口。
<!--Del-->
## 14400006 不支持的USB设备侧功能

**错误信息**

Unsupported operation. The function is not supported.

**错误描述**

不支持的操作。当前设备不支持该USB设备侧功能切换。

**可能原因**

不是正确的USB设备侧功能。

**处理步骤**

使用正确的USB设备侧功能。
<!--DelEnd-->
## 14401001 目标USB配件未匹配

**错误信息**

The target USBAccessory not matched.

**错误描述**

目标USB配件未匹配。

**处理步骤**

通过getAccessoryList获得配件列表，使用匹配的USBAccessory重新操作。

## 14401002 打开配件节点失败

**错误信息**

Failed to open the native accessory node.

**错误描述**

打开配件节点失败。

**处理步骤**

尝试重新调用接口。

## 14401003 不能重复打开配件

**错误信息**

Cannot reopen the accessory.

**错误描述**

不能重复打开配件。

**处理步骤**

配件已被打开，继续执行后续开发操作。

## 14400007 资源繁忙

**错误信息**

Resource busy. Possible causes: 1. The transfer has already been submitted. 2. The interface is claimed by another program or driver.

**错误描述**

资源被占用。

**可能原因**

1. 传输任务已提交。

2. 该接口已被另一个程序或驱动程序占用。

**处理步骤**

检查[usbManager.claimInterface](js-apis-usbManager.md#usbmanagerclaiminterface)接口是否调用成功。

## 14400008 没有设备(连接已断开)

**错误信息**

No such device (it may have been disconnected).

**错误描述**

未识别到正确设备信息。

**处理步骤**

检查设备类型是否正确，检查设备是否已成功连接。

## 14400009 内存不足

**错误信息**

Insufficient memory. Possible causes: 1. Memory allocation failed.

**错误描述**

内存申请时无内存可用，单次传输，数据大小最大为1KB。

**可能原因**

内存占用率过高，没有足够的空间分配给当前任务。

**处理步骤**

及时清理内存。

## 14400010 无法识别的错误

**错误信息**

Other USB error. Possible causes:Unrecognized discard error code.

**错误描述**

系统无法识别的错误。

**处理步骤**

查阅设备相关资料，尝试重新操作。

## 14400011 未找到正在进行的传输

**错误信息**

The transfer is not in progress, or is already complete or cancelled.

**错误描述**

此次传输已被取消或已经传输完成。

**处理步骤**

重新发起新的传输请求。

## 14400012 I/O错误

**错误信息**

Transmission I/O error.

**错误描述**

I/O通道异常，实际读/写操作失败。

**处理步骤**

尝试重新操作。
