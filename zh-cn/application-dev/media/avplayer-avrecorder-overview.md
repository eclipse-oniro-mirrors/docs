# AVPlayer和AVRecorder

media模块提供了[AVPlayer](#avplayer)和[AVRecorder](#avrecorder)用于播放、录制音视频。

## AVPlayer

AVPlayer主要工作是将Audio/Video媒体资源（比如mp4/mp3/mkv/mpeg-ts等）转码为可供渲染的图像和可听见的音频模拟信号，并通过输出设备进行播放。

AVPlayer提供功能完善一体化播放能力，应用只需要提供流媒体来源，不负责数据解析和解码就可达成播放效果。


### 音频播放

当使用AVPlayer开发音乐应用播放音频时，其交互关系如图所示。

**图1** 音频播放外部模块交互图  

![Audio Playback Interaction Diagram](figures/audio-playback-interaction-diagram.png)

音乐类应用通过调用JS接口层提供的AVPlayer接口实现相应功能时，框架层会通过播放服务（Player Framework）将资源解析成音频数据流（PCM），音频数据流经过软件解码后输出至音频服务（Audio Framework），由音频服务输出至音频驱动渲染，实现音频播放功能。完整的音频播放需要应用、Player Framework、Audio Framework、音频HDI共同实现。

图1中，数字标注表示需要数据与外部模块的传递。

1. 音乐应用将媒体资源传递给AVPlayer接口。

2. Player Framework将音频PCM数据流输出给Audio Framework，再由Audio Framework输出给音频HDI。

### 视频播放

当使用AVPlayer开发视频应用播放视频时，其交互关系如图所示。

**图2** 视频播放外部模块交互图  

![Video playback interaction diagram](figures/video-playback-interaction-diagram.png)

应用通过调用JS接口层提供的AVPlayer接口实现相应功能时，框架层会通过播放服务（Player Framework）解析成单独的音频数据流和视频数据流，音频数据流经过软件解码后输出至音频服务（Audio Framework），再至硬件接口层的音频HDI，实现音频播放功能。视频数据流经过硬件（推荐）/软件解码后输出至图形渲染服务（Graphic Framework），再输出至硬件接口层的显示HDI，完成图形渲染。

完整的视频播放需要：应用、XComponent、Player Framework、Graphic Framework、Audio Framework、显示HDI和音频HDI共同实现。

图2中，数字标注表示需要数据与外部模块的传递。

1. 应用从XComponent组件获取窗口SurfaceID，获取方式参考[XComponent](../reference/arkui-ts/ts-basic-components-xcomponent.md)。

2. 应用把媒体资源、SurfaceID传递给AVPlayer接口。

3. Player Framework把视频ES数据流输出给解码HDI，解码获得视频帧（NV12/NV21/RGBA）。

4. Player Framework把音频PCM数据流输出给Audio Framework，Audio Framework输出给音频HDI。

5. Player Framework把视频帧（NV12/NV21/RGBA）输出给Graphic Framework，Graphic Framework输出给显示HDI。

### 支持的格式与协议

推荐使用以下主流的播放格式，音视频容器、音视频编码属于内容创作者所掌握的专业领域，不建议应用开发者自制码流进行测试，以免产生无法播放、卡顿、花屏等兼容性问题。若发生此类问题不会影响系统，退出播放即可。

支持的协议如下：

| 协议类型 | 协议描述 | 
| -------- | -------- |
| 本地点播 | 协议格式：支持file&nbsp;descriptor，禁止file&nbsp;path |
| 网络点播 | 协议格式：支持http/https/hls |

支持的音频播放格式如下：

| 音频容器规格 | 规格描述 | 
| -------- | -------- |
| m4a | 音频格式：AAC | 
| aac | 音频格式：AAC | 
| mp3 | 音频格式：MP3 | 
| ogg | 音频格式：VORBIS | 
| wav | 音频格式：PCM | 

> **说明：**
> 
> 视频播放支持的视频格式分为必选规格和可选规格。必选规格为所有厂商均支持的视频格式。对于可选规格，厂商将基于实际情况决定是否实现。建议开发者做对应的兼容处理，保证应用功能全平台兼容。

| 视频格式 | 是否必选规格 |
| -------- | -------- |
| H264      | 是 |
| MPEG2     | 否 |
| MPEG4     | 否 |
| H263      | 否 |
| VP8       | 否 |

支持的视频播放格式和主流分辨率如下：

| 视频容器规格 | 规格描述 | 分辨率 | 
| -------- | -------- | -------- |
| mp4 | 视频格式：H264/MPEG2/MPEG4/H263<br/>音频格式：AAC/MP3 | 主流分辨率，如4K/1080P/720P/480P/270P | 
| mkv | 视频格式：H264/MPEG2/MPEG4/H263<br/>音频格式：AAC/MP3 | 主流分辨率，如4K/1080P/720P/480P/270P | 
| ts | 视频格式：H264/MPEG2/MPEG4<br/>音频格式：AAC/MP3 | 主流分辨率，如4K/1080P/720P/480P/270P | 
| webm | 视频格式：VP8<br/>音频格式：VORBIS | 主流分辨率，如4K/1080P/720P/480P/270P | 

## AVRecorder

AVRecorder主要工作是捕获音频信号，接收视频信号，完成音视频编码并保存到文件中，帮助开发者轻松实现音视频录制功能，包括开始录制、暂停录制、恢复录制、停止录制、释放资源等功能控制。它允许调用者指定录制的编码格式、封装格式、文件路径等参数。

**图3** 视频录制外部模块交互图  

![Video recording interaction diagram](figures/video-recording-interaction-diagram.png)

- 音频录制：应用通过调用JS接口层提供的AVRecorder接口实现音频录制时，框架层会通过录制服务（Player Framework），调用音频服务（Audio Framework）通过音频HDI捕获音频数据，通过软件编码封装后保存至文件中，实现音频录制功能。

- 视频录制：应用通过调用JS接口层提供的AVRecorder接口实现视频录制时，先通过Camera接口调用相机服务（Camera Framework）通过视频HDI捕获图像数据送至框架层的录制服务，录制服务将图像数据通过视频编码HDI编码，再将编码后的图像数据封装至文件中，实现视频录制功能。

通过音视频录制组合，可分别实现纯音频录制、纯视频录制，音视频录制。

图3中，数字标注表示需要数据与外部模块的传递。

1. 应用通过AVRecorder接口从录制服务获取SurfaceID。

2. 应用将SurfaceID设置给相机服务，相机服务可以通过SurfaceID获取到Surface。相机服务通过视频HDI捕获图像数据送至框架层的录制服务。

3. 相机服务通过Surface将视频数据传递给录制服务。

4. 录制服务通过视频编码HDI模块将视频数据编码。

5. 录制服务将音频参数设置给音频服务，并从音频服务获取到音频数据。

### 支持的格式

支持的音频源如下：

| 音频源类型 | 说明 | 
| -------- | -------- |
| mic | 系统麦克风作为音频源输入。 | 

支持的视频源如下：

| 视频源类型 | 说明 | 
| -------- | -------- |
| surface_yuv | 输入surface中携带的是raw&nbsp;data。 | 
| surface_es | 输入surface中携带的是ES&nbsp;data。 | 

支持的音视频编码格式如下：

| 音视频编码格式 | 说明 | 
| -------- | -------- |
| audio/mp4a-latm | 音频/mp4a-latm类型 | 
| video/mp4v-es | 视频/mpeg4类型 | 
| video/avc | 视频/avc类型 | 

支持的输出文件格式如下：

| 输出文件格式 | 说明 | 
| -------- | -------- |
| mp4 | 视频的容器格式，MP4。 | 
| m4a | 音频的容器格式，M4A。 | 
