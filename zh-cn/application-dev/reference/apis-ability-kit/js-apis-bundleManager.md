# @ohos.bundle.bundleManager (bundleManager模块)

本模块提供应用信息查询能力，支持[BundleInfo](js-apis-bundleManager-bundleInfo.md)、[ApplicationInfo](js-apis-bundleManager-applicationInfo.md)、[AbilityInfo](js-apis-bundleManager-abilityInfo.md)、[ExtensionAbilityInfo](js-apis-bundleManager-extensionAbilityInfo.md)等信息的查询。

> **说明：**
> 本模块首批接口从API version 9 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import { bundleManager } from '@kit.AbilityKit';
```

## 权限列表

| 权限                                       | 权限等级     | 描述            |
| ------------------------------------------ | ------------ | ------------------|
| ohos.permission.GET_BUNDLE_INFO_PRIVILEGED | system_basic | 允许查询应用的基本信息和其他敏感信息。 |

权限等级参考[权限APL等级说明](../../security/AccessToken/app-permission-mgmt-overview.md#权限机制中的基本概念)。

## 枚举

### BundleFlag

包信息标志，指示需要获取的包信息的内容。

 **系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 名称                                          | 值         | 说明                                                         |
| --------------------------------------------- | ---------- | ------------------------------------------------------------ |
| GET_BUNDLE_INFO_DEFAULT                       | 0x00000000 | 用于获取默认bundleInfo，获取的bundleInfo不包含signatureInfo、applicationInfo、hapModuleInfo、ability、extensionAbility和permission的信息。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| GET_BUNDLE_INFO_WITH_APPLICATION              | 0x00000001 | 用于获取包含applicationInfo的bundleInfo，获取的bundleInfo不包含signatureInfo、hapModuleInfo、ability、extensionAbility和permission的信息。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| GET_BUNDLE_INFO_WITH_HAP_MODULE               | 0x00000002 | 用于获取包含hapModuleInfo的bundleInfo，获取的bundleInfo不包含signatureInfo、applicationInfo、ability、extensionAbility和permission的信息。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| GET_BUNDLE_INFO_WITH_ABILITY                  | 0x00000004 | 用于获取包含ability的bundleInfo，获取的bundleInfo不包含signatureInfo、applicationInfo、extensionAbility和permission的信息。它不能单独使用，需要与GET_BUNDLE_INFO_WITH_HAP_MODULE一起使用。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| GET_BUNDLE_INFO_WITH_EXTENSION_ABILITY        | 0x00000008 | 用于获取包含extensionAbility的bundleInfo，获取的bundleInfo不包含signatureInfo、applicationInfo、ability 和permission的信息。它不能单独使用，需要与GET_BUNDLE_INFO_WITH_HAP_MODULE一起使用。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION     | 0x00000010 | 用于获取包含permission的bundleInfo。获取的bundleInfo不包含signatureInfo、applicationInfo、hapModuleInfo、extensionAbility和ability的信息。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| GET_BUNDLE_INFO_WITH_METADATA                 | 0x00000020 | 用于获取applicationInfo、moduleInfo和abilityInfo中包含的metadata。它不能单独使用，它需要与GET_BUNDLE_INFO_WITH_APPLICATION、GET_BUNDLE_INFO_WITH_HAP_MODULE、GET_BUNDLE_INFO_WITH_ABILITY、GET_BUNDLE_INFO_WITH_EXTENSION_ABILITY一起使用。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| GET_BUNDLE_INFO_WITH_DISABLE                  | 0x00000040 | 用于获取application被禁用的BundleInfo和被禁用的Ability信息。获取的bundleInfo不包含signatureInfo、applicationInfo、hapModuleInfo、ability、extensionAbility和permission的信息。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| GET_BUNDLE_INFO_WITH_SIGNATURE_INFO           | 0x00000080 | 用于获取包含signatureInfo的bundleInfo。获取的bundleInfo不包含applicationInfo、hapModuleInfo、extensionAbility、ability和permission的信息。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| GET_BUNDLE_INFO_WITH_MENU<sup>11+</sup>       | 0x00000100 | 用于获取包含fileContextMenuConfig的bundleInfo。它不能单独使用，需要与GET_BUNDLE_INFO_WITH_HAP_MODULE一起使用。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| GET_BUNDLE_INFO_WITH_ROUTER_MAP<sup>12+</sup> | 0x00000200 | 用于获取包含routerMap的bundleInfo。它不能单独使用，需要与GET_BUNDLE_INFO_WITH_HAP_MODULE一起使用。<br/>**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。 |
| GET_BUNDLE_INFO_WITH_SKILL<sup>12+</sup>      | 0x00000800 | 用于获取包含skills的bundleInfo。它不能单独使用，需要与GET_BUNDLE_INFO_WITH_HAP_MODULE、GET_BUNDLE_INFO_WITH_ABILITY、GET_BUNDLE_INFO_WITH_EXTENSION_ABILITY一起使用。<br/>**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。 |

### ExtensionAbilityType

指示扩展组件的类型。

 **系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 名称 | 值 | 说明 |
|:----------------:|:---:|-----|
| FORM             | 0   | [FormExtensionAbility](../apis-form-kit/js-apis-app-form-formExtensionAbility.md)：卡片扩展能力，提供卡片开发能力。<br>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| WORK_SCHEDULER   | 1   | [WorkSchedulerExtensionAbility](../apis-backgroundtasks-kit/js-apis-WorkSchedulerExtensionAbility.md)：延时任务扩展能力，允许应用在系统闲时执行实时性不高的任务。 |
| INPUT_METHOD     | 2   | [InputMethodExtensionAbility](../apis-ime-kit/js-apis-inputmethod-extension-ability.md)：输入法扩展能力，用于开发输入法应用。 |
| SERVICE          | 3   | <!--Del-->[<!--DelEnd-->ServiceExtensionAbility<!--Del-->](js-apis-app-ability-serviceExtensionAbility-sys.md)<!--DelEnd-->：后台服务扩展能力，提供后台运行并对外提供相应能力。 |
| ACCESSIBILITY    | 4   | <!--RP1-->[AccessibilityExtensionAbility](../apis-accessibility-kit/js-apis-application-accessibilityExtensionAbility.md)<!--RP1End-->：无障碍服务扩展能力，支持访问与操作前台界面。 |
| DATA_SHARE       | 5   | <!--Del-->[<!--DelEnd-->DataShareExtensionAbility <!--Del-->](../apis-arkdata/js-apis-application-dataShareExtensionAbility-sys.md)<!--DelEnd-->：数据共享扩展能力，用于对外提供数据读写服务。 |
| FILE_SHARE       | 6   | FileShareExtensionAbility：文件共享扩展能力，用于应用间的文件分享。预留能力，仅系统应用支持。 |
| STATIC_SUBSCRIBER| 7   | <!--Del-->[<!--DelEnd-->StaticSubscriberExtensionAbility <!--Del-->](../apis-basic-services-kit/js-apis-application-staticSubscriberExtensionAbility-sys.md)<!--DelEnd-->：静态广播扩展能力，用于处理静态事件，比如开机事件。 |
| WALLPAPER        | 8   | WallpaperExtensionAbility：壁纸扩展能力，用于实现桌面壁纸。预留能力，仅系统应用支持。 |
| BACKUP           |  9  | [BackupExtensionAbility](../apis-core-file-kit/js-apis-application-backupExtensionAbility.md)：数据备份扩展能力，提供应用数据的备份恢复能力。 |
| WINDOW           |  10 | <!--Del-->[<!--DelEnd-->WindowExtensionAbility<!--Del-->](../apis-arkui/js-apis-application-windowExtensionAbility-sys.md)<!--DelEnd-->：界面组合扩展能力，允许系统应用进行跨应用的界面拉起和嵌入。 |
| ENTERPRISE_ADMIN |  11 | [EnterpriseAdminExtensionAbility](../apis-mdm-kit/js-apis-EnterpriseAdminExtensionAbility.md)：企业设备管理扩展能力，提供企业管理时处理管理事件的能力，比如设备上应用安装事件、锁屏密码输入错误次数过多事件等。 |
| THUMBNAIL        | 13  | ThumbnailExtensionAbility：文件缩略图扩展能力，用于为文件提供图标缩略图的能力。预留能力，仅系统应用支持。 |
| PREVIEW          | 14  | PreviewExtensionAbility：文件预览扩展能力，提供文件预览的能力，其他应用可以直接在应用中嵌入显示。预留能力，仅系统应用支持。 |
| PRINT<sup>10+</sup> | 15 | PrintExtensionAbility：文件打印扩展能力，提供应用打印照片、文档等办公场景。仅系统应用支持。 |
| SHARE<sup>10+</sup> | 16 | [ShareExtensionAbility](js-apis-app-ability-shareExtensionAbility.md)：提供分享业务能力，为开发者提供基于UIExtension的分享业务模板。 |
| PUSH<sup>10+</sup> | 17 | PushExtensionAbility：推送扩展能力，提供推送场景化消息能力。预留能力，仅系统应用支持。 |
| DRIVER<sup>10+</sup> | 18 | [DriverExtensionAbility](../apis-driverdevelopment-kit/js-apis-app-ability-driverExtensionAbility.md)：驱动扩展能力，提供外设驱动扩展能力，仅系统应用支持。 |
| ACTION<sup>10+</sup> | 19 | [ActionExtensionAbility](js-apis-app-ability-actionExtensionAbility.md)：自定义服务扩展能力，为开发者提供基于UIExtension的自定义操作业务模板。 |
| ADS_SERVICE<sup>11+</sup> | 20 | AdsServiceExtensionAbility：广告服务扩展能力，对外提供后台自定义广告业务服务，仅系统应用支持。 |
| EMBEDDED_UI<sup>12+</sup> | 21 | [EmbeddedUIExtensionAbility](js-apis-app-ability-embeddedUIExtensionAbility.md)：嵌入式UI扩展能力，提供跨进程界面嵌入的能力。 |
| INSIGHT_INTENT_UI<sup>12+</sup> | 22 | InsightIntentUIExtensionAbility：为开发者提供能被小艺意图调用，以窗口形态呈现内容的扩展能力。 |
| UNSPECIFIED      | 255 | 不指定类型，配合queryExtensionAbilityInfo接口可以查询所有类型的ExtensionAbility。 |


### PermissionGrantState

指示权限授予状态。

 **原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

 **系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 名称 | 值 | 说明 |
|:----------------:|:---:|:---:|
| PERMISSION_DENIED|  -1 | 拒绝授予权限。 |
| PERMISSION_GRANTED |  0  |  授予权限。  |

### SupportWindowMode

标识该组件所支持的窗口模式。

 **原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

 **系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 名称 | 值 | 说明 |
|:----------------:|:---:|:---:|
| FULL_SCREEN      | 0   | 窗口支持全屏显示。 |
| SPLIT            | 1   | 窗口支持分屏显示。 |
| FLOATING         | 2   | 支持窗口化显示。   |

### LaunchType

指示组件的启动方式。

 **原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

 **系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 名称 | 值 | 说明 |
|:----------------:|:---:|:---:|
| SINGLETON        | 0   | ability的启动模式，表示单实例。 |
| MULTITON         | 1   | ability的启动模式，表示普通多实例。 |
| SPECIFIED        | 2   | ability的启动模式，表示该ability内部根据业务自己指定多实例。 |

### AbilityType

指示Ability组件的类型。

 **模型约束：** 仅可在FA模型下使用。

 **系统能力：** SystemCapability.BundleManager.BundleFramework.Core

|  名称   | 值   |                            说明                            |
| :-----: | ---- | :--------------------------------------------------------: |
| PAGE    | 1    | UI界面类型的Ability。表示基于Page模板开发的FA，用于提供与用户交互的能力。        |
| SERVICE | 2    | 后台服务类型的Ability，无UI界面。表示基于Service模板开发的PA，用于提供后台运行任务的能力。  |
|  DATA   | 3    | 表示基于Data模板开发的PA，用于对外部提供统一的数据访问对象。 |

### DisplayOrientation

标识该Ability的显示模式。该标签仅适用于page类型的Ability。

 **系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 名称                               |值 |说明 |
|:----------------------------------|---|---|
| UNSPECIFIED                        |0 |表示未定义方向模式，由系统判定。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| LANDSCAPE                          |1 |表示横屏显示模式。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| PORTRAIT                           |2 |表示竖屏显示模式。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| FOLLOW_RECENT                      |3 |表示跟随上一个显示模式。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| LANDSCAPE_INVERTED                 |4 |表示反向横屏显示模式。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| PORTRAIT_INVERTED                  |5 |表示反向竖屏显示模式。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| AUTO_ROTATION                      |6 |表示传感器自动旋转模式。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| AUTO_ROTATION_LANDSCAPE            |7 |表示传感器自动横向旋转模式。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| AUTO_ROTATION_PORTRAIT             |8 |表示传感器自动竖向旋转模式。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| AUTO_ROTATION_RESTRICTED           |9 |表示受开关控制的自动旋转模式。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。 |
| AUTO_ROTATION_LANDSCAPE_RESTRICTED |10|表述受开关控制的自动横向旋转模式。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。|
| AUTO_ROTATION_PORTRAIT_RESTRICTED  |11|表示受开关控制的自动竖向旋转模式。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。|
| LOCKED                             |12|表示锁定模式。<br/>**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。|
| AUTO_ROTATION_UNSPECIFIED<sup>12+</sup> |13|受开关控制和由系统判定的自动旋转模式。<br/>**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。|
| FOLLOW_DESKTOP<sup>12+</sup> |14|跟随桌面的旋转模式。<br/>**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。|

### CompatiblePolicy<sup>10+</sup>

标识共享库的版本兼容类型。

 **原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

 **系统能力:** SystemCapability.BundleManager.BundleFramework.Core

| 名称                   | 值   | 说明                             |
| ---------------------- | ---- | -------------------------------- |
| BACKWARD_COMPATIBILITY | 1    | 该字段表明共享库是向后兼容类型。 |

### ModuleType

标识模块类型。

 **原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

 **系统能力:** SystemCapability.BundleManager.BundleFramework.Core

| 名称    | 值   | 说明                 |
| ------- | ---- | -------------------- |
| ENTRY   | 1    | 应用的主模块。   |
| FEATURE | 2    | 应用的动态特性模块。 |
| SHARED  | 3    | 应用的动态共享库模块。  |

### BundleType

标识应用的类型。

 **原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

 **系统能力:** SystemCapability.BundleManager.BundleFramework.Core

| 名称           | 值   | 说明            |
| -------------- | ---- | --------------- |
| APP            | 0    | 该Bundle是应用。    |
| ATOMIC_SERVICE | 1    | 该Bundle是原子化服务。 |

### MultiAppModeType<sup>12+</sup>
标识应用多开的模式类型。

 **系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 名称 | 值 | 说明 |
|:----------------:|:---:|:---:|
| UNSPECIFIED|  0 | 未指定类型。 |
| MULTI_INSTANCE |  1  | 多实例模式。常驻进程不支持该字段。  |
| APP_CLONE |  2  |  分身模式。  |

## 接口

### bundleManager.getBundleInfoForSelf

getBundleInfoForSelf(bundleFlags: number): Promise\<BundleInfo>

根据给定的bundleFlags获取当前应用的BundleInfo，使用Promise异步回调。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名     | 类型   | 必填 | 说明                |
| ----------- | ------ | ---- | --------------------- |
| [bundleFlags](js-apis-bundleManager.md#bundleflag) | number | 是   | 指定返回的BundleInfo所包含的信息。 |

**返回值：**

| 类型                                                        | 说明                                  |
| ----------------------------------------------------------- | ------------------------------------- |
| Promise\<[BundleInfo](js-apis-bundleManager-bundleInfo.md)> | Promise对象，返回当前应用的BundleInfo。|

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|

**示例：**

```ts
// 额外获取带有metadataArray信息的appInfo
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';

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

