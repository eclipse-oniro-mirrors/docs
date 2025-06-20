# OH_AudioRenderer_Callbacks_Struct


## 概述

声明输出音频流的回调函数指针。

为了避免不可预期的行为，在设置音频回调函数时，请确保该结构体的每一个成员变量都被自定义的回调方法或空指针初始化。可参考[使用OHAudio开发音频播放功能](../../media/audio/using-ohaudio-for-playback.md)。

**系统能力：** SystemCapability.Multimedia.Audio.Core

**起始版本：** 10

**相关模块：**[OHAudio](_o_h_audio.md)

**所在头文件：**[native_audiostream_base.h](native__audiostream__base_8h.md)


## 汇总


### 成员变量

| 名称 | 描述 | 
| -------- | -------- |
| int32_t (\*[OH_AudioRenderer_OnWriteData](#oh_audiorenderer_onwritedata))([OH_AudioRenderer](_o_h_audio.md#oh_audiorenderer) \*renderer, void \*userData, void \*buffer, int32_t length) | 该函数指针将指向用于写入音频数据的回调函数。  | 
| int32_t (\*[OH_AudioRenderer_OnStreamEvent](#oh_audiorenderer_onstreamevent))([OH_AudioRenderer](_o_h_audio.md#oh_audiorenderer) \*renderer, void \*userData, [OH_AudioStream_Event](_o_h_audio.md#oh_audiostream_event) event) | 该函数指针将指向用于处理音频播放流事件的回调函数。  | 
| int32_t (\*[OH_AudioRenderer_OnInterruptEvent](#oh_audiorenderer_oninterruptevent))([OH_AudioRenderer](_o_h_audio.md#oh_audiorenderer) \*renderer, void \*userData, [OH_AudioInterrupt_ForceType](_o_h_audio.md#oh_audiointerrupt_forcetype) type, [OH_AudioInterrupt_Hint](_o_h_audio.md#oh_audiointerrupt_hint) hint) | 该函数指针将指向用于处理音频播放中断事件的回调函数。  | 
| int32_t (\*[OH_AudioRenderer_OnError](#oh_audiorenderer_onerror))([OH_AudioRenderer](_o_h_audio.md#oh_audiorenderer) \*renderer, void \*userData, [OH_AudioStream_Result](_o_h_audio.md#oh_audiostream_result) error) | 该函数指针将指向用于处理音频播放错误结果的回调函数。  | 


## 结构体成员变量说明

> **说明：**
> 以下回调接口的返回值没有枚举定义，当前版本实现并不按返回值区分处理，但为保证后续版本可扩展，默认使用0。


### OH_AudioRenderer_OnError

```
int32_t (*OH_AudioRenderer_Callbacks_Struct::OH_AudioRenderer_OnError)(OH_AudioRenderer *renderer, void *userData, OH_AudioStream_Result error)
```
**描述**
该函数指针将指向用于处理音频播放错误结果的回调函数。

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| renderer | 指向[OH_AudioStreamBuilder_GenerateRenderer](_o_h_audio.md#oh_audiostreambuilder_generaterenderer)创建的音频流实例。 |
| userData | 指向应用自定义的数据存储区域。 |
| error | 音频播放错误结果[OH_AudioStream_Result](_o_h_audio.md#oh_audiostream_result)，AUDIOSTREAM_ERROR_INVALID_PARAM、AUDIOSTREAM_ERROR_ILLEGAL_STATE或者AUDIOSTREAM_ERROR_SYSTEM。 |


### OH_AudioRenderer_OnInterruptEvent

```
int32_t (*OH_AudioRenderer_Callbacks_Struct::OH_AudioRenderer_OnInterruptEvent)(OH_AudioRenderer *renderer, void *userData, OH_AudioInterrupt_ForceType type, OH_AudioInterrupt_Hint hint)
```
**描述**
该函数指针将指向用于处理音频播放中断事件的回调函数。

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| renderer | 指向[OH_AudioStreamBuilder_GenerateRenderer](_o_h_audio.md#oh_audiostreambuilder_generaterenderer)创建的音频流实例。 |
| userData | 指向应用自定义的数据存储区域。 |
| type | 音频中断类型[OH_AudioInterrupt_ForceType](_o_h_audio.md#oh_audiointerrupt_forcetype)。 |
| hint | 音频中断提示类型[OH_AudioInterrupt_Hint](_o_h_audio.md#oh_audiointerrupt_hint)。 |

### OH_AudioRenderer_OnStreamEvent

```
int32_t (*OH_AudioRenderer_Callbacks_Struct::OH_AudioRenderer_OnStreamEvent)(OH_AudioRenderer *renderer, void *userData, OH_AudioStream_Event event)
```
**描述**
该函数指针将指向用于处理音频播放流事件的回调函数。

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| renderer | 指向[OH_AudioStreamBuilder_GenerateRenderer](_o_h_audio.md#oh_audiostreambuilder_generaterenderer)创建的音频流实例。 |
| userData | 指向应用自定义的数据存储区域。 |
| event | 音频事件[OH_AudioStream_Event](_o_h_audio.md#oh_audiostream_event)。 |


### OH_AudioRenderer_OnWriteData

```
int32_t (*OH_AudioRenderer_Callbacks_Struct::OH_AudioRenderer_OnWriteData)(OH_AudioRenderer *renderer, void *userData, void *buffer, int32_t length)
```
**描述**
该函数指针将指向用于写入音频数据的回调函数。

回调函数仅用来写入音频数据，请勿在回调函数中调用AudioRenderer相关接口。

回调函数结束后，音频服务会把buffer指针数据放入队列里等待播放，因此请勿在回调外再次更改buffer指向的数据，且务必保证往buffer填满length长度的待播放数据，否则会导致音频服务播放杂音。

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| renderer | 指向[OH_AudioStreamBuilder_GenerateRenderer](_o_h_audio.md#oh_audiostreambuilder_generaterenderer)创建的音频流实例。 |
| userData | 指向应用自定义的数据存储区域。 |
| buffer | 指向播放数据存储区域，用于应用填充播放数据。 |
| length | buffer的长度。 |
