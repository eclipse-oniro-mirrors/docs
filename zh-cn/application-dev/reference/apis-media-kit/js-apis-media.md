# @ohos.multimedia.media (媒体服务)

> **说明：**
> 本模块首批接口从API version 6开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

媒体子系统为开发者提供一套简单且易于理解的接口，使得开发者能够方便接入系统并使用系统的媒体资源。

媒体子系统包含了音视频相关媒体业务，提供以下常用功能：

- 音视频播放（[AVPlayer](#avplayer9)<sup>9+</sup>）

- 音视频录制（[AVRecorder](#avrecorder9)<sup>9+</sup>）

- 获取音视频元数据（[AVMetadataExtractor](#avmetadataextractor11)<sup>11+</sup>）

## 导入模块

```ts
import media from '@ohos.multimedia.media';
```

## media.createAVPlayer<sup>9+</sup>

createAVPlayer(callback: AsyncCallback\<AVPlayer>): void

异步方式创建音视频播放实例，通过注册回调函数获取返回值。

> **说明：**
>
> - 可创建的视频播放实例不能超过13个。
> - 可创建的音视频播放实例（即音频、视频、音视频三类相加）不能超过16个。
> - 可创建的音视频播放实例数量依赖于设备芯片的支持情况，如芯片支持创建的数量少于上述情况，请以芯片规格为准。如RK3568仅支持创建6个以内的视频播放实例。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                                                         |
| -------- | ------------------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback\<[AVPlayer](#avplayer9)> | 是   | 回调函数。异步返回AVPlayer实例，失败时返回null。可用于音视频播放。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                       |
| -------- | ------------------------------ |
| 5400101  | No memory. Return by callback. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let avPlayer: media.AVPlayer;
media.createAVPlayer((error: BusinessError, video: media.AVPlayer) => {
  if (video != null) {
    avPlayer = video;
    console.info('createAVPlayer success');
  } else {
    console.error(`createAVPlayer fail, error message:${error.message}`);
  }
});
```

## media.createAVPlayer<sup>9+</sup>

createAVPlayer(): Promise\<AVPlayer>

异步方式创建音视频播放实例，通过Promise获取返回值。

> **说明：**
>
> - 可创建的视频播放实例不能超过13个。
> - 可创建的音视频播放实例（即音频、视频、音视频三类相加）不能超过16个。
> - 可创建的音视频播放实例数量依赖于设备芯片的支持情况，如芯片支持创建的数量少于上述情况，请以芯片规格为准。如RK3568仅支持创建6个以内的视频播放实例。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**返回值：**

| 类型                            | 说明                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| Promise\<[AVPlayer](#avplayer9)> | Promise对象。异步返回AVPlayer实例，失败时返回null。可用于音视频播放。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                      |
| -------- | ----------------------------- |
| 5400101  | No memory. Return by promise. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let avPlayer: media.AVPlayer;
media.createAVPlayer().then((video: media.AVPlayer) => {
  if (video != null) {
    avPlayer = video;
    console.info('createAVPlayer success');
  } else {
    console.error('createAVPlayer fail');
  }
}).catch((error: BusinessError) => {
  console.error(`AVPlayer catchCallback, error message:${error.message}`);
});
```

## media.createAVRecorder<sup>9+</sup>

createAVRecorder(callback: AsyncCallback\<AVRecorder>): void

异步方式创建音视频录制实例。通过注册回调函数获取返回值。

> **说明：**
>
> - 可创建的音视频录制实例不能超过2个。
> - 由于设备共用音频通路，一个设备仅能有一个实例进行音频录制。创建第二个实例录制音频时，将会因为音频通路冲突导致创建失败。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**参数：**

| 参数名   | 类型                                       | 必填 | 说明                                                         |
| -------- | ------------------------------------------ | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback\<[AVRecorder](#avrecorder9)> | 是   | 回调函数。异步返回AVRecorder实例，失败时返回null。可用于录制音视频媒体。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                       |
| -------- | ------------------------------ |
| 5400101  | No memory. Return by callback. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
let avRecorder: media.AVRecorder;

media.createAVRecorder((error: BusinessError, recorder: media.AVRecorder) => {
  if (recorder != null) {
    avRecorder = recorder;
    console.info('createAVRecorder success');
  } else {
    console.error(`createAVRecorder fail, error message:${error.message}`);
  }
});
```

## media.createAVRecorder<sup>9+</sup>

createAVRecorder(): Promise\<AVRecorder>

异步方式创建音视频录制实例。通过Promise获取返回值。

> **说明：**
>
> - 可创建的音视频录制实例不能超过2个。
> - 由于设备共用音频通路，一个设备仅能有一个实例进行音频录制。创建第二个实例录制音频时，将会因为音频通路冲突导致创建失败。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**返回值：**

| 类型                                 | 说明                                                         |
| ------------------------------------ | ------------------------------------------------------------ |
| Promise\<[AVRecorder](#avrecorder9)> | Promise对象。异步返回AVRecorder实例，失败时返回null。可用于录制音视频媒体。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                      |
| -------- | ----------------------------- |
| 5400101  | No memory. Return by promise. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let avRecorder: media.AVRecorder;
media.createAVRecorder().then((recorder: media.AVRecorder) => {
  if (recorder != null) {
    avRecorder = recorder;
    console.info('createAVRecorder success');
  } else {
    console.error('createAVRecorder fail');
  }
}).catch((error: BusinessError) => {
  console.error(`createAVRecorder catchCallback, error message:${error.message}`);
});
```

## media.createAVMetadataExtractor<sup>11+</sup>

createAVMetadataExtractor(callback: AsyncCallback\<AVMetadataExtractor>): void

异步方式创建AVMetadataExtractor实例，通过注册回调函数获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.AVMetadataExtractor

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                                                         |
| -------- | ------------------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback\<[AVMetadataExtractor](#avmetadataextractor11)> | 是   | 回调函数。异步返回AVMetadataExtractor实例，失败时返回null。可用于获取音视频元信息。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                       |
| -------- | ------------------------------ |
| 5400101  | No memory. Returned by callback. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let avMetadataExtractor: media.AVMetadataExtractor;
media.createAVMetadataExtractor((error: BusinessError, extractor: media.AVMetadataExtractor) => {
  if (extractor != null) {
    avMetadataExtractor = extractor;
    console.info('createAVMetadataExtractor success');
  } else {
    console.error(`createAVMetadataExtractor fail, error message:${error.message}`);
  }
});
```

## media.createAVMetadataExtractor<sup>11+</sup>

createAVMetadataExtractor(): Promise\<AVMetadataExtractor>

异步方式创建AVMetadataExtractor对象，通过Promise获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.AVMetadataExtractor

**返回值：**

| 类型                            | 说明                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| Promise\<[AVMetadataExtractor](#avmetadataextractor11)> | Promise对象。异步返回AVMetadataExtractor实例，失败时返回null。可用于获取音视频元数据。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                      |
| -------- | ----------------------------- |
| 5400101  | No memory. Returned by promise. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let avMetadataExtractor: media.AVMetadataExtractor;
media.createAVMetadataExtractor().then((extractor: media.AVMetadataExtractor) => {
  if (extractor != null) {
    avMetadataExtractor = extractor;
    console.info('createAVMetadataExtractor success');
  } else {
    console.error('createAVMetadataExtractor fail');
  }
}).catch((error: BusinessError) => {
  console.error(`AVMetadataExtractor catchCallback, error message:${error.message}`);
});
```

## media.createSoundPool<sup>10+</sup>

createSoundPool(maxStreams: number, audioRenderInfo: audio.AudioRendererInfo, callback: AsyncCallback\<SoundPool>): void

创建音频池实例，使用callback方式异步获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.SoundPool

**参数：**

| 参数名   | 类型                                            | 必填 | 说明                                                         |
| -------- | ----------------------------------------------- | ---- | ------------------------------------------------------------ |
| maxStreams | number | 是   | soundPool实例的最大播放的流数 |
| audioRenderInfo | [audio.AudioRendererInfo](../apis-audio-kit/js-apis-audio.md#audiorendererinfo8)  | 是   | 音频播放参数信息 |
| callback | AsyncCallback<[SoundPool](js-apis-inner-multimedia-soundPool.md)> | 是   | 回调函数。异步返回SoundPool实例，失败时返回null。用于音频池实例的加载播放功能。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                       |
| -------- | ------------------------------ |
| 5400101  | No memory. Return by callback. |

**示例：**

```js
import audio from '@ohos.multimedia.audio'

let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage : audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags : 0
}

media.createSoundPool(5, audioRendererInfo, (error, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
  }
});
```

## media.createSoundPool<sup>10+</sup>

createSoundPool(maxStreams: number, audioRenderInfo: audio.AudioRendererInfo): Promise\<SoundPool>

创建音频池实例，使用Promise方式异步获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.SoundPool

**参数：**

| 参数名   | 类型                                            | 必填 | 说明                                                         |
| -------- | ----------------------------------------------- | ---- | ------------------------------------------------------------ |
| maxStreams | number | 是   | soundPool实例的最大播放的流数 |
| audioRenderInfo | [audio.AudioRendererInfo](../apis-audio-kit/js-apis-audio.md#audiorendererinfo8)  | 是   | 音频播放参数信息 |

**返回值：**

| 类型                                      | 说明                                                         |
| ----------------------------------------- | ------------------------------------------------------------ |
| Promise<[SoundPool](js-apis-inner-multimedia-soundPool.md)> | Promise对象。异步返回SoundPool实例，失败时返回null。用于音频池实例的加载播放功能。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                      |
| -------- | ----------------------------- |
| 5400101  | No memory. Return by promise. |

**示例：**

```js
import audio from '@ohos.multimedia.audio'
import { BusinessError } from '@ohos.base';

let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage : audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags : 0
}

media.createSoundPool(5, audioRendererInfo).then((soundpool_: media.SoundPool) => {
  if (soundpool_ != null) {
    soundPool = soundpool_;
    console.info('create SoundPool success');
  } else {
    console.error('create SoundPool fail');
  }
}, (error: BusinessError) => {
  console.error(`soundpool catchCallback, error message:${error.message}`);
});
```

## AVErrorCode<sup>9+</sup>

[媒体错误码](errorcode-media.md)类型枚举

**系统能力：** SystemCapability.Multimedia.Media.Core

| 名称                                  | 值      | 说明                                 |
| :------------------------------------ | ------- | ------------------------------------ |
| AVERR_OK                              | 0       | 表示操作成功。                       |
| AVERR_NO_PERMISSION                   | 201     | 表示无权限执行此操作。               |
| AVERR_INVALID_PARAMETER               | 401     | 表示传入入参无效。                   |
| AVERR_UNSUPPORT_CAPABILITY            | 801     | 表示当前版本不支持该API能力。        |
| AVERR_NO_MEMORY                       | 5400101 | 表示系统内存不足或服务数量达到上限。 |
| AVERR_OPERATE_NOT_PERMIT              | 5400102 | 表示当前状态不允许或无权执行此操作。 |
| AVERR_IO                              | 5400103 | 表示数据流异常信息。                 |
| AVERR_TIMEOUT                         | 5400104 | 表示系统或网络响应超时。             |
| AVERR_SERVICE_DIED                    | 5400105 | 表示服务进程死亡。                   |
| AVERR_UNSUPPORT_FORMAT                | 5400106 | 表示不支持当前媒体资源的格式。       |
| AVERR_AUDIO_INTERRUPTED<sup>11+</sup> | 5400107 | 表示音频焦点被抢占                   |

## MediaType<sup>8+</sup>

媒体类型枚举。

**系统能力：** SystemCapability.Multimedia.Media.Core

| 名称           | 值   | 说明       |
| -------------- | ---- | ---------- |
| MEDIA_TYPE_AUD | 0    | 表示音频。 |
| MEDIA_TYPE_VID | 1    | 表示视频。 |

## CodecMimeType<sup>8+</sup>

Codec MIME类型枚举。

**系统能力：** SystemCapability.Multimedia.Media.Core

| 名称         | 值                    | 说明                     |
| ------------ | --------------------- | ------------------------ |
| VIDEO_H263   | 'video/h263'          | 表示视频/h263类型。      |
| VIDEO_AVC    | 'video/avc'           | 表示视频/avc类型。       |
| VIDEO_MPEG2  | 'video/mpeg2'         | 表示视频/mpeg2类型。     |
| VIDEO_MPEG4  | 'video/mp4v-es'         | 表示视频/mpeg4类型。     |
| VIDEO_VP8    | 'video/x-vnd.on2.vp8' | 表示视频/vp8类型。       |
| VIDEO_HEVC<sup>11+</sup>   | 'video/hevc'          | 表示视频/H265类型。|
| AUDIO_AAC    | 'audio/mp4a-latm'     | 表示音频/mp4a-latm类型。 |
| AUDIO_VORBIS | 'audio/vorbis'        | 表示音频/vorbis类型。    |
| AUDIO_FLAC   | 'audio/flac'          | 表示音频/flac类型。      |

## MediaDescriptionKey<sup>8+</sup>

媒体信息描述枚举。

**系统能力：** SystemCapability.Multimedia.Media.Core

| 名称                     | 值              | 说明                                                         |
| ------------------------ | --------------- | ------------------------------------------------------------ |
| MD_KEY_TRACK_INDEX       | 'track_index'   | 表示轨道序号，其对应键值类型为number。                       |
| MD_KEY_TRACK_TYPE        | 'track_type'    | 表示轨道类型，其对应键值类型为number，参考[MediaType](#mediatype8)。 |
| MD_KEY_CODEC_MIME        | 'codec_mime'    | 表示codec_mime类型，其对应键值类型为string。                 |
| MD_KEY_DURATION          | 'duration'      | 表示媒体时长，其对应键值类型为number，单位为毫秒（ms）。     |
| MD_KEY_BITRATE           | 'bitrate'       | 表示比特率，其对应键值类型为number，单位为比特率（bps）。    |
| MD_KEY_WIDTH             | 'width'         | 表示视频宽度，其对应键值类型为number，单位为像素（px）。     |
| MD_KEY_HEIGHT            | 'height'        | 表示视频高度，其对应键值类型为number，单位为像素（px）。     |
| MD_KEY_FRAME_RATE        | 'frame_rate'    | 表示视频帧率，其对应键值类型为number，单位为100帧每秒（100fps）。 |
| MD_KEY_AUD_CHANNEL_COUNT | 'channel_count' | 表示声道数，其对应键值类型为number。                         |
| MD_KEY_AUD_SAMPLE_RATE   | 'sample_rate'   | 表示采样率，其对应键值类型为number，单位为赫兹（Hz）。       |

## BufferingInfoType<sup>8+</sup>

缓存事件类型枚举。

**系统能力：** SystemCapability.Multimedia.Media.Core

| 名称              | 值   | 说明                             |
| ----------------- | ---- | -------------------------------- |
| BUFFERING_START   | 1    | 表示开始缓存。                   |
| BUFFERING_END     | 2    | 表示结束缓存。                   |
| BUFFERING_PERCENT | 3    | 表示缓存百分比。                 |
| CACHED_DURATION   | 4    | 表示缓存时长，单位为毫秒（ms）。 |

## StateChangeReason<sup>9+</sup>

表示播放或录制实例状态机切换原因的枚举，伴随state一起上报。

**系统能力：** SystemCapability.Multimedia.Media.Core

| 名称       | 值   | 说明                                                         |
| ---------- | ---- | ------------------------------------------------------------ |
| USER       | 1    | 表示用户行为造成的状态切换，由用户或客户端主动调用接口产生。 |
| BACKGROUND | 2    | 表示后台系统行为造成的状态切换，比如应用未注册播控中心权限，退到后台时被系统强制暂停或停止。 |

## AVPlayer<sup>9+</sup>

播放管理类，用于管理和播放媒体资源。在调用AVPlayer的方法前，需要先通过[createAVPlayer()](#mediacreateavplayer9)构建一个AVPlayer实例。

Audio/Video播放demo可参考：[音频播放开发指导](../../media/media/using-avplayer-for-playback.md)、[视频播放开发指导](../../media/media/video-playback.md)。

### 属性

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

| 名称                                                | 类型                                                         | 可读 | 可写 | 说明                                                         |
| --------------------------------------------------- | ------------------------------------------------------------ | ---- | ---- | ------------------------------------------------------------ |
| url<sup>9+</sup>                                    | string                                                       | 是   | 是   | 媒体URL，只允许在**idle**状态下设置。<br/>支持的视频格式(mp4、mpeg-ts、mkv)。<br>支持的音频格式(m4a、aac、mp3、ogg、wav、flac)。<br/>**支持路径示例**：<br>1. fd类型播放：fd://xx。<br>![](figures/zh-cn_image_url.png)<br>2. http网络播放: http\://xx。<br/>3. https网络播放: https\://xx。<br/>4. hls网络播放路径：http\://xx或者https\://xx。<br>**说明：**<br>从API version 11开始不支持webm。 |
| fdSrc<sup>9+</sup>                                  | [AVFileDescriptor](#avfiledescriptor9)                       | 是   | 是   | 媒体文件描述，只允许在**idle**状态下设置。<br/>使用场景：应用中的媒体资源被连续存储在同一个文件中。<br/>支持的视频格式(mp4、mpeg-ts、mkv)。<br>支持的音频格式(m4a、aac、mp3、ogg、wav、flac)。<br/>**使用示例**：<br/>假设一个连续存储的媒体文件: <br/>视频1(地址偏移:0，字节长度:100)；<br/>视频2(地址偏移:101，字节长度:50)；<br/>视频3(地址偏移:151，字节长度:150)；<br/>1. 播放视频1：AVFileDescriptor { fd = 资源句柄; offset = 0; length = 100; }。<br/>2. 播放视频2：AVFileDescriptor { fd = 资源句柄; offset = 101; length = 50; }。<br/>3. 播放视频3：AVFileDescriptor { fd = 资源句柄; offset = 151; length = 150; }。<br/>假设是一个独立的媒体文件: 请使用src=fd://xx。<br>**说明：**<br>从API version 11开始不支持webm。 |
| dataSrc<sup>10+</sup>                               | [AVDataSrcDescriptor](#avdatasrcdescriptor10)                | 是   | 是   | 流式媒体资源描述，只允许在**idle**状态下设置。<br/>使用场景：应用播放从远端下载到本地的文件，在应用未下载完整音视频资源时，提前播放已获取的资源文件。<br/>支持的视频格式(mp4、mpeg-ts、mkv)。<br>支持的音频格式(m4a、aac、mp3、ogg、wav、flac)。<br/>**使用示例**：<br/>假设用户正在从远端服务器获取音视频媒体文件，希望下载到本地的同时播放已经下载好的部分: <br/>1.用户需要获取媒体文件的总大小size（单位为字节），获取不到时设置为-1。<br/>2.用户需要实现回调函数func用于填写数据，如果size = -1，则func形式为：func(buffer: ArrayBuffer, length: number)，此时播放器只会按照顺序获取数据；否则func形式为：func(buffer: ArrayBuffer, length: number, pos: number)，播放器会按需跳转并获取数据。<br/>3.用户设置AVDataSrcDescriptor {fileSize = size, callback = func}。<br/>**注意事项**：<br/>如果播放的是mp4/m4a格式用户需要保证moov字段（媒体信息字段）在mdat字段（媒体数据字段）之前，或者moov之前的字段小于10M，否则会导致解析失败无法播放。<br>**说明：**<br>从API version 11开始不支持webm。 |
| surfaceId<sup>9+</sup>                              | string                                                       | 是   | 是   | 视频窗口ID，默认无窗口，只允许在**initialized**状态下设置。<br/>使用场景：视频播放的窗口渲染，纯音频播放不用设置。<br/>**使用示例**：<br/>[通过Xcomponent创建surfaceId](../apis-arkui/arkui-ts/ts-basic-components-xcomponent.md#getxcomponentsurfaceid)。 |
| loop<sup>9+</sup>                                   | boolean                                                      | 是   | 是   | 视频循环播放属性，默认'false'，设置为'true'表示循环播放，动态属性。<br/>只允许在**prepared**/**playing**/**paused**/**completed**状态下设置。<br/>直播场景不支持loop设置。 |
| videoScaleType<sup>9+</sup>                         | [VideoScaleType](#videoscaletype9)                           | 是   | 是   | 视频缩放模式，默认VIDEO_SCALE_TYPE_FIT，动态属性。<br/>只允许在**prepared**/**playing**/**paused**/**completed**状态下设置。 |
| audioInterruptMode<sup>9+</sup>                     | [audio.InterruptMode](../apis-audio-kit/js-apis-audio.md#interruptmode9)       | 是   | 是   | 音频焦点模型，默认SHARE_MODE，动态属性。<br/>只允许在**prepared**/**playing**/**paused**/**completed**状态下设置。<br/>在第一次调用[play()](#play9)之前设置， 以便此后中断模式生效。 |
| audioRendererInfo<sup>10+</sup>                     | [audio.AudioRendererInfo](../apis-audio-kit/js-apis-audio.md#audiorendererinfo8) | 是   | 是   | 设置音频渲染信息，默认值usage为STREAM_USAGE_MUSIC，rendererFlags为0。<br/>只允许在**initialized**状态下设置。<br/>在第一次调用[prepare()](#prepare9)之前设置，以便音频渲染器信息在之后生效。 |
| audioEffectMode<sup>10+</sup>                       | [audio.AudioEffectMode](../apis-audio-kit/js-apis-audio.md#audioeffectmode10)  | 是   | 是   | 设置音频音效模式，默认值为EFFECT_DEFAULT，动态属性。audioRendererInfo的usage变动时会恢复为默认值，只允许在**prepared**/**playing**/**paused**/**completed**状态下设置。 |
| state<sup>9+</sup>                                  | [AVPlayerState](#avplayerstate9)                             | 是   | 否   | 音视频播放的状态，全状态有效，可查询参数。                   |
| currentTime<sup>9+</sup>                            | number                                                       | 是   | 否   | 视频的当前播放位置，单位为毫秒（ms），可查询参数。<br/>返回为(-1)表示无效值，**prepared**/**playing**/**paused**/**completed**状态下有效。<br/>直播场景默认返回(-1)。 |
| duration<sup>9+</sup> | number                                                       | 是   | 否   | 视频时长，单位为毫秒（ms），可查询参数。<br/>返回为(-1)表示无效值，**prepared**/**playing**/**paused**/**completed**状态下有效。<br/>直播场景默认返回(-1)。 |
| width<sup>9+</sup>                                  | number                                                       | 是   | 否   | 视频宽，单位为像素（px），可查询参数。<br/>返回为(0)表示无效值，**prepared**/**playing**/**paused**/**completed**状态下有效。 |
| height<sup>9+</sup>                                 | number                                                       | 是   | 否   | 视频高，单位为像素（px），可查询参数。<br/>返回为(0)表示无效值，**prepared**/**playing**/**paused**/**completed**状态下有效。 |

**说明：**

将资源句柄（fd）传递给媒体播放器之后，请不要通过该资源句柄做其他读写操作，包括但不限于将同一个资源句柄传递给多个媒体播放器。同一时间通过同一个资源句柄读写文件时存在竞争关系，将导致播放异常。

### on('stateChange')<sup>9+</sup>

on(type: 'stateChange', callback: (state: AVPlayerState, reason: StateChangeReason) => void): void

监听播放状态机AVPlayerState切换的事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | 状态机切换事件回调类型，支持的事件：'stateChange'，用户操作和系统都会触发此事件。 |
| callback | function | 是   | 状态机切换事件回调方法：<br/>state: [AVPlayerState](#avplayerstate9)，表示当前播放状态；<br/>reason: [StateChangeReason](#statechangereason9)，表示当前播放状态的切换原因。 |

**示例：**

```ts
avPlayer.on('stateChange', async (state: string, reason: media.StateChangeReason) => {
  switch (state) {
    case 'idle':
      console.info('state idle called');
      break;
    case 'initialized':
      console.info('initialized prepared called');
      break;
    case 'prepared':
      console.info('state prepared called');
      break;
    case 'playing':
      console.info('state playing called');
      break;
    case 'paused':
      console.info('state paused called');
      break;
    case 'completed':
      console.info('state completed called');
      break;
    case 'stopped':
      console.info('state stopped called');
      break;
    case 'released':
      console.info('state released called');
      break;
    case 'error':
      console.info('state error called');
      break;
    default:
      console.info('unknown state :' + state);
      break;
  }
})
```

### off('stateChange')<sup>9+</sup>

off(type: 'stateChange'): void

取消监听播放状态机[AVPlayerState](#avplayerstate9)切换的事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                  |
| ------ | ------ | ---- | ----------------------------------------------------- |
| type   | string | 是   | 状态机切换事件回调类型，取消注册的事件：'stateChange' |

**示例：**

```ts
avPlayer.off('stateChange')
```

### on('error')<sup>9+</sup>

on(type: 'error', callback: ErrorCallback): void

监听[AVPlayer](#avplayer9)的错误事件，该事件仅用于错误提示，不需要用户停止播控动作。如果此时[AVPlayerState](#avplayerstate9)也切至error状态，用户需要通过[reset()](#reset9)或者[release()](#release9)退出播放操作。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | 错误事件回调类型，支持的事件：'error'，用户操作和系统都会触发此事件。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback) | 是   | 错误事件回调方法：使用播放器的过程中发生错误，会提供错误码ID和错误信息。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息              |
| -------- | --------------------- |
| 201      | Permission denied     |
| 401      | The parameter check failed. |
| 801      | Capability not supported. |
| 5400101  | No Memory. Return by callback. |
| 5400102  | Operation not allowed.|
| 5400103  | I/O error             |
| 5400104  | Time out              |
| 5400105  | Service Died.         |
| 5400106  | Unsupport Format.     |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avPlayer.on('error', (error: BusinessError) => {
  console.info('error happened,and error message is :' + error.message)
  console.info('error happened,and error code is :' + error.code)
})
```

### off('error')<sup>9+</sup>

off(type: 'error'): void

取消监听播放的错误事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                      |
| ------ | ------ | ---- | ----------------------------------------- |
| type   | string | 是   | 错误事件回调类型，取消注册的事件：'error' |

**示例：**

```ts
avPlayer.off('error')
```

### prepare<sup>9+</sup>

prepare(callback: AsyncCallback\<void>): void

通过回调方式准备播放音频/视频，需在[stateChange](#onstatechange9)事件成功触发至initialized状态后，才能调用。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                 |
| -------- | -------- | ---- | -------------------- |
| callback | function | 是   | 准备播放的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400102  | Operation not allowed. Return by callback. |
| 5400106  | Unsupport format. Return by callback.      |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avPlayer.prepare((err: BusinessError) => {
  if (err == null) {
    console.info('prepare success');
  } else {
    console.error('prepare filed,error message is :' + err.message)
  }
})
```

### prepare<sup>9+</sup>

prepare(): Promise\<void>

通过Promise方式准备播放音频/视频，需在[stateChange](#onstatechange9)事件成功触发至initialized状态后，才能调用。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**返回值：**

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | 准备播放的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                                  |
| -------- | ----------------------------------------- |
| 5400102  | Operation not allowed. Return by promise. |
| 5400106  | Unsupport format. Return by promise.      |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avPlayer.prepare().then(() => {
  console.info('prepare success');
}, (err: BusinessError) => {
  console.error('prepare filed,error message is :' + err.message)
})
```

### play<sup>9+</sup>

play(callback: AsyncCallback\<void>): void

通过回调方式开始播放音视频资源，只能在prepared/paused/completed状态调用。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                 |
| -------- | -------- | ---- | -------------------- |
| callback | function | 是   | 开始播放的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400102  | Operation not allowed. Return by callback. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avPlayer.play((err: BusinessError) => {
  if (err == null) {
    console.info('play success');
  } else {
    console.error('play filed,error message is :' + err.message)
  }
})
```

### play<sup>9+</sup>

play(): Promise\<void>

通过Promise方式开始播放音视频资源，只能在prepared/paused/completed状态调用。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**返回值：**

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | 开始播放的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                  |
| -------- | ----------------------------------------- |
| 5400102  | Operation not allowed. Return by promise. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avPlayer.play().then(() => {
  console.info('play success');
}, (err: BusinessError) => {
  console.error('play filed,error message is :' + err.message)
})
```

### pause<sup>9+</sup>

pause(callback: AsyncCallback\<void>): void

通过回调方式暂停播放音视频资源，只能在playing状态调用。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                 |
| -------- | -------- | ---- | -------------------- |
| callback | function | 是   | 暂停播放的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400102  | Operation not allowed. Return by callback. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avPlayer.pause((err: BusinessError) => {
  if (err == null) {
    console.info('pause success');
  } else {
    console.error('pause filed,error message is :' + err.message)
  }
})
```

### pause<sup>9+</sup>

pause(): Promise\<void>

通过Promise方式暂停播放音视频资源，只能在playing状态调用。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**返回值：**

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | 暂停播放的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                  |
| -------- | ----------------------------------------- |
| 5400102  | Operation not allowed. Return by promise. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avPlayer.pause().then(() => {
  console.info('pause success');
}, (err: BusinessError) => {
  console.error('pause filed,error message is :' + err.message)
})
```

### stop<sup>9+</sup>

stop(callback: AsyncCallback\<void>): void

通过回调方式停止播放音视频资源，只能在prepared/playing/paused/completed状态调用。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                 |
| -------- | -------- | ---- | -------------------- |
| callback | function | 是   | 停止播放的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400102  | Operation not allowed. Return by callback. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avPlayer.stop((err: BusinessError) => {
  if (err == null) {
    console.info('stop success');
  } else {
    console.error('stop filed,error message is :' + err.message)
  }
})
```

### stop<sup>9+</sup>

stop(): Promise\<void>

通过Promise方式停止播放音视频资源，只能在prepared/playing/paused/completed状态调用。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**返回值：**

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | 停止播放的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                  |
| -------- | ----------------------------------------- |
| 5400102  | Operation not allowed. Return by promise. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avPlayer.stop().then(() => {
  console.info('stop success');
}, (err: BusinessError) => {
  console.error('stop filed,error message is :' + err.message)
})
```

### reset<sup>9+</sup>

reset(callback: AsyncCallback\<void>): void

通过回调方式重置播放，只能在initialized/prepared/playing/paused/completed/stopped/error状态调用。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                 |
| -------- | -------- | ---- | -------------------- |
| callback | function | 是   | 重置播放的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400102  | Operation not allowed. Return by callback. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avPlayer.reset((err: BusinessError) => {
  if (err == null) {
    console.info('reset success');
  } else {
    console.error('reset filed,error message is :' + err.message)
  }
})
```

### reset<sup>9+</sup>

reset(): Promise\<void>

通过Promise方式重置播放，只能在initialized/prepared/playing/paused/completed/stopped/error状态调用。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**返回值：**

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | 重置播放的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                  |
| -------- | ----------------------------------------- |
| 5400102  | Operation not allowed. Return by promise. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avPlayer.reset().then(() => {
  console.info('reset success');
}, (err: BusinessError) => {
  console.error('reset filed,error message is :' + err.message)
})
```

### release<sup>9+</sup>

release(callback: AsyncCallback\<void>): void

通过回调方式销毁播放资源，除released状态，都可以调用。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                 |
| -------- | -------- | ---- | -------------------- |
| callback | function | 是   | 销毁播放的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400102  | Operation not allowed. Return by callback. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avPlayer.release((err: BusinessError) => {
  if (err == null) {
    console.info('release success');
  } else {
    console.error('release filed,error message is :' + err.message)
  }
})
```

### release<sup>9+</sup>

release(): Promise\<void>

通过Promise方式销毁播放，除released状态，都可以调用。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**返回值：**

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | 销毁播放的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                  |
| -------- | ----------------------------------------- |
| 5400102  | Operation not allowed. Return by promise. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avPlayer.release().then(() => {
  console.info('release success');
}, (err: BusinessError) => {
  console.error('release filed,error message is :' + err.message)
})
```

### getTrackDescription<sup>9+</sup>

getTrackDescription(callback: AsyncCallback\<Array\<MediaDescription>>): void

通过回调方式获取音视频轨道信息，可以在prepared/playing/paused状态调用。获取所有音视轨道信息，应在数据加载回调后调用。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                         |
| -------- | ------------------------------------------------------------ | ---- | -------------------------------------------- |
| callback | AsyncCallback<Array<[MediaDescription](#mediadescription8)>> | 是   | 音视频轨道信息MediaDescription数组回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400102  | Operation not allowed. Return by callback. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avPlayer.getTrackDescription((error: BusinessError, arrList: Array<media.MediaDescription>) => {
  if ((arrList) != null) {
    console.info('getTrackDescription success');
  } else {
    console.error(`video getTrackDescription fail, error:${error}`);
  }
});
```

### getTrackDescription<sup>9+</sup>

getTrackDescription(): Promise\<Array\<MediaDescription>>

通过Promise方式获取音视频轨道信息，可以在prepared/playing/paused状态调用。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**返回值：**

| 类型                                                   | 说明                                              |
| ------------------------------------------------------ | ------------------------------------------------- |
| Promise<Array<[MediaDescription](#mediadescription8)>> | 音视频轨道信息MediaDescription数组Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                  |
| -------- | ----------------------------------------- |
| 5400102  | Operation not allowed. Return by promise. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avPlayer.getTrackDescription().then((arrList: Array<media.MediaDescription>) => {
  console.info('getTrackDescription success');
}).catch((error: BusinessError) => {
  console.error(`video catchCallback, error:${error}`);
});
```

### setDecryptionConfig<sup>11+</sup>

setDecryptionConfig(mediaKeySession: drm.MediaKeySession, secureVideoPath: boolean): void

设置解密配置。当收到[mediaKeySystemInfoUpdate事件](#onmediakeysysteminfoupdate11)时，需根据事件上报的信息创建相关配置并设置解密配置，否则无法播放。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                         |
| -------- | ------------------------------------------------------------ | ---- | -------------------------------------------- |
| mediaKeySession | [drm.MediaKeySession](../apis-drm-kit/js-apis-drm.md#mediakeysession) | 是   | 解密会话 |
| secureVideoPath | boolean | 是 | 安全视频通路，true表示选择安全视频通路，false表示选择非安全视频通路 |

**示例：**

关于drm模块的示例具体可见[js-apis-drm.md](../apis-drm-kit/js-apis-drm.md)。
```ts
import drm from '@ohos.multimedia.drm'

// 创建MediaKeySystem系统
let keySystem:drm.MediaKeySystem = drm.createMediaKeySystem('com.clearplay.drm');
// 创建MediaKeySession解密会话
let keySession:drm.MediaKeySession = keySystem.createMediaKeySession(drm.ContentProtectionLevel.CONTENT_PROTECTION_LEVEL_SW_CRYPTO);
// 安全视频通路标志
let secureVideoPath:boolean = false;
// 设置解密配置
avPlayer.setDecryptionConfig(keySession, secureVideoPath);
```

### getMediaKeySystemInfos<sup>11+</sup>

getMediaKeySystemInfos(): Array\<drm.MediaKeySystemInfo>

获取当前播放的媒体资源的MediaKeySystemInfo。需要在[mediaKeySystemInfoUpdate事件](#onmediakeysysteminfoupdate11)触发成功后才能调用。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**返回值：**

| 类型                                                   | 说明                                              |
| ------------------------------------------------------ | ------------------------------------------------- |
|  Array<[drm.MediaKeySystemInfo](../apis-drm-kit/js-apis-drm.md#mediakeysysteminfo)> | MediaKeySystemInfo数组，MediaKeySystemInfo具有uuid和pssh两个属性。 |

**示例：**

```ts
import drm from '@ohos.multimedia.drm'

const infos = avPlayer.getMediaKeySystemInfos();
console.info('GetMediaKeySystemInfos count: ' + infos.length);
for (var i = 0; i < infos.length; i++) {
  console.info('GetMediaKeySystemInfos uuid: ' + infos[i]["uuid"]);
  console.info('GetMediaKeySystemInfos pssh: ' + infos[i]["pssh"]);
}
```

### seek<sup>9+</sup>

seek(timeMs: number, mode?:SeekMode): void

跳转到指定播放位置，只能在prepared/playing/paused/completed状态调用，可以通过[seekDone事件](#onseekdone9)确认是否生效。
注：直播场景不支持seek。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名 | 类型                   | 必填 | 说明                                                         |
| ------ | ---------------------- | ---- | ------------------------------------------------------------ |
| timeMs | number                 | 是   | 指定的跳转时间节点，单位毫秒（ms），取值范围为[0, [duration](#属性)]。 |
| mode   | [SeekMode](#seekmode8) | 否   | 基于视频I帧的跳转模式，默认为SEEK_PREV_SYNC模式，**仅在视频资源播放时设置**。 |

**示例：**

```ts
let seekTime: number = 1000
avPlayer.seek(seekTime, media.SeekMode.SEEK_PREV_SYNC)
```

### on('seekDone')<sup>9+</sup>

on(type: 'seekDone', callback: Callback\<number>): void

监听seek生效的事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | seek生效的事件回调类型，支持的事件：'seekDone'，每次调用seek后都会回调此事件。 |
| callback | Callback\<number> | 是   | seek生效的事件回调方法，只会上报用户请求的time位置。<br/>**视频播放：**[SeekMode](#seekmode8)会造成实际跳转位置与用户设置产生偏差，精准位置需要通过currentTime获取，事件回调的time仅代表完成用户某一次请求。 |

**示例：**

```ts
avPlayer.on('seekDone', (seekDoneTime:number) => {
  console.info('seekDone success,and seek time is:' + seekDoneTime)
})
```

### off('seekDone')<sup>9+</sup>

off(type: 'seekDone'): void

取消监听seek生效的事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                 |
| ------ | ------ | ---- | ---------------------------------------------------- |
| type   | string | 是   | seek生效的事件回调类型，取消注册的事件：'seekDone'。 |

**示例：**

```ts
avPlayer.off('seekDone')
```

### setSpeed<sup>9+</sup>

setSpeed(speed: PlaybackSpeed): void

设置倍速模式，只能在prepared/playing/paused/completed状态调用，可以通过[speedDone事件](#onspeeddone9)确认是否生效。
注：直播场景不支持setSpeed。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名 | 类型                             | 必填 | 说明               |
| ------ | -------------------------------- | ---- | ------------------ |
| speed  | [PlaybackSpeed](#playbackspeed8) | 是   | 指定播放倍速模式。 |

**示例：**

```ts
avPlayer.setSpeed(media.PlaybackSpeed.SPEED_FORWARD_2_00_X)
```

### on('speedDone')<sup>9+</sup>

on(type: 'speedDone', callback: Callback\<number>): void

监听setSpeed生效的事件

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | setSpeed生效的事件回调类型，支持的事件：'speedDone'，每次调用setSpeed后都会回调此事件。 |
| callback | Callback\<number> | 是   | setSpeed生效的事件回调方法，上报生效的倍速模式，具体见[PlaybackSpeed](#playbackspeed8)。 |

**示例：**

```ts
avPlayer.on('speedDone', (speed:number) => {
  console.info('speedDone success,and speed value is:' + speed)
})
```

### off('speedDone')<sup>9+</sup>

off(type: 'speedDone'): void

取消监听setSpeed生效的事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                      |
| ------ | ------ | ---- | --------------------------------------------------------- |
| type   | string | 是   | setSpeed生效的事件回调类型，取消注册的事件：'speedDone'。 |

**示例：**

```ts
avPlayer.off('speedDone')
```

### setBitrate<sup>9+</sup>

setBitrate(bitrate: number): void

选择要播放的指定比特率，仅对**HLS协议网络流**有效，默认情况下，播放器会根据网络连接速度选择合适的比特率，只能在prepared/playing/paused/completed状态调用，可以通过[bitrateDone](#onbitratedone9)事件确认是否生效。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名  | 类型   | 必填 | 说明                                                         |
| ------- | ------ | ---- | ------------------------------------------------------------ |
| bitrate | number | 是   | 指定比特率，可以通过[availableBitrates](#onavailablebitrates9)事件获得当前HLS协议流可用的比特率，如果用户指定的比特率不在此列表中，则播放器将从可用比特率列表中选择最小和最接近的比特率。如果通过availableBitrates事件获得的比特率列表长度为0，则不支持指定比特率，也不会产生bitrateDone回调。 |

**示例：**

```ts
let bitrate: number = 96000
avPlayer.setBitrate(bitrate)
```

### on('bitrateDone')<sup>9+</sup>

on(type: 'bitrateDone', callback: Callback\<number>): void

监听setBitrate生效的事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | setBitrate生效的事件回调类型，支持的事件：'bitrateDone'，每次调用setBitrate后都会回调此事件。 |
| callback | function | 是   | setBitrate生效的事件回调方法，上报生效的比特率。             |

**示例：**

```ts
avPlayer.on('bitrateDone', (bitrate:number) => {
  console.info('bitrateDone success,and bitrate value is:' + bitrate)
})
```

### off('bitrateDone')<sup>9+</sup>

off(type: 'bitrateDone'): void

取消监听setBitrate生效的事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| type   | string | 是   | setBitrate生效的事件回调类型，取消注册的事件：'bitrateDone'。 |

**示例：**

```ts
avPlayer.off('bitrateDone')
```

### on('availableBitrates')<sup>9+</sup>

on(type: 'availableBitrates', callback: (bitrates: Array\<number>) => void): void

监听HLS协议流可用的比特率列表，只会在切换prepared状态后上报。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | HLS协议可用比特率上报事件回调类型，支持的事件：'availableBitrates'，只会在prepared之后上报一次。 |
| callback | function | 是   | HLS协议可用比特率上报事件回调方法，使用数组存放支持的比特率。如果数组长度为0，则不支持指定比特率。 |

**示例：**

```ts
avPlayer.on('availableBitrates', (bitrates: Array<number>) => {
  console.info('availableBitrates success,and availableBitrates length is:' + bitrates.length)
})
```

### off('availableBitrates')<sup>9+</sup>

off(type: 'availableBitrates'): void

取消监听HLS协议流可用的比特率列表，调用[prepare](#prepare9)后，上报此事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| type   | string | 是   | HLS协议可用比特率上报事件回调类型，取消注册的事件：'availableBitrates'。 |

**示例：**

```ts
avPlayer.off('availableBitrates')
```


### on('mediaKeySystemInfoUpdate')<sup>11+</sup>

on(type: 'mediaKeySystemInfoUpdate', callback: (mediaKeySystemInfo: Array\<drm.MediaKeySystemInfo>) => void): void

监听mediaKeySystemInfoUpdate事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | 版权保护信息更新上报事件回调类型，支持的事件：'mediaKeySystemInfoUpdate'，当播放内容的版权保护信息更新时上报事件。 |
| callback | function | 是   | 版权保护信息更新上报事件回调方法，上报MediaKeySystemInfo数组，具体可见[MediaKeySystemInfo](../apis-drm-kit/js-apis-drm.md#mediakeysysteminfo)。 |

**示例：**

```ts

import drm from './@ohos.multimedia.drm';

avPlayer.on('mediaKeySystemInfoUpdate', (mediaKeySystemInfo: Array<drm.MediaKeySystemInfo>) => {
    for (var i = 0; i < mediaKeySystemInfo.length; i++) {
      console.info('mediaKeySystemInfoUpdate happened uuid: ' + mediaKeySystemInfo[i]["uuid"]);
      console.info('mediaKeySystemInfoUpdate happened pssh: ' + mediaKeySystemInfo[i]["pssh"]);
    }
})
```

### off('mediaKeySystemInfoUpdate')<sup>11+</sup>

off(type: 'mediaKeySystemInfoUpdate', callback?: (mediaKeySystemInfo: Array<drm.MediaKeySystemInfo>) => void): void;

取消监听mediaKeySystemInfoUpdate事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| type   | string | 是   | 版权保护信息更新上报事件回调类型，取消注册的事件：'mediaKeySystemInfoUpdate'。 |
| callback | function | 否   | 版权保护信息更新上报事件回调方法，上报版权保护信息数组，具体可见[MediaKeySystemInfo](../apis-drm-kit/js-apis-drm.md#mediakeysysteminfo)。如填写该参数，则仅取消注册此回调方法，否则取消注册mediaKeySystemInfoUpdate事件的所有回调方法。 |

**示例：**

```ts
avPlayer.off('mediaKeySystemInfoUpdate')
```

### setVolume<sup>9+</sup>

setVolume(volume: number): void

设置媒体播放音量，只能在prepared/playing/paused/completed状态调用，可以通过[volumeChange事件](#onvolumechange9)确认是否生效。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| volume | number | 是   | 指定的相对音量大小，取值范围为[0.00-1.00]，1表示最大音量，即100%。 |

**示例：**

```ts
let volume: number = 1.0
avPlayer.setVolume(volume)
```

### on('volumeChange')<sup>9+</sup>

on(type: 'volumeChange', callback: Callback\<number>): void

监听setVolume生效的事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | setVolume生效的事件回调类型，支持的事件：'volumeChange'，每次调用setVolume后都会回调此事件。 |
| callback | function | 是   | setVolume生效的事件回调方法，上报生效的媒体音量。            |

**示例：**

```ts
avPlayer.on('volumeChange', (vol: number) => {
  console.info('volumeChange success,and new volume is :' + vol)
})
```

### off('volumeChange')<sup>9+</sup>

off(type: 'volumeChange'): void

取消监听setVolume生效的事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| type   | string | 是   | setVolume生效的事件回调类型，取消注册的事件：'volumeChange'。 |

**示例：**

```ts
avPlayer.off('volumeChange')
```

### on('endOfStream')<sup>9+</sup>

on(type: 'endOfStream', callback: Callback\<void>): void

监听资源播放至结尾的事件；如果用户设置[loop](#属性)=true，播放会跳转至开头重播；如果用户没有设置loop，会通过[stateChange](#onstatechange9)上报completed状态。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | 资源播放至结尾的事件回调类型，支持的事件：'endOfStream'，当播放至结尾时会上报此事件。 |
| callback | Callback\<void> | 是   | 资源播放至结尾的事件回调方法。                               |

**示例：**

```ts
avPlayer.on('endOfStream', () => {
  console.info('endOfStream success')
})
```

### off('endOfStream')<sup>9+</sup>

off(type: 'endOfStream'): void

取消监听资源播放至结尾的事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| type   | string | 是   | 资源播放至结尾的事件回调类型，取消注册的事件：'endOfStream'。 |

**示例：**

```ts
avPlayer.off('endOfStream')
```

### on('timeUpdate')<sup>9+</sup>

on(type: 'timeUpdate', callback: Callback\<number>): void

监听资源播放当前时间，单位为毫秒（ms），用于刷新进度条当前位置，默认间隔100ms时间上报，因用户操作(seek)产生的时间变化会立刻上报。
注：直播场景不支持timeUpdate上报。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                           |
| -------- | -------- | ---- | ---------------------------------------------- |
| type     | string   | 是   | 时间更新的回调类型，支持的事件：'timeUpdate'。 |
| callback | function | 是   | 当前时间。                                     |

**示例：**

```ts
avPlayer.on('timeUpdate', (time:number) => {
  console.info('timeUpdate success,and new time is :' + time)
})
```

### off('timeUpdate')<sup>9+</sup>

off(type: 'timeUpdate'): void

取消监听资源播放当前时间。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                               |
| ------ | ------ | ---- | -------------------------------------------------- |
| type   | string | 是   | 时间更新的回调类型，取消注册的事件：'timeUpdate'。 |

**示例：**

```ts
avPlayer.off('timeUpdate')
```

### on('durationUpdate')<sup>9+</sup>


on(type: 'durationUpdate', callback: Callback\<number>): void

监听资源播放资源的时长，单位为毫秒（ms），用于刷新进度条长度，默认只在prepared上报一次，同时允许一些特殊码流刷新多次时长。
注：直播场景不支持durationUpdate上报。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                               |
| -------- | -------- | ---- | -------------------------------------------------- |
| type     | string   | 是   | 时长更新的回调类型，支持的事件：'durationUpdate'。 |
| callback | function | 是   | 资源时长。                                         |

**示例：**

```ts
avPlayer.on('durationUpdate', (duration: number) => {
  console.info('durationUpdate success,new duration is :' + duration)
})
```

### off('durationUpdate')<sup>9+</sup>

off(type: 'durationUpdate'): void

取消监听资源播放资源的时长。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                   |
| ------ | ------ | ---- | ------------------------------------------------------ |
| type   | string | 是   | 时长更新的回调类型，取消注册的事件：'durationUpdate'。 |

**示例：**

```ts
avPlayer.off('durationUpdate')
```

### on('bufferingUpdate')<sup>9+</sup>

on(type: 'bufferingUpdate', callback: (infoType: BufferingInfoType, value: number) => void): void

订阅音视频缓存更新事件，仅网络播放支持该订阅事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | 播放缓存事件回调类型，支持的事件：'bufferingUpdate'。        |
| callback | function | 是   | 播放缓存事件回调方法。<br/>[BufferingInfoType](#bufferinginfotype8)为BUFFERING_PERCENT或CACHED_DURATION时，value值有效，否则固定为0。 |

**示例：**

```ts
avPlayer.on('bufferingUpdate', (infoType: media.BufferingInfoType, value: number) => {
  console.info('bufferingUpdate success,and infoType value is:' + infoType + ', value is :' + value)
})
```

### off('bufferingUpdate')<sup>9+</sup>

off(type: 'bufferingUpdate'): void

取消监听音视频缓存更新事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                      |
| ------ | ------ | ---- | --------------------------------------------------------- |
| type   | string | 是   | 播放缓存事件回调类型，取消注册的事件：'bufferingUpdate'。 |

**示例：**

```ts
avPlayer.off('bufferingUpdate')
```

### on('startRenderFrame')<sup>9+</sup>

on(type: 'startRenderFrame', callback: Callback\<void>): void

订阅视频播放开始首帧渲染的更新事件，仅视频播放支持该订阅事件，该事件仅代表播放服务将第一帧画面送显示模块，实际效果依赖显示服务渲染性能。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | 视频播放开始首帧渲染事件回调类型，支持的事件：'startRenderFrame'。 |
| callback | Callback\<void> | 是   | 视频播放开始首帧渲染事件回调方法。                           |

**示例：**

```ts
avPlayer.on('startRenderFrame', () => {
  console.info('startRenderFrame success')
})
```

### off('startRenderFrame')<sup>9+</sup>

off(type: 'startRenderFrame'): void

取消监听视频播放开始首帧渲染的更新事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| type   | string | 是   | 视频播放开始首帧渲染事件回调类型，取消注册的事件：'startRenderFrame'。 |

**示例：**

```ts
avPlayer.off('startRenderFrame')
```

### on('videoSizeChange')<sup>9+</sup>

on(type: 'videoSizeChange', callback: (width: number, height: number) => void): void

监听视频播放宽高变化事件，仅视频播放支持该订阅事件，默认只在prepared状态上报一次，但HLS协议码流会在切换分辨率时上报；

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | 视频播放宽高变化事件回调类型，支持的事件：'videoSizeChange'。 |
| callback | function | 是   | 视频播放宽高变化事件回调方法，width表示宽，height表示高。    |

**示例：**

```ts
avPlayer.on('videoSizeChange', (width: number, height: number) => {
  console.info('videoSizeChange success,and width is:' + width + ', height is :' + height)
})
```

### off('videoSizeChange')<sup>9+</sup>

off(type: 'videoSizeChange'): void

取消监听视频播放宽高变化事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| type   | string | 是   | 视频播放宽高变化事件回调类型，取消注册的事件：'videoSizeChange'。 |

**示例：**

```ts
avPlayer.off('videoSizeChange')
```

### on('audioInterrupt')<sup>9+</sup>

on(type: 'audioInterrupt', callback: (info: audio.InterruptEvent) => void): void

监听音频焦点变化事件，多个音视频资源同时播放时，会根据音频焦点模型[audio.InterruptMode](../apis-audio-kit/js-apis-audio.md#interruptmode9)触发此事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                     |
| -------- | ------------------------------------------------------------ | ---- | -------------------------------------------------------- |
| type     | string                                                       | 是   | 音频焦点变化事件回调类型，支持的事件：'audioInterrupt'。 |
| callback | [audio.InterruptEvent<sup>9+</sup>](../apis-audio-kit/js-apis-audio.md#interruptevent9) | 是   | 音频焦点变化事件回调方法。                               |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

avPlayer.on('audioInterrupt', (info: audio.InterruptEvent) => {
  console.info('audioInterrupt success,and InterruptEvent info is:' + info)
})
```

### off('audioInterrupt')<sup>9+</sup>

off(type: 'audioInterrupt'): void

取消监听音频焦点变化事件。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| type   | string | 是   | 音频焦点变化事件回调类型，取消注册的事件：'audioInterrupt'。 |

**示例：**

```ts
avPlayer.off('audioInterrupt')
```

### on('audioOutputDeviceChangeWithInfo') <sup>11+</sup>

on(type: 'audioOutputDeviceChangeWithInfo', callback: Callback\<audio.AudioStreamDeviceChangeInfo>): void

订阅监听音频流输出设备变化及原因，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型                       | 必填 | 说明                                        |
| :------- | :------------------------- | :--- | :------------------------------------------ |
| type     | string                     | 是   | 事件回调类型，支持的事件为：'outputDeviceChangeWithInfo'。 |
| callback | Callback\<[AudioStreamDeviceChangeInfo](../apis-audio-kit/js-apis-audio.md#audiostreamdevicechangeinfo11)> | 是   | 回调函数，返回当前音频流的输出设备描述信息及变化原因。 |

**错误码：**

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 401      | Parameter error. Return by callback.       |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

avPlayer.on('audioOutputDeviceChangeWithInfo', (data: audio.AudioStreamDeviceChangeInfo) => {
  console.info(`${JSON.stringify(data)}`);
});
```

### off('audioOutputDeviceChangeWithInfo') <sup>11+</sup>

off(type: 'audioOutputDeviceChangeWithInfo', callback?: Callback\<audio.AudioStreamDeviceChangeInfo>): void

取消订阅监听音频流输出设备变化及原因，使用callback方式返回结果。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

**参数：**

| 参数名   | 类型                       | 必填 | 说明                                        |
| :------- | :------------------------- | :--- | :------------------------------------------ |
| type     | string                     | 是   | 事件回调类型，支持的事件为：'outputDeviceChange'。 |
| callback | Callback\<[AudioStreamDeviceChangeInfo](../apis-audio-kit/js-apis-audio.md#audiostreamdevicechangeinfo11)> | 否   | 回调函数，返回当前音频流的输出设备描述信息及变化原因。 |

**错误码：**

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 401      | Parameter error. Return by callback.       |

**示例：**

```ts
avPlayer.off('audioOutputDeviceChangeWithInfo');
```

## AVPlayerState<sup>9+</sup>

[AVPlayer](#avplayer9)的状态机，可通过state属性主动获取当前状态，也可通过监听[stateChange](#onstatechange9)事件上报当前状态，状态机之间的切换规则，可参考[音频播放开发指导](../../media/media/using-avplayer-for-playback.md)。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

|              名称               |  类型  | 说明                                                         |
| :-----------------------------: | :----: | :----------------------------------------------------------- |
|              idle               | string | 闲置状态，AVPlayer刚被创建[createAVPlayer()](#mediacreateavplayer9)或者调用了[reset()](#reset9)方法之后，进入Idle状态。<br/>首次创建[createAVPlayer()](#mediacreateavplayer9)，所有属性都为默认值。<br/>调用[reset()](#reset9)方法，url<sup>9+</sup> 或 fdSrc<sup>9+</sup>或dataSrc<sup>10+</sup>属性及loop属性会被重置，其他用户设置的属性将被保留。 |
|           initialized           | string | 资源初始化，在Idle 状态设置 url<sup>9+</sup> 或 fdSrc<sup>9+</sup>属性，AVPlayer会进入initialized状态，此时可以配置窗口、音频等静态属性。 |
|            prepared             | string | 已准备状态，在initialized状态调用[prepare()](#prepare9)方法，AVPlayer会进入prepared状态，此时播放引擎的资源已准备就绪。 |
|             playing             | string | 正在播放状态，在prepared/paused/completed状态调用[play()](#play9)方法，AVPlayer会进入playing状态。 |
|             paused              | string | 暂停状态，在playing状态调用pause方法，AVPlayer会进入paused状态。 |
|            completed            | string | 播放至结尾状态，当媒体资源播放至结尾时，如果用户未设置循环播放（loop = true），AVPlayer会进入completed状态，此时调用[play()](#play9)会进入playing状态和重播，调用[stop()](#stop9)会进入stopped状态。 |
|             stopped             | string | 停止状态，在prepared/playing/paused/completed状态调用[stop()](#stop9)方法，AVPlayer会进入stopped状态，此时播放引擎只会保留属性，但会释放内存资源，可以调用[prepare()](#prepare9)重新准备，也可以调用[reset()](#reset9)重置，或者调用[release()](#release9)彻底销毁。 |
|            released             | string | 销毁状态，销毁与当前AVPlayer关联的播放引擎，无法再进行状态转换，调用[release()](#release9)方法后，会进入released状态，结束流程。 |
| error | string | 错误状态，当**播放引擎**发生**不可逆的错误**（详见[媒体错误码](errorcode-media.md)），则会转换至当前状态，可以调用[reset()](#reset9)重置，也可以调用[release()](#release9)销毁重建。<br/>**注意：** 区分error状态和 [on('error')](#onerror9) ：<br/>1、进入error状态时，会触发on('error')监听事件，可以通过on('error')事件获取详细错误信息；<br/>2、处于error状态时，播放服务进入不可播控的状态，要求客户端设计容错机制，使用[reset()](#reset9)重置或者[release()](#release9)销毁重建；<br/>3、如果客户端收到on('error')，但未进入error状态：<br/>原因1：客户端未按状态机调用API或传入参数错误，被AVPlayer拦截提醒，需要客户端调整代码逻辑；<br/>原因2：播放过程发现码流问题，导致容器、解码短暂异常，不影响连续播放和播控操作的，不需要客户端设计容错机制。 |

## AVFileDescriptor<sup>9+</sup>

音视频文件资源描述，一种特殊资源的播放方式，使用场景：应用中的音频资源被连续存储在同一个文件中，需要根据偏移量和长度进行播放。

**系统能力：** SystemCapability.Multimedia.Media.Core

| 名称   | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| fd     | number | 是   | 资源句柄，通过[resourceManager.getRawFd](../apis-localization-kit/js-apis-resource-manager.md#getrawfd9)获取。     |
| offset | number | 否   | 资源偏移量，默认值为0，需要基于预置资源的信息输入，非法值会造成音视频资源解析错误。 |
| length | number | 否   | 资源长度，默认值为文件中从偏移量开始的剩余字节，需要基于预置资源的信息输入，非法值会造成音视频资源解析错误。 |

## AVDataSrcDescriptor<sup>10+</sup>

音视频文件资源描述，用于DataSource播放方式，使用场景：应用在未获取完整音视频资源时，允许用户创建播放实例并开始播放，达到提前播放的目的。

**系统能力：** SystemCapability.Multimedia.Media.AVPlayer

| 名称   | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| fileSize     | number | 是   | 待播放文件大小（字节），-1代表大小未知。如果fileSize设置为-1, 播放模式类似于直播，不能进行seek及setSpeed操作，不能设置loop属性，因此不能重新播放。 |
| callback | function | 是   | 用户设置的回调函数，用于填写数据。<br>- 函数列式：callback: (buffer: ArrayBuffer, length: number, pos?:number) => number;<br>- buffer，ArrayBuffer类型，表示被填写的内存，必选。<br>- length，number类型，表示被填写内存的最大长度，必选。<br>- pos，number类型，表示填写的数据在资源文件中的位置，可选，当fileSize设置为-1时，该参数禁止被使用。 <br>- 返回值，number类型，返回要填充数据的长度。 |


## SeekMode<sup>8+</sup>

视频播放的Seek模式枚举，可通过seek方法作为参数传递下去。

**系统能力：** SystemCapability.Multimedia.Media.Core

| 名称           | 值   | 说明                                                         |
| -------------- | ---- | ------------------------------------------------------------ |
| SEEK_NEXT_SYNC | 0    | 表示跳转到指定时间点的下一个关键帧，建议向后快进的时候用这个枚举值。 |
| SEEK_PREV_SYNC | 1    | 表示跳转到指定时间点的上一个关键帧，建议向前快进的时候用这个枚举值。 |

## PlaybackSpeed<sup>8+</sup>

视频播放的倍速枚举，可通过setSpeed方法作为参数传递下去。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

| 名称                 | 值   | 说明                           |
| -------------------- | ---- | ------------------------------ |
| SPEED_FORWARD_0_75_X | 0    | 表示视频播放正常播速的0.75倍。 |
| SPEED_FORWARD_1_00_X | 1    | 表示视频播放正常播速。         |
| SPEED_FORWARD_1_25_X | 2    | 表示视频播放正常播速的1.25倍。 |
| SPEED_FORWARD_1_75_X | 3    | 表示视频播放正常播速的1.75倍。 |
| SPEED_FORWARD_2_00_X | 4    | 表示视频播放正常播速的2.00倍。 |

## VideoScaleType<sup>9+</sup>

枚举，视频缩放模式。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

| 名称                      | 值   | 说明                                             |
| ------------------------- | ---- | ------------------------------------------------ |
| VIDEO_SCALE_TYPE_FIT      | 0    | 默认比例类型，视频拉伸至与窗口等大。              |
| VIDEO_SCALE_TYPE_FIT_CROP | 1    | 保持视频宽高比拉伸至填满窗口，内容可能会有裁剪。 |

## MediaDescription<sup>8+</sup>

通过key-value方式获取媒体信息。

**系统能力：** SystemCapability.Multimedia.Media.Core

| 名称          | 类型   | 必填 | 说明                                                         |
| ------------- | ------ | ---- | ------------------------------------------------------------ |
| [key: string] | Object | 是   | 该键值对支持的key取值范围，请参考[MediaDescriptionKey](#mediadescriptionkey8);每个key值的Object类型和范围，请参考[MediaDescriptionKey](#mediadescriptionkey8)对应Key值的说明 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import media from '@ohos.multimedia.media';

function printfItemDescription(obj: media.MediaDescription, key: string) {
  let property: Object = obj[key];
  console.info('audio key is ' + key); // 通过key值获取对应的value。key值具体可见[MediaDescriptionKey]
  console.info('audio value is ' + property); //对应key值得value。其类型可为任意类型，具体key对应value的类型可参考[MediaDescriptionKey]
}

let avPlayer: media.AVPlayer | undefined = undefined;
media.createAVPlayer((err: BusinessError, player: media.AVPlayer) => {
  if(player != null) {
    avPlayer = player;
    console.info(`createAVPlayer success`);
    avPlayer.getTrackDescription((error: BusinessError, arrList: Array<media.MediaDescription>) => {
      if (arrList != null) {
        for (let i = 0; i < arrList.length; i++) {
          printfItemDescription(arrList[i], media.MediaDescriptionKey.MD_KEY_TRACK_TYPE);  //打印出每条轨道MD_KEY_TRACK_TYPE的值
        }
      } else {
        console.error(`audio getTrackDescription fail, error:${error}`);
      }
    });
  } else {
    console.error(`createAVPlayer fail, error message:${err.message}`);
  }
});
```

## AVRecorder<sup>9+</sup>

音视频录制管理类，用于音视频媒体录制。在调用AVRecorder的方法前，需要先通过[createAVRecorder()](#mediacreateavrecorder9)构建一个AVRecorder实例。

音视频录制demo可参考：[音频录制开发指导](../../media/media/using-avrecorder-for-recording.md)、[视频录制开发指导](../../media/media/video-recording.md)。

> **说明：**
>
> 使用相机进行视频录制时，需要与相机模块配合，相机模块接口的使用详情见[相机管理](../apis-camera-kit/js-apis-camera.md)。

### 属性

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

| 名称    | 类型                                 | 可读 | 可写 | 说明               |
| ------- | ------------------------------------ | ---- | ---- | ------------------ |
| state9+ | [AVRecorderState](#avrecorderstate9) | 是   | 否   | 音视频录制的状态。 |

### prepare<sup>9+</sup>

prepare(config: AVRecorderConfig, callback: AsyncCallback\<void>): void

异步方式进行音视频录制的参数设置。通过注册回调函数获取返回值。

**需要权限：** ohos.permission.MICROPHONE

不涉及音频录制时，可以不需要获取ohos.permission.MICROPHONE权限。

使用相机视频录制还需要与相机模块配合，相机模块接口的使用详情见[相机管理](../apis-camera-kit/js-apis-camera.md)。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**参数：**

| 参数名   | 类型                                   | 必填 | 说明                                  |
| -------- | -------------------------------------- | ---- | ------------------------------------- |
| config   | [AVRecorderConfig](#avrecorderconfig9) | 是   | 配置音视频录制的相关参数。            |
| callback | AsyncCallback\<void>                   | 是   | 异步音视频录制prepare方法的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                                |
| -------- | --------------------------------------- |
| 201      | Permission denied. Return by callback.  |
| 401      | Parameter error. Return by callback.    |
| 5400102  | Operate not permit. Return by callback. |
| 5400105  | Service died. Return by callback.       |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

// 配置参数以实际硬件设备支持的范围为准
let avRecorderProfile: media.AVRecorderProfile = {
  audioBitrate : 48000,
  audioChannels : 2,
  audioCodec : media.CodecMimeType.AUDIO_AAC,
  audioSampleRate : 48000,
  fileFormat : media.ContainerFormatType.CFT_MPEG_4,
  videoBitrate : 2000000,
  videoCodec : media.CodecMimeType.VIDEO_AVC,
  videoFrameWidth : 640,
  videoFrameHeight : 480,
  videoFrameRate : 30
}
let avRecorderConfig: media.AVRecorderConfig = {
  audioSourceType : media.AudioSourceType.AUDIO_SOURCE_TYPE_MIC,
  videoSourceType : media.VideoSourceType.VIDEO_SOURCE_TYPE_SURFACE_YUV,
  profile : avRecorderProfile,
  url : 'fd://', // 文件需先由调用者创建，赋予读写权限，将文件fd传给此参数，eg.fd://45
  rotation : 0, // 合理值0、90、180、270，非合理值prepare接口将报错
  location : { latitude : 30, longitude : 130 }
}

avRecorder.prepare(avRecorderConfig, (err: BusinessError) => {
  if (err == null) {
    console.info('prepare success');
  } else {
    console.error('prepare failed and error is ' + err.message);
  }
})
```

### prepare<sup>9+</sup>

prepare(config: AVRecorderConfig): Promise\<void>

异步方式进行音视频录制的参数设置。通过Promise获取返回值。

**需要权限：** ohos.permission.MICROPHONE

不涉及音频录制时，可以不需要获ohos.permission.MICROPHONE权限。

使用相机视频录制还需要与相机模块配合，相机模块接口的使用详情见[相机管理](../apis-camera-kit/js-apis-camera.md)。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**参数：**

| 参数名 | 类型                                   | 必填 | 说明                       |
| ------ | -------------------------------------- | ---- | -------------------------- |
| config | [AVRecorderConfig](#avrecorderconfig9) | 是   | 配置音视频录制的相关参数。 |

**返回值：**

| 类型           | 说明                                       |
| -------------- | ------------------------------------------ |
| Promise\<void> | 异步音视频录制prepare方法的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                               |
| -------- | -------------------------------------- |
| 201      | Permission denied. Return by promise.  |
| 401      | Parameter error. Return by promise.    |
| 5400102  | Operate not permit. Return by promise. |
| 5400105  | Service died. Return by promise.       |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

// 配置参数以实际硬件设备支持的范围为准
let avRecorderProfile: media.AVRecorderProfile = {
  audioBitrate : 48000,
  audioChannels : 2,
  audioCodec : media.CodecMimeType.AUDIO_AAC,
  audioSampleRate : 48000,
  fileFormat : media.ContainerFormatType.CFT_MPEG_4,
  videoBitrate : 2000000,
  videoCodec : media.CodecMimeType.VIDEO_AVC,
  videoFrameWidth : 640,
  videoFrameHeight : 480,
  videoFrameRate : 30
}
let avRecorderConfig: media.AVRecorderConfig = {
  audioSourceType : media.AudioSourceType.AUDIO_SOURCE_TYPE_MIC,
  videoSourceType : media.VideoSourceType.VIDEO_SOURCE_TYPE_SURFACE_YUV,
  profile : avRecorderProfile,
  url : 'fd://',  // 文件需先由调用者创建，赋予读写权限，将文件fd传给此参数，eg.fd://45
  rotation : 0, // 合理值0、90、180、270，非合理值prepare接口报错
  location : { latitude : 30, longitude : 130 }
}

avRecorder.prepare(avRecorderConfig).then(() => {
  console.info('prepare success');
}).catch((err: BusinessError) => {
  console.error('prepare failed and catch error is ' + err.message);
});
```

### getInputSurface<sup>9+</sup>

getInputSurface(callback: AsyncCallback\<string>): void

异步方式获得录制需要的surface。通过注册回调函数获取返回值。此surface提供给调用者，调用者从此surface中获取surfaceBuffer，填入相应的视频数据。

应当注意，填入的视频数据需要携带时间戳（单位ns）和buffersize。时间戳的起始时间请以系统启动时间为基准。

需在[prepare()](#prepare9-2)事件成功触发后，才能调用getInputSurface()方法。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**参数：**

| 参数名   | 类型                   | 必填 | 说明                        |
| -------- | ---------------------- | ---- | --------------------------- |
| callback | AsyncCallback\<string> | 是   | 异步获得surface的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                |
| -------- | --------------------------------------- |
| 5400102  | Operate not permit. Return by callback. |
| 5400103  | IO error. Return by callback.           |
| 5400105  | Service died. Return by callback.       |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
let surfaceID: string; // 该surfaceID用于传递给相机接口创造videoOutput

avRecorder.getInputSurface((err: BusinessError, surfaceId: string) => {
  if (err == null) {
    console.info('getInputSurface success');
    surfaceID = surfaceId;
  } else {
    console.error('getInputSurface failed and error is ' + err.message);
  }
});

```

### getInputSurface<sup>9+</sup>

getInputSurface(): Promise\<string>

异步方式获得录制需要的surface。通过Promise获取返回值。此surface提供给调用者，调用者从此surface中获取surfaceBuffer，填入相应的视频数据。

应当注意，填入的视频数据需要携带时间戳（单位ns）和buffersize。时间戳的起始时间请以系统启动时间为基准。

需在[prepare()](#prepare9-3)事件成功触发后，才能调用getInputSurface方法。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**返回值：**

| 类型             | 说明                             |
| ---------------- | -------------------------------- |
| Promise\<string> | 异步获得surface的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                               |
| -------- | -------------------------------------- |
| 5400102  | Operate not permit. Return by promise. |
| 5400103  | IO error. Return by promise.           |
| 5400105  | Service died. Return by promise.       |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
let surfaceID: string; // 该surfaceID用于传递给相机接口创造videoOutput

avRecorder.getInputSurface().then((surfaceId: string) => {
  console.info('getInputSurface success');
  surfaceID = surfaceId;
}).catch((err: BusinessError) => {
  console.error('getInputSurface failed and catch error is ' + err.message);
});
```

### start<sup>9+</sup>

start(callback: AsyncCallback\<void>): void

异步方式开始视频录制。通过注册回调函数获取返回值。

纯音频录制需在[prepare()](#prepare9-2)事件成功触发后，才能调用start方法。纯视频录制，音视频录制需在[getInputSurface()](#getinputsurface9)事件成功触发后，才能调用start方法。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**参数：**

| 参数名   | 类型                 | 必填 | 说明                         |
| -------- | -------------------- | ---- | ---------------------------- |
| callback | AsyncCallback\<void> | 是   | 异步开始视频录制的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                                |
| -------- | --------------------------------------- |
| 5400102  | Operate not permit. Return by callback. |
| 5400103  | IO error. Return by callback.           |
| 5400105  | Service died. Return by callback.       |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avRecorder.start((err: BusinessError) => {
  if (err == null) {
    console.info('start AVRecorder success');
  } else {
    console.error('start AVRecorder failed and error is ' + err.message);
  }
});
```

### start<sup>9+</sup>

start(): Promise\<void>

异步方式开始视频录制。通过Promise获取返回值。

纯音频录制需在[prepare()](#prepare9-3)事件成功触发后，才能调用start方法。纯视频录制，音视频录制需在[getInputSurface()](#getinputsurface9-1)事件成功触发后，才能调用start方法。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**返回值：**

| 类型           | 说明                                  |
| -------------- | ------------------------------------- |
| Promise\<void> | 异步开始视频录制方法的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                               |
| -------- | -------------------------------------- |
| 5400102  | Operate not permit. Return by promise. |
| 5400103  | IO error. Return by promise.           |
| 5400105  | Service died. Return by promise.       |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avRecorder.start().then(() => {
  console.info('start AVRecorder success');
}).catch((err: BusinessError) => {
  console.error('start AVRecorder failed and catch error is ' + err.message);
});
```

### pause<sup>9+</sup>

pause(callback: AsyncCallback\<void>): void

异步方式暂停视频录制。通过注册回调函数获取返回值。

需要[start()](#start9)事件成功触发后，才能调用pause方法，可以通过调用[resume()](#resume9)接口来恢复录制。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**参数：**

| 参数名   | 类型                 | 必填 | 说明                        |
| -------- | -------------------- | ---- | --------------------------- |
| callback | AsyncCallback\<void> | 是   | 异步获得surface的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                                |
| -------- | --------------------------------------- |
| 5400102  | Operate not permit. Return by callback. |
| 5400103  | IO error. Return by callback.           |
| 5400105  | Service died. Return by callback.       |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avRecorder.pause((err: BusinessError) => {
  if (err == null) {
    console.info('pause AVRecorder success');
  } else {
    console.error('pause AVRecorder failed and error is ' + err.message);
  }
});
```

### pause<sup>9+</sup>

pause(): Promise\<void>

异步方式暂停视频录制。通过Promise获取返回值。

需要[start()](#start9-1)事件成功触发后，才能调用pause方法，可以通过调用[resume()](#resume9-1)接口来恢复录制。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**返回值：**

| 类型           | 说明                                  |
| -------------- | ------------------------------------- |
| Promise\<void> | 异步暂停视频录制方法的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                               |
| -------- | -------------------------------------- |
| 5400102  | Operate not permit. Return by promise. |
| 5400103  | IO error. Return by promise.           |
| 5400105  | Service died. Return by promise.       |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avRecorder.pause().then(() => {
  console.info('pause AVRecorder success');
}).catch((err: BusinessError) => {
  console.error('pause AVRecorder failed and catch error is ' + err.message);
});
```

### resume<sup>9+</sup>

resume(callback: AsyncCallback\<void>): void

异步方式恢复视频录制。通过注册回调函数获取返回值。

需要在[pause()](#pause9-2)事件成功触发后，才能调用resume方法。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**参数：**

| 参数名   | 类型                 | 必填 | 说明                         |
| -------- | -------------------- | ---- | ---------------------------- |
| callback | AsyncCallback\<void> | 是   | 异步恢复视频录制的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                                |
| -------- | --------------------------------------- |
| 5400102  | Operate not permit. Return by callback. |
| 5400103  | IO error. Return by callback.           |
| 5400105  | Service died. Return by callback.       |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avRecorder.resume((err: BusinessError) => {
  if (err == null) {
    console.info('resume AVRecorder success');
  } else {
    console.error('resume AVRecorder failed and error is ' + err.message);
  }
});
```

### resume<sup>9+</sup>

resume(): Promise\<void>

异步方式恢复视频录制。通过Promise获取返回值。

需要在[pause()](#pause9-3)事件成功触发后，才能调用resume方法。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**返回值：**

| 类型           | 说明                                  |
| -------------- | ------------------------------------- |
| Promise\<void> | 异步恢复视频录制方法的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                               |
| -------- | -------------------------------------- |
| 5400102  | Operate not permit. Return by promise. |
| 5400103  | IO error. Return by promise.           |
| 5400105  | Service died. Return by promise.       |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avRecorder.resume().then(() => {
  console.info('resume AVRecorder success');
}).catch((err: BusinessError) => {
  console.error('resume AVRecorder failed and catch error is ' + err.message);
});
```

### stop<sup>9+</sup>

stop(callback: AsyncCallback\<void>): void

异步方式停止视频录制。通过注册回调函数获取返回值。

需要在[start()](#start9)或[pause()](#pause9-2)事件成功触发后，才能调用stop方法。

纯音频录制时，需要重新调用[prepare()](#prepare9-2)接口才能重新录制。纯视频录制，音视频录制时，需要重新调用[prepare()](#prepare9-2)和[getInputSurface()](#getinputsurface9)接口才能重新录制。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**参数：**

| 参数名   | 类型                 | 必填 | 说明                         |
| -------- | -------------------- | ---- | ---------------------------- |
| callback | AsyncCallback\<void> | 是   | 异步停止视频录制的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                                |
| -------- | --------------------------------------- |
| 5400102  | Operate not permit. Return by callback. |
| 5400103  | IO error. Return by callback.           |
| 5400105  | Service died. Return by callback.       |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avRecorder.stop((err: BusinessError) => {
  if (err == null) {
    console.info('stop AVRecorder success');
  } else {
    console.error('stop AVRecorder failed and error is ' + err.message);
  }
});
```

### stop<sup>9+</sup>

stop(): Promise\<void>

异步方式停止视频录制。通过Promise获取返回值。

需要在[start()](#start9-1)或[pause()](#pause9-3)事件成功触发后，才能调用stop方法。

纯音频录制时，需要重新调用[prepare()](#prepare9-3)接口才能重新录制。纯视频录制，音视频录制时，需要重新调用[prepare()](#prepare9-3)和[getInputSurface()](#getinputsurface9-1)接口才能重新录制。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**返回值：**

| 类型           | 说明                                  |
| -------------- | ------------------------------------- |
| Promise\<void> | 异步停止视频录制方法的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                               |
| -------- | -------------------------------------- |
| 5400102  | Operate not permit. Return by promise. |
| 5400103  | IO error. Return by promise.           |
| 5400105  | Service died. Return by promise.       |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avRecorder.stop().then(() => {
  console.info('stop AVRecorder success');
}).catch((err: BusinessError) => {
  console.error('stop AVRecorder failed and catch error is ' + err.message);
});
```

### reset<sup>9+</sup>

reset(callback: AsyncCallback\<void>): void

异步方式重置音视频录制。通过注册回调函数获取返回值。

纯音频录制时，需要重新调用[prepare()](#prepare9-2)接口才能重新录制。纯视频录制，音视频录制时，需要重新调用[prepare()](#prepare9-2)和[getInputSurface()](#getinputsurface9)接口才能重新录制。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**参数：**

| 参数名   | 类型                 | 必填 | 说明                           |
| -------- | -------------------- | ---- | ------------------------------ |
| callback | AsyncCallback\<void> | 是   | 异步重置音视频录制的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                          |
| -------- | --------------------------------- |
| 5400103  | IO error. Return by callback.     |
| 5400105  | Service died. Return by callback. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avRecorder.reset((err: BusinessError) => {
  if (err == null) {
    console.info('reset AVRecorder success');
  } else {
    console.error('reset AVRecorder failed and error is ' + err.message);
  }
});
```

### reset<sup>9+</sup>

reset(): Promise\<void>

异步方式重置音视频录制。通过Promise获取返回值。

纯音频录制时，需要重新调用[prepare()](#prepare9-3)接口才能重新录制。纯视频录制，音视频录制时，需要重新调用[prepare()](#prepare9-3)和[getInputSurface()](#getinputsurface9-1)接口才能重新录制。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**返回值：**

| 类型           | 说明                                    |
| -------------- | --------------------------------------- |
| Promise\<void> | 异步重置音视频录制方法的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                         |
| -------- | -------------------------------- |
| 5400103  | IO error. Return by promise.     |
| 5400105  | Service died. Return by promise. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avRecorder.reset().then(() => {
  console.info('reset AVRecorder success');
}).catch((err: BusinessError) => {
  console.error('reset AVRecorder failed and catch error is ' + err.message);
});
```

### release<sup>9+</sup>

release(callback: AsyncCallback\<void>): void

异步方式释放音视频录制资源。通过注册回调函数获取返回值。

释放音视频录制资源之后，该AVRecorder实例不能再进行任何操作。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**参数：**

| 参数名   | 类型                 | 必填 | 说明                               |
| -------- | -------------------- | ---- | ---------------------------------- |
| callback | AsyncCallback\<void> | 是   | 异步释放音视频录制资源的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                          |
| -------- | --------------------------------- |
| 5400105  | Service died. Return by callback. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avRecorder.release((err: BusinessError) => {
  if (err == null) {
    console.info('release AVRecorder success');
  } else {
    console.error('release AVRecorder failed and error is ' + err.message);
  }
});
```

### release<sup>9+</sup>

release(): Promise\<void>

异步方式释放音视频录制资源。通过Promise获取返回值。

释放音视频录制资源之后，该AVRecorder实例不能再进行任何操作。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**返回值：**

| 类型           | 说明                                        |
| -------------- | ------------------------------------------- |
| Promise\<void> | 异步释放音视频录制资源方法的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                          |
| -------- | --------------------------------- |
| 5400105  | Service died. Return by callback. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avRecorder.release().then(() => {
  console.info('release AVRecorder success');
}).catch((err: BusinessError) => {
  console.error('release AVRecorder failed and catch error is ' + err.message);
});
```

### getCurrentAudioCapturerInfo<sup>11+</sup>

getCurrentAudioCapturerInfo(callback: AsyncCallback\<audio.AudioCapturerChangeInfo>): void

异步方式获取当前音频采集参数。通过注册回调函数获取返回值。

在prepare()成功触发后，才能调用此方法。在stop()成功触发后，调用此方法会报错。

**系统能力**：SystemCapability.Multimedia.Media.AVRecorder

**参数**：

| 参数名   | 类型                                                         | 必填 | 说明                                 |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------ |
| callback | AsyncCallback\<[audio.AudioCapturerChangeInfo](../apis-audio-kit/js-apis-audio.md#audiocapturerchangeinfo9)> | 是   | 异步获取当前音频采集参数的回调方法。 |

**错误码**：

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400102  | Operation not allowed. Return by callback. |
| 5400103  | I/O error. Return by callback.             |
| 5400105  | Service died. Return by callback.          |

**示例**：

```ts
let currentCapturerInfo: audio.AudioCapturerChangeInfo;

avRecorder.getCurrentAudioCapturerInfo((err: BusinessError, capturerInfo: audio.AudioCapturerChangeInfo) => {
  if (err == null) {
    console.info('getCurrentAudioCapturerInfo success');
    currentCapturerInfo = capturerInfo;
  } else {
    console.error('getCurrentAudioCapturerInfo failed and error is ' + err.message);
  }
});
```

### getCurrentAudioCapturerInfo<sup>11+</sup>

getCurrentAudioCapturerInfo(): Promise\<audio.AudioCapturerChangeInfo>

异步方式获取当前音频采集参数。通过Promise获取返回值。

在prepare()成功触发后，才能调用此方法。在stop()成功触发后，调用此方法会报错。

**系统能力**：SystemCapability.Multimedia.Media.AVRecorder

**返回值**：

| 类型                                                         | 说明                                              |
| ------------------------------------------------------------ | ------------------------------------------------- |
| Promise\<[audio.AudioCapturerChangeInfo](../apis-audio-kit/js-apis-audio.md#audiocapturerchangeinfo9)> | 异步方式获取当前音频采集参数方法的Promise返回值。 |

**错误码**：

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                         |
| -------- | -------------------------------- |
| 5400102  | Operation not allowed.           |
| 5400103  | I/O error.                       |
| 5400105  | Service died. Return by promise. |

**示例**：

```ts
let currentCapturerInfo: audio.AudioCapturerChangeInfo;

avRecorder.getCurrentAudioCapturerInfo().then((capturerInfo: audio.AudioCapturerChangeInfo) => {
  console.info('getCurrentAudioCapturerInfo success');
  currentCapturerInfo = capturerInfo;
}).catch((err: BusinessError) => {
  console.error('getCurrentAudioCapturerInfo failed and catch error is ' + err.message);
});
```

### getAudioCapturerMaxAmplitude<sup>11+</sup>

getAudioCapturerMaxAmplitude(callback: AsyncCallback\<number>): void

异步方式获取当前音频最大振幅。通过注册回调函数获取返回值。

在prepare()成功触发后，才能调用此方法。在stop()成功触发后，调用此方法会报错。

调用接口时，获取到的返回值是上一次获取最大振幅的时刻到当前这段区间内的音频最大振幅。即，如果在1s的时刻获取了一次最大振幅，在2s时再获取到的最大振幅时1-2s这个区间里面的最大值。

**系统能力**：SystemCapability.Multimedia.Media.AVRecorder

**参数**：

| 参数名   | 类型                   | 必填 | 说明                                 |
| -------- | ---------------------- | ---- | ------------------------------------ |
| callback | AsyncCallback\<number> | 是   | 异步获取当前音频最大振幅的回调方法。 |

**错误码**：

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400102  | Operation not allowed. Return by callback. |
| 5400105  | Service died. Return by callback.          |

**示例**：

```ts
let maxAmplitude: number;

avRecorder.getAudioCapturerMaxAmplitude((err: BusinessError, amplitude: number) => {
  if (err == null) {
    console.info('getAudioCapturerMaxAmplitude success');
    maxAmplitude = amplitude;
  } else {
    console.error('getAudioCapturerMaxAmplitude failed and error is ' + err.message);
  }
});
```

### getAudioCapturerMaxAmplitude<sup>11+</sup>

getAudioCapturerMaxAmplitude(): Promise\<number>

异步方式获取当前音频最大振幅参数。通过Promise获取返回值。

在prepare()成功触发后，才能调用此方法。在stop()成功触发后，调用此方法会报错。

调用接口时，获取到的返回值是上一次获取最大振幅的时刻到当前这段区间内的音频最大振幅。即，如果在1s的时刻获取了一次最大振幅，在2s时再获取到的最大振幅时1-2s这个区间里面的最大值。

**系统能力**：SystemCapability.Multimedia.Media.AVRecorder

**返回值**：

| 类型             | 说明                                              |
| ---------------- | ------------------------------------------------- |
| Promise\<number> | 异步方式获取当前音频最大振幅方法的Promise返回值。 |

**错误码**：

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                         |
| -------- | -------------------------------- |
| 5400102  | Operation not allowed.           |
| 5400105  | Service died. Return by promise. |

**示例**：

```ts
let maxAmplitude: number;

avRecorder.getAudioCapturerMaxAmplitude().then((amplitude: number) => {
  console.info('getAudioCapturerMaxAmplitude success');
  maxAmplitude = amplitude;
}).catch((err: BusinessError) => {
  console.error('getAudioCapturerMaxAmplitude failed and catch error is ' + err.message);
});
```

### getAvailableEncoder<sup>11+</sup>

getAvailableEncoder(callback: AsyncCallback\<Array\<EncoderInfo>>): void

异步方式获取可用的编码器参数。通过注册回调函数获取返回值。

**系统能力**：SystemCapability.Multimedia.Media.AVRecorder

**参数**：

| 参数名   | 类型                                                  | 必填 | 说明                                 |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------ |
| callback | AsyncCallback\<Array\<[EncoderInfo](#encoderinfo11)>> | 是   | 异步获取可用的编码器参数的回调方法。 |

**错误码**：

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400102  | Operation not allowed. Return by callback. |
| 5400105  | Service died. Return by callback.          |

**示例**：

```ts
let encoderInfo: media.EncoderInfo;

avRecorder.getAvailableEncoder((err: BusinessError, info: media.EncoderInfo) => {
  if (err == null) {
    console.info('getAvailableEncoder success');
    encoderInfo = info;
  } else {
    console.error('getAvailableEncoder failed and error is ' + err.message);
  }
});
```

### getAvailableEncoder<sup>11+</sup>

getAvailableEncoder(): Promise\<Array\<EncoderInfo>>

异步方式获取可用的编码器参数。通过注册回调函数获取返回值。

**系统能力**：SystemCapability.Multimedia.Media.AVRecorder

**返回值**：

| 类型                                            | 说明                                            |
| ----------------------------------------------- | ----------------------------------------------- |
| Promise\<Array\<[EncoderInfo](#encoderinfo11)>> | 异步方式获取可用的编码参数方法的Promise返回值。 |

**错误码**：

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                         |
| -------- | -------------------------------- |
| 5400102  | Operation not allowed.           |
| 5400105  | Service died. Return by promise. |

**示例**：

```ts
let encoderInfo: media.EncoderInfo;

avRecorder.getAvailableEncoder().then((info: media.EncoderInfo) => {
  console.info('getAvailableEncoder success');
  encoderInfo = info;
}).catch((err: BusinessError) => {
  console.error('getAvailableEncoder failed and catch error is ' + err.message);
});
```

### getAVRecorderConfig<sup>11+</sup>

getAVRecorderConfig(callback: AsyncCallback\<AVRecorderConfig>): void

异步方式获取实时的配置参数。通过注册回调函数获取返回值。

只能在[prepare()](#prepare9-2)接口调用后调用。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**参数：**

| 参数名   | 类型                   | 必填 | 说明                        |
| -------- | ---------------------- | ---- | --------------------------- |
| callback | AsyncCallback\<[AVRecorderConfig](#avrecorderconfig9)> | 是   | 异步获得实时配置参数的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400102  | Operate not permit. Return by callback. |
| 5400103  | IO error. Return by callback.             |
| 5400105  | Service died. Return by callback.          |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let AVRecorderConfig: AVRecorderConfig;

avRecorder.getAVRecorderConfig((err: BusinessError, config: AVRecorderConfig) => {
  if (err == null) {
    console.info('getAVRecorderConfig success');
    AVRecorderConfig = config;
  } else {
    console.error('getAVRecorderConfig failed and error is ' + err.message);
  }
});
```

### getAVRecorderConfig<sup>11+</sup>

getAVRecorderConfig(): Promise\<AVRecorderConfig>;

异步方式获取实时的配置参数。通过Promise获取返回值。

只能在[prepare()](#prepare9-3)接口调用后调用。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**返回值：**

| 类型             | 说明                             |
| ---------------- | -------------------------------- |
| Promise\<[AVRecorderConfig](#avrecorderconfig9)> | 异步获得实时配置参数的回调方法。 |

**错误码：**
  
以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                  |
| -------- | ----------------------------------------- |
| 5400102  | Operate not permit. Return by promise. |
| 5400103  | IO error. Return by promise.             |
| 5400105  | Service died. Return by promise.          |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let AVRecorderConfig: AVRecorderConfig;

avRecorder.getAVRecorderConfig().then((config: AVRecorderConfig) => {
  console.info('getAVRecorderConfig success');
  AVRecorderConfig = config;
}).catch((err: BusinessError) => {
  console.error('getAVRecorderConfig failed and catch error is ' + err.message);
});
```

### on('stateChange')<sup>9+</sup>

on(type: 'stateChange', callback: (state: AVRecorderState, reason: StateChangeReason) => void): void

订阅录制状态机AVRecorderState切换的事件，当 AVRecorderState状态机发生变化时，会通过订阅的回调方法通知用户。用户只能订阅一个状态机切换事件的回调方法，当用户重复订阅时，以最后一次订阅的回调接口为准。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | 状态机切换事件回调类型，支持的事件：'stateChange'，用户操作和系统都会触发此事件。 |
| callback | function | 是   | 状态机切换事件回调方法：<br>state: [AVRecorderState](#avrecorderstate9)，表示当前播放状态 ；<br>reason: [StateChangeReason](#statechangereason9)，表示当前播放状态的切换原因。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                          |
| -------- | --------------------------------- |
| 5400103  | IO error. Return by callback.     |
| 5400105  | Service died. Return by callback. |

**示例：**

```ts
avRecorder.on('stateChange', async (state: media.AVRecorderState, reason: media.StateChangeReason) => {
  console.info('case state has changed, new state is :' + state + ',and new reason is : ' + reason);
});
```

### off('stateChange')<sup>9+</sup>

off(type: 'stateChange'): void

取消订阅播放状态机[AVRecorderState](#avrecorderstate9)切换的事件。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| type   | string | 是   | 状态机切换事件回调类型，支持的事件：'stateChange'，用户操作和系统都会触发此事件。 |

**示例：**

```ts
avRecorder.off('stateChange');
```

### on('error')<sup>9+</sup>

on(type: 'error', callback: ErrorCallback): void

订阅AVRecorder的错误事件，该事件仅用于错误提示，不需要用户停止播控动作。如果此时[AVRecorderState](#avrecorderstate9)也切至error状态，用户需要通过[reset()](#reset9-2)或者[release()](#release9-2)退出录制操作。

用户只能订阅一个错误事件的回调方法，当用户重复订阅时，以最后一次订阅的回调接口为准。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**参数：**

| 参数名   | 类型          | 必填 | 说明                                                         |
| -------- | ------------- | ---- | ------------------------------------------------------------ |
| type     | string        | 是   | 录制错误事件回调类型'error'。 <br>- 'error'：录制过程中发生错误，触发该事件。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback) | 是   | 录制错误事件回调方法。                                       |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)。

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400101  | No memory. Return by callback.             |
| 5400102  | Operation not allowed. Return by callback. |
| 5400103  | I/O error. Return by callback.             |
| 5400104  | Time out. Return by callback.              |
| 5400105  | Service died. Return by callback.          |
| 5400106  | Unsupport format. Return by callback.      |
| 5400107  | Audio interrupted. Return by callback.     |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

avRecorder.on('error', (err: BusinessError) => {
  console.info('case avRecorder.on(error) called, errMessage is ' + err.message);
});
```

### off('error')<sup>9+</sup>

off(type: 'error'): void

取消订阅录制错误事件，取消后不再接收到AVRecorder的错误事件。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| type   | string | 是   | 录制错误事件回调类型'error'。 <br>- 'error'：录制过程中发生错误，触发该事件。 |

**示例：**

```ts
avRecorder.off('error');
```

### on('audioCapturerChange')<sup>11+</sup>

on(type: 'audioCapturerChange', callback: Callback<audio.AudioCapturerChangeInfo>): void

订阅录音配置变化的回调，任意录音配置的变化会触发变化后的录音配置全量信息回调。

当用户重复订阅时，以最后一次订阅的回调接口为准。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   |录音配置变化的回调类型，支持的事件：'audioCapturerChange'。 |
| callback | Callback<[audio.AudioCapturerChangeInfo](../apis-audio-kit/js-apis-audio.md#audiocapturerchangeinfo9)> | 是 | 变化后的录音配置全量信息。|

**错误码：**

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 401      | Parameter error. Return by callback.       |

**示例：**

```ts
let capturerChangeInfo: audio.AudioCapturerChangeInfo;

avRecorder.on('audioCapturerChange',  (audioCapturerChangeInfo: audio.AudioCapturerChangeInfo) => {
  console.info('audioCapturerChange success');
  capturerChangeInfo = audioCapturerChangeInfo;
});
```

### off('audioCapturerChange')<sup>11+</sup>

off(type: 'audioCapturerChange'): void

取消订阅录音变化的回调事件。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| type   | string | 是   | 录音配置变化的回调类型，支持的事件：'audioCapturerChange'。 |

**示例：**

```ts
avRecorder.off('audioCapturerChange');
```

## AVRecorderState<sup>9+</sup>

音视频录制的状态机。可通过state属性获取当前状态。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

| 名称     | 类型   | 说明                                                         |
| -------- | ------ | ------------------------------------------------------------ |
| idle     | string | 闲置状态。此时可以调用[AVRecorder.prepare()](#prepare9-2)方法设置录制参数，进入prepared状态。AVRecorder刚被创建，或者在任何非released状态下调用[AVRecorder.reset()](#reset9-2)方法，均进入idle状态。 |
| prepared | string | 参数设置完成。此时可以调用[AVRecorder.start()](#start9)方法开始录制，进入started状态。 |
| started  | string | 正在录制。此时可以调用[AVRecorder.pause()](#pause9-2)方法暂停录制，进入paused状态。也可以调用[AVRecorder.stop()](#stop9-2)方法结束录制，进入stopped状态。 |
| paused   | string | 录制暂停。此时可以调用[AVRecorder.resume()](#resume9)方法继续录制，进入started状态。也可以调用[AVRecorder.stop()](#stop9-2)方法结束录制，进入stopped状态。 |
| stopped  | string | 录制停止。此时可以调用[AVRecorder.prepare()](#prepare9-2)方法设置录制参数，重新进入prepared状态。 |
| released | string | 录制资源释放。此时不能再进行任何操作。在任何其他状态下，均可以通过调用[AVRecorder.release()](#release9-2)方法进入released状态。 |
| error    | string | 错误状态。当AVRecorder实例发生不可逆错误，会转换至当前状态。切换至error状态时会伴随[AVRecorder.on('error')事件](#onerror9-1)，该事件会上报详细错误原因。在error状态时，用户需要调用[AVRecorder.reset()](#reset9-2)方法重置AVRecorder实例，或者调用[AVRecorder.release()](#release9-2)方法释放资源。 |

## AVRecorderConfig<sup>9+</sup>

表示音视频录制的参数设置。

通过audioSourceType和videoSourceType区分纯音频录制、纯视频录制或音视频录制。纯音频录制时，仅需要设置audioSourceType；纯视频录制时，仅需要设置videoSourceType；音视频录制时，audioSourceType和videoSourceType均需要设置。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

| 名称            | 类型                                     | 必填 | 说明                                                         |
| --------------- | ---------------------------------------- | ---- | ------------------------------------------------------------ |
| audioSourceType | [AudioSourceType](#audiosourcetype9)     | 否   | 选择录制的音频源类型。选择音频录制时必填。                   |
| videoSourceType | [VideoSourceType](#videosourcetype9)     | 否   | 选择录制的视频源类型。选择视频录制时必填。                   |
| profile         | [AVRecorderProfile](#avrecorderprofile9) | 是   | 录制的profile，必要参数。                                    |
| url             | string                                   | 是   | 录制输出URL：fd://xx (fd number) ![img](figures/zh-cn_image_url.png)，必要参数。 |
| rotation        | number                                   | 否   | 录制的视频旋转角度，mp4格式支持0，90，180，270，默认值为0。       |
| location        | [Location](#location)                    | 否   | 录制的地理位置，默认不记录地理位置信息。                     |

## AVRecorderProfile<sup>9+</sup>

音视频录制的配置文件。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

| 名称             | 类型                                         | 必填 | 说明                                                         |
| ---------------- | -------------------------------------------- | ---- | ------------------------------------------------------------ |
| audioBitrate     | number                                       | 否   | 音频编码比特率，选择音频录制时必填，支持范围[8000 - 384000]。 |
| audioChannels    | number                                       | 否   | 音频采集声道数，选择音频录制时必填，支持范围[1 - 2]。        |
| audioCodec       | [CodecMimeType](#codecmimetype8)             | 否   | 音频编码格式，选择音频录制时必填。当前仅支持AUDIO_AAC。      |
| audioSampleRate  | number                                       | 否   | 音频采样率，选择音频录制时必填，支持范围[8000, 11025, 12000, 16000, 22050, 24000, 32000, 44100, 48000, 64000, 96000]。 |
| fileFormat       | [ContainerFormatType](#containerformattype8) | 是   | 文件的容器格式，必要参数。                                   |
| videoBitrate     | number                                       | 否   | 视频编码比特率，选择视频录制时必填，支持范围[1 - 3000000]。  |
| videoCodec       | [CodecMimeType](#codecmimetype8)             | 否   | 视频编码格式，选择视频录制时必填。当前支持VIDEO_AVC。        |
| videoFrameWidth  | number                                       | 否   | 视频帧的宽，选择视频录制时必填，支持范围[2 - 1920]。         |
| videoFrameHeight | number                                       | 否   | 视频帧的高，选择视频录制时必填，支持范围[2 - 1080]。         |
| videoFrameRate   | number                                       | 否   | 视频帧率，选择视频录制时必填，支持范围[1 - 30]。             |
| isHdr<sup>11+</sup>            | boolean                        | 否   | HDR编码，选择视频录制时选填，isHdr默认为false，对应编码格式没有要求，isHdr为true时，对应的编码格式必须为video/hevc。|

## AudioSourceType<sup>9+</sup>

表示视频录制中音频源类型的枚举。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

| 名称                      | 值   | 说明                   |
| ------------------------- | ---- | ---------------------- |
| AUDIO_SOURCE_TYPE_DEFAULT | 0    | 默认的音频输入源类型。 |
| AUDIO_SOURCE_TYPE_MIC     | 1    | 表示MIC的音频输入源。  |

## VideoSourceType<sup>9+</sup>

表示视频录制中视频源类型的枚举。

**系统能力：** SystemCapability.Multimedia.Media.AVRecorder

| 名称                          | 值   | 说明                            |
| ----------------------------- | ---- | ------------------------------- |
| VIDEO_SOURCE_TYPE_SURFACE_YUV | 0    | 输入surface中携带的是raw data。 |
| VIDEO_SOURCE_TYPE_SURFACE_ES  | 1    | 输入surface中携带的是ES data。  |

## ContainerFormatType<sup>8+</sup>

表示容器格式类型的枚举，缩写为CFT。

**系统能力：** SystemCapability.Multimedia.Media.Core

| 名称        | 值    | 说明                  |
| ----------- | ----- | --------------------- |
| CFT_MPEG_4  | 'mp4' | 视频的容器格式，MP4。 |
| CFT_MPEG_4A | 'm4a' | 音频的容器格式，M4A。 |

## Location

视频录制的地理位置。

**系统能力：** SystemCapability.Multimedia.Media.Core

| 名称      | 类型   | 必填 | 说明             |
| --------- | ------ | ---- | ---------------- |
| latitude  | number | 是   | 地理位置的纬度。 |
| longitude | number | 是   | 地理位置的经度。 |

## EncoderInfo<sup>11+</sup>

编码器和规格参数

系统能力：SystemCapability.Multimedia.Media.AVRecorder

| 名称       | 类型                             | 可读 | 可写 | 说明                                                         |
| ---------- | -------------------------------- | ---- | ---- | ------------------------------------------------------------ |
| mimeType   | [CodecMimeType](#codecmimetype8) | 是   | 否   | 编码器MIME类型名称                                           |
| type       | string                           | 是   | 否   | 编码器类型，audio表示音频编码器，video表示视频编码器         |
| bitRate    | [Range](#range11)                | 是   | 否   | 比特率，包含该编码器的最大和最小值                           |
| frameRate  | [Range](#range11)                | 是   | 否   | 视频帧率，包含帧率的最大和最小值，仅视频编码器拥有           |
| width      | [Range](#range11)                | 是   | 否   | 视频帧的宽度，包含宽度的最大和最小值，仅视频编码器拥有       |
| height     | [Range](#range11)                | 是   | 否   | 视频帧的高度，包含高度的最大和最小值，仅视频编码器拥有       |
| channels   | [Range](#range11)                | 是   | 否   | 音频采集声道数，包含声道数的最大和最小值，仅音频编码器拥有   |
| sampleRate | Array\<number>                    | 是   | 否   | 音频采样率，包含所有可以使用的音频采样率值，仅音频编码器拥有 |

## Range<sup>11+</sup>

表示一个类型的范围

系统能力：SystemCapability.Multimedia.Media.AVRecorder

| 名称 | 类型   | 可读 | 可写 | 说明         |
| ---- | ------ | ---- | ---- | ------------ |
| min  | number | 是   | 否   | 范围的最小值 |
| max  | number | 是   | 否   | 范围的最大值 |



## AVMetadataExtractor<sup>11+</sup>

元数据获取类，用于从媒体资源中获取元数据。在调用AVMetadataExtractor的方法前，需要先通过[createAVMetadataExtractor()](#mediacreateavmetadataextractor11)构建一个AVMetadataExtractor实例。

获取音频或视频元数据的demo可参考：[获取音视频元数据开发指导](../../media/media/avmetadataextractor.md)。

### 属性

**系统能力：** SystemCapability.Multimedia.Media.AVMetadataExtractor

| 名称                                                | 类型                                                         | 可读 | 可写 | 说明                                                         |
| --------------------------------------------------- | ------------------------------------------------------------ | ---- | ---- | ------------------------------------------------------------ |
| fdSrc<sup>11+</sup>                                  | [AVFileDescriptor](#avfiledescriptor9)                       | 是   | 是   | 媒体文件描述，通过该属性设置数据源。在获取元信息之前，必须设置数据源属性，只能设置fdSrc和dataSrc的其中一个。<br/> **使用示例**：<br/>假设一个连续存储的媒体文件，地址偏移:0，字节长度:100。其文件描述为 AVFileDescriptor { fd = 资源句柄; offset = 0; length = 100; }。 |
| dataSrc<sup>11+</sup>                               | [AVDataSrcDescriptor](#avdatasrcdescriptor10)                | 是   | 是   | 流式媒体资源描述，通过该属性设置数据源。在获取元信息之前，必须设置数据源属性，只能设置fdSrc和dataSrc的其中一个。<br/> 当应用从远端获取音视频媒体文件，在应用未下载完整音视频资源时，可以设置dataSrc提前获取该资源的元信息。|

### fetchMetadata<sup>11+</sup>

fetchMetadata(callback: AsyncCallback\<AVMetadata>): void

异步方式获取媒体元数据。通过注册回调函数获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.AVMetadataExtractor

**参数：**

| 参数名   | 类型                                         | 必填 | 说明                                |
| -------- | -------------------------------------------- | ---- | ----------------------------------- |
| callback | AsyncCallback\<[AVMetadata](#avmetadata11)>       | 是   | 回调函数。异步返回音视频元数据对象（AVMetadata）。|

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400102  | Operation not allowed. Returned by callback. |
| 5400106  | Unsupported format. Returned by callback.  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import media from '@ohos.multimedia.media';

let avMetadataExtractor: media.AVMetadataExtractor | undefined = undefined;

// 获取元数据
media.createAVMetadataExtractor((err: BusinessError, extractor: media.AVMetadataExtractor) => {
  if(extractor != null){
    avMetadataExtractor = extractor;
    console.error(`createAVMetadataExtractor success`);
    avMetadataExtractor.fetchMetadata((error: BusinessError, metadata: media.AVMetadata) => {
      if (error) {
        console.error(`fetchMetadata callback failed, err = ${JSON.stringify(error)}`);
        return;
      }
      console.info(`fetchMetadata callback success, genre: ${metadata.genre}`);
    });
  } else {
    console.error(`createAVMetadataExtractor fail, error message:${err.message}`);
  }
});
```

### fetchMetadata<sup>11+</sup>

fetchMetadata(): Promise\<AVMetadata>

异步方式获取媒体元数据。通过Promise获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.AVMetadataExtractor

**返回值：**

| 类型           | 说明                                     |
| -------------- | ---------------------------------------- |
| Promise\<[AVMetadata](#avmetadata11)>  | Promise对象。异步返回音视频元数据对象（AVMetadata）。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                  |
| -------- | ----------------------------------------- |
| 5400102  | Operation not allowed. Returned by promise. |
| 5400106  | Unsupported format. Returned by promise.  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import media from '@ohos.multimedia.media';

let avMetadataExtractor: media.AVMetadataExtractor | undefined = undefined;

// 获取元信息
media.createAVMetadataExtractor((err: BusinessError, extractor: media.AVMetadataExtractor) => {
  if(extractor != null){
    avMetadataExtractor = extractor;
    console.error(`createAVMetadataExtractor success`);
    avMetadataExtractor.fetchMetadata().then((metadata: media.AVMetadata) => {
      console.info(`fetchMetadata callback success, genre: ${metadata.genre}`)
    }).catch((error: BusinessError) => {
      console.error(`fetchMetadata catchCallback, error message:${error.message}`);
    });
  } else {
    console.error(`createAVMetadataExtractor fail, error message:${err.message}`);
  }
});
```

### fetchAlbumCover<sup>11+</sup>

fetchAlbumCover(callback: AsyncCallback\<image.PixelMap>): void

异步方式获取音频专辑封面。通过注册回调函数获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.AVMetadataExtractor

**参数：**

| 参数名   | 类型                                         | 必填 | 说明                                |
| -------- | -------------------------------------------- | ---- | ----------------------------------- |
| callback | AsyncCallback\<[image.PixelMap](../apis-image-kit/js-apis-image.md#pixelmap7)>    | 是   | 回调函数。异步返回专辑封面。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400102  | Operation not allowed. Return by callback. |
| 5400106  | Unsupported format. Returned by callback.  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import media from '@ohos.multimedia.media';
import image from '@ohos.multimedia.image';

let avMetadataExtractor: media.AVMetadataExtractor | undefined = undefined;
let pixel_map : image.PixelMap | undefined = undefined;

// 获取专辑封面
media.createAVMetadataExtractor((err: BusinessError, extractor: media.AVMetadataExtractor) => {
  if(extractor != null){
    avMetadataExtractor = extractor;
    console.error(`createAVMetadataExtractor success`);
    avMetadataExtractor.fetchAlbumCover((error: BusinessError, pixelMap: image.PixelMap) => {
      if (error) {
        console.error(`fetchAlbumCover callback failed, error = ${JSON.stringify(error)}`);
        return;
      }
      pixel_map = pixelMap;
    });
  } else {
    console.error(`createAVMetadataExtractor fail, error message:${err.message}`);
  };
});
```

### fetchAlbumCover<sup>11+</sup>

fetchAlbumCover(): Promise\<image.PixelMap>

异步方式获取专辑封面。通过Promise获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.AVMetadataExtractor

**返回值：**

| 类型           | 说明                                     |
| -------------- | ---------------------------------------- |
| Promise\<[image.PixelMap](../apis-image-kit/js-apis-image.md#pixelmap7)> |  Promise对象。异步返回专辑封面。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                  |
| -------- | ----------------------------------------- |
| 5400102  | Operation not allowed. Returned by promise. |
| 5400106  | Unsupported format. Returned by promise.  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import media from '@ohos.multimedia.media';
import image from '@ohos.multimedia.image';

let avMetadataExtractor: media.AVMetadataExtractor | undefined = undefined;
let pixel_map : image.PixelMap | undefined = undefined;

// 获取专辑封面
media.createAVMetadataExtractor((err: BusinessError, extractor: media.AVMetadataExtractor) => {
  if(extractor != null){
    avMetadataExtractor = extractor;
    console.error(`createAVMetadataExtractor success`);
    avMetadataExtractor.fetchAlbumCover().then((pixelMap: image.PixelMap) => {
      pixel_map = pixelMap;
    }).catch((error: BusinessError) => {
      console.error(`fetchAlbumCover catchCallback, error message:${error.message}`);
    });
  } else {
    console.error(`createAVMetadataExtractor fail, error message:${err.message}`);
  };
});
```

### release<sup>11+</sup>

release(callback: AsyncCallback\<void>): void

异步方式释放资源。通过注册回调函数获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.AVMetadataExtractor

**参数：**

| 参数名   | 类型                                         | 必填 | 说明                                |
| -------- | -------------------------------------------- | ---- | ----------------------------------- |
| callback | AsyncCallback\<void>                   | 是   | 异步释放资源release方法的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400102  | Operation not allowed. Returned by callback. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import media from '@ohos.multimedia.media';

let avMetadataExtractor: media.AVMetadataExtractor | undefined = undefined;

//释放资源
media.createAVMetadataExtractor((err: BusinessError, extractor: media.AVMetadataExtractor) => {
  if(extractor != null){
    avMetadataExtractor = extractor;
    console.error(`createAVMetadataExtractor success`);
    avMetadataExtractor.release((error: BusinessError) => {
      if (error) {
        console.error(`release failed, err = ${JSON.stringify(error)}`);
        return;
      }
      console.info(`release success.`);
    });
  } else {
    console.error(`createAVMetadataExtractor fail, error message:${err.message}`);
  };
});
```

### release<sup>11+</sup>

release(): Promise\<void>

异步方式释放资源。通过Promise获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.AVMetadataExtractor

**返回值：**

| 类型           | 说明                                     |
| -------------- | ---------------------------------------- |
| Promise\<void> | 异步方式释放资源release方法的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                  |
| -------- | ----------------------------------------- |
| 5400102  | Operation not allowed. Returned by promise. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import media from '@ohos.multimedia.media';

let avMetadataExtractor: media.AVMetadataExtractor | undefined = undefined;

//释放资源
media.createAVMetadataExtractor((err: BusinessError, extractor: media.AVMetadataExtractor) => {
  if(extractor != null){
    avMetadataExtractor = extractor;
    console.error(`createAVMetadataExtractor success`);
    avMetadataExtractor.release().then(() => {
      console.info(`release success.`);
    }).catch((error: BusinessError) => {
      console.error(`release catchCallback, error message:${error.message}`);
    });
  } else {
    console.error(`createAVMetadataExtractor fail, error message:${err.message}`);
  };
});
```

## AVMetadata<sup>11+</sup>

音视频元数据，包含各个元数据字段。

**系统能力：** SystemCapability.Multimedia.Media.AVMetadataExtractor

| 名称   | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| album     | string | 否   | 专辑的标题。     |
| albumArtist | string | 否   | 专辑的艺术家。 |
| artist | string | 否   | 媒体资源的艺术家。 |
| author | string | 否   | 媒体资源的作者。 |
| dateTime | string | 否   | 媒体资源的创建时间。 |
| dateTimeFormat | string | 否   | 媒体资源的创建时间，按YYYY-MM-DD HH:mm:ss格式输出。 |
| composer | string | 否   | 媒体资源的作曲家。 |
| duration | string | 否   | 媒体资源的时长。 |
| genre | string | 否   | 媒体资源的类型或体裁。 |
| hasAudio | string | 否   | 媒体资源是否包含音频。 |
| hasVideo | string | 否   | 媒体资源是否包含视频。 |
| mimeType | string | 否   | 媒体资源的mime类型。 |
| trackCount | string | 否   | 媒体资源的轨道数量。 |
| sampleRate | string | 否   | 音频的采样率，单位为赫兹（Hz）。 |
| title | string | 否   | 媒体资源的标题。 |
| videoHeight | string | 否   | 视频的高度，单位为像素。 |
| videoWidth | string | 否   | 视频的宽度，单位为像素。 |
| videoOrientation | string | 否   | 视频的旋转方向，单位为度（°）。 |

## media.createAudioPlayer<sup>(deprecated)</sup>

createAudioPlayer(): AudioPlayer

同步方式创建音频播放实例。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[createAVPlayer](#mediacreateavplayer9)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**返回值：**

| 类型                        | 说明                                                         |
| --------------------------- | ------------------------------------------------------------ |
| [AudioPlayer](#audioplayerdeprecated) | 返回AudioPlayer类实例，失败时返回null。可用于音频播放、暂停、停止等操作。 |

**示例：**

```ts
let audioPlayer: media.AudioPlayer = media.createAudioPlayer();
```

## media.createVideoPlayer<sup>(deprecated)</sup>

createVideoPlayer(callback: AsyncCallback\<VideoPlayer>): void

异步方式创建视频播放实例，通过注册回调函数获取返回值。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[createAVPlayer](#mediacreateavplayer9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型                                       | 必填 | 说明                                                         |
| -------- | ------------------------------------------ | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback<[VideoPlayer](#videoplayerdeprecated)> | 是   | 回调函数。异步返回VideoPlayer实例，失败时返回null。可用于管理和播放视频媒体。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let videoPlayer: media.VideoPlayer;
media.createVideoPlayer((error: BusinessError, video: media.VideoPlayer) => {
  if (video != null) {
    videoPlayer = video;
    console.info('video createVideoPlayer success');
  } else {
    console.error(`video createVideoPlayer fail, error:${error}`);
  }
});
```

## media.createVideoPlayer<sup>(deprecated)</sup>

createVideoPlayer(): Promise\<VideoPlayer>

异步方式创建视频播放实例，通过Promise获取返回值。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[createAVPlayer](#mediacreateavplayer9-1)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**返回值：**

| 类型                                 | 说明                                                         |
| ------------------------------------ | ------------------------------------------------------------ |
| Promise<[VideoPlayer](#videoplayerdeprecated)> | Promise对象。异步返回VideoPlayer实例，失败时返回null。可用于管理和播放视频媒体。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let videoPlayer: media.VideoPlayer;
media.createVideoPlayer().then((video: media.VideoPlayer) => {
  if (video != null) {
    videoPlayer = video;
    console.info('video createVideoPlayer success');
  } else {
    console.error('video createVideoPlayer fail');
  }
}).catch((error: BusinessError) => {
  console.error(`video catchCallback, error:${error}`);
});
```

## media.createAudioRecorder<sup>(deprecated)</sup>

createAudioRecorder(): AudioRecorder

创建音频录制的实例来控制音频的录制。
一台设备只允许创建一个录制实例。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[createAVRecorder](#mediacreateavrecorder9)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**返回值:**

| 类型                            | 说明                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| [AudioRecorder](#audiorecorderdeprecated) | 返回AudioRecorder类实例，失败时返回null。可用于录制音频媒体。 |

**示例：**

```ts
let audioRecorder: media.AudioRecorder = media.createAudioRecorder();
```

## MediaErrorCode<sup>(deprecated)</sup>

媒体服务错误类型枚举。

> **说明：**
> 从API version 8开始支持，从API version 11开始废弃，建议使用[媒体错误码](#averrorcode9)替代。

**系统能力：** SystemCapability.Multimedia.Media.Core

| 名称                       | 值   | 说明                                   |
| -------------------------- | ---- | -------------------------------------- |
| MSERR_OK                   | 0    | 表示操作成功。                         |
| MSERR_NO_MEMORY            | 1    | 表示申请内存失败，系统可能无可用内存。 |
| MSERR_OPERATION_NOT_PERMIT | 2    | 表示无权限执行此操作。                 |
| MSERR_INVALID_VAL          | 3    | 表示传入入参无效。                     |
| MSERR_IO                   | 4    | 表示发生IO错误。                       |
| MSERR_TIMEOUT              | 5    | 表示操作超时。                         |
| MSERR_UNKNOWN              | 6    | 表示未知错误。                         |
| MSERR_SERVICE_DIED         | 7    | 表示服务端失效。                       |
| MSERR_INVALID_STATE        | 8    | 表示在当前状态下，不允许执行此操作。   |
| MSERR_UNSUPPORTED          | 9    | 表示在当前版本下，不支持此操作。       |

## AudioPlayer<sup>(deprecated)</sup>

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVPlayer](#avplayer9)替代。

音频播放管理类，用于管理和播放音频媒体。在调用AudioPlayer的方法前，需要先通过[createAudioPlayer()](#mediacreateaudioplayerdeprecated)构建一个AudioPlayer实例。

### 属性<sup>(deprecated)</sup>

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

| 名称                            | 类型                                                   | 可读 | 可写 | 说明                                                         |
| ------------------------------- | ------------------------------------------------------ | ---- | ---- | ------------------------------------------------------------ |
| src                             | string                                                 | 是   | 是   | 音频媒体URI，支持当前主流的音频格式(m4a、aac、mp3、ogg、wav)。<br>**支持路径示例**：<br>1. fd类型播放：fd://xx<br>![](figures/zh-cn_image_url.png)<br>2. http网络播放: http\://xx<br/>3. https网络播放: https\://xx<br/>4. hls网络播放路径：http\://xx或者https\://xx <br/>**需要权限：** ohos.permission.READ_MEDIA 或 ohos.permission.INTERNET。 |
| fdSrc<sup>9+</sup>              | [AVFileDescriptor](#avfiledescriptor9)                 | 是   | 是   | 音频媒体文件描述，使用场景：应用中的音频资源被连续存储在同一个文件中。<br/>**使用示例**：<br/>假设一个连续存储的音乐文件: <br/>音乐1(地址偏移:0，字节长度:100)<br/>音乐2(地址偏移:101，字节长度:50)<br/>音乐3(地址偏移:151，字节长度:150)<br/>1. 播放音乐1：AVFileDescriptor { fd = 资源句柄; offset = 0; length = 100; }<br/>2. 播放音乐2：AVFileDescriptor { fd = 资源句柄; offset = 101; length = 50; }<br/>3. 播放音乐3：AVFileDescriptor { fd = 资源句柄; offset = 151; length = 150; }<br/>假设是一个独立的音乐文件: 请使用src=fd://xx <br/> |
| loop                            | boolean                                                | 是   | 是   | 音频循环播放属性，设置为'true'表示循环播放。                 |
| audioInterruptMode<sup>9+</sup> | [audio.InterruptMode](../apis-audio-kit/js-apis-audio.md#interruptmode9) | 是   | 是   | 音频焦点模型。                                               |
| currentTime                     | number                                                 | 是   | 否   | 音频的当前播放位置，单位为毫秒（ms）。                       |
| duration                        | number                                                 | 是   | 否   | 音频时长，单位为毫秒（ms）。                                 |
| state                           | [AudioState](#audiostatedeprecated)                              | 是   | 否   | 可以查询音频播放的状态，该状态不可作为调用play/pause/stop等状态切换的触发条件。 |

### play<sup>(deprecated)</sup>

play(): void

开始播放音频资源，需在'dataLoad'事件成功触发后，才能调用。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVPlayer.play](#play9)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**示例：**

```ts
audioPlayer.on('play', () => {    //设置'play'事件回调
  console.info('audio play success');
});
audioPlayer.play();
```

### pause<sup>(deprecated)</sup>

pause(): void

暂停播放音频资源。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVPlayer.pause](#pause9)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**示例：**

```ts
audioPlayer.on('pause', () => {    //设置'pause'事件回调
  console.info('audio pause success');
});
audioPlayer.pause();
```

### stop<sup>(deprecated)</sup>

stop(): void

停止播放音频资源。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVPlayer.stop](#stop9)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**示例：**

```ts
audioPlayer.on('stop', () => {    //设置'stop'事件回调
  console.info('audio stop success');
});
audioPlayer.stop();
```

### reset<sup>(deprecated)</sup>

reset(): void

重置播放音频资源。

> **说明：**
> 从API version 7开始支持，从API version 9开始废弃，建议使用[AVPlayer.reset](#reset9)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**示例：**

```ts
audioPlayer.on('reset', () => {    //设置'reset'事件回调
  console.info('audio reset success');
});
audioPlayer.reset();
```

### seek<sup>(deprecated)</sup>

seek(timeMs: number): void

跳转到指定播放位置。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVPlayer.seek](#seek9)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                        |
| ------ | ------ | ---- | ----------------------------------------------------------- |
| timeMs | number | 是   | 指定的跳转时间节点，单位毫秒（ms），取值范围[0, duration]。 |

**示例：**

```ts
audioPlayer.on('timeUpdate', (seekDoneTime: number) => {    //设置'timeUpdate'事件回调
  if (seekDoneTime == null) {
    console.error('audio seek fail');
    return;
  }
  console.info('audio seek success. seekDoneTime: ' + seekDoneTime);
});
audioPlayer.seek(30000);    //seek到30000ms的位置
```

### setVolume<sup>(deprecated)</sup>

setVolume(vol: number): void

设置音量。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVPlayer.setVolume](#setvolume9)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| vol    | number | 是   | 指定的相对音量大小，取值范围为[0.00-1.00]，1表示最大音量，即100%。 |

**示例：**

```ts
audioPlayer.on('volumeChange', () => {    //设置'volumeChange'事件回调
  console.info('audio volumeChange success');
});
audioPlayer.setVolume(1);    //设置音量到100%
```

### release<sup>(deprecated)</sup>

release(): void

释放音频资源。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVPlayer.release](#release9)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**示例：**

```ts
audioPlayer.release();
audioPlayer = undefined;
```

### getTrackDescription<sup>(deprecated)</sup>

getTrackDescription(callback: AsyncCallback\<Array\<MediaDescription>>): void

通过回调方式获取音频轨道信息。需在'dataLoad'事件成功触发后，才能调用。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.getTrackDescription](#gettrackdescription9)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                       |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------ |
| callback | AsyncCallback\<Array\<[MediaDescription](#mediadescription8)>> | 是   | 音频轨道信息MediaDescription数组回调方法。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioPlayer.getTrackDescription((error: BusinessError, arrList: Array<media.MediaDescription>) => {
  if (arrList != null) {
    console.info('audio getTrackDescription success');
  } else {
    console.error(`audio getTrackDescription fail, error:${error}`);
  }
});
```

### getTrackDescription<sup>(deprecated)</sup>

getTrackDescription(): Promise\<Array\<MediaDescription>>

通过Promise方式获取音频轨道信息。需在'dataLoad'事件成功触发后，才能调用。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.getTrackDescription](#gettrackdescription9-1)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**返回值：**

| 类型                                                   | 说明                                            |
| ------------------------------------------------------ | ----------------------------------------------- |
| Promise<Array<[MediaDescription](#mediadescription8)>> | 音频轨道信息MediaDescription数组Promise返回值。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioPlayer.getTrackDescription().then((arrList: Array<media.MediaDescription>) => {
  console.info('audio getTrackDescription success');
}).catch((error: BusinessError) => {
  console.error(`audio catchCallback, error:${error}`);
});
```

### on('bufferingUpdate')<sup>(deprecated)</sup>

on(type: 'bufferingUpdate', callback: (infoType: BufferingInfoType, value: number) => void): void

开始订阅音频缓存更新事件。仅网络播放支持该订阅事件。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.on('bufferingUpdate')](#onbufferingupdate9)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | 音频缓存事件回调类型，支持的事件：'bufferingUpdate'。        |
| callback | function | 是   | 音频缓存事件回调方法。<br>[BufferingInfoType](#bufferinginfotype8)为BUFFERING_PERCENT或CACHED_DURATION时，value值有效，否则固定为0。 |

**示例：**

```ts
audioPlayer.on('bufferingUpdate', (infoType: media.BufferingInfoType, value: number) => {
  console.info('audio bufferingInfo type: ' + infoType);
  console.info('audio bufferingInfo value: ' + value);
});
```

### on('play' | 'pause' | 'stop' | 'reset' | 'dataLoad' | 'finish' | 'volumeChange')<sup>(deprecated)</sup>

on(type: 'play' | 'pause' | 'stop' | 'reset' | 'dataLoad' | 'finish' | 'volumeChange', callback: () => void): void

开始订阅音频播放事件。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVPlayer.on('stateChange')](#onstatechange9)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**参数：**

| 参数名   | 类型       | 必填 | 说明                                                         |
| -------- | ---------- | ---- | ------------------------------------------------------------ |
| type     | string     | 是   | 播放事件回调类型，支持的事件包括：'play' \| 'pause' \| 'stop' \| 'reset' \| 'dataLoad' \| 'finish' \| 'volumeChange'。<br>- 'play'：完成[play()](#playdeprecated)调用，音频开始播放，触发该事件。<br>- 'pause'：完成[pause()](#pausedeprecated)调用，音频暂停播放，触发该事件。<br>- 'stop'：完成[stop()](#stopdeprecated)调用，音频停止播放，触发该事件。<br>- 'reset'：完成[reset()](#resetdeprecated)调用，播放器重置，触发该事件。<br>- 'dataLoad'：完成音频数据加载后触发该事件，即src属性设置完成后触发该事件。<br>- 'finish'：完成音频播放后触发该事件。<br>- 'volumeChange'：完成[setVolume()](#setvolumedeprecated)调用，播放音量改变后触发该事件。 |
| callback | () => void | 是   | 播放事件回调方法。                                           |

**示例：**

```ts
import fs from '@ohos.file.fs';
import { BusinessError } from '@ohos.base';

let audioPlayer: media.AudioPlayer = media.createAudioPlayer();  //创建一个音频播放实例
audioPlayer.on('dataLoad', () => {            //设置'dataLoad'事件回调，src属性设置成功后，触发此回调
  console.info('audio set source success');
  audioPlayer.play();                       //开始播放，并触发'play'事件回调
});
audioPlayer.on('play', () => {                //设置'play'事件回调
  console.info('audio play success');
  audioPlayer.seek(30000);                  //调用seek方法，并触发'timeUpdate'事件回调
});
audioPlayer.on('pause', () => {               //设置'pause'事件回调
  console.info('audio pause success');
  audioPlayer.stop();                       //停止播放，并触发'stop'事件回调
});
audioPlayer.on('reset', () => {               //设置'reset'事件回调
  console.info('audio reset success');
  audioPlayer.release();                    //释放播放实例资源
  audioPlayer = undefined;
});
audioPlayer.on('timeUpdate', (seekDoneTime: number) => {  //设置'timeUpdate'事件回调
  if (seekDoneTime == null) {
    console.error('audio seek fail');
    return;
  }
  console.info('audio seek success, and seek time is ' + seekDoneTime);
  audioPlayer.setVolume(0.5);                //设置音量为50%，并触发'volumeChange'事件回调
});
audioPlayer.on('volumeChange', () => {         //设置'volumeChange'事件回调
  console.info('audio volumeChange success');
  audioPlayer.pause();                       //暂停播放，并触发'pause'事件回调
});
audioPlayer.on('finish', () => {               //设置'finish'事件回调
  console.info('audio play finish');
  audioPlayer.stop();                        //停止播放，并触发'stop'事件回调
});
audioPlayer.on('error', (error: BusinessError) => {  //设置'error'事件回调
  console.error(`audio error called, error: ${error}`);
});

// 用户选择音频设置fd(本地播放)
let fdPath = 'fd://';
// path路径的码流可通过"hdc file send D:\xxx\01.mp3 /data/accounts/account_0/appdata" 命令，将其推送到设备上
let path = '/data/accounts/account_0/appdata/ohos.xxx.xxx.xxx/01.mp3';
fs.open(path).then((file) => {
  fdPath = fdPath + '' + file.fd;
  console.info('open fd success fd is' + fdPath);
  audioPlayer.src = fdPath;  //设置src属性，并触发'dataLoad'事件回调
}, (err: BusinessError) => {
  console.error('open fd failed err is' + err);
}).catch((err: BusinessError) => {
  console.error('open fd failed err is' + err);
});
```

### on('timeUpdate')<sup>(deprecated)</sup>

on(type: 'timeUpdate', callback: Callback\<number>): void

开始订阅音频播放时间更新事件。处于播放状态时，每隔1s上报一次该事件。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVPlayer.on('timeUpdate')](#ontimeupdate9)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**参数：**

| 参数名   | 类型              | 必填 | 说明                                                         |
| -------- | ----------------- | ---- | ------------------------------------------------------------ |
| type     | string            | 是   | 播放事件回调类型，支持的事件包括：'timeUpdate'。<br>- 'timeUpdate'：音频播放时间戳更新，开始播放后自动触发该事件。 |
| callback | Callback\<number> | 是   | 播放事件回调方法。回调方法入参为更新后的时间戳。             |

**示例：**

```ts
audioPlayer.on('timeUpdate', (newTime: number) => {    //设置'timeUpdate'事件回调
  if (newTime == null) {
    console.error('audio timeUpadate fail');
    return;
  }
  console.info('audio timeUpadate success. seekDoneTime: ' + newTime);
});
audioPlayer.play();    //开始播放后，自动触发时间戳更新事件
```

### on('audioInterrupt')<sup>(deprecated)</sup>

on(type: 'audioInterrupt', callback: (info: audio.InterruptEvent) => void): void

监听音频焦点变化事件，参考[audio.InterruptEvent](../apis-audio-kit/js-apis-audio.md#interruptevent9)。

> **说明：**
> 从API version 9开始支持，从API version 9开始废弃，建议使用[AVPlayer.on('audioInterrupt')](#onaudiointerrupt9)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                     |
| -------- | ------------------------------------------------------------ | ---- | -------------------------------------------------------- |
| type     | string                                                       | 是   | 音频焦点变化事件回调类型，支持的事件：'audioInterrupt'。 |
| callback | function  | 是   | 音频焦点变化事件回调方法。                               |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

audioPlayer.on('audioInterrupt', (info: audio.InterruptEvent) => {
  console.info('audioInterrupt success,and InterruptEvent info is:' + info)
})
```

### on('error')<sup>(deprecated)</sup>

on(type: 'error', callback: ErrorCallback): void

开始订阅音频播放错误事件，当上报error错误事件后，用户需处理error事件，退出播放操作。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVPlayer.on('error')](#onerror9)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

**参数：**

| 参数名   | 类型          | 必填 | 说明                                                         |
| -------- | ------------- | ---- | ------------------------------------------------------------ |
| type     | string        | 是   | 播放错误事件回调类型，支持的事件包括：'error'。<br>- 'error'：音频播放中发生错误，触发该事件。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback) | 是   | 播放错误事件回调方法。                                       |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

audioPlayer.on('error', (error: BusinessError) => {  //设置'error'事件回调
  console.error(`audio error called, error: ${error}`);
});
audioPlayer.setVolume(3);  //设置volume为无效值，触发'error'事件
```

## AudioState<sup>(deprecated)</sup>

音频播放的状态机。可通过state属性获取当前状态。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVPlayerState](#avplayerstate9)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioPlayer

| 名称    | 类型   | 说明                                           |
| ------- | ------ | ---------------------------------------------- |
| idle    | string | 音频播放空闲，dataload/reset成功后处于此状态。 |
| playing | string | 音频正在播放，play成功后处于此状态。           |
| paused  | string | 音频暂停播放，pause成功后处于此状态。          |
| stopped | string | 音频播放停止，stop/播放结束后处于此状态。      |
| error   | string | 错误状态。                                     |

## VideoPlayer<sup>(deprecated)</sup>

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer](#avplayer9)替代。

视频播放管理类，用于管理和播放视频媒体。在调用VideoPlayer的方法前，需要先通过[createVideoPlayer()](#mediacreatevideoplayerdeprecated)构建一个VideoPlayer实例。

### 属性

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

| 名称                            | 类型                                                   | 可读 | 可写 | 说明                                                         |
| ------------------------------- | ------------------------------------------------------ | ---- | ---- | ------------------------------------------------------------ |
| url<sup>8+</sup>                | string                                                 | 是   | 是   | 视频媒体URL，支持当前主流的视频格式(mp4、mpeg-ts、mkv)。<br>**支持路径示例**：<br>1. fd类型播放：fd://xx<br>![](figures/zh-cn_image_url.png)<br>2. http网络播放: http\://xx<br/>3. https网络播放: https\://xx<br/>4. hls网络播放路径：http\://xx或者https\://xx<br>5. file类型: file\://xx<br/>**说明：**<br>从API version 11开始不支持webm。 |
| fdSrc<sup>9+</sup>              | [AVFileDescriptor](#avfiledescriptor9)                 | 是   | 是   | 视频媒体文件描述，使用场景：应用中的视频资源被连续存储在同一个文件中。<br/>**使用示例**：<br/>假设一个连续存储的音乐文件: <br/>视频1(地址偏移:0，字节长度:100)<br/>视频2(地址偏移:101，字节长度:50)<br/>视频3(地址偏移:151，字节长度:150)<br/>1. 播放视频1：AVFileDescriptor { fd = 资源句柄; offset = 0; length = 100; }<br/>2. 播放视频2：AVFileDescriptor { fd = 资源句柄; offset = 101; length = 50; }<br/>3. 播放视频3：AVFileDescriptor { fd = 资源句柄; offset = 151; length = 150; }<br/>假设是一个独立的视频文件: 请使用src=fd://xx <br/> |
| loop<sup>8+</sup>               | boolean                                                | 是   | 是   | 视频循环播放属性，设置为'true'表示循环播放。                 |
| videoScaleType<sup>9+</sup>     | [VideoScaleType](#videoscaletype9)                     | 是   | 是   | 视频缩放模式。默认值为VIDEO_SCALE_TYPE_FIT。                                               |
| audioInterruptMode<sup>9+</sup> | [audio.InterruptMode](../apis-audio-kit/js-apis-audio.md#interruptmode9) | 是   | 是   | 音频焦点模型。                                               |
| currentTime<sup>8+</sup>        | number                                                 | 是   | 否   | 视频的当前播放位置，单位为毫秒（ms）。                       |
| duration<sup>8+</sup>           | number                                                 | 是   | 否   | 视频时长，单位为毫秒（ms），返回-1表示直播模式。             |
| state<sup>8+</sup>              | [VideoPlayState](#videoplaystatedeprecated)                    | 是   | 否   | 视频播放的状态。                                             |
| width<sup>8+</sup>              | number                                                 | 是   | 否   | 视频宽，单位为像素（px）。                                   |
| height<sup>8+</sup>             | number                                                 | 是   | 否   | 视频高，单位为像素（px）。                                   |

### setDisplaySurface<sup>(deprecated)</sup>

setDisplaySurface(surfaceId: string, callback: AsyncCallback\<void>): void

通过回调方式设置SurfaceId。

*注意：SetDisplaySurface需要在设置url和Prepare之间，无音频的视频流必须设置Surface否则Prepare失败。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.surfaceId](#属性)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名    | 类型                 | 必填 | 说明                      |
| --------- | -------------------- | ---- | ------------------------- |
| surfaceId | string               | 是   | SurfaceId                 |
| callback  | AsyncCallback\<void> | 是   | 设置SurfaceId的回调方法。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let surfaceId: string = '';
videoPlayer.setDisplaySurface(surfaceId, (err: BusinessError) => {
  if (err == null) {
    console.info('setDisplaySurface success!');
  } else {
    console.error('setDisplaySurface fail!');
  }
});
```

### setDisplaySurface<sup>(deprecated)</sup>

setDisplaySurface(surfaceId: string): Promise\<void>

通过Promise方式设置SurfaceId。

*注意：SetDisplaySurface需要在设置url和Prepare之间，无音频的视频流必须设置Surface否则Prepare失败。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.surfaceId](#属性)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名    | 类型   | 必填 | 说明      |
| --------- | ------ | ---- | --------- |
| surfaceId | string | 是   | SurfaceId |

**返回值：**

| 类型           | 说明                           |
| -------------- | ------------------------------ |
| Promise\<void> | 设置SurfaceId的Promise返回值。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let surfaceId: string = '';
videoPlayer.setDisplaySurface(surfaceId).then(() => {
  console.info('setDisplaySurface success');
}).catch((error: BusinessError) => {
  console.error(`video catchCallback, error:${error}`);
});
```

### prepare<sup>(deprecated)</sup>

prepare(callback: AsyncCallback\<void>): void

通过回调方式准备播放视频。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.prepare](#prepare9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型                 | 必填 | 说明                     |
| -------- | -------------------- | ---- | ------------------------ |
| callback | AsyncCallback\<void> | 是   | 准备播放视频的回调方法。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

videoPlayer.prepare((err: BusinessError) => {
  if (err == null) {
    console.info('prepare success!');
  } else {
    console.error('prepare fail!');
  }
});
```

### prepare<sup>(deprecated)</sup>

prepare(): Promise\<void>

通过Promise方式准备播放视频。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.prepare](#prepare9-1)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | 准备播放视频的Promise返回值。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

videoPlayer.prepare().then(() => {
  console.info('prepare success');
}).catch((error: BusinessError) => {
  console.error(`video catchCallback, error:${error}`);
});
```

### play<sup>(deprecated)</sup>

play(callback: AsyncCallback\<void>): void

通过回调方式开始播放视频。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.play](#play9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型                 | 必填 | 说明                     |
| -------- | -------------------- | ---- | ------------------------ |
| callback | AsyncCallback\<void> | 是   | 开始播放视频的回调方法。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

videoPlayer.play((err: BusinessError) => {
  if (err == null) {
    console.info('play success!');
  } else {
    console.error('play fail!');
  }
});
```

### play<sup>(deprecated)</sup>

play(): Promise\<void>

通过Promise方式开始播放视频。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.play](#play9-1)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | 开始播放视频的Promise返回值。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

videoPlayer.play().then(() => {
  console.info('play success');
}).catch((error: BusinessError) => {
  console.error(`video catchCallback, error:${error}`);
});
```

### pause<sup>(deprecated)</sup>

pause(callback: AsyncCallback\<void>): void

通过回调方式暂停播放视频。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.pause](#pause9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型                 | 必填 | 说明                     |
| -------- | -------------------- | ---- | ------------------------ |
| callback | AsyncCallback\<void> | 是   | 暂停播放视频的回调方法。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

videoPlayer.pause((err: BusinessError) => {
  if (err == null) {
    console.info('pause success!');
  } else {
    console.error('pause fail!');
  }
});
```

### pause<sup>(deprecated)</sup>

pause(): Promise\<void>

通过Promise方式暂停播放视频。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.pause](#pause9-1)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | 暂停播放视频的Promise返回值。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

videoPlayer.pause().then(() => {
  console.info('pause success');
}).catch((error: BusinessError) => {
  console.error(`video catchCallback, error:${error}`);
});
```

### stop<sup>(deprecated)</sup>

stop(callback: AsyncCallback\<void>): void

通过回调方式停止播放视频。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.stop](#stop9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型                 | 必填 | 说明                     |
| -------- | -------------------- | ---- | ------------------------ |
| callback | AsyncCallback\<void> | 是   | 停止播放视频的回调方法。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

videoPlayer.stop((err: BusinessError) => {
  if (err == null) {
    console.info('stop success!');
  } else {
    console.error('stop fail!');
  }
});
```

### stop<sup>(deprecated)</sup>

stop(): Promise\<void>

通过Promise方式停止播放视频。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.stop](#stop9-1)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | 停止播放视频的Promise返回值。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

videoPlayer.stop().then(() => {
  console.info('stop success');
}).catch((error: BusinessError) => {
  console.error(`video catchCallback, error:${error}`);
});
```

### reset<sup>(deprecated)</sup>

reset(callback: AsyncCallback\<void>): void

通过回调方式重置播放视频。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.reset](#reset9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型                 | 必填 | 说明                     |
| -------- | -------------------- | ---- | ------------------------ |
| callback | AsyncCallback\<void> | 是   | 切换播放视频的回调方法。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

videoPlayer.reset((err: BusinessError) => {
  if (err == null) {
    console.info('reset success!');
  } else {
    console.error('reset fail!');
  }
});
```

### reset<sup>(deprecated)</sup>

reset(): Promise\<void>

通过Promise方式重置播放视频。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.reset](#reset9-1)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | 切换播放视频的Promise返回值。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

videoPlayer.reset().then(() => {
  console.info('reset success');
}).catch((error: BusinessError) => {
  console.error(`video catchCallback, error:${error}`);
});
```

### seek<sup>(deprecated)</sup>

seek(timeMs: number, callback: AsyncCallback\<number>): void

通过回调方式跳转到指定播放位置，默认跳转到指定时间点的上一个关键帧。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.seek](#seek9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型                   | 必填 | 说明                                                         |
| -------- | ---------------------- | ---- | ------------------------------------------------------------ |
| timeMs   | number                 | 是   | 指定的跳转时间节点，单位毫秒（ms），取值范围为[0, duration]。 |
| callback | AsyncCallback\<number> | 是   | 跳转到指定播放位置的回调方法。                               |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let videoPlayer: media.VideoPlayer;
media.createVideoPlayer((error: BusinessError, video: media.VideoPlayer) => {
  if (video != null) {
    videoPlayer = video;
    console.info('video createVideoPlayer success');
  } else {
    console.error(`video createVideoPlayer fail, error:${error}`);
  }
});

let seekTime: number = 5000;
videoPlayer.seek(seekTime, (err: BusinessError, result: number) => {
  if (err == null) {
    console.info('seek success!');
  } else {
    console.error('seek fail!');
  }
});
```

### seek<sup>(deprecated)</sup>

seek(timeMs: number, mode:SeekMode, callback: AsyncCallback\<number>): void

通过回调方式跳转到指定播放位置。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.seek](#seek9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型                   | 必填 | 说明                                                         |
| -------- | ---------------------- | ---- | ------------------------------------------------------------ |
| timeMs   | number                 | 是   | 指定的跳转时间节点，单位毫秒（ms），取值范围为[0, duration]。 |
| mode     | [SeekMode](#seekmode8) | 是   | 跳转模式。                                                   |
| callback | AsyncCallback\<number> | 是   | 跳转到指定播放位置的回调方法。                               |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let videoPlayer: media.VideoPlayer | null = null;
media.createVideoPlayer((error: BusinessError, video: media.VideoPlayer) => {
  if (video != null) {
    videoPlayer = video;
    console.info('video createVideoPlayer success');
  } else {
    console.error(`video createVideoPlayer fail, error:${error}`);
  }
});
let seekTime: number = 5000;
if (videoPlayer) {
  (videoPlayer as media.VideoPlayer).seek(seekTime, media.SeekMode.SEEK_NEXT_SYNC, (err: BusinessError, result: number) => {
    if (err == null) {
      console.info('seek success!');
    } else {
      console.error('seek fail!');
    }
  });
}
```

### seek<sup>(deprecated)</sup>

seek(timeMs: number, mode?:SeekMode): Promise\<number>

通过Promise方式跳转到指定播放位置，如果没有设置mode则跳转到指定时间点的上一个关键帧。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.seek](#seek9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名 | 类型                   | 必填 | 说明                                                         |
| ------ | ---------------------- | ---- | ------------------------------------------------------------ |
| timeMs | number                 | 是   | 指定的跳转时间节点，单位毫秒（ms），取值范围为[0, duration]。 |
| mode   | [SeekMode](#seekmode8) | 否   | 基于视频I帧的跳转模式，默认为SEEK_PREV_SYNC模式。            |

**返回值：**

| 类型             | 说明                                        |
| ---------------- | ------------------------------------------- |
| Promise\<number> | 跳转到指定播放位置的Promise返回值，单位ms。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let videoPlayer: media.VideoPlayer | null = null;
media.createVideoPlayer((error: BusinessError, video: media.VideoPlayer) => {
  if (video != null) {
    videoPlayer = video;
    console.info('video createVideoPlayer success');
  } else {
    console.error(`video createVideoPlayer fail, error:${error}`);
  }
});
let seekTime: number = 5000;
if (videoPlayer) {
  (videoPlayer as media.VideoPlayer).seek(seekTime).then((seekDoneTime: number) => { // seekDoneTime表示seek完成后的时间点
    console.info('seek success');
  }).catch((error: BusinessError) => {
    console.error(`video catchCallback, error:${error}`);
  });

  (videoPlayer as media.VideoPlayer).seek(seekTime, media.SeekMode.SEEK_NEXT_SYNC).then((seekDoneTime: number) => {
    console.info('seek success');
  }).catch((error: BusinessError) => {
    console.error(`video catchCallback, error:${error}`);
  });
}
```

### setVolume<sup>(deprecated)</sup>

setVolume(vol: number, callback: AsyncCallback\<void>): void

通过回调方式设置音量。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.setVolume](#setvolume9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                                         |
| -------- | -------------------- | ---- | ------------------------------------------------------------ |
| vol      | number               | 是   | 指定的相对音量大小，取值范围为[0.00-1.00]，1表示最大音量，即100%。 |
| callback | AsyncCallback\<void> | 是   | 设置音量的回调方法。                                         |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let vol: number = 0.5;
videoPlayer.setVolume(vol, (err: BusinessError) => {
  if (err == null) {
    console.info('setVolume success!');
  } else {
    console.error('setVolume fail!');
  }
});
```

### setVolume<sup>(deprecated)</sup>

setVolume(vol: number): Promise\<void>

通过Promise方式设置音量。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.setVolume](#setvolume9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| vol    | number | 是   | 指定的相对音量大小，取值范围为[0.00-1.00]，1表示最大音量，即100%。 |

**返回值：**

| 类型           | 说明                      |
| -------------- | ------------------------- |
| Promise\<void> | 设置音量的Promise返回值。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let vol: number = 0.5;
videoPlayer.setVolume(vol).then(() => {
  console.info('setVolume success');
}).catch((error: BusinessError) => {
  console.error(`video catchCallback, error:${error}`);
});
```

### release<sup>(deprecated)</sup>

release(callback: AsyncCallback\<void>): void

通过回调方式释放视频资源。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.release](#release9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型                 | 必填 | 说明                     |
| -------- | -------------------- | ---- | ------------------------ |
| callback | AsyncCallback\<void> | 是   | 释放视频资源的回调方法。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

videoPlayer.release((err: BusinessError) => {
  if (err == null) {
    console.info('release success!');
  } else {
    console.error('release fail!');
  }
});
```

### release<sup>(deprecated)</sup>

release(): Promise\<void>

通过Promise方式释放视频资源。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.release](#release9-1)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**返回值：**

| 类型           | 说明                          |
| -------------- | ----------------------------- |
| Promise\<void> | 释放视频资源的Promise返回值。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

videoPlayer.release().then(() => {
  console.info('release success');
}).catch((error: BusinessError) => {
  console.error(`video catchCallback, error:${error}`);
});
```

### getTrackDescription<sup>(deprecated)</sup>

getTrackDescription(callback: AsyncCallback\<Array\<MediaDescription>>): void

通过回调方式获取视频轨道信息。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.getTrackDescription](#gettrackdescription9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                       |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------ |
| callback | AsyncCallback\<Array\<[MediaDescription](#mediadescription8)>> | 是   | 视频轨道信息MediaDescription数组回调方法。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

videoPlayer.getTrackDescription((error: BusinessError, arrList: Array<media.MediaDescription>) => {
  if ((arrList) != null) {
    console.info('video getTrackDescription success');
  } else {
    console.error(`video getTrackDescription fail, error:${error}`);
  }
});
```

### getTrackDescription<sup>(deprecated)</sup>

getTrackDescription(): Promise\<Array\<MediaDescription>>

通过Promise方式获取视频轨道信息。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.getTrackDescription](#gettrackdescription9-1)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**返回值：**

| 类型                                                   | 说明                                            |
| ------------------------------------------------------ | ----------------------------------------------- |
| Promise<Array<[MediaDescription](#mediadescription8)>> | 视频轨道信息MediaDescription数组Promise返回值。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

videoPlayer.getTrackDescription().then((arrList: Array<media.MediaDescription>) => {
  if (arrList != null) {
    console.info('video getTrackDescription success');
  } else {
    console.error('video getTrackDescription fail');
  }
}).catch((error: BusinessError) => {
  console.error(`video catchCallback, error:${error}`);
});
```

### setSpeed<sup>(deprecated)</sup>

setSpeed(speed: number, callback: AsyncCallback\<number>): void

通过回调方式设置播放速度。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.setSpeed](#setspeed9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型                   | 必填 | 说明                                                       |
| -------- | ---------------------- | ---- | ---------------------------------------------------------- |
| speed    | number                 | 是   | 指定播放视频速度，具体见[PlaybackSpeed](#playbackspeed8)。 |
| callback | AsyncCallback\<number> | 是   | 设置播放速度的回调方法。                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let videoPlayer: media.VideoPlayer | null = null;
media.createVideoPlayer((error: BusinessError, video: media.VideoPlayer) => {
  if (video != null) {
    videoPlayer = video;
    console.info('video createVideoPlayer success');
  } else {
    console.error(`video createVideoPlayer fail, error:${error}`);
  }
});
let speed = media.PlaybackSpeed.SPEED_FORWARD_2_00_X;
if (videoPlayer) {
  (videoPlayer as media.VideoPlayer).setSpeed(speed, (err: BusinessError, result: number) => {
    if (err == null) {
      console.info('setSpeed success!');
    } else {
      console.error('setSpeed fail!');
    }
  });
}
```

### setSpeed<sup>(deprecated)</sup>

setSpeed(speed: number): Promise\<number>

通过Promise方式设置播放速度。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.setSpeed](#setspeed9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                       |
| ------ | ------ | ---- | ---------------------------------------------------------- |
| speed  | number | 是   | 指定播放视频速度，具体见[PlaybackSpeed](#playbackspeed8)。 |

**返回值：**

| 类型             | 说明                                                         |
| ---------------- | ------------------------------------------------------------ |
| Promise\<number> | 播放速度Promise返回值，具体见[PlaybackSpeed](#playbackspeed8)。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let videoPlayer: media.VideoPlayer | null = null;
media.createVideoPlayer((error: BusinessError, video: media.VideoPlayer) => {
  if (video != null) {
    videoPlayer = video;
    console.info('video createVideoPlayer success');
  } else {
    console.error(`video createVideoPlayer fail, error:${error}`);
  }
});
let speed = media.PlaybackSpeed.SPEED_FORWARD_2_00_X;
if (videoPlayer) {
  (videoPlayer as media.VideoPlayer).setSpeed(speed).then((result: number) => {
    console.info('setSpeed success');
  }).catch((error: BusinessError) => {
    console.error(`video catchCallback, error:${error}`);
  });
}
```

### on('playbackCompleted')<sup>(deprecated)</sup>

on(type: 'playbackCompleted', callback: Callback\<void>): void

开始监听视频播放完成事件。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.on('stateChange')](#onstatechange9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                        |
| -------- | -------- | ---- | ----------------------------------------------------------- |
| type     | string   | 是   | 视频播放完成事件回调类型，支持的事件：'playbackCompleted'。 |
| callback | Callback\<void> | 是   | 视频播放完成事件回调方法。                                  |

**示例：**

```ts
videoPlayer.on('playbackCompleted', () => {
  console.info('playbackCompleted success!');
});
```

### on('bufferingUpdate')<sup>(deprecated)</sup>

on(type: 'bufferingUpdate', callback: (infoType: BufferingInfoType, value: number) => void): void

开始监听视频缓存更新事件。仅网络播放支持该订阅事件。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.on('bufferingUpdate')](#onbufferingupdate9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | 视频缓存事件回调类型，支持的事件：'bufferingUpdate'。        |
| callback | function | 是   | 视频缓存事件回调方法。<br>[BufferingInfoType](#bufferinginfotype8)为BUFFERING_PERCENT或CACHED_DURATION时，value值有效，否则固定为0。 |

**示例：**

```ts
videoPlayer.on('bufferingUpdate', (infoType: media.BufferingInfoType, value: number) => {
  console.info('video bufferingInfo type: ' + infoType);
  console.info('video bufferingInfo value: ' + value);
});
```

### on('startRenderFrame')<sup>(deprecated)</sup>

on(type: 'startRenderFrame', callback: Callback\<void>): void

开始监听视频播放首帧送显上报事件。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.on('startRenderFrame')](#onstartrenderframe9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型            | 必填 | 说明                                                         |
| -------- | --------------- | ---- | ------------------------------------------------------------ |
| type     | string          | 是   | 视频播放首帧送显上报事件回调类型，支持的事件：'startRenderFrame'。 |
| callback | Callback\<void> | 是   | 视频播放首帧送显上报事件回调方法。                           |

**示例：**

```ts
videoPlayer.on('startRenderFrame', () => {
  console.info('startRenderFrame success!');
});
```

### on('videoSizeChanged')<sup>(deprecated)</sup>

on(type: 'videoSizeChanged', callback: (width: number, height: number) => void): void

开始监听视频播放宽高变化事件。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.on('videoSizeChange')](#onvideosizechange9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | 视频播放宽高变化事件回调类型，支持的事件：'videoSizeChanged'。 |
| callback | function | 是   | 视频播放宽高变化事件回调方法，width表示宽，height表示高。    |

**示例：**

```ts
videoPlayer.on('videoSizeChanged', (width: number, height: number) => {
  console.info('video width is: ' + width);
  console.info('video height is: ' + height);
});
```
### on('audioInterrupt')<sup>(deprecated)</sup>

on(type: 'audioInterrupt', callback: (info: audio.InterruptEvent) => void): void

监听音频焦点变化事件，参考[audio.InterruptEvent](../apis-audio-kit/js-apis-audio.md#interruptevent9)。

> **说明：**
> 从API version 9开始支持，从API version 9开始废弃，建议使用[AVPlayer.on('audioInterrupt')](#onaudiointerrupt9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                     |
| -------- | ------------------------------------------------------------ | ---- | -------------------------------------------------------- |
| type     | string                                                       | 是   | 音频焦点变化事件回调类型，支持的事件：'audioInterrupt'。 |
| callback | function | 是   | 音频焦点变化事件回调方法。                               |

**示例：**

```ts
import audio from '@ohos.multimedia.audio';

videoPlayer.on('audioInterrupt', (info: audio.InterruptEvent) => {
  console.info('audioInterrupt success,and InterruptEvent info is:' + info)
})
```

### on('error')<sup>(deprecated)</sup>

on(type: 'error', callback: ErrorCallback): void

开始监听视频播放错误事件，当上报error错误事件后，用户需处理error事件，退出播放操作。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayer.on('error')](#onerror9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

**参数：**

| 参数名   | 类型          | 必填 | 说明                                                         |
| -------- | ------------- | ---- | ------------------------------------------------------------ |
| type     | string        | 是   | 播放错误事件回调类型，支持的事件包括：'error'。<br>- 'error'：视频播放中发生错误，触发该事件。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback) | 是   | 播放错误事件回调方法。                                       |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

videoPlayer.on('error', (error: BusinessError) => {  // 设置'error'事件回调
  console.error(`video error called, error: ${error}`);
});
videoPlayer.url = 'fd://error';  //设置错误的播放地址，触发'error'事件
```

## VideoPlayState<sup>(deprecated)</sup>

视频播放的状态机，可通过state属性获取当前状态。

> **说明：**
> 从API version 8开始支持，从API version 9开始废弃，建议使用[AVPlayerState](#avplayerstate9)替代。

**系统能力：** SystemCapability.Multimedia.Media.VideoPlayer

| 名称     | 类型   | 说明           |
| -------- | ------ | -------------- |
| idle     | string | 视频播放空闲。 |
| prepared | string | 视频播放准备。 |
| playing  | string | 视频正在播放。 |
| paused   | string | 视频暂停播放。 |
| stopped  | string | 视频播放停止。 |
| error    | string | 错误状态。     |

## AudioRecorder<sup>(deprecated)</sup>

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVRecorder](#avrecorder9)替代。

音频录制管理类，用于录制音频媒体。在调用AudioRecorder的方法前，需要先通过[createAudioRecorder()](#mediacreateaudiorecorderdeprecated) 构建一个AudioRecorder实例。

### prepare<sup>(deprecated)</sup>

prepare(config: AudioRecorderConfig): void

录音准备。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVRecorder.prepare](#prepare9-2)替代。

**需要权限：** ohos.permission.MICROPHONE

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**参数：**

| 参数名 | 类型                                        | 必填 | 说明                                                         |
| ------ | ------------------------------------------- | ---- | ------------------------------------------------------------ |
| config | [AudioRecorderConfig](#audiorecorderconfigdeprecated) | 是   | 配置录音的相关参数，包括音频输出URI、编码格式、采样率、声道数、输出格式等。 |

**示例：**

```ts
let audioRecorderConfig: media.AudioRecorderConfig = {
  audioEncoder : media.AudioEncoder.AAC_LC,
  audioEncodeBitRate : 22050,
  audioSampleRate : 22050,
  numberOfChannels : 2,
  format : media.AudioOutputFormat.AAC_ADTS,
  uri : 'fd://1',       // 文件需先由调用者创建，并给予适当的权限
  location : { latitude : 30, longitude : 130},
}
audioRecorder.on('prepare', () => {    //设置'prepare'事件回调
  console.info('prepare success');
});
audioRecorder.prepare(audioRecorderConfig);
```

### start<sup>(deprecated)</sup>

start(): void

开始录制，需在'prepare'事件成功触发后，才能调用start方法。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVRecorder.start](#start9)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**示例：**

```ts
audioRecorder.on('start', () => {    //设置'start'事件回调
  console.info('audio recorder start success');
});
audioRecorder.start();
```

### pause<sup>(deprecated)</sup>

pause():void

暂停录制，需要在'start'事件成功触发后，才能调用pause方法。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVRecorder.pause](#pause9-2)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**示例：**

```ts
audioRecorder.on('pause', () => {    //设置'pause'事件回调
  console.info('audio recorder pause success');
});
audioRecorder.pause();
```

### resume<sup>(deprecated)</sup>

resume():void

恢复录制，需要在'pause'事件成功触发后，才能调用resume方法。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVRecorder.resume](#resume9)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**示例：**

```ts
audioRecorder.on('resume', () => {    //设置'resume'事件回调
  console.info('audio recorder resume success');
});
audioRecorder.resume();
```

### stop<sup>(deprecated)</sup>

stop(): void

停止录音。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVRecorder.stop](#stop9-2)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**示例：**

```ts
audioRecorder.on('stop', () => {    //设置'stop'事件回调
  console.info('audio recorder stop success');
});
audioRecorder.stop();
```

### release<sup>(deprecated)</sup>

release(): void

释放录音资源。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVRecorder.release](#release9-2)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**示例：**

```ts
audioRecorder.on('release', () => {    //设置'release'事件回调
  console.info('audio recorder release success');
});
audioRecorder.release();
audioRecorder = undefined;
```

### reset<sup>(deprecated)</sup>

reset(): void

重置录音。

进行重置录音之前，需要先调用stop()停止录音。重置录音之后，需要调用prepare()设置录音参数项，才能再次进行录音。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVRecorder.reset](#reset9-2)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**示例：**

```ts
audioRecorder.on('reset', () => {    //设置'reset'事件回调
  console.info('audio recorder reset success');
});
audioRecorder.reset();
```

### on('prepare' | 'start' | 'pause' | 'resume' | 'stop' | 'release' | 'reset')<sup>(deprecated)</sup>

on(type: 'prepare' | 'start' | 'pause' | 'resume' | 'stop' | 'release' | 'reset', callback: () => void): void

开始订阅音频录制事件。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVRecorder.on('stateChange')](#onstatechange9-1)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**参数：**

| 参数名   | 类型     | 必填 | 说明                                                         |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | 是   | 录制事件回调类型，支持的事件包括：'prepare'&nbsp;\|&nbsp;'start'&nbsp;\|  'pause' \| ’resume‘ \|&nbsp;'stop'&nbsp;\|&nbsp;'release'&nbsp;\|&nbsp;'reset'。<br/>-&nbsp;'prepare'&nbsp;：完成prepare调用，音频录制参数设置完成，触发该事件。<br/>-&nbsp;'start'&nbsp;：完成start调用，音频录制开始，触发该事件。<br/>-&nbsp;'pause': 完成pause调用，音频暂停录制，触发该事件。<br/>-&nbsp;'resume': 完成resume调用，音频恢复录制，触发该事件。<br/>-&nbsp;'stop'&nbsp;：完成stop调用，音频停止录制，触发该事件。<br/>-&nbsp;'release'&nbsp;：完成release调用，音频释放录制资源，触发该事件。<br/>-&nbsp;'reset'：完成reset调用，音频重置为初始状态，触发该事件。 |
| callback | ()=>void | 是   | 录制事件回调方法。                                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let audioRecorder: media.AudioRecorder = media.createAudioRecorder();  // 创建一个音频录制实例
let audioRecorderConfig: media.AudioRecorderConfig = {
  audioEncoder : media.AudioEncoder.AAC_LC,
  audioEncodeBitRate : 22050,
  audioSampleRate : 22050,
  numberOfChannels : 2,
  format : media.AudioOutputFormat.AAC_ADTS,
  uri : 'fd://xx',  // 文件需先由调用者创建，并给予适当的权限
  location : { latitude : 30, longitude : 130}
}
audioRecorder.on('error', (error: BusinessError) => {  // 设置'error'事件回调
  console.error(`audio error called, error: ${error}`);
});
audioRecorder.on('prepare', () => {  // 设置'prepare'事件回调
  console.info('prepare success');
  audioRecorder.start();  // 开始录制，并触发'start'事件回调
});
audioRecorder.on('start', () => {  // 设置'start'事件回调
  console.info('audio recorder start success');
});
audioRecorder.on('pause', () => {  // 设置'pause'事件回调
  console.info('audio recorder pause success');
});
audioRecorder.on('resume', () => {  // 设置'resume'事件回调
  console.info('audio recorder resume success');
});
audioRecorder.on('stop', () => {  // 设置'stop'事件回调
  console.info('audio recorder stop success');
});
audioRecorder.on('release', () => {  // 设置'release'事件回调
  console.info('audio recorder release success');
});
audioRecorder.on('reset', () => {  // 设置'reset'事件回调
  console.info('audio recorder reset success');
});
audioRecorder.prepare(audioRecorderConfig)  // 设置录制参数 ，并触发'prepare'事件回调
```

### on('error')<sup>(deprecated)</sup>

on(type: 'error', callback: ErrorCallback): void

开始订阅音频录制错误事件，当上报error错误事件后，用户需处理error事件，退出录制操作。

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVRecorder.on('error')](#onerror9-1)替代。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

**参数：**

| 参数名   | 类型          | 必填 | 说明                                                         |
| -------- | ------------- | ---- | ------------------------------------------------------------ |
| type     | string        | 是   | 录制错误事件回调类型'error'。<br/>-&nbsp;'error'：音频录制过程中发生错误，触发该事件。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback) | 是   | 录制错误事件回调方法。                                       |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let audioRecorderConfig: media.AudioRecorderConfig = {
  audioEncoder : media.AudioEncoder.AAC_LC,
  audioEncodeBitRate : 22050,
  audioSampleRate : 22050,
  numberOfChannels : 2,
  format : media.AudioOutputFormat.AAC_ADTS,
  uri : 'fd://xx',   // 文件需先由调用者创建，并给予适当的权限
  location : { latitude : 30, longitude : 130}
}
audioRecorder.on('error', (error: BusinessError) => {  // 设置'error'事件回调
  console.error(`audio error called, error: ${error}`);
});
audioRecorder.prepare(audioRecorderConfig);  // prepare不设置参数，触发'error'事件
```

## AudioRecorderConfig<sup>(deprecated)</sup>

> **说明：**
> 从API version 6开始支持，从API version 9开始废弃，建议使用[AVRecorderConfig](#avrecorderconfig9)替代。

表示音频的录音配置。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

| 名称                                | 类型                                         | 必填 | 说明                                                         |
| ----------------------------------- | -------------------------------------------- | ---- | ------------------------------------------------------------ |
| audioEncoder                        | [AudioEncoder](#audioencoderdeprecated)                | 否   | 音频编码格式，默认设置为AAC_LC。<br/>**说明：** 从API version 8开始废弃，建议使用audioEncoderMime替代。 |
| audioEncodeBitRate                  | number                                       | 否   | 音频编码比特率，默认值为48000。                              |
| audioSampleRate                     | number                                       | 否   | 音频采集采样率，默认值为48000。                              |
| numberOfChannels                    | number                                       | 否   | 音频采集声道数，默认值为2。                                  |
| format                              | [AudioOutputFormat](#audiooutputformatdeprecated)      | 否   | 音频输出封装格式，默认设置为MPEG_4。<br/>**说明：** 从API version 8开始废弃，建议使用fileFormat替代。 |
| location                            | [Location](#location)                        | 否   | 音频采集的地理位置。                                         |
| uri                                 | string                                       | 是   | 音频输出URI：fd://xx&nbsp;(fd&nbsp;number)<br/>![](figures/zh-cn_image_url.png) <br/>文件需要由调用者创建，并赋予适当的权限。 |
| audioEncoderMime<sup>8+</sup>       | [CodecMimeType](#codecmimetype8)             | 否   | 容器编码格式。                                               |
| fileFormat<sup>8+</sup>             | [ContainerFormatType](#containerformattype8) | 否   | 音频编码格式。                                               |

## AudioEncoder<sup>(deprecated)</sup>

> **说明：**
> 从API version 6开始支持，从API version 8开始废弃，建议使用[CodecMimeType](#codecmimetype8)替代。

表示音频编码格式的枚举。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

| 名称    | 值   | 说明                                                         |
| ------- | ---- | ------------------------------------------------------------ |
| DEFAULT | 0    | 默认编码格式。<br/>仅做接口定义，暂不支持使用。              |
| AMR_NB  | 1    | AMR-NB(Adaptive Multi Rate-Narrow Band Speech Codec) 编码格式。<br/>仅做接口定义，暂不支持使用。 |
| AMR_WB  | 2    | AMR-WB(Adaptive Multi Rate-Wide Band Speech Codec) 编码格式。<br/>仅做接口定义，暂不支持使用。 |
| AAC_LC  | 3    | AAC-LC（Advanced&nbsp;Audio&nbsp;Coding&nbsp;Low&nbsp;Complexity）编码格式。 |
| HE_AAC  | 4    | HE_AAC（High-Efficiency Advanced&nbsp;Audio&nbsp;Coding）编码格式。<br/>仅做接口定义，暂不支持使用。 |

## AudioOutputFormat<sup>(deprecated)</sup>

> **说明：**
> 从API version 6开始支持，从API version 8 开始废弃，建议使用[ContainerFormatType](#containerformattype8)替代。

表示音频封装格式的枚举。

**系统能力：** SystemCapability.Multimedia.Media.AudioRecorder

| 名称     | 值   | 说明                                                         |
| -------- | ---- | ------------------------------------------------------------ |
| DEFAULT  | 0    | 默认封装格式。<br/>仅做接口定义，暂不支持使用。              |
| MPEG_4   | 2    | 封装为MPEG-4格式。                                           |
| AMR_NB   | 3    | 封装为AMR_NB格式。<br/>仅做接口定义，暂不支持使用。          |
| AMR_WB   | 4    | 封装为AMR_WB格式。<br/>仅做接口定义，暂不支持使用。          |
| AAC_ADTS | 6    | 封装为ADTS（Audio&nbsp;Data&nbsp;Transport&nbsp;Stream）格式，是AAC音频的传输流格式。 |
