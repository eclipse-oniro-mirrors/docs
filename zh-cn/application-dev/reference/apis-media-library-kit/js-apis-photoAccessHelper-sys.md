# @ohos.file.photoAccessHelper (相册管理模块)(系统接口)

该模块提供相册管理模块能力，包括创建相册以及访问、修改相册中的媒体数据信息等。

> **说明：**
>
> - 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> - 当前页面仅包含本模块的系统接口，其他公开接口参见[@ohos.file.photoAccessHelper (相册管理模块)](js-apis-photoAccessHelper.md)。

## 导入模块

```ts
import photoAccessHelper from '@ohos.file.photoAccessHelper';
```

## PhotoAccessHelper

### createAsset

createAsset(displayName: string, callback: AsyncCallback&lt;PhotoAsset&gt;): void

指定待创建的图片或者视频的文件名，创建图片或视频资源，使用callback方式返回结果。

待创建的文件名参数规格为：
- 应包含有效文件主名和图片或视频扩展名。
- 文件名字符串长度为1~255。
- 文件主名中不允许出现的非法英文字符，包括：<br> . .. \ / : * ? " ' ` < > | { } [ ]

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| displayName  | string        | 是   | 创建的图片或者视频文件名。              |
| callback |  AsyncCallback&lt;[PhotoAsset](#photoasset)&gt; | 是   | callback返回创建的图片和视频结果。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   |  Called by non-system application.         |
| 401      |  if type displayName is not string.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000001      | Invalid display name.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('createAssetDemo');
  let testFileName: string = 'testFile' + Date.now() + '.jpg';
  phAccessHelper.createAsset(testFileName, (err, photoAsset) => {
    if (photoAsset !== undefined) {
      console.info('createAsset file displayName' + photoAsset.displayName);
      console.info('createAsset successfully');
    } else {
      console.error(`createAsset failed, error: ${err.code}, ${err.message}`);
    }
  });
}
```

### createAsset

createAsset(displayName: string): Promise&lt;PhotoAsset&gt;

指定待创建的图片或者视频的文件名，创建图片或视频资源，使用Promise方式返回结果。

待创建的文件名参数规格为：
- 应包含有效文件主名和图片或视频扩展名。
- 文件名字符串长度为1~255。
- 文件主名中不允许出现的非法英文字符，包括：<br> . .. \ / : * ? " ' ` < > | { } [ ]

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| displayName  | string        | 是   | 创建的图片或者视频文件名。              |

**返回值：**

