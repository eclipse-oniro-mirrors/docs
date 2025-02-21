# @ohos.bluetooth.pan (蓝牙pan模块)

pan模块提供了访问蓝牙个人区域网相关功能的方法。

> **说明：**
>
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。



## 导入模块

```js
import pan from '@ohos.bluetooth.pan';
```


## pan.createPanProfile

createPanProfile(): PanProfile

创建pan profile实例。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**返回值：**

| 类型                            | 说明         |
| ----------------------------- | ---------- |
| PanProfile | 返回该profile的实例。 |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let panProfile : pan.PanProfile= pan.createPanProfile();
    console.info('pan success');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```
