# usb_ddk_api.h


## Overview

Declares the USB DDK APIs used by the USB host to access USB devices.

**Since**

10

**Related Modules**

[UsbDdk](_usb_ddk.md)


## Summary


### Functions

| Name| Description|
| -------- | -------- |
| [OH_Usb_Init](_usb_ddk.md#oh_usb_init)&nbsp;(void) | Initializes the DDK.|
| [OH_Usb_Release](_usb_ddk.md#oh_usb_release)&nbsp;(void) | Releases the DDK.|
| [OH_Usb_GetDeviceDescriptor](_usb_ddk.md#oh_usb_getdevicedescriptor)&nbsp;(uint64_t&nbsp;deviceId,&nbsp;struct&nbsp;[UsbDeviceDescriptor](_usb_device_descriptor.md)&nbsp;\*desc) | Obtains the device descriptor.|
| [OH_Usb_GetConfigDescriptor](_usb_ddk.md#oh_usb_getconfigdescriptor)&nbsp;(uint64_t&nbsp;deviceId,&nbsp;uint8_t&nbsp;configIndex,&nbsp;struct&nbsp;[UsbDdkConfigDescriptor](_usb_ddk_config_descriptor.md)&nbsp;\*\*const&nbsp;config) | Obtains the configuration descriptor. To avoid memory leakage, use [OH_Usb_FreeConfigDescriptor()](_usb_ddk.md#oh_usb_freeconfigdescriptor) to release a descriptor after use.|
| [OH_Usb_FreeConfigDescriptor](_usb_ddk.md#oh_usb_freeconfigdescriptor)&nbsp;(const&nbsp;struct&nbsp;[UsbDdkConfigDescriptor](_usb_ddk_config_descriptor.md)&nbsp;\*const&nbsp;config) | Releases the configuration descriptor. To avoid memory leakage, release a descriptor after use.|
| [OH_Usb_ClaimInterface](_usb_ddk.md#oh_usb_claiminterface)&nbsp;(uint64_t&nbsp;deviceId,&nbsp;uint8_t&nbsp;interfaceIndex,&nbsp;uint64_t&nbsp;\*[interfaceHandle](usb__ddk__types_8h.md#interfacehandle)) | Declares a USB interface.|
| [OH_Usb_ReleaseInterface](_usb_ddk.md#oh_usb_releaseinterface)&nbsp;(uint64_t&nbsp;[interfaceHandle](usb__ddk__types_8h.md#interfacehandle)) | Releases a USB interface.|
| [OH_Usb_SelectInterfaceSetting](_usb_ddk.md#oh_usb_selectinterfacesetting)&nbsp;(uint64_t&nbsp;[interfaceHandle](usb__ddk__types_8h.md#interfacehandle),&nbsp;uint8_t&nbsp;settingIndex) | Activates the alternate setting of a USB interface.|
| [OH_Usb_GetCurrentInterfaceSetting](_usb_ddk.md#oh_usb_getcurrentinterfacesetting)&nbsp;(uint64_t&nbsp;[interfaceHandle](usb__ddk__types_8h.md#interfacehandle),&nbsp;uint8_t&nbsp;\*settingIndex) | Obtains the activated alternate setting of a USB interface.|
| [OH_Usb_SendControlReadRequest](_usb_ddk.md#oh_usb_sendcontrolreadrequest)&nbsp;(uint64_t&nbsp;[interfaceHandle](usb__ddk__types_8h.md#interfacehandle),&nbsp;const&nbsp;struct&nbsp;[UsbControlRequestSetup](_usb_control_request_setup.md)&nbsp;\*setup,&nbsp;uint32_t&nbsp;[timeout](usb__ddk__types_8h.md#timeout),&nbsp;uint8_t&nbsp;\*data,&nbsp;uint32_t&nbsp;\*dataLen) | Sends a control read transfer request. This API works in a synchronous manner.|
| [OH_Usb_SendControlWriteRequest](_usb_ddk.md#oh_usb_sendcontrolwriterequest)&nbsp;(uint64_t&nbsp;[interfaceHandle](usb__ddk__types_8h.md#interfacehandle),&nbsp;const&nbsp;struct&nbsp;[UsbControlRequestSetup](_usb_control_request_setup.md)&nbsp;\*setup,&nbsp;uint32_t&nbsp;[timeout](usb__ddk__types_8h.md#timeout),&nbsp;const&nbsp;uint8_t&nbsp;\*data,&nbsp;uint32_t&nbsp;dataLen) | Sends a control write transfer request. This API works in a synchronous manner.|
| [OH_Usb_SendPipeRequest](_usb_ddk.md#oh_usb_sendpiperequest)&nbsp;(const&nbsp;struct&nbsp;[UsbRequestPipe](_usb_request_pipe.md)&nbsp;\*pipe,&nbsp;[UsbDeviceMemMap](_usb_device_mem_map.md)&nbsp;\*devMmap) | Sends a pipe request. This API works in a synchronous manner. It applies to interrupt transfer and bulk transfer.|
| [OH_Usb_CreateDeviceMemMap](_usb_ddk.md#oh_usb_createdevicememmap)&nbsp;(uint64_t&nbsp;deviceId,&nbsp;size_t&nbsp;size,&nbsp;[UsbDeviceMemMap](_usb_device_mem_map.md)&nbsp;\*\*devMmap) | Creates a buffer. To avoid memory leakage, use [OH_Usb_DestroyDeviceMemMap()](_usb_ddk.md#oh_usb_destroydevicememmap) to destroy a buffer after use.|
| [OH_Usb_DestroyDeviceMemMap](_usb_ddk.md#oh_usb_destroydevicememmap)&nbsp;([UsbDeviceMemMap](_usb_device_mem_map.md)&nbsp;\*devMmap) | Destroys a buffer. To avoid resource leakage, destroy a buffer in time after use.|
