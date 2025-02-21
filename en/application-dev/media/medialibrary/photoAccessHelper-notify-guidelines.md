# Observing Media Assets

The **photoAccessHelper** module provides APIs for listening for media asset (image, video, and album) changes.

> **NOTE**
>
> Before you get started, obtain a **PhotoAccessHelper** instance and apply for required permissions. For details, see [Before You Start](photoAccessHelper-preparation.md).
> Unless otherwise specified, the **PhotoAccessHelper** instance obtained in the **Before You Start** section is used to call **photoAccessHelper** APIs. If the code for obtaining the **PhotoAccessHelper** instance is missing, an error will be reported to indicate that **photoAccessHelper** is not defined.

The APIs related to media asset change notifications can be called asynchronously only in callback mode. This topic covers only some of these APIs. For details about all available APIs, see [Album Management](../../reference/apis-media-library-kit/js-apis-photoAccessHelper.md). 
Unless otherwise specified, all the media assets to be obtained in this document exist in the database. If no media asset is obtained when the sample code is executed, check whether the media assets exist in the database.

## Listening for a URI

Use [registerChange](../../reference/apis-media-library-kit/js-apis-photoAccessHelper.md#registerchange) to listen for a URI. When the observed object changes, the registered callback will be invoked to return the value.

### Listening for a PhotoAsset

Register a listener for a **PhotoAsset** instance. When the observed **PhotoAsset** changes, the registered callback will be invoked to return the change.

**Prerequisites**

- A **PhotoAccessHelper** instance is obtained.
- The application has the ohos.permission.READ_IMAGEVIDEO and ohos.permission.WRITE_IMAGEVIDEO permissions.

Example: Listen for changes of an image. When the image is deleted, the registered callback will be invoked.

**How to Develop**

1. [Obtain the target media asset](photoAccessHelper-resource-guidelines.md#obtaining-media-assets).
2. Register a listener for a **PhotoAsset**.
3. Delete the **PhotoAsset**.

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import photoAccessHelper from '@ohos.file.photoAccessHelper';
const context = getContext(this);
let phAccessHelper = photoAccessHelper.getPhotoAccessHelper(context);

async function example() {
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  predicates.equalTo(photoAccessHelper.PhotoKeys.DISPLAY_NAME, 'test.jpg');
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    console.info('getAssets photoAsset.uri : ' + photoAsset.uri);
    let onCallback = (changeData: photoAccessHelper.ChangeData) => {
      console.info('onCallback successfully, changData: ' + JSON.stringify(changeData));
    }
    phAccessHelper.registerChange(photoAsset.uri, false, onCallback);
    await photoAccessHelper.MediaAssetChangeRequest.deleteAssets(context, [photoAsset]);
    fetchResult.close();
  } catch (err) {
    console.error('onCallback failed with err: ' + err);
  }
}
```

### Listening for an Album

Register a listener for an album. When the observed album changes, the registered callback will be invoked to return the change.

**Prerequisites**

- A **PhotoAccessHelper** instance is obtained.
- The application has the ohos.permission.READ_IMAGEVIDEO and ohos.permission.WRITE_IMAGEVIDEO permissions.

Example: Listen for a user album. When the album is renamed, the registered callback will be invoked.

**How to Develop**

1. [Obtain the target user album](photoAccessHelper-userAlbum-guidelines.md#obtaining-a-user-album).
2. Register a listener for the user album.
3. Rename the user album.


```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import photoAccessHelper from '@ohos.file.photoAccessHelper';
const context = getContext(this);
let phAccessHelper = photoAccessHelper.getPhotoAccessHelper(context);

async function example() {
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let albumName: photoAccessHelper.AlbumKeys = photoAccessHelper.AlbumKeys.ALBUM_NAME;
  predicates.equalTo(albumName, 'albumName');
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };

  try {
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, fetchOptions);
    let album: photoAccessHelper.Album = await fetchResult.getFirstObject();
    console.info('getAlbums successfully, albumUri: ' + album.albumUri);

    let onCallback = (changeData: photoAccessHelper.ChangeData) => {
      console.info('onCallback successfully, changData: ' + JSON.stringify(changeData));
    }
    phAccessHelper.registerChange(album.albumUri, false, onCallback);
    album.albumName = 'newAlbumName' + Date.now();
    await album.commitModify();
    fetchResult.close();
  } catch (err) {
    console.error('onCallback failed with err: ' + err);
  }
}
```

## Fuzzy Listening

You can set **forChildUris** to **true** to enable fuzzy listening.<br>If **uri** is an album URI, the value **true** of **forChildUris** enables listening for the changes of the files in the album, and the value **false** enables listening for only the changes of the album itself. <br>If **uri** is the URI of a **photoAsset**, there is no difference between **true** and **false** for **forChildUris**.<br>If **uri** is **DefaultChangeUri**, **forChildUris** must be set to **true**. If **forChildUris** is **false**, the URI cannot be found and no notification can be received.

### Listening for All PhotoAssets

Register a listener for all **PhotoAssets**. When a **PhotoAsset** object changes, the registered callback will be invoked.

**Prerequisites**

- A **PhotoAccessHelper** instance is obtained.
- The application has the ohos.permission.READ_IMAGEVIDEO and ohos.permission.WRITE_IMAGEVIDEO permissions.

Example: Register a listener for all **PhotoAssets**. When a **PhotoAsset** is deleted, the registered callback will be invoked.

**How to Develop**

1. Register a listener for all **PhotoAssets**.
2. [Obtain a media asset](photoAccessHelper-resource-guidelines.md#obtaining-media-assets).
3. Delete the media asset.

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import photoAccessHelper from '@ohos.file.photoAccessHelper';
const context = getContext(this);
let phAccessHelper = photoAccessHelper.getPhotoAccessHelper(context);

async function example() {
  let onCallback = (changeData: photoAccessHelper.ChangeData) => {
    console.info('onCallback successfully, changData: ' + JSON.stringify(changeData));
  }
  phAccessHelper.registerChange(photoAccessHelper.DefaultChangeUri.DEFAULT_PHOTO_URI, true, onCallback);
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    console.info('getAssets photoAsset.uri : ' + photoAsset.uri);
    await photoAccessHelper.MediaAssetChangeRequest.deleteAssets(context, [photoAsset]);
    fetchResult.close();
  } catch (err) {
    console.error('onCallback failed with err: ' + err);
  }
}
```

