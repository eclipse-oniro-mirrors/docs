# OH_Pixelmap_HdrGainmapMetadata

## 概述

HDR_GAINMAP_METADATA关键字对应的gainmap相关元数据值，参考ISO 21496-1。

**起始版本：** 12

**相关模块：** [Image_NativeModule](capi-image-nativemodule.md)

**所在头文件：** [pixelmap_native.h](capi-pixelmap-native-h.md)

## 汇总

### 成员变量

| 名称 | 描述 |
| -- | -- |
| uint16_t writerVersion | 元数据编写器使用的版本。 |
| uint16_t miniVersion | 元数据解析需要理解的最小版本。 |
| uint8_t gainmapChannelNum | Gainmap的颜色通道数，值为3时RGB通道的元数据值不同，值为1时各通道元数据值相同。 |
| bool useBaseColorFlag | 是否使用基础图的色彩空间，参考ISO 21496-1。 |
| float baseHeadroom | 基础图提亮比，参考ISO 21496-1。 |
| float alternateHeadroom | 提取的可选择图像提亮比，参考ISO 21496-1。 |
| float gainmapMax[3] | 增强图像的最大值，参考ISO 21496-1。 |
| float gainmapMin[3] | 增强图像的最小值，参考ISO 21496-1。 |
| float gamma[3] | gamma值，参考ISO 21496-1。 |
| float baselineOffset[3] | 基础图的偏移，参考ISO 21496-1。 |
| float alternateOffset[3] | 提取的可选择图像偏移量，参考ISO 21496-1。 |


