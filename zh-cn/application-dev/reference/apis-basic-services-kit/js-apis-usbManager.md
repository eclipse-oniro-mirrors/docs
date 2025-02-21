# @ohos.usbManager (USB管理)

本模块主要提供管理USB设备的相关功能，包括主设备上查询USB设备列表、批量数据传输、控制命令传输、权限控制等；从设备上端口管理、功能切换及查询等。

>  **说明：**
> 
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import { usbManager } from '@kit.BasicServicesKit';
```

## usbManager.getDevices

getDevices(): Array&lt;Readonly&lt;USBDevice&gt;&gt;

获取接入主设备的USB设备列表。如果没有设备接入，那么将会返回一个空的列表。

**系统能力：**  SystemCapability.USB.USBManager

**返回值：**

| 类型                                                   | 说明      |
| ---------------------------------------------------- | ------- |
| Array&lt;Readonly&lt;[USBDevice](#usbdevice)&gt;&gt; | 设备信息列表。 |

**示例：**

```ts
let devicesList: Array<usbManager.USBDevice> = usbManager.getDevices();
console.log(`devicesList = ${devicesList}`);
/*
devicesList 返回的数据结构,此处提供一个简单的示例，如下
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
              },
            ],
          },
        ],
      },
    ],
  },
]
*/
```

## usbManager.connectDevice

connectDevice(device: USBDevice): Readonly&lt;USBDevicePipe&gt;

根据getDevices()返回的设备信息打开USB设备。

需要调用[usbManager.getDevices](#usbmanagergetdevices)获取设备信息以及device，再调用[usbManager.requestRight](#usbmanagerrequestright)请求使用该设备的权限。

**系统能力：**  SystemCapability.USB.USBManager

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | ---------------- |
| device | [USBDevice](#usbdevice) | 是 | USB设备信息，用getDevices获取的busNum和devAddress确定设备，当前其他属性不做处理。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Readonly&lt;[USBDevicePipe](#usbdevicepipe)&gt; | 指定的传输通道对象。 |

**错误码：**

以下错误码的详细介绍参见[USB服务错误码](errorcode-usb.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401      | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |
| 14400001 | Permission denied. Call requestRight to get the permission first. |

**示例：**

```ts
let devicesList: Array<usbManager.USBDevice> = usbManager.getDevices();
if (devicesList.length == 0) {
  console.log(`device list is empty`);
}

let device: usbManager.USBDevice = devicesList[0];
usbManager.requestRight(device.name);
let devicepipe: usbManager.USBDevicePipe = usbManager.connectDevice(device);
console.log(`devicepipe = ${devicepipe}`);
```

## usbManager.hasRight

hasRight(deviceName: string): boolean

判断是否有权访问该设备。

如果“使用者”（如各种App或系统）有权访问设备则返回true；无权访问设备则返回false。

**系统能力：**  SystemCapability.USB.USBManager

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| deviceName | string | 是 | 设备名称，来自getDevices获取的设备列表。 |

**错误码：**

以下错误码的详细介绍请参见[USB服务错误码](errorcode-usb.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401      | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | true表示有访问设备的权限，false表示没有访问设备的权限。 |

**示例：**

```ts
let devicesList: Array<usbManager.USBDevice> = usbManager.getDevices();
if (devicesList.length == 0) {
  console.log(`device list is empty`);
}

let device: usbManager.USBDevice = devicesList[0];
usbManager.requestRight(device.name);
let right: boolean = usbManager.hasRight(device.name);
console.log(`${right}`);
```

## usbManager.requestRight

requestRight(deviceName: string): Promise&lt;boolean&gt;

请求软件包的临时权限以访问设备。使用Promise异步回调。系统应用默认拥有访问设备权限，无需调用此接口申请。

**系统能力：**  SystemCapability.USB.USBManager

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| deviceName | string | 是 | 设备名称，来自getDevices获取的设备列表。|

**错误码：**

以下错误码的详细介绍请参见[USB服务错误码](errorcode-usb.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401      | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;boolean&gt; | Promise对象，返回临时权限的申请结果。返回true表示临时权限申请成功；返回false则表示临时权限申请失败。 |

**示例：**

```ts
let devicesList: Array<usbManager.USBDevice> = usbManager.getDevices();
if (devicesList.length == 0) {
  console.log(`device list is empty`);
}