| 类型                        | 说明           |
| --------------------------- | -------------- |
| Promise&lt;[PhotoAsset](#photoasset)&gt; | Promise对象，返回创建的图片和视频结果。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   |  Called by non-system application.         |
| 401      |  if type displayName or albumUri is not string.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000001      | Invalid display name.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('createAssetDemo');
  try {
    let testFileName: string = 'testFile' + Date.now() + '.jpg';
    let photoAsset: photoAccessHelper.PhotoAsset = await phAccessHelper.createAsset(testFileName);
    console.info('createAsset file displayName' + photoAsset.displayName);
    console.info('createAsset successfully');
  } catch (err) {
    console.error(`createAsset failed, error: ${err.code}, ${err.message}`);
  }
}
```

### createAsset

createAsset(displayName: string, options: PhotoCreateOptions, callback: AsyncCallback&lt;PhotoAsset&gt;): void

指定待创建的图片或者视频的文件名和创建选项，创建图片或视频资源，使用callback方式返回结果。

待创建的文件名参数规格为：
- 应包含有效文件主名和图片或视频扩展名。
- 文件名字符串长度为1~255。
- 文件主名中不允许出现的非法英文字符，包括：<br> . .. \ / : * ? " ' ` < > | { } [ ]

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| displayName  | string        | 是   | 创建的图片或者视频文件名。              |
| options  | [PhotoCreateOptions](#photocreateoptions)        | 是   | 图片或视频的创建选项。              |
| callback |  AsyncCallback&lt;[PhotoAsset](#photoasset)&gt; | 是   | callback返回创建的图片和视频结果。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   |  Called by non-system application.         |
| 401      |  if type displayName is not string.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000001      | Invalid display name.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('createAssetDemo');
  let testFileName: string = 'testFile' + Date.now() + '.jpg';
  let createOption: photoAccessHelper.PhotoCreateOptions = {
    subtype: photoAccessHelper.PhotoSubtype.DEFAULT
  }
  phAccessHelper.createAsset(testFileName, createOption, (err, photoAsset) => {
    if (photoAsset !== undefined) {
      console.info('createAsset file displayName' + photoAsset.displayName);
      console.info('createAsset successfully');
    } else {
      console.error(`createAsset failed, error: ${err.code}, ${err.message}`);
    }
  });
}
```

### createAsset

createAsset(displayName: string, options: PhotoCreateOptions): Promise&lt;PhotoAsset&gt;

指定待创建的图片或者视频的文件名和创建选项，创建图片或视频资源，使用Promise方式返回结果。

待创建的文件名参数规格为：
- 应包含有效文件主名和图片或视频扩展名。
- 文件名字符串长度为1~255。
- 文件主名中不允许出现的非法英文字符，包括：<br> . .. \ / : * ? " ' ` < > | { } [ ]

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| displayName  | string        | 是   | 创建的图片或者视频文件名。              |
| options  |  [PhotoCreateOptions](#photocreateoptions)       | 是   | 图片或视频的创建选项。              |

**返回值：**

| 类型                        | 说明           |
| --------------------------- | -------------- |
| Promise&lt;[PhotoAsset](#photoasset)&gt; | Promise对象，返回创建的图片和视频结果。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   |  Called by non-system application.         |
| 401      |  if type displayName is not string.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000001      | Invalid display name.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('createAssetDemo');
  try {
    let testFileName:string = 'testFile' + Date.now() + '.jpg';
    let createOption: photoAccessHelper.PhotoCreateOptions = {
      subtype: photoAccessHelper.PhotoSubtype.DEFAULT
    }
    let photoAsset: photoAccessHelper.PhotoAsset = await phAccessHelper.createAsset(testFileName, createOption);
    console.info('createAsset file displayName' + photoAsset.displayName);
    console.info('createAsset successfully');
  } catch (err) {
    console.error(`createAsset failed, error: ${err.code}, ${err.message}`);
  }
}
```

### createAlbum<sup>(deprecated)</sup>

createAlbum(name: string, callback: AsyncCallback&lt;Album&gt;): void

创建相册，使用callback方式返回结果。

待创建的相册名参数规格为：
- 相册名字符串长度为1~255。
- 不允许出现的非法英文字符，包括：<br> . .. \ / : * ? " ' ` < > | { } [ ]
- 英文字符大小写不敏感。
- 相册名不允许重名。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAlbumChangeRequest.createAlbumRequest](#createalbumrequest11)替代。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| name  | string         | 是   | 待创建相册的相册名。              |
| callback |  AsyncCallback&lt;[Album](#album)&gt; | 是   | callback返回创建的相册实例。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   |  Called by non-system application.         |
| 401      |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900015       |  File exists.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('createAlbumDemo');
  let albumName: string = 'newAlbumName' + new Date().getTime();
  phAccessHelper.createAlbum(albumName, (err, album) => {
    if (err) {
      console.error(`createAlbumCallback failed with err: ${err.code}, ${err.message}`);
      return;
    }
    console.info('createAlbumCallback successfully, album: ' + album.albumName + ' album uri: ' + album.albumUri);
  });
}
```

### createAlbum<sup>(deprecated)</sup>

createAlbum(name: string): Promise&lt;Album&gt;

创建相册，使用Promise方式返回结果。

待创建的相册名参数规格为：
- 相册名字符串长度为1~255。
- 不允许出现的非法英文字符，包括：<br> . .. \ / : * ? " ' ` < > | { } [ ]
- 英文字符大小写不敏感。
- 相册名不允许重名。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAlbumChangeRequest.createAlbumRequest](#createalbumrequest11)替代。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| name  | string         | 是   | 待创建相册的相册名。              |

**返回值：**

| 类型                        | 说明           |
| --------------------------- | -------------- |
| Promise&lt;[Album](#album)&gt; | Promise对象，返回创建的相册实例。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   |  Called by non-system application.         |
| 401      |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900015       |  File exists.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  console.info('createAlbumDemo');
  let albumName: string = 'newAlbumName' + new Date().getTime();
  phAccessHelper.createAlbum(albumName).then((album) => {
    console.info('createAlbumPromise successfully, album: ' + album.albumName + ' album uri: ' + album.albumUri);
  }).catch((err: BusinessError) => {
    console.error(`createAlbumPromise failed with err: ${err.code}, ${err.message}`);
  });
}
```

### deleteAlbums<sup>(deprecated)</sup>

deleteAlbums(albums: Array&lt;Album&gt;, callback: AsyncCallback&lt;void&gt;): void

删除相册，使用callback方式返回结果。

删除相册前需先确保相册存在，只能删除用户相册。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAlbumChangeRequest.deleteAlbums](#deletealbums11)替代。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| albums  | Array&lt;[Album](#album)&gt;         | 是   | 待删除相册的数组。              |
| callback |  AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   |  Called by non-system application.         |
| 401      |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  // 示例代码为删除相册名为newAlbumName的相册。
  console.info('deleteAlbumsDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  predicates.equalTo('album_name', 'newAlbumName');
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, fetchOptions);
  let album: photoAccessHelper.Album = await fetchResult.getFirstObject();
  phAccessHelper.deleteAlbums([album], (err) => {
    if (err) {
      console.error(`deletePhotoAlbumsCallback failed with err: ${err.code}, ${err.message}`);
      return;
    }
    console.info('deletePhotoAlbumsCallback successfully');
  });
  fetchResult.close();
}
```

### deleteAlbums<sup>(deprecated)</sup>

deleteAlbums(albums: Array&lt;Album&gt;): Promise&lt;void&gt;

删除相册，使用Promise方式返回结果。

删除相册前需先确保相册存在，只能删除用户相册。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAlbumChangeRequest.deleteAlbums](#deletealbums11)替代。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| albums  |  Array&lt;[Album](#album)&gt;          | 是   | 待删除相册的数组。              |

**返回值：**

| 类型                        | 说明           |
| --------------------------- | -------------- |
| Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   |  Called by non-system application.         |
| 401      |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  // 示例代码为删除相册名为newAlbumName的相册。
  console.info('deleteAlbumsDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  predicates.equalTo('album_name', 'newAlbumName');
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, fetchOptions);
  let album: photoAccessHelper.Album = await fetchResult.getFirstObject();
  phAccessHelper.deleteAlbums([album]).then(() => {
    console.info('deletePhotoAlbumsPromise successfully');
    }).catch((err: BusinessError) => {
      console.error(`deletePhotoAlbumsPromise failed with err: ${err.code}, ${err.message}`);
  });
  fetchResult.close();
}
```

### getHiddenAlbums<sup>11+</sup>

getHiddenAlbums(mode: HiddenPhotosDisplayMode, options: FetchOptions, callback: AsyncCallback&lt;FetchResult&lt;Album&gt;&gt;): void

根据隐藏文件显示模式和检索选项获取系统中的隐藏相册，使用callback方式返回结果。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO 和 ohos.permission.MANAGE_PRIVATE_PHOTOS

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| mode  | [HiddenPhotosDisplayMode](#hiddenphotosdisplaymode11)         | 是   | 隐藏文件显示模式  |
| options  | [FetchOptions](js-apis-photoAccessHelper.md#fetchoptions)         | 是   |  检索选项  |
| callback |  AsyncCallback&lt;[FetchResult](js-apis-photoAccessHelper.md#fetchresult)&lt;[Album](#album)&gt;&gt; | 是   | callback返回获取相册的结果集。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201      |  Permission denied.         |
| 202      |  Called by non-system application.         |
| 401      |  if parameter is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

// 获取系统中包含隐藏文件且相册名为'newAlbumName'的相册
async function getHiddenAlbumsView() {
  console.info('getHiddenAlbumsViewDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  predicates.equalTo('album_name', 'newAlbumName');
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  phAccessHelper.getHiddenAlbums(photoAccessHelper.HiddenPhotosDisplayMode.ALBUMS_MODE, fetchOptions,
    async (err, fetchResult) => {
      if (fetchResult === undefined) {
        console.error('getHiddenAlbumsViewCallback fetchResult is undefined');
        return;
      }
      let album = await fetchResult.getFirstObject();
      console.info('getHiddenAlbumsViewCallback successfully, album name: ' + album.albumName);
      fetchResult.close();
  });
}
```

### getHiddenAlbums<sup>11+</sup>

getHiddenAlbums(mode: HiddenPhotosDisplayMode, callback: AsyncCallback&lt;FetchResult&lt;Album&gt;&gt;): void

根据隐藏文件显示模式获取系统中的隐藏相册，使用callback方式返回结果

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO 和 ohos.permission.MANAGE_PRIVATE_PHOTOS

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| mode  | [HiddenPhotosDisplayMode](#hiddenphotosdisplaymode11)         | 是   | 隐藏文件显示模式  |
| callback |  AsyncCallback&lt;[FetchResult](js-apis-photoAccessHelper.md#fetchresult)&lt;[Album](#album)&gt;&gt; | 是   | callback返回获取相册的结果集。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201      |  Permission denied.         |
| 202      |  Called by non-system application.         |
| 401      |  if parameter is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

// 获取系统预置的隐藏相册
async function getSysHiddenAlbum() {
  console.info('getSysHiddenAlbumDemo');
  phAccessHelper.getHiddenAlbums(photoAccessHelper.HiddenPhotosDisplayMode.ASSETS_MODE, async (err, fetchResult) => {
    if (fetchResult === undefined) {
      console.error('getSysHiddenAlbumCallback fetchResult is undefined');
      return;
    }
    let hiddenAlbum: photoAccessHelper.Album = await fetchResult.getFirstObject();
    console.info('getSysHiddenAlbumCallback successfully, albumUri: ' + hiddenAlbum.albumUri);
    fetchResult.close();
  });
}

// 获取隐藏相册-相册视图，即系统中包含隐藏文件的相册（不包含系统预置的隐藏相册本身和回收站相册）
async function getHiddenAlbumsView() {
  console.info('getHiddenAlbumsViewDemo');
  phAccessHelper.getHiddenAlbums(photoAccessHelper.HiddenPhotosDisplayMode.ALBUMS_MODE, async (err, fetchResult) => {
    if (fetchResult === undefined) {
      console.error('getHiddenAlbumsViewCallback fetchResult is undefined');
      return;
    }
    let albums: Array<photoAccessHelper.Album> = await fetchResult.getAllObjects();
    console.info('getHiddenAlbumsViewCallback successfully, albums size: ' + albums.length);

    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    for (let i = 0; i < albums.length; i++) {
      // 获取相册中的隐藏文件
      albums[i].getAssets(fetchOption, (err, assetFetchResult) => {
        console.info('album get hidden assets successfully, getCount: ' + assetFetchResult.getCount());
      });
    }
    fetchResult.close();
  });
}
```

### getHiddenAlbums<sup>11+</sup>

getHiddenAlbums(mode: HiddenPhotosDisplayMode, options?: FetchOptions): Promise&lt;FetchResult&lt;Album&gt;&gt;

根据隐藏文件显示模式和检索选项获取系统中的隐藏相册，使用Promise方式返回结果。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO 和 ohos.permission.MANAGE_PRIVATE_PHOTOS

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| mode  | [HiddenPhotosDisplayMode](#hiddenphotosdisplaymode11)         | 是   | 隐藏文件显示模式  |
| options  | [FetchOptions](js-apis-photoAccessHelper.md#fetchoptions)         | 否   |  检索选项，不填时默认根据隐藏文件显示模式检索。      |

**返回值：**

| 类型                        | 说明           |
| --------------------------- | -------------- |
| Promise&lt;[FetchResult](js-apis-photoAccessHelper.md#fetchresult)&lt;[Album](#album)&gt;&gt; | Promise对象，返回获取相册的结果集。

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

// 获取系统预置的隐藏相册
async function getSysHiddenAlbum() {
  console.info('getSysHiddenAlbumDemo');
  phAccessHelper.getHiddenAlbums(photoAccessHelper.HiddenPhotosDisplayMode.ASSETS_MODE)
    .then( async (fetchResult) => {
      if (fetchResult === undefined) {
        console.error('getSysHiddenAlbumPromise fetchResult is undefined');
        return;
      }
      let hiddenAlbum: photoAccessHelper.Album = await fetchResult.getFirstObject();
      console.info('getAlbumsPromise successfully, albumUri: ' + hiddenAlbum.albumUri);
      fetchResult.close();
    }).catch((err: BusinessError) => {
      console.error(`getSysHiddenAlbumPromise failed with err: ${err.code}, ${err.message}`);
    });
}

// 获取隐藏相册-相册视图，即系统中包含隐藏文件的相册（不包含系统预置的隐藏相册本身和回收站相册）
async function getHiddenAlbumsView() {
  console.info('getHiddenAlbumsViewDemo');
  phAccessHelper.getHiddenAlbums(photoAccessHelper.HiddenPhotosDisplayMode.ALBUMS_MODE).then( async (fetchResult) => {
    if (fetchResult === undefined) {
      console.error('getHiddenAlbumsViewPromise fetchResult is undefined');
      return;
    }
    let albums: Array<photoAccessHelper.Album> = await fetchResult.getAllObjects();
    console.info('getHiddenAlbumsViewPromise successfully, albums size: ' + albums.length);

    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    for (let i = 0; i < albums.length; i++) {
      // 获取相册中的隐藏文件
      albums[i].getAssets(fetchOption).then((assetFetchResult) => {
        console.info('album get hidden assets successfully, getCount: ' + assetFetchResult.getCount());
      }).catch((err: BusinessError) => {
        console.error(`album get hidden assets failed with error: ${err.code}, ${err.message}`);
      });
    }
    fetchResult.close();
  }).catch((err: BusinessError) => {
    console.error(`getHiddenAlbumsViewPromise failed with err: ${err.code}, ${err.message}`);
  });
}
```

### deleteAssets<sup>(deprecated)</sup>

deleteAssets(uriList: Array&lt;string&gt;, callback: AsyncCallback&lt;void&gt;): void

删除媒体文件，删除的文件进入到回收站，使用callback方式返回结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAssetChangeRequest.deleteAssets](js-apis-photoAccessHelper.md#deleteassets11)替代。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| uriList | Array&lt;string&gt; | 是   | 待删除的媒体文件uri数组。 |
| callback | AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   |  Called by non-system application.         |
| 401      |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000002       | Invalid uri.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('deleteAssetDemo');
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
    phAccessHelper.deleteAssets([asset.uri], (err) => {
      if (err === undefined) {
        console.info('deleteAssets successfully');
      } else {
        console.error(`deleteAssets failed with error: ${err.code}, ${err.message}`);
      }
    });
  } catch (err) {
    console.error(`fetch failed, error: ${err.code}, ${err.message}`);
  }
}
```

### deleteAssets<sup>(deprecated)</sup>

deleteAssets(uriList: Array&lt;string&gt;): Promise&lt;void&gt;

删除媒体文件，删除的文件进入到回收站，使用Promise方式返回结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAssetChangeRequest.deleteAssets](js-apis-photoAccessHelper.md#deleteassets11)替代。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| uriList | Array&lt;string&gt; | 是   | 待删除的媒体文件uri数组。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;void&gt;| Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   |  Called by non-system application.         |
| 401      |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000002       | Invalid uri.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('deleteDemo');
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
    await phAccessHelper.deleteAssets([asset.uri]);
    console.info('deleteAssets successfully');
  } catch (err) {
    console.error(`deleteAssets failed with error: ${err.code}, ${err.message}`);
  }
}
```

### getPhotoIndex

getPhotoIndex(photoUri: string, albumUri: string, options: FetchOptions, callback: AsyncCallback&lt;number&gt;): void

获取相册中图片或视频的位置，使用callback方式返回结果。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| photoUri | string | 是   | 所查询的图库资源的uri。 |
| albumUri | string | 是   | 相册uri，可以为空字符串，为空字符串时默认查询全部图库资源。   |
| options  | [FetchOptions](js-apis-photoAccessHelper.md#fetchoptions)       | 是   |  检索选项，predicates中必须设置一种检索排序方式，不设置或多设置均会导致接口调用异常。      |
| callback | AsyncCallback&lt;number&gt;| 是   | callback返回相册中资源的索引。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202     |  Called by non-system application.         |
| 401      |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('getPhotoIndexDemo');
    let predicatesForGetAsset: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOp: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicatesForGetAsset
    };
    // Obtain the uri of the album
    let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.FAVORITE, fetchOp);
    let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    predicates.orderByAsc(photoAccessHelper.PhotoKeys.DATE_MODIFIED);
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [photoAccessHelper.PhotoKeys.DATE_MODIFIED],
      predicates: predicates
    };
    let photoFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await album.getAssets(fetchOptions);
    let expectIndex = 1;
    // Obtain the uri of the second file
    let photoAsset: photoAccessHelper.PhotoAsset = await photoFetchResult.getObjectByPosition(expectIndex);

    phAccessHelper.getPhotoIndex(photoAsset.uri, album.albumUri, fetchOptions, (err, index) => {
      if (err === undefined) {
        console.info(`getPhotoIndex successfully and index is : ${index}`);
      } else {
        console.error(`getPhotoIndex failed; error: ${err.code}, ${err.message}`);
      }
    });
  } catch (error) {
    console.error(`getPhotoIndex failed; error: ${error.code}, ${error.message}`);
  }
}
```

### getPhotoIndex

getPhotoIndex(photoUri: string, albumUri: string, options: FetchOptions): Promise&lt;number&gt;

获取相册中图片或视频的位置，使用Promise方式返回结果。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| photoUri | string | 是   | 所查询的图库资源的uri。 |
| albumUri | string | 是   | 相册uri，可以为空字符串，为空字符串时默认查询全部图库资源。   |
| options  | [FetchOptions](js-apis-photoAccessHelper.md#fetchoptions)       | 是   |  检索选项，predicates中必须设置一种检索排序方式，不设置或多设置均会导致接口调用异常。      |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;number&gt;| 返回相册中资源的索引。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202     |  Called by non-system application.         |
| 401      |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  try {
    console.info('getPhotoIndexDemo');
    let predicatesForGetAsset: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOp: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicatesForGetAsset
    };
    // Obtain the uri of the album
    let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.FAVORITE, fetchOp);
    let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    predicates.orderByAsc(photoAccessHelper.PhotoKeys.DATE_MODIFIED);
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [photoAccessHelper.PhotoKeys.DATE_MODIFIED],
      predicates: predicates
    };
    let photoFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await album.getAssets(fetchOptions);
    let expectIndex = 1;
    // Obtain the uri of the second file
    let photoAsset: photoAccessHelper.PhotoAsset = await photoFetchResult.getObjectByPosition(expectIndex);
    phAccessHelper.getPhotoIndex(photoAsset.uri, album.albumUri, fetchOptions).then((index) => {
      console.info(`getPhotoIndex successfully and index is : ${index}`);
    }).catch((err: BusinessError) => {
      console.error(`getPhotoIndex failed; error: ${err.code}, ${err.message}`);
    });
  } catch (error) {
    console.error(`getPhotoIndex failed; error: ${error.code}, ${error.message}`);
  }
}
```

### saveFormInfo<sup>11+</sup>

saveFormInfo(info:FormInfo, callback: AsyncCallback&lt;void&gt;):void

