# @ohos.file.statvfs (文件系统空间统计)

该模块提供文件系统相关存储信息的功能，向应用程序提供获取文件系统总字节数、空闲字节数的JS接口。

> **说明：**
>
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```js
import statvfs from '@ohos.file.statvfs';
```

## statvfs.getFreeSize

getFreeSize(path:string):Promise&lt;number&gt;

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

**错误码：**

接口抛出错误码的详细介绍请参见[基础文件IO错误码](../errorcodes/errorcode-filemanagement.md#基础文件io错误码)。

**示例：**

  ```js
  let path = "/dev";
  statvfs.getFreeSize(path).then((number) => {
    console.info("getFreeSize promise successfully, Size: " + number);
  }).catch((err) => {
    console.info("getFreeSize failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## statvfs.getFreeSize

getFreeSize(path:string, callback:AsyncCallback&lt;number&gt;): void

异步方法获取指定文件系统空闲字节数，使用callback形式返回结果。

**系统能力**：SystemCapability.FileManagement.File.FileIO

**参数：**

  | 参数名   | 类型                        | 必填 | 说明                         |
  | -------- | --------------------------- | ---- | ---------------------------- |
  | path     | string                      | 是   | 需要查询的文件系统的文件路径 |
  | callback | AsyncCallback&lt;number&gt; | 是   | 异步获取空闲字节数之后的回调 |

**错误码：**

接口抛出错误码的详细介绍请参见[基础文件IO错误码](../errorcodes/errorcode-filemanagement.md#基础文件io错误码)。

**示例：**

  ```js
  let path = "/dev";
  statvfs.getFreeSize(path, (err, number) => {
    if (err) {
      console.info("getFreeSize failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("getFreeSize callback successfully, Size: " + number);
    }
  });
  ```

## statvfs.getTotalSize

getTotalSize(path: string): Promise&lt;number&gt;

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

**错误码：**

接口抛出错误码的详细介绍请参见[基础文件IO错误码](../errorcodes/errorcode-filemanagement.md#基础文件io错误码)。

**示例：**

  ```js
  let path = "/dev";
  statvfs.getTotalSize(path).then((number) => {
    console.info("getTotalSize promise successfully, Size: " + number);
  }).catch((err) => {
    console.info("getTotalSize with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## statvfs.getTotalSize

getTotalSize(path: string, callback: AsyncCallback&lt;number&gt;): void

异步方法获取指定文件系统总字节数，使用callback形式返回结果。

**系统能力**：SystemCapability.FileManagement.File.FileIO

**参数：**

  | 参数名   | 类型                        | 必填 | 说明                         |
  | -------- | --------------------------- | ---- | ---------------------------- |
  | path     | string                      | 是   | 需要查询的文件系统的文件路径 |
  | callback | AsyncCallback&lt;number&gt; | 是   | 异步获取总字节数之后的回调   |

**错误码：**

接口抛出错误码的详细介绍请参见[基础文件IO错误码](../errorcodes/errorcode-filemanagement.md#基础文件io错误码)。

**示例：**

  ```js
  let path = "/dev";
  statvfs.getTotalSize(path, (err, number) => {
    if (err) {
      console.info("getTotalSize with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("getTotalSize promise successfully, Size: " + number);
    }
  });
  ```