let device: usbManager.USBDevice = devicesList[0];
usbManager.requestRight(device.name).then(ret => {
  console.log(`requestRight = ${ret}`);
});
```

## usbManager.removeRight

removeRight(deviceName: string): boolean

移除软件包访问设备的权限。系统应用默认拥有访问设备权限，调用此接口不会产生影响。

**系统能力：**  SystemCapability.USB.USBManager

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| deviceName | string | 是 | 设备名称，来自getDevices获取的设备列表。|

**错误码：**

以下错误码的详细介绍请参见[USB服务错误码](errorcode-usb.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401      | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 返回权限移除结果。返回true表示权限移除成功；返回false则表示权限移除失败。 |

**示例：**

```ts
let devicesList: Array<usbManager.USBDevice> = usbManager.getDevices();
if (devicesList.length == 0) {
  console.log(`device list is empty`);
}

let device: usbManager.USBDevice = devicesList[0];
if (usbManager.removeRight(device.name)) {
  console.log(`Succeed in removing right`);
}
```

## usbManager.claimInterface

claimInterface(pipe: USBDevicePipe, iface: USBInterface, force ?: boolean): number

注册通信接口。

需要调用[usbManager.getDevices](#usbmanagergetdevices)获取设备信息以及interfaces；调用[usbManager.requestRight](#usbmanagerrequestright)获取设备请求权限；调用[usbManager.connectDevice](#usbmanagerconnectdevice)接口得到devicepipe作为参数。

> **说明：** 
>
> 单次批量传输的传输数据总量（包括pipe、endpoint、buffer、timeout）请控制在200KB以下。

**系统能力：**  SystemCapability.USB.USBManager

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| pipe | [USBDevicePipe](#usbdevicepipe) | 是 | 用于确定总线号和设备地址，需要调用connectDevice获取。|
| iface | [USBInterface](#usbinterface) | 是 | 用于确定需要获取接口的索引，需要调用getDevices获取设备信息并通过id确定唯一接口。|
| force | boolean | 否 | 可选参数，是否强制获取。默认值为false&nbsp;，表示不强制获取，用户按需选择。|

**错误码：**

以下错误码的详细介绍请参见[USB服务错误码](errorcode-usb.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401      | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 注册通信接口成功返回0；注册通信接口失败返回其他错误码。 |

**示例：**

```ts
let devicesList: Array<usbManager.USBDevice> = usbManager.getDevices();
if (devicesList.length == 0) {
  console.log(`device list is empty`);
}

let device: usbManager.USBDevice = devicesList[0];
usbManager.requestRight(device.name);
let devicepipe: usbManager.USBDevicePipe = usbManager.connectDevice(device);
let interfaces: usbManager.USBInterface = device.configs[0].interfaces[0];
let ret: number= usbManager.claimInterface(devicepipe, interfaces);
console.log(`claimInterface = ${ret}`);
```

## usbManager.releaseInterface

releaseInterface(pipe: USBDevicePipe, iface: USBInterface): number

释放注册过的通信接口。

需要调用[usbManager.claimInterface](#usbmanagerclaiminterface)先获取接口，才能使用此方法释放接口。

**系统能力：**  SystemCapability.USB.USBManager

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| pipe | [USBDevicePipe](#usbdevicepipe) | 是 | 用于确定总线号和设备地址，需要调用connectDevice获取。|
| iface | [USBInterface](#usbinterface) | 是 | 用于确定需要释放接口的索引，需要调用getDevices获取设备信息并通过id确定唯一接口。|

**错误码：**

以下错误码的详细介绍请参见[USB服务错误码](errorcode-usb.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401      | Parameter error.Possible causes:1.Mandatory parameters are left unspecified.2.Incorrect parameter types. |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 释放接口成功返回0；释放接口失败返回其他错误码。 |

**示例：**

```ts
let devicesList: Array<usbManager.USBDevice> = usbManager.getDevices();
if (devicesList.length == 0) {
  console.log(`device list is empty`);
}

