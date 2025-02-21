# native_avdemuxer.h


## 概述

声明用于音视频解封装的Native API。

**库：** libnative_media_avdemuxer.so

**起始版本：** 10

**相关模块：**[AVDemuxer](_a_v_demuxer.md)


## 汇总


### 函数

| 名称 | 描述 | 
| -------- | -------- |
| OH_AVDemuxer \* [OH_AVDemuxer_CreateWithSource](_a_v_demuxer.md#oh_avdemuxer_createwithsource) ([OH_AVSource](_a_v_source.md#oh_avsource) \*source) | 通过source实例对象创建OH_AVDemuxer实例对象。 | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AVDemuxer_Destroy](_a_v_demuxer.md#oh_avdemuxer_destroy) (OH_AVDemuxer \*demuxer) | 销毁OH_AVDemuxer实例并清理内部资源。 | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AVDemuxer_SelectTrackByID](_a_v_demuxer.md#oh_avdemuxer_selecttrackbyid) (OH_AVDemuxer \*demuxer, uint32_t trackIndex) | 选中指定轨道，解封装器将会从该轨道中读取数据。 | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AVDemuxer_UnselectTrackByID](_a_v_demuxer.md#oh_avdemuxer_unselecttrackbyid) (OH_AVDemuxer \*demuxer, uint32_t trackIndex) | 取消选择指定轨道，未选中的轨道的数据不会被解封装器读取。 | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AVDemuxer_ReadSample](_a_v_demuxer.md#oh_avdemuxer_readsample) (OH_AVDemuxer \*demuxer, uint32_t trackIndex, [OH_AVMemory](_core.md#oh_avmemory) \*sample, [OH_AVCodecBufferAttr](_o_h___a_v_codec_buffer_attr.md) \*info) | 从选中轨道中获取当前位置压缩帧及相关信息。 | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AVDemuxer_ReadSampleBuffer](_a_v_demuxer.md#oh_avdemuxer_readsamplebuffer) (OH_AVDemuxer \*demuxer, uint32_t trackIndex, [OH_AVBuffer](_core.md#oh_avbuffer) \*sample) | 从选中轨道中获取当前位置压缩帧及相关信息。 | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AVDemuxer_SeekToTime](_a_v_demuxer.md#oh_avdemuxer_seektotime) (OH_AVDemuxer \*demuxer, int64_t millisecond, [OH_AVSeekMode](_codec_base.md#oh_avseekmode) mode) | 根据设定的跳转模式，将所有选中的轨道到指定时间附近。  | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AVDemuxer_SetMediaKeySystemInfoCallback](_a_v_demuxer.md#oh_avdemuxer_setmediakeysysteminfocallback) (OH_AVDemuxer \*demuxer, DRM_MediaKeySystemInfoCallback callback) | 设置异步DRM信息回调函数。  | 
| [OH_AVErrCode](_core.md#oh_averrcode) [OH_AVDemuxer_GetMediaKeySystemInfo](_a_v_demuxer.md#oh_avdemuxer_getmediakeysysteminfo) (OH_AVDemuxer \*demuxer, DRM_MediaKeySystemInfo \*mediaKeySystemInfo) | 获取DRM信息。  | 
