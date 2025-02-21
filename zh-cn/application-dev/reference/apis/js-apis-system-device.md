# @system.device (设备信息)

本模块提供当前设备的信息。

> **说明：**
> - 从API Version 6开始，该接口不再维护，推荐使用新接口[`@ohos.deviceInfo`](js-apis-device-info.md)进行设备信息查询。
> 
> - 本模块首批接口从API version 3开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```
import device from '@system.device';
```

## device.getInfo

getInfo(options?: GetDeviceOptions): void

获取当前设备的信息。

> **说明：**<br>
> 在首页的onShow生命周期之前不建议调用device.getInfo接口。

**系统能力：** SystemCapability.Startup.SystemInfo

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| options | [GetDeviceOptions](#getdeviceoptions) | 否 | 定义设备信息获取的参数选项。 |

## GetDeviceOptions

定义设备信息获取的参数选项。

**系统能力：** SystemCapability.Startup.SystemInfo

| 名称 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| success | (data：DeviceResponse）=> void | 否 | 接口调用成功的回调函数。 data为成功返回的设备信息，具体参考[DeviceResponse](#deviceresponse)。|
| fail | (data：any,code:number）=> void | 否 | 接口调用失败的回调函数。 code为失败返回的错误码。<br>code:200，表示返回结果中存在无法获得的信息。|
| complete | （）=> void | 否 | 接口调用结束的回调函数。 |

## DeviceResponse

设备信息。

**系统能力：** SystemCapability.Startup.SystemInfo

| 名称 | 类型 | 说明 |
| -------- | -------- | -------- |
| brand | string | 品牌。 |
| manufacturer | string | 生产商。 |
| model | string | 型号。 |
| product | string | 代号。 |
| language<sup>4+</sup> | string | 系统语言。 |
| region<sup>4+</sup> | string | 系统地区。 |
| windowWidth | number | 可使用的窗口宽度。 |
| windowHeight | number | 可使用的窗口高度。 |
| screenDensity<sup>4+</sup> | number | 屏幕密度。 |
| screenShape<sup>4+</sup> | string | 屏幕形状。可取值：<br/>-&nbsp;rect：方形屏；<br/>-&nbsp;circle：圆形屏。 |
| apiVersion<sup>4+</sup> | number | 系统API版本号。 |
| deviceType<sup>4+</sup> | string | 设备类型。 |


**示例：**

```
export default {    
  getInfo() {        
    device.getInfo({            
      success: function(data) {                
        console.log('Device information obtained successfully. Device brand:' + data.brand);            
      },            
      fail: function(data, code) {                
        console.log('Failed to obtain device information. Error code:'+ code + '; Error information: ' + data);            
      },        
    });    
  },
}
```