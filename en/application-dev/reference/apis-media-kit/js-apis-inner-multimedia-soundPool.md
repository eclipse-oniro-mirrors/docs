# SoundPool (Sound Pool)

The **SoundPool** module provides APIs for loading, unloading, playing, and stopping playing system sounds, setting the volume, and setting the number of loops.

Before using these APIs, you must call [media.createSoundPool](js-apis-media.md#mediacreatesoundpool10) to create a **SoundPool** instance.

> **NOTE**
>
> The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```js
import media from '@ohos.multimedia.media';
import audio from '@ohos.multimedia.audio';
```

## PlayParameters

Describes the playback parameters of the sound pool.

These parameters are used to control the playback volume, number of loops, and priority.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

| Name           | Type                                    | Mandatory| Description                                                        |
| --------------- | ---------------------------------------- | ---- | ------------------------------------------------------------ |
| loop | number   | No | Number of loops. The value **0** means that the sound does not loop (the sound is played once), and **-1** means that the sound loops forever.                  |
| rate | number    | No | Playback rate. For details, see [AudioRendererRate](../apis-audio-kit/js-apis-audio.md#audiorendererrate8).|
| leftVolume  | number | No | Volume of the left channel. The value ranges from 0.0 to 1.0.                                   |
| rightVolume | number  | No | Volume of the right channel. (Currently, the volume cannot be set separately for the left and right channels. The volume set for the left channel is used.)|
| priority  | number  | No | Playback priority. The value **0** means the lowest priority. A larger value indicates a higher priority.     |

## SoundPool

Implements a sound pool that provides APIs for loading, unloading, playing, and stopping playing system sounds, setting the volume, and setting the number of loops. Before using these APIs, you must call [createSoundPool](js-apis-media.md#mediacreatesoundpool10) to create a **SoundPool** instance.

### load

load(uri: string, callback: AsyncCallback\<number>): void

Loads a sound. This API uses an asynchronous callback to obtain the sound ID. The input parameter **uri** is a string starting with fd://, which is generated based on the file descriptor (FD) obtained.

This API cannot be used to load resources in the **rawfile** directory. Instead, use **load(fd: number, offset: number, length: number, callback: AsyncCallback\<number>): void** or **load(fd: number, offset: number, length: number): Promise\<number>**.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type                                  | Mandatory| Description                                 |
| -------- | -------------------------------------- | ---- | ------------------------------------- |
| uri   | string | Yes  | URI of the audio file to load. Generally, the URI starts with fd://.|
| callback | AsyncCallback\<number>                   | Yes  | Callback used to return the sound ID. A valid value must be greater than 0.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 5400102  | Operation not allowed. Return by callback.|
| 5400103  | I/O error. Return by callback. |
| 5400105  | Service died. Return by callback. |

**Example**

```ts
import fs from '@ohos.file.fs';
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    let uri:string = "";
    let file: fs.File;
    // Obtain the URI starting with fd://.
    fs.open('/test_01.mp3', fs.OpenMode.READ_ONLY).then((file_: fs.File) => {
      file = file_;
      console.info("file fd: " + file.fd);
      uri = 'fd://' + (file.fd).toString()
      soundPool.load(uri, (error: BusinessError, soundId_: number) => {
        if (error) {
          console.error(`load soundPool Error: errCode is ${error.code}, errMessage is ${error.message}`)
        } else {
          console.info(`load soundPool Success` + JSON.stringify(soundId_))
        }
      });
    }); // '/test_01.mp3' here is only an example. You need to pass in the actual URI.
  }
});
```

### load

load(uri: string): Promise\<number>

Loads a sound. This API uses a promise to obtain the sound ID. The input parameter **uri** is a starting with fd://, which is generated based on the FD obtained.

This API cannot be used to load resources in the **rawfile** directory. Instead, use **load(fd: number, offset: number, length: number, callback: AsyncCallback\<number>): void** or **load(fd: number, offset: number, length: number): Promise\<number>**.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name| Type                                  | Mandatory| Description                      |
| ------ | -------------------------------------- | ---- | -------------------------- |
| uri | string | Yes  | URI of the audio file to load. Generally, the URI starts with fd://.|

**Return value**

| Type          | Description                                      |
| -------------- | ------------------------------------------ |
| Promise\<number> | Promise used to return the sound ID. A valid value must be greater than 0.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 5400102  | Operation not allowed. Return by promise.|
| 5400103  | I/O error. Return by promise. |
| 5400105  | Service died. Return by promise. |

**Example**

```ts
import fs from '@ohos.file.fs';
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    let uri:string = "";
    let soundID: number = 0;
    let file: fs.File;
    // Obtain the URI starting with fd://.
    fs.open('/test_01.mp3', fs.OpenMode.READ_ONLY).then((file_: fs.File) => {
      file = file_;
      console.info("file fd: " + file.fd);
      uri = 'fd://' + (file.fd).toString()
      soundPool.load(uri).then((soundId: number) => {
        console.info('soundPool load uri success');
        soundID = soundId;
      }, (err: BusinessError) => {
        console.error('soundPool load failed and catch error is ' + err.message);
      });
    }); // '/test_01.mp3' here is only an example. You need to pass in the actual URI.
  }
});

```

### load

load(fd: number, offset: number, length: number, callback: AsyncCallback\<number>): void

Loads a sound. This API uses an asynchronous callback to obtain the sound ID. The input parameter **fd** can be manually input or automatically obtained by reading the embedded resource of the application.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type                  | Mandatory| Description                       |
| -------- | ---------------------- | ---- | --------------------------- |
| fd     | number | Yes  | Resource handle, which is obtained by calling **resourceManager.getRawFileDescriptor**.    |
| offset | number | Yes  | Resource offset, which needs to be entered based on the preset resource information. An invalid value causes a failure to parse audio and video resources.|
| length | number | Yes  | Resource length, which needs to be entered based on the preset resource information. An invalid value causes a failure to parse audio and video resources.|
| callback | AsyncCallback\<number> | Yes  | Callback used to return the sound ID. A valid value must be greater than 0.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 5400102  | Operation not allowed. Return by callback. |
| 5400103  | I/O error. Return by callback. |
| 5400105  | Service died. Return by callback.       |

**Example**

```ts
import fs from '@ohos.file.fs';
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    let file: fs.File;
    let soundID: number = 0;
    let fileSize: number = 1; // Obtain the size through fs.stat().
    let uri: string = "";
    // Obtain the FD.
    fs.open('/test_01.mp3', fs.OpenMode.READ_ONLY).then((file_: fs.File) => {
      file = file_;
      console.info("file fd: " + file.fd);
      uri = 'fd://' + (file.fd).toString()
      soundPool.load(file.fd, 0, fileSize, (error: BusinessError, soundId_: number) => {
        if (error) {
          console.error(`load soundPool Error: errCode is ${error.code}, errMessage is ${error.message}`)
        } else {
          soundID = soundId_;
          console.info('load success soundid:' + soundId_);
        }
      });
    }); // '/test_01.mp3' here is only an example. You need to pass in the actual URI.
  }
});

```

### load

load(fd: number, offset: number, length: number): Promise\<number>

Loads a sound. This API uses a promise to obtain the sound ID. The input parameter **fd** can be manually input or automatically obtained by reading the embedded resource of the application.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type                  | Mandatory| Description                       |
| -------- | ---------------------- | ---- | --------------------------- |
| fd     | number | Yes  | Resource handle, which is obtained by calling **resourceManager.getRawFileDescriptor**.    |
| offset | number | Yes  | Resource offset, which needs to be entered based on the preset resource information. An invalid value causes a failure to parse audio and video resources.|
| length | number | Yes  | Resource length, which needs to be entered based on the preset resource information. An invalid value causes a failure to parse audio and video resources.|

**Return value**

| Type            | Description                            |
| ---------------- | -------------------------------- |
| Promise\<number> | Promise used to return the sound ID. A valid value must be greater than 0.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 5400102  | Operation not allowed. Return by promise.|
| 5400103  | I/O error. Return by promise. |
| 5400105  | Service died. Return by promise. |

**Example**

```ts
import fs from '@ohos.file.fs';
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    let file: fs.File;
    let soundID: number = 0;
    let fileSize: number = 1; // Obtain the size through fs.stat().
    let uri: string = "";
    // Obtain the FD.
    fs.open('/test_01.mp3', fs.OpenMode.READ_ONLY).then((file_: fs.File) => {
      file = file_;
      console.info("file fd: " + file.fd);
      uri = 'fd://' + (file.fd).toString()
      soundPool.load(file.fd, 0, fileSize).then((soundId: number) => {
        console.info('load success');
        soundID = soundId;
      }, (err: BusinessError) => {
        console.error('soundpool load failed and catch error is ' + err.message);
      });
    });
  }
});

```

### play

play(soundID: number, params: PlayParameters, callback: AsyncCallback\<number>): void

Plays a sound. This API uses an asynchronous callback to obtain the audio stream ID.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type                  | Mandatory| Description                       |
| -------- | ---------------------- | ---- | --------------------------- |
| soundID | number | Yes  | Sound ID, which is obtained by calling **load()**.|
| params | [PlayParameters](#playparameters) | Yes | Playback parameters.|
| callback | AsyncCallback\<number> | Yes  | Callback used to return the audio stream ID. A valid value must be greater than 0.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 401  | The parameter check failed. |
| 5400102  | Operation not allowed. Return by callback. |
| 5400105  | Service died. Return by callback.       |

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    let soundID: number = 0;
    let streamID: number = 0;
    let playParameters: media.PlayParameters = {
      loop: 3, // The sound loops three times.
      rate: audio.AudioRendererRate.RENDER_RATE_NORMAL, // The sound is played at the original frequency.
      leftVolume: 0.5, // range = 0.0-1.0
      rightVolume: 0.5, // range = 0.0-1.0
      priority: 0, // The sound playback has the lowest priority.
    }
    soundPool.play(soundID, playParameters, (error: BusinessError, streamId: number) => {
      if (error) {
        console.error(`play sound Error: errCode is ${error.code}, errMessage is ${error.message}`)
      } else {
        streamID = streamId;
        console.info('play success soundid:' + streamId);
      }
    });
  }
});

```

### play

play(soundID: number, callback: AsyncCallback\<number>): void

Plays a sound. This API uses an asynchronous callback to obtain the audio stream ID.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type                  | Mandatory| Description                       |
| -------- | ---------------------- | ---- | --------------------------- |
| soundID | number | Yes  | Sound ID, which is obtained by calling **load()**.|
| callback | AsyncCallback\<number> | Yes  | Callback used to return the audio stream ID. A valid value must be greater than 0.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 401  | The parameter check failed. |
| 5400102  | Operation not allowed. Return by callback. |
| 5400105  | Service died. Return by callback.       |

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    let soundID: number = 0;
    let streamID: number = 0;
    soundPool.play(soundID,  (error: BusinessError, streamId: number) => {
      if (error) {
        console.error(`play sound Error: errCode is ${error.code}, errMessage is ${error.message}`)
      } else {
        streamID = streamId;
        console.info('play success soundid:' + streamId);
      }
    });
  }
});

```

### play

play(soundID: number, params?: PlayParameters): Promise\<number>

Plays a sound. This API uses a promise to obtain the audio stream ID.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type                  | Mandatory| Description                       |
| -------- | ---------------------- | ---- | --------------------------- |
| soundID | number | Yes  | Sound ID, which is obtained by calling **load()**.|
| params | [PlayParameters](#playparameters) | No | Playback parameters.|

**Return value**

| Type            | Description                            |
| ---------------- | -------------------------------- |
| Promise\<number> | Promise used to return the audio stream ID. A valid value must be greater than 0.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 401  | The parameter check failed. |
| 5400102  | Operation not allowed. Return by promise. |
| 5400105  | Service died. Return by promise.       |

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    let soundID: number = 0;
    let streamID: number = 0;
    let playParameters: media.PlayParameters = {
      loop: 3, // The sound is played four times (three loops).
      rate: audio.AudioRendererRate.RENDER_RATE_NORMAL, // The sound is played at the original frequency.
      leftVolume: 0.5, // range = 0.0-1.0
      rightVolume: 0.5, // range = 0.0-1.0
      priority: 0, // The sound playback has the lowest priority.
    }

    soundPool.play(soundID, playParameters).then((streamId: number) => {
      console.info('play success');
      streamID = streamId;
    },(err: BusinessError) => {
      console.error('soundpool play failed and catch error is ' + err.message);
    });
  }
});

