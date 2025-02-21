# @ohos.multimedia.audio (Audio Management) (System API)

The **Audio** module provides basic audio management capabilities, including audio volume and audio device management, and audio data collection and rendering.

This module provides the following common audio-related functions:

- [AudioManager](#audiomanager): audio management.
- [TonePlayer](#toneplayer9): tone player, used to manage and play Dual Tone Multi Frequency (DTMF) tones, such as dial tones and ringback tones.

> **NOTE**
>
> - The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> - This topic describes only system APIs provided by the module. For details about its public APIs, see [@ohos.multimedia.audio (Audio Management)](js-apis-audio.md).

## Modules to Import

```ts
import audio from '@ohos.multimedia.audio';
```

## Constants

| Name                                   | Type     | Readable | Writable| Description              |
| --------------------------------------- | ----------| ---- | ---- | ------------------ |
| LOCAL_NETWORK_ID<sup>9+</sup>           | string    | Yes  | No  | Network ID of the local device.<br>This is a system API.<br>**System capability**: SystemCapability.Multimedia.Audio.Device |

## audio.createTonePlayer<sup>9+</sup>

createTonePlayer(options: AudioRendererInfo, callback: AsyncCallback&lt;TonePlayer&gt;): void

Creates a **TonePlayer** instance. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Multimedia.Audio.Tone

**System API**: This is a system API.

**Parameters**

| Name  | Type                                            | Mandatory| Description           |
| -------- | ----------------------------------------------- | ---- | -------------- |
| options  | [AudioRendererInfo](js-apis-audio.md#audiorendererinfo8)        | Yes  | Audio renderer information.|
| callback | AsyncCallback<[TonePlayer](#toneplayer9)>       | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined** and **data** is the **TonePlayer** instance obtained; otherwise, **err** is an error object.|

**Example**

```ts
import audio from '@ohos.multimedia.audio';

let audioRendererInfo: audio.AudioRendererInfo = {
  usage : audio.StreamUsage.STREAM_USAGE_DTMF,
  rendererFlags : 0
}
let tonePlayer: audio.TonePlayer;

audio.createTonePlayer(audioRendererInfo, (err, data) => {
  console.info(`callback call createTonePlayer: audioRendererInfo: ${audioRendererInfo}`);
  if (err) {
    console.error(`callback call createTonePlayer return error: ${err.message}`);
  } else {
    console.info(`callback call createTonePlayer return data: ${data}`);
    tonePlayer = data;
  }
});
```

## audio.createTonePlayer<sup>9+</sup>

createTonePlayer(options: AudioRendererInfo): Promise&lt;TonePlayer&gt;

Creates a **TonePlayer** instance. This API uses a promise to return the result.

**System capability**: SystemCapability.Multimedia.Audio.Tone

**System API**: This is a system API.

**Parameters**

| Name | Type                                          | Mandatory| Description        |
| :------ | :---------------------------------------------| :--- | :----------- |
| options | [AudioRendererInfo](js-apis-audio.md#audiorendererinfo8)      | Yes  | Audio renderer information.|

**Return value**

| Type                                     | Description                            |
| ----------------------------------------- | -------------------------------- |
| Promise<[TonePlayer](#toneplayer9)>       | Promise used to return the **TonePlayer** instance.|

**Example**

```ts
import audio from '@ohos.multimedia.audio';

let tonePlayer: audio.TonePlayer;
async function createTonePlayerBefore(){
  let audioRendererInfo: audio.AudioRendererInfo = {
    usage : audio.StreamUsage.STREAM_USAGE_DTMF,
    rendererFlags : 0
  }
  tonePlayer = await audio.createTonePlayer(audioRendererInfo);
}
```

## AudioVolumeType

Enumerates the audio stream types.

**System capability**: SystemCapability.Multimedia.Audio.Volume

| Name                        | Value     | Description      |
| ---------------------------- | ------ | ---------- |
| ULTRASONIC<sup>10+</sup>     | 10     | Audio stream for ultrasonic.<br>This is a system API.|
| ALL<sup>9+</sup>             | 100    | All public audio streams.<br>This is a system API.|

## InterruptRequestResultType<sup>9+</sup>

Enumerates the result types of audio interruption requests.

**System capability**: SystemCapability.Multimedia.Audio.Interrupt

**System API**: This is a system API.

| Name                        | Value     | Description      |
| ---------------------------- | ------ | ---------- |
| INTERRUPT_REQUEST_GRANT      | 0      | The audio interruption request is accepted.|
| INTERRUPT_REQUEST_REJECT     | 1      | The audio interruption request is denied. There may be a stream with a higher priority.|

## DeviceFlag

Enumerates the audio device flags.

**System capability**: SystemCapability.Multimedia.Audio.Device

| Name                           |  Value    | Description                       |
| ------------------------------- | ------ |---------------------------|
| NONE_DEVICES_FLAG<sup>9+</sup>  | 0      | No device is available.<br>This is a system API.       |
| DISTRIBUTED_OUTPUT_DEVICES_FLAG<sup>9+</sup> | 4   | Distributed output device.<br>This is a system API.   |
| DISTRIBUTED_INPUT_DEVICES_FLAG<sup>9+</sup>  | 8   | Distributed input device.<br>This is a system API.   |
| ALL_DISTRIBUTED_DEVICES_FLAG<sup>9+</sup>    | 12  | Distributed input and output device.<br>This is a system API.|

## DeviceUsage<sup>11+</sup>

Enumerates the audio device flags.

**System capability**: SystemCapability.Multimedia.Audio.Device

**System API**: This is a system API.

| Name                           |  Value    | Description                       |
| ------------------------------- | ------ |---------------------------|
| MEDIA_OUTPUT_DEVICES<sup>11+</sup> | 1      | Media output device.|
| MEDIA_INPUT_DEVICES<sup>11+</sup>  | 2      | Media input device.|
| ALL_MEDIA_DEVICES<sup>11+</sup>    | 3      | All media devices.|
| CALL_OUTPUT_DEVICES<sup>11+</sup>  | 4      | Call output device.|
| CALL_INPUT_DEVICES<sup>11+</sup>   | 8      | Call input device.|
| ALL_CALL_DEVICES<sup>11+</sup>     | 12     | All call devices.|

## StreamUsage

Enumerates the audio stream usage.

**System capability**: SystemCapability.Multimedia.Audio.Core

| Name                                     |  Value   | Description                                                                                                                                         |
| ------------------------------------------| ------ |---------------------------------------------------------------------------------------------------------------------------------------------|
| STREAM_USAGE_SYSTEM<sup>10+</sup>         | 9      | System tone (such as screen lock sound effect or key tone).<br>This is a system API. |
| STREAM_USAGE_DTMF<sup>10+</sup>           | 14     | Dial tone.<br>This is a system API.   |
| STREAM_USAGE_ENFORCED_TONE<sup>10+</sup>  | 15     | Forcible tone (such as camera shutter sound effect).<br>This is a system API.  |
| STREAM_USAGE_ULTRASONIC<sup>10+</sup>     | 16     | Ultrasonic (currently provided only for MSDP).<br>This is a system API.|

## InterruptRequestType<sup>9+</sup>

Enumerates the audio interruption request types.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Interrupt

| Name                              |  Value    | Description                      |
| ---------------------------------- | ------ | ------------------------- |
| INTERRUPT_REQUEST_TYPE_DEFAULT     | 0      |  Default type, which can be used to interrupt audio requests. |

## InterruptResult<sup>9+</sup>

Describes the audio interruption result.

**System capability**: SystemCapability.Multimedia.Audio.Interrupt

**System API**: This is a system API.

| Name         | Type                                                           | Mandatory| Description            |
| --------------| -------------------------------------------------------------- | ---- | ---------------- |
| requestResult | [InterruptRequestResultType](#interruptrequestresulttype9)     | Yes  | Audio interruption request type.|
| interruptNode | number                                                         | Yes  | Node to interrupt.|

## VolumeEvent<sup>9+</sup>

Describes the event received by the application when the volume is changed.

**System capability**: SystemCapability.Multimedia.Audio.Volume

| Name      | Type                               | Mandatory  | Description                                       |
| ---------- | ----------------------------------- | ---- |-------------------------------------------|
| volumeGroupId | number                           | Yes  | Volume group ID. It can be used as an input parameter of **getGroupManager**.<br>This is a system API.|
| networkId  | string                              | Yes  | Network ID.<br>This is a system API.   |

## ConnectType<sup>9+</sup>

Enumerates the types of connected devices.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Volume

| Name                           |  Value    | Description                  |
| :------------------------------ | :----- | :--------------------- |
| CONNECT_TYPE_LOCAL              | 1      | Local device.        |
| CONNECT_TYPE_DISTRIBUTED        | 2      | Distributed device.           |

## VolumeGroupInfos<sup>9+</sup>

Describes the volume group information. The value is an array of [VolumeGroupInfo](#volumegroupinfo9) and is read-only.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Volume

## VolumeGroupInfo<sup>9+</sup>

Describes the volume group information.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Volume

| Name                       | Type                      | Readable| Writable| Description      |
| -------------------------- | -------------------------- | ---- | ---- | ---------- |
| networkId<sup>9+</sup>     | string                     | Yes  | No  | Network ID of the device. |
| groupId<sup>9+</sup>       | number                     | Yes  | No  | Group ID of the device.|
| mappingId<sup>9+</sup>     | number                     | Yes  | No  | Group mapping ID.|
| groupName<sup>9+</sup>     | string                     | Yes  | No  | Group name.|
| type<sup>9+</sup>          | [ConnectType](#connecttype9)| Yes  | No  | Type of the connected device.|

## SourceType<sup>8+</sup>

Enumerates the audio source types.

| Name                                        |  Value    | Description                  |
| :------------------------------------------- | :----- | :--------------------- |
| SOURCE_TYPE_WAKEUP <sup>10+</sup>            | 3 | Audio recording source in voice wake-up scenarios.<br>**System capability**: SystemCapability.Multimedia.Audio.Core<br>**Required permissions**: ohos.permission.MANAGE_INTELLIGENT_VOICE <br> This is a system API.|
| SOURCE_TYPE_VOICE_CALL<sup>11+</sup>            | 4 | Audio source in voice calls.<br>**System capability**: SystemCapability.Multimedia.Audio.Core<br>**Required permissions**: ohos.permission.RECORD_VOICE_CALL <br> This is a system API.|

## AudioScene<sup>8+</sup>

Enumerates the audio scenes.

**System capability**: SystemCapability.Multimedia.Audio.Communication

| Name                  |  Value    | Description                                         |
| :--------------------- | :----- | :-------------------------------------------- |
| AUDIO_SCENE_RINGING    | 1      | Ringing audio scene.<br>This is a system API.|
| AUDIO_SCENE_PHONE_CALL | 2      | Phone call audio scene.<br>This is a system API.|

## VolumeAdjustType<sup>10+</sup>

Enumerates the volume adjustment types.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Volume

| Name                  |  Value    | Description                                         |
| :--------------------- | :----- | :-------------------------------------------- |
| VOLUME_UP              | 0      | Adjusts the volume upwards.<br>This is a system API.  |
| VOLUME_DOWN            | 1      | Adjusts the volume downwards.<br>This is a system API.  |

## AudioManager

Implements audio volume and audio device management. Before calling any API in **AudioManager**, you must use [getAudioManager](js-apis-audio.md#audiogetaudiomanager) to create an **AudioManager** instance.

### setExtraParameters<sup>11+</sup>

setExtraParameters(mainKey: string, kvpairs: Record<string, string\>): Promise&lt;void&gt;

Sets extended audio parameters. This API uses a promise to return the result.

**Required permissions**: ohos.permission.MODIFY_AUDIO_SETTINGS

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Core

**Parameters**

| Name| Type  | Mandatory| Description                  |
| ------ | ------ | ---- | ---------------------- |
| mainKey | string | Yes  | Main key of the audio parameter to set.|
| kvpairs | Record<string, string\> | Yes  | Sub-KV pair of the audio parameter to set.|

**Return value**

| Type               | Description                           |
| ------------------- | ------------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message                                                                                                      |
|-----|------------------------------------------------------------------------------------------------------------|
| 6800101 | Invalid parameter error. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let kvpairs = {} as Record<string, string>;
kvpairs = {
  'key_example': 'value_example'
}
audioManager.setExtraParameters('key_example', kvpairs).then(() => {
  console.info('Promise returned to indicate a successful setting of the extra parameters.');
}).catch ((err: BusinessError) => {
    console.error(`Failed to set the audio extra parameters ${err}`);
});
```

### getExtraParameters<sup>11+</sup>

getExtraParameters(mainKey: string, subKeys?: Array\<string>): Promise\<Record\<string, string>>

Obtains the value of an audio parameter. This API uses a promise to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Core

**Parameters**

| Name| Type  | Mandatory| Description                  |
| ------ | ------ |--| ---------------------- |
| mainKey | string | Yes| Main key of the audio parameter whose value is to be obtained.|
| subKeys | Array\<string> | No| Subkey of the audio parameter whose value is to be obtained.|

**Return value**

| Type                 | Description                               |
| --------------------- | ----------------------------------- |
| Promise\<Record\<string, string>> | Promise used to return the value of the audio parameter.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------ | -------------------------|
| 6800101 | Invalid parameter error. |

**Example**

```ts
import { BusinessError } from '@ohos.base';

let subKeys: Array<String> = ['key_example'];
audioManager.getExtraParameters('key_example', subKeys).then((value: Record<string, string>) => {
  console.info(`Promise returned to indicate that the value of the audio extra parameters is obtained ${value}.`);
}).catch ((err: BusinessError) => {
    console.error(`Failed to get the audio extra parameters ${err}`);
});
```

### setAudioScene<sup>8+</sup>

setAudioScene\(scene: AudioScene, callback: AsyncCallback<void\>\): void

Sets an audio scene. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Communication

**Parameters**

| Name  | Type                                | Mandatory| Description                |
| :------- | :----------------------------------- | :--- | :------------------- |
| scene    | [AudioScene](#audioscene8) | Yes  | Audio scene to set.      |
| callback | AsyncCallback<void\>                 | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**; otherwise, **err** is an error object.|

**Example**

```ts
import { BusinessError } from '@ohos.base';

audioManager.setAudioScene(audio.AudioScene.AUDIO_SCENE_PHONE_CALL, (err: BusinessError) => {
  if (err) {
    console.error(`Failed to set the audio scene mode. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate a successful setting of the audio scene mode.');
});
```

### setAudioScene<sup>8+</sup>

setAudioScene\(scene: AudioScene\): Promise<void\>

Sets an audio scene. This API uses a promise to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Communication

**Parameters**

| Name| Type                                | Mandatory| Description          |
| :----- | :----------------------------------- | :--- | :------------- |
| scene  | [AudioScene](#audioscene8) | Yes  | Audio scene to set.|

**Return value**

| Type          | Description                |
| :------------- | :------------------- |
| Promise<void\> | Promise that returns no value.|

**Example**

```ts
import { BusinessError } from '@ohos.base';

audioManager.setAudioScene(audio.AudioScene.AUDIO_SCENE_PHONE_CALL).then(() => {
  console.info('Promise returned to indicate a successful setting of the audio scene mode.');
}).catch ((err: BusinessError) => {
  console.error(`Failed to set the audio scene mode ${err}`);
});
```

### getSpatializationManager<sup>11+</sup>

getSpatializationManager(): AudioSpatializationManager

Obtains an **AudioSpatializationManager** instance.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Spatialization

**Return value**

| Type                                      | Description                         |
|------------------------------------------| ----------------------------- |
| [AudioSpatializationManager](#audiospatializationmanager11) | **AudioSpatializationManager** instance.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 202     | Not system App.                             |

**Example**

```ts
import audio from '@ohos.multimedia.audio';
let audioSpatializationManager: audio.AudioSpatializationManager = audioManager.getSpatializationManager();
```

### on('volumeChange')<sup>(deprecated)</sup>

on(type: 'volumeChange', callback: Callback\<VolumeEvent>): void

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [on('volumeChange')](js-apis-audio.md#onvolumechange9) in **AudioVolumeManager**.

Subscribes to system volume change events. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

Currently, when multiple **AudioManager** instances are used in a single process, only the subscription of the last instance takes effect, and the subscription of other instances is overwritten (even if the last instance does not initiate a subscription). Therefore, you are advised to use a single **AudioManager** instance.

**System capability**: SystemCapability.Multimedia.Audio.Volume

**Parameters**

| Name  | Type                                  | Mandatory| Description                                                        |
| -------- | -------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                                 | Yes  | Event type. The event **'volumeChange'** is triggered when the system volume is changed.|
| callback | Callback<[VolumeEvent](#volumeevent9)> | Yes  | Callback used to return the changed volume.|

**Example**

```ts
audioManager.on('volumeChange', (volumeEvent: audio.VolumeEvent) => {
  console.info(`VolumeType of stream: ${volumeEvent.volumeType} `);
  console.info(`Volume level: ${volumeEvent.volume} `);
  console.info(`Whether to updateUI: ${volumeEvent.updateUi} `);
});
```

### on('ringerModeChange')<sup>(deprecated)</sup>

on(type: 'ringerModeChange', callback: Callback\<AudioRingMode>): void

Subscribes to ringer mode change events. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9. You are advised to use [on('ringerModeChange')](js-apis-audio.md#onringermodechange9) in **AudioVolumeGroupManager**.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Communication

**Parameters**

| Name  | Type                                     | Mandatory| Description                                                        |
| -------- | ----------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | string                                    | Yes  | Event type. The event **'ringerModeChange'** is triggered when the ringer mode is changed.|
| callback | Callback<[AudioRingMode](js-apis-audio.md#audioringmode)> | Yes  | Callback used to return the changed ringer mode.                                                  |

**Example**

```ts
audioManager.on('ringerModeChange', (ringerMode: audio.AudioRingMode) => {
  console.info(`Updated ringermode: ${ringerMode}`);
});
```

## AudioVolumeManager<sup>9+</sup>

Implements audio volume management. Before calling an API in **AudioVolumeManager**, you must use [getVolumeManager](js-apis-audio.md#getvolumemanager9) to obtain an **AudioVolumeManager** instance.

### getVolumeGroupInfos<sup>9+</sup>

getVolumeGroupInfos(networkId: string, callback: AsyncCallback<VolumeGroupInfos\>\): void

Obtains the volume groups. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Volume

**Parameters**

| Name    | Type                                                        | Mandatory| Description                |
| ---------- | ------------------------------------------------------------ | ---- | -------------------- |
| networkId | string                                    | Yes  | Network ID of the device. The network ID of the local device is **audio.LOCAL_NETWORK_ID**.   |
| callback  | AsyncCallback&lt;[VolumeGroupInfos](#volumegroupinfos9)&gt; | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined** and **data** is the volume groups obtained; otherwise, **err** is an error object.|

**Example**
```ts
import { BusinessError } from '@ohos.base';

audioVolumeManager.getVolumeGroupInfos(audio.LOCAL_NETWORK_ID, (err: BusinessError, value: audio.VolumeGroupInfos) => {
  if (err) {
    console.error(`Failed to obtain the volume group infos list. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate that the volume group infos list is obtained.');
});
```

### getVolumeGroupInfos<sup>9+</sup>

getVolumeGroupInfos(networkId: string\): Promise<VolumeGroupInfos\>

Obtains the volume groups. This API uses a promise to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Volume

**Parameters**

| Name    | Type              | Mandatory| Description                |
| ---------- | ------------------| ---- | -------------------- |
| networkId | string             | Yes  | Network ID of the device. The network ID of the local device is **audio.LOCAL_NETWORK_ID**.  |

**Return value**

| Type               | Description                         |
| ------------------- | ----------------------------- |
| Promise&lt;[VolumeGroupInfos](#volumegroupinfos9)&gt; | Promise used to return the volume group information list.|

**Example**

```ts
async function getVolumeGroupInfos(){
  let volumegroupinfos: audio.VolumeGroupInfos = await audio.getAudioManager().getVolumeManager().getVolumeGroupInfos(audio.LOCAL_NETWORK_ID);
  console.info('Promise returned to indicate that the volumeGroup list is obtained.'+JSON.stringify(volumegroupinfos))
}
```

### getVolumeGroupInfosSync<sup>10+</sup>

getVolumeGroupInfosSync(networkId: string\): VolumeGroupInfos

Obtains the volume groups. This API returns the result synchronously.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Volume

**Parameters**

| Name    | Type              | Mandatory| Description                |
| ---------- | ------------------| ---- | -------------------- |
| networkId | string             | Yes  | Network ID of the device. The network ID of the local device is **audio.LOCAL_NETWORK_ID**.  |

**Return value**

| Type               | Description                         |
| ------------------- | ----------------------------- |
| [VolumeGroupInfos](#volumegroupinfos9) | Volume group information list.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 6800101 | invalid parameter error              |

**Example**

```ts
import { BusinessError } from '@ohos.base';

try {
  let volumegroupinfos: audio.VolumeGroupInfos = audioVolumeManager.getVolumeGroupInfosSync(audio.LOCAL_NETWORK_ID);
  console.info(`Indicate that the volumeGroup list is obtained. ${JSON.stringify(volumegroupinfos)}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`Failed to obtain the volumeGroup list ${error}`);
}
```

## AudioVolumeGroupManager<sup>9+</sup>

Manages the volume of an audio group. Before calling any API in **AudioVolumeGroupManager**, you must use [getVolumeGroupManager](js-apis-audio.md#getvolumegroupmanager9) to obtain an **AudioVolumeGroupManager** instance.

### setVolume<sup>9+</sup>

setVolume(volumeType: AudioVolumeType, volume: number, callback: AsyncCallback&lt;void&gt;): void

Sets the volume for a stream. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ACCESS_NOTIFICATION_POLICY

This permission is required only for muting or unmuting the ringer when **volumeType** is set to **AudioVolumeType.RINGTONE**.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Volume

**Parameters**

| Name    | Type                               | Mandatory| Description                                                    |
| ---------- | ----------------------------------- | ---- | -------------------------------------------------------- |
| volumeType | [AudioVolumeType](#audiovolumetype) | Yes  | Audio stream type.                                            |
| volume     | number                              | Yes  | Volume to set. The value range can be obtained by calling **getMinVolume** and **getMaxVolume**.|
| callback   | AsyncCallback&lt;void&gt;           | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**; otherwise, **err** is an error object.|

**Example**

```ts
import { BusinessError } from '@ohos.base';

audioVolumeGroupManager.setVolume(audio.AudioVolumeType.MEDIA, 10, (err: BusinessError) => {
  if (err) {
    console.error(`Failed to set the volume. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate a successful volume setting.');
});
```

### setVolume<sup>9+</sup>

setVolume(volumeType: AudioVolumeType, volume: number): Promise&lt;void&gt;

Sets the volume for a stream. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ACCESS_NOTIFICATION_POLICY

This permission is required only for muting or unmuting the ringer when **volumeType** is set to **AudioVolumeType.RINGTONE**.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Volume

**Parameters**

| Name    | Type                               | Mandatory| Description                                                    |
| ---------- | ----------------------------------- | ---- | -------------------------------------------------------- |
| volumeType | [AudioVolumeType](#audiovolumetype) | Yes  | Audio stream type.                                            |
| volume     | number                              | Yes  | Volume to set. The value range can be obtained by calling **getMinVolume** and **getMaxVolume**.|

**Return value**

| Type               | Description                         |
| ------------------- | ----------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
audioVolumeGroupManager.setVolume(audio.AudioVolumeType.MEDIA, 10).then(() => {
  console.info('Promise returned to indicate a successful volume setting.');
});
```

### mute<sup>9+</sup>

mute(volumeType: AudioVolumeType, mute: boolean, callback: AsyncCallback&lt;void&gt;): void

Mutes or unmutes a stream. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ACCESS_NOTIFICATION_POLICY

This permission is required only for muting or unmuting the ringer when **volumeType** is set to **AudioVolumeType.RINGTONE**.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Volume

**Parameters**

| Name    | Type                               | Mandatory| Description                                 |
| ---------- | ----------------------------------- | ---- | ------------------------------------- |
| volumeType | [AudioVolumeType](#audiovolumetype) | Yes  | Audio stream type.                         |
| mute       | boolean                             | Yes  | Mute status to set. The value **true** means to mute the stream, and **false** means the opposite.|
| callback   | AsyncCallback&lt;void&gt;           | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**; otherwise, **err** is an error object.|

**Example**

```ts
import { BusinessError } from '@ohos.base';

audioVolumeGroupManager.mute(audio.AudioVolumeType.MEDIA, true, (err: BusinessError) => {
  if (err) {
    console.error(`Failed to mute the stream. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate that the stream is muted.');
});
```

### mute<sup>9+</sup>

mute(volumeType: AudioVolumeType, mute: boolean): Promise&lt;void&gt;

Mutes or unmutes a stream. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ACCESS_NOTIFICATION_POLICY

This permission is required only for muting or unmuting the ringer when **volumeType** is set to **AudioVolumeType.RINGTONE**.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Volume

**Parameters**

| Name    | Type                               | Mandatory| Description                                 |
| ---------- | ----------------------------------- | ---- | ------------------------------------- |
| volumeType | [AudioVolumeType](#audiovolumetype) | Yes  | Audio stream type.                         |
| mute       | boolean                             | Yes  | Mute status to set. The value **true** means to mute the stream, and **false** means the opposite.|

**Return value**

| Type               | Description                         |
| ------------------- | ----------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
audioVolumeGroupManager.mute(audio.AudioVolumeType.MEDIA, true).then(() => {
  console.info('Promise returned to indicate that the stream is muted.');
});
```

### setRingerMode<sup>9+</sup>

setRingerMode(mode: AudioRingMode, callback: AsyncCallback&lt;void&gt;): void

Sets the ringer mode. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ACCESS_NOTIFICATION_POLICY

This permission is required only for muting or unmuting the ringer.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Volume

**Parameters**

| Name  | Type                           | Mandatory| Description                    |
| -------- | ------------------------------- | ---- | ------------------------ |
| mode     | [AudioRingMode](js-apis-audio.md#audioringmode) | Yes  | Ringer mode.          |
| callback | AsyncCallback&lt;void&gt;       | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**; otherwise, **err** is an error object.|

**Example**

```ts
import { BusinessError } from '@ohos.base';

audioVolumeGroupManager.setRingerMode(audio.AudioRingMode.RINGER_MODE_NORMAL, (err: BusinessError) => {
  if (err) {
    console.error(`Failed to set the ringer mode. ${err}`);
    return;
  }
  console.info('Callback invoked to indicate a successful setting of the ringer mode.');
});
```

### setRingerMode<sup>9+</sup>

setRingerMode(mode: AudioRingMode): Promise&lt;void&gt;

Sets the ringer mode. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ACCESS_NOTIFICATION_POLICY

This permission is required only for muting or unmuting the ringer.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Volume

**Parameters**

| Name| Type                           | Mandatory| Description          |
| ------ | ------------------------------- | ---- | -------------- |
| mode   | [AudioRingMode](js-apis-audio.md#audioringmode) | Yes  | Ringer mode.|

**Return value**

| Type               | Description                           |
| ------------------- | ------------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
audioVolumeGroupManager.setRingerMode(audio.AudioRingMode.RINGER_MODE_NORMAL).then(() => {
  console.info('Promise returned to indicate a successful setting of the ringer mode.');
});
```

### setMicMute<sup>11+</sup>

setMicMute(mute: boolean): Promise&lt;void&gt;

Mutes or unmutes the microphone. This API uses a promise to return the result.

**Required permissions**: ohos.permission.MANAGE_AUDIO_CONFIG

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Volume

**Parameters**

| Name| Type   | Mandatory| Description                                         |
| ------ | ------- | ---- | --------------------------------------------- |
| mute   | boolean | Yes  | Mute status to set. The value **true** means to mute the microphone, and **false** means the opposite.|

**Return value**

| Type               | Description                           |
| ------------------- | ------------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 201     | Permission denied.                          |
| 202     | Not system App.                             |
| 401     | Input parameter type or number mismatch.    |
| 6800101 | Input parameter value error.                |

**Example**

```ts
audioVolumeGroupManager.setMicMute(true).then(() => {
  console.info('Promise returned to indicate that the mic is muted.');
});
```

### adjustVolumeByStep<sup>10+</sup>

adjustVolumeByStep(adjustType: VolumeAdjustType, callback: AsyncCallback&lt;void&gt;): void

Adjusts the volume of the stream with the highest priority by step. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ACCESS_NOTIFICATION_POLICY

This permission is required only for muting or unmuting the ringer when **volumeType** is set to **AudioVolumeType.RINGTONE**.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Volume

**Parameters**

| Name    | Type                               | Mandatory| Description                                                    |
| ---------- | ----------------------------------- | ---- | -------------------------------------------------------- |
| adjustType | [VolumeAdjustType](#volumeadjusttype10) | Yes  | Volume adjustment type.                                            |
| callback   | AsyncCallback&lt;void&gt;           | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**; otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. Return by callback.                     |
| 6800301 | System error. Return by callback.                                |

**Example**

```ts
import { BusinessError } from '@ohos.base';

audioVolumeGroupManager.adjustVolumeByStep(audio.VolumeAdjustType.VOLUME_UP, (err: BusinessError) => {
  if (err) {
    console.error(`Failed to adjust the volume by step. ${err}`);
    return;
  } else {
    console.info('Success to adjust the volume by step.');
  }
});
```
### adjustVolumeByStep<sup>10+</sup>

adjustVolumeByStep(adjustType: VolumeAdjustType): Promise&lt;void&gt;

Adjusts the volume of the stream with the highest priority by step. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ACCESS_NOTIFICATION_POLICY

This permission is required only for muting or unmuting the ringer when **volumeType** is set to **AudioVolumeType.RINGTONE**.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Volume

**Parameters**

| Name    | Type                               | Mandatory| Description                                                    |
| ---------- | ----------------------------------- | ---- | -------------------------------------------------------- |
| adjustType | [VolumeAdjustType](#volumeadjusttype10) | Yes  | Volume adjustment type.                                            |

**Return value**

| Type               | Description                         |
| ------------------- | ----------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. Return by promise.                     |
| 6800301 | System error. Return by promise.                                |

**Example**

```ts
import { BusinessError } from '@ohos.base';

audioVolumeGroupManager.adjustVolumeByStep(audio.VolumeAdjustType.VOLUME_UP).then(() => {
  console.info('Success to adjust the volume by step.');
}).catch((error: BusinessError) => {
  console.error('Fail to adjust the volume by step.');
});
```

### adjustSystemVolumeByStep<sup>10+</sup>

adjustSystemVolumeByStep(volumeType: AudioVolumeType, adjustType: VolumeAdjustType, callback: AsyncCallback&lt;void&gt;): void

Adjusts the volume of a stream by step. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ACCESS_NOTIFICATION_POLICY

This permission is required only for muting or unmuting the ringer when **volumeType** is set to **AudioVolumeType.RINGTONE**.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Volume

**Parameters**

| Name    | Type                               | Mandatory| Description                                                    |
| ---------- | ----------------------------------- | ---- | -------------------------------------------------------- |
| volumeType | [AudioVolumeType](#audiovolumetype) | Yes  | Audio stream type.                                            |
| adjustType | [VolumeAdjustType](#volumeadjusttype10) | Yes  | Volume adjustment type.                                      |
| callback   | AsyncCallback&lt;void&gt;           | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**; otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. Return by callback.                     |
| 6800301 | System error. Return by callback.                                |

**Example**

```ts
import { BusinessError } from '@ohos.base';

audioVolumeGroupManager.adjustSystemVolumeByStep(audio.AudioVolumeType.MEDIA, audio.VolumeAdjustType.VOLUME_UP, (err: BusinessError) => {
  if (err) {
    console.error(`Failed to adjust the system volume by step ${err}`);
  } else {
    console.info('Success to adjust the system volume by step.');
  }
});
```
### adjustSystemVolumeByStep<sup>10+</sup>

adjustSystemVolumeByStep(volumeType: AudioVolumeType, adjustType: VolumeAdjustType): Promise&lt;void&gt;

Adjusts the volume of a stream by step. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ACCESS_NOTIFICATION_POLICY

This permission is required only for muting or unmuting the ringer when **volumeType** is set to **AudioVolumeType.RINGTONE**.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Volume

**Parameters**

| Name    | Type                               | Mandatory| Description                                                    |
| ---------- | ----------------------------------- | ---- | -------------------------------------------------------- |
| volumeType | [AudioVolumeType](#audiovolumetype) | Yes  | Audio stream type.                                            |
| adjustType | [VolumeAdjustType](#volumeadjusttype10) | Yes  | Volume adjustment type.                                            |

**Return value**

| Type               | Description                         |
| ------------------- | ----------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. Return by promise.                     |
| 6800301 | System error. Return by promise.                                |

**Example**

```ts
import { BusinessError } from '@ohos.base';

audioVolumeGroupManager.adjustSystemVolumeByStep(audio.AudioVolumeType.MEDIA, audio.VolumeAdjustType.VOLUME_UP).then(() => {
  console.info('Success to adjust the system volume by step.');
}).catch((error: BusinessError) => {
  console.error('Fail to adjust the system volume by step.');
});
```

## AudioRoutingManager<sup>9+</sup>

Implements audio routing management. Before calling any API in **AudioRoutingManager**, you must use [getRoutingManager](js-apis-audio.md#getroutingmanager9) to obtain an **AudioRoutingManager** instance.

### getAvailableDevices<sup>11+</sup>

getAvailableDevices(deviceUsage: DeviceUsage): AudioDeviceDescriptors

Obtains the available audio devices. This API returns the result synchronously.

**System capability**: SystemCapability.Multimedia.Audio.Device

**System API**: This is a system API.

**Parameters**

| Name    | Type                     | Mandatory| Description            |
| ---------- | ------------------------- | ---- | ---------------- |
| deviceUsage| [DeviceUsage](#deviceusage11) | Yes  | Device usage.|

**Return value**

| Type                                                        | Description                     |
| ------------------------------------------------------------ | ------------------------- |
| [AudioDeviceDescriptors](js-apis-audio.md#audiodevicedescriptors) | Device list.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 6800101 | invalid parameter error              |

**Example**

```ts
import { BusinessError } from '@ohos.base';

try {
  let data: audio.AudioDeviceDescriptors = audioRoutingManager.getAvailableDevices(audio.DeviceUsage.MEDIA_OUTPUT_DEVICES);
  console.info(`Indicate that the device list is obtained ${data}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`Failed to obtain the device list. ${error}`);
}
```

### on('availableDeviceChange')<sup>11+</sup>

on(type: 'availableDeviceChange', deviceUsage: DeviceUsage, callback: Callback<DeviceChangeAction\>): void

Subscribes to available audio device change events. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Multimedia.Audio.Device

**System API**: This is a system API.

**Parameters**

| Name  | Type                                                | Mandatory| Description                                      |
| :------- | :--------------------------------------------------- | :--- | :----------------------------------------- |
| type     | string                                               | Yes  | Event type. The event **'availableDeviceChange'** is triggered when the available devices change.|
| deviceUsage | [DeviceUsage](#deviceusage11)                       | Yes  | Device usage.    |
| callback | Callback<[DeviceChangeAction](js-apis-audio.md#devicechangeaction)\> | Yes  | Callback used to return the available device change details.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. |

**Example**

```ts
audioRoutingManager.on('availableDeviceChange', audio.DeviceUsage.MEDIA_OUTPUT_DEVICES, (deviceChanged: audio.DeviceChangeAction) => {
  console.info('device change type : ' + deviceChanged.type);
  console.info('device descriptor size : ' + deviceChanged.deviceDescriptors.length);
  console.info('device change descriptor : ' + deviceChanged.deviceDescriptors[0].deviceRole);
  console.info('device change descriptor : ' + deviceChanged.deviceDescriptors[0].deviceType);
});
```

### off('availableDeviceChange')<sup>11+</sup>

off(type: 'availableDeviceChange', callback?: Callback<DeviceChangeAction\>): void

Unsubscribes from available audio device change events. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Multimedia.Audio.Device

**System API**: This is a system API.

**Parameters**

| Name  | Type                                               | Mandatory| Description                                      |
| -------- | --------------------------------------------------- | ---- | ------------------------------------------ |
| type     | string                                              | Yes  | Event type. The event **'availableDeviceChange'** is triggered when the available devices change.|
| callback | Callback<[DeviceChangeAction](js-apis-audio.md#devicechangeaction)> | No  | Callback used to return the available device change details.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 6800101 | Invalid parameter error. |

**Example**

```ts
audioRoutingManager.off('availableDeviceChange');
```

### selectInputDevice<sup>9+</sup>

selectInputDevice(inputAudioDevices: AudioDeviceDescriptors, callback: AsyncCallback&lt;void&gt;): void

Selects an audio input device. Currently, only one input device can be selected. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Device

**Parameters**

| Name                      | Type                                                        | Mandatory| Description                     |
| --------------------------- | ------------------------------------------------------------ | ---- | ------------------------- |
| inputAudioDevices           | [AudioDeviceDescriptors](js-apis-audio.md#audiodevicedescriptors)            | Yes  | Input device.              |
| callback                    | AsyncCallback&lt;void&gt;                                    | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**; otherwise, **err** is an error object.|

**Example**
```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';

let inputAudioDeviceDescriptor: audio.AudioDeviceDescriptors = [{
  deviceRole : audio.DeviceRole.INPUT_DEVICE,
  deviceType : audio.DeviceType.MIC,
  id : 1,
  name : "",
  address : "",
  sampleRates : [44100],
  channelCounts : [2],
  channelMasks : [0],
  networkId : audio.LOCAL_NETWORK_ID,
  interruptGroupId : 1,
  volumeGroupId : 1,
  displayName : "",
}];

async function selectInputDevice(){
  audioRoutingManager.selectInputDevice(inputAudioDeviceDescriptor, (err: BusinessError) => {
    if (err) {
      console.error(`Result ERROR: ${err}`);
    } else {
      console.info('Select input devices result callback: SUCCESS');
    }
  });
}
```

### selectInputDevice<sup>9+</sup>

selectInputDevice(inputAudioDevices: AudioDeviceDescriptors): Promise&lt;void&gt;

**System API**: This is a system API.

Selects an audio input device. Currently, only one input device can be selected. This API uses a promise to return the result.

**System capability**: SystemCapability.Multimedia.Audio.Device

**Parameters**

| Name                      | Type                                                        | Mandatory| Description                     |
| --------------------------- | ------------------------------------------------------------ | ---- | ------------------------- |
| inputAudioDevices           | [AudioDeviceDescriptors](js-apis-audio.md#audiodevicedescriptors)            | Yes  | Input device.              |

**Return value**

| Type                 | Description                        |
| --------------------- | --------------------------- |
| Promise&lt;void&gt;   | Promise that returns no value.|

**Example**

```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';

let inputAudioDeviceDescriptor: audio.AudioDeviceDescriptors = [{
  deviceRole : audio.DeviceRole.INPUT_DEVICE,
  deviceType : audio.DeviceType.MIC,
  id : 1,
  name : "",
  address : "",
  sampleRates : [44100],
  channelCounts : [2],
  channelMasks : [0],
  networkId : audio.LOCAL_NETWORK_ID,
  interruptGroupId : 1,
  volumeGroupId : 1,
  displayName : "",
}];

async function getRoutingManager(){
  audioRoutingManager.selectInputDevice(inputAudioDeviceDescriptor).then(() => {
    console.info('Select input devices result promise: SUCCESS');
  }).catch((err: BusinessError) => {
    console.error(`Result ERROR: ${err}`);
  });
}
```

### selectOutputDevice<sup>9+</sup>

selectOutputDevice(outputAudioDevices: AudioDeviceDescriptors, callback: AsyncCallback&lt;void&gt;): void

Selects an audio output device. Currently, only one output device can be selected. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Device

**Parameters**

| Name                      | Type                                                        | Mandatory| Description                     |
| --------------------------- | ------------------------------------------------------------ | ---- | ------------------------- |
| outputAudioDevices          | [AudioDeviceDescriptors](js-apis-audio.md#audiodevicedescriptors)            | Yes  | Output device.              |
| callback                    | AsyncCallback&lt;void&gt;                                    | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**; otherwise, **err** is an error object.|

**Example**
```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';

let outputAudioDeviceDescriptor: audio.AudioDeviceDescriptors = [{
  deviceRole : audio.DeviceRole.OUTPUT_DEVICE,
  deviceType : audio.DeviceType.SPEAKER,
  id : 1,
  name : "",
  address : "",
  sampleRates : [44100],
  channelCounts : [2],
  channelMasks : [0],
  networkId : audio.LOCAL_NETWORK_ID,
  interruptGroupId : 1,
  volumeGroupId : 1,
  displayName : "",
}];

async function selectOutputDevice(){
  audioRoutingManager.selectOutputDevice(outputAudioDeviceDescriptor, (err: BusinessError) => {
    if (err) {
      console.error(`Result ERROR: ${err}`);
    } else {
      console.info('Select output devices result callback: SUCCESS'); }
  });
}
```

### selectOutputDevice<sup>9+</sup>

selectOutputDevice(outputAudioDevices: AudioDeviceDescriptors): Promise&lt;void&gt;

**System API**: This is a system API.

Selects an audio output device. Currently, only one output device can be selected. This API uses a promise to return the result.

**System capability**: SystemCapability.Multimedia.Audio.Device

**Parameters**

| Name                      | Type                                                        | Mandatory| Description                     |
| --------------------------- | ------------------------------------------------------------ | ---- | ------------------------- |
| outputAudioDevices          | [AudioDeviceDescriptors](js-apis-audio.md#audiodevicedescriptors)            | Yes  | Output device.              |

**Return value**

| Type                 | Description                        |
| --------------------- | --------------------------- |
| Promise&lt;void&gt;   | Promise that returns no value.|

**Example**

```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';

let outputAudioDeviceDescriptor: audio.AudioDeviceDescriptors = [{
  deviceRole : audio.DeviceRole.OUTPUT_DEVICE,
  deviceType : audio.DeviceType.SPEAKER,
  id : 1,
  name : "",
  address : "",
  sampleRates : [44100],
  channelCounts : [2],
  channelMasks : [0],
  networkId : audio.LOCAL_NETWORK_ID,
  interruptGroupId : 1,
  volumeGroupId : 1,
  displayName : "",
}];

async function selectOutputDevice(){
  audioRoutingManager.selectOutputDevice(outputAudioDeviceDescriptor).then(() => {
    console.info('Select output devices result promise: SUCCESS');
  }).catch((err: BusinessError) => {
    console.error(`Result ERROR: ${err}`);
  });
}
```

### selectOutputDeviceByFilter<sup>9+</sup>

selectOutputDeviceByFilter(filter: AudioRendererFilter, outputAudioDevices: AudioDeviceDescriptors, callback: AsyncCallback&lt;void&gt;): void

**System API**: This is a system API.

Selects an audio output device based on the filter criteria. Currently, only one output device can be selected. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Multimedia.Audio.Device

**Parameters**

| Name                      | Type                                                        | Mandatory| Description                     |
| --------------------------- | ------------------------------------------------------------ | ---- | ------------------------- |
| filter                      | [AudioRendererFilter](#audiorendererfilter9)                 | Yes  | Filter criteria.              |
| outputAudioDevices          | [AudioDeviceDescriptors](js-apis-audio.md#audiodevicedescriptors)            | Yes  | Output device.              |
| callback                    | AsyncCallback&lt;void&gt;                                    | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**; otherwise, **err** is an error object.|

**Example**
```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';

let outputAudioRendererFilter: audio.AudioRendererFilter = {
  uid : 20010041,
  rendererInfo : {
    usage : audio.StreamUsage.STREAM_USAGE_MUSIC,
    rendererFlags : 0
  },
  rendererId : 0
};

let outputAudioDeviceDescriptor: audio.AudioDeviceDescriptors = [{
  deviceRole : audio.DeviceRole.OUTPUT_DEVICE,
  deviceType : audio.DeviceType.SPEAKER,
  id : 1,
  name : "",
  address : "",
  sampleRates : [44100],
  channelCounts : [2],
  channelMasks : [0],
  networkId : audio.LOCAL_NETWORK_ID,
  interruptGroupId : 1,
  volumeGroupId : 1,
  displayName : "",
}];

async function selectOutputDeviceByFilter(){
  audioRoutingManager.selectOutputDeviceByFilter(outputAudioRendererFilter, outputAudioDeviceDescriptor, (err: BusinessError) => {
    if (err) {
      console.error(`Result ERROR: ${err}`);
    } else {
      console.info('Select output devices by filter result callback: SUCCESS'); }
  });
}
```

### selectOutputDeviceByFilter<sup>9+</sup>

selectOutputDeviceByFilter(filter: AudioRendererFilter, outputAudioDevices: AudioDeviceDescriptors): Promise&lt;void&gt;

**System API**: This is a system API.

Selects an audio output device based on the filter criteria. Currently, only one output device can be selected. This API uses a promise to return the result.

**System capability**: SystemCapability.Multimedia.Audio.Device

**Parameters**

| Name                | Type                                                        | Mandatory| Description                     |
| ----------------------| ------------------------------------------------------------ | ---- | ------------------------- |
| filter                | [AudioRendererFilter](#audiorendererfilter9)                 | Yes  | Filter criteria.              |
| outputAudioDevices    | [AudioDeviceDescriptors](js-apis-audio.md#audiodevicedescriptors)            | Yes  | Output device.              |

**Return value**

| Type                 | Description                        |
| --------------------- | --------------------------- |
| Promise&lt;void&gt;   | Promise that returns no value.|

**Example**

```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';

let outputAudioRendererFilter: audio.AudioRendererFilter = {
  uid : 20010041,
  rendererInfo : {
    usage : audio.StreamUsage.STREAM_USAGE_MUSIC,
    rendererFlags : 0
  },
  rendererId : 0
};

let outputAudioDeviceDescriptor: audio.AudioDeviceDescriptors = [{
  deviceRole : audio.DeviceRole.OUTPUT_DEVICE,
  deviceType : audio.DeviceType.SPEAKER,
  id : 1,
  name : "",
  address : "",
  sampleRates : [44100],
  channelCounts : [2],
  channelMasks : [0],
  networkId : audio.LOCAL_NETWORK_ID,
  interruptGroupId : 1,
  volumeGroupId : 1,
  displayName : "",
}];

async function selectOutputDeviceByFilter(){
  audioRoutingManager.selectOutputDeviceByFilter(outputAudioRendererFilter, outputAudioDeviceDescriptor).then(() => {
    console.info('Select output devices by filter result promise: SUCCESS');
  }).catch((err: BusinessError) => {
    console.error(`Result ERROR: ${err}`);
  })
}
```

## AudioRendererChangeInfo<sup>9+</sup>

Describes the audio renderer change event.

**System capability**: SystemCapability.Multimedia.Audio.Renderer

| Name              | Type                                      | Readable| Writable| Description                         |
| -------------------| ----------------------------------------- | ---- | ---- | ---------------------------- |
| clientUid          | number                                    | Yes  | No  | UID of the audio renderer client.<br>This is a system API.|
| rendererState      | [AudioState](js-apis-audio.md#audiostate8)                 | Yes  | No  | Audio state.<br>This is a system API.|

## AudioCapturerChangeInfo<sup>9+</sup>

Describes the audio capturer change event.

**System capability**: SystemCapability.Multimedia.Audio.Capturer

| Name              | Type                                      | Readable| Writable| Description                         |
| -------------------| ----------------------------------------- | ---- | ---- | ---------------------------- |
| clientUid          | number                                    | Yes  | No  | UID of the audio capturer client.<br>This is a system API.|
| capturerState      | [AudioState](js-apis-audio.md#audiostate8)                 | Yes  | No  | Audio state.<br>This is a system API.|

## AudioDeviceDescriptor

Describes an audio device.

| Name                         | Type                      | Readable| Writable| Description      |
| ----------------------------- | -------------------------- | ---- | ---- | ---------- |
| networkId<sup>9+</sup>        | string                     | Yes  | No  | ID of the device network.<br>This is a system API.<br>**System capability**: SystemCapability.Multimedia.Audio.Device|
| interruptGroupId<sup>9+</sup> | number                     | Yes  | No  | ID of the interruption group to which the device belongs.<br>This is a system API.<br> **System capability**: SystemCapability.Multimedia.Audio.Device|
| volumeGroupId<sup>9+</sup>    | number                     | Yes  | No  | ID of the volume group to which the device belongs.<br>This is a system API.<br> **System capability**: SystemCapability.Multimedia.Audio.Device|

## AudioRendererFilter<sup>9+</sup>

Implements filter criteria. Before calling **selectOutputDeviceByFilter**, you must obtain an **AudioRendererFilter** instance.

**System API**: This is a system API.

| Name         | Type                                    | Mandatory| Description         |
| -------------| ---------------------------------------- | ---- | -------------- |
| uid          | number                                   |  No | Application ID.<br>**System capability**: SystemCapability.Multimedia.Audio.Core|
| rendererInfo | [AudioRendererInfo](js-apis-audio.md#audiorendererinfo8) |  No | Audio renderer information.<br>**System capability**: SystemCapability.Multimedia.Audio.Renderer|
| rendererId   | number                                   |  No | Unique ID of an audio stream.<br>**System capability**: SystemCapability.Multimedia.Audio.Renderer|

**Example**

```ts
import audio from '@ohos.multimedia.audio';

let outputAudioRendererFilter: audio.AudioRendererFilter = {
  uid : 20010041,
  rendererInfo : {
    usage : audio.StreamUsage.STREAM_USAGE_MUSIC,
    rendererFlags : 0
  },
  rendererId : 0
};
```

## AudioSpatializationManager<sup>11+</sup>

Implements spatial audio management. Before calling an API in **AudioSpatializationManager**, you must use [getSpatializationManager](#getspatializationmanager11) to obtain an **AudioSpatializationManager** instance.

### isSpatializationSupported<sup>11+</sup>

isSpatializationSupported(): boolean

Checks whether the system supports spatial audio rendering. This API returns the result synchronously.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Spatialization

**Return value**

| Type                  | Description                                                        |
| ---------------------- | ------------------------------------------------------------ |
| boolean | Returns **true** if the system supports spatial audio rendering, and returns **false** otherwise.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 202     | Not system App.                             |

**Example**

```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';
try {
  let isSpatializationSupported: boolean = audioSpatializationManager.isSpatializationSupported();
  console.info(`AudioSpatializationManager isSpatializationSupported: ${isSpatializationSupported}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`ERROR: ${error}`);
}
```

### isSpatializationSupportedForDevice<sup>11+</sup>

isSpatializationSupportedForDevice(deviceDescriptor: AudioDeviceDescriptor): boolean

Checks whether a device supports spatial audio rendering. This API returns the result synchronously.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Spatialization

**Parameters**

| Name    | Type                                                        | Mandatory| Description                |
| ---------- | ------------------------------------------------------------ | ---- | -------------------- |
| deviceDescriptor | [AudioDeviceDescriptor](./js-apis-audio.md#audiodevicedescriptor)         | Yes  | Descriptor of the device.    |

**Return value**

| Type                  | Description                                                        |
| ---------------------- | ------------------------------------------------------------ |
| boolean | Returns **true** if the device supports spatial audio rendering, and returns **false** otherwise.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 202     | Not system App.                             |
| 401     | Input parameter type or number mismatch.    |
| 6800101 | Invalid parameter error.                    |

**Example**

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

### isHeadTrackingSupported<sup>11+</sup>

isHeadTrackingSupported(): boolean

Checks whether the system supports head tracking. This API returns the result synchronously.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Spatialization

**Return value**

| Type                  | Description                                                        |
| ---------------------- | ------------------------------------------------------------ |
| boolean | Returns **true** if the system supports head tracking, and returns **false** otherwise.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 202     | Not system App.                             |

**Example**

```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';
try {
  let isHeadTrackingSupported: boolean = audioSpatializationManager.isHeadTrackingSupported();
  console.info(`AudioSpatializationManager isHeadTrackingSupported: ${isHeadTrackingSupported}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`ERROR: ${error}`);
}
```

### isHeadTrackingSupportedForDevice<sup>11+</sup>

isHeadTrackingSupportedForDevice(deviceDescriptor: AudioDeviceDescriptor): boolean

Checks whether a device supports head tracking. This API returns the result synchronously.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Spatialization

**Parameters**

| Name    | Type                                                        | Mandatory| Description                |
| ---------- | ------------------------------------------------------------ | ---- | -------------------- |
| deviceDescriptor | [AudioDeviceDescriptor](./js-apis-audio.md#audiodevicedescriptor)         | Yes  | Descriptor of the device.    |

**Return value**

| Type                  | Description                                                        |
| ---------------------- | ------------------------------------------------------------ |
| boolean | Returns **true** if the device supports head tracking, and returns **false** otherwise.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 202     | Not system App.                             |
| 401     | Input parameter type or number mismatch.    |
| 6800101 | Invalid parameter error.                    |

**Example**

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

### setSpatializationEnabled<sup>11+</sup>

setSpatializationEnabled(enable: boolean, callback: AsyncCallback&lt;void&gt;): void

Enables or disables spatial audio rendering. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.MANAGE_SYSTEM_AUDIO_EFFECTS

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Spatialization

**Parameters**

| Name                      | Type                                                        | Mandatory| Description                     |
| --------------------------- | ------------------------------------------------------------ | ---- | ------------------------- |
| enable                      | boolean                                                      | Yes  | Whether to enable or disable spatial audio rendering. The value **true** means to enable spatial audio rendering, and **false** means the opposite. |
| callback                    | AsyncCallback&lt;void&gt;                                    | Yes  | Callback that returns no value.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 201     | Permission denied. Return by callback.      |
| 202     | Not system App.                             |
| 401     | Input parameter type or number mismatch.    |
| 6800101 | Invalid parameter error.                    |

**Example**
```ts
import audio from '@ohos.multimedia.audio';
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

### setSpatializationEnabled<sup>11+</sup>

setSpatializationEnabled(enable: boolean): Promise&lt;void&gt;

Enables or disables spatial audio rendering. This API uses a promise to return the result.

**Required permissions**: ohos.permission.MANAGE_SYSTEM_AUDIO_EFFECTS

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Spatialization

**Parameters**

| Name                | Type                                                        | Mandatory| Description                     |
| ----------------------| ------------------------------------------------------------ | ---- | ------------------------- |
| enable                | boolean                                                      | Yes  | Whether to enable or disable spatial audio rendering. The value **true** means to enable spatial audio rendering, and **false** means the opposite. |

**Return value**

| Type                 | Description                        |
| --------------------- | --------------------------- |
| Promise&lt;void&gt;   | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 201     | Permission denied. Return by promise.       |
| 202     | Not system App.                             |
| 401     | Input parameter type or number mismatch.    |

**Example**

```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';

let enable: boolean = true
audioSpatializationManager.setSpatializationEnabled(enable).then(() => {
  console.info(`setSpatializationEnabled success`);
}).catch((err: BusinessError) => {
  console.error(`Result ERROR: ${err}`);
});
```

### isSpatializationEnabled<sup>11+</sup>

isSpatializationEnabled(): boolean

Checks whether spatial audio rendering is enabled. This API returns the result synchronously.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Spatialization

**Return value**

| Type                  | Description                                                        |
| ---------------------- | ------------------------------------------------------------ |
| boolean | Returns **true** if spatial audio rendering is enabled, and returns **false** otherwise.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 202     | Not system App.                             |

**Example**

```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';
try {
  let isSpatializationEnabled: boolean = audioSpatializationManager.isSpatializationEnabled();
  console.info(`AudioSpatializationManager isSpatializationEnabled: ${isSpatializationEnabled}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`ERROR: ${error}`);
}
```

### on('spatializationEnabledChange')<sup>11+</sup>

on(type: 'spatializationEnabledChange', callback: Callback<boolean\>): void

Subscribes to spatial audio rendering status changes.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Spatialization

**Parameters**

| Name  | Type                                                | Mandatory| Description                                          |
| :------- | :--------------------------------------------------- | :--- |:---------------------------------------------|
| type     | string                                               | Yes  | Event type. The event **'spatializationEnabledChange'** is triggered when the status of spatial audio rendering changes.|
| callback | Callback<boolean\> | Yes  | Callback used to return the status of spatial audio rendering. The value **true** means that spatial audio rendering is enabled, and **false** means the opposite.   |

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 202     | Not system App.                             |
| 401     | Input parameter type or number mismatch.    |
| 6800101 | Invalid parameter error.                    |

**Example**

```ts
import audio from '@ohos.multimedia.audio';

audioSpatializationManager.on('spatializationEnabledChange', (isSpatializationEnabled: boolean) => {
  console.info(`isSpatializationEnabled: ${isSpatializationEnabled}`);
});
```

### off('spatializationEnabledChange')<sup>11+</sup>

off(type: 'spatializationEnabledChange', callback?: Callback<boolean\>): void

Unsubscribes from spatial audio rendering status changes.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Spatialization

**Parameters**

| Name  | Type                                               | Mandatory| Description                                      |
| -------- | --------------------------------------------------- | ---- | ------------------------------------------ |
| type     | string                                              | Yes  | Event type. The event **'spatializationEnabledChange'** is triggered when the status of spatial audio rendering changes.|
| callback | Callback<boolean\> | No  | Callback used to return the status of spatial audio rendering. The value **true** means that spatial audio rendering is enabled, and **false** means the opposite.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 202     | Not system App.                             |
| 401     | Input parameter type or number mismatch.    |
| 6800101 | Invalid parameter error.                    |

**Example**

```ts
import audio from '@ohos.multimedia.audio';
audioSpatializationManager.off('spatializationEnabledChange');
```


### setHeadTrackingEnabled<sup>11+</sup>

setHeadTrackingEnabled(enable: boolean, callback: AsyncCallback&lt;void&gt;): void

Enables or disables head tracking. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.MANAGE_SYSTEM_AUDIO_EFFECTS

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Spatialization

**Parameters**

| Name                      | Type                                                        | Mandatory| Description                     |
| --------------------------- | ------------------------------------------------------------ | ---- | ------------------------- |
| enable                      | boolean                                                      | Yes  | Whether to enable or disable head tracking. The value **true** means to enable head tracking, and **false** means the opposite. |
| callback                    | AsyncCallback&lt;void&gt;                                    | Yes  | Callback that returns no value.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 201     | Permission denied. Return by callback.      |
| 202     | Not system App.                             |
| 401     | Input parameter type or number mismatch.    |
| 6800101 | Invalid parameter error.                    |

**Example**
```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';

let enable: boolean = true
audioSpatializationManager.setHeadTrackingEnabled(enable, (err: BusinessError) => {
  if (err) {
    console.error(`Result ERROR: ${err}`);
  } else {
    console.info(`setHeadTrackingEnabled success`);
  }
});
```

### setHeadTrackingEnabled<sup>11+</sup>

setHeadTrackingEnabled(enable: boolean): Promise&lt;void&gt;

Enables or disables head tracking. This API uses a promise to return the result.

**Required permissions**: ohos.permission.MANAGE_SYSTEM_AUDIO_EFFECTS

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Spatialization

**Parameters**

| Name                | Type                                                        | Mandatory| Description                     |
| ----------------------| ------------------------------------------------------------ | ---- | ------------------------- |
| enable                | boolean                                                      | Yes  | Whether to enable or disable head tracking. The value **true** means to enable head tracking, and **false** means the opposite. |

**Return value**

| Type                 | Description                        |
| --------------------- | --------------------------- |
| Promise&lt;void&gt;   | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 201     | Permission denied. Return by promise.       |
| 202     | Not system App.                             |
| 401     | Input parameter type or number mismatch.    |

**Example**

```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';

let enable: boolean = true
audioSpatializationManager.setHeadTrackingEnabled(enable).then(() => {
  console.info(`setHeadTrackingEnabled success`);
}).catch((err: BusinessError) => {
  console.error(`Result ERROR: ${err}`);
});
```

### isHeadTrackingEnabled<sup>11+</sup>

isHeadTrackingEnabled(): boolean

Checks whether head tracking is enabled. This API returns the result synchronously.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Spatialization

**Return value**

| Type                  | Description                                                        |
| ---------------------- | ------------------------------------------------------------ |
| boolean | Returns **true** if head tracking is enabled, and returns **false** otherwise.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 202     | Not system App.                             |

**Example**

```ts
import audio from '@ohos.multimedia.audio';
import { BusinessError } from '@ohos.base';
try {
  let isHeadTrackingEnabled: boolean = audioSpatializationManager.isHeadTrackingEnabled();
  console.info(`AudioSpatializationManager isHeadTrackingEnabled: ${isHeadTrackingEnabled}`);
} catch (err) {
  let error = err as BusinessError;
  console.error(`ERROR: ${error}`);
}
```

### on('headTrackingEnabledChange')<sup>11+</sup>

on(type: 'headTrackingEnabledChange', callback: Callback<boolean\>): void

Subscribes to head tracking status changes.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Spatialization

**Parameters**

| Name  | Type                                                | Mandatory| Description                                      |
| :------- | :--------------------------------------------------- | :--- | :----------------------------------------- |
| type     | string                                               | Yes  | Event type. The event **'headTrackingEnabledChange'** is triggered when the status of head tracking changes.|
| callback | Callback<boolean\> | Yes  | Callback used to return the status of head tracking. The value **true** means that head tracking is enabled, and **false** means the opposite.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 202     | Not system App.                             |
| 401     | Input parameter type or number mismatch.    |
| 6800101 | Invalid parameter error.                    |

**Example**

```ts
import audio from '@ohos.multimedia.audio';

audioSpatializationManager.on('headTrackingEnabledChange', (isHeadTrackingEnabled: boolean) => {
  console.info(`isHeadTrackingEnabled: ${isHeadTrackingEnabled}`);
});
```

### off('headTrackingEnabledChange')<sup>11+</sup>

off(type: 'headTrackingEnabledChange', callback?: Callback<boolean\>): void

Unsubscribes from head tracking status changes.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Spatialization

**Parameters**

| Name  | Type                                               | Mandatory| Description                                      |
| -------- | --------------------------------------------------- | ---- | ------------------------------------------ |
| type     | string                                              | Yes  | Event type. The event **'headTrackingEnabledChange'** is triggered when the status of head tracking changes.|
| callback | Callback<boolean\> | No  | Callback used to return the status of head tracking. The value **true** means that head tracking is enabled, and **false** means the opposite.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 202     | Not system App.                             |
| 401     | Input parameter type or number mismatch.    |
| 6800101 | Invalid parameter error.                    |

**Example**

```ts
import audio from '@ohos.multimedia.audio';
audioSpatializationManager.off('headTrackingEnabledChange');
```

### updateSpatialDeviceState<sup>11+</sup>

updateSpatialDeviceState(spatialDeviceState: AudioSpatialDeviceState): void

Updates the state information of a spatial device. This API returns the result synchronously.

**Required permissions**: ohos.permission.MANAGE_SYSTEM_AUDIO_EFFECTS

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Spatialization

**Parameters**

| Name  | Type                                               | Mandatory| Description                                      |
| -------- | --------------------------------------------------- | ---- | ------------------------------------------ |
| spatialDeviceState     | [AudioSpatialDeviceState](#audiospatialdevicestate11)     | Yes  | New state information of the spatial device.|

**Error codes**

For details about the error codes, see [Audio Error Codes](errorcode-audio.md).

| ID| Error Message|
| ------- | --------------------------------------------|
| 201     | Permission denied.                          |
| 202     | Not system App.                             |
| 401     | Input parameter type or number mismatch.    |
| 6800101 | Invalid parameter error.                    |

**Example**

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

## AudioSpatialDeviceState<sup>11+</sup>

Defines the state information of a spatial device.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Spatialization

| Name                         | Type                      | Readable| Writable| Description      |
| ----------------------------- | -------------------------- | ---- | ---- | ---------- |
| address<sup>11+</sup>                    | string         | Yes  | Yes  | Address of the spatial device.|
| isSpatializationSupported<sup>11+</sup>  | boolean        | Yes  | Yes  | Whether the spatial device supports spatial audio rendering.|
| isHeadTrackingSupported<sup>11+</sup>    | boolean        | Yes  | Yes  | Whether the spatial device supports head tracking.|
| spatialDeviceType<sup>11+</sup>          | [AudioSpatialDeviceType](#audiospatialdevicetype11)   | Yes  | Yes  | Type of the spatial device.|

**Example**

```ts
import audio from '@ohos.multimedia.audio';

let spatialDeviceState: audio.AudioSpatialDeviceState = {
  address: "123",
  isSpatializationSupported: true,
  isHeadTrackingSupported: true,
  spatialDeviceType: audio.AudioSpatialDeviceType.SPATIAL_DEVICE_TYPE_IN_EAR_HEADPHONE
}
```

## AudioSpatialDeviceType<sup>11+</sup>

Enumerates the types of spatial devices.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Spatialization

| Name                              |  Value    | Description                      |
| ---------------------------------- | ------ | ------------------------- |
| SPATIAL_DEVICE_TYPE_NONE                   | 0      |  No spatial device. |
| SPATIAL_DEVICE_TYPE_IN_EAR_HEADPHONE       | 1      |  In-ear headphones.      |
| SPATIAL_DEVICE_TYPE_HALF_IN_EAR_HEADPHONE  | 2      |  Half-in-ear headphones.    |
| SPATIAL_DEVICE_TYPE_OVER_EAR_HEADPHONE     | 3      |  Over-ear headphones.      |
| SPATIAL_DEVICE_TYPE_GLASSES                | 4      |  Glasses.      |
| SPATIAL_DEVICE_TYPE_OTHERS                 | 5      |  Other type of the spatial device.|

## ToneType<sup>9+</sup>

Enumerates the tone types of the player.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Tone

| Name                                             |  Value   | Description                         |
| :------------------------------------------------ | :----- | :----------------------------|
| TONE_TYPE_DIAL_0                                  | 0      | DTMF tone of key 0.                |
| TONE_TYPE_DIAL_1                                  | 1      | DTMF tone of key 1.                |
| TONE_TYPE_DIAL_2                                  | 2      | DTMF tone of key 2.                |
| TONE_TYPE_DIAL_3                                  | 3      | DTMF tone of key 3.                |
| TONE_TYPE_DIAL_4                                  | 4      | DTMF tone of key 4.                |
| TONE_TYPE_DIAL_5                                  | 5      | DTMF tone of key 5.                |
| TONE_TYPE_DIAL_6                                  | 6      | DTMF tone of key 6.                |
| TONE_TYPE_DIAL_7                                  | 7      | DTMF tone of key 7.                |
| TONE_TYPE_DIAL_8                                  | 8      | DTMF tone of key 8.                |
| TONE_TYPE_DIAL_9                                  | 9      | DTMF tone of key 9.                |
| TONE_TYPE_DIAL_S                                  | 10     | DTMF tone of the star key (*).                |
| TONE_TYPE_DIAL_P                                  | 11     | DTMF tone of the pound key (#).                |
| TONE_TYPE_DIAL_A                                  | 12     | DTMF tone of key A.                |
| TONE_TYPE_DIAL_B                                  | 13     | DTMF tone of key B.                |
| TONE_TYPE_DIAL_C                                  | 14     | DTMF tone of key C.                |
| TONE_TYPE_DIAL_D                                  | 15     | DTMF tone of key D.                |
| TONE_TYPE_COMMON_SUPERVISORY_DIAL                 | 100    | Supervisory tone - dial tone.         |
| TONE_TYPE_COMMON_SUPERVISORY_BUSY                 | 101    | Supervisory tone - busy.             |
| TONE_TYPE_COMMON_SUPERVISORY_CONGESTION           | 102    | Supervisory tone - congestion.           |
| TONE_TYPE_COMMON_SUPERVISORY_RADIO_ACK            | 103    | Supervisory tone - radio path acknowledgment.     |
| TONE_TYPE_COMMON_SUPERVISORY_RADIO_NOT_AVAILABLE  | 104    | Supervisory tone - radio path not available.    |
| TONE_TYPE_COMMON_SUPERVISORY_CALL_WAITING         | 106    | Supervisory tone - call waiting tone.       |
| TONE_TYPE_COMMON_SUPERVISORY_RINGTONE             | 107    | Supervisory tone - ringing tone.           |
| TONE_TYPE_COMMON_PROPRIETARY_BEEP                 | 200    | Proprietary tone - beep tone.         |
| TONE_TYPE_COMMON_PROPRIETARY_ACK                  | 201    | Proprietary tone - ACK.               |
| TONE_TYPE_COMMON_PROPRIETARY_PROMPT               | 203    | Proprietary tone - PROMPT.            |
| TONE_TYPE_COMMON_PROPRIETARY_DOUBLE_BEEP          | 204    | Proprietary tone - double beep tone.         |

## TonePlayer<sup>9+</sup>

Provides APIs for playing and managing DTMF tones, such as dial tones, ringback tones, supervisory tones, and proprietary tones.
Before calling any API in **TonePlayer**, you must use [createTonePlayer](#audiocreatetoneplayer9) to create a **TonePlayer** instance.

**System API**: This is a system API.

### load<sup>9+</sup>

load(type: ToneType, callback: AsyncCallback&lt;void&gt;): void

Loads the DTMF tone configuration. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Tone

**Parameters**

| Name         | Type                       | Mandatory | Description                           |
| :--------------| :-------------------------- | :-----| :------------------------------ |
| type           | [ToneType](#tonetype9)       | Yes   | Tone type.                |
| callback       | AsyncCallback<void\>        | Yes   | Callback used to return the result. If the operation is successful, **err** is **undefined**; otherwise, **err** is an error object.|

**Example**

```ts
import { BusinessError } from '@ohos.base';

tonePlayer.load(audio.ToneType.TONE_TYPE_DIAL_5, (err: BusinessError) => {
  if (err) {
    console.error(`callback call load failed error: ${err.message}`);
    return;
  } else {
    console.info('callback call load success');
  }
});
```

### load<sup>9+</sup>

load(type: ToneType): Promise&lt;void&gt;

Loads the DTMF tone configuration. This API uses a promise to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Tone

**Parameters**

| Name        | Type                   | Mandatory |  Description            |
| :------------- | :--------------------- | :---  | ---------------- |
| type           | [ToneType](#tonetype9)   | Yes   | Tone type. |

**Return value**

| Type           | Description                       |
| :--------------| :-------------------------- |
| Promise<void\> | Promise that returns no value.|

**Example**

```ts
tonePlayer.load(audio.ToneType.TONE_TYPE_DIAL_1).then(() => {
  console.info('promise call load ');
}).catch(() => {
  console.error('promise call load fail');
});
```

### start<sup>9+</sup>

start(callback: AsyncCallback&lt;void&gt;): void

Starts DTMF tone playing. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Tone

**Parameters**

| Name  | Type                | Mandatory| Description                          |
| :------- | :------------------- | :--- | :----------------------------- |
| callback | AsyncCallback<void\> | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**; otherwise, **err** is an error object.|

**Example**

```ts
import { BusinessError } from '@ohos.base';

tonePlayer.start((err: BusinessError) => {
  if (err) {
    console.error(`callback call start failed error: ${err.message}`);
    return;
  } else {
    console.info('callback call start success');
  }
});
```

### start<sup>9+</sup>

start(): Promise&lt;void&gt;

Starts DTMF tone playing. This API uses a promise to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Tone

**Return value**

| Type          | Description                         |
| :------------- | :---------------------------- |
| Promise<void\> | Promise that returns no value.|

**Example**

```ts
tonePlayer.start().then(() => {
  console.info('promise call start');
}).catch(() => {
  console.error('promise call start fail');
});
```

### stop<sup>9+</sup>

stop(callback: AsyncCallback&lt;void&gt;): void

Stops the tone that is being played. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Tone

**Parameters**

| Name  | Type                | Mandatory| Description                          |
| :------- | :------------------- | :--- | :----------------------------- |
| callback | AsyncCallback<void\> | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**; otherwise, **err** is an error object.|

**Example**

```ts
import { BusinessError } from '@ohos.base';

tonePlayer.stop((err: BusinessError) => {
  if (err) {
    console.error(`callback call stop error: ${err.message}`);
    return;
  } else {
    console.error('callback call stop success ');
  }
});
```

### stop<sup>9+</sup>

stop(): Promise&lt;void&gt;

Stops the tone that is being played. This API uses a promise to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Tone

**Return value**

| Type          | Description                         |
| :------------- | :---------------------------- |
| Promise<void\> | Promise that returns no value.|

**Example**

```ts
tonePlayer.stop().then(() => {
  console.info('promise call stop finish');
}).catch(() => {
  console.error('promise call stop fail');
});
```

### release<sup>9+</sup>

release(callback: AsyncCallback&lt;void&gt;): void

Releases the resources associated with the **TonePlayer** instance. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Tone

**Parameters**

| Name  | Type                | Mandatory| Description                           |
| :------- | :------------------- | :--- | :---------------------------- |
| callback | AsyncCallback<void\> | Yes  | Callback used to return the result. If the operation is successful, **err** is **undefined**; otherwise, **err** is an error object.|

**Example**

```ts
import { BusinessError } from '@ohos.base';

tonePlayer.release((err: BusinessError) => {
  if (err) {
    console.error(`callback call release failed error: ${err.message}`);
    return;
  } else {
    console.info('callback call release success ');
  }
});
```

### release<sup>9+</sup>

release(): Promise&lt;void&gt;

Releases the resources associated with the **TonePlayer** instance. This API uses a promise to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Multimedia.Audio.Tone

**Return value**

| Type          | Description                         |
| :------------- | :---------------------------- |
| Promise<void\> | Promise that returns no value.|

**Example**

```ts
tonePlayer.release().then(() => {
  console.info('promise call release');
}).catch(() => {
  console.error('promise call release fail');
});
```