let device: usbManager.USBDevice = devicesList[0];
usbManager.requestRight(device.name);
let devicepipe: usbManager.USBDevicePipe = usbManager.connectDevice(device);
let interfaces: usbManager.USBInterface = device.configs[0].interfaces[0];
let ret: number = usbManager.claimInterface(devicepipe, interfaces);
ret = usbManager.releaseInterface(devicepipe, interfaces);
console.log(`releaseInterface = ${ret}`);
```

## usbManager.setConfiguration

setConfiguration(pipe: USBDevicePipe, config: USBConfiguration): number

设置设备配置。

需要调用[usbManager.getDevices](#usbmanagergetdevices)获取设备信息以及config；调用[usbManager.requestRight](#usbmanagerrequestright)获取设备请求权限；调用[usbManager.connectDevice](#usbmanagerconnectdevice)得到devicepipe作为参数。

**系统能力：**  SystemCapability.USB.USBManager

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| pipe | [USBDevicePipe](#usbdevicepipe) | 是 | 用于确定总线号和设备地址，需要调用connectDevice获取。|
| config | [USBConfiguration](#usbconfiguration) | 是 | 用于确定需要设置的配置，需要调用getDevices获取设备信息并通过id用于确定唯一设置。|

**错误码：**

以下错误码的详细介绍请参见[USB服务错误码](errorcode-usb.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401      | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 设置设备配置成功返回0；设置设备配置失败返回其他错误码。 |

**示例：**

```ts
let devicesList: Array<usbManager.USBDevice> = usbManager.getDevices();
if (devicesList.length == 0) {
  console.log(`device list is empty`);
}

let device: usbManager.USBDevice = devicesList[0];
usbManager.requestRight(device.name);
let devicepipe: usbManager.USBDevicePipe = usbManager.connectDevice(device);
let config: usbManager.USBConfiguration = device.configs[0];
let ret: number= usbManager.setConfiguration(devicepipe, config);
console.log(`setConfiguration = ${ret}`);
```

## usbManager.setInterface

setInterface(pipe: USBDevicePipe, iface: USBInterface): number

设置设备接口。

需要调用[usbManager.getDevices](#usbmanagergetdevices)获取设备列表以及interfaces；调用[usbManager.requestRight](#usbmanagerrequestright)获取设备请求权限；调用[usbManager.connectDevice](#usbmanagerconnectdevice)得到devicepipe作为参数；调用[usbManager.claimInterface](#usbmanagerclaiminterface)注册通信接口。

**系统能力：**  SystemCapability.USB.USBManager

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| pipe | [USBDevicePipe](#usbdevicepipe) | 是 | 用于确定总线号和设备地址，需要调用connectDevice获取。|
| iface | [USBInterface](#usbinterface)   | 是 | 用于确定需要设置的接口，需要调用getDevices获取设备信息并通过id和alternateSetting确定唯一接口。|

**错误码：**

以下错误码的详细介绍请参见[USB服务错误码](errorcode-usb.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401      | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 设置设备接口成功返回0；设置设备接口失败返回其他错误码。 |

**示例：**

```ts
let devicesList: Array<usbManager.USBDevice> = usbManager.getDevices();
if (devicesList.length == 0) {
  console.log(`device list is empty`);
}

let device: usbManager.USBDevice = devicesList[0];
usbManager.requestRight(device.name);
let devicepipe: usbManager.USBDevicePipe = usbManager.connectDevice(device);
let interfaces: usbManager.USBInterface = device.configs[0].interfaces[0];
let ret: number = usbManager.claimInterface(devicepipe, interfaces);
ret = usbManager.setInterface(devicepipe, interfaces);
console.log(`setInterface = ${ret}`);
```

## usbManager.getRawDescriptor

getRawDescriptor(pipe: USBDevicePipe): Uint8Array

获取原始的USB描述符。

需要调用[usbManager.getDevices](#usbmanagergetdevices)获取设备列表；调用[usbManager.requestRight](#usbmanagerrequestright)获取设备请求权限；调用[usbManager.connectDevice](#usbmanagerconnectdevice)接口得到devicepipe作为参数。

**系统能力：**  SystemCapability.USB.USBManager

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| pipe | [USBDevicePipe](#usbdevicepipe) | 是 | 用于确定总线号和设备地址，需要调用connectDevice获取。|

**错误码：**

以下错误码的详细介绍请参见[USB服务错误码](errorcode-usb.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401      | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Uint8Array | 返回获取的原始数据；失败返回undefined。 |

**示例：**

```ts
let devicesList: Array<usbManager.USBDevice> = usbManager.getDevices();
if (devicesList.length == 0) {
  console.log(`device list is empty`);
}

