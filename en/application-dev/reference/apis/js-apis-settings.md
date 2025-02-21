# @ohos.settings (Data Item Settings)

The **settings** module provides APIs for setting data items.

> **NOTE**
> 
> The initial APIs of this module are supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```js
import settings from '@ohos.settings';
```

## date

Provides data items for setting the time and date formats.

### Attributes

**System capability**: SystemCapability.Applications.settings.Core

| Name               | Type  | Readable| Writable| Description                                                        |
| ------------------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| DATE_FORMAT         | string | Yes  | Yes  | Date format.<br>The value can be **mm/dd/yyyy**, **dd/mm/yyyy**, or **yyyy/mm/dd**, where **mm** indicates the month, **dd** indicates the day, and **yyyy** indicates the year.|
| TIME_FORMAT         | string | Yes  | Yes  | Time format.<br>**12**: 12-hour format.<br>**24**: 24-hour format.|
| AUTO_GAIN_TIME      | string | Yes  | Yes  | Whether the date, time, and time zone are automatically obtained from the Network Identity and Time Zone (NITZ).<br>The value **true** means that the date, time, and time zone are automatically obtained from NITZ; and **false** means the opposite. |
| AUTO_GAIN_TIME_ZONE | string | Yes  | Yes  | Whether the time zone is automatically obtained from NITZ.<br>The value **true** means that the time zone is automatically obtained from NITZ; and **false** means the opposite. |

## display

Provides data items for setting the display effects.

### Attributes

**System capability**: SystemCapability.Applications.settings.Core

| Name                         | Type  | Readable| Writable| Description                                                        |
| ----------------------------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| FONT_SCALE                    | string | Yes  | Yes  | Scale factor of the font. The value is a floating point number.                                |
| SCREEN_BRIGHTNESS_STATUS      | string | Yes  | Yes  | Screen brightness. The value ranges from 0 to 255.                              |
| AUTO_SCREEN_BRIGHTNESS        | string | Yes  | Yes  | Whether automatic screen brightness adjustment is enabled.<br>**AUTO_SCREEN_BRIGHTNESS_MODE**: Automatic screen brightness adjustment is enabled.<br>**MANUAL_SCREEN_BRIGHTNESS_MODE**: Automatic screen brightness adjustment is disabled. |
| AUTO_SCREEN_BRIGHTNESS_MODE   | number | Yes  | Yes  | Value of **AUTO_SCREEN_BRIGHTNESS** when automatic screen brightness adjustment is enabled.          |
| MANUAL_SCREEN_BRIGHTNESS_MODE | number | Yes  | Yes  | Value of **AUTO_SCREEN_BRIGHTNESS** when automatic screen brightness adjustment is disabled.          |
| SCREEN_OFF_TIMEOUT            | string | Yes  | Yes  | Waiting time for the device to enter the sleep state when not in use (unit: ms).  |
| DEFAULT_SCREEN_ROTATION       | string | Yes  | Yes  | Rotation angle. This attribute is valid only when screen auto-rotation is disabled.<br>**0**: The screen rotates by 0 degrees.<br>**1**: The screen rotates by 90 degrees.<br>**2**: The screen rotates by 180 degrees.<br>**3**: The screen rotates by 270 degrees.|
| ANIMATOR_DURATION_SCALE       | string | Yes  | Yes  | Scale factor for the animation duration. This affects the start delay and duration of all such animations.<br>If the value is **0**, the animation ends immediately. The default value is **1**.|
| TRANSITION_ANIMATION_SCALE    | string | Yes  | Yes  | Scale factor for transition animations.<br>The value **0** indicates that the transition animations are disabled.          |
| WINDOW_ANIMATION_SCALE        | string | Yes  | Yes  | Scale factor for normal window animations.<br>The value **0** indicates that window animations are disabled.      |
| DISPLAY_INVERSION_STATUS      | string | Yes  | Yes  | Whether display color inversion is enabled.<br>**1**: Display color inversion is enabled.<br>**0**: Display color inversion is disabled.|

## general

Provides data items for setting the general information about the device.

### Attributes

