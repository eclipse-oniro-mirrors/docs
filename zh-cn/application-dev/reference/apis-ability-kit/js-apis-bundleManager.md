# @ohos.bundle.bundleManager (bundleManager模块)

本模块提供应用信息查询能力，支持BundleInfo、ApplicationInfo、Ability、ExtensionAbility等信息的查询。

> **说明：**
> 本模块首批接口从API version 9 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import bundleManager from '@ohos.bundle.bundleManager';
```

## 枚举

### BundleFlag

包信息标志，指示需要获取的包信息的内容。

 **系统能力：** SystemCapability.BundleManager.BundleFramework.Core。

| 名称                                      | 值         | 说明                                                         |
| ----------------------------------------- | ---------- | ------------------------------------------------------------ |
| GET_BUNDLE_INFO_DEFAULT                   | 0x00000000 | 用于获取默认bundleInfo，获取的bundleInfo不包含signatureInfo、applicationInfo、hapModuleInfo、ability、extensionAbility和permission的信息。 |
| GET_BUNDLE_INFO_WITH_APPLICATION          | 0x00000001 | 用于获取包含applicationInfo的bundleInfo，获取的bundleInfo不包含signatureInfo、hapModuleInfo、ability、extensionAbility和permission的信息。 |
| GET_BUNDLE_INFO_WITH_HAP_MODULE           | 0x00000002 | 用于获取包含hapModuleInfo的bundleInfo，获取的bundleInfo不包含signatureInfo、applicationInfo、ability、extensionAbility和permission的信息。 |
| GET_BUNDLE_INFO_WITH_ABILITY              | 0x00000004 | 用于获取包含ability的bundleInfo，获取的bundleInfo不包含signatureInfo、applicationInfo、extensionAbility和permission的信息。它不能单独使用，需要与GET_BUNDLE_INFO_WITH_HAP_MODULE一起使用。 |
| GET_BUNDLE_INFO_WITH_EXTENSION_ABILITY    | 0x00000008 | 用于获取包含extensionAbility的bundleInfo，获取的bundleInfo不包含signatureInfo、applicationInfo、ability 和permission的信息。它不能单独使用，需要与GET_BUNDLE_INFO_WITH_HAP_MODULE一起使用。 |
| GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION | 0x00000010 | 用于获取包含permission的bundleInfo。获取的bundleInfo不包含signatureInfo、applicationInfo、hapModuleInfo、extensionAbility和ability的信息。 |
| GET_BUNDLE_INFO_WITH_METADATA             | 0x00000020 | 用于获取applicationInfo、moduleInfo和abilityInfo中包含的metadata。它不能单独使用，它需要与GET_BUNDLE_INFO_WITH_APPLICATION、GET_BUNDLE_INFO_WITH_HAP_MODULE、GET_BUNDLE_INFO_WITH_ABILITY、GET_BUNDLE_INFO_WITH_EXTENSION_ABILITY一起使用。 |
| GET_BUNDLE_INFO_WITH_DISABLE              | 0x00000040 | 用于获取application被禁用的BundleInfo和被禁用的Ability信息。获取的bundleInfo不包含signatureInfo、applicationInfo、hapModuleInfo、ability、extensionAbility和permission的信息。 |
| GET_BUNDLE_INFO_WITH_SIGNATURE_INFO       | 0x00000080 | 用于获取包含signatureInfo的bundleInfo。获取的bundleInfo不包含applicationInfo、hapModuleInfo、extensionAbility、ability和permission的信息。 |
| GET_BUNDLE_INFO_WITH_MENU<sup>11+</sup>   | 0x00000100 | 用于获取包含fileContextMenuConfig的bundleInfo。它不能单独使用，需要与GET_BUNDLE_INFO_WITH_HAP_MODULE一起使用。 |

### ExtensionAbilityType

指示扩展组件的类型。

 **系统能力：** SystemCapability.BundleManager.BundleFramework.Core。

| 名称 | 值 | 说明 |
|:----------------:|:---:|-----|
| FORM             | 0   | [FormExtensionAbility](../apis-form-kit/js-apis-app-form-formExtensionAbility.md)：卡片扩展能力，提供卡片开发能力。 |
| WORK_SCHEDULER   | 1   | [WorkSchedulerExtensionAbility](../apis-backgroundtasks-kit/js-apis-WorkSchedulerExtensionAbility.md)：延时任务扩展能力，允许应用在系统闲时执行实时性不高的任务。 |
| INPUT_METHOD     | 2   | [InputMethodExtensionAbility](../apis-ime-kit/js-apis-inputmethod-extension-ability.md)：输入法扩展能力，用于开发输入法应用。 |
| SERVICE          | 3   | [ServiceExtensionAbility](js-apis-app-ability-serviceExtensionAbility-sys.md)：后台服务扩展能力，提供后台运行并对外提供相应能力。 |
| ACCESSIBILITY    | 4   | [AccessibilityExtensionAbility](../apis-accessibility-kit/js-apis-application-accessibilityExtensionAbility.md)：无障碍服务扩展能力，支持访问与操作前台界面。 |
| DATA_SHARE       | 5   | [DataShareExtensionAbility](../apis-arkdata/js-apis-application-dataShareExtensionAbility-sys.md)：数据共享扩展能力，用于对外提供数据读写服务。 |
| FILE_SHARE       | 6   | FileShareExtensionAbility：文件共享扩展能力，用于应用间的文件分享。预留能力，当前暂未支持。 |
| STATIC_SUBSCRIBER| 7   | [StaticSubscriberExtensionAbility](../apis-basic-services-kit/js-apis-application-staticSubscriberExtensionAbility-sys.md)：静态广播扩展能力，用于处理静态事件，比如开机事件。 |
| WALLPAPER        | 8   | WallpaperExtensionAbility：壁纸扩展能力，用于实现桌面壁纸。预留能力，当前暂未支持。 |
| BACKUP           |  9  | [BackupExtensionAbility](../apis-core-file-kit/js-apis-application-backupExtensionAbility.md)：数据备份扩展能力，提供应用数据的备份恢复能力。 |
| WINDOW           |  10 | [WindowExtensionAbility](../apis-arkui/js-apis-application-windowExtensionAbility-sys.md)：界面组合扩展能力，允许系统应用进行跨应用的界面拉起和嵌入。 |
| ENTERPRISE_ADMIN |  11 | [EnterpriseAdminExtensionAbility](../apis-mdm-kit/js-apis-EnterpriseAdminExtensionAbility-sys.md)：企业设备管理扩展能力，提供企业管理时处理管理事件的能力，比如设备上应用安装事件、锁屏密码输入错误次数过多事件等。 |
| THUMBNAIL        | 13  | ThumbnailExtensionAbility：文件缩略图扩展能力，用于为文件提供图标缩略图的能力。预留能力，当前暂未支持。 |
| PREVIEW          | 14  | PreviewExtensionAbility：文件预览扩展能力，提供文件预览的能力，其他应用可以直接在应用中嵌入显示。预留能力，当前暂未支持。 |
| PRINT<sup>10+</sup> | 15 | PrintExtensionAbility：文件打印扩展能力，提供应用打印照片、文档等办公场景。当前支持图片打印，文档类型暂未支持。 |
| SHARE<sup>10+</sup> | 16 | [ShareExtensionAbility](js-apis-app-ability-shareExtensionAbility.md)：提供分享业务能力，为开发者提供基于UIExtension的分享业务模板。 |
| PUSH<sup>10+</sup> | 17 | PushExtensionAbility：推送扩展能力，提供推送场景化消息能力。预留能力，当前暂未支持。 |
| DRIVER<sup>10+</sup> | 18 | [DriverExtensionAbility](../apis-driverdevelopment-kit/js-apis-app-ability-driverExtensionAbility.md)：驱动扩展能力，提供外设驱动扩展能力，当前暂未支持。 |
| ACTION<sup>10+</sup> | 19 | [ActionExtensionAbility](js-apis-app-ability-actionExtensionAbility.md)：自定义服务扩展能力，为开发者提供基于UIExtension的自定义操作业务模板。 |
| ADS_SERVICE<sup>11+</sup> | 20 | AdsServiceExtensionAbility：广告服务扩展能力，对外提供后台自定义广告业务服务，当前暂未支持。 |
| UNSPECIFIED      | 255 | 不指定类型，配合queryExtensionAbilityInfo接口可以查询所有类型的ExtensionAbility。 |


### PermissionGrantState

指示权限授予状态。

 **系统能力：** SystemCapability.BundleManager.BundleFramework.Core。

| 名称 | 值 | 说明 |
|:----------------:|:---:|:---:|
| PERMISSION_DENIED|  -1 | 拒绝授予权限。 |
| PERMISSION_GRANTED |  0  |  授予权限。  |

### SupportWindowMode

标识该组件所支持的窗口模式。

 **系统能力：** SystemCapability.BundleManager.BundleFramework.Core。

| 名称 | 值 | 说明 |
|:----------------:|:---:|:---:|
| FULL_SCREEN      | 0   | 窗口支持全屏显示。 |
| SPLIT            | 1   | 窗口支持分屏显示。 |
| FLOATING         | 2   | 支持窗口化显示。   |

### LaunchType

指示组件的启动方式。

 **系统能力：** SystemCapability.BundleManager.BundleFramework.Core。

| 名称 | 值 | 说明 |
|:----------------:|:---:|:---:|
| SINGLETON        | 0   | ability的启动模式，表示单实例。 |
| MULTITON         | 1   | ability的启动模式，表示普通多实例。 |
| SPECIFIED        | 2   | ability的启动模式，表示该ability内部根据业务自己指定多实例。 |

### AbilityType

指示Ability组件的类型。

 **模型约束：** 仅可在FA模型下使用

 **系统能力：** SystemCapability.BundleManager.BundleFramework.Core。

|  名称   | 值   |                            说明                            |
| :-----: | ---- | :--------------------------------------------------------: |
| PAGE    | 1    | UI界面类型的Ability。表示基于Page模板开发的FA，用于提供与用户交互的能力。        |
| SERVICE | 2    | 后台服务类型的Ability，无UI界面。表示基于Service模板开发的PA，用于提供后台运行任务的能力。  |
|  DATA   | 3    | 表示基于Data模板开发的PA，用于对外部提供统一的数据访问对象。 |

### DisplayOrientation

标识该Ability的显示模式。该标签仅适用于page类型的Ability。

 **系统能力：** SystemCapability.BundleManager.BundleFramework.Core。

| 名称                               |值 |说明 |
|:----------------------------------|---|---|
| UNSPECIFIED                        |0 |表示未定义方向模式，由系统判定。 |
| LANDSCAPE                          |1 |表示横屏显示模式。 |
| PORTRAIT                           |2 |表示竖屏显示模式。 |
| FOLLOW_RECENT                      |3 |表示跟随上一个显示模式。 |
| LANDSCAPE_INVERTED                 |4 |表示反向横屏显示模式。 |
| PORTRAIT_INVERTED                  |5 |表示反向竖屏显示模式。 |
| AUTO_ROTATION                      |6 |表示传感器自动旋转模式。 |
| AUTO_ROTATION_LANDSCAPE            |7 |表示传感器自动横向旋转模式。 |
| AUTO_ROTATION_PORTRAIT             |8 |表示传感器自动竖向旋转模式。 |
| AUTO_ROTATION_RESTRICTED           |9 |表示受开关控制的自动旋转模式。 |
| AUTO_ROTATION_LANDSCAPE_RESTRICTED |10|表述受开关控制的自动横向旋转模式。|
| AUTO_ROTATION_PORTRAIT_RESTRICTED  |11|表示受开关控制的自动竖向旋转模式。|
| LOCKED                             |12|表示锁定模式。|

### CompatiblePolicy<sup>10+</sup>

标识共享库的版本兼容类型。

 **系统能力:** SystemCapability.BundleManager.BundleFramework.Core

| 名称                   | 值   | 说明                             |
| ---------------------- | ---- | -------------------------------- |
| BACKWARD_COMPATIBILITY | 1    | 该字段表明共享库是向后兼容类型。 |

### ModuleType

标识模块类型。

 **系统能力:** SystemCapability.BundleManager.BundleFramework.Core

| 名称    | 值   | 说明                 |
| ------- | ---- | -------------------- |
| ENTRY   | 1    | 应用的主模块。   |
| FEATURE | 2    | 应用的动态特性模块。 |
| SHARED  | 3    | 应用的动态共享库模块。  |

### BundleType

标识应用的类型。

 **系统能力:** SystemCapability.BundleManager.BundleFramework.Core

| 名称           | 值   | 说明            |
| -------------- | ---- | --------------- |
| APP            | 0    | 该Bundle是应用。    |
| ATOMIC_SERVICE | 1    | 该Bundle是元服务。 |

## 接口

### bundleManager.getBundleInfoForSelf

getBundleInfoForSelf(bundleFlags: number): Promise\<BundleInfo>

以异步方法根据给定的bundleFlags获取当前应用的BundleInfo，使用Promise形式返回结果。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名     | 类型   | 必填 | 说明                |
| ----------- | ------ | ---- | --------------------- |
| [bundleFlags](js-apis-bundleManager.md#bundleflag) | number | 是   | 指定返回的BundleInfo所包含的信息。 |

**返回值：**

| 类型                                                        | 说明                                  |
| ----------------------------------------------------------- | ------------------------------------- |
| Promise\<[BundleInfo](js-apis-bundleManager-bundleInfo.md)> | Promise对象，返回当前应用的BundleInfo。|

**示例：**

```ts
// 额外获取带有metadataArray信息的appInfo
import bundleManager from '@ohos.bundle.bundleManager';
import { BusinessError } from '@ohos.base';
import hilog from '@ohos.hilog';