usbManager.requestRight(devicesList[0].name);
let devicepipe: usbManager.USBDevicePipe = usbManager.connectDevice(devicesList[0]);
let ret: Uint8Array = usbManager.getRawDescriptor(devicepipe);
```

## usbManager.getFileDescriptor

getFileDescriptor(pipe: USBDevicePipe): number

获取文件描述符。

需要调用[usbManager.getDevices](#usbmanagergetdevices)获取设备列表；调用[usbManager.requestRight](#usbmanagerrequestright)获取设备请求权限；调用[usbManager.connectDevice](#usbmanagerconnectdevice)接口得到devicepipe作为参数。

**系统能力：**  SystemCapability.USB.USBManager

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| pipe | [USBDevicePipe](#usbdevicepipe) | 是 | 用于确定总线号和设备地址，需要调用connectDevice获取。|

**错误码：**

以下错误码的详细介绍请参见[USB服务错误码](errorcode-usb.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401      | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |

**返回值：**

| 类型     | 说明                   |
| ------ | -------------------- |
| number | 返回设备对应的文件描述符；失败返回-1。 |

**示例：**

```ts
let devicesList: Array<usbManager.USBDevice> = usbManager.getDevices();
if (devicesList.length == 0) {
  console.log(`device list is empty`);
}

usbManager.requestRight(devicesList[0].name);
let devicepipe: usbManager.USBDevicePipe = usbManager.connectDevice(devicesList[0]);
let ret: number = usbManager.getFileDescriptor(devicepipe);
```

## usbManager.controlTransfer<sup>(deprecated)</sup>

controlTransfer(pipe: USBDevicePipe, controlparam: USBControlParams, timeout ?: number): Promise&lt;number&gt;

控制传输。

需要调用[usbManager.getDevices](#usbmanagergetdevices)获取设备列表；调用[usbManager.requestRight](#usbmanagerrequestright)获取设备请求权限；调用[usbManager.connectDevice](#usbmanagerconnectdevice)接口得到devicepipe作为参数。

**说明：**

> 从 API version 9开始支持，从API version 12开始废弃。建议使用 [usbControlTransfer](#usbmanagerusbcontroltransfer12) 替代。

**系统能力：**  SystemCapability.USB.USBManager

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| pipe | [USBDevicePipe](#usbdevicepipe) | 是 | 用于确定设备，需要调用connectDevice获取。|
| controlparam | [USBControlParams](#usbcontrolparams) | 是 | 控制传输参数，按需设置参数，参数传参类型请参考USB协议。|
| timeout | number | 否 | 超时时间（单位：ms），可选参数，默认为0不超时，用户按需选择 。 |

**错误码：**

以下错误码的详细介绍请参见[USB服务错误码](errorcode-usb.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401      | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;number&gt; | Promise对象，获取传输或接收到的数据块大小。失败返回-1。 |

**示例：**

```ts
class PARA {
  request: number = 0
  reqType: usbManager.USBControlRequestType = 0
  target: usbManager.USBRequestTargetType = 0
  value: number = 0
  index: number = 0
  data: Uint8Array = new Uint8Array()
}

let param: PARA = {
  request: 0x06,
  reqType: 0x80,
  target:0,
  value: 0x01 << 8 | 0,
  index: 0,
  data: new Uint8Array(18)
};

let devicesList: Array<usbManager.USBDevice> = usbManager.getDevices();
if (devicesList.length == 0) {
  console.log(`device list is empty`);
}

