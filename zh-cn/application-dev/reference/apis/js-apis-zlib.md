# @ohos.zlib (Zip模块)

本模块提供压缩解压缩文件的能力。

> **说明：**
>
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```javascript
import zlib from '@ohos.zlib';
```

## zlib.zipFile<sup>(deprecated)</sup>
zipFile(inFile: string, outFile: string, options: Options): Promise&lt;void&gt;

压缩接口，压缩完成后返回执行结果，使用Promise异步返回。

> **说明：**
>
> 从API version 7 开始支持，从API 9 开始废弃。建议使用[zlib.compressFile](#zlibcompressfile9)。

**系统能力：** SystemCapability.BundleManager.Zlib

**参数：**

| 参数名  | 类型                | 必填 | 说明                                                         |
| ------- | ------------------- | ---- | ------------------------------------------------------------ |
| inFile  | string              | 是   | 指定压缩的文件夹路径或者文件路径，对应的路径参考[FA模型](js-apis-inner-app-context.md)，[Stage模型](js-apis-inner-application-context.md)。 |
| outFile | string              | 是   | 指定压缩结果的文件路径（文件的扩展名zip）。                  |
| options | [Options](#options) | 是   | 压缩的可选参数。                                             |

**返回值：**

| 类型           | 说明                                                         |
| -------------- | ------------------------------------------------------------ |
| Promise\<void> | Promise对象，无返回值。 |

**示例：**

```typescript
// 代码中使用的路径需为应用的沙箱路径，如/data/storage/el2/base/haps,也可以通过context获取。
import zlib from '@ohos.zlib';
let inFile = '/xxx/filename.xxx';
let outFile = '/xxx/xxx.zip';
let options = {
  level: zlib.CompressLevel.COMPRESS_LEVEL_DEFAULT_COMPRESSION,
  memLevel: zlib.MemLevel.MEM_LEVEL_DEFAULT,
  strategy: zlib.CompressStrategy.COMPRESS_STRATEGY_DEFAULT_STRATEGY
};

zlib.zipFile(inFile, outFile, options).then((data) => {
    console.info('zipFile result is ' + JSON.stringify(data));
}).catch((err) => {
    console.error('error is ' + JSON.stringify(err));
});
```

## zlib.unzipFile<sup>(deprecated)</sup>

unzipFile(inFile:string, outFile:string, options: Options): Promise&lt;void&gt;

解压文件，解压完成后返回执行结果，使用Promise异步返回。

> **说明：**
>
> 从API version 7 开始支持，从API 9 开始废弃。建议使用[zlib.decompressFile](#zlibdecompressfile9)。

**系统能力：** SystemCapability.BundleManager.Zlib

**参数：**

| 参数名  | 类型                | 必填 | 说明                                                         |
| ------- | ------------------- | ---- | ------------------------------------------------------------ |
| inFile  | string              | 是   | 指定待解压的文件夹路径或者文件路径，对应的路径参考[FA模型](js-apis-inner-app-context.md)，[stage模型](js-apis-inner-application-context.md)。 |
| outFile | string              | 是   | 指定的解压文件路径。                                         |
| options | [Options](#options) | 是   | 解压的可选参数。                                             |

**返回值：**

| 类型           | 说明                                                         |
| -------------- | ------------------------------------------------------------ |
| Promise\<void> | Promise对象，无返回值。 |

**示例：**

```typescript
// 代码中使用的路径需为应用的沙箱路径，如/data/storage/el2/base/haps,也可以通过context获取。
import zlib from '@ohos.zlib';
let inFile = '/xx/xxx.zip';
let outFile = '/xxx';

let options = {
  level: zlib.CompressLevel.COMPRESS_LEVEL_DEFAULT_COMPRESSION,
  memLevel: zlib.MemLevel.MEM_LEVEL_DEFAULT,
  strategy: zlib.CompressStrategy.COMPRESS_STRATEGY_DEFAULT_STRATEGY
};
zlib.unzipFile(inFile, outFile, options).then((data) => {
    console.info('unzipFile result is ' + JSON.stringify(data));
}).catch((err)=>{
    console.error('error is ' + JSON.stringify(err));
})
```

## zlib.compressFile<sup>9+</sup>

compressFile(inFile: string, outFile: string, options: Options, callback: AsyncCallback\<void>): void

压缩文件，压缩的结果，使用callback异步回调返回。成功返回null，失败返回错误码。

**系统能力：** SystemCapability.BundleManager.Zlib

**参数：**

| 参数名                  | 类型                | 必填 | 说明                                                         |
| ----------------------- | ------------------- | ---- | ------------------------------------------------------------ |
| inFile                  | string              | 是   | 指定压缩的文件夹路径或者文件路径，对应的路径参考[FA模型](js-apis-inner-app-context.md)，[stage模型](js-apis-inner-application-context.md)。 |
| outFile                 | string              | 是   | 指定压缩结果的文件路径。                                           |
| options                 | [Options](#options) | 是   | 压缩的配置参数。                                               |
| callback                | AsyncCallback\<void> | 是   | 异步获取压缩结果之后的回调。成功返回null，失败返回错误码。             |

**错误码：**

以下错误码的详细介绍请参见[ohos.zlib错误码](../errorcodes/errorcode-zlib.md)。
| 错误码ID | 错误信息                               |
| -------- | --------------------------------------|
| 900001   | The Input source file is invalid.      |
| 900002   | The Input destination file is invalid. |

**示例：**

```typescript
// 代码中使用的路径需为应用的沙箱路径，如/data/storage/el2/base/haps,也可以通过context获取。
import zlib from '@ohos.zlib';
let inFile = '/xxx/filename.xxx';
let outFile = '/xxx/xxx.zip';
let options = {
  level: zlib.CompressLevel.COMPRESS_LEVEL_DEFAULT_COMPRESSION,
  memLevel: zlib.MemLevel.MEM_LEVEL_DEFAULT,
  strategy: zlib.CompressStrategy.COMPRESS_STRATEGY_DEFAULT_STRATEGY
};

try {
    zlib.compressFile(inFile, outFile, options, (errData) => {
        if (errData !== null) {
            console.error(`errData is errCode:${errData.code}  message:${errData.message}`);
        }
    })
} catch(errData) {
    console.error(`errData is errCode:${errData.code}  message:${errData.message}`);
}
```

## zlib.compressFile<sup>9+</sup>

compressFile(inFile: string, outFile: string, options: Options): Promise\<void>

压缩文件，压缩的结果，使用Promise异步返回。成功时返回null，失败时返回错误码。

**系统能力：** SystemCapability.BundleManager.Zlib

**参数：**

| 参数名  | 类型                | 必填 | 说明                                                         |
| ------- | ------------------- | ---- | ------------------------------------------------------------ |
| inFile  | string              | 是   | 指定压缩的文件夹路径或者文件路径，对应的路径参考[FA模型](js-apis-inner-app-context.md)，[stage模型](js-apis-inner-application-context.md)。 |
| outFile | string              | 是   | 指定压缩结果的文件路径。                                           |
| options | [Options](#options) | 是   | 压缩的配置参数。                                               |

**返回值：**

| 类型           | 说明                    |
| -------------- | ----------------------- |
| Promise\<void> | Promise对象，无返回值。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.zlib错误码](../errorcodes/errorcode-zlib.md)。

| 错误码ID | 错误信息                               |
| -------- | ------------------------------------- |
| 900001   | The Input source file is invalid.      |
| 900002   | The Input destination file is invalid. |

**示例：**

```typescript
// 代码中使用的路径需为应用的沙箱路径，如/data/storage/el2/base/haps,也可以通过context获取。
import zlib from '@ohos.zlib';
let inFile = '/xxx/filename.xxx';
let outFile = '/xxx/xxx.zip';
let options = {
  level: zlib.CompressLevel.COMPRESS_LEVEL_DEFAULT_COMPRESSION,
  memLevel: zlib.MemLevel.MEM_LEVEL_DEFAULT,
  strategy: zlib.CompressStrategy.COMPRESS_STRATEGY_DEFAULT_STRATEGY
};

try {
    zlib.compressFile(inFile, outFile, options).then((data) => {
        console.info('compressFile success. data: ' + JSON.stringify(data));
    }).catch((errData) => {
        console.error(`errData is errCode:${errData.code}  message:${errData.message}`);
    })
} catch(errData) {
    console.error(`errData is errCode:${errData.code}  message:${errData.message}`);
}
```



## zlib.decompressFile<sup>9+</sup>

decompressFile(inFile: string, outFile: string, options: Options, callback: AsyncCallback\<void>): void

解压文件，解压的结果，使用callback异步回调返回。成功时返回null，失败时返回错误码。

**系统能力：** SystemCapability.BundleManager.Zlib

**参数：**

| 参数名                  | 类型                | 必填 | 说明                                                         |
| ----------------------- | ------------------- | ---- | ------------------------------------------------------------ |
| inFile                  | string              | 是   | 指定的待解压缩文件的文件路径，文件后缀需要以.zip结尾。对应的路径参考[FA模型](js-apis-inner-app-context.md)，[stage模型](js-apis-inner-application-context.md)。 |
| outFile                 | string              | 是   | 指定的解压后的文件夹路径，文件夹目录路径需要在系统中存在，不存在则会解压失败。路径必须为沙箱路径，沙箱路径可以通过context获取，具体方法可参考[application/context（Stage模型）](js-apis-inner-application-context.md)或 [app/context（FA模型）](js-apis-inner-app-context.md)。 |
| options                 | [Options](#options) | 是   | 解压的配置参数。                                             |
| callback                | AsyncCallback\<void> | 是   | 异步获取解压结果之后的回调。成功返回null，失败返回错误码。             |

**错误码：**

以下错误码的详细介绍请参见[ohos.zlib错误码](../errorcodes/errorcode-zlib.md)。

| 错误码ID | 错误信息                               |
| -------- | --------------------------------------|
| 900001   | The Input source file is invalid.      |
| 900002   | The Input destination file is invalid. |

**示例：**

```typescript
// 代码中使用的路径需为应用的沙箱路径，如/data/storage/el2/base/haps,也可以通过context获取。
import zlib from '@ohos.zlib';
let inFile = '/xx/xxx.zip';
let outFile = '/xxx';
let options = {
  level: zlib.CompressLevel.COMPRESS_LEVEL_DEFAULT_COMPRESSION,
  memLevel: zlib.MemLevel.MEM_LEVEL_DEFAULT,
  strategy: zlib.CompressStrategy.COMPRESS_STRATEGY_DEFAULT_STRATEGY
};

try {
    zlib.decompressFile(inFile, outFile, options, (errData) => {
        if (errData !== null) {
            console.error(`errData is errCode:${errData.code}  message:${errData.message}`);
        }
    })
} catch(errData) {
    console.error(`errData is errCode:${errData.code}  message:${errData.message}`);
}
```

## zlib.decompressFile<sup>9+</sup>

decompressFile(inFile: string, outFile: string, options: Options): Promise\<void>

解压文件，解压的结果，使用Promise异步返回。成功时返回null，失败时返回错误码。

**系统能力：** SystemCapability.BundleManager.Zlib

**参数：**

| 参数名  | 类型                | 必填 | 说明                                                         |
| ------- | ------------------- | ---- | ------------------------------------------------------------ |
| inFile  | string              | 是   | 指定的待解压缩文件的文件路径，文件后缀需要以.zip结尾。对应的路径参考[FA模型](js-apis-inner-app-context.md)，[stage模型](js-apis-inner-application-context.md)。 |
| outFile | string              | 是   | 指定的解压后的文件夹路径，文件夹目录路径需要在系统中存在，不存在则会解压失败。路径必须为沙箱路径，沙箱路径可以通过context获取，具体方法可参考[application/context（Stage模型）](js-apis-inner-application-context.md)或 [app/context（FA模型）](js-apis-inner-app-context.md)。 |
| options | [Options](#options) | 是   | 解压时的配置参数。                                           |

**返回值：**

| 类型           | 说明                    |
| -------------- | ----------------------- |
| Promise\<void> | Promise对象，无返回值。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.zlib错误码](../errorcodes/errorcode-zlib.md)。

| 错误码ID | 错误信息                               |
| ------ | ------------------------------------- |
| 900001 | The Input source file is invalid.      |
| 900002 | The Input destination file is invalid. |

**示例：**

```typescript
// 代码中使用的路径需为应用的沙箱路径，如/data/storage/el2/base/haps,也可以通过context获取。
import zlib from '@ohos.zlib';
let inFile = '/xx/xxx.zip';
let outFile = '/xxx';
let options = {
  level: zlib.CompressLevel.COMPRESS_LEVEL_DEFAULT_COMPRESSION,
  memLevel: zlib.MemLevel.MEM_LEVEL_DEFAULT,
  strategy: zlib.CompressStrategy.COMPRESS_STRATEGY_DEFAULT_STRATEGY
};

try {
    zlib.decompressFile(inFile, outFile, options).then((data) => {
        console.info('decompressFile success. data: ' + JSON.stringify(data));
    }).catch((errData) => {
        console.error(`errData is errCode:${errData.code}  message:${errData.message}`);
    })
} catch(errData) {
    console.error(`errData is errCode:${errData.code}  message:${errData.message}`);
}
```

## Options

**系统能力：** SystemCapability.BundleManager.Zlib

| 名称     | 类型             | 可读 | 可写 | 说明                                                       |
| -------- | ---------------- | ---- | ---- | ---------------------------------------------------------- |
| level    | CompressLevel     | 是   | 否   | 参考[zip.CompressLevel枚举定义](#zipcompresslevel)。       |
| memLevel | MemLevel         | 是   | 否   | 参考[zip.MemLevel枚举定义](#zipmemlevel)。                 |
| strategy | CompressStrategy | 是   | 否   | 参考[zip.CompressStrategy枚举定义](#zipcompressstrategy)。 |

## zip.CompressLevel

**系统能力：** SystemCapability.BundleManager.Zlib

| 名称                               | 值   | 说明              |
| ---------------------------------- | ---- | ----------------- |
| COMPRESS_LEVEL_NO_COMPRESSION      | 0    | 压缩率为0压缩等级。 |
| COMPRESS_LEVEL_BEST_SPEED          | 1    | 最佳速度压缩等级。  |
| COMPRESS_LEVEL_BEST_COMPRESSION    | 9    | 最佳压缩等级。      |
| COMPRESS_LEVEL_DEFAULT_COMPRESSION | -1   | 默认压缩等级。      |

## zip.MemLevel

**系统能力：** SystemCapability.BundleManager.Zlib

| 名称              | 值   | 说明                             |
| ----------------- | ---- | -------------------------------- |
| MEM_LEVEL_MIN     | 1    | zip 接口在压缩过程中最小使用内存。 |
| MEM_LEVEL_MAX     | 9    | zip 接口在压缩过程中最大使用内存。 |
| MEM_LEVEL_DEFAULT | 8    | zip 接口在压缩过程中默认使用内存。 |

## zip.CompressStrategy

**系统能力：** SystemCapability.BundleManager.Zlib

| 名称                               | 值   | 说明                     |
| ---------------------------------- | ---- | ------------------------ |
| COMPRESS_STRATEGY_DEFAULT_STRATEGY | 0    | 常规数据策略。             |
| COMPRESS_STRATEGY_FILTERED         | 1    | 过滤器产生的数据压缩策略。 |
| COMPRESS_STRATEGY_HUFFMAN_ONLY     | 2    | 霍夫曼编码格式压缩策略。   |
| COMPRESS_STRATEGY_RLE              | 3    | 游标编码压缩策略。         |
| COMPRESS_STRATEGY_FIXED            | 4    | 固定的压缩策略。           |

## zip.ErrorCode

**系统能力：** SystemCapability.BundleManager.Zlib

| 名称             | 值   | 说明         |
| ---------------- | ---- | ------------ |
| ERROR_CODE_OK    | 0    | 函数调用成功。 |
| ERROR_CODE_ERRNO | -1   | 函数调用失败。 |
