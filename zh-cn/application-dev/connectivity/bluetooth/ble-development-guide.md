# 广播与扫描开发指导

## 简介
广播与扫描，主要提供了蓝牙设备的开启广播、关闭广播、开启扫描、关闭扫描方法，通过广播和扫描发现对端蓝牙设备，实现低功耗的通信。

## 场景介绍
主要场景有：

- 开启、关闭广播
- 开启、关闭扫描

## 接口说明

完整的 JS API 说明以及实例代码请参考：[BLE 接口](../../reference/apis-connectivity-kit/js-apis-bluetooth-ble.md)。

具体接口说明如下表。

| 接口名                             | 功能描述                                                                       |
| ---------------------------------- | ------------------------------------------------------------------------------ |
| startBLEScan()                     | 发起BLE扫描流程。                                                               |
| stopBLEScan()                      | 停止BLE扫描流程。                                                                |
| startAdvertising()                 | 开始发送BLE广播。                                                                |
| stopAdvertising()                  | 停止发送BLE广播。                                                                |
| on(type: 'advertisingStateChange') | 订阅BLE广播状态。                                                                |
| off(type: 'advertisingStateChange')| 取消订阅BLE广播状态。                                                            |
| on(type: 'BLEDeviceFind')          | 订阅BLE设备发现上报事件。                                                        |
| off(type: 'BLEDeviceFind')         | 取消订阅BLE设备发现上报事件。                                                     |

## 主要场景开发步骤

### 开启、关闭广播
1. import需要的ble模块。
2. 开启设备的蓝牙。
3. 需要SystemCapability.Communication.Bluetooth.Core系统能力。
4. 开启广播，对端设备扫描该广播。
5. 关闭广播。
6. 示例代码：

```ts
import ble from '@ohos.bluetooth.ble';
import { BusinessError } from '@ohos.base';

// 开启广播
let manufactureValueBuffer = new Uint8Array(4);
manufactureValueBuffer[0] = 1;
manufactureValueBuffer[1] = 2;
manufactureValueBuffer[2] = 3;
manufactureValueBuffer[3] = 4;
let serviceValueBuffer = new Uint8Array(4);
serviceValueBuffer[0] = 5;
serviceValueBuffer[1] = 6;
serviceValueBuffer[2] = 7;
serviceValueBuffer[3] = 8;
let setting: ble.AdvertiseSetting = {
  interval: 150,
  txPower: 0,
  connectable: true
};
let manufactureDataUnit: ble.ManufactureData = {
  manufactureId: 4567,
  manufactureValue: manufactureValueBuffer.buffer
};
let serviceDataUnit: ble.ServiceData = {
  serviceUuid: "00001888-0000-1000-8000-00805f9b34fb",
  serviceValue: serviceValueBuffer.buffer
};
let advData: ble.AdvertiseData = {
  serviceUuids: ["00001888-0000-1000-8000-00805f9b34fb"],
  manufactureData: [manufactureDataUnit],
  serviceData: [serviceDataUnit],
  includeDeviceName: false // 表示是否携带设备名，可选参数。注意带上设备名时广播包长度不能超出31个字节。
};
let advResponse: ble.AdvertiseData = {
  serviceUuids: ["00001888-0000-1000-8000-00805f9b34fb"],
  manufactureData: [manufactureDataUnit],
  serviceData: [serviceDataUnit]
};

ble.startAdvertising(setting, advData, advResponse);
console.info('startAdvertising success');

// 关闭广播
ble.stopAdvertising();
console.info('stopAdvertising success');
```

7. 错误码请参见[蓝牙服务子系统错误码](../../reference/apis-connectivity-kit/errorcode-bluetoothManager.md)。
8. 如何验证：执行开启广播的用例代码，记录日志“startAdvertising success”，并且使用另外一部手机安装nrfConnect软件开启扫描，如果扫描到该广播，广播内容“Manufacturer data的值为:0x01020304，Service Data的值为:0x05060708”，表示开启广播成功。关闭广播后，扫描不到该内容的广播。

### 开启、关闭扫描
1. import需要的ble模块。
2. 开启设备的蓝牙。
3. 需要SystemCapability.Communication.Bluetooth.Core系统能力。
4. 对端设备开启广播。
5. 本端设备开启扫描，获取扫描结果。
6. 关闭扫描。
7. 示例代码:

```ts
import ble from '@ohos.bluetooth.ble';
import { BusinessError } from '@ohos.base';

// 开启扫描
let scanFilter: ble.ScanFilter = {
  name: 'Jackistang'
};
let scanOptions: ble.ScanOptions = {
  interval: 500,
  dutyMode: ble.ScanDuty.SCAN_MODE_LOW_POWER,
  matchMode: ble.MatchMode.MATCH_MODE_AGGRESSIVE
}
ble.startBLEScan([scanFilter], scanOptions);
console.info('startBleScan success')

// 接收扫描结果
ble.on('BLEDeviceFind', (data) => {
  if (data.length > 0) {
    console.info('BLE scan result = ' + data[0].deviceName);
  }
});

// 关闭扫描
ble.stopBLEScan();
console.info('stopBleScan success');
```

8. 错误码请参见[蓝牙服务子系统错误码](../../reference/apis-connectivity-kit/errorcode-bluetoothManager.md)。
9. 如何验证：使用另外一部手机安装nrfConnect软件并且配置好广播，设备名称修改为“Jackistang”，开启广播。然后测试手机开启扫描，大概每隔0.5秒记录日志“BLE scan result =  = Jackistang”，则表示开启扫描成功。关闭扫描后，不会再有该记录日志产生。