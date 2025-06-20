# 使用AVPlayer播放流媒体(ArkTS)

本开发指导将介绍如何使用[AVPlayer](media-kit-intro.md#avplayer)开发流媒体直播、点播功能，以完整地播放一个流媒体视频作为示例，实现端到端播放流媒体资源。
当前指导仅介绍如何实现流媒体播放功能，本地音视频播放等其他场景，请参考[视频播放](video-playback.md)。

## 流媒体支持的格式

| 流媒体协议类型 | 典型链接 | 网络点播 | 网络直播 |内容保护 |
| -------- | -------- | -------- | -------- | -------- |
| HLS | `https://xxxx/index.m3u8` | 支持 | 支持 | 支持，详见[DRM Kit](../drm/drm-overview.md)。 |
| DASH | `https://xxxx.mpd` | 支持 | - | 支持，详见[DRM Kit](../drm/drm-overview.md)。 |
| HTTP/HTTPS | `https://xxxx.mp4` | 支持 | - | - |
| HTTP-FLV | `https://xxxx.flv` | 支持 | 支持 | - |

## 开发步骤

创建AVPlayer，设置播放资源和窗口，设置播放参数（音量/倍速/缩放模式），播放控制（播放/暂停/跳转/停止），重置，销毁资源。在进行应用开发的过程中，开发者可以通过AVPlayer的state属性主动获取当前状态或使用on('stateChange')方法监听状态变化。如果应用在视频播放器处于错误状态时执行操作，系统可能会抛出异常或生成其他未定义的行为。状态的详细说明请参考[AVPlayerState](../../reference/apis-media-kit/js-apis-media.md#avplayerstate9)。具体的开发步骤如下：

1. 创建实例createAVPlayer()，AVPlayer初始化idle状态。

2. 设置业务需要的监听事件，搭配全流程场景使用。支持的监听事件包括：

   | 事件类型 | 说明 |
   | -------- | -------- |
   | stateChange | 必要事件，监听播放器的state属性改变。 |
   | error | 必要事件，监听播放器的错误信息。 |
   | durationUpdate | 用于进度条，监听进度条长度，刷新资源时长。 |
   | timeUpdate | 用于进度条，监听进度条当前位置，刷新当前时间。 |
   | seekDone | 响应API调用，监听seek()请求完成情况。<br/>当使用seek()跳转到指定播放位置后，如果seek操作成功，将上报该事件。 |
   | speedDone | 响应API调用，监听setSpeed()请求完成情况。<br/>当使用setSpeed()设置播放倍速后，如果setSpeed操作成功，将上报该事件。 |
   | volumeChange | 响应API调用，监听setVolume()请求完成情况。<br/>当使用setVolume()调节播放音量后，如果setVolume操作成功，将上报该事件。 |
   | bufferingUpdate | 用于网络播放，监听网络播放缓冲信息，用于上报缓冲百分比以及缓存播放进度。 |
   | audioInterrupt | 监听音频焦点切换信息，搭配属性audioInterruptMode使用。<br/>如果当前设备存在多个音频正在播放，音频焦点被切换（即播放其他媒体如通话等）时将上报该事件，应用可以及时处理。 |

3. 设置资源：[使用AVPlayer设置播放URL](playback-url-setting-method.md)，AVPlayer进入initialized状态。
   > **说明：**
   >
   > 下面代码示例中的url仅作示意使用，开发者需根据实际情况，确认资源有效性并设置：
   > 
   > - 使用网络播放路径，需[声明权限](../../security/AccessToken/declare-permissions.md)：ohos.permission.INTERNET。
   > 
   > - 需要使用支持的播放格式与协议。
   > 

4. 设置窗口：获取并设置属性SurfaceID，用于设置显示画面。

   应用需要从XComponent组件获取surfaceID，获取方式请参考[XComponent](../../reference/apis-arkui/arkui-ts/ts-basic-components-xcomponent.md)。

5. 准备播放：调用prepare()，AVPlayer进入prepared状态，此时可以获取duration，设置缩放模式、音量等。

6. 视频播控：播放play()，暂停pause()，跳转seek()，停止stop() 等操作。

7. （可选）更换资源：调用reset()重置资源，AVPlayer重新进入idle状态，允许更换资源url。

8. 退出播放：调用release()销毁实例，AVPlayer进入released状态，退出播放。

## 注意事项

播放流媒体的标准流程如上述开发步骤所示，但使用不同的流媒体格式在实际开发的过程中还是会存在一定差异，本节将详细描述不同流媒体格式业务的差异，包括设置视频起播策略、切换音视频轨道等。

### 流媒体缓冲状态

当下载速率低于片源的码率时，可能会出现卡顿，此时播放器检测到缓冲区数据不足，会先缓冲一些数据再播放，避免连续卡顿。一次卡顿对应的缓冲事件上报过程为：BUFFERING_START-> BUFFERING_PERCENT 0 -> ... -> BUFFERING_PERCENT 100 -> BUFFERING_END。而CACHED_DURATION无论是卡顿过程中还是播放过程中，都会持续上报，直至下载至资源末尾。详见[BufferingInfoType缓冲事件类型枚举](../../reference/apis-media-kit/js-apis-media.md#bufferinginfotype8)。

监听当前bufferingUpdate缓冲状态示例代码：

```ts
avPlayer.on('bufferingUpdate', (infoType : media.BufferingInfoType, value : number) => {
  console.info(`AVPlayer bufferingUpdate, infoType is ${infoType}, value is ${value}.`);
})
```

### HLS切换码率

当前流媒体HLS协议流支持多码率播放，默认情况下，播放器会根据网络下载速度选择合适的码率。

1. 通过[on('availableBitrates')](../../reference/apis-media-kit/js-apis-media.md#onavailablebitrates9)监听当前HLS协议流可用的码率，若监听的码率列表长度为0，则不支持设置指定码率。

    ```ts
    // 创建avPlayer实例对象。
    let avPlayer: media.AVPlayer = await media.createAVPlayer();
    // 监听当前HLS协议流可用的码率。
    avPlayer.on('availableBitrates', (bitrates: Array<number>) => {
      console.info('availableBitrates called, and availableBitrates length is: ' + bitrates.length);
    })
    ```

2. 通过[setBitrate](../../reference/apis-media-kit/js-apis-media.md#setbitrate9)接口设置播放码率，若用户设置的码率不在可用码率中，播放器将从可用码率中选择最小且最接近的码率。该接口只能在prepared/playing/paused/completed状态下调用，可通过监听[bitrateDone](../../reference/apis-media-kit/js-apis-media.md#onbitratedone9)事件确认是否生效。

    ```ts
    // 创建avPlayer实例对象。
    let avPlayer: media.AVPlayer = await media.createAVPlayer();
    // 监听码率设置是否生效。
    avPlayer.on('bitrateDone', (bitrate: number) => {
      console.info('bitrateDone called, and bitrate value is: ' + bitrate);
    })
    // 设置播放码率。
    let bitrate: number = 96000;
    avPlayer.setBitrate(bitrate);
    ```

### DASH设置视频起播策略

为了保证在弱网环境下的播放体验，AVPlayer会默认选择最低的视频分辨率开始播放，随后依据网络状况自动调整。开发者可根据实际需求，自定义DASH视频的起播策略，包括设定视频的宽度、高度以及色彩格式等参数。

以调节视频起播分辨率为例，下述示例代码描述了设置视频宽度1920px、高度1080px起播。此时，AVPlayer会选择MPD资源中一路分辨率为1920x1080的视频资源进行播放。

```ts
let mediaSource : media.MediaSource = media.createMediaSourceWithUrl("http://test.cn/dash/aaa.mpd",  {"User-Agent" : "User-Agent-Value"});
let playbackStrategy : media.PlaybackStrategy = {preferredWidth: 1920, preferredHeight: 1080};
avPlayer.setMediaSource(mediaSource, playbackStrategy);
```

### DASH切换音视频轨道

DASH流媒体资源一般包含多路分辨率、码率、采样率、编码格式等参数各不相同的音频、视频和字幕资源。默认情况下，AVPlayer会依据网络状况自动切换不同码率的视频轨道。开发者可根据实际需求，自主选择指定的音视频轨道进行播放，此时自适应码率切换策略会失效。

1. 设置selectTrack生效的监听事件[trackChange](../../reference/apis-media-kit/js-apis-media.md#ontrackchange12)。

    ```ts
    avPlayer.on('trackChange', (index: number, isSelect: boolean) => {
      console.info(`trackChange info, index: ${index}, isSelect: ${isSelect}`);
    })
    ```

2. 调用[getTrackDescription](../../reference/apis-media-kit/js-apis-media.md#gettrackdescription9)获取所有音视频轨道列表。开发者可根据实际需求，基于[MediaDescription](../../reference/apis-media-kit/js-apis-media.md#mediadescription8)各字段信息，确定目标轨道索引。

    ```ts
    // 以获取1080p视频轨道索引为例。
    public videoTrackIndex: number;
    avPlayer.getTrackDescription((error: BusinessError, arrList: Array<media.MediaDescription>) => {
      if (arrList != null) {
        for (let i = 0; i < arrList.length; i++) {
          let propertyIndex: Object = arrList[i][media.MediaDescriptionKey.MD_KEY_TRACK_INDEX];
          let propertyType: Object = arrList[i][media.MediaDescriptionKey.MD_KEY_TRACK_TYPE];
          let propertyWidth: Object = arrList[i][media.MediaDescriptionKey.MD_KEY_WIDTH];
          let propertyHeight: Object = arrList[i][media.MediaDescriptionKey.MD_KEY_HEIGHT];
          if (propertyType == media.MediaType.MEDIA_TYPE_VID && propertyWidth == 1920 && propertyHeight == 1080) {
            videoTrackIndex = parseInt(propertyIndex.toString()); // 获取1080p视频轨道索引。
          }
        }
      } else {
        console.error(`getTrackDescription fail, error:${error}`);
      }
    });
    ```                   

3. 在音视频播放过程中调用[selectTrack](../../reference/apis-media-kit/js-apis-media.md#selecttrack12)选择对应的音视频轨道，或者调用[deselectTrack](../../reference/apis-media-kit/js-apis-media.md#deselecttrack12)取消选择的音视频轨道。

    ```ts
    // 切换至目标视频轨道。
    avPlayer.selectTrack(videoTrackIndex);
    // 取消选择目标视频轨道。
    // avPlayer.deselectTrack(videoTrackIndex);
    ```

## 异常场景说明

使用avPlayer播放流媒体过程中断网：流媒体模块会根据返回的错误码、服务器请求失败的响应时间、请求次数等因素综合处理。若错误码类型属于不进行请求重试的类型，会向应用上报对应的错误码。若错误码类型需要进行请求重试，会在30s内进行至多10次的请求重试。若请求重试次数超过10次，或重试总时长超过30秒，会向应用上报对应的错误码。若请求重试成功，则继续播放。

## 完整示例

参考以下示例，完整地播放一个流媒体视频。

```ts
import { media } from '@kit.MediaKit';
import { fileIo as fs } from '@kit.CoreFileKit';
import { common } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';

export class AVPlayerDemo {
  private count: number = 0;
  private surfaceID: string = ''; // surfaceID用于播放画面显示，具体的值需要通过Xcomponent接口获取，相关文档链接见上面Xcomponent创建方法。
  private isSeek: boolean = true; // 用于区分模式是否支持seek操作。
  public audioTrackList: number[] = [];
  public videoTrackList: number[] = [];

  constructor(surfaceID: string) {
    this.surfaceID = surfaceID;
  }

  // 注册avplayer回调函数。
  setAVPlayerCallback(avPlayer: media.AVPlayer) {
    // startRenderFrame首帧渲染回调函数。
    avPlayer.on('startRenderFrame', () => {
      console.info(`AVPlayer start render frame`);
    });
    // seek操作结果回调函数。
    avPlayer.on('seekDone', (seekDoneTime: number) => {
      console.info(`AVPlayer seek succeeded, seek time is ${seekDoneTime}`);
    })
    // avPlayer.on('trackChange', (index: number, isSelect: boolean) => {
    //   console.info(`AVPlayer track changed, track index: ${index}, isSelect: ${isSelect}`);
    // })
    // error回调监听函数,当avPlayer在操作过程中出现错误时调用 reset接口触发重置流程。
    avPlayer.on('error', (err: BusinessError) => {
      console.error(`Invoke avPlayer failed, code is ${err.code}, message is ${err.message}`);
      avPlayer.reset(); // 调用reset重置资源，触发idle状态。
    })
    // 状态机变化回调函数。
    avPlayer.on('stateChange', async (state: string, reason: media.StateChangeReason) => {
      switch (state) {
        case 'idle': // 成功调用reset接口后触发该状态机上报。
          console.info('AVPlayer state idle called.');
          avPlayer.release(); // 调用release接口销毁实例对象。
          break;
        case 'initialized': // avplayer 设置播放源后触发该状态上报。
          console.info('AVPlayer state initialized called.');
          avPlayer.surfaceId = this.surfaceID; // 设置显示画面，当播放的资源为纯音频时无需设置。
          avPlayer.prepare();
          break;
        case 'prepared': // prepare调用成功后上报该状态机。
          console.info('AVPlayer state prepared called.');
          avPlayer.play(); // 调用播放接口开始播放。
          break;
        case 'playing': // play成功调用后触发该状态机上报。
          console.info('AVPlayer state playing called.');
          break;
        case 'paused': // pause成功调用后触发该状态机上报。
          console.info('AVPlayer state paused called.');
          break;
        case 'completed': // 播放结束后触发该状态机上报。
          console.info('AVPlayer state completed called.');
          avPlayer.stop(); //调用播放结束接口。
          break;
        case 'stopped': // stop接口成功调用后触发该状态机上报。
          console.info('AVPlayer state stopped called.');
          avPlayer.reset(); // 调用reset接口初始化avplayer状态。
          break;
        case 'released':
          console.info('AVPlayer state released called.');
          break;
        default:
          console.info('AVPlayer state unknown called.');
          break;
      }
    })
    // 监听流媒体缓冲状态、缓冲百分比、已缓冲数据预估可播放时长。
    avPlayer.on('bufferingUpdate', (infoType : media.BufferingInfoType, value : number) => {
      console.info(`AVPlayer bufferingUpdate, infoType is ${infoType}, value is ${value}.`);
    })
  }

  // 以下demo为通过url设置网络地址来实现播放流媒体HLS点播视频。
  async avPlayerVodDemo() {
    // 创建avPlayer实例对象。
    let avPlayer: media.AVPlayer = await media.createAVPlayer();
    // 创建状态机变化回调函数。
    this.setAVPlayerCallback(avPlayer);
    this.isSeek = true; // 点播支持seek操作。
    avPlayer.url = 'http://xxx.xxx.xxx.xxx:xx/xx/index.m3u8';
  }

  // 以下demo为通过url设置网络地址来实现播放流媒体HLS直播视频。
  async avPlayerLiveDemo() {
    // 创建avPlayer实例对象。
    let avPlayer: media.AVPlayer = await media.createAVPlayer();
    // 创建状态机变化回调函数。
    this.setAVPlayerCallback(avPlayer);
    this.isSeek = false; // 直播不支持seek操作。
    avPlayer.url = 'http://xxx.xxx.xxx.xxx:xx/xx/index.m3u8';
  }

  // 以下demo为通过url设置网络地址来实现播放Dash流媒体视频。
  async avPlayerDashDemo() {
    // 创建avPlayer实例对象。
    let avPlayer: media.AVPlayer = await media.createAVPlayer();
    // 创建状态机变化回调函数。
    this.setAVPlayerCallback(avPlayer);
    // 设置播放偏好策略。
    // let mediaSource : media.MediaSource = media.createMediaSourceWithUrl("http://test.cn/dash/aaa.mpd",  {"User-Agent" : "User-Agent-Value"});
    // let playbackStrategy : media.PlaybackStrategy = {preferredWidth: 1, preferredHeight: 2, preferredBufferDuration: 3, preferredHdr: false};
    // avPlayer.setMediaSource(mediaSource, playbackStrategy);
    this.isSeek = true; // 表示支持seek操作。
    avPlayer.url = 'http://test.cn/dash/aaa.mpd'; //须替换为DASH资源实际地址。

    // 通过selectTrack设置音频/视频轨道，通过deselectTrack取消上次设置的音频/视频轨道并恢复到默认音频/视频轨道。
    avPlayer.getTrackDescription((error: BusinessError, arrList: Array<media.MediaDescription>) => {
      if (arrList != null) {
        for (let i = 0; i < arrList.length; i++) {
          let propertyIndex: Object = arrList[i][media.MediaDescriptionKey.MD_KEY_TRACK_INDEX];
          let propertyType: Object = arrList[i][media.MediaDescriptionKey.MD_KEY_TRACK_TYPE];
          if (propertyType == 0) {
            this.audioTrackList.push(parseInt(propertyIndex.toString())); // 获取音频轨道列表。
          } else if (propertyType == 1) {
            this.videoTrackList.push(parseInt(propertyIndex.toString())); // 获取视频轨道列表。
          }
        }
      } else {
        console.error(`getTrackDescription fail, error:${error}`);
      }
    });
    // 选择其中一个视频轨道。
    // avPlayer.selectTrack(this.videoTrackList[0]);
    // 取消选择的视频轨道。
    // avPlayer.deselectTrack(this.videoTrackList[0]);
  }

  // 以下demo为通过setMediaSource设置自定义头域及媒体播放优选参数实现初始播放参数设置，以流媒体Https点播为例。
  async preDownloadDemo() {
    // 创建avPlayer实例对象。
    let avPlayer: media.AVPlayer = await media.createAVPlayer();
    // 创建状态机变化回调函数。
    this.setAVPlayerCallback(avPlayer);
    this.isSeek = true; // 点播支持seek操作。
    // 创建mediaSource实例对象，设置媒体来源，定制HTTP请求，如需要，可以键值对的形式设置User-Agent、Cookie、Referer等字段。
    let mediaSource : media.MediaSource = media.createMediaSourceWithUrl("https://xxx.xxx",  {"User-Agent" : "User-Agent-Value", "Cookie" : "Cookie-Value", "Referer" : "Referer-Value"});
    // 设置播放策略，设置缓冲区数据量为20s。
    let playbackStrategy : media.PlaybackStrategy = {preferredBufferDuration: 20};
    // 为avPlayer设置媒体来源和播放策略。
    avPlayer.setMediaSource(mediaSource, playbackStrategy);
  }
}
```