usbManager.requestRight(devicesList[0].name);
let devicepipe: usbManager.USBDevicePipe = usbManager.connectDevice(devicesList[0]);
usbManager.controlTransfer(devicepipe, param).then((ret: number) => {
console.log(`controlTransfer = ${ret}`);
})
```

## usbManager.usbControlTransfer<sup>12+</sup>

usbControlTransfer(pipe: USBDevicePipe, requestparam: USBDeviceRequestParams, timeout ?: number): Promise&lt;number&gt;

控制传输。

需要调用[usbManager.getDevices](#usbmanagergetdevices)获取设备列表；调用[usbManager.requestRight](#usbmanagerrequestright)获取设备请求权限；调用[usbManager.connectDevice](#usbmanagerconnectdevice)接口得到devicepipe作为参数。

**系统能力：**  SystemCapability.USB.USBManager

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| pipe | [USBDevicePipe](#usbdevicepipe) | 是 | 用于确定设备。 |
| requestparam | [USBDeviceRequestParams](#usbdevicerequestparams12) | 是 | 控制传输参数，按需设置参数，参数传参类型请参考USB协议。 |
| timeout | number | 否 | 超时时间（单位：ms），可选参数，默认为0不超时。 |

**错误码：**

以下错误码的详细介绍请参见[USB服务错误码](errorcode-usb.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401      | Parameter error.Possible causes:1.Mandatory parameters are left unspecified.2.Incorrect parameter types. |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;number&gt; | Promise对象，获取传输或接收到的数据块大小。失败返回-1。 |

**示例：**

```ts
class PARA {
  bmRequestType: number = 0
  bRequest: number = 0
  wValue: number = 0
  wIndex: number = 0
  wLength: number = 0
  data: Uint8Array = new Uint8Array()
}

let param: PARA = {
  bmRequestType: 0x80,
  bRequest: 0x06,

  wValue:0x01 << 8 | 0,
  wIndex: 0,
  wLength: 18,
  data: new Uint8Array(18)
};

let devicesList: Array<usbManager.USBDevice> = usbManager.getDevices();
if (devicesList.length == 0) {
  console.log(`device list is empty`);
}

usbManager.requestRight(devicesList[0].name);
let devicepipe: usbManager.USBDevicePipe = usbManager.connectDevice(devicesList[0]);
usbManager.usbControlTransfer(devicepipe, param).then((ret: number) => {
console.log(`usbControlTransfer = ${ret}`);
})
```

## usbManager.bulkTransfer

bulkTransfer(pipe: USBDevicePipe, endpoint: USBEndpoint, buffer: Uint8Array, timeout ?: number): Promise&lt;number&gt;

批量传输。

需要调用[usbManager.getDevices](#usbmanagergetdevices)获取设备信息列表以及endpoint；再调用[usbManager.requestRight](#usbmanagerrequestright)获取设备请求权限；然后调用[usbManager.connectDevice](#usbmanagerconnectdevice)接口得到返回数据devicepipe之后，再次获取接口[usbManager.claimInterface](#usbmanagerclaiminterface)；再调用usb.bulkTransfer接口。

**系统能力：**  SystemCapability.USB.USBManager

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| pipe | [USBDevicePipe](#usbdevicepipe) | 是 | 用于确定设备，需要调用connectDevice获取。|
| endpoint | [USBEndpoint](#usbendpoint) | 是 | 用于确定传输的端口，需要调用getDevices获取设备信息列表以及endpoint，address用于确定端点地址，direction用于确定端点的方向，interfaceId用于确定所属接口，当前其他属性不做处理。|
| buffer | Uint8Array | 是 | 用于写入或读取数据的缓冲区。 |
| timeout | number | 否 | 超时时间（单位：ms），可选参数，默认为0不超时，用户按需选择。 |

**错误码：**

以下错误码的详细介绍请参见[USB服务错误码](errorcode-usb.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401      | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;number&gt; | Promise对象，获取传输或接收到的数据块大小。失败返回-1。 |

**示例：**

> **说明：** 
>
> 以下示例代码只是调用bulkTransfer接口的必要流程，实际调用时，设备开发者需要遵循设备相关协议进行调用，确保数据的正确传输和设备的兼容性。

```ts
//usbManager.getDevices 接口返回数据集合，取其中一个设备对象，并获取权限 。
//把获取到的设备对象作为参数传入usbManager.connectDevice;当usbManager.connectDevice接口成功返回之后；
//才可以调用第三个接口usbManager.claimInterface.当usbManager.claimInterface 调用成功以后,再调用该接口。
let devicesList: Array<usbManager.USBDevice> = usbManager.getDevices();
if (devicesList.length == 0) {
  console.log(`device list is empty`);
}

let device: usbManager.USBDevice = devicesList[0];
usbManager.requestRight(device.name);