将图库卡片相关信息保存到数据库中，使用callback方式返回结果。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| info  | [FormInfo](#forminfo11)        | 是   | 图库卡片信息，包括图库卡片的id和卡片绑定的图片的uri。              |
| callback |  AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission verification failed, usually the result returned by VerifyAccessToken.         |
| 202   | Permission verification failed, application which is not a system application uses system API.         |
| 401   | if the argument is invalid.         |
| 14000011       | System inner fail.         |


**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  console.info('saveFormInfoDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
  let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();

  let info: photoAccessHelper.FormInfo = {
    //formId是一个由纯数字组成的字符串，uri为图库中存在的图片的uri信息，图库中无图片创建卡片时uri需为空字符串
    formId : "20230116123",
    uri: photoAsset.uri,
  }

  phAccessHelper.saveFormInfo(info, async (err: BusinessError) => {
    if (err == undefined) {
      console.info('saveFormInfo success');
    } else {
      console.error(`saveFormInfo fail with error: ${err.code}, ${err.message}`);
    }
  });
}
```

### saveFormInfo<sup>11+</sup>

saveFormInfo(info:FormInfo):Promise&lt;void&gt;

将图库卡片相关信息保存到数据库中，使用Promise方式返回结果。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| info  | [FormInfo](#forminfo11)        | 是   | 图库卡片信息，包括图库卡片的id和卡片绑定的图片的uri。              |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;void&gt;| Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission verification failed, usually the result returned by VerifyAccessToken.         |
| 202   | Permission verification failed, application which is not a system application uses system API.         |
| 401   | if the argument is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  console.info('saveFormInfoDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
  let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();

  let info: photoAccessHelper.FormInfo = {
    //formId是一个由纯数字组成的字符串，uri为图库中存在的图片的uri信息，图库中无图片创建卡片时uri需为空字符串
    formId: "20230116123",
    uri: photoAsset.uri,
  }

  phAccessHelper.saveFormInfo(info).then(() => {
    console.info('saveFormInfo successfully');
  }).catch((err: BusinessError) => {
    console.error(`saveFormInfo failed with error: ${err.code}, ${err.message}`);
  });
}
```

### removeFormInfo<sup>11+</sup>

removeFormInfo(info:FormInfo, callback: AsyncCallback&lt;void&gt;):void

从数据库中删除图库卡片信息，使用callback方式返回结果。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| info  | [FormInfo](#forminfo11)        | 是   |  图库卡片信息，包括图库卡片的id和卡片绑定的图片的uri。              |
| callback |  AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission verification failed, usually the result returned by VerifyAccessToken.         |
| 202   | Permission verification failed, application which is not a system application uses system API.         |
| 401   | if the argument is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  console.info('removeFormInfoDemo');
  let info: photoAccessHelper.FormInfo = {
    //formId是一个由纯数字组成的字符串，移除卡片的时候uri填空即可
    formId: "20230116123",
    uri: "",
  }

  phAccessHelper.removeFormInfo(info, async (err: BusinessError) => {
    if (err == undefined) {
      console.info('removeFormInfo success');
    } else {
      console.error(`removeFormInfo fail with error: ${err.code}, ${err.message}`);
    }
  });
}
```

### removeFormInfo<sup>11+</sup>

removeFormInfo(info:FormInfo):Promise&lt;void&gt;

从数据库中删除图库卡片信息，使用Promise方式返回结果。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                     | 必填 | 说明                      |
| -------- | ------------------------ | ---- | ------------------------- |
| info  | [FormInfo](#forminfo11)        | 是   |  图库卡片信息，包括图库卡片的id和卡片绑定的图片的uri。              |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;void&gt;| Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission verification failed, usually the result returned by VerifyAccessToken.         |
| 202   | Permission verification failed, application which is not a system application uses system API.         |
| 401   | if the argument is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  console.info('removeFormInfoDemo');
  let info: photoAccessHelper.FormInfo = {
    //formId是一个由纯数字组成的字符串，移除卡片的时候uri填空即可
    formId: "20230116123",
    uri: "",
  }

  phAccessHelper.removeFormInfo(info).then(() => {
    console.info('removeFormInfo successfully');
  }).catch((err: BusinessError) => {
    console.error(`removeFormInfo failed with error: ${err.code}, ${err.message}`);
  });
}
```

## PhotoAsset

提供封装文件属性的方法。

### open<sup>(deprecated)</sup>

open(mode: string, callback: AsyncCallback&lt;number&gt;): void

打开当前文件，使用callback方式返回异步结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。出于安全考量，不再提供获取正式媒体文件句柄的接口。

**注意**：当前此（写）操作是互斥的操作，返回的文件描述符在使用完毕后需要调用close进行释放。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO 或 ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名      | 类型                          | 必填   | 说明                                  |
| -------- | --------------------------- | ---- | ----------------------------------- |
| mode     | string                      | 是    | 打开文件方式，分别为：'r'（只读）, 'w'（只写）, 'rw'（读写）。 |
| callback | AsyncCallback&lt;number&gt; | 是    | callback返回文件描述符。                            |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202     |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('Open demo');
  let testFileName: string = 'testFile' + Date.now() + '.jpg';
  let photoAsset: photoAccessHelper.PhotoAsset = await phAccessHelper.createAsset(testFileName);
  photoAsset.open('rw', (err, fd) => {
    if (fd !== undefined) {
      console.info('File fd' + fd);
      photoAsset.close(fd);
    } else {
      console.error(`Open file err: ${err.code}, ${err.message}`);
    }
  });
}
```

### open<sup>(deprecated)</sup>

open(mode: string): Promise&lt;number&gt;

打开当前文件，使用promise方式返回异步结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。出于安全考量，不再提供获取正式媒体文件句柄的接口。

**注意**：当前此（写）操作是互斥的操作，返回的文件描述符在使用完毕后需要调用close进行释放。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO 或 ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型     | 必填   | 说明                                  |
| ---- | ------ | ---- | ----------------------------------- |
| mode | string | 是    | 打开文件方式，分别为：'r'（只读）, 'w'（只写）, 'rw'（读写）。 |

**返回值：**

| 类型                    | 说明            |
| --------------------- | ------------- |
| Promise&lt;number&gt; | Promise对象，返回文件描述符。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202     |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('Open demo');
  try {
    let testFileName: string = 'testFile' + Date.now() + '.jpg';
    let photoAsset: photoAccessHelper.PhotoAsset = await phAccessHelper.createAsset(testFileName);
    let fd: number = await photoAsset.open('rw');
    if (fd !== undefined) {
      console.info('File fd' + fd);
      photoAsset.close(fd);
    } else {
      console.error('Open file fail');
    }
  } catch (err) {
    console.error(`Open demo err: ${err.code}, ${err.message}`);
  }
}
```

### setFavorite<sup>(deprecated)</sup>

setFavorite(favoriteState: boolean, callback: AsyncCallback&lt;void&gt;): void

将文件设置为收藏文件，使用callback方式返回异步结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAssetChangeRequest.setFavorite](#setfavorite11)替代。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型                        | 必填   | 说明                                 |
| ---------- | ------------------------- | ---- | ---------------------------------- |
| favoriteState | boolean                   | 是    | 是否设置为收藏文件， true：设置为收藏文件，false：取消收藏。 |
| callback   | AsyncCallback&lt;void&gt; | 是    | callback返回void。                              |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('setFavoriteDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let asset = await fetchResult.getFirstObject();
  asset.setFavorite(true, (err) => {
    if (err === undefined) {
      console.info('favorite successfully');
    } else {
      console.error(`favorite failed with error: ${err.code}, ${err.message}`);
    }
  });
}
```

### setFavorite<sup>(deprecated)</sup>

setFavorite(favoriteState: boolean): Promise&lt;void&gt;

将文件设置为收藏文件，使用promise方式返回异步结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAssetChangeRequest.setFavorite](#setfavorite11)替代。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| favoriteState | boolean | 是    | 是否设置为收藏文件， true：设置为收藏文件，false：取消收藏。 |

**返回值：**

| 类型                  | 说明         |
| ------------------- | ---------- |
| Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  console.info('setFavoriteDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let asset = await fetchResult.getFirstObject();
  asset.setFavorite(true).then(() => {
    console.info('setFavorite successfully');
  }).catch((err: BusinessError) => {
    console.error(`setFavorite failed with error: ${err.code}, ${err.message}`);
  });
}
```

### setHidden<sup>(deprecated)</sup>

setHidden(hiddenState: boolean, callback: AsyncCallback&lt;void&gt;): void

将文件设置为隐私文件，使用callback方式返回异步结果。

隐私文件存在隐私相册中，用户通过隐私相册去获取隐私文件后可以通过设置hiddenState为false来从隐私相册中移除。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAssetChangeRequest.setHidden](#sethidden11)替代。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型                        | 必填   | 说明                                 |
| ---------- | ------------------------- | ---- | ---------------------------------- |
| hiddenState | boolean                   | 是    | 是否设置为隐藏文件，true:将文件资产放入隐藏相册;false:从隐藏相册中恢复。 |
| callback   | AsyncCallback&lt;void&gt; | 是    | callback返回void。                              |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('setHiddenDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let asset = await fetchResult.getFirstObject();
  asset.setHidden(true, (err) => {
    if (err === undefined) {
      console.info('setHidden successfully');
    } else {
      console.error(`setHidden failed with error: ${err.code}, ${err.message}`);
    }
  });
}
```

### setHidden<sup>(deprecated)</sup>

setHidden(hiddenState: boolean): Promise&lt;void&gt;

将文件设置为隐私文件，使用promise方式返回异步结果。

隐私文件存在隐私相册中，用户通过隐私相册去获取隐私文件后可以通过设置hiddenState为false来从隐私相册中移除。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAssetChangeRequest.setHidden](#sethidden11)替代。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| hiddenState | boolean | 是    | 是否设置为隐藏文件，true:将文件资产放入隐藏相册;false:从隐藏相册中恢复。 |

**返回值：**

| 类型                  | 说明         |
| ------------------- | ---------- |
| Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  // 示例代码为将文件从隐藏相册中恢复，需要先在隐藏相册预置资源
  console.info('setHiddenDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let albumList: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.HIDDEN);
  let album = await albumList.getFirstObject();
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await album.getAssets(fetchOption);
  let asset = await fetchResult.getFirstObject();
  asset.setHidden(false).then(() => {
    console.info('setHidden successfully');
  }).catch((err: BusinessError) => {
    console.error(`setHidden failed with error: ${err.code}, ${err.message}`);
  });
}
```

### getExif

getExif(): Promise&lt;string&gt;

返回jpg格式图片Exif标签组成的json格式的字符串，该方法使用Promise方式返回结果。

此接口中获取的Exif标签信息是由[image](../apis-image-kit/js-apis-image.md)模块提供。Exif标签详细信息请参考[image.PropertyKey](../apis-image-kit/js-apis-image.md#propertykey7)。

**注意**：此接口返回的是Exif标签组成的json格式的字符串，完整Exif信息由all_exif与[PhotoKeys.USER_COMMENT](#photokeys)组成，fetchColumns需要传入这两个字段。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;string&gt; | 返回Exif标签组成的json格式的字符串。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('getExifDemo');
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [ 'all_exif',  photoAccessHelper.PhotoKeys.USER_COMMENT],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    let exifMessage = await photoAsset.getExif();
    let userCommentKey = 'UserComment';
    let userComment = JSON.stringify(JSON.parse(exifMessage), [userCommentKey]);
    console.info('getExifDemo userComment: ' + JSON.stringify(userComment));
    fetchResult.close();
  } catch (err) {
    console.error(`getExifDemoCallback failed with error: ${err.code}, ${err.message}`);
  }
}
```

### getExif

getExif(callback: AsyncCallback&lt;string&gt;): void

返回jpg格式图片Exif标签组成的json格式的字符串，使用callback方式返回异步结果。

此接口中获取的Exif标签信息是由[image](../apis-image-kit/js-apis-image.md)模块提供。Exif标签详细信息请参考[image.PropertyKey](../apis-image-kit/js-apis-image.md#propertykey7)。

**注意**：此接口返回的是Exif标签组成的json格式的字符串，完整Exif信息由all_exif与[PhotoKeys.USER_COMMENT](#photokeys)组成，fetchColumns需要传入这两个字段。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| callback | AsyncCallback&lt;string&gt; | 是   | 返回Exif字段组成的json格式的字符串。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('getExifDemo');
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    predicates.isNotNull('all_exif')
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: ['all_exif', photoAccessHelper.PhotoKeys.USER_COMMENT],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    console.info('getExifDemo photoAsset displayName: ' + JSON.stringify(photoAsset.displayName));
    let userCommentKey = 'UserComment';
    photoAsset.getExif((err, exifMessage) => {
      if (exifMessage !== undefined) {
        let userComment = JSON.stringify(JSON.parse(exifMessage), [userCommentKey]);
        console.info('getExifDemo userComment: ' + JSON.stringify(userComment));
      } else {
        console.error(`getExif failed, error: ${err.code}, ${err.message}`);
      }
    });
    fetchResult.close();
  } catch (err) {
    console.error(`getExifDemoCallback failed with error: ${err.code}, ${err.message}`);
  }
}
```

### setUserComment<sup>(deprecated)</sup>

setUserComment(userComment: string): Promise&lt;void&gt;

修改图片或者视频的备注信息，该方法使用Promise来返回结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAssetChangeRequest.setUserComment](#setusercomment11)替代。

**注意**：此接口只可修改图片或者视频的备注信息。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| userComment | string | 是   | 待修改的图片或视频的备注信息，备注信息最长为420字符。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
|Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('setUserCommentDemo')
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    let userComment = 'test_set_user_comment';
    await photoAsset.setUserComment(userComment);
  } catch (err) {
    console.error(`setUserCommentDemoPromise failed with error: ${err.code}, ${err.message}`);
  }
}
```

### setUserComment<sup>(deprecated)</sup>

setUserComment(userComment: string, callback: AsyncCallback&lt;void&gt;): void

修改图片或者视频的备注信息，该方法使用callback形式来返回结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAssetChangeRequest.setUserComment](#setusercomment11)替代。

**注意**：此接口只可修改图片或者视频的备注信息。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| userComment | string | 是   | 待修改的图片或视频的备注信息，备注信息最长为420字符。 |
| callback | AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('setUserCommentDemo')
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    let userComment = 'test_set_user_comment';
    photoAsset.setUserComment(userComment, (err) => {
      if (err === undefined) {
        console.info('setUserComment successfully');
      } else {
        console.error(`setUserComment failed with error: ${err.code}, ${err.message}`);
      }
    });
  } catch (err) {
    console.error(`setUserCommentDemoCallback failed with error: ${err.code}, ${err.message}`);
  }
}
```

