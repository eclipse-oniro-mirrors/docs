# OH_AVRecorder_Config

## 概述

提供媒体AVRecorder的配置定义。

**起始版本：** 18

**相关模块：** [AVRecorder](capi-avrecorder.md)

**所在头文件：** [avrecorder_base.h](capi-avrecorder-base-h.md)

## 汇总

### 成员变量

| 名称 | 描述 |
| -- | -- |
| [OH_AVRecorder_AudioSourceType](capi-avrecorder-base-h.md#oh_avrecorder_audiosourcetype) audioSourceType | 录制音频源类型。 |
| [OH_AVRecorder_VideoSourceType](capi-avrecorder-base-h.md#oh_avrecorder_videosourcetype) videoSourceType | 录制视频源类型。 |
| [OH_AVRecorder_Profile](capi-oh-avrecorder-profile.md) profile | 包含音频和视频编码配置。 |
| char* url | 定义文件URL，格式为fd://xx。 |
| [OH_AVRecorder_FileGenerationMode](capi-avrecorder-base-h.md#oh_avrecorder_filegenerationmode) fileGenerationMode | 指定录制输出文件的生成模式。 |
| [OH_AVRecorder_Metadata](capi-oh-avrecorder-metadata.md) metadata | 包含录制媒体的附加元数据。 |
| int32_t maxDuration | 指定录制的最大时长。 |


