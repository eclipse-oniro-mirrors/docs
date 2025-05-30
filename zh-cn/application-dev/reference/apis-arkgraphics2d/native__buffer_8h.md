# native_buffer.h


## 概述

定义获取和使用NativeBuffer的相关函数。

**引用文件：**&lt;native_buffer/native_buffer.h&gt;

**库：** libnative_buffer.so

**系统能力：** SystemCapability.Graphic.Graphic2D.NativeBuffer

**起始版本：** 9

**相关模块：**[OH_NativeBuffer](_o_h___native_buffer.md)


## 汇总


### 结构体

| 名称 | 描述 |
| -------- | -------- |
| struct  [OH_NativeBuffer_Config](_o_h___native_buffer___config.md) | OH_NativeBuffer的属性配置，用于申请新的OH_NativeBuffer实例或查询现有实例的相关属性。  |
| struct  [OH_NativeBuffer_Plane](_o_h___native_buffer___plane.md) | 单个图像平面格式信息。  |
| struct  [OH_NativeBuffer_Planes](_o_h___native_buffer___planes.md) | OH_NativeBuffer的图像平面格式信息。  |


### 类型定义

| 名称 | 描述 |
| -------- | -------- |
| typedef struct [OH_NativeBuffer](_o_h___native_buffer.md#oh_nativebuffer)  [OH_NativeBuffer](_o_h___native_buffer.md#oh_nativebuffer) | 提供OH_NativeBuffer结构体声明。  |
| typedef enum [OH_NativeBuffer_Usage](_o_h___native_buffer.md#oh_nativebuffer_usage)  [OH_NativeBuffer_Usage](_o_h___native_buffer.md#oh_nativebuffer_usage) | OH_NativeBuffer的用途。  |
| typedef enum [OH_NativeBuffer_Format](_o_h___native_buffer.md#oh_nativebuffer_format)  [OH_NativeBuffer_Format](_o_h___native_buffer.md#oh_nativebuffer_format) | OH_NativeBuffer的格式。  |
| typedef enum [OH_NativeBuffer_TransformType](_o_h___native_buffer.md#oh_nativebuffer_transformtype)  [OH_NativeBuffer_TransformType](_o_h___native_buffer.md#oh_nativebuffer_transformtype) | OH_NativeBuffer的转换类型。  |
| typedef enum [OH_NativeBuffer_ColorGamut](_o_h___native_buffer.md#oh_nativebuffer_colorgamut)  [OH_NativeBuffer_ColorGamut](_o_h___native_buffer.md#oh_nativebuffer_colorgamut) | OH_NativeBuffer的色域。  |
| typedef enum [OHNativeErrorCode](_o_h___native_buffer.md#ohnativeerrorcode)  [OHNativeErrorCode](_o_h___native_buffer.md#ohnativeerrorcode) | 接口错误码说明（仅用于查询）。  |
| typedef struct [OH_NativeBuffer_Config](_o_h___native_buffer___config.md)  [OH_NativeBuffer_Config](_o_h___native_buffer.md#oh_nativebuffer_config) | OH_NativeBuffer的属性配置，用于申请新的OH_NativeBuffer实例或查询现有实例的相关属性。  |
| typedef struct [OH_NativeBuffer_Plane](_o_h___native_buffer___plane.md)  [OH_NativeBuffer_Plane](_o_h___native_buffer.md#oh_nativebuffer_plane) | 单个图像平面格式信息。  |
| typedef struct [OH_NativeBuffer_Planes](_o_h___native_buffer___planes.md)  [OH_NativeBuffer_Planes](_o_h___native_buffer.md#oh_nativebuffer_planes) | OH_NativeBuffer的图像平面格式信息。  |


### 枚举

| 名称 | 描述 |
| -------- | -------- |
| [OH_NativeBuffer_Usage](_o_h___native_buffer.md#oh_nativebuffer_usage-1) {<br/>NATIVEBUFFER_USAGE_CPU_READ = (1ULL &lt;&lt; 0), NATIVEBUFFER_USAGE_CPU_WRITE = (1ULL &lt;&lt; 1), NATIVEBUFFER_USAGE_MEM_DMA = (1ULL &lt;&lt; 3), NATIVEBUFFER_USAGE_HW_RENDER = (1ULL &lt;&lt; 8),<br/>NATIVEBUFFER_USAGE_HW_TEXTURE = (1ULL &lt;&lt; 9), NATIVEBUFFER_USAGE_CPU_READ_OFTEN = (1ULL &lt;&lt; 16), NATIVEBUFFER_USAGE_ALIGNMENT_512 = (1ULL &lt;&lt; 18)<br/>} | OH_NativeBuffer的用途。  |
| [OH_NativeBuffer_Format](_o_h___native_buffer.md#oh_nativebuffer_format-1) {<br/>NATIVEBUFFER_PIXEL_FMT_CLUT8 = 0, NATIVEBUFFER_PIXEL_FMT_CLUT1, NATIVEBUFFER_PIXEL_FMT_CLUT4, NATIVEBUFFER_PIXEL_FMT_RGB_565 = 3,<br/>NATIVEBUFFER_PIXEL_FMT_RGBA_5658, NATIVEBUFFER_PIXEL_FMT_RGBX_4444, NATIVEBUFFER_PIXEL_FMT_RGBA_4444, NATIVEBUFFER_PIXEL_FMT_RGB_444,<br/>NATIVEBUFFER_PIXEL_FMT_RGBX_5551, NATIVEBUFFER_PIXEL_FMT_RGBA_5551, NATIVEBUFFER_PIXEL_FMT_RGB_555, NATIVEBUFFER_PIXEL_FMT_RGBX_8888,<br/>NATIVEBUFFER_PIXEL_FMT_RGBA_8888, NATIVEBUFFER_PIXEL_FMT_RGB_888, NATIVEBUFFER_PIXEL_FMT_BGR_565, NATIVEBUFFER_PIXEL_FMT_BGRX_4444,<br/>NATIVEBUFFER_PIXEL_FMT_BGRA_4444, NATIVEBUFFER_PIXEL_FMT_BGRX_5551, NATIVEBUFFER_PIXEL_FMT_BGRA_5551, NATIVEBUFFER_PIXEL_FMT_BGRX_8888,<br/>NATIVEBUFFER_PIXEL_FMT_BGRA_8888, NATIVEBUFFER_PIXEL_FMT_YUV_422_I, NATIVEBUFFER_PIXEL_FMT_YCBCR_422_SP, NATIVEBUFFER_PIXEL_FMT_YCRCB_422_SP,<br/>NATIVEBUFFER_PIXEL_FMT_YCBCR_420_SP, NATIVEBUFFER_PIXEL_FMT_YCRCB_420_SP, NATIVEBUFFER_PIXEL_FMT_YCBCR_422_P, NATIVEBUFFER_PIXEL_FMT_YCRCB_422_P,<br/>NATIVEBUFFER_PIXEL_FMT_YCBCR_420_P, NATIVEBUFFER_PIXEL_FMT_YCRCB_420_P, NATIVEBUFFER_PIXEL_FMT_YUYV_422_PKG, NATIVEBUFFER_PIXEL_FMT_UYVY_422_PKG,<br/>NATIVEBUFFER_PIXEL_FMT_YVYU_422_PKG, NATIVEBUFFER_PIXEL_FMT_VYUY_422_PKG, NATIVEBUFFER_PIXEL_FMT_RGBA_1010102, NATIVEBUFFER_PIXEL_FMT_YCBCR_P010,<br/>NATIVEBUFFER_PIXEL_FMT_YCRCB_P010, NATIVEBUFFER_PIXEL_FMT_RAW10, NATIVEBUFFER_PIXEL_FMT_BLOB, NATIVEBUFFER_PIXEL_FMT_RGBA16_FLOAT,<br/>NATIVEBUFFER_PIXEL_FMT_VENDER_MASK = 0X7FFF0000, NATIVEBUFFER_PIXEL_FMT_BUTT = 0X7FFFFFFF<br/>} | OH_NativeBuffer的格式。  |
| [OH_NativeBuffer_TransformType](_o_h___native_buffer.md#oh_nativebuffer_transformtype-1) {<br/>NATIVEBUFFER_ROTATE_NONE = 0, NATIVEBUFFER_ROTATE_90, NATIVEBUFFER_ROTATE_180, NATIVEBUFFER_ROTATE_270,<br/>NATIVEBUFFER_FLIP_H, NATIVEBUFFER_FLIP_V, NATIVEBUFFER_FLIP_H_ROT90, NATIVEBUFFER_FLIP_V_ROT90,<br/>NATIVEBUFFER_FLIP_H_ROT180, NATIVEBUFFER_FLIP_V_ROT180, NATIVEBUFFER_FLIP_H_ROT270, NATIVEBUFFER_FLIP_V_ROT270<br/>} | OH_NativeBuffer的转换类型。  |
| [OH_NativeBuffer_ColorGamut](_o_h___native_buffer.md#oh_nativebuffer_colorgamut-1) {<br/>NATIVEBUFFER_COLOR_GAMUT_NATIVE = 0, NATIVEBUFFER_COLOR_GAMUT_STANDARD_BT601 = 1, NATIVEBUFFER_COLOR_GAMUT_STANDARD_BT709 = 2, NATIVEBUFFER_COLOR_GAMUT_DCI_P3 = 3,<br/>NATIVEBUFFER_COLOR_GAMUT_SRGB = 4, NATIVEBUFFER_COLOR_GAMUT_ADOBE_RGB = 5, NATIVEBUFFER_COLOR_GAMUT_DISPLAY_P3 = 6, NATIVEBUFFER_COLOR_GAMUT_BT2020 = 7,<br/>NATIVEBUFFER_COLOR_GAMUT_BT2100_PQ = 8, NATIVEBUFFER_COLOR_GAMUT_BT2100_HLG = 9, NATIVEBUFFER_COLOR_GAMUT_DISPLAY_BT2020 = 10<br/>} | OH_NativeBuffer的色域。  |
| [OHNativeErrorCode](_o_h___native_buffer.md#ohnativeerrorcode-1) {<br/>NATIVE_ERROR_OK = 0, NATIVE_ERROR_MEM_OPERATION_ERROR = 30001000, NATIVE_ERROR_INVALID_ARGUMENTS = 40001000, NATIVE_ERROR_NO_PERMISSION = 40301000,<br/>NATIVE_ERROR_NO_BUFFER = 40601000, NATIVE_ERROR_NO_CONSUMER = 41202000, NATIVE_ERROR_NOT_INIT = 41203000, NATIVE_ERROR_CONSUMER_CONNECTED = 41206000,<br/>NATIVE_ERROR_BUFFER_STATE_INVALID = 41207000, NATIVE_ERROR_BUFFER_IN_CACHE = 41208000, NATIVE_ERROR_BUFFER_QUEUE_FULL = 41209000, NATIVE_ERROR_BUFFER_NOT_IN_CACHE = 41210000,<br/>NATIVE_ERROR_CONSUMER_DISCONNECTED = 41211000, NATIVE_ERROR_CONSUMER_NO_LISTENER_REGISTERED = 41212000, NATIVE_ERROR_UNSUPPORTED = 50102000, NATIVE_ERROR_UNKNOWN = 50002000,<br/>NATIVE_ERROR_HDI_ERROR = 50007000, NATIVE_ERROR_BINDER_ERROR = 50401000, NATIVE_ERROR_EGL_STATE_UNKNOWN = 60001000, NATIVE_ERROR_EGL_API_FAILED = 60002000<br/>} | 接口错误码说明（仅用于查询）。  |


### 函数

| 名称 | 描述 |
| -------- | -------- |
| [OH_NativeBuffer](_o_h___native_buffer.md#oh_nativebuffer) \* [OH_NativeBuffer_Alloc](_o_h___native_buffer.md#oh_nativebuffer_alloc) (const [OH_NativeBuffer_Config](_o_h___native_buffer___config.md) \*config) | 通过OH_NativeBuffer_Config创建OH_NativeBuffer实例，每次调用都会产生一个新的OH_NativeBuffer实例。<br/>本接口需要与[OH_NativeBuffer_Unreference](_o_h___native_buffer.md#oh_nativebuffer_unreference)接口配合使用，否则会存在内存泄露。<br/>本接口为非线程安全类型接口。 |
| int32_t [OH_NativeBuffer_Reference](_o_h___native_buffer.md#oh_nativebuffer_reference) ([OH_NativeBuffer](_o_h___native_buffer.md#oh_nativebuffer) \*buffer) | 将OH_NativeBuffer对象的引用计数加1。<br/>本接口需要与[OH_NativeBuffer_Unreference](_o_h___native_buffer.md#oh_nativebuffer_unreference)接口配合使用，否则会存在内存泄露。<br/>本接口为非线程安全类型接口。 |
| int32_t [OH_NativeBuffer_Unreference](_o_h___native_buffer.md#oh_nativebuffer_unreference) ([OH_NativeBuffer](_o_h___native_buffer.md#oh_nativebuffer) \*buffer) | 将OH_NativeBuffer对象的引用计数减1，当引用计数为0的时候，该NativeBuffer对象会被析构掉。<br/>本接口为非线程安全类型接口。 |
| void [OH_NativeBuffer_GetConfig](_o_h___native_buffer.md#oh_nativebuffer_getconfig) ([OH_NativeBuffer](_o_h___native_buffer.md#oh_nativebuffer) \*buffer, [OH_NativeBuffer_Config](_o_h___native_buffer___config.md) \*config) | 用于获取OH_NativeBuffer的属性。<br/>本接口为非线程安全类型接口。 |
| int32_t [OH_NativeBuffer_Map](_o_h___native_buffer.md#oh_nativebuffer_map) ([OH_NativeBuffer](_o_h___native_buffer.md#oh_nativebuffer) \*buffer, void \*\*virAddr) | 将OH_NativeBuffer对应的ION内存映射到进程空间。<br/>本接口需要与[OH_NativeBuffer_Unmap](_o_h___native_buffer.md#oh_nativebuffer_unmap)接口配合使用。<br/>本接口为非线程安全类型接口。 |
| int32_t [OH_NativeBuffer_Unmap](_o_h___native_buffer.md#oh_nativebuffer_unmap) ([OH_NativeBuffer](_o_h___native_buffer.md#oh_nativebuffer) \*buffer) | 将OH_NativeBuffer对应的ION内存从进程空间移除。<br/>本接口为非线程安全类型接口。 |
| uint32_t [OH_NativeBuffer_GetSeqNum](_o_h___native_buffer.md#oh_nativebuffer_getseqnum) ([OH_NativeBuffer](_o_h___native_buffer.md#oh_nativebuffer) \*buffer) | 获取OH_NativeBuffer的序列号。<br/>本接口为非线程安全类型接口。 |
| int32_t [OH_NativeBuffer_SetColorSpace](_o_h___native_buffer.md#oh_nativebuffer_setcolorspace) ([OH_NativeBuffer](_o_h___native_buffer.md#oh_nativebuffer) \*buffer, [OH_NativeBuffer_ColorSpace](_o_h___native_buffer.md#oh_nativebuffer_colorspace) colorSpace) | 为OH_NativeBuffer设置颜色空间属性。<br/>本接口为非线程安全类型接口。 |
| int32_t [OH_NativeBuffer_MapPlanes](_o_h___native_buffer.md#oh_nativebuffer_mapplanes) ([OH_NativeBuffer](_o_h___native_buffer.md#oh_nativebuffer) \*buffer, void \*\*virAddr, [OH_NativeBuffer_Planes](_o_h___native_buffer___planes.md) \*outPlanes) | 将OH_NativeBuffer对应的多通道ION内存映射到进程空间。<br/>本接口为非线程安全类型接口。 |
| int32_t [OH_NativeBuffer_FromNativeWindowBuffer](_o_h___native_buffer.md#oh_nativebuffer_fromnativewindowbuffer) (OHNativeWindowBuffer \*nativeWindowBuffer, [OH_NativeBuffer](_o_h___native_buffer.md#oh_nativebuffer) \*\*buffer) | 将OHNativeWindowBuffer实例转换为OH_NativeBuffer实例。<br/>本接口为非线程安全类型接口。 |
| int32_t [OH_NativeBuffer_GetColorSpace](_o_h___native_buffer.md#oh_nativebuffer_getcolorspace) ([OH_NativeBuffer](_o_h___native_buffer.md#oh_nativebuffer) \*buffer, [OH_NativeBuffer_ColorSpace](_o_h___native_buffer.md#oh_nativebuffer_colorspace) \*colorSpace) | 获取OH_NativeBuffer颜色空间属性。<br/>本接口为非线程安全类型接口。 |
| int32_t [OH_NativeBuffer_SetMetadataValue](_o_h___native_buffer.md#oh_nativebuffer_setmetadatavalue) ([OH_NativeBuffer](_o_h___native_buffer.md#oh_nativebuffer) \*buffer, [OH_NativeBuffer_MetadataKey](_o_h___native_buffer.md#oh_nativebuffer_metadatakey) metadataKey, int32_t size, uint8_t \*metaData) | 为OH_NativeBuffer设置元数据属性值。<br/>本接口为非线程安全类型接口。 |
| int32_t [OH_NativeBuffer_GetMetadataValue](_o_h___native_buffer.md#oh_nativebuffer_getmetadatavalue) ([OH_NativeBuffer](_o_h___native_buffer.md#oh_nativebuffer) \*buffer, [OH_NativeBuffer_MetadataKey](_o_h___native_buffer.md#oh_nativebuffer_metadatakey) metadataKey, int32_t \*size, uint8_t \*\*metaData) | 获取OH_NativeBuffer元数据属性值。<br/>本接口为非线程安全类型接口。 |
