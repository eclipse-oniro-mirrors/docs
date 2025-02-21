# @ohos.file.storageStatistics (应用空间统计)

该模块提供空间查询相关的常用功能：包括对内外卡的空间查询，对应用分类数据统计的查询，对应用数据的查询等。

> **说明：**
>
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import  { storageStatistics } from '@kit.CoreFileKit';
```

## storageStatistics.getCurrentBundleStats<sup>9+</sup>

getCurrentBundleStats(): Promise&lt;BundleStats&gt;

应用异步获取当前应用存储空间大小（单位为Byte），以Promise方式返回。

**系统能力**：SystemCapability.FileManagement.StorageService.SpatialStatistics

**返回值：**

  | 类型                                        | 说明                       |
  | ------------------------------------------ | -------------------------- |
  | Promise&lt;[Bundlestats](#bundlestats9)&gt; | Promise对象，返回指定卷上的应用存储空间大小（单位为Byte）      |

**错误码：**

以下错误码的详细介绍请参见[文件管理错误码](errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 401 | The input parameter is invalid. Possible causes: Mandatory parameters are left unspecified. |
| 13600001 | IPC error. |
| 13900042 | Unknown error. |

**示例：**

  ```ts
  import { BusinessError } from '@kit.BasicServicesKit';
  storageStatistics.getCurrentBundleStats().then((BundleStats: storageStatistics.BundleStats) => {
    console.info("getCurrentBundleStats successfully:" + JSON.stringify(BundleStats));
  }).catch((err: BusinessError) => {
    console.error("getCurrentBundleStats failed with error:"+ JSON.stringify(err));
  });
  ```

## storageStatistics.getCurrentBundleStats<sup>9+</sup>

getCurrentBundleStats(callback: AsyncCallback&lt;BundleStats&gt;): void

应用异步获取当前应用存储空间大小（单位为Byte），以callback方式返回。

**系统能力**：SystemCapability.FileManagement.StorageService.SpatialStatistics

**参数：**

  | 参数名    | 类型                                                       | 必填  | 说明                                 |
  | -------- | --------------------------------------------------------- | ---- | ------------------------------------ |
  | callback | AsyncCallback&lt;[BundleStats](#bundlestats9)&gt;          | 是   | 获取指定卷上的应用存储空间大小之后的回调        |

**错误码：**

以下错误码的详细介绍请参见[文件管理错误码](errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | -------- |
| 401 | The input parameter is invalid. Possible causes: Mandatory parameters are left unspecified. |
| 13600001 | IPC error. |
| 13900042 | Unknown error. |

**示例：**

  ```ts
  import { BusinessError } from '@kit.BasicServicesKit';
  storageStatistics.getCurrentBundleStats((error: BusinessError, bundleStats: storageStatistics.BundleStats) => {
    if (error) {
      console.error("getCurrentBundleStats failed with error:" + JSON.stringify(error));
    } else {
      // do something
      console.info("getCurrentBundleStats successfully:" + JSON.stringify(bundleStats));
    }
  });
  ```

## BundleStats<sup>9+</sup>

**系统能力**：SystemCapability.FileManagement.StorageService.SpatialStatistics

| 名称      | 类型   | 必填 | 说明           |
| --------- | ------ | --- | -------------- |
| appSize   | number | 是 | 应用安装文件大小（单位为Byte）    |
| cacheSize | number | 是 | 应用缓存文件大小（单位为Byte）   |
| dataSize  | number | 是 | 应用文件存储大小（除应用安装文件和缓存文件）（单位为Byte） |
