# USB服务开发指导



## 场景介绍

Host模式下，可以获取到已经连接的USB设备列表，并根据需要打开和关闭设备、控制设备权限、进行数据传输等。


## 接口说明

USB服务主要提供的功能有：查询USB设备列表、批量数据传输、控制命令传输、权限控制等。

USB类开放能力如下，具体请查阅[API参考文档](../reference/apis/js-apis-usbManager.md)。

**表1** USB类的开放能力接口

| 接口名                                                       | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| hasRight(deviceName: string): boolean                         | 判断是否有权访问该设备 |
| requestRight(deviceName: string): Promise&lt;boolean&gt;       | 请求软件包的临时权限以访问设备。使用Promise异步回调。                        |
| removeRight(deviceName: string): boolean | 移除软件包对设备的访问权限。|
| connectDevice(device: USBDevice): Readonly&lt;USBDevicePipe&gt; | 根据`getDevices()`返回的设备信息打开USB设备。                |
| getDevices(): Array&lt;Readonly&lt;USBDevice&gt;&gt;          | 获取接入主设备的USB设备列表。如果没有设备接入，那么将会返回一个空的列表。                                            |
| setConfiguration(pipe: USBDevicePipe, config: USBConfiguration): number | 设置设备的配置。                                             |
| setInterface(pipe: USBDevicePipe, iface: USBInterface): number   | 设置设备的接口。                                             |
| claimInterface(pipe: USBDevicePipe, iface: USBInterface, force ?: boolean): number | 注册通信接口。                                                   |
| bulkTransfer(pipe: USBDevicePipe, endpoint: USBEndpoint, buffer: Uint8Array, timeout ?: number): Promise&lt;number&gt; | 批量传输。                                                   |
| closePipe(pipe: USBDevicePipe): number                         | 关闭设备消息控制通道。                                       |
| releaseInterface(pipe: USBDevicePipe, iface: USBInterface): number | 释放注册过的通信接口。                                                   |
| getFileDescriptor(pipe: USBDevicePipe): number                 | 获取文件描述符。                                             |
| getRawDescriptor(pipe: USBDevicePipe): Uint8Array              | 获取原始的USB描述符。                                        |
| controlTransfer(pipe: USBDevicePipe, controlparam: USBControlParams, timeout ?: number): Promise&lt;number&gt; | 控制传输。                                                   |


## 开发步骤

USB设备可作为Host设备连接Device设备进行数据传输。开发示例如下：


1. 获取设备列表。

   ```ts
   // 导入USB接口api包。
   import usb from '@ohos.usbManager';
   // 获取设备列表。
   let deviceList : Array<usb.USBDevice> = usb.getDevices();
   /*
   deviceList结构示例
   [
     {
       name: "1-1",
       serial: "",
       manufacturerName: "",
       productName: "",
       version: "",
       vendorId: 7531,
       productId: 2,
       clazz: 9,
       subClass: 0,
       protocol: 1,
       devAddress: 1,
       busNum: 1,
       configs: [
         {
           id: 1,
           attributes: 224,
           isRemoteWakeup: true,
           isSelfPowered: true,
           maxPower: 0,
           name: "1-1",
           interfaces: [
             {
               id: 0,
               protocol: 0,
               clazz: 9,
               subClass: 0,
               alternateSetting: 0,
               name: "1-1",
               endpoints: [
                 {
                   address: 129,
                   attributes: 3,
                   interval: 12,
                   maxPacketSize: 4,
                   direction: 128,
                   number: 1,
                   type: 3,
                   interfaceId: 0,
                 }
               ]
             }
           ]
         }
       ]
     }
   ]
   */
   ```

2. 获取设备操作权限。

   ```ts
   import usb from '@ohos.usbManager';
   import { BusinessError } from '@ohos.base';

   let deviceName : string = deviceList[0].name;
   // 申请操作指定的device的操作权限。
   usb.requestRight(deviceName).then((hasRight : boolean) => {
     console.info("usb device request right result: " + hasRight);
   }).catch((error : BusinessError)=> {
     console.info("usb device request right failed : " + error);
   });
   ```

3. 打开Device设备。

   ```ts
   // 打开设备，获取数据传输通道。
   let pipe : USBDevicePipe = usb.connectDevice(deviceList[0]);
   let interface1 : number = deviceList[0].configs[0].interfaces[0];
   /*
    打开对应接口，在设备信息（deviceList）中选取对应的interface。
   interface1为设备配置中的一个接口。
   */
   usb.claimInterface(pipe, interface1, true);
   ```

4. 数据传输。

   ```ts
   import usb from '@ohos.usbManager';
   import { BusinessError } from '@ohos.base';
   /*
    读取数据，在device信息中选取对应数据接收的endpoint来做数据传输
   （endpoint.direction == 0x80）；dataUint8Array是要读取的数据，类型为Uint8Array。
   */
   let inEndpoint : USBEndpoint = interface1.endpoints[2];
   let outEndpoint : USBEndpoint = interface1.endpoints[1];
   let dataUint8Array : Array<number> = new Uint8Array(1024);
   usb.bulkTransfer(pipe, inEndpoint, dataUint8Array, 15000).then((dataLength : number) => {
   if (dataLength >= 0) {
     console.info("usb readData result Length : " + dataLength);
   } else {
     console.info("usb readData failed : " + dataLength);
   }
   }).catch((error : BusinessError) => {
   console.info("usb readData error : " + JSON.stringify(error));
   });
   // 发送数据，在device信息中选取对应数据发送的endpoint来做数据传输。（endpoint.direction == 0）
   usb.bulkTransfer(pipe, outEndpoint, dataUint8Array, 15000).then((dataLength : number) => {
     if (dataLength >= 0) {
       console.info("usb writeData result write length : " + dataLength);
     } else {
       console.info("writeData failed");
     }
   }).catch((error : BusinessError) => {
     console.info("usb writeData error : " + JSON.stringify(error));
   });
   ```

5. 释放接口，关闭设备。

   ```ts
   usb.releaseInterface(pipe, interface1);
   usb.closePipe(pipe);
   ```

## 相关实例

针对USB管理开发，有以下相关实例可供参考：

- [`USBManager`：USB管理（ArkTS）（API9）](https://gitee.com/openharmony/applications_app_samples/tree/OpenHarmony-3.2-Release/code/BasicFeature/DeviceManagement/USBManager)