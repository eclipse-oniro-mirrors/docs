# @ohos.app.ability.quickFixManager (quickFixManager)

quickFixManager模块提供快速修复的能力，快速修复是OpenHarmony提供给开发者的一种技术手段，支持开发者以远快于（小时级、分钟级）应用升级的方式进行缺陷修复。

> **说明：**
>
> 本模块首批接口从API version 9 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import quickFixManager from '@ohos.app.ability.quickFixManager';
```

## HapModuleQuickFixInfo

hap级别的快速修复信息。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.QuickFix

**系统API**: 此接口为系统接口，三方应用不支持调用。

| 名称        | 类型                 | 必填 | 说明                                                         |
| ----------- | -------------------- | ---- | ------------------------------------------------------------ |
| moduleName    | string               | 是   | hap包的名称。                               |
| originHapHash    | string               | 是   | 指示hap的哈希值。                               |
| quickFixFilePath    | string               | 是   | 指示快速修复文件的安装路径。                               |

## ApplicationQuickFixInfo

应用级别的快速修复信息。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.QuickFix

**系统API**: 此接口为系统接口，三方应用不支持调用。

| 名称        | 类型                 | 必填 | 说明                                                         |
| ----------- | -------------------- | ---- | ------------------------------------------------------------ |
| bundleName    | string               | 是   | 应用的包名。                               |
| bundleVersionCode    | number               | 是   | 应用的版本号。                               |
| bundleVersionName    | string               | 是   | 应用版本号的文字描述。                               |
| quickFixVersionCode    | number               | 是   | 快速修复补丁包的版本号。                               |
| quickFixVersionName    | string               | 是   | 快速修复补丁包版本号的文字描述。                               |
| hapModuleQuickFixInfo    | Array\<[HapModuleQuickFixInfo](#hapmodulequickfixinfo)>      | 是   | hap级别的快速修复信息。     |

## quickFixManager.applyQuickFix

applyQuickFix(hapModuleQuickFixFiles: Array\<string>, callback: AsyncCallback\<void>): void;

快速修复的补丁安装接口。

**需要权限**: ohos.permission.INSTALL_BUNDLE

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.QuickFix

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | hapModuleQuickFixFiles | Array\<string> | 是 | 快速修复补丁文件（补丁文件需包含有效的文件路径）。 |
  | callback | AsyncCallback\<void> | 是 | 表示指定的回调方法。 |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 18500002 | The specified quick fix is invalid. It may not exist or inaccessible. |
| 18500008 | Internal error. |

在打补丁过程中发生的错误，其错误码及错误信息通过公共事件[COMMON_EVENT_QUICK_FIX_APPLY_RESULT](commonEventManager-definitions.md#common_event_quick_fix_apply_result-9)的参数返回给应用开发者。这部分错误码及错误信息如下：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 18500003 | Deploy hqf failed. |
| 18500004 | Switch hqf failed. |
| 18500005 | Delete hqf failed. |
| 18500006 | Load patch failed. |
| 18500007 | Unload patch failed. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

> 说明：调用applyQuickFix接口时，补丁文件所在路径为应用沙箱路径。沙箱路径的获取参考[获取应用的沙箱路径](js-apis-bundle-BundleInstaller.md#获取应用的沙箱路径)，映射到设备上的路径为/proc/&lt;应用进程Id&gt;/root/沙箱路径。

**示例：**

```ts
  import quickFixManager from '@ohos.app.ability.quickFixManager';

  try {
    let hapModuleQuickFixFiles = ['/data/storage/el2/base/entry.hqf'];
    quickFixManager.applyQuickFix(hapModuleQuickFixFiles, (error) => {
      if (error) {
          console.info( `applyQuickFix failed with error + ${error}`);
      } else {
          console.info( 'applyQuickFix success');
      }
    });
  } catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
  }