let devicepipe: usbManager.USBDevicePipe = usbManager.connectDevice(device);
for (let i = 0; i < device.configs[0].interfaces.length; i++) {
  if (device.configs[0].interfaces[i].endpoints[0].attributes == 2) {
    let endpoint: usbManager.USBEndpoint = device.configs[0].interfaces[i].endpoints[0];
    let interfaces: usbManager.USBInterface = device.configs[0].interfaces[i];
    let ret: number = usbManager.claimInterface(devicepipe, interfaces);
    let buffer =  new Uint8Array(128);
    usbManager.bulkTransfer(devicepipe, endpoint, buffer).then((ret: number) => {
      console.log(`bulkTransfer = ${ret}`);
    });
  }
}
```

## usbManager.closePipe

closePipe(pipe: USBDevicePipe): number

关闭设备消息控制通道。

需要调用[usbManager.getDevices](#usbmanagergetdevices)获取设备列表；调用[usbManager.requestRight](#usbmanagerrequestright)获取设备请求权限；调用[usbManager.connectDevice](#usbmanagerconnectdevice)得到devicepipe作为参数。

**系统能力：**  SystemCapability.USB.USBManager

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| pipe | [USBDevicePipe](#usbdevicepipe) | 是 | 用于确定USB设备消息控制通道，需要调用connectDevice获取。|

**错误码：**

以下错误码的详细介绍请参见[USB服务错误码](errorcode-usb.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401      | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 关闭设备消息控制通道成功返回0；关闭设备消息控制通道失败返回其他错误码。 |

**示例：**

```ts
let devicesList: Array<usbManager.USBDevice> = usbManager.getDevices();
if (devicesList.length == 0) {
  console.log(`device list is empty`);
}

