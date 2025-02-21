# RemoteAbilityInfo
> ![icon-note.gif](public_sys-resources/icon-note.gif)
> **说明：**
> 本模块首批接口从API version 9 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

包含远程的ability信息，通过接口[distributedBundle.getRemoteAbilityInfo](js-apis-distributedBundleManager.md)获取。

## RemoteAbilityInfo

 **系统能力:** SystemCapability.BundleManager.DistributedBundleFramework

 **系统接口：**  此接口为系统接口。

| 名称        | 类型                                         | 可读 | 可写 | 说明                    |
| ----------- | -------------------------------------------- | ---- | ---- | ----------------------- |
| elementName | [ElementName](js-apis-bundleManager-elementName.md) | 是   | 否   | 指明远程ability的ElementName信息。       |
| label       | string                                       | 是   | 否   | 指明远程ability的标签信息。   |
| icon        | string                                       | 是   | 否   | 指明的远程ability的图标信息。 |
