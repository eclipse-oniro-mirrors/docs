# ElementName

> **说明：**
> 本模块首批接口从API version 9 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

ElementName信息，通过接口[Context.getElementName](js-apis-inner-app-context.md#contextgetelementname7)获取。
## ElementName

 **系统能力:** SystemCapability.BundleManager.BundleFramework.Core

| 名称                     | 类型     | 可读 | 可写 | 说明                       |
| ----------------------- | ---------| ---- | ---- | ------------------------- |
| deviceId                | string   | 是   | 是   | 设备ID。                   |
| bundleName              | string   | 是   | 是   | 应用Bundle名称。          |
| abilityName             | string   | 是   | 是   | Ability名称。               |
| uri                     | string   | 是   | 是   | 资源标识符。                 |
| shortName               | string   | 是   | 是   | Ability短名称。               |
| moduleName              | string   | 是   | 是   | Ability所属的HAP的模块名称。   |