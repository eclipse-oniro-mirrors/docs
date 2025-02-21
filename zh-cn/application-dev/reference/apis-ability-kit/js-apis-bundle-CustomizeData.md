# CustomizeData

> **说明：**
> 本模块首批接口从API version 7 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

自定义元数据。

## CustomizeData<sup>(deprecated)</sup>

> 从API version 9开始不再维护，建议使用[Metadata](js-apis-bundleManager-metadata.md)替代。

**系统能力**:  以下各项对应的系统能力均为SystemCapability.BundleManager.BundleFramework



| 名称               | 类型   | 可读 | 可写 | 说明             |
| ------------------ | ------ | ---- | ---- | ---------------- |
| name               | string | 是   | 是   | 标识自定义数据项的键名称。 |
| value              | string | 是   | 是   | 标识自定义数据项的值名称。   |
| extra<sup>8+</sup> | string | 是   | 是   | 标识用户自定义数据格式，标签值为标识该数据的资源的索引值。       |