# @ohos.multimedia.audio (音频管理)

音频管理提供管理音频的一些基础能力，包括对音频音量、音频设备的管理，以及对音频数据的采集和渲染等。

该模块提供以下音频相关的常用功能：

- [AudioManager](#audiomanager)：音频管理。
- [AudioRenderer](#audiorenderer8)：音频渲染，用于播放PCM（Pulse Code Modulation）音频数据。
- [AudioCapturer](#audiocapturer8)：音频采集，用于录制PCM音频数据。

> **说明：**
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import audio from '@ohos.multimedia.audio';
```

## 常量

| 名称                                    | 类型      | 可读  | 可写 | 说明               |
| --------------------------------------- | ----------| ---- | ---- | ------------------ |
| DEFAULT_VOLUME_GROUP_ID<sup>9+</sup>    | number    | 是   | 否   | 默认音量组id。<br> **系统能力：** SystemCapability.Multimedia.Audio.Volume       |
| DEFAULT_INTERRUPT_GROUP_ID<sup>9+</sup> | number    | 是   | 否   | 默认音频中断组id。<br> **系统能力：** SystemCapability.Multimedia.Audio.Interrupt       |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

const defaultVolumeGroupId = audio.DEFAULT_VOLUME_GROUP_ID;
const defaultInterruptGroupId = audio.DEFAULT_INTERRUPT_GROUP_ID;
```

## audio.getAudioManager

getAudioManager(): AudioManager

获取音频管理器。

**系统能力：** SystemCapability.Multimedia.Audio.Core

**返回值：**

| 类型                          | 说明         |
| ----------------------------- | ------------ |
| [AudioManager](#audiomanager) | 音频管理对象。 |

**示例：**
```ts
import audio from '@ohos.multimedia.audio';

let audioManager = audio.getAudioManager();
```

## audio.createAudioRenderer<sup>8+</sup>

createAudioRenderer(options: AudioRendererOptions, callback: AsyncCallback\<AudioRenderer>): void

获取音频渲染器。使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                                            | 必填 | 说明             |
| -------- | ----------------------------------------------- | ---- | ---------------- |
| options  | [AudioRendererOptions](#audiorendereroptions8)  | 是   | 配置渲染器。     |
| callback | AsyncCallback<[AudioRenderer](#audiorenderer8)> | 是   | 回调函数。当获取音频渲染器成功，err为undefined，data为获取到的音频渲染器对象；否则为错误对象。 |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

let audioStreamInfo: audio.AudioStreamInfo = {
  samplingRate: audio.AudioSamplingRate.SAMPLE_RATE_44100,
  channels: audio.AudioChannel.CHANNEL_1,
  sampleFormat: audio.AudioSampleFormat.SAMPLE_FORMAT_S16LE,
  encodingType: audio.AudioEncodingType.ENCODING_TYPE_RAW
}

let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_VOICE_COMMUNICATION,
  rendererFlags: 0
}

let audioRendererOptions: audio.AudioRendererOptions = {
  streamInfo: audioStreamInfo,
  rendererInfo: audioRendererInfo
}

audio.createAudioRenderer(audioRendererOptions,(err, data) => {
  if (err) {
    console.error(`AudioRenderer Created: Error: ${err}`);
  } else {
    console.info('AudioRenderer Created: Success: SUCCESS');
    let audioRenderer = data;
  }
});
```

## audio.createAudioRenderer<sup>8+</sup>

createAudioRenderer(options: AudioRendererOptions): Promise<AudioRenderer\>

获取音频渲染器。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名  | 类型                                           | 必填 | 说明         |
| :------ | :--------------------------------------------- | :--- | :----------- |
| options | [AudioRendererOptions](#audiorendereroptions8) | 是   | 配置渲染器。 |

**返回值：**

| 类型                                      | 说明             |
| ----------------------------------------- | ---------------- |
| Promise<[AudioRenderer](#audiorenderer8)> | Promise对象，返回音频渲染器对象。 |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';

let audioStreamInfo: audio.AudioStreamInfo = {
  samplingRate: audio.AudioSamplingRate.SAMPLE_RATE_44100,
  channels: audio.AudioChannel.CHANNEL_1,
  sampleFormat: audio.AudioSampleFormat.SAMPLE_FORMAT_S16LE,
  encodingType: audio.AudioEncodingType.ENCODING_TYPE_RAW
}

let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_VOICE_COMMUNICATION,
  rendererFlags: 0
}

let audioRendererOptions: audio.AudioRendererOptions = {
  streamInfo: audioStreamInfo,
  rendererInfo: audioRendererInfo
}

let audioRenderer: audio.AudioRenderer;
audio.createAudioRenderer(audioRendererOptions).then((data) => {
  audioRenderer = data;
  console.info('AudioFrameworkRenderLog: AudioRenderer Created : Success : Stream Type: SUCCESS');
}).catch((err: BusinessError) => {
  console.error(`AudioFrameworkRenderLog: AudioRenderer Created : ERROR : ${err}`);
});
```

## audio.createAudioCapturer<sup>8+</sup>

createAudioCapturer(options: AudioCapturerOptions, callback: AsyncCallback<AudioCapturer\>): void

获取音频采集器。使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**需要权限：** ohos.permission.MICROPHONE

仅设置Mic音频源（即[SourceType](#sourcetype8)为SOURCE_TYPE_MIC）时需要该权限。

**参数：**

| 参数名   | 类型                                            | 必填 | 说明             |
| :------- | :---------------------------------------------- | :--- | :--------------- |
| options  | [AudioCapturerOptions](#audiocaptureroptions8)  | 是   | 配置音频采集器。 |
| callback | AsyncCallback<[AudioCapturer](#audiocapturer8)> | 是   | 回调函数。当获取音频采集器成功，err为undefined，data为获取到的音频采集器对象；否则为错误对象。 |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

let audioStreamInfo: audio.AudioStreamInfo = {
  samplingRate: audio.AudioSamplingRate.SAMPLE_RATE_44100,
  channels: audio.AudioChannel.CHANNEL_2,
  sampleFormat: audio.AudioSampleFormat.SAMPLE_FORMAT_S16LE,
  encodingType: audio.AudioEncodingType.ENCODING_TYPE_RAW
}

let audioCapturerInfo: audio.AudioCapturerInfo = {
  source: audio.SourceType.SOURCE_TYPE_MIC,
  capturerFlags: 0
}

let audioCapturerOptions: audio.AudioCapturerOptions = {
  streamInfo: audioStreamInfo,
  capturerInfo: audioCapturerInfo
}

audio.createAudioCapturer(audioCapturerOptions, (err, data) => {
  if (err) {
    console.error(`AudioCapturer Created : Error: ${err}`);
  } else {
    console.info('AudioCapturer Created : Success : SUCCESS');
    let audioCapturer = data;
  }
});
```

## audio.createAudioCapturer<sup>8+</sup>

createAudioCapturer(options: AudioCapturerOptions): Promise<AudioCapturer\>

获取音频采集器。使用Promise 方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**需要权限：** ohos.permission.MICROPHONE

仅设置Mic音频源（即[SourceType](#sourcetype8)为SOURCE_TYPE_MIC）时需要该权限。

**参数：**

| 参数名  | 类型                                           | 必填 | 说明             |
| :------ | :--------------------------------------------- | :--- | :--------------- |
| options | [AudioCapturerOptions](#audiocaptureroptions8) | 是   | 配置音频采集器。 |

**返回值：**

| 类型                                      | 说明           |
| ----------------------------------------- | -------------- |
| Promise<[AudioCapturer](#audiocapturer8)> | Promise对象，返回音频采集器对象。 |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';

let audioStreamInfo: audio.AudioStreamInfo = {
  samplingRate: audio.AudioSamplingRate.SAMPLE_RATE_44100,
  channels: audio.AudioChannel.CHANNEL_2,
  sampleFormat: audio.AudioSampleFormat.SAMPLE_FORMAT_S16LE,
  encodingType: audio.AudioEncodingType.ENCODING_TYPE_RAW
}

let audioCapturerInfo: audio.AudioCapturerInfo = {
  source: audio.SourceType.SOURCE_TYPE_MIC,
  capturerFlags: 0
}

let audioCapturerOptions:audio.AudioCapturerOptions = {
  streamInfo: audioStreamInfo,
  capturerInfo: audioCapturerInfo
}

let audioCapturer: audio.AudioCapturer;
audio.createAudioCapturer(audioCapturerOptions).then((data) => {
  audioCapturer = data;
  console.info('AudioCapturer Created : Success : Stream Type: SUCCESS');
}).catch((err: BusinessError) => {
  console.error(`AudioCapturer Created : ERROR : ${err}`);
});
```

## AudioVolumeType

枚举，音频流类型。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

| 名称                         | 值      | 说明       |
| ---------------------------- | ------ | ---------- |
| VOICE_CALL<sup>8+</sup>      | 0      | 语音电话。 |
| RINGTONE                     | 2      | 铃声。     |
| MEDIA                        | 3      | 媒体。     |
| ALARM<sup>10+</sup>          | 4      | 闹钟。     |
| ACCESSIBILITY<sup>10+</sup>  | 5      | 无障碍。   |
| VOICE_ASSISTANT<sup>8+</sup> | 9      | 语音助手。 |

## InterruptMode<sup>9+</sup>

枚举，焦点模型。

**系统能力：** SystemCapability.Multimedia.Audio.Interrupt

| 名称                         | 值      | 说明       |
| ---------------------------- | ------ | ---------- |
| SHARE_MODE                   | 0      | 共享焦点模式。 |
| INDEPENDENT_MODE             | 1      | 独立焦点模式。 |

## DeviceFlag

枚举，可获取的设备种类。

**系统能力：** SystemCapability.Multimedia.Audio.Device

| 名称                            |  值     | 说明                        |
| ------------------------------- | ------ |---------------------------|
| OUTPUT_DEVICES_FLAG             | 1      | 输出设备。                     |
| INPUT_DEVICES_FLAG              | 2      | 输入设备。                     |
| ALL_DEVICES_FLAG                | 3      | 所有设备。                     |

## DeviceRole

枚举，设备角色。

**系统能力：** SystemCapability.Multimedia.Audio.Device

| 名称          |  值    | 说明           |
| ------------- | ------ | -------------- |
| INPUT_DEVICE  | 1      | 输入设备角色。 |
| OUTPUT_DEVICE | 2      | 输出设备角色。 |

## DeviceType

枚举，设备类型。

**系统能力：** SystemCapability.Multimedia.Audio.Device

| 名称                 | 值     | 说明                                                      |
| ---------------------| ------ | --------------------------------------------------------- |
| INVALID              | 0      | 无效设备。                                                |
| EARPIECE             | 1      | 听筒。                                                    |
| SPEAKER              | 2      | 扬声器。                                                  |
| WIRED_HEADSET        | 3      | 有线耳机，带麦克风。                                      |
| WIRED_HEADPHONES     | 4      | 有线耳机，无麦克风。                                      |
| BLUETOOTH_SCO        | 7      | 蓝牙设备SCO（Synchronous Connection Oriented）连接。      |
| BLUETOOTH_A2DP       | 8      | 蓝牙设备A2DP（Advanced Audio Distribution Profile）连接。 |
| MIC                  | 15     | 麦克风。                                                  |
| USB_HEADSET          | 22     | USB耳机，带麦克风。                                       |
| DEFAULT<sup>9+</sup> | 1000   | 默认设备类型。                                            |

## CommunicationDeviceType<sup>9+</sup>

枚举，用于通信的可用设备类型。

**系统能力：** SystemCapability.Multimedia.Audio.Communication

| 名称          | 值     | 说明          |
| ------------- | ------ | -------------|
| SPEAKER       | 2      | 扬声器。      |

## AudioRingMode

枚举，铃声模式。

**系统能力：** SystemCapability.Multimedia.Audio.Communication

| 名称                |  值    | 说明       |
| ------------------- | ------ | ---------- |
| RINGER_MODE_SILENT  | 0      | 静音模式。 |
| RINGER_MODE_VIBRATE | 1      | 震动模式。 |
| RINGER_MODE_NORMAL  | 2      | 响铃模式。 |

## AudioSampleFormat<sup>8+</sup>

枚举，音频采样格式。

**系统能力：** SystemCapability.Multimedia.Audio.Core

| 名称                                |  值    | 说明                       |
| ---------------------------------- | ------ | -------------------------- |
| SAMPLE_FORMAT_INVALID              | -1     | 无效格式。                 |
| SAMPLE_FORMAT_U8                   | 0      | 无符号8位整数。            |
| SAMPLE_FORMAT_S16LE                | 1      | 带符号的16位整数，小尾数。 |
| SAMPLE_FORMAT_S24LE                | 2      | 带符号的24位整数，小尾数。 <br>由于系统限制，该采样格式仅部分设备支持，请根据实际情况使用。|
| SAMPLE_FORMAT_S32LE                | 3      | 带符号的32位整数，小尾数。 <br>由于系统限制，该采样格式仅部分设备支持，请根据实际情况使用。|
| SAMPLE_FORMAT_F32LE<sup>9+</sup>   | 4      | 带符号的32位浮点数，小尾数。 <br>由于系统限制，该采样格式仅部分设备支持，请根据实际情况使用。|

## AudioErrors<sup>9+</sup>

枚举，音频错误码。

**系统能力：** SystemCapability.Multimedia.Audio.Core

| 名称                 | 值      | 说明         |
| ---------------------| --------| ----------------- |
| ERROR_INVALID_PARAM  | 6800101 | 无效入参。         |
| ERROR_NO_MEMORY      | 6800102 | 分配内存失败。     |
| ERROR_ILLEGAL_STATE  | 6800103 | 状态不支持。       |
| ERROR_UNSUPPORTED    | 6800104 | 参数选项不支持。    |
| ERROR_TIMEOUT        | 6800105 | 处理超时。         |
| ERROR_STREAM_LIMIT   | 6800201 | 音频流数量达到限制。|
| ERROR_SYSTEM         | 6800301 | 系统处理异常。     |

## AudioChannel<sup>8+</sup>

枚举， 音频声道。

**系统能力：** SystemCapability.Multimedia.Audio.Core

| 名称      |  值       | 说明   |
| --------- | -------- |------|
| CHANNEL_1 | 0x1 << 0 | 单声道。 |
| CHANNEL_2 | 0x1 << 1 | 双声道。 |
| CHANNEL_3<sup>11+</sup> | 3 | 三声道。 |
| CHANNEL_4<sup>11+</sup> | 4 | 四声道。 |
| CHANNEL_5<sup>11+</sup> | 5 | 五声道。 |
| CHANNEL_6<sup>11+</sup> | 6 | 六声道。 |
| CHANNEL_7<sup>11+</sup> | 7 | 七声道。 |
| CHANNEL_8<sup>11+</sup> | 8 | 八声道。 |
| CHANNEL_9<sup>11+</sup> | 9 | 九声道。 |
| CHANNEL_10<sup>11+</sup> | 10 | 十声道。 |
| CHANNEL_12<sup>11+</sup> | 12 | 十二声道。 |
| CHANNEL_14<sup>11+</sup> | 14 | 十四声道。 |
| CHANNEL_16<sup>11+</sup> | 16 | 十六声道。 |

## AudioSamplingRate<sup>8+</sup>

枚举，音频采样率，具体设备支持的采样率规格会存在差异。

**系统能力：** SystemCapability.Multimedia.Audio.Core

| 名称              |  值    | 说明            |
| ----------------- | ------ | --------------- |
| SAMPLE_RATE_8000  | 8000   | 采样率为8000。  |
| SAMPLE_RATE_11025 | 11025  | 采样率为11025。 |
| SAMPLE_RATE_12000 | 12000  | 采样率为12000。 |
| SAMPLE_RATE_16000 | 16000  | 采样率为16000。 |
| SAMPLE_RATE_22050 | 22050  | 采样率为22050。 |
| SAMPLE_RATE_24000 | 24000  | 采样率为24000。 |
| SAMPLE_RATE_32000 | 32000  | 采样率为32000。 |
| SAMPLE_RATE_44100 | 44100  | 采样率为44100。 |
| SAMPLE_RATE_48000 | 48000  | 采样率为48000。 |
| SAMPLE_RATE_64000 | 64000  | 采样率为64000。 |
| SAMPLE_RATE_96000 | 96000  | 采样率为96000。 |

## AudioEncodingType<sup>8+</sup>

枚举，音频编码类型。

**系统能力：** SystemCapability.Multimedia.Audio.Core

| 名称                  |  值    | 说明      |
| --------------------- | ------ | --------- |
| ENCODING_TYPE_INVALID | -1     | 无效。    |
| ENCODING_TYPE_RAW     | 0      | PCM编码。 |

## AudioChannelLayout<sup>11+</sup>

枚举，音频文件声道布局类型。

**系统能力：** SystemCapability.Multimedia.Audio.Core

| 名称                            |  值              | 说明                                          |
| ------------------------------ | ---------------- | --------------------------------------------- |
| CH_LAYOUT_UNKNOWN              | 0x0              | 未知声道布局。                                 |
| CH_LAYOUT_MONO                 | 0x4              | 声道布局为MONO。                               |
| CH_LAYOUT_STEREO               | 0x3              | 声道布局为STEREO。                             |
| CH_LAYOUT_STEREO_DOWNMIX       | 0x60000000       | 声道布局为STEREO-DOWNMIX。                     |
| CH_LAYOUT_2POINT1              | 0xB              | 声道布局为2.1。                                |
| CH_LAYOUT_3POINT0              | 0x103            | 声道布局为3.0。                                |
| CH_LAYOUT_SURROUND             | 0x7              | 声道布局为SURROUND。                           |
| CH_LAYOUT_3POINT1              | 0xF              | 声道布局为3.1。                                |
| CH_LAYOUT_4POINT0              | 0x107            | 声道布局为4.0。                                |
| CH_LAYOUT_QUAD                 | 0x33             | 声道布局为QUAD。                               |
| CH_LAYOUT_QUAD_SIDE            | 0x603            | 声道布局为QUAD-SIDE。                          |
| CH_LAYOUT_2POINT0POINT2        | 0x3000000003     | 声道布局为2.0.2。                              |
| CH_LAYOUT_AMB_ORDER1_ACN_N3D   | 0x100000000001   | 声道排序为ACN_N3D（根据ITU标准）的一阶FOA文件。  |
| CH_LAYOUT_AMB_ORDER1_ACN_SN3D  | 0x100000001001   | 声道排序为ACN_SN3D（根据ITU标准）的一阶FOA文件。 |
| CH_LAYOUT_AMB_ORDER1_FUMA      | 0x100000000101   | 声道排序为FUMA（根据ITU标准）的一阶FOA文件。     |
| CH_LAYOUT_4POINT1              | 0x10F            | 声道布局为4.1                                  |
| CH_LAYOUT_5POINT0              | 0x607            | 声道布局为5.0。                                |
| CH_LAYOUT_5POINT0_BACK         | 0x37             | 声道布局为5.0-BACK。                           |
| CH_LAYOUT_2POINT1POINT2        | 0x300000000B     | 声道布局为2.1.2。                              |
| CH_LAYOUT_3POINT0POINT2        | 0x3000000007     | 声道布局为3.0.2。                              |
| CH_LAYOUT_5POINT1              | 0x60F            | 声道布局为5.1。                                |
| CH_LAYOUT_5POINT1_BACK         | 0x3F             | 声道布局为5.1-BACK。                           |
| CH_LAYOUT_6POINT0              | 0x707            | 声道布局为6.0。                                |
| CH_LAYOUT_HEXAGONAL            | 0x137            | 声道布局为HEXAGONAL。                          |
| CH_LAYOUT_3POINT1POINT2        | 0x500F           | 声道布局为3.1.2。                              |
| CH_LAYOUT_6POINT0_FRONT        | 0x6C3            | 声道布局为6.0-FRONT。                          |
| CH_LAYOUT_6POINT1              | 0x70F            | 声道布局为6.1。                                |
| CH_LAYOUT_6POINT1_BACK         | 0x13F            | 声道布局为6.1-BACK。                           |
| CH_LAYOUT_6POINT1_FRONT        | 0x6CB            | 声道布局为6.1-FRONT。                          |
| CH_LAYOUT_7POINT0              | 0x637            | 声道布局为7.0。                                |
| CH_LAYOUT_7POINT0_FRONT        | 0x6C7            | 声道布局为7.0-FRONT。                          |
| CH_LAYOUT_7POINT1              | 0x63F            | 声道布局为7.1。                                |
| CH_LAYOUT_OCTAGONAL            | 0x737            | 声道布局为OCTAGONAL。                          |
| CH_LAYOUT_5POINT1POINT2        | 0x300000060F     | 声道布局为5.1.2。                              |
| CH_LAYOUT_7POINT1_WIDE         | 0x6CF            | 声道布局为7.1-WIDE。                           |
| CH_LAYOUT_7POINT1_WIDE_BACK    | 0xFF             | 声道布局为7.1-WIDE-BACK。                      |
| CH_LAYOUT_AMB_ORDER2_ACN_N3D   | 0x100000000002   | 声道排序为ACN_N3D（根据ITU标准）的二阶HOA文件。  |
| CH_LAYOUT_AMB_ORDER2_ACN_SN3D  | 0x100000001002   | 声道排序为ACN_SN3D（根据ITU标准）的二阶HOA文件。 |
| CH_LAYOUT_AMB_ORDER2_FUMA      | 0x100000000102   | 声道排序为FUMA（根据ITU标准）的二阶HOA文件。     |
| CH_LAYOUT_5POINT1POINT4        | 0x2D60F          | 声道布局为5.1.4。                              |
| CH_LAYOUT_7POINT1POINT2        | 0x300000063F     | 声道布局为7.1.2。                              |
| CH_LAYOUT_7POINT1POINT4        | 0x2D63F          | 声道布局为7.1.4。                              |
| CH_LAYOUT_10POINT2             | 0x180005737      | 声道布局为10.2。                               |
| CH_LAYOUT_9POINT1POINT4        | 0x18002D63F      | 声道布局为9.1.4。                              |
| CH_LAYOUT_9POINT1POINT6        | 0x318002D63F     | 声道布局为9.1.6。                              |
| CH_LAYOUT_HEXADECAGONAL        | 0x18003F737      | 声道布局为HEXADECAGONAL。                      |
| CH_LAYOUT_AMB_ORDER3_ACN_N3D   | 0x100000000003   | 声道排序为ACN_N3D（根据ITU标准）的三阶HOA文件。  |
| CH_LAYOUT_AMB_ORDER3_ACN_SN3D  | 0x100000001003   | 声道排序为ACN_SN3D（根据ITU标准）的三阶HOA文件。 |
| CH_LAYOUT_AMB_ORDER3_FUMA      | 0x100000000103   | 声道排序为FUMA（根据ITU标准）的三阶HOA文件。     |

## ContentType<sup>(deprecated)</sup>

枚举，音频内容类型。

> **说明：**
> 从 API version 7 开始支持，从 API version 10 开始废弃。建议使用[StreamUsage](#streamusage)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Core

| 名称                               |  值    | 说明       |
| ---------------------------------- | ------ | ---------- |
| CONTENT_TYPE_UNKNOWN               | 0      | 未知类型。 |
| CONTENT_TYPE_SPEECH                | 1      | 语音。     |
| CONTENT_TYPE_MUSIC                 | 2      | 音乐。     |
| CONTENT_TYPE_MOVIE                 | 3      | 电影。     |
| CONTENT_TYPE_SONIFICATION          | 4      | 通知音。   |
| CONTENT_TYPE_RINGTONE<sup>8+</sup> | 5      | 铃声。     |

## StreamUsage

枚举，音频流使用类型。

**系统能力：** SystemCapability.Multimedia.Audio.Core

| 名称                                      |  值    | 说明                                                                                                                                          |
| ------------------------------------------| ------ |---------------------------------------------------------------------------------------------------------------------------------------------|
| STREAM_USAGE_UNKNOWN                      | 0      | 未知类型。                                                                                                                                       |
| STREAM_USAGE_MEDIA<sup>(deprecated)</sup>                        | 1      | 媒体。<br/> 从API version 7开始支持，从API version 10 开始废弃。建议使用该枚举中的STREAM_USAGE_MUSIC、STREAM_USAGE_MOVIE、STREAM_USAGE_GAME或STREAM_USAGE_AUDIOBOOK替代。 |
| STREAM_USAGE_MUSIC<sup>10+</sup>          | 1      | 音乐。                                                                                                                                         |
| STREAM_USAGE_VOICE_COMMUNICATION          | 2      | 语音通信。                                                                                                                                       | 
| STREAM_USAGE_VOICE_ASSISTANT<sup>9+</sup> | 3      | 语音播报。                                                                                                                                       |
| STREAM_USAGE_ALARM<sup>10+</sup>          | 4      | 闹钟。                                                                                                                                         |
| STREAM_USAGE_VOICE_MESSAGE<sup>10+</sup>  | 5      | 语音消息。                                                                                                                                       |
| STREAM_USAGE_NOTIFICATION_RINGTONE<sup>(deprecated)</sup>        | 6      | 通知铃声。<br/> 从 API version 10 开始废弃。建议使用该枚举中的STREAM_USAGE_RINGTONE替代。                                                                          |
| STREAM_USAGE_RINGTONE<sup>10+</sup>       | 6      | 铃声。                                                                                                                                         |
| STREAM_USAGE_NOTIFICATION<sup>10+</sup>   | 7      | 通知。                                                                                                                                         |
| STREAM_USAGE_ACCESSIBILITY<sup>10+</sup>  | 8      | 无障碍。                                                                                                                                        |
| STREAM_USAGE_MOVIE<sup>10+</sup>          | 10     | 电影或视频。                                                                                                                                      |
| STREAM_USAGE_GAME<sup>10+</sup>           | 11     | 游戏音效。                                                                                                                                       |
| STREAM_USAGE_AUDIOBOOK<sup>10+</sup>      | 12     | 有声读物。                                                                                                                                       |
| STREAM_USAGE_NAVIGATION<sup>10+</sup>     | 13     | 导航。                                                                                                                                         |

## AudioState<sup>8+</sup>

枚举，音频状态。

**系统能力：** SystemCapability.Multimedia.Audio.Core

| 名称           | 值     | 说明             |
| -------------- | ------ | ---------------- |
| STATE_INVALID  | -1     | 无效状态。       |
| STATE_NEW      | 0      | 创建新实例状态。 |
| STATE_PREPARED | 1      | 准备状态。       |
| STATE_RUNNING  | 2      | 运行状态。 |
| STATE_STOPPED  | 3      | 停止状态。       |
| STATE_RELEASED | 4      | 释放状态。       |
| STATE_PAUSED   | 5      | 暂停状态。       |

## AudioEffectMode<sup>10+</sup>

枚举，音效模式。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

| 名称               | 值     | 说明       |
| ------------------ | ------ | ---------- |
| EFFECT_NONE        | 0      | 关闭音效。 |
| EFFECT_DEFAULT     | 1      | 默认音效。 |

## AudioRendererRate<sup>8+</sup>

枚举，音频渲染速度。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

| 名称               | 值     | 说明       |
| ------------------ | ------ | ---------- |
| RENDER_RATE_NORMAL | 0      | 正常速度。 |
| RENDER_RATE_DOUBLE | 1      | 2倍速。    |
| RENDER_RATE_HALF   | 2      | 0.5倍数。  |

## InterruptType

枚举，中断类型。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

| 名称                 |  值     | 说明                   |
| -------------------- | ------ | ---------------------- |
| INTERRUPT_TYPE_BEGIN | 1      | 音频播放中断事件开始。 |
| INTERRUPT_TYPE_END   | 2      | 音频播放中断事件结束。 |

## InterruptForceType<sup>9+</sup>

枚举，强制打断类型。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

| 名称            |  值    | 说明                                 |
| --------------- | ------ | ------------------------------------ |
| INTERRUPT_FORCE | 0      | 由系统进行操作，强制打断音频播放。   |
| INTERRUPT_SHARE | 1      | 由应用进行操作，可以选择打断或忽略。 |

## InterruptHint

枚举，中断提示。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

| 名称                               |  值     | 说明                                         |
| ---------------------------------- | ------ | -------------------------------------------- |
| INTERRUPT_HINT_NONE<sup>8+</sup>   | 0      | 无提示。                                     |
| INTERRUPT_HINT_RESUME              | 1      | 提示音频恢复。                               |
| INTERRUPT_HINT_PAUSE               | 2      | 提示音频暂停。                               |
| INTERRUPT_HINT_STOP                | 3      | 提示音频停止。                               |
| INTERRUPT_HINT_DUCK                | 4      | 提示音频躲避。（躲避：音量减弱，而不会停止） |
| INTERRUPT_HINT_UNDUCK<sup>8+</sup> | 5      | 提示音量恢复。                               |

## AudioStreamInfo<sup>8+</sup>

音频流信息。

**系统能力：** SystemCapability.Multimedia.Audio.Core

| 名称         | 类型                                               | 必填 | 说明               |
| ------------ | ------------------------------------------------- | ---- | ------------------ |
| samplingRate | [AudioSamplingRate](#audiosamplingrate8)          | 是   | 音频文件的采样率。 |
| channels     | [AudioChannel](#audiochannel8)                    | 是   | 音频文件的通道数。 |
| sampleFormat | [AudioSampleFormat](#audiosampleformat8)          | 是   | 音频采样格式。     |
| encodingType | [AudioEncodingType](#audioencodingtype8)          | 是   | 音频编码格式。     |
| channelLayout<sup>11+</sup> | [AudioChannelLayout](#audiochannellayout11)  | 否   | 音频声道布局。     |

## AudioRendererInfo<sup>8+</sup>

音频渲染器信息。

**系统能力：** SystemCapability.Multimedia.Audio.Core

| 名称          | 类型                        | 必填  | 说明             |
| ------------- | --------------------------- | ---- | ---------------- |
| content       | [ContentType](#contenttypedeprecated) | 否   | 音频内容类型。<br>API version 8、9为必填参数，从API version 10开始，变更为可选参数。 |
| usage         | [StreamUsage](#streamusage) | 是   | 音频流使用类型。 |
| rendererFlags | number                      | 是   | 音频渲染器标志。<br>0代表普通音频渲染器，1代表低时延音频渲染器。ArkTS接口暂不支持低时延音频渲染器。 |

## AudioRendererOptions<sup>8+</sup>

音频渲染器选项信息。

| 名称         | 类型                                     | 必填  | 说明             |
| ------------ | ---------------------------------------- | ---- | ---------------- |
| streamInfo   | [AudioStreamInfo](#audiostreaminfo8)     | 是   | 表示音频流信息。<br/>**系统能力：** SystemCapability.Multimedia.Audio.Renderer |
| rendererInfo | [AudioRendererInfo](#audiorendererinfo8) | 是   | 表示渲染器信息。<br/>**系统能力：** SystemCapability.Multimedia.Audio.Renderer |
| privacyType<sup>10+</sup> | [AudioPrivacyType](#audioprivacytype10) | 否 | 表示音频流是否可以被其他应用录制，默认值为0。<br/>**系统能力：** SystemCapability.Multimedia.Audio.PlaybackCapture |

## AudioPrivacyType<sup>10+</sup>

枚举类型，用于标识对应播放音频流是否支持被其他应用录制。

**系统能力：** SystemCapability.Multimedia.Audio.PlaybackCapture

| 名称                 | 值   | 说明                             |
| -------------------- | ---- | -------------------------------- |
| PRIVACY_TYPE_PUBLIC  | 0    | 表示音频流可以被其他应用录制。   |
| PRIVACY_TYPE_PRIVATE | 1    | 表示音频流不可以被其他应用录制。 |

## InterruptEvent<sup>9+</sup>

播放中断时，应用接收的中断事件。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

| 名称      | 类型                                       |必填   | 说明                                 |
| --------- | ------------------------------------------ | ---- | ------------------------------------ |
| eventType | [InterruptType](#interrupttype)            | 是   | 中断事件类型，开始或是结束。         |
| forceType | [InterruptForceType](#interruptforcetype9) | 是   | 操作是由系统执行或是由应用程序执行。 |
| hintType  | [InterruptHint](#interrupthint)            | 是   | 中断提示。                           |

## VolumeEvent<sup>9+</sup>

音量改变时，应用接收的事件。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

| 名称       | 类型                                | 必填   | 说明                                        |
| ---------- | ----------------------------------- | ---- |-------------------------------------------|
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。                                    |
| volume     | number                              | 是   | 音量等级，可设置范围通过getMinVolume和getMaxVolume获取。  |
| updateUi   | boolean                             | 是   | 在UI中显示音量变化，true为显示，false为不显示。             |

## MicStateChangeEvent<sup>9+</sup>

麦克风状态变化时，应用接收的事件。

**系统能力：** SystemCapability.Multimedia.Audio.Device

| 名称       | 类型                                | 必填 | 说明                                                     |
| ---------- | ----------------------------------- | ---- |-------------------------------------------------------- |
| mute | boolean | 是   | 回调返回系统麦克风静音状态，true为静音，false为非静音。          |

## DeviceChangeAction

描述设备连接状态变化和设备信息。

**系统能力：** SystemCapability.Multimedia.Audio.Device

| 名称              | 类型                                              | 必填 | 说明               |
| :---------------- | :------------------------------------------------ | :--- | :----------------- |
| type              | [DeviceChangeType](#devicechangetype)             | 是   | 设备连接状态变化。 |
| deviceDescriptors | [AudioDeviceDescriptors](#audiodevicedescriptors) | 是   | 设备信息。         |

## ChannelBlendMode<sup>11+</sup>

枚举，声道混合模式类型。

**系统能力：** SystemCapability.Multimedia.Audio.Core

| 名称                                         |  值     | 说明                   |
| :------------------------------------------- | :----- | :--------------------- |
| MODE_DEFAULT | 0     | 无声道混合。  |
| MODE_BLEND_LR | 1      | 混合左右声道。 |
| MODE_ALL_LEFT | 2      | 从左声道拷贝覆盖到右声道混合。  |
| MODE_ALL_RIGHT | 3 | 从右声道拷贝覆盖到左声道混合。 |

## AudioStreamDeviceChangeReason<sup>11+</sup>

枚举，流设备变更原因。

**系统能力：** SystemCapability.Multimedia.Audio.Device

| 名称                                        |  值     | 说明              |
|:------------------------------------------| :----- |:----------------|
| REASON_UNKNOWN | 0 | 未知原因。           |
| REASON_NEW_DEVICE_AVAILABLE | 1 | 新设备可用。         |
| REASON_OLD_DEVICE_UNAVAILABLE | 2 | 旧设备不可用。当报告此原因时，应用程序应考虑暂停音频播放。 |
| REASON_OVERRODE | 3 | 强选。 |

## AudioStreamDeviceChangeInfo<sup>11+</sup>

流设备变更时，应用接收的事件。

**系统能力：** SystemCapability.Multimedia.Audio.Device

| 名称              | 类型                                                                | 必填 | 说明               |
| :---------------- |:------------------------------------------------------------------| :--- | :----------------- |
| devices              | [AudioDeviceDescriptors](#audiodevicedescriptors)                 | 是   | 设备信息。 |
| changeReason | [AudioStreamDeviceChangeReason](#audiostreamdevicechangereason11) | 是   | 流设备变更原因。 |

## DeviceChangeType

枚举，设备连接状态变化。

**系统能力：** SystemCapability.Multimedia.Audio.Device

| 名称       | 值   | 说明           |
| :--------- | :--- | :------------- |
| CONNECT    | 0    | 设备连接。     |
| DISCONNECT | 1    | 断开设备连接。 |

## AudioCapturerOptions<sup>8+</sup>

音频采集器选项信息。

| 名称                                | 类型                                                      | 必填 | 说明                                                         |
| ----------------------------------- | --------------------------------------------------------- | ---- | ------------------------------------------------------------ |
| streamInfo                          | [AudioStreamInfo](#audiostreaminfo8)                      | 是   | 表示音频流信息。 <br/>**系统能力：** SystemCapability.Multimedia.Audio.Capturer   |
| capturerInfo                        | [AudioCapturerInfo](#audiocapturerinfo8)                   | 是   | 表示采集器信息。 <br/>**系统能力：** SystemCapability.Multimedia.Audio.Capturer        |
| playbackCaptureConfig<sup>10+</sup> | [AudioPlaybackCaptureConfig](#audioplaybackcaptureconfig10) | 否   | 音频内录的配置信息。<br/>**系统能力：** SystemCapability.Multimedia.Audio.PlaybackCapture |

## AudioCapturerInfo<sup>8+</sup>

描述音频采集器信息。

**系统能力：** SystemCapability.Multimedia.Audio.Core

| 名称          | 类型                      | 必填 | 说明             |
| :------------ | :------------------------ | :--- | :--------------- |
| source        | [SourceType](#sourcetype8) | 是   | 音源类型。       |
| capturerFlags | number                    | 是   | 音频采集器标志。<br>0代表普通音频采集器，1代表低时延音频采集器。ArkTS接口暂不支持低时延音频采集器。 |

## SourceType<sup>8+</sup>

枚举，音源类型。

| 名称                                         |  值     | 说明                   |
| :------------------------------------------- | :----- | :--------------------- |
| SOURCE_TYPE_INVALID                          | -1     | 无效的音频源。<br/>**系统能力：** SystemCapability.Multimedia.Audio.Core  |
| SOURCE_TYPE_MIC                              | 0      | Mic音频源。<br/>**系统能力：** SystemCapability.Multimedia.Audio.Core |
| SOURCE_TYPE_VOICE_RECOGNITION<sup>9+</sup>   | 1      | 语音识别源。<br/>**系统能力：** SystemCapability.Multimedia.Audio.Core  |
| SOURCE_TYPE_PLAYBACK_CAPTURE<sup>10+</sup>   | 2 | 播放音频流（内录）录制音频源。<br/>**系统能力：** SystemCapability.Multimedia.Audio.PlaybackCapture |
| SOURCE_TYPE_VOICE_COMMUNICATION              | 7      | 语音通话场景的音频源。<br/>**系统能力：** SystemCapability.Multimedia.Audio.Core |

## AudioPlaybackCaptureConfig<sup>10+</sup>

播放音频流录制（内录）的配置信息。

**系统能力：** SystemCapability.Multimedia.Audio.PlaybackCapture

| 名称          | 类型                                          | 必填 | 说明                             |
| ------------- | --------------------------------------------- | ---- | -------------------------------- |
| filterOptions | [CaptureFilterOptions](#capturefilteroptions10) | 是   | 需要录制的播放音频流的筛选信息。 |

## CaptureFilterOptions<sup>10+</sup>

待录制的播放音频流的筛选信息。

**需要权限：**

- 在API version 10时，CaptureFilterOptions支持使用StreamUsage.STREAM_USAGE_VOICE_COMMUNICATION，使用时需要申请权限ohos.permission.CAPTURE_VOICE_DOWNLINK_AUDIO，该权限仅系统应用可申请。

- 从API version 11开始，CaptureFilterOptions不再支持使用StreamUsage.STREAM_USAGE_VOICE_COMMUNICATION，所以当前接口不再涉及此权限。

**系统能力：** SystemCapability.Multimedia.Audio.PlaybackCapture

| 名称   | 类型                               | 必填 | 说明                                                         |
| ------ | ---------------------------------- | ---- | ------------------------------------------------------------ |
| usages | Array<[StreamUsage](#streamusage)> | 是   | 指定需要录制的音频播放流的StreamUsage类型。可同时指定0个或多个StreamUsage。Array为空时，默认录制StreamUsage为STREAM_USAGE_MUSIC、STREAM_USAGE_MOVIE、STREAM_USAGE_GAME和STREAM_USAGE_AUDIOBOOK的音频播放流。 |

## AudioScene<sup>8+</sup>

枚举，音频场景。

**系统能力：** SystemCapability.Multimedia.Audio.Communication

| 名称                   |  值     | 说明                                          |
| :--------------------- | :----- | :-------------------------------------------- |
| AUDIO_SCENE_DEFAULT    | 0      | 默认音频场景。                                |
| AUDIO_SCENE_VOICE_CHAT | 3      | 语音聊天模式。                                |

## AudioManager

管理音频音量和音频设备。在调用AudioManager的接口前，需要先通过[getAudioManager](#audiogetaudiomanager)创建实例。

### setAudioParameter<sup>(deprecated)</sup>

setAudioParameter(key: string, value: string, callback: AsyncCallback&lt;void&gt;): void

音频参数设置，使用callback方式异步返回结果。

接口用于为根据硬件设备支持能力扩展音频配置。支持的参数与产品、设备强相关，非通用参数，示例代码内使用样例参数。

> **说明：**
> 从 API version 7 开始支持，从 API version 11 开始废弃。替代接口仅面向系统应用开放。

**需要权限：** ohos.permission.MODIFY_AUDIO_SETTINGS

**系统能力：** SystemCapability.Multimedia.Audio.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明                     |
| -------- | ------------------------- | ---- | ------------------------ |
| key      | string                    | 是   | 被设置的音频参数的键。   |
| value    | string                    | 是   | 被设置的音频参数的值。   |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。当音频参数设置成功，err为undefined，否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioManager.setAudioParameter('key_example', 'value_example', (err: BusinessError) => {
  if (err) {
    console.error(`Failed to set the audio parameter. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate a successful setting of the audio parameter.');
});
```

### setAudioParameter<sup>(deprecated)</sup>

setAudioParameter(key: string, value: string): Promise&lt;void&gt;

音频参数设置，使用Promise方式异步返回结果。

接口用于为根据硬件设备支持能力扩展音频配置。支持的参数与产品、设备强相关，非通用参数，示例代码内使用样例参数。

> **说明：**
> 从 API version 7 开始支持，从 API version 11 开始废弃。替代接口仅面向系统应用开放。

**需要权限：** ohos.permission.MODIFY_AUDIO_SETTINGS

**系统能力：** SystemCapability.Multimedia.Audio.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明                   |
| ------ | ------ | ---- | ---------------------- |
| key    | string | 是   | 被设置的音频参数的键。 |
| value  | string | 是   | 被设置的音频参数的值。 |

**返回值：**

| 类型                | 说明                            |
| ------------------- | ------------------------------- |
| Promise&lt;void&gt; | Promise对象，无返回结果。 |

**示例：**

```ts
audioManager.setAudioParameter('key_example', 'value_example').then(() => {
  console.info('Promise returned to indicate a successful setting of the audio parameter.');
});
```

### getAudioParameter<sup>(deprecated)</sup>

getAudioParameter(key: string, callback: AsyncCallback&lt;string&gt;): void

获取指定音频参数值，使用callback方式异步返回结果。

本接口的使用场景为根据硬件设备支持能力扩展音频配置。在不同的设备平台上，所支持的音频参数会存在差异。示例代码内使用样例参数，实际支持的音频配置参数见具体设备平台的资料描述。

> **说明：**
> 从 API version 7 开始支持，从 API version 11 开始废弃。替代接口仅面向系统应用开放。

**系统能力：** SystemCapability.Multimedia.Audio.Core

**参数：**

| 参数名   | 类型                        | 必填 | 说明                         |
| -------- | --------------------------- | ---- | ---------------------------- |
| key      | string                      | 是   | 待获取的音频参数的键。       |
| callback | AsyncCallback&lt;string&gt; | 是   | 回调函数。当获取指定音频参数值成功，err为undefined，data为获取到的指定音频参数值；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioManager.getAudioParameter('key_example', (err: BusinessError, value: string) => {
  if (err) {
    console.error(`Failed to obtain the value of the audio parameter. ${err}`);
    return;
  }
  console.info(`Callback invoked to indicate that the value of the audio parameter is obtained ${value}.`);
});
```

### getAudioParameter<sup>(deprecated)</sup>

getAudioParameter(key: string): Promise&lt;string&gt;

获取指定音频参数值，使用Promise方式异步返回结果。

本接口的使用场景为根据硬件设备支持能力扩展音频配置。在不同的设备平台上，所支持的音频参数会存在差异。示例代码内使用样例参数，实际支持的音频配置参数见具体设备平台的资料描述。

> **说明：**
> 从 API version 7 开始支持，从 API version 11 开始废弃。替代接口仅面向系统应用开放。

**系统能力：** SystemCapability.Multimedia.Audio.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明                   |
| ------ | ------ | ---- | ---------------------- |
| key    | string | 是   | 待获取的音频参数的键。 |

**返回值：**

| 类型                  | 说明                                |
| --------------------- | ----------------------------------- |
| Promise&lt;string&gt; | Promise对象，返回获取的音频参数的值。 |

**示例：**

```ts
audioManager.getAudioParameter('key_example').then((value: string) => {
  console.info(`Promise returned to indicate that the value of the audio parameter is obtained ${value}.`);
});
```

### getAudioScene<sup>8+</sup>

getAudioScene\(callback: AsyncCallback<AudioScene\>\): void

获取音频场景模式，使用callback方式返回异步结果。

**系统能力：** SystemCapability.Multimedia.Audio.Communication

**参数：**

| 参数名   | 类型                                                | 必填 | 说明                         |
| :------- | :-------------------------------------------------- | :--- | :--------------------------- |
| callback | AsyncCallback<[AudioScene](#audioscene8)> | 是   | 回调函数。当获取音频场景模式成功，err为undefined，data为获取到的音频场景模式；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioManager.getAudioScene((err: BusinessError, value: audio.AudioScene) => {
  if (err) {
    console.error(`Failed to obtain the audio scene mode. ${err}`);
    return;
  }
  console.info(`Callback invoked to indicate that the audio scene mode is obtained ${value}.`);
});
```

### getAudioScene<sup>8+</sup>

getAudioScene\(\): Promise<AudioScene\>

获取音频场景模式，使用Promise方式返回异步结果。

**系统能力：** SystemCapability.Multimedia.Audio.Communication

**返回值：**

| 类型                                          | 说明                         |
| :-------------------------------------------- | :--------------------------- |
| Promise<[AudioScene](#audioscene8)> | Promise对象，返回音频场景模式。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioManager.getAudioScene().then((value: audio.AudioScene) => {
  console.info(`Promise returned to indicate that the audio scene mode is obtained ${value}.`);
}).catch ((err: BusinessError) => {
  console.error(`Failed to obtain the audio scene mode ${err}`);
});
```

### getAudioSceneSync<sup>10+</sup>

getAudioSceneSync\(\): AudioScene

获取音频场景模式，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Communication

**返回值：**

| 类型                                          | 说明                         |
| :-------------------------------------------- | :--------------------------- |
| [AudioScene](#audioscene8) | 音频场景模式。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let value: audio.AudioScene = audioManager.getAudioSceneSync();
  console.info(`indicate that the audio scene mode is obtained ${value}.`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`Failed to obtain the audio scene mode ${error}`);
}
```

### getVolumeManager<sup>9+</sup>

getVolumeManager(): AudioVolumeManager

获取音频音量管理器。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**返回值：**

| 类型                                      | 说明                          |
|-----------------------------------------| ----------------------------- |
| [AudioVolumeManager](#audiovolumemanager9) | AudioVolumeManager实例 |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

let audioVolumeManager: audio.AudioVolumeManager = audioManager.getVolumeManager();
```

### getStreamManager<sup>9+</sup>

getStreamManager(): AudioStreamManager

获取音频流管理器。

**系统能力：** SystemCapability.Multimedia.Audio.Core

**返回值：**

| 类型                                         | 说明                          |
|--------------------------------------------| ----------------------------- |
| [AudioStreamManager](#audiostreammanager9) | AudioStreamManager实例 |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

let audioStreamManager: audio.AudioStreamManager = audioManager.getStreamManager();
```

### getRoutingManager<sup>9+</sup>

getRoutingManager(): AudioRoutingManager

获取音频路由设备管理器。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**返回值：**

| 类型                                       | 说明                          |
|------------------------------------------| ----------------------------- |
| [AudioRoutingManager](#audioroutingmanager9) | AudioRoutingManager实例 |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

let audioRoutingManager: audio.AudioRoutingManager = audioManager.getRoutingManager();
```

### setVolume<sup>(deprecated)</sup>

setVolume(volumeType: AudioVolumeType, volume: number, callback: AsyncCallback&lt;void&gt;): void

设置指定流的音量，使用callback方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃。建议使用AudioVolumeGroupManager中的[setVolume](#setvolume9)替代，替代接口能力仅对系统应用开放。

**需要权限：** ohos.permission.ACCESS_NOTIFICATION_POLICY

仅设置铃声（即volumeType为AudioVolumeType.RINGTONE）在静音和非静音状态切换时需要该权限。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明                                                     |
| ---------- | ----------------------------------- | ---- | -------------------------------------------------------- |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。                                             |
| volume     | number                              | 是   | 音量等级，可设置范围通过getMinVolume和getMaxVolume获取。 |
| callback   | AsyncCallback&lt;void&gt;           | 是   | 回调函数。当设置指定流的音量成功，err为undefined，否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioManager.setVolume(audio.AudioVolumeType.MEDIA, 10, (err: BusinessError) => {
  if (err) {
    console.error(`Failed to set the volume. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate a successful volume setting.');
});
```

### setVolume<sup>(deprecated)</sup>

setVolume(volumeType: AudioVolumeType, volume: number): Promise&lt;void&gt;

设置指定流的音量，使用Promise方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃。建议使用AudioVolumeGroupManager中的[setVolume](#setvolume9)替代，替代接口能力仅对系统应用开放。

**需要权限：** ohos.permission.ACCESS_NOTIFICATION_POLICY

仅设置铃声（即volumeType为AudioVolumeType.RINGTONE）在静音和非静音状态切换时需要该权限。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明                                                     |
| ---------- | ----------------------------------- | ---- | -------------------------------------------------------- |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。                                             |
| volume     | number                              | 是   | 音量等级，可设置范围通过getMinVolume和getMaxVolume获取。 |

**返回值：**

| 类型                | 说明                          |
| ------------------- | ----------------------------- |
| Promise&lt;void&gt; | Promise对象，无返回结果。 |

**示例：**

```ts
audioManager.setVolume(audio.AudioVolumeType.MEDIA, 10).then(() => {
  console.info('Promise returned to indicate a successful volume setting.');
});
```

### getVolume<sup>(deprecated)</sup>

getVolume(volumeType: AudioVolumeType, callback: AsyncCallback&lt;number&gt;): void

获取指定流的音量，使用callback方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioVolumeGroupManager中的[getVolume](#getvolume9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明               |
| ---------- | ----------------------------------- | ---- | ------------------ |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。       |
| callback   | AsyncCallback&lt;number&gt;         | 是   | 回调函数。当获取指定流的音量成功，err为undefined，data为获取到的指定流的音量；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioManager.getVolume(audio.AudioVolumeType.MEDIA, (err: BusinessError, value: number) => {
  if (err) {
    console.error(`Failed to obtain the volume. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate that the volume is obtained.');
});
```

### getVolume<sup>(deprecated)</sup>

getVolume(volumeType: AudioVolumeType): Promise&lt;number&gt;

获取指定流的音量，使用Promise方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioVolumeGroupManager中的[getVolume](#getvolume9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明         |
| ---------- | ----------------------------------- | ---- | ------------ |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。 |

**返回值：**

| 类型                  | 说明                      |
| --------------------- | ------------------------- |
| Promise&lt;number&gt; | Promise对象，返回音量大小。 |

**示例：**

```ts
audioManager.getVolume(audio.AudioVolumeType.MEDIA).then((value: number) => {
  console.info(`Promise returned to indicate that the volume is obtained ${value} .`);
});
```

### getMinVolume<sup>(deprecated)</sup>

getMinVolume(volumeType: AudioVolumeType, callback: AsyncCallback&lt;number&gt;): void

获取指定流的最小音量，使用callback方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioVolumeGroupManager中的[getMinVolume](#getminvolume9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明               |
| ---------- | ----------------------------------- | ---- | ------------------ |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。       |
| callback   | AsyncCallback&lt;number&gt;         | 是   | 回调函数。当获取指定流的最小音量成功，err为undefined，data为获取到的指定流的最小音量；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioManager.getMinVolume(audio.AudioVolumeType.MEDIA, (err: BusinessError, value: number) => {
  if (err) {
    console.error(`Failed to obtain the minimum volume. ${err}`);
    return;
  }
  console.info(`Callback invoked to indicate that the minimum volume is obtained. ${value}`);
});
```

### getMinVolume<sup>(deprecated)</sup>

getMinVolume(volumeType: AudioVolumeType): Promise&lt;number&gt;

获取指定流的最小音量，使用Promise方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioVolumeGroupManager中的[getMinVolume](#getminvolume9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明         |
| ---------- | ----------------------------------- | ---- | ------------ |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。 |

**返回值：**

| 类型                  | 说明                      |
| --------------------- | ------------------------- |
| Promise&lt;number&gt; | Promise对象，返回最小音量。 |

**示例：**

```ts
audioManager.getMinVolume(audio.AudioVolumeType.MEDIA).then((value: number) => {
  console.info(`Promised returned to indicate that the minimum volume is obtained. ${value}`);
});
```

### getMaxVolume<sup>(deprecated)</sup>

getMaxVolume(volumeType: AudioVolumeType, callback: AsyncCallback&lt;number&gt;): void

获取指定流的最大音量，使用callback方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioVolumeGroupManager中的[getMaxVolume](#getmaxvolume9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明                   |
| ---------- | ----------------------------------- | ---- | ---------------------- |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。           |
| callback   | AsyncCallback&lt;number&gt;         | 是   | 回调函数。当获取指定流的最大音量成功，err为undefined，data为获取到的指定流的最大音量；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioManager.getMaxVolume(audio.AudioVolumeType.MEDIA, (err: BusinessError, value: number) => {
  if (err) {
    console.error(`Failed to obtain the maximum volume. ${err}`);
    return;
  }
  console.info(`Callback invoked to indicate that the maximum volume is obtained. ${value}`);
});
```

### getMaxVolume<sup>(deprecated)</sup>

getMaxVolume(volumeType: AudioVolumeType): Promise&lt;number&gt;

获取指定流的最大音量，使用Promise方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioVolumeGroupManager中的[getMaxVolume](#getmaxvolume9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明         |
| ---------- | ----------------------------------- | ---- | ------------ |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。 |

**返回值：**

| 类型                  | 说明                          |
| --------------------- | ----------------------------- |
| Promise&lt;number&gt; | Promise对象，返回最大音量。 |

**示例：**

```ts
audioManager.getMaxVolume(audio.AudioVolumeType.MEDIA).then((data: number) => {
  console.info('Promised returned to indicate that the maximum volume is obtained.');
});
```

### mute<sup>(deprecated)</sup>

mute(volumeType: AudioVolumeType, mute: boolean, callback: AsyncCallback&lt;void&gt;): void

设置指定音量流静音，使用callback方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃。替代接口仅面向系统应用开放。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明                                  |
| ---------- | ----------------------------------- | ---- | ------------------------------------- |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。                          |
| mute       | boolean                             | 是   | 静音状态，true为静音，false为非静音。 |
| callback   | AsyncCallback&lt;void&gt;           | 是   | 回调函数。当设置指定音量流静音成功，err为undefined，否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioManager.mute(audio.AudioVolumeType.MEDIA, true, (err: BusinessError) => {
  if (err) {
    console.error(`Failed to mute the stream. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate that the stream is muted.');
});
```

### mute<sup>(deprecated)</sup>

mute(volumeType: AudioVolumeType, mute: boolean): Promise&lt;void&gt;

设置指定音量流静音，使用Promise方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃。替代接口仅面向系统应用开放。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明                                  |
| ---------- | ----------------------------------- | ---- | ------------------------------------- |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。                          |
| mute       | boolean                             | 是   | 静音状态，true为静音，false为非静音。 |

**返回值：**

| 类型                | 说明                          |
| ------------------- | ----------------------------- |
| Promise&lt;void&gt; | Promise对象，无返回结果。 |

**示例：**


```ts
audioManager.mute(audio.AudioVolumeType.MEDIA, true).then(() => {
  console.info('Promise returned to indicate that the stream is muted.');
});
```

### isMute<sup>(deprecated)</sup>

isMute(volumeType: AudioVolumeType, callback: AsyncCallback&lt;boolean&gt;): void

获取指定音量流是否被静音，使用callback方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioVolumeGroupManager中的[isMute](#ismute9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明                                            |
| ---------- | ----------------------------------- | ---- | ----------------------------------------------- |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。                                    |
| callback   | AsyncCallback&lt;boolean&gt;        | 是   | 回调函数。当获取指定音量流是否被静音成功，err为undefined，data为true为静音，false为非静音；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioManager.isMute(audio.AudioVolumeType.MEDIA, (err: BusinessError, value: boolean) => {
  if (err) {
    console.error(`Failed to obtain the mute status. ${err}`);
    return;
  }
  console.info(`Callback invoked to indicate that the mute status of the stream is obtained. ${value}`);
});
```

### isMute<sup>(deprecated)</sup>

isMute(volumeType: AudioVolumeType): Promise&lt;boolean&gt;

获取指定音量流是否被静音，使用Promise方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioVolumeGroupManager中的[isMute](#ismute9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明         |
| ---------- | ----------------------------------- | ---- | ------------ |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。 |

**返回值：**

| 类型                   | 说明                                                   |
| ---------------------- | ------------------------------------------------------ |
| Promise&lt;boolean&gt; | Promise对象，返回流静音状态，true为静音，false为非静音。 |

**示例：**

```ts
audioManager.isMute(audio.AudioVolumeType.MEDIA).then((value: boolean) => {
  console.info(`Promise returned to indicate that the mute status of the stream is obtained ${value}.`);
});
```

### isActive<sup>(deprecated)</sup>

isActive(volumeType: AudioVolumeType, callback: AsyncCallback&lt;boolean&gt;): void

获取指定音量流是否为活跃状态，使用callback方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioStreamManager中的[isActive](#isactive9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明                                              |
| ---------- | ----------------------------------- | ---- | ------------------------------------------------- |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。                                      |
| callback   | AsyncCallback&lt;boolean&gt;        | 是   | 回调函数。当获取指定音量流是否为活跃状态成功，err为undefined，data为true为活跃，false为不活跃；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioManager.isActive(audio.AudioVolumeType.MEDIA, (err: BusinessError, value: boolean) => {
  if (err) {
    console.error(`Failed to obtain the active status of the stream. ${err}`);
    return;
  }
  console.info(`Callback invoked to indicate that the active status of the stream is obtained ${value}.`);
});
```

### isActive<sup>(deprecated)</sup>

isActive(volumeType: AudioVolumeType): Promise&lt;boolean&gt;

获取指定音量流是否为活跃状态，使用Promise方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioStreamManager中的[isActive](#isactive9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明         |
| ---------- | ----------------------------------- | ---- | ------------ |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。 |

**返回值：**

| 类型                   | 说明                                                     |
| ---------------------- | -------------------------------------------------------- |
| Promise&lt;boolean&gt; | Promise对象，返回流的活跃状态，true为活跃，false为不活跃。 |

**示例：**

```ts
audioManager.isActive(audio.AudioVolumeType.MEDIA).then((value: boolean) => {
  console.info(`Promise returned to indicate that the active status of the stream is obtained ${value}.`);
});
```

### setRingerMode<sup>(deprecated)</sup>

setRingerMode(mode: AudioRingMode, callback: AsyncCallback&lt;void&gt;): void

设置铃声模式，使用callback方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃。替代接口仅面向系统应用开放。

**需要权限：** ohos.permission.ACCESS_NOTIFICATION_POLICY

仅在静音和非静音状态切换时需要该权限。

**系统能力：** SystemCapability.Multimedia.Audio.Communication

**参数：**

| 参数名   | 类型                            | 必填 | 说明                     |
| -------- | ------------------------------- | ---- | ------------------------ |
| mode     | [AudioRingMode](#audioringmode) | 是   | 音频铃声模式。           |
| callback | AsyncCallback&lt;void&gt;       | 是   | 回调函数。当设置铃声模式成功，err为undefined，否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioManager.setRingerMode(audio.AudioRingMode.RINGER_MODE_NORMAL, (err: BusinessError) => {
  if (err) {
    console.error(`Failed to set the ringer mode. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate a successful setting of the ringer mode.');
});
```

### setRingerMode<sup>(deprecated)</sup>

setRingerMode(mode: AudioRingMode): Promise&lt;void&gt;

设置铃声模式，使用Promise方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃。替代接口仅面向系统应用开放。


**需要权限：** ohos.permission.ACCESS_NOTIFICATION_POLICY

仅在静音和非静音状态切换时需要该权限。

**系统能力：** SystemCapability.Multimedia.Audio.Communication

**参数：**

| 参数名 | 类型                            | 必填 | 说明           |
| ------ | ------------------------------- | ---- | -------------- |
| mode   | [AudioRingMode](#audioringmode) | 是   | 音频铃声模式。 |

**返回值：**

| 类型                | 说明                            |
| ------------------- | ------------------------------- |
| Promise&lt;void&gt; | Promise对象，无返回结果。 |

**示例：**

```ts
audioManager.setRingerMode(audio.AudioRingMode.RINGER_MODE_NORMAL).then(() => {
  console.info('Promise returned to indicate a successful setting of the ringer mode.');
});
```

### getRingerMode<sup>(deprecated)</sup>

getRingerMode(callback: AsyncCallback&lt;AudioRingMode&gt;): void

获取铃声模式，使用callback方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioVolumeGroupManager中的[getRingerMode](#getringermode9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Communication

**参数：**

| 参数名   | 类型                                                 | 必填 | 说明                     |
| -------- | ---------------------------------------------------- | ---- | ------------------------ |
| callback | AsyncCallback&lt;[AudioRingMode](#audioringmode)&gt; | 是   | 回调函数。当获取铃声模式成功，err为undefined，data为获取到的铃声模式；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioManager.getRingerMode((err: BusinessError, value: audio.AudioRingMode) => {
  if (err) {
    console.error(`Failed to obtain the ringer mode. ${err}`);
    return;
  }
  console.info(`Callback invoked to indicate that the ringer mode is obtained ${value}.`);
});
```

### getRingerMode<sup>(deprecated)</sup>

getRingerMode(): Promise&lt;AudioRingMode&gt;

获取铃声模式，使用Promise方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioVolumeGroupManager中的[getRingerMode](#getringermode9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Communication

**返回值：**

| 类型                                           | 说明                            |
| ---------------------------------------------- | ------------------------------- |
| Promise&lt;[AudioRingMode](#audioringmode)&gt; | Promise对象，返回系统的铃声模式。 |

**示例：**

```ts
audioManager.getRingerMode().then((value: audio.AudioRingMode) => {
  console.info(`Promise returned to indicate that the ringer mode is obtained ${value}.`);
});
```

### getDevices<sup>(deprecated)</sup>

getDevices(deviceFlag: DeviceFlag, callback: AsyncCallback&lt;AudioDeviceDescriptors&gt;): void

获取音频设备列表，使用callback方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioRoutingManager中的[getDevices](#getdevices9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                 |
| ---------- | ------------------------------------------------------------ | ---- | -------------------- |
| deviceFlag | [DeviceFlag](#deviceflag)                                    | 是   | 设备类型的flag。     |
| callback   | AsyncCallback&lt;[AudioDeviceDescriptors](#audiodevicedescriptors)&gt; | 是   | 回调函数。当获取音频设备列表成功，err为undefined，data为获取到的音频设备列表；否则为错误对象。 |

**示例：**
```ts
import { BusinessError } from '@ohos.base';

audioManager.getDevices(audio.DeviceFlag.OUTPUT_DEVICES_FLAG, (err: BusinessError, value: audio.AudioDeviceDescriptors) => {
  if (err) {
    console.error(`Failed to obtain the device list. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate that the device list is obtained.');
});
```

### getDevices<sup>(deprecated)</sup>

getDevices(deviceFlag: DeviceFlag): Promise&lt;AudioDeviceDescriptors&gt;

获取音频设备列表，使用Promise方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioRoutingManager中的[getDevices](#getdevices9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名     | 类型                      | 必填 | 说明             |
| ---------- | ------------------------- | ---- | ---------------- |
| deviceFlag | [DeviceFlag](#deviceflag) | 是   | 设备类型的flag。 |

**返回值：**

| 类型                                                         | 说明                      |
| ------------------------------------------------------------ | ------------------------- |
| Promise&lt;[AudioDeviceDescriptors](#audiodevicedescriptors)&gt; | Promise对象，返回设备列表。 |

**示例：**

```ts
audioManager.getDevices(audio.DeviceFlag.OUTPUT_DEVICES_FLAG).then((data: audio.AudioDeviceDescriptors) => {
  console.info('Promise returned to indicate that the device list is obtained.');
});
```

### setDeviceActive<sup>(deprecated)</sup>

setDeviceActive(deviceType: ActiveDeviceType, active: boolean, callback: AsyncCallback&lt;void&gt;): void

设置设备激活状态，使用callback方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioRoutingManager中的[setCommunicationDevice](#setcommunicationdevice9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名     | 类型                                  | 必填 | 说明          |
| ---------- | ------------------------------------- | ---- |-------------|
| deviceType | [ActiveDeviceType](#activedevicetypedeprecated) | 是   | 活跃音频设备类型。   |
| active     | boolean                               | 是   | 设备激活状态。     |
| callback   | AsyncCallback&lt;void&gt;             | 是   | 回调函数。当设置设备激活状态成功，err为undefined，否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioManager.setDeviceActive(audio.ActiveDeviceType.SPEAKER, true, (err: BusinessError) => {
  if (err) {
    console.error(`Failed to set the active status of the device. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate that the device is set to the active status.');
});
```

### setDeviceActive<sup>(deprecated)</sup>

setDeviceActive(deviceType: ActiveDeviceType, active: boolean): Promise&lt;void&gt;

设置设备激活状态，使用Promise方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioRoutingManager中的[setCommunicationDevice](#setcommunicationdevice9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名     | 类型                                  | 必填 | 说明               |
| ---------- | ------------------------------------- | ---- | ------------------ |
| deviceType | [ActiveDeviceType](#activedevicetypedeprecated) | 是   | 活跃音频设备类型。 |
| active     | boolean                               | 是   | 设备激活状态。     |

**返回值：**

| 类型                | 说明                            |
| ------------------- | ------------------------------- |
| Promise&lt;void&gt; | Promise对象，无返回结果。 |

**示例：**


```ts
audioManager.setDeviceActive(audio.ActiveDeviceType.SPEAKER, true).then(() => {
  console.info('Promise returned to indicate that the device is set to the active status.');
});
```

### isDeviceActive<sup>(deprecated)</sup>

isDeviceActive(deviceType: ActiveDeviceType, callback: AsyncCallback&lt;boolean&gt;): void

获取指定设备的激活状态，使用callback方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioRoutingManager中的[isCommunicationDeviceActive](#iscommunicationdeviceactive9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名     | 类型                                  | 必填 | 说明                     |
| ---------- | ------------------------------------- | ---- | ------------------------ |
| deviceType | [ActiveDeviceType](#activedevicetypedeprecated) | 是   | 活跃音频设备类型。       |
| callback   | AsyncCallback&lt;boolean&gt;          | 是   | 回调函数。当获取指定设备的激活状态成功，err为undefined，data为true为激活，false为未激活；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioManager.isDeviceActive(audio.ActiveDeviceType.SPEAKER, (err: BusinessError, value: boolean) => {
  if (err) {
    console.error(`Failed to obtain the active status of the device. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate that the active status of the device is obtained.');
});
```

### isDeviceActive<sup>(deprecated)</sup>

isDeviceActive(deviceType: ActiveDeviceType): Promise&lt;boolean&gt;

获取指定设备的激活状态，使用Promise方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioRoutingManager中的[isCommunicationDeviceActive](#iscommunicationdeviceactive9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名     | 类型                                  | 必填 | 说明               |
| ---------- | ------------------------------------- | ---- | ------------------ |
| deviceType | [ActiveDeviceType](#activedevicetypedeprecated) | 是   | 活跃音频设备类型。 |

**返回值：**

| Type                   | Description                           |
| ---------------------- |---------------------------------------|
| Promise&lt;boolean&gt; | Promise对象，返回设备的激活状态，true激活，false未激活。  |

**示例：**

```ts
audioManager.isDeviceActive(audio.ActiveDeviceType.SPEAKER).then((value: boolean) => {
  console.info(`Promise returned to indicate that the active status of the device is obtained ${value}.`);
});
```

### setMicrophoneMute<sup>(deprecated)</sup>

setMicrophoneMute(mute: boolean, callback: AsyncCallback&lt;void&gt;): void

设置麦克风静音状态，使用callback方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃。替代接口仅面向系统应用开放。

**需要权限：** ohos.permission.MICROPHONE

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名   | 类型                      | 必填 | 说明                                          |
| -------- | ------------------------- | ---- | --------------------------------------------- |
| mute     | boolean                   | 是   | 待设置的静音状态，true为静音，false为非静音。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。当设置麦克风静音状态成功，err为undefined，否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioManager.setMicrophoneMute(true, (err: BusinessError) => {
  if (err) {
    console.error(`Failed to mute the microphone. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate that the microphone is muted.');
});
```

### setMicrophoneMute<sup>(deprecated)</sup>

setMicrophoneMute(mute: boolean): Promise&lt;void&gt;

设置麦克风静音状态，使用Promise方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃。替代接口仅面向系统应用开放。

**需要权限：** ohos.permission.MICROPHONE

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名 | 类型    | 必填 | 说明                                          |
| ------ | ------- | ---- | --------------------------------------------- |
| mute   | boolean | 是   | 待设置的静音状态，true为静音，false为非静音。 |

**返回值：**

| 类型                | 说明                            |
| ------------------- | ------------------------------- |
| Promise&lt;void&gt; | Promise对象，无返回结果。 |

**示例：**

```ts
audioManager.setMicrophoneMute(true).then(() => {
  console.info('Promise returned to indicate that the microphone is muted.');
});
```

### isMicrophoneMute<sup>(deprecated)</sup>

isMicrophoneMute(callback: AsyncCallback&lt;boolean&gt;): void

获取麦克风静音状态，使用callback方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioVolumeGroupManager中的[isMicrophoneMute](#ismicrophonemute9)替代。

**需要权限：** ohos.permission.MICROPHONE

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名   | 类型                         | 必填 | 说明                                                    |
| -------- | ---------------------------- | ---- | ------------------------------------------------------- |
| callback | AsyncCallback&lt;boolean&gt; | 是   | 回调函数。当获取麦克风静音状态成功，err为undefined，data为true为静音，false为非静音；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioManager.isMicrophoneMute((err: BusinessError, value: boolean) => {
  if (err) {
    console.error(`Failed to obtain the mute status of the microphone. ${err}`);
    return;
  }
  console.info(`Callback invoked to indicate that the mute status of the microphone is obtained ${value}.`);
});
```

### isMicrophoneMute<sup>(deprecated)</sup>

isMicrophoneMute(): Promise&lt;boolean&gt;

获取麦克风静音状态，使用Promise方式异步返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioVolumeGroupManager中的[isMicrophoneMute](#ismicrophonemute9)替代。

**需要权限：** ohos.permission.MICROPHONE

**系统能力：** SystemCapability.Multimedia.Audio.Device

**返回值：**

| 类型                   | 说明                                                         |
| ---------------------- | ------------------------------------------------------------ |
| Promise&lt;boolean&gt; | Promise对象，返回系统麦克风静音状态，true为静音，false为非静音。 |

**示例：**

```ts
audioManager.isMicrophoneMute().then((value: boolean) => {
  console.info(`Promise returned to indicate that the mute status of the microphone is obtained ${value}.`);
});
```

### on('deviceChange')<sup>(deprecated)</sup>

on(type: 'deviceChange', callback: Callback<DeviceChangeAction\>): void

设备更改。音频设备连接状态变化，使用callback方式返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioRoutingManager中的[on('deviceChange')](#ondevicechange9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名   | 类型                                                 | 必填 | 说明                                       |
| :------- | :--------------------------------------------------- | :--- | :----------------------------------------- |
| type     | string                                               | 是   | 订阅的事件的类型。支持事件：'deviceChange' |
| callback | Callback<[DeviceChangeAction](#devicechangeaction)\> | 是   | 回调函数，返回设备更新详情。 |

**示例：**

```ts
audioManager.on('deviceChange', (deviceChanged: audio.DeviceChangeAction) => {
  console.info(`device change type : ${deviceChanged.type} `);
  console.info(`device descriptor size : ${deviceChanged.deviceDescriptors.length} `);
  console.info(`device change descriptor : ${deviceChanged.deviceDescriptors[0].deviceRole} `);
  console.info(`device change descriptor : ${deviceChanged.deviceDescriptors[0].deviceType} `);
});
```

### off('deviceChange')<sup>(deprecated)</sup>

off(type: 'deviceChange', callback?: Callback<DeviceChangeAction\>): void

取消订阅音频设备连接变化事件，使用callback方式返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 9 开始废弃，建议使用AudioRoutingManager中的[off('deviceChange')](#offdevicechange9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名   | 类型                                                | 必填 | 说明                                       |
| -------- | --------------------------------------------------- | ---- | ------------------------------------------ |
| type     | string                                              | 是   | 订阅的事件的类型。支持事件：'deviceChange' |
| callback | Callback<[DeviceChangeAction](#devicechangeaction)> | 否   | 回调函数，返回设备更新详情。 |

**示例：**

```ts
audioManager.off('deviceChange');
```

### on('interrupt')<sup>(deprecated)</sup>

on(type: 'interrupt', interrupt: AudioInterrupt, callback: Callback\<InterruptAction>): void

请求焦点并开始监听音频打断事件（当应用程序的音频被另一个播放事件中断，回调通知此应用程序），使用callback方式返回结果。

与[on('audioInterrupt')](#onaudiointerrupt9)作用一致，均用于监听焦点变化。为无音频流的场景（未曾创建AudioRenderer对象），比如FM、语音唤醒等提供焦点变化监听功能。

> **说明：**
> 从 API version 7 开始支持，从 API version 11 开始废弃，建议使用AudioCapturer中的[on('audioInterrupt')](#onaudiointerrupt10)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名    | 类型                                                      | 必填 | 说明                                                         |
| --------- |---------------------------------------------------------| ---- | ------------------------------------------------------------ |
| type      | string                                                  | 是   | 音频打断事件回调类型，支持的事件为：'interrupt'（多应用之间第二个应用会打断第一个应用，触发该事件）。 |
| interrupt | [AudioInterrupt](#audiointerruptdeprecated)             | 是   | 音频打断事件类型的参数。                                     |
| callback  | Callback<[InterruptAction](#interruptactiondeprecated)> | 是   | 回调函数，返回音频打断时，应用接收的中断事件信息。 |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

let interAudioInterrupt: audio.AudioInterrupt = {
  streamUsage:2,
  contentType:0,
  pauseWhenDucked:true
};
audioManager.on('interrupt', interAudioInterrupt, (InterruptAction: audio.InterruptAction) => {
  if (InterruptAction.actionType === 0) {
    console.info('An event to gain the audio focus starts.');
    console.info(`Focus gain event: ${InterruptAction} `);
  }
  if (InterruptAction.actionType === 1) {
    console.info('An audio interruption event starts.');
    console.info(`Audio interruption event: ${InterruptAction} `);
  }
});
```

### off('interrupt')<sup>(deprecated)</sup>

off(type: 'interrupt', interrupt: AudioInterrupt, callback?: Callback\<InterruptAction>): void

取消监听音频打断事件（删除监听事件，取消打断），使用callback方式返回结果。

> **说明：**
> 从 API version 7 开始支持，从 API version 11 开始废弃，建议使用AudioCapturer中的[off('audioInterrupt')](#offaudiointerrupt10)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名    | 类型                                                      | 必填 | 说明                                                         |
| --------- |---------------------------------------------------------| ---- | ------------------------------------------------------------ |
| type      | string                                                  | 是   | 音频打断事件回调类型，支持的事件为：'interrupt'（多应用之间第二个应用会打断第一个应用，触发该事件）。 |
| interrupt | [AudioInterrupt](#audiointerruptdeprecated)                       | 是   | 音频打断事件类型的参数。                                     |
| callback  | Callback<[InterruptAction](#interruptactiondeprecated)> | 否   | 回调函数，返回删除监听事件，取消打断时，应用接收的中断事件信息。 |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

let interAudioInterrupt: audio.AudioInterrupt = {
  streamUsage:2,
  contentType:0,
  pauseWhenDucked:true
};
audioManager.off('interrupt', interAudioInterrupt, (InterruptAction: audio.InterruptAction) => {
  if (InterruptAction.actionType === 0) {
    console.info('An event to release the audio focus starts.');
    console.info(`Focus release event: ${InterruptAction} `);
  }
});
```

## AudioVolumeManager<sup>9+</sup>

音量管理。在使用AudioVolumeManager的接口前，需要使用[getVolumeManager](#getvolumemanager9)获取AudioVolumeManager实例。

### getVolumeGroupManager<sup>9+</sup>

getVolumeGroupManager(groupId: number, callback: AsyncCallback<AudioVolumeGroupManager\>\): void

获取音频组管理器，使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                                                        |
| ---------- | ------------------------------------------------------------ | ---- |-----------------------------------------------------------|
| groupId    | number                                    | 是   | 音量组id，默认使用LOCAL_VOLUME_GROUP_ID。                          |
| callback   | AsyncCallback&lt;[AudioVolumeGroupManager](#audiovolumegroupmanager9)&gt; | 是   | 回调函数。当获取音频组管理器成功，err为undefined，data为获取到的音频组管理器对象；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let groupId: number = audio.DEFAULT_VOLUME_GROUP_ID;
audioVolumeManager.getVolumeGroupManager(groupId, (err: BusinessError, value: audio.AudioVolumeGroupManager) => {
  if (err) {
    console.error(`Failed to obtain the volume group infos list. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate that the volume group infos list is obtained.');
});

```

### getVolumeGroupManager<sup>9+</sup>

getVolumeGroupManager(groupId: number\): Promise<AudioVolumeGroupManager\>

获取音频组管理器，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                      | 必填 | 说明                               |
| ---------- | ---------------------------------------- | ---- |----------------------------------|
| groupId    | number                                   | 是   | 音量组id，默认使用LOCAL_VOLUME_GROUP_ID。 |

**返回值：**

| 类型                | 说明                          |
| ------------------- | ----------------------------- |
| Promise&lt; [AudioVolumeGroupManager](#audiovolumegroupmanager9) &gt; | Promise对象，返回音量组实例。 |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

let groupId: number = audio.DEFAULT_VOLUME_GROUP_ID;
let audioVolumeGroupManager: audio.AudioVolumeGroupManager | undefined = undefined;
async function getVolumeGroupManager(){
  audioVolumeGroupManager = await audioVolumeManager.getVolumeGroupManager(groupId);
  console.info('Promise returned to indicate that the volume group infos list is obtained.');
}
```

### getVolumeGroupManagerSync<sup>10+</sup>

getVolumeGroupManagerSync(groupId: number\): AudioVolumeGroupManager

获取音频组管理器，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                      | 必填 | 说明                               |
| ---------- | ---------------------------------------- | ---- |----------------------------------|
| groupId    | number                                   | 是   | 音量组id，默认使用LOCAL_VOLUME_GROUP_ID。 |

**返回值：**

| 类型                | 说明                          |
| ------------------- | ----------------------------- |
| [AudioVolumeGroupManager](#audiovolumegroupmanager9) | 音量组实例。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | invalid parameter error              |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let audioVolumeGroupManager: audio.AudioVolumeGroupManager = audioVolumeManager.getVolumeGroupManagerSync(audio.DEFAULT_VOLUME_GROUP_ID);
  console.info(`Get audioVolumeGroupManager success.`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`Failed to get audioVolumeGroupManager, error: ${error}`);
}
```

### on('volumeChange')<sup>9+</sup>

on(type: 'volumeChange', callback: Callback\<VolumeEvent>): void

监听系统音量变化事件，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名   | 类型                                   | 必填 | 说明                                                         |
| -------- | -------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                                 | 是   | 事件回调类型，支持的事件为：'volumeChange'。 |
| callback | Callback<[VolumeEvent](#volumeevent9)> | 是   | 回调函数，返回变化后的音量信息。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. |

**示例：**

```ts
audioVolumeManager.on('volumeChange', (volumeEvent: audio.VolumeEvent) => {
  console.info(`VolumeType of stream: ${volumeEvent.volumeType} `);
  console.info(`Volume level: ${volumeEvent.volume} `);
  console.info(`Whether to updateUI: ${volumeEvent.updateUi} `);
});
```

## AudioVolumeGroupManager<sup>9+</sup>

管理音频组音量。在调用AudioVolumeGroupManager的接口前，需要先通过 [getVolumeGroupManager](#getvolumegroupmanager9) 创建实例。

### getVolume<sup>9+</sup>

getVolume(volumeType: AudioVolumeType, callback: AsyncCallback&lt;number&gt;): void

获取指定流的音量，使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明               |
| ---------- | ----------------------------------- | ---- | ------------------ |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。       |
| callback   | AsyncCallback&lt;number&gt;         | 是   | 回调函数。当获取指定流的音量成功，err为undefined，data为获取到的指定流的音量；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioVolumeGroupManager.getVolume(audio.AudioVolumeType.MEDIA, (err: BusinessError, value: number) => {
  if (err) {
    console.error(`Failed to obtain the volume. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate that the volume is obtained.');
});
```

### getVolume<sup>9+</sup>

getVolume(volumeType: AudioVolumeType): Promise&lt;number&gt;

获取指定流的音量，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明         |
| ---------- | ----------------------------------- | ---- | ------------ |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。 |

**返回值：**

| 类型                  | 说明                      |
| --------------------- | ------------------------- |
| Promise&lt;number&gt; | Promise对象，返回音量大小。 |

**示例：**

```ts
audioVolumeGroupManager.getVolume(audio.AudioVolumeType.MEDIA).then((value: number) => {
  console.info(`Promise returned to indicate that the volume is obtained ${value}.`);
});
```

### getVolumeSync<sup>10+</sup>

getVolumeSync(volumeType: AudioVolumeType): number;

获取指定流的音量，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明         |
| ---------- | ----------------------------------- | ---- | ------------ |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。 |

**返回值：**

| 类型                  | 说明                      |
| --------------------- | ------------------------- |
| number | 返回音量大小。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | invalid parameter error              |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let value: number = audioVolumeGroupManager.getVolumeSync(audio.AudioVolumeType.MEDIA);
  console.info(`Indicate that the volume is obtained ${value}.`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`Failed to obtain the volume, error ${error}.`);
}
```

### getMinVolume<sup>9+</sup>

getMinVolume(volumeType: AudioVolumeType, callback: AsyncCallback&lt;number&gt;): void

获取指定流的最小音量，使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明               |
| ---------- | ----------------------------------- | ---- | ------------------ |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。       |
| callback   | AsyncCallback&lt;number&gt;         | 是   | 回调函数。当获取指定流的最小音量成功，err为undefined，data为获取到的指定流的最小音量；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioVolumeGroupManager.getMinVolume(audio.AudioVolumeType.MEDIA, (err: BusinessError, value: number) => {
  if (err) {
    console.error(`Failed to obtain the minimum volume. ${err}`);
    return;
  }
  console.info(`Callback invoked to indicate that the minimum volume is obtained. ${value}`);
});
```

### getMinVolume<sup>9+</sup>

getMinVolume(volumeType: AudioVolumeType): Promise&lt;number&gt;

获取指定流的最小音量，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明         |
| ---------- | ----------------------------------- | ---- | ------------ |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。 |

**返回值：**

| 类型                  | 说明                      |
| --------------------- | ------------------------- |
| Promise&lt;number&gt; | Promise对象，返回最小音量。 |

**示例：**

```ts
audioVolumeGroupManager.getMinVolume(audio.AudioVolumeType.MEDIA).then((value: number) => {
  console.info(`Promised returned to indicate that the minimum volume is obtained ${value}.`);
});
```

### getMinVolumeSync<sup>10+</sup>

getMinVolumeSync(volumeType: AudioVolumeType): number;

获取指定流的最小音量，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明         |
| ---------- | ----------------------------------- | ---- | ------------ |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。 |

**返回值：**

| 类型                  | 说明                      |
| --------------------- | ------------------------- |
| number | 返回最小音量。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | invalid parameter error              |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let value: number = audioVolumeGroupManager.getMinVolumeSync(audio.AudioVolumeType.MEDIA);
  console.info(`Indicate that the minimum volume is obtained ${value}.`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`Failed to obtain the minimum volume, error ${error}.`);
}
```

### getMaxVolume<sup>9+</sup>

getMaxVolume(volumeType: AudioVolumeType, callback: AsyncCallback&lt;number&gt;): void

获取指定流的最大音量，使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明                   |
| ---------- | ----------------------------------- | ---- | ---------------------- |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。           |
| callback   | AsyncCallback&lt;number&gt;         | 是   | 回调函数。当获取指定流的最大音量成功，err为undefined，data为获取到的指定流的最大音量；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioVolumeGroupManager.getMaxVolume(audio.AudioVolumeType.MEDIA, (err: BusinessError, value: number) => {
  if (err) {
    console.error(`Failed to obtain the maximum volume. ${err}`);
    return;
  }
  console.info(`Callback invoked to indicate that the maximum volume is obtained. ${value}`);
});
```

### getMaxVolume<sup>9+</sup>

getMaxVolume(volumeType: AudioVolumeType): Promise&lt;number&gt;

获取指定流的最大音量，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明         |
| ---------- | ----------------------------------- | ---- | ------------ |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。 |

**返回值：**

| 类型                  | 说明                          |
| --------------------- | ----------------------------- |
| Promise&lt;number&gt; | Promise对象，返回最大音量大小。 |

**示例：**

```ts
audioVolumeGroupManager.getMaxVolume(audio.AudioVolumeType.MEDIA).then((data: number) => {
  console.info('Promised returned to indicate that the maximum volume is obtained.');
});
```

### getMaxVolumeSync<sup>10+</sup>

getMaxVolumeSync(volumeType: AudioVolumeType): number;

获取指定流的最大音量，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明         |
| ---------- | ----------------------------------- | ---- | ------------ |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。 |

**返回值：**

| 类型                  | 说明                          |
| --------------------- | ----------------------------- |
| number | 返回最大音量大小。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | invalid parameter error              |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let value: number = audioVolumeGroupManager.getMaxVolumeSync(audio.AudioVolumeType.MEDIA);
  console.info(`Indicate that the maximum volume is obtained. ${value}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`Failed to obtain the maximum volume, error ${error}.`);
}
```

### isMute<sup>9+</sup>

isMute(volumeType: AudioVolumeType, callback: AsyncCallback&lt;boolean&gt;): void

获取指定音量流是否被静音，使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明                                            |
| ---------- | ----------------------------------- | ---- | ----------------------------------------------- |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。                                    |
| callback   | AsyncCallback&lt;boolean&gt;        | 是   | 回调函数。当获取指定音量流是否被静音成功，err为undefined，data为true为静音，false为非静音；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioVolumeGroupManager.isMute(audio.AudioVolumeType.MEDIA, (err: BusinessError, value: boolean) => {
  if (err) {
    console.error(`Failed to obtain the mute status. ${err}`);
    return;
  }
  console.info(`Callback invoked to indicate that the mute status of the stream is obtained ${value}.`);
});
```

### isMute<sup>9+</sup>

isMute(volumeType: AudioVolumeType): Promise&lt;boolean&gt;

获取指定音量流是否被静音，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明         |
| ---------- | ----------------------------------- | ---- | ------------ |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。 |

**返回值：**

| 类型                   | 说明                                                   |
| ---------------------- | ------------------------------------------------------ |
| Promise&lt;boolean&gt; | Promise对象，返回流静音状态，true为静音，false为非静音。 |

**示例：**

```ts
audioVolumeGroupManager.isMute(audio.AudioVolumeType.MEDIA).then((value: boolean) => {
  console.info(`Promise returned to indicate that the mute status of the stream is obtained ${value}.`);
});
```

### isMuteSync<sup>10+</sup>

isMuteSync(volumeType: AudioVolumeType): boolean

获取指定音量流是否被静音，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明         |
| ---------- | ----------------------------------- | ---- | ------------ |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。 |

**返回值：**

| 类型                   | 说明                                                   |
| ---------------------- | ------------------------------------------------------ |
| boolean | 返回流静音状态，true为静音，false为非静音。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | invalid parameter error              |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let value: boolean = audioVolumeGroupManager.isMuteSync(audio.AudioVolumeType.MEDIA);
  console.info(`Indicate that the mute status of the stream is obtained ${value}.`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`Failed to obtain the mute status of the stream, error ${error}.`);
}
```

### getRingerMode<sup>9+</sup>

getRingerMode(callback: AsyncCallback&lt;AudioRingMode&gt;): void

获取铃声模式，使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名   | 类型                                                 | 必填 | 说明                     |
| -------- | ---------------------------------------------------- | ---- | ------------------------ |
| callback | AsyncCallback&lt;[AudioRingMode](#audioringmode)&gt; | 是   | 回调函数。当获取铃声模式成功，err为undefined，data为获取到的铃声模式；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioVolumeGroupManager.getRingerMode((err: BusinessError, value: audio.AudioRingMode) => {
  if (err) {
    console.error(`Failed to obtain the ringer mode. ${err}`);
    return;
  }
  console.info(`Callback invoked to indicate that the ringer mode is obtained ${value}.`);
});
```

### getRingerMode<sup>9+</sup>

getRingerMode(): Promise&lt;AudioRingMode&gt;

获取铃声模式，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**返回值：**

| 类型                                           | 说明                            |
| ---------------------------------------------- | ------------------------------- |
| Promise&lt;[AudioRingMode](#audioringmode)&gt; | Promise对象，返回系统的铃声模式。 |

**示例：**

```ts
audioVolumeGroupManager.getRingerMode().then((value: audio.AudioRingMode) => {
  console.info(`Promise returned to indicate that the ringer mode is obtained ${value}.`);
});
```

### getRingerModeSync<sup>10+</sup>

getRingerModeSync(): AudioRingMode

获取铃声模式，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**返回值：**

| 类型                                           | 说明                            |
| ---------------------------------------------- | ------------------------------- |
| [AudioRingMode](#audioringmode) | 返回系统的铃声模式。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let value: audio.AudioRingMode = audioVolumeGroupManager.getRingerModeSync();
  console.info(`Indicate that the ringer mode is obtained ${value}.`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`Failed to obtain the ringer mode, error ${error}.`);
}
```

### on('ringerModeChange')<sup>9+</sup>

on(type: 'ringerModeChange', callback: Callback\<AudioRingMode>): void

监听铃声模式变化事件，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名   | 类型                                      | 必填 | 说明                                                         |
| -------- | ----------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                                    | 是   | 事件回调类型，支持的事件为：'ringerModeChange'（铃声模式变化事件，检测到铃声模式改变时，触发该事件）。 |
| callback | Callback<[AudioRingMode](#audioringmode)> | 是   | 回调函数，返回变化后的铃音模式。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. |

**示例：**

```ts
audioVolumeGroupManager.on('ringerModeChange', (ringerMode: audio.AudioRingMode) => {
  console.info(`Updated ringermode: ${ringerMode}`);
});
```

### setMicrophoneMute<sup>(deprecated)</sup>

setMicrophoneMute(mute: boolean, callback: AsyncCallback&lt;void&gt;): void

设置麦克风静音状态，使用callback方式异步返回结果。

> **说明：**
>
> 从 API version 9开始支持，从API version 11 开始废弃。替代接口仅面向系统应用开放。

**需要权限：** ohos.permission.MANAGE_AUDIO_CONFIG，该权限仅系统应用可申请。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名   | 类型                      | 必填 | 说明                                          |
| -------- | ------------------------- | ---- | --------------------------------------------- |
| mute     | boolean                   | 是   | 待设置的静音状态，true为静音，false为非静音。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调函数。当设置麦克风静音状态成功，err为undefined，否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioVolumeGroupManager.setMicrophoneMute(true, (err: BusinessError) => {
  if (err) {
    console.error(`Failed to mute the microphone. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate that the microphone is muted.');
});
```

### setMicrophoneMute<sup>(deprecated)</sup>

setMicrophoneMute(mute: boolean): Promise&lt;void&gt;

设置麦克风静音状态，使用Promise方式异步返回结果。

> **说明：**
>
> 从 API version 9开始支持，从API version 11 开始废弃。替代接口仅面向系统应用开放。

**需要权限：** ohos.permission.MANAGE_AUDIO_CONFIG，该权限仅系统应用可申请。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名 | 类型    | 必填 | 说明                                          |
| ------ | ------- | ---- | --------------------------------------------- |
| mute   | boolean | 是   | 待设置的静音状态，true为静音，false为非静音。 |

**返回值：**

| 类型                | 说明                            |
| ------------------- | ------------------------------- |
| Promise&lt;void&gt; | Promise对象，无返回结果。 |

**示例：**

```ts
audioVolumeGroupManager.setMicrophoneMute(true).then(() => {
  console.info('Promise returned to indicate that the microphone is muted.');
});
```

### isMicrophoneMute<sup>9+</sup>

isMicrophoneMute(callback: AsyncCallback&lt;boolean&gt;): void

获取麦克风静音状态，使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名   | 类型                         | 必填 | 说明                                                    |
| -------- | ---------------------------- | ---- | ------------------------------------------------------- |
| callback | AsyncCallback&lt;boolean&gt; | 是   | 回调函数。当获取麦克风静音状态成功，err为undefined，data为true为静音，false为非静音；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioVolumeGroupManager.isMicrophoneMute((err: BusinessError, value: boolean) => {
  if (err) {
    console.error(`Failed to obtain the mute status of the microphone. ${err}`);
    return;
  }
  console.info(`Callback invoked to indicate that the mute status of the microphone is obtained ${value}.`);
});
```

### isMicrophoneMute<sup>9+</sup>

isMicrophoneMute(): Promise&lt;boolean&gt;

获取麦克风静音状态，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**返回值：**

| 类型                   | 说明                                                         |
| ---------------------- | ------------------------------------------------------------ |
| Promise&lt;boolean&gt; | Promise对象，返回系统麦克风静音状态，true为静音，false为非静音。 |

**示例：**

```ts
audioVolumeGroupManager.isMicrophoneMute().then((value: boolean) => {
  console.info(`Promise returned to indicate that the mute status of the microphone is obtained ${value}.`);
});
```

### isMicrophoneMuteSync<sup>10+</sup>

isMicrophoneMuteSync(): boolean

获取麦克风静音状态，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**返回值：**

| 类型                   | 说明                                                         |
| ---------------------- | ------------------------------------------------------------ |
| boolean | 返回系统麦克风静音状态，true为静音，false为非静音。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let value: boolean = audioVolumeGroupManager.isMicrophoneMuteSync();
  console.info(`Indicate that the mute status of the microphone is obtained ${value}.`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`Failed to obtain the mute status of the microphone, error ${error}.`);
}
```

### on('micStateChange')<sup>9+</sup>

on(type: 'micStateChange', callback: Callback&lt;MicStateChangeEvent&gt;): void

监听系统麦克风状态更改事件，使用callback方式返回结果。

目前此订阅接口在单进程多AudioManager实例的使用场景下，仅最后一个实例的订阅生效，其他实例的订阅会被覆盖（即使最后一个实例没有进行订阅），因此推荐使用单一AudioManager实例进行开发。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名   | 类型                                   | 必填 | 说明                                                         |
| -------- | -------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                                 | 是   | 事件回调类型，支持的事件为：'micStateChange'（系统麦克风状态变化事件，检测到系统麦克风状态改变时，触发该事件）。 |
| callback | Callback<[MicStateChangeEvent](#micstatechangeevent9)> | 是   | 回调函数，返回变更后的麦克风状态。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. |

**示例：**

```ts
audioVolumeGroupManager.on('micStateChange', (micStateChange: audio.MicStateChangeEvent) => {
  console.info(`Current microphone status is: ${micStateChange.mute} `);
});
```

### isVolumeUnadjustable<sup>10+</sup>

isVolumeUnadjustable(): boolean

获取固定音量模式开关状态，打开时进入固定音量模式，此时音量固定无法被调节，使用同步方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**返回值：**

| 类型                   | 说明                                                   |
| ---------------------- | ------------------------------------------------------ |
| boolean            | 同步接口，返回固定音量模式开关状态，true为固定音量模式，false为非固定音量模式。 |

**示例：**

```ts
let volumeAdjustSwitch: boolean = audioVolumeGroupManager.isVolumeUnadjustable();
console.info(`Whether it is volume unadjustable: ${volumeAdjustSwitch}.`);
```

### getSystemVolumeInDb<sup>10+</sup>

getSystemVolumeInDb(volumeType: AudioVolumeType, volumeLevel: number, device: DeviceType, callback: AsyncCallback&lt;number&gt;): void

获取音量增益dB值，使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明                                                     |
| ---------- | ----------------------------------- | ---- | -------------------------------------------------------- |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。                                             |
| volumeLevel | number                         | 是   | 音量等级。                                               |
| device     | [DeviceType](#devicetype)           | 是   | 设备类型。                                               |
| callback   | AsyncCallback&lt;number&gt;           | 是   | 回调函数。当获取音量增益dB值成功，err为undefined，data为获取到的音量增益dB值；否则为错误对象。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. Return by callback.                     |
| 6800301 | System error. Return by callback.                                |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioVolumeGroupManager.getSystemVolumeInDb(audio.AudioVolumeType.MEDIA, 3, audio.DeviceType.SPEAKER, (err: BusinessError, dB: number) => {
  if (err) {
    console.error(`Failed to get the volume DB. ${err}`);
  } else {
    console.info(`Success to get the volume DB. ${dB}`);
  }
});
```
### getSystemVolumeInDb<sup>10+</sup>

getSystemVolumeInDb(volumeType: AudioVolumeType, volumeLevel: number, device: DeviceType): Promise&lt;number&gt;

获取音量增益dB值，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明                                                     |
| ---------- | ----------------------------------- | ---- | -------------------------------------------------------- |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。                                             |
| volumeLevel | number                              | 是   | 音量等级。                                             |
| device     | [DeviceType](#devicetype)           | 是   | 设备类型。                                               |

**返回值：**

| 类型                  | 说明                               |
| --------------------- | ---------------------------------- |
| Promise&lt;number&gt; | Promise对象，返回对应的音量增益dB值。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. Return by promise.                     |
| 6800301 | System error. Return by promise.                                |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioVolumeGroupManager.getSystemVolumeInDb(audio.AudioVolumeType.MEDIA, 3, audio.DeviceType.SPEAKER).then((value: number) => {
  console.info(`Success to get the volume DB. ${value}`);
}).catch((error: BusinessError) => {
  console.error(`Fail to adjust the system volume by step. ${error}`);
});
```

### getSystemVolumeInDbSync<sup>10+</sup>

getSystemVolumeInDbSync(volumeType: AudioVolumeType, volumeLevel: number, device: DeviceType): number

获取音量增益dB值，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Volume

**参数：**

| 参数名     | 类型                                | 必填 | 说明                                                     |
| ---------- | ----------------------------------- | ---- | -------------------------------------------------------- |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音量流类型。                                             |
| volumeLevel | number                              | 是   | 音量等级。                                             |
| device     | [DeviceType](#devicetype)           | 是   | 设备类型。                                               |

**返回值：**

| 类型                  | 说明                               |
| --------------------- | ---------------------------------- |
| number | 返回对应的音量增益dB值。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | invalid parameter error                     |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let value: number = audioVolumeGroupManager.getSystemVolumeInDbSync(audio.AudioVolumeType.MEDIA, 3, audio.DeviceType.SPEAKER);
  console.info(`Success to get the volume DB. ${value}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`Fail to adjust the system volume by step. ${error}`);
}
```

## AudioStreamManager<sup>9+</sup>

管理音频流。在使用AudioStreamManager的API前，需要使用[getStreamManager](#getstreammanager9)获取AudioStreamManager实例。

### getCurrentAudioRendererInfoArray<sup>9+</sup>

getCurrentAudioRendererInfoArray(callback: AsyncCallback&lt;AudioRendererChangeInfoArray&gt;): void

获取当前音频渲染器的信息。使用callback异步回调。

**系统能力**: SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名     | 类型                                 | 必填     | 说明                         |
| -------- | ----------------------------------- | -------- | --------------------------- |
| callback | AsyncCallback<[AudioRendererChangeInfoArray](#audiorendererchangeinfoarray9)> | 是     | 回调函数。当获取当前音频渲染器的信息成功，err为undefined，data为获取到的当前音频渲染器的信息；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioStreamManager.getCurrentAudioRendererInfoArray(async (err: BusinessError, AudioRendererChangeInfoArray: audio.AudioRendererChangeInfoArray) => {
  console.info('getCurrentAudioRendererInfoArray **** Get Callback Called ****');
  if (err) {
    console.error(`getCurrentAudioRendererInfoArray :ERROR: ${err}`);
  } else {
    if (AudioRendererChangeInfoArray != null) {
      for (let i = 0; i < AudioRendererChangeInfoArray.length; i++) {
        let AudioRendererChangeInfo: audio.AudioRendererChangeInfo = AudioRendererChangeInfoArray[i];
        console.info(`StreamId for ${i} is: ${AudioRendererChangeInfo.streamId}`);
        console.info(`Content ${i} is: ${AudioRendererChangeInfo.rendererInfo.content}`);
        console.info(`Stream ${i} is: ${AudioRendererChangeInfo.rendererInfo.usage}`);
        console.info(`Flag ${i} is: ${AudioRendererChangeInfo.rendererInfo.rendererFlags}`);
        for (let j = 0;j < AudioRendererChangeInfo.deviceDescriptors.length; j++) {
          console.info(`Id: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].id}`);
          console.info(`Type: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].deviceType}`);
          console.info(`Role: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].deviceRole}`);
          console.info(`Name: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].name}`);
          console.info(`Address: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].address}`);
          console.info(`SampleRate: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].sampleRates[0]}`);
          console.info(`ChannelCount: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].channelCounts[0]}`);
          console.info(`ChannelMask: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].channelMasks[0]}`);
        }
      }
    }
  }
});
```

### getCurrentAudioRendererInfoArray<sup>9+</sup>

getCurrentAudioRendererInfoArray(): Promise&lt;AudioRendererChangeInfoArray&gt;

获取当前音频渲染器的信息。使用Promise异步回调。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型                                                                              | 说明                                    |
| ---------------------------------------------------------------------------------| --------------------------------------- |
| Promise<[AudioRendererChangeInfoArray](#audiorendererchangeinfoarray9)>          | Promise对象，返回当前音频渲染器信息。      |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function getCurrentAudioRendererInfoArray(){
  await audioStreamManager.getCurrentAudioRendererInfoArray().then((AudioRendererChangeInfoArray: audio.AudioRendererChangeInfoArray) => {
    console.info(`getCurrentAudioRendererInfoArray ######### Get Promise is called ##########`);
    if (AudioRendererChangeInfoArray != null) {
      for (let i = 0; i < AudioRendererChangeInfoArray.length; i++) {
        let AudioRendererChangeInfo: audio.AudioRendererChangeInfo = AudioRendererChangeInfoArray[i];
        console.info(`StreamId for ${i} is: ${AudioRendererChangeInfo.streamId}`);
        console.info(`Content ${i} is: ${AudioRendererChangeInfo.rendererInfo.content}`);
        console.info(`Stream ${i} is: ${AudioRendererChangeInfo.rendererInfo.usage}`);
        console.info(`Flag ${i} is: ${AudioRendererChangeInfo.rendererInfo.rendererFlags}`);
        for (let j = 0;j < AudioRendererChangeInfo.deviceDescriptors.length; j++) {
          console.info(`Id: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].id}`);
          console.info(`Type: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].deviceType}`);
          console.info(`Role: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].deviceRole}`);
          console.info(`Name: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].name}`);
          console.info(`Address: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].address}`);
          console.info(`SampleRate: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].sampleRates[0]}`);
          console.info(`ChannelCount: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].channelCounts[0]}`);
          console.info(`ChannelMask: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].channelMasks[0]}`);
        }
      }
    }
  }).catch((err: BusinessError) => {
    console.error(`getCurrentAudioRendererInfoArray :ERROR: ${err}`);
  });
}
```
### getCurrentAudioRendererInfoArraySync<sup>10+</sup>

getCurrentAudioRendererInfoArraySync(): AudioRendererChangeInfoArray

获取当前音频渲染器的信息，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型                                                                              | 说明                                    |
| ---------------------------------------------------------------------------------| --------------------------------------- |
| [AudioRendererChangeInfoArray](#audiorendererchangeinfoarray9)          | 返回当前音频渲染器信息。      |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let audioRendererChangeInfoArray: audio.AudioRendererChangeInfoArray = audioStreamManager.getCurrentAudioRendererInfoArraySync();
  console.info(`getCurrentAudioRendererInfoArraySync success.`);
  if (audioRendererChangeInfoArray != null) {
    for (let i = 0; i < audioRendererChangeInfoArray.length; i++) {
      let AudioRendererChangeInfo: audio.AudioRendererChangeInfo = audioRendererChangeInfoArray[i];
      console.info(`StreamId for ${i} is: ${AudioRendererChangeInfo.streamId}`);
      console.info(`Content ${i} is: ${AudioRendererChangeInfo.rendererInfo.content}`);
      console.info(`Stream ${i} is: ${AudioRendererChangeInfo.rendererInfo.usage}`);
      console.info(`Flag ${i} is: ${AudioRendererChangeInfo.rendererInfo.rendererFlags}`);
      for (let j = 0;j < AudioRendererChangeInfo.deviceDescriptors.length; j++) {
        console.info(`Id: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].id}`);
        console.info(`Type: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].deviceType}`);
        console.info(`Role: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].deviceRole}`);
        console.info(`Name: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].name}`);
        console.info(`Address: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].address}`);
        console.info(`SampleRate: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].sampleRates[0]}`);
        console.info(`ChannelCount: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].channelCounts[0]}`);
        console.info(`ChannelMask: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].channelMasks[0]}`);
      }
    }
  }
} catch (err) {
  let error = err as BusinessError;
  console.error(`getCurrentAudioRendererInfoArraySync :ERROR: ${error}`);
}
```

### getCurrentAudioCapturerInfoArray<sup>9+</sup>

getCurrentAudioCapturerInfoArray(callback: AsyncCallback&lt;AudioCapturerChangeInfoArray&gt;): void

获取当前音频采集器的信息。使用callback异步回调。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名        | 类型                                 | 必填      | 说明                                                      |
| ---------- | ----------------------------------- | --------- | -------------------------------------------------------- |
| callback   | AsyncCallback<[AudioCapturerChangeInfoArray](#audiocapturerchangeinfoarray9)> | 是    | 回调函数。当获取当前音频采集器的信息成功，err为undefined，data为获取到的当前音频采集器的信息；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioStreamManager.getCurrentAudioCapturerInfoArray(async (err: BusinessError, AudioCapturerChangeInfoArray: audio.AudioCapturerChangeInfoArray) => {
  console.info('getCurrentAudioCapturerInfoArray **** Get Callback Called ****');
  if (err) {
    console.error(`getCurrentAudioCapturerInfoArray :ERROR: ${err}`);
  } else {
    if (AudioCapturerChangeInfoArray != null) {
      for (let i = 0; i < AudioCapturerChangeInfoArray.length; i++) {
        console.info(`StreamId for ${i} is: ${AudioCapturerChangeInfoArray[i].streamId}`);
        console.info(`Source for ${i} is: ${AudioCapturerChangeInfoArray[i].capturerInfo.source}`);
        console.info(`Flag  ${i} is: ${AudioCapturerChangeInfoArray[i].capturerInfo.capturerFlags}`);
        for (let j = 0; j < AudioCapturerChangeInfoArray[i].deviceDescriptors.length; j++) {
          console.info(`Id: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].id}`);
          console.info(`Type: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].deviceType}`);
          console.info(`Role: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].deviceRole}`);
          console.info(`Name: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].name}`);
          console.info(`Address: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].address}`);
          console.info(`SampleRate: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].sampleRates[0]}`);
          console.info(`ChannelCount: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].channelCounts[0]}`);
          console.info(`ChannelMask: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].channelMasks[0]}`);
        }
      }
    }
  }
});
```

### getCurrentAudioCapturerInfoArray<sup>9+</sup>

getCurrentAudioCapturerInfoArray(): Promise&lt;AudioCapturerChangeInfoArray&gt;

获取当前音频采集器的信息。使用Promise异步回调。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型                                                                         | 说明                                 |
| -----------------------------------------------------------------------------| ----------------------------------- |
| Promise<[AudioCapturerChangeInfoArray](#audiocapturerchangeinfoarray9)>      | Promise对象，返回当前音频采集器信息。  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function getCurrentAudioCapturerInfoArray(){
  await audioStreamManager.getCurrentAudioCapturerInfoArray().then((AudioCapturerChangeInfoArray: audio.AudioCapturerChangeInfoArray) => {
    console.info('getCurrentAudioCapturerInfoArray **** Get Promise Called ****');
    if (AudioCapturerChangeInfoArray != null) {
      for (let i = 0; i < AudioCapturerChangeInfoArray.length; i++) {
        console.info(`StreamId for ${i} is: ${AudioCapturerChangeInfoArray[i].streamId}`);
        console.info(`Source for ${i} is: ${AudioCapturerChangeInfoArray[i].capturerInfo.source}`);
        console.info(`Flag  ${i} is: ${AudioCapturerChangeInfoArray[i].capturerInfo.capturerFlags}`);
        for (let j = 0; j < AudioCapturerChangeInfoArray[i].deviceDescriptors.length; j++) {
          console.info(`Id: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].id}`);
          console.info(`Type: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].deviceType}`);
          console.info(`Role: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].deviceRole}`);
          console.info(`Name: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].name}`);
          console.info(`Address: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].address}`);
          console.info(`SampleRate: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].sampleRates[0]}`);
          console.info(`ChannelCount: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].channelCounts[0]}`);
          console.info(`ChannelMask: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].channelMasks[0]}`);
        }
      }
    }
  }).catch((err: BusinessError) => {
    console.error(`getCurrentAudioCapturerInfoArray :ERROR: ${err}`);
  });
}
```
### getCurrentAudioCapturerInfoArraySync<sup>10+</sup>

getCurrentAudioCapturerInfoArraySync(): AudioCapturerChangeInfoArray

获取当前音频采集器的信息，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**返回值：**

| 类型                                                                         | 说明                                 |
| -----------------------------------------------------------------------------| ----------------------------------- |
| [AudioCapturerChangeInfoArray](#audiocapturerchangeinfoarray9)      | 返回当前音频采集器信息。  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let audioCapturerChangeInfoArray: audio.AudioCapturerChangeInfoArray = audioStreamManager.getCurrentAudioCapturerInfoArraySync();
  console.info('getCurrentAudioCapturerInfoArraySync success.');
  if (audioCapturerChangeInfoArray != null) {
    for (let i = 0; i < audioCapturerChangeInfoArray.length; i++) {
      console.info(`StreamId for ${i} is: ${audioCapturerChangeInfoArray[i].streamId}`);
      console.info(`Source for ${i} is: ${audioCapturerChangeInfoArray[i].capturerInfo.source}`);
      console.info(`Flag  ${i} is: ${audioCapturerChangeInfoArray[i].capturerInfo.capturerFlags}`);
      for (let j = 0; j < audioCapturerChangeInfoArray[i].deviceDescriptors.length; j++) {
        console.info(`Id: ${i} : ${audioCapturerChangeInfoArray[i].deviceDescriptors[j].id}`);
        console.info(`Type: ${i} : ${audioCapturerChangeInfoArray[i].deviceDescriptors[j].deviceType}`);
        console.info(`Role: ${i} : ${audioCapturerChangeInfoArray[i].deviceDescriptors[j].deviceRole}`);
        console.info(`Name: ${i} : ${audioCapturerChangeInfoArray[i].deviceDescriptors[j].name}`);
        console.info(`Address: ${i} : ${audioCapturerChangeInfoArray[i].deviceDescriptors[j].address}`);
        console.info(`SampleRate: ${i} : ${audioCapturerChangeInfoArray[i].deviceDescriptors[j].sampleRates[0]}`);
        console.info(`ChannelCount: ${i} : ${audioCapturerChangeInfoArray[i].deviceDescriptors[j].channelCounts[0]}`);
        console.info(`ChannelMask: ${i} : ${audioCapturerChangeInfoArray[i].deviceDescriptors[j].channelMasks[0]}`);
      }
    }
  }
} catch (err) {
  let error = err as BusinessError;
  console.error(`getCurrentAudioCapturerInfoArraySync ERROR: ${error}`);
}
```

### on('audioRendererChange')<sup>9+</sup>

on(type: 'audioRendererChange', callback: Callback&lt;AudioRendererChangeInfoArray&gt;): void

监听音频渲染器更改事件，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名      | 类型        | 必填      | 说明                                                                     |
| -------- | ---------- | --------- | ------------------------------------------------------------------------ |
| type     | string     | 是        | 事件类型，支持的事件`'audioRendererChange'`：当音频渲染器发生更改时触发。     |
| callback | Callback<[AudioRendererChangeInfoArray](#audiorendererchangeinfoarray9)> | 是  |  回调函数，返回当前音频渲染器信息。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. |

**示例：**

```ts
audioStreamManager.on('audioRendererChange',  (AudioRendererChangeInfoArray: audio.AudioRendererChangeInfoArray) => {
  for (let i = 0; i < AudioRendererChangeInfoArray.length; i++) {
    let AudioRendererChangeInfo: audio.AudioRendererChangeInfo = AudioRendererChangeInfoArray[i];
    console.info(`## RendererChange on is called for ${i} ##`);
    console.info(`StreamId for ${i} is: ${AudioRendererChangeInfo.streamId}`);
    console.info(`Content ${i} is: ${AudioRendererChangeInfo.rendererInfo.content}`);
    console.info(`Stream ${i} is: ${AudioRendererChangeInfo.rendererInfo.usage}`);
    console.info(`Flag ${i} is: ${AudioRendererChangeInfo.rendererInfo.rendererFlags}`);
    for (let j = 0;j < AudioRendererChangeInfo.deviceDescriptors.length; j++) {
      console.info(`Id: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].id}`);
      console.info(`Type: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].deviceType}`);
      console.info(`Role: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].deviceRole}`);
      console.info(`Name: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].name}`);
      console.info(`Address: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].address}`);
      console.info(`SampleRate: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].sampleRates[0]}`);
      console.info(`ChannelCount: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].channelCounts[0]}`);
      console.info(`ChannelMask: ${i} : ${AudioRendererChangeInfo.deviceDescriptors[j].channelMasks[0]}`);
    }
  }
});
```

### off('audioRendererChange')<sup>9+</sup>

off(type: 'audioRendererChange'): void

取消监听音频渲染器更改事件。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名     | 类型     | 必填 | 说明              |
| -------- | ------- | ---- | ---------------- |
| type     | string  | 是   | 事件类型，支持的事件`'audioRendererChange'`：音频渲染器更改事件。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息                     |
| ------- |--------------------------|
| 6800101 | Invalid parameter error. |

**示例：**

```ts
audioStreamManager.off('audioRendererChange');
console.info('######### RendererChange Off is called #########');
```

### on('audioCapturerChange')<sup>9+</sup>

on(type: 'audioCapturerChange', callback: Callback&lt;AudioCapturerChangeInfoArray&gt;): void

监听音频采集器更改事件，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名     | 类型     | 必填      | 说明                                                                                           |
| -------- | ------- | --------- | ----------------------------------------------------------------------- |
| type     | string  | 是        | 事件类型，支持的事件`'audioCapturerChange'`：当音频采集器发生更改时触发。     |
| callback | Callback<[AudioCapturerChangeInfoArray](#audiocapturerchangeinfoarray9)> | 是     | 回调函数，返回当前音频采集器信息。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. |

**示例：**

```ts
audioStreamManager.on('audioCapturerChange', (AudioCapturerChangeInfoArray: audio.AudioCapturerChangeInfoArray) =>  {
  for (let i = 0; i < AudioCapturerChangeInfoArray.length; i++) {
    console.info(`## CapChange on is called for element ${i} ##`);
    console.info(`StreamId for ${i} is: ${AudioCapturerChangeInfoArray[i].streamId}`);
    console.info(`Source for ${i} is: ${AudioCapturerChangeInfoArray[i].capturerInfo.source}`);
    console.info(`Flag  ${i} is: ${AudioCapturerChangeInfoArray[i].capturerInfo.capturerFlags}`);
    for (let j = 0; j < AudioCapturerChangeInfoArray[i].deviceDescriptors.length; j++) {
      console.info(`Id: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].id}`);
      console.info(`Type: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].deviceType}`);
      console.info(`Role: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].deviceRole}`);
      console.info(`Name: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].name}`);
      console.info(`Address: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].address}`);
      console.info(`SampleRate: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].sampleRates[0]}`);
      console.info(`ChannelCount: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].channelCounts[0]}`);
      console.info(`ChannelMask: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].channelMasks[0]}`);
    }
  }
});
```

### off('audioCapturerChange')<sup>9+</sup>

off(type: 'audioCapturerChange'): void

取消监听音频采集器更改事件。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名       | 类型     | 必填 | 说明                                                          |
| -------- | -------- | --- | ------------------------------------------------------------- |
| type     | string   |是   | 事件类型，支持的事件`'audioCapturerChange'`：音频采集器更改事件。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. |

**示例：**

```ts
audioStreamManager.off('audioCapturerChange');
console.info('######### CapturerChange Off is called #########');

```

### isActive<sup>9+</sup>

isActive(volumeType: AudioVolumeType, callback: AsyncCallback&lt;boolean&gt;): void

获取指定音频流是否为活跃状态，使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名     | 类型                                | 必填 | 说明                                              |
| ---------- | ----------------------------------- | ---- | ------------------------------------------------- |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音频流类型。                                      |
| callback   | AsyncCallback&lt;boolean&gt;        | 是   | 回调函数。当获取指定音频流是否为活跃状态成功，err为undefined，data为true为活跃，false为不活跃；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioStreamManager.isActive(audio.AudioVolumeType.MEDIA, (err: BusinessError, value: boolean) => {
if (err) {
  console.error(`Failed to obtain the active status of the stream. ${err}`);
  return;
}
  console.info(`Callback invoked to indicate that the active status of the stream is obtained ${value}.`);
});
```

### isActive<sup>9+</sup>

isActive(volumeType: AudioVolumeType): Promise&lt;boolean&gt;

获取指定音频流是否为活跃状态，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名     | 类型                                | 必填 | 说明         |
| ---------- | ----------------------------------- | ---- | ------------ |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音频流类型。 |

**返回值：**

| 类型                   | 说明                                                     |
| ---------------------- | -------------------------------------------------------- |
| Promise&lt;boolean&gt; | Promise对象，返回流的活跃状态，true为活跃，false为不活跃。 |

**示例：**

```ts
audioStreamManager.isActive(audio.AudioVolumeType.MEDIA).then((value: boolean) => {
  console.info(`Promise returned to indicate that the active status of the stream is obtained ${value}.`);
});
```

### isActiveSync<sup>10+</sup>

isActiveSync(volumeType: AudioVolumeType): boolean

获取指定音频流是否为活跃状态，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名     | 类型                                | 必填 | 说明         |
| ---------- | ----------------------------------- | ---- | ------------ |
| volumeType | [AudioVolumeType](#audiovolumetype) | 是   | 音频流类型。 |

**返回值：**

| 类型                   | 说明                                                     |
| ---------------------- | -------------------------------------------------------- |
| boolean | 返回流的活跃状态，true为活跃，false为不活跃。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | invalid parameter error              |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let value: boolean = audioStreamManager.isActiveSync(audio.AudioVolumeType.MEDIA);
  console.info(`Indicate that the active status of the stream is obtained ${value}.`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`Failed to obtain the active status of the stream ${error}.`);
}
```

### getAudioEffectInfoArray<sup>10+</sup>

getAudioEffectInfoArray(usage: StreamUsage, callback: AsyncCallback&lt;AudioEffectInfoArray&gt;): void

获取当前音效模式的信息。使用callback异步回调。

**系统能力**: SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名    | 类型                                | 必填     | 说明                         |
| -------- | ----------------------------------- | -------- | --------------------------- |
| usage    | [StreamUsage](#streamusage)                                    | 是     |  音频流使用类型。                |
| callback | AsyncCallback<[AudioEffectInfoArray](#audioeffectinfoarray10)> | 是     | 回调函数。当获取当前音效模式的信息成功，err为undefined，data为获取到的当前音效模式的信息；否则为错误对象。|

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. Return by callback.|

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioStreamManager.getAudioEffectInfoArray(audio.StreamUsage.STREAM_USAGE_MUSIC, async (err: BusinessError, audioEffectInfoArray: audio.AudioEffectInfoArray) => {
  console.info('getAudioEffectInfoArray **** Get Callback Called ****');
  if (err) {
    console.error(`getAudioEffectInfoArray :ERROR: ${err}`);
    return;
  } else {
    console.info(`The effect modes are: ${audioEffectInfoArray}`);
  }
});
```

### getAudioEffectInfoArray<sup>10+</sup>

getAudioEffectInfoArray(usage: StreamUsage): Promise&lt;AudioEffectInfoArray&gt;

获取当前音效模式的信息。使用Promise异步回调。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名    | 类型                                | 必填     | 说明                         |
| -------- | ----------------------------------- | -------- | --------------------------- |
| usage    | [StreamUsage](#streamusage)         | 是     |  音频流使用类型。               |

**返回值：**

| 类型                                                                      | 说明                                    |
| --------------------------------------------------------------------------| --------------------------------------- |
| Promise<[AudioEffectInfoArray](#audioeffectinfoarray10)>                  | Promise对象，返回当前音效模式的信息。      |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. Return by promise. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioStreamManager.getAudioEffectInfoArray(audio.StreamUsage.STREAM_USAGE_MUSIC).then((audioEffectInfoArray: audio.AudioEffectInfoArray) => {
  console.info('getAudioEffectInfoArray ######### Get Promise is called ##########');
  console.info(`The effect modes are: ${audioEffectInfoArray}`);
}).catch((err: BusinessError) => {
  console.error(`getAudioEffectInfoArray :ERROR: ${err}`);
});
```

### getAudioEffectInfoArraySync<sup>10+</sup>

getAudioEffectInfoArraySync(usage: StreamUsage): AudioEffectInfoArray

获取当前音效模式的信息，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名    | 类型                                | 必填     | 说明                         |
| -------- | ----------------------------------- | -------- | --------------------------- |
| usage    | [StreamUsage](#streamusage)         | 是     |  音频流使用类型。               |

**返回值：**

| 类型                                                                      | 说明                                    |
| --------------------------------------------------------------------------| --------------------------------------- |
| [AudioEffectInfoArray](#audioeffectinfoarray10)                  | 返回当前音效模式的信息。      |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let audioEffectInfoArray: audio.AudioEffectInfoArray = audioStreamManager.getAudioEffectInfoArraySync(audio.StreamUsage.STREAM_USAGE_MUSIC);
  console.info(`The effect modes are: ${audioEffectInfoArray}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`getAudioEffectInfoArraySync ERROR: ${error}`);
}
```

## AudioRoutingManager<sup>9+</sup>

音频路由管理。在使用AudioRoutingManager的接口前，需要使用[getRoutingManager](#getroutingmanager9)获取AudioRoutingManager实例。

### getDevices<sup>9+</sup>

getDevices(deviceFlag: DeviceFlag, callback: AsyncCallback&lt;AudioDeviceDescriptors&gt;): void

获取音频设备列表，使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                 |
| ---------- | ------------------------------------------------------------ | ---- | -------------------- |
| deviceFlag | [DeviceFlag](#deviceflag)                                    | 是   | 设备类型的flag。     |
| callback   | AsyncCallback&lt;[AudioDeviceDescriptors](#audiodevicedescriptors)&gt; | 是   | 回调函数。当获取音频设备列表成功，err为undefined，data为获取到的音频设备列表；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRoutingManager.getDevices(audio.DeviceFlag.OUTPUT_DEVICES_FLAG, (err: BusinessError, value: audio.AudioDeviceDescriptors) => {
  if (err) {
    console.error(`Failed to obtain the device list. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate that the device list is obtained.');
});
```

### getDevices<sup>9+</sup>

getDevices(deviceFlag: DeviceFlag): Promise&lt;AudioDeviceDescriptors&gt;

获取音频设备列表，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名     | 类型                      | 必填 | 说明             |
| ---------- | ------------------------- | ---- | ---------------- |
| deviceFlag | [DeviceFlag](#deviceflag) | 是   | 设备类型的flag。 |

**返回值：**

| 类型                                                         | 说明                      |
| ------------------------------------------------------------ | ------------------------- |
| Promise&lt;[AudioDeviceDescriptors](#audiodevicedescriptors)&gt; | Promise对象，返回设备列表。 |

**示例：**

```ts
audioRoutingManager.getDevices(audio.DeviceFlag.OUTPUT_DEVICES_FLAG).then((data: audio.AudioDeviceDescriptors) => {
  console.info('Promise returned to indicate that the device list is obtained.');
});
```

### getDevicesSync<sup>10+</sup>

getDevicesSync(deviceFlag: DeviceFlag): AudioDeviceDescriptors

获取音频设备列表，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名     | 类型                      | 必填 | 说明             |
| ---------- | ------------------------- | ---- | ---------------- |
| deviceFlag | [DeviceFlag](#deviceflag) | 是   | 设备类型的flag。 |

**返回值：**

| 类型                                                         | 说明                      |
| ------------------------------------------------------------ | ------------------------- |
| [AudioDeviceDescriptors](#audiodevicedescriptors) | 返回设备列表。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | invalid parameter error              |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let data: audio.AudioDeviceDescriptors = audioRoutingManager.getDevicesSync(audio.DeviceFlag.OUTPUT_DEVICES_FLAG);
  console.info(`Indicate that the device list is obtained ${data}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`Failed to obtain the device list. ${error}`);
}
```

### on('deviceChange')<sup>9+</sup>

on(type: 'deviceChange', deviceFlag: DeviceFlag, callback: Callback<DeviceChangeAction\>): void

设备更改。音频设备连接状态变化，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名   | 类型                                                 | 必填 | 说明                                       |
| :------- | :--------------------------------------------------- | :--- | :----------------------------------------- |
| type     | string                                               | 是   | 订阅的事件的类型。支持事件：'deviceChange' |
| deviceFlag | [DeviceFlag](#deviceflag)                                    | 是   | 设备类型的flag。     |
| callback | Callback<[DeviceChangeAction](#devicechangeaction)\> | 是   | 回调函数，返回设备更新详情。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. |

**示例：**

```ts
audioRoutingManager.on('deviceChange', audio.DeviceFlag.OUTPUT_DEVICES_FLAG, (deviceChanged: audio.DeviceChangeAction) => {
  console.info('device change type : ' + deviceChanged.type);
  console.info('device descriptor size : ' + deviceChanged.deviceDescriptors.length);
  console.info('device change descriptor : ' + deviceChanged.deviceDescriptors[0].deviceRole);
  console.info('device change descriptor : ' + deviceChanged.deviceDescriptors[0].deviceType);
});
```

### off('deviceChange')<sup>9+</sup>

off(type: 'deviceChange', callback?: Callback<DeviceChangeAction\>): void

取消订阅音频设备连接变化事件，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名   | 类型                                                | 必填 | 说明                                       |
| -------- | --------------------------------------------------- | ---- | ------------------------------------------ |
| type     | string                                              | 是   | 订阅的事件的类型。支持事件：'deviceChange' |
| callback | Callback<[DeviceChangeAction](#devicechangeaction)> | 否   | 回调函数，返回设备更新详情。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. |

**示例：**

```ts
audioRoutingManager.off('deviceChange');
```

### setCommunicationDevice<sup>9+</sup>

setCommunicationDevice(deviceType: CommunicationDeviceType, active: boolean, callback: AsyncCallback&lt;void&gt;): void

设置通信设备激活状态，使用callback方式异步返回结果。

该接口由于功能设计变化，将在后续版本废弃，不建议开发者使用。

**系统能力：** SystemCapability.Multimedia.Audio.Communication

**参数：**

| 参数名     | 类型                                  | 必填 | 说明                      |
| ---------- | ------------------------------------- | ---- |-------------------------|
| deviceType | [CommunicationDeviceType](#communicationdevicetype9) | 是   | 音频设备类型。                 |
| active     | boolean                               | 是   | 设备激活状态，true激活，false未激活。 |
| callback   | AsyncCallback&lt;void&gt;             | 是   | 回调函数。当设置通信设备激活状态成功，err为undefined，否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRoutingManager.setCommunicationDevice(audio.CommunicationDeviceType.SPEAKER, true, (err: BusinessError) => {
  if (err) {
    console.error(`Failed to set the active status of the device. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate that the device is set to the active status.');
});
```

### setCommunicationDevice<sup>9+</sup>

setCommunicationDevice(deviceType: CommunicationDeviceType, active: boolean): Promise&lt;void&gt;

设置通信设备激活状态，使用Promise方式异步返回结果。

该接口由于功能设计变化，将在后续版本废弃，不建议开发者使用。

**系统能力：** SystemCapability.Multimedia.Audio.Communication

**参数：**

| 参数名     | 类型                                                   | 必填 | 说明               |
| ---------- | ----------------------------------------------------- | ---- | ------------------ |
| deviceType | [CommunicationDeviceType](#communicationdevicetype9)  | 是   | 活跃音频设备类型。 |
| active     | boolean                                               | 是   | 设备激活状态，true激活，false未激活。     |

**返回值：**

| 类型                | 说明                            |
| ------------------- | ------------------------------- |
| Promise&lt;void&gt; | Promise对象，无返回结果。 |

**示例：**

```ts
audioRoutingManager.setCommunicationDevice(audio.CommunicationDeviceType.SPEAKER, true).then(() => {
  console.info('Promise returned to indicate that the device is set to the active status.');
});
```

### isCommunicationDeviceActive<sup>9+</sup>

isCommunicationDeviceActive(deviceType: CommunicationDeviceType, callback: AsyncCallback&lt;boolean&gt;): void

获取指定通信设备的激活状态，使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Communication

**参数：**

| 参数名     | 类型                                                  | 必填 | 说明                     |
| ---------- | ---------------------------------------------------- | ---- | ------------------------ |
| deviceType | [CommunicationDeviceType](#communicationdevicetype9) | 是   | 活跃音频设备类型。       |
| callback   | AsyncCallback&lt;boolean&gt;                         | 是   | 回调函数。当获取指定通信设备的激活状态成功，err为undefined，data为true为激活，false为未激活；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRoutingManager.isCommunicationDeviceActive(audio.CommunicationDeviceType.SPEAKER, (err: BusinessError, value: boolean) => {
  if (err) {
    console.error(`Failed to obtain the active status of the device. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate that the active status of the device is obtained.');
});
```

### isCommunicationDeviceActive<sup>9+</sup>

isCommunicationDeviceActive(deviceType: CommunicationDeviceType): Promise&lt;boolean&gt;

获取指定通信设备的激活状态，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Communication

**参数：**

| 参数名     | 类型                                                  | 必填 | 说明               |
| ---------- | ---------------------------------------------------- | ---- | ------------------ |
| deviceType | [CommunicationDeviceType](#communicationdevicetype9) | 是   | 活跃音频设备类型。 |

**返回值：**

| Type                   | Description                     |
| ---------------------- | ------------------------------- |
| Promise&lt;boolean&gt; | Promise对象，返回设备的激活状态，true激活，false未激活。 |

**示例：**

```ts
audioRoutingManager.isCommunicationDeviceActive(audio.CommunicationDeviceType.SPEAKER).then((value: boolean) => {
  console.info(`Promise returned to indicate that the active status of the device is obtained ${value}.`);
});
```

### isCommunicationDeviceActiveSync<sup>10+</sup>

isCommunicationDeviceActiveSync(deviceType: CommunicationDeviceType): boolean

获取指定通信设备的激活状态，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Communication

**参数：**

| 参数名     | 类型                                                  | 必填 | 说明               |
| ---------- | ---------------------------------------------------- | ---- | ------------------ |
| deviceType | [CommunicationDeviceType](#communicationdevicetype9) | 是   | 活跃音频设备类型。 |

**返回值：**

| Type                   | Description                     |
| ---------------------- | ------------------------------- |
| boolean | 返回设备的激活状态，true激活，false未激活。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | invalid parameter error              |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let value: boolean = audioRoutingManager.isCommunicationDeviceActiveSync(audio.CommunicationDeviceType.SPEAKER);
  console.info(`Indicate that the active status of the device is obtained ${value}.`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`Failed to obtain the active status of the device ${error}.`);
}
```

### getPreferOutputDeviceForRendererInfo<sup>10+</sup>

getPreferOutputDeviceForRendererInfo(rendererInfo: AudioRendererInfo, callback: AsyncCallback&lt;AudioDeviceDescriptors&gt;): void

根据音频信息，返回优先级最高的输出设备，使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名                       | 类型                                                         | 必填 | 说明                      |
| --------------------------- | ------------------------------------------------------------ | ---- | ------------------------- |
| rendererInfo                | [AudioRendererInfo](#audiorendererinfo8)                     | 是   | 表示渲染器信息。             |
| callback                    | AsyncCallback&lt;[AudioDeviceDescriptors](#audiodevicedescriptors)&gt;  | 是   | 回调函数。当获取优先级最高的输出设备成功，err为undefined，data为获取到的优先级最高的输出设备信息；否则为错误对象。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息                                           |
| ------- |--------------------------------------------------|
| 6800101 | Input parameter value error. Return by callback. |
| 6800301 | System error. Return by callback.                |

**示例：**
```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';

let rendererInfo: audio.AudioRendererInfo = {
  usage : audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags : 0
}

async function getPreferOutputDevice() {
  audioRoutingManager.getPreferOutputDeviceForRendererInfo(rendererInfo, (err: BusinessError, desc: audio.AudioDeviceDescriptors) => {
    if (err) {
      console.error(`Result ERROR: ${err}`);
    } else {
      console.info(`device descriptor: ${desc}`);
    }
  });
}
```

### getPreferOutputDeviceForRendererInfo<sup>10+</sup>
getPreferOutputDeviceForRendererInfo(rendererInfo: AudioRendererInfo): Promise&lt;AudioDeviceDescriptors&gt;

根据音频信息，返回优先级最高的输出设备，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名                 | 类型                                                         | 必填 | 说明                      |
| ----------------------| ------------------------------------------------------------ | ---- | ------------------------- |
| rendererInfo          | [AudioRendererInfo](#audiorendererinfo8)                     | 是   | 表示渲染器信息。            |

**返回值：**

| 类型                  | 说明                         |
| --------------------- | --------------------------- |
| Promise&lt;[AudioDeviceDescriptors](#audiodevicedescriptors)&gt;   | Promise对象，返回优先级最高的输出设备信息。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息                                          |
| ------- |-------------------------------------------------|
| 6800101 | Input parameter value error. Return by promise. |
| 6800301 | System error. Return by promise.                |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';

let rendererInfo: audio.AudioRendererInfo = {
  usage : audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags : 0
}

async function getPreferOutputDevice() {
  audioRoutingManager.getPreferOutputDeviceForRendererInfo(rendererInfo).then((desc: audio.AudioDeviceDescriptors) => {
    console.info(`device descriptor: ${desc}`);
  }).catch((err: BusinessError) => {
    console.error(`Result ERROR: ${err}`);
  })
}
```

### getPreferredOutputDeviceForRendererInfoSync<sup>10+</sup>
getPreferredOutputDeviceForRendererInfoSync(rendererInfo: AudioRendererInfo): AudioDeviceDescriptors

根据音频信息，返回优先级最高的输出设备，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名                 | 类型                                                         | 必填 | 说明                      |
| ----------------------| ------------------------------------------------------------ | ---- | ------------------------- |
| rendererInfo          | [AudioRendererInfo](#audiorendererinfo8)                     | 是   | 表示渲染器信息。            |

**返回值：**

| 类型                  | 说明                         |
| --------------------- | --------------------------- |
| [AudioDeviceDescriptors](#audiodevicedescriptors)   | 返回优先级最高的输出设备信息。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息                     |
| ------- |--------------------------|
| 6800101 | Invalid parameter error. |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';

let rendererInfo: audio.AudioRendererInfo = {
  usage : audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags : 0
}

try {
  let desc: audio.AudioDeviceDescriptors = audioRoutingManager.getPreferredOutputDeviceForRendererInfoSync(rendererInfo);
  console.info(`device descriptor: ${desc}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`Result ERROR: ${error}`);
}
```

### on('preferOutputDeviceChangeForRendererInfo')<sup>10+</sup>

on(type: 'preferOutputDeviceChangeForRendererInfo', rendererInfo: AudioRendererInfo, callback: Callback<AudioDeviceDescriptors\>): void

订阅最高优先级输出设备变化事件，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名   | 类型                                                 | 必填 | 说明                                                      |
| :------- | :--------------------------------------------------- | :--- |:--------------------------------------------------------|
| type     | string                                               | 是   | 订阅的事件的类型。支持事件：'preferOutputDeviceChangeForRendererInfo' |
| rendererInfo  | [AudioRendererInfo](#audiorendererinfo8)        | 是   | 表示渲染器信息。                                                |
| callback | Callback<[AudioDeviceDescriptors](#audiodevicedescriptors)\> | 是   | 回调函数，返回优先级最高的输出设备信息。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Input parameter value error. |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

let rendererInfo: audio.AudioRendererInfo = {
  usage : audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags : 0
}

audioRoutingManager.on('preferOutputDeviceChangeForRendererInfo', rendererInfo, (desc: audio.AudioDeviceDescriptors) => {
  console.info(`device descriptor: ${desc}`);
});
```

### off('preferOutputDeviceChangeForRendererInfo')<sup>10+</sup>

off(type: 'preferOutputDeviceChangeForRendererInfo', callback?: Callback<AudioDeviceDescriptors\>): void

取消订阅最高优先级输出音频设备变化事件，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名   | 类型                                                | 必填 | 说明                                       |
| -------- | --------------------------------------------------- | ---- | ------------------------------------------ |
| type     | string                                              | 是   | 订阅的事件的类型。支持事件：'preferOutputDeviceChangeForRendererInfo' |
| callback | Callback<[AudioDeviceDescriptors](#audiodevicedescriptors)> | 否   | 回调函数，返回优先级最高的输出设备信息。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Input parameter value error. |

**示例：**

```ts
audioRoutingManager.off('preferOutputDeviceChangeForRendererInfo');
```

### getPreferredInputDeviceForCapturerInfo<sup>10+</sup>

getPreferredInputDeviceForCapturerInfo(capturerInfo: AudioCapturerInfo, callback: AsyncCallback&lt;AudioDeviceDescriptors&gt;): void

根据音频信息，返回优先级最高的输入设备，使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名                       | 类型                                                         | 必填 | 说明                      |
| --------------------------- | ------------------------------------------------------------ | ---- | ------------------------- |
| capturerInfo                | [AudioCapturerInfo](#audiocapturerinfo8)                     | 是   | 表示采集器信息。             |
| callback                    | AsyncCallback&lt;[AudioDeviceDescriptors](#audiodevicedescriptors)&gt;  | 是   | 回调函数。当获取优先级最高的输入设备成功，err为undefined，data为获取到的优先级最高的输入设备信息；否则为错误对象。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. Return by callback.|
| 6800301 | System error. Return by callback.           |

**示例：**
```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';

let capturerInfo: audio.AudioCapturerInfo = {
  source: audio.SourceType.SOURCE_TYPE_MIC,
  capturerFlags: 0
}

audioRoutingManager.getPreferredInputDeviceForCapturerInfo(capturerInfo, (err: BusinessError, desc: audio.AudioDeviceDescriptors) => {
  if (err) {
    console.error(`Result ERROR: ${err}`);
  } else {
    console.info(`device descriptor: ${desc}`);
  }
});
```

### getPreferredInputDeviceForCapturerInfo<sup>10+</sup>

getPreferredInputDeviceForCapturerInfo(capturerInfo: AudioCapturerInfo): Promise&lt;AudioDeviceDescriptors&gt;

根据音频信息，返回优先级最高的输入设备，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名                 | 类型                                                         | 必填 | 说明                      |
| ----------------------| ------------------------------------------------------------ | ---- | ------------------------- |
| capturerInfo          | [AudioCapturerInfo](#audiocapturerinfo8)                     | 是   | 表示采集器信息。            |

**返回值：**

| 类型                  | 说明                         |
| --------------------- | --------------------------- |
| Promise&lt;[AudioDeviceDescriptors](#audiodevicedescriptors)&gt;   | Promise对象，返回优先级最高的输入设备信息。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. Return by promise. |
| 6800301 | System error. Return by promise.            |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';

let capturerInfo: audio.AudioCapturerInfo = {
  source: audio.SourceType.SOURCE_TYPE_MIC,
  capturerFlags: 0
}

audioRoutingManager.getPreferredInputDeviceForCapturerInfo(capturerInfo).then((desc: audio.AudioDeviceDescriptors) => {
  console.info(`device descriptor: ${desc}`);
}).catch((err: BusinessError) => {
  console.error(`Result ERROR: ${err}`);
});
```

### getPreferredInputDeviceForCapturerInfoSync<sup>10+</sup>

getPreferredInputDeviceForCapturerInfoSync(capturerInfo: AudioCapturerInfo): AudioDeviceDescriptors

根据音频信息，返回优先级最高的输入设备，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名                 | 类型                                                         | 必填 | 说明                      |
| ----------------------| ------------------------------------------------------------ | ---- | ------------------------- |
| capturerInfo          | [AudioCapturerInfo](#audiocapturerinfo8)                     | 是   | 表示采集器信息。            |

**返回值：**

| 类型                  | 说明                         |
| --------------------- | --------------------------- |
| [AudioDeviceDescriptors](#audiodevicedescriptors)   | 返回优先级最高的输入设备信息。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';

let capturerInfo: audio.AudioCapturerInfo = {
  source: audio.SourceType.SOURCE_TYPE_MIC,
  capturerFlags: 0
}

try {
  let desc: audio.AudioDeviceDescriptors = audioRoutingManager.getPreferredInputDeviceForCapturerInfoSync(capturerInfo);
  console.info(`device descriptor: ${desc}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`Result ERROR: ${error}`);
}
```

### on('preferredInputDeviceChangeForCapturerInfo')<sup>10+</sup>

on(type: 'preferredInputDeviceChangeForCapturerInfo', capturerInfo: AudioCapturerInfo, callback: Callback<AudioDeviceDescriptors\>): void

订阅最高优先级输入设备变化事件，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名   | 类型                                                 | 必填 | 说明                                       |
| :------- | :--------------------------------------------------- | :--- | :----------------------------------------- |
| type     | string                                               | 是   | 订阅的事件的类型。支持事件：'preferredInputDeviceChangeForCapturerInfo' |
| capturerInfo  | [AudioCapturerInfo](#audiocapturerinfo8)        | 是   | 表示采集器信息。              |
| callback | Callback<[AudioDeviceDescriptors](#audiodevicedescriptors)\> | 是   | 回调函数，返回优先级最高的输入设备信息。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

let capturerInfo: audio.AudioCapturerInfo = {
  source: audio.SourceType.SOURCE_TYPE_MIC,
  capturerFlags: 0
}

audioRoutingManager.on('preferredInputDeviceChangeForCapturerInfo', capturerInfo, (desc: audio.AudioDeviceDescriptors) => {
  console.info(`device descriptor: ${desc}`);
});
```

### off('preferredInputDeviceChangeForCapturerInfo')<sup>10+</sup>

off(type: 'preferredInputDeviceChangeForCapturerInfo', callback?: Callback<AudioDeviceDescriptors\>): void

取消订阅最高优先级输入音频设备变化事件，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名   | 类型                                                | 必填 | 说明                                       |
| -------- | --------------------------------------------------- | ---- | ------------------------------------------ |
| type     | string                                              | 是   | 订阅的事件的类型。支持事件：'preferredInputDeviceChangeForCapturerInfo' |
| callback | Callback<[AudioDeviceDescriptors](#audiodevicedescriptors)> | 否   | 回调函数，返回优先级最高的输入设备信息。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. |

**示例：**

```ts
audioRoutingManager.off('preferredInputDeviceChangeForCapturerInfo');
```

## AudioRendererChangeInfoArray<sup>9+</sup>

数组类型，AudioRenderChangeInfo数组，只读。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

## AudioRendererChangeInfo<sup>9+</sup>

描述音频渲染器更改信息。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

| 名称               | 类型                                       | 可读 | 可写 | 说明                          |
| -------------------| ----------------------------------------- | ---- | ---- | ---------------------------- |
| streamId           | number                                    | 是   | 否   | 音频流唯一id。                |
| rendererInfo       | [AudioRendererInfo](#audiorendererinfo8)  | 是   | 否   | 音频渲染器信息。               |
| deviceDescriptors  | [AudioDeviceDescriptors](#audiodevicedescriptors)      | 是   | 否   | 音频设备描述。|

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

const audioManager = audio.getAudioManager();
let audioStreamManager = audioManager.getStreamManager();

audioStreamManager.on('audioRendererChange',  (AudioRendererChangeInfoArray) => {
  for (let i = 0; i < AudioRendererChangeInfoArray.length; i++) {
    console.info(`## RendererChange on is called for ${i} ##`);
    console.info(`StreamId for ${i} is: ${AudioRendererChangeInfoArray[i].streamId}`);
    console.info(`Content for ${i} is: ${AudioRendererChangeInfoArray[i].rendererInfo.content}`);
    console.info(`Stream for ${i} is: ${AudioRendererChangeInfoArray[i].rendererInfo.usage}`);
    console.info(`Flag ${i} is: ${AudioRendererChangeInfoArray[i].rendererInfo.rendererFlags}`);
    let devDescriptor = AudioRendererChangeInfoArray[i].deviceDescriptors;
    for (let j = 0; j < AudioRendererChangeInfoArray[i].deviceDescriptors.length; j++) {
      console.info(`Id: ${i} : ${AudioRendererChangeInfoArray[i].deviceDescriptors[j].id}`);
      console.info(`Type: ${i} : ${AudioRendererChangeInfoArray[i].deviceDescriptors[j].deviceType}`);
      console.info(`Role: ${i} : ${AudioRendererChangeInfoArray[i].deviceDescriptors[j].deviceRole}`);
      console.info(`Name: ${i} : ${AudioRendererChangeInfoArray[i].deviceDescriptors[j].name}`);
      console.info(`Addr: ${i} : ${AudioRendererChangeInfoArray[i].deviceDescriptors[j].address}`);
      console.info(`SR: ${i} : ${AudioRendererChangeInfoArray[i].deviceDescriptors[j].sampleRates[0]}`);
      console.info(`C ${i} : ${AudioRendererChangeInfoArray[i].deviceDescriptors[j].channelCounts[0]}`);
      console.info(`CM: ${i} : ${AudioRendererChangeInfoArray[i].deviceDescriptors[j].channelMasks[0]}`);
    }
  }
});
```


## AudioCapturerChangeInfoArray<sup>9+</sup>

数组类型，AudioCapturerChangeInfo数组，只读。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

## AudioCapturerChangeInfo<sup>9+</sup>

描述音频采集器更改信息。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

| 名称               | 类型                                       | 可读 | 可写 | 说明                          |
| -------------------| ----------------------------------------- | ---- | ---- | ---------------------------- |
| streamId           | number                                    | 是   | 否   | 音频流唯一id。                |
| capturerInfo       | [AudioCapturerInfo](#audiocapturerinfo8)  | 是   | 否   | 音频采集器信息。               |
| deviceDescriptors  | [AudioDeviceDescriptors](#audiodevicedescriptors)      | 是   | 否   | 音频设备描述。|
| muted<sup>11+</sup>  | boolean    | 是   | 否   | 音频采集器静音状态。true表示音频采集器为静音状态，false表示音频采集器为非静音状态。|

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

const audioManager = audio.getAudioManager();
let audioStreamManager = audioManager.getStreamManager();

audioStreamManager.on('audioCapturerChange', (AudioCapturerChangeInfoArray) =>  {
  for (let i = 0; i < AudioCapturerChangeInfoArray.length; i++) {
    console.info(`## CapChange on is called for element ${i} ##`);
    console.info(`StrId for  ${i} is: ${AudioCapturerChangeInfoArray[i].streamId}`);
    console.info(`Src for ${i} is: ${AudioCapturerChangeInfoArray[i].capturerInfo.source}`);
    console.info(`Flag ${i} is: ${AudioCapturerChangeInfoArray[i].capturerInfo.capturerFlags}`);
    let devDescriptor = AudioCapturerChangeInfoArray[i].deviceDescriptors;
    for (let j = 0; j < AudioCapturerChangeInfoArray[i].deviceDescriptors.length; j++) {
      console.info(`Id: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].id}`);
      console.info(`Type: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].deviceType}`);
      console.info(`Role: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].deviceRole}`);
      console.info(`Name: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].name}`);
      console.info(`Addr: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].address}`);
      console.info(`SR: ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].sampleRates[0]}`);
      console.info(`C ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].channelCounts[0]}`);
      console.info(`CM ${i} : ${AudioCapturerChangeInfoArray[i].deviceDescriptors[j].channelMasks[0]}`);
    }
  }
});
```

## AudioEffectInfoArray<sup>10+</sup>

待查询ContentType和StreamUsage组合场景下的音效模式数组类型，[AudioEffectMode](#audioeffectmode10)数组，只读。

## AudioDeviceDescriptors

设备属性数组类型，为[AudioDeviceDescriptor](#audiodevicedescriptor)的数组，只读。

## AudioDeviceDescriptor

描述音频设备。

| 名称                          | 类型                       | 可读 | 可写 | 说明       |
| ----------------------------- | -------------------------- | ---- | ---- | ---------- |
| deviceRole                    | [DeviceRole](#devicerole)  | 是   | 否   | 设备角色。 <br> **系统能力：** SystemCapability.Multimedia.Audio.Device|
| deviceType                    | [DeviceType](#devicetype)  | 是   | 否   | 设备类型。 <br> **系统能力：** SystemCapability.Multimedia.Audio.Device|
| id<sup>9+</sup>               | number                     | 是   | 否   | 设备id，唯一。  <br> **系统能力：** SystemCapability.Multimedia.Audio.Device|
| name<sup>9+</sup>             | string                     | 是   | 否   | 设备名称。<br>如果是蓝牙设备，需要申请权限ohos.permission.USE_BLUETOOTH。 <br> **系统能力：** SystemCapability.Multimedia.Audio.Device|
| address<sup>9+</sup>          | string                     | 是   | 否   | 设备地址。<br>如果是蓝牙设备，需要申请权限ohos.permission.USE_BLUETOOTH。 <br> **系统能力：** SystemCapability.Multimedia.Audio.Device|
| sampleRates<sup>9+</sup>      | Array&lt;number&gt;        | 是   | 否   | 支持的采样率。 <br> **系统能力：** SystemCapability.Multimedia.Audio.Device|
| channelCounts<sup>9+</sup>    | Array&lt;number&gt;        | 是   | 否   | 支持的通道数。 <br> **系统能力：** SystemCapability.Multimedia.Audio.Device|
| channelMasks<sup>9+</sup>     | Array&lt;number&gt;        | 是   | 否   | 支持的通道掩码。 <br> **系统能力：** SystemCapability.Multimedia.Audio.Device|
| displayName<sup>10+</sup>     | string                     | 是   | 否   | 设备显示名。 <br> **系统能力：** SystemCapability.Multimedia.Audio.Device|
| encodingTypes<sup>11+</sup>    | Array&lt;[AudioEncodingType](#audioencodingtype8)&gt;                     | 是   | 否   | 支持的编码类型。 <br> **系统能力：** SystemCapability.Multimedia.Audio.Core|

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

function displayDeviceProp(value: audio.AudioDeviceDescriptor) {
  deviceRoleValue = value.deviceRole;
  deviceTypeValue = value.deviceType;
}

let deviceRoleValue: audio.DeviceRole | undefined = undefined;;
let deviceTypeValue: audio.DeviceType | undefined = undefined;;
audio.getAudioManager().getDevices(1).then((value: audio.AudioDeviceDescriptors) => {
  console.info('AudioFrameworkTest: Promise: getDevices OUTPUT_DEVICES_FLAG');
  value.forEach(displayDeviceProp);
  if (deviceTypeValue != undefined && deviceRoleValue != undefined){
    console.info('AudioFrameworkTest: Promise: getDevices : OUTPUT_DEVICES_FLAG :  PASS');
  } else {
    console.error('AudioFrameworkTest: Promise: getDevices : OUTPUT_DEVICES_FLAG :  FAIL');
  }
});
```

## AudioRenderer<sup>8+</sup>

提供音频渲染的相关接口。在调用AudioRenderer的接口前，需要先通过[createAudioRenderer](#audiocreateaudiorenderer8)创建实例。

### 属性

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

| 名称  | 类型                     | 可读 | 可写 | 说明               |
| ----- | -------------------------- | ---- | ---- | ------------------ |
| state<sup>8+</sup> | [AudioState](#audiostate8) | 是   | 否   | 音频渲染器的状态。 |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

let state: audio.AudioState = audioRenderer.state;
```

### getRendererInfo<sup>8+</sup>

getRendererInfo(callback: AsyncCallback<AudioRendererInfo\>): void

获取当前被创建的音频渲染器的信息，使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                                                     | 必填 | 说明                   |
| :------- | :------------------------------------------------------- | :--- | :--------------------- |
| callback | AsyncCallback<[AudioRendererInfo](#audiorendererinfo8)\> | 是   | 回调函数。当获取音频渲染器的信息成功，err为undefined，data为获取到的音频渲染器的信息；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getRendererInfo((err: BusinessError, rendererInfo: audio.AudioRendererInfo) => {
  console.info('Renderer GetRendererInfo:');
  console.info(`Renderer content: ${rendererInfo.content}`);
  console.info(`Renderer usage: ${rendererInfo.usage}`);
  console.info(`Renderer flags: ${rendererInfo.rendererFlags}`);
});
```

### getRendererInfo<sup>8+</sup>

getRendererInfo(): Promise<AudioRendererInfo\>

获取当前被创建的音频渲染器的信息，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型                                               | 说明                            |
| -------------------------------------------------- | ------------------------------- |
| Promise<[AudioRendererInfo](#audiorendererinfo8)\> | Promise对象，返回音频渲染器信息。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getRendererInfo().then((rendererInfo: audio.AudioRendererInfo) => {
  console.info('Renderer GetRendererInfo:');
  console.info(`Renderer content: ${rendererInfo.content}`);
  console.info(`Renderer usage: ${rendererInfo.usage}`);
  console.info(`Renderer flags: ${rendererInfo.rendererFlags}`)
}).catch((err: BusinessError) => {
  console.error(`AudioFrameworkRenderLog: RendererInfo :ERROR: ${err}`);
});
```

### getRendererInfoSync<sup>10+</sup>

getRendererInfoSync(): AudioRendererInfo

获取当前被创建的音频渲染器的信息，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型                                               | 说明                            |
| -------------------------------------------------- | ------------------------------- |
| [AudioRendererInfo](#audiorendererinfo8) | 返回音频渲染器信息。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let rendererInfo: audio.AudioRendererInfo = audioRenderer.getRendererInfoSync();
  console.info(`Renderer content: ${rendererInfo.content}`);
  console.info(`Renderer usage: ${rendererInfo.usage}`);
  console.info(`Renderer flags: ${rendererInfo.rendererFlags}`)
} catch (err) {
  let error = err as BusinessError;
  console.error(`AudioFrameworkRenderLog: RendererInfo :ERROR: ${error}`);
}
```

### getStreamInfo<sup>8+</sup>

getStreamInfo(callback: AsyncCallback<AudioStreamInfo\>): void

获取音频流信息，使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                                                 | 必填 | 说明                 |
| :------- | :--------------------------------------------------- | :--- | :------------------- |
| callback | AsyncCallback<[AudioStreamInfo](#audiostreaminfo8)\> | 是   | 回调函数。当获取音频流信息成功，err为undefined，data为获取到的音频流信息；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getStreamInfo((err: BusinessError, streamInfo: audio.AudioStreamInfo) => {
  console.info('Renderer GetStreamInfo:');
  console.info(`Renderer sampling rate: ${streamInfo.samplingRate}`);
  console.info(`Renderer channel: ${streamInfo.channels}`);
  console.info(`Renderer format: ${streamInfo.sampleFormat}`);
  console.info(`Renderer encoding type: ${streamInfo.encodingType}`);
});
```

### getStreamInfo<sup>8+</sup>

getStreamInfo(): Promise<AudioStreamInfo\>

获取音频流信息，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型                                           | 说明                   |
| :--------------------------------------------- | :--------------------- |
| Promise<[AudioStreamInfo](#audiostreaminfo8)\> | Promise对象，返回音频流信息. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getStreamInfo().then((streamInfo: audio.AudioStreamInfo) => {
  console.info('Renderer GetStreamInfo:');
  console.info(`Renderer sampling rate: ${streamInfo.samplingRate}`);
  console.info(`Renderer channel: ${streamInfo.channels}`);
  console.info(`Renderer format: ${streamInfo.sampleFormat}`);
  console.info(`Renderer encoding type: ${streamInfo.encodingType}`);
}).catch((err: BusinessError) => {
  console.error(`ERROR: ${err}`);
});
```

### getStreamInfoSync<sup>10+</sup>

getStreamInfoSync(): AudioStreamInfo

获取音频流信息，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型                                           | 说明                   |
| :--------------------------------------------- | :--------------------- |
| [AudioStreamInfo](#audiostreaminfo8) | 返回音频流信息. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let streamInfo: audio.AudioStreamInfo = audioRenderer.getStreamInfoSync();
  console.info(`Renderer sampling rate: ${streamInfo.samplingRate}`);
  console.info(`Renderer channel: ${streamInfo.channels}`);
  console.info(`Renderer format: ${streamInfo.sampleFormat}`);
  console.info(`Renderer encoding type: ${streamInfo.encodingType}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`ERROR: ${error}`);
}
```

### getAudioStreamId<sup>9+</sup>

getAudioStreamId(callback: AsyncCallback<number\>): void

获取音频流id，使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                                                 | 必填 | 说明                 |
| :------- | :--------------------------------------------------- | :--- | :------------------- |
| callback | AsyncCallback<number\> | 是   | 回调函数。当获取音频流id成功，err为undefined，data为获取到的音频流id；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getAudioStreamId((err: BusinessError, streamId: number) => {
  console.info(`Renderer GetStreamId: ${streamId}`);
});
```

### getAudioStreamId<sup>9+</sup>

getAudioStreamId(): Promise<number\>

获取音频流id，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型                                           | 说明                   |
| :--------------------------------------------- | :--------------------- |
| Promise<number\> | Promise对象，返回音频流id。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getAudioStreamId().then((streamId: number) => {
  console.info(`Renderer getAudioStreamId: ${streamId}`);
}).catch((err: BusinessError) => {
  console.error(`ERROR: ${err}`);
});
```

### getAudioStreamIdSync<sup>10+</sup>

getAudioStreamIdSync(): number

获取音频流id，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型                                           | 说明                   |
| :--------------------------------------------- | :--------------------- |
| number | 返回音频流id。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let streamId: number = audioRenderer.getAudioStreamIdSync();
  console.info(`Renderer getAudioStreamIdSync: ${streamId}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`ERROR: ${error}`);
}
```

### setAudioEffectMode<sup>10+</sup>

setAudioEffectMode(mode: AudioEffectMode, callback: AsyncCallback\<void>): void

设置当前音效模式。使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                                     | 必填 | 说明                     |
| -------- | ---------------------------------------- | ---- | ------------------------ |
| mode     | [AudioEffectMode](#audioeffectmode10)    | 是   | 音效模式。               |
| callback | AsyncCallback\<void>                     | 是   | 回调函数。当设置当前音效模式成功，err为undefined，否则为错误对象。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | ----------------------------------------------|
| 6800101 | Invalid parameter error. Return by callback.  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.setAudioEffectMode(audio.AudioEffectMode.EFFECT_DEFAULT, (err: BusinessError) => {
  if (err) {
    console.error('Failed to set params');
  } else {
    console.info('Callback invoked to indicate a successful audio effect mode setting.');
  }
});
```

### setAudioEffectMode<sup>10+</sup>

setAudioEffectMode(mode: AudioEffectMode): Promise\<void>

设置当前音效模式。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名 | 类型                                     | 必填 | 说明         |
| ------ | ---------------------------------------- | ---- | ------------ |
| mode   | [AudioEffectMode](#audioeffectmode10)   | 是   | 音效模式。 |

**返回值：**

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | Promise对象，无返回结果。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | ---------------------------------------------|
| 6800101 | Invalid parameter error. Return by promise.  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.setAudioEffectMode(audio.AudioEffectMode.EFFECT_DEFAULT).then(() => {
  console.info('setAudioEffectMode SUCCESS');
}).catch((err: BusinessError) => {
  console.error(`ERROR: ${err}`);
});
```

### getAudioEffectMode<sup>10+</sup>

getAudioEffectMode(callback: AsyncCallback\<AudioEffectMode>): void

获取当前音效模式。使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                                                    | 必填 | 说明               |
| -------- | ------------------------------------------------------- | ---- | ------------------ |
| callback | AsyncCallback<[AudioEffectMode](#audioeffectmode10)> | 是   | 回调函数。当获取当前音效模式成功，err为undefined，data为获取到的当前音效模式；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getAudioEffectMode((err: BusinessError, effectMode: audio.AudioEffectMode) => {
  if (err) {
    console.error('Failed to get params');
  } else {
    console.info(`getAudioEffectMode: ${effectMode}`);
  }
});
```

### getAudioEffectMode<sup>10+</sup>

getAudioEffectMode(): Promise\<AudioEffectMode>

获取当前音效模式。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型                                              | 说明                      |
| ------------------------------------------------- | ------------------------- |
| Promise<[AudioEffectMode](#audioeffectmode10)> | Promise对象，返回当前音效模式。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getAudioEffectMode().then((effectMode: audio.AudioEffectMode) => {
  console.info(`getAudioEffectMode: ${effectMode}`);
}).catch((err: BusinessError) => {
  console.error(`ERROR: ${err}`);
});
```

### start<sup>8+</sup>

start(callback: AsyncCallback<void\>): void

启动音频渲染器。使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                 | 必填 | 说明       |
| -------- | -------------------- | ---- | ---------- |
| callback | AsyncCallback\<void> | 是   | 回调函数。当启动音频渲染器成功，err为undefined，否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.start((err: BusinessError) => {
  if (err) {
    console.error('Renderer start failed.');
  } else {
    console.info('Renderer start success.');
  }
});
```

### start<sup>8+</sup>

start(): Promise<void\>

启动音频渲染器。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | Promise对象，无返回结果。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.start().then(() => {
  console.info('Renderer started');
}).catch((err: BusinessError) => {
  console.error(`ERROR: ${err}`);
});
```

### pause<sup>8+</sup>

pause(callback: AsyncCallback\<void>): void

暂停渲染。使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                 | 必填 | 说明             |
| -------- | -------------------- | ---- | ---------------- |
| callback | AsyncCallback\<void> | 是   | 回调函数。当暂停渲染成功，err为undefined，否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.pause((err: BusinessError) => {
  if (err) {
    console.error('Renderer pause failed');
  } else {
    console.info('Renderer paused.');
  }
});
```

### pause<sup>8+</sup>

pause(): Promise\<void>

暂停渲染。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | Promise对象，无返回结果。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.pause().then(() => {
  console.info('Renderer paused');
}).catch((err: BusinessError) => {
  console.error(`ERROR: ${err}`);
});
```

### drain<sup>8+</sup>

drain(callback: AsyncCallback\<void>): void

检查缓冲区是否已被耗尽。使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                 | 必填 | 说明             |
| -------- | -------------------- | ---- | ---------------- |
| callback | AsyncCallback\<void> | 是   | 回调函数。当检查缓冲区是否已被耗尽成功，err为undefined，否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.drain((err: BusinessError) => {
  if (err) {
    console.error('Renderer drain failed');
  } else {
    console.info('Renderer drained.');
  }
});
```

### drain<sup>8+</sup>

drain(): Promise\<void>

检查缓冲区是否已被耗尽。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | Promise对象，无返回结果。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.drain().then(() => {
  console.info('Renderer drained successfully');
}).catch((err: BusinessError) => {
  console.error(`ERROR: ${err}`);
});
```

### flush<sup>11+</sup>

flush(): Promise\<void>

清空缓冲区（[AudioState](#audiostate8)为STATE_RUNNING、STATE_PAUSED、STATE_STOPPED状态下可用）。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | Promise对象，无返回结果。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800103 | Operation not permit at current state. Return by promise. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.flush().then(() => {
  console.info('Renderer flushed successfully');
}).catch((err: BusinessError) => {
  console.error(`ERROR: ${err}`);
});
```

### stop<sup>8+</sup>

stop(callback: AsyncCallback\<void>): void

停止渲染。使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                 | 必填 | 说明             |
| -------- | -------------------- | ---- | ---------------- |
| callback | AsyncCallback\<void> | 是   | 回调函数。当停止渲染成功，err为undefined，否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.stop((err: BusinessError) => {
  if (err) {
    console.error('Renderer stop failed');
  } else {
    console.info('Renderer stopped.');
  }
});
```

### stop<sup>8+</sup>

stop(): Promise\<void>

停止渲染。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | Promise对象，无返回结果。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.stop().then(() => {
  console.info('Renderer stopped successfully');
}).catch((err: BusinessError) => {
  console.error(`ERROR: ${err}`);
});
```

### release<sup>8+</sup>

release(callback: AsyncCallback\<void>): void

释放音频渲染器。使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                 | 必填 | 说明             |
| -------- | -------------------- | ---- | ---------------- |
| callback | AsyncCallback\<void> | 是   | 回调函数。当释放音频渲染器成功，err为undefined，否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.release((err: BusinessError) => {
  if (err) {
    console.error('Renderer release failed');
  } else {
    console.info('Renderer released.');
  }
});
```

### release<sup>8+</sup>

release(): Promise\<void>

释放渲染器。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | Promise对象，无返回结果。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.release().then(() => {
  console.info('Renderer released successfully');
}).catch((err: BusinessError) => {
  console.error(`ERROR: ${err}`);
});
```

### write<sup>8+(deprecated)</sup>

write(buffer: ArrayBuffer, callback: AsyncCallback\<number>): void

写入缓冲区。使用callback方式异步返回结果。

> **说明：**
> 从 API version 8 开始支持，从 API version 11 开始废弃，建议使用AudioRenderer中的[on('writeData')](#onwritedata11)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                   | 必填 | 说明                                                |
| -------- | ---------------------- | ---- | --------------------------------------------------- |
| buffer   | ArrayBuffer            | 是   | 要写入缓冲区的数据。                                |
| callback | AsyncCallback\<number> | 是   | 回调函数。当写入缓冲区成功，err为undefined，data为获取到的写入的字节数；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import fs from '@ohos.file.fs';

let bufferSize: number;
class Options {
  offset?: number;
  length?: number;
}
audioRenderer.getBufferSize().then((data: number)=> {
  console.info(`AudioFrameworkRenderLog: getBufferSize: SUCCESS ${data}`);
  bufferSize = data;
  console.info(`Buffer size: ${bufferSize}`);
  let path = getContext().cacheDir;
  let filePath = path + '/StarWars10s-2C-48000-4SW.wav';
  let file: fs.File = fs.openSync(filePath, fs.OpenMode.READ_ONLY);
  fs.stat(filePath).then(async (stat: fs.Stat) => {
    let buf = new ArrayBuffer(bufferSize);
    let len = stat.size % bufferSize == 0 ? Math.floor(stat.size / bufferSize) : Math.floor(stat.size / bufferSize + 1);
    for (let i = 0;i < len; i++) {
      let options: Options = {
        offset: i * bufferSize,
        length: bufferSize
      }
      let readsize: number = await fs.read(file.fd, buf, options)
      let writeSize: number = await new Promise((resolve,reject)=>{
        audioRenderer.write(buf,(err: BusinessError, writeSize: number)=>{
          if(err){
            reject(err)
          }else{
            resolve(writeSize)
          }
        })
      })
    }
  });
  }).catch((err: BusinessError) => {
    console.error(`AudioFrameworkRenderLog: getBufferSize: ERROR: ${err}`);
});


```

### write<sup>8+(deprecated)</sup>

write(buffer: ArrayBuffer): Promise\<number>

写入缓冲区。使用Promise方式异步返回结果。

> **说明：**
> 从 API version 8 开始支持，从 API version 11 开始废弃，建议使用AudioRenderer中的[on('writeData')](#onwritedata11)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                   | 必填 | 说明                                                |
| -------- | ---------------------- | ---- | --------------------------------------------------- |
| buffer   | ArrayBuffer            | 是   | 要写入缓冲区的数据。                                |

**返回值：**

| 类型             | 说明                                                         |
| ---------------- | ------------------------------------------------------------ |
| Promise\<number> | Promise对象，返回写入的字节数。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import fs from '@ohos.file.fs';

let bufferSize: number;
class Options {
  offset?: number;
  length?: number;
}
audioRenderer.getBufferSize().then((data: number) => {
  console.info(`AudioFrameworkRenderLog: getBufferSize: SUCCESS ${data}`);
  bufferSize = data;
  console.info(`BufferSize: ${bufferSize}`);
  let path = getContext().cacheDir;
  let filePath = path + '/StarWars10s-2C-48000-4SW.wav';
  let file: fs.File = fs.openSync(filePath, fs.OpenMode.READ_ONLY);
  fs.stat(filePath).then(async (stat: fs.Stat) => {
    let buf = new ArrayBuffer(bufferSize);
    let len = stat.size % bufferSize == 0 ? Math.floor(stat.size / bufferSize) : Math.floor(stat.size / bufferSize + 1);
    for (let i = 0;i < len; i++) {
      let options: Options = {
        offset: i * bufferSize,
        length: bufferSize
      }
      let readsize: number = await fs.read(file.fd, buf, options)
      try{
        let writeSize: number = await audioRenderer.write(buf);
      } catch(err) {
        let error = err as BusinessError;
        console.error(`audioRenderer.write err: ${error}`);
      }
    }
  });
}).catch((err: BusinessError) => {
  console.error(`AudioFrameworkRenderLog: getBufferSize: ERROR: ${err}`);
});
```

### getAudioTime<sup>8+</sup>

getAudioTime(callback: AsyncCallback\<number>): void

获取时间戳（从 1970 年 1 月 1 日开始）。使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                   | 必填 | 说明             |
| -------- | ---------------------- | ---- | ---------------- |
| callback | AsyncCallback\<number> | 是   | 回调函数。当获取时间戳成功，err为undefined，data为获取到的时间戳；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getAudioTime((err: BusinessError, timestamp: number) => {
  console.info(`Current timestamp: ${timestamp}`);
});
```

### getAudioTime<sup>8+</sup>

getAudioTime(): Promise\<number>

获取时间戳（从 1970 年 1 月 1 日开始）。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型             | 描述                    |
| ---------------- | ----------------------- |
| Promise\<number> | Promise对象，返回时间戳。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getAudioTime().then((timestamp: number) => {
  console.info(`Current timestamp: ${timestamp}`);
}).catch((err: BusinessError) => {
  console.error(`ERROR: ${err}`);
});
```

### getAudioTimeSync<sup>10+</sup>

getAudioTimeSync(): number

获取时间戳（从 1970 年 1 月 1 日开始），同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型             | 描述                    |
| ---------------- | ----------------------- |
| number | 返回时间戳。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let timestamp: number = audioRenderer.getAudioTimeSync();
  console.info(`Current timestamp: ${timestamp}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`ERROR: ${error}`);
}
```

### getBufferSize<sup>8+</sup>

getBufferSize(callback: AsyncCallback\<number>): void

获取音频渲染器的最小缓冲区大小。使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                   | 必填 | 说明                 |
| -------- | ---------------------- | ---- | -------------------- |
| callback | AsyncCallback\<number> | 是   | 回调函数。当获取音频渲染器的最小缓冲区大小成功，err为undefined，data为获取到的最小缓冲区大小；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let bufferSize: number;
audioRenderer.getBufferSize((err: BusinessError, data: number) => {
  if (err) {
    console.error('getBufferSize error');
  } else {
    console.info(`AudioFrameworkRenderLog: getBufferSize: SUCCESS ${data}`);
    bufferSize = data;
  }
});
```

### getBufferSize<sup>8+</sup>

getBufferSize(): Promise\<number>

获取音频渲染器的最小缓冲区大小。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型             | 说明                        |
| ---------------- | --------------------------- |
| Promise\<number> | Promise对象，返回缓冲区大小。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let bufferSize: number;
audioRenderer.getBufferSize().then((data: number) => {
  console.info(`AudioFrameworkRenderLog: getBufferSize: SUCCESS ${data}`);
  bufferSize = data;
}).catch((err: BusinessError) => {
  console.error(`AudioFrameworkRenderLog: getBufferSize: ERROR: ${err}`);
});
```

### getBufferSizeSync<sup>10+</sup>

getBufferSizeSync(): number

获取音频渲染器的最小缓冲区大小，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型             | 说明                        |
| ---------------- | --------------------------- |
| number | 返回缓冲区大小。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let bufferSize: number = 0;
try {
  bufferSize = audioRenderer.getBufferSizeSync();
  console.info(`AudioFrameworkRenderLog: getBufferSize: SUCCESS ${bufferSize}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`AudioFrameworkRenderLog: getBufferSize: ERROR: ${error}`);
}
```

### setRenderRate<sup>8+(deprecated)</sup>

setRenderRate(rate: AudioRendererRate, callback: AsyncCallback\<void>): void

设置音频渲染速率。使用callback方式异步返回结果。

> **说明：**
> 从 API version 8 开始支持，从 API version 11 开始废弃。建议使用AudioRenderer中的[setSpeed](#setspeed11)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                                     | 必填 | 说明                     |
| -------- | ---------------------------------------- | ---- | ------------------------ |
| rate     | [AudioRendererRate](#audiorendererrate8) | 是   | 渲染的速率。             |
| callback | AsyncCallback\<void>                     | 是   | 回调函数。当设置音频渲染速率成功，err为undefined，否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.setRenderRate(audio.AudioRendererRate.RENDER_RATE_NORMAL, (err: BusinessError) => {
  if (err) {
    console.error('Failed to set params');
  } else {
    console.info('Callback invoked to indicate a successful render rate setting.');
  }
});
```

### setRenderRate<sup>8+(deprecated)</sup>

setRenderRate(rate: AudioRendererRate): Promise\<void>

设置音频渲染速率。使用Promise方式异步返回结果。

> **说明：**
> 从 API version 8 开始支持，从 API version 11 开始废弃。建议使用AudioRenderer中的[setSpeed](#setspeed11)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名 | 类型                                     | 必填 | 说明         |
| ------ | ---------------------------------------- | ---- | ------------ |
| rate   | [AudioRendererRate](#audiorendererrate8) | 是   | 渲染的速率。 |

**返回值：**

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | Promise对象，无返回结果。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.setRenderRate(audio.AudioRendererRate.RENDER_RATE_NORMAL).then(() => {
  console.info('setRenderRate SUCCESS');
}).catch((err: BusinessError) => {
  console.error(`ERROR: ${err}`);
});
```

### setSpeed<sup>11+</sup>

setSpeed(speed: number): void

设置播放倍速。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名 | 类型                                     | 必填 | 说明                   |
| ------ | ---------------------------------------- | ---- |----------------------|
| speed | number | 是   | 设置播放的倍速值（倍速范围：0.25-4.0）。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Input parameter value error. |

**示例：**

```ts
audioRenderer.setSpeed(1.5);
```

### getRenderRate<sup>8+(deprecated)</sup>

getRenderRate(callback: AsyncCallback\<AudioRendererRate>): void

获取当前渲染速率。使用callback方式异步返回结果。

> **说明：**
> 从 API version 8 开始支持，从 API version 11 开始废弃。建议使用AudioRenderer中的[getSpeed](#getspeed11)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                                                    | 必填 | 说明               |
| -------- | ------------------------------------------------------- | ---- | ------------------ |
| callback | AsyncCallback<[AudioRendererRate](#audiorendererrate8)> | 是   | 回调函数。当获取当前渲染速率成功，err为undefined，data为获取到的当前渲染速率；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getRenderRate((err: BusinessError, renderRate: audio.AudioRendererRate) => {
  console.info(`getRenderRate: ${renderRate}`);
});
```

### getRenderRate<sup>8+(deprecated)</sup>

getRenderRate(): Promise\<AudioRendererRate>

获取当前渲染速率。使用Promise方式异步返回结果。

> **说明：**
> 从 API version 8 开始支持，从 API version 11 开始废弃。建议使用AudioRenderer中的[getSpeed](#getspeed11)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型                                              | 说明                      |
| ------------------------------------------------- | ------------------------- |
| Promise<[AudioRendererRate](#audiorendererrate8)> | Promise对象，返回渲染速率。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getRenderRate().then((renderRate: audio.AudioRendererRate) => {
  console.info(`getRenderRate: ${renderRate}`);
}).catch((err: BusinessError) => {
  console.error(`ERROR: ${err}`);
});
```

### getRenderRateSync<sup>10+(deprecated)</sup>

getRenderRateSync(): AudioRendererRate

获取当前渲染速率，同步返回结果。

> **说明：**
> 从 API version 10 开始支持，从 API version 11 开始废弃。建议使用AudioRenderer中的[getSpeed](#getspeed11)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型                                              | 说明                      |
| ------------------------------------------------- | ------------------------- |
| [AudioRendererRate](#audiorendererrate8) | 返回渲染速率。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let renderRate: audio.AudioRendererRate = audioRenderer.getRenderRateSync();
  console.info(`getRenderRate: ${renderRate}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`ERROR: ${error}`);
}
```

### getSpeed<sup>11+</sup>

getSpeed(): number

获取播放倍速。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型                                              | 说明        |
| ------------------------------------------------- |-----------|
| number | 返回播放的倍速值。 |

**示例：**

```ts
let speed = audioRenderer.getSpeed();
```

### setInterruptMode<sup>9+</sup>

setInterruptMode(mode: InterruptMode): Promise&lt;void&gt;

设置应用的焦点模型。使用Promise异步回调。

**系统能力：** SystemCapability.Multimedia.Audio.Interrupt

**参数：**

| 参数名     | 类型                                | 必填   | 说明        |
| ---------- | ---------------------------------- | ------ | ---------- |
| mode       | [InterruptMode](#interruptmode9)    | 是     | 焦点模型。  |

**返回值：**

| 类型                | 说明                          |
| ------------------- | ----------------------------- |
| Promise&lt;void&gt; | Promise对象，无返回结果。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let mode = 0;
audioRenderer.setInterruptMode(mode).then(() => {
  console.info('setInterruptMode Success!');
}).catch((err: BusinessError) => {
  console.error(`setInterruptMode Fail: ${err}`);
});
```
### setInterruptMode<sup>9+</sup>

setInterruptMode(mode: InterruptMode, callback: AsyncCallback\<void>): void

设置应用的焦点模型。使用Callback回调返回执行结果。

**系统能力：** SystemCapability.Multimedia.Audio.Interrupt

**参数：**

| 参数名   | 类型                                | 必填   | 说明            |
| ------- | ----------------------------------- | ------ | -------------- |
|mode     | [InterruptMode](#interruptmode9)     | 是     | 焦点模型。|
|callback | AsyncCallback\<void>                 | 是     |回调函数。当设置应用的焦点模型成功，err为undefined，否则为错误对象。|

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let mode = 1;
audioRenderer.setInterruptMode(mode, (err: BusinessError) => {
  if(err){
    console.error(`setInterruptMode Fail: ${err}`);
  }
  console.info('setInterruptMode Success!');
});
```

### setInterruptModeSync<sup>10+</sup>

setInterruptModeSync(mode: InterruptMode): void

设置应用的焦点模型，同步设置。

**系统能力：** SystemCapability.Multimedia.Audio.Interrupt

**参数：**

| 参数名     | 类型                                | 必填   | 说明        |
| ---------- | ---------------------------------- | ------ | ---------- |
| mode       | [InterruptMode](#interruptmode9)    | 是     | 焦点模型。  |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | invalid parameter error              |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  audioRenderer.setInterruptModeSync(0);
  console.info('setInterruptMode Success!');
} catch (err) {
  let error = err as BusinessError;
  console.error(`setInterruptMode Fail: ${error}`);
}
```

### setVolume<sup>9+</sup>

setVolume(volume: number): Promise&lt;void&gt;

设置应用的音量。使用Promise异步回调。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名     | 类型    | 必填   | 说明                 |
| ---------- | ------- | ------ | ------------------- |
| volume     | number  | 是     | 音量值范围为0.0-1.0。 |

**返回值：**

| 类型                | 说明                          |
| ------------------- | ----------------------------- |
| Promise&lt;void&gt; | Promise对象，无返回结果。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.setVolume(0.5).then(() => {
  console.info('setVolume Success!');
}).catch((err: BusinessError) => {
  console.error(`setVolume Fail: ${err}`);
});
```
### setVolume<sup>9+</sup>

setVolume(volume: number, callback: AsyncCallback\<void>): void

设置应用的音量。使用Callback回调返回执行结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名  | 类型       | 必填   | 说明                 |
| ------- | -----------| ------ | ------------------- |
|volume   | number     | 是     | 音量值范围为0.0-1.0。 |
|callback | AsyncCallback\<void> | 是     |回调函数。当设置应用的音量成功，err为undefined，否则为错误对象。|

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.setVolume(0.5, (err: BusinessError) => {
  if(err){
    console.error(`setVolume Fail: ${err}`);
    return;
  }
  console.info('setVolume Success!');
});
```

### getMinStreamVolume<sup>10+</sup>

getMinStreamVolume(callback: AsyncCallback&lt;number&gt;): void

获取应用基于音频流的最小音量。使用Callback回调返回。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名  | 类型       | 必填   | 说明                 |
| ------- | -----------| ------ | ------------------- |
|callback |AsyncCallback&lt;number&gt; | 是     |回调函数。当获取应用基于音频流的最小音量成功，err为undefined，data为获取到的应用基于音频流的最小音量（音量范围0-1）；否则为错误对象。|

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getMinStreamVolume((err: BusinessError, minVolume: number) => {
  if (err) {
    console.error(`getMinStreamVolume error: ${err}`);
  } else {
    console.info(`getMinStreamVolume Success! ${minVolume}`);
  }
});
```
### getMinStreamVolume<sup>10+</sup>

getMinStreamVolume(): Promise&lt;number&gt;

获取应用基于音频流的最小音量。使用Promise异步回调。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型                | 说明                          |
| ------------------- | ----------------------------- |
| Promise&lt;number&gt;| Promise对象，返回音频流最小音量（音量范围0-1）。|

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getMinStreamVolume().then((value: number) => {
  console.info(`Get min stream volume Success! ${value}`);
}).catch((err: BusinessError) => {
  console.error(`Get min stream volume Fail: ${err}`);
});
```

### getMinStreamVolumeSync<sup>10+</sup>

getMinStreamVolumeSync(): number

获取应用基于音频流的最小音量，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型                | 说明                          |
| ------------------- | ----------------------------- |
| number| 返回音频流最小音量（音量范围0-1）。|

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let value: number = audioRenderer.getMinStreamVolumeSync();
  console.info(`Get min stream volume Success! ${value}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`Get min stream volume Fail: ${error}`);
}
```

### getMaxStreamVolume<sup>10+</sup>

getMaxStreamVolume(callback: AsyncCallback&lt;number&gt;): void

获取应用基于音频流的最大音量。使用Callback回调返回。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名  | 类型       | 必填   | 说明                 |
| ------- | -----------| ------ | ------------------- |
|callback | AsyncCallback&lt;number&gt; | 是     |回调函数。当获取应用基于音频流的最大音量成功，err为undefined，data为获取到的应用基于音频流的最大音量（音量范围0-1）；否则为错误对象。|

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getMaxStreamVolume((err: BusinessError, maxVolume: number) => {
  if (err) {
    console.error(`getMaxStreamVolume Fail: ${err}`);
  } else {
    console.info(`getMaxStreamVolume Success! ${maxVolume}`);
  }
});
```
### getMaxStreamVolume<sup>10+</sup>

getMaxStreamVolume(): Promise&lt;number&gt;

获取应用基于音频流的最大音量。使用Promise异步回调。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型                | 说明                          |
| ------------------- | ----------------------------- |
| Promise&lt;number&gt;| Promise对象，返回音频流最大音量（音量范围0-1）。|

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getMaxStreamVolume().then((value: number) => {
  console.info(`Get max stream volume Success! ${value}`);
}).catch((err: BusinessError) => {
  console.error(`Get max stream volume Fail: ${err}`);
});
```

### getMaxStreamVolumeSync<sup>10+</sup>

getMaxStreamVolumeSync(): number

获取应用基于音频流的最大音量，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型                | 说明                          |
| ------------------- | ----------------------------- |
| number| 返回音频流最大音量（音量范围0-1）。|

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let value: number = audioRenderer.getMaxStreamVolumeSync();
  console.info(`Get max stream volume Success! ${value}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`Get max stream volume Fail: ${error}`);
}
```

### getUnderflowCount<sup>10+</sup>

getUnderflowCount(callback: AsyncCallback&lt;number&gt;): void

获取当前播放音频流的欠载音频帧数量。使用Callback回调返回。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名  | 类型       | 必填   | 说明                 |
| ------- | -----------| ------ | ------------------- |
|callback | AsyncCallback&lt;number&gt; | 是     |回调函数。当获取当前播放音频流的欠载音频帧数量成功，err为undefined，data为获取到的当前播放音频流的欠载音频帧数量；否则为错误对象。|

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getUnderflowCount((err: BusinessError, underflowCount: number) => {
  if (err) {
    console.error(`getUnderflowCount Fail: ${err}`);
  } else {
    console.info(`getUnderflowCount Success! ${underflowCount}`);
  }
});
```
### getUnderflowCount<sup>10+</sup>

getUnderflowCount(): Promise&lt;number&gt;

获取当前播放音频流的欠载音频帧数量。使用Promise异步回调。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型                | 说明                          |
| ------------------- | ----------------------------- |
| Promise&lt;number&gt;| Promise对象，返回音频流的欠载音频帧数量。|

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getUnderflowCount().then((value: number) => {
  console.info(`Get underflow count Success! ${value}`);
}).catch((err: BusinessError) => {
  console.error(`Get underflow count Fail: ${err}`);
});
```

### getUnderflowCountSync<sup>10+</sup>

getUnderflowCountSync(): number

获取当前播放音频流的欠载音频帧数量，同步返回数据。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**返回值：**

| 类型                | 说明                          |
| ------------------- | ----------------------------- |
| number| 返回音频流的欠载音频帧数量。|

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let value: number = audioRenderer.getUnderflowCountSync();
  console.info(`Get underflow count Success! ${value}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`Get underflow count Fail: ${error}`);
}
```

### getCurrentOutputDevices<sup>10+</sup>

getCurrentOutputDevices(callback: AsyncCallback&lt;AudioDeviceDescriptors&gt;): void

获取音频流输出设备描述符。使用Callback回调返回。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名  | 类型       | 必填   | 说明                 |
| ------- | -----------| ------ | ------------------- |
|callback | AsyncCallback\<[AudioDeviceDescriptors](#audiodevicedescriptors)>| 是     |回调函数。当获取音频流输出设备描述符成功，err为undefined，data为获取到的音频流输出设备描述符；否则为错误对象。|

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getCurrentOutputDevices((err: BusinessError, deviceInfo: audio.AudioDeviceDescriptors) => {
  if (err) {
    console.error(`getCurrentOutputDevices Fail: ${err}`);
  } else {
    for (let i = 0; i < deviceInfo.length; i++) {
      console.info(`DeviceInfo id: ${deviceInfo[i].id}`);
      console.info(`DeviceInfo type: ${deviceInfo[i].deviceType}`);
      console.info(`DeviceInfo role: ${deviceInfo[i].deviceRole}`);
      console.info(`DeviceInfo name: ${deviceInfo[i].name}`);
      console.info(`DeviceInfo address: ${deviceInfo[i].address}`);
      console.info(`DeviceInfo samplerate: ${deviceInfo[i].sampleRates[0]}`);
      console.info(`DeviceInfo channelcount: ${deviceInfo[i].channelCounts[0]}`);
      console.info(`DeviceInfo channelmask: ${deviceInfo[i].channelMasks[0]}`);
    }
  }
});
```
### getCurrentOutputDevices<sup>10+</sup>

getCurrentOutputDevices(): Promise&lt;AudioDeviceDescriptors&gt;

获取音频流输出设备描述符。使用Promise异步回调。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**返回值：**

| 类型                | 说明                          |
| ------------------- | ----------------------------- |
| Promise&lt;[AudioDeviceDescriptors](#audiodevicedescriptors)&gt;| Promise对象，返回音频流的输出设备描述信息 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioRenderer.getCurrentOutputDevices().then((deviceInfo: audio.AudioDeviceDescriptors) => {
  for (let i = 0; i < deviceInfo.length; i++) {
    console.info(`DeviceInfo id: ${deviceInfo[i].id}`);
    console.info(`DeviceInfo type: ${deviceInfo[i].deviceType}`);
    console.info(`DeviceInfo role: ${deviceInfo[i].deviceRole}`);
    console.info(`DeviceInfo name: ${deviceInfo[i].name}`);
    console.info(`DeviceInfo address: ${deviceInfo[i].address}`);
    console.info(`DeviceInfo samplerate: ${deviceInfo[i].sampleRates[0]}`);
    console.info(`DeviceInfo channelcount: ${deviceInfo[i].channelCounts[0]}`);
    console.info(`DeviceInfo channelmask: ${deviceInfo[i].channelMasks[0]}`);
  }
}).catch((err: BusinessError) => {
  console.error(`Get current output devices Fail: ${err}`);
});
```

### getCurrentOutputDevicesSync<sup>10+</sup>

getCurrentOutputDevicesSync(): AudioDeviceDescriptors

获取音频流输出设备描述符，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**返回值：**

| 类型                | 说明                          |
| ------------------- | ----------------------------- |
| [AudioDeviceDescriptors](#audiodevicedescriptors) | 返回音频流的输出设备描述信息 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let deviceInfo: audio.AudioDeviceDescriptors = audioRenderer.getCurrentOutputDevicesSync();
  for (let i = 0; i < deviceInfo.length; i++) {
    console.info(`DeviceInfo id: ${deviceInfo[i].id}`);
    console.info(`DeviceInfo type: ${deviceInfo[i].deviceType}`);
    console.info(`DeviceInfo role: ${deviceInfo[i].deviceRole}`);
    console.info(`DeviceInfo name: ${deviceInfo[i].name}`);
    console.info(`DeviceInfo address: ${deviceInfo[i].address}`);
    console.info(`DeviceInfo samplerate: ${deviceInfo[i].sampleRates[0]}`);
    console.info(`DeviceInfo channelcount: ${deviceInfo[i].channelCounts[0]}`);
    console.info(`DeviceInfo channelmask: ${deviceInfo[i].channelMasks[0]}`);
  }
} catch (err) {
  let error = err as BusinessError;
  console.error(`Get current output devices Fail: ${error}`);
}
```
### setChannelBlendMode<sup>11+</sup>

setChannelBlendMode(mode: ChannelBlendMode): void

设置单双声道混合模式。使用同步方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名     | 类型                                | 必填 | 说明                                                     |
| ---------- | ----------------------------------- | ---- | -------------------------------------------------------- |
| mode | [ChannelBlendMode](#channelblendmode11) | 是   | 声道混合模式类型。                                             |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Input parameter value error.              |
| 6800103 | Operation not permit at current state.    |

**示例：**

```ts
let mode = audio.ChannelBlendMode.MODE_DEFAULT;

audioRenderer.setChannelBlendMode(mode);
console.info(`BlendMode: ${mode}`);
```
### setVolumeWithRamp<sup>11+</sup>

setVolumeWithRamp(volume: number, duration: number): void

设置音量渐变模式。使用同步方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名     | 类型                                | 必填 | 说明                                                     |
| ---------- | ----------------------------------- | ---- | -------------------------------------------------------- |
| volume     | number | 是   | 渐变目标音量值，音量范围为[0.0, 1.0]。                                             |
| duration     | number | 是   | 渐变持续时间，单位为ms。                                             |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Input parameter value error.              |
| 401 | Input parameter type or number mismatch.    |

**示例：**

```ts
let volume = 0.5;
let duration = 1000;

audioRenderer.setVolumeWithRamp(volume, duration);
console.info(`setVolumeWithRamp: ${volume}`);
```

### on('audioInterrupt')<sup>9+</sup>

on(type: 'audioInterrupt', callback: Callback\<InterruptEvent>): void

监听音频中断事件，使用callback方式返回结果。

与[on('interrupt')](#oninterruptdeprecated)一致，均用于监听焦点变化。AudioRenderer对象在start事件发生时会主动获取焦点，在pause、stop等事件发生时会主动释放焦点，不需要开发者主动发起获取焦点或释放焦点的申请。

**系统能力：** SystemCapability.Multimedia.Audio.Interrupt

**参数：**

| 参数名   | 类型                                         | 必填 | 说明                                                         |
| -------- | -------------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                                       | 是   | 事件回调类型，支持的事件为：'audioInterrupt'（中断事件被触发，音频渲染被中断。） |
| callback | Callback\<[InterruptEvent](#interruptevent9)\> | 是   | 回调函数，返回播放中断时，应用接收的中断事件信息。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

let isPlaying: boolean; // 标识符，表示是否正在渲染
let isDucked: boolean; // 标识符，表示是否被降低音量
onAudioInterrupt();

async function onAudioInterrupt(){
  audioRenderer.on('audioInterrupt', (interruptEvent: audio.InterruptEvent) => {
    if (interruptEvent.forceType == audio.InterruptForceType.INTERRUPT_FORCE) {
      // 由系统进行操作，强制打断音频渲染，应用需更新自身状态及显示内容等
      switch (interruptEvent.hintType) {
        case audio.InterruptHint.INTERRUPT_HINT_PAUSE:
          // 音频流已被暂停，临时失去焦点，待可重获焦点时会收到resume对应的interruptEvent
          console.info('Force paused. Update playing status and stop writing');
          isPlaying = false; // 简化处理，代表应用切换至暂停状态的若干操作
          break;
        case audio.InterruptHint.INTERRUPT_HINT_STOP:
          // 音频流已被停止，永久失去焦点，若想恢复渲染，需用户主动触发
          console.info('Force stopped. Update playing status and stop writing');
          isPlaying = false; // 简化处理，代表应用切换至暂停状态的若干操作
          break;
        case audio.InterruptHint.INTERRUPT_HINT_DUCK:
          // 音频流已被降低音量渲染
          console.info('Force ducked. Update volume status');
          isDucked = true; // 简化处理，代表应用更新音量状态的若干操作
          break;
        case audio.InterruptHint.INTERRUPT_HINT_UNDUCK:
          // 音频流已被恢复正常音量渲染
          console.info('Force ducked. Update volume status');
          isDucked = false; // 简化处理，代表应用更新音量状态的若干操作
          break;
        default:
          console.info('Invalid interruptEvent');
          break;
      }
    } else if (interruptEvent.forceType == audio.InterruptForceType.INTERRUPT_SHARE) {
      // 由应用进行操作，应用可以自主选择打断或忽略
      switch (interruptEvent.hintType) {
        case audio.InterruptHint.INTERRUPT_HINT_RESUME:
          // 建议应用继续渲染（说明音频流此前被强制暂停，临时失去焦点，现在可以恢复渲染）
          console.info('Resume force paused renderer or ignore');
          // 若选择继续渲染，需在此处主动执行开始渲染的若干操作
          break;
        case audio.InterruptHint.INTERRUPT_HINT_PAUSE:
          // 建议应用暂停渲染
          console.info('Choose to pause or ignore');
          // 若选择暂停渲染，需在此处主动执行暂停渲染的若干操作
          break;
        case audio.InterruptHint.INTERRUPT_HINT_STOP:
          // 建议应用停止渲染
          console.info('Choose to stop or ignore');
          // 若选择停止渲染，需在此处主动执行停止渲染的若干操作
          break;
        case audio.InterruptHint.INTERRUPT_HINT_DUCK:
          // 建议应用降低音量渲染
          console.info('Choose to duck or ignore');
          // 若选择降低音量渲染，需在此处主动执行降低音量渲染的若干操作
          break;
        case audio.InterruptHint.INTERRUPT_HINT_UNDUCK:
          // 建议应用恢复正常音量渲染
          console.info('Choose to unduck or ignore');
          // 若选择恢复正常音量渲染，需在此处主动执行恢复正常音量渲染的若干操作
          break;
        default:
          break;
      }
    }
  });
}
```

### on('markReach')<sup>8+</sup>

on(type: 'markReach', frame: number, callback: Callback&lt;number&gt;): void

订阅到达标记的事件。 当渲染的帧数达到 frame 参数的值时，回调被调用，使用callback方式返回结果。

**系统能力:** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                     | 必填 | 说明                                      |
| :------- | :----------------------- | :--- | :---------------------------------------- |
| type     | string                   | 是   | 事件回调类型，支持的事件为：'markReach'。 |
| frame    | number                   | 是   | 触发事件的帧数。 该值必须大于 0。         |
| callback | Callback\<number>         | 是   | 回调函数，返回frame 参数的值 |

**示例：**

```ts
audioRenderer.on('markReach', 1000, (position: number) => {
  if (position == 1000) {
    console.info('ON Triggered successfully');
  }
});
```


### off('markReach') <sup>8+</sup>

off(type: 'markReach'): void

取消订阅标记事件。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                              |
| :----- | :----- | :--- | :------------------------------------------------ |
| type   | string | 是   | 要取消订阅事件的类型。支持的事件为：'markReach'。 |

**示例：**

```ts
audioRenderer.off('markReach');
```

### on('periodReach') <sup>8+</sup>

on(type: 'periodReach', frame: number, callback: Callback&lt;number&gt;): void

订阅到达标记的事件。 当渲染的帧数达到 frame 参数的值时，触发回调并返回设定的值，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                     | 必填 | 说明                                        |
| :------- | :----------------------- | :--- | :------------------------------------------ |
| type     | string                   | 是   | 事件回调类型，支持的事件为：'periodReach'。 |
| frame    | number                   | 是   | 触发事件的帧数。 该值必须大于 0。           |
| callback | Callback\<number>         | 是   | 回调函数，返回frame 参数的值 |

**示例：**

```ts
audioRenderer.on('periodReach', 1000, (position: number) => {
  if (position == 1000) {
    console.info('ON Triggered successfully');
  }
});
```

### off('periodReach') <sup>8+</sup>

off(type: 'periodReach'): void

取消订阅标记事件。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                |
| :----- | :----- | :--- | :-------------------------------------------------- |
| type   | string | 是   | 要取消订阅事件的类型。支持的事件为：'periodReach'。 |

**示例：**

```ts
audioRenderer.off('periodReach');
```

### on('stateChange') <sup>8+</sup>

on(type: 'stateChange', callback: Callback<AudioState\>): void

订阅监听状态变化，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                       | 必填 | 说明                                        |
| :------- | :------------------------- | :--- | :------------------------------------------ |
| type     | string                     | 是   | 事件回调类型，支持的事件为：'stateChange'。 |
| callback | Callback\<[AudioState](#audiostate8)> | 是   | 回调函数，返回当前音频的状态。 |

**示例：**

```ts
audioRenderer.on('stateChange', (state: audio.AudioState) => {
  if (state == 1) {
    console.info('audio renderer state is: STATE_PREPARED');
  }
  if (state == 2) {
    console.info('audio renderer state is: STATE_RUNNING');
  }
});
```

### on('outputDeviceChange') <sup>10+</sup>

on(type: 'outputDeviceChange', callback: Callback\<AudioDeviceDescriptors>): void

订阅监听音频输出设备变化，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名   | 类型                       | 必填 | 说明                                        |
| :------- | :------------------------- | :--- | :------------------------------------------ |
| type     | string                     | 是   | 事件回调类型，支持的事件为：'outputDeviceChange'。 |
| callback | Callback\<[AudioDeviceDescriptors](#audiodevicedescriptors)> | 是   | 回调函数，返回当前音频流的输出设备描述信息。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. |

**示例：**

```ts
audioRenderer.on('outputDeviceChange', (deviceInfo: audio.AudioDeviceDescriptors) => {
  console.info(`DeviceInfo id: ${deviceInfo[0].id}`);
  console.info(`DeviceInfo name: ${deviceInfo[0].name}`);
  console.info(`DeviceInfo address: ${deviceInfo[0].address}`);
});
```

### off('outputDeviceChange') <sup>10+</sup>

off(type: 'outputDeviceChange', callback?: Callback\<AudioDeviceDescriptors>): void

取消订阅监听音频输出设备变化，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名   | 类型                       | 必填 | 说明                                        |
| :------- | :------------------------- | :--- | :------------------------------------------ |
| type     | string                     | 是   | 事件回调类型，支持的事件为：'outputDeviceChange'。 |
| callback | Callback\<[AudioDeviceDescriptors](#audiodevicedescriptors)> | 否   | 回调函数，返回当前音频流的输出设备描述信息。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. |

**示例：**

```ts
audioRenderer.off('outputDeviceChange', (deviceInfo: audio.AudioDeviceDescriptors) => {
  console.info(`DeviceInfo id: ${deviceInfo[0].id}`);
  console.info(`DeviceInfo name: ${deviceInfo[0].name}`);
  console.info(`DeviceInfo address: ${deviceInfo[0].address}`);
});
```

### on('outputDeviceChangeWithInfo') <sup>11+</sup>

on(type: 'outputDeviceChangeWithInfo', callback: Callback\<AudioStreamDeviceChangeInfo>): void

订阅监听音频流输出设备变化及原因，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名   | 类型                                                                       | 必填 | 说明                                          |
| :------- |:-------------------------------------------------------------------------| :--- |:--------------------------------------------|
| type     | string                                                                   | 是   | 事件回调类型，支持的事件为：'outputDeviceChangeWithInfo'。 |
| callback | Callback\<[AudioStreamDeviceChangeInfo](#audiostreamdevicechangeinfo11)> | 是   | 回调函数，返回当前音频流的输出设备描述信息及变化原因。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | if input parameter value error. |

**示例：**

```ts
audioRenderer.on('outputDeviceChangeWithInfo', (deviceChangeInfo: audio.AudioStreamDeviceChangeInfo) => {
  console.info(`DeviceInfo id: ${deviceChangeInfo.devices[0].id}`);
  console.info(`DeviceInfo name: ${deviceChangeInfo.devices[0].name}`);
  console.info(`DeviceInfo address: ${deviceChangeInfo.devices[0].address}`);
  console.info(`Device change reason: ${deviceChangeInfo.changeReason}`);
});
```

### off('outputDeviceChangeWithInfo') <sup>11+</sup>

off(type: 'outputDeviceChangeWithInfo', callback?: Callback\<AudioStreamDeviceChangeInfo>): void

取消订阅监听音频流输出设备变化及原因，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名   | 类型                                                                       | 必填 | 说明                                          |
| :------- |:-------------------------------------------------------------------------| :--- |:--------------------------------------------|
| type     | string                                                                   | 是   | 事件回调类型，支持的事件为：'outputDeviceChangeWithInfo'。 |
| callback | Callback\<[AudioStreamDeviceChangeInfo](#audiostreamdevicechangeinfo11)> | 否   | 回调函数，返回当前音频流的输出设备描述信息及变化原因。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | if input parameter value error. |

**示例：**

```ts
audioRenderer.off('outputDeviceChangeWithInfo', (deviceChangeInfo: audio.AudioStreamDeviceChangeInfo) => {
  console.info(`DeviceInfo id: ${deviceChangeInfo.devices[0].id}`);
  console.info(`DeviceInfo name: ${deviceChangeInfo.devices[0].name}`);
  console.info(`DeviceInfo address: ${deviceChangeInfo.devices[0].address}`);
  console.info(`Device change reason: ${deviceChangeInfo.changeReason}`);
});
```

### on('writeData')<sup>11+</sup>

on(type: 'writeData', callback: Callback\<ArrayBuffer>): void

订阅监听音频数据写入回调，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                     | 必填 | 说明                         |
| :------- |:-----------------------| :--- |:---------------------------|
| type     | string                 | 是   | 事件回调类型，支持的事件为：'writeData'。 |
| callback | Callback\<ArrayBuffer> | 是   | 回调函数，返回待写入的数据缓冲区。            |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Input parameter value error. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import fs from '@ohos.file.fs';

let bufferSize: number = 0;
class Options {
  offset?: number;
  length?: number;
}

let writeDataCallback = (buffer: ArrayBuffer) => {
  let path = getContext().cacheDir;
  //确保该路径下存在该资源
  let filePath = path + '/StarWars10s-2C-48000-4SW.wav';
  let file: fs.File = fs.openSync(filePath, fs.OpenMode.READ_ONLY);
  let options: Options = {
    offset: bufferSize,
    length: buffer.byteLength
  }
  fs.readSync(file.fd, buffer, options);
  bufferSize += buffer.byteLength;
}

audioRenderer.on('writeData', writeDataCallback);
audioRenderer.start().then(() => {
  console.info('Renderer started');
}).catch((err: BusinessError) => {
  console.error(`ERROR: ${err}`);
});
```

### off('writeData')<sup>11+</sup>

off(type: 'writeData', callback?: Callback\<ArrayBuffer>): void

取消订阅监听音频数据写入回调，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

**参数：**

| 参数名   | 类型                     | 必填 | 说明                                         |
| :------- |:-----------------------| :--- |:-------------------------------------------|
| type     | string                 | 是   | 事件回调类型，支持的事件为：'writeData'。                 |
| callback | Callback\<ArrayBuffer> | 否   | 回调函数，返回待写入的数据缓冲区。                            |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Input parameter value error. |

**示例：**

```ts
audioRenderer.off('writeData', (data: ArrayBuffer) => {
    console.info(`write data: ${data}`);
});
```

## AudioCapturer<sup>8+</sup>

提供音频采集的相关接口。在调用AudioCapturer的接口前，需要先通过[createAudioCapturer](#audiocreateaudiocapturer8)创建实例。

### 属性

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

| 名称  | 类型                     | 可读 | 可写 | 说明             |
| :---- | :------------------------- | :--- | :--- | :--------------- |
| state<sup>8+</sup>  | [AudioState](#audiostate8) | 是 | 否   | 音频采集器状态。 |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

let state: audio.AudioState = audioCapturer.state;
```

### getCapturerInfo<sup>8+</sup>

getCapturerInfo(callback: AsyncCallback<AudioCapturerInfo\>): void

获取采集器信息。使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名   | 类型                              | 必填 | 说明                                 |
| :------- | :-------------------------------- | :--- | :----------------------------------- |
| callback | AsyncCallback<[AudioCapturerInfo](#audiocapturerinfo8)\> | 是   | 回调函数。当获取采集器信息成功，err为undefined，data为获取到的采集器信息；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioCapturer.getCapturerInfo((err: BusinessError, capturerInfo: audio.AudioCapturerInfo) => {
  if (err) {
    console.error('Failed to get capture info');
  } else {
    console.info('Capturer getCapturerInfo:');
    console.info(`Capturer source: ${capturerInfo.source}`);
    console.info(`Capturer flags: ${capturerInfo.capturerFlags}`);
  }
});
```


### getCapturerInfo<sup>8+</sup>

getCapturerInfo(): Promise<AudioCapturerInfo\>

获取采集器信息。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**返回值：**

| 类型                                              | 说明                                |
| :------------------------------------------------ | :---------------------------------- |
| Promise<[AudioCapturerInfo](#audiocapturerinfo8)\> | Promise对象，返回采集器信息。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioCapturer.getCapturerInfo().then((audioParamsGet: audio.AudioCapturerInfo) => {
  if (audioParamsGet != undefined) {
    console.info('AudioFrameworkRecLog: Capturer CapturerInfo:');
    console.info(`AudioFrameworkRecLog: Capturer SourceType: ${audioParamsGet.source}`);
    console.info(`AudioFrameworkRecLog: Capturer capturerFlags: ${audioParamsGet.capturerFlags}`);
  } else {
    console.info(`AudioFrameworkRecLog: audioParamsGet is : ${audioParamsGet}`);
    console.info('AudioFrameworkRecLog: audioParams getCapturerInfo are incorrect');
  }
}).catch((err: BusinessError) => {
  console.error(`AudioFrameworkRecLog: CapturerInfo :ERROR: ${err}`);
})
```

### getCapturerInfoSync<sup>10+</sup>

getCapturerInfoSync(): AudioCapturerInfo

获取采集器信息，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**返回值：**

| 类型                                              | 说明                                |
| :------------------------------------------------ | :---------------------------------- |
| [AudioCapturerInfo](#audiocapturerinfo8) | 返回采集器信息。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let audioParamsGet: audio.AudioCapturerInfo = audioCapturer.getCapturerInfoSync();
  console.info(`AudioFrameworkRecLog: Capturer SourceType: ${audioParamsGet.source}`);
  console.info(`AudioFrameworkRecLog: Capturer capturerFlags: ${audioParamsGet.capturerFlags}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`AudioFrameworkRecLog: CapturerInfo :ERROR: ${error}`);
}
```

### getStreamInfo<sup>8+</sup>

getStreamInfo(callback: AsyncCallback<AudioStreamInfo\>): void

获取采集器流信息。使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名   | 类型                                                 | 必填 | 说明                             |
| :------- | :--------------------------------------------------- | :--- | :------------------------------- |
| callback | AsyncCallback<[AudioStreamInfo](#audiostreaminfo8)\> | 是   | 回调函数。当获取采集器流信息成功，err为undefined，data为获取到的采集器流信息；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioCapturer.getStreamInfo((err: BusinessError, streamInfo: audio.AudioStreamInfo) => {
  if (err) {
    console.error('Failed to get stream info');
  } else {
    console.info('Capturer GetStreamInfo:');
    console.info(`Capturer sampling rate: ${streamInfo.samplingRate}`);
    console.info(`Capturer channel: ${streamInfo.channels}`);
    console.info(`Capturer format: ${streamInfo.sampleFormat}`);
    console.info(`Capturer encoding type: ${streamInfo.encodingType}`);
  }
});
```

### getStreamInfo<sup>8+</sup>

getStreamInfo(): Promise<AudioStreamInfo\>

获取采集器流信息。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**返回值：**

| 类型                                           | 说明                            |
| :--------------------------------------------- | :------------------------------ |
| Promise<[AudioStreamInfo](#audiostreaminfo8)\> | Promise对象，返回流信息。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioCapturer.getStreamInfo().then((audioParamsGet: audio.AudioStreamInfo) => {
  console.info('getStreamInfo:');
  console.info(`sampleFormat: ${audioParamsGet.sampleFormat}`);
  console.info(`samplingRate: ${audioParamsGet.samplingRate}`);
  console.info(`channels: ${audioParamsGet.channels}`);
  console.info(`encodingType: ${audioParamsGet.encodingType}`);
}).catch((err: BusinessError) => {
  console.error(`getStreamInfo :ERROR: ${err}`);
});
```

### getStreamInfoSync<sup>10+</sup>

getStreamInfoSync(): AudioStreamInfo

获取采集器流信息，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**返回值：**

| 类型                                           | 说明                            |
| :--------------------------------------------- | :------------------------------ |
| [AudioStreamInfo](#audiostreaminfo8) | 返回流信息。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let audioParamsGet: audio.AudioStreamInfo = audioCapturer.getStreamInfoSync();
  console.info(`sampleFormat: ${audioParamsGet.sampleFormat}`);
  console.info(`samplingRate: ${audioParamsGet.samplingRate}`);
  console.info(`channels: ${audioParamsGet.channels}`);
  console.info(`encodingType: ${audioParamsGet.encodingType}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`getStreamInfo :ERROR: ${error}`);
}
```

### getAudioStreamId<sup>9+</sup>

getAudioStreamId(callback: AsyncCallback<number\>): void

获取音频流id，使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名   | 类型                                                 | 必填 | 说明                 |
| :------- | :--------------------------------------------------- | :--- | :------------------- |
| callback | AsyncCallback<number\> | 是   | 回调函数。当获取音频流id成功，err为undefined，data为获取到的音频流id；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioCapturer.getAudioStreamId((err: BusinessError, streamId: number) => {
  console.info(`audioCapturer GetStreamId: ${streamId}`);
});
```

### getAudioStreamId<sup>9+</sup>

getAudioStreamId(): Promise<number\>

获取音频流id，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**返回值：**

| 类型             | 说明                   |
| :----------------| :--------------------- |
| Promise<number\> | Promise对象，返回音频流id。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioCapturer.getAudioStreamId().then((streamId: number) => {
  console.info(`audioCapturer getAudioStreamId: ${streamId}`);
}).catch((err: BusinessError) => {
  console.error(`ERROR: ${err}`);
});
```

### getAudioStreamIdSync<sup>10+</sup>

getAudioStreamIdSync(): number

获取音频流id，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**返回值：**

| 类型             | 说明                   |
| :----------------| :--------------------- |
| number | 返回音频流id。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let streamId: number = audioCapturer.getAudioStreamIdSync();
  console.info(`audioCapturer getAudioStreamIdSync: ${streamId}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`ERROR: ${error}`);
}
```

### start<sup>8+</sup>

start(callback: AsyncCallback<void\>): void

启动音频采集器。使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名   | 类型                 | 必填 | 说明                           |
| :------- | :------------------- | :--- | :----------------------------- |
| callback | AsyncCallback<void\> | 是   | 回调函数。当启动音频采集器成功，err为undefined，否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioCapturer.start((err: BusinessError) => {
  if (err) {
    console.error('Capturer start failed.');
  } else {
    console.info('Capturer start success.');
  }
});
```


### start<sup>8+</sup>

start(): Promise<void\>

启动音频采集器。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**返回值：**

| 类型           | 说明                          |
| :------------- | :---------------------------- |
| Promise<void\> | Promise对象，无返回结果。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioCapturer.start().then(() => {
  console.info('AudioFrameworkRecLog: ---------START---------');
  console.info('AudioFrameworkRecLog: Capturer started: SUCCESS');
  console.info(`AudioFrameworkRecLog: AudioCapturer: STATE: ${audioCapturer.state}`);
  console.info('AudioFrameworkRecLog: Capturer started: SUCCESS');
  if ((audioCapturer.state == audio.AudioState.STATE_RUNNING)) {
    console.info('AudioFrameworkRecLog: AudioCapturer is in Running State');
  }
}).catch((err: BusinessError) => {
  console.error(`AudioFrameworkRecLog: Capturer start :ERROR : ${err}`);
});
```

### stop<sup>8+</sup>

stop(callback: AsyncCallback<void\>): void

停止采集。使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名   | 类型                 | 必填 | 说明                           |
| :------- | :------------------- | :--- | :----------------------------- |
| callback | AsyncCallback<void\> | 是   | 回调函数。当停止采集成功，err为undefined，否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioCapturer.stop((err: BusinessError) => {
  if (err) {
    console.error('Capturer stop failed');
  } else {
    console.info('Capturer stopped.');
  }
});
```


### stop<sup>8+</sup>

stop(): Promise<void\>

停止采集。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**返回值：**

| 类型           | 说明                          |
| :------------- | :---------------------------- |
| Promise<void\> | Promise对象，无返回结果。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioCapturer.stop().then(() => {
  console.info('AudioFrameworkRecLog: ---------STOP RECORD---------');
  console.info('AudioFrameworkRecLog: Capturer stopped: SUCCESS');
  if ((audioCapturer.state == audio.AudioState.STATE_STOPPED)){
    console.info('AudioFrameworkRecLog: State is Stopped:');
  }
}).catch((err: BusinessError) => {
  console.error(`AudioFrameworkRecLog: Capturer stop: ERROR: ${err}`);
});
```

### release<sup>8+</sup>

release(callback: AsyncCallback<void\>): void

释放采集器。使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                |
| :------- | :------------------- | :--- | :---------------------------------- |
| callback | AsyncCallback<void\> | 是   | 回调函数。当释放采集器成功，err为undefined，否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioCapturer.release((err: BusinessError) => {
  if (err) {
    console.error('capturer release failed');
  } else {
    console.info('capturer released.');
  }
});
```


### release<sup>8+</sup>

release(): Promise<void\>

释放采集器。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**返回值：**

| 类型           | 说明                          |
| :------------- | :---------------------------- |
| Promise<void\> | Promise对象，无返回结果。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioCapturer.release().then(() => {
  console.info('AudioFrameworkRecLog: ---------RELEASE RECORD---------');
  console.info('AudioFrameworkRecLog: Capturer release : SUCCESS');
  console.info(`AudioFrameworkRecLog: AudioCapturer : STATE : ${audioCapturer.state}`);
}).catch((err: BusinessError) => {
  console.error(`AudioFrameworkRecLog: Capturer stop: ERROR: ${err}`);
});
```

### read<sup>8+(deprecated)</sup>

read(size: number, isBlockingRead: boolean, callback: AsyncCallback<ArrayBuffer\>): void

读入缓冲区。使用callback方式异步返回结果。

> **说明：**
> 从 API version 8 开始支持，从 API version 11 开始废弃，建议使用AudioCapturer中的[on('readData')](#onreaddata11)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名         | 类型                        | 必填 | 说明                             |
| :------------- | :-------------------------- | :--- | :------------------------------- |
| size           | number                      | 是   | 读入的字节数。                   |
| isBlockingRead | boolean                     | 是   | 是否阻塞读操作 ，true阻塞，false不阻塞。                 |
| callback       | AsyncCallback<ArrayBuffer\> | 是   | 回调函数。当读入缓冲区成功，err为undefined，data为获取到的缓冲区；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let bufferSize: number = 0;
audioCapturer.getBufferSize().then((data: number) => {
  console.info(`AudioFrameworkRecLog: getBufferSize: SUCCESS ${data}`);
  bufferSize = data;
}).catch((err: BusinessError) => {
  console.error(`AudioFrameworkRecLog: getBufferSize: ERROR: ${err}`);
});
audioCapturer.read(bufferSize, true, (err: BusinessError, buffer: ArrayBuffer) => {
  if (!err) {
    console.info('Success in reading the buffer data');
  }
});
```

### read<sup>8+(deprecated)</sup>

read(size: number, isBlockingRead: boolean): Promise<ArrayBuffer\>

读入缓冲区。使用Promise方式异步返回结果。

> **说明：**
> 从 API version 8 开始支持，从 API version 11 开始废弃，建议使用AudioCapturer中的[on('readData')](#onreaddata11)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名         | 类型    | 必填 | 说明             |
| :------------- | :------ | :--- | :--------------- |
| size           | number  | 是   | 读入的字节数。   |
| isBlockingRead | boolean | 是   | 是否阻塞读操作 ，true阻塞，false不阻塞。 |

**返回值：**

| 类型                  | 说明                                                   |
| :-------------------- | :----------------------------------------------------- |
| Promise<ArrayBuffer\> | Promise对象，返回读取的缓冲区数据。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let bufferSize: number = 0;
audioCapturer.getBufferSize().then((data: number) => {
  console.info(`AudioFrameworkRecLog: getBufferSize: SUCCESS ${data}`);
  bufferSize = data;
}).catch((err: BusinessError) => {
  console.error(`AudioFrameworkRecLog: getBufferSize: ERROR ${err}`);
});
console.info(`Buffer size: ${bufferSize}`);
audioCapturer.read(bufferSize, true).then((buffer: ArrayBuffer) => {
  console.info('buffer read successfully');
}).catch((err: BusinessError) => {
  console.error(`ERROR : ${err}`);
});
```

### getAudioTime<sup>8+</sup>

getAudioTime(callback: AsyncCallback<number\>): void

获取时间戳（从1970年1月1日开始），单位为纳秒。使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名   | 类型                   | 必填 | 说明                           |
| :------- | :--------------------- | :--- | :----------------------------- |
| callback | AsyncCallback<number\> | 是   | 回调函数。当获取时间戳成功，err为undefined，data为获取到的时间戳；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioCapturer.getAudioTime((err: BusinessError, timestamp: number) => {
  console.info(`Current timestamp: ${timestamp}`);
});
```

### getAudioTime<sup>8+</sup>

getAudioTime(): Promise<number\>

获取时间戳（从1970年1月1日开始），单位为纳秒。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**返回值：**

| 类型             | 说明                          |
| :--------------- | :---------------------------- |
| Promise<number\> | Promise对象，返回时间戳（从1970年1月1日开始），单位为纳秒。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioCapturer.getAudioTime().then((audioTime: number) => {
  console.info(`AudioFrameworkRecLog: AudioCapturer getAudioTime : Success ${audioTime}`);
}).catch((err: BusinessError) => {
  console.error(`AudioFrameworkRecLog: AudioCapturer Created : ERROR : ${err}`);
});
```

### getAudioTimeSync<sup>10+</sup>

getAudioTimeSync(): number

获取时间戳（从1970年1月1日开始），单位为纳秒，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**返回值：**

| 类型             | 说明                          |
| :--------------- | :---------------------------- |
| number | 返回时间戳。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

try {
  let audioTime: number = audioCapturer.getAudioTimeSync();
  console.info(`AudioFrameworkRecLog: AudioCapturer getAudioTimeSync : Success ${audioTime}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`AudioFrameworkRecLog: AudioCapturer getAudioTimeSync : ERROR : ${error}`);
}
```

### getBufferSize<sup>8+</sup>

getBufferSize(callback: AsyncCallback<number\>): void

获取采集器合理的最小缓冲区大小。使用callback方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名   | 类型                   | 必填 | 说明                                 |
| :------- | :--------------------- | :--- | :----------------------------------- |
| callback | AsyncCallback<number\> | 是   | 回调函数。当获取采集器合理的最小缓冲区大小成功，err为undefined，data为获取到的采集器合理的最小缓冲区大小；否则为错误对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioCapturer.getBufferSize((err: BusinessError, bufferSize: number) => {
  if (!err) {
    console.info(`BufferSize : ${bufferSize}`);
    audioCapturer.read(bufferSize, true).then((buffer: ArrayBuffer) => {
      console.info(`Buffer read is ${buffer.byteLength}`);
    }).catch((err: BusinessError) => {
      console.error(`AudioFrameworkRecLog: AudioCapturer Created : ERROR : ${err}`);
    });
  }
});
```

### getBufferSize<sup>8+</sup>

getBufferSize(): Promise<number\>

获取采集器合理的最小缓冲区大小。使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**返回值：**

| 类型             | 说明                                |
| :--------------- | :---------------------------------- |
| Promise<number\> | Promise对象，返回缓冲区大小。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let bufferSize: number = 0;
audioCapturer.getBufferSize().then((data: number) => {
  console.info(`AudioFrameworkRecLog: getBufferSize :SUCCESS ${data}`);
  bufferSize = data;
}).catch((err: BusinessError) => {
  console.error(`AudioFrameworkRecLog: getBufferSize :ERROR : ${err}`);
});
```

### getBufferSizeSync<sup>10+</sup>

getBufferSizeSync(): number

获取采集器合理的最小缓冲区大小，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**返回值：**

| 类型             | 说明                                |
| :--------------- | :---------------------------------- |
| number | 返回缓冲区大小。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let bufferSize: number = 0;
try {
  bufferSize = audioCapturer.getBufferSizeSync();
  console.info(`AudioFrameworkRecLog: getBufferSizeSync :SUCCESS ${bufferSize}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`AudioFrameworkRecLog: getBufferSizeSync :ERROR : ${error}`);
}
```

### getCurrentInputDevices<sup>11+</sup>

getCurrentInputDevices(): AudioDeviceDescriptors

获取录音流输入设备描述符。使用同步方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**返回值：**

| 类型                   | 说明                                                   |
| ---------------------- | ------------------------------------------------------ |
| [AudioDeviceDescriptors](#audiodevicedescriptors)            | 同步接口，返回设备属性数组类型数据。 |

**示例：**

```ts
let deviceDescriptors: audio.AudioDeviceDescriptors = audioCapturer.getCurrentInputDevices();
console.info(`Device id: ${deviceDescriptors[0].id}`);
console.info(`Device type: ${deviceDescriptors[0].deviceType}`);
console.info(`Device role: ${deviceDescriptors[0].deviceRole}`);
console.info(`Device name: ${deviceDescriptors[0].name}`);
console.info(`Device address: ${deviceDescriptors[0].address}`);
console.info(`Device samplerates: ${deviceDescriptors[0].sampleRates[0]}`);
console.info(`Device channelcounts: ${deviceDescriptors[0].channelCounts[0]}`);
console.info(`Device channelmask: ${deviceDescriptors[0].channelMasks[0]}`);
if (deviceDescriptors[0].encodingTypes) {
  console.info(`Device encodingTypes: ${deviceDescriptors[0].encodingTypes[0]}`);
}
```

### getCurrentAudioCapturerChangeInfo<sup>11+</sup>

getCurrentAudioCapturerChangeInfo(): AudioCapturerChangeInfo

获取录音流配置。使用同步方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**返回值：**

| 类型             | 说明                                |
| :--------------- | :---------------------------------- |
| [AudioCapturerChangeInfo](#audiocapturerchangeinfo9) | 同步接口，返回描述音频采集器更改信息。 |

**示例：**

```ts
let info: audio.AudioCapturerChangeInfo = audioCapturer.getCurrentAudioCapturerChangeInfo();
console.info(`Info streamId: ${info.streamId}`);
console.info(`Info source: ${info.capturerInfo.source}`);
console.info(`Info capturerFlags: ${info.capturerInfo.capturerFlags}`);
console.info(`Info muted: ${info.muted}`);
console.info(`Info type: ${info.deviceDescriptors[0].deviceType}`);
console.info(`Info role: ${info.deviceDescriptors[0].deviceRole}`);
console.info(`Info name: ${info.deviceDescriptors[0].name}`);
console.info(`Info address: ${info.deviceDescriptors[0].address}`);
console.info(`Info samplerates: ${info.deviceDescriptors[0].sampleRates[0]}`);
console.info(`Info channelcounts: ${info.deviceDescriptors[0].channelCounts[0]}`);
console.info(`Info channelmask: ${info.deviceDescriptors[0].channelMasks[0]}`);
if (info.deviceDescriptors[0].encodingTypes) {
  console.info(`Device encodingTypes: ${info.deviceDescriptors[0].encodingTypes[0]}`);
}
```

### on('audioInterrupt')<sup>10+</sup>

on(type: 'audioInterrupt', callback: Callback\<InterruptEvent>): void

监听音频中断事件，使用callback方式返回结果。

与[on('interrupt')](#oninterruptdeprecated)一致，均用于监听焦点变化。AudioCapturer对象在start事件发生时会主动获取焦点，在pause、stop等事件发生时会主动释放焦点，不需要开发者主动发起获取焦点或释放焦点的申请。

**系统能力：** SystemCapability.Multimedia.Audio.Interrupt

**参数：**

| 参数名   | 类型                                         | 必填 | 说明                                                         |
| -------- | -------------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                                       | 是   | 事件回调类型，支持的事件为：'audioInterrupt'（中断事件被触发，音频采集被中断。） |
| callback | Callback\<[InterruptEvent](#interruptevent9)\> | 是   | 回调函数，返回播放中断时，应用接收的中断事件信息。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

let isCapturing: boolean; // 标识符，表示是否正在采集
onAudioInterrupt();

async function onAudioInterrupt(){
  audioCapturer.on('audioInterrupt', (interruptEvent: audio.InterruptEvent) => {
    if (interruptEvent.forceType == audio.InterruptForceType.INTERRUPT_FORCE) {
      // 由系统进行操作，强制打断音频采集，应用需更新自身状态及显示内容等
      switch (interruptEvent.hintType) {
        case audio.InterruptHint.INTERRUPT_HINT_PAUSE:
          // 音频流已被暂停，临时失去焦点，待可重获焦点时会收到resume对应的interruptEvent
          console.info('Force paused. Update capturing status and stop reading');
          isCapturing = false; // 简化处理，代表应用切换至暂停状态的若干操作
          break;
        case audio.InterruptHint.INTERRUPT_HINT_STOP:
          // 音频流已被停止，永久失去焦点，若想恢复采集，需用户主动触发
          console.info('Force stopped. Update capturing status and stop reading');
          isCapturing = false; // 简化处理，代表应用切换至暂停状态的若干操作
          break;
        default:
          console.info('Invalid interruptEvent');
          break;
      }
    } else if (interruptEvent.forceType == audio.InterruptForceType.INTERRUPT_SHARE) {
      // 由应用进行操作，应用可以自主选择打断或忽略
      switch (interruptEvent.hintType) {
        case audio.InterruptHint.INTERRUPT_HINT_RESUME:
          // 建议应用继续采集（说明音频流此前被强制暂停，临时失去焦点，现在可以恢复采集）
          console.info('Resume force paused renderer or ignore');
          // 若选择继续采集，需在此处主动执行开始采集的若干操作
          break;
        case audio.InterruptHint.INTERRUPT_HINT_PAUSE:
          // 建议应用暂停采集
          console.info('Choose to pause or ignore');
          // 若选择暂停采集，需在此处主动执行暂停采集的若干操作
          break;
        case audio.InterruptHint.INTERRUPT_HINT_STOP:
          // 建议应用停止采集
          console.info('Choose to stop or ignore');
          // 若选择停止采集，需在此处主动执行停止采集的若干操作
          break;
        default:
          break;
      }
    }
  });
}
```

### off('audioInterrupt')<sup>10+</sup>

off(type: 'audioInterrupt'): void

取消订阅音频中断事件。

**系统能力：** SystemCapability.Multimedia.Audio.Interrupt

**参数：**

| 参数名   | 类型                                         | 必填 | 说明                                                         |
| -------- | -------------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                                       | 是   | 事件回调类型，支持的事件为：'audioInterrupt' |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. |

**示例：**

```ts
audioCapturer.off('audioInterrupt');
```

### on('inputDeviceChange')<sup>11+</sup>

on(type: 'inputDeviceChange', callback: Callback\<AudioDeviceDescriptors>): void

订阅监听音频输入设备变化，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名   | 类型                       | 必填 | 说明                                        |
| :------- | :------------------------- | :--- | :------------------------------------------ |
| type     | string                     | 是   | 事件回调类型，支持的事件为：'inputDeviceChange'。 |
| callback | Callback\<[AudioDeviceDescriptors](#audiodevicedescriptors)> | 是   | 回调函数，返回监听的音频输入设备变化(返回数据为切换后的设备信息)。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Input parameter value error.              |

**示例：**

```ts
audioCapturer.on('inputDeviceChange', (deviceChangeInfo: audio.AudioDeviceDescriptors) => {
  console.info(`inputDevice id: ${deviceChangeInfo[0].id}`);
  console.info(`inputDevice deviceRole: ${deviceChangeInfo[0].deviceRole}`);
  console.info(`inputDevice deviceType: ${deviceChangeInfo[0].deviceType}`);
});
```
### off('inputDeviceChange')<sup>11+</sup>

off(type: 'inputDeviceChange', callback?: Callback\<AudioDeviceDescriptors>): void

取消订阅音频输入设备更改事件，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Device

**参数：**

| 参数名   | 类型                       | 必填 | 说明                                       |
| :------- | :------------------------- | :--- |:-----------------------------------------|
| type     | string                     | 是   | 事件回调类型，支持的事件为：'inputDeviceChange'。       |
| callback | Callback\<[AudioDeviceDescriptors](#audiodevicedescriptors)> | 否   | 回调函数，返回监听的音频输入设备信息。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Input parameter value error.              |

**示例：**

```ts
audioCapturer.off('inputDeviceChange');
```

### on('audioCapturerChange')<sup>11+</sup>

on(type: 'audioCapturerChange', callback: Callback\<AudioCapturerChangeInfo>): void

订阅监听录音流配置变化，使用callback方式返回结果。订阅内部是异步实现，是非精确回调，在录音流配置变化的同时注册回调，收到的返回结果存在变化可能性。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名   | 类型                       | 必填 | 说明                                        |
| :------- | :------------------------- | :--- | :------------------------------------------ |
| type     | string                     | 是   | 事件回调类型，支持的事件为：'audioCapturerChange'。 |
| callback | Callback\<[AudioCapturerChangeInfo](#audiocapturerchangeinfo9)> | 是   | 回调函数，录音流配置或状态变化时返回监听的录音流当前配置和状态信息。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Input parameter value error.              |

**示例：**

```ts
audioCapturer.on('audioCapturerChange', (capturerChangeInfo: audio.AudioCapturerChangeInfo) => {
  console.info(`audioCapturerChange id: ${capturerChangeInfo[0].id}`);
  console.info(`audioCapturerChange deviceRole: ${capturerChangeInfo[0].deviceRole}`);
  console.info(`audioCapturerChange deviceType: ${capturerChangeInfo[0].deviceType}`);
});
```

### off('audioCapturerChange')<sup>11+</sup>

off(type: 'audioCapturerChange', callback?: Callback\<AudioCapturerChangeInfo>): void

取消订阅音频输入设备更改事件，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名   | 类型                       | 必填 | 说明                                        |
| :------- | :------------------------- | :--- | :------------------------------------------ |
| type     | string                     | 是   | 事件回调类型，支持的事件为：'audioCapturerChange'。 |
| callback | Callback\<[AudioCapturerChangeInfo](#audiocapturerchangeinfo9)> | 否   | 回调函数，返回取消监听的录音流配置或状态变化。 |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Input parameter value error.              |

**示例：**

```ts
audioCapturer.off('audioCapturerChange');
```

### on('markReach')<sup>8+</sup>

on(type: 'markReach', frame: number, callback: Callback&lt;number&gt;): void

订阅标记到达的事件。 当采集的帧数达到 frame 参数的值时，回调被触发，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名   | 类型                     | 必填 | 说明                                       |
| :------- | :----------------------  | :--- | :----------------------------------------- |
| type     | string                   | 是   | 事件回调类型，支持的事件为：'markReach'。  |
| frame    | number                   | 是   | 触发事件的帧数。 该值必须大于0。           |
| callback | Callback\<number>         | 是   | 回调函数，返回frame 参数的值 |

**示例：**

```ts
audioCapturer.on('markReach', 1000, (position: number) => {
  if (position == 1000) {
    console.info('ON Triggered successfully');
  }
});
```

### off('markReach')<sup>8+</sup>

off(type: 'markReach'): void

取消订阅标记到达的事件。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                          |
| :----- | :----- | :--- | :-------------------------------------------- |
| type   | string | 是   | 取消事件回调类型，支持的事件为：'markReach'。 |

**示例：**

```ts
audioCapturer.off('markReach');
```

### on('periodReach')<sup>8+</sup>

on(type: 'periodReach', frame: number, callback: Callback&lt;number&gt;): void

订阅到达标记的事件。 当采集的帧数达到 frame 参数的值时，触发回调并返回设定的值，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名   | 类型                     | 必填 | 说明                                        |
| :------- | :----------------------- | :--- | :------------------------------------------ |
| type     | string                   | 是   | 事件回调类型，支持的事件为：'periodReach'。 |
| frame    | number                   | 是   | 触发事件的帧数。 该值必须大于0。            |
| callback | Callback\<number>         | 是   |回调函数，返回frame 参数的值。    |

**示例：**

```ts
audioCapturer.on('periodReach', 1000, (position: number) => {
  if (position == 1000) {
    console.info('ON Triggered successfully');
  }
});
```

### off('periodReach')<sup>8+</sup>

off(type: 'periodReach'): void

取消订阅标记到达的事件。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                            |
| :----- | :----- | :--- | :---------------------------------------------- |
| type   | string | 是  | 取消事件回调类型，支持的事件为：'periodReach'。 |

**示例：**

```ts
audioCapturer.off('periodReach');
```

### on('stateChange') <sup>8+</sup>

on(type: 'stateChange', callback: Callback<AudioState\>): void

订阅监听状态变化，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名   | 类型                       | 必填 | 说明                                        |
| :------- | :------------------------- | :--- | :------------------------------------------ |
| type     | string                     | 是   | 事件回调类型，支持的事件为：'stateChange'。 |
| callback | Callback\<[AudioState](#audiostate8)> | 是   | 回调函数，返回当前音频的状态。 |

**示例：**

```ts
audioCapturer.on('stateChange', (state: audio.AudioState) => {
  if (state == 1) {
    console.info('audio capturer state is: STATE_PREPARED');
  }
  if (state == 2) {
    console.info('audio capturer state is: STATE_RUNNING');
  }
});
```

### on('readData')<sup>11+</sup>

on(type: 'readData', callback: Callback\<ArrayBuffer>): void

订阅监听音频数据读入回调，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名   | 类型                     | 必填 | 说明                        |
| :------- |:-----------------------| :--- |:--------------------------|
| type     | string                 | 是   | 事件回调类型，支持的事件为：'readData'。 |
| callback | Callback\<ArrayBuffer> | 是   | 回调函数，返回读到的数据缓冲区。            |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Input parameter value error. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import fs from '@ohos.file.fs';

let bufferSize: number = 0;
class Options {
  offset?: number;
  length?: number;
}

let readDataCallback = (buffer: ArrayBuffer) => {
  let path = getContext().cacheDir;
  let filePath = path + '/StarWars10s-2C-48000-4SW.wav';
  let file: fs.File = fs.openSync(filePath, fs.OpenMode.READ_WRITE);
  let options: Options = {
    offset: bufferSize,
    length: buffer.byteLength
  }
  fs.writeSync(file.fd, buffer, options);
  bufferSize += buffer.byteLength;
}
audioCapturer.on('readData', readDataCallback);
audioCapturer.start((err: BusinessError) => {
  if (err) {
    console.error('Capturer start failed.');
  } else {
    console.info('Capturer start success.');
  }
});
```

### off('readData')<sup>11+</sup>

off(type: 'readData', callback?: Callback\<ArrayBuffer>): void

取消订阅监听音频数据读入回调，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Audio.Capturer

**参数：**

| 参数名   | 类型                     | 必填 | 说明                                         |
| :------- |:-----------------------| :--- |:-------------------------------------------|
| type     | string                 | 是   | 事件回调类型，支持的事件为：'readData'。                 |
| callback | Callback\<ArrayBuffer> | 否   | 回调函数，返回读到的数据缓冲区。                            |

**错误码：**

以下错误码的详细介绍请参见[Audio错误码](errorcode-audio.md)。

| 错误码ID | 错误信息 |
| ------- | --------------------------------------------|
| 6800101 | Input parameter value error. |

**示例：**

```ts
audioCapturer.off('readData', (data: ArrayBuffer) => {
    console.info(`read data: ${data}`);
});
```

## ActiveDeviceType<sup>(deprecated)</sup>

枚举，活跃设备类型。

> **说明：**
>
> 从 API version 9 开始废弃，建议使用[CommunicationDeviceType](#communicationdevicetype9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Device

| 名称          |  值     | 说明                                                 |
| ------------- | ------ | ---------------------------------------------------- |
| SPEAKER       | 2      | 扬声器。                                             |
| BLUETOOTH_SCO | 7      | 蓝牙设备SCO（Synchronous Connection Oriented）连接。 |

## InterruptActionType<sup>(deprecated)</sup>

枚举，中断事件返回类型。

> **说明：**
>
> 从 API version 7 开始支持，从 API version 9 开始废弃。无替代接口，与中断事件配套使用。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

| 名称           |  值     | 说明               |
| -------------- | ------ | ------------------ |
| TYPE_ACTIVATED | 0      | 表示触发焦点事件。 |
| TYPE_INTERRUPT | 1      | 表示音频打断事件。 |

## AudioInterrupt<sup>(deprecated)</sup>

音频监听事件传入的参数。

> **说明：**
>
> 从 API version 7 开始支持，从 API version 9 开始废弃。无替代接口，与中断事件配套使用。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

| 名称            | 类型                        | 必填 | 说明                                                         |
| --------------- | --------------------------- | ----| ------------------------------------------------------------ |
| streamUsage     | [StreamUsage](#streamusage) | 是  | 音频流使用类型。                                             |
| contentType     | [ContentType](#contenttypedeprecated) | 是  | 音频打断媒体类型。                                           |
| pauseWhenDucked | boolean                     | 是  | 音频打断时是否可以暂停音频播放（true表示音频播放可以在音频打断期间暂停，false表示相反）。 |

## InterruptAction<sup>(deprecated)</sup>

音频打断/获取焦点事件的回调方法。

> **说明：**
>
> 从 API version 7 开始支持，从 API version 9 开始废弃。建议使用[InterruptEvent](#interruptevent9)替代。

**系统能力：** SystemCapability.Multimedia.Audio.Renderer

| 名称       | 类型                                        | 必填 | 说明                                                         |
| ---------- | ------------------------------------------- | ---- | ------------------------------------------------------------ |
| actionType | [InterruptActionType](#interruptactiontypedeprecated) | 是   | 事件返回类型。TYPE_ACTIVATED为焦点触发事件，TYPE_INTERRUPT为音频打断事件。 |
| type       | [InterruptType](#interrupttype)             | 否   | 打断事件类型。                                               |
| hint       | [InterruptHint](#interrupthint)             | 否   | 打断事件提示。                                               |
| activated  | boolean                                     | 否   | 获得/释放焦点。true表示焦点获取/释放成功，false表示焦点获得/释放失败。 |
