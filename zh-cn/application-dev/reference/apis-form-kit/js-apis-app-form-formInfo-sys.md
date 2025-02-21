# @ohos.app.form.formInfo (formInfo)(系统接口)

formInfo模块提供了卡片信息和状态等相关类型和枚举。

> **说明：**
>
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> 当前页面仅包含本模块的系统接口，其他公共接口参见[@ohos.app.form.formInfo (formInfo)](./js-apis-app-form-formInfo.md)。

## 导入模块

```ts
import formInfo from '@ohos.app.form.formInfo';
```


##  FormParam

卡片参数枚举。

**系统能力**：SystemCapability.Ability.Form

| 名称        | 值   | 说明         |
| ----------- | ---- | ------------ |
| DEVICE_ID_KEY    | 'ohos.extra.param.key.device_id'   | 设备标识。 <br>**系统接口**: 此接口为系统接口。  |


## FormUsageState

卡片当前使用状态枚举。

**系统能力**：SystemCapability.Ability.Form

**系统接口**: 此接口为系统接口。

| 名称        |  值   | 说明         |
| ----------- | ---- | ------------ |
| USED<sup>11+</sup> | 0   | 表示卡片在使用中。 |
| UNUSED<sup>11+</sup> | 1   | 表示卡片未被使用。 |

## RunningFormInfo<sup>10+</sup>

已添加的卡片信息，包括使用中的以及未使用的卡片。

**系统能力**：SystemCapability.Ability.Form

**系统接口**: 此接口为系统接口。

| 名称        | 类型                 | 可读    | 可写    | 说明                                                         |
| ----------- | -------- | -------- | -------------------- | ------------------------------------------------------------ |
| formId  | string               | 是    | 否     | 卡片标识。                   |
| bundleName<sup>10+</sup>  | string               | 是    | 否     | 提供方卡片所属包的Bundle名称。                   |
| hostBundleName  | string               | 是    | 否     | 使用方卡片所属包的Bundle名称。                   |
| visibilityType  | [VisibilityType](js-apis-app-form-formInfo.md#visibilitytype)               | 是    | 否     | 卡片当前可见类型枚举。                   |
| moduleName<sup>10+</sup>  | string               | 是    | 否     | 卡片所属模块的模块名称。                      |
| abilityName<sup>10+</sup> | string               | 是    | 否     | 卡片所属的Ability名称。                       |
| formName<sup>10+</sup>        | string               | 是    | 否     | 卡片名称。                                 |
| dimension | number               | 是    | 否     | 卡片规格。   |
| formUsageState<sup>11+</sup> | [FormUsageState](#formusagestate)         | 是    | 否     | 卡片当前使用状态枚举。   |
| formDescription<sup>11+</sup> | string         | 是    | 否     | 提供方卡片配置文件中的描述信息。   |

## formProviderFilter<sup>10+</sup>

卡片提供方信息。

**模型约束**：此接口仅可在Stage模型下使用。

**系统能力**：SystemCapability.Ability.Form

**系统接口**: 此接口为系统接口。

| 名称        | 类型                 | 可读    | 可写    | 说明                                                         |
| ----------- | -------- | -------- | -------------------- | ------------------------------------------------------------ |
| bundleName  | string               | 是    | 否     | 提供方卡片所属包的Bundle名称。  |
| formName    | string               | 是    | 否     | 卡片名称。                     |
| moduleName  | string               | 是    | 否     | 卡片所属模块的模块名称。        |
| abilityName | string               | 是    | 否     | 卡片所属的Ability名称。        |
| isUnusedIncluded<sup>11+</sup> | boolean               | 是    | 否     | 是否包含未使用的卡片。        |


