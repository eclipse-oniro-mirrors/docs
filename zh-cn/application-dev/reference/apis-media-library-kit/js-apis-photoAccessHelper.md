# @ohos.file.photoAccessHelper (相册管理模块)

该模块提供相册管理模块能力，包括创建相册以及访问、修改相册中的媒体数据信息等。

> **说明：**
>
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import photoAccessHelper from '@ohos.file.photoAccessHelper';
```

## photoAccessHelper.getPhotoAccessHelper

getPhotoAccessHelper(context: Context): PhotoAccessHelper

获取相册管理模块的实例，用于访问和修改相册中的媒体文件。

**模型约束**： 此接口仅可在Stage模型下使用。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型    | 必填 | 说明                       |
| ------- | ------- | ---- | -------------------------- |
| context | [Context](../apis-ability-kit/js-apis-inner-application-context.md) | 是   | 传入Ability实例的Context。 |

**返回值：**

| 类型                            | 说明    |
| ----------------------------- | :---- |
| [PhotoAccessHelper](#photoaccesshelper) | 相册管理模块的实例。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |

**示例：**

```ts
//此处获取的phAccessHelper实例为全局对象，后续使用到phAccessHelper的地方默认为使用此处获取的对象，如未添加此段代码报phAccessHelper未定义的错误请自行添加
let context = getContext(this);
let phAccessHelper = photoAccessHelper.getPhotoAccessHelper(context);
```

## PhotoAccessHelper

### getAssets

getAssets(options: FetchOptions, callback: AsyncCallback&lt;FetchResult&lt;PhotoAsset&gt;&gt;): void

获取图片和视频资源，使用callback方式返回结果。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| options  | [FetchOptions](#fetchoptions)        | 是   | 图片和视频检索选项。              |
| callback |  AsyncCallback&lt;[FetchResult](#fetchresult)&lt;[PhotoAsset](#photoasset)&gt;&gt; | 是   | callback返回图片和视频检索结果集。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if type options is not FetchOptions.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getAssets');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };

  phAccessHelper.getAssets(fetchOptions, async (err, fetchResult) => {
    if (fetchResult !== undefined) {
      console.info('fetchResult success');
      let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
      if (photoAsset !== undefined) {
        console.info('photoAsset.displayName : ' + photoAsset.displayName);
      }
    } else {
      console.error(`fetchResult fail with error: ${err.code}, ${err.message}`);
    }
  });
}
```

### getAssets

getAssets(options: FetchOptions): Promise&lt;FetchResult&lt;PhotoAsset&gt;&gt;

获取图片和视频资源，使用Promise方式返回结果。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**参数：**

| 参数名  | 类型                | 必填 | 说明             |
| ------- | ------------------- | ---- | ---------------- |
| options | [FetchOptions](#fetchoptions)   | 是   | 图片和视频检索选项。     |

**返回值：**

| 类型                        | 说明           |
| --------------------------- | -------------- |
| Promise&lt;[FetchResult](#fetchresult)&lt;[PhotoAsset](#photoasset)&gt;&gt; | Promise对象，返回图片和视频数据结果集。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if type options is not FetchOptions.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getAssets');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    if (fetchResult !== undefined) {
      console.info('fetchResult success');
      let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
      if (photoAsset !== undefined) {
        console.info('photoAsset.displayName :' + photoAsset.displayName);
      }
    }
  } catch (err) {
    console.error(`getAssets failed, error: ${err.code}, ${err.message}`);
  }
}
```

### createAsset

createAsset(photoType: PhotoType, extension: string, options: CreateOptions, callback: AsyncCallback&lt;string&gt;): void

指定待创建的文件类型、后缀和创建选项，创建图片或视频资源，使用callback方式返回结果。

此接口在未申请相册管理模块权限'ohos.permission.WRITE_IMAGEVIDEO'时，可以使用安全控件创建媒体资源，详情请参考[开发指南](../../media/medialibrary/photoAccessHelper-resource-guidelines.md#使用安全控件创建媒体资源)。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| photoType  | [PhotoType](#phototype)        | 是   | 创建的文件类型，IMAGE或者VIDEO类型。              |
| extension  | string        | 是   | 文件名后缀参数，例如：'jpg'。              |
| options  | [CreateOptions](#createoptions)        | 是   | 创建选项，例如{title: 'testPhoto'}。              |
| callback |  AsyncCallback&lt;string&gt; | 是   | callback返回创建的图片和视频的uri。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if type createOption is wrong.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('createAssetDemo');
  let photoType: photoAccessHelper.PhotoType = photoAccessHelper.PhotoType.IMAGE;
  let extension:string = 'jpg';
  let options: photoAccessHelper.CreateOptions = {
    title: 'testPhoto'
  }
  phAccessHelper.createAsset(photoType, extension, options, (err, uri) => {
    if (uri !== undefined) {
      console.info('createAsset uri' + uri);
      console.info('createAsset successfully');
    } else {
      console.error(`createAsset failed, error: ${err.code}, ${err.message}`);
    }
  });
}
```

### createAsset

createAsset(photoType: PhotoType, extension: string, callback: AsyncCallback&lt;string&gt;): void

指定待创建的文件类型和后缀，创建图片或视频资源，使用callback方式返回结果。

此接口在未申请相册管理模块权限'ohos.permission.WRITE_IMAGEVIDEO'时，可以使用安全控件创建媒体资源，详情请参考[开发指南](../../media/medialibrary/photoAccessHelper-resource-guidelines.md#使用安全控件创建媒体资源)。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| photoType  | [PhotoType](#phototype)        | 是   | 创建的文件类型，IMAGE或者VIDEO类型。              |
| extension  | string        | 是   | 文件名后缀参数，例如：'jpg'。              |
| callback |  AsyncCallback&lt;string&gt; | 是   | callback返回创建的图片和视频的uri。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if type createOption is wrong.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('createAssetDemo');
  let photoType: photoAccessHelper.PhotoType = photoAccessHelper.PhotoType.IMAGE;
  let extension: string = 'jpg';
  phAccessHelper.createAsset(photoType, extension, (err, uri) => {
    if (uri !== undefined) {
      console.info('createAsset uri' + uri);
      console.info('createAsset successfully');
    } else {
      console.error(`createAsset failed, error: ${err.code}, ${err.message}`);
    }
  });
}
```

### createAsset

createAsset(photoType: PhotoType, extension: string, options?: CreateOptions): Promise&lt;string&gt;

指定待创建的文件类型、后缀和创建选项，创建图片或视频资源，使用Promise方式返回结果。

此接口在未申请相册管理模块权限'ohos.permission.WRITE_IMAGEVIDEO'时，可以使用安全控件创建媒体资源，详情请参考[开发指南](../../media/medialibrary/photoAccessHelper-resource-guidelines.md#使用安全控件创建媒体资源)。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| photoType  | [PhotoType](#phototype)        | 是   | 创建的文件类型，IMAGE或者VIDEO类型。              |
| extension  | string        | 是   | 文件名后缀参数，例如：'jpg'。              |
| options  | [CreateOptions](#createoptions)        | 否   | 创建选项，例如{title: 'testPhoto'}。              |

**返回值：**

| 类型                        | 说明           |
| --------------------------- | -------------- |
| Promise&lt;string&gt; | Promise对象，返回创建的图片和视频的uri。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if type createOption is wrong.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('createAssetDemo');
  try {
    let photoType: photoAccessHelper.PhotoType = photoAccessHelper.PhotoType.IMAGE;
    let extension: string = 'jpg';
    let options: photoAccessHelper.CreateOptions = {
      title: 'testPhoto'
    }
    let uri: string = await phAccessHelper.createAsset(photoType, extension, options);
    console.info('createAsset uri' + uri);
    console.info('createAsset successfully');
  } catch (err) {
    console.error(`createAsset failed, error: ${err.code}, ${err.message}`);
  }
}
```

### getAlbums

getAlbums(type: AlbumType, subtype: AlbumSubtype, options: FetchOptions, callback: AsyncCallback&lt;FetchResult&lt;Album&gt;&gt;): void

根据检索选项和相册类型获取相册，使用callback方式返回结果。