```

### stop

stop(streamID: number, callback: AsyncCallback\<void>): void

Stops playing a sound. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type                  | Mandatory| Description                       |
| -------- | ---------------------- | ---- | --------------------------- |
| streamID | number | Yes  | Audio stream ID, which is obtained by calling **play()**.|
| callback | AsyncCallback\<void> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 401  | The parameter check failed. |
| 5400102  | Operation not allowed. Return by callback. |
| 5400105  | Service died. Return by callback.       |

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    let streamID: number = 0;
    // Call play() to obtain the stream ID.
    soundPool.stop(streamID, (error: BusinessError) => {
      if (error) {
        console.error(`stop sound Error: errCode is ${error.code}, errMessage is ${error.message}`)
      } else {
        console.info('stop success');
      }
    })
  }
});

```

### stop

stop(streamID: number): Promise\<void>

Stops playing a sound. This API uses a promise to return the result.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type                  | Mandatory| Description                       |
| -------- | ---------------------- | ---- | --------------------------- |
| streamID | number | Yes  | Audio stream ID, which is obtained by calling **play()**.|

**Return value**

| Type            | Description                            |
| ---------------- | -------------------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 401  | The parameter check failed. |
| 5400102  | Operation not allowed. Return by promise. |
| 5400105  | Service died. Return by promise.       |

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    let streamID: number = 0;
    // Call play() to obtain the stream ID.
    soundPool.stop(streamID).then(() => {
      console.info('stop success');
    }, (err: BusinessError) => {
      console.error('soundpool load stop and catch error is ' + err.message);
    });
  }
});
```

### setLoop

setLoop(streamID: number, loop: number, callback: AsyncCallback\<void>): void;

Sets the loop mode for an audio stream. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type                  | Mandatory| Description                       |
| -------- | ---------------------- | ---- | --------------------------- |
| streamID | number | Yes  | Audio stream ID, which is obtained by calling **play()**.|
| loop | number | Yes  | Number of loops. The value **0** means that the sound does not loop (the sound is played once), and **-1** means that the sound loops forever.|
| callback | AsyncCallback\<void> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 401  | The parameter check failed. |
| 5400102  | Operation not allowed. Return by callback. |
| 5400105  | Service died. Return by callback.       |

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    let streamID: number = 0;
    // Call play() to obtain the stream ID.
    // Set the number of loops to 2.
    soundPool.setLoop(streamID, 2, (error: BusinessError) => {
      if (error) {
        console.error(`setLoop soundPool Error: errCode is ${error.code}, errMessage is ${error.message}`)
      } else {
        console.info('setLoop success streamID:' + streamID);
      }
    });
  }
});

```

