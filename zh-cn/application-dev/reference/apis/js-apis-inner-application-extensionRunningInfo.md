# ExtensionRunningInfo

ExtensionRunningInfo模块提供对Extension运行的相关信息和类型进行设置和查询的能力，可以通过[getExtensionRunningInfos](js-apis-app-ability-abilityManager.md#getextensionrunninginfos)获取。

> **说明：**
> 
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> 本模块接口均为系统接口，三方应用不支持调用

## 导入模块

```ts
import abilityManager from '@ohos.app.ability.abilityManager';
```

## 使用说明

通过abilityManager中方法获取。

## 属性

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

| 名称 | 类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| extension | ElementName | 是 | 否 | Extension匹配信息。 |
| pid | number | 是 | 否 | 进程ID。 |
| uid | number | 是 | 否 | 用户ID。 |
| processName | string | 是 | 否 | 进程名称。 |
| startTime | number | 是 | 否 | Extension启动时间。 |
| clientPackage | Array&lt;String&gt; | 是 | 否 | 表示当期进程下的所有包名。 |
| type | [bundle.ExtensionAbilityType](js-apis-Bundle.md) | 是 | 否 | Extension类型。 |

**示例：**
```ts
import abilityManager from '@ohos.application.abilityManager';
let upperLimit = 1;
abilityManager.getExtensionRunningInfos(upperLimit, (err,data) => {
    console.log('getExtensionRunningInfos err: '  + err + ' data: ' + JSON.stringify(data));
    for (let i = 0; i < data.length; i++) {
        let extensionRunningInfo = data[i];
        console.log('extensionRunningInfo.extension: ' + JSON.stringify(extensionRunningInfo.extension));
        console.log('extensionRunningInfo.pid: ' + JSON.stringify(extensionRunningInfo.pid));
        console.log('extensionRunningInfo.uid: ' + JSON.stringify(extensionRunningInfo.uid));
        console.log('extensionRunningInfo.processName: ' + JSON.stringify(extensionRunningInfo.processName));
        console.log('extensionRunningInfo.startTime: ' + JSON.stringify(extensionRunningInfo.startTime));
        console.log('extensionRunningInfo.clientPackage: ' + JSON.stringify(extensionRunningInfo.clientPackage));
        console.log('extensionRunningInfo.type: ' + JSON.stringify(extensionRunningInfo.type));
    }
});
```