### setPending<sup>11+</sup>

setPending(pendingState: boolean, callback: AsyncCallback&lt;void&gt;): void

为图片或视频资源设置pending状态，该方法使用callback形式来返回结果。

将文件通过`setPending(true)`设置为pending状态后，只能通过`setPending(false)`解除pending状态。可以通过`photoAsset.get(photoAccessHelper.PhotoKeys.PENDING)`的方式获取是否为pending状态，pending状态下返回true，否则返回false。

**注意**：setPending只能在文件的创建期使用，在文件的首次创建流程的close之后，无法通过setPending(true)将文件设置为pending状态。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| pendingState | boolean | 是    | 设置的pending状态，true为设置pending状态，false为解除pending状态 |
| callback | AsyncCallback&lt;void&gt; | 是    | Callback对象，返回void |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission denied.        |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |
| 14000011   | System inner fail.        |

**示例：**

```ts
async function example() {
  try {
    console.info('setPendingCallbackDemo');
    let testFileName: string = 'testFile' + Date.now() + '.jpg';
    let photoAsset = await phAccessHelper.createAsset(testFileName);
    let fd = await photoAsset.open('rw');
    photoAsset.setPending(true, async (err) => {
      if (err !== undefined) {
        console.error(`setPending(true) failed with error: ${err.code}, ${err.message}`);
        return;
      }
      // write photo buffer in fd
      photoAsset.setPending(false, async (err) => {
        if (err !== undefined) {
          console.error(`setPending(false) failed with error: ${err.code}, ${err.message}`);
          return;
        }
        await photoAsset.close(fd);
      });
    });
  } catch (err) {
    console.error(`setPendingCallbackDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### setPending<sup>11+</sup>

setPending(pendingState: boolean): Promise&lt;void&gt;

为图片或视频资源设置pending状态，该方法使用promise形式来返回结果。

将文件通过`setPending(true)`设置为pending状态后，只能通过`setPending(false)`解除pending状态。可以通过`photoAsset.get(photoAccessHelper.PhotoKeys.PENDING)`的方式获取是否为pending状态，pending状态下返回true，否则返回false。

**注意**：setPending只能在文件的创建期使用，在文件的首次创建流程的close之后，无法通过setPending(true)将文件设置为pending状态。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| pendingState | boolean | 是    | 设置的pending状态，true为设置pending状态，false为解除pending状态。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
|Promise&lt;boolean&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission denied.        |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |
| 14000011   | System inner fail.        |

**示例：**

```ts
async function example() {
  try {
    console.info('setPendingPromiseDemo');
    let testFileName: string = 'testFile' + Date.now() + '.jpg';
    let photoAsset = await phAccessHelper.createAsset(testFileName);
    let fd = await photoAsset.open('rw');
    await photoAsset.setPending(true);
    // write photo buffer in fd
    photoAsset.setPending(false);
    await photoAsset.close(fd);
  } catch (err) {
    console.error(`setPendingPromiseDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### isEdited<sup>11+</sup>

isEdited(callback: AsyncCallback&lt;boolean&gt;): void

查询图片或视频资源是否被编辑过，该方法使用callback形式来返回结果。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| callback | AsyncCallback&lt;boolean&gt; | 是    | Callback对象，返回图片或视频资源是否被编辑过 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission denied.        |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |
| 14000011   | System inner fail.        |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('isEditedCallbackDemo')
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    photoAsset.isEdited((err, isEdited) => {
      if (err === undefined) {
        if (isEdited === true) {
          console.info('Photo is edited');
        } else {
          console.info('Photo is not edited');
        }
      } else {
        console.error(`isEdited failed with error: ${err.code}, ${err.message}`);
      }
    });
  } catch (err) {
    console.error(`isEditedDemoCallback failed with error: ${err.code}, ${err.message}`);
  }
}
```

### isEdited<sup>11+</sup>

isEdited(): Promise&lt;boolean&gt;

查询图片或视频资源是否被编辑过，该方法使用promise形式来返回结果。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
|Promise&lt;boolean&gt; | Promise对象，返回图片或视频资源是否被编辑过。 |


**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission denied.        |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |
| 14000011   | System inner fail.        |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('isEditedPromiseDemo')
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    let isEdited = await photoAsset.isEdited();
    if (isEdited === true) {
      console.info('Photo is edited');
    } else {
      console.info('Photo is not edited');
    }
  } catch (err) {
    console.error(`isEditedDemoCallback failed with error: ${err.code}, ${err.message}`);
  }
}
```

### requestEditData<sup>11+</sup>

requestEditData(callback: AsyncCallback&lt;string&gt;): void

获得图片或视频资源的编辑数据，该方法使用callback形式来返回结果。

