# @ohos.zlib (Zip)

The **Zip** module provides APIs for file compression and decompression.

> **NOTE**
>
> The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```javascript
import zlib from '@ohos.zlib';
```

## zlib.zipFile<sup>(deprecated)</sup>
zipFile(inFile: string, outFile: string, options: Options): Promise&lt;void&gt;

Zips a file. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [zlib.compressFile](#zlibcompressfile9) instead.

**System capability**: SystemCapability.BundleManager.Zlib

**Parameters**

| Name | Type               | Mandatory| Description                                                        |
| ------- | ------------------- | ---- | ------------------------------------------------------------ |
| inFile  | string              | Yes  | Path of the folder or file to zip. For details about the path, see [FA Model](js-apis-inner-app-context.md) and [Stage Model](js-apis-inner-application-context.md).|
| outFile | string              | Yes  | Path of the zipped file. The file name extension is .zip.                 |
| options | [Options](#options) | Yes  | Optional parameters for the zip operation.                                            |

**Return value**

| Type          | Description                                                        |
| -------------- | ------------------------------------------------------------ |
| Promise\<void> | Promise that returns no value.|

**Example**

```typescript
// The path used in the code must be an application sandbox path, for example, /data/storage/el2/base/haps. You can obtain the path through the context.
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

Unzips a file. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [zlib.decompressFile](#zlibdecompressfile9) instead.

**System capability**: SystemCapability.BundleManager.Zlib

**Parameters**

| Name | Type               | Mandatory| Description                                                        |
| ------- | ------------------- | ---- | ------------------------------------------------------------ |
| inFile  | string              | Yes  | Path of the folder or file to unzip. For details about the path, see [FA Model](js-apis-inner-app-context.md) and [Stage Model](js-apis-inner-application-context.md).|
| outFile | string              | Yes  | Path of the unzipped file.                                        |
| options | [Options](#options) | Yes  | Optional parameters for the unzip operation.                                            |

**Return value**

| Type          | Description                                                        |
| -------------- | ------------------------------------------------------------ |
| Promise\<void> | Promise that returns no value.|

**Example**

```typescript
// The path used in the code must be an application sandbox path, for example, /data/storage/el2/base/haps. You can obtain the path through the context.
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

Compresses a file. This API uses an asynchronous callback to return the result.  

**System capability**: SystemCapability.BundleManager.Zlib

**Parameters**

| Name                 | Type               | Mandatory| Description                                                        |
| ----------------------- | ------------------- | ---- | ------------------------------------------------------------ |
| inFile                  | string              | Yes  | Path of the folder or file to compress. For details about the path, see [FA Model](js-apis-inner-app-context.md) and [Stage Model](js-apis-inner-application-context.md).|
| outFile                 | string              | Yes  | Path of the compressed file.                                          |
| options                 | [Options](#options) | Yes  | Compression parameters.                                              |
| callback                | AsyncCallback\<void> | Yes  | Callback used to return the result. If the operation is successful, **null** is returned; otherwise, a specific error code is returned.            |

**Error codes**

For details about the error codes, see [zlib Error Codes](../errorcodes/errorcode-zlib.md).
| ID| Error Message                              |
| -------- | --------------------------------------|
| 900001   | The Input source file is invalid.      |
| 900002   | The Input destination file is invalid. |

**Example**

```typescript
// The path used in the code must be an application sandbox path, for example, /data/storage/el2/base/haps. You can obtain the path through the context.
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

Compresses a file. This API uses a promise to return the result. If the operation is successful, **null** is returned; otherwise, a specific error code is returned.

**System capability**: SystemCapability.BundleManager.Zlib

**Parameters**

| Name | Type               | Mandatory| Description                                                        |
| ------- | ------------------- | ---- | ------------------------------------------------------------ |
| inFile  | string              | Yes  | Path of the folder or file to compress. For details about the path, see [FA Model](js-apis-inner-app-context.md) and [Stage Model](js-apis-inner-application-context.md).|
| outFile | string              | Yes  | Path of the compressed file.                                          |
| options | [Options](#options) | Yes  | Compression parameters.                                              |

**Return value**

| Type          | Description                   |
| -------------- | ----------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [zlib Error Codes](../errorcodes/errorcode-zlib.md).

| ID| Error Message                              |
| -------- | ------------------------------------- |
| 900001   | The Input source file is invalid.      |
| 900002   | The Input destination file is invalid. |

**Example**

```typescript
// The path used in the code must be an application sandbox path, for example, /data/storage/el2/base/haps. You can obtain the path through the context.
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

Decompresses a file. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.BundleManager.Zlib

**Parameters**

| Name                 | Type               | Mandatory| Description                                                        |
| ----------------------- | ------------------- | ---- | ------------------------------------------------------------ |
| inFile                  | string              | Yes  | Path of the file to decompress. The file name extension must be .zip. For details about the path, see [FA Model](js-apis-inner-app-context.md) and [Stage Model](js-apis-inner-application-context.md).|
| outFile                 | string              | Yes  | Path of the decompressed file. The path must exist in the system. Otherwise, the decompression fails. The path must be an application sandbox path, which can be obtained from the context. For details about the context, see [FA Model](js-apis-inner-app-context.md) and [Stage Model](js-apis-inner-application-context.md).|
| options                 | [Options](#options) | Yes  | Decompression parameters.                                            |
| callback                | AsyncCallback\<void> | Yes  | Callback used to return the result. If the operation is successful, **null** is returned; otherwise, a specific error code is returned.            |

**Error codes**

For details about the error codes, see [zlib Error Codes](../errorcodes/errorcode-zlib.md).

| ID| Error Message                              |
| -------- | --------------------------------------|
| 900001   | The Input source file is invalid.      |
| 900002   | The Input destination file is invalid. |

**Example**

```typescript
// The path used in the code must be an application sandbox path, for example, /data/storage/el2/base/haps. You can obtain the path through the context.
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

Decompresses a file. This API uses a promise to return the result.

**System capability**: SystemCapability.BundleManager.Zlib

**Parameters**

| Name | Type               | Mandatory| Description                                                        |
| ------- | ------------------- | ---- | ------------------------------------------------------------ |
| inFile  | string              | Yes  | Path of the file to decompress. The file name extension must be .zip. For details about the path, see [FA Model](js-apis-inner-app-context.md) and [Stage Model](js-apis-inner-application-context.md).|
| outFile | string              | Yes  | Path of the decompressed file. The path must exist in the system. Otherwise, the decompression fails. The path must be an application sandbox path, which can be obtained from the context. For details about the context, see [FA Model](js-apis-inner-app-context.md) and [Stage Model](js-apis-inner-application-context.md).|
| options | [Options](#options) | Yes  | Decompression parameters.                                          |

**Return value**

| Type          | Description                   |
| -------------- | ----------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

For details about the error codes, see [zlib Error Codes](../errorcodes/errorcode-zlib.md).

| ID| Error Message                              |
| ------ | ------------------------------------- |
| 900001 | The Input source file is invalid.      |
| 900002 | The Input destination file is invalid. |

**Example**

```typescript
// The path used in the code must be an application sandbox path, for example, /data/storage/el2/base/haps. You can obtain the path through the context.
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

**System capability**: SystemCapability.BundleManager.Zlib

| Name    | Type            | Readable| Writable| Description                                                      |
| -------- | ---------------- | ---- | ---- | ---------------------------------------------------------- |
| level    | CompressLevel     | Yes  | No  | See [zip.CompressLevel](#zipcompresslevel).      |
| memLevel | MemLevel         | Yes  | No  | See [zip.MemLevel](#zipmemlevel).                |
| strategy | CompressStrategy | Yes  | No  | See [zip.CompressStrategy](#zipcompressstrategy).|

## zip.CompressLevel

**System capability**: SystemCapability.BundleManager.Zlib

| Name                              | Value  | Description             |
| ---------------------------------- | ---- | ----------------- |
| COMPRESS_LEVEL_NO_COMPRESSION      | 0    | Compress level 0 that indicates uncompressed.|
| COMPRESS_LEVEL_BEST_SPEED          | 1    | Compression level 1 that gives the best speed. |
| COMPRESS_LEVEL_BEST_COMPRESSION    | 9    | Compression level 9 that gives the best compression.     |
| COMPRESS_LEVEL_DEFAULT_COMPRESSION | -1   | Default compression level.     |

## zip.MemLevel

**System capability**: SystemCapability.BundleManager.Zlib

| Name             | Value  | Description                            |
| ----------------- | ---- | -------------------------------- |
| MEM_LEVEL_MIN     | 1    | Minimum memory used by the **zip** API during compression.|
| MEM_LEVEL_MAX     | 9    | Maximum memory used by the **zip** API during compression.|
| MEM_LEVEL_DEFAULT | 8    | Default memory used by the **zip** API during compression.|

## zip.CompressStrategy

**System capability**: SystemCapability.BundleManager.Zlib

| Name                              | Value  | Description                    |
| ---------------------------------- | ---- | ------------------------ |
| COMPRESS_STRATEGY_DEFAULT_STRATEGY | 0    | Default compression strategy.            |
| COMPRESS_STRATEGY_FILTERED         | 1    | Filtered compression strategy.|
| COMPRESS_STRATEGY_HUFFMAN_ONLY     | 2    | Huffman coding compression strategy.  |
| COMPRESS_STRATEGY_RLE              | 3    | RLE compression strategy.        |
| COMPRESS_STRATEGY_FIXED            | 4    | Fixed compression strategy.          |

## zip.ErrorCode

**System capability**: SystemCapability.BundleManager.Zlib

| Name            | Value  | Description        |
| ---------------- | ---- | ------------ |
| ERROR_CODE_OK    | 0    | The API is successfully called.|
| ERROR_CODE_ERRNO | -1   | Failed to call the API.|