```

## quickFixManager.applyQuickFix

applyQuickFix(hapModuleQuickFixFiles: Array\<string>): Promise\<void>;

快速修复的补丁安装接口。

**需要权限**: ohos.permission.INSTALL_BUNDLE

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.QuickFix

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | hapModuleQuickFixFiles | Array\<string> | 是 | 快速修复补丁文件（补丁文件需包含有效的文件路径）。 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise\<void> | 返回相应结果。 |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 18500002 | The specified quick fix is invalid. It may not exist or inaccessible. |
| 18500008 | Internal error. |

在打补丁过程中发生的错误，其错误码及错误信息通过公共事件[COMMON_EVENT_QUICK_FIX_APPLY_RESULT](commonEventManager-definitions.md#common_event_quick_fix_apply_result-9)的参数返回给应用开发者。这部分错误码及错误信息如下：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 18500003 | Deploy hqf failed. |
| 18500004 | Switch hqf failed. |
| 18500005 | Delete hqf failed. |
| 18500006 | Load patch failed. |
| 18500007 | Unload patch failed. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
  import quickFixManager from '@ohos.app.ability.quickFixManager';

  let hapModuleQuickFixFiles = ['/data/storage/el2/base/entry.hqf'];
  try {
    quickFixManager.applyQuickFix(hapModuleQuickFixFiles).then(() => {
      console.info('applyQuickFix success');
    }).catch((error) => {
      console.info(`applyQuickFix err: + ${error}`);
    });
  } catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
  }
```

## quickFixManager.getApplicationQuickFixInfo

getApplicationQuickFixInfo(bundleName: string, callback: AsyncCallback\<ApplicationQuickFixInfo>): void;

获取应用的快速修复信息。

**需要权限**: ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.QuickFix

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 | 
  | -------- | -------- | -------- | -------- |
  | bundleName | string | 是 |应用的包名。  | 
  | callback | AsyncCallback\<[ApplicationQuickFixInfo](#applicationquickfixinfo)> | 是 | 应用的快速修复信息。 | 

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 18500001 | The specified bundleName is invalid. |
| 18500008 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**

```ts
  import quickFixManager from '@ohos.app.ability.quickFixManager';

  try {
    let bundleName = 'bundleName'
    quickFixManager.getApplicationQuickFixInfo(bundleName, (error, data) => {
      if (error) {
        console.info(`getApplicationQuickFixInfo error: + ${error}`);
      } else {
        console.info(`getApplicationQuickFixInfo success: + ${data}`);
      }
    });
  } catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
  }
```

## quickFixManager.getApplicationQuickFixInfo

getApplicationQuickFixInfo(bundleName: string): Promise\<ApplicationQuickFixInfo>;

获取应用的快速修复信息。

**需要权限**: ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.QuickFix

**系统API**: 此接口为系统接口，三方应用不支持调用。

**参数：**

  | 参数名 | 类型 | 必填 | 说明 | 
  | -------- | -------- | -------- | -------- |
  | bundleName | string | 是 | 应用的包名。  | 

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise\<[ApplicationQuickFixInfo](#applicationquickfixinfo)> | 返回应用的快速修复信息。 |

**错误码**：

| 错误码ID | 错误信息 |
| ------- | -------- |
| 18500001 | The specified bundleName is invalid. |
| 18500008 | Internal error. |

以上错误码详细介绍请参考[errcode-ability](../errorcodes/errorcode-ability.md)。

**示例：**
    
  ```ts 
  import quickFixManager from '@ohos.app.ability.quickFixManager';

  try {
    let bundleName = 'bundleName';
    quickFixManager.getApplicationQuickFixInfo(bundleName).then((data) => {
      console.info(`getApplicationQuickFixInfo success: + ${data}`);
    }).catch((error) => {
      console.info(`getApplicationQuickFixInfo err: + ${error}`);
    });
  } catch (paramError) {
    console.log('error: ' + paramError.code + ', ' + paramError.message);
  }
```
