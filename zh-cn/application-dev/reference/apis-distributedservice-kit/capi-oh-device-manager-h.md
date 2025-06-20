# oh_device_manager.h

## 概述

提供访问可信设备和本地设备信息的接口。

**引用文件：** <distributedhardware/device_manager/oh_device_manager.h>

**库：** libdevicemanager_ndk.so

**系统能力：** SystemCapability.DistributedHardware.DeviceManager

**起始版本：** 20

**相关模块：** [DeviceManager](capi-devicemanager.md)

## 汇总

### 函数

| 名称 | 描述 |
| -- | -- |
| [int32_t OH_DeviceManager_GetLocalDeviceName(char **localDeviceName, unsigned int &len)](#oh_devicemanager_getlocaldevicename) | 获取本地设备显示名。<br>设备显示名称涉及用户的隐私数据，需要应用提供相关隐私声明，声明设备显示名的用途。 |

## 函数说明

### OH_DeviceManager_GetLocalDeviceName()

```
int32_t OH_DeviceManager_GetLocalDeviceName(char **localDeviceName, unsigned int &len)
```

**描述**

获取本地设备显示名。<br>设备显示名称涉及用户的隐私数据，需要应用提供相关隐私声明，声明设备显示名的用途。

**需要权限：** ohos.permission.READ_LOCAL_DEVICE_NAME

**起始版本：** 20


**参数：**

| 参数项 | 描述 |
| -- | -- |
| char **localDeviceName | 表示本地设备显示名字符串的地址指针。使用后需要手动释放空间资源。应用具备  ohos.permission.READ_LOCAL_DEVICE_NAME 权限，返回设备显示名称；否则返回设备默认名称。 |
| unsigned int &len | 表示本地设备显示名字符串的长度。 |

**返回：**

| 类型 | 说明                                                                                                                                                                                                                                                                                                                                                                           |
| -- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| int32_t | 返回执行的错误码。错误码定义详见[DeviceManager_ErrorCode](capi-oh-device-manager-err-code-h.md#devicemanager_errorcode)。<br>         返回[ERR_OK](capi-oh-device-manager-err-code-h.md#devicemanager_errorcode)，表示执行成功。<br>         返回[DM_ERR_FAILED](capi-oh-device-manager-err-code-h.md#devicemanager_errorcode)，表示函数执行失败。<br>         返回[DM_ERR_OBTAIN_SERVICE](capi-oh-device-manager-err-code-h.md#devicemanager_errorcode)，表示获取设备管理服务失败。<br>         返回[DM_ERR_OBTAIN_BUNDLE_NAME](capi-oh-device-manager-err-code-h.md#devicemanager_errorcode)，表示获取bundleName失败。 |