**System capability**: SystemCapability.Applications.settings.Core

| Name                            | Type  | Readable| Writable| Description                                                        |
| -------------------------------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| SETUP_WIZARD_FINISHED            | string | Yes  | Yes  | Whether the startup wizard is running.<br>If the value is **0**, the startup wizard is not running.<br>If the value is not **0**, the startup wizard is running.|
| END_BUTTON_ACTION                | string | Yes  | Yes  | Action after the call end button is pressed if the user is not in a call.<br>**0**: Nothing happens.<br>**1**: The home screen is displayed.<br>**2**: The device enters sleep mode and the screen is locked.<br>**3**: The home screen is displayed. If the focus is already on the home screen, the device will enter sleep mode.|
| ACCELEROMETER_ROTATION_STATUS    | string | Yes  | Yes  | Whether the accelerometer is used to change screen orientation, that is, whether to enable auto-rotation.<br>**1**: The accelerometer is used.<br>**0**: The accelerometer is not used.|
| AIRPLANE_MODE_STATUS             | string | Yes  | Yes  | Whether airplane mode is enabled.<br>**1**: Airplane mode is enabled.<br>**0**: Airplane mode is disabled.|
| DEVICE_PROVISION_STATUS          | string | Yes  | Yes  | Whether the device is preconfigured.<br>On a multi-user device with a single system user, the screen may be locked when the value is **true**. In addition, other features cannot be started on the system user unless they are marked to display on the lock screen.|
| HDC_STATUS                       | string | Yes  | Yes  | Whether the hard disk controller (HDC) on the USB device is enabled.<br>**true**: HDC is enabled.<br>**false**: HDC is disabled.|
| BOOT_COUNTING                    | string | Yes  | Yes  | Number of boot operations after the device is powered on.                                    |
| CONTACT_METADATA_SYNC_STATUS     | string | Yes  | Yes  | Whether contacts metadata synchronization is enabled.<br>**true**: Contacts metadata synchronization is enabled.<br>**false**: Contacts metadata synchronization is disabled.|
| DEVELOPMENT_SETTINGS_STATUS      | string | Yes  | Yes  | Whether developer options are enabled.<br>**true**: Developer options are enabled.<br>**false**: Developer options are disabled.|
| DEVICE_NAME                      | string | Yes  | Yes  | Device name.                                                  |
| USB_STORAGE_STATUS               | string | Yes  | Yes  | Whether USB mass storage is enabled.<br>**true**: USB mass storage is enabled.<br>**false**: USB mass storage is disabled.|
| DEBUGGER_WAITING                 | string | Yes  | Yes  | Whether the device waits for the debugger when starting an application to debug.<br>**1**: The device waits for the debugger.<br>**0**: The device does not wait for the debugger. In this case, the application runs normally.|
| DEBUG_APP_PACKAGE                | string | Yes  | Yes  | Bundle name of the application to be debugged.                             |
| ACCESSIBILITY_STATUS             | string | Yes  | Yes  | Whether accessibility is enabled.<br>**1**: Accessibility is enabled.<br>**0**: Accessibility is disabled.|
| ACTIVATED_ACCESSIBILITY_SERVICES | string | Yes  | Yes  | List of activated accessibility features.                                    |
| GEOLOCATION_ORIGINS_ALLOWED      | string | Yes  | Yes  | Default geographic location that can be used by the browser. Multiple geographic locations are separated by spaces.      |
| SKIP_USE_HINTS                   | string | Yes  | Yes  | Whether the application should attempt to skip all introductory hints at the first startup. This feature is intended for temporary or experienced users.<br>**1**: The application attempts to skip all introductory hints at the first startup.<br>**0**: The application does not skip all introductory hints at the first startup.|
| TOUCH_EXPLORATION_STATUS         | string | Yes  | Yes  | Whether touch exploration is enabled.<br>**1**: Touch exploration is enabled.<br>**0**: Touch exploration is disabled.|

## input

Provides data items for setting input methods.

### Attributes

**System capability**: SystemCapability.Applications.settings.Core

