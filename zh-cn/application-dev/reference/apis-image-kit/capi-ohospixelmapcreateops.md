# OhosPixelMapCreateOps

## 概述

用于定义创建 pixel map 设置选项的相关信息。

**起始版本：** 10

**相关模块：** [Image](capi-image.md)

**所在头文件：** [image_pixel_map_mdk.h](capi-image-pixel-map-mdk-h.md)

## 汇总

### 成员变量

| 名称 | 描述 |
| -- | -- |
| uint32_t width | 图片的宽，用pixels表示。 |
| uint32_t height | 图片的高，用pixels表示。 |
| int32_t pixelFormat | 图片的格式。取值范围：<br>0：未知格式。<br>2：格式为RGB_565。<br>3：格式为RGBA_8888<br>4：	格式为BGRA_8888。<br>5：格式为RGB_888。<br>6：格式为ALPHA_8。<br>7：格式为RGBA_F16。<br>8：格式为NV21。<br>9：格式为NV12。 |
| uint32_t editable | 图片的编辑类型，true为图像像素可编辑，false为不可编辑。 |
| uint32_t alphaType | 图片的alpha类型。取值范围：<br>0：未知透明度。<br>1：没有alpha或图片全透明。<br>2：RGB前乘alpha。<br>3：	RGB不前乘alpha。 |
| uint32_t scaleMode | 图片的缩放类型。取值范围：<br>1：缩放图像以填充目标图像区域并居中裁剪区域外的效果。<br>0：图像适合目标尺寸的效果。 |