let bundleFlags = bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_APPLICATION | bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_METADATA;

try {
  bundleManager.getBundleInfoForSelf(bundleFlags).then((data) => {
    hilog.info(0x0000, 'testTag', 'getBundleInfoForSelf successfully. Data: %{public}s', JSON.stringify(data));
  }).catch((err: BusinessError) => {
    hilog.error(0x0000, 'testTag', 'getBundleInfoForSelf failed. Cause: %{public}s', err.message);
  });
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'getBundleInfoForSelf failed: %{public}s', message);
}
```

### bundleManager.getBundleInfoForSelf

getBundleInfoForSelf(bundleFlags: number, callback: AsyncCallback\<BundleInfo>): void

以异步方法根据给定的bundleFlags获取当前应用的BundleInfo，使用callback形式返回结果。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名     | 类型   | 必填 | 说明                |
| ----------- | ------ | ---- | --------------------- |
| [bundleFlags](js-apis-bundleManager.md#bundleflag) | number | 是   | 指定返回的BundleInfo所包含的信息。 |
| callback | AsyncCallback\<[BundleInfo](js-apis-bundleManager-bundleInfo.md)> | 是 | 回调函数，当获取成功时，err为null，data为获取到的当前应用的BundleInfo；否则为错误对象。 |

**示例：**

```ts
// 额外获取带有permissions信息的abilitiesInfo
import bundleManager from '@ohos.bundle.bundleManager';
import { BusinessError } from '@ohos.base';
import hilog from '@ohos.hilog';

