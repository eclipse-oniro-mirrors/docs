# USB DDK开发指导

## 场景介绍

USB DDK（USB Driver Develop Kit）是为开发者提供的USB驱动程序开发套件，支持开发者基于用户态，在应用层开发USB设备驱动。提供了一系列主机侧访问设备的接口，包括主机侧打开和关闭接口、管道同步异步读写通信、控制传输、中断传输等。

## 约束与限制

* USB DDK开放API支持USB接口非标外设扩展驱动开发场景。

* USB DDK开放API使用范围内仅允许DriverExtensionAbilit生命周期内使用。

* 使用USB DDK开放API需要在module.json5中声明匹配的ACL权限，例如ohos.permission.ACCESS_DDK_USB。

## 接口说明

| 名称 | 描述 |
| -------- | -------- |
| OH_Usb_Init(void) | 初始化DDK。 |
| OH_Usb_Release(void) | 释放DDK。 |
| OH_Usb_GetDeviceDescriptor(uint64_t deviceId, struct UsbDeviceDescriptor *desc) | 获取设备描述符。 |
| OH_Usb_GetConfigDescriptor(uint64_t deviceId, uint8_t configIndex, struct UsbDdkConfigDescriptor **const config) | 获取配置描述符。请在描述符使用完后使用OH_Usb_FreeConfigDescriptor()释放描述符，否则会造成内存泄露。 |
| OH_Usb_FreeConfigDescriptor(const struct UsbDdkConfigDescriptor *const config) | 释放配置描述符，请在描述符使用完后释放描述符，否则会造成内存泄露。 |
| OH_Usb_ClaimInterface(uint64_t deviceId, uint8_t interfaceIndex, uint64_t *interfaceHandle) | 声明接口。 |
| OH_Usb_SelectInterfaceSetting(uint64_t interfaceHandle, uint8_t settingIndex) | 激活接口的备用设置。 |
| OH_Usb_GetCurrentInterfaceSetting(uint64_t interfaceHandle, uint8_t \*settingIndex) | 获取接口当前激活的备用设置。 |
| OH_Usb_SendControlReadRequest(uint64_t interfaceHandle, const struct UsbControlRequestSetup \*setup, uint32_t timeout, uint8_t \*data, uint32_t \*dataLen) | 发送控制读请求，该接口为同步接口。 |
| OH_Usb_SendControlWriteRequest(uint64_t interfaceHandle, const struct UsbControlRequestSetup \*setup, uint32_t, const uint8_t \*data, uint32_t dataLen) | 发送控制写请求，该接口为同步接口。 |
| OH_Usb_ReleaseInterface(uint64_t interfaceHandle) | 释放接口。 |
| OH_Usb_SendPipeRequest(const struct UsbRequestPipe *pipe, UsbDeviceMemMap *devMmap) | 发送管道请求，该接口为同步接口。中断传输和批量传输都使用该接口发送请求。 |
| OH_Usb_CreateDeviceMemMap(uint64_t deviceId, size_t size, UsbDeviceMemMap **devMmap) | 创建缓冲区。请在缓冲区使用完后，调用OH_Usb_DestroyDeviceMemMap()销毁缓冲区，否则会造成资源泄露。 |
| OH_Usb_DestroyDeviceMemMap(UsbDeviceMemMap *devMmap) | 销毁缓冲区。请在缓冲区使用完后及时销毁缓冲区，否则会造成资源泄露。 |

详细的接口说明请参考[USB DDK](../reference/apis-driverdevelopment-kit/_usb_ddk.md)。

## 开发步骤

以下步骤描述了如何使用 **USB DDK**开发USB驱动：

**添加动态链接库**

CMakeLists.txt中添加以下lib。
```txt
libusb_ndk.z.so
```

**头文件**
```c++
#include <usb/usb_ddk_api.h>
#include <usb/usb_ddk_types.h>
```

1. 获取设备描述符。

    使用 **usb_ddk_api.h** 的 **OH_Usb_Init** 接口初始化DDK，并使用 **OH_Usb_GetDeviceDescriptor**获取到设备描述符。

    ```c++
    // 初始化USB DDK
    OH_Usb_Init();
    struct UsbDeviceDescriptor devDesc;
    uint64_t deviceId = 0;
    // 获取设备描述符
    OH_Usb_GetDeviceDescriptor(deviceId, &devDesc);
    ```

