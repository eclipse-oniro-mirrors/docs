# @ohos.request (Upload and Download)

The **request** module provides applications with basic upload, download, and background transmission agent capabilities.

> **NOTE**
>
> The initial APIs of this module are supported since API version 6. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import


```js
import request from '@ohos.request';
```

## Constants

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

### Network Types
You can set **networkType** in [DownloadConfig](#downloadconfig) to specify the network type for the download service.

| Name| Type| Value| Description|
| -------- | -------- | -------- | -------- |
| NETWORK_MOBILE | number | 0x00000001 | Whether download is allowed on a mobile network.|
| NETWORK_WIFI | number | 0x00010000 | Whether download is allowed on a WLAN.|

### Download Error Codes
The table below lists the values of **err** in the callback of [on('fail')<sup>7+</sup>](#onfail7) and the values of **failedReason** returned by [getTaskInfo<sup>9+</sup>](#gettaskinfo9).

| Name| Type| Value| Description|
| -------- | -------- | -------- | -------- |
| ERROR_CANNOT_RESUME<sup>7+</sup> | number |   0   | Failure to resume the download due to network errors.|
| ERROR_DEVICE_NOT_FOUND<sup>7+</sup> | number |   1   | Failure to find a storage device such as a memory card.|
| ERROR_FILE_ALREADY_EXISTS<sup>7+</sup> | number |   2   | Failure to download the file because it already exists.|
| ERROR_FILE_ERROR<sup>7+</sup> | number |   3   | File operation failure.|
| ERROR_HTTP_DATA_ERROR<sup>7+</sup> | number |   4   | HTTP transmission failure.|
| ERROR_INSUFFICIENT_SPACE<sup>7+</sup> | number |   5   | Insufficient storage space.|
| ERROR_TOO_MANY_REDIRECTS<sup>7+</sup> | number |   6   | Error caused by too many network redirections.|
| ERROR_UNHANDLED_HTTP_CODE<sup>7+</sup> | number |   7   | Unidentified HTTP code.|
| ERROR_UNKNOWN<sup>7+</sup> | number |   8   | Unknown error.|
| ERROR_OFFLINE<sup>9+</sup> | number |   9   | No network connection.|
| ERROR_UNSUPPORTED_NETWORK_TYPE<sup>9+</sup> | number |   10   | Network type mismatch.|


### Causes of Download Pause
The table below lists the values of **pausedReason** returned by [getTaskInfo<sup>9+</sup>](#gettaskinfo9).

| Name| Type| Value| Description|
| -------- | -------- | -------- | -------- |
| PAUSED_QUEUED_FOR_WIFI<sup>7+</sup> | number |   0   | Download paused and queuing for a WLAN connection, because the file size exceeds the maximum value allowed by a mobile network session.|
| PAUSED_WAITING_FOR_NETWORK<sup>7+</sup> | number |   1   | Download paused due to a network connection problem, for example, network disconnection.|
| PAUSED_WAITING_TO_RETRY<sup>7+</sup> | number |   2   | Download paused and then retried.|
| PAUSED_BY_USER<sup>9+</sup> | number |   3   | The user paused the session.|
| PAUSED_UNKNOWN<sup>7+</sup> | number |   4   | Download paused due to unknown reasons.|

### Download Task Status Codes
The table below lists the values of **status** returned by [getTaskInfo<sup>9+</sup>](#gettaskinfo9).

| Name| Type| Value| Description|
| -------- | -------- | -------- | -------- |
| SESSION_SUCCESSFUL<sup>7+</sup> | number |   0   | Successful download.|
| SESSION_RUNNING<sup>7+</sup> | number |   1   | Download in progress.|
| SESSION_PENDING<sup>7+</sup> | number |   2   | Download pending.|
| SESSION_PAUSED<sup>7+</sup> | number |   3   | Download paused.|
| SESSION_FAILED<sup>7+</sup> | number |   4   | Download failure without retry.|


## request.uploadFile<sup>9+</sup>

uploadFile(context: BaseContext, config: UploadConfig): Promise&lt;UploadTask&gt;

Uploads files. This API uses a promise to return the result. You can use [on('complete'|'fail')<sup>9+</sup>](#oncomplete--fail9) to obtain the upload error information.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Upload

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | context | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md) | Yes| Application-based context.|
  | config | [UploadConfig](#uploadconfig6) | Yes| Upload configurations.|


**Return value**

  | Type| Description|
  | -------- | -------- |
  | Promise&lt;[UploadTask](#uploadtask)&gt; | Promise used to return the upload task.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400002 | bad file path. |

**Example**

  ```ts
  let uploadTask: request.UploadTask;
  let uploadConfig: request.UploadConfig = {
    url: 'http://www.example.com', // Replace the URL with the HTTP address of the real server.
    header: { 'Accept': '*/*' },
    method: "POST",
    files: [{ filename: "test", name: "test", uri: "internal://cache/test.jpg", type: "jpg" }],
    data: [{ name: "name123", value: "123" }],
  };
  try {
    request.uploadFile(getContext(), uploadConfig).then((data: request.UploadTask) => {
      uploadTask = data;
    }).catch((err: BusinessError) => {
      console.error(`Failed to request the upload. Code: ${err.code}, message: ${err.message}`);
    });
  } catch (err) {
    console.error(`Failed to request the upload. err: ${JSON.stringify(err)}`);
  }
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).


## request.uploadFile<sup>9+</sup>

uploadFile(context: BaseContext, config: UploadConfig, callback: AsyncCallback&lt;UploadTask&gt;): void

Uploads files. This API uses an asynchronous callback to return the result. You can use [on('complete'|'fail')<sup>9+</sup>](#oncomplete--fail9) to obtain the upload error information.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Upload

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | context | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md) | Yes| Application-based context.|
  | config | [UploadConfig](#uploadconfig6) | Yes| Upload configurations.|
  | callback | AsyncCallback&lt;[UploadTask](#uploadtask)&gt; | Yes| Callback used to return the **UploadTask** object.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400002 | bad file path. |

**Example**

  ```ts
  let uploadTask: request.UploadTask;
  let uploadConfig: request.UploadConfig = {
    url: 'http://www.example.com', // Replace the URL with the HTTP address of the real server.
    header: { 'Accept': '*/*' },
    method: "POST",
    files: [{ filename: "test", name: "test", uri: "internal://cache/test.jpg", type: "jpg" }],
    data: [{ name: "name123", value: "123" }],
  };
  try {
    request.uploadFile(getContext(), uploadConfig, (err: BusinessError, data: request.UploadTask) => {
      if (err) {
        console.error(`Failed to request the upload. Code: ${err.code}, message: ${err.message}`);
        return;
      }
      uploadTask = data;
    });
  } catch (err) {
    console.error(`Failed to request the upload. err: ${JSON.stringify(err)}`);
  }
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

## request.upload<sup>(deprecated)</sup>

upload(config: UploadConfig): Promise&lt;UploadTask&gt;

Uploads files. This API uses a promise to return the result.

**Model restriction**: This API can be used only in the FA model.

> **NOTE**
>
> This API is deprecated since API version 9. You are advised to use [request.uploadFile<sup>9+</sup>](#requestuploadfile9) instead.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Upload

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | config | [UploadConfig](#uploadconfig6) | Yes| Upload configurations.|

**Return value**

  | Type| Description|
  | -------- | -------- |
  | Promise&lt;[UploadTask](#uploadtask)&gt; | Promise used to return the upload task.|

**Example**

  ```js
  let uploadTask;
  let uploadConfig = {
    url: 'http://www.example.com', // Replace the URL with the HTTP address of the real server.
    header: { 'Accept': '*/*' },
    method: "POST",
    files: [{ filename: "test", name: "test", uri: "internal://cache/test.jpg", type: "jpg" }],
    data: [{ name: "name123", value: "123" }],
  };
  request.upload(uploadConfig).then((data) => {
    uploadTask = data;
  }).catch((err) => {
    console.error(`Failed to request the upload. Code: ${err.code}, message: ${err.message}`);
  })
  ```


## request.upload<sup>(deprecated)</sup>

upload(config: UploadConfig, callback: AsyncCallback&lt;UploadTask&gt;): void

Uploads files. This API uses an asynchronous callback to return the result.

**Model restriction**: This API can be used only in the FA model.

> **NOTE**
>
> This API is deprecated since API version 9. You are advised to use [request.uploadFile<sup>9+</sup>](#requestuploadfile9-1) instead.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Upload

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | config | [UploadConfig](#uploadconfig6) | Yes| Upload configurations.|
  | callback | AsyncCallback&lt;[UploadTask](#uploadtask)&gt; | Yes| Callback used to return the **UploadTask** object.|

**Example**

  ```js
  let uploadTask;
  let uploadConfig = {
    url: 'http://www.example.com', // Replace the URL with the HTTP address of the real server.
    header: { 'Accept': '*/*' },
    method: "POST",
    files: [{ filename: "test", name: "test", uri: "internal://cache/test.jpg", type: "jpg" }],
    data: [{ name: "name123", value: "123" }],
  };
  request.upload(uploadConfig, (err, data) => {
    if (err) {
      console.error(`Failed to request the upload. Code: ${err.code}, message: ${err.message}`);
      return;
    }
    uploadTask = data;
  });
  ```

## UploadTask

Implements file uploads. Before using any APIs of this class, you must obtain an **UploadTask** object through [request.uploadFile<sup>9+</sup>](#requestuploadfile9) in promise mode or [request.uploadFile<sup>9+</sup>](#requestuploadfile9-1) in callback mode.



### on('progress')

on(type: 'progress', callback:(uploadedSize: number, totalSize: number) =&gt; void): void

Subscribes to upload progress events. This API uses a callback to return the result asynchronously.

> **NOTE**
>
> To maintain a balance between power consumption and performance, this API cannot be called when the application is running in the background.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Upload

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Type of the event to subscribe to. The value is **'progress'** (upload progress).|
  | callback | function | Yes| Callback for the upload progress event.|

  Parameters of the callback function

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| uploadedSize | number | Yes| Size of the uploaded files, in bytes.|
| totalSize | number | Yes| Total size of the files to upload, in bytes.|

**Example**

  ```ts
  let upProgressCallback = (uploadedSize: number, totalSize: number) => {
    console.info("upload totalSize:" + totalSize + "  uploadedSize:" + uploadedSize);
  };
  uploadTask.on('progress', upProgressCallback);
  ```


### on('headerReceive')<sup>7+</sup>

on(type: 'headerReceive', callback:  (header: object) =&gt; void): void

Subscribes to HTTP header events for the upload task. This API uses a callback to return the result asynchronously.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Upload

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Type of the event to subscribe to. The value is **'headerReceive'** (response header).|
  | callback | function | Yes| Callback for the HTTP Response Header event.|

  Parameters of the callback function

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| header | object | Yes| HTTP Response Header.|

**Example**

  ```ts
  let headerCallback = (headers: object) => {
    console.info("upOnHeader headers:" + JSON.stringify(headers));
  };
  uploadTask.on('headerReceive', headerCallback);
  ```


### on('complete' | 'fail')<sup>9+</sup>

 on(type:'complete' | 'fail', callback: Callback&lt;Array&lt;TaskState&gt;&gt;): void;

Subscribes to upload completion or failure events. This API uses a callback to return the result asynchronously.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Upload

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Type of the event to subscribe to. The value **'complete'** means the upload completion event, and **'fail'** means the upload failure event.|
  | callback | Callback&lt;Array&lt;TaskState&gt;&gt; | Yes| Callback used to return the result.|

  Parameters of the callback function

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| taskstates | Array&lt;[TaskState](#taskstate9)&gt; | Yes| Upload result.|

**Example**

  ```ts
  let upCompleteCallback = (taskStates: Array<request.TaskState>) => {
    for (let i = 0; i < taskStates.length; i++) {
      console.info("upOnComplete taskState:" + JSON.stringify(taskStates[i]));
    }
  };
  uploadTask.on('complete', upCompleteCallback);

  let upFailCallback = (taskStates: Array<request.TaskState>) => {
    for (let i = 0; i < taskStates.length; i++) {
      console.info("upOnFail taskState:" + JSON.stringify(taskStates[i]));
    }
  };
  uploadTask.on('fail', upFailCallback);
  ```


### off('progress')

off(type:  'progress',  callback?: (uploadedSize: number, totalSize: number) =&gt;  void): void

Unsubscribes from upload progress events.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Upload

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Type of the event to unsubscribe from. The value is **'progress'** (upload progress).|
  | callback | function | No| Callback to unregister. If this parameter is not specified, all callbacks of the current type will be unregistered.<br>**uploadedSize**: size of the uploaded files, in B.<br>**totalSize**: Total size of the files to upload, in B.|

**Example**

  ```ts
  let upProgressCallback1 = (uploadedSize: number, totalSize: number) => {
    console.info('Upload delete progress notification.' + 'totalSize:' + totalSize + 'uploadedSize:' + uploadedSize);
  };
  let upProgressCallback2 = (uploadedSize: number, totalSize: number) => {
    console.info('Upload delete progress notification.' + 'totalSize:' + totalSize + 'uploadedSize:' + uploadedSize);
  };
  uploadTask.on('progress', upProgressCallback1);
  uploadTask.on('progress', upProgressCallback2);
  // Unsubscribe from upProgressCallback1.
  uploadTask.off('progress', upProgressCallback1);
  // Unsubscribe from all callbacks of upload progress events.
  uploadTask.off('progress');
  ```


### off('headerReceive')<sup>7+</sup>

off(type: 'headerReceive', callback?: (header: object) =&gt; void): void

This interface is used to unsubscribe from the HTTP header event of an upload task.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Upload

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Type of the event to unsubscribe from. The value is **'headerReceive'** (response header).|
  | callback | function | No| Callback to unregister. If this parameter is not specified, all callbacks of the current type will be unregistered.|

**Example**

  ```ts
  let headerCallback1 = (header: object) => {
    console.info(`Upload delete headerReceive notification. header: ${JSON.stringify(header)}`);
  };
  let headerCallback2 = (header: object) => {
    console.info(`Upload delete headerReceive notification. header: ${JSON.stringify(header)}`);
  };
  uploadTask.on('headerReceive', headerCallback1);
  uploadTask.on('headerReceive', headerCallback2);
  // Unsubscribe from headerCallback1.
  uploadTask.off('headerReceive', headerCallback1);
  // Unsubscribe from all callbacks of the HTTP header events for the upload task.
  uploadTask.off('headerReceive');
  ```

### off('complete' | 'fail')<sup>9+</sup>

 off(type:'complete' | 'fail', callback?: Callback&lt;Array&lt;TaskState&gt;&gt;): void;

Unsubscribes from upload completion or failure events.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Upload

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Type of the event to subscribe to. The value **'complete'** means the upload completion event, and **'fail'** means the upload failure event.|
  | callback | Callback&lt;Array&lt;TaskState&gt;&gt; | No| Callback to unregister. If this parameter is not specified, all callbacks of the current type will be unregistered.|

**Example**

  ```ts
  let upCompleteCallback1 = (taskStates: Array<request.TaskState>) => {
    console.info('Upload delete complete notification.');
    for (let i = 0; i < taskStates.length; i++) {
      console.info('taskState:' + JSON.stringify(taskStates[i]));
    }
  };
  let upCompleteCallback2 = (taskStates: Array<request.TaskState>) => {
    console.info('Upload delete complete notification.');
    for (let i = 0; i < taskStates.length; i++) {
      console.info('taskState:' + JSON.stringify(taskStates[i]));
    }
  };
  uploadTask.on('complete', upCompleteCallback1);
  uploadTask.on('complete', upCompleteCallback2);
  // Unsubscribe from headerCallback1.
  uploadTask.off('complete', upCompleteCallback1);
  // Unsubscribe from all callbacks of the upload completion events.
  uploadTask.off('complete');

  let upFailCallback1 = (taskStates: Array<request.TaskState>) => {
    console.info('Upload delete fail notification.');
    for (let i = 0; i < taskStates.length; i++) {
      console.info('taskState:' + JSON.stringify(taskStates[i]));
    }
  };
  let upFailCallback2 = (taskStates: Array<request.TaskState>) => {
    console.info('Upload delete fail notification.');
    for (let i = 0; i < taskStates.length; i++) {
      console.info('taskState:' + JSON.stringify(taskStates[i]));
    }
  };
  uploadTask.on('fail', upFailCallback1);
  uploadTask.on('fail', upFailCallback2);
  // Unsubscribe from headerCallback1.
  uploadTask.off('fail', upFailCallback1);
  // Unsubscribe from all callbacks of the upload failure events.
  uploadTask.off('fail');
  ```

### delete<sup>9+</sup>
delete(): Promise&lt;boolean&gt;

Deletes this upload task. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Upload

**Return value**

  | Type| Description|
  | -------- | -------- |
  | Promise&lt;boolean&gt; | Promise used to return the result. The value **true** indicates that the operation is successful, and the value **false** indicates the opposite.|

**Example**

  ```ts
  uploadTask.delete().then((result: boolean) => {
    console.info('Succeeded in deleting the upload task.');
  }).catch((err: BusinessError) => {
    console.error(`Failed to delete the upload task. Code: ${err.code}, message: ${err.message}`);
  });
  ```


### delete<sup>9+</sup>

delete(callback: AsyncCallback&lt;boolean&gt;): void

Deletes this upload task. This API uses an asynchronous callback to return the result. 

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Upload

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | Yes| Callback used to return the result. The value **true** indicates that the operation is successful, and the value **false** indicates the opposite.|

**Example**

  ```ts
  uploadTask.delete((err: BusinessError, result: boolean) => {
    if (err) {
      console.error(`Failed to delete the upload task. Code: ${err.code}, message: ${err.message}`);
      return;
    }
    console.info('Succeeded in deleting the upload task.');
  });
  ```


### remove<sup>(deprecated)</sup>

remove(): Promise&lt;boolean&gt;

Removes this upload task. This API uses a promise to return the result. 

> **NOTE**
>
> This API is deprecated since API version 9. You are advised to use [delete<sup>9+</sup>](#delete9) instead.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Upload

**Return value**

  | Type| Description|
  | -------- | -------- |
  | Promise&lt;boolean&gt; | Promise used to return the result. The value **true** indicates that the operation is successful, and the value **false** indicates the opposite.|

**Example**

  ```js
  uploadTask.remove().then((result) => {
    console.info('Succeeded in removing the upload task.');
  }).catch((err) => {
    console.error(`Failed to remove the upload task. Code: ${err.code}, message: ${err.message}`);
  });
  ```


### remove<sup>(deprecated)</sup>

remove(callback: AsyncCallback&lt;boolean&gt;): void

Removes this upload task. This API uses an asynchronous callback to return the result. 

> **NOTE**
>
> This API is deprecated since API version 9. You are advised to use [delete<sup>9+</sup>](#delete9-1) instead.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Upload

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | Yes| Callback used to return the result. The value **true** indicates that the operation is successful, and the value **false** indicates the opposite.|

**Example**

  ```js
  uploadTask.remove((err, result) => {
    if (err) {
      console.error(`Failed to remove the upload task. Code: ${err.code}, message: ${err.message}`);
      return;
    }
    if (result) {
      console.info('Succeeded in removing the upload task.');
    } else {
      console.error(`Failed to remove the upload task. Code: ${err.code}, message: ${err.message}`);
    }
  });
  ```

## UploadConfig<sup>6+</sup>
Describes the configuration of an upload task.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Upload

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| url | string | Yes| Resource URL.|
| header | Object | Yes| HTTP or HTTPS header added to an upload request.|
| method | string | Yes|  HTTP request method. The value can be **POST** or **PUT**. The default value is **POST**. Use the **PUT** method to modify resources and the **POST** method to add resources.|
| index<sup>11+</sup> | number | No| Path index of the task. The default value is **0**.|
| begins<sup>11+</sup> | number | No| File start point to read when the task begins. The default value is **0**. The value is a closed interval.|
| ends<sup>11+</sup> | number | No| File start point to read when the task ends. The default value is **-1**. The value is a closed interval.|
| files | Array&lt;[File](#file)&gt; | Yes| List of files to upload, The files are submitted in multipart/form-data format.|
| data | Array&lt;[RequestData](#requestdata)&gt; | Yes| Form data in the request body.|

## TaskState<sup>9+</sup>
Implements a **TaskState** object, which is the callback parameter of the [on('complete' | 'fail')<sup>9+</sup>](#oncomplete--fail9) and [off('complete' | 'fail')<sup>9+</sup>](#offcomplete--fail9) APIs.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Upload

| Name| Type| Mandatory| Description                                              |
| -------- | -------- | -------- |--------------------------------------------------|
| path | string | Yes| File path.                                            |
| responseCode | number | Yes| Return value of an upload task. The value **0** means that the task is successful, and other values means that the task fails. For details about the task result, see **message**. You are advised to create an upload task by using [request.agent.create<sup>10+</sup>](#requestagentcreate10-1) and handle exceptions based on standard error codes.|
| message | string | Yes| Description of the upload task result.                                      |

The following table describes the enum values of **responseCode**.

| Result Code| Description                              |
|-----|------------------------------------|
| 0   | Upload success.                              |
| 5   | Task suspended or stopped proactively.                        |
| 6   | Foreground task stopped. The reason is that the application, to which the task belongs, is switched to the background or terminated. Check the application status. |
| 7   | No network connection. Check whether the device is connected to the network.                 |
| 8   | Network mismatch. Check whether the current network type matches the network type required by the task.    |
| 10  | Failed to create the HTTP request. Verify the parameters or try again.         |
| 12  | Request timeout. Verify the parameter configuration or the network connection, or try again.         |
| 13  | Connection failed. Verify the parameter configuration or the network connection, or try again.       |
| 14  | Request failed. Verify the parameter configuration or the network connection, or try again.       |
| 15  | Upload failed. Verify the parameter configuration or the network connection, or try again.       |
| 16  | Redirection failed. Verify the parameter configuration or the network connection, or try again.      |
| 17  | Protocol error. The server returns a 4XX or 5XX status code. Verify the parameter configuration and try again.|
| 20  | Other errors. Verify the parameter configuration or the network connection, or try again.       |

## File
Defines the file list in [UploadConfig<sup>6+<sup>](#uploadconfig6).

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| filename | string | Yes| File name in the header when **multipart** is used.|
| name | string | Yes| Name of a form item when **multipart** is used. The default value is **file**.|
| uri | string | Yes| Local path for storing files.<br>Only the **internal** protocol is currently supported. **internal://cache/** is the private directory of the application and is mandatory. Example:<br>internal://cache/path/to/file.txt |
| type | string | Yes| Type of the file content. By default, the type is obtained based on the extension of the file name or URI.|


## RequestData
Defines the form data in [UploadConfig<sup>6+<sup>](#uploadconfig6).

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| name | string | Yes| Name of a form element.|
| value | string | Yes| Value of a form element.|

## request.downloadFile<sup>9+</sup>

downloadFile(context: BaseContext, config: DownloadConfig): Promise&lt;DownloadTask&gt;

Downloads files. This API uses a promise to return the result. You can use [on('complete'|'pause'|'remove')<sup>7+</sup>](#oncompletepauseremove7) to obtain the download task state, which can be completed, paused, or removed. You can also use [on('fail')<sup>7+</sup>](#onfail7) to obtain the task download error information.


**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | context | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md) | Yes| Application-based context.|
  | config | [DownloadConfig](#downloadconfig) | Yes| Download configuration.|

**Return value**

  | Type| Description|
  | -------- | -------- |
  | Promise&lt;[DownloadTask](#downloadtask)&gt; | Promise used to return the download task.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400001 | file operation error. |
  | 13400002 | bad file path. |
  | 13400003 | task service ability error. |

**Example**

  ```ts
import { BusinessError } from '@ohos.base';

  try {
    // Replace the URL with the HTTP address of the real server.
    request.downloadFile(getContext(), { url: 'https://xxxx/xxxx.hap' }).then((data: request.DownloadTask) => {
       let downloadTask: request.DownloadTask = data;
    }).catch((err: BusinessError) => {
      console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
    })
  } catch (err) {
    console.error(`Failed to request the download. err: ${JSON.stringify(err)}`);
  }
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).


## request.downloadFile<sup>9+</sup>

downloadFile(context: BaseContext, config: DownloadConfig, callback: AsyncCallback&lt;DownloadTask&gt;): void;

Downloads files. This API uses an asynchronous callback to return the result. You can use [on('complete'|'pause'|'remove')<sup>7+</sup>](#oncompletepauseremove7) to obtain the download task state, which can be completed, paused, or removed. You can also use [on('fail')<sup>7+</sup>](#onfail7) to obtain the task download error information.


**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | context | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md) | Yes| Application-based context.|
  | config | [DownloadConfig](#downloadconfig) | Yes| Download configuration.|
  | callback | AsyncCallback&lt;[DownloadTask](#downloadtask)&gt; | Yes| Callback used to return the download task.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400001 | file operation error. |
  | 13400002 | bad file path. |
  | 13400003 | task service ability error. |

**Example**

  ```ts
import { BusinessError } from '@ohos.base';

  try {
    // Replace the URL with the HTTP address of the real server.
    request.downloadFile(getContext(), {
      url: 'https://xxxx/xxxxx.hap',
      filePath: 'xxx/xxxxx.hap'
    }, (err: BusinessError, data: request.DownloadTask) => {
      if (err) {
        console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
        return;
      }
      let downloadTask: request.DownloadTask = data;
    });
  } catch (err) {
    console.error(`Failed to request the download. err: ${JSON.stringify(err)}`);
  }
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

## request.download<sup>(deprecated)</sup>

download(config: DownloadConfig): Promise&lt;DownloadTask&gt;

Downloads files. This API uses a promise to return the result.

> **NOTE**
>
> This API is deprecated since API version 9. You are advised to use [request.downloadFile<sup>9+</sup>](#requestdownloadfile9) instead.

**Model restriction**: This API can be used only in the FA model.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | config | [DownloadConfig](#downloadconfig) | Yes| Download configuration.|

**Return value**

  | Type| Description|
  | -------- | -------- |
  | Promise&lt;[DownloadTask](#downloadtask)&gt; | Promise used to return the download task.|

**Example**

  ```js
  let downloadTask;
  // Replace the URL with the HTTP address of the real server.
  request.download({ url: 'https://xxxx/xxxx.hap' }).then((data) => {
    downloadTask = data;
  }).catch((err) => {
    console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
  })
  ```


## request.download<sup>(deprecated)</sup>

download(config: DownloadConfig, callback: AsyncCallback&lt;DownloadTask&gt;): void

Downloads files. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is deprecated since API version 9. You are advised to use [request.downloadFile<sup>9+</sup>](#requestdownloadfile9-1) instead.

**Model restriction**: This API can be used only in the FA model.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | config | [DownloadConfig](#downloadconfig) | Yes| Download configuration.|
  | callback | AsyncCallback&lt;[DownloadTask](#downloadtask)&gt; | Yes| Callback used to return the download task.|

**Example**

  ```js
  let downloadTask;
  // Replace the URL with the HTTP address of the real server.
  request.download({ url: 'https://xxxx/xxxxx.hap', 
  filePath: 'xxx/xxxxx.hap'}, (err, data) => {
    if (err) {
      console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
      return;
    }
    downloadTask = data;
  });
  ```

## DownloadTask

Implements file downloads. Before using any APIs of this class, you must obtain a **DownloadTask** object through [request.downloadFile<sup>9+</sup>](#requestdownloadfile9) in promise mode or [request.downloadFile<sup>9+</sup>](#requestdownloadfile9-1) in callback mode.


### on('progress')

on(type: 'progress', callback:(receivedSize: number, totalSize: number) =&gt; void): void

Subscribes to download progress events. This API uses a callback to return the result asynchronously.

> **NOTE**
>
> To maintain a balance between power consumption and performance, this API cannot be called when the application is running in the background.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Type of the event to subscribe to. The value is **'progress'** (download progress).|
  | callback | function | Yes| Callback used to return the result.|

  Parameters of the callback function

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| receivedSize | number | Yes| Size of the downloaded files, in bytes.|
| totalSize | number | Yes| Total size of the files to download, in bytes.|

**Example**

  ```ts
import { BusinessError } from '@ohos.base';

  try {
    // Replace the URL with the HTTP address of the real server.
    request.downloadFile(getContext(), { url: 'https://xxxx/xxxx.hap' }).then((data: request.DownloadTask) => {
      let downloadTask: request.DownloadTask = data;
      let progressCallback = (receivedSize: number, totalSize: number) => {
        console.info("download receivedSize:" + receivedSize + " totalSize:" + totalSize);
      };
      downloadTask.on('progress', progressCallback);
    }).catch((err: BusinessError) => {
      console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
    })
  } catch (err) {
    console.error(`Failed to request the download. err: ${JSON.stringify(err)}`);
  }
  ```


### off('progress')

off(type: 'progress', callback?: (receivedSize: number, totalSize: number) =&gt; void): void

Unsubscribes from download progress events.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Type of the event to unsubscribe from. The value is **'progress'** (download progress).|
  | callback | function | No| Callback to unregister. If this parameter is not specified, all callbacks of the current type will be unregistered.<br>**receivedSize**: size of the downloaded files.<br>**totalSize**: total size of the files to download.|

**Example**

  ```ts
import { BusinessError } from '@ohos.base';

try {
  // Replace the URL with the HTTP address of the real server.
  request.downloadFile(getContext(), { url: 'https://xxxx/xxxx.hap' }).then((data: request.DownloadTask) => {
    let downloadTask: request.DownloadTask = data;
    let progressCallback1 = (receivedSize: number, totalSize: number) => {
      console.info('Download delete progress notification.' + 'receivedSize:' + receivedSize + 'totalSize:' + totalSize);
    };
    let progressCallback2 = (receivedSize: number, totalSize: number) => {
      console.info('Download delete progress notification.' + 'receivedSize:' + receivedSize + 'totalSize:' + totalSize);
    };
    downloadTask.on('progress', progressCallback1);
    downloadTask.on('progress', progressCallback2);
    // Unsubscribe from progressCallback1.
    downloadTask.off('progress', progressCallback1);
    // Unsubscribe from all callbacks of download progress events.
    downloadTask.off('progress');
  }).catch((err: BusinessError) => {
    console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
  })
} catch (err) {
  console.error(`Failed to request the download. err: ${JSON.stringify(err)}`);
}
  ```


### on('complete'|'pause'|'remove')<sup>7+</sup>

on(type: 'complete'|'pause'|'remove', callback:() =&gt; void): void

Subscribes to download events. This API uses a callback to return the result asynchronously.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Type of the event to subscribe to.<br>- **'complete'**: download task completion event.<br>- **'pause'**: download task pause event.<br>- **'remove'**: download task removal event.|
  | callback | function | Yes| Callback used to return the result.|

**Example**

  ```ts
import { BusinessError } from '@ohos.base';

try {
  // Replace the URL with the HTTP address of the real server.
  request.downloadFile(getContext(), { url: 'https://xxxx/xxxx.hap' }).then((data: request.DownloadTask) => {
    let downloadTask: request.DownloadTask = data;
    let completeCallback = () => {
      console.info('Download task completed.');
    };
    downloadTask.on('complete', completeCallback);

    let pauseCallback = () => {
      console.info('Download task pause.');
    };
    downloadTask.on('pause', pauseCallback);

    let removeCallback = () => {
      console.info('Download task remove.');
    };
    downloadTask.on('remove', removeCallback);
  }).catch((err: BusinessError) => {
    console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
  })
} catch (err) {
  console.error(`Failed to request the download. err: ${JSON.stringify(err)}`);
}
  ```


### off('complete'|'pause'|'remove')<sup>7+</sup>

off(type: 'complete'|'pause'|'remove', callback?:() =&gt; void): void

Unsubscribes from download events.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Type of the event to unsubscribe from.<br>- **'complete'**: download task completion event.<br>- **'pause'**: download task pause event.<br>- **'remove'**: download task removal event.|
  | callback | function | No| Callback to unregister. If this parameter is not specified, all callbacks of the current type will be unregistered.|

**Example**

  ```ts
import { BusinessError } from '@ohos.base';

try {
  // Replace the URL with the HTTP address of the real server.
  request.downloadFile(getContext(), { url: 'https://xxxx/xxxx.hap' }).then((data: request.DownloadTask) => {
    let downloadTask: request.DownloadTask = data;
    let completeCallback1 = () => {
      console.info('Download delete complete notification.');
    };
    let completeCallback2 = () => {
      console.info('Download delete complete notification.');
    };
    downloadTask.on('complete', completeCallback1);
    downloadTask.on('complete', completeCallback2);
    // Unsubscribe from completeCallback1.
    downloadTask.off('complete', completeCallback1);
    // Unsubscribe from all callbacks of the download completion events.
    downloadTask.off('complete');

    let pauseCallback1 = () => {
      console.info('Download delete pause notification.');
    };
    let pauseCallback2 = () => {
      console.info('Download delete pause notification.');
    };
    downloadTask.on('pause', pauseCallback1);
    downloadTask.on('pause', pauseCallback2);
    // Unsubscribe from pauseCallback1.
    downloadTask.off('pause', pauseCallback1);
    // Unsubscribe from all callbacks of the download pause events.
    downloadTask.off('pause');

    let removeCallback1 = () => {
      console.info('Download delete remove notification.');
    };
    let removeCallback2 = () => {
      console.info('Download delete remove notification.');
    };
    downloadTask.on('remove', removeCallback1);
    downloadTask.on('remove', removeCallback2);
    // Unsubscribe from removeCallback1.
    downloadTask.off('remove', removeCallback1);
    // Unsubscribe from all callbacks of the download removal events.
    downloadTask.off('remove');
  }).catch((err: BusinessError) => {
    console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
  })
} catch (err) {
  console.error(`Failed to request the download. err: ${JSON.stringify(err)}`);
}
  
  ```


### on('fail')<sup>7+</sup>

on(type: 'fail', callback: (err: number) =&gt; void): void

Subscribes to download failure events. This API uses a callback to return the result asynchronously.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Type of the event to subscribe to. The value is **'fail'** (download failure).|
  | callback | function | Yes| Callback for the download task failure event.|

  Parameters of the callback function

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| err | number | Yes| Error code of the download failure. For details about the error codes, see [Download Error Codes](#download-error-codes).|

**Example**

  ```ts
import { BusinessError } from '@ohos.base';

try {
  // Replace the URL with the HTTP address of the real server.
  request.downloadFile(getContext(), { url: 'https://xxxx/xxxx.hap' }).then((data: request.DownloadTask) => {
    let downloadTask: request.DownloadTask = data;
    let failCallback = (err: number) => {
      console.error(`Failed to download the task. Code: ${err}`);
    };
    downloadTask.on('fail', failCallback);
  }).catch((err: BusinessError) => {
    console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
  })
} catch (err) {
  console.error(`Failed to request the download. err: ${JSON.stringify(err)}`);
}
  ```


### off('fail')<sup>7+</sup>

off(type: 'fail', callback?: (err: number) =&gt; void): void

Unsubscribes from download failure events.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Type of the event to unsubscribe from. The value is **'fail'** (download failure).|
  | callback | function | No| Callback to unregister. If this parameter is not specified, all callbacks of the current type will be unregistered.|

**Example**

  ```ts
import { BusinessError } from '@ohos.base';

try {
  // Replace the URL with the HTTP address of the real server.
  request.downloadFile(getContext(), { url: 'https://xxxx/xxxx.hap' }).then((data: request.DownloadTask) => {
    let downloadTask: request.DownloadTask = data;
    let failCallback1 = (err: number) => {
      console.error(`Failed to download the task. Code: ${err}`);
    };
    let failCallback2 = (err: number) => {
      console.error(`Failed to download the task. Code: ${err}`);
    };
    downloadTask.on('fail', failCallback1);
    downloadTask.on('fail', failCallback2);
    // Unsubscribe from failCallback1.
    downloadTask.off('fail', failCallback1);
    // Unsubscribe from all callbacks of the download failure events.
    downloadTask.off('fail');
  }).catch((err: BusinessError) => {
    console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
  })
} catch (err) {
  console.error(`Failed to request the download. err: ${JSON.stringify(err)}`);
}
  ```

### delete<sup>9+</sup>

delete(): Promise&lt;boolean&gt;

Deletes this download task. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Return value**

  | Type| Description|
  | -------- | -------- |
  | Promise&lt;boolean&gt; | Promise used to return the result. The value **true** indicates that the operation is successful, and the value **false** indicates the opposite.|

**Example**

  ```ts
import { BusinessError } from '@ohos.base';

try {
  // Replace the URL with the HTTP address of the real server.
  request.downloadFile(getContext(), { url: 'https://xxxx/xxxx.hap' }).then((data: request.DownloadTask) => {
    let downloadTask: request.DownloadTask = data;
    downloadTask.delete().then((result: boolean) => {
      console.info('Succeeded in removing the download task.');
    }).catch((err: BusinessError) => {
      console.error(`Failed to remove the download task. Code: ${err.code}, message: ${err.message}`);
    });
  }).catch((err: BusinessError) => {
    console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
  })
} catch (err) {
  console.error(`Failed to request the download. err: ${JSON.stringify(err)}`);
}
  ```


### delete<sup>9+</sup>

delete(callback: AsyncCallback&lt;boolean&gt;): void

Deletes this download task. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | Yes| Callback used to return the result. The value **true** indicates that the operation is successful, and the value **false** indicates the opposite.|

**Example**

  ```ts
import { BusinessError } from '@ohos.base';

try {
  // Replace the URL with the HTTP address of the real server.
  request.downloadFile(getContext(), { url: 'https://xxxx/xxxx.hap' }).then((data: request.DownloadTask) => {
    let downloadTask: request.DownloadTask = data;
    downloadTask.delete((err: BusinessError, result: boolean) => {
      if (err) {
        console.error(`Failed to remove the download task. Code: ${err.code}, message: ${err.message}`);
        return;
      }
      console.info('Succeeded in removing the download task.');
    });
  }).catch((err: BusinessError) => {
    console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
  })
} catch (err) {
  console.error(`Failed to request the download. err: ${JSON.stringify(err)}`);
}
  ```


### getTaskInfo<sup>9+</sup>

getTaskInfo(): Promise&lt;DownloadInfo&gt;

Obtains the information about this download task. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Return value**

  | Type| Description|
  | -------- | -------- |
  | Promise&lt;[DownloadInfo](#downloadinfo7)&gt; |  Promise used to return the download task information.|

**Example**

  ```ts
import { BusinessError } from '@ohos.base';

try {
  // Replace the URL with the HTTP address of the real server.
  request.downloadFile(getContext(), { url: 'https://xxxx/xxxx.hap' }).then((data: request.DownloadTask) => {
    let downloadTask: request.DownloadTask = data;
    downloadTask.getTaskInfo().then((downloadInfo: request.DownloadInfo) => {
      console.info('Succeeded in querying the download task')
    }).catch((err: BusinessError) => {
      console.error(`Failed to query the download task. Code: ${err.code}, message: ${err.message}`)
    });
  }).catch((err: BusinessError) => {
    console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
  })
} catch (err) {
  console.error(`Failed to request the download. err: ${JSON.stringify(err)}`);
} 
  ```


### getTaskInfo<sup>9+</sup>

getTaskInfo(callback: AsyncCallback&lt;DownloadInfo&gt;): void

Obtains the information about this download task. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;[DownloadInfo](#downloadinfo7)&gt; | Yes| Callback used to return the download task information.|

**Example**

  ```ts
import { BusinessError } from '@ohos.base';

try {
  // Replace the URL with the HTTP address of the real server.
  request.downloadFile(getContext(), { url: 'https://xxxx/xxxx.hap' }).then((data: request.DownloadTask) => {
    let downloadTask: request.DownloadTask = data;
    downloadTask.getTaskInfo((err: BusinessError, downloadInfo: request.DownloadInfo) => {
      if (err) {
        console.error(`Failed to query the download mimeType. Code: ${err.code}, message: ${err.message}`);
      } else {
        console.info('Succeeded in querying the download mimeType');
      }
    });
  }).catch((err: BusinessError) => {
    console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
  })
} catch (err) {
  console.error(`Failed to request the download. err: ${JSON.stringify(err)}`);
}
  ```


### getTaskMimeType<sup>9+</sup>

getTaskMimeType(): Promise&lt;string&gt;

Queries **MimeType** (that is, media type of resources) of a download task. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Return value**

  | Type| Description|
  | -------- | -------- |
  | Promise&lt;string&gt; | Promise used to return the **MimeType** of the download task.|

**Example**

  ```ts
import { BusinessError } from '@ohos.base';

try {
  // Replace the URL with the HTTP address of the real server.
  request.downloadFile(getContext(), { url: 'https://xxxx/xxxx.hap' }).then((data: request.DownloadTask) => {
    let downloadTask: request.DownloadTask = data;
    downloadTask.getTaskMimeType().then((data: string) => {
      console.info('Succeeded in querying the download MimeType');
    }).catch((err: BusinessError) => {
      console.error(`Failed to query the download MimeType. Code: ${err.code}, message: ${err.message}`)
    });
  }).catch((err: BusinessError) => {
    console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
  })
} catch (err) {
  console.error(`Failed to request the download. err: ${JSON.stringify(err)}`);
}
  ```


### getTaskMimeType<sup>9+</sup>

getTaskMimeType(callback: AsyncCallback&lt;string&gt;): void;

Obtains the **MimeType** of this download task. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;string&gt; | Yes| Callback used to return the **MimeType** of the download task.|

**Example**

  ```ts
import { BusinessError } from '@ohos.base';

try {
  // Replace the URL with the HTTP address of the real server.
  request.downloadFile(getContext(), { url: 'https://xxxx/xxxx.hap' }).then((data: request.DownloadTask) => {
    let downloadTask: request.DownloadTask = data;
    downloadTask.getTaskMimeType((err: BusinessError, data: string) => {
      if (err) {
        console.error(`Failed to query the download mimeType. Code: ${err.code}, message: ${err.message}`);
      } else {
        console.info('Succeeded in querying the download mimeType');
      }
    });
  }).catch((err: BusinessError) => {
    console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
  })
} catch (err) {
  console.error(`Failed to request the download. err: ${JSON.stringify(err)}`);
}
  ```


### suspend<sup>9+</sup>

suspend(): Promise&lt;boolean&gt;

Pauses this download task. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Return value**

  | Type| Description|
  | -------- | -------- |
  | Promise&lt;boolean&gt; | Promise used to return the result.|

**Example**

  ```ts
import { BusinessError } from '@ohos.base';

try {
  // Replace the URL with the HTTP address of the real server.
  request.downloadFile(getContext(), { url: 'https://xxxx/xxxx.hap' }).then((data: request.DownloadTask) => {
    let downloadTask: request.DownloadTask = data;
    downloadTask.suspend().then((result: boolean) => {
      console.info('Succeeded in pausing the download task.');
    }).catch((err: BusinessError) => {
      console.error(`Failed to pause the download task. Code: ${err.code}, message: ${err.message}`);
    });
  }).catch((err: BusinessError) => {
    console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
  })
} catch (err) {
  console.error(`Failed to request the download. err: ${JSON.stringify(err)}`);
}
  ```


### suspend<sup>9+</sup>

suspend(callback: AsyncCallback&lt;boolean&gt;): void

Pauses this download task. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | Yes| Callback used to return the result.|

**Example**

  ```ts
import { BusinessError } from '@ohos.base';

try {
  // Replace the URL with the HTTP address of the real server.
  request.downloadFile(getContext(), { url: 'https://xxxx/xxxx.hap' }).then((data: request.DownloadTask) => {
    let downloadTask: request.DownloadTask = data;
    downloadTask.suspend((err: BusinessError, result: boolean) => {
      if (err) {
        console.error(`Failed to pause the download task. Code: ${err.code}, message: ${err.message}`);
        return;
      }
      console.info('Succeeded in pausing the download task.');
    });
  }).catch((err: BusinessError) => {
    console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
  })
} catch (err) {
  console.error(`Failed to request the download. err: ${JSON.stringify(err)}`);
}
  ```


### restore<sup>9+</sup>

restore(): Promise&lt;boolean&gt;

Resumes this download task. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Return value**

  | Type| Description|
  | -------- | -------- |
  | Promise&lt;boolean&gt; | Promise used to return the result.|

**Example**

  ```ts
import { BusinessError } from '@ohos.base';

try {
  // Replace the URL with the HTTP address of the real server.
  request.downloadFile(getContext(), { url: 'https://xxxx/xxxx.hap' }).then((data: request.DownloadTask) => {
    let downloadTask: request.DownloadTask = data;
    downloadTask.restore().then((result: boolean) => {
      console.info('Succeeded in resuming the download task.')
    }).catch((err: BusinessError) => {
      console.error(`Failed to resume the download task. Code: ${err.code}, message: ${err.message}`);
    });
  }).catch((err: BusinessError) => {
    console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
  })
} catch (err) {
  console.error(`Failed to request the download. err: ${JSON.stringify(err)}`);
}
  ```


### restore<sup>9+</sup>

restore(callback: AsyncCallback&lt;boolean&gt;): void

Resumes this download task. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | Yes| Callback used to return the result.|

**Example**

  ```ts
import { BusinessError } from '@ohos.base';

try {
  // Replace the URL with the HTTP address of the real server.
  request.downloadFile(getContext(), { url: 'https://xxxx/xxxx.hap' }).then((data: request.DownloadTask) => {
    let downloadTask: request.DownloadTask = data;
    downloadTask.restore((err: BusinessError, result: boolean) => {
      if (err) {
        console.error(`Failed to resume the download task. Code: ${err.code}, message: ${err.message}`);
        return;
      }
      console.info('Succeeded in resuming the download task.');
    });
  }).catch((err: BusinessError) => {
    console.error(`Failed to request the download. Code: ${err.code}, message: ${err.message}`);
  })
} catch (err) {
  console.error(`Failed to request the download. err: ${JSON.stringify(err)}`);
}
  ```


### remove<sup>(deprecated)</sup>

remove(): Promise&lt;boolean&gt;

Removes this download task. This API uses a promise to return the result.

> **NOTE**
>
> This API is deprecated since API version 9. You are advised to use [delete<sup>9+</sup>](#delete9-2) instead.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Return value**

  | Type| Description|
  | -------- | -------- |
  | Promise&lt;boolean&gt; | Promise used to return the result.|

**Example**

  ```js
  downloadTask.remove().then((result) => {
    console.info('Succeeded in removing the download task.');
  }).catch ((err) => {
    console.error(`Failed to remove the download task. Code: ${err.code}, message: ${err.message}`);
  });
  ```


### remove<sup>(deprecated)</sup>

remove(callback: AsyncCallback&lt;boolean&gt;): void

Removes this download task. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is deprecated since API version 9. You are advised to use [delete<sup>9+</sup>](#delete9-3) instead.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | Yes| Callback used to return the result.|

**Example**

  ```js
  downloadTask.remove((err, result)=>{
    if(err) {
      console.error(`Failed to remove the download task. Code: ${err.code}, message: ${err.message}`);
      return;
    }
    console.info('Succeeded in removing the download task.');
  });
  ```


### query<sup>(deprecated)</sup>

query(): Promise&lt;DownloadInfo&gt;

Queries this download task. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and is deprecated since API version 9. You are advised to use [getTaskInfo<sup>9+</sup>](#gettaskinfo9) instead.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Return value**

  | Type| Description|
  | -------- | -------- |
  | Promise&lt;[DownloadInfo](#downloadinfo7)&gt; | Promise used to return the download task information.|

**Example**

  ```js
  downloadTask.query().then((downloadInfo) => {    
    console.info('Succeeded in querying the download task.')
  }) .catch((err) => {
    console.error(`Failed to query the download task. Code: ${err.code}, message: ${err.message}`)
  });
  ```


### query<sup>(deprecated)</sup>

query(callback: AsyncCallback&lt;DownloadInfo&gt;): void

Queries this download task. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and is deprecated since API version 9. You are advised to use [getTaskInfo<sup>9+</sup>](#gettaskinfo9-1) instead.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;[DownloadInfo](#downloadinfo7)&gt; | Yes| Callback used to return the download task information.|

**Example**

  ```js
  downloadTask.query((err, downloadInfo)=>{
    if(err) {
      console.error(`Failed to query the download mimeType. Code: ${err.code}, message: ${err.message}`);
    } else {
      console.info('Succeeded in querying the download task.');
    }
  });
  ```


### queryMimeType<sup>(deprecated)</sup>

queryMimeType(): Promise&lt;string&gt;

Queries the **MimeType** of this download task. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and is deprecated since API version 9. You are advised to use [getTaskMimeType<sup>9+</sup>](#gettaskmimetype9) instead.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Return value**

  | Type| Description|
  | -------- | -------- |
  | Promise&lt;string&gt; | Promise used to return the **MimeType** of the download task.|

**Example**

  ```js
  downloadTask.queryMimeType().then((data) => {    
    console.info('Succeeded in querying the download MimeType.');
  }).catch((err) => {
    console.error(`Failed to query the download MimeType. Code: ${err.code}, message: ${err.message}`)
  });
  ```


### queryMimeType<sup>(deprecated)</sup>

queryMimeType(callback: AsyncCallback&lt;string&gt;): void;

Queries the **MimeType** of this download task. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and is deprecated since API version 9. You are advised to use [getTaskMimeType<sup>9+</sup>](#gettaskmimetype9-1) instead.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;string&gt; | Yes| Callback used to return the **MimeType** of the download task.|

**Example**

  ```js
  downloadTask.queryMimeType((err, data)=>{
    if(err) {
      console.error(`Failed to query the download mimeType. Code: ${err.code}, message: ${err.message}`);
    } else {
      console.info('Succeeded in querying the download mimeType.');
    }
  });
  ```


### pause<sup>(deprecated)</sup>

pause(): Promise&lt;void&gt;

Pauses this download task. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and is deprecated since API version 9. You are advised to use [suspend<sup>9+</sup>](#suspend9) instead.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Return value**

  | Type| Description|
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise used to return the result.|

**Example**

  ```js
  downloadTask.pause().then((result) => {    
    console.info('Succeeded in pausing the download task.');
  }).catch((err) => {
    console.error(`Failed to pause the download task. Code: ${err.code}, message: ${err.message}`);
  });
  ```


### pause<sup>(deprecated)</sup>

pause(callback: AsyncCallback&lt;void&gt;): void

> **NOTE**
>
> This API is supported since API version 7 and is deprecated since API version 9. You are advised to use [suspend<sup>9+</sup>](#suspend9-1) instead.

Pauses this download task. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

**Example**

  ```js
  downloadTask.pause((err, result)=>{
    if(err) {
      console.error(`Failed to pause the download task. Code: ${err.code}, message: ${err.message}`);
      return;
    }
    console.info('Succeeded in pausing the download task.');
  });
  ```


### resume<sup>(deprecated)</sup>

resume(): Promise&lt;void&gt;

Resumes this download task. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and is deprecated since API version 9. You are advised to use [restore<sup>9+</sup>](#restore9) instead.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Return value**

  | Type| Description|
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise used to return the result.|

**Example**

  ```js
  downloadTask.resume().then((result) => {
    console.info('Succeeded in resuming the download task.')
  }).catch((err) => {
    console.error(`Failed to resume the download task. Code: ${err.code}, message: ${err.message}`);
  });
  ```


### resume<sup>(deprecated)</sup>

resume(callback: AsyncCallback&lt;void&gt;): void

> **NOTE**
>
> This API is supported since API version 7 and is deprecated since API version 9. You are advised to use [restore<sup>9+</sup>](#restore9-1) instead.

Resumes this download task. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

**Example**

  ```js
  downloadTask.resume((err, result)=>{
    if (err) {
      console.error(`Failed to resume the download task. Code: ${err.code}, message: ${err.message}`);
      return;
    }
    console.info('Succeeded in resuming the download task.');
  });
  ```


## DownloadConfig
Defines the download task configuration.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| url | string | Yes| Resource URL.|
| header | Object | No| HTTPS flag header to be included in the download request.<br>The **X-TLS-Version** parameter in **header** specifies the TLS version to be used. If this parameter is not set, the CURL_SSLVERSION_TLSv1_2 version is used. Available options are as follows:<br>CURL_SSLVERSION_TLSv1_0<br>CURL_SSLVERSION_TLSv1_1<br>CURL_SSLVERSION_TLSv1_2<br>CURL_SSLVERSION_TLSv1_3<br>The **X-Cipher-List** parameter in **header** specifies the cipher suite list to be used. If this parameter is not specified, the secure cipher suite list is used. Available options are as follows:<br>- The TLS 1.2 cipher suite list includes the following ciphers:<br>TLS_DHE_RSA_WITH_AES_128_GCM_SHA256,TLS_DHE_RSA_WITH_AES_256_GCM_SHA384,<br>TLS_DHE_DSS_WITH_AES_128_GCM_SHA256,TLS_DSS_RSA_WITH_AES_256_GCM_SHA384,<br>TLS_PSK_WITH_AES_256_GCM_SHA384,TLS_DHE_PSK_WITH_AES_128_GCM_SHA256,<br>TLS_DHE_PSK_WITH_AES_256_GCM_SHA384,TLS_DHE_PSK_WITH_CHACHA20_POLY1305_SHA256,<br>TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256,TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384,<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256,TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384,<br>TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256,TLS_ECDHE_PSK_WITH_CHACHA20_POLY1305_SHA256,<br>TLS_ECDHE_PSK_WITH_AES_128_GCM_SHA256,TLS_ECDHE_PSK_WITH_AES_256_GCM_SHA384,<br>TLS_ECDHE_PSK_WITH_AES_128_GCM_SHA256,TLS_DHE_RSA_WITH_AES_128_CCM,<br>TLS_DHE_RSA_WITH_AES_256_CCM,TLS_DHE_RSA_WITH_CHACHA20_POLY1305_SHA256,<br>TLS_PSK_WITH_AES_256_CCM,TLS_DHE_PSK_WITH_AES_128_CCM,<br>TLS_DHE_PSK_WITH_AES_256_CCM,TLS_ECDHE_ECDSA_WITH_AES_128_CCM,<br>TLS_ECDHE_ECDSA_WITH_AES_256_CCM,TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256<br>- The TLS 1.3 cipher suite list includes the following ciphers:<br>TLS_AES_128_GCM_SHA256,TLS_AES_256_GCM_SHA384,TLS_CHACHA20_POLY1305_SHA256,TLS_AES_128_CCM_SHA256<br>- The TLS 1.3 cipher suite list adds the Chinese national cryptographic algorithm:<br>TLS_SM4_GCM_SM3,TLS_SM4_CCM_SM3 |
| enableMetered | boolean | No| Whether download is allowed on a metered connection. The default value is **false**. In general cases, a mobile data connection is metered, while a Wi-Fi connection is not.<br>- **true**: allowed<br>- **false**: not allowed|
| enableRoaming | boolean | No| Whether download is allowed on a roaming network. The default value is **false**.<br>- **true**: allowed<br>- **false**: not allowed|
| description | string | No| Description of the download session.|
| filePath<sup>7+</sup> | string | No| Path where the downloaded file is stored.<br>- In the FA model, use [context](../apis-ability-kit/js-apis-inner-app-context.md#contextgetcachedir) to obtain the application storage path.<br>- In the stage model, use [AbilityContext](../apis-ability-kit/js-apis-inner-application-context.md) to obtain the application storage path.|
| networkType | number | No| Network type allowed for the download. The default value is **NETWORK_MOBILE and NETWORK_WIFI**.<br>- NETWORK_MOBILE: 0x00000001<br>- NETWORK_WIFI: 0x00010000|
| title | string | No| Download task name.|
| background<sup>9+</sup> | boolean | No| Whether to enable background task notification so that the download status is displayed in the notification panel. The default value is false.|


## DownloadInfo<sup>7+</sup>
Defines the download task information, which is the callback parameter of the [getTaskInfo<sup>9+</sup>](#gettaskinfo9) API.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.MiscServices.Download

| Name| Type|Mandatory|  Description|
| -------- | -------- | -------- | -------- |
| downloadId | number |Yes| ID of the download task.|
| failedReason | number|Yes| Cause of the download failure. The value can be any constant in [Download Error Codes](#download-error-codes).|
| fileName | string |Yes| Name of the downloaded file.|
| filePath | string |Yes| URI of the saved file.|
| pausedReason | number |Yes| Cause of download pause. The value can be any constant in [Causes of Download Pause](#causes-of-download-pause).|
| status | number |Yes| Download task status code. The value can be any constant in [Download Task Status Codes](#download-task-status-codes).|
| targetURI | string |Yes| URI of the downloaded file.|
| downloadTitle | string |Yes| Name of the download task.|
| downloadTotalBytes | number |Yes| Total size of the files to download, in bytes.|
| description | string |Yes| Description of the download task.|
| downloadedBytes | number |Yes| Size of the files downloaded, in bytes.|

## Action<sup>10+</sup>  

Defines action options.

**System capability**: SystemCapability.Request.FileTransferAgent

| Name| Value|Description|
| -------- | -------- |-------- |
| DOWNLOAD | 0 |Download.|
| UPLOAD | 1 |Upload.|


## Mode<sup>10+</sup>  
Defines mode options.<br>
After an application is switched to the background for a period of time, background tasks are not affected but foreground tasks will fail or pause.

**System capability**: SystemCapability.Request.FileTransferAgent

| Name| Value|Description|
| -------- | -------- |-------- |
| BACKGROUND | 0 |Background task.|
| FOREGROUND | 1 |Foreground task.|

## Network<sup>10+</sup>  

Defines network options.<br>
If the network does not meet the preset conditions, the tasks that have not been executed will await for execution, and the tasks that are being executed will fail or pause.

**System capability**: SystemCapability.Request.FileTransferAgent

| Name| Value|Description|
| -------- | -------- |-------- |
| ANY | 0 |Network of any type.|
| WIFI | 1 |Wi-Fi network.|
| CELLULAR | 2 |Cellular data network.|

## BroadcastEvent<sup>11+</sup>

Defines a custom system event. You can use a common event API to obtain the event.
The upload and download SA has the **ohos.permission.SEND_TASK_COMPLETE_EVENT** permission. You can configure the level-2 configuration file to which the metadata of an event points to intercept other event senders.

You can use the **CommonEventData** type to transmit data related to common events. The members in **CommonEventData** are different from those described in [CommonEventData](js-apis-inner-commonEvent-commonEventData.md). Specifically, **CommonEventData.code** indicates the task status, which is **0x40 COMPLETE** or **0x41 FAILED**, and **CommonEventData.data** indicates the task ID.

For details about event configuration information, see [Subscribing to Common Events in Static Mode (for System Applications Only)](../../basic-services/common-event/common-event-static-subscription.md).

**System capability**: SystemCapability.Request.FileTransferAgent

| Name| Value| Description       |
| -------- | ------- |-----------|
| COMPLETE | 'ohos.request.event.COMPLETE' | Task completion event.|

## FileSpec<sup>10+</sup> 
Provides the file information of a table item.

**System capability**: SystemCapability.Request.FileTransferAgent

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| path | string | Yes| Relative path in the cache folder of the invoker.|
| mimeType | string | No| MIME type of the file, which is obtained from the file name.|
| filename | string | No| File name. The default value is obtained from the file path.|
| extras | Object | No| Additional information of the file.|


## FormItem<sup>10+</sup> 
Describes the form item of a task.

**System capability**: SystemCapability.Request.FileTransferAgent

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| name | string | Yes| Form parameter name.|
| value | string \| [FileSpec](#filespec10) \| Array&lt;[FileSpec](#filespec10)&gt; | Yes| Form parameter value.|


## Config<sup>10+</sup> 
Provides the configuration information of an upload or download task.

**System capability**: SystemCapability.Request.FileTransferAgent

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| action | [Action](#action10) | Yes| Task action.<br>- **UPLOAD**<br>- **DOWNLOAD**|
| url | string | Yes| Resource URL. The value contains a maximum of 2048 characters.|
| title | string | No| Task title. The value contains a maximum of 256 characters. The default value is **upload** or **download** in lowercase. Set the value to that of **action**.|
| description | string | No| Task description. The value contains a maximum of 1024 characters. The default value is a null string.|
| mode | [Mode](#mode10) | No| Task mode. The default mode is background.|
| overwrite | boolean | No| Whether to overwrite an existing file during the download. The default value is **false**.<br>- **true**: Overwrite the existing file.<br>- **false**: Do not overwrite the existing file. In this case, the download fails.|
| method | string | No| Standard HTTP method for the task. The value can be **GET**, **POST**, or **PUT**, which is case-insensitive.<br>- If the task is an upload, use **PUT** or **POST**. The default value is **PUT**.<br>- If the task is a download, use **GET** or **POST**. The default value is **GET**.|
| headers | object | No| HTTP headers to be included in the task.<br>- If the task is an upload, the default **Content-Type** is **multipart/form-data**.<br>- If the task is a download, the default **Content-Type** is **application/json**.|
| data | string \| Array&lt;[FormItem](#formitem10)&gt; | No| Task data.<br>- If the task is a download, the value is a string, typically in JSON format (an object will be converted to a JSON string); the default value is null.<br>- If the task is an upload, the value is Array<[FormItem](#formitem10)>; the default value is null.|
| saveas | string | No| Path for storing downloaded files. The options are as follows:<br>- Relative path in the cache folder of the invoker, for example, **"./xxx/yyy/zzz.html"** and **"xxx/yyy/zzz.html"**.<br>- URI (applicable when the application has the permission to access the URI), for example, **"datashare://bundle/xxx/yyy/zzz.html"**. This function is not supported currently.<br>The default value is a relative path in the cache folder of the application.|
| network | [Network](#network10) | No| Network used for the task. The default value is **ANY** (Wi-Fi or cellular).|
| metered | boolean | No| Whether the task is allowed on a metered connection. The default value is **false**.<br>- **true**: task allowed on a metered connection.<br>- **false**: task not allowed on a metered connection.|
| roaming | boolean | No| Whether the task is allowed on a roaming network. The default value is **true**.<br>- **true**: task allowed on a roaming network.<br>- **false**: task not allowed on a roaming network.|
| retry | boolean | No| Whether automatic retry is enabled for the task. This parameter is only applicable to background tasks. The default value is **true**.<br>- **true**: automatic retry enabled for the task.<br>- **-false**: automatic retry not enabled for the task.|
| redirect | boolean | No| Whether redirection is allowed. The default value is **true**.<br>- **true**: redirection allowed.<br>- **false**: task not allowed on a metered connection.|
| index | number | No| Path index of the task. It is usually used for resumable downloads. The default value is **0**.|
| begins | number | No| File start point of the task. It is usually used for resumable downloads. The default value is **0**. The value is a closed interval.<br>- If the task is a download, the value is obtained by sending an HTTP range request to read the start position when the server starts to download files.<br>- If the task is an upload, the value is obtained at the beginning of the upload.|
| ends | number | No| File end point of the task. It is usually used for resumable downloads. The default value is **-1**. The value is a closed interval.<br>- If the task is a download, the value is obtained by sending an HTTP range request to read the end position when the server starts to download files.<br>- If the task is an upload, the value is obtained at the end of the upload.|
| gauge | boolean | No| Whether to send progress notifications. This parameter applies only to background tasks. The default value is **false**.<br>- **false**: Progress notifications are not sent. This means that a notification is sent only to indicate the result of the total task.<br>- **true**: Progress notifications are sent to indicate the result of each file.|
| precise | boolean | No| - If this parameter is set to **true**, the task fails when the file size cannot be obtained.<br>- If this parameter is set to **false**, the task continues when the file size is set to **-1**.<br>The default value is **false**.|
| token | string | No| Token of the task. If the task has a token configured, this token is required for query of the task. The value contains 8 to 2048 bytes. This parameter is left empty by default.|
| priority<sup>11+</sup> | number | No| Priority of the task. For tasks in the same mode, a smaller value indicates a higher priority.<br>Default value: **0**|
| extras | object | No| Additional information of the task. This parameter is left empty by default.|

## State<sup>10+</sup>  

Defines the current task status.

**System capability**: SystemCapability.Request.FileTransferAgent

| Name| Value|Description|
| -------- | -------- |-------- |
| INITIALIZED | 0x00 |The task is initialized based on the configuration specified in [Config](#config10).|
| WAITING | 0x10 |The task lacks resources for running or the resources for retries do not match the network status.|
| RUNNING | 0x20 |The task is being executed.|
| RETRYING | 0x21 |The task has failed at least once and is being executed again.|
| PAUSED | 0x30 |The task is suspended and will be resumed later.|
| STOPPED | 0x31 |The task is stopped.|
| COMPLETED | 0x40 |The task is complete.|
| FAILED | 0x41 |The task fails.|
| REMOVED | 0x50 |The task is removed.|


## Progress<sup>10+</sup> 
Describes the data structure of the task progress.

**System capability**: SystemCapability.Request.FileTransferAgent

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| state | [State](#state10) | Yes| Current task status.|
| index | number | Yes| Index of the file that is being processed in the task.|
| processed | number | Yes| Size of processed data in the current file in the task, in bytes.|
| sizes | Array&lt;number&gt; | Yes| Size of files in the task, in bytes.|
| extras | object | No| Extra information of the task, for example, the header and body of the response from the server.|


## Faults<sup>10+</sup>  

Defines the cause of a task failure.

**System capability**: SystemCapability.Request.FileTransferAgent

| Name| Value|Description|
| -------- | -------- |-------- |
| OTHERS | 0xFF |Other fault.|
| DISCONNECTED | 0x00 |Network disconnection.|
| TIMEOUT | 0x10 |Timeout.|
| PROTOCOL | 0x20 |Protocol error, for example, an internal server error (500) or a data range that cannot be processed (416).|
| FSIO | 0x40 |File system I/O error, for example, an error that occurs during the open, search, read, write, or close operation.|


## Filter<sup>10+</sup>
Defines the filter criteria.

**System capability**: SystemCapability.Request.FileTransferAgent

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| before | number | No| Unix timestamp of the end time, in milliseconds. The default value is the invoking time.|
| after | number | No| Unix timestamp of the start time, in milliseconds. The default value is the invoking time minus 24 hours.|
| state | [State](#state10) | No| Task state.|
| action | [Action](#action10) | No| Task action.<br>- **UPLOAD**<br>- **DOWNLOAD**|
| mode | [Mode](#mode10) | No| Task mode.<br>- **FOREGROUND**: foreground task.<br>- **BACKGROUND**: background task.<br>- No value: All tasks are queried.|

## TaskInfo<sup>10+</sup> 
Defines the data structure of the task information for query. The fields available vary depending on the query type.

**System capability**: SystemCapability.Request.FileTransferAgent

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| saveas | string | No| Path for storing downloaded files. The options are as follows:<br>- Relative path in the cache folder of the invoker, for example, **"./xxx/yyy/zzz.html"** and **"xxx/yyy/zzz.html"**.<br>- URI (applicable when the application has the permission to access the URI), for example, **"datashare://bundle/xxx/yyy/zzz.html"**. This function is not supported currently.<br>The default value is a relative path in the cache folder of the application.|
| url | string | No| Task URL.<br>It can be obtained through [request.agent.show<sup>10+</sup>](#requestagentshow10-1) or [request.agent.touch<sup>10+</sup>](#requestagenttouch10-1).|
| data | string \| Array&lt;[FormItem](#formitem10)&gt; | No| Task value.<br>It can be obtained through [request.agent.show<sup>10+</sup>](#requestagentshow10-1) or [request.agent.touch<sup>10+</sup>](#requestagenttouch10-1).|
| tid | string | Yes| Task ID.|
| title | string | Yes| Task title.|
| description | string | Yes| Task description.|
| action | [Action](#action10) | Yes| Task action.<br>- **UPLOAD**<br>- **DOWNLOAD**|
| mode | [Mode](#mode10) | Yes| Task mode.<br>- **FOREGROUND**: foreground task.<br>- **BACKGROUND**: background task.|
| priority<sup>11+</sup> | number | No| Task priority. The priority of a foreground task is higher than that of a background task. For tasks in the same mode, a smaller value indicates a higher priority.|
| mimeType | string | Yes| MIME type in the task configuration.|
| progress | [Progress](#progress10) | Yes| Task progress.|
| gauge | boolean | Yes| Whether to send progress notifications. This parameter applies only to background tasks.|
| ctime | number | Yes| Unix timestamp when the task is created, in milliseconds. The value is generated by the system of the current device.<br>Note: When [request.agent.search<sup>10+</sup>](#requestagentsearch10-1) is used for query, this value must be within the range of [after,before] for the task ID to be obtained. For details about **before** and **after**, see [Filter](#filter10).
| mtime | number | Yes| Unix timestamp when the task state changes, in milliseconds. The value is generated by the system of the current device.|
| retry | boolean | Yes| Whether automatic retry is enabled for the task. This parameter applies only to background tasks.|
| tries | number | Yes| Number of retries of the task.|
| faults | [Faults](#faults10) | Yes| Failure cause of the task.<br>- **OTHERS**: other fault.<br>- **DISCONNECT**: network disconnection.<br>- **TIMEOUT**: timeout.<br>- **PROTOCOL**: protocol error.<br>- **FSIO**: file system I/O error.|
| reason | string | Yes| Reason why the task is waiting, failed, stopped, or paused.|
| extras | string | No| Extra information of the task|


## Task<sup>10+</sup> 
Implements an upload or download task. Before using this API, you must obtain a **Task** object, from a promise through [request.agent.create<sup>10+</sup>](#requestagentcreate10-1) or from a callback through [request.agent.create<sup>10+</sup>](#requestagentcreate10).

### Attributes
Task attributes include the task ID and task configuration.

**System capability**: SystemCapability.Request.FileTransferAgent

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| tid | string | Yes| Task ID, which is unique in the system and is automatically generated by the system.|
| config | [Config](#config10) | Yes| Task configuration.|


### on('progress')<sup>10+</sup>

on(event: 'progress', callback: (progress: Progress) =&gt; void): void

Subscribes to task progress changes. This API uses a callback to return the result asynchronously.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | event | string | Yes| Type of the event to subscribe to.<br>The value is **'progress'**, indicating the task progress.|
  | callback | function | Yes| Callback used to return the data structure of the task progress.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 21900005 | task mode error. |

**Example**

  ```ts
  let attachments: Array<request.agent.FormItem> = [{
    name: "taskOnTest",
    value: {
      filename: "taskOnTest.avi",
      mimeType: "application/octet-stream",
      path: "./taskOnTest.avi",
    }
  }];
  let config: request.agent.Config = {
    action: request.agent.Action.UPLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskOnTest',
    description: 'Sample code for event listening',
    mode: request.agent.Mode.FOREGROUND,
    overwrite: false,
    method: "PUT",
    data: attachments,
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  let createOnCallback = (progress: request.agent.Progress) => {
    console.info('upload task progress.');
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.on('progress', createOnCallback);
    console.info(`Succeeded in creating a upload task. result: ${task.tid}`);
    task.start();
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a upload task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

### on('completed')<sup>10+</sup>

on(event: 'completed', callback: (progress: Progress) =&gt; void): void

Subscribes to task completion events. This API uses a callback to return the result asynchronously.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | event | string | Yes| Type of the event to subscribe to.<br>The value is **'completed'**, indicating task completion.|
  | callback | function | Yes| Callback used to return the data structure of the task progress.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 21900005 | task mode error. |

**Example**

  ```ts
  let attachments: Array<request.agent.FormItem> = [{
    name: "taskOnTest",
    value: {
      filename: "taskOnTest.avi",
      mimeType: "application/octet-stream",
      path: "./taskOnTest.avi",
    }
  }];
  let config: request.agent.Config = {
    action: request.agent.Action.UPLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskOnTest',
    description: 'Sample code for event listening',
    mode: request.agent.Mode.FOREGROUND,
    overwrite: false,
    method: "PUT",
    data: attachments,
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  let createOnCallback = (progress: request.agent.Progress) => {
    console.info('upload task completed.');
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.on('completed', createOnCallback);
    console.info(`Succeeded in creating a upload task. result: ${task.tid}`);
    task.start();
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a upload task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

### on('failed')<sup>10+</sup>

on(event: 'failed', callback: (progress: Progress) =&gt; void): void

Subscribes to task failure events. This API uses a callback to return the result asynchronously.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | event | string | Yes| Type of the event to subscribe to.<br>The value is **'failed'**, indicating task failure.|
  | callback | function | Yes| Callback used to return the data structure of the task progress.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 21900005 | task mode error. |

**Example**

  ```ts
  let attachments: Array<request.agent.FormItem> = [{
    name: "taskOnTest",
    value: {
      filename: "taskOnTest.avi",
      mimeType: "application/octet-stream",
      path: "./taskOnTest.avi",
    }
  }];
  let config: request.agent.Config = {
    action: request.agent.Action.UPLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskOnTest',
    description: 'Sample code for event listening',
    mode: request.agent.Mode.FOREGROUND,
    overwrite: false,
    method: "PUT",
    data: attachments,
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  let createOnCallback = (progress: request.agent.Progress) => {
    console.info('upload task failed.');
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.on('failed', createOnCallback);
    console.info(`Succeeded in creating a upload task. result: ${task.tid}`);
    task.start();
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a upload task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

### on('pause')<sup>11+</sup>

on(event: 'pause', callback: (progress: Progress) =&gt; void): void

Subscribes to task pause events. This API uses a callback to return the result asynchronously.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | event | string | Yes| Type of the event to subscribe to.<br>The value is **'pause'**, indicating task pause.|
  | callback | function | Yes| Callback used to return the data structure of the task progress.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

**Example**

  ```ts
  let attachments: Array<request.agent.FormItem> = [{
    name: "taskOnTest",
    value: {
      filename: "taskOnTest.avi",
      mimeType: "application/octet-stream",
      path: "./taskOnTest.avi",
    }
  }];
  let config: request.agent.Config = {
    action: request.agent.Action.UPLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskOnTest',
    description: 'Sample code for event listening',
    mode: request.agent.Mode.FOREGROUND,
    overwrite: false,
    method: "PUT",
    data: attachments,
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  let createOnCallback = (progress: request.agent.Progress) => {
    console.info('upload task pause.');
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.on('pause', createOnCallback);
    console.info(`Succeeded in creating a upload task. result: ${task.tid}`);
    task.start();
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a upload task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

### on('resume')<sup>11+</sup>

on(event: 'resume', callback: (progress: Progress) =&gt; void): void

Subscribes to task resume events. This API uses a callback to return the result asynchronously.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | event | string | Yes| Type of the event to subscribe to.<br>The value is **'resume'**, indicating task resume.|
  | callback | function | Yes| Callback used to return the data structure of the task progress.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

**Example**

  ```ts
  let attachments: Array<request.agent.FormItem> = [{
    name: "taskOnTest",
    value: {
      filename: "taskOnTest.avi",
      mimeType: "application/octet-stream",
      path: "./taskOnTest.avi",
    }
  }];
  let config: request.agent.Config = {
    action: request.agent.Action.UPLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskOnTest',
    description: 'Sample code for event listening',
    mode: request.agent.Mode.FOREGROUND,
    overwrite: false,
    method: "PUT",
    data: attachments,
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  let createOnCallback = (progress: request.agent.Progress) => {
    console.info('upload task resume.');
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.on('resume', createOnCallback);
    console.info(`Succeeded in creating a upload task. result: ${task.tid}`);
    task.start();
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a upload task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

### on('remove')<sup>11+</sup>

on(event: 'remove', callback: (progress: Progress) =&gt; void): void

Subscribes to task removal events. This API uses a callback to return the result asynchronously.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | event | string | Yes| Type of the event to subscribe to.<br>The value is **'remove'**, indicating task removal.|
  | callback | function | Yes| Callback used to return the data structure of the task progress.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

**Example**

  ```ts
  let attachments: Array<request.agent.FormItem> = [{
    name: "taskOnTest",
    value: {
      filename: "taskOnTest.avi",
      mimeType: "application/octet-stream",
      path: "./taskOnTest.avi",
    }
  }];
  let config: request.agent.Config = {
    action: request.agent.Action.UPLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskOnTest',
    description: 'Sample code for event listening',
    mode: request.agent.Mode.FOREGROUND,
    overwrite: false,
    method: "PUT",
    data: attachments,
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  let createOnCallback = (progress: request.agent.Progress) => {
    console.info('upload task remove.');
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.on('remove', createOnCallback);
    console.info(`Succeeded in creating a upload task. result: ${task.tid}`);
    task.start();
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a upload task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

### off('progress')<sup>10+</sup>

off(event: 'progress', callback?: (progress: Progress) =&gt; void): void

Unsubscribes from task progress events.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | event | string | Yes| Type of the event to subscribe to.<br>The value is **'progress'**, indicating the task progress.|
  | callback | function | No| Callback to unregister. If this parameter is not specified, all callbacks of the current type will be unregistered.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 21900005 | task mode error. |

**Example**

  ```ts
  let attachments: Array<request.agent.FormItem> = [{
    name: "taskOffTest",
    value: {
      filename: "taskOffTest.avi",
      mimeType: "application/octet-stream",
      path: "./taskOffTest.avi",
    }
  }];
  let config: request.agent.Config = {
    action: request.agent.Action.UPLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskOffTest',
    description: 'Sample code for event listening',
    mode: request.agent.Mode.FOREGROUND,
    overwrite: false,
    method: "PUT",
    data: attachments,
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  let createOffCallback1 = (progress: request.agent.Progress) => {
    console.info('upload task progress.');
  };
  let createOffCallback2 = (progress: request.agent.Progress) => {
    console.info('upload task progress.');
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.on('progress', createOffCallback1);
    task.on('progress', createOffCallback2);
    // Unsubscribe from createOffCallback1.
    task.off('progress', createOffCallback1);
    // Unsubscribe from all callbacks of task progress changes.
    task.off('progress');
    console.info(`Succeeded in creating a upload task. result: ${task.tid}`);
    task.start();
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a upload task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

### off('completed')<sup>10+</sup>

off(event: 'completed', callback?: (progress: Progress) =&gt; void): void

Unsubscribes from task completion events.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | event | string | Yes| Type of the event to subscribe to.<br>The value is **'completed'**, indicating task completion.|
  | callback | function | No| Callback to unregister. If this parameter is not specified, all callbacks of the current type will be unregistered.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 21900005 | task mode error. |

**Example**

  ```ts
  let attachments: Array<request.agent.FormItem> = [{
    name: "taskOffTest",
    value: {
      filename: "taskOffTest.avi",
      mimeType: "application/octet-stream",
      path: "./taskOffTest.avi",
    }
  }];
  let config: request.agent.Config = {
    action: request.agent.Action.UPLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskOffTest',
    description: 'Sample code for event listening',
    mode: request.agent.Mode.FOREGROUND,
    overwrite: false,
    method: "PUT",
    data: attachments,
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  let createOffCallback1 = (progress: request.agent.Progress) => {
    console.info('upload task completed.');
  };
  let createOffCallback2 = (progress: request.agent.Progress) => {
    console.info('upload task completed.');
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.on('completed', createOffCallback1);
    task.on('completed', createOffCallback2);
    // Unsubscribe from createOffCallback1.
    task.off('completed', createOffCallback1);
    // Unsubscribe from all callbacks of the task completion events.
    task.off('completed');
    console.info(`Succeeded in creating a upload task. result: ${task.tid}`);
    task.start();
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a upload task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

### off('failed')<sup>10+</sup>

off(event: 'failed', callback?: (progress: Progress) =&gt; void): void

Unsubscribes from task failure events.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | event | string | Yes| Type of the event to subscribe to.<br>The value is **'failed'**, indicating task failure.|
  | callback | function | No| Callback to unregister. If this parameter is not specified, all callbacks of the current type will be unregistered.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 21900005 | task mode error. |

**Example**

  ```ts
  let attachments: Array<request.agent.FormItem> = [{
    name: "taskOffTest",
    value: {
      filename: "taskOffTest.avi",
      mimeType: "application/octet-stream",
      path: "./taskOffTest.avi",
    }
  }];
  let config: request.agent.Config = {
    action: request.agent.Action.UPLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskOffTest',
    description: 'Sample code for event listening',
    mode: request.agent.Mode.FOREGROUND,
    overwrite: false,
    method: "PUT",
    data: attachments,
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  let createOffCallback1 = (progress: request.agent.Progress) => {
    console.info('upload task failed.');
  };
  let createOffCallback2 = (progress: request.agent.Progress) => {
    console.info('upload task failed.');
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.on('failed', createOffCallback1);
    task.on('failed', createOffCallback2);
    // Unsubscribe from createOffCallback1.
    task.off('failed', createOffCallback1);
    // Unsubscribe from all callbacks of the task failure events.
    task.off('failed');
    console.info(`Succeeded in creating a upload task. result: ${task.tid}`);
    task.start();
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a upload task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

### off('pause')<sup>11+</sup>

off(event: 'pause', callback?: (progress: Progress) =&gt; void): void

Unsubscribes from the foreground task pause event.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | event | string | Yes| Type of the event to subscribe to.<br>The value is **'pause'**, indicating task pause.|
  | callback | function | No| Callback to unregister. If this parameter is not specified, all callbacks of the current type will be unregistered.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

**Example**

  ```ts
  let attachments: Array<request.agent.FormItem> = [{
    name: "taskOffTest",
    value: {
      filename: "taskOffTest.avi",
      mimeType: "application/octet-stream",
      path: "./taskOffTest.avi",
    }
  }];
  let config: request.agent.Config = {
    action: request.agent.Action.UPLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskOffTest',
    description: 'Sample code for event listening',
    mode: request.agent.Mode.FOREGROUND,
    overwrite: false,
    method: "PUT",
    data: attachments,
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  let createOffCallback1 = (progress: request.agent.Progress) => {
    console.info('upload task pause.');
  };
  let createOffCallback2 = (progress: request.agent.Progress) => {
    console.info('upload task pause.');
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.on('pause', createOffCallback1);
    task.on('pause', createOffCallback2);
    // Unsubscribe from createOffCallback1.
    task.off('pause', createOffCallback1);
    // Unsubscribe from all callbacks of the foreground task pause event.
    task.off('pause');
    console.info(`Succeeded in creating a upload task. result: ${task.tid}`);
    task.start();
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a upload task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

### off('resume')<sup>11+</sup>

off(event: 'resume', callback?: (progress: Progress) =&gt; void): void

Unsubscribes from the foreground task resume event.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | event | string | Yes| Type of the event to subscribe to.<br>The value is **'resume'**, indicating task resume.|
  | callback | function | No| Callback to unregister. If this parameter is not specified, all callbacks of the current type will be unregistered.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

**Example**

  ```ts
  let attachments: Array<request.agent.FormItem> = [{
    name: "taskOffTest",
    value: {
      filename: "taskOffTest.avi",
      mimeType: "application/octet-stream",
      path: "./taskOffTest.avi",
    }
  }];
  let config: request.agent.Config = {
    action: request.agent.Action.UPLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskOffTest',
    description: 'Sample code for event listening',
    mode: request.agent.Mode.FOREGROUND,
    overwrite: false,
    method: "PUT",
    data: attachments,
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  let createOffCallback1 = (progress: request.agent.Progress) => {
    console.info('upload task resume.');
  };
  let createOffCallback2 = (progress: request.agent.Progress) => {
    console.info('upload task resume.');
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.on('resume', createOffCallback1);
    task.on('resume', createOffCallback2);
    // Unsubscribe from createOffCallback1.
    task.off('resume', createOffCallback1);
    // Unsubscribe from all callbacks of the foreground task resume event.
    task.off('resume');
    console.info(`Succeeded in creating a upload task. result: ${task.tid}`);
    task.start();
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a upload task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

### off('remove')<sup>11+</sup>

off(event: 'remove', callback?: (progress: Progress) =&gt; void): void

Unsubscribes from the task removal event.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | event | string | Yes| Type of the event to subscribe to.<br>The value is **'remove'**, indicating task removal.|
  | callback | function | No| Callback to unregister. If this parameter is not specified, all callbacks of the current type will be unregistered.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

**Example**

  ```ts
  let attachments: Array<request.agent.FormItem> = [{
    name: "taskOffTest",
    value: {
      filename: "taskOffTest.avi",
      mimeType: "application/octet-stream",
      path: "./taskOffTest.avi",
    }
  }];
  let config: request.agent.Config = {
    action: request.agent.Action.UPLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskOffTest',
    description: 'Sample code for event listening',
    mode: request.agent.Mode.FOREGROUND,
    overwrite: false,
    method: "PUT",
    data: attachments,
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  let createOffCallback1 = (progress: request.agent.Progress) => {
    console.info('upload task remove.');
  };
  let createOffCallback2 = (progress: request.agent.Progress) => {
    console.info('upload task remove.');
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.on('remove', createOffCallback1);
    task.on('remove', createOffCallback2);
    // Unsubscribe from createOffCallback1.
    task.off('remove', createOffCallback1);
    // Unsubscribe from all callbacks of the task removal event.
    task.off('remove');
    console.info(`Succeeded in creating a upload task. result: ${task.tid}`);
    task.start();
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a upload task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

### start<sup>10+</sup>

start(callback: AsyncCallback&lt;void&gt;): void

Starts this task. This API cannot be used to start an initialized task. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | function | Yes| Callback used to return the result. If the operation is successful, **err** is **undefined**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400003 | task service ability error. |
  | 21900007 | task state error. |

**Example**

  ```ts
  let config: request.agent.Config = {
    action: request.agent.Action.DOWNLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskStartTest',
    description: 'Sample code for start the download task',
    mode: request.agent.Mode.BACKGROUND,
    overwrite: false,
    method: "GET",
    data: "",
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.start((err: BusinessError) => {
      if (err) {
        console.error(`Failed to start the download task, Code: ${err.code}, message: ${err.message}`);
        return;
      }
      console.info(`Succeeded in starting a download task.`);
    });
    console.info(`Succeeded in creating a download task. result: ${task.tid}`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a download task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

### start<sup>10+</sup>

start(): Promise&lt;void&gt;

Starts this task. This API cannot be used to start an initialized task. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Request.FileTransferAgent

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400003 | task service ability error. |
  | 21900007 | task state error. |

**Example**

  ```ts
  let config: request.agent.Config = {
    action: request.agent.Action.DOWNLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskStartTest',
    description: 'Sample code for start the download task',
    mode: request.agent.Mode.BACKGROUND,
    overwrite: false,
    method: "GET",
    data: "",
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.start().then(() => {
      console.info(`Succeeded in starting a download task.`);
    }).catch((err: BusinessError) => {
      console.error(`Failed to start the download task, Code: ${err.code}, message: ${err.message}`);
    });
    console.info(`Succeeded in creating a download task. result: ${task.tid}`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a download task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

### pause<sup>10+</sup>

pause(callback: AsyncCallback&lt;void&gt;): void

Pauses this task. This API can be used to pause a background task that is waiting, running, or retrying. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | function | Yes| Callback used to return the result. If the operation is successful, **err** is **undefined**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400003 | task service ability error. |
  | 21900005 | task mode error. |
  | 21900007 | task state error. |

**Example**

  ```ts
  let config: request.agent.Config = {
    action: request.agent.Action.DOWNLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskPauseTest',
    description: 'Sample code for pause the download task',
    mode: request.agent.Mode.BACKGROUND,
    overwrite: false,
    method: "GET",
    data: "",
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.start();
    for(var t = Date.now(); Date.now() - t <= 1000;); // To prevent asynchronous out-of-order, wait for 1 second before performing the next operation.
    task.pause((err: BusinessError) => {
      if (err) {
        console.error(`Failed to pause the download task, Code: ${err.code}, message: ${err.message}`);
        return;
      }
      console.info(`Succeeded in pausing a download task. `);
    });
    console.info(`Succeeded in creating a download task. result: ${task.tid}`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a download task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

> **NOTE**
>
> The error code **21900005 task mode error** is removed from API version 11.

### pause<sup>10+</sup>

pause(): Promise&lt;void&gt;

Pauses this task. This API can be used to pause a background task that is waiting, running, or retrying. This API uses a promise to return the result.

**System capability**: SystemCapability.Request.FileTransferAgent

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400003 | task service ability error. |
  | 21900005 | task mode error. |
  | 21900007 | task state error. |

**Example**

  ```ts
  let config: request.agent.Config = {
    action: request.agent.Action.DOWNLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskPauseTest',
    description: 'Sample code for pause the download task',
    mode: request.agent.Mode.BACKGROUND,
    overwrite: false,
    method: "GET",
    data: "",
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.start();
    for(var t = Date.now(); Date.now() - t <= 1000;); // To prevent asynchronous out-of-order, wait for 1 second before performing the next operation.
    task.pause().then(() => {
      console.info(`Succeeded in pausing a download task. `);
    }).catch((err: BusinessError) => {
      console.error(`Failed to pause the upload task, Code: ${err.code}, message: ${err.message}`);
    });
    console.info(`Succeeded in creating a download task. result: ${task.tid}`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a upload task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

> **NOTE**
>
> The error code **21900005 task mode error** is removed from API version 11.

### resume<sup>10+</sup>

resume(callback: AsyncCallback&lt;void&gt;): void

Resumes this task. This API can be used to resume a paused background task. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | function | Yes| Callback used to return the result. If the operation is successful, **err** is **undefined**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400003 | task service ability error. |
  | 21900005 | task mode error. |
  | 21900007 | task state error. |

**Example**

  ```ts
  let config: request.agent.Config = {
    action: request.agent.Action.DOWNLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskResumeTest',
    description: 'Sample code for resume the download task',
    mode: request.agent.Mode.BACKGROUND,
    overwrite: false,
    method: "GET",
    data: "",
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.start();
    for(var t = Date.now(); Date.now() - t <= 1000;); // To prevent asynchronous out-of-order, wait for 1 second before performing the next operation.
    task.pause();
    for(var t = Date.now(); Date.now() - t <= 1000;); // To prevent asynchronous out-of-order, wait for 1 second before performing the next operation.
    task.resume((err: BusinessError) => {
      if (err) {
        console.error(`Failed to resume the download task, Code: ${err.code}, message: ${err.message}`);
        return;
      }
      console.info(`Succeeded in resuming a download task. `);
    });
    console.info(`Succeeded in creating a download task. result: ${task.tid}`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a download task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

> **NOTE**
>
> The error code **21900005 task mode error** is removed from API version 11.


### resume<sup>10+</sup>

resume(): Promise&lt;void&gt;

Resumes this task. This API can be used to resume a paused background task. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Request.FileTransferAgent

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400003 | task service ability error. |
  | 21900005 | task mode error. |
  | 21900007 | task state error. |

**Example**

  ```ts
  let config: request.agent.Config = {
    action: request.agent.Action.DOWNLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskResumeTest',
    description: 'Sample code for resume the download task',
    mode: request.agent.Mode.BACKGROUND,
    overwrite: false,
    method: "GET",
    data: "",
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.start();
    for(var t = Date.now(); Date.now() - t <= 1000;); // To prevent asynchronous out-of-order, wait for 1 second before performing the next operation.
    task.pause();
    for(var t = Date.now(); Date.now() - t <= 1000;); // To prevent asynchronous out-of-order, wait for 1 second before performing the next operation.
    task.resume().then(() => {
      console.info(`Succeeded in resuming a download task. `);
    }).catch((err: BusinessError) => {
      console.error(`Failed to resume the download task, Code: ${err.code}, message: ${err.message}`);
    });
    console.info(`Succeeded in creating a download task. result: ${task.tid}`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a download task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

> **NOTE**
>
> The error code **21900005 task mode error** is removed from API version 11.


### stop<sup>10+</sup>

stop(callback: AsyncCallback&lt;void&gt;): void

Stops this task. This API can be used to stop a running, waiting, or retrying task. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | function | Yes| Callback used to return the result. If the operation is successful, **err** is **undefined**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400003 | task service ability error. |
  | 21900007 | task state error. |

**Example**

  ```ts
  let config: request.agent.Config = {
    action: request.agent.Action.DOWNLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskStopTest',
    description: 'Sample code for stop the download task',
    mode: request.agent.Mode.BACKGROUND,
    overwrite: false,
    method: "GET",
    data: "",
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.start();
    for(var t = Date.now(); Date.now() - t <= 1000;); // To prevent asynchronous out-of-order, wait for 1 second before performing the next operation.
    task.stop((err: BusinessError) => {
      if (err) {
        console.error(`Failed to stop the download task, Code: ${err.code}, message: ${err.message}`);
        return;
      }
      console.info(`Succeeded in stopping a download task. `);
    });
    console.info(`Succeeded in creating a download task. result: ${task.tid}`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a download task, Code: ${err.code}, message: ${err.message}`);
  });
  ```


### stop<sup>10+</sup>

stop(): Promise&lt;void&gt;

Stops this task. This API can be used to stop a running, waiting, or retrying task. This API uses a promise to return the result.

**System capability**: SystemCapability.Request.FileTransferAgent

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400003 | task service ability error. |
  | 21900007 | task state error. |

**Example**

  ```ts
  let config: request.agent.Config = {
    action: request.agent.Action.DOWNLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'taskStopTest',
    description: 'Sample code for stop the download task',
    mode: request.agent.Mode.BACKGROUND,
    overwrite: false,
    method: "GET",
    data: "",
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    task.start();
    for(var t = Date.now(); Date.now() - t <= 1000;); // To prevent asynchronous out-of-order, wait for 1 second before performing the next operation.
    task.stop().then(() => {
      console.info(`Succeeded in stopping a download task. `);
    }).catch((err: BusinessError) => {
      console.error(`Failed to stop the download task, Code: ${err.code}, message: ${err.message}`);
    });
    console.info(`Succeeded in creating a download task. result: ${task.tid}`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to create a download task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

## request.agent.create<sup>10+</sup>

create(context: BaseContext, config: Config, callback: AsyncCallback&lt;Task&gt;): void

Creates an upload or download task and adds it to the queue. An application can create a maximum of 10 unfinished tasks. This API uses an asynchronous callback to return the result.


**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | config | [Config](#config10) | Yes| Task configuration.|
  | context | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md) | Yes| Application-based context.|
  | callback | AsyncCallback&lt;[Task](#task10)&gt; | Yes| Callback used to return the configuration about the created task.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400001 | file operation error. |
  | 13400003 | task service ability error. |
  | 21900004 | application task queue full error. |
  | 21900005 | task mode error. |

**Example**

  ```ts
  let attachments: Array<request.agent.FormItem> = [{
    name: "createTest",
    value: {
      filename: "createTest.avi",
      mimeType: "application/octet-stream",
      path: "./createTest.avi",
    }
  }];
  let config: request.agent.Config = {
    action: request.agent.Action.UPLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'createTest',
    description: 'Sample code for create task',
    mode: request.agent.Mode.BACKGROUND,
    overwrite: false,
    method: "PUT",
    data: attachments,
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  request.agent.create(getContext(), config, (err: BusinessError, task: request.agent.Task) => {
    if (err) {
      console.error(`Failed to create a download task, Code: ${err.code}, message: ${err.message}`);
      return;
    }
    console.info(`Succeeded in creating a download task. result: ${task.config}`);
    task.start();
  });
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

## request.agent.create<sup>10+</sup>

create(context: BaseContext, config: Config): Promise&lt;Task&gt;

Creates an upload or download task and adds it to the queue. An application can create a maximum of 10 unfinished tasks. This API uses a promise to return the result.


**Required permissions**: ohos.permission.INTERNET

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | context | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md) | Yes| Application-based context.|
  | config | [Config](#config10) | Yes| Task configuration.|

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;[Task](#task10)&gt; | Promise used to return the configuration about the created task.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400001 | file operation error. |
  | 13400003 | task service ability error. |
  | 21900004 | application task queue full error. |
  | 21900005 | task mode error. |

**Example**

  ```ts
  let attachments: Array<request.agent.FormItem> = [{
    name: "createTest",
    value: {
      filename: "createTest.avi",
      mimeType: "application/octet-stream",
      path: "./createTest.avi",
    }
  }];
  let config: request.agent.Config = {
    action: request.agent.Action.UPLOAD,
    url: 'http://127.0.0.1', // Replace the URL with the HTTP address of the real server.
    title: 'createTest',
    description: 'Sample code for create task',
    mode: request.agent.Mode.BACKGROUND,
    overwrite: false,
    method: "PUT",
    data: attachments,
    saveas: "./",
    network: request.agent.Network.CELLULAR,
    metered: false,
    roaming: true,
    retry: true,
    redirect: true,
    index: 0,
    begins: 0,
    ends: -1,
    gauge: false,
    precise: false,
    token: "it is a secret"
  };
  request.agent.create(getContext(), config).then((task: request.agent.Task) => {
    console.info(`Succeeded in creating a download task. result: ${task.config}`);
    task.start();
  }).catch((err) => {
    console.error(`Failed to create a download task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

> **NOTE**
>
> For details about how to obtain the context in the example, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

## request.agent.getTask<sup>11+</sup>

getTask(context: BaseContext, id: string, token?: string): Promise&lt;Task&gt;

Obtains task information based on the task ID. This API uses a promise to return the result.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | context | [BaseContext](../apis-ability-kit/js-apis-inner-application-baseContext.md) | Yes| Application-based context.|
  | id | string | Yes| Task ID.|
  | token | string | No| Token for task query.|

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;[Task](#task10)&gt; | Promise used to return the configuration about the created task.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400003 | task service ability error. |
  | 21900006 | task not found error. |

**Example**

  ```ts
  request.agent.getTask(context, "123456").then((task: request.agent.Task) => {
    console.info(`Succeeded in querying a upload task. result: ${task.uid}`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to query a upload task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

## request.agent.remove<sup>10+</sup>

remove(id: string, callback: AsyncCallback&lt;void&gt;): void

Removes a specified task of the invoker. If the task is being executed, the task is forced to stop. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | id | string | Yes| Task ID.|
  | callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result. If the operation is successful, **err** is **undefined**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400003 | task service ability error. |
  | 21900006 | task not found error. |

**Example**

  ```ts
  request.agent.remove("123456", (err: BusinessError) => {
    if (err) {
      console.error(`Failed to removing a download task, Code: ${err.code}, message: ${err.message}`);
      return;
    }
    console.info(`Succeeded in creating a download task.`);
  });
  ```


## request.agent.remove<sup>10+</sup>

remove(id: string): Promise&lt;void&gt;

Removes a specified task of the invoker. If the task is being executed, the task is forced to stop. This API uses a promise to return the result.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | id | string | Yes| Task ID.|

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400003 | task service ability error. |
  | 21900006 | task not found error. |

**Example**

  ```ts
  request.agent.remove("123456").then(() => {
    console.info(`Succeeded in removing a download task. `);
  }).catch((err: BusinessError) => {
    console.error(`Failed to remove a download task, Code: ${err.code}, message: ${err.message}`);
  });
  ```


## request.agent.show<sup>10+</sup>

show(id: string, callback: AsyncCallback&lt;TaskInfo&gt;): void

Queries a task details based on the task ID. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | id | string | Yes| Task ID.|
  | callback | AsyncCallback&lt;[TaskInfo](#taskinfo10)&gt; | Yes| Callback used to return task details.|

**Error codes**
For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400003 | task service ability error. |
  | 21900006 | task not found error. |

**Example**

  ```ts
  request.agent.show("123456", (err: BusinessError, taskInfo: request.agent.TaskInfo) => {
    if (err) {
      console.error(`Failed to show a upload task, Code: ${err.code}, message: ${err.message}`);
      return;
    }
    console.info(`Succeeded in showing a upload task.`);
  });
  ```


## request.agent.show<sup>10+</sup>

show(id: string): Promise&lt;TaskInfo&gt;

Queries a task details based on the task ID. This API uses a promise to return the result.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | id | string | Yes| Task ID.|

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;[TaskInfo](#taskinfo10)&gt; | Promise Promise used to return task details.|

**Error codes**
For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400003 | task service ability error. |
  | 21900006 | task not found error. |

**Example**

  ```ts
  request.agent.show("123456").then((taskInfo: request.agent.TaskInfo) => {
    console.info(`Succeeded in showing a upload task.`);
  }).catch((err: BusinessError) => {
    console.error(`Failed to show a upload task, Code: ${err.code}, message: ${err.message}`);
  });
  ```


## request.agent.touch<sup>10+</sup>

touch(id: string, token: string, callback: AsyncCallback&lt;TaskInfo&gt;): void

Queries the task details based on the task ID and token. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | id | string | Yes| Task ID.|
  | token | string | Yes| Token for task query.|
  | callback | AsyncCallback&lt;[TaskInfo](#taskinfo10)&gt; | Yes| Callback used to return task details.|

**Error codes**
For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400003 | task service ability error. |
  | 21900006 | task not found error. |

**Example**

  ```ts
  request.agent.touch("123456", "token", (err: BusinessError, taskInfo: request.agent.TaskInfo) => {
    if (err) {
      console.error(`Failed to touch a upload task, Code: ${err.code}, message: ${err.message}`);
      return;
    }
    console.info(`Succeeded in touching a upload task.`);
  });
  ```


## request.agent.touch<sup>10+</sup>

touch(id: string, token: string): Promise&lt;TaskInfo&gt;

Queries the task details based on the task ID and token. This API uses a promise to return the result.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | id | string | Yes| Task ID.|
  | token | string | Yes| Token for task query.|

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;[TaskInfo](#taskinfo10)&gt; | Promise Promise used to return task details.|

**Error codes**
For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400003 | task service ability error. |
  | 21900006 | task not found error. |

**Example**

  ```ts
  request.agent.touch("123456", "token").then((taskInfo: request.agent.TaskInfo) => {
    console.info(`Succeeded in touching a upload task. `);
  }).catch((err: BusinessError) => {
    console.error(`Failed to touch a upload task, Code: ${err.code}, message: ${err.message}`);
  });
  ```

## request.agent.search<sup>10+</sup>

search(callback: AsyncCallback&lt;Array&lt;string&gt;&gt;): void

Searches for task IDs based on [Filter](#filter10). This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;Array&lt;string&gt;&gt; | Yes| Callback used to return task ID matches.|

**Error codes**
For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400003 | task service ability error. |

**Example**

  ```ts
  request.agent.search((err: BusinessError, data: Array<string>) => {
    if (err) {
      console.error(`Upload task search failed. Code: ${err.code}, message: ${err.message}`);
      return;
    }
    console.info(`Upload task search succeeded. `);
  });
  ```

## request.agent.search<sup>10+</sup>

search(filter: Filter, callback: AsyncCallback&lt;Array&lt;string&gt;&gt;): void

Searches for task IDs based on [Filter](#filter10). This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | filter | [Filter](#filter10) | Yes| Filter criteria.|
  | callback | AsyncCallback&lt;Array&lt;string&gt;&gt; | Yes| Callback used to return task ID matches.|

**Error codes**
For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400003 | task service ability error. |

**Example**

  ```ts
  let filter: request.agent.Filter = {
    bundle: "com.example.myapplication",
    action: request.agent.Action.UPLOAD,
    mode: request.agent.Mode.BACKGROUND
  }
  request.agent.search(filter, (err: BusinessError, data: Array<string>) => {
    if (err) {
      console.error(`Upload task search failed. Code: ${err.code}, message: ${err.message}`);
      return;
    }
    console.info(`Upload task search succeeded. `);
  });
  ```


## request.agent.search<sup>10+</sup>

search(filter?: Filter): Promise&lt;Array&lt;string&gt;&gt;

Searches for task IDs based on [Filter](#filter10). This API uses a promise to return the result.

**System capability**: SystemCapability.Request.FileTransferAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | filter | [Filter](#filter10) | No| Filter criteria.|

**Return value**

| Type               | Description                     |
| ------------------- | ------------------------- |
| Promise&lt;Array&lt;string&gt;&gt; | Promise Promise used to return task ID matches.|

**Error codes**
For details about the error codes, see [Upload and Download Error Codes](errorcode-request.md).

  | ID| Error Message|
  | -------- | -------- |
  | 13400003 | task service ability error. |

**Example**

  ```ts
  let filter: request.agent.Filter = {
    bundle: "com.example.myapplication",
    action: request.agent.Action.UPLOAD,
    mode: request.agent.Mode.BACKGROUND
  }
  request.agent.search(filter).then((data: Array<string>) => {
    console.info(`Upload task search succeeded. `);
  }).catch((err: BusinessError) => {
    console.error(`Upload task search failed. Code: ${err.code}, message: ${err.message}`);
  });
  ```
