# native_avcodec_videodecoder.h


## 概述

声明用于视频解码的Native API。

**起始版本：**
9

**相关模块:**

[VideoDecoder](_video_decoder.md)


## 汇总


### 函数

| 名称 | 描述 | 
| -------- | -------- |
| [OH_VideoDecoder_CreateByMime](_video_decoder.md#oh_videodecoder_createbymime) (const char \*mime) | 通过mime类型创建一个视频解码器实例，大多数情况下推荐使用该接口。| 
| [OH_VideoDecoder_CreateByName](_video_decoder.md#oh_videodecoder_createbyname) (const char \*name) | 通过视频解码器名称创建一个视频解码器实例，使用这个接口的前提是必须清楚解码器准确的名称。| 
| [OH_VideoDecoder_Destroy](_video_decoder.md#oh_videodecoder_destroy) (OH_AVCodec \*codec) | 清空解码器内部资源，并销毁解码器实例。| 
| [OH_VideoDecoder_SetCallback](_video_decoder.md#oh_videodecoder_setcallback) (OH_AVCodec \*codec, [OH_AVCodecAsyncCallback](_o_h___a_v_codec_async_callback.md) callback, void \*userData) | 设置异步回调函数，使得你的应用能够响应视频解码器产生的事件，该接口被调用必须是在Prepare被调用前。| 
| [OH_VideoDecoder_SetSurface](_video_decoder.md#oh_videodecoder_setsurface) (OH_AVCodec \*codec, OHNativeWindow \*window) | 指定输出Surface，以提供视频解码输出，该接口被调用必须是在Prepare被调用前。| 
| [OH_VideoDecoder_Configure](_video_decoder.md#oh_videodecoder_configure) (OH_AVCodec \*codec, OH_AVFormat \*format) | 配置视频解码器，典型地，需要配置被解码视频轨道的描述信息，这些信息能够从容器中提取出来， 该接口被调用必须是在Prepare被调用前。| 
| [OH_VideoDecoder_Prepare](_video_decoder.md#oh_videodecoder_prepare) (OH_AVCodec \*codec) | 准备解码器内部资源，调用该接口前必须先调用Configure接口。| 
| [OH_VideoDecoder_Start](_video_decoder.md#oh_videodecoder_start) (OH_AVCodec \*codec) | 启动解码器，该接口必须在已经Prepare成功后调用。 在启动成功后，解码器将开始报告[OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata)事件。| 
| [OH_VideoDecoder_Stop](_video_decoder.md#oh_videodecoder_stop) (OH_AVCodec \*codec) | 停止解码器。在停止后可通过Start重新进入Started状态，但需要注意的是，若先前给解码器输入过 Codec-Specific-Data，则需要重新输入。| 
| [OH_VideoDecoder_Flush](_video_decoder.md#oh_videodecoder_flush) (OH_AVCodec \*codec) | 清空解码器内部缓存的输入输出数据。在该接口被调用后，所有先前通过异步回调报告的Buffer的索引都将 失效，确保不要再访问这些索引对应的Buffers。| 
| [OH_VideoDecoder_Reset](_video_decoder.md#oh_videodecoder_reset) (OH_AVCodec \*codec) | 重置解码器。如需继续解码工作，需要重新调用Configure接口以配置该解码器实例。| 
| [OH_VideoDecoder_GetOutputDescription](_video_decoder.md#oh_videodecoder_getoutputdescription) (OH_AVCodec \*codec) | 获取该解码器输出数据的描述信息，需要注意的是，返回值所指向的OH_AVFormat实例的生命周期 将会再下一次调用该接口时或者该OH_AVCodec实例被销毁时失效。| 
| [OH_VideoDecoder_SetParameter](_video_decoder.md#oh_videodecoder_setparameter) (OH_AVCodec \*codec, OH_AVFormat \*format) | 向解码器设置动态参数，注意：该接口仅能在解码器被启动后调用，同时错误的参数设置，可能会导致解码失败。| 
| [OH_VideoDecoder_PushInputData](_video_decoder.md#oh_videodecoder_pushinputdata) (OH_AVCodec \*codec, uint32_t index, [OH_AVCodecBufferAttr](_o_h___a_v_codec_buffer_attr.md) attr) | 将填充好数据的输入Buffer提交给视频解码器。[OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata)回调会报告可用的输入 Buffer及对应的索引值。一旦指定索引的Buffer被提交给解码器，直到再一次收到[OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata) 回调报告相同索引的Buffer可用前，该Buffer都不可以再次被访问。另外，对于部分解码器，要求在最开始给解码器输入 Codec-Specific-Data，用以初始化解码器的解码过程，例如H264格式的PPS/SPS数据。| 
| [OH_VideoDecoder_RenderOutputData](_video_decoder.md#oh_videodecoder_renderoutputdata) (OH_AVCodec \*codec, uint32_t index) | 将处理结束的输出Buffer交还给解码器，并通知解码器完成将该Buffer内包含的解码后的数据在输出Surface上渲染。 如果先前未配置输出Surface，调用该接口仅仅将指定索引对应的输出Buffer交还给解码器。| 
| [OH_VideoDecoder_FreeOutputData](_video_decoder.md#oh_videodecoder_freeoutputdata) (OH_AVCodec \*codec, uint32_t index) | 将处理结束的输出Buffer交还给解码器。| 
