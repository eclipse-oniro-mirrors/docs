# @ohos.bluetooth.constant (蓝牙constant模块)（系统接口）

constant模块提供了蓝牙中常量的定义。

> **说明：**
>
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> 当前页面仅包含本模块的系统接口，其他公开接口参见[@ohos.bluetooth.constant (蓝牙constant模块)](js-apis-bluetooth-constant.md)

## 导入模块

```js
import constant from '@ohos.bluetooth.constant';
```

## ProfileUuids

枚举，表示Profile的UUID。

**系统接口：** 此接口为系统接口。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称                                   | 值    | 说明              |
| ------------------------------------| ------ | --------------- |
| PROFILE_UUID_HFP_AG      | '0000111F-0000-1000-8000-00805F9B34FB' | 代表HFPAG Profile的UUID。<br/>此接口为系统接口。 |
| PROFILE_UUID_HFP_HF      | '0000111E-0000-1000-8000-00805F9B34FB' | 代表HFPHF Profile的UUID。<br/>此接口为系统接口。  |
| PROFILE_UUID_HSP_AG      | '00001112-0000-1000-8000-00805F9B34FB' | 代表HSPAG Profile的UUID。<br/>此接口为系统接口。  |
| PROFILE_UUID_HSP_HS      | '00001108-0000-1000-8000-00805F9B34FB' | 代表HSPHS Profile的UUID。<br/>此接口为系统接口。  |
| PROFILE_UUID_A2DP_SRC    | '0000110A-0000-1000-8000-00805F9B34FB' | 代表A2DPSRC Profile的UUID。<br/>此接口为系统接口。  |
| PROFILE_UUID_A2DP_SINK   | '0000110B-0000-1000-8000-00805F9B34FB' | 代表A2DPSINK Profile的UUID。<br/>此接口为系统接口。  |
| PROFILE_UUID_AVRCP_CT    | '0000110E-0000-1000-8000-00805F9B34FB' | 代表AVRCPCT Profile的UUID。<br/>此接口为系统接口。  |
| PROFILE_UUID_AVRCP_TG    | '0000110C-0000-1000-8000-00805F9B34FB' | 代表AVRCPTG Profile的UUID。<br/>此接口为系统接口。  |
| PROFILE_UUID_HID         | '00001124-0000-1000-8000-00805F9B34FB' | 代表HID Profile的UUID。<br/>此接口为系统接口。  |
| PROFILE_UUID_HOGP        | '00001812-0000-1000-8000-00805F9B34FB' | 代表HOGP Profile的UUID。<br/>此接口为系统接口。  |


## AccessAuthorization<sup>11+</sup>

枚举，访问权限。

**系统接口：** 此接口为系统接口。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

| 名称                 | 值  | 说明     |
| ------------------ | ---- | ------ |
| UNKNOWN<sup>11+</sup> | 0    | 未知。<br/>此接口为系统接口。  |
| ALLOWED<sup>11+</sup> | 1    | 允许。<br/>此接口为系统接口。  |
| REJECTED<sup>11+</sup> | 2    | 拒绝。<br/>此接口为系统接口。 |