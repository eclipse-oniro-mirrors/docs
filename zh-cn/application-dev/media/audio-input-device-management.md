# 音频输入设备管理

有时设备同时连接多个音频输入设备，需要指定音频输入设备进行音频录制，此时需要使用AudioRoutingManager接口进行输入设备的管理，API说明可以参考[AudioRoutingManager API文档](../reference/apis/js-apis-audio.md#audioroutingmanager9)。

## 创建AudioRoutingManager实例

在使用AudioRoutingManager管理音频设备前，需要先导入模块并创建实例。

```ts
import audio from '@ohos.multimedia.audio';  // 导入audio模块

let audioManager = audio.getAudioManager();  // 需要先创建AudioManager实例

let audioRoutingManager = audioManager.getRoutingManager();  // 再调用AudioManager的方法创建AudioRoutingManager实例
```

## 支持的音频输入设备类型

目前支持的音频输入设备见下表：

| 名称 | 值 | 说明 | 
| -------- | -------- | -------- |
| WIRED_HEADSET | 3 | 有线耳机，带麦克风。 | 
| BLUETOOTH_SCO | 7 | 蓝牙设备SCO（Synchronous Connection Oriented）连接。 | 
| MIC | 15 | 麦克风。 | 
| USB_HEADSET | 22 | USB耳机，带麦克风。 | 

## 获取输入设备信息

使用getDevices()方法可以获取当前所有输入设备的信息。

```ts
audioRoutingManager.getDevices(audio.DeviceFlag.INPUT_DEVICES_FLAG).then((data) => {
  console.info('Promise returned to indicate that the device list is obtained.');
});
```

## 监听设备连接状态变化

可以设置监听事件来监听设备连接状态的变化，当有设备连接或断开时触发回调：

```ts
// 监听音频设备状态变化
audioRoutingManager.on('deviceChange', audio.DeviceFlag.INPUT_DEVICES_FLAG, (deviceChanged) => {
  console.info('device change type : ' + deviceChanged.type);  // 设备连接状态变化，0为连接，1为断开连接
  console.info('device descriptor size : ' + deviceChanged.deviceDescriptors.length);
  console.info('device change descriptor : ' + deviceChanged.deviceDescriptors[0].deviceRole);  // 设备角色
  console.info('device change descriptor : ' + deviceChanged.deviceDescriptors[0].deviceType);  // 设备类型
});

// 取消监听音频设备状态变化
audioRoutingManager.off('deviceChange', (deviceChanged) => {
  console.info('Should be no callback.');
});
```

## 选择音频输入设备（仅对系统应用开放）

选择音频输入设备，当前只能选择一个输入设备，以设备id作为唯一标识。AudioDeviceDescriptors的具体信息可以参考[AudioDeviceDescriptors](../reference/apis/js-apis-audio.md#audiodevicedescriptors)。

> **说明：**
> 
> 用户可以选择连接一组音频设备（如一对蓝牙耳机），但系统侧只感知为一个设备，该组设备共用一个设备id。

```ts
let inputAudioDeviceDescriptor = [{
    deviceRole : audio.DeviceRole.INPUT_DEVICE,
    deviceType : audio.DeviceType.EARPIECE,
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

async function getRoutingManager(){
    audioRoutingManager.selectInputDevice(inputAudioDeviceDescriptor).then(() => {
      console.info('Invoke selectInputDevice succeeded.');
    }).catch((err) => {
      console.error(`Invoke selectInputDevice failed, code is ${err.code}, message is ${err.message}`);
    });
}

```