2. 获取配置描述符及声明接口。
    
    使用 **usb_ddk_api.h** 的 **OH_Usb_GetConfigDescriptor** 接口获取配置描述符 **config**，并使用 OH_Usb_ClaimInterface 声明"认领"接口。

    ```c++
    struct UsbDdkConfigDescriptor *config = nullptr;
    // 获取配置描述符
    OH_Usb_GetConfigDescriptor(deviceId, 1, &config);
    // 根据配置描述符,找到所需要通信的interfaceIndex
    uint8_t interfaceIndex = 0;
    // 声明接口
    uint64_t interfaceHandle = 0;
    OH_Usb_ClaimInterface(deviceId, interfaceIndex, &interfaceHandle);
    // 释放配置描述符
    OH_Usb_FreeConfigDescriptor(config);
    ```
3. 获取当前激活接口的备用设置及激活备用设置。

    使用 **usb_ddk_api.h** 的 **OH_Usb_GetCurrentInterfaceSetting** 获取备用设置，并使用 **OH_Usb_SelectInterfaceSetting** 激活备用设置。

    ```c++
    uint8_t settingIndex = 0;
    // 接口获取备用设置
    OH_Usb_GetCurrentInterfaceSetting(interfaceHandle, &settingIndex);

    // 激活备用设置
    OH_Usb_SelectInterfaceSetting(interfaceHandle, &settingIndex);
    ```
4. 发送控制读请求、发送控制写请求。

    使用 **usb_ddk_api.h** 的**OH_Usb_SendControlReadRequest**发送控制读请求，或者使用**OH_Usb_SendControlWriteRequest**发送控制写请求。

    ```c++
        // 超时时间，设置为1s;
    uint32_t timeout = 1000;

    struct UsbControlRequestSetup setupRead;
    setupRead.bmRequestType	= 0x80;
    setupRead.bRequest = 0x08;
    setupRead.wValue = 0;
    setupRead.wIndex = 0;
    setupRead.wLength = 0x01;
    uint8_t dataRead[256] = {0};
    uint32_t dataReadLen = 256;
    // 发送控制读请求
    OH_Usb_SendControlReadRequest(interfaceHandle, &setupRead, timeout, dataRead, &dataReadLen);

    struct UsbControlRequestSetup setupWrite;
    setupWrite.bmRequestType = 0;
    setupWrite.bRequest = 0x09;
    setupWrite.wValue = 1;
    setupWrite.wIndex = 0;
    setupWrite.wLength = 0;
    uint8_t dataWrite[256] = {0};
    uint32_t dataWriteLen = 256;
    // 发送控制写请求
    OH_Usb_SendControlWriteRequest(interfaceHandle, &setupWrite, timeout, dataWrite, &dataWriteLen);
    ```

5. 创建内存映射缓冲区及发送请求。

    使用 **usb_ddk_api.h** 的**OH_Usb_CreateDeviceMemMap**接口创建内存映射缓冲区**devMmap**，并使用**OH_Usb_SendPipeRequest**发送请求。

    ```c++
    struct UsbDeviceMemMap *devMmap = nullptr;
    // 创建用于存放数据的缓冲区
    size_t bufferLen = 10;
    OH_Usb_CreateDeviceMemMap(deviceId, bufferLen, &devMmap);
    struct UsbRequestPipe pipe;
    pipe.interfaceHandle = interfaceHandle;
    // 根据配置描述符找到所要通信的端点
    pipe.endpoint = 128;
    pipe.timeout = UINT32_MAX;
    // 发送请求
    OH_Usb_SendPipeRequest(&pipe, devMmap);
    ```

6. 释放资源。

    在所有请求处理完毕，程序退出前，使用 **usb_ddk_api.h** 的 **OH_Usb_DestroyDeviceMemMap** 接口销毁缓冲区。使用**OH_Usb_ReleaseInterface**释放接口。使用**OH_Usb_Release**释放USB DDK。

    ```c++
    // 销毁缓冲区
    OH_Usb_DestroyDeviceMemMap(devMmap);
    // 释放接口
    OH_Usb_ReleaseInterface(interfaceHandle);
    // 释放USB DDK
    OH_Usb_Release();
    ```