获取相册前需先保证相册存在。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| type  | [AlbumType](#albumtype)         | 是   | 相册类型。              |
| subtype  | [AlbumSubtype](#albumsubtype)         | 是   | 相册子类型。              |
| options  | [FetchOptions](#fetchoptions)         | 是   |  检索选项。              |
| callback |  AsyncCallback&lt;[FetchResult](#fetchresult)&lt;[Album](#album)&gt;&gt; | 是   | callback返回获取相册的结果集。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if type options is not FetchOption.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  // 示例代码中为获取相册名为newAlbumName的相册。
  console.info('getAlbumsDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  predicates.equalTo('album_name', 'newAlbumName');
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, fetchOptions, async (err, fetchResult) => {
    if (err) {
      console.error(`getAlbumsCallback failed with err: ${err.code}, ${err.message}`);
      return;
    }
    if (fetchResult === undefined) {
      console.error('getAlbumsCallback fetchResult is undefined');
      return;
    }
    let album = await fetchResult.getFirstObject();
    console.info('getAlbumsCallback successfully, albumName: ' + album.albumName);
    fetchResult.close();
  });
}
```

### getAlbums

getAlbums(type: AlbumType, subtype: AlbumSubtype, callback: AsyncCallback&lt;FetchResult&lt;Album&gt;&gt;): void

根据相册类型获取相册，使用callback方式返回结果。

获取相册前需先保证相册存在。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| type  | [AlbumType](#albumtype)         | 是   | 相册类型。              |
| subtype  | [AlbumSubtype](#albumsubtype)         | 是   | 相册子类型。              |
| callback |  AsyncCallback&lt;[FetchResult](#fetchresult)&lt;[Album](#album)&gt;&gt; | 是   | callback返回获取相册的结果集。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if type options is not FetchOption.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
async function example() {
  // 示例代码中为获取统相册VIDEO，默认已预置。
  console.info('getAlbumsDemo');
  phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.VIDEO, async (err, fetchResult) => {
    if (err) {
      console.error(`getAlbumsCallback failed with err: ${err.code}, ${err.message}`);
      return;
    }
    if (fetchResult === undefined) {
      console.error('getAlbumsCallback fetchResult is undefined');
      return;
    }
    let album: photoAccessHelper.Album = await fetchResult.getFirstObject();
    console.info('getAlbumsCallback successfully, albumUri: ' + album.albumUri);
    fetchResult.close();
  });
}
```

### getAlbums

getAlbums(type: AlbumType, subtype: AlbumSubtype, options?: FetchOptions): Promise&lt;FetchResult&lt;Album&gt;&gt;

根据检索选项和相册类型获取相册，使用Promise方式返回结果。

获取相册前需先保证相册存在。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| type  | [AlbumType](#albumtype)         | 是   | 相册类型。              |
| subtype  | [AlbumSubtype](#albumsubtype)         | 是   | 相册子类型。              |
| options  | [FetchOptions](#fetchoptions)         | 否   |  检索选项，不填时默认根据相册类型检索。              |

**返回值：**

| 类型                        | 说明           |
| --------------------------- | -------------- |
| Promise&lt;[FetchResult](#fetchresult)&lt;[Album](#album)&gt;&gt; | Promise对象，返回获取相册的结果集。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if type options is not FetchOption.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  // 示例代码中为获取相册名为newAlbumName的相册。
  console.info('getAlbumsDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  predicates.equalTo('album_name', 'newAlbumName');
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, fetchOptions).then( async (fetchResult) => {
    if (fetchResult === undefined) {
      console.error('getAlbumsPromise fetchResult is undefined');
      return;
    }
    let album: photoAccessHelper.Album = await fetchResult.getFirstObject();
    console.info('getAlbumsPromise successfully, albumName: ' + album.albumName);
    fetchResult.close();
  }).catch((err: BusinessError) => {
    console.error(`getAlbumsPromise failed with err: ${err.code}, ${err.message}`);
  });
}
```

### registerChange

registerChange(uri: string, forChildUris: boolean, callback: Callback&lt;ChangeData&gt;) : void

注册对指定uri的监听，使用callback方式返回异步结果。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名    | 类型                                        | 必填 | 说明                                                         |
| --------- | ------------------------------------------- | ---- | ------------------------------------------------------------ |
| uri       | string                                      | 是   | PhotoAsset的uri, Album的uri或[DefaultChangeUri](#defaultchangeuri)的值。 |
| forChildUris | boolean                                     | 是   | 是否模糊监听，uri为相册uri时，forChildUris为true能监听到相册中文件的变化，如果是false只能监听相册本身变化。uri为photoAsset时，forChildUris为true、false没有区别，uri为DefaultChangeUri时，forChildUris必须为true，如果为false将找不到该uri，收不到任何消息。 |
| callback  | Callback&lt;[ChangeData](#changedata)&gt; | 是   | 返回要监听的[ChangeData](#changedata)。注：uri可以注册多个不同的callback监听，[unRegisterChange](#unregisterchange)可以关闭该uri所有监听，也可以关闭指定callback的监听。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('registerChangeDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
  let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
  if (photoAsset !== undefined) {
    console.info('photoAsset.displayName : ' + photoAsset.displayName);
  }
  let onCallback1 = (changeData: photoAccessHelper.ChangeData) => {
      console.info('onCallback1 success, changData: ' + JSON.stringify(changeData));
    //file had changed, do something
  }
  let onCallback2 = (changeData: photoAccessHelper.ChangeData) => {
      console.info('onCallback2 success, changData: ' + JSON.stringify(changeData));
    //file had changed, do something
  }
  // 注册onCallback1监听
  phAccessHelper.registerChange(photoAsset.uri, false, onCallback1);
  // 注册onCallback2监听
  phAccessHelper.registerChange(photoAsset.uri, false, onCallback2);

  await photoAccessHelper.MediaAssetChangeRequest.deleteAssets(context, [photoAsset]);
}
```

### unRegisterChange

unRegisterChange(uri: string, callback?: Callback&lt;ChangeData&gt;): void

取消指定uri的监听，一个uri可以注册多个监听，存在多个callback监听时，可以取消指定注册的callback的监听；不指定callback时取消该uri的所有监听。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                                        | 必填 | 说明                                                         |
| -------- | ------------------------------------------- | ---- | ------------------------------------------------------------ |
| uri      | string                                      | 是   | PhotoAsset的uri, Album的uri或[DefaultChangeUri](#defaultchangeuri)的值。 |
| callback | Callback&lt;[ChangeData](#changedata)&gt; | 否   | 取消[registerChange](#registerchange)注册时的callback的监听，不填时，取消该uri的所有监听。注：off指定注册的callback后不会进入此回调。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('offDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
  let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
  if (photoAsset !== undefined) {
    console.info('photoAsset.displayName : ' + photoAsset.displayName);
  }
  let onCallback1 = (changeData: photoAccessHelper.ChangeData) => {
    console.info('onCallback1 on');
  }
  let onCallback2 = (changeData: photoAccessHelper.ChangeData) => {
    console.info('onCallback2 on');
  }
  // 注册onCallback1监听
  phAccessHelper.registerChange(photoAsset.uri, false, onCallback1);
  // 注册onCallback2监听
  phAccessHelper.registerChange(photoAsset.uri, false, onCallback2);
  // 关闭onCallback1监听，onCallback2 继续监听
  phAccessHelper.unRegisterChange(photoAsset.uri, onCallback1);
  await photoAccessHelper.MediaAssetChangeRequest.deleteAssets(context, [photoAsset]);
}
```

### createDeleteRequest<sup>(deprecated)</sup>

createDeleteRequest(uriList: Array&lt;string&gt;, callback: AsyncCallback&lt;void&gt;): void

创建一个弹出框来删除照片，删除的文件进入到回收站，使用callback方式返回结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAssetChangeRequest.deleteAssets](#deleteassets11-1)替代。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| uriList | Array&lt;string&gt; | 是   | 待删除的媒体文件uri数组，最大删除数量300。 |
| callback | AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('createDeleteRequestDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let asset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    if (asset === undefined) {
      console.error('asset not exist');
      return;
    }
    phAccessHelper.createDeleteRequest([asset.uri], (err) => {
      if (err === undefined) {
        console.info('createDeleteRequest successfully');
      } else {
        console.error(`createDeleteRequest failed with error: ${err.code}, ${err.message}`);
      }
    });
  } catch (err) {
    console.error(`fetch failed, error: ${err.code}, ${err.message}`);
  }
}
```

### createDeleteRequest<sup>(deprecated)</sup>

createDeleteRequest(uriList: Array&lt;string&gt;): Promise&lt;void&gt;

创建一个弹出框来删除照片，删除的文件进入到回收站，使用Promise方式返回结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAssetChangeRequest.deleteAssets](#deleteassets11-1)替代。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| uriList | Array&lt;string&gt; | 是   | 待删除的媒体文件uri数组，最大删除数量300。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;void&gt;| Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('createDeleteRequestDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let asset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    if (asset === undefined) {
      console.error('asset not exist');
      return;
    }
    await phAccessHelper.createDeleteRequest([asset.uri]);
    console.info('createDeleteRequest successfully');
  } catch (err) {
    console.error(`createDeleteRequest failed with error: ${err.code}, ${err.message}`);
  }
}
```

### applyChanges<sup>11+</sup>

applyChanges(mediaChangeRequest: MediaChangeRequest): Promise&lt;void&gt;

提交媒体变更请求，使用Promise方式返回结果。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| mediaChangeRequest  | [MediaChangeRequest](#mediachangerequest11)  | 是  |  媒体变更请求，支持资产变更请求和相册变更请求。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;void&gt;| Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission denied.         |
| 401   | if parameter is invalid.   |
| 14000011  | System inner fail.     |

**示例：**

该接口依赖于[MediaChangeRequest](#mediachangerequest11)对象，详细代码示例请参见[MediaAssetChangeRequest](#mediaassetchangerequest11)和[MediaAlbumChangeRequest](#mediaalbumchangerequest11)中的接口示例。

### release

release(callback: AsyncCallback&lt;void&gt;): void

释放PhotoAccessHelper实例，使用callback方式返回结果。
当后续不需要使用PhotoAccessHelper实例中的方法时调用。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明                 |
| -------- | ------------------------- | ---- | -------------------- |
| callback | AsyncCallback&lt;void&gt; | 是   | 回调表示成功还是失败。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if parameter is invalid.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('releaseDemo');
  phAccessHelper.release((err) => {
    if (err !== undefined) {
      console.error(`release failed. error: ${err.code}, ${err.message}`);
    } else {
      console.info('release ok.');
    }
  });
}
```

### release

release(): Promise&lt;void&gt;

释放PhotoAccessHelper实例，使用Promise方式返回结果。
当后续不需要使用PhotoAccessHelper 实例中的方法时调用。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                | 说明                              |
| ------------------- | --------------------------------- |
| Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if parameter is invalid.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('releaseDemo');
  try {
    await phAccessHelper.release();
    console.info('release ok.');
  } catch (err) {
    console.error(`release failed. error: ${err.code}, ${err.message}`);
  }
}
```

## PhotoAsset

提供封装文件属性的方法。

### 属性

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                      | 类型                     | 可读 | 可写 | 说明                                                   |
| ------------------------- | ------------------------ | ---- | ---- | ------------------------------------------------------ |
| uri                       | string                   | 是   | 否   | 媒体文件资源uri（如：file://media/Photo/1/IMG_datetime_0001/displayName.jpg），详情参见用户文件uri介绍中的[媒体文件uri](../../file-management/user-file-uri-intro.md#媒体文件uri)。         |
| photoType   | [PhotoType](#phototype) | 是   | 否   | 媒体文件类型                                               |
| displayName               | string                   | 是   | 否   | 显示文件名，包含后缀名。                                 |

### get

get(member: string): MemberType

获取PhotoAsset成员参数。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名      | 类型                        | 必填   | 说明    |
| -------- | ------------------------- | ---- | ----- |
| member | string | 是    | 成员参数名称，在get时，除了'uri'、'media_type'和'display_name'三个属性之外，其他的属性都需要在fetchColumns中填入需要get的[PhotoKeys](#photokeys)，例如：get title属性fetchColumns: ['title']。 |

**返回值：**

| 类型                | 说明                              |
| ------------------- | --------------------------------- |
| [MemberType](#membertype) | 获取PhotoAsset成员参数的值。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401    | if parameter is invalid.         |
| 13900020     | Invalid argument.         |
| 14000014     | Member is not a valid PhotoKey.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('photoAssetGetDemo');
  try {
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption: photoAccessHelper.FetchOptions = {
      fetchColumns: ['title'],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    let title: photoAccessHelper.PhotoKeys = photoAccessHelper.PhotoKeys.TITLE;
    let photoAssetTitle: photoAccessHelper.MemberType = photoAsset.get(title.toString());
    console.info('photoAsset Get photoAssetTitle = ', photoAssetTitle);
  } catch (err) {
    console.error(`release failed. error: ${err.code}, ${err.message}`);
  }
}
```

### set

set(member: string, value: string): void

设置PhotoAsset成员参数。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名      | 类型                        | 必填   | 说明    |
| -------- | ------------------------- | ---- | ----- |
| member | string | 是    | 成员参数名称例如：[PhotoKeys](#photokeys).TITLE。 |
| value | string | 是    | 设置成员参数名称，只能修改[PhotoKeys](#photokeys).TITLE的值。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401    | if parameter is invalid.         |
| 13900020     | Invalid argument.         |
| 14000014     | Member is not a valid PhotoKey.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('photoAssetSetDemo');
  try {
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption: photoAccessHelper.FetchOptions = {
      fetchColumns: ['title'],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    let title: string = photoAccessHelper.PhotoKeys.TITLE.toString();
    photoAsset.set(title, 'newTitle');
  } catch (err) {
    console.error(`release failed. error: ${err.code}, ${err.message}`);
  }
}
```

### commitModify

commitModify(callback: AsyncCallback&lt;void&gt;): void

修改文件的元数据，使用callback方式返回异步结果。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名      | 类型                        | 必填   | 说明    |
| -------- | ------------------------- | ---- | ----- |
| callback | AsyncCallback&lt;void&gt; | 是    | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401    | if values to commit is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000001      | Invalid display name.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('commitModifyDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: ['title'],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
  let title: string = photoAccessHelper.PhotoKeys.TITLE.toString();
  let photoAssetTitle: photoAccessHelper.MemberType = photoAsset.get(title);
  console.info('photoAsset get photoAssetTitle = ', photoAssetTitle);
  photoAsset.set(title, 'newTitle2');
  photoAsset.commitModify((err) => {
    if (err === undefined) {
      let newPhotoAssetTitle: photoAccessHelper.MemberType = photoAsset.get(title);
      console.info('photoAsset get newPhotoAssetTitle = ', newPhotoAssetTitle);
    } else {
      console.error(`commitModify failed, error: ${err.code}, ${err.message}`);
    }
  });
}
```

### commitModify

commitModify(): Promise&lt;void&gt;

修改文件的元数据，使用promise方式返回异步结果。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                  | 说明         |
| ------------------- | ---------- |
| Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401    | if values to commit is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000001      | Invalid display name.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('commitModifyDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: ['title'],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
  let title: string = photoAccessHelper.PhotoKeys.TITLE.toString();
  let photoAssetTitle: photoAccessHelper.MemberType = photoAsset.get(title);
  console.info('photoAsset get photoAssetTitle = ', photoAssetTitle);
  photoAsset.set(title, 'newTitle3');
  try {
    await photoAsset.commitModify();
    let newPhotoAssetTitle: photoAccessHelper.MemberType = photoAsset.get(title);
    console.info('photoAsset get newPhotoAssetTitle = ', newPhotoAssetTitle);
  } catch (err) {
    console.error(`release failed. error: ${err.code}, ${err.message}`);
  }
}
```

### getReadOnlyFd<sup>(deprecated)</sup>

getReadOnlyFd(callback: AsyncCallback&lt;number&gt;): void

以只读方式打开当前文件，使用callback方式返回异步结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。出于安全考量，不再提供获取正式媒体文件句柄的接口。

**注意**：返回的文件描述符在使用完毕后需要调用close进行释放。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名      | 类型                          | 必填   | 说明                                  |
| -------- | --------------------------- | ---- | ----------------------------------- |
| callback | AsyncCallback&lt;number&gt; | 是    | callback返回文件描述符。                            |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('getReadOnlyFdDemo');
  // 需要保证设备中存在可读取图片视频文件
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let assetResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
  let photoAsset: photoAccessHelper.PhotoAsset = await assetResult.getFirstObject();
  photoAsset.getReadOnlyFd((err, fd) => {
    if (fd !== undefined) {
      console.info('File fd' + fd);
      photoAsset.close(fd);
    } else {
      console.error(`getReadOnlyFd err: ${err.code}, ${err.message}`);
    }
  });
}
```

### getReadOnlyFd<sup>(deprecated)</sup>

getReadOnlyFd(): Promise&lt;number&gt;

以只读方式打开当前文件，使用promise方式返回异步结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。出于安全考量，不再提供获取正式媒体文件句柄的接口。

**注意**：返回的文件描述符在使用完毕后需要调用close进行释放。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                    | 说明            |
| --------------------- | ------------- |
| Promise&lt;number&gt; | Promise对象，返回文件描述符。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('getReadOnlyFdDemo');
  try {
    // 需要保证设备中存在可读取图片视频文件
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let assetResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await assetResult.getFirstObject();
    let fd: number = await photoAsset.getReadOnlyFd();
    if (fd !== undefined) {
      console.info('File fd' + fd);
      photoAsset.close(fd);
    } else {
      console.error('getReadOnlyFd fail');
    }
  } catch (err) {
    console.error(`getReadOnlyFd demo err: ${err.code}, ${err.message}`);
  }
}
```

### close<sup>(deprecated)</sup>

close(fd: number, callback: AsyncCallback&lt;void&gt;): void

关闭当前文件，使用callback方式返回异步结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。出于安全考量，不再提供获取正式媒体文件句柄的接口。对应的close接口一并废弃。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名      | 类型                        | 必填   | 说明    |
| -------- | ------------------------- | ---- | ----- |
| fd       | number                    | 是    | 文件描述符。 |
| callback | AsyncCallback&lt;void&gt; | 是    | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('closeDemo');
  try {
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    let fd: number = await photoAsset.open('rw');
    console.info('file fd', fd);
    photoAsset.close(fd, (err) => {
      if (err === undefined) {
        console.info('asset close succeed.');
      } else {
        console.error(`close failed, error: ${err.code}, ${err.message}`);
      }
    });
  } catch (err) {
    console.error(`close failed, error: ${err.code}, ${err.message}`);
  }
}
```

### close<sup>(deprecated)</sup>

close(fd: number): Promise&lt;void&gt;

关闭当前文件，使用promise方式返回异步结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。出于安全考量，不再提供获取正式媒体文件句柄的接口。对应的close接口一并废弃。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| fd   | number | 是    | 文件描述符。 |

**返回值：**

| 类型                  | 说明         |
| ------------------- | ---------- |
| Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('closeDemo');
  try {
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
    let asset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    let fd = await asset.open('rw');
    console.info('file fd', fd);
    await asset.close(fd);
    console.info('asset close succeed.');
  } catch (err) {
    console.error(`close failed, error: ${err.code}, ${err.message}`);
  }
}
```

### getThumbnail

getThumbnail(callback: AsyncCallback&lt;image.PixelMap&gt;): void

获取文件的缩略图，使用callback方式返回异步结果。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名      | 类型                                  | 必填   | 说明               |
| -------- | ----------------------------------- | ---- | ---------------- |
| callback | AsyncCallback&lt;[image.PixelMap](../apis-image-kit/js-apis-image.md#pixelmap7)&gt; | 是    | callback返回缩略图的PixelMap。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getThumbnailDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let asset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
  console.info('asset displayName = ', asset.displayName);
  asset.getThumbnail((err, pixelMap) => {
    if (err === undefined) {
      console.info('getThumbnail successful ' + pixelMap);
    } else {
      console.error(`getThumbnail fail with error: ${err.code}, ${err.message}`);
    }
  });
}
```

### getThumbnail

getThumbnail(size: image.Size, callback: AsyncCallback&lt;image.PixelMap&gt;): void

获取文件的缩略图，传入缩略图尺寸，使用callback方式返回异步结果。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名      | 类型                                  | 必填   | 说明               |
| -------- | ----------------------------------- | ---- | ---------------- |
| size     | [image.Size](../apis-image-kit/js-apis-image.md#size) | 是    | 缩略图尺寸。            |
| callback | AsyncCallback&lt;[image.PixelMap](../apis-image-kit/js-apis-image.md#pixelmap7)&gt; | 是    | callback返回缩略图的PixelMap。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import image from '@ohos.multimedia.image'

async function example() {
  console.info('getThumbnailDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let size: image.Size = { width: 720, height: 720 };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let asset = await fetchResult.getFirstObject();
  console.info('asset displayName = ', asset.displayName);
  asset.getThumbnail(size, (err, pixelMap) => {
    if (err === undefined) {
      console.info('getThumbnail successful ' + pixelMap);
    } else {
      console.error(`getThumbnail fail with error: ${err.code}, ${err.message}`);
    }
  });
}
```

### getThumbnail

getThumbnail(size?: image.Size): Promise&lt;image.PixelMap&gt;

获取文件的缩略图，传入缩略图尺寸，使用promise方式返回异步结果。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型             | 必填   | 说明    |
| ---- | -------------- | ---- | ----- |
| size | [image.Size](../apis-image-kit/js-apis-image.md#size) | 否    | 缩略图尺寸。 |

**返回值：**

| 类型                            | 说明                    |
| ----------------------------- | --------------------- |
| Promise&lt;[image.PixelMap](../apis-image-kit/js-apis-image.md#pixelmap7)&gt; | Promise对象，返回缩略图的PixelMap。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import image from '@ohos.multimedia.image'
import { BusinessError } from '@ohos.base';

async function example() {
  console.info('getThumbnailDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let size: image.Size = { width: 720, height: 720 };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let asset = await fetchResult.getFirstObject();
  console.info('asset displayName = ', asset.displayName);
  asset.getThumbnail(size).then((pixelMap) => {
    console.info('getThumbnail successful ' + pixelMap);
  }).catch((err: BusinessError) => {
    console.error(`getThumbnail fail with error: ${err.code}, ${err.message}`);
  });
}
```

## PhotoViewPicker

图库选择器对象，用来支撑选择图片/视频等用户场景。在使用前，需要先创建PhotoViewPicker实例。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**示例：**

```ts
let photoPicker = new photoAccessHelper.PhotoViewPicker();
```

### select

select(option?: PhotoSelectOptions) : Promise&lt;PhotoSelectResult&gt;

通过选择模式拉起photoPicker界面，用户可以选择一个或多个图片/视频。接口采用promise异步返回形式，传入可选参数PhotoSelectOptions对象，返回PhotoSelectResult对象。

**注意**：此接口返回的PhotoSelectResult对象中的photoUris只能通过临时授权的方式调用[photoAccessHelper.getAssets接口](#getassets)去使用，具体使用方式参见用户文件uri介绍中的[媒体文件uri的使用方式](../../file-management/user-file-uri-intro.md#媒体文件uri的使用方式)。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型    | 必填 | 说明                       |
| ------- | ------- | ---- | -------------------------- |
| option | [PhotoSelectOptions](#photoselectoptions) | 否   | photoPicker选择选项，若无此参数，则默认选择媒体文件类型为图片和视频类型，选择媒体文件数量的最大值为50 |

**返回值：**

| 类型                            | 说明    |
| ----------------------------- | :---- |
| Promise&lt;[PhotoSelectResult](#photoselectresult)&gt; | Promise对象。返回photoPicker选择后的结果集 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if parameter is invalid.         |
| 13900042      | Unknown error.         |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
async function example01() {
  try {
    let PhotoSelectOptions = new photoAccessHelper.PhotoSelectOptions();
    PhotoSelectOptions.MIMEType = photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE;
    PhotoSelectOptions.maxSelectNumber = 5;
    let photoPicker = new photoAccessHelper.PhotoViewPicker();
    photoPicker.select(PhotoSelectOptions).then((PhotoSelectResult: photoAccessHelper.PhotoSelectResult) => {
      console.info('PhotoViewPicker.select successfully, PhotoSelectResult uri: ' + JSON.stringify(PhotoSelectResult));
    }).catch((err: BusinessError) => {
      console.error(`PhotoViewPicker.select failed with err: ${err.code}, ${err.message}`);
    });
  } catch (error) {
    let err: BusinessError = error as BusinessError;
    console.error(`PhotoViewPicker failed with err: ${err.code}, ${err.message}`);
  }
}
```

### select

select(option: PhotoSelectOptions, callback: AsyncCallback&lt;PhotoSelectResult&gt;) : void

通过选择模式拉起photoPicker界面，用户可以选择一个或多个图片/视频。接口采用callback异步返回形式，传入参数PhotoSelectOptions对象，返回PhotoSelectResult对象。

**注意**：此接口返回的PhotoSelectResult对象中的photoUris只能通过临时授权的方式调用[photoAccessHelper.getAssets接口](#getassets)去使用，具体使用方式参见用户文件uri介绍中的[媒体文件uri的使用方式](../../file-management/user-file-uri-intro.md#媒体文件uri的使用方式)。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型    | 必填 | 说明                       |
| ------- | ------- | ---- | -------------------------- |
| option | [PhotoSelectOptions](#photoselectoptions) | 是   | photoPicker选择选项 |
| callback | AsyncCallback&lt;[PhotoSelectResult](#photoselectresult)&gt;      | 是   | callback 返回photoPicker选择后的结果集 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if parameter is invalid.         |
| 13900042      | Unknown error.         |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
async function example02() {
  try {
    let PhotoSelectOptions = new photoAccessHelper.PhotoSelectOptions();
    PhotoSelectOptions.MIMEType = photoAccessHelper.PhotoViewMIMETypes.IMAGE_TYPE;
    PhotoSelectOptions.maxSelectNumber = 5;
    let photoPicker = new photoAccessHelper.PhotoViewPicker();
    photoPicker.select(PhotoSelectOptions, (err: BusinessError, PhotoSelectResult: photoAccessHelper.PhotoSelectResult) => {
      if (err) {
        console.error(`PhotoViewPicker.select failed with err: ${err.code}, ${err.message}`);
        return;
      }
      console.info('PhotoViewPicker.select successfully, PhotoSelectResult uri: ' + JSON.stringify(PhotoSelectResult));
    });
  } catch (error) {
    let err: BusinessError = error as BusinessError;
    console.error(`PhotoViewPicker failed with err: ${err.code}, ${err.message}`);
  }
}
```

### select

select(callback: AsyncCallback&lt;PhotoSelectResult&gt;) : void

通过选择模式拉起photoPicker界面，用户可以选择一个或多个图片/视频。接口采用callback异步返回形式，返回PhotoSelectResult对象。

**注意**：此接口返回的PhotoSelectResult对象中的photoUris只能通过临时授权的方式调用[photoAccessHelper.getAssets接口](#getassets)去使用，具体使用方式参见用户文件uri介绍中的[媒体文件uri的使用方式](../../file-management/user-file-uri-intro.md#媒体文件uri的使用方式)。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型    | 必填 | 说明                       |
| ------- | ------- | ---- | -------------------------- |
| callback | AsyncCallback&lt;[PhotoSelectResult](#photoselectresult)&gt;      | 是   | callback 返回photoPicker选择后的结果集 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if parameter is invalid.         |
| 13900042      | Unknown error.         |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
async function example03() {
  try {
    let photoPicker = new photoAccessHelper.PhotoViewPicker();
    photoPicker.select((err: BusinessError, PhotoSelectResult: photoAccessHelper.PhotoSelectResult) => {
      if (err) {
        console.error(`PhotoViewPicker.select failed with err: ${err.code}, ${err.message}`);
        return;
      }
      console.info('PhotoViewPicker.select successfully, PhotoSelectResult uri: ' + JSON.stringify(PhotoSelectResult));
    });
  } catch (error) {
    let err: BusinessError = error as BusinessError;
    console.error(`PhotoViewPicker failed with err: ${err.code}, ${err.message}`);
  }
}
```

## FetchResult

文件检索结果集。

### getCount

getCount(): number

获取文件检索结果中的文件总数。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型     | 说明       |
| ------ | -------- |
| number | 检索到的文件总数。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getCountDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let fetchCount = fetchResult.getCount();
  console.info('fetchCount = ', fetchCount);
}
```

### isAfterLast

isAfterLast(): boolean

检查结果集是否指向最后一行。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型      | 说明                                 |
| ------- | ---------------------------------- |
| boolean | 当读到最后一条记录后，后续没有记录返回true，否则返回false。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let fetchCount = fetchResult.getCount();
  console.info('count:' + fetchCount);
  let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getLastObject();
  if (fetchResult.isAfterLast()) {
    console.info('photoAsset isAfterLast displayName = ', photoAsset.displayName);
  } else {
    console.info('photoAsset not isAfterLast.');
  }
}
```

### close

close(): void

释放FetchResult实例并使其失效。无法调用其他方法。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('fetchResultCloseDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
    fetchResult.close();
    console.info('close succeed.');
  } catch (err) {
    console.error(`close fail. error: ${err.code}, ${err.message}`);
  }
}
```

### getFirstObject

getFirstObject(callback: AsyncCallback&lt;T&gt;): void

获取文件检索结果中的第一个文件资产。此方法使用callback形式返回结果。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                                          | 必填 | 说明                                        |
| -------- | --------------------------------------------- | ---- | ------------------------------------------- |
| callback | AsyncCallback&lt;T&gt; | 是   | 异步获取结果集中的第一个完成后的回调。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getFirstObjectDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  fetchResult.getFirstObject((err, photoAsset) => {
    if (photoAsset !== undefined) {
      console.info('photoAsset displayName: ', photoAsset.displayName);
    } else {
      console.error(`photoAsset failed with err:${err.code}, ${err.message}`);
    }
  });
}
```

### getFirstObject

getFirstObject(): Promise&lt;T&gt;

获取文件检索结果中的第一个文件资产。此方法使用promise方式来异步返回。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                                    | 说明                       |
| --------------------------------------- | -------------------------- |
| Promise&lt;T&gt; | Promise对象，返回结果集中第一个对象。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getFirstObjectDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
  console.info('photoAsset displayName: ', photoAsset.displayName);
}
```

### getNextObject

getNextObject(callback: AsyncCallback&lt;T&gt;): void

获取文件检索结果中的下一个文件资产。此方法使用callback形式返回结果。
在调用此方法之前，必须使用[isAfterLast()](#isafterlast)来检查当前位置是否为最后一行。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名    | 类型                                          | 必填 | 说明                                      |
| --------- | --------------------------------------------- | ---- | ----------------------------------------- |
| callback | AsyncCallback&lt;T&gt; | 是   | 异步返回结果集中下一个之后的回调。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getNextObjectDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  await fetchResult.getFirstObject();
  if (!fetchResult.isAfterLast()) {
    fetchResult.getNextObject((err, photoAsset) => {
      if (photoAsset !== undefined) {
        console.info('photoAsset displayName: ', photoAsset.displayName);
      } else {
        console.error(`photoAsset failed with err: ${err.code}, ${err.message}`);
      }
    });
  }
}
```

### getNextObject

getNextObject(): Promise&lt;T&gt;

获取文件检索结果中的下一个文件资产。此方法使用promise方式来异步返回。
在调用此方法之前，必须使用[isAfterLast()](#isafterlast)来检查当前位置是否为最后一行。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;T&gt; | Promise对象，返回结果集中下一个对象。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getNextObjectDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  await fetchResult.getFirstObject();
  if (!fetchResult.isAfterLast()) {
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getNextObject();
    console.info('photoAsset displayName: ', photoAsset.displayName);
  }
}
```

### getLastObject

getLastObject(callback: AsyncCallback&lt;T&gt;): void

获取文件检索结果中的最后一个文件资产。此方法使用callback回调来返回。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                                          | 必填 | 说明                        |
| -------- | --------------------------------------------- | ---- | --------------------------- |
| callback | AsyncCallback&lt;T&gt; | 是   | 异步返回结果集中最后一个的回调。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getLastObjectDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  fetchResult.getLastObject((err, photoAsset) => {
    if (photoAsset !== undefined) {
      console.info('photoAsset displayName: ', photoAsset.displayName);
    } else {
      console.error(`photoAsset failed with err: ${err.code}, ${err.message}`);
    }
  });
}
```

### getLastObject

getLastObject(): Promise&lt;T&gt;

获取文件检索结果中的最后一个文件资产。此方法使用Promise方式来返回。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;T&gt; | Promise对象，返回结果集中最后一个对象。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getLastObjectDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getLastObject();
  console.info('photoAsset displayName: ', photoAsset.displayName);
}
```

### getObjectByPosition

getObjectByPosition(index: number, callback: AsyncCallback&lt;T&gt;): void

获取文件检索结果中具有指定索引的文件资产。此方法使用callback来返回。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名       | 类型                                       | 必填   | 说明                 |
| -------- | ---------------------------------------- | ---- | ------------------ |
| index    | number                                   | 是    | 要获取的文件的索引，从0开始。     |
| callback | AsyncCallback&lt;T&gt; | 是    | 异步返回指定索引的文件资产的回调。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if type index is not number.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getObjectByPositionDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  fetchResult.getObjectByPosition(0, (err, photoAsset) => {
    if (photoAsset !== undefined) {
      console.info('photoAsset displayName: ', photoAsset.displayName);
    } else {
      console.error(`photoAsset failed with err: ${err.code}, ${err.message}`);
    }
  });
}
```

### getObjectByPosition

getObjectByPosition(index: number): Promise&lt;T&gt;

获取文件检索结果中具有指定索引的文件资产。此方法使用Promise形式返回文件Asset。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名    | 类型     | 必填   | 说明             |
| ----- | ------ | ---- | -------------- |
| index | number | 是    | 要获取的文件的索引，从0开始。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;T&gt; | Promise对象，返回结果集中指定索引的一个对象。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if type index is not number.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getObjectByPositionDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getObjectByPosition(0);
  console.info('photoAsset displayName: ', photoAsset.displayName);
}
```

### getAllObjects

getAllObjects(callback: AsyncCallback&lt;Array&lt;T&gt;&gt;): void

获取文件检索结果中的所有文件资产。此方法使用callback形式返回结果。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                                          | 必填 | 说明                                        |
| -------- | --------------------------------------------- | ---- | ------------------------------------------- |
| callback | AsyncCallback&lt;Array&lt;T&gt;&gt; | 是   | 异步获取结果集中的所有文件资产完成后的回调。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getAllObjectDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  fetchResult.getAllObjects((err, photoAssetList) => {
    if (photoAssetList !== undefined) {
      console.info('photoAssetList length: ', photoAssetList.length);
    } else {
      console.error(`photoAssetList failed with err:${err.code}, ${err.message}`);
    }
  });
}
```

### getAllObjects

getAllObjects(): Promise&lt;Array&lt;T&gt;&gt;

获取文件检索结果中的所有文件资产。此方法使用promise方式来异步返回。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                                    | 说明                       |
| --------------------------------------- | -------------------------- |
| Promise&lt;Array&lt;T&gt;&gt; | Promise对象，返回结果集中所有文件资产数组。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('getAllObjectDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let photoAssetList: Array<photoAccessHelper.PhotoAsset> = await fetchResult.getAllObjects();
  console.info('photoAssetList length: ', photoAssetList.length);
}
```

## Album

实体相册

### 属性

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称           | 类型    | 可读   | 可写  | 说明   |
| ------------ | ------ | ---- | ---- | ------- |
| albumType | [AlbumType]( #albumtype) | 是    | 否    | 相册类型。    |
| albumSubtype | [AlbumSubtype]( #albumsubtype) | 是    | 否   | 相册子类型。    |
| albumName | string | 是    | 用户相册可写，预置相册不可写   | 相册名称。    |
| albumUri | string | 是    | 否    | 相册Uri。   |
| count | number | 是    | 否    |  相册中文件数量。 |
| coverUri | string | 是    | 否    | 封面文件Uri。 |
| imageCount<sup>11+</sup> | number | 是   | 否   | 相册中图片数量。|
| videoCount<sup>11+</sup> | number | 是   | 否   | 相册中视频数量。|

### getAssets

getAssets(options: FetchOptions, callback: AsyncCallback&lt;FetchResult&lt;PhotoAsset&gt;&gt;): void

获取相册中的文件。该方法使用callback形式来返回文件。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| options | [FetchOptions](#fetchoptions) | 是   | 检索选项。 |
| callback | AsyncCallback&lt;[FetchResult](#fetchresult)&lt;[PhotoAsset](#photoasset)&gt;&gt; | 是   | callback返回图片和视频数据结果集。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if type options is not FetchOptions.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('albumGetAssetsDemoCallback');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let albumFetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let albumList: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, albumFetchOptions);
  let album: photoAccessHelper.Album = await albumList.getFirstObject();
  album.getAssets(fetchOption, (err, albumFetchResult) => {
    if (albumFetchResult !== undefined) {
      console.info('album getAssets successfully, getCount: ' + albumFetchResult.getCount());
    } else {
      console.error(`album getAssets failed with error: ${err.code}, ${err.message}`);
    }
  });
}
```

### getAssets

getAssets(options: FetchOptions): Promise&lt;FetchResult&lt;PhotoAsset&gt;&gt;

获取相册中的文件。该方法使用Promise来返回文件。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| options | [FetchOptions](#fetchoptions) | 是   | 检索选项。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;[FetchResult](#fetchresult)&lt;[PhotoAsset](#photoasset)&gt;&gt; | Promise对象，返回图片和视频数据结果集。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if type options is not FetchOptions.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  console.info('albumGetAssetsDemoPromise');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let albumFetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let albumList: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, albumFetchOptions);
  let album: photoAccessHelper.Album = await albumList.getFirstObject();
  album.getAssets(fetchOption).then((albumFetchResult) => {
    console.info('album getAssets successfully, getCount: ' + albumFetchResult.getCount());
  }).catch((err: BusinessError) => {
    console.error(`album getAssets failed with error: ${err.code}, ${err.message}`);
  });
}
```

### commitModify

commitModify(callback: AsyncCallback&lt;void&gt;): void

更新相册属性修改到数据库中。该方法使用callback形式来返回结果。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| callback | AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       | if value to modify is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('albumCommitModifyDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let albumFetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let albumList: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, albumFetchOptions);
  let album: photoAccessHelper.Album = await albumList.getFirstObject();
  album.albumName = 'hello';
  album.commitModify((err) => {
    if (err !== undefined) {
      console.error(`commitModify failed with error: ${err.code}, ${err.message}`);
    } else {
      console.info('commitModify successfully');
    }
  });
}
```

### commitModify

commitModify(): Promise&lt;void&gt;

更新相册属性修改到数据库中。该方法使用Promise来返回结果。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                  | 说明           |
| ------------------- | ------------ |
| Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if value to modify is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  console.info('albumCommitModifyDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let albumFetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let albumList: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, albumFetchOptions);
  let album: photoAccessHelper.Album = await albumList.getFirstObject();
  album.albumName = 'hello';
  album.commitModify().then(() => {
    console.info('commitModify successfully');
  }).catch((err: BusinessError) => {
    console.error(`commitModify failed with error: ${err.code}, ${err.message}`);
  });
}
```

### addAssets<sup>(deprecated)</sup>

addAssets(assets: Array&lt;PhotoAsset&gt;, callback: AsyncCallback&lt;void&gt;): void

往相册中添加图片或者视频，需要先预置相册和文件资源。该方法使用callback形式来返回结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAlbumChangeRequest.addAssets](#addassets11)替代。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 待添加到相册中的图片或视频数组。 |
| callback | AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('addAssetsDemoCallback');
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC);
    let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
    let asset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    album.addAssets([asset], (err) => {
      if (err === undefined) {
        console.info('album addAssets successfully');
      } else {
        console.error(`album addAssets failed with error: ${err.code}, ${err.message}`);
      }
    });
  } catch (err) {
    console.error(`addAssetsDemoCallback failed with error: ${err.code}, ${err.message}`);
  }
}
```

### addAssets<sup>(deprecated)</sup>

addAssets(assets: Array&lt;PhotoAsset&gt;): Promise&lt;void&gt;

往相册中添加图片或者视频，需要先预置相册和文件资源。该方法使用Promise来返回结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAlbumChangeRequest.addAssets](#addassets11)替代。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 待添加到相册中的图片或视频数组。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
|Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  try {
    console.info('addAssetsDemoPromise');
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC);
    let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
    let asset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    album.addAssets([asset]).then(() => {
      console.info('album addAssets successfully');
    }).catch((err: BusinessError) => {
      console.error(`album addAssets failed with error: ${err.code}, ${err.message}`);
    });
  } catch (err) {
    console.error(`addAssetsDemoPromise failed with error: ${err.code}, ${err.message}`);
  }
}
```

### removeAssets<sup>(deprecated)</sup>

removeAssets(assets: Array&lt;PhotoAsset&gt;, callback: AsyncCallback&lt;void&gt;): void

从相册中移除图片或者视频，需要先预置相册和文件资源。该方法使用callback形式来返回结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAlbumChangeRequest.removeAssets](#removeassets11)替代。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 相册中待移除的图片或视频数组。 |
| callback | AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('removeAssetsDemoCallback');
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC);
    let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await album.getAssets(fetchOption);
    let asset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    album.removeAssets([asset], (err) => {
      if (err === undefined) {
        console.info('album removeAssets successfully');
      } else {
        console.error(`album removeAssets failed with error: ${err.code}, ${err.message}`);
      }
    });
  } catch (err) {
    console.error(`removeAssetsDemoCallback failed with error: ${err.code}, ${err.message}`);
  }
}
```

### removeAssets<sup>(deprecated)</sup>

removeAssets(assets: Array&lt;PhotoAsset&gt;): Promise&lt;void&gt;

从相册中移除图片或者视频，需要先预置相册和文件资源。该方法使用Promise来返回结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAlbumChangeRequest.removeAssets](#removeassets11)替代。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 相册中待移除的图片或视频数组。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
|Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  try {
    console.info('removeAssetsDemoPromise');
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC);
    let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await album.getAssets(fetchOption);
    let asset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    album.removeAssets([asset]).then(() => {
      console.info('album removeAssets successfully');
    }).catch((err: BusinessError) => {
      console.error(`album removeAssets failed with error: ${err.code}, ${err.message}`);
    });
  } catch (err) {
    console.error(`removeAssetsDemoPromise failed with error: ${err.code}, ${err.message}`);
  }
}
```

## MediaAssetChangeRequest<sup>11+</sup>

资产变更请求。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

### constructor<sup>11+</sup>

constructor(asset: PhotoAsset)

构造函数。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| asset | [PhotoAsset](#photoasset) | 是   | 需要变更的资产。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if parameter is invalid.         |
| 14000011       | System inner fail.          |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('MediaAssetChangeRequest constructorDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
  let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
  let assetChangeRequest: photoAccessHelper.MediaAssetChangeRequest = new photoAccessHelper.MediaAssetChangeRequest(photoAsset);
}
```

### createImageAssetRequest<sup>11+</sup>

static createImageAssetRequest(context: Context, fileUri: string): MediaAssetChangeRequest

创建图片资产变更请求。

通过fileUri指定待创建资产的数据来源，可参考[FileUri](../apis-core-file-kit/js-apis-file-fileuri.md)。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型    | 必填 | 说明                       |
| ------- | ------- | ---- | -------------------------- |
| context | [Context](../apis-ability-kit/js-apis-inner-application-context.md) | 是   | 传入Ability实例的Context。 |
| fileUri | string | 是   | 图片资产的数据来源，在应用沙箱下的uri。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| [MediaAssetChangeRequest](#mediaassetchangerequest11) | 返回创建资产的变更请求。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |
| 13900002   | No such file.         |
| 14000011   | System inner fail.        |

**示例：**

```ts
async function example() {
  console.info('createImageAssetRequestDemo');
  try {
    // 需要确保fileUri对应的资源存在
    let fileUri = 'file://com.example.temptest/data/storage/el2/base/haps/entry/files/test.jpg';
    let assetChangeRequest: photoAccessHelper.MediaAssetChangeRequest = photoAccessHelper.MediaAssetChangeRequest.createImageAssetRequest(context, fileUri);
    await phAccessHelper.applyChanges(assetChangeRequest);
    console.info('apply createImageAssetRequest successfully');
  } catch (err) {
    console.error(`createImageAssetRequestDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### createVideoAssetRequest<sup>11+</sup>

static createVideoAssetRequest(context: Context, fileUri: string): MediaAssetChangeRequest

创建视频资产变更请求。

通过fileUri指定待创建资产的数据来源，可参考[FileUri](../apis-core-file-kit/js-apis-file-fileuri.md)。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型    | 必填 | 说明                       |
| ------- | ------- | ---- | -------------------------- |
| context | [Context](../apis-ability-kit/js-apis-inner-application-context.md) | 是   | 传入Ability实例的Context。 |
| fileUri | string | 是   | 视频资产的数据来源，在应用沙箱下的uri。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| [MediaAssetChangeRequest](#mediaassetchangerequest11) | 返回创建资产的变更请求。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401   | if parameter is invalid.         |
| 13900002   | No such file.         |
| 14000011   | System inner fail.        |

**示例：**

```ts
async function example() {
  console.info('createVideoAssetRequestDemo');
  try {
    // 需要确保fileUri对应的资源存在
    let fileUri = 'file://com.example.temptest/data/storage/el2/base/haps/entry/files/test.mp4';
    let assetChangeRequest: photoAccessHelper.MediaAssetChangeRequest = photoAccessHelper.MediaAssetChangeRequest.createVideoAssetRequest(context, fileUri);
    await phAccessHelper.applyChanges(assetChangeRequest);
    console.info('apply createVideoAssetRequest successfully');
  } catch (err) {
    console.error(`createVideoAssetRequestDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### createAssetRequest<sup>11+</sup>

static createAssetRequest(context: Context, photoType: PhotoType, extension: string, options?: CreateOptions): MediaAssetChangeRequest

指定待创建的文件类型和扩展名，创建资产变更请求。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型    | 必填 | 说明                       |
| ------- | ------- | ---- | -------------------------- |
| context | [Context](../apis-ability-kit/js-apis-inner-application-context.md) | 是   | 传入Ability实例的Context。 |
| photoType  | [PhotoType](#phototype)        | 是   | 待创建的文件类型，IMAGE或者VIDEO类型。              |
| extension  | string        | 是   | 文件扩展名，例如：'jpg'。              |
| options  | [CreateOptions](#createoptions)        | 否   | 创建选项，例如：{title: 'testPhoto'}。              |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| [MediaAssetChangeRequest](#mediaassetchangerequest11) | 返回创建资产的变更请求。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if parameter is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('createAssetRequestDemo');
  try {
    let photoType: photoAccessHelper.PhotoType = photoAccessHelper.PhotoType.IMAGE;
    let extension: string = 'jpg';
    let options: photoAccessHelper.CreateOptions = {
      title: 'testPhoto'
    }
    let assetChangeRequest: photoAccessHelper.MediaAssetChangeRequest = photoAccessHelper.MediaAssetChangeRequest.createAssetRequest(context, photoType, extension, options);
    // 需要确保fileUri对应的资源存在
    let fileUri = 'file://com.example.temptest/data/storage/el2/base/haps/entry/files/test.jpg';
    assetChangeRequest.addResource(photoAccessHelper.ResourceType.IMAGE_RESOURCE, fileUri);
    await phAccessHelper.applyChanges(assetChangeRequest);
    console.info('apply createAssetRequest successfully');
  } catch (err) {
    console.error(`createAssetRequestDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### deleteAssets<sup>11+</sup>

static deleteAssets(context: Context, assets: Array&lt;PhotoAsset&gt;): Promise&lt;void&gt;

删除媒体文件，删除的文件进入到回收站，使用Promise方式返回结果。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型    | 必填 | 说明                       |
| ------- | ------- | ---- | -------------------------- |
| context | [Context](../apis-ability-kit/js-apis-inner-application-context.md) | 是   | 传入Ability实例的Context。 |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 待删除的媒体文件数组。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;void&gt;| Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201      |  Permission denied.         |
| 401      |  if parameter is invalid.   |
| 14000011 |  System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('deleteAssetsDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAssetList: Array<photoAccessHelper.PhotoAsset> = await fetchResult.getAllObjects();
    await photoAccessHelper.MediaAssetChangeRequest.deleteAssets(context, photoAssetList);
    console.info('deleteAssets successfully');
  } catch (err) {
    console.error(`deleteAssetsDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### deleteAssets<sup>11+</sup>

static deleteAssets(context: Context, uriList: Array&lt;string&gt;): Promise&lt;void&gt;

删除媒体文件，删除的文件进入到回收站，使用Promise方式返回结果。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型    | 必填 | 说明                       |
| ------- | ------- | ---- | -------------------------- |
| context | [Context](../apis-ability-kit/js-apis-inner-application-context.md) | 是   | 传入Ability实例的Context。 |
| uriList | Array&lt;string&gt; | 是   | 待删除的媒体文件uri数组。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;void&gt;| Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201      |  Permission denied.         |
| 401      |  if parameter is invalid.   |
| 14000002 |  Invalid asset uri.         |
| 14000011 |  System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('deleteAssetsDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let asset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    await photoAccessHelper.MediaAssetChangeRequest.deleteAssets(context, [asset.uri]);
    console.info('deleteAssets successfully');
  } catch (err) {
    console.error(`deleteAssetsDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### getAsset<sup>11+</sup>

getAsset(): PhotoAsset

获取当前资产变更请求中的资产。

**注意**：对于创建资产的变更请求，在调用[applyChanges](#applychanges11)提交生效之前，该接口返回null。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| [PhotoAsset](#photoasset) | 返回当前资产变更请求中的资产。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if parameter is invalid.   |
| 14000011 |  System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('getAssetDemo');
  try {
    // 需要确保fileUri对应的资源存在
    let fileUri = 'file://com.example.temptest/data/storage/el2/base/haps/entry/files/test.jpg';
    let assetChangeRequest: photoAccessHelper.MediaAssetChangeRequest = photoAccessHelper.MediaAssetChangeRequest.createImageAssetRequest(context, fileUri);
    await phAccessHelper.applyChanges(assetChangeRequest);
    let asset: photoAccessHelper.PhotoAsset = assetChangeRequest.getAsset();
    console.info('create asset successfully with uri = ' + asset.uri);
  } catch (err) {
    console.error(`getAssetDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### setTitle<sup>11+</sup>

setTitle(title: string): void

修改媒体资产的标题。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| title | string | 是   | 待修改的资产标题。 |

title参数规格为：
- 不应包含扩展名。
- 文件名字符串长度为1~255。
- 不允许出现非法字符，包括：<br> . .. \ / : * ? " ' ` < > | { } [ ]

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  console.info('setTitleDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let asset = await fetchResult.getFirstObject();
  let assetChangeRequest: photoAccessHelper.MediaAssetChangeRequest = new photoAccessHelper.MediaAssetChangeRequest(asset);
  let newTitle: string = 'newTitle';
  assetChangeRequest.setTitle(newTitle);
  phAccessHelper.applyChanges(assetChangeRequest).then(() => {
    console.info('apply setTitle successfully');
  }).catch((err: BusinessError) => {
    console.error(`apply setTitle failed with error: ${err.code}, ${err.message}`);
  });
}
```

### getWriteCacheHandler<sup>11+</sup>

getWriteCacheHandler(): Promise&lt;number&gt;

获取临时文件写句柄。

**注意**：对于同一个资产变更请求，不支持在成功获取临时文件写句柄后，重复调用该接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;number&gt; | Promise对象，返回临时文件写句柄。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission denied.        |
| 401      |  if parameter is invalid.   |
| 14000011 |  System inner fail.         |
| 14000016 |  Operation Not Support.     |

**示例：**

```ts
import fs from '@ohos.file.fs';

async function example() {
  console.info('getWriteCacheHandlerDemo');
  try {
    let photoType: photoAccessHelper.PhotoType = photoAccessHelper.PhotoType.VIDEO;
    let extension: string = 'mp4';
    let assetChangeRequest: photoAccessHelper.MediaAssetChangeRequest = photoAccessHelper.MediaAssetChangeRequest.createAssetRequest(context, photoType, extension);
    let fd: number = await assetChangeRequest.getWriteCacheHandler();
    console.info('getWriteCacheHandler successfully');
    // write date into fd
    await fs.close(fd);
    await phAccessHelper.applyChanges(assetChangeRequest);
  } catch (err) {
    console.error(`getWriteCacheHandlerDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### addResource<sup>11+</sup>

addResource(type: ResourceType, fileUri: string): void

通过fileUri从应用沙箱添加资源。

**注意**：对于同一个资产变更请求，不支持在成功添加资源后，重复调用该接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型    | 必填 | 说明                       |
| ------- | ------- | ---- | -------------------------- |
| type | [ResourceType](#resourcetype11) | 是   | 待添加资源的类型。 |
| fileUri | string | 是   | 待添加资源的数据来源，在应用沙箱下的uri。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if parameter is invalid.   |
| 13900002      |  No such file.   |
| 14000011 |  System inner fail.         |
| 14000016 |  Operation Not Support.     |

**示例：**

```ts
async function example() {
  console.info('addResourceByFileUriDemo');
  try {
    let photoType: photoAccessHelper.PhotoType = photoAccessHelper.PhotoType.IMAGE;
    let extension: string = 'jpg';
    let assetChangeRequest: photoAccessHelper.MediaAssetChangeRequest = photoAccessHelper.MediaAssetChangeRequest.createAssetRequest(context, photoType, extension);
    // 需要确保fileUri对应的资源存在
    let fileUri = 'file://com.example.temptest/data/storage/el2/base/haps/entry/files/test.jpg';
    assetChangeRequest.addResource(photoAccessHelper.ResourceType.IMAGE_RESOURCE, fileUri);
    await phAccessHelper.applyChanges(assetChangeRequest);
    console.info('addResourceByFileUri successfully');
  } catch (err) {
    console.error(`addResourceByFileUriDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### addResource<sup>11+</sup>

addResource(type: ResourceType, data: ArrayBuffer): void

通过ArrayBuffer数据添加资源。

**注意**：对于同一个资产变更请求，不支持在成功添加资源后，重复调用该接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型    | 必填 | 说明                       |
| ------- | ------- | ---- | -------------------------- |
| type | [ResourceType](#resourcetype11) | 是   | 待添加资源的类型。 |
| data | ArrayBuffer | 是   | 待添加资源的数据。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if parameter is invalid.   |
| 14000011 |  System inner fail.         |
| 14000016 |  Operation Not Support.     |

**示例：**

```ts
async function example() {
  console.info('addResourceByArrayBufferDemo');
  try {
    let photoType: photoAccessHelper.PhotoType = photoAccessHelper.PhotoType.IMAGE;
    let extension: string = 'jpg';
    let assetChangeRequest: photoAccessHelper.MediaAssetChangeRequest = photoAccessHelper.MediaAssetChangeRequest.createAssetRequest(context, photoType, extension);
    let buffer: ArrayBuffer = new ArrayBuffer(2048);
    assetChangeRequest.addResource(photoAccessHelper.ResourceType.IMAGE_RESOURCE, buffer);
    await phAccessHelper.applyChanges(assetChangeRequest);
    console.info('addResourceByArrayBuffer successfully');
  } catch (err) {
    console.error(`addResourceByArrayBufferDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

## MediaAlbumChangeRequest<sup>11+</sup>

相册变更请求。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

### constructor<sup>11+</sup>

constructor(album: Album)

构造函数。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| album | [Album](#album) | 是   | 需要变更的相册。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if parameter is invalid.         |
| 14000011       | System inner fail.          |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('MediaAlbumChangeRequest constructorDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, fetchOptions);
  let album: photoAccessHelper.Album = await fetchResult.getFirstObject();
  let albumChangeRequest: photoAccessHelper.MediaAlbumChangeRequest = new photoAccessHelper.MediaAlbumChangeRequest(album);
}
```

### getAlbum<sup>11+</sup>

getAlbum(): Album

获取当前相册变更请求中的相册。

**注意**：对于创建相册的变更请求，在调用[applyChanges](#applychanges11)提交生效之前，该接口返回null。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| [Album](#album) | 返回当前相册变更请求中的相册。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401      |  if parameter is invalid.   |
| 14000011 |  System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('getAlbumDemo');
  try {
    // 请确保图库内存在用户相册
    let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC);
    let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
    let albumChangeRequest: photoAccessHelper.MediaAlbumChangeRequest = new photoAccessHelper.MediaAlbumChangeRequest(album);
    let changeRequestAlbum: photoAccessHelper.Album = albumChangeRequest.getAlbum();
    console.info('change request album uri: ' + changeRequestAlbum.albumUri);
  } catch (err) {
    console.error(`getAlbumDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### setAlbumName<sup>11+</sup>

setAlbumName(name: string): void

设置相册名称。

相册名的参数规格为：
- 相册名字符串长度为1~255。
- 不允许出现非法字符，包括：<br> . .. \ / : * ? " ' ` < > | { } [ ]
- 英文字符大小写不敏感。
- 相册名不允许重名。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| name | string | 是   | 待设置的相册名称。|

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('setAlbumNameDemo');
  try {
    let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC);
    let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
    let albumChangeRequest: photoAccessHelper.MediaAlbumChangeRequest = new photoAccessHelper.MediaAlbumChangeRequest(album);
    let newAlbumName: string = 'newAlbumName' + new Date().getTime();
    albumChangeRequest.setAlbumName(newAlbumName);
    await phAccessHelper.applyChanges(albumChangeRequest);
    console.info('setAlbumName successfully');
  } catch (err) {
    console.error(`setAlbumNameDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### addAssets<sup>11+</sup>

addAssets(assets: Array&lt;PhotoAsset&gt;): void

向相册中添加资产。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 待添加到相册中的资产数组。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |
| 14000016 |  Operation Not Support.     |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('addAssetsDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    // 请确保图库内存在用户相册和照片
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let asset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC);
    let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
    let albumChangeRequest: photoAccessHelper.MediaAlbumChangeRequest = new photoAccessHelper.MediaAlbumChangeRequest(album);
    albumChangeRequest.addAssets([asset]);
    await phAccessHelper.applyChanges(albumChangeRequest);
    console.info('addAssets successfully');
  } catch (err) {
    console.error(`addAssetsDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### removeAssets<sup>11+</sup>

removeAssets(assets: Array&lt;PhotoAsset&gt;): void

从相册中移除资产。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 待从相册中移除的资产数组。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |
| 14000016 |  Operation Not Support.     |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('removeAssetsDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC);
    let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await album.getAssets(fetchOptions);
    let asset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();

    let albumChangeRequest: photoAccessHelper.MediaAlbumChangeRequest = new photoAccessHelper.MediaAlbumChangeRequest(album);
    albumChangeRequest.removeAssets([asset]);
    await phAccessHelper.applyChanges(albumChangeRequest);
    console.info('removeAssets successfully');
  } catch (err) {
    console.error(`removeAssetsDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

## MediaAssetManager<sup>11+</sup>

### requestImage<sup>11+</sup>

static requestImage(context: Context, asset: PhotoAsset, requestOptions: RequestOptions, dataHandler: MediaAssetDataHandler&lt;image.ImageSource&gt;): Promise&lt;string&gt;

根据不同的策略模式，请求图片资源。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**参数：**

| 参数名            | 类型                                                                                                        | 必填 | 说明                      |
|----------------|-----------------------------------------------------------------------------------------------------------| ---- | ------------------------- |
| context        | [Context](../apis-ability-kit/js-apis-inner-application-context.md)                                                           | 是   | 传入Ability实例的Context。 |
| asset         | [PhotoAsset](#photoasset)                                                                                | 是   | 待请求的的媒体文件对象。 |
| requestOptions | [RequestOptions](#requestoptions11)                                                                        | 是   | 图片请求策略模式配置项。       
| dataHandler    | [MediaAssetDataHandler](#mediaassetdatahandler11)&lt;[image.ImageSource](../apis-image-kit/js-apis-image.md#imagesource)&gt; | 是   | 媒体资源处理器，当所请求的图片资源准备完成时会触发回调。

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201      |  Permission denied         |
| 401      |  if parameter is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import image from '@ohos.multimedia.image'

class MediaHandler implements photoAccessHelper.MediaAssetDataHandler<image.ImageSource> {
    onDataPrepared(data: image.ImageSource) {
        console.info('on image data prepared');
    }
}

async function example() {
  console.info('requestImage');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let requestOptions: photoAccessHelper.RequestOptions = {
    deliveryMode: photoAccessHelper.DeliveryMode.HIGH_QUALITY_MODE,
  }
  const handler = new MediaHandler();

  phAccessHelper.getAssets(fetchOptions, async (err, fetchResult) => {
      console.info('fetchResult success');
      let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
      await photoAccessHelper.MediaAssetManager.requestImage(context, photoAsset, requestOptions, handler);
      console.info('requestImage successfully');
  });
}
```

### requestImageData<sup>11+</sup>

static requestImageData(context: Context, asset: PhotoAsset, requestOptions: RequestOptions, dataHandler: MediaAssetDataHandler&lt;ArrayBuffer&gt;): Promise&lt;string&gt;

根据不同的策略模式，请求图片资源数据。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**参数：**

| 参数名   | 类型                                                                   | 必填 | 说明                      |
| -------- |----------------------------------------------------------------------| ---- | ------------------------- |
| context | [Context](../apis-ability-kit/js-apis-inner-application-context.md)                      | 是   | 传入Ability实例的Context。 |
| asset | [PhotoAsset](#photoasset)                                            | 是   | 待请求的的媒体文件对象。 |
| requestOptions  | [RequestOptions](#requestoptions11)                                  | 是   | 图片请求策略模式配置项。       
| dataHandler  | [MediaAssetDataHandler](#mediaassetdatahandler11)&lt;ArrayBuffer&gt; | 是   | 媒体资源处理器，当所请求的图片资源准备完成时会触发回调。

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201      |  Permission denied         |
| 401      |  if parameter is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
class MediaDataHandler implements photoAccessHelper.MediaAssetDataHandler<ArrayBuffer> {
    onDataPrepared(data: ArrayBuffer) {
        console.info('on image data prepared');
    }
}

async function example() {
  console.info('requestImageData');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let requestOptions: photoAccessHelper.RequestOptions = {
    deliveryMode: photoAccessHelper.DeliveryMode.HIGH_QUALITY_MODE,
  }
  const handler = new MediaDataHandler();

  phAccessHelper.getAssets(fetchOptions, async (err, fetchResult) => {
      console.info('fetchResult success');
      let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
      await photoAccessHelper.MediaAssetManager.requestImageData(context, photoAsset, requestOptions, handler);
      console.info('requestImageData successfully');
  });
}
```

## MediaAssetDataHandler<sup>11+</sup>

媒体资源处理器，应用在onDataPrepared方法中可自定义媒体资源处理逻辑。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

### onDataPrepared<sup>11+</sup>

onDataPrepared(data: T): void

媒体资源就绪通知，当所请求的图片资源准备就绪时系统会回调此方法。
T支持ArrayBuffer与[ImageSource](../apis-image-kit/js-apis-image.md#imagesource)两种数据类型。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型 | 必填 | 说明                                                                            |
|------|---| ---- |-------------------------------------------------------------------------------|
| data | T | 是   | 泛型，支持ArrayBuffer与[ImageSource](../apis-image-kit/js-apis-image.md#imagesource)两种数据类型。 |

**示例**
```ts
import image from '@ohos.multimedia.image'

class MediaHandler implements photoAccessHelper.MediaAssetDataHandler<image.ImageSource> {
  onDataPrepared(data: image.ImageSource) {
    // 自定义对ImageSource的处理逻辑
    console.info('on image data prepared');
  }
}

class MediaDataHandler implements photoAccessHelper.MediaAssetDataHandler<ArrayBuffer> {
  onDataPrepared(data: ArrayBuffer) {
    // 自定义对ArrayBuffer的处理逻辑
    console.info('on image data prepared');
  }
}
```

## MemberType

type MemberType = number | string | boolean

PhotoAsset的成员类型。

成员类型为下表类型中的并集。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 类型 | 说明 |
| ---- | ---- |
| number | 表示值类型为数字，可取任意值。 |
| string | 表示值类型为字符，可取任意值。|
| boolean | 表示值类型为布尔类型。 |

## PhotoType

枚举，媒体文件类型。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称  |  值 |  说明 |
| ----- |  ---- |  ---- |
| IMAGE |  1 |  图片。 |
| VIDEO |  2 |  视频。 |

## AlbumType

枚举，相册类型，表示是用户相册还是系统预置相册。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                  | 值    | 说明                        |
| ------------------- | ---- | ------------------------- |
| USER                | 0    | 用户相册。                     |
| SYSTEM              | 1024 | 系统预置相册。                   |

## AlbumSubtype

枚举，相册子类型，表示具体的相册类型。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                                | 值          | 说明                              |
| --------------------------------- | ---------- | ------------------------------- |
| USER\_GENERIC                     | 1          | 用户相册。                           |
| FAVORITE                          | 1025       | 收藏夹。                            |
| VIDEO                             | 1026       | 视频相册。                           |
| ANY                               | 2147483647 | 任意相册。                           |

## PhotoKeys

枚举，图片和视频文件关键信息。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称          | 值              | 说明                                                       |
| ------------- | ------------------- | ---------------------------------------------------------- |
| URI           | 'uri'                 | 文件uri。                                                   |
| PHOTO_TYPE    | 'media_type'           | 媒体文件类型。                                              |
| DISPLAY_NAME  | 'display_name'        | 显示名字。                                                   |
| SIZE          | 'size'                | 文件大小（单位：字节）。                                                   |
| DATE_ADDED    | 'date_added'          | 添加日期（添加文件时间距1970年1月1日的秒数值）。             |
| DATE_MODIFIED | 'date_modified'       | 修改日期（修改文件时间距1970年1月1日的秒数值，修改文件名不会改变此值，当文件内容发生修改时才会更新）。 |
| DURATION      | 'duration'            | 持续时间（单位：毫秒）。                                    |
| WIDTH         | 'width'               | 图片宽度（单位：像素）。                                    |
| HEIGHT        | 'height'              | 图片高度（单位：像素）。                                      |
| DATE_TAKEN    | 'date_taken'          | 拍摄日期（文件拍照时间距1970年1月1日的秒数值）。                |
| ORIENTATION   | 'orientation'         | 图片文件的方向。                                             |
| FAVORITE      | 'is_favorite'            | 收藏。                                                    |
| TITLE         | 'title'               | 文件标题。                                                   |

## AlbumKeys

枚举，相册关键信息。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称          | 值              | 说明                                                       |
| ------------- | ------------------- | ---------------------------------------------------------- |
| URI           | 'uri'                 | 相册uri。                                                   |
| ALBUM_NAME    | 'album_name'          | 相册名字。                                                   |

## CreateOptions

图片或视频的创建选项。

title参数规格为：
- 不应包含扩展名。
- 文件名字符串长度为1~255。
- 文件名中不允许出现的非法英文字符，包括：<br> . .. \ / : * ? " ' ` < > | { } [ ]

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                   | 类型                | 必填 | 说明                                              |
| ---------------------- | ------------------- | ---- | ------------------------------------------------ |
| title           | string | 否  | 图片或者视频的标题。  |


## FetchOptions

检索条件。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                   | 类型                | 可读 | 可写 | 说明                                              |
| ---------------------- | ------------------- | ---- |---- | ------------------------------------------------ |
| fetchColumns           | Array&lt;string&gt; | 是   | 是   | 检索条件，指定列名查询。<br>对于照片，如果该参数为空，默认查询'uri'、'media_type'和'display_name'，使用[get](#get)接口获取当前对象的其他属性时将会报错。示例：fetchColumns: ['uri', 'title']。<br>对于相册，如果该参数为空，默认查询'uri'和'album_name'。 |
| predicates           | [dataSharePredicates.DataSharePredicates](../apis-arkdata/js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | 是   | 谓词查询，显示过滤条件。 |

## RequestOptions<sup>11+</sup>

请求策略。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                   | 类型                              | 可读 | 可写 | 说明                                              |
| ---------------------- |---------------------------------| ---- |---- | ------------------------------------------------ |
| deliveryMode           | [DeliveryMode](#deliverymode11) | 是   | 是   | 请求资源分发模式，可以指定对于该资源的请求策略，可被配置为快速模式，高质量模式，均衡模式三种策略。 |

## MediaChangeRequest<sup>11+</sup>

媒体变更请求，资产变更请求和相册变更请求的父类型。

**注意**：媒体变更请求需要在调用[applyChanges](#applychanges11)后才会提交生效。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

## ResourceType<sup>11+</sup>

枚举，写入资源的类型。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称  |  值 |  说明 |
| ----- |  ---- |  ---- |
| IMAGE_RESOURCE |  1 |  表示图片资源。 |
| VIDEO_RESOURCE |  2 |  表示视频资源。 |

## ChangeData

监听器回调函数的值。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称    | 类型                        | 可读 | 可写 | 说明                                                         |
| ------- | --------------------------- | ---- | ---- | ------------------------------------------------------------ |
| type    | [NotifyType](#notifytype) | 是   | 否   | ChangeData的通知类型。                                       |
| uris    | Array&lt;string&gt;         | 是   | 否   | 相同[NotifyType](#notifytype)的所有uri，可以是PhotoAsset或Album。 |
| extraUris | Array&lt;string&gt;         | 是   | 否   | 相册中变动文件的uri数组。                                    |

## NotifyType

枚举，通知事件的类型。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                      | 值   | 说明                             |
| ------------------------- | ---- | -------------------------------- |
| NOTIFY_ADD                | 0    | 添加文件集或相册通知的类型。     |
| NOTIFY_UPDATE             | 1    | 文件集或相册的更新通知类型。     |
| NOTIFY_REMOVE             | 2    | 删除文件集或相册的通知类型。     |
| NOTIFY_ALBUM_ADD_ASSET    | 3    | 在相册中添加的文件集的通知类型。 |
| NOTIFY_ALBUM_REMOVE_ASSET | 4    | 在相册中删除的文件集的通知类型。 |

## DefaultChangeUri

枚举，DefaultChangeUri子类型。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称              | 值                      | 说明                                                         |
| ----------------- | ----------------------- | ------------------------------------------------------------ |
| DEFAULT_PHOTO_URI | 'file://media/Photo'      | 默认PhotoAsset的Uri，与forSubUri{true}一起使用，将接收所有PhotoAsset的更改通知。 |
| DEFAULT_ALBUM_URI | 'file://media/PhotoAlbum' | 默认相册的Uri，与forSubUri{true}一起使用，将接收所有相册的更改通知。 |

## PhotoViewMIMETypes

枚举，可选择的媒体文件类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称  |  值 |  说明 |
| ----- |  ---- | ---- |
| IMAGE_TYPE  |  'image/*' | 图片类型。 |
| VIDEO_TYPE |  'video/*' | 视频类型。 |
| IMAGE_VIDEO_TYPE |  '\*/*' | 图片和视频类型。 |

## RecommendationType<sup>11+</sup>

枚举，推荐的照片类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称  |  值 |  说明 |
| ----- |  ---- | ---- |
| QR_OR_BAR_CODE  |  1 | 二维码或条码。 |
| QR_CODE |  2 | 二维码。 |
| BAR_CODE |  3 | 条码。 |
| ID_CARD |  4 | 身份证。 |
| PROFILE_PICTURE |  5 | 头像。 |

## RecommendationOptions<sup>11+</sup>

照片推荐选项(基于照片数据分析结果，依赖设备适配)。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                    | 类型                | 必填 | 说明                          |
| ----------------------- | ------------------- | ---- | -------------------------------- |
| recommendationType | [RecommendationType](#recommendationtype11)   | 否   | 可选择的照片推荐类型，若无此参数，则默认为不推荐照片。 |

## PhotoSelectOptions

图库选择选项。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                    | 类型                | 必填 | 说明                          |
| ----------------------- | ------------------- | ---- | -------------------------------- |
| MIMEType              | [PhotoViewMIMETypes](#photoviewmimetypes)   | 否   | 可选择的媒体文件类型，若无此参数，则默认为图片和视频类型。 |
| maxSelectNumber       | number | 否   | 选择媒体文件数量的最大值(默认值为50，最大值为500)。      |
| isPhotoTakingSupported<sup>11+</sup> | boolean  | 否   | 支持拍照。 |
| isEditSupported<sup>11+</sup>       | boolean | 否   | 支持编辑照片。      |
| isSearchSupported<sup>11+</sup> | boolean  | 否   | 支持搜索。 |
| recommendationOptions<sup>11+</sup>       | [RecommendationOptions](#recommendationoptions11)   | 否   | 支持照片推荐。      |
| preselectedUris<sup>11+</sup> | Array&lt;string&gt;  | 否   | 预选择图片的uri数据。 |

## PhotoSelectResult

返回图库选择后的结果集。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                    | 类型                | 可读 | 可写 | 说明                           |
| ----------------------- | ------------------- | ---- | ---- | ------------------------------ |
| photoUris        | Array&lt;string&gt;    | 是   | 是   | 返回图库选择后的媒体文件的uri数组，此uri数组只能通过临时授权的方式调用[photoAccessHelper.getAssets接口](#getassets)去使用，具体使用方式参见用户文件uri介绍中的[媒体文件uri的使用方式](../../file-management/user-file-uri-intro.md#媒体文件uri的使用方式)。 |
| isOriginalPhoto        | boolean    | 是   | 是   | 返回图库选择后的媒体文件是否为原图。 |


## DeliveryMode<sup>11+</sup>

枚举，资源分发模式。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称  |  值 |  说明 |
| ----- |  ---- |  ---- |
| FAST_MODE |  0 |  快速模式。 |
| HIGH_QUALITY_MODE |  1 |  高质量模式。 |
| BALANCE_MODE |  2 |  均衡模式。 |