### setLoop

setLoop(streamID: number, loop: number): Promise\<void>

Sets the loop mode for an audio stream. This API uses a promise to return the result.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type                  | Mandatory| Description                       |
| -------- | ---------------------- | ---- | --------------------------- |
| streamID | number | Yes  | Audio stream ID, which is obtained by calling **play()**.|
| loop | number | Yes  | Number of loops. The value **0** means that the sound does not loop (the sound is played once), and **-1** means that the sound loops forever.|

**Return value**

| Type            | Description                            |
| ---------------- | -------------------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 401  | The parameter check failed. |
| 5400102  | Operation not allowed. Return by promise. |
| 5400105  | Service died. Return by promise.       |

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    let streamID: number = 0;
    // Call play() to obtain the stream ID.
    // Set the number of loops to 1.
    soundPool.setLoop(streamID, 1).then(() => {
      console.info('setLoop success streamID:' + streamID);
    }).catch((err: BusinessError) => {
      console.error('soundpool setLoop failed and catch error is ' + err.message);
    });
  }
});

```

### setPriority

setPriority(streamID: number, priority: number, callback: AsyncCallback\<void>): void

Sets the priority for an audio stream. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type                  | Mandatory| Description                       |
| -------- | ---------------------- | ---- | --------------------------- |
| streamID | number | Yes  | Audio stream ID, which is obtained by calling **play()**.|
| priority | number | Yes  | Priority. The value **0** means the lowest priority.|
| callback | AsyncCallback\<void> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 401  | The parameter check failed. |
| 5400102  | Operation not allowed. Return by callback. |
| 5400105  | Service died. Return by callback.       |

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    let streamID: number = 0;
    // Call play() to obtain the stream ID.
    // Set the priority to 1.
    soundPool.setPriority(streamID, 1, (error: BusinessError) => {
      if (error) {
        console.error(`setPriority soundPool Error: errCode is ${error.code}, errMessage is ${error.message}`)
      } else {
        console.info('setPriority success streamID:' + streamID);
      }
    });
  }
});

```

