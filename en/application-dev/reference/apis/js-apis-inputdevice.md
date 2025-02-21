# @ohos.multimodalInput.inputDevice (Input Device)

The **inputDevice** module allows you to listen for hot swap events of input devices and query information about input devices.

> **NOTE**
>
> The initial APIs of this module are supported since API version 8. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```js
import inputDevice from '@ohos.multimodalInput.inputDevice';
```

## inputDevice.getDeviceList<sup>9+</sup>

getDeviceList(callback: AsyncCallback&lt;Array&lt;number&gt;&gt;): void

Obtains the IDs of all input devices. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

**Parameters**

| Name    | Type                                    | Mandatory| Description                                    |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| callback | AsyncCallback&lt;Array&lt;number&gt;&gt; | Yes  | Callback used to return the result.|

**Example**

```js
try {
  inputDevice.getDeviceList((error, ids) => {
    if (error) {
      console.log(`Failed to get device id list, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Device id list: ${JSON.stringify(ids)}`);
  });
} catch (error) {
  console.log(`Failed to get device id list, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.getDeviceList<sup>9+</sup>

getDeviceList(): Promise&lt;Array&lt;number&gt;&gt;

Obtains the IDs of all input devices. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

**Return value**

| Parameters                              | Description                                       |
| ---------------------------------- | ------------------------------------------- |
| Promise&lt;Array&lt;number&gt;&gt; | Promise used to return the result.|

**Example**

```js
try {
  inputDevice.getDeviceList().then((ids) => {
    console.log(`Device id list: ${JSON.stringify(ids)}`);
  });
} catch (error) {
  console.log(`Failed to get device id list, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.getDeviceInfo<sup>9+</sup>

getDeviceInfo(deviceId: number, callback: AsyncCallback&lt;InputDeviceData&gt;): void

Obtains information about an input device. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

**Parameters**