| Name                                | Type  | Readable| Writable| Description                                                        |
| ------------------------------------ | ------ | ---- | ---- | ------------------------------------------------------------ |
| DEFAULT_INPUT_METHOD                 | string | Yes  | Yes  | Default input method and its ID.                                          |
| ACTIVATED_INPUT_METHOD_SUB_MODE      | string | Yes  | Yes  | Type and ID of the default input method keyboard.                                  |
| ACTIVATED_INPUT_METHODS              | string | Yes  | Yes  | List of activated input methods.<br>The list is a string that contains the IDs and keyboard types of activated input methods. The IDs are separated by colons (:), and keyboard types are separated by semicolons (;). An example format is **ima0:keyboardType0;keyboardType1;ima1:ima2:keyboardTypes0,** where **ima** indicates the ID of an input method, and **keyboardType** indicates the keyboard type.|
| SELECTOR_VISIBILITY_FOR_INPUT_METHOD | string | Yes  | Yes  | Whether the input method selector is visible.<br>**1**: The input method selector is visible.<br>**0**: The input method selector is invisible.|
| AUTO_CAPS_TEXT_INPUT                 | string | Yes  | Yes  | Whether automatic capitalization is enabled for the text editor.<br>**0**: Automatic capitalization is disabled.<br>**1**: Automatic capitalization is enabled.|
| AUTO_PUNCTUATE_TEXT_INPUT            | string | Yes  | Yes  | Whether automatic punctuation is enabled for the text editor. Automatic punctuation enables the text editor to convert two spaces into a period (.) and a space.<br>**0**: Automatic punctuation is disabled.<br>**1**: Automatic punctuation is enabled.|
| AUTO_REPLACE_TEXT_INPUT              | string | Yes  | Yes  | Whether autocorrect is enabled for the text editor. Autocorrect enables the text editor to correct typos.<br>**0**: Autocorrect is disabled.<br>**1**: Autocorrect is enabled |
| SHOW_PASSWORD_TEXT_INPUT             | string | Yes  | Yes  | Whether password presentation is enabled in the text editor. Password presentation enables the text editor to show password characters when the user types them.<br>**0**: Password presentation is disabled.<br>**1**: Password presentation is enabled.|

## network

Provides data items for setting network information.

### Attributes

**System capability**: SystemCapability.Applications.settings.Core

| Name                    | Type  | Readable| Writable| Description                                                        |
| ------------------------ | ------ | ---- | ---- | ------------------------------------------------------------ |
| DATA_ROAMING_STATUS      | string | Yes  | Yes  | Whether data roaming is enabled.<br>**true**: Data roaming is enabled.<br>**false**: Data roaming is disabled.|
| HTTP_PROXY_CFG           | string | Yes  | Yes  | Host name and port number of the global HTTP proxy. The host name and port number are separated by a colon (:).|
| NETWORK_PREFERENCE_USAGE | string | Yes  | Yes  | User preferences for the network to use.                                  |

## phone

Provides data items for setting the modes of answering incoming and outgoing calls.

### Attributes

**System capability**: SystemCapability.Applications.settings.Core

| Name              | Type  | Readable| Writable| Description                                                        |
| ------------------ | ------ | ---- | ---- | ------------------------------------------------------------ |
| RTT_CALLING_STATUS | string | Yes  | Yes  | Whether the real-time text (RTT) feature is enabled. If this feature is enabled, incoming and outgoing calls are answered as RTT calls when supported by the device and carrier.<br> **1**: RTT is enabled.<br> **0**: RTT is disabled.|

## sound

Provides data items for setting the sound effects.

### Attributes

**System capability**: SystemCapability.Applications.settings.Core