let bundleFlags = bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_HAP_MODULE | bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_ABILITY | bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION;

try {
  bundleManager.getBundleInfoForSelf(bundleFlags, (err, data) => {
    if (err) {
      hilog.error(0x0000, 'testTag', 'getBundleInfoForSelf failed: %{public}s', err.message);
    } else {
      hilog.info(0x0000, 'testTag', 'getBundleInfoForSelf successfully: %{public}s', JSON.stringify(data));
    }
  });
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'getBundleInfoForSelf failed: %{public}s', message);
}
```

### bundleManager.getProfileByAbility

getProfileByAbility(moduleName: string, abilityName: string, metadataName: string, callback: AsyncCallback\<Array\<string\>\>): void

以异步方法根据给定的moduleName、abilityName和metadataName（module.json中[metadata标签](../../quick-start/module-configuration-file.md#metadata标签)下的name）获取相应配置文件的json格式字符串，使用callback形式返回结果。

>如果配置文件信息采用了资源引用格式，则返回值将保持资源引用格式（例如 $string:res_id），开发者可以通过资源管理模块的相关接口，来获取引用的资源。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名       | 类型                          | 必填 | 说明                                                         |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| moduleName   | string                        | 是   | 表示Module名称。                                     |
| abilityName  | string                        | 是   | 表示UIAbility组件的名称。                                    |
| metadataName | string                        | 是   | 表示UIAbility组件的元信息名称，即module.json5配置文件中abilities标签下的metadata标签的name。                                  |
| callback     | AsyncCallback<Array\<string>> | 是   | 回调函数，当获取成功时，err为null，data为获取到的Array\<string>；否则为错误对象。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 17700002 | The specified moduleName is not existed.                      |
| 17700003 | The specified abilityName is not existed.                     |
| 17700024 | Failed to get the profile because there is no profile in the HAP. |
| 17700026 | The specified bundle is disabled.                             |
| 17700029 | The specified ability is disabled.                            |

**示例：**

```ts
import bundleManager from '@ohos.bundle.bundleManager';
import { BusinessError } from '@ohos.base';
import hilog from '@ohos.hilog';

