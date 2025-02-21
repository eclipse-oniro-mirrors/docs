# AppProvisionInfo (系统接口)

应用[HarmonyAppProvision配置文件](../../security/app-provision-structure.md)中的信息，可以通过[getAppProvisionInfo](js-apis-bundleManager.md#bundlemanagergetappprovisioninfo10)获取。

> **说明：**
>
> 本模块首批接口从API version 10 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>
> 本模块为系统接口。

## AppProvisionInfo

**系统能力:** SystemCapability.BundleManager.BundleFramework.Core

**系统接口：**  此接口为系统接口。

| 名称                      | 类型   | 可读 | 可写 | 说明                 |
| ------------------------- | ------ | ---- | ---- | -------------------- |
| versionCode              | number | 是   | 否   | 配置文件的版本号。 |
| versionName              | string | 是   | 否   | 配置文件的版本名称。  |
| uuid                     | string | 是   | 否   | 配置文件中的uuid。 |
| type                     | string | 是   | 否   | 配置文件的类型，为debug或者release。 |
| appDistributionType      | string | 是   | 否   | 配置文件中的分发类型，为app_gallery、enterprise、os_integration和crowdtesting其中之一。 |
| validity                 | [Validity](#validity) | 是   | 否   | 配置文件中的有效期。 |
| developerId              | string | 是   | 否   | 配置文件中的开发者ID。 |
| certificate              | string | 是   | 否   | 配置文件中的证书公钥。 |
| apl                      | string | 是   | 否   | 配置文件中的apl字段，为normal、system_basic和system_core其中之一。 |
| issuer                      | string | 是   | 否   | 配置文件中的发行者名称。 |
|appIdentifier<sup>11+</sup>| string         | 是   | 否   | 应用的唯一标识，由云端统一分配。该ID在应用全生命周期中不会发生变化，包括版本升级、证书变更、开发者公私钥变更、应用转移等。            |

## Validity

**系统能力:** SystemCapability.BundleManager.BundleFramework.Core

**系统接口：**  此接口为系统接口。

| 名称                      | 类型   | 可读 | 可写 | 说明                 |
| ------------------------- | ------ | ---- | ---- | -------------------- |
| notBefore                 | number | 是   | 否   | 配置文件的最早有效日期。 |
| notAfter                  | number | 是   | 否   | 配置文件的最晚有效日期。 |