# AudioCodec


## 概述

AudioCodec模块提供用于音频编解码功能的函数。

**系统能力：** SystemCapability.Multimedia.Media.AudioCodec

**起始版本：** 11


## 汇总


### 文件

| 名称 | 描述 | 
| -------- | -------- |
| [native_avcodec_audiocodec.h](native__avcodec__audiocodec_8h.md) | 声明用于音频编解码的Native API。 | 


### 函数

| 名称 | 描述 | 
| -------- | -------- |
| OH_AVCodec \* [OH_AudioCodec_CreateByMime](#oh_audiocodec_createbymime) (const char \*mime, bool isEncoder) | 根据MIME类型创建音频编解码器实例。 | 
| OH_AVCodec \* [OH_AudioCodec_CreateByName](#oh_audiocodec_createbyname) (const char \*name) | 通过音频编解码器名称创建音频编解码器实例。 | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AudioCodec_Destroy](#oh_audiocodec_destroy) (OH_AVCodec \*codec) | 清理编解码器内部资源，销毁编解码器实例。 | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AudioCodec_RegisterCallback](#oh_audiocodec_registercallback) (OH_AVCodec \*codec, [OH_AVCodecCallback](_o_h___a_v_codec_callback.md) callback, void \*userData) | 设置异步回调函数，使应用可以响应音频编解码器生成的事件。在调用Prepare之前，必须调用此接口。 | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AudioCodec_Configure](#oh_audiocodec_configure) (OH_AVCodec \*codec, const OH_AVFormat \*format) | 要配置音频编解码器，通常需要配置音频描述信息。 | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AudioCodec_Prepare](#oh_audiocodec_prepare) (OH_AVCodec \*codec) | 准备编解码器的内部资源。 | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AudioCodec_Start](#oh_audiocodec_start) (OH_AVCodec \*codec) | Prepare成功后调用此接口启动编解码器。 | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AudioCodec_Stop](#oh_audiocodec_stop) (OH_AVCodec \*codec) | 停止编解码器。 | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AudioCodec_Flush](#oh_audiocodec_flush) (OH_AVCodec \*codec) | 清除编解码器中缓存的输入和输出数据。 | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AudioCodec_Reset](#oh_audiocodec_reset) (OH_AVCodec \*codec) | 重置编解码器。如果要继续编解码，需要再次调用Configure接口配置编解码器实例。 | 
| OH_AVFormat \* [OH_AudioCodec_GetOutputDescription](#oh_audiocodec_getoutputdescription) (OH_AVCodec \*codec) | 获取编解码器输出数据的描述信息。 | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AudioCodec_SetParameter](#oh_audiocodec_setparameter) (OH_AVCodec \*codec, const OH_AVFormat \*format) | 配置编解码器的动态参数。 | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AudioCodec_PushInputBuffer](#oh_audiocodec_pushinputbuffer) (OH_AVCodec \*codec, uint32_t index) | 将填充有数据的输入缓冲区提交给音频编解码器。 | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AudioCodec_FreeOutputBuffer](#oh_audiocodec_freeoutputbuffer) (OH_AVCodec \*codec, uint32_t index) | 将处理后的输出缓冲区返回给编解码器。 | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AudioCodec_IsValid](#oh_audiocodec_isvalid) (OH_AVCodec \*codec, bool \*isValid) | 检查当前编解码器实例是否有效，可用于后台故障恢复或应用程序从后台恢复时检测编解码器有效状态。 | 


## 函数说明


### OH_AudioCodec_Configure()

```
OH_AVErrCode OH_AudioCodec_Configure (OH_AVCodec *codec, const OH_AVFormat *format)
```

**描述**

要配置音频编解码器，通常需要配置音频描述信息。在调用Prepare之前，必须调用此接口。

**系统能力：** SystemCapability.Multimedia.Media.AudioCodec

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针。 | 
| format | 指向OH_AVFormat的指针，给出要编解码的音频轨道的描述。 | 

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅 [OH_AVErrCode](_core.md#oh_averrcode)。


### OH_AudioCodec_CreateByMime()

```
OH_AVCodec* OH_AudioCodec_CreateByMime (const char *mime, bool isEncoder)
```

**描述**

根据MIME类型创建音频编解码器实例，大多数场景下建议使用此方式。

**系统能力：** SystemCapability.Multimedia.Media.AudioCodec

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| mime | MIME类型描述字符串，请参阅[AVCODEC_MIMETYPE](_codec_base.md#变量)。 | 
| isEncoder | true表示需要创建编码器，false表示需要创建解码器。 | 

**返回：**

返回OH_AVCodec实例的指针。


### OH_AudioCodec_CreateByName()

```
OH_AVCodec* OH_AudioCodec_CreateByName (const char *name)
```

**描述**

通过音频编解码器名称创建音频编解码器实例，使用此接口的前提是知道编解码器的确切名称。

**系统能力：** SystemCapability.Multimedia.Media.AudioCodec

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| name | 音频编解码器名称。 | 

**返回：**

返回OH_AVCodec实例的指针。


### OH_AudioCodec_Destroy()

```
OH_AVErrCode OH_AudioCodec_Destroy (OH_AVCodec *codec)
```

**描述**

清理编解码器内部资源，销毁编解码器实例。

**系统能力：** SystemCapability.Multimedia.Media.AudioCodec

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针。 | 

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅 [OH_AVErrCode](_core.md#oh_averrcode)。


### OH_AudioCodec_Flush()

```
OH_AVErrCode OH_AudioCodec_Flush (OH_AVCodec *codec)
```

**描述**

清除编解码器中缓存的输入和输出数据。

调用此接口后，以前通过异步回调上报的所有缓冲区索引都将失效，请确保不要访问这些索引对应的缓冲区。

**系统能力：** SystemCapability.Multimedia.Media.AudioCodec

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针。 | 

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅 [OH_AVErrCode](_core.md#oh_averrcode)。


### OH_AudioCodec_FreeOutputBuffer()

```
OH_AVErrCode OH_AudioCodec_FreeOutputBuffer (OH_AVCodec *codec, uint32_t index)
```

**描述**

将处理后的输出缓冲区返回给编解码器。

**系统能力：** SystemCapability.Multimedia.Media.AudioCodec

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针。 | 
| index | 输出Buffer对应的索引值。 | 

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅 [OH_AVErrCode](_core.md#oh_averrcode)。


### OH_AudioCodec_GetOutputDescription()

```
OH_AVFormat* OH_AudioCodec_GetOutputDescription (OH_AVCodec *codec)
```

**描述**

获取编解码器输出数据的描述信息。

需要注意的是，返回值所指向的OH_AVFormat实例的生命周期需要调用[OH_AVFormat_Destroy](_core.md#oh_avformat_destroy)接口手动释放。

**系统能力：** SystemCapability.Multimedia.Media.AudioCodec

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针。 | 

**返回：**

返回OH_AVFormat句柄指针，生命周期将使用下一个GetOutputDescription刷新，或使用OH_AVCodec销毁。


### OH_AudioCodec_IsValid()

```
OH_AVErrCode OH_AudioCodec_IsValid (OH_AVCodec *codec, bool *isValid)
```

**描述**

检查当前编解码器实例是否有效，可用于后台故障恢复或应用程序从后台恢复时检测编解码器有效状态。

**系统能力：** SystemCapability.Multimedia.Media.AudioCodec

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针。 | 
| isValid | 输出参数。指向布尔实例的指针，true：编解码器实例有效，false：编解码器实例无效。 | 

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅 [OH_AVErrCode](_core.md#oh_averrcode)。


### OH_AudioCodec_Prepare()

```
OH_AVErrCode OH_AudioCodec_Prepare (OH_AVCodec *codec)
```

**描述**

准备编解码器的内部资源，在调用此接口之前必须调用Configure接口。

**系统能力：** SystemCapability.Multimedia.Media.AudioCodec

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针。 | 

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅 [OH_AVErrCode](_core.md#oh_averrcode)。


### OH_AudioCodec_PushInputBuffer()

```
OH_AVErrCode OH_AudioCodec_PushInputBuffer (OH_AVCodec *codec, uint32_t index)
```

**描述**

将填充有数据的输入缓冲区提交给音频编解码器。

[OH_AVCodecOnNeedInputBuffer](_codec_base.md#oh_avcodeconneedinputbuffer)回调将报告可用的输入缓冲区和对应的索引值。一旦具有指定索引的缓冲区被提交给音频编解码器，该缓冲区将无法再次访问， 直到再次收到[OH_AVCodecOnNeedInputBuffer](_codec_base.md#oh_avcodeconneedinputbuffer)回调，收到相同索引时此缓冲区才可使用。

此外，对于某些编解码器，需要在开始时向编解码器输入编解码特定配置数据(Codec-Specific-Data)， 以初始化编解码器的编解码过程。

**系统能力：** SystemCapability.Multimedia.Media.AudioCodec

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针。 | 
| index | 输入缓冲区Buffer对应的索引值。 | 

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅 [OH_AVErrCode](_core.md#oh_averrcode)。


### OH_AudioCodec_RegisterCallback()

```
OH_AVErrCode OH_AudioCodec_RegisterCallback (OH_AVCodec *codec, OH_AVCodecCallback callback, void *userData)
```

**描述**

设置异步回调函数，使应用可以响应音频编解码器生成的事件。在调用Prepare之前，必须调用此接口。

**系统能力：** SystemCapability.Multimedia.Media.AudioCodec

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针。 | 
| callback | 所有回调函数的集合，请参见 [OH_AVCodecCallback](_o_h___a_v_codec_callback.md)。 | 
| userData | 用户特定数据。 | 

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅 [OH_AVErrCode](_core.md#oh_averrcode)。


### OH_AudioCodec_Reset()

```
OH_AVErrCode OH_AudioCodec_Reset (OH_AVCodec *codec)
```

**描述**

重置编解码器。如果要继续编解码，需要再次调用Configure接口配置编解码器实例。

**系统能力：** SystemCapability.Multimedia.Media.AudioCodec

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针。 | 

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅 [OH_AVErrCode](_core.md#oh_averrcode)。


### OH_AudioCodec_SetParameter()

```
OH_AVErrCode OH_AudioCodec_SetParameter (OH_AVCodec *codec, const OH_AVFormat *format)
```

**描述**

配置编解码器的动态参数。

注意：该接口必须在编解码器启动后才能调用。另外，参数配置错误可能会导致编解码失败。

**系统能力：** SystemCapability.Multimedia.Media.AudioCodec

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针。 | 
| format | OH_AVFormat句柄指针。 | 

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅 [OH_AVErrCode](_core.md#oh_averrcode)。


### OH_AudioCodec_Start()

```
OH_AVErrCode OH_AudioCodec_Start (OH_AVCodec *codec)
```

**描述**

Prepare成功后调用此接口启动编解码器。启动后，编解码器将开始上报OH_AVCodecOnNeedInputBuffer事件。

**系统能力：** SystemCapability.Multimedia.Media.AudioCodec

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针。 | 

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅 [OH_AVErrCode](_core.md#oh_averrcode)。


### OH_AudioCodec_Stop()

```
OH_AVErrCode OH_AudioCodec_Stop (OH_AVCodec *codec)
```

**描述**

停止编解码器。

停止后，可以通过Start重新进入已启动状态（started），但需要注意的是， 如果编解码器之前已输入数据，则需要重新输入编解码器数据。

**系统能力：** SystemCapability.Multimedia.Media.AudioCodec

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| codec | 指向OH_AVCodec实例的指针。 | 

**返回：**

如果执行成功，则返回AV_ERR_OK，否则返回特定错误代码，请参阅 [OH_AVErrCode](_core.md#oh_averrcode)。