| Name                        | Type  | Readable| Writable| Description                                                        |
| ---------------------------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| VIBRATE_WHILE_RINGING        | string | Yes  | Yes  | Whether the device vibrates when it is ringing for an incoming call. This attribute is applicable to the phone and settings applications and affects only the scenario where the device rings for an incoming call. It does not affect any other application or scenario.|
| DEFAULT_ALARM_ALERT          | string | Yes  | Yes  | Storage area of the system default alarms and alerts.                                    |
| DTMF_TONE_TYPE_WHILE_DIALING | string | Yes  | Yes  | Type of the dual tone multi-frequency (DTMF) tone played while dialing.<br>**0**: normal short tone.<br>**1**: long tone.|
| DTMF_TONE_WHILE_DIALING      | string | Yes  | Yes  | Whether the DTMF tone is played when dialing.<br>**1**: DTMF tone is played when dialing.<br>**0**: DTMF tone is not played when dialing.|
| AFFECTED_MODE_RINGER_STREAMS | string | Yes  | Yes  | Which audio streams are affected by changes on the ringing mode and Do Not Disturb (DND) mode. If you want a specific audio stream to be affected by changes of the ringing mode and DDN mode, set the corresponding bit to **1**.|
| AFFECTED_MUTE_STREAMS        | string | Yes  | Yes  | Audio streams affected by the mute mode. If you want a specific audio stream to remain muted in mute mode, set the corresponding bit to **1**.|
| DEFAULT_NOTIFICATION_SOUND   | string | Yes  | Yes  | Storage area of the system default notification tone.                                  |
| DEFAULT_RINGTONE             | string | Yes  | Yes  | Storage area of the system default ringtone.                                    |
| SOUND_EFFECTS_STATUS         | string | Yes  | Yes  | Whether the sound feature is available.<br>**0**: The feature is not available.<br>**1**: The feature is available.  |
| VIBRATE_STATUS               | string | Yes  | Yes  | Whether the device vibrates for an event. This attribute is used inside the system.<br>**1**: The device vibrates for an event.<br>**0**: The device does not vibrate for an event.|
| HAPTIC_FEEDBACK_STATUS       | string | Yes  | Yes  | Whether haptic feedback is enabled.<br>**true**: Haptic feedback is enabled.<br>**false**: Haptic feedback is disabled.|

## TTS

Provides data items for setting text-to-speech (TTS) information.

### Attributes

**System capability**: SystemCapability.Applications.settings.Core

| Name               | Type  | Readable| Writable| Description                                                        |
| ------------------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| DEFAULT_TTS_PITCH   | string | Yes  | Yes  | Default pitch of the TTS engine.<br>100 = 1x. If the value is set to **200**, the frequency is twice the normal sound frequency.|
| DEFAULT_TTS_RATE    | string | Yes  | Yes  | Default voice rate of the TTS engine.<br>100 = 1x.                        |
| DEFAULT_TTS_SYNTH   | string | Yes  | Yes  | Default TTS engine.                                               |
| ENABLED_TTS_PLUGINS | string | Yes  | Yes  | List of activated plug-in packages used for TTS. Multiple plug-in packages are separated by spaces.          |


## wireless

Provides data items for setting wireless network information.

### Attributes

**System capability**: SystemCapability.Applications.settings.Core