let moduleName = 'entry';
let abilityName = 'EntryAbility';
let metadataName = 'ability_metadata';

try {
  bundleManager.getProfileByAbility(moduleName, abilityName, metadataName, (err, data) => {
    if (err) {
      hilog.error(0x0000, 'testTag', 'getProfileByAbility failed. Cause: %{public}s', err.message);
    } else {
      hilog.info(0x0000, 'testTag', 'getProfileByAbility successfully: %{public}s', JSON.stringify(data));
    }
  });
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'getProfileByAbility failed. Cause: %{public}s', message);
}
```

### bundleManager.getProfileByAbility

getProfileByAbility(moduleName: string, abilityName: string, metadataName?: string): Promise\<Array\<string\>\>

以异步方法根据给定的moduleName、abilityName和metadataName（module.json中[metadata标签](../../quick-start/module-configuration-file.md#metadata标签)下的name）获取相应配置文件的json格式字符串，使用Promise形式返回结果。

>如果配置文件信息采用了资源引用格式，则返回值将保持资源引用格式（例如 $string:res_id），开发者可以通过资源管理模块的相关接口，来获取引用的资源。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名       | 类型   | 必填 | 说明                       |
| ------------ | ------ | ---- | -------------------------- |
| moduleName   | string | 是   | 表示Module名称。   |
| abilityName  | string | 是   | 表示UIAbility组件的名称。  |
| metadataName | string | 否   | 表示UIAbility组件的元信息名称，即module.json5配置文件中abilities标签下的metadata标签的name，默认值为空。 |

**返回值：**

| 类型                    | 说明                            |
| ----------------------- | ------------------------------- |
| Promise<Array\<string>> | Promise对象，返回Array\<string>。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 17700002 | The specified moduleName is not existed.                      |
| 17700003 | The specified abilityName is not existed.                     |
| 17700024 | Failed to get the profile because there is no profile in the HAP. |
| 17700026 | The specified bundle is disabled.                             |
| 17700029 | The specified ability is disabled.                            |

**示例：**

```ts
import bundleManager from '@ohos.bundle.bundleManager';
import { BusinessError } from '@ohos.base';
import hilog from '@ohos.hilog';

