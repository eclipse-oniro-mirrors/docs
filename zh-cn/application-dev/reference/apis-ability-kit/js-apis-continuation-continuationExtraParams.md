# ContinuationExtraParams

流转管理入口中设备选择模块所需的过滤参数，可以作为[startContinuationDeviceManager](js-apis-continuation-continuationManager.md#continuationmanagerstartcontinuationdevicemanager9-1)的入参。

> **说明：**
> 
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## ContinuationExtraParams

表示流转管理入口中设备选择模块所需的过滤参数。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.DistributedAbilityManager

| 名称 | 类型 | 只读 | 必填 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| deviceType | Array\<string> | 否 | 否 | 表示设备类型。|
| targetBundle | string | 否 | 否 | 表示目标Bundle名称。 |
| description | string | 否 | 否 | 表示设备过滤的描述。 |
| filter | any | 否 | 否 | 表示设备过滤的参数。 |
| continuationMode | [ContinuationMode](js-apis-continuation-continuationManager.md#continuationmode) | 否 | 否 | 表示协同的模式。 |
| authInfo | Record<string, Object> | 否 | 否 | 表示认证的信息。 |