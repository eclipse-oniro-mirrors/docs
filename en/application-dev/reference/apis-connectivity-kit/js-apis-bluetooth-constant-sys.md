# @ohos.bluetooth.constant (Bluetooth Constant Module) (System API)

The **constant** module provides definitions of the constants used in Bluetooth.

> **NOTE**
>
> - The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> - This topic describes only the system APIs provided by the module. For details about its public APIs, see [@ohos.bluetooth.constant (Bluetooth Constant Module)](js-apis-bluetooth-constant.md).

## Modules to Import

```js
import constant from '@ohos.bluetooth.constant';
```

## ProfileUuids

Enumerates profile UUIDs.

**System API**: This is a system API.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name                                  | Value   | Description             |
| ------------------------------------| ------ | --------------- |
| PROFILE_UUID_HFP_AG      | '0000111F-0000-1000-8000-00805F9B34FB' | UUID of the HFPAG Profile.<br>This is a system API.|
| PROFILE_UUID_HFP_HF      | '0000111E-0000-1000-8000-00805F9B34FB' | UUID of the HFPHF Profile.<br>This is a system API. |
| PROFILE_UUID_HSP_AG      | '00001112-0000-1000-8000-00805F9B34FB' | UUID of the HSPAG Profile.<br>This is a system API. |
| PROFILE_UUID_HSP_HS      | '00001108-0000-1000-8000-00805F9B34FB' | UUID of the HSPHS Profile.<br>This is a system API. |
| PROFILE_UUID_A2DP_SRC    | '0000110A-0000-1000-8000-00805F9B34FB' | Indicates the UID of the A2DPSRC Profile.<br>This is a system API. |
| PROFILE_UUID_A2DP_SINK   | '0000110B-0000-1000-8000-00805F9B34FB' | UUID of the A2DPSINK Profile.<br>This is a system API. |
| PROFILE_UUID_AVRCP_CT    | '0000110E-0000-1000-8000-00805F9B34FB' | UUID of the AVRCPCT Profile.<br>This is a system API. |
| PROFILE_UUID_AVRCP_TG    | '0000110C-0000-1000-8000-00805F9B34FB' | UUID of the AVRCPTG Profile.<br>This is a system API. |
| PROFILE_UUID_HID         | '00001124-0000-1000-8000-00805F9B34FB' | UUID of the HID Profile.<br>This is a system API. |
| PROFILE_UUID_HOGP        | '00001812-0000-1000-8000-00805F9B34FB' | UUID of the HOGP Profile.<br>This is a system API. |


## AccessAuthorization<sup>11+</sup>

Enumerates the access permissions.

**System API**: This is a system API.

**System capability**: SystemCapability.Communication.Bluetooth.Core

| Name                | Value | Description    |
| ------------------ | ---- | ------ |
| UNKNOWN<sup>11+</sup> | 0    | Unknown.<br>This is a system API. |
| ALLOWED<sup>11+</sup> | 1    | Access allowed.<br>This is a system API. |
| REJECTED<sup>11+</sup> | 2    | Access rejected.<br>This is a system API.|