let moduleName = 'entry';
let abilityName = 'EntryAbility';

try {
  bundleManager.getProfileByAbility(moduleName, abilityName).then((data) => {
    hilog.info(0x0000, 'testTag', 'getProfileByAbility successfully. Data: %{public}s', JSON.stringify(data));
  }).catch((err: BusinessError) => {
    hilog.error(0x0000, 'testTag', 'getProfileByAbility failed. Cause: %{public}s', err.message);
  });
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'getProfileByAbility failed. Cause: %{public}s', message);
}
```

```ts
import bundleManager from '@ohos.bundle.bundleManager';
import { BusinessError } from '@ohos.base';
import hilog from '@ohos.hilog';

let moduleName = 'entry';
let abilityName = 'EntryAbility';
let metadataName = 'ability_metadata';

try {
  bundleManager.getProfileByAbility(moduleName, abilityName, metadataName).then((data) => {
    hilog.info(0x0000, 'testTag', 'getProfileByAbility successfully. Data: %{public}s', JSON.stringify(data));
  }).catch((err: BusinessError) => {
    hilog.error(0x0000, 'testTag', 'getProfileByAbility failed. Cause: %{public}s', err.message);
  });
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'getProfileByAbility failed. Cause: %{public}s', message);
}
```

### bundleManager.getProfileByAbilitySync<sup>10+</sup>

getProfileByAbilitySync(moduleName: string, abilityName: string, metadataName?: string): Array\<string\>

以同步方法根据给定的moduleName、abilityName和metadataName（module.json中[metadata标签](../../quick-start/module-configuration-file.md#metadata标签)下的name）获取相应配置文件的json格式字符串，返回对象为string数组。

>如果配置文件信息采用了资源引用格式，则返回值将保持资源引用格式（例如 $string:res_id），开发者可以通过资源管理模块的相关接口，来获取引用的资源。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名       | 类型   | 必填 | 说明                       |
| ------------ | ------ | ---- | -------------------------- |
| moduleName   | string | 是   | 表示Module名称。   |
| abilityName  | string | 是   | 表示UIAbility组件的名称。  |
| metadataName | string | 否   | 表示UIAbility组件的元信息名称，即module.json5配置文件中abilities标签下的metadata标签的name，默认值为空。 |

**返回值：**

| 类型                    | 说明                            |
| ----------------------- | ------------------------------- |
| Array\<string> | 数组对象，返回Array\<string>。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 17700002 | The specified moduleName is not existed.                      |
| 17700003 | The specified abilityName is not existed.                     |
| 17700024 | Failed to get the profile because there is no profile in the HAP. |
| 17700026 | The specified bundle is disabled.                             |
| 17700029 | The specified ability is disabled.                            |

**示例：**

```ts
import bundleManager from '@ohos.bundle.bundleManager';
import { BusinessError } from '@ohos.base';
import hilog from '@ohos.hilog';

let moduleName = 'entry';
let abilityName = 'EntryAbility';

try {
  let data = bundleManager.getProfileByAbilitySync(moduleName, abilityName);
  hilog.info(0x0000, 'testTag', 'getProfileByAbilitySync successfully. Data: %{public}s', JSON.stringify(data));
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'getProfileByAbilitySync failed. Cause: %{public}s', message);
}
```

```ts
import bundleManager from '@ohos.bundle.bundleManager';
import { BusinessError } from '@ohos.base';
import hilog from '@ohos.hilog';

