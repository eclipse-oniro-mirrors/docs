# 应用接入数据备份恢复

应用接入数据备份恢复需要通过BackupExtensionAbility实现。

BackupExtensionAbility，是[Stage模型](../application-models/stage-model-development-overview.md)中扩展组件[ExtensionAbility](../application-models/extensionability-overview.md)的派生类。开发者可以通过修改配置文件定制备份恢复框架的行为，包括是否允许备份恢复，备份哪些文件等。

## 接口说明

| 模块        | 类名                   | 接口                                          | 接口描述                                                          |
| ----------- | ---------------------- | --------------------------------------------- | ----------------------------------------------------------------- |
| application | BundleVersion          | code: number                                  | 应用版本号。                                                      |
| application | BundleVersion          | name: string                                  | 应用版本名称。                                                    |
| application | BackupExtensionAbility | onBackup(): void                              | 由Extension机制提供的，应由应用开发者扩展实现的触发备份前的回调。 |
| application | BackupExtensionAbility | onRestore(bundleVersion: BundleVersion): void | 由Extension机制提供的，应由应用开发者扩展实现的触发恢复后的回调。 |
| application | BackupExtensionAbility | context: ExtensionContext                     | BackupExtensionAbility的上下文环境，继承自Context。               |

备份恢复扩展能力API的使用指导请参见[API参考](../reference/apis-core-file-kit/js-apis-application-backupExtensionAbility.md#backupextensionability)。

## 约束与限制

- 当备份恢复时，所有待备份文件及目录的路径不得超过4095字节，否则将导致未定义行为。
- 当备份目录时，应用进程必须拥有读取该目录及其所有子目录的权限（DAC中的`r`），否则将导致备份失败。
- 当备份文件时，应用进程必须拥有搜索该文件所有祖父级目录的权限（DAC中的`x`），否则将导致备份失败。

## 开发步骤

1. 在应用配置文件`module.json5`中注册`extensionAbilities`相关配置

   新增`"extensionAbilities"`字段，其中注册类型`"type"`设置为`"backup"`，元数据信息["metadata"](../reference/apis-ability-kit/js-apis-bundleManager-metadata.md)新增一个`"name"`为`"ohos.  extension. backup"`的条目。

   BackupExtensionAbility配置文件示例：

   ```json
   {
       "extensionAbilities": [
           {
               "description": "$string:ServiceExtAbility",
               "icon": "$media:icon",
               "name": "BackupExtensionAbility",
               "type": "backup",
               "visible": true,
               "metadata": [
                   {
                       "name": "ohos.extension.backup",
                       "resource": "$profile:backup_config"
                   }
               ],
               // 在BackupExtension.ts文件里自定义继承BackupExtensionAbility，重写其中的onBackup和onRestore方法。
               // 如果没有特殊要求可以空实现，则备份恢复服务会按照统一的备份恢复数据规则进行备份恢复。
               "srcEntrance": "./ets/BackupExtension/BackupExtension.ts", 
           }      
       ]
   }
   ```

2. 新增元数据资源配置文件

   在元数据资源配置文件中，定义备份恢复时需要传输的文件。元数据资源配置文件名称需要与`module.json5`中`"metadata.resource"`名称保持一致，其保存位置在工程的`resources/profile`文件夹下。

   元数据资源配置文件示例：

   ```json
   {
       "allowToBackupRestore": true,
       "includes": [
           "/data/storage/el2/base/files/users/"
       ],
       "excludes": [
           "/data/storage/el2/base/files/users/hidden/"
       ],
       "fullBackupOnly": false,
       "restoreDeps": "",
   }
   ```

3. 开发者可以在`BackupExtension.ts`文件中自定义类继承的`BackupExtensionAbility`，通过重写其`onBackup`和`onRestore`方法，使其达到在备份预加工应用数据或者在恢复阶段加工待恢复文件。

   如果没有特殊要求可以空实现，则备份恢复服务会按照统一的备份恢复数据规则进行备份恢复。

   下面的示例展示了一个空实现的`BackupExtension.ts`文件。

    ```ts
    import BackupExtensionAbility, {BundleVersion} from '@ohos.application.BackupExtensionAbility';
    import {hilog} from '@Kit.PerformanceAnalysisKit';
    
    const TAG = `FileBackupExtensionAbility`;
    export default class BackupExtension extends  BackupExtensionAbility {
      async onBackup ()   {
        hilog.info(TAG, `onBackup ok`);
      }

      async onRestore (bundleVersion : BundleVersion) {
        hilog.info(TAG, `onRestore ok ${JSON.stringify(bundleVersion)}`);
        hilog.info(TAG, `onRestore end`);
      }
    }
    ```

### 元数据资源配置文件说明

| 属性名称             | 数据类型   | 必填 | 含义                                                                                                                                                                                            |
| -------------------- | ---------- | ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| allowToBackupRestore | 布尔值     | 是   | 是否允许备份恢复，默认为false。                                                                                                                                                                 |
| includes             | 字符串数组 | 否   | 应用沙箱中需要备份的文件和目录。<br>当模式串以非/开始时，表示一个相对于根路径的相对路径。<br>当`includes`已配置时，备份恢复框架会采用开发者配置的模式串，否则将会采用下述代码段内容作为默认值。 |
| excludes             | 字符串数组 | 否   | `includes`中无需备份的例外项。格式同`includes`。<br>当`excludes`已配置时，备份恢复框架会采用开发者配置的模式串，否则将会采用**空数组**作为默认值。                                              |
| fullBackupOnly       | 布尔值     | 否   | 是否使用应用默认恢复目录，默认值为false。当值为true时，恢复数据会以 **/data/storage/el2/backup/restore/** 为根目录解压数据。<br>当值为false或者不配置该字段时，恢复数据会以/为根目录解压数据。   |
| restoreDeps          | 字符串     | 否   | 应用恢复时依赖其他应用数据，默认值为""，需要配置的依赖应用名称，多个应用以 **,** 分隔。                                                                                                           |

> **说明：**
> 
> **有关fullBackupOnly字段的说明**
> - 当fullBackupOnly为false时，恢复的数据意味着会对同路径下的同名文件进行覆盖。
> - 当fullBackupOnly为true时，恢复数据会以 **/data/storage/el2/backup/restore/** 为根目录解压数据，开发者可在OnRestore内访问数据进行最终的恢复。
>
> 开发者可根据自身的业务场景，选择对应的恢复数据方式。如果配置了fullBackupOnly为true，那么开发者需要在OnRestore内自行实现恢复数据的逻辑。
>
> 举个例子：假设应用的数据备份路径为：**data/storage/el2/base/files/A/** 。那么在恢复时，数据会被解压到：**/data/storage/el2/backup/restore/data/storage/el2/base/files/A/** 目录下。

**includes默认值：**

```json
{
    "includes": [
    "data/storage/el1/database/",
    "data/storage/el1/base/files/",
    "data/storage/el1/base/preferences/",
    "data/storage/el1/base/haps/<module-name>/files/",
    "data/storage/el1/base/haps/<module-name>/preferences/",
    "data/storage/el2/database/",
    "data/storage/el2/base/files/",
    "data/storage/el2/base/preferences/",
    "data/storage/el2/base/haps/<module-name>/files/",
    "data/storage/el2/base/haps/<module-name>/preferences/",
    "data/storage/el2/distributedfiles/"
    ]
}
```

## 相关实例

针对应用接入数据的备份与恢复，有以下相关实例可供参考：

- [应用接入数据备份恢复（ArkTS）（Full SDK）（API10）](https://gitee.com/openharmony/applications_app_samples/tree/master/code/BasicFeature/FileManagement/FileBackupExtension)