### setPriority

setPriority(streamID: number, priority: number): Promise\<void>

Sets the priority for an audio stream. This API uses a promise to return the result.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type                  | Mandatory| Description                       |
| -------- | ---------------------- | ---- | --------------------------- |
| streamID | number | Yes  | Audio stream ID, which is obtained by calling **play()**.|
| priority | number | Yes  | Priority. The value **0** means the lowest priority.|

**Return value**

| Type            | Description                            |
| ---------------- | -------------------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 401  | The parameter check failed. |
| 5400102  | Operation not allowed. Return by promise. |
| 5400105  | Service died. Return by promise.       |

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    let streamID: number = 0;
    // Call play() to obtain the stream ID.
    // Set the priority to 1.

    soundPool.setPriority(streamID, 1).then(() => {
      console.info('setPriority success');
    }, (err: BusinessError) => {
      console.error('soundpool setPriority failed and catch error is ' + err.message);
    });
  }
});

```

### setRate

setRate(streamID: number, rate: audio.AudioRendererRate, callback: AsyncCallback\<void>): void

Sets the playback rate for an audio stream. This API uses an asynchronous callback to return the result.

> **NOTE**
> This API is available in OpenHarmony 4.0. The function implementation depends on the device. Currently, only the RK3568 development board supports the playback rate setting.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type                  | Mandatory| Description                       |
| -------- | ---------------------- | ---- | --------------------------- |
| streamID | number | Yes  | Audio stream ID, which is obtained by calling **play()**.|
| rate | [audio.AudioRendererRate](../apis-audio-kit/js-apis-audio.md#audiorendererrate8) | Yes  | Playback rate.|
| callback | AsyncCallback\<void> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 401  | The parameter check failed. |
| 5400102  | Operation not allowed. Return by callback. |
| 5400105  | Service died. Return by callback.       |

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    let streamID: number = 0;
    let selectedAudioRendererRate: audio.AudioRendererRate = audio.AudioRendererRate.RENDER_RATE_NORMAL; // The sound is played at the original frequency.
    // Call play() to obtain the stream ID.
    soundPool.setRate(streamID, selectedAudioRendererRate, (error: BusinessError) => {
      if (error) {
        console.error(`setRate soundPool Error: errCode is ${error.code}, errMessage is ${error.message}`)
      } else {
        console.info('setRate success streamID:' + streamID);
      }
    })
  }
});

```