| Name                             | Type  | Readable| Writable| Description                                                        |
| --------------------------------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| BLUETOOTH_DISCOVER_ABILITY_STATUS | string | Yes  | Yes  | Whether the device can be discovered or connected by other devices through Bluetooth.<br>**0**: The device cannot be discovered or connected.<br>**1**: The device can be connected but cannot be discovered.<br>**2**: The device can be discovered and connected.|
| BLUETOOTH_DISCOVER_TIMEOUT        | string | Yes  | Yes  | Duration for discovering a device through Bluetooth, in seconds.<br>After the duration expires, the device cannot be discovered through Bluetooth.|
| AIRPLANE_MODE_RADIOS              | string | Yes  | Yes  | List of radio signals to be disabled when airplane mode is enabled.<br>Multiple radio signals are separated by commas (,). The list can include the following: **BLUETOOTH_RADIO**, **CELL_RADIO**, **NFC_RADIO**, and **WIFI_RADIO**.|
| BLUETOOTH_RADIO                   | string | Yes  | No  | A value of **AIRPLANE_MODE_RADIOS** to indicate that Bluetooth is disabled in airplane mode.|
| CELL_RADIO                        | string | Yes  | No  | A value of **AIRPLANE_MODE_RADIOS** to indicate that cellular radio is disabled in airplane mode.|
| NFC_RADIO                         | string | Yes  | No  | A value of **AIRPLANE_MODE_RADIOS** to indicate that NFC is disabled in airplane mode.|
| WIFI_RADIO                        | string | Yes  | No  | A value of **AIRPLANE_MODE_RADIOS** to indicate that Wi-Fi is disabled in airplane mode.|
| BLUETOOTH_STATUS                  | string | Yes  | Yes  | Whether Bluetooth is available.<br>**true**: Bluetooth is available.<br>**false**: Bluetooth is unavailable.|
| OWNER_LOCKDOWN_WIFI_CFG           | string | Yes  | Yes  | Whether the Wi-Fi configuration created by the application of the device owner should be locked down.<br>**true**: The Wi-Fi configuration should be locked down.<br>**false**: The Wi-Fi configuration should not be locked down.|
| WIFI_DHCP_MAX_RETRY_COUNT         | string | Yes  | Yes  | Maximum number of attempts to obtain an IP address from the DHCP server.                    |
| WIFI_TO_MOBILE_DATA_AWAKE_TIMEOUT | string | Yes  | Yes  | Maximum duration to hold a wake lock when waiting for the mobile data connection to establish after the Wi-Fi connection is disconnected. |
| WIFI_STATUS                       | string | Yes  | Yes  | Whether Wi-Fi is available.<br>**true**: Wi-Fi is available.<br>**false**: Wi-Fi is unavailable.|
| WIFI_WATCHDOG_STATUS              | string | Yes  | Yes  | Whether Wi-Fi watchdog is available.<br>**true**: Wi-Fi watchdog is available.<br>**false**: Wi-Fi watchdog is unavailable.|


## settings.setValue

setValue(dataAbilityHelper: DataAbilityHelper, name: string, value: object, callback: AsyncCallback\<boolean>): void

Sets the value for a data item. This API uses an asynchronous callback to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Applications.settings.Core

**Parameters**

| Name           | Type                                             | Mandatory| Description                                                        |
| ----------------- | ------------------------------------------------- | ---- | ------------------------------------------------------------ |
| dataAbilityHelper | [DataAbilityHelper](js-apis-inner-ability-dataAbilityHelper.md) | Yes  | **DataAbilityHelper** class.                                            |
| name              | string                                            | Yes  | Name of the target data item. Data items can be classified as follows:<br>- Existing data items in the database<br>- Custom data items|
| value             | object                                            | Yes  | Value of the data item. The value range varies by service.                              |
| callback          | AsyncCallback\<boolean>                           | Yes  | Callback used to return the result. Returns **true** if the operation is successful; returns **false** otherwise.              |

**Example**

```js
import featureAbility from '@ohos.ability.featureAbility';

// Update the value of SCREEN_BRIGHTNESS_STATUS. (As this data item exists in the database, the setValue API will update its value.)
let uri = settings.getUriSync(settings.display.SCREEN_BRIGHTNESS_STATUS);
let helper = featureAbility.acquireDataAbilityHelper(uri);
// @ts-ignore
// The value of the data item is a string.
settings.setValue(helper, settings.display.SCREEN_BRIGHTNESS_STATUS, '100', (status) => {
    console.log('Callback return whether value is set.');
});
```

## settings.setValue

setValue(dataAbilityHelper: DataAbilityHelper, name: string, value: object): Promise\<boolean>

Sets the value for a data item. This API uses a promise to return the result.

**System API**: This is a system API.

**System capability**: SystemCapability.Applications.settings.Core

**Parameters**

| Name           | Type                                             | Mandatory| Description                                                        |
| ----------------- | ------------------------------------------------- | ---- | ------------------------------------------------------------ |
| dataAbilityHelper | [DataAbilityHelper](js-apis-inner-ability-dataAbilityHelper.md) | Yes  | **DataAbilityHelper** class.                                            |
| name              | string                                            | Yes  | Name of the target data item. Data items can be classified as follows:<br>- Existing data items in the database<br>- Custom data items|
| value             | object                                            | Yes  | Value of the data item. The value range varies by service.                              |

