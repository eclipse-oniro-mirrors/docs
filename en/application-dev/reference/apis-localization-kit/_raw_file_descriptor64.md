# RawFileDescriptor64

## Overview

Defines the file descriptor of a large rawfile. **RawFileDescriptor** is an output parameter of [OH_ResourceManager_GetRawFileDescriptor64](rawfile.md#oh_resourcemanager_getrawfiledescriptor64). It contains the file descriptor of a raw file and the start position and length of the raw file in the HAP.

**Since**: 11

**Related module**: [Rawfile] (rawfile.md)

## Summary

### Member Variables

| Name| Description| 
| -------- | -------- |
| [fd](#fd) | File descriptor of the rawfile, in int.| 
| [start](#start) | Start position of the rawfile in the HAP, in int64_t.| 
| [length](#length) | Length of the rawfile in the HAP, in int64_t.| 

## Member Variable Description

### fd

```
int RawFileDescriptor64::fd
```

**Description**

File descriptor of the rawfile, in int.

### length

```
int64_t RawFileDescriptor64::length
```

**Description**

Length of the rawfile in the HAP, in int64_t.

### start

```
int64_t RawFileDescriptor64::start
```

**Description**

Start position of the rawfile in the HAP, in int64_t.