let moduleName: string = 'entry';
let abilityName: string = 'EntryAbility';
let metadataName: string = 'ability_metadata';

try {
  let data = bundleManager.getProfileByAbilitySync(moduleName, abilityName, metadataName);
  hilog.info(0x0000, 'testTag', 'getProfileByAbilitySync successfully. Data: %{public}s', JSON.stringify(data));
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'getProfileByAbilitySync failed. Cause: %{public}s', message);
}
```

### bundleManager.getProfileByExtensionAbility

getProfileByExtensionAbility(moduleName: string, extensionAbilityName: string, metadataName: string, callback: AsyncCallback\<Array\<string\>\>): void

以异步方法根据给定的moduleName、extensionAbilityName和metadataName（module.json中[metadata标签](../../quick-start/module-configuration-file.md#metadata标签)下的name）获取相应配置文件的json格式字符串，使用callback形式返回结果。

>如果配置文件信息采用了资源引用格式，则返回值将保持资源引用格式（例如 $string:res_id），开发者可以通过资源管理模块的相关接口，来获取引用的资源。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名                 | 类型                          | 必填 | 说明                                                         |
| -------------------- | ----------------------------- | ---- | ------------------------------------------------------------ |
| moduleName           | string                        | 是   | 表示Module名称。                                   |
| extensionAbilityName | string                        | 是   | 表示ExtensionAbility组件的名称。                         |
| metadataName         | string                        | 是   | 表示ExtensionAbility组件的名称。组件的元信息名称，即module.json5配置文件中extensionAbilities标签下的metadata标签的name。                                 |
| callback             | AsyncCallback<Array\<string>> | 是   | 回调函数，当获取成功时，err为null，data为获取到的Array\<string>；否则为错误对象。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 17700002 | The specified moduleName is not existed.                      |
| 17700003 | The specified extensionAbilityName not existed.            |
| 17700024 | Failed to get the profile because there is no profile in the HAP. |
| 17700026 | The specified bundle is disabled.                             |

**示例：**

```ts
import bundleManager from '@ohos.bundle.bundleManager';
import { BusinessError } from '@ohos.base';
import hilog from '@ohos.hilog';

let moduleName = 'entry';
let extensionAbilityName = 'com.example.myapplication.extension';
let metadataName = 'ability_metadata';

try {
  bundleManager.getProfileByExtensionAbility(moduleName, extensionAbilityName, metadataName, (err, data) => {
    if (err) {
      hilog.error(0x0000, 'testTag', 'getProfileByExtensionAbility failed: %{public}s', err.message);
    } else {
      hilog.info(0x0000, 'testTag', 'getProfileByExtensionAbility successfully: %{public}s', JSON.stringify(data));
    }
  });
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'getProfileByExtensionAbility failed: %{public}s', message);
}
```

### bundleManager.getProfileByExtensionAbility

getProfileByExtensionAbility(moduleName: string, extensionAbilityName: string, metadataName?: string): Promise\<Array\<string\>\>

以异步方法根据给定的moduleName、extensionAbilityName和metadataName（module.json中[metadata标签](../../quick-start/module-configuration-file.md#metadata标签)下的name）获取相应配置文件的json格式字符串，使用Promise形式返回结果。

>如果配置文件信息采用了资源引用格式，则返回值将保持资源引用格式（例如 $string:res_id），开发者可以通过资源管理模块的相关接口，来获取引用的资源。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名                 | 类型   | 必填 | 说明                               |
| -------------------- | ------ | ---- | ---------------------------------- |
| moduleName           | string | 是   | 表示Module名称。           |
| extensionAbilityName | string | 是   | 表示ExtensionAbility组件的名称。 |
| metadataName         | string | 否   | 表示ExtensionAbility组件的名称。组件的元信息名称，即module.json5配置文件中extensionAbilities标签下的metadata标签的name，默认值为空。         |

**返回值：**

| 类型                    | 说明                                |
| ----------------------- | ----------------------------------- |
| Promise<Array\<string>> | Promise对象，返回Array\<string>对象。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 17700002 | The specified moduleName is not existed.                      |
| 17700003 | The specified extensionAbilityName not existed.            |
| 17700024 | Failed to get the profile because there is no profile in the HAP. |
| 17700026 | The specified bundle is disabled.                             |

**示例：**

```ts
import bundleManager from '@ohos.bundle.bundleManager';
import { BusinessError } from '@ohos.base';
import hilog from '@ohos.hilog';