**Return value**

| Type             | Description                                              |
| ----------------- | -------------------------------------------------- |
| Promise\<boolean> | Promise used to return the result. Returns **true** if the operation is successful; returns **false** otherwise.|

**Example**

```js
import featureAbility from '@ohos.ability.featureAbility';

// Update the value of SCREEN_BRIGHTNESS_STATUS. (As this data item exists in the database, the setValue API will update its value.)
let uri = settings.getUriSync(settings.display.SCREEN_BRIGHTNESS_STATUS);
let helper = featureAbility.acquireDataAbilityHelper(uri);
// @ts-ignore
// The value of the data item is a string.
settings.setValue(helper, settings.display.SCREEN_BRIGHTNESS_STATUS, '100').then((status) => {
    console.log('Callback return whether value is set.');
});
```

## settings.enableAirplaneMode

enableAirplaneMode(enable: boolean, callback: AsyncCallback\<void>): void

Enables or disables airplane mode. This API uses an asynchronous callback to return the result.

This API is not supported currently.

**System capability**: SystemCapability.Applications.settings.Core

**Parameters**

| Name  | Type                | Mandatory| Description                                           |
| -------- | -------------------- | ---- | ----------------------------------------------- |
| enable   | boolean              | Yes  | Whether airplane mode is enabled. **true** means that airplane mode is enabled, and **false** means the opposite.|
| callback | AsyncCallback\<void> | Yes  | Callback used to return the result.                                     |

**Example**

```js
let isEnabled = true;
settings.enableAirplaneMode(isEnabled, (err) => {
    if (err) {
        console.log('Failed to enable AirplaneMode.');
        return;
    }
    console.log('Return true if enable.');
})
```

## settings.enableAirplaneMode

enableAirplaneMode(enable: boolean): Promise\<void>

Enables or disables airplane mode. This API uses a promise to return the result.

This API is not supported currently.

**System capability**: SystemCapability.Applications.settings.Core

**Parameters**

| Name| Type   | Mandatory| Description                                           |
| ------ | ------- | ---- | ----------------------------------------------- |
| enable | boolean | Yes  | Whether airplane mode is enabled. **true** means that airplane mode is enabled, and **false** means the opposite.|

**Return value**

| Type          | Description                     |
| -------------- | ------------------------- |
| Promise\<void> | Promise that returns no value.|

**Example**

```js
let isEnabled = true;
settings.enableAirplaneMode(isEnabled).then(() => {
  console.log('Succeeded in enabling AirplaneMode.');
}).catch((err) => {
  console.log(`Failed to enable AirplaneMode. Cause: ${err}`);
})
```

## settings.canShowFloating

canShowFloating(callback: AsyncCallback\<boolean>): void

Checks whether the application can be displayed in a floating window. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Applications.settings.Core

**Parameters**

| Name  | Type                   | Mandatory| Description                                                        |
| -------- | ----------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback\<boolean> | Yes  | Callback used to return the result.<br>Returns **true** if the application can be displayed in a floating window; returns **false** otherwise.|

**Example**

```js
settings.canShowFloating((status) => {
    console.log('Checks whether a specified application can show as float window.');
});
```

## settings.canShowFloating

canShowFloating(): Promise\<boolean>

Checks whether the application can be displayed in a floating window. This API uses a promise to return the result.

**System capability**: SystemCapability.Applications.settings.Core

**Return value**

| Type             | Description                                                        |
| ----------------- | ------------------------------------------------------------ |
| Promise\<boolean> | Promise used to return the result.<br>Returns **true** if the application can be displayed in a floating window; returns **false** otherwise.|

**Example**

```js
settings.canShowFloating().then((status) => {
    console.log('Checks whether a specified application can show as float window.');
});
```

## settings.getUriSync<sup>8+</sup>

getUriSync(name: string): string

Obtains the URI of a data item.

**System capability**: SystemCapability.Applications.settings.Core

**Parameters**

| Name| Type  | Mandatory| Description                                                        |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| name   | string | Yes  | Name of the target data item. Data items can be classified as follows:<br>- Existing data items in the database<br>- Custom data items|