### setRate

setRate(streamID: number, rate: audio.AudioRendererRate): Promise\<void>

Sets the playback rate for an audio stream. This API uses a promise to return the result.

> **NOTE**
> This API is available in OpenHarmony 4.0. The function implementation depends on the device. Currently, only the RK3568 development board supports the playback rate setting.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type                  | Mandatory| Description                       |
| -------- | ---------------------- | ---- | --------------------------- |
| streamID | number | Yes  | Audio stream ID, which is obtained by calling **play()**.|
| rate | [audio.AudioRendererRate](../apis-audio-kit/js-apis-audio.md#audiorendererrate8) | Yes  | Playback rate.|

**Return value**

| Type            | Description                            |
| ---------------- | -------------------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 401  | The parameter check failed. |
| 5400102  | Operation not allowed. Return by promise. |
| 5400105  | Service died. Return by promise.       |

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    let streamID: number = 0;
    let selectedAudioRendererRate: audio.AudioRendererRate = audio.AudioRendererRate.RENDER_RATE_NORMAL; // The sound is played at the original frequency.
    // Call play() to obtain the stream ID.
    soundPool.setRate(streamID, selectedAudioRendererRate).then(() => {
      console.info('setRate success');
    }, (err: BusinessError) => {
      console.error('soundpool setRate failed and catch error is ' + err.message);
    });
  }
});

