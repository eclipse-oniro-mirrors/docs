# Distributed Audio Playback (for System Applications Only)

Distributed audio playback enables an application to continue audio playback on another device in the same network.

You can use distributed audio playback to transfer all audio streams or the specified audio stream being played on the current device to a remote device.

## How to Develop

Before continuing audio playback on another device in the same network, you must obtain the device list on the network and listen for device connection state changes. For details, see [Audio Output Device Management](audio-output-device-management.md).

When obtaining the device list on the network, you can specify **DeviceFlag** to filter out the required devices.

| Name| Description| 
| -------- | -------- |
| NONE_DEVICES_FLAG<sup>9+</sup> | None. This is a system API.| 
| OUTPUT_DEVICES_FLAG | Local output device.| 
| INPUT_DEVICES_FLAG | Local input device.| 
| ALL_DEVICES_FLAG | Local input and output device.| 
| DISTRIBUTED_OUTPUT_DEVICES_FLAG<sup>9+</sup> | Remote output device. This is a system API.| 
| DISTRIBUTED_INPUT_DEVICES_FLAG<sup>9+</sup> | Remote input device. This is a system API.| 
| ALL_DISTRIBUTED_DEVICES_FLAG<sup>9+</sup> | Remote input and output device. This is a system API.| 

For details about the API reference, see [AudioRoutingManager](../reference/apis/js-apis-audio.md#audioroutingmanager9).

### Continuing the Playing of All Audio Streams

1. [Obtain the output device information](audio-output-device-management.md#obtaining-output-device-information).

2. Create an **AudioDeviceDescriptor** instance to describe an audio output device.

3. Call **selectOutputDevice** to select a remote device, on which all the audio streams will continue playing.

```ts
let outputAudioDeviceDescriptor = [{
  deviceRole: audio.DeviceRole.OUTPUT_DEVICE,
  deviceType: audio.DeviceType.SPEAKER,
  id: 1,
  name: "",
  address: "",
  sampleRates: [44100],
  channelCounts: [2],
  channelMasks: [0],
  networkId: audio.LOCAL_NETWORK_ID,
  interruptGroupId: 1,
  volumeGroupId: 1,
}];

async function selectOutputDevice() {
  audioRoutingManager.selectOutputDevice(outputAudioDeviceDescriptor, (err) => {
    if (err) {
      console.error(`Invoke selectOutputDevice failed, code is ${err.code}, message is ${err.message}`);
    } else {
      console.info('Invoke selectOutputDevice succeeded.');
    }
  });
}
```

### Continuing the Playing of the Specified Audio Stream

1. [Obtain the output device information](audio-output-device-management.md#obtaining-output-device-information).

2. Create an **AudioRendererFilter** instance, with **uid** to specify an application and **rendererId** to specify an audio stream.

3. Create an **AudioDeviceDescriptor** instance to describe an audio output device.

4. Call **selectOutputDeviceByFilter** to select a remote device, on which the specified audio stream will continue playing.
 
```ts
let outputAudioRendererFilter = {
  uid: 20010041,
  rendererInfo: {
    content: audio.ContentType.CONTENT_TYPE_MUSIC,
    usage: audio.StreamUsage.STREAM_USAGE_MEDIA,
    rendererFlags: 0 },
  rendererId: 0 };

let outputAudioDeviceDescriptor = [{
  deviceRole: audio.DeviceRole.OUTPUT_DEVICE,
  deviceType: audio.DeviceType.SPEAKER,
  id: 1,
  name: "",
  address: "",
  sampleRates: [44100],
  channelCounts: [2],
  channelMasks: [0],
  networkId: audio.LOCAL_NETWORK_ID,
  interruptGroupId: 1,
  volumeGroupId: 1,
}];

async function selectOutputDeviceByFilter() {
  audioRoutingManager.selectOutputDeviceByFilter(outputAudioRendererFilter, outputAudioDeviceDescriptor, (err) => {
    if (err) {
      console.error(`Invoke selectOutputDeviceByFilter failed, code is ${err.code}, message is ${err.message}`);
    } else {
      console.info('Invoke selectOutputDeviceByFilter succeeded.');
    }
  });
}
```