**Return value**

| Type  | Description         |
| ------ | ------------- |
| string | URI of the data item.|

**Example**

```js
// Obtain the URI of a data item.
let urivar = settings.getUriSync(settings.display.SCREEN_BRIGHTNESS_STATUS);
```

## setting.getURI<sup>(deprecated)</sup>

getURI(name: string, callback: AsyncCallback\<object>): void

Obtains the URI of a data item. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9.

**System capability**: SystemCapability.Applications.settings.Core

**Parameters**

| Name  | Type                  | Mandatory| Description                                                        |
| -------- | ---------------------- | ---- | ------------------------------------------------------------ |
| name     | string                 | Yes  | Name of the target data item. Data items can be classified as follows:<br>- Existing data items in the database<br>- Custom data items|
| callback | AsyncCallback\<object> | Yes  | Callback used to obtain the URI of the data item.                                 |

**Example**

```js
settings.getURI(settings.display.SCREEN_BRIGHTNESS_STATUS, (uri) => {
    console.log(`callback:uri -> ${JSON.stringify(uri)}`)
})
```

## setting.getURI<sup>(deprecated)</sup>

getURI(name: string): Promise\<object>

Obtains the URI of a data item. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9.

**System capability**: SystemCapability.Applications.settings.Core

**Parameters**

| Name| Type  | Mandatory| Description                                                        |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| name   | string | Yes  | Name of the target data item. Data items can be classified as follows:<br>- Existing data items in the database<br>- Custom data items|

**Return value**

| Type            | Description                                |
| ---------------- | ------------------------------------ |
| Promise\<object> | Promise used to return the URI of the data item.|

**Example**

```js
settings.getURI(settings.display.SCREEN_BRIGHTNESS_STATUS).then((uri) => {
    console.log(`promise:uri -> ${JSON.stringify(uri)}`)
})
```

## setting.getValue<sup>(deprecated)</sup>

getValue(dataAbilityHelper: DataAbilityHelper, name: string, callback: AsyncCallback\<object>): void

Obtains the value of a data item in the database. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9.

**Model restriction**: This API can be used only in the FA model.

**System capability**: SystemCapability.Applications.settings.Core

**Parameters**

| Name           | Type                                             | Mandatory| Description                                                        |
| ----------------- | ------------------------------------------------- | ---- | ------------------------------------------------------------ |
| dataAbilityHelper | [DataAbilityHelper](js-apis-inner-ability-dataAbilityHelper.md) | Yes  | **DataAbilityHelper** class.                                            |
| name              | string                                            | Yes  | Name of the target data item. Data items can be classified as follows:<br> - Existing data items in the database<br>- Custom data items|
| callback          | AsyncCallback\<object>                            | Yes  | Callback used to return the value of the data item.                            |

**Example**

```js
import featureAbility from '@ohos.ability.featureAbility';

let uri = settings.getUriSync(settings.display.SCREEN_BRIGHTNESS_STATUS);
let helper = featureAbility.acquireDataAbilityHelper(uri);
settings.getValue(helper, settings.display.SCREEN_BRIGHTNESS_STATUS, (err, value) => {
    if (err) {
        console.error(`Failed to get the setting. ${err.message} `);
        return;
    }
    console.log(`callback:value -> ${JSON.stringify(value)}`)
});
```

## setting.getValue<sup>(deprecated)</sup>

getValue(dataAbilityHelper: DataAbilityHelper, name: string): Promise\<object>

Obtains the value of a data item in the database. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9.

**Model restriction**: This API can be used only in the FA model.

**System capability**: SystemCapability.Applications.settings.Core

**Parameters**

| Name           | Type                                             | Mandatory| Description                                                        |
| ----------------- | ------------------------------------------------- | ---- | ------------------------------------------------------------ |
| dataAbilityHelper | [DataAbilityHelper](js-apis-inner-ability-dataAbilityHelper.md) | Yes  | **DataAbilityHelper** class.                                            |
| name              | string                                            | Yes  | Name of the target data item. Data items can be classified as follows:<br> - Existing data items in the database<br>- Custom data items|

