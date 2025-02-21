# @ohos.bluetooth.pbap (蓝牙pbap模块)

pbap模块提供了访问电话簿相关功能的方法。

> **说明：**
>
> 本模块首批接口从API version 11开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。



## 导入模块

```js
import pbap from '@ohos.bluetooth.pbap';
```


## pbap.createPbapServerProfile

createPbapServerProfile(): PbapServerProfile

创建pbapServer profile实例。

**系统能力**：SystemCapability.Communication.Bluetooth.Core。

**返回值：**

| 类型                            | 说明         |
| ----------------------------- | ---------- |
| PbapServerProfile | 返回该profile的实例。 |

**示例：**

```js
import { BusinessError } from '@ohos.base';
try {
    let pbapServerProfile = pbap.createPbapServerProfile();
    console.info('pbapServer success');
} catch (err) {
    console.error('errCode: ' + (err as BusinessError).code + ', errMessage: ' + (err as BusinessError).message);
}
```