## Unregistering Listening for a URI

Use [unRegisterChange](../../reference/apis-media-library-kit/js-apis-photoAccessHelper.md#unregisterchange) to unregister the listening for the specified URI. Multiple listeners can be registered for a URI. If multiple listener callbacks exist, you can specify a callback to unregister a specific listener. If no callback is specified, all listeners of the URI will be unregistered.

**Prerequisites**

- A **PhotoAccessHelper** instance is obtained.
- The application has the ohos.permission.READ_IMAGEVIDEO and ohos.permission.WRITE_IMAGEVIDEO permissions.

Example: Unregister listening for an image. The unregistered listener callback will not be invoked when the image is deleted.

**How to Develop**

1. [Obtain a media asset](photoAccessHelper-resource-guidelines.md#obtaining-media-assets).
2. Unregister the listener for the URI of the media asset obtained.
3. Delete the media asset.

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import photoAccessHelper from '@ohos.file.photoAccessHelper';
const context = getContext(this);
let phAccessHelper = photoAccessHelper.getPhotoAccessHelper(context);

async function example() {
  let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
  predicates.equalTo(photoAccessHelper.PhotoKeys.DISPLAY_NAME, 'test.jpg');
  let fetchOptions: photoAccessHelper.FetchOptions = {
    fetchColumns: [],
    predicates: predicates
  };
  try {
    let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(fetchOptions);
    let photoAsset: photoAccessHelper.PhotoAsset = await fetchResult.getFirstObject();
    console.info('getAssets photoAsset.uri : ' + photoAsset.uri);
    let onCallback1 = (changeData: photoAccessHelper.ChangeData) => {
      console.info('onCallback1, changData: ' + JSON.stringify(changeData));
    }
    let onCallback2 = (changeData: photoAccessHelper.ChangeData) => {
      console.info('onCallback2, changData: ' + JSON.stringify(changeData));
    }
    phAccessHelper.registerChange(photoAsset.uri, false, onCallback1);
    phAccessHelper.registerChange(photoAsset.uri, false, onCallback2);
    phAccessHelper.unRegisterChange(photoAsset.uri, onCallback1);
    await photoAccessHelper.MediaAssetChangeRequest.deleteAssets(context, [photoAsset]);
    fetchResult.close();
  } catch (err) {
    console.error('onCallback failed with err: ' + err);
  }
}
```
