# native_avcodec_audiodecoder.h


## 概述

声明用于音频解码的Native API。

**起始版本：**
9

**相关模块:**

[AudioDecoder](_audio_decoder.md)


## 汇总


### 函数

  | 名称 | 描述 | 
| -------- | -------- |
| [OH_AudioDecoder_CreateByMime](_audio_decoder.md#oh_audiodecoder_createbymime) (const char \*mime) | 通过mime类型创建一个音频解码器实例，大多数情况下推荐使用该接口。  | 
| [OH_AudioDecoder_CreateByName](_audio_decoder.md#oh_audiodecoder_createbyname) (const char \*name) | 通过音频解码器名称创建一个音频解码器实例，使用这个接口的前提是必须清楚解码器准确的名称。  | 
| [OH_AudioDecoder_Destroy](_audio_decoder.md#oh_audiodecoder_destroy) (OH_AVCodec \*codec) | 清空解码器内部资源，并销毁解码器实例  | 
| [OH_AudioDecoder_SetCallback](_audio_decoder.md#oh_audiodecoder_setcallback) (OH_AVCodec \*codec, [OH_AVCodecAsyncCallback](_o_h___a_v_codec_async_callback.md) callback, void \*userData) | 设置异步回调函数，使得你的应用能够响应音频解码器产生的事件，该接口被调用必须是在Prepare被调用前。  | 
| [OH_AudioDecoder_Configure](_audio_decoder.md#oh_audiodecoder_configure) (OH_AVCodec \*codec, OH_AVFormat \*format) | 配置音频解码器，典型地，需要配置被解码音频轨道的描述信息，这些信息能够从容器中提取出来， 该接口被调用必须是在Prepare被调用前。  | 
| [OH_AudioDecoder_Prepare](_audio_decoder.md#oh_audiodecoder_prepare) (OH_AVCodec \*codec) | 准备解码器内部资源，调用该接口前必须先调用Configure接口。  | 
| [OH_AudioDecoder_Start](_audio_decoder.md#oh_audiodecoder_start) (OH_AVCodec \*codec) | 启动解码器，该接口必须在已经Prepare成功后调用。 在启动成功后，解码器将开始报告[OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata)事件。  | 
| [OH_AudioDecoder_Stop](_audio_decoder.md#oh_audiodecoder_stop) (OH_AVCodec \*codec) | 停止解码器。在停止后可通过Start重新进入Started状态，但需要注意的是，若先前给解码器输入过 Codec-Specific-Data，则需要重新输入。  | 
| [OH_AudioDecoder_Flush](_audio_decoder.md#oh_audiodecoder_flush) (OH_AVCodec \*codec) | 清空解码器内部缓存的输入输出数据。在该接口被调用后，所有先前通过异步回调报告的Buffer的索引都将 失效，确保不要再访问这些索引对应的Buffers。  | 
| [OH_AudioDecoder_Reset](_audio_decoder.md#oh_audiodecoder_reset) (OH_AVCodec \*codec) | 重置解码器。如需继续解码工作，需要重新调用Configure接口以配置该解码器实例。  | 
| [OH_AudioDecoder_GetOutputDescription](_audio_decoder.md#oh_audiodecoder_getoutputdescription) (OH_AVCodec \*codec) | 获取该解码器输出数据的描述信息，需要注意的是，返回值所指向的OH_AVFormat实例需调用者手动释放。  | 
| [OH_AudioDecoder_SetParameter](_audio_decoder.md#oh_audiodecoder_setparameter) (OH_AVCodec \*codec, OH_AVFormat \*format) | 向解码器设置动态参数，注意：该接口仅能在解码器被启动后调用，同时错误的参数设置，可能会导致解码失败。  | 
| [OH_AudioDecoder_PushInputData](_audio_decoder.md#oh_audiodecoder_pushinputdata) (OH_AVCodec \*codec, uint32_t index, [OH_AVCodecBufferAttr](_o_h___a_v_codec_buffer_attr.md) attr) | 将填充好数据的输入Buffer提交给音频解码器。[OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata)回调会报告可用的输入 Buffer及对应的索引值。一旦指定索引的Buffer被提交给解码器，直到再一次收到[OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata) 回调报告相同索引的Buffer可用前，该Buffer都不可以再次被访问。另外，对于部分解码器，要求在最开始给解码器输入 Codec-Specific-Data，用以初始化解码器的解码过程。  | 
| [OH_AudioDecoder_FreeOutputData](_audio_decoder.md#oh_audiodecoder_freeoutputdata) (OH_AVCodec \*codec, uint32_t index) | 将处理结束的输出Buffer交还给解码器。  | 
