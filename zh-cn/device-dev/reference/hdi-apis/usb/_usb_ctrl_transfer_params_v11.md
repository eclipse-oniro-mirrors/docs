# UsbCtrlTransferParams


## 概述

USB设备控制传输信息。

**起始版本：** 5.0

**相关模块：**[HdiUsb](_hdi_usb.md)


## 汇总


### Public 属性

| 名称 | 描述 | 
| -------- | -------- |
| int [requestType](#requesttype) | 请求类型。 | 
| int [requestCmd](#requestcmd) | 请求命令。 | 
| int [value](#value) | 请求值。 | 
| int [index](#index) | 索引值。 | 
| int [length](#length) | 数据长度。 | 
| int [timeout](#timeout) | 超时时间。 | 


## 类成员变量说明


### index

```
int UsbCtrlTransferParams::index
```

**描述**

索引值。


### length

```
int UsbCtrlTransferParams::length
```

**描述**

数据长度。


### requestCmd

```
int UsbCtrlTransferParams::requestCmd
```

**描述**

请求命令。


### requestType

```
int UsbCtrlTransferParams::requestType
```

**描述**

请求类型。


### timeout

```
int UsbCtrlTransferParams::timeout
```

**描述**

超时时间。


### value

```
int UsbCtrlTransferParams::value
```

**描述**

请求值。
