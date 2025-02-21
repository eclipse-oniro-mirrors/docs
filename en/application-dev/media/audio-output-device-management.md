# Audio Output Device Management

If a device is connected to multiple audio output devices, you can use **AudioRoutingManager** to specify an audio output device to play audio. For details about the API reference, see [AudioRoutingManager](../reference/apis/js-apis-audio.md#audioroutingmanager9).

## Creating an AudioRoutingManager Instance

Before using **AudioRoutingManager** to manage audio devices, import the audio module and create an **AudioManager** instance.

```ts
import audio from '@ohos.multimedia.audio'; // Import the audio module.

let audioManager = audio.getAudioManager(); // Create an AudioManager instance.

let audioRoutingManager = audioManager.getRoutingManager(); // Call an API of AudioManager to create an AudioRoutingManager instance.
```

## Supported Audio Output Device Types

The table below lists the supported audio output devices.

| Name| Value| Description| 
| -------- | -------- | -------- |
| EARPIECE | 1 | Earpiece.| 
| SPEAKER | 2 | Speaker.| 
| WIRED_HEADSET | 3 | Wired headset with a microphone.| 
| WIRED_HEADPHONES | 4 | Wired headset without microphone.| 
| BLUETOOTH_SCO | 7 | Bluetooth device using Synchronous Connection Oriented (SCO) links.| 
| BLUETOOTH_A2DP | 8 | Bluetooth device using Advanced Audio Distribution Profile (A2DP) links.| 
| USB_HEADSET | 22 | USB Type-C headset.| 

## Obtaining Output Device Information

Use **getDevices()** to obtain information about all the output devices.

```ts
audioRoutingManager.getDevices(audio.DeviceFlag.OUTPUT_DEVICES_FLAG).then((data) => {
  console.info('Promise returned to indicate that the device list is obtained.');
});
```

## Listening for Device Connection State Changes

Set a listener to listen for changes of the device connection state. When a device is connected or disconnected, a callback is triggered.

```ts
// Listen for connection state changes of audio devices.
audioRoutingManager.on('deviceChange', audio.DeviceFlag.OUTPUT_DEVICES_FLAG, (deviceChanged) => {
  console.info('device change type: ' + deviceChanged.type); // Device connection state change. The value 0 means that the device is connected and 1 means that the device is disconnected.
  console.info('device descriptor size : ' + deviceChanged.deviceDescriptors.length);
  console.info('device change descriptor: ' + deviceChanged.deviceDescriptors[0].deviceRole); // Device role.
  console.info('device change descriptor: ' + deviceChanged.deviceDescriptors[0].deviceType); // Device type.
});

// Cancel the listener for the connection state changes of audio devices.
audioRoutingManager.off('deviceChange', (deviceChanged) => {
  console.info('Should be no callback.');
});
```

## Selecting an Audio Output Device (for System Applications only)

Currently, only one output device can be selected, and the device ID is used as the unique identifier. For details about audio device descriptors, see [AudioDeviceDescriptors](../reference/apis/js-apis-audio.md#audiodevicedescriptors).

> **NOTE**
> 
> The user can connect to a group of audio devices (for example, a pair of Bluetooth headsets), but the system treats them as one device (a group of devices that share the same device ID).

```ts
let outputAudioDeviceDescriptor = [{
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
}];

async function selectOutputDevice(){
  audioRoutingManager.selectOutputDevice(outputAudioDeviceDescriptor).then(() => {
    console.info('Invoke selectOutputDevice succeeded.');
  }).catch((err) => {
    console.error(`Invoke selectOutputDevice failed, code is ${err.code}, message is ${err.message}`);
  });
}
```
