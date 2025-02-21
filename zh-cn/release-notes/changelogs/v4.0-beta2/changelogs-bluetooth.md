# bluetooth子系统ChangeLog

## cl.bluetooth.1 蓝牙模块新增接口，属性及枚举

**变更影响**

新增接口，提供通过非蓝牙扫描的方式(例如NFC等)获取到外设的地址，发起配对的能力；支持profile的连接管理设置能力等。

**关键接口/组件变更**

| 模块名         |新增声明                                                 |
| ------------- |-------------------------------------------------------- |
|@ohos.bluetoothManager| [pairCredibleDevice(deviceId: string, transport: BluetoothTransport, callback: AsyncCallback&lt;void&gt;): void](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagerpaircredibledevice10)    |
|@ohos.bluetoothManager| [pairCredibleDevice(deviceId: string, transport: BluetoothTransport): Promise&lt;void&gt;](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagerpaircredibledevice10-1)    |
|@ohos.bluetoothManager| [getRemoteProfileUuids(device: string, callback: AsyncCallback&lt;Array&lt;ProfileUuids&gt;&gt;): void](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagergetremoteprofileuuids10)    |
|@ohos.bluetoothManager| [getRemoteProfileUuids(device: string): Promise&lt;Array&lt;ProfileUuids&gt;&gt;](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagergetremoteprofileuuids10-1)    |
|@ohos.bluetoothManager| [getLocalProfileUuids(callback: AsyncCallback&lt;Array&lt;ProfileUuids&gt;&gt;): void](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagergetlocalprofileuuids10)    |
|@ohos.bluetoothManager| [getLocalProfileUuids(): Promise&lt;Array&lt;ProfileUuids&gt;&gt;](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagergetlocalprofileuuids10-1)    |
|@ohos.bluetoothManager| [setDevicePinCode(device: string, code: string, callback: AsyncCallback&lt;void&gt;): void](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagersetdevicepincode10)    |
|@ohos.bluetoothManager| [setDevicePinCode(device: string, code: string): Promise&lt;void&gt;](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagersetdevicepincode10-1)    |
|@ohos.bluetoothManager| [setConnectionStrategy(device: string, strategy: ConnectionStrategy, callback: AsyncCallback&lt;void&gt;): void](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagersetconnectionstrategy10)|
|@ohos.bluetoothManager| [setConnectionStrategy(device: string, strategy: ConnectionStrategy): Promise&lt;void&gt;](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagersetconnectionstrategy10-1) |
|@ohos.bluetoothManager| [getConnectionStrategy(device: string, callback: AsyncCallback&lt;ConnectionStrategy&gt;): void](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagergetconnectionstrategy10)|
|@ohos.bluetoothManager| [getConnectionStrategy(device: string): Promise&lt;ConnectionStrategy&gt;](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagergetconnectionstrategy10-1) |
|@ohos.bluetoothManager|[ConnectionStrategy](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#connectionstrategy10)|
|@ohos.bluetoothManager|[properties](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#blecharacteristic)|
|@ohos.bluetoothManager|[deviceName](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#scanresult)|
|@ohos.bluetoothManager|[includeDeviceName](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#advertisedata)|
|@ohos.bluetoothManager|[GattProperties](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#gattproperties10)|
|@ohos.bluetoothManager|[pinType](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#pintype10)|
|@ohos.bluetoothManager|[BluetoothTransport](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothtransport10)|
|@ohos.bluetoothManager|[ProfileUuids](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/zh-cn/application-dev/referenceapis/js-apis-bluetoothManager.md#profileuuids10)|

**适配指导**

请参考各新增接口文档下的示例。


<!--no_check-->