let moduleName = 'entry';
let extensionAbilityName = 'com.example.myapplication.extension';
let metadataName = 'ability_metadata';

try {
  bundleManager.getProfileByExtensionAbility(moduleName, extensionAbilityName).then((data) => {
    hilog.info(0x0000, 'testTag', 'getProfileByExtensionAbility successfully. Data: %{public}s', JSON.stringify(data));
  }).catch((err: BusinessError) => {
    hilog.error(0x0000, 'testTag', 'getProfileByExtensionAbility failed. Cause: %{public}s', err.message);
  });
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'getProfileByExtensionAbility failed. Cause: %{public}s', message);
}

try {
  bundleManager.getProfileByExtensionAbility(moduleName, extensionAbilityName, metadataName).then((data) => {
    hilog.info(0x0000, 'testTag', 'getProfileByExtensionAbility successfully. Data: %{public}s', JSON.stringify(data));
  }).catch((err: BusinessError) => {
    hilog.error(0x0000, 'testTag', 'getProfileByExtensionAbility failed. Cause: %{public}s', err.message);
  });
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'getProfileByExtensionAbility failed. Cause: %{public}s', message);
}
```

### bundleManager.getProfileByExtensionAbilitySync<sup>10+</sup>

getProfileByExtensionAbilitySync(moduleName: string, extensionAbilityName: string, metadataName?: string): Array\<string\>

以同步方法根据给定的moduleName、extensionAbilityName和metadataName（module.json中[metadata标签](../../quick-start/module-configuration-file.md#metadata标签)下的name）获取相应配置文件的json格式字符串，返回对象为string数组。

>如果配置文件信息采用了资源引用格式，则返回值将保持资源引用格式（例如 $string:res_id），开发者可以通过资源管理模块的相关接口，来获取引用的资源。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名                 | 类型   | 必填 | 说明                               |
| -------------------- | ------ | ---- | ---------------------------------- |
| moduleName           | string | 是   | 表示Module名称。           |
| extensionAbilityName | string | 是   | 表示ExtensionAbility组件的名称。 |
| metadataName         | string | 否   | 表示ExtensionAbility组件的名称。组件的元信息名称，即module.json5配置文件中extensionAbilities标签下的metadata标签的name，默认值为空。         |

**返回值：**

| 类型                    | 说明                                |
| ----------------------- | ----------------------------------- |
| Array\<string> | 返回Array\<string>对象。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 17700002 | The specified moduleName is not existed.                      |
| 17700003 | The specified extensionAbilityName not existed.            |
| 17700024 | Failed to get the profile because there is no profile in the HAP. |
| 17700026 | The specified bundle is disabled.                             |

**示例：**

```ts
import bundleManager from '@ohos.bundle.bundleManager';
import { BusinessError } from '@ohos.base';
import hilog from '@ohos.hilog';

let moduleName = 'entry';
let extensionAbilityName = 'com.example.myapplication.extension';
let metadataName = 'ability_metadata';

try {
  let data = bundleManager.getProfileByExtensionAbilitySync(moduleName, extensionAbilityName);
  hilog.info(0x0000, 'testTag', 'getProfileByExtensionAbilitySync successfully. Data: %{public}s', JSON.stringify(data));
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'getProfileByExtensionAbilitySync failed. Cause: %{public}s', message);
}

try {
  let data = bundleManager.getProfileByExtensionAbilitySync(moduleName, extensionAbilityName, metadataName);
  hilog.info(0x0000, 'testTag', 'getProfileByExtensionAbilitySync successfully. Data: %{public}s', JSON.stringify(data));
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'getProfileByExtensionAbilitySync failed. Cause: %{public}s', message);
}
```

### bundleManager.getBundleInfoForSelfSync<sup>10+</sup>

getBundleInfoForSelfSync(bundleFlags: number): BundleInfo

以同步方法根据给定的bundleFlags获取当前应用的BundleInfo。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名     | 类型   | 必填 | 说明                |
| ----------- | ------ | ---- | --------------------- |
| [bundleFlags](js-apis-bundleManager.md#bundleflag) | number | 是   | 指定返回的BundleInfo所包含的信息。 |

**返回值：**

| 类型                                              | 说明                 |
| ------------------------------------------------- | -------------------- |
| [BundleInfo](js-apis-bundleManager-bundleInfo.md) | 返回BundleInfo对象。 |

**示例：**

```ts
import bundleManager from '@ohos.bundle.bundleManager';
import { BusinessError } from '@ohos.base';
import hilog from '@ohos.hilog';

