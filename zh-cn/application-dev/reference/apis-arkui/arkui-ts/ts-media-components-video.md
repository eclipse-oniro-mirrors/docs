# Video

用于播放视频文件并控制其播放状态的组件。 

>  **说明：**
>
>  该组件从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。<br/>
>  Video组件只提供简单的视频播放功能，无法支撑复杂的视频播控场景。复杂开发场景推荐使用[AVPlayer播控API](../../apis-media-kit/js-apis-media.md#avplayer9)和[XComponent](ts-basic-components-xcomponent.md)组件开发。

## 权限列表

使用网络视频时，需要申请权限ohos.permission.INTERNET。具体申请方式请参考[声明权限](../../../security/AccessToken/declare-permissions.md)。


## 子组件

不支持子组件。


## 接口

### Video

Video(value: VideoOptions)

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | [VideoOptions](#videooptions对象说明) | 是 | 视频信息。 |

##  VideoOptions对象说明

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称              | 类型                                                     | 必填 | 说明                                                     |
| ------------------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| src                 | string \| [Resource](ts-types.md#resource)                            | 否   | 视频的数据源，支持本地视频和网络视频。<br>Resource格式可以跨包/跨模块访问资源文件，常用于访问本地视频。<br/>- 支持rawfile文件下的资源，即通过$rawfile引用视频文件。<br/>string格式可用于加载网络视频和本地视频，常用于加载网络视频。<br/>- 支持网络视频地址。<br/>- 支持file://路径前缀的字符串，即[应用沙箱URI](../../apis-core-file-kit/js-apis-file-fileuri.md#constructor10)：file://\<bundleName>/\<sandboxPath>。用于读取应用沙箱路径内的资源。需要保证目录包路径下的文件有可读权限。<br/>**说明：**<br/>视频支持的格式是：mp4、mkv、TS。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| currentProgressRate | number&nbsp;\|&nbsp;string&nbsp;\|&nbsp;[PlaybackSpeed<sup>8+</sup>](#playbackspeed8枚举说明) | 否   | 视频播放倍速。<br/>**说明：**<br/>number取值仅支持：0.75，1.0，1.25，1.75，2.0。<br/>默认值：1.0 \| PlaybackSpeed.Speed_Forward_1_00_X<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| previewUri          | string&nbsp;\| [PixelMap](../../apis-image-kit/js-apis-image.md#pixelmap7)&nbsp;\|&nbsp;[Resource](ts-types.md)  | 否   | 视频未播放时的预览图片路径，默认不显示图片。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。                 |
| controller          | [VideoController](#videocontroller)                          | 否   | 设置视频控制器，可以控制视频的播放状态。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。                     |
| imageAIOptions<sup>12+</sup>  | [ImageAIOptions](ts-image-common.md#imageaioptions) | 否   | 设置图像AI分析选项，可配置分析类型或绑定一个分析控制器。<br/>**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。 |

## PlaybackSpeed<sup>8+</sup>枚举说明

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称                 | 说明           |
| -------------------- | -------------- |
| Speed_Forward_0_75_X | 0.75倍速播放。 |
| Speed_Forward_1_00_X | 1倍速播放。    |
| Speed_Forward_1_25_X | 1.25倍速播放。 |
| Speed_Forward_1_75_X | 1.75倍速播放。 |
| Speed_Forward_2_00_X | 2倍速播放。    |

## 属性

除支持[通用属性](ts-universal-attributes-size.md)外，还支持以下属性：

### muted

muted(value: boolean)

设置是否静音。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                         |
| ------ | ------- | ---- | ---------------------------- |
| value  | boolean | 是   | 是否静音。<br/>默认值：false |

### autoPlay

autoPlay(value: boolean)

设置是否自动播放。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                             |
| ------ | ------- | ---- | -------------------------------- |
| value  | boolean | 是   | 是否自动播放。<br/>默认值：false |

### controls

controls(value: boolean)

设置控制视频播放的控制栏是否显示。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                                            |
| ------ | ------- | ---- | ----------------------------------------------- |
| value  | boolean | 是   | 控制视频播放的控制栏是否显示。<br/>默认值：true |

### objectFit

objectFit(value: ImageFit)

设置视频显示模式。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型                                      | 必填 | 说明                             |
| ------ | ----------------------------------------- | ---- | -------------------------------- |
| value  | [ImageFit](ts-appendix-enums.md#imagefit) | 是   | 视频显示模式。<br/>默认值：Cover |

### loop

loop(value: boolean)

设置是否单个视频循环播放。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型    | 必填 | 说明                                     |
| ------ | ------- | ---- | ---------------------------------------- |
| value  | boolean | 是   | 是否单个视频循环播放。<br/>默认值：false |

### enableAnalyzer<sup>12+</sup>

enableAnalyzer(enable: boolean)

设置组件支持AI分析，当前支持主体识别、文字识别和对象查找等功能。
使能后，视频播放暂停时自动进入分析状态，开始分析当前画面帧，视频继续播放后自动退出分析状态。
不能和[overlay](ts-universal-attributes-overlay.md)属性同时使用，两者同时设置时[overlay](ts-universal-attributes-overlay.md)中[CustomBuilder](ts-types.md#custombuilder8)属性将失效。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| enable | boolean | 是 | 是否启用AI分析功能 |

> **说明：**
>
> 当前仅在使用自定义控制栏([controls](#controls)属性设置为false)时支持该功能。
> 该特性依赖设备能力。

### analyzerConfig<sup>12+</sup>

analyzerConfig(config: ImageAnalyzerConfig)

设置AI分析识别类型，包括主体识别、文字识别和对象查找等功能。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| config | [ImageAnalyzerConfig](ts-image-common.md#imageanalyzerconfig) | 是 | 设置AI分析识别类型 |

## 事件

除支持[通用事件](ts-universal-events-click.md)外，还支持以下事件：

### onStart

onStart(event: () => void)

播放时触发该事件。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### onPause

onPause(event: () => void)

暂停时触发该事件。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### onFinish

onFinish(event: () => void)

播放结束时触发该事件。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### onError

onError(event: () => void)

播放失败时触发该事件。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### onStop<sup>12+</sup>

onStop(event: Callback&lt;void&gt;)

播放停止时触发该事件(当stop()方法被调用后触发)。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### onPrepared

onPrepared(callback: (event: { duration: number }) => void)

视频准备完成时触发该事件。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名   | 类型   | 必填 | 说明                       |
| -------- | ------ | ---- | -------------------------- |
| duration | number | 是   | 当前视频的时长，单位为秒。 |

### onSeeking

onSeeking(callback: (event: { time: number }) => void)

操作进度条过程时上报时间信息。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明                           |
| ------ | ------ | ---- | ------------------------------ |
| time   | number | 是   | 当前视频播放的进度，单位为秒。 |

### onSeeked

onSeeked(callback: (event: { time: number }) => void)

操作进度条完成后，上报播放时间信息。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明                           |
| ------ | ------ | ---- | ------------------------------ |
| time   | number | 是   | 当前视频播放的进度，单位为秒。 |

### onUpdate

onUpdate(callback: (event: { time: number }) => void)

播放进度变化时触发该事件。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名 | 类型   | 必填 | 说明                           |
| ------ | ------ | ---- | ------------------------------ |
| time   | number | 是   | 当前视频播放的进度，单位为秒。 |

### onFullscreenChange

onFullscreenChange(callback: (event: { fullscreen: boolean }) => void)

在全屏播放与非全屏播放状态之间切换时触发该事件。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名     | 类型    | 必填 | 说明                                                  |
| ---------- | ------- | ---- | ----------------------------------------------------- |
| fullscreen | boolean | 是   | 为true表示进入全屏播放状态，为false则表示非全屏播放。 |

## VideoController

一个VideoController对象可以控制一个或多个video，可用视频播放实例请参考[@ohos.multimedia.media](../../apis-media-kit/js-apis-media.md)。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### 导入对象

```ts
let controller: VideoController = new VideoController()
```

### constructor

constructor()

VideoController的构造函数。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### start

start()

开始播放。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### pause

pause()

暂停播放，显示当前帧，再次播放时从当前位置继续播放。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### stop

stop()

停止播放，显示当前帧，再次播放时从头开始播放。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### reset<sup>12+</sup>

reset(): void

video组件重置AVPlayer。显示当前帧，再次播放时从头开始播放。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### setCurrentTime

setCurrentTime(value: number)

指定视频播放的进度位置。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名   | 类型   | 必填   | 说明           |
| ----- | ------ | ---- | -------------- |
| value | number | 是    | 视频播放进度位置，单位为s。 |

### requestFullscreen

requestFullscreen(value: boolean)

请求全屏播放。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名 | 类型 | 必填 | 说明                         |
| ------ | -------- | ---- | -------------------------------- |
| value  | boolean  | 是   | 是否全屏（填充满应用窗口）播放。 |

### exitFullscreen

exitFullscreen()

退出全屏播放。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

### setCurrentTime<sup>8+</sup>

setCurrentTime(value: number, seekMode: SeekMode)

指定视频播放的进度位置，并指定跳转模式。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**参数：**

| 参数名      | 类型     | 必填   | 说明           |
| -------- | -------- | ---- | -------------- |
| value    | number   | 是    | 视频播放进度位置，单位为s。 |
| seekMode | [SeekMode](#seekmode8枚举说明) | 是    | 跳转模式。          |

## SeekMode<sup>8+</sup>枚举说明

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称             | 说明                         |
| ---------------- | ---------------------------- |
| PreviousKeyframe | 跳转到前一个最近的关键帧。   |
| NextKeyframe     | 跳转到后一个最近的关键帧。   |
| ClosestKeyframe  | 跳转到最近的关键帧。         |
| Accurate         | 精准跳转，不论是否为关键帧。 |

## 示例

### 示例1（视频播放基础用法）

基础用法，包括控制栏、预览图、自动播放、播放速度、控制器（开始播放、暂停播放、停止播放、重置avPlayer、跳转等）以及一些状态回调方法。

```ts
// xxx.ets
@Entry
@Component
struct VideoCreateComponent {
  @State videoSrc: Resource = $rawfile('video1.mp4')
  @State previewUri: Resource = $r('app.media.poster1')
  @State curRate: PlaybackSpeed = PlaybackSpeed.Speed_Forward_1_00_X
  @State isAutoPlay: boolean = false
  @State showControls: boolean = true
  controller: VideoController = new VideoController()

  build() {
    Column() {
      Video({
        src: this.videoSrc,
        previewUri: this.previewUri,
        currentProgressRate: this.curRate,
        controller: this.controller
      })
        .width('100%')
        .height(600)
        .autoPlay(this.isAutoPlay)
        .controls(this.showControls)
        .onStart(() => {
          console.info('onStart')
        })
        .onPause(() => {
          console.info('onPause')
        })
        .onFinish(() => {
          console.info('onFinish')
        })
        .onError(() => {
          console.info('onError')
        })
        .onStop(() => {
          console.info('onStop')
        })
        .onPrepared((e?: DurationObject) => {
          if (e != undefined) {
            console.info('onPrepared is ' + e.duration)
          }
        })
        .onSeeking((e?: TimeObject) => {
          if (e != undefined) {
            console.info('onSeeking is ' + e.time)
          }
        })
        .onSeeked((e?: TimeObject) => {
          if (e != undefined) {
            console.info('onSeeked is ' + e.time)
          }
        })
        .onUpdate((e?: TimeObject) => {
          if (e != undefined) {
            console.info('onUpdate is ' + e.time)
          }
        })
        .onFullscreenChange((e?: FullscreenObject) => {
          if (e != undefined) {
            console.info('onFullscreenChange is ' + e.fullscreen)
          }
        })

      Row() {
        Button('src').onClick(() => {
          this.videoSrc = $rawfile('video2.mp4') // 切换视频源
        }).margin(5)
        Button('previewUri').onClick(() => {
          this.previewUri = $r('app.media.poster2') // 切换视频预览海报
        }).margin(5)
        Button('controls').onClick(() => {
          this.showControls = !this.showControls // 切换是否显示视频控制栏
        }).margin(5)
      }

      Row() {
        Button('start').onClick(() => {
          this.controller.start() // 开始播放
        }).margin(2)
        Button('pause').onClick(() => {
          this.controller.pause() // 暂停播放
        }).margin(2)
        Button('stop').onClick(() => {
          this.controller.stop() // 结束播放
        }).margin(2)
        Button('reset').onClick(() => {
          this.controller.reset() // 重置AVPlayer
        }).margin(2)
        Button('setTime').onClick(() => {
          this.controller.setCurrentTime(10, SeekMode.Accurate) // 精准跳转到视频的10s位置
        }).margin(2)
      }

      Row() {
        Button('rate 0.75').onClick(() => {
          this.curRate = PlaybackSpeed.Speed_Forward_0_75_X // 0.75倍速播放
        }).margin(5)
        Button('rate 1').onClick(() => {
          this.curRate = PlaybackSpeed.Speed_Forward_1_00_X // 原倍速播放
        }).margin(5)
        Button('rate 2').onClick(() => {
          this.curRate = PlaybackSpeed.Speed_Forward_2_00_X // 2倍速播放
        }).margin(5)
      }
    }
  }
}

interface DurationObject {
  duration: number;
}

interface TimeObject {
  time: number;
}

interface FullscreenObject {
  fullscreen: boolean;
}
```

### 示例2（图像分析功能）

使用enableAnalyzer属性开启图像AI分析。

```ts
// xxx.ets
@Entry
@Component
struct ImageAnalyzerExample {
  @State videoSrc: Resource = $rawfile('video1.mp4')
  @State previewUri: Resource = $r('app.media.poster1')
  @State showControls: boolean = true
  controller: VideoController = new VideoController()
  config: ImageAnalyzerConfig = {
    types: [ImageAnalyzerType.SUBJECT, ImageAnalyzerType.TEXT]
  }
  private aiController: ImageAnalyzerController = new ImageAnalyzerController()
  private options: ImageAIOptions = {
    types: [ImageAnalyzerType.SUBJECT, ImageAnalyzerType.TEXT],
    aiController: this.aiController
  }

  build() {
    Column() {
      Video({
        src: this.videoSrc,
        previewUri: this.previewUri,
        controller: this.controller,
        imageAIOptions: this.options
      })
        .width('100%')
        .height(600)
        .controls(false)
        .enableAnalyzer(true)
        .analyzerConfig(this.config)
        .onStart(() => {
          console.info('onStart')
        })
        .onPause(() => {
          console.info('onPause')
        })

      Row() {
        Button('start').onClick(() => {
          this.controller.start() // 开始播放
        }).margin(5)
        Button('pause').onClick(() => {
          this.controller.pause() // 暂停播放
        }).margin(5)
        Button('getTypes').onClick(() => {
            this.aiController.getImageAnalyzerSupportTypes()
        }).margin(5)
      }
    }
  }
}
```

### 示例3（播放拖入的视频）

以下示例展示了如何使Video组件能够播放拖入的视频。

```ts
// xxx.ets
import { unifiedDataChannel, uniformTypeDescriptor } from '@kit.ArkData';

@Entry
@Component
struct Index {
  @State videoSrc: Resource | string = $rawfile('video1.mp4');
  private controller: VideoController = new VideoController();

  build() {
    Column() {
      Video({
        src: this.videoSrc,
        controller: this.controller
      })
        .width('100%')
        .height(600)
        .onPrepared(() => {
          // 在onPrepared回调中执行controller的start方法，确保视频源更换后直接开始播放。
          this.controller.start();
        })
        .onDrop((e: DragEvent) => {
          // 外部视频拖入应用Video组件范围，松手后触发通过onDrop注册的回调。
          // 在DragEvent中会包含拖入的视频源信息，取出后赋值给状态变量videoSrc即可改变Video的视频源。
          let record = e.getData().getRecords()[0];
          if (record.getType() == uniformTypeDescriptor.UniformDataType.VIDEO) {
            let videoInfo = record as unifiedDataChannel.Video;
            this.videoSrc = videoInfo.videoUri;
          }
        })
    }
  }
}
```