| Name    | Type                                                    | Mandatory| Description                                   |
| -------- | -------------------------------------------------------- | ---- | --------------------------------------- |
| deviceId | number                                                   | Yes  | ID of the input device.                 |
| callback | AsyncCallback&lt;[InputDeviceData](#inputdevicedata)&gt; | Yes  | Callback used to return the result, which is an **InputDeviceData** object.|

**Example**

```js
// Obtain the name of the device whose ID is 1.
try {
  inputDevice.getDeviceInfo(1, (error, deviceData) => {
    if (error) {
      console.log(`Failed to get device info, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Device info: ${JSON.stringify(deviceData)}`);
  });
} catch (error) {
  console.log(`Failed to get device info, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.getDeviceInfo<sup>9+</sup>

getDeviceInfo(deviceId: number): Promise&lt;InputDeviceData&gt;

Obtains information about an input device. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

**Parameters**

| Name    | Type  | Mandatory| Description                  |
| -------- | ------ | ---- | ---------------------- |
| deviceId | number | Yes  | ID of the input device.|

**Return value**

| Parameters                                              | Description                           |
| -------------------------------------------------- | ------------------------------- |
| Promise&lt;[InputDeviceData](#inputdevicedata)&gt; | Promise used to return the result.|

**Example**

```js
// Obtain the name of the device whose ID is 1.
try {
  inputDevice.getDeviceInfo(1).then((deviceData) => {
    console.log(`Device info: ${JSON.stringify(deviceData)}`);
  });
} catch (error) {
  console.log(`Failed to get device info, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.on<sup>9+</sup>

on(type: "change", listener: Callback&lt;DeviceListener&gt;): void

Enables listening for device hot swap events.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

**Parameters**

| Name      | Type                                      | Mandatory  | Description         |
| -------- | ---------------------------------------- | ---- | ----------- |
| type     | string                                   | Yes   | Event type of the input device. |
| listener | Callback&lt;[DeviceListener](#devicelistener9)&gt; | Yes   | Listener for events of the input device.|

**Example**

```js
let isPhysicalKeyboardExist = true;
try {
  inputDevice.on("change", (data) => {
    console.log(`Device event info: ${JSON.stringify(data)}`);
    inputDevice.getKeyboardType(data.deviceId, (err, type) => {
      console.log("The keyboard type is: " + type);
      if (type == inputDevice.KeyboardType.ALPHABETIC_KEYBOARD && data.type == 'add') {
        // The physical keyboard is connected.
        isPhysicalKeyboardExist = true;
      } else if (type == inputDevice.KeyboardType.ALPHABETIC_KEYBOARD && data.type == 'remove') {
        // The physical keyboard is disconnected.
        isPhysicalKeyboardExist = false;
      }
    });
  });
  // Check whether the soft keyboard is open based on the value of isPhysicalKeyboardExist.
} catch (error) {
  console.log(`Get device info failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.off<sup>9+</sup>

off(type: "change", listener?: Callback&lt;DeviceListener&gt;): void

Disables listening for device hot swap events. This API is called before the application exits.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

**Parameters**

| Name      | Type                                      | Mandatory  | Description         |
| -------- | ---------------------------------------- | ---- | ----------- |
| type     | string                                   | Yes   | Event type of the input device. |
| listener | Callback&lt;[DeviceListener](#devicelistener9)&gt; | No   | Listener for events of the input device.|

**Example**

```js
function callback(data) {
  console.log(`Report device event info: ${JSON.stringify(data, [`type`, `deviceId`])}`);
};

try {
  inputDevice.on("change", callback);
} catch (error) {
  console.log(`Listen device event failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}

// Disable this listener.
try {
  inputDevice.off("change", callback);
} catch (error) {
  console.log(`Cancel listening device event failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}

// Disable all listeners.
try {
  inputDevice.off("change");
} catch (error) {
  console.log(`Cancel all listening device event failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.getDeviceIds<sup>(deprecated)</sup>

getDeviceIds(callback: AsyncCallback&lt;Array&lt;number&gt;&gt;): void

Obtains the IDs of all input devices. This API uses an asynchronous callback to return the result.

This API is deprecated since API version 9. You are advised to use [inputDevice.getDeviceList](#inputdevicegetdevicelist9) instead.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

**Parameters**

| Name    | Type                                    | Mandatory| Description                                    |
| -------- | ---------------------------------------- | ---- | ---------------------------------------- |
| callback | AsyncCallback&lt;Array&lt;number&gt;&gt; | Yes  | Callback used to return the result.|

**Example**

```js
inputDevice.getDeviceIds((error, ids) => {
  if (error) {
    console.log(`Failed to get device id list, error: ${JSON.stringify(error, [`code`, `message`])}`);
    return;
  }
  console.log(`Device id list: ${JSON.stringify(ids)}`);
});
```

## inputDevice.getDeviceIds<sup>(deprecated)</sup>

getDeviceIds(): Promise&lt;Array&lt;number&gt;&gt;

Obtains the IDs of all input devices. This API uses a promise to return the result.

This API is deprecated since API version 9. You are advised to use [inputDevice.getDeviceList](#inputdevicegetdevicelist9) instead.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

**Return value**

| Parameters                              | Description                                       |
| ---------------------------------- | ------------------------------------------- |
| Promise&lt;Array&lt;number&gt;&gt; | Promise used to return the result.|

**Example**

```js
inputDevice.getDeviceIds().then((ids) => {
  console.log(`Device id list: ${JSON.stringify(ids)}`);
});
```

## inputDevice.getDevice<sup>(deprecated)</sup>

getDevice(deviceId: number, callback: AsyncCallback&lt;InputDeviceData&gt;): void

Obtains information about an input device. This API uses an asynchronous callback to return the result.

This API is deprecated since API version 9. You are advised to use [inputDevice.getDeviceInfo](#inputdevicegetdeviceinfo9) instead.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

**Parameters**

| Name    | Type                                                    | Mandatory| Description                            |
| -------- | -------------------------------------------------------- | ---- | -------------------------------- |
| deviceId | number                                                   | Yes  | ID of the input device.                    |
| callback | AsyncCallback&lt;[InputDeviceData](#inputdevicedata)&gt; | Yes  | Callback used to return the result, which is an **InputDeviceData** object.|

**Example**

```js
// Obtain the name of the device whose ID is 1.
inputDevice.getDevice(1, (error, deviceData) => {
  if (error) {
    console.log(`Failed to get device info, error: ${JSON.stringify(error, [`code`, `message`])}`);
    return;
  }
  console.log(`Device info: ${JSON.stringify(deviceData)}`);
});
```

## inputDevice.getDevice<sup>(deprecated)</sup>

getDevice(deviceId: number): Promise&lt;InputDeviceData&gt;

Obtains information about an input device. This API uses a promise to return the result.

This API is deprecated since API version 9. You are advised to use [inputDevice.getDeviceInfo](#inputdevicegetdeviceinfo9) instead.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

**Parameters**

| Name    | Type  | Mandatory| Description        |
| -------- | ------ | ---- | ------------ |
| deviceId | number | Yes  | ID of the input device.|

**Return value**

| Parameters                                              | Description                               |
| -------------------------------------------------- | ----------------------------------- |
| Promise&lt;[InputDeviceData](#inputdevicedata)&gt; | Promise used to return the result.|

**Example**

```js
// Obtain the name of the device whose ID is 1.
inputDevice.getDevice(1).then((deviceData) => {
  console.log(`Device info: ${JSON.stringify(deviceData)}`);
});
```

## inputDevice.supportKeys<sup>9+</sup>

supportKeys(deviceId: number, keys: Array&lt;KeyCode&gt;, callback: AsyncCallback &lt;Array&lt;boolean&gt;&gt;): void

Obtains the key codes supported by the input device. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

**Parameters**

| Name    | Type                                     | Mandatory| Description                                                  |
| -------- | ----------------------------------------- | ---- | ------------------------------------------------------ |
| deviceId | number                                    | Yes  | Unique ID of the input device. If the same physical device is repeatedly inserted and removed, its ID changes.|
| keys     | Array&lt;KeyCode&gt;                      | Yes  | Key codes to be queried. A maximum of five key codes can be specified.               |
| callback | AsyncCallback&lt;Array&lt;boolean&gt;&gt; | Yes  | Callback used to return the result.                          |

**Example**

```js
// Check whether the input device whose ID is 1 supports key codes 17, 22, and 2055.
try {
  inputDevice.supportKeys(1, [17, 22, 2055], (error, supportResult) => {
    console.log(`Query result: ${JSON.stringify(supportResult)}`);
  });
} catch (error) {
  console.log(`Query failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.supportKeys<sup>9+</sup>

supportKeys(deviceId: number, keys: Array&lt;KeyCode&gt;): Promise&lt;Array&lt;boolean&gt;&gt;

Obtains the key codes supported by the input device. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

**Parameters**

| Name    | Type                | Mandatory| Description                                                  |
| -------- | -------------------- | ---- | ------------------------------------------------------ |
| deviceId | number               | Yes  | Unique ID of the input device. If the same physical device is repeatedly inserted and removed, its ID changes.|
| keys     | Array&lt;KeyCode&gt; | Yes  | Key codes to be queried. A maximum of five key codes can be specified.               |

**Return value**

| Parameters                               | Description                           |
| ----------------------------------- | ------------------------------- |
| Promise&lt;Array&lt;boolean&gt;&gt; | Promise used to return the result.|

**Example**

```js
// Check whether the input device whose ID is 1 supports key codes 17, 22, and 2055.
try {
  inputDevice.supportKeys(1, [17, 22, 2055]).then((supportResult) => {
    console.log(`Query result: ${JSON.stringify(supportResult)}`);
  });
} catch (error) {
  console.log(`Query failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.getKeyboardType<sup>9+</sup>

getKeyboardType(deviceId: number, callback: AsyncCallback&lt;KeyboardType&gt;): void

Obtains the keyboard type of an input device. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

**Parameters**

| Name    | Type                                               | Mandatory| Description                                                        |
| -------- | --------------------------------------------------- | ---- | ------------------------------------------------------------ |
| deviceId | number                                              | Yes  | Unique ID of the input device. If the same physical device is repeatedly inserted and removed, its ID changes.|
| callback | AsyncCallback&lt;[KeyboardType](#keyboardtype9)&gt; | Yes  | Callback used to return the result.                                |

**Example**

```js
// Query the keyboard type of the input device whose ID is 1.
try {
  inputDevice.getKeyboardType(1, (error, type) => {
    if (error) {
      console.log(`Failed to get keyboard type, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Keyboard type: ${JSON.stringify(type)}`);
  });
} catch (error) {
  console.log(`Failed to get keyboard type, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## inputDevice.getKeyboardType<sup>9+</sup>

getKeyboardType(deviceId: number): Promise&lt;KeyboardType&gt;

Obtains the keyboard type of an input device. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

**Parameters**

| Name    | Type  | Mandatory| Description                                                        |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| deviceId | number | Yes  | Unique ID of the input device. If the same physical device is repeatedly inserted and removed, its ID changes.|

**Return value**

| Parameters                                         | Description                           |
| --------------------------------------------- | ------------------------------- |
| Promise&lt;[KeyboardType](#keyboardtype9)&gt; | Promise used to return the result.|

**Example**

```js
// Query the keyboard type of the input device whose ID is 1.
try {
  inputDevice.getKeyboardType(1).then((type) => {
    console.log(`Keyboard type: ${JSON.stringify(type)}`);
  });
} catch (error) {
  console.log(`Failed to get keyboard type, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## DeviceListener<sup>9+</sup>

Defines the listener for hot swap events of an input device.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

| Name       | Type  | Readable  | Writable  | Description     |
| --------- | ------ | ---- | ---- | ------- |
| type     | [ChangedType](#changedtype) | Yes| No| Device change type, which indicates whether an input device is inserted or removed.|
| deviceId | number                      | Yes| No| Unique ID of the input device. If the same physical device is repeatedly inserted and removed, its ID changes.|

## InputDeviceData

Defines the information about an input device.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

| Name       | Type  | Readable  | Writable  | Description     |
| --------- | ------ | ---- | ---- | ------- |
| id                   | number                                 | Yes| No| Unique ID of the input device. If the same physical device is repeatedly inserted and removed, its ID changes.|
| name                 | string                                 | Yes| No| Name of the input device.                                            |
| sources              | Array&lt;[SourceType](#sourcetype)&gt; | Yes| No| Source type of the input device. For example, if a keyboard is attached with a touchpad, the device has two input sources: keyboard and touchpad.|
| axisRanges           | Array&lt;[AxisRange](#axisrange)&gt;  | Yes| No| Axis information of the input device.                                          |
| bus<sup>9+</sup>     | number                                 | Yes| No| Bus type of the input device.                                        |
| product<sup>9+</sup> | number                                 | Yes| No| Product information of the input device.                                        |
| vendor<sup>9+</sup>  | number                                 | Yes| No| Vendor information of the input device.                                        |
| version<sup>9+</sup> | number                                 | Yes| No| Version information of the input device.                                        |
| phys<sup>9+</sup>    | string                                 | Yes| No| Physical address of the input device.                                        |
| uniq<sup>9+</sup>    | string                                 | Yes| No| Unique ID of the input device.                                        |

## AxisType<sup>9+</sup>

Defines the axis type of an input device.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

| Name       | Type  | Readable  | Writable  | Description     |
| --------- | ------ | ---- | ---- | ------- |
| touchMajor  | string | Yes| No| touchMajor axis. |
| touchMinor  | string | Yes| No| touchMinor axis. |
| toolMinor   | string | Yes| No| toolMinor axis.  |
| toolMajor   | string | Yes| No| toolMajor axis.  |
| orientation | string | Yes| No| Orientation axis.|
| pressure    | string | Yes| No| Pressure axis.   |
| x           | string | Yes| No| X axis.          |
| y           | string | Yes| No| Y axis.          |
| NULL        | string | Yes| No| None.             |

## AxisRange

Defines the axis range of an input device.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

| Name       | Type  | Readable  | Writable  | Description     |
| --------- | ------ | ---- | ---- | ------- |
| source                  | [SourceType](#sourcetype) | Yes| No| Input source type of the axis.|
| axis                    | [AxisType](#axistype9)    | Yes| No| Axis type.   |
| max                     | number                    | Yes| No| Maximum value of the axis.  |
| min                     | number                    | Yes| No| Minimum value of the axis.  |
| fuzz<sup>9+</sup>       | number                    | Yes| No| Fuzzy value of the axis.  |
| flat<sup>9+</sup>       | number                    | Yes| No| Benchmark value of the axis.  |
| resolution<sup>9+</sup> | number                    | Yes| No| Resolution of the axis.  |

## SourceType<sup>9+</sup>

Input source type of the axis. For example, if a mouse reports an x-axis event, the input source of the x-axis is the mouse.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

| Name       | Type  | Readable  | Writable  | Description     |
| --------- | ------ | ---- | ---- | ------- |
| keyboard    | string | Yes| No| The input device is a keyboard. |
| touchscreen | string | Yes| No| The input device is a touchscreen.|
| mouse       | string | Yes| No| The input device is a mouse. |
| trackball   | string | Yes| No| The input device is a trackball.|
| touchpad    | string | Yes| No| The input device is a touchpad.|
| joystick    | string | Yes| No| The input device is a joystick.|

## ChangedType<sup>9+</sup>

Defines the change type for the hot swap event of an input device.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

| Name       | Type  | Readable  | Writable  | Description     |
| --------- | ------ | ---- | ---- | ------- |
| add    | string | Yes| No| An input device is inserted.|
| remove | string | Yes| No| An input device is removed.|

## KeyboardType<sup>9+</sup>

Enumerates the keyboard types.

**System capability**: SystemCapability.MultimodalInput.Input.InputDevice

| Name                 | Value   | Description       |
| ------------------- | ---- | --------- |
| NONE                | 0    | Keyboard without keys. |
| UNKNOWN             | 1    | Keyboard with unknown keys.|
| ALPHABETIC_KEYBOARD | 2    | Full keyboard. |
| DIGITAL_KEYBOARD    | 3    | Keypad. |
| HANDWRITING_PEN     | 4    | Stylus. |
| REMOTE_CONTROL      | 5    | Remote control. |