根据给定的bundleFlags获取当前应用的BundleInfo，使用callback异步回调。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名     | 类型   | 必填 | 说明                |
| ----------- | ------ | ---- | --------------------- |
| [bundleFlags](js-apis-bundleManager.md#bundleflag) | number | 是   | 指定返回的BundleInfo所包含的信息。 |
| callback | AsyncCallback\<[BundleInfo](js-apis-bundleManager-bundleInfo.md)> | 是 | 回调函数，当获取成功时，err为null，data为获取到的当前应用的BundleInfo；否则为错误对象。 |

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|

**示例：**

```ts
// 额外获取带有permissions信息的abilitiesInfo
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';

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

根据给定的moduleName、abilityName和metadataName（module.json中[metadata标签](../../quick-start/module-configuration-file.md#metadata标签)下的name）获取相应配置文件的json格式字符串，使用callback异步回调。

>如果配置文件信息采用了资源引用格式，则返回值将保持资源引用格式（例如 $string:res_id），开发者可以通过资源管理模块的相关接口，来获取引用的资源。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名       | 类型                          | 必填 | 说明                                                         |
| ------------ | ----------------------------- | ---- | ------------------------------------------------------------ |
| moduleName   | string                        | 是   | 表示Module名称。                                     |
| abilityName  | string                        | 是   | 表示UIAbility组件的名称。                                    |
| metadataName | string                        | 是   | 表示UIAbility组件的元信息名称，即module.json5配置文件中abilities标签下的metadata标签的name。                                  |
| callback     | AsyncCallback<Array\<string>> | 是   | 回调函数，当获取成功时，err为null，data为获取到的Array\<string>；否则为错误对象。 |

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
| 17700002 | The specified moduleName is not existed.                      |
| 17700003 | The specified abilityName is not existed.                     |
| 17700024 | Failed to get the profile because there is no profile in the HAP. |
| 17700026 | The specified bundle is disabled.                             |
| 17700029 | The specified ability is disabled.                            |

**示例：**

```ts
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';

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

根据给定的moduleName、abilityName和metadataName（module.json中[metadata标签](../../quick-start/module-configuration-file.md#metadata标签)下的name）获取相应配置文件的json格式字符串，使用Promise异步回调。

>如果配置文件信息采用了资源引用格式，则返回值将保持资源引用格式（例如 $string:res_id），开发者可以通过资源管理模块的相关接口，来获取引用的资源。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

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

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
| 17700002 | The specified moduleName is not existed.                      |
| 17700003 | The specified abilityName is not existed.                     |
| 17700024 | Failed to get the profile because there is no profile in the HAP. |
| 17700026 | The specified bundle is disabled.                             |
| 17700029 | The specified ability is disabled.                            |

**示例：**

```ts
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';

let moduleName = 'entry';
let abilityName = 'EntryAbility';

try {
  // 通过模块名称和ability名称获取相应配置文件的json格式字符串信息
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
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';

let moduleName = 'entry';
let abilityName = 'EntryAbility';
let metadataName = 'ability_metadata';

try {
  // 通过模块名称，ability名称和UIAbility组件的元信息名称获取相应配置文件的json格式字符串信息
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

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

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

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
| 17700002 | The specified moduleName is not existed.                      |
| 17700003 | The specified abilityName is not existed.                     |
| 17700024 | Failed to get the profile because there is no profile in the HAP. |
| 17700026 | The specified bundle is disabled.                             |
| 17700029 | The specified ability is disabled.                            |

**示例：**

```ts
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';

let moduleName = 'entry';
let abilityName = 'EntryAbility';

try {
  // 通过模块名称和ability名称获取相应配置文件的json格式字符串信息
  let data = bundleManager.getProfileByAbilitySync(moduleName, abilityName);
  hilog.info(0x0000, 'testTag', 'getProfileByAbilitySync successfully. Data: %{public}s', JSON.stringify(data));
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'getProfileByAbilitySync failed. Cause: %{public}s', message);
}
```

```ts
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';

let moduleName: string = 'entry';
let abilityName: string = 'EntryAbility';
let metadataName: string = 'ability_metadata';

try {
  // 通过模块名称，ability名称和UIAbility组件的元信息名称获取相应配置文件的json格式字符串信息
  let data = bundleManager.getProfileByAbilitySync(moduleName, abilityName, metadataName);
  hilog.info(0x0000, 'testTag', 'getProfileByAbilitySync successfully. Data: %{public}s', JSON.stringify(data));
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'getProfileByAbilitySync failed. Cause: %{public}s', message);
}
```

### bundleManager.getProfileByExtensionAbility

getProfileByExtensionAbility(moduleName: string, extensionAbilityName: string, metadataName: string, callback: AsyncCallback\<Array\<string\>\>): void

根据给定的moduleName、extensionAbilityName和metadataName（module.json中[metadata标签](../../quick-start/module-configuration-file.md#metadata标签)下的name）获取相应配置文件的json格式字符串，使用callback异步回调。

>如果配置文件信息采用了资源引用格式，则返回值将保持资源引用格式（例如 $string:res_id），开发者可以通过资源管理模块的相关接口，来获取引用的资源。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名                 | 类型                          | 必填 | 说明                                                         |
| -------------------- | ----------------------------- | ---- | ------------------------------------------------------------ |
| moduleName           | string                        | 是   | 表示Module名称。                                   |
| extensionAbilityName | string                        | 是   | 表示ExtensionAbility组件的名称。                         |
| metadataName         | string                        | 是   | 表示ExtensionAbility组件的名称。组件的元信息名称，即module.json5配置文件中extensionAbilities标签下的metadata标签的name。                                 |
| callback             | AsyncCallback<Array\<string>> | 是   | 回调函数，当获取成功时，err为null，data为获取到的Array\<string>；否则为错误对象。 |

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
| 17700002 | The specified moduleName is not existed.                      |
| 17700003 | The specified extensionAbilityName not existed.            |
| 17700024 | Failed to get the profile because there is no profile in the HAP. |
| 17700026 | The specified bundle is disabled.                             |

**示例：**

```ts
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';

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