```

### setVolume

setVolume(streamID: number, leftVolume: number, rightVolume: number, callback: AsyncCallback\<void>): void

Sets the volume for an audio stream. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type                  | Mandatory| Description                       |
| -------- | ---------------------- | ---- | --------------------------- |
| streamID | number | Yes  | Audio stream ID, which is obtained by calling **play()**.|
| leftVolume | number | Yes  | Volume of the left channel. The value ranges from 0.0 to 1.0.|
| rightVolume | number | Yes  | Volume of the right channel. Currently, setting the volume for the right channel does not take effect. The volume set for the left channel is used.|
| callback | AsyncCallback\<void> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 401  | The parameter check failed. |
| 5400102  | Operation not allowed. Return by callback. |
| 5400105  | Service died. Return by callback.       |

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    let streamID: number = 0;
    // Call play() to obtain the stream ID.
    // Set the volume to 0.5.
    soundPool.setVolume(streamID, 0.5, 0.5, (error: BusinessError) => {
      if (error) {
        console.error(`setVolume soundPool Error: errCode is ${error.code}, errMessage is ${error.message}`)
      } else {
        console.info('setVolume success streamID:' + streamID);
      }
    })
  }
});

```

### setVolume

setVolume(streamID: number, leftVolume: number, rightVolume: number): Promise\<void>

Sets the volume for an audio stream. This API uses a promise to return the result.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type                  | Mandatory| Description                       |
| -------- | ---------------------- | ---- | --------------------------- |
| streamID | number | Yes  | Audio stream ID, which is obtained by calling **play()**.|
| leftVolume | number | Yes  | Volume of the left channel. The value ranges from 0.0 to 1.0.|
| rightVolume | number | Yes  | Volume of the right channel. Currently, setting the volume for the right channel does not take effect. The volume set for the left channel is used.|

**Return value**

| Type            | Description                            |
| ---------------- | -------------------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 401  | The parameter check failed. |
| 5400102  | Operation not allowed. Return by promise. |
| 5400105  | Service died. Return by promise.       |

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    let streamID: number = 0;
    // Call play() to obtain the stream ID.

    soundPool.setVolume(streamID, 0.5, 0.5).then(() => {
      console.info('setVolume success');
    }, (err: BusinessError) => {
      console.error('soundpool setVolume failed and catch error is ' + err.message);
    });
  }
});

```

### unload

unload(soundID: number, callback: AsyncCallback\<void>): void

Unloads a sound. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type                  | Mandatory| Description                       |
| -------- | ---------------------- | ---- | --------------------------- |
| soundID | number | Yes  | Sound ID, which is obtained by calling **load()**.|
| callback | AsyncCallback\<void> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 5400102  | Operation not allowed. Return by callback. |
| 5400103  | I/O error. Return by callback. |
| 5400105  | Service died. Return by callback.       |

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    let soundID: number = 0;
    // Call load() to obtain the sound ID.
    soundPool.unload(soundID, (error: BusinessError) => {
      if (error) {
        console.error(`unload soundPool Error: errCode is ${error.code}, errMessage is ${error.message}`)
      } else {
        console.info('unload success:');
      }
    })
  }
});

```

### unload

unload(soundID: number): Promise\<void>

Unloads a sound. This API uses a promise to return the result.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type                  | Mandatory| Description                       |
| -------- | ---------------------- | ---- | --------------------------- |
| soundID | number | Yes  | Sound ID, which is obtained by calling **load()**.|

**Return value**

| Type            | Description                            |
| ---------------- | -------------------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 5400102  | Operation not allowed. Return by promise. |
| 5400103  | I/O error. Return by promise. |
| 5400105  | Service died. Return by promise.       |

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    let soundID: number = 0;
    // Call load() to obtain the sound ID.

    soundPool.unload(soundID).then(() => {
      console.info('unload success');
    }, (err: BusinessError) => {
      console.error('soundpool unload failed and catch error is ' + err.message);
    });
  }
});

```

### release

release(callback: AsyncCallback\<void>): void

Releases this **SoundPool** instance. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type                  | Mandatory| Description                       |
| -------- | ---------------------- | ---- | --------------------------- |
| callback | AsyncCallback\<void> | Yes  | Callback used to return the result.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 5400105  | Service died. Return by callback.       |

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    soundPool.release((error: BusinessError) => {
      if (error) {
        console.error(`release soundPool Error: errCode is ${error.code}, errMessage is ${error.message}`)
      } else {
        console.info('release success');
      }
    })
  }
});


```

### release

release(): Promise\<void>

Releases this **SoundPool** instance. This API uses a promise to return the result.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Return value**

