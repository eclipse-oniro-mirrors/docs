# @ohos.multimedia.media (媒体服务)(系统接口)

媒体子系统为开发者提供一套简单且易于理解的接口，使得开发者能够方便接入系统并使用系统的媒体资源。

媒体子系统包含了音视频相关媒体业务，提供以下常用功能：

- 获取视频缩略图（[AVImageGenerator](#avimagegenerator11)<sup>11+</sup>）

> **说明：**
>
> - 本模块首批接口从API version 6开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> - 当前页面仅包含本模块的系统接口，其他公开接口参见[@ohos.multimedia.media (媒体服务)](js-apis-media.md)。

## 导入模块

```ts
import media from '@ohos.multimedia.media';
```

## media.createAVImageGenerator<sup>11+</sup>

createAVImageGenerator(callback: AsyncCallback\<AVImageGenerator>): void

异步方式创建AVImageGenerator实例，通过注册回调函数获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.AVImageGenerator

**系统接口：** 该接口为系统接口

**参数：**

| 参数名   | 类型                                  | 必填 | 说明                                                         |
| -------- | ------------------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback\<[AVImageGenerator](#avimagegenerator11)> | 是   | 回调函数。异步返回AVImageGenerator实例，失败时返回null。可用于获取视频缩略图。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                       |
| -------- | ------------------------------ |
| 5400101  | No memory. Returned by callback. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let avImageGenerator: media.AVImageGenerator;
media.createAVImageGenerator((error: BusinessError, generator: media.AVImageGenerator) => {
  if (generator != null) {
    avImageGenerator = generator;
    console.info('createAVImageGenerator success');
  } else {
    console.error(`createAVImageGenerator fail, error message:${error.message}`);
  }
});
```

## media.createAVImageGenerator<sup>11+</sup>

createAVImageGenerator(): Promise\<AVImageGenerator>

异步方式创建AVImageGenerator对象，通过Promise获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.AVImageGenerator

**系统接口：** 该接口为系统接口

**返回值：**

| 类型                            | 说明                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| Promise\<[AVImageGenerator](#avimagegenerator11)> | Promise对象。异步返回AVImageGenerator实例，失败时返回null。可用于获取视频缩略图。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                      |
| -------- | ----------------------------- |
| 5400101  | No memory. Returned by promise. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let avImageGenerator: media.AVImageGenerator;
media.createAVImageGenerator().then((generator: media.AVImageGenerator) => {
  if (generator != null) {
    avImageGenerator = generator;
    console.info('createAVImageGenerator success');
  } else {
    console.error('createAVImageGenerator fail');
  }
}).catch((error: BusinessError) => {
  console.error(`AVImageGenerator catchCallback, error message:${error.message}`);
});
```

## media.createVideoRecorder<sup>9+</sup>

createVideoRecorder(callback: AsyncCallback\<VideoRecorder>): void

异步方式创建视频录制实例。通过注册回调函数获取返回值。
一台设备只允许创建一个录制实例。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

**参数：**

| 参数名   | 类型                                            | 必填 | 说明                                                         |
| -------- | ----------------------------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback<[VideoRecorder](#videorecorder9)> | 是   | 回调函数。异步返回VideoRecorder实例，失败时返回null。可用于录制视频媒体。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                       |
| -------- | ------------------------------ |
| 5400101  | No memory. Return by callback. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let videoRecorder: media.VideoRecorder;
media.createVideoRecorder((error: BusinessError, video: media.VideoRecorder) => {
  if (video != null) {
    videoRecorder = video;
    console.info('video createVideoRecorder success');
  } else {
    console.error(`video createVideoRecorder fail, error message:${error.message}`);
  }
});
```

## media.createVideoRecorder<sup>9+</sup>

createVideoRecorder(): Promise\<VideoRecorder>

异步方式创建视频录制实例。通过Promise获取返回值。
一台设备只允许创建一个录制实例。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

**返回值：**

| 类型                                      | 说明                                                         |
| ----------------------------------------- | ------------------------------------------------------------ |
| Promise<[VideoRecorder](#videorecorder9)> | Promise对象。异步返回VideoRecorder实例，失败时返回null。可用于录制视频媒体。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                      |
| -------- | ----------------------------- |
| 5400101  | No memory. Return by promise. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let videoRecorder: media.VideoRecorder;
media.createVideoRecorder().then((video: media.VideoRecorder) => {
  if (video != null) {
    videoRecorder = video;
    console.info('video createVideoRecorder success');
  } else {
    console.error('video createVideoRecorder fail');
  }
}).catch((error: BusinessError) => {
  console.error(`video catchCallback, error message:${error.message}`);
});
```

## AVImageGenerator<sup>11+</sup>

视频缩略图获取类，用于从视频资源中获取缩略图。在调用AVImageGenerator的方法前，需要先通过[createAVImageGenerator()](#mediacreateavimagegenerator11)构建一个AVImageGenerator实例。

获取视频缩略图的demo可参考：[获取视频缩略图开发指导](../../media/media/avimagegenerator.md)。

### 属性

**系统能力：** SystemCapability.Multimedia.Media.AVImageGenerator

**系统接口：** 该接口为系统接口

| 名称                                                | 类型                                                         | 可读 | 可写 | 说明                                                         |
| --------------------------------------------------- | ------------------------------------------------------------ | ---- | ---- | ------------------------------------------------------------ |
| fdSrc<sup>11+</sup>                                  | [AVFileDescriptor](js-apis-media.md#avfiledescriptor9)                       | 是   | 是   | 媒体文件描述，通过该属性设置数据源。<br/> **使用示例**：<br/>假设一个连续存储的媒体文件，地址偏移:0，字节长度:100。其文件描述为 AVFileDescriptor { fd = 资源句柄; offset = 0; length = 100; }。 |

### fetchFrameByTime<sup>11+</sup>

fetchFrameByTime(timeUs: number, options: AVImageQueryOptions, param: PixelMapParams, callback: AsyncCallback\<image.PixelMap>): void

异步方式获取视频缩略图。通过注册回调函数获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.AVImageGenerator

**系统接口：** 该接口为系统接口

**参数：**

| 参数名   | 类型                                         | 必填 | 说明                                |
| -------- | -------------------------------------------- | ---- | ----------------------------------- |
| timeUs | number                   | 是   | 需要获取的缩略图在视频中的时间点，单位为微秒（μs）。 |
| options | [AVImageQueryOptions](#avimagequeryoptions11)     | 是   | 需要获取的缩略图时间点与视频帧的对应关系。 |
| param | [PixelMapParams](#pixelmapparams11)      | 是   | 需要获取的缩略图的格式参数。 |
| callback | AsyncCallback\<[image.PixelMap](../apis-image-kit/js-apis-image.md#pixelmap7)>   | 是   | 回调函数，异步返回视频缩略图对象。 |

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
import image from '@ohos.multimedia.image';

let avImageGenerator: media.AVImageGenerator | undefined = undefined;
let pixel_map : image.PixelMap | undefined = undefined;

// 初始化入参
let timeUs: number = 0

let queryOption: media.AVImageQueryOptions = media.AVImageQueryOptions.AV_IMAGE_QUERY_NEXT_SYNC

let param: media.PixelMapParams = {
  width : 300,
  height : 300,
  colorFormat : media.PixelFormat.RGB_565
}

// 获取缩略图
media.createAVImageGenerator((err: BusinessError, generator: media.AVImageGenerator) => {
  if(generator != null){
    avImageGenerator = generator;
    console.error(`createAVImageGenerator success`);
    avImageGenerator.fetchFrameByTime(timeUs, queryOption, param, (error: BusinessError, pixelMap) => {
      if (error) {
        console.error(`fetchFrameByTime callback failed, err = ${JSON.stringify(error)}`)
        return
      }
      pixel_map = pixelMap;
    });
  } else {
    console.error(`createAVImageGenerator fail, error message:${err.messag-e}`);
  };
});
```

### fetchFrameByTime<sup>11+</sup>

fetchFrameByTime(timeUs: number, options: AVImageQueryOptions, param: PixelMapParams): Promise<image.PixelMap>

异步方式获取视频缩略图。通过Promise获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.AVImageGenerator

**系统接口：** 该接口为系统接口

**参数：**

| 参数名   | 类型                                         | 必填 | 说明                                |
| -------- | -------------------------------------------- | ---- | ----------------------------------- |
| timeUs | number                   | 是   | 需要获取的缩略图在视频中的时间点，单位为微秒（μs）。 |
| options | [AVImageQueryOptions](#avimagequeryoptions11)     | 是   | 需要获取的缩略图时间点与视频帧的对应关系。 |
| param | [PixelMapParams](#pixelmapparams11)      | 是   | 需要获取的缩略图的格式参数。 |

**返回值：**

| 类型           | 说明                                     |
| -------------- | ---------------------------------------- |
| Promise\<[image.PixelMap](../apis-image-kit/js-apis-image.md#pixelmap7)> | Promise对象，异步返回视频缩略图对象。 |

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

let avImageGenerator: media.AVImageGenerator | undefined = undefined;
let pixel_map : image.PixelMap | undefined = undefined;

// 初始化入参
let timeUs: number = 0

let queryOption: media.AVImageQueryOptions = media.AVImageQueryOptions.AV_IMAGE_QUERY_NEXT_SYNC

let param: media.PixelMapParams = {
  width : 300,
  height : 300,
  colorFormat : media.PixelFormat.RGB_565
}

// 获取缩略图
media.createAVImageGenerator((err: BusinessError, generator: media.AVImageGenerator) => {
  if(generator != null){
    avImageGenerator = generator;
    console.error(`createAVImageGenerator success`);
    avImageGenerator.fetchFrameByTime(timeUs, queryOption, param).then((pixelMap: image.PixelMap) => {
      pixel_map = pixelMap;
    }).catch((error: BusinessError) => {
      console.error(`fetchFrameByTime catchCallback, error message:${error.message}`);
    });
  } else {
    console.error(`createAVImageGenerator fail, error message:${err.message}`);
  };
});
```

### release<sup>11+</sup>

release(callback: AsyncCallback\<void>): void

异步方式释放资源。通过注册回调函数获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.AVImageGenerator

**系统接口：** 该接口为系统接口

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

let avImageGenerator: media.AVImageGenerator | undefined = undefined;

//释放资源
media.createAVImageGenerator((err: BusinessError, generator: media.AVImageGenerator) => {
  if(generator != null){
    avImageGenerator = generator;
    console.error(`createAVImageGenerator success`);
    avImageGenerator.release((error: BusinessError) => {
      if (error) {
        console.error(`release failed, err = ${JSON.stringify(error)}`);
        return;
      }
      console.info(`release success.`);
    });
  } else {
    console.error(`createAVImageGenerator fail, error message:${err.message}`);
  };
});
```

### release<sup>11+</sup>

release(): Promise\<void>

异步方式释放资源。通过Promise获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.AVImageGenerator

**系统接口：** 该接口为系统接口

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

let avImageGenerator: media.AVImageGenerator | undefined = undefined;

//释放资源
media.createAVImageGenerator((err: BusinessError, generator: media.AVImageGenerator) => {
  if(generator != null){
    avImageGenerator = generator;
    console.error(`creatAVImageGenerator success`);
    avImageGenerator.release().then(() => {
      console.info(`release success.`);
    }).catch((error: BusinessError) => {
      console.error(`release catchCallback, error message:${error.message}`);
    });
  } else {
    console.error(`creatAVImageGenerator fail, error message:${err.message}`);
  };
});
```

## AVImageQueryOptions<sup>11+</sup>

需要获取的缩略图时间点与视频帧的对应关系。

在获取视频缩略图时，传入的时间点与实际取得的视频帧所在时间点不一定相等，需要指定传入的时间点与实际取得的视频帧的时间关系。

**系统能力：** SystemCapability.Multimedia.Media.AVImageGenerator

**系统接口：** 该接口为系统接口

| 名称                     | 值              | 说明                                                         |
| ------------------------ | --------------- | ------------------------------------------------------------ |
| AV_IMAGE_QUERY_NEXT_SYNC       | 0   | 表示选取传入时间点或之后的关键帧。                       |
| AV_IMAGE_QUERY_PREVIOUS_SYNC        | 1    | 表示选取传入时间点或之前的关键帧。 |
| AV_IMAGE_QUERY_CLOSEST_SYNC        | 2    | 表示选取离传入时间点最近的关键帧。                 |
| AV_IMAGE_QUERY_CLOSEST          | 3      | 表示选取离传入时间点最近的帧，该帧不一定是关键帧。     |

## PixelMapParams<sup>11+</sup>

获取视频缩略图时，输出缩略图的格式参数。

**系统能力：** SystemCapability.Multimedia.Media.AVImageGenerator

**系统接口：** 该接口为系统接口

| 名称     | 类型   |  可读   |   可写    |  说明                   |
| -------- | ------ |   ------| ------ | ---------------------- |
| width     | number |  是   |  是   |  输出的缩略图宽度。         |
| height | number |  是   |  是   | 输出的缩略图高度。 |
| colorFormat  | [PixelFormat](#pixelformat11) |  是   |  是   | 输出的缩略图颜色格式。         |

## PixelFormat<sup>11+</sup>

获取视频缩略图时，输出的缩略图采用的颜色格式枚举。

**系统能力：** SystemCapability.Multimedia.Media.AVImageGenerator

**系统接口：** 该接口为系统接口

| 名称                     | 值              | 说明                                                         |
| ------------------------ | --------------- | ------------------------------------------------------------ |
| RGB_565       | 2   | 表示RGB_565颜色格式。                       |
| RGBA_8888        | 3    | 表示RGBA_8888颜色格式。 |
| RGB_888        | 5    | 表示RGB_888颜色格式。                 |

## VideoRecorder<sup>9+</sup>

> **说明：**
> AVRecorder<sup>9+</sup>发布后，VideoRecorder停止维护，建议使用[AVRecorder](js-apis-media.md#avrecorder9)替代。

视频录制管理类，用于录制视频媒体。在调用VideoRecorder的方法前，需要先通过[createVideoRecorder()](#mediacreatevideorecorder9)构建一个[VideoRecorder](#videorecorder9)实例。

### 属性

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

| 名称               | 类型                                   | 可读 | 可写 | 说明             |
| ------------------ | -------------------------------------- | ---- | ---- | ---------------- |
| state<sup>9+</sup> | [VideoRecordState](#videorecordstate9) | 是   | 否   | 视频录制的状态。 |

### prepare<sup>9+</sup>

prepare(config: VideoRecorderConfig, callback: AsyncCallback\<void>): void

异步方式进行视频录制的参数设置。通过注册回调函数获取返回值。

**需要权限：** ohos.permission.MICROPHONE

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

**参数：**

| 参数名   | 类型                                         | 必填 | 说明                                |
| -------- | -------------------------------------------- | ---- | ----------------------------------- |
| config   | [VideoRecorderConfig](#videorecorderconfig9) | 是   | 配置视频录制的相关参数。            |
| callback | AsyncCallback\<void>                         | 是   | 异步视频录制prepare方法的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 201      | Permission denied. Return by callback.     |
| 401      | Parameter error. Return by callback.       |
| 5400102  | Operation not allowed. Return by callback. |
| 5400105  | Service died. Return by callback.          |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

// 配置参数以实际硬件设备支持的范围为准
let videoProfile: media.VideoRecorderProfile = {
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

let videoConfig: media.VideoRecorderConfig = {
  audioSourceType : media.AudioSourceType.AUDIO_SOURCE_TYPE_MIC,
  videoSourceType : media.VideoSourceType.VIDEO_SOURCE_TYPE_SURFACE_YUV,
  profile : videoProfile,
  url : 'fd://xx', // 文件需先由调用者创建，并给予适当的权限
  rotation : 0,
  location : { latitude : 30, longitude : 130 }
}

// asyncallback
videoRecorder.prepare(videoConfig, (err: BusinessError) => {
  if (err == null) {
    console.info('prepare success');
  } else {
    console.error('prepare failed and error is ' + err.message);
  }
})
```

### prepare<sup>9+</sup>

prepare(config: VideoRecorderConfig): Promise\<void>

异步方式进行视频录制的参数设置。通过Promise获取返回值。

**需要权限：** ohos.permission.MICROPHONE

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

**参数：**

| 参数名 | 类型                                         | 必填 | 说明                     |
| ------ | -------------------------------------------- | ---- | ------------------------ |
| config | [VideoRecorderConfig](#videorecorderconfig9) | 是   | 配置视频录制的相关参数。 |

**返回值：**

| 类型           | 说明                                     |
| -------------- | ---------------------------------------- |
| Promise\<void> | 异步视频录制prepare方法的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                  |
| -------- | ----------------------------------------- |
| 201      | Permission denied. Return by promise.     |
| 401      | Parameter error. Return by promise.       |
| 5400102  | Operation not allowed. Return by promise. |
| 5400105  | Service died. Return by promise.          |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

// 配置参数以实际硬件设备支持的范围为准
let videoProfile: media.VideoRecorderProfile = {
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

let videoConfig: media.VideoRecorderConfig = {
  audioSourceType : media.AudioSourceType.AUDIO_SOURCE_TYPE_MIC,
  videoSourceType : media.VideoSourceType.VIDEO_SOURCE_TYPE_SURFACE_YUV,
  profile : videoProfile,
  url : 'fd://xx', // 文件需先由调用者创建，并给予适当的权限
  rotation : 0,
  location : { latitude : 30, longitude : 130 }
}

// promise
videoRecorder.prepare(videoConfig).then(() => {
  console.info('prepare success');
}).catch((err: BusinessError) => {
  console.error('prepare failed and catch error is ' + err.message);
});
```

### getInputSurface<sup>9+</sup>

getInputSurface(callback: AsyncCallback\<string>): void

异步方式获得录制需要的surface。通过注册回调函数获取返回值。此surface提供给调用者，调用者从此surface中获取surfaceBuffer，填入相应的数据。

应当注意，填入的视频数据需要携带时间戳（单位ns），buffersize。时间戳的起始时间请以系统启动时间为基准。

只能在[prepare()](#prepare9)接口调用后调用。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

**参数：**

| 参数名   | 类型                   | 必填 | 说明                        |
| -------- | ---------------------- | ---- | --------------------------- |
| callback | AsyncCallback\<string> | 是   | 异步获得surface的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400102  | Operation not allowed. Return by callback. |
| 5400103  | I/O error. Return by callback.             |
| 5400105  | Service died. Return by callback.          |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

// asyncallback
let surfaceID: string; // 传递给外界的surfaceID
videoRecorder.getInputSurface((err: BusinessError, surfaceId: string) => {
  if (err == null) {
    console.info('getInputSurface success');
    surfaceID = surfaceId;
  } else {
    console.error('getInputSurface failed and error is ' + err.message);
  }
});
```

### getInputSurface<sup>9+</sup>

getInputSurface(): Promise\<string>;

 异步方式获得录制需要的surface。通过Promise获取返回值。此surface提供给调用者，调用者从此surface中获取surfaceBuffer，填入相应的数据。

应当注意，填入的视频数据需要携带时间戳（单位ns），buffersize。时间戳的起始时间请以系统启动时间为基准。

只能在[prepare()](#prepare9-1)接口调用后调用。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

**返回值：**

| 类型             | 说明                             |
| ---------------- | -------------------------------- |
| Promise\<string> | 异步获得surface的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                  |
| -------- | ----------------------------------------- |
| 5400102  | Operation not allowed. Return by promise. |
| 5400103  | I/O error. Return by promise.             |
| 5400105  | Service died. Return by promise.          |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

// promise
let surfaceID: string; // 传递给外界的surfaceID
videoRecorder.getInputSurface().then((surfaceId: string) => {
  console.info('getInputSurface success');
  surfaceID = surfaceId;
}).catch((err: BusinessError) => {
  console.error('getInputSurface failed and catch error is ' + err.message);
});
```

### start<sup>9+</sup>

start(callback: AsyncCallback\<void>): void

异步方式开始视频录制。通过注册回调函数获取返回值。

在[prepare()](#prepare9)和[getInputSurface()](#getinputsurface9)后调用，需要依赖数据源先给surface传递数据。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

**参数：**

| 参数名   | 类型                 | 必填 | 说明                         |
| -------- | -------------------- | ---- | ---------------------------- |
| callback | AsyncCallback\<void> | 是   | 异步开始视频录制的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400102  | Operation not allowed. Return by callback. |
| 5400103  | I/O error. Return by callback.             |
| 5400105  | Service died. Return by callback.          |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

// asyncallback
videoRecorder.start((err: BusinessError) => {
  if (err == null) {
    console.info('start videorecorder success');
  } else {
    console.error('start videorecorder failed and error is ' + err.message);
  }
});
```

### start<sup>9+</sup>

start(): Promise\<void>

异步方式开始视频录制。通过Promise获取返回值。

在[prepare()](#prepare9-1)和[getInputSurface()](#getinputsurface9-1)后调用，需要依赖数据源先给surface传递数据。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

**返回值：**

| 类型           | 说明                                  |
| -------------- | ------------------------------------- |
| Promise\<void> | 异步开始视频录制方法的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                  |
| -------- | ----------------------------------------- |
| 5400102  | Operation not allowed. Return by promise. |
| 5400103  | I/O error. Return by promise.             |
| 5400105  | Service died. Return by promise.          |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

// promise
videoRecorder.start().then(() => {
  console.info('start videorecorder success');
}).catch((err: BusinessError) => {
  console.error('start videorecorder failed and catch error is ' + err.message);
});
```

### pause<sup>9+</sup>

pause(callback: AsyncCallback\<void>): void

异步方式暂停视频录制。通过注册回调函数获取返回值。

在[start()](#start9)后调用。可以通过调用[resume()](#resume9)接口来恢复录制。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

**参数：**

| 参数名   | 类型                 | 必填 | 说明                         |
| -------- | -------------------- | ---- | ---------------------------- |
| callback | AsyncCallback\<void> | 是   | 异步暂停视频录制的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400102  | Operation not allowed. Return by callback. |
| 5400103  | I/O error. Return by callback.             |
| 5400105  | Service died. Return by callback.          |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

// asyncallback
videoRecorder.pause((err: BusinessError) => {
  if (err == null) {
    console.info('pause videorecorder success');
  } else {
    console.error('pause videorecorder failed and error is ' + err.message);
  }
});
```

### pause<sup>9+</sup>

pause(): Promise\<void>

异步方式暂停视频录制。通过Promise获取返回值。

在[start()](#start9-1)后调用。可以通过调用[resume()](#resume9-1)接口来恢复录制。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

**返回值：**

| 类型           | 说明                                  |
| -------------- | ------------------------------------- |
| Promise\<void> | 异步暂停视频录制方法的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                  |
| -------- | ----------------------------------------- |
| 5400102  | Operation not allowed. Return by promise. |
| 5400103  | I/O error. Return by promise.             |
| 5400105  | Service died. Return by promise.          |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

// promise
videoRecorder.pause().then(() => {
  console.info('pause videorecorder success');
}).catch((err: BusinessError) => {
  console.error('pause videorecorder failed and catch error is ' + err.message);
});
```

### resume<sup>9+</sup>

resume(callback: AsyncCallback\<void>): void

异步方式恢复视频录制。通过注册回调函数获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

**参数：**

| 参数名   | 类型                 | 必填 | 说明                         |
| -------- | -------------------- | ---- | ---------------------------- |
| callback | AsyncCallback\<void> | 是   | 异步恢复视频录制的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400102  | Operation not allowed. Return by callback. |
| 5400103  | I/O error. Return by callback.             |
| 5400105  | Service died. Return by callback.          |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

// asyncallback
videoRecorder.resume((err: BusinessError) => {
  if (err == null) {
    console.info('resume videorecorder success');
  } else {
    console.error('resume videorecorder failed and error is ' + err.message);
  }
});
```

### resume<sup>9+</sup>

resume(): Promise\<void>

异步方式恢复视频录制。通过Promise获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

**返回值：**

| 类型           | 说明                                  |
| -------------- | ------------------------------------- |
| Promise\<void> | 异步恢复视频录制方法的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                  |
| -------- | ----------------------------------------- |
| 5400102  | Operation not allowed. Return by promise. |
| 5400103  | I/O error. Return by promise.             |
| 5400105  | Service died. Return by promise.          |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

// promise
videoRecorder.resume().then(() => {
  console.info('resume videorecorder success');
}).catch((err: BusinessError) => {
  console.error('resume videorecorder failed and catch error is ' + err.message);
});
```

### stop<sup>9+</sup>

stop(callback: AsyncCallback\<void>): void

异步方式停止视频录制。通过注册回调函数获取返回值。

需要重新调用[prepare()](#prepare9)和[getInputSurface()](#getinputsurface9)接口才能重新录制。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

**参数：**

| 参数名   | 类型                 | 必填 | 说明                         |
| -------- | -------------------- | ---- | ---------------------------- |
| callback | AsyncCallback\<void> | 是   | 异步停止视频录制的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                   |
| -------- | ------------------------------------------ |
| 5400102  | Operation not allowed. Return by callback. |
| 5400103  | I/O error. Return by callback.             |
| 5400105  | Service died. Return by callback.          |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

// asyncallback
videoRecorder.stop((err: BusinessError) => {
  if (err == null) {
    console.info('stop videorecorder success');
  } else {
    console.error('stop videorecorder failed and error is ' + err.message);
  }
});
```

### stop<sup>9+</sup>

stop(): Promise\<void>

异步方式停止视频录制。通过Promise获取返回值。

需要重新调用[prepare()](#prepare9-1)和[getInputSurface()](#getinputsurface9-1)接口才能重新录制。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

**返回值：**

| 类型           | 说明                                  |
| -------------- | ------------------------------------- |
| Promise\<void> | 异步停止视频录制方法的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                                  |
| -------- | ----------------------------------------- |
| 5400102  | Operation not allowed. Return by promise. |
| 5400103  | I/O error. Return by promise.             |
| 5400105  | Service died. Return by promise.          |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

// promise
videoRecorder.stop().then(() => {
  console.info('stop videorecorder success');
}).catch((err: BusinessError) => {
  console.error('stop videorecorder failed and catch error is ' + err.message);
});
```

### release<sup>9+</sup>

release(callback: AsyncCallback\<void>): void

异步方式释放视频录制资源。通过注册回调函数获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

**参数：**

| 参数名   | 类型                 | 必填 | 说明                             |
| -------- | -------------------- | ---- | -------------------------------- |
| callback | AsyncCallback\<void> | 是   | 异步释放视频录制资源的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                          |
| -------- | --------------------------------- |
| 5400105  | Service died. Return by callback. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

// asyncallback
videoRecorder.release((err: BusinessError) => {
  if (err == null) {
    console.info('release videorecorder success');
  } else {
    console.error('release videorecorder failed and error is ' + err.message);
  }
});
```

### release<sup>9+</sup>

release(): Promise\<void>

异步方式释放视频录制资源。通过Promise获取返回值。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

**返回值：**

| 类型           | 说明                                      |
| -------------- | ----------------------------------------- |
| Promise\<void> | 异步释放视频录制资源方法的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                          |
| -------- | --------------------------------- |
| 5400105  | Service died. Return by callback. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

// promise
videoRecorder.release().then(() => {
  console.info('release videorecorder success');
}).catch((err: BusinessError) => {
  console.error('release videorecorder failed and catch error is ' + err.message);
});
```

### reset<sup>9+</sup>

reset(callback: AsyncCallback\<void>): void

异步方式重置视频录制。通过注册回调函数获取返回值。

需要重新调用[prepare()](#prepare9)和[getInputSurface()](#getinputsurface9)接口才能重新录制。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

**参数：**

| 参数名   | 类型                 | 必填 | 说明                         |
| -------- | -------------------- | ---- | ---------------------------- |
| callback | AsyncCallback\<void> | 是   | 异步重置视频录制的回调方法。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                          |
| -------- | --------------------------------- |
| 5400103  | I/O error. Return by callback.    |
| 5400105  | Service died. Return by callback. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

// asyncallback
videoRecorder.reset((err: BusinessError) => {
  if (err == null) {
    console.info('reset videorecorder success');
  } else {
    console.error('reset videorecorder failed and error is ' + err.message);
  }
});
```

### reset<sup>9+</sup>

reset(): Promise\<void>

异步方式重置视频录制。通过Promise获取返回值。

需要重新调用[prepare()](#prepare9-1)和[getInputSurface()](#getinputsurface9-1)接口才能重新录制。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

**返回值：**

| 类型           | 说明                                  |
| -------------- | ------------------------------------- |
| Promise\<void> | 异步重置视频录制方法的Promise返回值。 |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                         |
| -------- | -------------------------------- |
| 5400103  | I/O error. Return by promise.    |
| 5400105  | Service died. Return by promise. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

// promise
videoRecorder.reset().then(() => {
  console.info('reset videorecorder success');
}).catch((err: BusinessError) => {
  console.error('reset videorecorder failed and catch error is ' + err.message);
});
```

### on('error')<sup>9+</sup>

on(type: 'error', callback: ErrorCallback): void

开始订阅视频录制错误事件，当上报error错误事件后，用户需处理error事件，退出录制操作。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

**参数：**

| 参数名   | 类型          | 必填 | 说明                                                         |
| -------- | ------------- | ---- | ------------------------------------------------------------ |
| type     | string        | 是   | 录制错误事件回调类型'error'。<br/>-&nbsp;'error'：视频录制过程中发生错误，触发该事件。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback) | 是   | 录制错误事件回调方法。                                       |

**错误码：**

以下错误码的详细介绍请参见[媒体错误码](errorcode-media.md)

| 错误码ID | 错误信息                          |
| -------- | --------------------------------- |
| 5400103  | I/O error. Return by callback.    |
| 5400105  | Service died. Return by callback. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

// 当获取videoRecordState接口出错时通过此订阅事件上报
videoRecorder.on('error', (error: BusinessError) => { // 设置'error'事件回调
  console.error(`audio error called, error: ${error}`);
})
```

## VideoRecordState<sup>9+</sup>

视频录制的状态机。可通过state属性获取当前状态。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

| 名称     | 类型   | 说明                   |
| -------- | ------ | ---------------------- |
| idle     | string | 视频录制空闲。         |
| prepared | string | 视频录制参数设置完成。 |
| playing  | string | 视频正在录制。         |
| paused   | string | 视频暂停录制。         |
| stopped  | string | 视频录制停止。         |
| error    | string | 错误状态。             |

## VideoRecorderConfig<sup>9+</sup>

表示视频录制的参数设置。

通过audioSourceType和videoSourceType区分纯视频录制和音视频录制（纯音频录制请使用[AVRecorder](js-apis-media.md#avrecorder9)或[AudioRecorder](js-apis-media.md#audiorecorderdeprecated)）。纯视频录制时，仅需要设置videoSourceType；音视频录制时，audioSourceType和videoSourceType均需要设置。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

| 名称            | 类型                                           | 必填 | 说明                                                         |
| --------------- | ---------------------------------------------- | ---- | ------------------------------------------------------------ |
| audioSourceType | [AudioSourceType](js-apis-media.md#audiosourcetype9)           | 否   | 视频录制的音频源类型，选择音频录制时必填。                      |
| videoSourceType | [VideoSourceType](js-apis-media.md#videosourcetype9)           | 是   | 视频录制的视频源类型。                                       |
| profile         | [VideoRecorderProfile](#videorecorderprofile9) | 是   | 视频录制的profile。                                          |
| rotation        | number                                         | 否   | 录制的视频旋转角度，仅支持0，90，180，270，默认值为0。       |
| location        | [Location](js-apis-media.md#location)                          | 否   | 录制视频的地理位置，默认不记录地理位置信息。                 |
| url             | string                                         | 是   | 视频输出URL：fd://xx&nbsp;(fd&nbsp;number)<br/>![](figures/zh-cn_image_url.png) |

## VideoRecorderProfile<sup>9+</sup>

视频录制的配置文件。

**系统能力：** SystemCapability.Multimedia.Media.VideoRecorder

**系统接口：** 该接口为系统接口

| 名称             | 类型                                         | 必填 | 说明             |
| ---------------- | -------------------------------------------- | ---- | ---------------- |
| audioBitrate     | number                                       | 否   | 音频编码比特率，选择音频录制时必填。 |
| audioChannels    | number                                       | 否   | 音频采集声道数，选择音频录制时必填。 |
| audioCodec       | [CodecMimeType](js-apis-media.md#codecmimetype8)             | 否   | 音频编码格式，选择音频录制时必填。   |
| audioSampleRate  | number                                       | 否   | 音频采样率，选择音频录制时必填。     |
| fileFormat       | [ContainerFormatType](js-apis-media.md#containerformattype8) | 是   | 文件的容器格式。 |
| videoBitrate     | number                                       | 是   | 视频编码比特率。 |
| videoCodec       | [CodecMimeType](js-apis-media.md#codecmimetype8)             | 是   | 视频编码格式。   |
| videoFrameWidth  | number                                       | 是   | 录制视频帧的宽。 |
| videoFrameHeight | number                                       | 是   | 录制视频帧的高。 |
| videoFrameRate   | number                                       | 是   | 录制视频帧率。   |
