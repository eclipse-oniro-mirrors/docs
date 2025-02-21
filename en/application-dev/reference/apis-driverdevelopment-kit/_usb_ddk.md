# USB DDK


## Overview

Provides USB DDK APIs to open and close USB interfaces, perform non-isochronous and isochronous data transfer over USB pipes, and implement control transfer and interrupt transfer, etc.

**System capability**: SystemCapability.Driver.USB.Extension

**Since**

10

## Summary


### File

| Name| Description|
| -------- | -------- |
| [usb_ddk_api.h](usb__ddk__api_8h.md) | Declares the USB DDK APIs used by the USB host to access USB devices.<br>File to include: &lt;usb/usb_ddk_api.h&gt;<br>Library: libusb_ndk.z.so|
| [usb_ddk_types.h](usb__ddk__types_8h.md) | Provides the enumerated variables, structures, and macros used in USB DDK APIs.<br>File to include: &lt;usb/usb_ddk_types.h&gt; <br>Library: libusb_ndk.z.so|


### Structs

| Name| Description|
| -------- | -------- |
| [UsbControlRequestSetup](_usb_control_request_setup.md) | Setup data for control transfer. It corresponds to **Setup Data** in the USB protocol.|
| [UsbDeviceDescriptor](_usb_device_descriptor.md) | Standard device descriptor, corresponding to **Standard Device Descriptor** in the USB protocol.|
| [UsbConfigDescriptor](_usb_config_descriptor.md) | Standard configuration descriptor, corresponding to **Standard Configuration Descriptor** in the USB protocol.|
| [UsbInterfaceDescriptor](_usb_interface_descriptor.md) | Standard interface descriptor, corresponding to **Standard Interface Descriptor** in the USB protocol.|
| [UsbEndpointDescriptor](_usb_endpoint_descriptor.md) | Standard endpoint descriptor, corresponding to **Standard Endpoint Descriptor** in the USB protocol.|
| [UsbDdkEndpointDescriptor](_usb_ddk_endpoint_descriptor.md) | Endpoint descriptor.|
| [UsbDdkInterfaceDescriptor](_usb_ddk_interface_descriptor.md) | Interface descriptor.|
| [UsbDdkInterface](_usb_ddk_interface.md) | USB DDK interface, which is a collection of alternate settings for a particular USB interface.|
| [UsbDdkConfigDescriptor](_usb_ddk_config_descriptor.md) | Configuration descriptor.|
| [UsbRequestPipe](_usb_request_pipe.md) | Request pipe.|
| [UsbDeviceMemMap](_usb_device_mem_map.md) | Device memory map created by calling [OH_Usb_CreateDeviceMemMap()](#oh_usb_createdevicememmap). A buffer using the device memory map can provide better performance.|

### Enums

| Name| Description|
| -------- | -------- |
| [UsbDdkErrCode](#usbddkerrcode) {<br>USB_DDK_SUCCESS = 0, USB_DDK_FAILED = -1, USB_DDK_INVALID_PARAMETER = -2, USB_DDK_MEMORY_ERROR = -3,<br>USB_DDK_INVALID_OPERATION = -4, USB_DDK_NULL_PTR = -5, USB_DDK_DEVICE_BUSY = -6, USB_DDK_TIMEOUT = -7<br>} | USB DDK error code definitions.|


### Functions

| Name| Description|
| -------- | -------- |
| [OH_Usb_Init](#oh_usb_init) (void) | Initializes the DDK.|
| [OH_Usb_Release](#oh_usb_release) (void) | Releases the DDK.|
| [OH_Usb_GetDeviceDescriptor](#oh_usb_getdevicedescriptor) (uint64_t deviceId, struct [UsbDeviceDescriptor](_usb_device_descriptor.md) \*desc) | Obtains the device descriptor.|
| [OH_Usb_GetConfigDescriptor](#oh_usb_getconfigdescriptor) (uint64_t deviceId, uint8_t configIndex, struct [UsbDdkConfigDescriptor](_usb_ddk_config_descriptor.md) \*\*const config) | Obtains the configuration descriptor. To avoid memory leakage, use **OH_Usb_FreeConfigDescriptor** to release a descriptor after use.|
| [OH_Usb_FreeConfigDescriptor](#oh_usb_freeconfigdescriptor) (const struct [UsbDdkConfigDescriptor](_usb_ddk_config_descriptor.md) \*const config) | Releases the configuration descriptor. To avoid memory leakage, release a descriptor after use.|
| [OH_Usb_ClaimInterface](#oh_usb_claiminterface) (uint64_t deviceId, uint8_t interfaceIndex, uint64_t \*[interfaceHandle](usb__ddk__types_8h.md#interfacehandle)) | Declares a USB interface.|
| [OH_Usb_ReleaseInterface](#oh_usb_releaseinterface) (uint64_t [interfaceHandle](usb__ddk__types_8h.md#interfacehandle)) | Releases a USB interface.|
| [OH_Usb_SelectInterfaceSetting](#oh_usb_selectinterfacesetting) (uint64_t [interfaceHandle](usb__ddk__types_8h.md#interfacehandle), uint8_t settingIndex) | Activates the alternate setting of a USB interface.|
| [OH_Usb_GetCurrentInterfaceSetting](#oh_usb_getcurrentinterfacesetting) (uint64_t [interfaceHandle](usb__ddk__types_8h.md#interfacehandle), uint8_t \*settingIndex) | Obtains the activated alternate setting of a USB interface.|
| [OH_Usb_SendControlReadRequest](#oh_usb_sendcontrolreadrequest) (uint64_t [interfaceHandle](usb__ddk__types_8h.md#interfacehandle), const struct [UsbControlRequestSetup](_usb_control_request_setup.md) \*setup, uint32_t [timeout](usb__ddk__types_8h.md#timeout), uint8_t \*data, uint32_t \*dataLen) | Sends a control read transfer request. This API works in a synchronous manner.|
| [OH_Usb_SendControlWriteRequest](#oh_usb_sendcontrolwriterequest) (uint64_t [interfaceHandle](usb__ddk__types_8h.md#interfacehandle), const struct [UsbControlRequestSetup](_usb_control_request_setup.md) \*setup, uint32_t [timeout](usb__ddk__types_8h.md#timeout), const uint8_t \*data, uint32_t dataLen) | Sends a control write transfer request. This API works in a synchronous manner.|
| [OH_Usb_SendPipeRequest](#oh_usb_sendpiperequest) (const struct [UsbRequestPipe](_usb_request_pipe.md) \*pipe, [UsbDeviceMemMap](_usb_device_mem_map.md) \*devMmap) | Sends a pipe request. This API works in a synchronous manner. It applies to interrupt transfer and bulk transfer.|
| [OH_Usb_CreateDeviceMemMap](#oh_usb_createdevicememmap) (uint64_t deviceId, size_t size, [UsbDeviceMemMap](_usb_device_mem_map.md) \*\*devMmap) | Creates a buffer. To avoid memory leakage, use [OH_Usb_DestroyDeviceMemMap()](#oh_usb_destroydevicememmap) to destroy a buffer after use.|
| [OH_Usb_DestroyDeviceMemMap](#oh_usb_destroydevicememmap) ([UsbDeviceMemMap](_usb_device_mem_map.md) \*devMmap) | Destroys a buffer. To avoid resource leakage, destroy a buffer in time after use.|

#### Description of deviceId

You can call **queryDevices()** to obtain the device ID, that is, **deviceId**.
For details, see [Peripheral Management Development](../../device/driver/externaldevice-guidelines.md).

## Enum Description


### UsbDdkErrCode


```
enum UsbDdkErrCode
```

**Description**

USB DDK error code definitions.

| Value| Description|
| -------- | -------- |
| USB_DDK_SUCCESS | Operation successful.|
| USB_DDK_FAILED | Operation failed.|
| USB_DDK_INVALID_PARAMETER | Invalid parameter.|
| USB_DDK_MEMORY_ERROR | Memory-related error, for example, insufficient memory, memory data copy failure, or memory application failure.|
| USB_DDK_INVALID_OPERATION | Invalid operation.|
| USB_DDK_NULL_PTR | Null pointer.|
| USB_DDK_DEVICE_BUSY | Device busy.|
| USB_DDK_TIMEOUT | Transfer timed out.|


## Function Description


### OH_Usb_ClaimInterface()


```
int32_t OH_Usb_ClaimInterface (uint64_t deviceId, uint8_t interfaceIndex, uint64_t * interfaceHandle )
```

**Description**

Declares a USB interface.

**Required permissions**: ohos.permission.ACCESS_DDK_USB

**Parameters**

| Name| Description|
| -------- | -------- |
| deviceId | Device ID.|
| interfaceIndex | Interface index, which corresponds to [bInterfaceNumber](_usb_interface_descriptor.md#binterfacenumber) in the USB protocol.|
| interfaceHandle | Interface operation handle. After the interface is claimed successfully, a value will be assigned to this parameter.|

**Returns**

**0** if the operation is successful; a negative value otherwise.


### OH_Usb_CreateDeviceMemMap()


```
int32_t OH_Usb_CreateDeviceMemMap (uint64_t deviceId, size_t size, UsbDeviceMemMap ** devMmap )
```

**Description**

Creates a buffer. To avoid memory leakage, use [OH_Usb_DestroyDeviceMemMap()](#oh_usb_destroydevicememmap) to destroy a buffer after use.

**Required permissions**: ohos.permission.ACCESS_DDK_USB

**Parameters**

| Name| Description|
| -------- | -------- |
| deviceId | Device ID.|
| size | Buffer size.|
| devMmap | Data memory map, through which the created buffer is returned to the caller.|

**Returns**

**0** if the operation is successful; a negative value otherwise.


### OH_Usb_DestroyDeviceMemMap()


```
void OH_Usb_DestroyDeviceMemMap (UsbDeviceMemMap * devMmap)
```

**Description**

Destroys a buffer. To avoid resource leakage, destroy a buffer in time after use.

**Required permissions**: ohos.permission.ACCESS_DDK_USB

**Parameters**

| Name| Description|
| -------- | -------- |
| devMmap | Destroys the buffer created by [OH_Usb_CreateDeviceMemMap()](#oh_usb_createdevicememmap).|


### OH_Usb_FreeConfigDescriptor()


```
void OH_Usb_FreeConfigDescriptor (struct UsbDdkConfigDescriptor *const config)
```

**Description**

Releases the configuration descriptor. To avoid memory leakage, use **OH_Usb_FreeConfigDescriptor** to release a descriptor after use.

**Required permissions**: ohos.permission.ACCESS_DDK_USB

**Parameters**

| Name| Description|
| -------- | -------- |
| config | Configuration descriptor obtained by calling [OH_Usb_GetConfigDescriptor()](#oh_usb_getconfigdescriptor).|


### OH_Usb_GetConfigDescriptor()


```
int32_t OH_Usb_GetConfigDescriptor (uint64_t deviceId, uint8_t configIndex, struct UsbDdkConfigDescriptor **const config )
```

**Description**

Obtains the configuration descriptor. To avoid memory leakage, use **OH_Usb_FreeConfigDescriptor** to release a descriptor after use.

**Required permissions**: ohos.permission.ACCESS_DDK_USB

**Parameters**

| Name| Description|
| -------- | -------- |
| deviceId | Device ID.|
| configIndex | Configuration ID, which corresponds to [bConfigurationValue](_usb_config_descriptor.md#bconfigurationvalue) in the USB protocol.|
| config | Configuration descriptor, which includes the standard configuration descriptor defined in the USB protocol and the associated interface descriptor and endpoint descriptor.|

**Returns**

**0** if the operation is successful; a negative value otherwise.


### OH_Usb_GetCurrentInterfaceSetting()


```
int32_t OH_Usb_GetCurrentInterfaceSetting (uint64_t interfaceHandle, uint8_t * settingIndex )
```

**Description**

Obtains the activated alternate setting of a USB interface.

**Required permissions**: ohos.permission.ACCESS_DDK_USB

**Parameters**

| Name| Description|
| -------- | -------- |
| interfaceHandle | Interface operation handle.|
| settingIndex | Index of the alternate setting, which corresponds to [bAlternateSetting](_usb_interface_descriptor.md#balternatesetting) in the USB protocol.|

**Returns**

**0** if the operation is successful; a negative value otherwise.


### OH_Usb_GetDeviceDescriptor()


```
int32_t OH_Usb_GetDeviceDescriptor (uint64_t deviceId, struct UsbDeviceDescriptor * desc )
```

**Description**

Obtains the device descriptor.

**Required permissions**: ohos.permission.ACCESS_DDK_USB

**Parameters**

| Name| Description|
| -------- | -------- |
| deviceId | Device ID.|
| desc | Device descriptor. For details, see [UsbDeviceDescriptor](_usb_device_descriptor.md).|

**Returns**

**0** if the operation is successful; a negative value otherwise.


### OH_Usb_Init()


```
int32_t OH_Usb_Init (void )
```

**Description**

Initializes the DDK.

**Required permissions**: ohos.permission.ACCESS_DDK_USB

**Returns**

**0** if the operation is successful; a negative value otherwise.


### OH_Usb_Release()


```
void OH_Usb_Release (void )
```

**Description**

Releases the DDK.

**Required permissions**: ohos.permission.ACCESS_DDK_USB


### OH_Usb_ReleaseInterface()


```
int32_t OH_Usb_ReleaseInterface (uint64_t interfaceHandle)
```

**Description**

Releases a USB interface.

**Required permissions**: ohos.permission.ACCESS_DDK_USB

**Parameters**

| Name| Description|
| -------- | -------- |
| interfaceHandle | Interface operation handle.|

**Returns**

**0** if the operation is successful; a negative value otherwise.


### OH_Usb_SelectInterfaceSetting()


```
int32_t OH_Usb_SelectInterfaceSetting (uint64_t interfaceHandle, uint8_t settingIndex )
```

**Description**

Activates the alternate setting of a USB interface.

**Required permissions**: ohos.permission.ACCESS_DDK_USB

**Parameters**

| Name| Description|
| -------- | -------- |
| interfaceHandle | Interface operation handle.|
| settingIndex | Index of the alternate setting, which corresponds to [bAlternateSetting](_usb_interface_descriptor.md#balternatesetting) in the USB protocol.|

**Returns**

**0** if the operation is successful; a negative value otherwise.


### OH_Usb_SendControlReadRequest()


```
int32_t OH_Usb_SendControlReadRequest (uint64_t interfaceHandle, const struct UsbControlRequestSetup * setup, uint32_t timeout, uint8_t * data, uint32_t * dataLen )
```

**Description**

Sends a control read transfer request. This API works in a synchronous manner.

**Required permissions**: ohos.permission.ACCESS_DDK_USB

**Parameters**

| Name| Description|
| -------- | -------- |
| interfaceHandle | Interface operation handle.|
| setup | Request parameters. For details, see [UsbControlRequestSetup](_usb_control_request_setup.md).|
| timeout | Timeout duration, in milliseconds.|
| data | Data to be transferred.|
| dataLen | Data length. The return value indicates the length of the actually read data.|

**Returns**

**0** if the operation is successful; a negative value otherwise.


### OH_Usb_SendControlWriteRequest()


```
int32_t OH_Usb_SendControlWriteRequest (uint64_t interfaceHandle, const struct UsbControlRequestSetup * setup, uint32_t timeout, const uint8_t * data, uint32_t dataLen )
```

**Description**

Sends a control write transfer request. This API works in a synchronous manner.

**Required permissions**: ohos.permission.ACCESS_DDK_USB

**Parameters**

| Name| Description|
| -------- | -------- |
| interfaceHandle | Interface operation handle.|
| setup | Request parameters. For details, see [UsbControlRequestSetup](_usb_control_request_setup.md).|
| timeout | Timeout duration, in milliseconds.|
| data | Data to be transferred.|
| dataLen | Data length.|

**Returns**

**0** if the operation is successful; a negative value otherwise.


### OH_Usb_SendPipeRequest()


```
int32_t OH_Usb_SendPipeRequest (const struct UsbRequestPipe * pipe, UsbDeviceMemMap * devMmap )
```

**Description**

Sends a pipe request. This API works in a synchronous manner. It applies to interrupt transfer and bulk transfer.

**Required permissions**: ohos.permission.ACCESS_DDK_USB

**Parameters**

| Name| Description|
| -------- | -------- |
| pipe | Pipe used to transfer data.|
| devMmap | Device memory map, which can be obtained by calling [OH_Usb_CreateDeviceMemMap()](#oh_usb_createdevicememmap).|

**Returns**

**0** if the operation is successful; a negative value otherwise.

 