# CodecVideoPortCap


## 概述

定义视频编解码能力。

**起始版本：** 4.1

**相关模块：**[Codec](_codec_v20.md)


## 汇总


### Public 属性

| 名称 | 描述 | 
| -------- | -------- |
| struct [Rect](_rect_v20.md)[minSize](#minsize) | 支持的最小分辨率。  | 
| struct [Rect](_rect_v20.md)[maxSize](#maxsize) | 支持的最大分辨率。  | 
| struct [Alignment](_alignment_v20.md)[whAlignment](#whalignment) | 宽高对齐值。  | 
| struct [RangeValue](_range_value_v20.md)[blockCount](#blockcount) | 支持的块数量范围。  | 
| struct [RangeValue](_range_value_v20.md)[blocksPerSecond](#blockspersecond) | 每秒可处理的块数量范围。  | 
| struct [Rect](_rect_v20.md)[blockSize](#blocksize) | 支持的块大小。  | 
| int[] [supportPixFmts](#supportpixfmts) | 支持的像素格式，详见**Display中display_type.h定义的PixeFormat**。  | 
| enum [BitRateMode](_codec_v20.md#bitratemode)[] bitRatemode struct [RangeValue](_range_value_v20.md)[frameRate](#framerate) | 传输速率模式，有恒定的，有变化的等几种模式。详见[BitRateMode](_codec_v20.md#bitratemode)。  | 
|  int[] [measuredFrameRate](#measuredframerate) | &lt; 帧率的范围。 实测的帧率。  | 


## 类成员变量说明


### blockCount

```
struct RangeValue CodecVideoPortCap::blockCount
```
**描述**
支持的块数量范围。


### blockSize

```
struct Rect CodecVideoPortCap::blockSize
```
**描述**
支持的块大小。


### blocksPerSecond

```
struct RangeValue CodecVideoPortCap::blocksPerSecond
```
**描述**
每秒可处理的块数量范围。


### frameRate

```
enum BitRateMode [] bitRatemode struct RangeValue CodecVideoPortCap::frameRate
```
**描述**
传输速率模式，有恒定的，有变化的等几种模式。详见[BitRateMode](_codec_v20.md#bitratemode)。


### maxSize

```
struct Rect CodecVideoPortCap::maxSize
```
**描述**
支持的最大分辨率。


### measuredFrameRate

```
 int [] CodecVideoPortCap::measuredFrameRate
```
**描述**
&lt; 帧率的范围。 实测的帧率。


### minSize

```
struct Rect CodecVideoPortCap::minSize
```
**描述**
支持的最小分辨率。


### supportPixFmts

```
int [] CodecVideoPortCap::supportPixFmts
```
**描述**
支持的像素格式，详见**Display中display_type.h定义的PixeFormat**。


### whAlignment

```
struct Alignment CodecVideoPortCap::whAlignment
```
**描述**
宽高对齐值。
