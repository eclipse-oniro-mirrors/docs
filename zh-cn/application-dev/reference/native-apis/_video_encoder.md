# VideoEncoder


## 概述

VideoEncoder模块提供用于视频编码功能的函数和枚举。该模块在部分设备上可能不支持，可以通过[CanIUse](../syscap.md)接口确认。

@syscap SystemCapability.Multimedia.Media.VideoEncoder

**起始版本：**
9

## 汇总


### 文件

  | 名称 | 描述 | 
| -------- | -------- |
| [native_avcodec_videoencoder.h](native__avcodec__videoencoder_8h.md) | 声明用于视频编码的Native API。<br>引用文件：<multimedia/player_framework/native_avcodec_videoencoder.h>  | 


### 类型定义

  | 名称 | 描述 | 
| -------- | -------- |
| [OH_VideoEncodeBitrateMode](#oh_videoencodebitratemode) | 视频编码的比特率模式。  | 


### 枚举

  | 名称 | 描述 | 
| -------- | -------- |
| [OH_VideoEncodeBitrateMode](#oh_videoencodebitratemode) { **CBR** = 0, **VBR** = 1, **CQ** = 2 } | 视频编码的比特率模式。  | 


### 函数

  | 名称 | 描述 | 
| -------- | -------- |
| [OH_VideoEncoder_CreateByMime](#oh_videoencoder_createbymime) (const char \*mime) | 通过mime类型创建一个视频编码器实例，大多数情况下推荐使用该接口。  | 
| [OH_VideoEncoder_CreateByName](#oh_videoencoder_createbyname) (const char \*name) | 通过视频编码器名称创建一个视频编码器实例，使用这个接口的前提是必须清楚编码器准确的名称。  | 
| [OH_VideoEncoder_Destroy](#oh_videoencoder_destroy) (OH_AVCodec \*codec) | 清空编码器内部资源，并销毁编码器实例。  | 
| [OH_VideoEncoder_SetCallback](#oh_videoencoder_setcallback) (OH_AVCodec \*codec, [OH_AVCodecAsyncCallback](_o_h___a_v_codec_async_callback.md) callback, void \*userData) | 设置异步回调函数，使得你的应用能够响应视频编码器产生的事件，该接口被调用必须是在Prepare被调用前。  | 
| [OH_VideoEncoder_Configure](#oh_videoencoder_configure) (OH_AVCodec \*codec, OH_AVFormat \*format) | 配置视频编码器，典型地，需要配置被编码视频轨道的描述信息，该接口被调用必须是在Prepare被调用前。  | 
| [OH_VideoEncoder_Prepare](#oh_videoencoder_prepare) (OH_AVCodec \*codec) | 准备编码器内部资源，调用该接口前必须先调用Configure接口。  | 
| [OH_VideoEncoder_Start](#oh_videoencoder_start) (OH_AVCodec \*codec) | 启动编码器，该接口必须在已经Prepare成功后调用。 在启动成功后，编码器将开始报告[OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata)事件。  | 
| [OH_VideoEncoder_Stop](#oh_videoencoder_stop) (OH_AVCodec \*codec) | 停止编码器。在停止后可通过Start重新进入Started状态。  | 
| [OH_VideoEncoder_Flush](#oh_videoencoder_flush) (OH_AVCodec \*codec) | 清空编码器内部缓存的输入输出数据。在该接口被调用后，所有先前通过异步回调报告的Buffer的索引都将 失效，确保不要再访问这些索引对应的Buffers。  | 
| [OH_VideoEncoder_Reset](#oh_videoencoder_reset) (OH_AVCodec \*codec) | 重置编码器。如需继续编码工作，需要重新调用Configure接口以配置该编码器实例。  | 
| [OH_VideoEncoder_GetOutputDescription](#oh_videoencoder_getoutputdescription) (OH_AVCodec \*codec) | 获取该编码器输出数据的描述信息，需要注意的是，返回值所指向的OH_AVFormat实例的生命周期 将会再下一次调用该接口时或者该OH_AVCodec实例被销毁时失效。  | 
| [OH_VideoEncoder_SetParameter](#oh_videoencoder_setparameter) (OH_AVCodec \*codec, OH_AVFormat \*format) | 向编码器设置动态参数，注意：该接口仅能在编码器被启动后调用，同时错误的参数设置，可能会导致编码失败。  | 
| [OH_VideoEncoder_GetSurface](#oh_videoencoder_getsurface) (OH_AVCodec \*codec, OHNativeWindow \*\*window) | 从视频编码器获取输入Surface， 该接口被调用必须是在Prepare被调用前。  | 
| [OH_VideoEncoder_FreeOutputData](#oh_videoencoder_freeoutputdata) (OH_AVCodec \*codec, uint32_t index) | 将处理结束的输出Buffer交还给编码器。  | 
| [OH_VideoEncoder_NotifyEndOfStream](#oh_videoencoder_notifyendofstream) (OH_AVCodec \*codec) | 通知视频编码器输入码流已结束。surface模式推荐使用该接口通知编码器码流结束。  | 


## 类型定义说明


### OH_VideoEncodeBitrateMode

  
```
typedef enum OH_VideoEncodeBitrateModeOH_VideoEncodeBitrateMode
```
**描述:**
视频编码的比特率模式。

@syscap SystemCapability.Multimedia.Media.VideoEncoder


## 枚举类型说明


### OH_VideoEncodeBitrateMode

  
```
enum OH_VideoEncodeBitrateMode
```
**描述:**
视频编码的比特率模式。

@syscap SystemCapability.Multimedia.Media.VideoEncoder

  | 枚举值 | 描述 | 
| -------- | -------- |
| CBR  | 恒定比特率模式 | 
| VBR  | 可变比特率模式 | 
| CQ  | 恒定质量模式 | 


## 函数说明


### OH_VideoEncoder_Configure()

  
```
OH_AVErrCode OH_VideoEncoder_Configure (OH_AVCodec * codec, OH_AVFormat * format )
```
**描述:**
配置视频编码器，典型地，需要配置被编码视频轨道的描述信息，该接口被调用必须是在Prepare被调用前。

@syscap SystemCapability.Multimedia.Media.VideoEncoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 
| format | 指向OH_AVFormat的指针，用以给出待编码视频轨道的描述信息  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoEncoder_CreateByMime()

  
```
OH_AVCodec* OH_VideoEncoder_CreateByMime (const char * mime)
```
**描述:**
通过mime类型创建一个视频编码器实例，大多数情况下推荐使用该接口。

@syscap SystemCapability.Multimedia.Media.VideoEncoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| mime | mime类型描述字符串，参考[OH_AVCODEC_MIMETYPE_VIDEO_AVC](_codec_base.md#oh_avcodec_mimetype_video_avc) | 

**返回:**

返回一个指向OH_AVCodec实例的指针


### OH_VideoEncoder_CreateByName()

  
```
OH_AVCodec* OH_VideoEncoder_CreateByName (const char * name)
```
**描述:**
通过视频编码器名称创建一个视频编码器实例，使用这个接口的前提是必须清楚编码器准确的名称。

@syscap SystemCapability.Multimedia.Media.VideoEncoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| name | 视频编码器名称  | 

**返回:**

返回一个指向OH_AVCodec实例的指针


### OH_VideoEncoder_Destroy()

  
```
OH_AVErrCode OH_VideoEncoder_Destroy (OH_AVCodec * codec)
```
**描述:**
清空编码器内部资源，并销毁编码器实例。

@syscap SystemCapability.Multimedia.Media.VideoEncoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoEncoder_Flush()

  
```
OH_AVErrCode OH_VideoEncoder_Flush (OH_AVCodec * codec)
```
**描述:**
清空编码器内部缓存的输入输出数据。在该接口被调用后，所有先前通过异步回调报告的Buffer的索引都将 失效，确保不要再访问这些索引对应的Buffers。

@syscap SystemCapability.Multimedia.Media.VideoEncoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoEncoder_FreeOutputData()

  
```
OH_AVErrCode OH_VideoEncoder_FreeOutputData (OH_AVCodec * codec, uint32_t index )
```
**描述:**
将处理结束的输出Buffer交还给编码器。

@syscap SystemCapability.Multimedia.Media.VideoEncoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 
| index | 输出Buffer对应的索引值  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoEncoder_GetOutputDescription()

  
```
OH_AVFormat* OH_VideoEncoder_GetOutputDescription (OH_AVCodec * codec)
```
**描述:**
获取该编码器输出数据的描述信息，需要注意的是，返回值所指向的OH_AVFormat实例的生命周期 将会再下一次调用该接口时或者该OH_AVCodec实例被销毁时失效。

@syscap SystemCapability.Multimedia.Media.VideoEncoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 

**返回:**

返回AVFormat实例的指针


### OH_VideoEncoder_GetSurface()

  
```
OH_AVErrCode OH_VideoEncoder_GetSurface (OH_AVCodec * codec, OHNativeWindow ** window )
```
**描述:**
从视频编码器获取输入Surface， 该接口被调用必须是在Prepare被调用前。

@syscap SystemCapability.Multimedia.Media.VideoEncoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 
| window | 指向一个OHNativeWindow实例的指针  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoEncoder_NotifyEndOfStream()

  
```
OH_AVErrCode OH_VideoEncoder_NotifyEndOfStream (OH_AVCodec * codec)
```
**描述:**
通知视频编码器输入码流已结束。surface模式推荐使用该接口通知编码器码流结束。

@syscap SystemCapability.Multimedia.Media.VideoEncoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoEncoder_Prepare()

  
```
OH_AVErrCode OH_VideoEncoder_Prepare (OH_AVCodec * codec)
```
**描述:**
准备编码器内部资源，调用该接口前必须先调用Configure接口。

@syscap SystemCapability.Multimedia.Media.VideoEncoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoEncoder_Reset()

  
```
OH_AVErrCode OH_VideoEncoder_Reset (OH_AVCodec * codec)
```
**描述:**
重置编码器。如需继续编码工作，需要重新调用Configure接口以配置该编码器实例。

@syscap SystemCapability.Multimedia.Media.VideoEncoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoEncoder_SetCallback()

  
```
OH_AVErrCode OH_VideoEncoder_SetCallback (OH_AVCodec * codec, OH_AVCodecAsyncCallback callback, void * userData )
```
**描述:**
设置异步回调函数，使得你的应用能够响应视频编码器产生的事件，该接口被调用必须是在Prepare被调用前。

@syscap SystemCapability.Multimedia.Media.VideoEncoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 
| callback | 一个包含所有回调函数的集合体，参考[OH_AVCodecAsyncCallback](_o_h___a_v_codec_async_callback.md) | 
| userData | 用户特定数据  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoEncoder_SetParameter()

  
```
OH_AVErrCode OH_VideoEncoder_SetParameter (OH_AVCodec * codec, OH_AVFormat * format )
```
**描述:**
向编码器设置动态参数，注意：该接口仅能在编码器被启动后调用，同时错误的参数设置，可能会导致编码失败。

@syscap SystemCapability.Multimedia.Media.VideoEncoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 
| format | OH_AVFormat句柄指针  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoEncoder_Start()

  
```
OH_AVErrCode OH_VideoEncoder_Start (OH_AVCodec * codec)
```
**描述:**
启动编码器，该接口必须在已经Prepare成功后调用。 在启动成功后，编码器将开始报告[OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata)事件。

@syscap SystemCapability.Multimedia.Media.VideoEncoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoEncoder_Stop()

  
```
OH_AVErrCode OH_VideoEncoder_Stop (OH_AVCodec * codec)
```
**描述:**
停止编码器。在停止后可通过Start重新进入Started状态。

@syscap SystemCapability.Multimedia.Media.VideoEncoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)
