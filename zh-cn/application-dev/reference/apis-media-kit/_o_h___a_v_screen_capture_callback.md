# OH_AVScreenCaptureCallback


## 概述

OH_AVScreenCapture中所有异步回调函数指针的集合。将该结构体的实例注册到OH_AVScreenCapture实例中，并处理回调上报的信息，以保证OH_AVScreenCapture的正常运行。

从API 12开始，推荐使用接口[OH_AVScreenCapture_OnError](_a_v_screen_capture.md#oh_avscreencapture_onerror) [OH_AVScreenCapture_OnBufferAvailable](_a_v_screen_capture.md#oh_avscreencapture_onbufferavailable)替代。

**系统能力：** SystemCapability.Multimedia.Media.AVScreenCapture

**起始版本：** 10

**相关模块：**[AVScreenCapture](_a_v_screen_capture.md)

**所在头文件：**[native_avscreen_capture_base.h](native__avscreen__capture__base_8h.md)


## 汇总


### 成员变量

| 名称 | 描述 | 
| -------- | -------- |
| [OH_AVScreenCaptureOnError](_a_v_screen_capture.md#oh_avscreencaptureonerror) [onError](#onerror) | 监控录屏调用操作错误，请参见[OH_AVScreenCaptureOnError](_a_v_screen_capture.md#oh_avscreencaptureonerror)。 | 
| [OH_AVScreenCaptureOnAudioBufferAvailable](_a_v_screen_capture.md#oh_avscreencaptureonaudiobufferavailable) [onAudioBufferAvailable](#onaudiobufferavailable) | 监控音频码流是否有数据产生，请参见[OH_AVScreenCaptureOnAudioBufferAvailable](_a_v_screen_capture.md#oh_avscreencaptureonaudiobufferavailable)。 | 
| [OH_AVScreenCaptureOnVideoBufferAvailable](_a_v_screen_capture.md#oh_avscreencaptureonvideobufferavailable) [onVideoBufferAvailable](#onvideobufferavailable) | 监控视频码流是否有数据产生，请参见[OH_AVScreenCaptureOnVideoBufferAvailable](_a_v_screen_capture.md#oh_avscreencaptureonvideobufferavailable)。 | 


## 结构体成员变量说明


### onAudioBufferAvailable

```
OH_AVScreenCaptureOnAudioBufferAvailable OH_AVScreenCaptureCallback::onAudioBufferAvailable
```

监控音频码流是否有数据产生，请参见[OH_AVScreenCaptureOnAudioBufferAvailable](_a_v_screen_capture.md#oh_avscreencaptureonaudiobufferavailable)。

从API 12开始，推荐使用接口[OH_AVScreenCapture_OnBufferAvailable](_a_v_screen_capture.md#oh_avscreencapture_onbufferavailable)替代。

**起始版本：** 10


### onError

```
OH_AVScreenCaptureOnError OH_AVScreenCaptureCallback::onError
```

监控录屏调用操作错误，请参见[OH_AVScreenCaptureOnError](_a_v_screen_capture.md#oh_avscreencaptureonerror)。

从API 12开始，推荐使用接口[OH_AVScreenCapture_OnError](_a_v_screen_capture.md#oh_avscreencapture_onerror)替代。

**起始版本：** 10


### onVideoBufferAvailable

```
OH_AVScreenCaptureOnVideoBufferAvailable OH_AVScreenCaptureCallback::onVideoBufferAvailable
```

监控视频码流是否有数据产生，请参见[OH_AVScreenCaptureOnVideoBufferAvailable](_a_v_screen_capture.md#oh_avscreencaptureonvideobufferavailable)。

从API 12开始，推荐使用接口[OH_AVScreenCapture_OnBufferAvailable](_a_v_screen_capture.md#oh_avscreencapture_onbufferavailable)替代。

**起始版本：** 10