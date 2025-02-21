# image_mdk.h


## 概述

声明访问图像剪辑矩形、大小、格式和组件数据的方法。

**起始版本：** 10

**相关模块：** [Image](image.md)


## 汇总


### 结构体

| 名称 | 描述 | 
| -------- | -------- |
| [OhosImageRect](_o_h_o_s_1_1_media_1_1_ohos_image_rect.md) | 定义图像矩形信息。 | 
| [OhosImageComponent](_o_h_o_s_1_1_media_1_1_ohos_image_component.md) | 定义图像组成信息。 | 


### 类型定义

| 名称 | 描述 | 
| -------- | -------- |
| [ImageNative](image.md#imagenative) | 为图像接口定义native层图像对象。 | 


### 枚举

| 名称 | 描述 | 
| -------- | -------- |
| { [OHOS_IMAGE_FORMAT_YCBCR_422_SP](image.md#anonymous-enum-13) = 1000,<br/>[OHOS_IMAGE_FORMAT_JPEG](image.md#anonymous-enum-13) = 2000, } | 图像格式枚举值。 | 
| { [OHOS_IMAGE_COMPONENT_FORMAT_YUV_Y](image.md#anonymous-enum-13-1) = 1,<br/>[OHOS_IMAGE_COMPONENT_FORMAT_YUV_U](image.md#anonymous-enum-13-1) = 2,<br/>[OHOS_IMAGE_COMPONENT_FORMAT_YUV_V](image.md#anonymous-enum-13-1) = 3,<br/>[OHOS_IMAGE_COMPONENT_FORMAT_JPEG](image.md#anonymous-enum-13-1) = 4, } | 图像组成类型枚举值。 | 


### 函数

| 名称 | 描述 | 
| -------- | -------- |
| [OH_Image_InitImageNative](image.md#oh_image_initimagenative) (napi_env env, napi_value source) | 从输入的JavaScript Native API **图像** 对象中解析 native **ImageNative** 对象。 | 
| [OH_Image_ClipRect](image.md#oh_image_cliprect) (const [ImageNative](image.md#imagenative) \*native, struct [OhosImageRect](_o_h_o_s_1_1_media_1_1_ohos_image_rect.md) \*rect) | 获取native **ImageNative** 对象 [OhosImageRect](_o_h_o_s_1_1_media_1_1_ohos_image_rect.md) 信息。 | 
| [OH_Image_Size](image.md#oh_image_size) (const [ImageNative](image.md#imagenative) \*native, struct [OhosImageSize](_ohos_image_size.md) \*size) | 获取native **ImageNative** 对象的 [OhosImageSize](_ohos_image_size.md) 信息。 | 
| [OH_Image_Format](image.md#oh_image_format) (const [ImageNative](image.md#imagenative) \*native, int32_t \*format) | 获取native **ImageNative** 对象的图像格式。 | 
| [OH_Image_GetComponent](image.md#oh_image_getcomponent) (const [ImageNative](image.md#imagenative) \*native, int32_t componentType, struct [OhosImageComponent](_o_h_o_s_1_1_media_1_1_ohos_image_component.md) \*componentNative) | 从 native **ImageNative** 对象中获取 [OhosImageComponent](_o_h_o_s_1_1_media_1_1_ohos_image_component.md)。 | 
| [OH_Image_Release](image.md#oh_image_release) ([ImageNative](image.md#imagenative) \*native) | 释放 **ImageNative** native对象。 | 
<!--no_check-->