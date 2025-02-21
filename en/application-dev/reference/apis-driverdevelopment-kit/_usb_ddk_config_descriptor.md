# UsbDdkConfigDescriptor


## Overview

Defines configuration descriptors.

**Since**

10

**Related Modules**

[UsbDdk](_usb_ddk.md)


## Summary


### Member Variables

| Name| Description|
| -------- | -------- |
| [configDescriptor](#configdescriptor) | Standard configuration descriptor.|
| [interface](#interface) | Interfaces contained in the configuration.|
| [extra](#extra) | Unresolved descriptor, including class- or vendor-specific descriptors.|
| [extraLength](#extralength) | Length of the unresolved descriptor.|


## Member Variable Description


### configDescriptor


```
struct UsbConfigDescriptor UsbDdkConfigDescriptor::configDescriptor
```

**Description**

Standard configuration descriptor.


### extra


```
const uint8_t* UsbDdkConfigDescriptor::extra
```

**Description**

Unresolved descriptor, including class- or vendor-specific descriptors.


### extraLength


```
uint32_t UsbDdkConfigDescriptor::extraLength
```

**Description**

Length of the unresolved descriptor.


### interface


```
struct UsbDdkInterface* UsbDdkConfigDescriptor::interface
```

**Description**

Interfaces contained in the configuration.
