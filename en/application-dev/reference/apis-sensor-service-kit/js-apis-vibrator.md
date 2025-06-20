# @ohos.vibrator (Vibrator)

The **vibrator** module allows precise control over the vibration of device vibrators. With the APIs provided by this module, you can start vibration in various modes such as specified duration, preset effect, and custom effect and stop any or all of them.

> **NOTE**
>
> The initial APIs of this module are supported since API version 8. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```ts
import { vibrator } from '@kit.SensorServiceKit';
```

## vibrator.startVibration<sup>9+</sup>

startVibration(effect: VibrateEffect, attribute: VibrateAttribute, callback: AsyncCallback&lt;void&gt;): void

Starts vibration with the specified effect and attribute. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.VIBRATE

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name   | Type                                  | Mandatory| Description                                                        |
| --------- | -------------------------------------- | ---- | :----------------------------------------------------------- |
| effect    | [VibrateEffect](#vibrateeffect9)       | Yes  | Vibration effect. The following options are supported:<br>- [VibrateTime](#vibratetime9): starts vibration of the specified duration. This mode is not recommended because there is no start or stop.<br>- [VibratePreset](#vibratepreset9): starts vibration based on the preset effect. This mode is applicable to short vibration scenarios.<br>- [VibrateFromFile](#vibratefromfile10): starts the vibration according to a custom vibration configuration file. This mode is applicable to short vibration scenarios.<br>- [VibrateFromPattern<sup>18+</sup>](#vibratefrompattern18): starts vibration according to a custom vibration pattern.|
| attribute | [VibrateAttribute](#vibrateattribute9) | Yes  | Vibration attribute.                                              |
| callback  | AsyncCallback&lt;void&gt;              | Yes  | Callback used to return the operation result. If the operation is successful, **err** is **undefined**; otherwise, **err** is an error object, which contains the error code and error information.|

**Error codes**

For details about the error codes, see [Vibrator Error Codes](errorcode-vibrator.md) and [Universal Error Codes](../errorcode-universal.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 201      | Permission denied.                                           |
| 401      | Parameter error.Possible causes:1. Mandatory parameters are left unspecified;2. Incorrect parameter types;3. Parameter verification failed. |
| 801      | Capability not supported.                                    |
| 14600101 | Device operation failed.                                     |

**Example**

1. Start vibration based on the preset effect.

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

try {
  // Check whether 'haptic.clock.timer' is supported.
  vibrator.isSupportEffect('haptic.clock.timer', (err: BusinessError, state: boolean) => {
    if (err) {
      console.error(`Failed to query effect. Code: ${err.code}, message: ${err.message}`);
      return;
    }
    console.info('Succeed in querying effect');
    if (state) {
      try {
        vibrator.startVibration({
          type: 'preset',
          effectId: 'haptic.clock.timer',
          count: 1,
        }, {
          usage: 'alarm' // The switch control is subject to the selected type.
        }, (error: BusinessError) => {
          if (error) {
            console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
			return;
          }
          console.info('Succeed in starting vibration');
          
        });
      } catch (err) {
        let e: BusinessError = err as BusinessError;
		console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
      }
    }
  })
} catch (error) {
  let e: BusinessError = error as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}
```

2. Start vibration according to the custom vibration configuration file.

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { resourceManager } from '@kit.LocalizationKit';
import { BusinessError } from '@kit.BasicServicesKit';

const fileName: string = 'xxx.json';

@Entry
@Component
struct Index {
  uiContext = this.getUIContext();

  build() {
    Row() {
      Column() {
        Button('alarm-file')
          .onClick(() => {
            let rawFd: resourceManager.RawFileDescriptor | undefined = this.uiContext.getHostContext()?.resourceManager.getRawFdSync(fileName);
            if (rawFd != undefined) {
              try {
                vibrator.startVibration({
                  type: "file",
                  hapticFd: { fd: rawFd.fd, offset: rawFd.offset, length: rawFd.length }
                }, {
                  id: 0,
                  usage: 'alarm' // The switch control is subject to the selected type.
                }, (error: BusinessError) => {
                  if (error) {
                    console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
                    return;
                  }
                  console.info('Succeed in starting vibration');
                });
              } catch (err) {
                let e: BusinessError = err as BusinessError;
                console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
              }
            }
            this.uiContext.getHostContext()?.resourceManager.closeRawFdSync(fileName);
          })
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

3. Start vibration of the specified duration.

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

try {
  vibrator.startVibration({
    type: 'time',
    duration: 1000,
  }, {
    id: 0,
    usage: 'alarm' // The switch control is subject to the selected type.
  }, (error: BusinessError) => {
    if (error) {
      console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
      return;
    }
    console.info('Succeed in starting vibration');
  });
} catch (err) {
  let e: BusinessError = err as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}
```

## vibrator.startVibration<sup>9+</sup>

startVibration(effect: VibrateEffect, attribute: VibrateAttribute): Promise&lt;void&gt;

Starts vibration with the specified effect and attribute. This API uses a promise to return the result.

**Required permissions**: ohos.permission.VIBRATE

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name   | Type                                  | Mandatory| Description                                                        |
| --------- | -------------------------------------- | ---- | ------------------------------------------------------------ |
| effect    | [VibrateEffect](#vibrateeffect9)       | Yes  | Vibration effect. The following options are supported:<br>- [VibrateTime](#vibratetime9): starts vibration of the specified duration. This mode is not recommended because there is no start or stop.<br>- [VibratePreset](#vibratepreset9): starts vibration based on the preset effect. This mode is applicable to short vibration scenarios.<br>- [VibrateFromFile](#vibratefromfile10): starts vibration according to a custom vibration configuration file.<br>- [VibrateFromPattern<sup>18+</sup>](#vibratefrompattern18): starts vibration according to a custom vibration pattern.|
| attribute | [VibrateAttribute](#vibrateattribute9) | Yes  | Vibration attribute.                                              |

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Vibrator Error Codes](errorcode-vibrator.md) and [Universal Error Codes](../errorcode-universal.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 201      | Permission denied.                                           |
| 401      | Parameter error.Possible causes:1. Mandatory parameters are left unspecified;2. Incorrect parameter types;3. Parameter verification failed. |
| 801      | Capability not supported.                                    |
| 14600101 | Device operation failed.                                     |

**Example**

1. Start vibration based on the preset effect.

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

try {
  // Check whether 'haptic.clock.timer' is supported.
  vibrator.isSupportEffect('haptic.clock.timer', (err: BusinessError, state: boolean) => {
    if (err) {
      console.error(`Failed to query effect. Code: ${err.code}, message: ${err.message}`);
      return;
    }
    console.info('Succeed in querying effect');
    if (state) {
      try {
        vibrator.startVibration({
          type: 'preset',
          effectId: 'haptic.clock.timer',
          count: 1,
        }, {
          usage: 'alarm' // The switch control is subject to the selected type.
        }, (error: BusinessError) => {
          if (error) {
            console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
			return;
          }
          console.info('Succeed in starting vibration');
          
        });
      } catch (err) {
        let e: BusinessError = err as BusinessError;
		console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
      }
    }
  })
} catch (error) {
  let e: BusinessError = error as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}
```

2. Start vibration according to the custom vibration configuration file.

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { resourceManager } from '@kit.LocalizationKit';
import { BusinessError } from '@kit.BasicServicesKit';

const fileName: string = 'xxx.json';

@Entry
@Component
struct Index {
  uiContext = this.getUIContext();

  build() {
    Row() {
      Column() {
        Button('alarm-file')
          .onClick(() => {
            let rawFd: resourceManager.RawFileDescriptor | undefined = this.uiContext.getHostContext()?.resourceManager.getRawFdSync(fileName);
            if (rawFd != undefined) {
              try {
                vibrator.startVibration({
                  type: "file",
                  hapticFd: { fd: rawFd.fd, offset: rawFd.offset, length: rawFd.length }
                }, {
                  id: 0,
                  usage: 'alarm' // The switch control is subject to the selected type.
                }, (error: BusinessError) => {
                  if (error) {
                    console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
                    return;
                  }
                  console.info('Succeed in starting vibration');
                });
              } catch (err) {
                let e: BusinessError = err as BusinessError;
                console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
              }
            }
            this.uiContext.getHostContext()?.resourceManager.closeRawFdSync(fileName);
          })
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

3. Start vibration of the specified duration.

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

try {
  vibrator.startVibration({
    type: 'time',
    duration: 1000
  }, {
    id: 0,
    usage: 'alarm' // The switch control is subject to the selected type.
  }).then(() => {
    console.info('Succeed in starting vibration');
  }, (error: BusinessError) => {
    console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
  });
} catch (err) {
  let e: BusinessError = err as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}
```

## vibrator.stopVibration<sup>9+</sup>

stopVibration(stopMode: VibratorStopMode, callback: AsyncCallback&lt;void&gt;): void

Stops vibration in the specified mode. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                                 | Mandatory| Description                                                        |
| -------- | ------------------------------------- | ---- | ------------------------------------------------------------ |
| stopMode | [VibratorStopMode](#vibratorstopmode) | Yes  | Mode to stop the vibration. The options are as follows:<br>- **VIBRATOR_STOP_MODE_TIME**: used to stop vibration of the specified duration.<br>- **VIBRATOR_STOP_MODE_PRESET**: used to stop vibration of the preset effect.<br>To stop custom vibration, use [vibrator.stopVibration<sup>10+</sup>](#vibratorstopvibration10).|
| callback | AsyncCallback&lt;void&gt;             | Yes  | Callback used to return the result. If the vibration stops, **err** is **undefined**; otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 201      | Permission denied.                                           |
| 401      | Parameter error.Possible causes:1. Mandatory parameters are left unspecified;2. Incorrect parameter types;3. Parameter verification failed. |

**Example**

Stop vibration of the specified duration.

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

try {
  // Start vibration of the specified duration.
  vibrator.startVibration({
    type: 'time',
    duration: 1000,
  }, {
    id: 0,
    usage: 'alarm' // The switch control is subject to the selected type.
  }, (error: BusinessError) => {
    if (error) {
      console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
      return;
    }
    console.info('Succeed in starting vibration');
  });
} catch (err) {
  let e: BusinessError = err as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}

try {
  // Stop vibration in VIBRATOR_STOP_MODE_TIME mode.
  vibrator.stopVibration(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_TIME, (error: BusinessError) => {
    if (error) {
      console.error(`Failed to stop vibration. Code: ${error.code}, message: ${error.message}`);
      return;
    }
    console.info('Succeed in stopping vibration');
  })
} catch (err) {
  let e: BusinessError = err as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}
```

Stop preset vibration.

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

try {
  // Start vibration with a preset effect.
  vibrator.startVibration({
    type: 'preset',
    effectId: 'haptic.clock.timer',
    count: 1,
  }, {
    id: 0,
    usage: 'alarm' // The switch control is subject to the selected type.
  }, (error: BusinessError) => {
    if (error) {
      console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
      return;
    }
    console.info('Succeed in starting vibration');
  });
} catch (err) {
  let e: BusinessError = err as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}

try {
  // Stop vibration in VIBRATOR_STOP_MODE_PRESET mode.
  vibrator.stopVibration(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_PRESET, (error: BusinessError) => {
    if (error) {
      console.error(`Failed to stop vibration. Code: ${error.code}, message: ${error.message}`);
      return;
    }
    console.info('Succeed in stopping vibration');
  })
} catch (err) {
  let e: BusinessError = err as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}
```

## vibrator.stopVibration<sup>9+</sup>

stopVibration(stopMode: VibratorStopMode): Promise&lt;void&gt;

Stops vibration in the specified mode. This API uses a promise to return the result.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                                 | Mandatory| Description                                                        |
| -------- | ------------------------------------- | ---- | ------------------------------------------------------------ |
| stopMode | [VibratorStopMode](#vibratorstopmode) | Yes  | Vibration stop mode:<br>- **VIBRATOR_STOP_MODE_TIME**: used to stop vibration of the specified duration.<br>- **VIBRATOR_STOP_MODE_PRESET**: used to stop vibration of the preset effect.<br>To stop custom vibration, use [vibrator.stopVibration<sup>10+</sup>](#vibratorstopvibration10-1).|

**Return value**

| Type               | Description         |
| ------------------- | ------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 201      | Permission denied.                                           |
| 401      | Parameter error.Possible causes:1. Mandatory parameters are left unspecified;2. Incorrect parameter types;3. Parameter verification failed. |

**Example**

Stop vibration of the specified duration.

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

try {
  // Start vibration of the specified duration.
  vibrator.startVibration({
    type: 'time',
    duration: 1000,
  }, {
    id: 0,
    usage: 'alarm' // The switch control is subject to the selected type.
  }).then(() => {
    console.info('Succeed in starting vibration');
  }, (error: BusinessError) => {
    console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
  });
} catch (err) {
  let e: BusinessError = err as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}

try {
  // Stop vibration in VIBRATOR_STOP_MODE_TIME mode.
  vibrator.stopVibration(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_TIME).then(() => {
    console.info('Succeed in stopping vibration');
  }, (error: BusinessError) => {
    console.error(`Failed to stop vibration. Code: ${error.code}, message: ${error.message}`);
  });
} catch (err) {
  let e: BusinessError = err as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}
```

Stop preset vibration.

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

try {
  // Start vibration with a preset effect.
  vibrator.startVibration({
    type: 'preset',
    effectId: 'haptic.clock.timer',
    count: 1,
  }, {
    id: 0,
    usage: 'alarm' // The switch control is subject to the selected type.
  }).then(() => {
    console.info('Succeed in starting vibration');
  }, (error: BusinessError) => {
    console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
  });
} catch (err) {
  let e: BusinessError = err as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}

try {
  // Stop vibration in VIBRATOR_STOP_MODE_PRESET mode.
  vibrator.stopVibration(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_PRESET).then(() => {
    console.info('Succeed in stopping vibration');
  }, (error: BusinessError) => {
    console.error(`Failed to stop vibration. Code: ${error.code}, message: ${error.message}`);
  });
} catch (err) {
  let e: BusinessError = err as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}
```

## vibrator.stopVibration<sup>10+</sup>

stopVibration(callback: AsyncCallback&lt;void&gt;): void

Stops vibration in all modes. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.VIBRATE

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                     | Mandatory| Description                                                        |
| -------- | ------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result. If the vibration stops, **err** is **undefined**; otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md).

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |

**Example**

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

try {
  // Stop vibration in all modes.
  vibrator.stopVibration((error: BusinessError) => {
    if (error) {
      console.error(`Failed to stop vibration. Code: ${error.code}, message: ${error.message}`);
      return;
    }
    console.info('Succeed in stopping vibration');
  })
} catch (error) {
  let e: BusinessError = error as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}
```

## vibrator.stopVibration<sup>10+</sup>

stopVibration(): Promise&lt;void&gt;

Stops vibration in all modes. This API uses a promise to return the result.

**Required permissions**: ohos.permission.VIBRATE

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Sensors.MiscDevice

**Return value**

| Type               | Description         |
| ------------------- | ------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md).

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |

**Example**

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

try {
  // Stop vibration in all modes.
  vibrator.stopVibration().then(() => {
    console.info('Succeed in stopping vibration');
  }, (error: BusinessError) => {
    console.error(`Failed to stop vibration. Code: ${error.code}, message: ${error.message}`);
  });
} catch (error) {
  let e: BusinessError = error as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}
```

## vibrator.stopVibrationSync<sup>12+</sup>

stopVibrationSync(): void

Stops any form of motor vibration.

**Required permissions**: ohos.permission.VIBRATE

**Atomic service API**: This API can be used in atomic services since API version 12.

**System capability**: SystemCapability.Sensors.MiscDevice

**Error codes**

For details about the error codes, see [Vibrator Error Codes](errorcode-vibrator.md) and [Universal Error Codes](../errorcode-universal.md).

| ID| Error Message                |
| -------- | ------------------------ |
| 201      | Permission denied.       |
| 14600101 | Device operation failed. |

**Example**

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

try {
  // Stop any form of motor vibration.
    vibrator.stopVibrationSync()
    console.info('Succeed in stopping vibration');
} catch (error) {
  let e: BusinessError = error as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}
```

## vibrator.isSupportEffect<sup>10+</sup>

isSupportEffect(effectId: string, callback: AsyncCallback&lt;boolean&gt;): void

Checks whether an effect ID is supported. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                        | Mandatory| Description                                                       |
| -------- | ---------------------------- | ---- | ----------------------------------------------------------- |
| effectId | string                       | Yes  | Vibration effect ID.                                           |
| callback | AsyncCallback&lt;boolean&gt; | Yes  | Callback used to return the result. The value **true** means that the effect ID is supported, and the value **false** means the opposite.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 201      | Permission denied.                                           |
| 401      | Parameter error.Possible causes:1. Mandatory parameters are left unspecified;2. Incorrect parameter types;3. Parameter verification failed. |

**Example**

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

try {
  // Check whether 'haptic.clock.timer' is supported.
  vibrator.isSupportEffect('haptic.clock.timer', (err: BusinessError, state: boolean) => {
    if (err) {
      console.error(`Failed to query effect. Code: ${err.code}, message: ${err.message}`);
      return;
    }
    console.info('Succeed in querying effect');
    if (state) {
      try {
        // To use startVibration, you must configure the ohos.permission.VIBRATE permission.
        vibrator.startVibration({
          type: 'preset',
          effectId: 'haptic.clock.timer',
          count: 1,
        }, {
          usage: 'unknown' // The switch control is subject to the selected type.
        }, (error: BusinessError) => {
          if (error) {
            console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
          } else {
            console.info('Succeed in starting vibration');
          }
        });
      } catch (error) {
        let e: BusinessError = error as BusinessError;
        console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
      }
    }
  })
} catch (error) {
  let e: BusinessError = error as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}
```

## vibrator.isSupportEffect<sup>10+</sup>

isSupportEffect(effectId: string): Promise&lt;boolean&gt;

Checks whether an effect ID is supported. This API uses a promise to return the result.

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type  | Mandatory| Description            |
| -------- | ------ | ---- | ---------------- |
| effectId | string | Yes  | Vibration effect ID.|

**Return value**

| Type                  | Description                                                        |
| ---------------------- | ------------------------------------------------------------ |
| Promise&lt;boolean&gt; | Promise that returns the result. The value **true** means that the effect ID is supported, and the value **false** means the opposite.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 201      | Permission denied.                                           |
| 401      | Parameter error.Possible causes:1. Mandatory parameters are left unspecified;2. Incorrect parameter types;3. Parameter verification failed. |

**Example**

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

try {
  // Check whether 'haptic.clock.timer' is supported.
  vibrator.isSupportEffect('haptic.clock.timer').then((state: boolean) => {
    console.info(`The query result is ${state}`);
    if (state) {
      try {
        vibrator.startVibration({
          type: 'preset',
          effectId: 'haptic.clock.timer',
          count: 1,
        }, {
          usage: 'unknown' // The switch control is subject to the selected type.
        }).then(() => {
          console.info('Succeed in starting vibration');
        }).catch((error: BusinessError) => {
          console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
        });
      } catch (error) {
        let e: BusinessError = error as BusinessError;
        console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
      }
    }
  }, (error: BusinessError) => {
    console.error(`Failed to query effect. Code: ${error.code}, message: ${error.message}`);
  })
} catch (error) {
  let e: BusinessError = error as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}
```

## vibrator.isSupportEffectSync<sup>12+</sup>

isSupportEffectSync(effectId: string): boolean

Checks whether the preset vibration effect is supported.

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type  | Mandatory| Description                |
| -------- | ------ | ---- | -------------------- |
| effectId | string | Yes  | ID of the preset vibration effect.|

**Return value**

| Type   | Description                                                       |
| ------- | ----------------------------------------------------------- |
| boolean | Returned object. The value **true** means that the effect ID is supported, and the value **false** means the opposite.|

**Error codes**

For details about the error codes, see [Vibrator Error Codes](errorcode-vibrator.md) and [Universal Error Codes](../errorcode-universal.md).

| ID| Error Message                                                    |
| -------- | ------------------------------------------------------------ |
| 401      | Parameter error.Possible causes:1. Mandatory parameters are left unspecified;2. Incorrect parameter types;3. Parameter verification failed. |
| 14600101 | Device operation failed.                                     |

**Example**

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

try {
    // Check whether the preset 'haptic.clock.timer' is supported.
    let ret = vibrator.isSupportEffectSync('haptic.clock.timer');
    console.info(`The query result is ${ret}`);
} catch (error) {
    let e: BusinessError = error as BusinessError;
    console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}
```

## vibrator.isHdHapticSupported<sup>12+</sup>

isHdHapticSupported(): boolean

Checks whether HD vibration is supported.

**System capability**: SystemCapability.Sensors.MiscDevice

**Return value**

| Type   | Description                                                     |
| ------- | --------------------------------------------------------- |
| boolean | Boolean value indicating whether HD vibration is supported. The value **true** indicates that HD vibration is supported, and the value **false** indicates the opposite.|

**Error codes**

For details about the error codes, see [Vibrator Error Codes](errorcode-vibrator.md).

| ID| Error Message                |
| -------- | ------------------------ |
| 14600101 | Device operation failed. |

**Example**

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

try {
    // Check whether HD vibration is supported.
    let ret = vibrator.isHdHapticSupported();
    console.info(`The query result is ${ret}`);
} catch (error) {
    let e: BusinessError = error as BusinessError;
    console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}
```

## VibratorPatternBuilder<sup>18+</sup>

### vibrator('addContinuousEvent')<sup>18+</sup>

addContinuousEvent(time: number, duration: number, options?: ContinuousParam): VibratorPatternBuilder;

Adds a long vibration event as a **VibratorPattern** object.

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                                 | Mandatory| Description                    |
| -------- | ------------------------------------- | ---- | ------------------------ |
| time     | number                                | Yes  | Start time of the long vibration.    |
| duration | number                                | Yes  | Duration of the long vibration.    |
| options  | [ContinuousParam](#continuousparam18) | No  | Optional parameters.|

**Return value**

| Type                  | Description                                                |
| ---------------------- | ---------------------------------------------------- |
| VibratorPatternBuilder | **VibratorPatternBuilder** object representing a long vibration event.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md).

| ID| Error Message        |
| -------- | ---------------- |
| 401      | Parameter error. |

**Example**

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

let builder = new vibrator.VibratorPatternBuilder();
try {
  let pointsMe: vibrator.VibratorCurvePoint[] = [
	{ time: 0, intensity: 0, frequency: -7 },
	{ time: 42, intensity: 1, frequency: -6 },
	{ time: 128, intensity: 0.94, frequency: -4 },
	{ time: 217, intensity: 0.63, frequency: -14 },
	{ time: 763, intensity: 0.48, frequency: -14 },
	{ time: 1125, intensity: 0.53, frequency: -10 },
	{ time: 1503, intensity: 0.42, frequency: -14 },
	{ time: 1858, intensity: 0.39, frequency: -14 },
	{ time: 2295, intensity: 0.34, frequency: -17 },
	{ time: 2448, intensity: 0.21, frequency: -14 },
	{ time: 2468, intensity: 0, frequency: -21 }
  ] // No less than four VibratorCurvePoint objects must be set. The maximum value is 16.
  let param: vibrator.ContinuousParam = {
	intensity: 97,
	frequency: 34,
	points:pointsMe,
	index: 0
  }
  builder.addContinuousEvent(0, 2468, param);
  console.info(`addContinuousEvent builder is ${builder.build()}`);
} catch(error) {
  let e: BusinessError = error as BusinessError;
  console.error(`Exception. Code ${e.code}`);
}
```

### vibrator('addTransientEvent')<sup>18+</sup>

addTransientEvent(time: number, options?: TransientParam): VibratorPatternBuilder;

Adds a short vibration event as a **VibratorPattern** object.

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name | Type                               | Mandatory| Description                    |
| ------- | ----------------------------------- | ---- | ------------------------ |
| time    | number                              | Yes  | Start time of long vibration.    |
| options | [TransientParam](#transientparam18) | No  | Optional parameters.|

**Return value**

| Type                  | Description                                            |
| ---------------------- | ------------------------------------------------ |
| VibratorPatternBuilder | **VibratorPatternBuilder** object representing a short vibration event.|

**Error codes**

For details about the error codes, see [Universal Error Codes](../errorcode-universal.md).

| ID| Error Message        |
| -------- | ---------------- |
| 401      | Parameter error. |

**Example**

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

let builder = new vibrator.VibratorPatternBuilder();
try {
  let param: vibrator.TransientParam = {
	intensity: 80,
	frequency: 70,
	index: 0
  }
  builder.addTransientEvent(0, param);
  console.log(`addTransientEvent builder is ${builder.build()}`);
} catch(error) {
  let e: BusinessError = error as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}
```

### vibrator('build')<sup>18+</sup>

build(): VibratorPattern;

Constructor used to create a **VibratorPattern** object, which determines the vibration sequence of short or long events.

**System capability**: SystemCapability.Sensors.MiscDevice

**Return value**

| Type                                 | Description                              |
| ------------------------------------- | ---------------------------------- |
| [VibratorPattern](#vibratorpattern18) | **VibratorPattern** object.|

**Example**

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

let builder = new vibrator.VibratorPatternBuilder();
try {
  let param: vibrator.TransientParam = {
	intensity: 80,
	frequency: 70,
	index: 0
  }
  builder.addTransientEvent(0, param);
  console.log(`addTransientEvent builder is ${builder.build()}`);
} catch(error) {
  let e: BusinessError = error as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}
try {
  vibrator.startVibration({
	type: "pattern",
	pattern: builder.build()
  }, {
	usage: "alarm", // The switch control is subject to the selected type.
  }, (error) => {
	if (error) {
	  let e: BusinessError = error as BusinessError;
	  console.error(`Vibrate fail. Code: ${e.code}, message: ${e.message}`);
	} else {
	  console.info(`vibrate success`);
	}
  });
} catch(error) {
  let e: BusinessError = error as BusinessError;
  console.error(`An unexpected error occurred. Code: ${e.code}, message: ${e.message}`);
}
```

## EffectId

Enumerates the preset vibration effect IDs. This parameter is needed when you call [vibrator.startVibration9+](#vibratorstartvibration9) or [vibrator.stopVibration9+](#vibratorstopvibration9-1) to deliver the vibration effect specified by [VibratePreset](#vibratepreset9). This parameter supports a variety of values, such as **haptic.clock.timer**.

Note: Preset effects vary according to devices. You are advised to call [vibrator.isSupportEffect](#vibratorissupporteffect10-1)<sup>10+</sup> to check whether the device supports the preset effect before use.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name              | Value                  | Description                            |
| ------------------ | -------------------- | -------------------------------- |
| EFFECT_CLOCK_TIMER | 'haptic.clock.timer' | Vibration effect when a user adjusts the timer.|

## HapticFeedback<sup>12+</sup>

Defines the vibration effect. The frequency of the same vibration effect may vary depending on the vibrator, but the frequency trend remains consistent.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name                               | Value                     | Description                        |
| ----------------------------------- | ----------------------- | ---------------------------- |
| EFFECT_SOFT                         | 'haptic.effect.soft'    | Soft vibration, low frequency.|
| EFFECT_HARD                         | 'haptic.effect.hard'    | Hard vibration, medium frequency.|
| EFFECT_SHARP                        | 'haptic.effect.sharp'   | Sharp vibration, high frequency.|
| EFFECT_NOTICE_SUCCESS<sup>18+</sup> | 'haptic.notice.success' | Vibration for a success notification.    |
| EFFECT_NOTICE_FAILURE<sup>18+</sup> | 'haptic.notice.fail'    | Vibration for a failure notification.    |
| EFFECT_NOTICE_WARNING<sup>18+</sup> | 'haptic.notice.warning' | Vibration for an alert.    |

## VibratorStopMode

Enumerates vibration stop modes. This parameter is required for [vibrator.stopVibration9+](#vibratorstopvibration9) or [vibrator.stopVibration9+](#vibratorstopvibration9-1). The stop mode must match that delivered in [VibrateEffect9+](#vibrateeffect9).

**System capability**: SystemCapability.Sensors.MiscDevice

| Name                     | Value      | Description                    |
| ------------------------- | -------- | ------------------------ |
| VIBRATOR_STOP_MODE_TIME   | 'time'   | The vibration to stop is in **duration** mode.|
| VIBRATOR_STOP_MODE_PRESET | 'preset' | The vibration to stop is in **EffectId** mode.|

## VibrateEffect<sup>9+</sup>

Describes the vibration effect. This parameter is required for [vibrator.startVibration9+](#vibratorstartvibration9) or [vibrator.startVibration9+](#vibratorstartvibration9-1).

**System capability**: SystemCapability.Sensors.MiscDevice

| Type                                 | Description                                                        |
| ------------------------------------- | ------------------------------------------------------------ |
| [VibrateTime](#vibratetime9)          | Start vibration of the specified duration.<br>**Atomic service API**: This API can be used in atomic services since API version 11.|
| [VibratePreset](#vibratepreset9)      | Vibration with a preset effect.                              |
| [VibrateFromFile](#vibratefromfile10) | Vibration according to a custom vibration configuration file.                        |
| VibrateFromPattern<sup>18+</sup>      | Triggers vibration with the custom effect. This API uses an asynchronous callback to return the result.                            |

## VibrateTime<sup>9+</sup>

Represents vibration of the specified duration.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name    | Type  | Mandatory| Description                                  |
| -------- | ------ | ---- | -------------------------------------- |
| type     | 'time' | Yes  | The value is **time**, indicating vibration of the specified duration.|
| duration | number | Yes  | Vibration duration, in ms.            |

## VibratePreset<sup>9+</sup>

Represents the preset vibration effect. You can pass this value to [VibrateEffect9+](#vibrateeffect9) to specify a preset vibration effect when calling [vibrator.startVibration9+](#vibratorstartvibration9) or [vibrator.startVibration9+](#vibratorstartvibration9-1).

**System capability**: SystemCapability.Sensors.MiscDevice

| Name                   | Type    | Mandatory| Description                                                        |
| ----------------------- | -------- | ---- | ------------------------------------------------------------ |
| type                    | 'preset' | Yes  | The value **preset** means vibration with the specified effect.                |
| effectId                | string   | Yes  | Preset vibration effect ID.                                          |
| count                   | number   | No  | Number of repeated vibrations. This parameter is optional. The default value is **1**.                        |
| intensity<sup>12+</sup> | number   | No  | Vibration intensity. This parameter is optional. The value range is [0, 100]. The default value is **100**. If vibration intensity adjustment is not supported, the default vibration intensity will be used.|

## VibrateFromFile<sup>10+</sup>

Represents a custom vibration pattern. It is supported only by certain devices. An error code will be returned if a device does not support this vibration mode. You can pass this value to [VibrateEffect9+](#vibrateeffect9) to specify a custom vibration pattern when calling [vibrator.startVibration9+](#vibratorstartvibration9) or [vibrator.startVibration9+](#vibratorstartvibration9-1).

**System capability**: SystemCapability.Sensors.MiscDevice

| Name    | Type                                                        | Mandatory| Description                                      |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------ |
| type     | 'file'                                                       | Yes  | The value **file** means vibration according to a vibration configuration file.|
| hapticFd | [HapticFileDescriptor](#hapticfiledescriptor10)<sup>10+</sup> | Yes  | File descriptor (FD) of the vibration configuration file.                    |

## HapticFileDescriptor<sup>10+</sup>

Describes the FD of a custom vibration configuration file. Ensure that the file is available, and the parameters in it can be obtained from the sandbox path through the [file management API](../apis-core-file-kit/js-apis-file-fs.md#fsopen) or from the HAP resource through the [resource management API](../apis-localization-kit/js-apis-resource-manager.md#getrawfd9). The use case is as follows: The system triggers vibration according to the sequence set in a configuration file, based on the specified offset and length. For details about the storage format of the vibration sequence, see [Custom Vibration](../../device/sensor/vibrator-guidelines.md#custom-vibration).

**System capability**: SystemCapability.Sensors.MiscDevice

| Name  | Type  | Mandatory| Description                                                        |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| fd     | number | Yes  | FD of the custom vibration configuration file.                                            |
| offset | number | No  | Offset from the start position of the file, in bytes. The default value is the start position of the file, and the value cannot exceed the valid range of the file.|
| length | number | No  | Resource length, in bytes. The default value is the length from the offset position to the end of the file, and the value cannot exceed the valid range of the file.|

## VibratorEventType<sup>18+</sup>

Vibration event type.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name      | Type  | Mandatory| Description             |
| ---------- | ------ | ---- | ----------------- |
| CONTINUOUS | number | Yes  | The value **0** indicates long vibration.|
| TRANSIENT  | number | Yes  | The value **1** indicates short vibration.|

## VibratorCurvePoint<sup>18+</sup>

Defines the gain relative to the vibration intensity.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name     | Type  | Mandatory| Description                                                        |
| --------- | ------ | ---- | ------------------------------------------------------------ |
| time      | number | Yes  | Start time offset.                                              |
| intensity | number | No  | Gain relative to the vibration intensity. This parameter is optional. The value range is [0, 1]. If this parameter is left empty, the default value is **1**.|
| frequency | number | No  | Change relative to the vibration frequency. This parameter is optional. The value range is [-100, 100]. If this parameter is left empty, the default value is 0.|

## VibratorEvent<sup>18+</sup>

Vibration event.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name     | Type                           | Mandatory| Description                                                        |
| --------- | ------------------------------- | ---- | ------------------------------------------------------------ |
| eventType | VibratorEventType               | Yes  | Vibration event type.                                              |
| time      | number                          | Yes  | Vibration start time.                                              |
| duration  | number                          | No  | Vibration duration. This parameter is optional. The value range is [0, 5000]. The default value is **48** for short vibration and **1000** for long vibration.|
| intensity | number                          | No  | Vibration intensity. This parameter is optional. The value range is [0, 100]. If this parameter is left empty, the default value is **100**.|
| frequency | number                          | No  | Vibration frequency. This parameter is optional.The value range is [0, 100]. If this parameter is left empty, the default value is **50**. |
| index     | number                          | No  | Channel number. This parameter is optional. If this parameter is left empty, the default value is **0**.                   |
| points    | Array&lt;VibratorCurvePoint&gt; | No  | Adjustment points of the vibration curve.                            |

## VibratorPattern<sup>18+</sup>

Defines the vibration sequence.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name  | Type                      | Mandatory| Description                                                |
| ------ | -------------------------- | ---- | ---------------------------------------------------- |
| time   | number                     | Yes  | Absolute vibration start time.                                  |
| events | Array&lt;VibratorEvent&gt; | Yes  | Vibration event array, which is the **VibratorPattern** object returned by **build() **.|

## ContinuousParam<sup>18+</sup>

Defines the parameters for continuous vibration.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name     | Type                | Mandatory| Description                                                        |
| --------- | -------------------- | ---- | ------------------------------------------------------------ |
| intensity | number               | No  | Vibration intensity. This parameter is optional. The value range is [0, 100]. If this parameter is left empty, the default value is **100**.|
| frequency | number               | No  | Vibration frequency. This parameter is optional.The value range is [0, 100]. If this parameter is left empty, the default value is **50**. |
| points    | VibratorCurvePoint[] | No  | Adjustment points of the vibration curve.                            |
| index     | number               | No  | Channel number. This parameter is optional. If this parameter is left empty, the default value is **0**.                   |

## TransientParam<sup>18+</sup>

Defines the parameters for transient vibration.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name     | Type  | Mandatory| Description                                       |
| --------- | ------ | ---- | ------------------------------------------- |
| intensity | number | No  | Vibration intensity. This parameter is optional. If this parameter is left empty, the default value is **100**.|
| frequency | number | No  | Vibration frequency. This parameter is optional. If this parameter is left empty, the default value is **50**. |
| index     | number | No  | Channel number. This parameter is optional. If this parameter is left empty, the default value is **0**.  |

## VibrateFromPattern<sup>18+</sup>

Defines the custom vibration effect.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name   | Type           | Mandatory| Description                                                |
| ------- | --------------- | ---- | ---------------------------------------------------- |
| type    | 'pattern'       | Yes  | If the value is **pattern**, the vibrator vibrates based on the specified pattern.           |
| pattern | VibratorPattern | Yes  | Vibration event array, which is the **VibratorPattern** object returned by **build() **.|

## VibrateAttribute<sup>9+</sup>

Describes the vibration attribute.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name | Type            | Mandatory| Description                  |
| ----- | ---------------- | ---- | ---------------------- |
| id    | number           | No  | Vibrator ID. The default value is **0**.|
| usage | [Usage](#usage9) | Yes  | Vibration scenario.  |

## Usage<sup>9+</sup>

type Usage = 'unknown' | 'alarm' | 'ring' | 'notification' | 'communication' | 'touch' | 'media' | 'physicalFeedback' | 'simulateReality'

Enumerates the vibration scenarios.

**Atomic service API**: This API can be used in atomic services since API version 11.

**System capability**: SystemCapability.Sensors.MiscDevice
<!--RP1-->

| Type              | Description                                                   |
| ------------------ | ------------------------------------------------------- |
| 'unknown'          | Unknown scenario, with the lowest priority. This parameter has a fixed value of **unknown**.|
| 'alarm'            | Vibration for alarms. This parameter has a fixed value of **alarm**.                  |
| 'ring'             | Vibration for ringing. This parameter has a fixed value of **ring**.                   |
| 'notification'     | Vibration for notification. This parameter has a fixed value of **notification**.           |
| 'communication'    | Vibration for communication. This parameter has a fixed value of **communication**.          |
| 'touch'            | Vibration for touch. This parameter has a fixed value of **touch**.                  |
| 'media'            | Vibration for media. This parameter has a fixed value of **media**.                |
| 'physicalFeedback' | Vibration for physical feedback. This parameter has a fixed value of **physicalFeedback**.   |
| 'simulateReality'  | Vibration for simulated reality. This parameter has a fixed value of **simulateReality**.    |

<!--RP1End-->

## vibrator.vibrate<sup>(deprecated)</sup>

vibrate(duration: number): Promise&lt;void&gt;

Triggers vibration with the specified duration. This API uses a promise to return the result.

This API is deprecated since API version 9. You are advised to use [vibrator.startVibration](#vibratorstartvibration9-1)<sup>9+</sup> instead.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type  | Mandatory| Description                  |
| -------- | ------ | ---- | ---------------------- |
| duration | number | Yes  | Vibration duration, in ms.|

**Return value**

| Type               | Description         |
| ------------------- | ------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

vibrator.vibrate(1000).then(() => {
  console.info('Succeed in vibrating');
}, (error: BusinessError) => {
  console.error(`Failed to vibrate. Code: ${error.code}, message: ${error.message}`);
});
```

## vibrator.vibrate<sup>(deprecated)</sup>

vibrate(duration: number, callback?: AsyncCallback&lt;void&gt;): void

Triggers vibration with the specified duration. This API uses an asynchronous callback to return the result.

This API is deprecated since API version 9. You are advised to use [vibrator.startVibration](#vibratorstartvibration9)<sup>9+</sup> instead.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                     | Mandatory| Description                                                      |
| -------- | ------------------------- | ---- | ---------------------------------------------------------- |
| duration | number                    | Yes  | Vibration duration, in ms.                                    |
| callback | AsyncCallback&lt;void&gt; | No  | Callback used to return the result. If the vibration starts, **err** is **undefined**; otherwise, **err** is an error object.|

**Example**

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

vibrator.vibrate(1000, (error: BusinessError) => {
  if (error) {
    console.error(`Failed to vibrate. Code: ${error.code}, message: ${error.message}`);
  } else {
    console.info('Succeed in vibrating');
  }
})
```


## vibrator.vibrate<sup>(deprecated)</sup>

vibrate(effectId: EffectId): Promise&lt;void&gt;

Triggers vibration with the specified effect. This API uses a promise to return the result.

This API is deprecated since API version 9. You are advised to use [vibrator.startVibration](#vibratorstartvibration9-1)<sup>9+</sup> instead.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                 | Mandatory| Description              |
| -------- | --------------------- | ---- | ------------------ |
| effectId | [EffectId](#effectid) | Yes  | Preset vibration effect ID.|

**Return value**

| Type               | Description         |
| ------------------- | ------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

vibrator.vibrate(vibrator.EffectId.EFFECT_CLOCK_TIMER).then(() => {
  console.info('Succeed in vibrating');
}, (error: BusinessError) => {
  console.error(`Failed to vibrate. Code: ${error.code}, message: ${error.message}`);
});
```


## vibrator.vibrate<sup>(deprecated)</sup>

vibrate(effectId: EffectId, callback?: AsyncCallback&lt;void&gt;): void

Triggers vibration with the specified effect. This API uses an asynchronous callback to return the result.

This API is deprecated since API version 9. You are advised to use [vibrator.startVibration](#vibratorstartvibration9)<sup>9+</sup> instead.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                     | Mandatory| Description                                                      |
| -------- | ------------------------- | ---- | ---------------------------------------------------------- |
| effectId | [EffectId](#effectid)     | Yes  | Preset vibration effect ID.                                        |
| callback | AsyncCallback&lt;void&gt; | No  | Callback used to return the result. If the vibration starts, **err** is **undefined**; otherwise, **err** is an error object.|

**Example**

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

vibrator.vibrate(vibrator.EffectId.EFFECT_CLOCK_TIMER, (error: BusinessError) => {
  if (error) {
    console.error(`Failed to vibrate. Code: ${error.code}, message: ${error.message}`);
  } else {
    console.info('Succeed in vibrating');
  }
})
```

## vibrator.stop<sup>(deprecated)</sup>

stop(stopMode: VibratorStopMode): Promise&lt;void&gt;

Stops vibration in the specified mode. This API uses a promise to return the result.

This API is deprecated since API version 9. You are advised to use [vibrator.stopVibration](#vibratorstopvibration9-1)<sup>9+</sup> instead.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                                 | Mandatory| Description                    |
| -------- | ------------------------------------- | ---- | ------------------------ |
| stopMode | [VibratorStopMode](#vibratorstopmode) | Yes  | Mode to stop the vibration.|

**Return value**

| Type               | Description         |
| ------------------- | ------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

// Start vibration based on the specified effect ID.
vibrator.vibrate(vibrator.EffectId.EFFECT_CLOCK_TIMER, (error: BusinessError) => {
  if (error) {
    console.error(`Failed to vibrate. Code: ${error.code}, message: ${error.message}`);
  } else {
    console.info('Succeed in vibrating');
  }
})
// Stop vibration in VIBRATOR_STOP_MODE_PRESET mode.
vibrator.stop(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_PRESET).then(() => {
  console.info('Succeed in stopping');
}, (error: BusinessError) => {
  console.error(`Failed to stop. Code: ${error.code}, message: ${error.message}`);
});
```


## vibrator.stop<sup>(deprecated)</sup>

stop(stopMode: VibratorStopMode, callback?: AsyncCallback&lt;void&gt;): void

Stops vibration in the specified mode. This API uses an asynchronous callback to return the result.

This API is deprecated since API version 9. You are advised to use [vibrator.stopVibration](#vibratorstopvibration9)<sup>9+</sup> instead.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                                 | Mandatory| Description                                                        |
| -------- | ------------------------------------- | ---- | ------------------------------------------------------------ |
| stopMode | [VibratorStopMode](#vibratorstopmode) | Yes  | Mode to stop the vibration.                                    |
| callback | AsyncCallback&lt;void&gt;             | No  | Callback used to return the result. If the vibration stops, **err** is **undefined**; otherwise, **err** is an error object.|

**Example**

```ts
import { vibrator } from '@kit.SensorServiceKit';
import { BusinessError } from '@kit.BasicServicesKit';

// Start vibration based on the specified effect ID.
vibrator.vibrate(vibrator.EffectId.EFFECT_CLOCK_TIMER, (error: BusinessError) => {
  if (error) {
    console.error(`Failed to vibrate. Code: ${error.code}, message: ${error.message}`);
  } else {
    console.info('Succeed in vibrating');
  }
})
// Stop vibration in VIBRATOR_STOP_MODE_PRESET mode.
vibrator.stop(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_PRESET, (error: BusinessError) => {
  if (error) {
    console.error(`Failed to stop. Code: ${error.code}, message: ${error.message}`);
  } else {
    console.info('Succeed in stopping');
  }
})
```