| Type            | Description                            |
| ---------------- | -------------------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Media Error Codes](errorcode-media.md).

| ID| Error Message                               |
| -------- | --------------------------------------- |
| 5400105  | Service died. Return by promise.       |

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    soundPool.release().then(() => {
      console.info('release success');
    }, (err: BusinessError) => {
      console.error('soundpool release failed and catch error is ' + err.message);
    });
  }
});

```

### on('loadComplete')

on(type: 'loadComplete', callback: Callback\<number>): void

Subscribes to events indicating that a sound finishes loading.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type    | Mandatory| Description                                                        |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | Yes  | Event type, which is **'loadComplete'** in this case. This event is triggered when a sound is loaded.|
| callback | Callback\<number> | Yes  | ID of the sound that has been loaded.                              |

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    soundPool.on('loadComplete', (soundId: number) => {
      console.info('loadComplete success, soundId: ' + soundId)
    })
  }
});

```

### off('loadComplete')

off(type: 'loadComplete'): void

Unsubscribes from events indicating that a sound finishes loading.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name| Type  | Mandatory| Description                                                        |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| type   | string | Yes  | Event type. The value is fixed at **'loadComplete'**.|

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    soundPool.off('loadComplete')
  }
});

```

### on('playFinished')

on(type: 'playFinished', callback: Callback\<void>): void

Subscribes to events indicating that a sound finishes playing.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type    | Mandatory| Description                                                        |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | Yes  | Event type, which is **'playFinished'** in this case. This event is triggered when a sound finishes playing.|
| callback | Callback\<void> | Yes  |  Callback used to return the result.       |

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    soundPool.on('playFinished', () => {
      console.info('playFinished success')
    });
  }
});

```

### off('playFinished')

off(type: 'playFinished'): void

Unsubscribes from events indicating that a sound finishes playing.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name| Type  | Mandatory| Description                                                        |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| type   | string | Yes  | Event type. The value is fixed at **'playFinished'**.|

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    soundPool.off('playFinished')
  }
});

```

### on('error')

on(type: 'error', callback: ErrorCallback): void

Subscribes to error events of this **SoundPool** instance. This event is used only for error prompt.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name  | Type    | Mandatory| Description                                                        |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| type     | string   | Yes  | Event type, which is **'error'** in this case. This event can be triggered by both user operations and the system.|
| callback | ErrorCallback | Yes  | Callback used to return the error code ID and error message.|

The **SoundPool** class provides the following error types<a name = error_info></a>:

| ID| Error Message             | Description                                                        |
| -------- | --------------------- | ------------------------------------------------------------ |
| 401      | Invalid Parameter.    | Incorrect input parameter, causing an invalid call.                                    |
| 801      | Unsupport Capability. | Unsupported API, causing an invalid call.                             |
| 5400101  | No Memory.            | Insufficient memory.|
| 5400102  | Operation Not Allowed.   | Unsupported operation in the current state, causing an invalid call.                      |
| 5400103  | IO Error.             | I/O exception.|
| 5400105  | Service Died.         | The playback process is dead, and the service on which the sound pool depends is abnormal.|

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    soundPool.on('error', (error: BusinessError) => {
      console.error('error happened,and error message is :' + error.message)
      console.error('error happened,and error code is :' + error.code)
    })
  }
});

```

### off('error')

off(type: 'error'): void

Unsubscribes from error events of this **SoundPool** instance.

**System capability**: SystemCapability.Multimedia.Media.SoundPool

**Parameters**

| Name| Type  | Mandatory| Description                                     |
| ------ | ------ | ---- | ----------------------------------------- |
| type   | string | Yes  | Event type, which is **'error'** in this case.|

**Example**

```js
import { BusinessError } from '@ohos.base';

// Create a SoundPool instance.
let soundPool: media.SoundPool;
let audioRendererInfo: audio.AudioRendererInfo = {
  usage: audio.StreamUsage.STREAM_USAGE_MUSIC,
  rendererFlags: 1
}
media.createSoundPool(5, audioRendererInfo, (error: BusinessError, soundPool_: media.SoundPool) => {
  if (error) {
    console.error(`createSoundPool failed`)
    return;
  } else {
    soundPool = soundPool_;
    console.info(`createSoundPool success`)
    soundPool.off('error')
  }
});
```