如果资源未编辑过，则返回一个空字符串。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| callback | AsyncCallback&lt;string&gt; | 是    | Callback对象，返回图片或视频资源的编辑数据 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission denied.        |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |
| 14000011   | System inner fail.        |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('requestEditDataCallbackDemo')
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    photoAsset.requestEditData((err, editdata) => {
      if (err === undefined) {
        console.info('Editdata is ' + editdata);
      } else {
        console.error(`requestEditData failed with error: ${err.code}, ${err.message}`);
      }
    });
  } catch (err) {
    console.error(`requestEditDataCallbackDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### requestEditData<sup>11+</sup>

requestEditData(): Promise&lt;string&gt;

获得图片或视频资源的编辑数据，该方法使用promise形式来返回结果。

如果资源未编辑过，则返回一个空字符串。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
|Promise&lt;string&gt; | Promise对象，返回图片或视频资源的编辑数据。 |


**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission denied.        |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |
| 14000011   | System inner fail.        |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('requestEditDataPromiseDemo')
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    let editdata: string = await photoAsset.requestEditData();
    console.info('Editdata is ' + editdata);
  } catch (err) {
    console.error(`requestEditDataPromiseDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### getEditData<sup>11+</sup>

getEditData(): Promise&lt;MediaAssetEditData&gt;

获得资产编辑数据，该方法使用promise形式来返回结果。

如果资源未编辑过，则返回的编辑数据的内容为空字符串。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
|Promise&lt;[MediaAssetEditData](#mediaasseteditdata11)&gt; | Promise对象，返回资产编辑数据。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission denied.        |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |
| 14000011   | System inner fail.        |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('getEditDataDemo')
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    let assetEditData: photoAccessHelper.MediaAssetEditData = await photoAsset.getEditData();
    let data: string = assetEditData.data;
    console.info('edit data is ' + data);
  } catch (err) {
    console.error(`getEditDataDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### requestSource<sup>11+</sup>

requestSource(callback: AsyncCallback&lt;number&gt;): void

打开源文件并返回fd，该方法使用callback形式来返回结果。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| callback | AsyncCallback&lt;number&gt; | 是    | Callback对象，返回源文件fd。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission denied.        |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |
| 14000011   | System inner fail.        |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('requsetSourceCallbackDemo')
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    photoAsset.requestSource((err, fd) => {
      if (err === undefined) {
        console.info('Source fd is ' + fd);
      } else {
        console.error(`requestSource failed with error: ${err.code}, ${err.message}`);
      }
    });
  } catch (err) {
    console.error(`requsetSourceCallbackDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### requestSource<sup>11+</sup>

requestSource(): Promise&lt;number&gt;

打开源文件并返回fd，该方法使用promise形式来返回结果。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
|Promise&lt;number&gt; | Promise对象，返回源文件fd。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission denied.        |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |
| 14000011   | System inner fail.        |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('requsetSourcePromiseDemo')
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    let fd = await photoAsset.requestSource();
    console.info('Source fd is ' + fd);
  } catch (err) {
    console.error(`requsetSourcePromiseDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### commitEditedAsset<sup>11+</sup>

commitEditedAsset(editData: string, uri: string, callback: AsyncCallback&lt;void&gt;)

提交编辑数据以及编辑后的图片或视频，该方法使用callback形式来返回结果。

通过uri将编辑后的文件传递给媒体库，uri是编辑后的文件在应用沙箱下的FileUri，可参考[FileUri](../apis-core-file-kit/js-apis-file-fileuri.md)。

**注意**：新的编辑数据提交后，将覆盖掉原来的编辑数据。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| editData | string | 是    | 提交的编辑数据。 |
| uri | string | 是    | 提交的编辑后的图片或视频，在应用沙箱下的uri。 |
| callback | AsyncCallback&lt;void&gt; | 是    | Callback对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission denied.        |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |
| 14000011   | System inner fail.        |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('commitEditedAssetCallbackDemo')
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    let editData = '123456';
    let uri = 'file://com.example.temptest/data/storage/el2/base/haps/entry/files/test.jpg';
    photoAsset.commitEditedAsset(editData, uri, (err) => {
      if (err === undefined) {
        console.info('commitEditedAsset is successful');
      } else {
        console.error(`commitEditedAsset failed with error: ${err.code}, ${err.message}`);
      }
    });
  } catch (err) {
    console.error(`commitEditedAssetCallbackDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### commitEditedAsset<sup>11+</sup>

commitEditedAsset(editData: string, uri: string): Promise&lt;void&gt;

提交编辑数据以及编辑后的图片或视频，该方法使用promise形式来返回结果。

通过uri将编辑后的文件传递给媒体库，uri是编辑后的文件在应用沙箱下的FileUri，可参考[FileUri](../apis-core-file-kit/js-apis-file-fileuri.md)。

**注意**：新的编辑数据提交后，将覆盖掉原来的编辑数据。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| editData | string | 是    | 提交的编辑数据。 |
| uri | string | 是    | 提交的编辑后的图片或视频，在应用沙箱下的uri。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
|Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission denied.        |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |
| 14000011   | System inner fail.        |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('commitEditedAssetPromiseDemo')
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    let editData = '123456';
    let uri = 'file://com.example.temptest/data/storage/el2/base/haps/entry/files/test.jpg';
    await photoAsset.commitEditedAsset(editData, uri);
    console.info('commitEditedAsset is successful');
  } catch (err) {
    console.error(`commitEditedAssetPromiseDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### revertToOriginal<sup>11+</sup>

revertToOriginal(callback: AsyncCallback&lt;void&gt;)

回退到编辑前的状态，该方法使用callback形式来返回结果。

**注意**：调用该接口后，编辑数据和编辑后的图片或视频资源都将被删除，无法恢复，请谨慎调用。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| callback | AsyncCallback&lt;void&gt; | 是    | Callback对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission denied.        |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |
| 14000011   | System inner fail.        |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('revertToOriginalCallbackDemo')
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    photoAsset.revertToOriginal((err) => {
      if (err === undefined) {
        console.info('revertToOriginal is successful');
      } else {
        console.error(`revertToOriginal failed with error: ${err.code}, ${err.message}`);
      }
    });
  } catch (err) {
    console.error(`revertToOriginalCallbackDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### revertToOriginal<sup>11+</sup>

revertToOriginal(): Promise&lt;void&gt;

回退到编辑前的状态，该方法使用promise形式来返回结果。

**注意**：调用该接口后，编辑数据和编辑后的图片或视频资源都将被删除，无法恢复，请谨慎调用。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
|Promise&lt;string&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission denied.        |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |
| 14000011   | System inner fail.        |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('revertToOriginalPromiseDemo')
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    photoAsset.revertToOriginal();
    console.info('revertToOriginal is successful');
  } catch (err) {
    console.error(`revertToOriginalPromiseDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### requestPhoto<sup>11+</sup>

requestPhoto(callback: AsyncCallback&lt;image.PixelMap&gt;): string

通过callback的形式，获取资源的快速缩略图和普通缩略图。

快速缩略图尺寸为128\*128，普通缩略图尺寸为256\*256。应用调用接口后，callback将返回两次缩略图对象，第一次为快速缩略图，第二次为普通缩略图。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| callback | AsyncCallback&lt;[image.PixelMap](../apis-image-kit/js-apis-image.md#pixelmap7)&gt; | 是    | Callback对象，返回获取的缩略图，调用2次。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| string | 本次获取任务的id。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission denied.        |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |
| 14000011   | System inner fail.        |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import image from '@ohos.multimedia.image'

async function example() {
  try {
    console.info('requestPhotoDemo')
    let options: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: new dataSharePredicates.DataSharePredicates()
    }
    let fetchResult = await phAccessHelper.getAssets(options);
    let photoAsset = await fetchResult.getFirstObject();
    let taskId: string = photoAsset.requestPhoto(async (err, pixel: image.PixelMap) => {
      if (err === undefined) {
        console.info("requestSource in, size: " + JSON.stringify((await pixel.getImageInfo()).size))
      } else {
        console.error(`requestSource failed with error: ${err.code}, ${err.message}`);
      }
    })
    console.info('requestSource taskId: ' + taskId)
  } catch (err) {
    console.error(`requestPhotoDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### requestPhoto<sup>11+</sup>

requestPhoto(options: RequestPhotoOptions, callback: AsyncCallback&lt;image.PixelMap&gt;): string

通过callback的形式，根据传入的选项，获取资源的缩略图。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| options | [RequestPhotoOptions](#requestphotooptions11) | 是    | 获取资源缩略图的选项。 |
| callback | AsyncCallback&lt;[image.PixelMap](../apis-image-kit/js-apis-image.md#pixelmap7)&gt; | 是    | Callback对象，返回获取的缩略图，根据选项的设置可能调用超过1次。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| string | 本次获取任务的id。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission denied.        |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |
| 14000011   | System inner fail.        |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import image from '@ohos.multimedia.image'

async function example() {
  try {
    console.info('requestPhotoDemo')
    let options: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: new dataSharePredicates.DataSharePredicates()
    }
    let fetchResult = await phAccessHelper.getAssets(options);
    let photoAsset = await fetchResult.getFirstObject();
    let taskId: string = photoAsset.requestPhoto({
      "size": {
        "width": 256,
        "height": 256
      },
      "requestPhotoType": photoAccessHelper.RequestPhotoType.REQUEST_ALL_THUMBNAILS
    }, async (err, pixel: image.PixelMap) => {
      if (err === undefined) {
        console.info("requestSource in, size: " + JSON.stringify((await pixel.getImageInfo()).size))
      } else {
        console.error(`requestSource failed with error: ${err.code}, ${err.message}`);
      }
    })
    console.info('requestSource taskId: ' + taskId)
  } catch (err) {
    console.error(`requestPhotoDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### cancelPhotoRequest<sup>11+</sup>

cancelPhotoRequest(requestId: string): void

根据id取消指定的获取媒体缩略图的任务。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| requestId | string | 是    | 待取消的获取媒体缩略图的任务id。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201   | Permission denied.        |
| 202   | Called by non-system application.         |
| 401   | if parameter is invalid.         |
| 14000011   | System inner fail.        |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import image from '@ohos.multimedia.image'

async function example() {
  try {
    console.info('cancelPhotoRequestDemo')
    let options: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: new dataSharePredicates.DataSharePredicates()
    }
    let fetchResult = await phAccessHelper.getAssets(options);
    let photoAsset = await fetchResult.getFirstObject();
    let taskId: string = photoAsset.requestPhoto({
      "size": {
        "width": 256,
        "height": 256
      },
      "requestPhotoType": photoAccessHelper.RequestPhotoType.REQUEST_ALL_THUMBNAILS
    }, async (err, pixel: image.PixelMap) => {
      if (err === undefined) {
        console.info("requestSource in, size: " + JSON.stringify((await pixel.getImageInfo()).size))
      } else {
        console.error(`requestSource failed with error: ${err.code}, ${err.message}`);
      }
    })
    console.info('requestSource taskId: ' + taskId)
    photoAsset.cancelPhotoRequest(taskId);
  } catch (err) {
    console.error(`cancelPhotoRequestDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### getAnalysisData<sup>11+</sup>

getAnalysisData(analysisType: AnalysisType): Promise\<string>

根据智慧分析类型获取指定分析结果数据。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.READ\_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名          | 类型           | 必填 | 说明           |
| :----------- | :----------- | :- | :----------- |
| analysisType | [AnalysisType](#analysistype11) | 是  | 需要获取的智慧分析类型。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID    | 错误信息                              |
| :------- | :-------------------------------- |
| 201      | Permission denied.                |
| 202      | Called by non-system application. |
| 401      | if parameter is invalid.          |
| 14000011 | System inner fail.                |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('getAnalysisDataDemo')
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: new dataSharePredicates.DataSharePredicates()
    }
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> =
      await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    if (photoAsset != undefined) {
      let analysisData: string = await photoAsset.getAnalysisData(
        photoAccessHelper.AnalysisType.ANALYSIS_OCR);
      console.info('get ocr result: ' + JSON.stringify(analysisData));
    }
    fetchResult.close();
  } catch (err) {
    console.error(`getAnalysisDataDemofailed with error: ${err.code}, ${err.message}`);
  }
}
```

## Album

实体相册

### recoverAssets<sup>(deprecated)</sup>

recoverAssets(assets: Array&lt;PhotoAsset&gt;, callback: AsyncCallback&lt;void&gt;): void

从回收站中恢复图片或者视频，需要先在回收站中预置文件资源。该方法使用callback形式来返回结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAlbumChangeRequest.recoverAssets](#recoverassets11)替代。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 回收站中待恢复图片或者视频数组。 |
| callback | AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202      |  Called by non-system application.         |
| 401      |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('recoverAssetsDemoCallback');
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.TRASH);
    let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await album.getAssets(fetchOption);
    let asset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    album.recoverAssets([asset], (err) => {
      if (err === undefined) {
        console.info('album recoverAssets successfully');
      } else {
        console.error(`album recoverAssets failed with error: ${err.code}, ${err.message}`);
      }
    });
  } catch (err) {
    console.error(`recoverAssetsDemoCallback failed with error: ${err.code}, ${err.message}`);
  }
}
```

### recoverAssets<sup>(deprecated)</sup>

recoverAssets(assets: Array&lt;PhotoAsset&gt;): Promise&lt;void&gt;

从回收站中恢复图片或者视频，需要先在回收站中预置文件资源。该方法使用Promise来返回结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAlbumChangeRequest.recoverAssets](#recoverassets11)替代。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 回收站中待恢复图片或者视频数组。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
|Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202      |  Called by non-system application.         |
| 401      |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  try {
    console.info('recoverAssetsDemoPromise');
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.TRASH);
    let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await album.getAssets(fetchOption);
    let asset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    album.recoverAssets([asset]).then(() => {
      console.info('album recoverAssets successfully');
    }).catch((err: BusinessError) => {
      console.error(`album recoverAssets failed with error: ${err.code}, ${err.message}`);
    });
  } catch (err) {
    console.error(`recoverAssetsDemoPromise failed with error: ${err.code}, ${err.message}`);
  }
}
```

### deleteAssets<sup>(deprecated)</sup>

deleteAssets(assets: Array&lt;PhotoAsset&gt;, callback: AsyncCallback&lt;void&gt;): void

从回收站中彻底删除图片或者视频，需要先在回收站中预置文件资源。该方法使用callback形式来返回结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAlbumChangeRequest.deleteAssets](#deleteassets11)替代。

**注意**：此操作不可逆，执行此操作后文件资源将彻底删除，请谨慎操作。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 回收站中待彻底删除图片或者视频数组。 |
| callback | AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202      |  Called by non-system application.         |
| 401      |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('deleteAssetsDemoCallback');
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.TRASH);
    let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await album.getAssets(fetchOption);
    let asset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    album.deleteAssets([asset], (err) => {
      if (err === undefined) {
        console.info('album deleteAssets successfully');
      } else {
        console.error(`album deleteAssets failed with error: ${err.code}, ${err.message}`);
      }
    });
  } catch (err) {
    console.error(`deleteAssetsDemoCallback failed with error: ${err.code}, ${err.message}`);
  }
}
```

### deleteAssets<sup>(deprecated)</sup>

deleteAssets(assets: Array&lt;PhotoAsset&gt;): Promise&lt;void&gt;

从回收站中彻底删除图片或者视频，需要先在回收站中预置文件资源。该方法使用Promise来返回结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAlbumChangeRequest.deleteAssets](#deleteassets11)替代。

**注意**：此操作不可逆，执行此操作后文件资源将彻底删除，请谨慎操作。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 回收站中待彻底删除图片或者视频数组。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
|Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202      |  Called by non-system application.         |
| 401      |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  try {
    console.info('deleteAssetsDemoPromise');
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.TRASH);
    let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await album.getAssets(fetchOption);
    let asset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    album.deleteAssets([asset]).then(() => {
      console.info('album deleteAssets successfully');
    }).catch((err: BusinessError) => {
      console.error(`album deleteAssets failed with error: ${err.code}, ${err.message}`);
    });
  } catch (err) {
    console.error(`deleteAssetsDemoPromise failed with error: ${err.code}, ${err.message}`);
  }
}
```

### setCoverUri<sup>(deprecated)</sup>

setCoverUri(uri: string, callback: AsyncCallback&lt;void&gt;): void

设置相册封面，该方法使用callback形式来返回结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAlbumChangeRequest.setCoverUri](#setcoveruri11)替代。

**注意**：此接口只可修改用户相册封面，不允许修改系统相册封面。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| uri | string | 是   | 待设置为相册封面文件的uri。 |
| callback | AsyncCallback&lt;void&gt; | 是   | callback返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202      |  Called by non-system application.         |
| 401      |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('setCoverUriDemoCallback');
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC);
    let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await album.getAssets(fetchOption);
    let asset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    album.setCoverUri(asset.uri, (err) => {
      if (err === undefined) {
        console.info('album setCoverUri successfully');
      } else {
        console.error(`album setCoverUri failed with error: ${err.code}, ${err.message}`);
      }
    });
  } catch (err) {
    console.error(`setCoverUriDemoCallback failed with error: ${err.code}, ${err.message}`);
  }
}
```

### setCoverUri<sup>(deprecated)</sup>

setCoverUri(uri: string): Promise&lt;void&gt;

设置相册封面，该方法使用Promise来返回结果。

> **说明：** 
>
> 从API version 10开始支持，从API version 11开始废弃。建议使用[MediaAlbumChangeRequest.setCoverUri](#setcoveruri11)替代。

**注意**：此接口只可修改用户相册封面，不允许修改系统相册封面。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| uri | string | 是   | 待设置为相册封面文件的uri。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
|Promise&lt;void&gt; | Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202      |  Called by non-system application.         |
| 401      |  if parameter is invalid.         |
| 13900012     | Permission denied.         |
| 13900020     | Invalid argument.         |
| 14000011       | System inner fail.         |
**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  try {
    console.info('setCoverUriDemoPromise');
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let fetchOption: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC);
    let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await album.getAssets(fetchOption);
    let asset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    album.setCoverUri(asset.uri).then(() => {
      console.info('album setCoverUri successfully');
    }).catch((err: BusinessError) => { 
      console.error(`album setCoverUri failed with error: ${err.code}, ${err.message}`);
    });
  } catch (err) {
    console.error(`setCoverUriDemoPromise failed with error: ${err.code}, ${err.message}`);
  }
}
```

## MediaAssetEditData<sup>11+</sup>

资产编辑数据。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

### 属性

| 名称           | 类型    | 可读   | 可写  | 说明   |
| ------------ | ------ | ---- | ---- | ------- |
| compatibleFormat | string | 是    | 是    | 编辑数据的格式。**系统接口**：此接口为系统接口。    |
| formatVersion | string | 是    | 是   | 编辑数据格式的版本。**系统接口**：此接口为系统接口。    |
| data | string | 是    | 是   | 编辑数据的内容。**系统接口**：此接口为系统接口。    |

### constructor<sup>11+</sup>

constructor(compatibleFormat: string, formatVersion: string)

构造函数。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| compatibleFormat | string | 是   | 编辑数据的格式。 |
| formatVersion | string | 是   | 编辑数据格式的版本。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202      |  Called by non-system application.         |
| 401      |  if parameter is invalid.         |
| 14000011       | System inner fail.          |

**示例：**

```ts
let assetEditData: photoAccessHelper.MediaAssetEditData = new photoAccessHelper.MediaAssetEditData('system', '1.0');
```

## MediaAssetChangeRequest<sup>11+</sup>

资产变更请求。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

### createAssetRequest<sup>11+</sup>

static createAssetRequest(context: Context, displayName: string, options?: PhotoCreateOptions): MediaAssetChangeRequest

指定待创建的图片或者视频的文件名，创建资产变更请求。

待创建的文件名参数规格为：
- 应包含有效文件主名和图片或视频扩展名。
- 文件名字符串长度为1~255。
- 文件主名中不允许出现非法字符，包括：<br> . .. \ / : * ? " ' ` < > | { } [ ]

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型    | 必填 | 说明                       |
| ------- | ------- | ---- | -------------------------- |
| context | [Context](../apis-ability-kit/js-apis-inner-application-context.md) | 是   | 传入Ability实例的Context。 |
| displayName  | string        | 是   | 待创建的图片或者视频文件名。              |
| options  | [PhotoCreateOptions](#photocreateoptions)        | 否   | 图片或视频的创建选项。              |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| [MediaAssetChangeRequest](#mediaassetchangerequest11) | 返回创建资产的变更请求。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   |  Called by non-system application.         |
| 401      |  if parameter is invalid.         |
| 14000001      | Invalid display name.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('createAssetRequestDemo');
  try {
    let testFileName: string = 'testFile' + Date.now() + '.jpg';
    let assetChangeRequest: photoAccessHelper.MediaAssetChangeRequest = photoAccessHelper.MediaAssetChangeRequest.createAssetRequest(context, testFileName);
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

### setFavorite<sup>11+</sup>

setFavorite(favoriteState: boolean): void

将文件设置为收藏文件。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| favoriteState | boolean | 是    | 是否设置为收藏文件， true：设置为收藏文件；false：取消收藏。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  console.info('setFavoriteDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let asset = await fetchResult.getFirstObject();
  let assetChangeRequest: photoAccessHelper.MediaAssetChangeRequest = new photoAccessHelper.MediaAssetChangeRequest(asset);
  assetChangeRequest.setFavorite(true);
  phAccessHelper.applyChanges(assetChangeRequest).then(() => {
    console.info('apply setFavorite successfully');
  }).catch((err: BusinessError) => {
    console.error(`apply setFavorite failed with error: ${err.code}, ${err.message}`);
  });
}
```

### setHidden<sup>11+</sup>

setHidden(hiddenState: boolean): void

将文件设置为隐藏文件。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| hiddenState | boolean  | 是    | 是否设置为隐藏文件，true：将文件资产放入隐藏相册；false：从隐藏相册中恢复。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  console.info('setHiddenDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let asset = await fetchResult.getFirstObject();
  let assetChangeRequest: photoAccessHelper.MediaAssetChangeRequest = new photoAccessHelper.MediaAssetChangeRequest(asset);
  assetChangeRequest.setHidden(true);
  phAccessHelper.applyChanges(assetChangeRequest).then(() => {
    console.info('apply setHidden successfully');
  }).catch((err: BusinessError) => {
    console.error(`apply setHidden failed with error: ${err.code}, ${err.message}`);
  });
}
```

### setUserComment<sup>11+</sup>

setUserComment(userComment: string): void

修改媒体资产的备注信息。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| userComment | string | 是   | 待修改的资产备注信息，备注信息最长为420字符。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  console.info('setUserCommentDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let asset = await fetchResult.getFirstObject();
  let assetChangeRequest: photoAccessHelper.MediaAssetChangeRequest = new photoAccessHelper.MediaAssetChangeRequest(asset);
  let userComment: string = 'test_set_user_comment';
  assetChangeRequest.setUserComment(userComment);
  phAccessHelper.applyChanges(assetChangeRequest).then(() => {
    console.info('apply setUserComment successfully');
  }).catch((err: BusinessError) => {
    console.error(`apply setUserComment failed with error: ${err.code}, ${err.message}`);
  });
}
```

### setEditData<sup>11+</sup>

setEditData(editData: MediaAssetEditData): void

保存资产的编辑数据。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| editData | [MediaAssetEditData](#mediaasseteditdata11) | 是   | 待保存的资产编辑数据。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  console.info('setEditDataDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let asset = await fetchResult.getFirstObject();
  let assetChangeRequest: photoAccessHelper.MediaAssetChangeRequest = new photoAccessHelper.MediaAssetChangeRequest(asset);

  let assetEditData: photoAccessHelper.MediaAssetEditData = new photoAccessHelper.MediaAssetEditData('system', '1.0');
  let fileUri = 'file://com.example.temptest/data/storage/el2/base/haps/entry/files/test.jpg';
  assetChangeRequest.addResource(photoAccessHelper.ResourceType.IMAGE_RESOURCE, fileUri);
  assetEditData.data = '123456';
  assetChangeRequest.setEditData(assetEditData);
  phAccessHelper.applyChanges(assetChangeRequest).then(() => {
    console.info('apply setEditData successfully');
  }).catch((err: BusinessError) => {
    console.error(`apply setEditData failed with error: ${err.code}, ${err.message}`);
  });
}
```

### addResource<sup>11+</sup>

addResource(type: ResourceType, proxy: PhotoProxy): void

通过PhotoProxy数据添加资源。

**注意**：对于同一个资产变更请求，不支持在成功添加资源后，重复调用该接口。

**系统接口**：此接口为系统接口，仅提供给相机应用使用。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型                              | 必填 | 说明                   |
| ------- |---------------------------------| ---- |----------------------|
| type | [ResourceType](#resourcetype11) | 是   | 待添加资源的类型。            |
| proxy | [PhotoProxy](#photoproxy11)     | 是   | 待添加资源的PhotoProxy 数据。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID    | 错误信息                              |
|----------|-----------------------------------|
| 202      | Called by non-system application. |
| 401      | if parameter is invalid.          |
| 14000011 | System inner fail.                | 
| 14000016 | Operation Not Support.            |

**示例：**

```ts
class PhotoProxyImpl implements photoAccessHelper.PhotoProxy {
  // 应用实现PhotoProxy
}

async function example() {
  console.info('addResourceByPhotoProxyDemo');
  try {
    let photoType: photoAccessHelper.PhotoType = photoAccessHelper.PhotoType.IMAGE;
    let extension: string = 'jpg';
    let assetChangeRequest: photoAccessHelper.MediaAssetChangeRequest = photoAccessHelper.MediaAssetChangeRequest.createAssetRequest(context, photoType, extension);
    let photoProxy: PhotoProxyImpl = new PhotoProxyImpl();
    assetChangeRequest.addResource(photoAccessHelper.ResourceType.IMAGE_RESOURCE, photoProxy);
    await phAccessHelper.applyChanges(assetChangeRequest);
    console.info('addResourceByPhotoProxy successfully');
  } catch (err) {
    console.error(`addResourceByPhotoProxyDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### setLocation<sup>11+</sup>

setLocation(longitude: number, latitude: number): void

设置文件的经纬度信息。

**系统接口**：此接口为系统接口

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型          | 必填 | 说明    |
| ------- |-------------| ---- |-------|
| longitude | number      | 是   | 经度。 |
| latitude | number | 是   | 纬度。   |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202      | Called by non-system application. |
| 401      |  if parameter is invalid.   |
| 14000011 |  System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  console.info('setLocationDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let asset = await fetchResult.getFirstObject();
  let assetChangeRequest: photoAccessHelper.MediaAssetChangeRequest = new photoAccessHelper.MediaAssetChangeRequest(asset);
  assetChangeRequest.setLocation(120.52, 30.40);
  phAccessHelper.applyChanges(assetChangeRequest).then(() => {
    console.info('apply setLocation successfully');
  }).catch((err: BusinessError) => {
    console.error(`apply setLocation failed with error: ${err.code}, ${err.message}`);
  });
}
```

## MediaAssetsChangeRequest<sup>11+</sup>

批量资产变更请求。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

### constructor<sup>11+</sup>

constructor(assets: Array&lt;PhotoAsset&gt;)

构造函数。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 需要变更的资产数组。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.   |
| 401      |  if parameter is invalid.         |
| 14000011       | System inner fail.          |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('MediaAssetsChangeRequest constructorDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let photoAssetList: Array<photoAccessHelper.PhotoAsset> = await fetchResult.getAllObjects();
  let assetsChangeRequest: photoAccessHelper.MediaAssetsChangeRequest = new photoAccessHelper.MediaAssetsChangeRequest(photoAssetList);
}
```

### setFavorite<sup>11+</sup>

setFavorite(favoriteState: boolean): void

将文件设置为收藏文件。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| favoriteState | boolean | 是    | 是否设置为收藏文件， true：设置为收藏文件；false：取消收藏。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  console.info('setFavoriteDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let photoAssetList: Array<photoAccessHelper.PhotoAsset> = await fetchResult.getAllObjects();
  let assetsChangeRequest: photoAccessHelper.MediaAssetsChangeRequest = new photoAccessHelper.MediaAssetsChangeRequest(photoAssetList);
  assetsChangeRequest.setFavorite(true);
  phAccessHelper.applyChanges(assetsChangeRequest).then(() => {
    console.info('apply setFavorite successfully');
  }).catch((err: BusinessError) => {
    console.error(`apply setFavorite failed with error: ${err.code}, ${err.message}`);
  });
}
```

### setHidden<sup>11+</sup>

setHidden(hiddenState: boolean): void

将文件设置为隐藏文件。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| hiddenState | boolean  | 是    | 是否设置为隐藏文件，true：将文件资产放入隐藏相册；false：从隐藏相册中恢复。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  console.info('setHiddenDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let photoAssetList: Array<photoAccessHelper.PhotoAsset> = await fetchResult.getAllObjects();
  let assetsChangeRequest: photoAccessHelper.MediaAssetsChangeRequest = new photoAccessHelper.MediaAssetsChangeRequest(photoAssetList);
  assetsChangeRequest.setHidden(true);
  phAccessHelper.applyChanges(assetsChangeRequest).then(() => {
    console.info('apply setHidden successfully');
  }).catch((err: BusinessError) => {
    console.error(`apply setHidden failed with error: ${err.code}, ${err.message}`);
  });
}
```

### setUserComment<sup>11+</sup>

setUserComment(userComment: string): void

修改媒体资产的备注信息。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| userComment | string | 是   | 待修改的资产备注信息，备注信息最长为420字符。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import { BusinessError } from '@ohos.base';

async function example() {
  console.info('setUserCommentDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOption: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOption);
  let photoAssetList: Array<photoAccessHelper.PhotoAsset> = await fetchResult.getAllObjects();
  let assetsChangeRequest: photoAccessHelper.MediaAssetsChangeRequest = new photoAccessHelper.MediaAssetsChangeRequest(photoAssetList);
  assetsChangeRequest.setUserComment('test_set_user_comment');
  phAccessHelper.applyChanges(assetsChangeRequest).then(() => {
    console.info('apply setUserComment successfully');
  }).catch((err: BusinessError) => {
    console.error(`apply setUserComment failed with error: ${err.code}, ${err.message}`);
  });
}
```

## MediaAlbumChangeRequest<sup>11+</sup>

相册变更请求。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

### createAlbumRequest<sup>11+</sup>

static createAlbumRequest(context: Context, name: string): MediaAlbumChangeRequest

创建相册变更请求。

相册名的参数规格为：
- 相册名字符串长度为1~255。
- 不允许出现非法字符，包括：<br> . .. \ / : * ? " ' ` < > | { } [ ]
- 英文字符大小写不敏感。
- 相册名不允许重名。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型    | 必填 | 说明                       |
| ------- | ------- | ---- | -------------------------- |
| context | [Context](../apis-ability-kit/js-apis-inner-application-context.md) | 是   | 传入Ability实例的Context。 |
| name | string | 是   | 待创建相册的名称。|

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| [MediaAlbumChangeRequest](#mediaalbumchangerequest11) | 返回创建相册的变更请求。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202   |  Called by non-system application.         |
| 401   | if parameter is invalid.         |
| 14000011   | System inner fail.        |

**示例：**

```ts
async function example() {
  console.info('createAlbumRequestDemo');
  try {
    let albumName: string = 'newAlbumName' + new Date().getTime();
    let albumChangeRequest: photoAccessHelper.MediaAlbumChangeRequest = photoAccessHelper.MediaAlbumChangeRequest.createAlbumRequest(context, albumName);
    await phAccessHelper.applyChanges(albumChangeRequest);
    console.info('apply createAlbumRequest successfully');
  } catch (err) {
    console.error(`createAlbumRequestDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### deleteAlbums<sup>11+</sup>

static deleteAlbums(context: Context, albums: Array&lt;Album&gt;): Promise&lt;void&gt;

删除相册，使用Promise方式返回结果。

删除相册前需先确保相册存在，只能删除用户相册。

**系统接口**：此接口为系统接口。

**需要权限**：ohos.permission.WRITE_IMAGEVIDEO

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名  | 类型    | 必填 | 说明                       |
| ------- | ------- | ---- | -------------------------- |
| context | [Context](../apis-ability-kit/js-apis-inner-application-context.md) | 是   | 传入Ability实例的Context。 |
| albums  |  Array&lt;[Album](#album)&gt;          | 是   | 待删除的相册数组。         |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;void&gt;| Promise对象，返回void。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 201      |  Permission denied.         |
| 202   |  Called by non-system application.  |
| 401      |  if parameter is invalid.   |
| 14000011 |  System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('deleteAlbumsDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, fetchOptions);
    let album: photoAccessHelper.Album = await fetchResult.getFirstObject();
    await photoAccessHelper.MediaAlbumChangeRequest.deleteAlbums(context, [album]);
    console.info('deleteAlbums successfully');
  } catch (err) {
    console.error(`deleteAlbumsDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### setCoverUri<sup>11+</sup>

setCoverUri(coverUri: string): void

设置相册封面。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| coverUri | string | 是   | 待设置为相册封面文件的uri。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('setCoverUriDemo');
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
    albumChangeRequest.setCoverUri(asset.uri);
    await phAccessHelper.applyChanges(albumChangeRequest);
    console.info('setCoverUri successfully');
  } catch (err) {
    console.error(`setCoverUriDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### moveAssets<sup>11+</sup>

moveAssets(assets: Array&lt;PhotoAsset&gt;, targetAlbum: Album): void

从相册中移动资产到另一个目标相册。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 待从相册中移出的资产数组。 |
| targetAlbum | Album | 是   | 待移入资产的目标相册。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202      |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |
| 14000016 |  Operation Not Support.     |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('moveAssetsDemo');
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

    if (albumFetchResult.isAfterLast()) {
      console.error('lack of album to be moved into');
      return;
    }
    let nextAlbum: photoAccessHelper.Album = await albumFetchResult.getNextObject();
    let albumChangeRequest: photoAccessHelper.MediaAlbumChangeRequest = new photoAccessHelper.MediaAlbumChangeRequest(album);
    albumChangeRequest.moveAssets([asset], nextAlbum);
    await phAccessHelper.applyChanges(albumChangeRequest);
    console.info('moveAssets successfully');
  } catch (err) {
    console.error(`moveAssetsDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### recoverAssets<sup>11+</sup>

recoverAssets(assets: Array&lt;PhotoAsset&gt;): void

从回收站中恢复资产。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 待从回收站中恢复的资产数组。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202      |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |
| 14000016 |  Operation Not Support.     |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('recoverAssetsDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.TRASH);
    let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await album.getAssets(fetchOptions);
    let asset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();

    let albumChangeRequest: photoAccessHelper.MediaAlbumChangeRequest = new photoAccessHelper.MediaAlbumChangeRequest(album);
    albumChangeRequest.recoverAssets([asset]);
    await phAccessHelper.applyChanges(albumChangeRequest);
    console.info('recoverAssets successfully');
  } catch (err) {
    console.error(`recoverAssetsDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### deleteAssets<sup>11+</sup>

deleteAssets(assets: Array&lt;PhotoAsset&gt;): void

从回收站中彻底删除资产。

**注意**：此操作不可逆，执行此操作后文件资源将彻底删除，请谨慎操作。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| assets | Array&lt;[PhotoAsset](#photoasset)&gt; | 是   | 待从回收站中彻底删除的资产数组。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202      |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |
| 14000016 |  Operation Not Support.     |

**示例：**

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  console.info('deleteAssetsPermanentlyDemo');
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SYSTEM, photoAccessHelper.AlbumSubtype.TRASH);
    let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await album.getAssets(fetchOptions);
    let asset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();

    let albumChangeRequest: photoAccessHelper.MediaAlbumChangeRequest = new photoAccessHelper.MediaAlbumChangeRequest(album);
    albumChangeRequest.deleteAssets([asset]);
    await phAccessHelper.applyChanges(albumChangeRequest);
    console.info('succeed to deleteAssets permanently');
  } catch (err) {
    console.error(`deleteAssetsPermanentlyDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

### setDisplayLevel<sup>11+</sup>

setDisplayLevel(displayLevel: number): void

设置人像相册的显示级别。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| displayLevel | number | 是    | 设置人像相册的显示级别， 0：取消该人像相册收藏；1：设置人像相册为首届面；2：设置人像相册为更多界面；3：设置人像相册为收藏界面。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

``` ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('setDisplayLevel Example')
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    predicates.equalTo('user_display_level', 2);
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SMART, photoAccessHelper.AlbumSubtype.PORTRAIT, fetchOptions);
    let album: photoAccessHelper.Album = await fetchResult.getFirstObject();
    let changeRequest: photoAccessHelper.MediaAlbumChangeRequest = new photoAccessHelper.MediaAlbumChangeRequest(album);
    changeRequest.setDisplayLevel(1);
    await phAccessHelper.applyChanges(changeRequest);
  } catch (err) {
    console.error(`setDisplayLevel failed with error: ${err.code}, ${err.message}`);
  }
}
```

### setIsMe<sup>11+</sup>

setIsMe(): void

将人像相册的人物关系设置为“我”。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

``` ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('setIsMe Example')
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    predicates.equalTo('user_display_level', 2);
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SMART, photoAccessHelper.AlbumSubtype.PORTRAIT, fetchOptions);
    let album: photoAccessHelper.Album = await fetchResult.getFirstObject();
    let changeRequest: photoAccessHelper.MediaAlbumChangeRequest = new photoAccessHelper.MediaAlbumChangeRequest(album);
    changeRequest.setIsMe();
    await phAccessHelper.applyChanges(changeRequest);
  } catch (err) {
    console.error(`setIsMe failed with error: ${err.code}, ${err.message}`);
  }
}
```

### dismissAssets<sup>11+</sup>

dismissAssets(assets: Array&lt;PhotoAsset&gt;): void

从该人像相册中移除指定图片。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| assets | Array&lt;PhotoAsset&gt; | 是    | 需要移除的文件列表 。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |
| 14000016       | Operation Not support.         |

**示例：**

``` ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('dismissAssets Example')
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    predicates.equalTo('user_display_level', 2);
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SMART, photoAccessHelper.AlbumSubtype.PORTRAIT, fetchOptions);
    let album: photoAccessHelper.Album = await fetchResult.getFirstObject();

    let predicatesAsset: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    let assetFetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicatesAsset
    };
    let assetFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(assetFetchOptions);
    let asset: photoAccessHelper.PhotoAsset = await assetFetchResult.getFirstObject();

    let changeRequest: photoAccessHelper.MediaAlbumChangeRequest = new photoAccessHelper.MediaAlbumChangeRequest(album);
    changeRequest.dismissAssets([asset]);
    await phAccessHelper.applyChanges(changeRequest);
  } catch (err) {
    console.error(`dismissAssets failed with error: ${err.code}, ${err.message}`);
  }
}
```

### mergeAlbum<sup>11+</sup>

mergeAlbum(target: Album): void

将两个人像相册合并。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| target | [Album](#album) | 是    | 需要合并的目标相册，合并相册必须重命名。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202        |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |
| 14000016       | Operation Not support.         |

**示例：**

``` ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';

async function example() {
  try {
    console.info('mergeAlbum Example')
    let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
    predicates.equalTo('user_display_level', 2);
    let fetchOptions: photoAccessHelper.FetchOptions = {
      fetchColumns: [],
      predicates: predicates
    };
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.SMART, photoAccessHelper.AlbumSubtype.PORTRAIT, fetchOptions);
    let album: photoAccessHelper.Album = await fetchResult.getFirstObject();
    if (fetchResult.isAfterLast()) {
      console.error('lack of album to merge');
      return;
    }
    let target: photoAccessHelper.Album = await fetchResult.getNextObject();

    let changeRequest: photoAccessHelper.MediaAlbumChangeRequest = new photoAccessHelper.MediaAlbumChangeRequest(album);
    changeRequest.mergeAlbum(target);
    changeRequest.setAlbumName("testName");
    await phAccessHelper.applyChanges(changeRequest);
  } catch (err) {
    console.error(`mergeAlbum failed with error: ${err.code}, ${err.message}`);
  }
}
```

### placeBefore<sup>11+</sup>

placeBefore(album: Album): void;

将当前相册排序到目标相册之前。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| album | [Album](#album) | 是   |  目标相册。如果要将当前相册排序到末位，则目标相册传入null。 |

**错误码：**

接口抛出错误码的详细介绍请参见[通用错误码](../errorcode-universal.md)和[文件管理错误码](../apis-core-file-kit/errorcode-filemanagement.md)。

| 错误码ID | 错误信息 |
| -------- | ---------------------------------------- |
| 202      |  Called by non-system application.         |
| 401       |  if parameter is invalid.         |
| 14000011       | System inner fail.         |

**示例：**

```ts
async function example() {
  console.info('placeBeforeDemo');
  try {
    let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC);
    let firstAlbum: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
    if (albumFetchResult.isAfterLast()) {
      console.error('lack of album to place before');
      return;
    }
    let secondAlbum: photoAccessHelper.Album = await albumFetchResult.getNextObject();
    let albumChangeRequest: photoAccessHelper.MediaAlbumChangeRequest = new photoAccessHelper.MediaAlbumChangeRequest(secondAlbum);
    albumChangeRequest.placeBefore(firstAlbum);
    await phAccessHelper.applyChanges(albumChangeRequest);
    console.info('placeBefore successfully');
  } catch (err) {
    console.error(`placeBeforeDemo failed with error: ${err.code}, ${err.message}`);
  }
}
```

## PhotoSubtype

枚举，不同[PhotoAsset](#photoasset)的类型。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称  |  值 |  说明 |
| ----- |  ---- |  ---- |
| DEFAULT |  0 |  默认照片类型。 |
| SCREENSHOT |  1 |  截屏录屏文件类型。 |

## PositionType

枚举，文件位置，表示文件在本地或云端。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称  |  值 |  说明 |
| ----- |  ---- |  ---- |
| LOCAL |  1 << 0 |  文件只存在于本端设备。 |
| CLOUD |  1 << 1 |  文件只存在于云端。 |

## AlbumType

枚举，相册类型，表示是用户相册还是系统预置相册。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                  | 值    | 说明                        |
| ------------------- | ---- | ------------------------- |
| SMART<sup>11+</sup> | 4096 | 智慧分析相册。**系统接口**：此接口为系统接口。 |

## AlbumSubtype

枚举，相册子类型，表示具体的相册类型。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                                | 值          | 说明                              |
| --------------------------------- | ---------- | ------------------------------- |
| HIDDEN                            | 1027       | 隐藏相册。**系统接口**：此接口为系统接口。         |
| TRASH                             | 1028       | 回收站。**系统接口**：此接口为系统接口。          |
| SCREENSHOT                        | 1029       | 截屏和录屏相册。**系统接口**：此接口为系统接口。      |
| CAMERA                            | 1030       | 相机拍摄的照片和视频相册。**系统接口**：此接口为系统接口。 |
| IMAGE<sup>11+</sup>               | 1031       | 所有图片相册。**系统接口**：此接口为系统接口。       |
| SOURCE\_GENERIC<sup>11+</sup>     | 2049       | 来源相册。**系统接口**：此接口为系统接口。         |
| CLASSIFY<sup>11+</sup>            | 4097       | 分类相册。**系统接口**：此接口为系统接口。         |
| GEOGRAPHY\_LOCATION<sup>11+</sup> | 4099       | 地图相册。**系统接口**：此接口为系统接口。         |
| GEOGRAPHY\_CITY<sup>11+</sup>     | 4100       | 城市相册。**系统接口**：此接口为系统接口。         |
| SHOOTING\_MODE<sup>11+</sup>      | 4101       | 拍摄模式相册。**系统接口**：此接口为系统接口。       |
| PORTRAIT<sup>11+</sup>            | 4102       | 人像相册。**系统接口**：此接口为系统接口。         |

## RequestPhotoType<sup>11+</sup>

枚举，获取图片或视频缩略图的操作类型。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称  |  值 |  说明 |
| ----- |  ---- |  ---- |
| REQUEST_ALL_THUMBNAILS  |  0 |  即获取快速缩略图，又获取质量缩略图。 |
| REQUEST_FAST_THUMBNAIL |  1 |  只获取快速缩略图。 |
| REQUEST_QUALITY_THUMBNAIL |  2 |  只获取质量缩略图。 |

## PhotoKeys

枚举，图片和视频文件关键信息。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称          | 值              | 说明                                                       |
| ------------- | ------------------- | ---------------------------------------------------------- |
| POSITION  | 'position'            | 文件位置类型。**系统接口**：此接口为系统接口。                               |
| DATE_TRASHED  | 'date_trashed'  | 删除日期（删除文件时间距1970年1月1日的秒数值）。**系统接口**：此接口为系统接口。                 |
| HIDDEN  | 'hidden'            | 文件的隐藏状态。**系统接口**：此接口为系统接口。                               |
| CAMERA_SHOT_KEY  | 'camera_shot_key'  | 锁屏相机拍照或录像的标记字段（仅开放给系统相机,其key值由系统相机定义）。**系统接口**：此接口为系统接口。            |
| USER_COMMENT<sup>10+</sup>  | 'user_comment'            | 用户注释信息。**系统接口**：此接口为系统接口。           |
| DATE_YEAR<sup>11+</sup>  | 'date_year'            | 创建文件的年份。**系统接口**：此接口为系统接口。           |
| DATE_MONTH<sup>11+</sup>  | 'date_month'            | 创建文件的月份。**系统接口**：此接口为系统接口。           |
| DATE_DAY<sup>11+</sup>  | 'date_day'            | 创建文件的日期。**系统接口**：此接口为系统接口。           |
| PENDING<sup>11+</sup>  | 'pending'            | pending状态。**系统接口**：此接口为系统接口。           |

## HiddenPhotosDisplayMode<sup>11+</sup>

枚举，系统中隐藏文件显示模式。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称          | 值              | 说明                                                       |
| ------------- | ------------------- | ---------------------------------------------------------- |
| ASSETS_MODE   | 0       | 按系统预置的隐藏相册显示隐藏文件，即显示系统中所有的隐藏文件。    |
| ALBUMS_MODE    | 1    | 按相册显示隐藏文件（即显示系统中所有包含隐藏文件的相册，除系统预置的隐藏相册本身和回收站相册以外）。  |

## PhotoCreateOptions

图片或视频的创建选项。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                   | 类型                | 必填 | 说明                                              |
| ---------------------- | ------------------- | ---- | ------------------------------------------------ |
| subtype           | [PhotoSubtype](#photosubtype) | 否  | 图片或者视频的子类型。  |
| cameraShotKey           | string | 否  | 锁屏相机拍照或录像的标记字段（仅开放给系统相机,其key值由系统相机定义）。   |

## RequestPhotoOptions<sup>11+</sup>

获取图片或视频缩略图的选项。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                   | 类型                | 必填 | 说明                                              |
| ---------------------- | ------------------- | ---- | ------------------------------------------------ |
| size           | [image.Size](../apis-image-kit/js-apis-image.md#size) | 否  | 获取缩略图的尺寸。  |
| requestPhotoType    | [RequestPhotoType](#requestphototype11) | 否  | 获取的操作类型。  |

## RequestOptions<sup>11+</sup>

请求策略。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                   | 类型                              | 可读 | 可写 | 说明                                              |
| ---------------------- |---------------------------------| ---- |---- | ------------------------------------------------ |
| sourceMode           | [SourceMode](#sourcemode11)     | 是   | 是   | 资源文件的读取类型，可以指定当前请求获取的是源文件，或是编辑后的文件。**系统接口**：此接口为系统接口。 |

## PhotoProxy<sup>11+</sup>

照片代理，相机应用通过该对象写入图片数据。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

## MediaChangeRequest<sup>11+</sup>

媒体变更请求，资产变更请求和相册变更请求的父类型。

**注意**：媒体变更请求需要在调用[applyChanges](js-apis-photoAccessHelper.md#applychanges11)后才会提交生效。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

## FormInfo<sup>11+</sup>

图库卡片相关信息。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                   | 类型                | 必填 | 说明                                              |
| ---------------------- | ------------------- | ---- | ------------------------------------------------ |
|formId       |string  |是 | 卡片的ID，由图库创建卡片时提供。 |
|uri          |string  |是 | 卡片绑定的图片的uri。创建卡片时uri可为空或图片的uri，移除卡片时uri不做校验，传空即可。  |

## ResourceType<sup>11+</sup>

枚举，写入资源的类型。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称  |  值 |  说明 |
| ----- |  ---- |  ---- |
| PHOTO_PROXY |  3 |  表示照片代理资源。**系统接口**：此接口为系统接口。 |

## DefaultChangeUri

枚举，DefaultChangeUri子类型。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称              | 值                      | 说明                                                         |
| ----------------- | ----------------------- | ------------------------------------------------------------ |
| DEFAULT_HIDDEN_ALBUM_URI<sup>11+</sup>  | 'file://media/HiddenAlbum' | 隐藏相册-相册视图中相册的Uri，即系统中包含隐藏文件的相册（不包含系统预置隐藏相册和回收站相册）的Uri，仅用于隐藏相册-相册视图场景的通知。**系统接口**：此接口为系统接口。 |

## SourceMode<sup>11+</sup>

枚举，资源文件的读取类型。

**系统接口**：此接口为系统接口。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称  |  值 |  说明 |
| ----- |  ---- |  ---- |
| ORIGINAL_MODE |  0 |  读取源文件。 |
| EDITED_MODE |  1 |  读取编辑后的文件。|

## AnalysisType<sup>11+</sup>

枚举，智慧分析类型。

**系统能力**：SystemCapability.FileManagement.PhotoAccessHelper.Core

| 名称                            | 值  | 说明       |
| :---------------------------- | :- | :------- |
| ANALYSIS\_AESTHETICS\_SCORE   | 0  | 美学评分分析类别。**系统接口**：此接口为系统接口。    |
| ANALYSIS\_LABEL               | 1  | 分类标签分析类别。**系统接口**：此接口为系统接口。    |
| ANALYSIS\_OCR                 | 2  | 文字识别分析类别。**系统接口**：此接口为系统接口。    |
| ANALYSIS\_FACE                | 3  | 人脸检测分析类别。**系统接口**：此接口为系统接口。    |
| ANALYSIS\_OBJECT              | 4  | 目标检测分析类别。**系统接口**：此接口为系统接口。    |
| ANALYSIS\_RECOMMENDATION      | 5  | 推荐构图分析类别。**系统接口**：此接口为系统接口。    |
| ANALYSIS\_SEGMENTATION        | 6  | 抠图分析类别。**系统接口**：此接口为系统接口。    |
| ANALYSIS\_COMPOSITION         | 7  | 美学构图分析类别。**系统接口**：此接口为系统接口。   |
| ANALYSIS\_SALIENCY            | 8  | 最佳呈现主体中心分析类别。**系统接口**：此接口为系统接口。   |
| ANALYSIS\_DETAIL\_ADDRESS     | 9  | 详细地址分析类别。**系统接口**：此接口为系统接口。    |