# @ohos.multimedia.medialibrary (媒体库管理)

> **说明：**
>
> - 该组件从API version 6开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。
> - 本模块从API version 9开始废弃。对应的替代接口请参考具体接口说明。

## 导入模块

```ts
import mediaLibrary from '@ohos.multimedia.mediaLibrary';
```

## mediaLibrary.getMediaLibrary<sup>8+</sup>

getMediaLibrary(context: Context): MediaLibrary

获取媒体库的实例，用于访问和修改用户等个人媒体数据信息（如音频、视频、图片、文档等）。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[getPhotoAccessHelper](js-apis-photoAccessHelper.md#photoaccesshelpergetphotoaccesshelper)替代。

**模型约束**：此接口仅可在Stage模型下使用。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名  | 类型    | 必填 | 说明                       |
| ------- | ------- | ---- | -------------------------- |
| context | Context | 是   | 传入Ability实例的Context。 |

**返回值：**

| 类型                            | 说明    |
| ----------------------------- | :---- |
| [MediaLibrary](#medialibrary) | 媒体库实例。 |

**示例：**

```ts
// 获取mediaLibrary实例，后续用到此实例均采用此处获取的实例。
const context = getContext(this);
let media: mediaLibrary.MediaLibrary = mediaLibrary.getMediaLibrary(context);
```

## mediaLibrary.getMediaLibrary

getMediaLibrary(): MediaLibrary

获取媒体库的实例，用于访问和修改用户等个人媒体数据信息（如音频、视频、图片、文档等）。

> **说明：**
>
> 此接口从API version 9开始废弃。无替代接口。

**模型约束**：此接口仅可在FA模型下使用。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**返回值：**

| 类型                          | 说明       |
| ----------------------------- | :--------- |
| [MediaLibrary](#medialibrary) | 媒体库实例。 |

**示例：**

```ts
let media: mediaLibrary.MediaLibrary = mediaLibrary.getMediaLibrary();
```

## MediaLibrary

### getFileAssets<sup>7+</sup>

getFileAssets(options: MediaFetchOptions, callback: AsyncCallback&lt;FetchFileResult&gt;): void 

获取文件资源，使用callback方式返回异步结果。

> **说明：**
>
> - 此接口从API version 9开始废弃。请使用[getAssets](js-apis-photoAccessHelper.md#getassets)替代。
> - 在API version 10上，摒弃了物理目录作为相册的设计，采用了逻辑相册的设计，一个相册中可以添加多个文件，一个文件也可以在多个相册中呈现。新的设计将带来parent、albumId、albumUri和albumName属性使用上的不兼容，无法作为MediaFetchOptions的参数在getFileAssets接口中使用。

**需要权限**：ohos.permission.READ_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名   | 类型                                                | 必填 | 说明                              |
| -------- | --------------------------------------------------- | ---- | --------------------------------- |
| options  | [MediaFetchOptions](#mediafetchoptions7)            | 是   | 文件检索选项。                      |
| callback | AsyncCallback<[FetchFileResult](#fetchfileresult7)> | 是   | callback返回文件检索结果集。 |

**示例：**

```ts
async function example() {
  // 创建文件获取选项，此处参数为获取image类型的文件资源。
  let imagesFetchOp: mediaLibrary.MediaFetchOptions = {
    selections: mediaLibrary.FileKey.MEDIA_TYPE + '= ?',
    selectionArgs: [mediaLibrary.MediaType.IMAGE.toString()],
  };
  // 获取文件资源，使用callback方式返回异步结果。
  media.getFileAssets(imagesFetchOp, async (error, fetchFileResult) => {
    // 判断获取的文件资源的检索结果集是否为undefined，若为undefined则接口调用失败。
    if (fetchFileResult == undefined) {
      console.error('get fetchFileResult failed with error: ' + error);
      return;
    }
    // 获取文件检索结果集中的总数。
    const count = fetchFileResult.getCount();
    // 判断结果集中的数量是否小于0，小于0时表示接口调用失败。
    if (count < 0) {
      console.error('get count from fetchFileResult failed, count: ' + count);
      return;
    }
    // 判断结果集中的数量是否等于0，等于0时表示接口调用成功，但是检索结果集为空，请检查文件获取选项参数配置是否有误和设备中是否存在相应文件。
    if (count == 0) {
      console.info('The count of fetchFileResult is zero');
      return;
    }
    console.info('Get fetchFileResult successfully, count: ' + count);
    // 获取文件检索结果集中的第一个资源，使用callback方式返回异步结果，文件数量较多时请使用getAllObject接口。
    fetchFileResult.getFirstObject(async (error, fileAsset) => {
      // 检查获取的第一个资源是否为undefined，若为undefined则接口调用失败。
      if (fileAsset == undefined) {
        console.error('get first object failed with error: ' + error);
        return;
      }
      console.info('fileAsset.displayName ' + '0 : ' + fileAsset.displayName);
      // 调用 getNextObject 接口获取下一个资源，直到最后一个。
      for (let i = 1; i < count; i++) {
        let fileAsset = await fetchFileResult.getNextObject();
        console.info('fileAsset.displayName ' + i + ': ' + fileAsset.displayName);
      }
      // 释放FetchFileResult实例并使其失效。无法调用其他方法。
      fetchFileResult.close();
    });
  });
}
```

### getFileAssets<sup>7+</sup>

getFileAssets(options: MediaFetchOptions): Promise&lt;FetchFileResult&gt;

获取文件资源，使用Promise方式返回结果。

> **说明：**
>
> - 此接口从API version 9开始废弃。请使用[getAssets](js-apis-photoAccessHelper.md#getassets-1)替代。
> - 在API version 10上，摒弃了物理目录作为相册的设计，采用了逻辑相册的设计，一个相册中可以添加多个文件，一个文件也可以在多个相册中呈现。新的设计将带来parent、albumId、albumUri和albumName属性使用上的不兼容，无法作为MediaFetchOptions的参数在getFileAssets接口中使用。

**需要权限**：ohos.permission.READ_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名  | 类型                                     | 必填 | 说明         |
| ------- | ---------------------------------------- | ---- | ------------ |
| options | [MediaFetchOptions](#mediafetchoptions7) | 是   | 文件检索选项。 |

**返回值：**

| 类型                                 | 说明           |
| ------------------------------------ | -------------- |
| Promise&lt;[FetchFileResult](#fetchfileresult7)&gt; | Promise对象，返回文件检索结果集。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  // 创建文件获取选项，此处参数为获取image类型的文件资源。
  let imagesFetchOp: mediaLibrary.MediaFetchOptions = {
    selections: mediaLibrary.FileKey.MEDIA_TYPE + '= ?',
    selectionArgs: [mediaLibrary.MediaType.IMAGE.toString()],
  };
  // 获取文件资源，使用Promise方式返回结果。
  media.getFileAssets(imagesFetchOp).then(async (fetchFileResult) => {
    // 获取文件检索结果集中的总数。
    const count = fetchFileResult.getCount();
    // 判断结果集中的数量是否小于0，小于0时表示接口调用失败。
    if (count < 0) {
      console.error('get count from fetchFileResult failed, count: ' + count);
      return;
    }
    // 判断结果集中的数量是否等于0，等于0时表示接口调用成功，但是检索结果集为空，请检查文件获取选项参数配置是否有误和设备中是否存在相应文件。
    if (count == 0) {
      console.info('The count of fetchFileResult is zero');
      return;
    }
    console.info('Get fetchFileResult successfully, count: ' + count);
    // 获取文件检索结果集中的第一个资源，使用Promise方式返回异步结果，文件数量较多时请使用getAllObject接口。
    fetchFileResult.getFirstObject().then(async (fileAsset) => {
      console.info('fileAsset.displayName ' + '0 : ' + fileAsset.displayName);
      // 调用 getNextObject 接口获取下一个资源，直到最后一个。
      for (let i = 1; i < count; i++) {
        let fileAsset = await fetchFileResult.getNextObject();
        console.info('fileAsset.displayName ' + i + ': ' + fileAsset.displayName);
      }
      // 释放FetchFileResult实例并使其失效。无法调用其他方法。
      fetchFileResult.close();
    }).catch((error: BusinessError) => {
      // 调用getFirstObject接口失败。
      console.error('get first object failed with error: ' + error);
    });
  }).catch((error: BusinessError) => {
    // 调用getFileAssets接口失败。
    console.error('get file assets failed with error: ' + error);
  });
}
```

### on<sup>8+</sup>

on(type: 'deviceChange'&#124;'albumChange'&#124;'imageChange'&#124;'audioChange'&#124;'videoChange'&#124;'fileChange'&#124;'remoteFileChange', callback: Callback&lt;void&gt;): void

打开媒体库变更通知，使用callback方式返回异步结果。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[registerChange](js-apis-photoAccessHelper.md#registerchange)替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名      | 类型                   | 必填   | 说明                                       |
| -------- | -------------------- | ---- | ---------------------------------------- |
| type     | 'deviceChange'&#124;<br/>'albumChange'&#124;<br/>'imageChange'&#124;<br/>'audioChange'&#124;<br/>'videoChange'&#124;<br/>'fileChange'&#124;<br/>'remoteFileChange'               | 是    | 媒体类型 <br/>'deviceChange'：&nbsp;注册设备变更 <br/>'albumChange'：&nbsp;相册变更<br/>'imageChange'：&nbsp;图片文件变更<br/>'audioChange'： &nbsp;音频文件变更<br/>'videoChange'：  &nbsp;视频文件变更<br/>'fileChange'：     &nbsp;文件变更<br/>'remoteFileChange'：&nbsp;注册设备上文件变更。 |
| callback | Callback&lt;void&gt; | 是    | callbac返回空。                                    |

**示例：**

```ts
media.on('imageChange', () => {
  // image file had changed, do something.
});
```

### off<sup>8+</sup>

off(type: 'deviceChange'&#124;'albumChange'&#124;'imageChange'&#124;'audioChange'&#124;'videoChange'&#124;'fileChange'&#124;'remoteFileChange', callback?: Callback&lt;void&gt;): void

关闭媒体库变更通知，使用callback方式返回异步结果。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[unRegisterChange](js-apis-photoAccessHelper.md#unregisterchange)替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名      | 类型                   | 必填   | 说明                                       |
| -------- | -------------------- | ---- | ---------------------------------------- |
| type     | 'deviceChange'&#124;<br/>'albumChange'&#124;<br/>'imageChange'&#124;<br/>'audioChange'&#124;<br/>'videoChange'&#124;<br/>'fileChange'&#124;<br/>'remoteFileChange'               | 是    | 媒体类型 <br/>'deviceChange'：&nbsp;注册设备变更 <br/>'albumChange'：&nbsp;相册变更<br/>'imageChange'：&nbsp;图片文件变更<br/>'audioChange'： &nbsp;音频文件变更<br/>'videoChange'：  &nbsp;视频文件变更<br/>'fileChange'：     &nbsp;文件变更<br/>'remoteFileChange'：&nbsp;注册设备上文件变更。 |
| callback | Callback&lt;void&gt; | 否    | callback返回空。                                    |

**示例：**

```ts
media.off('imageChange', () => {
  // stop listening successfully.
});
```

### createAsset<sup>8+</sup>

createAsset(mediaType: MediaType, displayName: string, relativePath: string, callback: AsyncCallback&lt;FileAsset&gt;): void

创建媒体资源，使用callback方式返回结果。

> **说明：**
>
> - 此接口从API version 9开始废弃。请使用[createAsset](js-apis-photoAccessHelper.md#createasset)替代。
> - 由于API version 10的SDK上relativePath和相册没有关联关系，文件创建成功后，relativePath的最后一级目录不会作为相册呈现。

**需要权限**：ohos.permission.READ_MEDIA, ohos.permission.WRITE_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名       | 类型                                    | 必填 | 说明                                                         |
| ------------ | --------------------------------------- | ---- | ------------------------------------------------------------ |
| mediaType    | [MediaType](#mediatype8)                | 是   | 媒体类型。                                                     |
| displayName  | string                                  | 是   | 展示文件名。                                                   |
| relativePath | string                                  | 是   | 文件保存路径，可以通过[getPublicDirectory](#getpublicdirectory8)获取不同类型文件的保存路径。 |
| callback     | AsyncCallback<[FileAsset](#fileasset7)> | 是   | callback返回创建的媒体资源FileAsset对象。                          |

**示例：**

```ts
async function example() {
  // 使用Callback方式创建Image类型文件。
  let mediaType = mediaLibrary.MediaType.IMAGE;
  let DIR_IMAGE = mediaLibrary.DirectoryType.DIR_IMAGE;
  const path = await media.getPublicDirectory(DIR_IMAGE);
  media.createAsset(mediaType, 'imageCallBack.jpg', path + 'myPicture/', (error, fileAsset) => {
    if (fileAsset != undefined) {
      console.info('createAsset successfully, message');
    } else {
      console.error('createAsset failed with error: ' + error);
    }
  });
}
```

### createAsset<sup>8+</sup>

createAsset(mediaType: MediaType, displayName: string, relativePath: string): Promise&lt;FileAsset&gt;

创建媒体资源，使用Promise方式返回结果。

> **说明：**
>
> - 此接口从API version 9开始废弃。请使用[createAsset](js-apis-photoAccessHelper.md#createasset-1)替代。
> - 由于API version 10的SDK上relativePath和相册没有关联关系，文件创建成功后，relativePath的最后一级目录不会作为相册呈现。

**需要权限**：ohos.permission.READ_MEDIA, ohos.permission.WRITE_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名       | 类型                     | 必填 | 说明                                                         |
| ------------ | ------------------------ | ---- | ------------------------------------------------------------ |
| mediaType    | [MediaType](#mediatype8) | 是   | 媒体类型。                                                     |
| displayName  | string                   | 是   | 展示文件名。                                                   |
| relativePath | string                   | 是   | 相对路径，可以通过getPublicDirectory获取不同类型媒体文件的一层目录的relative path。 |

**返回值：**

| 类型                     | 说明              |
| ------------------------ | ----------------- |
| Promise&lt;[FileAsset](#fileasset7)&gt; | Promise对象，返回创建媒体数据的FileAsset。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  // 使用Promise方式创建Image类型文件。
  let mediaType = mediaLibrary.MediaType.IMAGE;
  let DIR_IMAGE = mediaLibrary.DirectoryType.DIR_IMAGE;
  const path = await media.getPublicDirectory(DIR_IMAGE);
  media.createAsset(mediaType, 'imagePromise.jpg', path + 'myPicture/').then((fileAsset) => {
    console.info('createAsset successfully, message = ' + JSON.stringify(fileAsset));
  }).catch((error: BusinessError) => {
    console.error('createAsset failed with error: ' + error);
  });
}
```

### getPublicDirectory<sup>8+</sup>

getPublicDirectory(type: DirectoryType, callback: AsyncCallback&lt;string&gt;): void

获取公共目录路径，使用callback方式返回结果。

> **说明：**
>
> 此接口从API version 9开始废弃。无替代接口。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名   | 类型                             | 必填 | 说明                      |
| -------- | -------------------------------- | ---- | ------------------------- |
| type     | [DirectoryType](#directorytype8) | 是   | 公共目录类型。              |
| callback | AsyncCallback&lt;string&gt;      | 是   | callback返回公共目录路径。 |

**示例：**

```ts
let DIR_CAMERA = mediaLibrary.DirectoryType.DIR_CAMERA;
media.getPublicDirectory(DIR_CAMERA, (error, dicResult) => {
  if (dicResult == 'Camera/') {
    console.info('getPublicDirectory DIR_CAMERA successfully');
  } else {
    console.error('getPublicDirectory DIR_CAMERA failed with error: ' + error);
  }
});
```

### getPublicDirectory<sup>8+</sup>

getPublicDirectory(type: DirectoryType): Promise&lt;string&gt;

获取公共目录路径，使用Promise方式返回结果。

> **说明：**
>
> 此接口从API version 9开始废弃。无替代接口。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名 | 类型                             | 必填 | 说明         |
| ------ | -------------------------------- | ---- | ------------ |
| type   | [DirectoryType](#directorytype8) | 是   | 公共目录类型。 |

**返回值：**

| 类型             | 说明             |
| ---------------- | ---------------- |
| Promise\<string> | Promise对象，返回公共目录路径。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  let DIR_CAMERA = mediaLibrary.DirectoryType.DIR_CAMERA;
  media.getPublicDirectory(DIR_CAMERA).then((dicResult) => {
    if (dicResult == 'Camera/') {
      console.info('getPublicDirectory DIR_CAMERA successfully');
    } else {
      console.error('getPublicDirectory DIR_CAMERA failed');
    }
  }).catch((error: BusinessError) => {
    console.error('getPublicDirectory failed with error: ' + error);
  });
}
```

### getAlbums<sup>7+</sup>

getAlbums(options: MediaFetchOptions, callback: AsyncCallback&lt;Array&lt;Album&gt;&gt;): void

获取相册列表，使用callback 方式返回结果。

> **说明：**
>
> - 此接口从API version 9开始废弃。请使用[getAlbums](js-apis-photoAccessHelper.md#getalbums)替代。
> - 由于API version 10的SDK上relativePath和相册没有关联关系，在使用getAlbums时不支持relativePath作为查询条件，当前仅支持“Camera”和“ScreenShots”两类相册。

**需要权限**：ohos.permission.READ_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名   | 类型                                         | 必填 | 说明                        |
| -------- | -------------------------------------------- | ---- | --------------------------- |
| options  | [MediaFetchOptions](#mediafetchoptions7)     | 是   | 相册检索条件。                |
| callback | AsyncCallback&lt;Array<[Album](#album7)>&gt; | 是   | callback返回获取的Album结果集。 |

**示例：**

```ts
async function example() {
  let albumFetchOp: mediaLibrary.MediaFetchOptions = {
    selections: mediaLibrary.FileKey.ALBUM_NAME + '= ?',
    selectionArgs: ['Camera'],
  };
  media.getAlbums(albumFetchOp, (error, albumList) => {
    if (albumList != undefined) {
      console.info('getAlbums successfully: ' + JSON.stringify(albumList));
    } else {
      console.error('getAlbums failed with error: ' + error);
    }
  });
}
```

### getAlbums<sup>7+</sup>

getAlbums(options: MediaFetchOptions): Promise&lt;Array&lt;Album&gt;&gt;

获取相册列表，使用 promise 方式返回结果。

> **说明：**
>
> - 此接口从API version 9开始废弃。请使用[getAlbums](js-apis-photoAccessHelper.md#getalbums-2)替代。
> - 由于API version 10的SDK上relativePath和相册没有关联关系，在使用getAlbums时不支持relativePath作为查询条件.当前仅支持“Camera”和“ScreenShots”两类相册。

**需要权限**：ohos.permission.READ_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名  | 类型                                     | 必填 | 说明         |
| ------- | ---------------------------------------- | ---- | ------------ |
| options | [MediaFetchOptions](#mediafetchoptions7) | 是   | 相册获取条件。 |

**返回值：**

| 类型                             | 说明          |
| -------------------------------- | ------------- |
| Promise<Array<[Album](#album7)>> | Promise对象，返回获取的Album结果集。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  let albumFetchOp: mediaLibrary.MediaFetchOptions = {
    selections: mediaLibrary.FileKey.ALBUM_NAME + '= ?',
    selectionArgs: ['Camera'],
  };
  media.getAlbums(albumFetchOp).then((albumList) => {
    console.info('getAlbums successfully: ' + JSON.stringify(albumList));
  }).catch((error: BusinessError) => {
    console.error('getAlbums failed with error: ' + error);
  });
}
```

### release<sup>8+</sup>

release(callback: AsyncCallback&lt;void&gt;): void

释放MediaLibrary实例。
当后续不需要使用MediaLibrary实例中的方法时调用。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[release](js-apis-photoAccessHelper.md#release)替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名      | 类型                        | 必填   | 说明         |
| -------- | ------------------------- | ---- | ---------- |
| callback | AsyncCallback&lt;void&gt; | 是    | callback返回空。 |

**示例：**

```ts
media.release(() => {
  // do something.
});
```

### release<sup>8+</sup>

release(): Promise&lt;void&gt;

释放MediaLibrary实例。
当后续不需要使用MediaLibrary实例中的方法时调用。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[release](js-apis-photoAccessHelper.md#release-1)替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**返回值：**

| 类型                  | 说明                   |
| ------------------- | -------------------- |
| Promise&lt;void&gt; | Promise对象，返回空。 |

**示例：**

```ts
media.release();
```

### storeMediaAsset

storeMediaAsset(option: MediaAssetOption, callback: AsyncCallback&lt;string&gt;): void

保存媒体资源，以异步方法获取保存成功的URI，使用callback形式返回结果。

> **说明：**
>
> - 此接口为API version 6开始支持，只支持FA模型使用。
> - 此接口从API version 9开始废弃。请使用[save](../apis-core-file-kit/js-apis-file-picker.md#save-1)接口替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名      | 类型                                    | 必填   | 说明                      |
| -------- | ------------------------------------- | ---- | ----------------------- |
| option   | [MediaAssetOption](#mediaassetoption) | 是    | 媒体资源选项。                 |
| callback | AsyncCallback&lt;string&gt;           | 是    | callback返回保存媒体资源成功后得到的URI。 |

**示例：**

```ts
let option: mediaLibrary.MediaAssetOption = {
  src : '/data/storage/el2/base/haps/entry/image.png',
  mimeType : 'image/*',
  relativePath : 'Pictures/'
};
mediaLibrary.getMediaLibrary().storeMediaAsset(option, (error, value) => {
  if (error) {
    console.error('storeMediaAsset failed with error: ' + error);
    return;
  }
  console.info('Media resources stored. ');
  // Obtain the URI that stores media resources.
});
```

### storeMediaAsset

storeMediaAsset(option: MediaAssetOption): Promise&lt;string&gt;

保存媒体资源，以异步方法获取保存成功的URI，使用Promise形式返回结果。

> **说明：**
>
> - 此接口为API version 6开始支持，只支持FA模型使用。
> - 此接口从API version 9开始废弃。请使用[save](../apis-core-file-kit/js-apis-file-picker.md#save)接口替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名    | 类型                                    | 必填   | 说明      |
| ------ | ------------------------------------- | ---- | ------- |
| option | [MediaAssetOption](#mediaassetoption) | 是    | 媒体资源选项。 |

**返回值：**

| 类型                    | 说明                           |
| --------------------- | ---------------------------- |
| Promise&lt;string&gt; | Promise对象，返回保存媒体资源成功后得到的URI。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let option: mediaLibrary.MediaAssetOption = {
  src : '/data/storage/el2/base/haps/entry/image.png',
  mimeType : 'image/*',
  relativePath : 'Pictures/'
};
mediaLibrary.getMediaLibrary().storeMediaAsset(option).then((value) => {
  console.info('Media resources stored.');
  // Obtain the URI that stores media resources.
}).catch((error: BusinessError) => {
  console.error('storeMediaAsset failed with error: ' + error);
});
```

### startImagePreview

startImagePreview(images: Array&lt;string&gt;, index: number, callback: AsyncCallback&lt;void&gt;): void

启动图片预览界面并限定预览开始显示的图片。可以预览指定序号的单张本地图片（file://），也可以预览列表中的所有网络图片（https://）。使用callback方式进行异步回调。

> **说明：**
>
> - 此接口为API version 6开始支持，只支持FA模型使用。
> - 此接口从API version 9开始废弃。建议使用[Image组件](../apis-arkui/arkui-ts/ts-basic-components-image.md)替代。<br/>Image组件，可用于本地图片和网络图片的渲染展示。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名      | 类型                        | 必填   | 说明                                       |
| -------- | ------------------------- | ---- | ---------------------------------------- |
| images   | Array&lt;string&gt;       | 是    | 预览的图片URI（'https://'，'file://'）列表。 |
| index    | number                    | 是    | 开始显示的图片序号。                               |
| callback | AsyncCallback&lt;void&gt; | 是    | callback返回空。                        |

**示例：**

```ts
let images = [
  'file://media/xxxx/2',
  'file://media/xxxx/3'
];
/* 网络图片使用方式。
let images = [
  'https://media.xxxx.com/image1.jpg',
  'https://media.xxxx.com/image2.jpg'
];
*/
let index = 1;
mediaLibrary.getMediaLibrary().startImagePreview(images, index, (error) => {
  if (error) {
    console.error('startImagePreview failed with error: ' + error);
    return;
  }
  console.info('Succeeded in previewing the images.');
});
```

### startImagePreview

startImagePreview(images: Array&lt;string&gt;, callback: AsyncCallback&lt;void&gt;): void

启动图片预览界面，可以预览列表中首张本地图片（file://），也可以预览列表中的所有网络图片（https://）。使用callback方式进行异步回调。

> **说明：**
>
> - 此接口为API version 6开始支持，只支持FA模型使用。
> - 此接口从API version 9开始废弃。建议使用[Image组件](../apis-arkui/arkui-ts/ts-basic-components-image.md)替代。<br/>Image组件，可用于本地图片和网络图片的渲染展示。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名      | 类型                        | 必填   | 说明                                       |
| -------- | ------------------------- | ---- | ---------------------------------------- |
| images   | Array&lt;string&gt;       | 是    | 预览的图片URI（'https://'，'file://'）列表。 |
| callback | AsyncCallback&lt;void&gt; | 是    | callback返回空。                        |

**示例：**

```ts
let images = [
  'file://media/xxxx/2',
  'file://media/xxxx/3'
];
/* 网络图片使用方式。
let images = [
  'https://media.xxxx.com/image1.jpg',
  'https://media.xxxx.com/image2.jpg'
];
*/
mediaLibrary.getMediaLibrary().startImagePreview(images, (error) => {
  if (error) {
    console.error('startImagePreview failed with error: ' + error);
    return;
  }
  console.info('Succeeded in previewing the images.');
});
```

### startImagePreview

startImagePreview(images: Array&lt;string&gt;, index?: number): Promise&lt;void&gt;

启动图片预览界面并限定预览开始显示的图片。可以预览指定序号的单张本地图片（file://），也可以预览列表中的所有网络图片（https://）。使用Promise方式进行异步回调。

> **说明：**
>
> - 此接口为API version 6开始支持，只支持FA模型使用。
> - 此接口从API version 9开始废弃。建议使用[Image组件](../apis-arkui/arkui-ts/ts-basic-components-image.md)替代。<br/>Image组件，可用于本地图片和网络图片的渲染展示。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名    | 类型                  | 必填   | 说明                                       |
| ------ | ------------------- | ---- | ---------------------------------------- |
| images | Array&lt;string&gt; | 是    | 预览的图片URI（'https://'，'file://'）列表。 |
| index  | number              | 否    | 开始显示的图片序号，不选择时默认为0。                      |

**返回值：**

| 类型                  | 说明                              |
| ------------------- | ------------------------------- |
| Promise&lt;void&gt; | Promise对象，返回空。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let images = [
  'file://media/xxxx/2',
  'file://media/xxxx/3'
];
/* 网络图片使用方式。
let images = [
  'https://media.xxxx.com/image1.jpg',
  'https://media.xxxx.com/image2.jpg'
];
*/
let index = 1;
mediaLibrary.getMediaLibrary().startImagePreview(images, index).then(() => {
  console.info('Succeeded in previewing the images.');
}).catch((error: BusinessError) => {
  console.error('startImagePreview failed with error: ' + error);
});
```

### startMediaSelect

startMediaSelect(option: MediaSelectOption, callback: AsyncCallback&lt;Array&lt;string&gt;&gt;): void

启动媒体选择界面，以异步方法获取选择的媒体URI列表，使用callback形式返回结果。

> **说明：**
>
> - 此接口为API version 6开始支持，只支持FA模型使用。
> - 此接口从API version 9开始废弃。请使用[select](../apis-core-file-kit/js-apis-file-picker.md#select-1)接口替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名      | 类型                                       | 必填   | 说明                                   |
| -------- | ---------------------------------------- | ---- | ------------------------------------ |
| option   | [MediaSelectOption](#mediaselectoption)  | 是    | 媒体选择选项。                              |
| callback | AsyncCallback&lt;Array&lt;string&gt;&gt; | 是    | callback返回选择的媒体URI列表。 |

**示例：**

```ts
let option : mediaLibrary.MediaSelectOption = {
  type : 'media',
  count : 2
};
mediaLibrary.getMediaLibrary().startMediaSelect(option, (error, value) => {
  if (error) {
    console.error('startMediaSelect failed with error: ' + error);
    return;
  }
  console.info('Media resources selected.');
  // Obtain the media selection value.
});
```

### startMediaSelect

startMediaSelect(option: MediaSelectOption): Promise&lt;Array&lt;string&gt;&gt;

启动媒体选择界面，以异步方法获取选择的媒体URI列表，使用Promise形式返回结果。

> **说明：**
>
> - 此接口为API version 6开始支持，只支持FA模型使用。
> - 此接口从API version 9开始废弃。请使用[select](../apis-core-file-kit/js-apis-file-picker.md#select)接口替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名    | 类型                                      | 必填   | 说明      |
| ------ | --------------------------------------- | ---- | ------- |
| option | [MediaSelectOption](#mediaselectoption) | 是    | 媒体选择选项。 |

**返回值：**

| 类型                                 | 说明                                       |
| ---------------------------------- | ---------------------------------------- |
| Promise&lt;Array&lt;string&gt;&gt; | Promise对象，返回选择的媒体URI列表。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

let option : mediaLibrary.MediaSelectOption = {
  type : 'media',
  count : 2
};
mediaLibrary.getMediaLibrary().startMediaSelect(option).then((value) => {
  console.info('Media resources selected.');
  // Obtain the media selection value.
}).catch((error: BusinessError) => {
  console.error('startMediaSelect failed with error: ' + error);
});
```

## FileAsset<sup>7+</sup>

提供封装文件属性的方法。

> **说明：**
>
> - title字段默认为去掉后缀的文件名，音频和视频文件会尝试解析文件内容，部分设备写入后在触发扫描时会被还原。
> - orientation字段部分设备可能不支持修改，建议使用[ImageSource.modifyImageProperty](../apis-image-kit/js-apis-image.md#modifyimagepropertydeprecated)接口。
> - 此接口从API version 9开始废弃。请使用[PhotoAsset](js-apis-photoAccessHelper.md#photoasset)替代。

### 属性

**系统能力：** 以下各项对应的系统能力均为SystemCapability.Multimedia.MediaLibrary.Core

| 名称                      | 类型                     | 可读 | 可写 | 说明                                                   |
| ------------------------- | ------------------------ | ---- | ---- | ------------------------------------------------------ |
| id                        | number                   | 是   | 否   | 文件资源编号。                                           |
| uri                       | string                   | 是   | 否   | 文件资源uri（如：file://media/image/2)。         |
| mimeType                  | string                   | 是   | 否   | 文件扩展属性。                                           |
| mediaType<sup>8+</sup>    | [MediaType](#mediatype8) | 是   | 否   | 媒体类型。                                               |
| displayName               | string                   | 是   | 是   | 显示文件名，包含后缀名。                                 |
| title                     | string                   | 是   | 是   | 文件标题。                                               |
| relativePath<sup>8+</sup> | string                   | 是   | 是   | 相对公共目录路径。                                       |
| parent<sup>8+</sup>       | number                   | 是   | 否   | 父目录id。由于API version 10的SDK上Asset可以存在多个相册，该属性不兼容。获取值始终为0。                        |
| size                      | number                   | 是   | 否   | 文件大小（单位：字节）。                                 |
| dateAdded                 | number                   | 是   | 否   | 添加日期（添加文件时间到1970年1月1日的秒数值）。         |
| dateModified              | number                   | 是   | 否   | 修改日期（修改文件时间到1970年1月1日的秒数值，修改文件名不会改变此值，当文件内容发生修改时才会更新）。|
| dateTaken                 | number                   | 是   | 否   | 拍摄日期（文件拍照时间到1970年1月1日的秒数值）。         |
| artist<sup>8+</sup>       | string                   | 是   | 否   | 作者。                                                   |
| audioAlbum<sup>8+</sup>   | string                   | 是   | 否   | 专辑。                                                   |
| width                     | number                   | 是   | 否   | 图片宽度（单位：像素）。                                 |
| height                    | number                   | 是   | 否   | 图片高度（单位：像素）。                                 |
| orientation               | number                   | 是   | 是   | 图片显示方向（顺时针旋转角度，如0，90，180  单位：度）。 |
| duration<sup>8+</sup>     | number                   | 是   | 否   | 持续时间（单位：毫秒）。                                   |
| albumId                   | number                   | 是   | 否   | 文件所归属的相册编号。由于API version 10的SDK上Asset可以存在多个相册，该属性不兼容。获取值始终为0。                   |
| albumUri<sup>8+</sup>     | string                   | 是   | 否   | 文件所归属相册uri。由于API version 10的SDK上Asset可以存在多个相册，该属性不兼容。获取值始终为空字符串。                      |
| albumName                 | string                   | 是   | 否   | 文件所归属相册名称。由于API version 10的SDK上Asset可以存在多个相册，该属性不兼容。获取值始终为空字符串。                     |

### isDirectory<sup>8+</sup>

isDirectory(callback: AsyncCallback&lt;boolean&gt;): void

判断fileAsset是否为目录，使用callback方式返回异步结果。

> **说明：**
>
> 此接口从API version 9开始废弃。无替代接口。

**需要权限**：ohos.permission.READ_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名      | 类型                           | 必填   | 说明                  |
| -------- | ---------------------------- | ---- | ------------------- |
| callback | AsyncCallback&lt;boolean&gt; | 是    | callback返回boolean值，值为true则是目录，值为false则非目录。 |

**示例：**

```ts
async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  const fetchFileResult = await media.getFileAssets(getImageOp);
  const asset = await fetchFileResult.getFirstObject();
  asset.isDirectory((error, isDirectory) => {
    if (error) {
      console.error('isDirectory failed with error: ' + error);
    } else {
      console.info('isDirectory result:' + isDirectory);
    }
  });
  fetchFileResult.close();
}
```

### isDirectory<sup>8+</sup>

isDirectory():Promise&lt;boolean&gt;

判断fileAsset是否为目录，使用Promise方式返回异步结果。

> **说明：**
>
> 此接口从API version 9开始废弃。无替代接口。

**需要权限**：ohos.permission.READ_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**返回值：**

| 类型                     | 说明                           |
| ---------------------- | ---------------------------- |
| Promise&lt;boolean&gt; | Promise对象，返回boolean值，值为true则是目录，值为false则非目录。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  const fetchFileResult = await media.getFileAssets(getImageOp);
  const asset = await fetchFileResult.getFirstObject();
  asset.isDirectory().then((isDirectory) => {
    console.info('isDirectory result:' + isDirectory);
  }).catch((error: BusinessError) => {
    console.error('isDirectory failed with error: ' + error);
  });
  fetchFileResult.close();
}
```

### commitModify<sup>8+</sup>

commitModify(callback: AsyncCallback&lt;void&gt;): void

修改文件的元数据，使用callback方式返回异步结果。

> **说明：**
>
> - 此接口从API version 9开始废弃。请使用[commitModify](js-apis-photoAccessHelper.md#commitmodify)替代。
> - 由于API version 10的SDK上audio没有orientation属性，在使用commitModify接口时将无法对audio资源的orientation属性进行修改。

**需要权限**：ohos.permission.READ_MEDIA, ohos.permission.WRITE_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名      | 类型                        | 必填   | 说明    |
| -------- | ------------------------- | ---- | ----- |
| callback | AsyncCallback&lt;void&gt; | 是    | callback返回空。 |

**示例：**

```ts
async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  const fetchFileResult = await media.getFileAssets(getImageOp);
  const asset = await fetchFileResult.getFirstObject();
  asset.title = 'newtitle';
  asset.commitModify(() => {
    console.info('commitModify successfully');
  });
  fetchFileResult.close();
}
```

### commitModify<sup>8+</sup>

commitModify(): Promise&lt;void&gt;

修改文件的元数据，使用promise方式返回异步结果。

> **说明：**
>
> - 此接口从API version 9开始废弃。请使用[commitModify](js-apis-photoAccessHelper.md#commitmodify-1)替代。
> 由于API version 10的SDK上audio没有orientation属性，在使用commitModify接口时将无法对audio资源的orientation属性进行修改。

**需要权限**：ohos.permission.READ_MEDIA, ohos.permission.WRITE_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**返回值：**

| 类型                  | 说明         |
| ------------------- | ---------- |
| Promise&lt;void&gt; | Promise对象，返回空。 |

**示例：**

```ts
async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  const fetchFileResult = await media.getFileAssets(getImageOp);
  const asset = await fetchFileResult.getFirstObject();
  asset.title = 'newtitle';
  await asset.commitModify();
  fetchFileResult.close();
}
```

### open<sup>8+</sup>

open(mode: string, callback: AsyncCallback&lt;number&gt;): void

打开当前文件，使用callback方式返回异步结果。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[open](js-apis-photoAccessHelper.md#open)替代。

**注意**：以 'w' 模式打开文件时，返回的fd无法进行读取。但由于不同文件系统实现上的差异，部分用户态文件系统在 'w' 模式打开时会允许用fd读取。若有针对fd的读写行为，建议使用 'rw' 模式打开文件。当前写操作是互斥的操作，写操作完成后需要调用close进行释放。

**需要权限**：ohos.permission.READ_MEDIA or ohos.permission.WRITE_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名      | 类型                          | 必填   | 说明                                  |
| -------- | --------------------------- | ---- | ----------------------------------- |
| mode     | string                      | 是    | 打开文件方式，如：'r'（只读）, 'w'（只写）, 'rw'（读写）。 |
| callback | AsyncCallback&lt;number&gt; | 是    | callback返回文件描述符。                            |

**示例：**

```ts
async function example() {
  let mediaType = mediaLibrary.MediaType.IMAGE;
  let DIR_IMAGE = mediaLibrary.DirectoryType.DIR_IMAGE;
  const path = await media.getPublicDirectory(DIR_IMAGE);
  const asset = await media.createAsset(mediaType, 'image00003.jpg', path);
  asset.open('rw', (error, fd) => {
    if (fd > 0) {
      asset.close(fd);
    } else {
      console.error('File Open failed with error: ' + error);
    }
  });
}
```

### open<sup>8+</sup>

open(mode: string): Promise&lt;number&gt;

打开当前文件，使用promise方式返回异步结果。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[open](js-apis-photoAccessHelper.md#open-1)替代。

**注意**：以 'w' 模式打开文件时，返回的fd无法进行读取。但由于不同文件系统实现上的差异，部分用户态文件系统在 'w' 模式打开时会允许用fd读取。若有针对fd的读写行为，建议使用 'rw' 模式打开文件。当前写操作是互斥的操作，写操作完成后需要调用close进行释放。

**需要权限**：ohos.permission.READ_MEDIA or ohos.permission.WRITE_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名  | 类型     | 必填   | 说明                                  |
| ---- | ------ | ---- | ----------------------------------- |
| mode | string | 是    | 打开文件方式，如：'r'（只读）, 'w'（只写）, 'rw'（读写）。 |

**返回值：**

| 类型                    | 说明            |
| --------------------- | ------------- |
| Promise&lt;number&gt; | Promise对象，返回文件描述符。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  let mediaType = mediaLibrary.MediaType.IMAGE;
  let DIR_IMAGE = mediaLibrary.DirectoryType.DIR_IMAGE;
  const path = await media.getPublicDirectory(DIR_IMAGE);
  const asset = await media.createAsset(mediaType, 'image00003.jpg', path);
  asset.open('rw').then((fd) => {
    console.info('File open fd: ' + fd);
  }).catch((error: BusinessError) => {
    console.error('File open failed with error: ' + error);
  });
}
```

### close<sup>8+</sup>

close(fd: number, callback: AsyncCallback&lt;void&gt;): void

关闭当前文件，使用callback方式返回异步结果。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[close](js-apis-photoAccessHelper.md#close)替代。

**需要权限**：ohos.permission.READ_MEDIA or ohos.permission.WRITE_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名      | 类型                        | 必填   | 说明    |
| -------- | ------------------------- | ---- | ----- |
| fd       | number                    | 是    | 文件描述符。 |
| callback | AsyncCallback&lt;void&gt; | 是    | callback返回空。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  const fetchFileResult = await media.getFileAssets(getImageOp);
  const asset = await fetchFileResult.getFirstObject();
  asset.open('rw').then((fd) => {
    console.info('File open fd: ' + fd);
    asset.close(fd, (error) => {
      if (error) {
        console.error('asset.close failed with error: ' + error);
      } else {
        console.info('asset.close successfully');
      }
    });
  }).catch((error: BusinessError) => {
    console.error('File open failed with error: ' + error);
  });
  fetchFileResult.close();
}
```

### close<sup>8+</sup>

close(fd: number): Promise&lt;void&gt;

关闭当前文件，使用promise方式返回异步结果。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[close](js-apis-photoAccessHelper.md#close-1)替代。

**需要权限**：ohos.permission.READ_MEDIA or ohos.permission.WRITE_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名  | 类型     | 必填   | 说明    |
| ---- | ------ | ---- | ----- |
| fd   | number | 是    | 文件描述符。 |

**返回值：**

| 类型                  | 说明         |
| ------------------- | ---------- |
| Promise&lt;void&gt; | Promise对象，返回空。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  const fetchFileResult = await media.getFileAssets(getImageOp);
  const asset = await fetchFileResult.getFirstObject();
  asset.open('rw').then((fd) => {
    console.info('File fd!' + fd);
    asset.close(fd).then(() => {
      console.info('asset.close successfully');
    }).catch((closeErr) => {
      console.error('asset.close fail, closeErr: ' + closeErr);
    });
  }).catch((error: BusinessError) => {
    console.error('open File failed with error: ' + error);
  });
  fetchFileResult.close();
}
```

### getThumbnail<sup>8+</sup>

getThumbnail(callback: AsyncCallback&lt;image.PixelMap&gt;): void

获取文件的缩略图，使用callback方式返回异步结果。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[getThumbnail](js-apis-photoAccessHelper.md#getthumbnail)替代。

**需要权限**：ohos.permission.READ_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名      | 类型                                  | 必填   | 说明               |
| -------- | ----------------------------------- | ---- | ---------------- |
| callback | AsyncCallback&lt;image.PixelMap&gt; | 是    | callback返回缩略图的PixelMap。 |

**示例：**

```ts
async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  const fetchFileResult = await media.getFileAssets(getImageOp);
  const asset = await fetchFileResult.getFirstObject();
  asset.getThumbnail((error, pixelmap) => {
    if (error) {
      console.error('mediaLibrary getThumbnail failed with error: ' + error);
    } else {
      console.info('mediaLibrary getThumbnail Successful, pixelmap ' + JSON.stringify(pixelmap));
    }
  });
  fetchFileResult.close();
}
```

### getThumbnail<sup>8+</sup>

getThumbnail(size: Size, callback: AsyncCallback&lt;image.PixelMap&gt;): void

获取文件的缩略图，传入缩略图尺寸，使用callback方式返回异步结果。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[getThumbnail](js-apis-photoAccessHelper.md#getthumbnail-1)替代。

**需要权限**：ohos.permission.READ_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名      | 类型                                  | 必填   | 说明               |
| -------- | ----------------------------------- | ---- | ---------------- |
| size     | [Size](#size8)                      | 是    | 缩略图尺寸。            |
| callback | AsyncCallback&lt;image.PixelMap&gt; | 是    | callback返回缩略图的PixelMap。 |

**示例：**

```ts
async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  let size: mediaLibrary.Size = { width: 720, height: 720 };
  const fetchFileResult = await media.getFileAssets(getImageOp);
  const asset = await fetchFileResult.getFirstObject();
  asset.getThumbnail(size, (error, pixelmap) => {
    if (error) {
      console.error('mediaLibrary getThumbnail failed with error: ' + error);
    } else {
      console.info('mediaLibrary getThumbnail Successful, pixelmap ' + JSON.stringify(pixelmap));
    }
  });
  fetchFileResult.close();
}
```

### getThumbnail<sup>8+</sup>

getThumbnail(size?: Size): Promise&lt;image.PixelMap&gt;

获取文件的缩略图，传入缩略图尺寸，使用promise方式返回异步结果。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[getThumbnail](js-apis-photoAccessHelper.md#getthumbnail-2)替代。

**需要权限**：ohos.permission.READ_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名  | 类型             | 必填   | 说明    |
| ---- | -------------- | ---- | ----- |
| size | [Size](#size8) | 否    | 缩略图尺寸。 |

**返回值：**

| 类型                            | 说明                    |
| ----------------------------- | --------------------- |
| Promise&lt;image.PixelMap&gt; | Promise对象，返回缩略图的PixelMap。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  let size: mediaLibrary.Size = { width: 720, height: 720 };
  const fetchFileResult = await media.getFileAssets(getImageOp);
  const asset = await fetchFileResult.getFirstObject();
  asset.getThumbnail(size).then((pixelmap) => {
    console.info('mediaLibrary getThumbnail Successful, pixelmap ' + JSON.stringify(pixelmap));
  }).catch((error: BusinessError) => {
    console.error('mediaLibrary getThumbnail failed with error: ' + error);
  });
  fetchFileResult.close();
}
```

### favorite<sup>8+</sup>

favorite(isFavorite: boolean, callback: AsyncCallback&lt;void&gt;): void

将文件设置为收藏文件，使用callback方式返回异步结果。

> **说明：**
>
> 此接口从API version 9开始废弃。替代接口仅对系统应用开放。

**需要权限**：ohos.permission.READ_MEDIA, ohos.permission.WRITE_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名        | 类型                        | 必填   | 说明                                 |
| ---------- | ------------------------- | ---- | ---------------------------------- |
| isFavorite | boolean                   | 是    | 是否设置为收藏文件， true：设置为收藏文件，false：取消收藏。 |
| callback   | AsyncCallback&lt;void&gt; | 是    | callback返回空。                              |

**示例：**

```ts
async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  const fetchFileResult = await media.getFileAssets(getImageOp);
  const asset = await fetchFileResult.getFirstObject();
  asset.favorite(true,(error) => {
    if (error) {
      console.error('mediaLibrary favorite failed with error: ' + error);
    } else {
      console.info('mediaLibrary favorite Successful');
    }
  });
  fetchFileResult.close();
}
```

### favorite<sup>8+</sup>

favorite(isFavorite: boolean): Promise&lt;void&gt;

将文件设置为收藏文件，使用promise方式返回异步结果。

> **说明：**
>
> 此接口从API version 9开始废弃。替代接口仅对系统应用开放。

**需要权限**：ohos.permission.READ_MEDIA, ohos.permission.WRITE_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名        | 类型      | 必填   | 说明                                 |
| ---------- | ------- | ---- | ---------------------------------- |
| isFavorite | boolean | 是    | 是否设置为收藏文件， true：设置为收藏文件，false：取消收藏。 |

**返回值：**

| 类型                  | 说明         |
| ------------------- | ---------- |
| Promise&lt;void&gt; | Promise对象，返回空。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  const fetchFileResult = await media.getFileAssets(getImageOp);
  const asset = await fetchFileResult.getFirstObject();
  asset.favorite(true).then(() => {
    console.info('mediaLibrary favorite Successful');
  }).catch((error: BusinessError) => {
    console.error('mediaLibrary favorite failed with error: ' + error);
  });
  fetchFileResult.close();
}
```

### isFavorite<sup>8+</sup>

isFavorite(callback: AsyncCallback&lt;boolean&gt;): void

判断该文件是否为收藏文件，使用callback方式返回异步结果。

> **说明：**
>
> 此接口从API version 9开始废弃。无替代接口。

**需要权限**：ohos.permission.READ_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名      | 类型                           | 必填   | 说明          |
| -------- | ---------------------------- | ---- | ----------- |
| callback | AsyncCallback&lt;boolean&gt; | 是    | callback返回boolean值，值为true则为已收藏，值为false则为未收藏。 |

**示例：**

```ts
async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  const fetchFileResult = await media.getFileAssets(getImageOp);
  const asset = await fetchFileResult.getFirstObject();
  asset.isFavorite((error, isFavorite) => {
    if (error) {
      console.error('mediaLibrary favoriisFavoritete failed with error: ' + error);
    } else {
      console.info('mediaLibrary isFavorite Successful, isFavorite result: ' + isFavorite);
    }
  });
  fetchFileResult.close();
}
```

### isFavorite<sup>8+</sup>

isFavorite():Promise&lt;boolean&gt;

判断该文件是否为收藏文件，使用promise方式返回异步结果。

> **说明：**
>
> 此接口从API version 9开始废弃。无替代接口。

**需要权限**：ohos.permission.READ_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**返回值：**

| 类型                     | 说明                 |
| ---------------------- | ------------------ |
| Promise&lt;boolean&gt; | Promise对象，返回boolean值，值为true则为已收藏，值为false则为未收藏。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  const fetchFileResult = await media.getFileAssets(getImageOp);
  const asset = await fetchFileResult.getFirstObject();
  asset.isFavorite().then((isFavorite) => {
    console.info('mediaLibrary isFavorite Successful, isFavorite result: ' + isFavorite);
  }).catch((error: BusinessError) => {
    console.error('mediaLibrary favoriisFavoritete failed with error: ' + error);
  });
  fetchFileResult.close();
}
```

### trash<sup>8+</sup>

trash(isTrash: boolean, callback: AsyncCallback&lt;void&gt;): void

当文件被定位时，将文件放到垃圾文件夹，使用callback方式返回异步结果。

放入垃圾文件夹的文件不会被真正删除，可以通过isTrash = false参数恢复成正常文件。

> **说明：**
>
> 此接口从API version 9开始废弃。替代接口仅对系统应用开放。

**需要权限**：ohos.permission.READ_MEDIA, ohos.permission.WRITE_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名      | 类型                        | 必填   | 说明        |
| -------- | ------------------------- | ---- | --------- |
| isTrash  | boolean                   | 是    | 是否设置为垃圾文件。 |
| callback | AsyncCallback&lt;void&gt; | 是    | callback返回空。     |

**示例：**

```ts
async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  const fetchFileResult = await media.getFileAssets(getImageOp);
  const asset = await fetchFileResult.getFirstObject();
  asset.trash(true, (error) => {
    if (error) {
      console.error('mediaLibrary trash failed with error: ' + error);
    } else {
      console.info('mediaLibrary trash Successful');
    }
  });
  fetchFileResult.close();
}
```

### trash<sup>8+</sup>

trash(isTrash: boolean): Promise&lt;void&gt;

当文件被定位时，将文件放到垃圾文件夹，使用promise方式返回异步结果。

放入垃圾文件夹的文件不会被真正删除，可以通过isTrash = false参数恢复成正常文件。

> **说明：**
>
> 此接口从API version 9开始废弃。替代接口仅对系统应用开放。

**需要权限**：ohos.permission.READ_MEDIA, ohos.permission.WRITE_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名     | 类型      | 必填   | 说明        |
| ------- | ------- | ---- | --------- |
| isTrash | boolean | 是    | 是否设置为垃圾文件。 |

**返回值：**

| 类型                  | 说明         |
| ------------------- | ---------- |
| Promise&lt;void&gt; | Promise对象，返回空 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  const fetchFileResult = await media.getFileAssets(getImageOp);
  const asset = await fetchFileResult.getFirstObject();
  asset.trash(true).then(() => {
    console.info('trash successfully');
  }).catch((error: BusinessError) => {
    console.error('trash failed with error: ' + error);
  });
  fetchFileResult.close();
}
```

### isTrash<sup>8+</sup>

isTrash(callback: AsyncCallback&lt;boolean&gt;): void

当文件被定位，判断文件是否为垃圾文件，使用callback方式返回异步结果。

> **说明：**
>
> 此接口从API version 9开始废弃。无替代接口。

**需要权限**：ohos.permission.READ_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名      | 类型                           | 必填   | 说明              |
| -------- | ---------------------------- | ---- | --------------- |
| callback | AsyncCallback&lt;boolean&gt; | 是    | callback返回boolean值，值为true则为垃圾文件，值为false则为非垃圾文件。 |

**示例：**

```ts
async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  const fetchFileResult = await media.getFileAssets(getImageOp);
  const asset = await fetchFileResult.getFirstObject();
  asset.isTrash((error, isTrash) => {
    if (error) {
      console.error('Failed to get trash state failed with error: ' + error);
      return;
    }
    console.info('Get trash state successfully, isTrash result: ' + isTrash);
  });
  fetchFileResult.close();
}
```

### isTrash<sup>8+</sup>

isTrash():Promise&lt;boolean&gt;

当文件被定位，判断文件是否为垃圾文件，使用promise方式返回异步结果。

> **说明：**
>
> 此接口从API version 9开始废弃。无替代接口。

**需要权限**：ohos.permission.READ_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**返回值：**

| 类型                  | 说明                   |
| ------------------- | -------------------- |
| Promise&lt;void&gt; | Promise对象，返回boolean值，值为true则为垃圾文件，值为false则为非垃圾文件。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  const fetchFileResult = await media.getFileAssets(getImageOp);
  const asset = await fetchFileResult.getFirstObject();
  asset.isTrash().then((isTrash) => {
    console.info('isTrash result: ' + isTrash);
  }).catch((error: BusinessError) => {
    console.error('isTrash failed with error: ' + error);
  });
  fetchFileResult.close();
}
```

## FetchFileResult<sup>7+</sup>

文件检索结果集。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[FetchResult](js-apis-photoAccessHelper.md#fetchresult)替代。

### getCount<sup>7+</sup>

getCount(): number

获取文件检索结果中的文件总数。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[getCount](js-apis-photoAccessHelper.md#getcount)替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**返回值：**

| 类型     | 说明       |
| ------ | -------- |
| number | 检索到的文件总数。 |

**示例：**

```ts
async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let fileType = mediaLibrary.MediaType.FILE;
  let getFileCountOneOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [fileType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  let fetchFileResult = await media.getFileAssets(getFileCountOneOp);
  const fetchCount = fetchFileResult.getCount();
  console.info('fetchCount result: ' + fetchCount);
  fetchFileResult.close();
}
```

### isAfterLast<sup>7+</sup>

isAfterLast(): boolean

检查结果集是否指向最后一行。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[isAfterLast](js-apis-photoAccessHelper.md#isafterlast)替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**返回值：**

| 类型      | 说明                                 |
| ------- | ---------------------------------- |
| boolean | 当读到最后一条记录后，后续没有记录返回true，否则返回false。 |

**示例：**

```ts
async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  let fetchFileResult = await media.getFileAssets(getImageOp);
  const fetchCount = fetchFileResult.getCount();
  console.info('mediaLibrary fetchFileResult.getCount, count:' + fetchCount);
  let fileAsset = await fetchFileResult.getFirstObject();
  for (let i = 1; i < fetchCount; i++) {
    fileAsset = await fetchFileResult.getNextObject();
    if(i == fetchCount - 1) {
      let result = fetchFileResult.isAfterLast();
      console.info('mediaLibrary fileAsset isAfterLast result: ' + result);
      fetchFileResult.close();
    }
  }
}
```

### close<sup>7+</sup>

close(): void

释放 FetchFileResult 实例并使其失效。无法调用其他方法。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[close](js-apis-photoAccessHelper.md#close)替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**示例：**

```ts
async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  let fetchFileResult = await media.getFileAssets(getImageOp);
  fetchFileResult.close();
}
```

### getFirstObject<sup>7+</sup>

getFirstObject(callback: AsyncCallback&lt;FileAsset&gt;): void

获取文件检索结果中的第一个文件资产。此方法使用回调返回FileAsset。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[getFirstObject](js-apis-photoAccessHelper.md#getfirstobject)替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名   | 类型                                          | 必填 | 说明                                        |
| -------- | --------------------------------------------- | ---- | ------------------------------------------- |
| callback | AsyncCallback&lt;[FileAsset](#fileasset7)&gt; | 是   | callback返回文件检索结果集中第一个FileAsset对象。 |

**示例：**

```ts
async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  let fetchFileResult = await media.getFileAssets(getImageOp);
  fetchFileResult.getFirstObject((error, fileAsset) => {
    if (error) {
      console.error('fetchFileResult getFirstObject failed with error: ' + error);
      return;
    }
    console.info('getFirstObject successfully, displayName : ' + fileAsset.displayName);
    fetchFileResult.close();
  })
}
```

### getFirstObject<sup>7+</sup>

getFirstObject(): Promise&lt;FileAsset&gt;

获取文件检索结果中的第一个文件资产。此方法使用Promise方式返回FileAsset。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[getFirstObject](js-apis-photoAccessHelper.md#getfirstobject-1)替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**返回值：**

| 类型                                    | 说明                       |
| --------------------------------------- | -------------------------- |
| Promise&lt;[FileAsset](#fileasset7)&gt; | Promise对象，返回文件检索结果集中第一个FileAsset。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  let fetchFileResult = await media.getFileAssets(getImageOp);
  fetchFileResult.getFirstObject().then((fileAsset) => {
    console.info('getFirstObject successfully, displayName: ' + fileAsset.displayName);
    fetchFileResult.close();
  }).catch((error: BusinessError) => {
    console.error('getFirstObject failed with error: ' + error);
  });
}
```

### getNextObject<sup>7+</sup>

getNextObject(callback: AsyncCallback&lt;FileAsset&gt;): void

获取文件检索结果中的下一个文件资产，此方法使用callback形式返回结果。

> **说明：**
>
> - 在使用前需要先使用[getFirstObject](#getfirstobject7)接口获取第一个文件资产，然后使用[isAfterLast](#isafterlast7)确认文件检索集当前不是指向最后一个时方可使用此接口。
> - 此接口从API version 9开始废弃。请使用[getNextObject](js-apis-photoAccessHelper.md#getnextobject)替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名    | 类型                                          | 必填 | 说明                                      |
| --------- | --------------------------------------------- | ---- | ----------------------------------------- |
| callbacke | AsyncCallback&lt;[FileAsset](#fileasset7)&gt; | 是   | callback返回文件检索结果集中下一个FileAsset对象。 |

**示例：**

```ts
async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  let fetchFileResult = await media.getFileAssets(getImageOp);
  let fileAsset = await fetchFileResult.getFirstObject();
  console.log('fetchFileResult getFirstObject successfully, displayName: ' + fileAsset.displayName);
  if (!fetchFileResult.isAfterLast()) {
    fetchFileResult.getNextObject((error, fileAsset) => {
      if (error) {
        console.error('fetchFileResult getNextObject failed with error: ' + error);
        return;
      }
      console.log('fetchFileResult getNextObject successfully, displayName: ' + fileAsset.displayName);
      fetchFileResult.close();
    })
  }
}

```

### getNextObject<sup>7+</sup>

getNextObject(): Promise&lt;FileAsset&gt;

获取文件检索结果中的下一个文件资产。此方法使用promise方式来异步返回FileAsset。

> **说明：**
>
> - 在使用前需要先使用[getFirstObject](#getfirstobject7)接口获取第一个文件资产，然后使用[isAfterLast](#isafterlast7)确认文件检索集当前不是指向最后一个时方可使用此接口。
> - 此接口从API version 9开始废弃。请使用[getNextObject](js-apis-photoAccessHelper.md#getnextobject-1)替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;[FileAsset](#fileasset7)&gt; | Promise对象，返回文件检索结果集中下一个FileAsset。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  let fetchFileResult = await media.getFileAssets(getImageOp);
  let fileAsset = await fetchFileResult.getFirstObject();
  console.log('fetchFileResult getFirstObject successfully, displayName: ' + fileAsset.displayName);
  if (!fetchFileResult.isAfterLast()) {
    fetchFileResult.getNextObject().then((fileAsset) => {
      console.info('fetchFileResult getNextObject successfully, displayName: ' + fileAsset.displayName);
      fetchFileResult.close();
    }).catch((error: BusinessError) => {
      console.error('fetchFileResult getNextObject failed with error: ' + error);
    })
  }
}
```

### getLastObject<sup>7+</sup>

getLastObject(callback: AsyncCallback&lt;FileAsset&gt;): void

获取文件检索结果中的最后一个文件资产。此方法使用callback回调来返回FileAsset。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[getLastObject](js-apis-photoAccessHelper.md#getlastobject)替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名   | 类型                                          | 必填 | 说明                        |
| -------- | --------------------------------------------- | ---- | --------------------------- |
| callback | AsyncCallback&lt;[FileAsset](#fileasset7)&gt; | 是   | callback返回文件检索结果集中最后一个FileAsset对象。 |

**示例：**

```ts
async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  let fetchFileResult = await media.getFileAssets(getImageOp);
  fetchFileResult.getLastObject((error, fileAsset) => {
    if (error) {
      console.error('getLastObject failed with error: ' + error);
      return;
    }
    console.info('getLastObject successfully, displayName: ' + fileAsset.displayName);
    fetchFileResult.close();
  })
}
```

### getLastObject<sup>7+</sup>

getLastObject(): Promise&lt;FileAsset&gt;

获取文件检索结果中的最后一个文件资产。此方法使用Promise方式来返回FileAsset。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[getLastObject](js-apis-photoAccessHelper.md#getlastobject-1)替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;[FileAsset](#fileasset7)&gt; | Promise对象，返回文件检索结果集中最后一个FileAsset。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  let fetchFileResult = await media.getFileAssets(getImageOp);
  fetchFileResult.getLastObject().then((fileAsset) => {
    console.info('getLastObject successfully, displayName: ' + fileAsset.displayName);
    fetchFileResult.close();
  }).catch((error: BusinessError) => {
    console.error('getLastObject failed with error: ' + error);
  });
}
```

### getPositionObject<sup>7+</sup>

getPositionObject(index: number, callback: AsyncCallback&lt;FileAsset&gt;): void

获取文件检索结果中具有指定索引的文件资产。此方法使用回调来返回FileAsset。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[getObjectByPosition](js-apis-photoAccessHelper.md#getobjectbyposition)替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名       | 类型                                       | 必填   | 说明                 |
| -------- | ---------------------------------------- | ---- | ------------------ |
| index    | number                                   | 是    | 要获取的文件的索引，从0开始(注意该值要小于文件检索集的count值)。     |
| callback | AsyncCallback&lt;[FileAsset](#fileasset7)&gt; | 是    | callback返回文件检索结果集中指定索引处的FileAsset对象。 |

**示例：**

```ts
async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  let fetchFileResult = await media.getFileAssets(getImageOp);
  fetchFileResult.getPositionObject(0, (error, fileAsset) => {
    if (error) {
      console.error('getPositionObject failed with error: ' + error);
      return;
    }
    console.info('getPositionObject successfully, displayName: ' + fileAsset.displayName);
    fetchFileResult.close();
  })
}
```

### getPositionObject<sup>7+</sup>

getPositionObject(index: number): Promise&lt;FileAsset&gt;

获取文件检索结果中具有指定索引的文件资产。此方法使用Promise形式返回文件Asset。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[getObjectByPosition](js-apis-photoAccessHelper.md#getobjectbyposition-1)替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名    | 类型     | 必填   | 说明             |
| ----- | ------ | ---- | -------------- |
| index | number | 是    | 要获取的文件的索引，从0开始(注意该值要小于文件检索集的count值)。 |

**返回值：**

| 类型                                    | 说明              |
| --------------------------------------- | ----------------- |
| Promise&lt;[FileAsset](#fileasset7)&gt; | Promise对象，返回文件检索结果集中指定索引处的FileAsset。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  let fetchFileResult = await media.getFileAssets(getImageOp);
  fetchFileResult.getPositionObject(0).then((fileAsset) => {
    console.info('getPositionObject successfully, displayName: ' + fileAsset.displayName);
    fetchFileResult.close();
  }).catch((error: BusinessError) => {
    console.error('getPositionObject failed with error: ' + error);
  });
}
```

### getAllObject<sup>7+</sup>

getAllObject(callback: AsyncCallback&lt;Array&lt;FileAsset&gt;&gt;): void

获取文件检索结果中的所有文件资产。此方法使用Callback回调来返回FileAsset结果集。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[getAllObjects](js-apis-photoAccessHelper.md#getallobjects)替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名       | 类型                                       | 必填   | 说明                   |
| -------- | ---------------------------------------- | ---- | -------------------- |
| callback | AsyncCallback&lt;Array&lt;[FileAsset](#fileasset7)&gt;&gt; | 是    | callback返回文件检索结果集中所有的FileAsset对象。 |

**示例：**

```ts
async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  let fetchFileResult = await media.getFileAssets(getImageOp);
  fetchFileResult.getAllObject((error, fileAssetList) => {
    if (error) {
      console.error('getAllObject failed with error: ' + error);
      return;
    }
    for (let i = 0; i < fetchFileResult.getCount(); i++) {
      console.info('getAllObject fileAssetList ' + i + ' displayName: ' + fileAssetList[i].displayName);
    }
    fetchFileResult.close();
  })
}
```

### getAllObject<sup>7+</sup>

getAllObject(): Promise&lt;Array&lt;FileAsset&gt;&gt;

获取文件检索结果中的所有文件资产。此方法使用Promise来返回FileAsset结果集。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[getAllObjects](js-apis-photoAccessHelper.md#getallobjects-1)替代。

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**返回值：**

| 类型                                     | 说明                  |
| ---------------------------------------- | --------------------- |
| Promise&lt;Array&lt;[FileAsset](#fileasset7)&gt;&gt; | Promise对象，返回文件检索结果集中所有的FileAsset。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  let fileKeyObj = mediaLibrary.FileKey;
  let imageType = mediaLibrary.MediaType.IMAGE;
  let getImageOp: mediaLibrary.MediaFetchOptions = {
    selections: fileKeyObj.MEDIA_TYPE + '= ?',
    selectionArgs: [imageType.toString()],
    order: fileKeyObj.DATE_ADDED + ' DESC',
  };
  let fetchFileResult = await media.getFileAssets(getImageOp);
  fetchFileResult.getAllObject().then((fileAssetList) => {
    for (let i = 0; i < fetchFileResult.getCount(); i++) {
      console.info('getAllObject fileAssetList ' + i + ' displayName: ' + fileAssetList[i].displayName);
    } 
    fetchFileResult.close();
  }).catch((error: BusinessError) => {
    console.error('getAllObject failed with error: ' + error);
  });
}
```

## Album<sup>7+</sup>

实体相册

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[Album](js-apis-photoAccessHelper.md#album)替代。

### 属性

**系统能力：** 以下各项对应的系统能力均为SystemCapability.Multimedia.MediaLibrary.Core

| 名称           | 类型    | 可读   | 可写   | 说明      |
| ------------ | ------ | ---- | ---- | ------- |
| albumId | number | 是    | 否    | 相册编号。    |
| albumName | string | 是    | 是    | 相册名称。    |
| albumUri<sup>8+</sup> | string | 是    | 否    | 相册Uri。   |
| dateModified | number | 是    | 否    | 修改日期。    |
| count<sup>8+</sup> | number | 是    | 否    | 相册中文件数量。 |
| relativePath<sup>8+</sup> | string | 是    | 否    | 相对路径。    |
| coverUri<sup>8+</sup> | string | 是    | 否    | 封面文件Uri。 |

### commitModify<sup>8+</sup>

commitModify(callback: AsyncCallback&lt;void&gt;): void

更新相册属性修改到数据库中。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[commitModify](js-apis-photoAccessHelper.md#commitmodify-2)替代。

**需要权限**：ohos.permission.READ_MEDIA, ohos.permission.WRITE_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明       |
| -------- | ------------------------- | ---- | ---------- |
| callback | AsyncCallback&lt;void&gt; | 是   | callback返回空。 |

**示例：**

```ts
async function example() {
  // 获取相册需要先预置相册和资源，示例代码为预置的新建相册1。
  let albumFetchOp: mediaLibrary.MediaFetchOptions = {
    selections: mediaLibrary.FileKey.ALBUM_NAME + '= ?',
    selectionArgs: ['新建相册1'],
  };
  const albumList = await media.getAlbums(albumFetchOp);
  const album = albumList[0];
  album.albumName = 'hello';
  album.commitModify((error) => {
    if (error) {
      console.error('commitModify failed with error: ' + error);
      return;
    }
    console.info('commitModify successful.');
  });
}
```

### commitModify<sup>8+</sup>

commitModify(): Promise&lt;void&gt;

更新相册属性修改到数据库中。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[commitModify](js-apis-photoAccessHelper.md#commitmodify-3)替代。

**需要权限**：ohos.permission.READ_MEDIA, ohos.permission.WRITE_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**返回值：**

| 类型                  | 说明           |
| ------------------- | ------------ |
| Promise&lt;void&gt; | Promise对象，返回空。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  // 获取相册需要先预置相册和资源，示例代码为预置的新建相册1。
  let albumFetchOp: mediaLibrary.MediaFetchOptions = {
    selections: mediaLibrary.FileKey.ALBUM_NAME + '= ?',
    selectionArgs: ['新建相册1'],
  };
  const albumList = await media.getAlbums(albumFetchOp);
  const album = albumList[0];
  album.albumName = 'hello';
  album.commitModify().then(() => {
    console.info('commitModify successfully');
  }).catch((error: BusinessError) => {
    console.error('commitModify failed with error: ' + error);
  });
}
```

### getFileAssets<sup>7+</sup>

getFileAssets(callback: AsyncCallback&lt;FetchFileResult&gt;): void

按照检索条件获取相册中的文件。此方法使用Callback回调来返回文件结果集。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[getAssets](js-apis-photoAccessHelper.md#getassets)替代。

**需要权限**：ohos.permission.READ_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名   | 类型                                                | 必填 | 说明                                |
| -------- | --------------------------------------------------- | ---- | ----------------------------------- |
| callback | AsyncCallback<[FetchFileResult](#fetchfileresult7)> | 是   | callback返回相册中的文件检索结果集。 |

**示例：**

```ts
async function example() {
  // 获取相册需要先预置相册和资源，示例代码为预置的新建相册1。
  let albumFetchOp: mediaLibrary.MediaFetchOptions = {
    selections: mediaLibrary.FileKey.ALBUM_NAME + '= ?',
    selectionArgs: ['新建相册1'],
  };
  // 获取符合检索要求的相册，返回相册列表。
  const albumList = await media.getAlbums(albumFetchOp);
  const album = albumList[0];
  // 取到相册列表中的一个相册，获取此相册中所有符合媒体检索选项的媒体资源。
  album.getFileAssets((error, fetchFileResult) => {
    if (error) {
      console.error('album getFileAssets failed with error: ' + error);
      return;
    }
    let count = fetchFileResult.getCount();
    console.info('album getFileAssets successfully, count: ' + count);
    fetchFileResult.close();
  });
}
```

### getFileAssets<sup>7+</sup>

getFileAssets(options: MediaFetchOptions, callback: AsyncCallback&lt;FetchFileResult&gt;): void

按照检索条件获取相册中的文件。此方法使用Callback回调来返回文件结果集。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[getAssets](js-apis-photoAccessHelper.md#getassets)替代。

**需要权限**：ohos.permission.READ_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名   | 类型                                                | 必填 | 说明                                |
| -------- | --------------------------------------------------- | ---- | ----------------------------------- |
| options  | [MediaFetchOptions](#mediafetchoptions7)            | 是   | 媒体检索选项。                      |
| callback | AsyncCallback<[FetchFileResult](#fetchfileresult7)> | 是   | callback返回相册中的文件检索结果集。 |

**示例：**

```ts
async function example() {
  // 获取相册需要先预置相册和资源，示例代码为预置的新建相册1。
  let albumFetchOp: mediaLibrary.MediaFetchOptions = {
    selections: mediaLibrary.FileKey.ALBUM_NAME + '= ?',
    selectionArgs: ['新建相册1'],
  };
  let fileNoArgsfetchOp: mediaLibrary.MediaFetchOptions = {
    selections: '',
    selectionArgs: [],
  };
  // 获取符合检索要求的相册，返回相册列表。
  const albumList = await media.getAlbums(albumFetchOp);
  const album = albumList[0];
  // 取到相册列表中的一个相册，获取此相册中所有符合媒体检索选项的媒体资源。
  album.getFileAssets(fileNoArgsfetchOp, (error, fetchFileResult) => {
    if (error) {
      console.error('album getFileAssets failed with error: ' + error);
      return;
    }
    let count = fetchFileResult.getCount();
    console.info('album getFileAssets successfully, count: ' + count);
    fetchFileResult.close();
  });
}
```

### getFileAssets<sup>7+</sup>

 getFileAssets(options?: MediaFetchOptions): Promise&lt;FetchFileResult&gt;

按照检索条件获取相册中的文件。此方法使用异步Promise来返回文件结果集。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[getAssets](js-apis-photoAccessHelper.md#getassets-1)替代。

**需要权限**：ohos.permission.READ_MEDIA

**系统能力**：SystemCapability.Multimedia.MediaLibrary.Core

**参数：**

| 参数名  | 类型                                     | 必填 | 说明           |
| ------- | ---------------------------------------- | ---- | -------------- |
| options | [MediaFetchOptions](#mediafetchoptions7) | 否   | 媒体检索选项。 |

**返回值：**

| 类型                                          | 说明                      |
| --------------------------------------------- | ------------------------- |
| Promise<[FetchFileResult](#fetchfileresult7)> | Promise对象，返回相册中的文件检索结果集。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

async function example() {
  // 获取相册需要先预置相册和资源，示例代码为预置的新建相册1。
  let albumFetchOp: mediaLibrary.MediaFetchOptions = {
    selections: mediaLibrary.FileKey.ALBUM_NAME + '= ?',
    selectionArgs: ['新建相册1'],
  };
  let fileNoArgsfetchOp: mediaLibrary.MediaFetchOptions = {
    selections: '',
    selectionArgs: [],
  };
  // 获取符合检索要求的相册，返回相册列表。
  const albumList = await media.getAlbums(albumFetchOp);
  const album = albumList[0];
  // 取到相册列表中的一个相册，获取此相册中所有符合媒体检索选项的媒体资源。
  album.getFileAssets(fileNoArgsfetchOp).then((fetchFileResult) => {
    let count = fetchFileResult.getCount();
    console.info('album getFileAssets successfully, count: ' + count);
    fetchFileResult.close();
  }).catch((error: BusinessError) => {
    console.error('album getFileAssets failed with error: ' + error);
  });
}
```

## MediaType<sup>8+</sup>

枚举，媒体类型。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[PhotoType](js-apis-photoAccessHelper.md#phototype)替代。

**系统能力：** 以下各项对应的系统能力均为SystemCapability.Multimedia.MediaLibrary.Core

| 名称  |  值 |  说明 |
| ----- |  ---- | ---- |
| FILE  |  0 | 文件。 |
| IMAGE |  1 | 图片。 |
| VIDEO |  2 | 视频。|
| AUDIO |  3 | 音频。 |

## FileKey<sup>8+</sup>

枚举，文件关键信息。

> **说明：**
>
> - bucket_id字段在文件重命名或移动后可能会发生变化，开发者使用前需要重新获取。
> - 此接口从API version 9开始废弃。请使用[PhotoKeys](js-apis-photoAccessHelper.md#photokeys)替代。

**系统能力：** 以下各项对应的系统能力均为SystemCapability.Multimedia.MediaLibrary.Core

| 名称          | 值              | 说明                                                       |
| ------------- | ------------------- | ---------------------------------------------------------- |
| ID            | 'file_id'             | 文件编号。                                                   |
| RELATIVE_PATH | 'relative_path'       | 相对公共目录路径。                                           |
| DISPLAY_NAME  | 'display_name'        | 显示名字。                                                   |
| PARENT        | 'parent'              | 父目录id。                                                   |
| MIME_TYPE     | 'mime_type'           | 文件扩展属性(如：image/*、video/*、file/*)。                                             |
| MEDIA_TYPE    | 'media_type'          | 媒体类型。                                                   |
| SIZE          | 'size'                | 文件大小（单位：字节）。                                     |
| DATE_ADDED    | 'date_added'          | 添加日期（添加文件时间到1970年1月1日的秒数值）。             |
| DATE_MODIFIED | 'date_modified'       | 修改日期（修改文件时间到1970年1月1日的秒数值，修改文件名不会改变此值，当文件内容发生修改时才会更新）。 |
| DATE_TAKEN    | 'date_taken'          | 拍摄日期（文件拍照时间到1970年1月1日的秒数值）。             |
| TITLE         | 'title'               | 文件标题。                                                   |
| ARTIST        | 'artist'              | 作者。                                                       |
| AUDIOALBUM    | 'audio_album'         | 专辑。                                                       |
| DURATION      | 'duration'            | 持续时间（单位：毫秒）。                                       |
| WIDTH         | 'width'               | 图片宽度（单位：像素）。                                     |
| HEIGHT        | 'height'              | 图片高度（单位：像素）。                                     |
| ORIENTATION   | 'orientation'         | 图片显示方向，即顺时针旋转角度，如0，90，180。（单位：度）。 |
| ALBUM_ID      | 'bucket_id'           | 文件所归属的相册编号。                                       |
| ALBUM_NAME    | 'bucket_display_name' | 文件所归属相册名称。                                         |

## DirectoryType<sup>8+</sup>

枚举，目录类型。

> **说明：**
>
> 此接口从API version 9开始废弃。无替代接口。

**系统能力：** 以下各项对应的系统能力均为SystemCapability.Multimedia.MediaLibrary.Core

| 名称          | 值 |  说明               |
| ------------- | --- | ------------------ |
| DIR_CAMERA    |  0 | 表示Camera文件路径。 |
| DIR_VIDEO     |  1 |  表示视频路径。       |
| DIR_IMAGE     |  2 | 表示图片路径。       |
| DIR_AUDIO     |  3 | 表示音频路径。       |
| DIR_DOCUMENTS |  4 | 表示文档路径。       |
| DIR_DOWNLOAD  |  5 |  表示下载路径。       |

## MediaFetchOptions<sup>7+</sup>

检索条件。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[FetchOptions](js-apis-photoAccessHelper.md#fetchoptions)替代。

**系统能力：** 以下各项对应的系统能力均为SystemCapability.Multimedia.MediaLibrary.Core

| 名称                    | 类型                | 可读 | 可写 | 说明                                                         |
| ----------------------- | ------------------- | ---- | ---- | ------------------------------------------------------------ |
| selections              | string              | 是   | 是   | 检索条件，使用[FileKey](#filekey8)中的枚举值作为检索条件的列名。示例：<br/>selections: mediaLibrary.FileKey.MEDIA_TYPE + '= ? OR ' + mediaLibrary.FileKey.MEDIA_TYPE + '= ?', |
| selectionArgs           | Array&lt;string&gt; | 是   | 是   | 检索条件的值，对应selections中检索条件列的值。<br/>示例：<br/>selectionArgs: [mediaLibrary.MediaType.IMAGE.toString(), mediaLibrary.MediaType.VIDEO.toString()], |
| order                   | string              | 是   | 是   | 检索结果排序方式，使用[FileKey](#filekey8)中的枚举值作为检索结果排序的列，可以用升序或降序排列。示例：<br/>升序排列：order: mediaLibrary.FileKey.DATE_ADDED + ' ASC'<br/>降序排列：order: mediaLibrary.FileKey.DATE_ADDED + ' DESC' |
| uri<sup>8+</sup>        | string              | 是   | 是   | 文件URI。                                                      |
| networkId<sup>8+</sup>  | string              | 是   | 是   | 注册设备网络ID。                                               |
| extendArgs<sup>8+</sup> | string              | 是   | 是   | 扩展的检索参数，目前没有扩展检索参数。                         |

## Size<sup>8+</sup>

图片尺寸。

> **说明：**
>
> 此接口从API version 9开始废弃。请使用[image.Size](../apis-image-kit/js-apis-image.md#size)替代。

**系统能力：**  以下各项对应的系统能力均为SystemCapability.Multimedia.MediaLibrary.Core

| 名称     | 类型     | 可读   | 可写   | 说明       |
| ------ | ------ | ---- | ---- | -------- |
| width  | number | 是    | 是    | 宽（单位：像素）。 |
| height | number | 是    | 是    | 高（单位：像素）。 |

## MediaAssetOption

媒体资源选项。

> **说明：**
>
> 此接口从API version 9开始废弃。无替代接口。

**系统能力：** 以下各项对应的系统能力均为SystemCapability.Multimedia.MediaLibrary.Core

| 名称         | 类型   | 可读 | 可写 | 说明                                                         |
| ------------ | ------ | ---- | ---- | ------------------------------------------------------------ |
| src          | string | 是   | 是   | 本地文件应用沙箱路径。                                       |
| mimeType     | string | 是   | 是   | 媒体MIME（Multipurpose&nbsp;Internet&nbsp;Mail&nbsp;Extensions）类型。<br/>包括：'image/\*'、'video/\*'、'audio/\*'、 'file\*'。 |
| relativePath | string | 是   | 是   | 自定义媒体资源保存位置，例：Pictures/ 不填则保存到默认路径。 <br/> image类型默认路径Pictures/ <br/> video类型默认路径Videos/ <br/> audio类型默认路径Audios/ <br/> file类型默认路径Documents/ 。 |

## MediaSelectOption

媒体资源类型选项。

> **说明：**
>
> 此接口从API version 9开始废弃。无替代接口。

**系统能力：** 以下各项对应的系统能力均为SystemCapability.Multimedia.MediaLibrary.Core

| 名称    | 类型     | 可读 | 可写 | 说明                   |
| ----- | ------ | ---- | ---- | -------------------- |
| type  | 'image' &#124; 'video' &#124; 'media' | 是    | 是  | 媒体类型，包括：image, video, media，当前仅支持media类型。 |
| count | number | 是    | 是  | 可以选择媒体数量的最大值，count = 1表示单选，count大于1表示多选。            |