let bundleFlags = bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION;

try {
  let data = bundleManager.getBundleInfoForSelfSync(bundleFlags);
  hilog.info(0x0000, 'testTag', 'getBundleInfoForSelfSync successfully: %{public}s', JSON.stringify(data));
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'getBundleInfoForSelfSync failed: %{public}s', message);
}
```

### bundleManager.verifyAbc<sup>11+</sup>

verifyAbc(abcPaths: Array\<string>, deleteOriginalFiles: boolean, callback: AsyncCallback\<void>): void

根据给定的abcPaths和deleteOriginalFiles校验.abc文件。使用callback异步回调。

**需要权限：** ohos.permission.RUN_DYN_CODE

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名     | 类型   | 必填 | 说明                       |
| ----------- | ------ | ---- | ---------------------------- |
| abcPaths  | Array\<string> | 是   | .abc文件路径。 |
| deleteOriginalFiles | boolean | 是   | 是否删除.abc文件，true删除，false不删除。|
| callback | AsyncCallback\<void> | 是 | 回调函数，当获取成功时，err为null；否则为错误对象。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                              |
| -------- | ------------------------------------- |
| 17700201 | Failed to verify the abc file. |

**示例：**

```ts
import bundleManager from '@ohos.bundle.bundleManager';
import { BusinessError } from '@ohos.base';
import hilog from '@ohos.hilog';

let abcPaths: Array<string> = ['/data/storage/el2/base/a.abc'];

try {
  bundleManager.verifyAbc(abcPaths, true, (err, data) => {
    if (err) {
      hilog.error(0x0000, 'testTag', 'verifyAbc failed: %{public}s', err.message);
    } else {
      hilog.info(0x0000, 'testTag', 'verifyAbc successfully');
    }
  });
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'verifyAbc failed: %{public}s', message);
}
```

### bundleManager.verifyAbc<sup>11+</sup>

verifyAbc(abcPaths: Array\<string>, deleteOriginalFiles: boolean): Promise\<void>

根据给定的abcPaths和deleteOriginalFiles校验.abc文件。使用Promise异步回调。

**需要权限：** ohos.permission.RUN_DYN_CODE

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名     | 类型   | 必填 | 说明                       |
| ----------- | ------ | ---- | ---------------------------- |
| abcPaths  | Array\<string> | 是   | .abc文件路径。 |
| deleteOriginalFiles | boolean | 是   | 是否删除.abc文件，true删除，false不删除。       |

**返回值：**

| 类型                                                        | 说明                        |
| ----------------------------------------------------------- | --------------------------- |
| Promise\<void> | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                            |
| -------- | --------------------------------------|
| 17700201 | Failed to verify the abc file. |

**示例：**

```ts
import bundleManager from '@ohos.bundle.bundleManager';
import { BusinessError } from '@ohos.base';
import hilog from '@ohos.hilog';

let abcPaths: Array<string> = ['/data/storage/el2/base/a.abc'];

try {
  bundleManager.verifyAbc(abcPaths, true).then((data) => {
    hilog.info(0x0000, 'testTag', 'verifyAbc successfully');
  }).catch((err: BusinessError) => {
    hilog.error(0x0000, 'testTag', 'verifyAbc failed. Cause: %{public}s', err.message);
  });
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'verifyAbc failed. Cause: %{public}s', message);
}
```

### bundleManager.deleteAbc<sup>11+</sup>

deleteAbc(abcPath: string): Promise\<void>

根据给定的abcPath删除.abc文件。使用Promise异步回调。

**需要权限：** ohos.permission.RUN_DYN_CODE

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名     | 类型   | 必填 | 说明                       |
| ----------- | ------ | ---- | ---------------------------- |
| abcPath  | string | 是   | .abc文件路径。 |

**返回值：**

| 类型                                                        | 说明                        |
| ----------------------------------------------------------- | --------------------------- |
| Promise\<void> | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                            |
| -------- | --------------------------------------|
| 17700202 | Failed to delete the abc file. |

**示例：**

```ts
import bundleManager from '@ohos.bundle.bundleManager';
import { BusinessError } from '@ohos.base';
import hilog from '@ohos.hilog';

let abcPath: string = '/data/storage/el2/base/a.abc';

try {
  bundleManager.deleteAbc(abcPath).then((data) => {
    hilog.info(0x0000, 'testTag', 'deleteAbc successfully');
  }).catch((err: BusinessError) => {
    hilog.error(0x0000, 'testTag', 'deleteAbc failed. Cause: %{public}s', err.message);
  });
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'deleteAbc failed. Cause: %{public}s', message);
}
```