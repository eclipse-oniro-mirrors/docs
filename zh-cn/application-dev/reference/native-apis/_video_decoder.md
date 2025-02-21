# VideoDecoder


## 概述

VideoDecoder模块提供用于视频解码功能的函数。该模块在部分设备上可能不支持，可以通过[CanIUse](../syscap.md)接口确认。

@syscap SystemCapability.Multimedia.Media.VideoDecoder

**起始版本：**
9


## 汇总


### 文件

  | 名称 | 描述 | 
| -------- | -------- |
| [native_avcodec_videodecoder.h](native__avcodec__videodecoder_8h.md) | 声明用于视频解码的Native API。<br>引用文件：<multimedia/player_framework/native_avcodec_videodecoder.h>  | 


### 函数

  | 名称 | 描述 | 
| -------- | -------- |
| [OH_VideoDecoder_CreateByMime](#oh_videodecoder_createbymime) (const char \*mime) | 通过mime类型创建一个视频解码器实例，大多数情况下推荐使用该接口。  | 
| [OH_VideoDecoder_CreateByName](#oh_videodecoder_createbyname) (const char \*name) | 通过视频解码器名称创建一个视频解码器实例，使用这个接口的前提是必须清楚解码器准确的名称。  | 
| [OH_VideoDecoder_Destroy](#oh_videodecoder_destroy) (OH_AVCodec \*codec) | 清空解码器内部资源，并销毁解码器实例。  | 
| [OH_VideoDecoder_SetCallback](#oh_videodecoder_setcallback) (OH_AVCodec \*codec, [OH_AVCodecAsyncCallback](_o_h___a_v_codec_async_callback.md) callback, void \*userData) | 设置异步回调函数，使得你的应用能够响应视频解码器产生的事件，该接口被调用必须是在Prepare被调用前。  | 
| [OH_VideoDecoder_SetSurface](#oh_videodecoder_setsurface) (OH_AVCodec \*codec, OHNativeWindow \*window) | 指定输出Surface，以提供视频解码输出，该接口被调用必须是在Prepare被调用前。  | 
| [OH_VideoDecoder_Configure](#oh_videodecoder_configure) (OH_AVCodec \*codec, OH_AVFormat \*format) | 配置视频解码器，典型地，需要配置被解码视频轨道的描述信息，这些信息能够从容器中提取出来， 该接口被调用必须是在Prepare被调用前。  | 
| [OH_VideoDecoder_Prepare](#oh_videodecoder_prepare) (OH_AVCodec \*codec) | 准备解码器内部资源，调用该接口前必须先调用Configure接口。  | 
| [OH_VideoDecoder_Start](#oh_videodecoder_start) (OH_AVCodec \*codec) | 启动解码器，该接口必须在已经Prepare成功后调用。 在启动成功后，解码器将开始报告[OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata)事件。  | 
| [OH_VideoDecoder_Stop](#oh_videodecoder_stop) (OH_AVCodec \*codec) | 停止解码器。在停止后可通过Start重新进入Started状态，但需要注意的是，若先前给解码器输入过 Codec-Specific-Data，则需要重新输入。  | 
| [OH_VideoDecoder_Flush](#oh_videodecoder_flush) (OH_AVCodec \*codec) | 清空解码器内部缓存的输入输出数据。在该接口被调用后，所有先前通过异步回调报告的Buffer的索引都将 失效，确保不要再访问这些索引对应的Buffers。  | 
| [OH_VideoDecoder_Reset](#oh_videodecoder_reset) (OH_AVCodec \*codec) | 重置解码器。如需继续解码工作，需要重新调用Configure接口以配置该解码器实例。  | 
| [OH_VideoDecoder_GetOutputDescription](#oh_videodecoder_getoutputdescription) (OH_AVCodec \*codec) | 获取该解码器输出数据的描述信息，需要注意的是，返回值所指向的OH_AVFormat实例的生命周期 将会再下一次调用该接口时或者该OH_AVCodec实例被销毁时失效。  | 
| [OH_VideoDecoder_SetParameter](#oh_videodecoder_setparameter) (OH_AVCodec \*codec, OH_AVFormat \*format) | 向解码器设置动态参数，注意：该接口仅能在解码器被启动后调用，同时错误的参数设置，可能会导致解码失败。  | 
| [OH_VideoDecoder_PushInputData](#oh_videodecoder_pushinputdata) (OH_AVCodec \*codec, uint32_t index, [OH_AVCodecBufferAttr](_o_h___a_v_codec_buffer_attr.md) attr) | 将填充好数据的输入Buffer提交给视频解码器。[OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata)回调会报告可用的输入 Buffer及对应的索引值。一旦指定索引的Buffer被提交给解码器，直到再一次收到[OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata) 回调报告相同索引的Buffer可用前，该Buffer都不可以再次被访问。另外，对于部分解码器，要求在最开始给解码器输入 Codec-Specific-Data，用以初始化解码器的解码过程，例如H264格式的PPS/SPS数据。  | 
| [OH_VideoDecoder_RenderOutputData](#oh_videodecoder_renderoutputdata) (OH_AVCodec \*codec, uint32_t index) | 将处理结束的输出Buffer交还给解码器，并通知解码器完成将该Buffer内包含的解码后的数据在输出Surface上渲染。 如果先前未配置输出Surface，调用该接口仅仅将指定索引对应的输出Buffer交还给解码器。  | 
| [OH_VideoDecoder_FreeOutputData](#oh_videodecoder_freeoutputdata) (OH_AVCodec \*codec, uint32_t index) | 将处理结束的输出Buffer交还给解码器。  | 


## 函数说明


### OH_VideoDecoder_Configure()

  
```
OH_AVErrCode OH_VideoDecoder_Configure (OH_AVCodec * codec, OH_AVFormat * format )
```
**描述:**
配置视频解码器，典型地，需要配置被解码视频轨道的描述信息，这些信息能够从容器中提取出来， 该接口被调用必须是在Prepare被调用前。

@syscap SystemCapability.Multimedia.Media.VideoDecoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 
| format | 指向OH_AVFormat的指针，用以给出待解码视频轨道的描述信息  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoDecoder_CreateByMime()

  
```
OH_AVCodec* OH_VideoDecoder_CreateByMime (const char * mime)
```
**描述:**
通过mime类型创建一个视频解码器实例，大多数情况下推荐使用该接口。

@syscap SystemCapability.Multimedia.Media.VideoDecoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| mime | mime类型描述字符串，参考[OH_AVCODEC_MIMETYPE_VIDEO_AVC](_codec_base.md#oh_avcodec_mimetype_video_avc) | 

**返回:**

返回一个指向OH_AVCodec实例的指针


### OH_VideoDecoder_CreateByName()

  
```
OH_AVCodec* OH_VideoDecoder_CreateByName (const char * name)
```
**描述:**
通过视频解码器名称创建一个视频解码器实例，使用这个接口的前提是必须清楚解码器准确的名称。

@syscap SystemCapability.Multimedia.Media.VideoDecoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| name | 视频解码器名称  | 

**返回:**

返回一个指向OH_AVCodec实例的指针


### OH_VideoDecoder_Destroy()

  
```
OH_AVErrCode OH_VideoDecoder_Destroy (OH_AVCodec * codec)
```
**描述:**
清空解码器内部资源，并销毁解码器实例。

@syscap SystemCapability.Multimedia.Media.VideoDecoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoDecoder_Flush()

  
```
OH_AVErrCode OH_VideoDecoder_Flush (OH_AVCodec * codec)
```
**描述:**
清空解码器内部缓存的输入输出数据。在该接口被调用后，所有先前通过异步回调报告的Buffer的索引都将 失效，确保不要再访问这些索引对应的Buffers。

@syscap SystemCapability.Multimedia.Media.VideoDecoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoDecoder_FreeOutputData()

  
```
OH_AVErrCode OH_VideoDecoder_FreeOutputData (OH_AVCodec * codec, uint32_t index )
```
**描述:**
将处理结束的输出Buffer交还给解码器。

@syscap SystemCapability.Multimedia.Media.VideoDecoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 
| index | 输出Buffer对应的索引值  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoDecoder_GetOutputDescription()

  
```
OH_AVFormat* OH_VideoDecoder_GetOutputDescription (OH_AVCodec * codec)
```
**描述:**
获取该解码器输出数据的描述信息，需要注意的是，返回值所指向的OH_AVFormat实例的生命周期 将会再下一次调用该接口时或者该OH_AVCodec实例被销毁时失效。

@syscap SystemCapability.Multimedia.Media.VideoDecoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 

**返回:**

返回AVFormat实例的指针


### OH_VideoDecoder_Prepare()

  
```
OH_AVErrCode OH_VideoDecoder_Prepare (OH_AVCodec * codec)
```
**描述:**
准备解码器内部资源，调用该接口前必须先调用Configure接口。

@syscap SystemCapability.Multimedia.Media.VideoDecoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoDecoder_PushInputData()

  
```
OH_AVErrCode OH_VideoDecoder_PushInputData (OH_AVCodec * codec, uint32_t index, OH_AVCodecBufferAttr attr )
```
**描述:**
将填充好数据的输入Buffer提交给视频解码器。[OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata)回调会报告可用的输入 Buffer及对应的索引值。一旦指定索引的Buffer被提交给解码器，直到再一次收到[OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata) 回调报告相同索引的Buffer可用前，该Buffer都不可以再次被访问。另外，对于部分解码器，要求在最开始给解码器输入 Codec-Specific-Data，用以初始化解码器的解码过程，例如H264格式的PPS/SPS数据。

@syscap SystemCapability.Multimedia.Media.VideoDecoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 
| index | 输入Buffer对应的索引值  | 
| attr | 描述该Buffer内所包含数据的信息  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoDecoder_RenderOutputData()

  
```
OH_AVErrCode OH_VideoDecoder_RenderOutputData (OH_AVCodec * codec, uint32_t index )
```
**描述:**
将处理结束的输出Buffer交还给解码器，并通知解码器完成将该Buffer内包含的解码后的数据在输出Surface上渲染。 如果先前未配置输出Surface，调用该接口仅仅将指定索引对应的输出Buffer交还给解码器。

@syscap SystemCapability.Multimedia.Media.VideoDecoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 
| index | 输出Buffer对应的索引值  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoDecoder_Reset()

  
```
OH_AVErrCode OH_VideoDecoder_Reset (OH_AVCodec * codec)
```
**描述:**
重置解码器。如需继续解码工作，需要重新调用Configure接口以配置该解码器实例。

@syscap SystemCapability.Multimedia.Media.VideoDecoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoDecoder_SetCallback()

  
```
OH_AVErrCode OH_VideoDecoder_SetCallback (OH_AVCodec * codec, OH_AVCodecAsyncCallback callback, void * userData )
```
**描述:**
设置异步回调函数，使得你的应用能够响应视频解码器产生的事件，该接口被调用必须是在Prepare被调用前。

@syscap SystemCapability.Multimedia.Media.VideoDecoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 
| callback | 一个包含所有回调函数的集合体，参考[OH_AVCodecAsyncCallback](_o_h___a_v_codec_async_callback.md) | 
| userData | 用户特定数据  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoDecoder_SetParameter()

  
```
OH_AVErrCode OH_VideoDecoder_SetParameter (OH_AVCodec * codec, OH_AVFormat * format )
```
**描述:**
向解码器设置动态参数，注意：该接口仅能在解码器被启动后调用，同时错误的参数设置，可能会导致解码失败。

@syscap SystemCapability.Multimedia.Media.VideoDecoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 
| format | 指向OH_AVFormat实例的指针  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoDecoder_SetSurface()

  
```
OH_AVErrCode OH_VideoDecoder_SetSurface (OH_AVCodec * codec, OHNativeWindow * window )
```
**描述:**
指定输出Surface，以提供视频解码输出，该接口被调用必须是在Prepare被调用前。

@syscap SystemCapability.Multimedia.Media.VideoDecoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 
| window | 指向一个OHNativeWindow实例的指针  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoDecoder_Start()

  
```
OH_AVErrCode OH_VideoDecoder_Start (OH_AVCodec * codec)
```
**描述:**
启动解码器，该接口必须在已经Prepare成功后调用。 在启动成功后，解码器将开始报告[OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata)事件。

@syscap SystemCapability.Multimedia.Media.VideoDecoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)


### OH_VideoDecoder_Stop()

  
```
OH_AVErrCode OH_VideoDecoder_Stop (OH_AVCodec * codec)
```
**描述:**
停止解码器。在停止后可通过Start重新进入Started状态，但需要注意的是，若先前给解码器输入过 Codec-Specific-Data，则需要重新输入。

@syscap SystemCapability.Multimedia.Media.VideoDecoder

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针  | 

**返回:**

执行成功返回AV_ERR_OK

执行失败返回具体错误码，参考[OH_AVErrCode](_core.md#oh_averrcode)
