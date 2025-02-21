# 音效管理

音效管理主要包括播放实例音效管理、全局音效查询和空间音频管理三部分，播放实例音效管理主要包括查询和设置当前音频播放流的音效模式，全局音效查询支持查询[StreamUsage](../../reference/apis-audio-kit/js-apis-audio.md#streamusage)对应场景支持的音效模式，空间音频管理包含空间音频相关状态和能力的查询、设置与监听。

## 播放实例音效管理

主要包括查询和设置当前音频播放流的音效模式，[音效模式](../../reference/apis-audio-kit/js-apis-audio.md#audioeffectmode10)包括EFFECT_NONE关闭音效模式和EFFECT_DEFAULT默认音效模式。默认音效模式会根据创建音频流的[StreamUsage](../../reference/apis-audio-kit/js-apis-audio.md#streamusage)自动加载对应场景的音效。

### 获取播放实例

管理播放实例音效的接口是[getAudioEffectMode()](../../reference/apis-audio-kit/js-apis-audio.md#getaudioeffectmode10)查询当前音频播放流的音效模式和[setAudioEffectMode(mode: AudioEffectMode)](../../reference/apis-audio-kit/js-apis-audio.md#setaudioeffectmode10)设置当前音频播放流的音效模式，在使用之前，需要使用[createAudioRenderer(options: AudioRendererOptions)](../../reference/apis-audio-kit/js-apis-audio.md#audiocreateaudiorenderer8)先创建音频播放流AudioRenderer实例。

1. 导入音频接口。

    ```ts
    import audio from '@ohos.multimedia.audio';
    ```

2. 配置音频渲染参数并创建AudioRenderer实例，音频渲染参数的详细信息可以查看[AudioRendererOptions](../../reference/apis-audio-kit/js-apis-audio.md#audiorendereroptions8)，创建AudioRenderer实例时会默认挂载EFFECT_DEFAULT模式音效。

    ```ts
    import { BusinessError } from '@ohos.base';

    let audioStreamInfo: audio.AudioStreamInfo = {
      samplingRate: audio.AudioSamplingRate.SAMPLE_RATE_44100,
      channels: audio.AudioChannel.CHANNEL_1,
      sampleFormat: audio.AudioSampleFormat.SAMPLE_FORMAT_S16LE,
      encodingType: audio.AudioEncodingType.ENCODING_TYPE_RAW
    };

    let audioRendererInfo: audio.AudioRendererInfo = {
      usage: audio.StreamUsage.STREAM_USAGE_VOICE_COMMUNICATION,
      rendererFlags: 0
    };

    let audioRendererOptions: audio.AudioRendererOptions = {
      streamInfo: audioStreamInfo,
      rendererInfo: audioRendererInfo
    };
    let audioRenderer: audio.AudioRenderer | undefined = undefined;
   
    audio.createAudioRenderer(audioRendererOptions, (err: BusinessError, data: audio.AudioRenderer) => {
      if (err) {
        console.error(`Invoke createAudioRenderer failed, code is ${err.code}, message is ${err.message}`);
        return;
      } else {
        console.info('Invoke createAudioRenderer succeeded.');
        audioRenderer = data;
      }
    });
    ```

### 查询当前播放实例的音效模式

  ```ts
  import audio from '@ohos.multimedia.audio';
  import { BusinessError } from '@ohos.base';

  audioRenderer.getAudioEffectMode((err: BusinessError, effectMode: audio.AudioEffectMode) => {
    if (err) {
      console.error(`Failed to get params, code is ${err.code}, message is ${err.message}`);
      return;    
    } else {
      console.info(`getAudioEffectMode: ${effectMode}`);
    }
  });
  ```

### 设置当前播放实例的音效模式

关闭系统音效：

  ```ts
  import audio from '@ohos.multimedia.audio';
  import { BusinessError } from '@ohos.base';

  audioRenderer.setAudioEffectMode(audio.AudioEffectMode.EFFECT_NONE, (err: BusinessError) => {
    if (err) {
      console.error(`Failed to set params, code is ${err.code}, message is ${err.message}`);
      return;
    } else {
      console.info('Callback invoked to indicate a successful audio effect mode setting.');
    }
  });
  ```

开启系统音效默认模式：

  ```ts
  import audio from '@ohos.multimedia.audio';
  import { BusinessError } from '@ohos.base';

  audioRenderer.setAudioEffectMode(audio.AudioEffectMode.EFFECT_DEFAULT, (err: BusinessError) => {
    if (err) {
      console.error(`Failed to set params, code is ${err.code}, message is ${err.message}`);
      return;
    } else {
      console.info('Callback invoked to indicate a successful audio effect mode setting.');
    }
  });
  ```

## 全局查询音效模式

主要包括全局音效查询相应[StreamUsage](../../reference/apis-audio-kit/js-apis-audio.md#streamusage)对应场景的音效模式。
对于播放音频类的应用，开发者需要关注该应用的音频流使用什么音效模式并做出相应的操作，比如音乐App播放时，应选择音乐场景下的模式。在使用查询接口前，开发者需要使用getStreamManager()创建一个AudioStreamManager音频流管理实例。

### 获取音频流管理接口

创建AudioStreamManager实例。在使用AudioStreamManager的API前，需要使用getStreamManager()创建一个AudioStreamManager实例。

   ```ts
   import audio from '@ohos.multimedia.audio';

   let audioManager = audio.getAudioManager();
   let audioStreamManager = audioManager.getStreamManager();
   ```

### 查询对应场景的音效模式

  ```ts
  import audio from '@ohos.multimedia.audio';
  import { BusinessError } from '@ohos.base';

  audioStreamManager.getAudioEffectInfoArray(audio.StreamUsage.STREAM_USAGE_MEDIA, async (err: BusinessError, audioEffectInfoArray: audio.AudioEffectInfoArray) => {
    if (err) {
      console.error('Failed to get effect info array');
      return;    
    } else {
      console.info(`getAudioEffectInfoArray: ${audioEffectInfoArray}`);
    }
  });
  ```

## 空间音频管理（仅对系统应用开放）

空间音频管理仅开放给系统级应用，主要包括空间音频相关状态（空间音频渲染的开启与关闭、头动跟踪的开启与关闭）的查询、设置与监听，空间音频相关能力（空间音频渲染能力、头动跟踪能力）的查询，以及空间化设备状态的更新。

对于播放音频类的系统级应用，开发者可以查询空间音频渲染与头动跟踪的开关状态，以及系统/指定设备是否支持空间音频渲染与头动跟踪能力。

对于空间音频控制类的系统级应用（比如空间音频UX等），开发者在查询上述状态和能力之外，还可以对空间音频渲染和头动跟踪的开关进行设置，以及更新空间化设备的状态，指明特定空间化设备是否支持空间音频渲染和头动跟踪能力。
在使用此功能前，应用需要先申请权限`ohos.permission.MANAGE_SYSTEM_AUDIO_EFFECTS`，申请方式请参考：[申请应用权限](../../security/AccessToken/determine-application-mode.md#system_basic等级的应用申请权限)。

### 获取空间音频管理接口

创建AudioSpatializationManager实例。在使用AudioSpatializationManager的API前，需要使用getSpatializationManager()创建一个AudioSpatializationManager实例。

  ```ts
  import audio from '@ohos.multimedia.audio';

  let audioManager = audio.getAudioManager();
  let audioSpatializationManager = audioManager.getSpatializationManager();
  ```

### 查询系统是否支持空间音频渲染能力

系统应用开发者可以通过[isSpatializationSupported](../../reference/apis-audio-kit/js-apis-audio-sys.md#isspatializationsupported11)接口查询当前系统是否具有空间音频渲染的能力。

  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    let isSpatializationSupported: boolean = audioSpatializationManager.isSpatializationSupported();
    console.info(`AudioSpatializationManager isSpatializationSupported: ${isSpatializationSupported}`);
  } catch (err) {
    let error = err as BusinessError;
    console.error(`ERROR: ${error}`);
  }
  ```

### 查询指定设备是否支持空间音频渲染能力

系统应用开发者可以通过[isSpatializationSupportedForDevice](../../reference/apis-audio-kit/js-apis-audio-sys.md#isspatializationsupportedfordevice11)接口查询指定设备是否具有空间音频渲染的能力，开发者需要使用AudioDeviceDescriptor作为入参来指定设备，建议通过音频框架中其他接口来获取当前已连接设备或当前发声设备的AudioDeviceDescriptor。AudioDeviceDescriptor的具体信息可以参考[AudioDeviceDescriptor](../../reference/apis-audio-kit/js-apis-audio.md#audiodevicedescriptor)。

  ```ts
  import audio from '@ohos.multimedia.audio';
  import { BusinessError } from '@ohos.base';

  let deviceDescriptor: audio.AudioDeviceDescriptor = {
    deviceRole : audio.DeviceRole.OUTPUT_DEVICE,
    deviceType : audio.DeviceType.BLUETOOTH_A2DP,
    id : 1,
    name : "",
    address : "123",
    sampleRates : [44100],
    channelCounts : [2],
    channelMasks : [0],
    networkId : audio.LOCAL_NETWORK_ID,
    interruptGroupId : 1,
    volumeGroupId : 1,
    displayName : ""
  }
  try {
    let isSpatializationSupportedForDevice: boolean = audioSpatializationManager.isSpatializationSupportedForDevice(deviceDescriptor);
    console.info(`AudioSpatializationManager isSpatializationSupportedForDevice: ${isSpatializationSupportedForDevice}`);
  } catch (err) {
    let error = err as BusinessError;
    console.error(`ERROR: ${error}`);
  }
  ```

### 查询系统是否支持头动跟踪能力

系统应用开发者可以通过[isHeadTrackingSupported](../../reference/apis-audio-kit/js-apis-audio-sys.md#isheadtrackingsupported11)接口查询当前系统是否具有头动跟踪的能力。

  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    let isHeadTrackingSupported: boolean = audioSpatializationManager.isHeadTrackingSupported();
    console.info(`AudioSpatializationManager isHeadTrackingSupported: ${isHeadTrackingSupported}`);
  } catch (err) {
    let error = err as BusinessError;
    console.error(`ERROR: ${error}`);
  }
  ```

### 查询指定设备是否支持头动跟踪能力

系统应用开发者可以通过[isHeadTrackingSupportedForDevice](../../reference/apis-audio-kit/js-apis-audio-sys.md#isheadtrackingsupportedfordevice11)接口查询指定设备是否具有头动跟踪的能力，开发者需要使用AudioDeviceDescriptor作为入参来指定设备，建议通过音频框架中其他接口来获取当前已连接设备或当前发声设备的AudioDeviceDescriptor。AudioDeviceDescriptor的具体信息可以参考[AudioDeviceDescriptor](../../reference/apis-audio-kit/js-apis-audio.md#audiodevicedescriptor)。

  ```ts
  import audio from '@ohos.multimedia.audio';
  import { BusinessError } from '@ohos.base';

  let deviceDescriptor: audio.AudioDeviceDescriptor = {
    deviceRole : audio.DeviceRole.OUTPUT_DEVICE,
    deviceType : audio.DeviceType.BLUETOOTH_A2DP,
    id : 1,
    name : "",
    address : "123",
    sampleRates : [44100],
    channelCounts : [2],
    channelMasks : [0],
    networkId : audio.LOCAL_NETWORK_ID,
    interruptGroupId : 1,
    volumeGroupId : 1,
    displayName : ""
  }
  try {
    let isHeadTrackingSupportedForDevice: boolean = audioSpatializationManager.isHeadTrackingSupportedForDevice(deviceDescriptor);
    console.info(`AudioSpatializationManager isHeadTrackingSupportedForDevice: ${isHeadTrackingSupportedForDevice}`);
  } catch (err) {
    let error = err as BusinessError;
    console.error(`ERROR: ${error}`);
  }
  ```

### 开启/关闭空间音频渲染效果

系统应用开发者可以通过[setSpatializationEnabled](../../reference/apis-audio-kit/js-apis-audio-sys.md#setspatializationenabled11)接口开启/关闭空间音频渲染的效果，入参为true时为开启空间音频渲染，入参为false时为关闭空间音频渲染。

在使用此功能前，应用需要先申请权限`ohos.permission.MANAGE_SYSTEM_AUDIO_EFFECTS`，申请方式请参考：[申请应用权限](../../security/AccessToken/determine-application-mode.md#system_basic等级的应用申请权限)。

在开启空间音频渲染时，需要先确保系统和当前发声设备都具有空间音频渲染的能力，同时，如果音频流的AudioEffectMode为EFFECT_NONE，则无论是否开启空间音频渲染，都不会有空间音频渲染效果。

  ```ts
  import { BusinessError } from '@ohos.base';

  let enable: boolean = true
  audioSpatializationManager.setSpatializationEnabled(enable, (err: BusinessError) => {
    if (err) {
      console.error(`Result ERROR: ${err}`);
    } else {
      console.info(`setSpatializationEnabled success`);
    }
  });
  ```

### 查询空间音频渲染效果的开关状态

系统应用开发者可以通过[isSpatializationEnabled](../../reference/apis-audio-kit/js-apis-audio-sys.md#isspatializationenabled11)接口查询空间音频渲染效果的开关状态，返回true为空间音频渲染开启，false为空间音频渲染关闭。该接口将返回setSpatializationEnabled()接口中成功设置的值，默认为开启。该状态仅为开关状态，实际是否生效还需依赖系统和当前发声设备是否支持空间音频渲染，以及音频流的AudioEffectMode。

  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    let isSpatializationEnabled: boolean = audioSpatializationManager.isSpatializationEnabled();
    console.info(`AudioSpatializationManager isSpatializationEnabled: ${isSpatializationEnabled}`);
  } catch (err) {
    let error = err as BusinessError;
    console.error(`ERROR: ${error}`);
  }
  ```

### 订阅空间音频渲染效果的开关状态变化事件

系统应用开发者可以通过[on('spatializationEnabledChange')](../../reference/apis-audio-kit/js-apis-audio-sys.md#onspatializationenabledchange11)接口订阅空间音频渲染效果的开关状态变化事件，回调为true为空间音频渲染被开启，false为空间音频渲染被关闭。当开发者通过setSpatializationEnabled()接口成功地改变了空间音频渲染的开关状态时，回调将被触发。

  ```ts
  import { BusinessError } from '@ohos.base';

  audioSpatializationManager.on('spatializationEnabledChange', (isSpatializationEnabled: boolean) => {
    console.info(`isSpatializationEnabled: ${isSpatializationEnabled}`);
  });
  ```

### 取消订阅空间音频渲染效果的开关状态变化事件

系统应用开发者可以通过[off('spatializationEnabledChange')](../../reference/apis-audio-kit/js-apis-audio-sys.md#offspatializationenabledchange11)接口取消订阅空间音频渲染效果的开关状态变化事件。

  ```ts
  import { BusinessError } from '@ohos.base';

  audioSpatializationManager.off('spatializationEnabledChange');
  ```

### 开启/关闭头动跟踪效果

系统应用开发者可以通过[setHeadTrackingEnabled](../../reference/apis-audio-kit/js-apis-audio-sys.md#setheadtrackingenabled11)接口开启/关闭头动跟踪的效果，入参为true时为开启头动跟踪，入参为false时为关闭头动跟踪。

在使用此功能前，应用需要先申请权限`ohos.permission.MANAGE_SYSTEM_AUDIO_EFFECTS`，申请方式请参考：[申请应用权限](../../security/AccessToken/determine-application-mode.md#system_basic等级的应用申请权限)。

在开启头动跟踪时，需要先确保系统和当前发声设备都具有头动跟踪的能力。同时，如果音频流的AudioEffectMode为EFFECT_NONE，则无论是否开启头动跟踪，都不会有头动跟踪效果。

  ```ts
  import { BusinessError } from '@ohos.base';

  let enable: boolean = true;
  audioSpatializationManager.setHeadTrackingEnabled(enable, (err: BusinessError) => {
    if (err) {
      console.error(`Result ERROR: ${err}`);
    } else {
      console.info(`setHeadTrackingEnabled success`);
    }
  });
  ```

### 查询头动跟踪效果的开关状态

系统应用开发者可以通过[isHeadTrackingEnabled](../../reference/apis-audio-kit/js-apis-audio-sys.md#isheadtrackingenabled11)接口查询头动跟踪效果的开关状态，返回true为头动跟踪开启，false为头动跟踪关闭。该接口将返回setHeadTrackingEnabled()接口中成功设置的值，默认为关闭。该状态仅为开关状态，实际是否生效还需依赖系统和当前发声设备是否支持头动跟踪，以及音频流的AudioEffectMode。

  ```ts
  import { BusinessError } from '@ohos.base';

  try {
    let isHeadTrackingEnabled: boolean = audioSpatializationManager.isHeadTrackingEnabled();
    console.info(`AudioSpatializationManager isHeadTrackingEnabled: ${isHeadTrackingEnabled}`);
  } catch (err) {
    let error = err as BusinessError;
    console.error(`ERROR: ${error}`);
  }
  ```

### 订阅头动跟踪效果的开关状态变化事件

系统应用开发者可以通过[on('headTrackingEnabledChange')](../../reference/apis-audio-kit/js-apis-audio-sys.md#onheadtrackingenabledchange11)接口订阅头动跟踪效果的开关状态变化事件，回调为true为头动跟踪被开启，false为头动跟踪被关闭。当开发者通过setHeadTrackingEnabled()接口成功地改变了头动跟踪的开关状态时，回调将被触发。

  ```ts
  audioSpatializationManager.on('headTrackingEnabledChange', (isHeadTrackingEnabled: boolean) => {
    console.info(`isHeadTrackingEnabled: ${isHeadTrackingEnabled}`);
  });
  ```

### 取消订阅头动跟踪效果的开关状态变化事件

系统应用开发者可以通过[off('headTrackingEnabledChange')](../../reference/apis-audio-kit/js-apis-audio-sys.md#offheadtrackingenabledchange11)接口取消订阅头动跟踪效果的开关状态变化事件。

  ```ts
  audioSpatializationManager.off('headTrackingEnabledChange');
  ```

### 更新空间化设备状态

系统应用开发者可以通过[updateSpatialDeviceState](../../reference/apis-audio-kit/js-apis-audio-sys.md#updatespatialdevicestate11)接口更新空间化设备状态，空间化设备状态包含设备的地址、是否具有空间音频渲染的能力、是否具有头动跟踪的能力和设备的形态类型。

在使用此功能前，应用需要先申请权限`ohos.permission.MANAGE_SYSTEM_AUDIO_EFFECTS`，申请方式请参考：[申请应用权限](../../security/AccessToken/determine-application-mode.md#system_basic等级的应用申请权限)。

空间化设备状态AudioSpatialDeviceState的具体信息可以参考[AudioSpatialDeviceState](../../reference/apis-audio-kit/js-apis-audio-sys.md#audiospatialdevicestate11)。

  ```ts
  import audio from '@ohos.multimedia.audio';
  import { BusinessError } from '@ohos.base';

  let spatialDeviceState: audio.AudioSpatialDeviceState = {
    address: "123",
    isSpatializationSupported: true,
    isHeadTrackingSupported: true,
    spatialDeviceType: audio.AudioSpatialDeviceType.SPATIAL_DEVICE_TYPE_IN_EAR_HEADPHONE
  }
  try {
    audioSpatializationManager.updateSpatialDeviceState(spatialDeviceState);
    console.info(`AudioSpatializationManager updateSpatialDeviceState success`);
  } catch (err) {
    let error = err as BusinessError;
    console.error(`ERROR: ${error}`);
  }
  ```