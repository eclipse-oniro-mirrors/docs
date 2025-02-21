# @ohos.statfs (statfs)

该模块提供文件系统相关存储信息的功能，向应用程序提供获取文件系统总字节数、空闲字节数的JS接口。

> **说明：**
>
> - 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> - 本模块从API version 9开始废弃，建议使用[@ohos.file.statvfs](js-apis-file-statvfs.md)替代。

## 导入模块

```ts
import statfs from '@ohos.statfs';
```

## statfs.getFreeBytes

getFreeBytes(path:string):Promise&lt;number&gt;

异步方法获取指定文件系统空闲字节数，以Promise形式返回结果。

**系统能力**：SystemCapability.FileManagement.File.FileIO

**参数：**

  | 参数名 | 类型   | 必填 | 说明                         |
  | ------ | ------ | ---- | ---------------------------- |
  | path   | string | 是   | 需要查询的文件系统的文件路径 |

**返回值：**

  | 类型                  | 说明           |
  | --------------------- | -------------- |
  | Promise&lt;number&gt; | 返回空闲字节数 |

**示例：**

  ```ts
  import { BusinessError } from '@ohos.base';
  let path = "/dev";
  statfs.getFreeBytes(path).then((number: number) => {
    console.info("getFreeBytes promise successfully:" + number);
  }).catch((err: BusinessError) => {
    console.info("getFreeBytes failed with error:" + JSON.stringify(err));
  });
  ```

## statfs.getFreeBytes

getFreeBytes(path:string, callback:AsyncCallback&lt;number&gt;): void

异步方法获取指定文件系统空闲字节数，使用callback形式返回结果。

**系统能力**：SystemCapability.FileManagement.File.FileIO

**参数：**

  | 参数名   | 类型                        | 必填 | 说明                         |
  | -------- | --------------------------- | ---- | ---------------------------- |
  | path     | string                      | 是   | 需要查询的文件系统的文件路径 |
  | callback | AsyncCallback&lt;number&gt; | 是   | 异步获取空闲字节数之后的回调 |

**示例：**

  ```ts
  import common from '@ohos.app.ability.common';
  let context = getContext(this) as common.UIAbilityContext;
  let path = context.filesDir;
  statfs.getFreeBytes(path, (err: BusinessError, freeBytes:Number) => {
      if (err) {
          console.error('getFreeBytes callback failed');
      } else {
          console.info('getFreeBytes callback success' + freeBytes);
      }
  });
  ```

## statfs.getTotalBytes

getTotalBytes(path: string): Promise&lt;number&gt;

异步方法获取指定文件系统总字节数，以Promise形式返回结果。

**系统能力**：SystemCapability.FileManagement.File.FileIO

**参数：**

  | 参数名 | 类型   | 必填 | 说明                         |
  | ---- | ------ | ---- | ---------------------------- |
  | path | string | 是   | 需要查询的文件系统的文件路径 |

**返回值：**

  | 类型                  | 说明         |
  | --------------------- | ------------ |
  | Promise&lt;number&gt; | 返回总字节数 |

**示例：**

  ```ts
  import { BusinessError } from '@ohos.base';
  let path = "/dev";
  statfs.getTotalBytes(path).then((number: number) => {
    console.info("getTotalBytes promise successfully:" + number);
  }).catch((err: BusinessError) => {
    console.info("getTotalBytes failed with error:" + JSON.stringify(err));
  });
  ```

## statfs.getTotalBytes

getTotalBytes(path: string, callback: AsyncCallback&lt;number&gt;): void

异步方法获取指定文件系统总字节数，使用callback形式返回结果。

**系统能力**：SystemCapability.FileManagement.File.FileIO

**参数：**

  | 参数名   | 类型                        | 必填 | 说明                         |
  | -------- | --------------------------- | ---- | ---------------------------- |
  | path     | string                      | 是   | 需要查询的文件系统的文件路径 |
  | callback | AsyncCallback&lt;number&gt; | 是   | 异步获取总字节数之后的回调   |

**示例：**

  ```ts
  import common from '@ohos.app.ability.common';
  let context = getContext(this) as common.UIAbilityContext;
  let path = context.filesDir;
  statfs.getTotalBytes(path, (err: BusinessError, totalBytes:Number) => {
      if (err) {
          console.error('getTotalBytes callback failed');
      } else {
          console.info('getTotalBytes callback success' + totalBytes);
      }
  });
  ```

