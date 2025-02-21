# IThermalCallback


## **概述**

订阅设备发热状态的回调。

服务创建此回调对象后，可以调用[IThermalInterface](interface_i_thermal_interface.md)的接口注册回调，从而订阅设备发热状态的变化。

**Since:**

3.1

**相关模块:**

[Thermal](thermal.md)


## **汇总**


### Public 成员函数

  | 名称 | 描述 | 
| -------- | -------- |
| [OnThermalDataEvent](#onthermaldataevent)&nbsp;([in]&nbsp;struct&nbsp;[HdfThermalCallbackInfo](_hdf_thermal_callback_info.md)&nbsp;event) | 设备发热状态变化的回调方法。 | 


## **成员函数说明**


### OnThermalDataEvent()

  
```
IThermalCallback::OnThermalDataEvent ([in] struct HdfThermalCallbackInfo event)
```

**描述：**

设备发热状态变化的回调方法。

当设备发热状态发生变化时，将通过此方法的参数返回给服务。

**参数:**

  | 名称 | 描述 | 
| -------- | -------- |
| event | 设备发热信息，包括器件类型、器件温度。 | 

**参见:**

[HdfThermalCallbackInfo](_hdf_thermal_callback_info.md)
