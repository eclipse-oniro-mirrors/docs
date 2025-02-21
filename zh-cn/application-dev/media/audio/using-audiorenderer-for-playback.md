# 使用AudioRenderer开发音频播放功能

AudioRenderer是音频渲染器，用于播放PCM（Pulse Code Modulation）音频数据，相比AVPlayer而言，可以在输入前添加数据预处理，更适合有音频开发经验的开发者，以实现更灵活的播放功能。

## 开发指导

使用AudioRenderer播放音频涉及到AudioRenderer实例的创建、音频渲染参数的配置、渲染的开始与停止、资源的释放等。本开发指导将以一次渲染音频数据的过程为例，向开发者讲解如何使用AudioRenderer进行音频渲染，建议搭配[AudioRenderer的API说明](../../reference/apis-audio-kit/js-apis-audio.md#audiorenderer8)阅读。

下图展示了AudioRenderer的状态变化，在创建实例后，调用对应的方法可以进入指定的状态实现对应的行为。需要注意的是在确定的状态执行不合适的方法可能导致AudioRenderer发生错误，建议开发者在调用状态转换的方法前进行状态检查，避免程序运行产生预期以外的结果。

为保证UI线程不被阻塞，大部分AudioRenderer调用都是异步的。对于每个API均提供了callback函数和Promise函数，以下示例均采用callback函数。

**图1** AudioRenderer状态变化示意图

![AudioRenderer status change](figures/audiorenderer-status-change.png)

在进行应用开发的过程中，建议开发者通过[on('stateChange')](../../reference/apis-audio-kit/js-apis-audio.md#onstatechange-8)方法订阅AudioRenderer的状态变更。因为针对AudioRenderer的某些操作，仅在音频播放器在固定状态时才能执行。如果应用在音频播放器处于错误状态时执行操作，系统可能会抛出异常或生成其他未定义的行为。

- prepared状态： 通过调用[createAudioRenderer()](../../reference/apis-audio-kit/js-apis-audio.md#audiocreateaudiorenderer8)方法进入到该状态。

- running状态： 正在进行音频数据播放，可以在prepared状态通过调用[start()](../../reference/apis-audio-kit/js-apis-audio.md#start8)方法进入此状态，也可以在paused状态和stopped状态通过调用[start()](../../reference/apis-audio-kit/js-apis-audio.md#start8)方法进入此状态。

- paused状态： 在running状态可以通过调用[pause()](../../reference/apis-audio-kit/js-apis-audio.md#pause8)方法暂停音频数据的播放并进入paused状态，暂停播放之后可以通过调用[start()](../../reference/apis-audio-kit/js-apis-audio.md#start8)方法继续音频数据播放。

- stopped状态： 在paused/running状态可以通过[stop()](../../reference/apis-audio-kit/js-apis-audio.md#stop8)方法停止音频数据的播放。

- released状态： 在prepared、paused、stopped等状态，用户均可通过[release()](../../reference/apis-audio-kit/js-apis-audio.md#release8)方法释放掉所有占用的硬件和软件资源，并且不会再进入到其他的任何一种状态了。

### 开发步骤及注意事项

1. 配置音频渲染参数并创建AudioRenderer实例，音频渲染参数的详细信息可以查看[AudioRendererOptions](../../reference/apis-audio-kit/js-apis-audio.md#audiorendereroptions8)。
     
    ```ts
    import audio from '@ohos.multimedia.audio';

    let audioStreamInfo: audio.AudioStreamInfo = {
      samplingRate: audio.AudioSamplingRate.SAMPLE_RATE_48000, // 采样率
      channels: audio.AudioChannel.CHANNEL_2, // 通道
      sampleFormat: audio.AudioSampleFormat.SAMPLE_FORMAT_S16LE, // 采样格式
      encodingType: audio.AudioEncodingType.ENCODING_TYPE_RAW // 编码格式
    };

    let audioRendererInfo: audio.AudioRendererInfo = {
      usage: audio.StreamUsage.STREAM_USAGE_VOICE_COMMUNICATION,
      rendererFlags: 0
    };

    let audioRendererOptions: audio.AudioRendererOptions = {
      streamInfo: audioStreamInfo,
      rendererInfo: audioRendererInfo
    };

    audio.createAudioRenderer(audioRendererOptions, (err, data) => {
      if (err) {
        console.error(`Invoke createAudioRenderer failed, code is ${err.code}, message is ${err.message}`);
        return;
      } else {
        console.info('Invoke createAudioRenderer succeeded.');
        let audioRenderer = data;
      }
    });
    ```

2. 调用on('writeData')方法，订阅监听音频数据写入回调。
     
    ```ts
    import { BusinessError } from '@ohos.base';
    import fs from '@ohos.file.fs';

    let bufferSize: number = 0;
    class Options {
      offset?: number;
      length?: number;
    }

    let path = getContext().cacheDir;
    //确保该路径下存在该资源
    let filePath = path + '/StarWars10s-2C-48000-4SW.wav';
    let file: fs.File = fs.openSync(filePath, fs.OpenMode.READ_ONLY);
   
    let writeDataCallback = (buffer: ArrayBuffer) => {
      
      let options: Options = {
        offset: bufferSize,
        length: buffer.byteLength
      }
      fs.readSync(file.fd, buffer, options);
      bufferSize += buffer.byteLength;
    }

    audioRenderer.on('writeData', writeDataCallback);
    ```

3. 调用start()方法进入running状态，开始渲染音频。
     
    ```ts
    import { BusinessError } from '@ohos.base';

    audioRenderer.start((err: BusinessError) => {
      if (err) {
        console.error(`Renderer start failed, code is ${err.code}, message is ${err.message}`);
      } else {
        console.info('Renderer start success.');
      }
    });
    ```

4. 调用stop()方法停止渲染。
     
    ```ts
    import { BusinessError } from '@ohos.base';

    audioRenderer.stop((err: BusinessError) => {
      if (err) {
        console.error(`Renderer stop failed, code is ${err.code}, message is ${err.message}`);
      } else {
        console.info('Renderer stopped.');
      }
    });
    ```

5. 调用release()方法销毁实例，释放资源。
     
    ```ts
    import { BusinessError } from '@ohos.base';

    audioRenderer.release((err: BusinessError) => {
      if (err) {
        console.error(`Renderer release failed, code is ${err.code}, message is ${err.message}`);
      } else {
        console.info('Renderer released.');
      } 
    });
    ```

### 完整示例

下面展示了使用AudioRenderer渲染音频文件的示例代码。
  
```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';
import fs from '@ohos.file.fs';

const TAG = 'AudioRendererDemo';

class Options {
  offset?: number;
  length?: number;
}

let context = getContext(this);
let bufferSize: number = 0;
let renderModel: audio.AudioRenderer | undefined = undefined;
let audioStreamInfo: audio.AudioStreamInfo = {
  samplingRate: audio.AudioSamplingRate.SAMPLE_RATE_48000, // 采样率
  channels: audio.AudioChannel.CHANNEL_2, // 通道
  sampleFormat: audio.AudioSampleFormat.SAMPLE_FORMAT_S16LE, // 采样格式
  encodingType: audio.AudioEncodingType.ENCODING_TYPE_RAW // 编码格式
}
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC, // 音频流使用类型
  rendererFlags: 0 // 音频渲染器标志
}
let audioRendererOptions: audio.AudioRendererOptions = {
  streamInfo: audioStreamInfo,
  rendererInfo: audioRendererInfo
}
let path = getContext().cacheDir;
//确保该路径下存在该资源
let filePath = path + '/StarWars10s-2C-48000-4SW.wav';
let file: fs.File = fs.openSync(filePath, fs.OpenMode.READ_ONLY);

let writeDataCallback = (buffer: ArrayBuffer) => {
  let options: Options = {
    offset: bufferSize,
    length: buffer.byteLength
  }
  fs.readSync(file.fd, buffer, options);
   bufferSize += buffer.byteLength;
}

// 初始化，创建实例，设置监听事件
function init() {
  audio.createAudioRenderer(audioRendererOptions, (err, renderer) => { // 创建AudioRenderer实例
    if (!err) {
      console.info(`${TAG}: creating AudioRenderer success`);
      renderModel = renderer;
      if (renderModel !== undefined) {
        (renderModel as audio.AudioRenderer).on('writeData', writeDataCallback);
      }
    } else {
      console.info(`${TAG}: creating AudioRenderer failed, error: ${err.message}`);
    }
  });
}

// 开始一次音频渲染
function start() {
  if (renderModel !== undefined) {
    let stateGroup = [audio.AudioState.STATE_PREPARED, audio.AudioState.STATE_PAUSED, audio.AudioState.STATE_STOPPED];
    if (stateGroup.indexOf((renderModel as audio.AudioRenderer).state.valueOf()) === -1) { // 当且仅当状态为prepared、paused和stopped之一时才能启动渲染
      console.error(TAG + 'start failed');
      return;
    }
    // 启动渲染
    (renderModel as audio.AudioRenderer).start((err: BusinessError) => {
      if (err) {
        console.error('Renderer start failed.');
      } else {
        console.info('Renderer start success.');
      }
    });
  }
}

// 暂停渲染
function pause() {
  if (renderModel !== undefined) {
    // 只有渲染器状态为running的时候才能暂停
    if ((renderModel as audio.AudioRenderer).state.valueOf() !== audio.AudioState.STATE_RUNNING) {
      console.info('Renderer is not running');
      return;
    }
    // 暂停渲染
    (renderModel as audio.AudioRenderer).pause((err: BusinessError) => {
      if (err) {
        console.error('Renderer pause failed.');
      } else {
        console.info('Renderer pause success.');
      }
    });
  }
}

// 停止渲染
async function stop() {
  if (renderModel !== undefined) {
    // 只有渲染器状态为running或paused的时候才可以停止
    if ((renderModel as audio.AudioRenderer).state.valueOf() !== audio.AudioState.STATE_RUNNING && (renderModel as audio.AudioRenderer).state.valueOf() !== audio.AudioState.STATE_PAUSED) {
      console.info('Renderer is not running or paused.');
      return;
    }
    // 停止渲染
    (renderModel as audio.AudioRenderer).stop((err: BusinessError) => {
      if (err) {
        console.error('Renderer stop failed.');
      } else {
        fs.close(file);
        console.info('Renderer stop success.');
      }
    });
  }
}

// 销毁实例，释放资源
async function release() {
  if (renderModel !== undefined) {
    // 渲染器状态不是released状态，才能release
    if (renderModel.state.valueOf() === audio.AudioState.STATE_RELEASED) {
      console.info('Renderer already released');
      return;
    }
    // 释放资源
    (renderModel as audio.AudioRenderer).release((err: BusinessError) => {
      if (err) {
        console.error('Renderer release failed.');
      } else {
        console.info('Renderer release success.');
      }
    });
  }
}
```

当同优先级或高优先级音频流要使用输出设备时，当前音频流会被中断，应用可以自行响应中断事件并做出处理。具体的音频并发处理方式可参考[多音频播放的并发策略](audio-playback-concurrency.md)。