**Return value**

| Type            | Description                               |
| ---------------- | ----------------------------------- |
| Promise\<object> | Promise used to return the value of the data item.|

**Example**

```js
import featureAbility from '@ohos.ability.featureAbility';

let uri = settings.getUriSync(settings.display.SCREEN_BRIGHTNESS_STATUS);
let helper = featureAbility.acquireDataAbilityHelper(uri);
settings.getValue(helper, settings.display.SCREEN_BRIGHTNESS_STATUS).then((value) => {
    console.log(`promise:value -> ${JSON.stringify(value)}`)
});
```

## settings.getValueSync<sup>(deprecated)</sup>

getValueSync(dataAbilityHelper: DataAbilityHelper, name: string, defValue: string): string

Obtains the value of a data item. Unlike **getValue**, this API returns the result synchronously.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9.

**Model restriction**: This API can be used only in the FA model.

**System capability**: SystemCapability.Applications.settings.Core

**Parameters**

| Name           | Type                                             | Mandatory| Description                                                        |
| ----------------- | ------------------------------------------------- | ---- | ------------------------------------------------------------ |
| dataAbilityHelper | [DataAbilityHelper](js-apis-inner-ability-dataAbilityHelper.md) | Yes  | **DataAbilityHelper** class.                                            |
| name              | string                                            | Yes  | Name of the target data item. Data items can be classified as follows:<br>- Existing data items in the database<br>- Custom data items|
| defValue          | string                                            | Yes  | Default value, which is returned when the value of a data item is not found in the database. Set this parameter as needed.|

**Return value**

| Type  | Description            |
| ------ | ---------------- |
| string | Value of the data item.|

**Example**

```js
import featureAbility from '@ohos.ability.featureAbility';

// Obtain the value of SCREEN_BRIGHTNESS_STATUS (this data item already exists in the database).
let uri = settings.getUriSync(settings.display.SCREEN_BRIGHTNESS_STATUS);
let helper = featureAbility.acquireDataAbilityHelper(uri);
let value = settings.getValueSync(helper, settings.display.SCREEN_BRIGHTNESS_STATUS, '10');
```

## settings.setValueSync<sup>(deprecated)</sup>

setValueSync(dataAbilityHelper: DataAbilityHelper, name: string, value: string): boolean

Sets the value for a data item. Unlike **setValue**, this API returns the result synchronously.

If the specified data item exists in the database, the **setValueSync** method updates the value of the data item. If the data item does not exist in the database, the **setValueSync** method inserts the data item into the database.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9.

**Model restriction**: This API can be used only in the FA model.

**Required permissions**: ohos.permission.MANAGE_SECURE_SETTINGS (available only to system applications)

**System capability**: SystemCapability.Applications.settings.Core

**Parameters**

| Name           | Type                                             | Mandatory| Description                                                        |
| ----------------- | ------------------------------------------------- | ---- | ------------------------------------------------------------ |
| dataAbilityHelper | [DataAbilityHelper](js-apis-inner-ability-dataAbilityHelper.md) | Yes  | **DataAbilityHelper** class.                                            |
| name              | string                                            | Yes  | Name of the target data item. Data items can be classified as follows:<br>- Existing data items in the database<br>- Custom data items|
| value             | string                                            | Yes  | Value of the data item. The value range varies by service.                      |

**Return value**

| Type   | Description                                                        |
| ------- | ------------------------------------------------------------ |
| boolean | Result indicating whether the value is set successfully. Returns **true** if the value is set successfully; returns **false** otherwise.|

**Example**

```js
import featureAbility from '@ohos.ability.featureAbility';

// Update the value of SCREEN_BRIGHTNESS_STATUS. (As this data item exists in the database, the setValueSync API will update the value of the data item.)
let uri = settings.getUriSync(settings.display.SCREEN_BRIGHTNESS_STATUS);
let helper = featureAbility.acquireDataAbilityHelper(uri);
let ret = settings.setValueSync(helper, settings.display.SCREEN_BRIGHTNESS_STATUS, '100');
```
