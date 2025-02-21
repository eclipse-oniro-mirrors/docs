# @ohos.file.hash (File Hash Processing)

The **FileHash** module implements hash processing on files.

> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```ts
import Hash from '@ohos.file.hash';
```

## Guidelines

Before using the APIs provided by this module to perform operations on a file or directory, obtain the application sandbox path of the file or directory as follows:

  ```ts
  import UIAbility from '@ohos.app.ability.UIAbility';
  import window from '@ohos.window';

  export default class EntryAbility extends UIAbility {
    onWindowStageCreate(windowStage: window.WindowStage) {
      let context = this.context;
      let pathDir = context.filesDir;
    }
  }
  ```

For details about how to obtain the application sandbox path, see [Obtaining Application File Paths](../../application-models/application-context-stage.md#obtaining-application-file-paths).

## Hash.hash

hash(path: string, algorithm: string): Promise&lt;string&gt;

Calculates a hash value for a file. This API uses a promise to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name   | Type  | Mandatory| Description                                                        |
| --------- | ------ | ---- | ------------------------------------------------------------ |
| path      | string | Yes  | Path of the file in the application sandbox.                            |
| algorithm | string | Yes  | Algorithm used to calculate the hash value. The value can be **md5**, **sha1**, or **sha256**. **sha256** is recommended for security purposes.|

**Return value**

  | Type                   | Description                        |
  | --------------------- | -------------------------- |
  | Promise&lt;string&gt; | Promise used to return the hash value. The hash value is a hexadecimal string consisting of digits and uppercase letters.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](errorcode-filemanagement.md#basic-file-io-error-codes).

| ID| Error Message|
| -------- | -------- |
| 13900020 | Invalid argument |
| 13900042 | Unknown error |

**Example**

  ```ts
  import { BusinessError } from '@ohos.base';
  let filePath = pathDir + "/test.txt";
  Hash.hash(filePath, "sha256").then((str: string) => {
    console.info("calculate file hash succeed:" + str);
  }).catch((err: BusinessError) => {
    console.error("calculate file hash failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## Hash.hash

hash(path: string, algorithm: string, callback: AsyncCallback&lt;string&gt;): void

Calculates a hash value for a file. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.FileManagement.File.FileIO

**Parameters**

| Name   | Type                       | Mandatory| Description                                                        |
| --------- | --------------------------- | ---- | ------------------------------------------------------------ |
| path      | string                      | Yes  | Path of the file in the application sandbox.                            |
| algorithm | string                      | Yes  | Algorithm used to calculate the hash value. The value can be **md5**, **sha1**, or **sha256**. **sha256** is recommended for security purposes.|
| callback  | AsyncCallback&lt;string&gt; | Yes  | Callback invoked to return the hash value obtained. The hash value is a hexadecimal string consisting of digits and uppercase letters.|

**Error codes**

For details about the error codes, see [Basic File IO Error Codes](errorcode-filemanagement.md#basic-file-io-error-codes).

| ID| Error Message|
| -------- | -------- |
| 13900020 | Invalid argument |
| 13900042 | Unknown error |

**Example**

  ```ts
  import { BusinessError } from '@ohos.base';
  let filePath = pathDir + "/test.txt";
  Hash.hash(filePath, "sha256", (err: BusinessError, str: string) => {
    if (err) {
      console.error("calculate file hash failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("calculate file hash succeed:" + str);
    }
  });
  ```