根据给定的moduleName、extensionAbilityName和metadataName（module.json中[metadata标签](../../quick-start/module-configuration-file.md#metadata标签)下的name）获取相应配置文件的json格式字符串，使用Promise异步回调。

>如果配置文件信息采用了资源引用格式，则返回值将保持资源引用格式（例如 $string:res_id），开发者可以通过资源管理模块的相关接口，来获取引用的资源。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

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

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
| 17700002 | The specified moduleName is not existed.                      |
| 17700003 | The specified extensionAbilityName not existed.            |
| 17700024 | Failed to get the profile because there is no profile in the HAP. |
| 17700026 | The specified bundle is disabled.                             |

**示例：**

```ts
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';

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

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

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

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
| 17700002 | The specified moduleName is not existed.                      |
| 17700003 | The specified extensionAbilityName not existed.            |
| 17700024 | Failed to get the profile because there is no profile in the HAP. |
| 17700026 | The specified bundle is disabled.                             |

**示例：**

```ts
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';

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

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名     | 类型   | 必填 | 说明                |
| ----------- | ------ | ---- | --------------------- |
| [bundleFlags](js-apis-bundleManager.md#bundleflag) | number | 是   | 指定返回的BundleInfo所包含的信息。 |

**返回值：**

| 类型                                              | 说明                 |
| ------------------------------------------------- | -------------------- |
| [BundleInfo](js-apis-bundleManager-bundleInfo.md) | 返回BundleInfo对象。 |

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|

**示例：**

```ts
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';

let bundleFlags = bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION;

try {
  let data = bundleManager.getBundleInfoForSelfSync(bundleFlags);
  hilog.info(0x0000, 'testTag', 'getBundleInfoForSelfSync successfully: %{public}s', JSON.stringify(data));
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'getBundleInfoForSelfSync failed: %{public}s', message);
}
```

### bundleManager.canOpenLink<sup>12+</sup>

canOpenLink(link: string): boolean

查询给定的链接是否可以打开。指定链接的scheme需要在module.json文件的querySchemes字段下配置。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名     | 类型   | 必填 | 说明                |
| ----------- | ------ | ---- | --------------------- |
| link | string | 是   | 表示需要查询的链接。 |

**返回值：**

| 类型                                              | 说明                 |
| ------------------------------------------------- | -------------------- |
| boolean | 返回true表示给定的链接可以打开，返回false表示给定的链接不能打开。 |

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                                                     |
| -------- | ------------------------------------------------------------ |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
| 17700055 | The specified link is invalid.                      |
| 17700056 | The scheme of the specified link is not in the querySchemes.        |

**示例：**

```ts
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';

try {
  let link = 'welink://';
  let data = bundleManager.canOpenLink(link);
  hilog.info(0x0000, 'testTag', 'canOpenLink successfully: %{public}s', JSON.stringify(data));
} catch (err) {
  let message = (err as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'canOpenLink failed: %{public}s', message);
}
```

### bundleManager.getLaunchWant<sup>13+</sup>

getLaunchWant(): Want

获取自身用于启动应用程序的Want参数。

**原子化服务API：** 从API version 13开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**返回值：**

| 类型                                | 说明                                        |
| ----------------------------------- | ------------------------------------------- |
| [Want](js-apis-app-ability-want.md) | 返回包含Bundle名称和Ability名称的Want对象。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                      |
| -------- | ----------------------------- |
| 17700072 | The launch want is not found. |

**示例：**

```ts
import { BusinessError } from '@kit.BasicServicesKit';
import { bundleManager } from '@kit.AbilityKit';
import { hilog } from '@kit.PerformanceAnalysisKit';

try {
  let want = bundleManager.getLaunchWant();
  hilog.info(0x0000, 'testTag', 'getLaunchWant ability name: %{public}s', want.abilityName);
  hilog.info(0x0000, 'testTag', 'getLaunchWant bundle name: %{public}s', want.bundleName);
} catch (error) {
  let message = (error as BusinessError).message;
  hilog.error(0x0000, 'testTag', 'getLaunchWant failed: %{public}s', message);
}
```

### bundleManager.getBundleInfo<sup>14+</sup>

getBundleInfo(bundleName: string, bundleFlags: number, userId: number, callback: AsyncCallback\<BundleInfo>): void

根据给定的bundleName、bundleFlags和userId获取BundleInfo，使用callback异步回调。

获取调用方自己的信息时不需要权限。

**需要权限：** ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名  | 类型   | 必填 | 说明                       |
| ----------- | ------ | ---- | ---------------------------- |
| bundleName  | string | 是   | 表示要查询的应用Bundle名称。 |
| [bundleFlags](js-apis-bundleManager.md#bundleflag) | number | 是   | 指定返回的BundleInfo所包含的信息。|
| userId      | number | 是   | 表示用户ID。  |
| callback | AsyncCallback\<[BundleInfo](js-apis-bundleManager-bundleInfo.md)> | 是 | 回调函数，当获取成功时，err为null，data为获取到的bundleInfo；否则为错误对象。 |

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                              |
| -------- | ------------------------------------- |
| 201 | Permission denied. |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
| 17700001 | The specified bundleName is not found. |
| 17700004 | The specified user ID is not found.     |
| 17700026 | The specified bundle is disabled.      |

**示例：**

```ts
// 额外获取AbilityInfo
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';
let bundleName = 'com.example.myapplication';
let bundleFlags = bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_HAP_MODULE | bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_ABILITY;
let userId = 100;

try {
    bundleManager.getBundleInfo(bundleName, bundleFlags, userId, (err, data) => {
        if (err) {
            hilog.error(0x0000, 'testTag', 'getBundleInfo failed: %{public}s', err.message);
        } else {
            hilog.info(0x0000, 'testTag', 'getBundleInfo successfully: %{public}s', JSON.stringify(data));
        }
    });
} catch (err) {
    let message = (err as BusinessError).message;
    hilog.error(0x0000, 'testTag', 'getBundleInfo failed: %{public}s', message);
}
```

```ts
// 额外获取ApplicationInfo中的metadata
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';
let bundleName = 'com.example.myapplication';
let bundleFlags = bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_APPLICATION | bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_METADATA;
let userId = 100;

try {
    bundleManager.getBundleInfo(bundleName, bundleFlags, userId, (err, data) => {
        if (err) {
            hilog.error(0x0000, 'testTag', 'getBundleInfo failed: %{public}s', err.message);
        } else {
            hilog.info(0x0000, 'testTag', 'getBundleInfo successfully: %{public}s', JSON.stringify(data));
        }
    });
} catch (err) {
    let message = (err as BusinessError).message;
    hilog.error(0x0000, 'testTag', 'getBundleInfo failed: %{public}s', message);
}
```

### bundleManager.getBundleInfo<sup>14+</sup>

getBundleInfo(bundleName: string, bundleFlags: number, callback: AsyncCallback\<BundleInfo>): void

根据给定的bundleName和bundleFlags获取BundleInfo，使用callback异步回调。

获取调用方自己的信息时不需要权限。

**需要权限：** ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名     | 类型   | 必填 | 说明                       |
| ----------- | ------ | ---- | ---------------------------- |
| bundleName  | string | 是   | 表示要查询的应用Bundle名称。 |
| [bundleFlags](js-apis-bundleManager.md#bundleflag) | number | 是   | 指定返回的BundleInfo所包含的信息。|
| callback | AsyncCallback\<[BundleInfo](js-apis-bundleManager-bundleInfo.md)> | 是 | 回调函数，当获取成功时，err为null，data为获取到的BundleInfo；否则为错误对象。 |

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                              |
| -------- | ------------------------------------- |
| 201 | Permission denied. |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
| 17700001 | The specified bundleName is not found. |
| 17700026 | The specified bundle is disabled.      |

**示例：**

```ts
// 额外获取extensionAbility
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';
let bundleName = 'com.example.myapplication';
let bundleFlags = bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_HAP_MODULE | bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_EXTENSION_ABILITY;

try {
    bundleManager.getBundleInfo(bundleName, bundleFlags, (err, data) => {
        if (err) {
            hilog.error(0x0000, 'testTag', 'getBundleInfo failed: %{public}s', err.message);
        } else {
            hilog.info(0x0000, 'testTag', 'getBundleInfo successfully: %{public}s', JSON.stringify(data));
        }
    });
} catch (err) {
    let message = (err as BusinessError).message;
    hilog.error(0x0000, 'testTag', 'getBundleInfo failed: %{public}s', message);
}
```

### bundleManager.getBundleInfo<sup>14+</sup>

getBundleInfo(bundleName: string, bundleFlags: number, userId?: number): Promise\<BundleInfo>

根据给定的bundleName、bundleFlags和userId获取BundleInfo，使用Promise异步回调。

获取调用方自己的信息时不需要权限。

**需要权限：** ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名     | 类型   | 必填 | 说明                       |
| ----------- | ------ | ---- | ---------------------------- |
| bundleName  | string | 是   | 表示要查询的应用Bundle名称。 |
| [bundleFlags](js-apis-bundleManager.md#bundleflag) | number | 是   | 指定返回的BundleInfo所包含的信息。       |
| userId      | number | 否   | 表示用户ID，默认值：调用方所在用户，取值范围：大于等于0。  |

**返回值：**

| 类型                                                        | 说明                        |
| ----------------------------------------------------------- | --------------------------- |
| Promise\<[BundleInfo](js-apis-bundleManager-bundleInfo.md)> | Promise对象，返回BundleInfo。 |

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                            |
| -------- | --------------------------------------|
| 201 | Permission denied. |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
| 17700001 | The specified bundleName is not found. |
| 17700004 | The specified user ID is not found.     |
| 17700026 | The specified bundle is disabled.      |

**示例：**

```ts
// 额外获取ApplicationInfo和SignatureInfo
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';
let bundleName = 'com.example.myapplication';
let bundleFlags = bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_APPLICATION | bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_SIGNATURE_INFO;
let userId = 100;

try {
    bundleManager.getBundleInfo(bundleName, bundleFlags, userId).then((data) => {
        hilog.info(0x0000, 'testTag', 'getBundleInfo successfully. Data: %{public}s', JSON.stringify(data));
    }).catch((err: BusinessError) => {
        hilog.error(0x0000, 'testTag', 'getBundleInfo failed. Cause: %{public}s', err.message);
    });
} catch (err) {
    let message = (err as BusinessError).message;
    hilog.error(0x0000, 'testTag', 'getBundleInfo failed. Cause: %{public}s', message);
}
```

```ts
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';
let bundleName = 'com.example.myapplication';
let bundleFlags = bundleManager.BundleFlag.GET_BUNDLE_INFO_DEFAULT;

try {
    bundleManager.getBundleInfo(bundleName, bundleFlags).then((data) => {
        hilog.info(0x0000, 'testTag', 'getBundleInfo successfully. Data: %{public}s', JSON.stringify(data));
    }).catch((err: BusinessError) => {
        hilog.error(0x0000, 'testTag', 'getBundleInfo failed. Cause: %{public}s', err.message);
    });
} catch (err) {
    let message = (err as BusinessError).message;
    hilog.error(0x0000, 'testTag', 'getBundleInfo failed. Cause: %{public}s', message);
}

```

### bundleManager.getBundleInfoSync<sup>14+</sup>

getBundleInfoSync(bundleName: string, bundleFlags: number, userId: number): BundleInfo

以同步方法根据给定的bundleName、bundleFlags和userId获取BundleInfo。

获取调用方自己的信息时不需要权限。

**需要权限：** ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名       | 类型   | 必填 | 说明                                                     |
| ----------- | ------ | ---- | -------------------------------------------------------- |
| bundleName  | string | 是   | 表示应用程序的bundleName。                                 |
| [bundleFlags](js-apis-bundleManager.md#bundleflag) | number | 是   | 表示用于指定将返回的BundleInfo对象中包含的信息的标志。 |
| userId      | number | 是   | 表示用户ID。                                             |

**返回值：**

| 类型       | 说明                 |
| ---------- | -------------------- |
| [BundleInfo](js-apis-bundleManager-bundleInfo.md) | 返回BundleInfo对象。 |

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                             |
| -------- | ------------------------------------- |
| 201 | Permission denied. |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
| 17700001 | The specified bundleName is not found. |
| 17700004 | The specified user ID is not found.     |
| 17700026 | The specified bundle is disabled.      |

**示例：**

```ts
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';
let bundleName = 'com.example.myapplication';
let bundleFlags = bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION;
let userId = 100;

try {
    let data = bundleManager.getBundleInfoSync(bundleName, bundleFlags, userId);
    hilog.info(0x0000, 'testTag', 'getBundleInfoSync successfully: %{public}s', JSON.stringify(data));
} catch (err) {
    let message = (err as BusinessError).message;
    hilog.error(0x0000, 'testTag', 'getBundleInfoSync failed: %{public}s', message);
}
```

### bundleManager.getBundleInfoSync<sup>14+</sup>

getBundleInfoSync(bundleName: string, bundleFlags: number): BundleInfo

以同步方法根据给定的bundleName、bundleFlags获取BundleInfo。

获取调用方自己的信息时不需要权限。

**需要权限：** ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                                                   |
| ----------- | --------------------- | ---- | ------------------------------------------------------ |
| bundleName  | string                | 是   | 表示应用程序的bundleName。                             |
| [bundleFlags](js-apis-bundleManager.md#bundleflag) | number | 是   | 表示用于指定将返回的BundleInfo对象中包含的信息的标志。 |

**返回值：**

| 类型                                              | 说明                 |
| ------------------------------------------------- | -------------------- |
| [BundleInfo](js-apis-bundleManager-bundleInfo.md) | 返回BundleInfo对象。 |

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                               |
| -------- | -------------------------------------- |
| 201 | Permission denied. |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
| 17700001 | The specified bundleName is not found. |
| 17700026 | The specified bundle is disabled.      |

**示例：**

```ts
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';
let bundleName = 'com.example.myapplication';
let bundleFlags = bundleManager.BundleFlag.GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION;
try {
    let data = bundleManager.getBundleInfoSync(bundleName, bundleFlags);
    hilog.info(0x0000, 'testTag', 'getBundleInfoSync successfully: %{public}s', JSON.stringify(data));
} catch (err) {
    let message = (err as BusinessError).message;
    hilog.error(0x0000, 'testTag', 'getBundleInfoSync failed: %{public}s', message);
}
```

### bundleManager.getBundleNameByUid<sup>14+</sup>

getBundleNameByUid(uid: number, callback: AsyncCallback\<string>): void

根据给定的uid获取对应的bundleName，使用callback异步回调。

**需要权限：** ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名   | 类型                   | 必填 | 说明                                                         |
| -------- | ---------------------- | ---- | ------------------------------------------------------------ |
| uid      | number                 | 是   | 表示应用程序的UID。                                            |
| callback | AsyncCallback\<string> | 是   | 回调函数，当获取成功时，err为null，data为获取到的BundleName；否则为错误对象。 |

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息            |
| -------- | --------------------- |
| 201 | Permission denied. |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
| 17700021 | The uid is not found. |

**示例：**

```ts
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';
let uid = 20010005;
try {
    bundleManager.getBundleNameByUid(uid, (err, data) => {
        if (err) {
            hilog.error(0x0000, 'testTag', 'getBundleNameByUid failed: %{public}s', err.message);
        } else {
            hilog.info(0x0000, 'testTag', 'getBundleNameByUid successfully: %{public}s', JSON.stringify(data));
        }
    });
} catch (err) {
    let message = (err as BusinessError).message;
    hilog.error(0x0000, 'testTag', 'getBundleNameByUid failed: %{public}s', message);
}
```

### bundleManager.getBundleNameByUid<sup>14+</sup>

getBundleNameByUid(uid: number): Promise\<string>

根据给定的uid获取对应的bundleName，使用Promise异步回调。

**需要权限：** ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明                |
| ---- | ------ | ---- | ------------------ |
| uid  | number | 是   | 表示应用程序的UID。 |

**返回值：**

| 类型             | 说明                        |
| ---------------- | --------------------------- |
| Promise\<string> | Promise对象，返回bundleName。 |

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息            |
| -------- | ---------------------|
| 201 | Permission denied. |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
| 17700021 | The uid is not found. |

**示例：**

```ts
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';
let uid = 20010005;
try {
    bundleManager.getBundleNameByUid(uid).then((data) => {
        hilog.info(0x0000, 'testTag', 'getBundleNameByUid successfully. Data: %{public}s', JSON.stringify(data));
    }).catch((err: BusinessError) => {
        hilog.error(0x0000, 'testTag', 'getBundleNameByUid failed. Cause: %{public}s', err.message);
    });
} catch (err) {
    let message = (err as BusinessError).message;
    hilog.error(0x0000, 'testTag', 'getBundleNameByUid failed. Cause: %{public}s', message);
}
```

### bundleManager.getBundleNameByUidSync<sup>14+</sup>

getBundleNameByUidSync(uid: number): string

以同步方法根据给定的uid获取对应的bundleName。

**需要权限：** ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明                |
| ---- | ------ | ---- | ------------------ |
| uid  | number | 是   | 表示应用程序的UID。 |

**返回值：**

| 类型             | 说明                        |
| ---------------- | --------------------------- |
| string | 返回获取到的bundleName。 |

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息            |
| -------- | ---------------------|
| 201 | Permission denied. |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
| 17700021 | The uid is not found. |

**示例：**

```ts
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';
let uid = 20010005;
try {
    let data = bundleManager.getBundleNameByUidSync(uid);
    hilog.info(0x0000, 'testTag', 'getBundleNameByUidSync successfully. Data: %{public}s', JSON.stringify(data));
} catch (err) {
    let message = (err as BusinessError).message;
    hilog.error(0x0000, 'testTag', 'getBundleNameByUidSync failed. Cause: %{public}s', message);
}
```

### bundleManager.getAppCloneIdentity<sup>14+</sup>

getAppCloneIdentity(uid: number): Promise\<AppCloneIdentity>;

根据uid查询分身应用的bundleName和appIndex。使用Promise异步回调。

**需要权限：** ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名     | 类型   | 必填 | 说明                       |
| ---------- | ------ | ---- | ---------------------------|
|    uid     | number |  是  |     表示应用程序的UID。      |

**返回值：**

| 类型                                                        | 说明                        |
| ----------------------------------------------------------- | --------------------------- |
| Promise\<AppCloneIdentity> | 以Promise方式返回\<AppCloneIdentity>。 |

**错误码：**

以下错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[ohos.bundle错误码](errorcode-bundle.md)。

| 错误码ID | 错误信息                            |
| -------- | --------------------------------------|
| 201 | Permission denied. |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
| 17700021 | The uid is not found. |

**示例：**

```ts
import { bundleManager } from '@kit.AbilityKit';
import { BusinessError } from '@kit.BasicServicesKit';
import { hilog } from '@kit.PerformanceAnalysisKit';
let uid = 20010005;

try {
    bundleManager.getAppCloneIdentity(uid).then((res) => {
        hilog.info(0x0000, 'testTag', 'getAppCloneIdentity res = %{public}s', JSON.stringify(res));
    }).catch((err: BusinessError) => {
        hilog.error(0x0000, 'testTag', 'getAppCloneIdentity failed. Cause: %{public}s', err.message);
    });
} catch (err) {
    let message = (err as BusinessError).message;
    hilog.error(0x0000, 'testTag', 'getAppCloneIdentity failed. Cause: %{public}s', message);
}
```

### ApplicationInfo

type ApplicationInfo = _ApplicationInfo

应用程序信息。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 类型                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [_ApplicationInfo](js-apis-bundleManager-applicationInfo.md#applicationinfo-1) | 应用程序信息。 |

### ModuleMetadata<sup>10+</sup>

type ModuleMetadata = _ModuleMetadata

模块的元数据信息。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 类型                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [_ModuleMetadata](js-apis-bundleManager-applicationInfo.md#ModuleMetadata10) | 模块的元数据信息。 |

### Metadata

type Metadata = _Metadata

元数据信息。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力**: SystemCapability.BundleManager.BundleFramework.Core

| 类型                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [_Metadata](js-apis-bundleManager-metadata.md#metadata) | 元数据信息。 |

### BundleInfo

type BundleInfo = _BundleInfo.BundleInfo

应用包信息。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力**: SystemCapability.BundleManager.BundleFramework.Core

| 类型                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [_BundleInfo.BundleInfo](js-apis-bundleManager-bundleInfo.md#bundleinfo) | 应用包信息。 |


### UsedScene

type UsedScene = _BundleInfo.UsedScene

权限使用的场景和时机。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力:** SystemCapability.BundleManager.BundleFramework.Core

| 类型                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [_BundleInfo.UsedScene](js-apis-bundleManager-bundleInfo.md#usedscene) | 权限使用的场景和时机。 |

### ReqPermissionDetail

type ReqPermissionDetail = _BundleInfo.ReqPermissionDetail

应用运行时需向系统申请的权限集合的详细信息。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力:** SystemCapability.BundleManager.BundleFramework.Core

| 类型                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [_BundleInfo.ReqPermissionDetail](js-apis-bundleManager-bundleInfo.md#reqpermissiondetail) | 应用运行时需向系统申请的权限集合的详细信息。 |

### SignatureInfo

type SignatureInfo = _BundleInfo.SignatureInfo

应用包的签名信息。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 类型                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [_BundleInfo.SignatureInfo](js-apis-bundleManager-bundleInfo.md#signatureinfo) | 应用包的签名信息。 |

### HapModuleInfo

type HapModuleInfo = _HapModuleInfo.HapModuleInfo

HAP信息。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 类型                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [_HapModuleInfo.HapModuleInfo](js-apis-bundleManager-hapModuleInfo.md#hapmoduleinfo-1) | HAP信息。 |

### PreloadItem

type PreloadItem = _HapModuleInfo.PreloadItem

原子化服务中模块的预加载模块信息。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力:** SystemCapability.BundleManager.BundleFramework.Core

| 类型                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [_HapModuleInfo.PreloadItem](js-apis-bundleManager-hapModuleInfo.md#preloaditem) | 原子化服务中模块的预加载模块信息。 |

### Dependency

type Dependency = _HapModuleInfo.Dependency

模块所依赖的动态共享库信息。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 类型                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [_HapModuleInfo.Dependency](js-apis-bundleManager-hapModuleInfo.md#dependency) | 模块所依赖的动态共享库信息。 |

### RouterItem<sup>12+</sup>

type RouterItem = _HapModuleInfo.RouterItem

模块配置的路由表信息。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 类型                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [_HapModuleInfo.RouterItem](js-apis-bundleManager-hapModuleInfo.md#routeritem12) | 模块配置的路由表信息。 |

### DataItem<sup>12+</sup>

type DataItem = _HapModuleInfo.DataItem

模块配置的路由表中的自定义数据。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 类型                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [_HapModuleInfo.DataItem](js-apis-bundleManager-hapModuleInfo.md#dataitem12) | 模块配置的路由表中的自定义数据。 |

### AbilityInfo

type AbilityInfo = _AbilityInfo.AbilityInfo

Ability信息。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 类型                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [_AbilityInfo.AbilityInfo](js-apis-bundleManager-abilityInfo.md#abilityinfo-1) |Ability信息。 |

### WindowSize

type WindowSize = _AbilityInfo.WindowSize

窗口尺寸。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 类型                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [_AbilityInfo.WindowSize](js-apis-bundleManager-abilityInfo.md#windowsize) |窗口尺寸。 |


### ExtensionAbilityInfo

type ExtensionAbilityInfo = _ExtensionAbilityInfo.ExtensionAbilityInfo

ExtensionAbility信息。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 类型                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [_ExtensionAbilityInfo.ExtensionAbilityInfo](js-apis-bundleManager-extensionAbilityInfo.md#extensionabilityinfo-1) |ExtensionAbility信息。 |

### ElementName

type ElementName = _ElementName

ElementName信息。

**原子化服务API：** 从API version 11开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 类型                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [_ElementName](js-apis-bundleManager-elementName.md#elementname-1) |ElementName信息。 |

### Skill<sup>12+</sup>

type Skill = _Skill.Skill

skill信息。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 类型                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [_Skill.Skill](js-apis-bundleManager-skill.md#skill-1) |skill信息。 |

### SkillUrl<sup>12+</sup>

type SkillUrl = _Skill.SkillUri

SkillUri信息。

**原子化服务API：** 从API version 12开始，该接口支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

| 类型                                                         | 说明           |
| ------------------------------------------------------------ | -------------- |
| [_Skill.SkillUri](js-apis-bundleManager-skill.md#skilluri) |SkillUri信息。 |