usbManager.requestRight(devicesList[0].name);
let devicepipe: usbManager.USBDevicePipe = usbManager.connectDevice(devicesList[0]);
let ret: number = usbManager.closePipe(devicepipe);
console.log(`closePipe = ${ret}`);
```

## USBEndpoint

通过USB发送和接收数据的端口。通过[USBInterface](#usbinterface)获取。

**系统能力：** SystemCapability.USB.USBManager

| 名称            | 类型                                        | 必填            |说明            |
| ------------- | ------------------------------------------- | ------------- |------------- |
| address       | number                                      | 是 |端点地址。         |
| attributes    | number                                      | 是 |端点属性。         |
| interval      | number                                      | 是 |端点间隔。         |
| maxPacketSize | number                                      | 是 |端点最大数据包大小。    |
| direction     | [USBRequestDirection](#usbrequestdirection) | 是 |端点的方向。        |
| number        | number                                      | 是 |端点号。          |
| type          | number                                      | 是 |端点类型。         |
| interfaceId   | number                                      | 是 |端点所属的接口的唯一标识。 |

## USBInterface

一个[USBConfiguration](#usbconfiguration)中可以含有多个USBInterface，每个USBInterface提供一个功能。

**系统能力：** SystemCapability.USB.USBManager

| 名称               | 类型                                     | 必填            |说明                    |
| ---------------- | ---------------------------------------- | ------------- |--------------------- |
| id               | number                                   | 是 |接口的唯一标识。              |
| protocol         | number                                   | 是 |接口的协议。                |
| clazz            | number                                   | 是 |设备类型。                 |
| subClass         | number                                   | 是 |设备子类。                 |
| alternateSetting | number                                   | 是 |在同一个接口中的多个描述符中进行切换设置。 |
| name             | string                                   | 是 |接口名称。                 |
| endpoints        | Array&lt;[USBEndpoint](#usbendpoint)&gt; | 是 |当前接口所包含的端点。           |

## USBConfiguration

USB配置，一个[USBDevice](#usbdevice)中可以含有多个配置。

**系统能力：** SystemCapability.USB.USBManager

| 名称             | 类型                                             | 必填  |说明              |
| -------------- | ------------------------------------------------ | --------------- |--------------- |
| id             | number                                           | 是 |配置的唯一标识。        |
| attributes     | number                                           | 是 |配置的属性。          |
| maxPower       | number                                           | 是 |最大功耗，以毫安为单位。    |
| name           | string                                           | 是 |配置的名称，可以为空。     |
| isRemoteWakeup | boolean                                          | 是 |检查当前配置是否支持远程唤醒。 |
| isSelfPowered  | boolean                                          | 是 | 检查当前配置是否支持独立电源。 |
| interfaces     | Array&nbsp;&lt;[USBInterface](#usbinterface)&gt; | 是 |配置支持的接口属性。      |

## USBDevice

USB设备信息。

**系统能力：** SystemCapability.USB.USBManager

| 名称               | 类型                                 | 必填         |说明         |
| ---------------- | ------------------------------------ | ---------- |---------- |
| busNum           | number                               | 是 |总线地址。      |
| devAddress       | number                               | 是 |设备地址。      |
| serial           | string                               | 是 |序列号。       |
| name             | string                               | 是 |设备名字。      |
| manufacturerName | string                               | 是 | 产商信息。      |
| productName      | string                               | 是 |产品信息。      |
| version          | string                               | 是 |版本。        |
| vendorId         | number                               | 是 |厂商ID。      |
| productId        | number                               | 是 |产品ID。      |
| clazz            | number                               | 是 |设备类。       |
| subClass         | number                               | 是 |设备子类。      |
| protocol         | number                               | 是 |设备协议码。     |
| configs          | Array&lt;[USBConfiguration](#usbconfiguration)&gt; | 是 |设备配置描述符信息。 |

## USBDevicePipe

USB设备消息传输通道，用于确定设备。

**系统能力：** SystemCapability.USB.USBManager

| 名称         | 类型   | 必填    |说明    |
| ---------- | ------ | ----- |----- |
| busNum     | number |是 | 总线地址。 |
| devAddress | number |是 | 设备地址。 |

## USBControlParams

控制传输参数。

**系统能力：** SystemCapability.USB.USBManager

| 名称      | 类型                                            | 必填               |说明               |
| ------- | ----------------------------------------------- | ---------------- |---------------- |
| request | number                                          | 是   |请求类型。            |
| target  | [USBRequestTargetType](#usbrequesttargettype)   | 是   |请求目标类型。          |
| reqType | [USBControlRequestType](#usbcontrolrequesttype) | 是   |请求控制类型。          |
| value   | number                                          | 是   |请求参数。            |
| index   | number                                          | 是   |请求参数value对应的索引值。 |
| data    | Uint8Array                                      | 是   |用于写入或读取的缓冲区。     |

## USBDeviceRequestParams<sup>12+</sup>

控制传输参数。

**系统能力：** SystemCapability.USB.USBManager

| 名称      | 类型                                            | 必填               |说明               |
| ------- | ----------------------------------------------- | ---------------- |---------------- |
| bmRequestType | number                                    | 是   |请求控制类型。            |
| bRequest  | number                                        | 是   |请求类型。          |
| wValue | number                                           | 是   |请求参数。          |
| wIndex   | number                                         | 是   |请求参数value对应的索引值。            |
| wLength   | number                                        | 是   |请求数据的长度 |
| data    | Uint8Array                                      | 是   |用于写入或读取的缓冲区。     |

## USBRequestTargetType

请求目标类型。

**系统能力：** SystemCapability.USB.USBManager

| 名称                         | 值   | 说明   |
| ---------------------------- | ---- | ------ |
| USB_REQUEST_TARGET_DEVICE    | 0    | 设备。 |
| USB_REQUEST_TARGET_INTERFACE | 1    | 接口。 |
| USB_REQUEST_TARGET_ENDPOINT  | 2    | 端点。 |
| USB_REQUEST_TARGET_OTHER     | 3    | 其他。 |

## USBControlRequestType

控制请求类型。

**系统能力：** SystemCapability.USB.USBManager

| 名称                      | 值   | 说明   |
| ------------------------- | ---- | ------ |
| USB_REQUEST_TYPE_STANDARD | 0    | 标准。 |
| USB_REQUEST_TYPE_CLASS    | 1    | 类。   |
| USB_REQUEST_TYPE_VENDOR   | 2    | 厂商。 |

## USBRequestDirection

请求方向。

**系统能力：** SystemCapability.USB.USBManager

| 名称                        | 值   | 说明                     |
| --------------------------- | ---- | ------------------------ |
| USB_REQUEST_DIR_TO_DEVICE   | 0    | 写数据，主设备往从设备。 |
| USB_REQUEST_DIR_FROM_DEVICE | 0x80 | 读数据，从设备往主设备。 |

