# native_avcodec_base.h


## 概述

声明运行音视频编解码通用的结构体、字符常量、枚举。

**起始版本：**
9

**相关模块:**

[CodecBase](_codec_base.md)


## 汇总


### 结构体

| 名称 | 描述 | 
| -------- | -------- |
| [OH_AVCodecBufferAttr](_o_h___a_v_codec_buffer_attr.md) | 定义OH_AVCodec的Buffer描述信息。| 
| [OH_AVCodecAsyncCallback](_o_h___a_v_codec_async_callback.md) | AVCodec所有的异步回调函数指针集合。注册一个该结构体实例给OH_AVCodec实例，并处理通过该回调报告 的信息，以确保AVCodec正常运转。| 


### 类型定义

| 名称 | 描述 | 
| -------- | -------- |
| [OH_AVCodecBufferFlags](_codec_base.md#oh_avcodecbufferflags) | 枚举OH_AVCodec的Buffer标记的类别。| 
| [OH_AVCodecBufferAttr](_codec_base.md#oh_avcodecbufferattr) | 定义OH_AVCodec的Buffer描述信息。| 
| (\*[OH_AVCodecOnError](_codec_base.md#oh_avcodeconerror)) (OH_AVCodec \*codec, int32_t errorCode, void \*userData) | 当OH_AVCodec实例运行发生错误时，该函数指针会被调用以报告具体错误信息。| 
| (\*[OH_AVCodecOnStreamChanged](_codec_base.md#oh_avcodeconstreamchanged)) (OH_AVCodec \*codec, OH_AVFormat \*format, void \*userData) | 当输出流发生变化时，该函数指针会被调用以报告新的流描述信息。 需要注意的时，OH_AVFormat指针的生命周期仅维持在该函数指针被调用时上有效，禁止在调用结束后继续访问。| 
| (\*[OH_AVCodecOnNeedInputData](_codec_base.md#oh_avcodeconneedinputdata)) (OH_AVCodec \*codec, uint32_t index, OH_AVMemory \*data, void \*userData) | 当AVCodec运行过程中需要新的输入数据时，该函数指针会被调用，并携带一块可用的Buffer以供填入新的输入数据。| 
| (\*[OH_AVCodecOnNewOutputData](_codec_base.md#oh_avcodeconnewoutputdata)) (OH_AVCodec \*codec, uint32_t index, OH_AVMemory \*data, [OH_AVCodecBufferAttr](_o_h___a_v_codec_buffer_attr.md) \*attr, void \*userData) | 当AVCodec运行过程中产生了新的输出数据时，该函数指针会被调用，并携带一块包含新输出数据的Buffer， 需要注意的是，OH_AVCodecBufferAttr指针的生命周期仅维持在该函数指针被调用时有效，禁止调用结束后继续访问。| 
| [OH_AVCodecAsyncCallback](_codec_base.md#oh_avcodecasynccallback) | AVCodec所有的异步回调函数指针集合。注册一个该结构体实例给OH_AVCodec实例，并处理通过该回调报告 的信息，以确保AVCodec正常运转。| 
| [OH_MediaType](_codec_base.md#oh_mediatype) | 媒体类型。| 
| [OH_AVCProfile](_codec_base.md#oh_avcprofile) | AVC Profile枚举。| 
| [OH_AACProfile](_codec_base.md#oh_aacprofile) | AAC Profile枚举。| 


### 枚举

| 名称 | 描述 | 
| -------- | -------- |
| [OH_AVCodecBufferFlags](_codec_base.md#oh_avcodecbufferflags) {<br/>**AVCODEC_BUFFER_FLAGS_NONE** = 0,  **AVCODEC_BUFFER_FLAGS_EOS** = 1 &lt;&lt; 0,  **AVCODEC_BUFFER_FLAGS_SYNC_FRAME** = 1 &lt;&lt; 1,  **AVCODEC_BUFFER_FLAGS_INCOMPLETE_FRAME** = 1 &lt;&lt; 2,<br/> **AVCODEC_BUFFER_FLAGS_CODEC_DATA** = 1 &lt;&lt; 3<br/>} | 枚举OH_AVCodec的Buffer标记的类别。| 
| [OH_MediaType](_codec_base.md#oh_mediatype) {  **MEDIA_TYPE_AUD** = 0,  **MEDIA_TYPE_VID** = 1 } | 媒体类型。| 
| [OH_AVCProfile](_codec_base.md#oh_avcprofile) { **AVC_PROFILE_BASELINE** = 0, **AVC_PROFILE_HIGH** = 4, **AVC_PROFILE_MAIN** = 8 } | AVC Profile枚举。| 
| [OH_AACProfile](_codec_base.md#oh_aacprofile) { **AAC_PROFILE_LC** = 0 } | AAC Profile枚举。| 


### 变量

| 名称 | 描述 | 
| -------- | -------- |
| [OH_AVCODEC_MIMETYPE_VIDEO_AVC](_codec_base.md#oh_avcodec_mimetype_video_avc) | AVC视频编解码器的MIME类型。| 
| [OH_AVCODEC_MIMETYPE_AUDIO_AAC](_codec_base.md#oh_avcodec_mimetype_audio_aac) | AAC音频编解码器的MIME类型。| 
| [OH_ED_KEY_TIME_STAMP](_codec_base.md#oh_ed_key_time_stamp) | 提供统一的surface Buffer附属数据的字符描述符。| 
| [OH_ED_KEY_EOS](_codec_base.md#oh_ed_key_eos) | surface附属数据中结束流的字符描述符，值类型为bool。 | 
| [OH_MD_KEY_TRACK_TYPE](_codec_base.md#oh_md_key_track_type) | 为媒体播放框架提供统一的字符描述符。| 
| [OH_MD_KEY_CODEC_MIME](_codec_base.md#oh_md_key_codec_mime) | MIME类型的字符描述符，值类型为string。 | 
| [OH_MD_KEY_DURATION](_codec_base.md#oh_md_key_duration) |duration的字符描述符，值类型为int64_t。| 
| [OH_MD_KEY_BITRATE](_codec_base.md#oh_md_key_bitrate) | 比特率的字符描述符，值类型为uint32_t。 | 
| [OH_MD_KEY_MAX_INPUT_SIZE](_codec_base.md#oh_md_key_max_input_size) | 最大输入尺寸的字符描述符，值类型为uint32_t。 | 
| [OH_MD_KEY_WIDTH](_codec_base.md#oh_md_key_width) | 视频宽度的字符描述符，值类型为uint32_t。 | 
| [OH_MD_KEY_HEIGHT](_codec_base.md#oh_md_key_height) | 视频高度的字符描述符，值类型为uint32_t。 | 
| [OH_MD_KEY_PIXEL_FORMAT](_codec_base.md#oh_md_key_pixel_format) | 视频像素格式的字符描述符，值类型为int32_t，具体见[OH_AVPixelFormat](_core.md#oh_avpixelformat)。 | 
| [OH_MD_KEY_AUDIO_SAMPLE_FORMAT](_codec_base.md#oh_md_key_audio_sample_format) | 音频采样格式的字符描述符，值类型为uint32_t。 | 
| [OH_MD_KEY_FRAME_RATE](_codec_base.md#oh_md_key_frame_rate) | 视频帧率的字符描述符，值类型为double。| 
| [OH_MD_KEY_VIDEO_ENCODE_BITRATE_MODE](_codec_base.md#oh_md_key_video_encode_bitrate_mode) | 视频编码比特率模式的字符描述符，值类型为int32_t，具体见[OH_VideoEncodeBitrateMode](_video_encoder.md#oh_videoencodebitratemode)。 | 
| [OH_MD_KEY_PROFILE](_codec_base.md#oh_md_key_profile) | 音视频编码能力的字符描述符，值类型为int32_t，具体见[OH_AVCProfile](_codec_base.md#oh_avcprofile)或[OH_AACProfile](_codec_base.md#oh_aacprofile)。 | 
| [OH_MD_KEY_AUD_CHANNEL_COUNT](_codec_base.md#oh_md_key_aud_channel_count) | 音频声道数的字符描述符，值类型为uint32_t。 | 
| [OH_MD_KEY_AUD_SAMPLE_RATE](_codec_base.md#oh_md_key_aud_sample_rate) | 音频采样率的字符描述符，值类型为uint32_t。 | 
| [OH_MD_KEY_I_FRAME_INTERVAL](_codec_base.md#oh_md_key_i_frame_interval) | I帧间隔时长的字符描述符，值类型为int32_t，单位是毫秒。| 
| [OH_MD_KEY_ROTATION](_codec_base.md#oh_md_key_rotation) | surface旋转角度的字符描述符，值类型为int32_t，限于{0, 90, 180, 270}，默认值为0。 | 
