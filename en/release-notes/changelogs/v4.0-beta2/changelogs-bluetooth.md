# Bluetooth Subsystem Changelog

## cl.bluetooth.1 New APIs, Attributes, and Enums

**Change Impact**

Added APIs to provide capabilities of obtaining the peripheral device address in non-Bluetooth scan mode (for example NFC), initiating pairing, and setting profile connection management.

**Key API/Component Changes**

| Module         | API                                                 |
| ------------- |-------------------------------------------------------- |
|@ohos.bluetoothManager| [pairCredibleDevice(deviceId: string, transport: BluetoothTransport, callback: AsyncCallback&lt;void&gt;): void](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagerpaircredibledevice10)    |
|@ohos.bluetoothManager| [pairCredibleDevice(deviceId: string, transport: BluetoothTransport): Promise&lt;void&gt;](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagerpaircredibledevice10-1)    |
|@ohos.bluetoothManager| [getRemoteProfileUuids(device: string, callback: AsyncCallback&lt;Array&lt;ProfileUuids&gt;&gt;): void](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagergetremoteprofileuuids10)    |
|@ohos.bluetoothManager| [getRemoteProfileUuids(device: string): Promise&lt;Array&lt;ProfileUuids&gt;&gt;](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagergetremoteprofileuuids10-1)    |
|@ohos.bluetoothManager| [getLocalProfileUuids(callback: AsyncCallback&lt;Array&lt;ProfileUuids&gt;&gt;): void](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagergetlocalprofileuuids10)    |
|@ohos.bluetoothManager| [getLocalProfileUuids(): Promise&lt;Array&lt;ProfileUuids&gt;&gt;](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagergetlocalprofileuuids10-1)    |
|@ohos.bluetoothManager| [setDevicePinCode(device: string, code: string, callback: AsyncCallback&lt;void&gt;): void](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagersetdevicepincode10)    |
|@ohos.bluetoothManager| [setDevicePinCode(device: string, code: string): Promise&lt;void&gt;](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagersetdevicepincode10-1)    |
|@ohos.bluetoothManager| [setConnectionStrategy(device: string, strategy: ConnectionStrategy, callback: AsyncCallback&lt;void&gt;): void](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagersetconnectionstrategy10)|
|@ohos.bluetoothManager| [setConnectionStrategy(device: string, strategy: ConnectionStrategy): Promise&lt;void&gt;](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagersetconnectionstrategy10-1) |
|@ohos.bluetoothManager| [getConnectionStrategy(device: string, callback: AsyncCallback&lt;ConnectionStrategy&gt;): void](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagergetconnectionstrategy10)|
|@ohos.bluetoothManager| [getConnectionStrategy(device: string): Promise&lt;ConnectionStrategy&gt;](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothmanagergetconnectionstrategy10-1) |
|@ohos.bluetoothManager|[ConnectionStrategy](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#connectionstrategy10)|
|@ohos.bluetoothManager|[properties](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#blecharacteristic)|
|@ohos.bluetoothManager|[deviceName](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#scanresult)|
|@ohos.bluetoothManager|[includeDeviceName](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#advertisedata)|
|@ohos.bluetoothManager|[GattProperties](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#gattproperties10)|
|@ohos.bluetoothManager|[pinType](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#pintype10)|
|@ohos.bluetoothManager|[BluetoothTransport](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#bluetoothtransport10)|
|@ohos.bluetoothManager|[ProfileUuids](https://gitee.com/openharmony/docs/tree/OpenHarmony-4.0-Beta2/en/application-dev/referenceapis/js-apis-bluetoothManager.md#profileuuids10)|

**Adaptation Guide**

For details, see examples in the related API references.
