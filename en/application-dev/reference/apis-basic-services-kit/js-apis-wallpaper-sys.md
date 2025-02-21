# @ohos.wallpaper (Wallpaper) (System API)

The **wallpaper** module provides APIs for switching between wallpapers. Since API version 9, the APIs of this module function as system APIs, and only system applications are allowed to switch between wallpapers. Applications that use the wallpaper, for example, the home screen, need to subscribe to wallpaper changes and update the wallpaper accordingly.

> **NOTE**
> 
> The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.
> This topic describes only system APIs provided by the module. For details about its public APIs, see [@ohos.wallpaper (Wallpaper)](js-apis-wallpaper.md).


## Modules to Import


```ts
import wallpaper from '@ohos.wallpaper';
```
## WallpaperResourceType<sup>10+</sup>

Enumerates the types of wallpaper resources.

**System capability**: SystemCapability.MiscServices.Wallpaper

**System API**: This is a system API.

| Name| Value|Description|
| -------- | -------- |-------- |
| DEFAULT | 0 |Default type (image resource).|
| PICTURE | 1 |Image resource.|
| VIDEO | 2 |Video resource.|
| PACKAGE | 3 |Package resource.|

## wallpaper.setVideo<sup>10+</sup>

setVideo(source: string, wallpaperType: WallpaperType, callback: AsyncCallback&lt;void&gt;): void

Sets a video resource as the home screen wallpaper or lock screen wallpaper. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.SET_WALLPAPER

**System capability**: SystemCapability.MiscServices.Wallpaper

**System API**: This is a system API.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| source | string | Yes| URI of an MP4 file.|
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | Yes| Wallpaper type.|
| callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result. If the wallpaper is set, **err** is **undefined**. Otherwise, **err** is an error object.|

**Example**

```ts
import { BusinessError } from '@ohos.base';

let wallpaperPath = "/data/storage/el2/base/haps/entry/files/test.mp4";
try {
    wallpaper.setVideo(wallpaperPath, wallpaper.WallpaperType.WALLPAPER_SYSTEM, (error: BusinessError) => {
        if (error) {
            console.error(`failed to setVideo because: ${JSON.stringify(error)}`);
            return;
        }
        console.log(`success to setVideo.`);
    });
} catch (error) {
    console.error(`failed to setVideo because: ${JSON.stringify(error)}`);
}

```

## wallpaper.setVideo<sup>10+</sup>

setVideo(source: string, wallpaperType: WallpaperType): Promise&lt;void&gt;

Sets a video resource as the home screen wallpaper or lock screen wallpaper. This API uses a promise to return the result.

**Required permissions**: ohos.permission.SET_WALLPAPER

**System capability**: SystemCapability.MiscServices.Wallpaper

**System API**: This is a system API.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| source | string | Yes| URI of an MP4 file.|
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | Yes| Wallpaper type.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
import { BusinessError } from '@ohos.base';

let wallpaperPath = "/data/storage/el2/base/haps/entry/files/test.mp4";
try {
    wallpaper.setVideo(wallpaperPath, wallpaper.WallpaperType.WALLPAPER_SYSTEM).then(() => {
        console.log(`success to setVideo.`);
    }).catch((error: BusinessError) => {
        console.error(`failed to setVideo because: ${JSON.stringify(error)}`);
    });
} catch (error) {
    console.error(`failed to setVideo because: ${JSON.stringify(error)}`);
}
```

## wallpaper.setCustomWallpaper<sup>10+</sup>

setCustomWallpaper(source: string, wallpaperType: WallpaperType, callback: AsyncCallback&lt;void&gt;): void

Sets a specific ZIP file as the wallpaper. This API works only when **com.ohos.sceneboard** is set. Applications with the **ohos.permission.GET_WALLPAPER** permission have access to the **/data/wallpaper/** directory. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.SET_WALLPAPER

**System capability**: SystemCapability.MiscServices.Wallpaper

**System API**: This is a system API.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| source | string | Yes| ZIP file to set as the wallpaper.|
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | Yes| Wallpaper type.|
| callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result. If the wallpaper is set, **err** is **undefined**. Otherwise, **err** is an error object.|

**Example**

```ts
import { BusinessError } from '@ohos.base';

let wallpaperPath = "/data/storage/el2/base/haps/entry/files/test.zip";
try {
    wallpaper.setCustomWallpaper(wallpaperPath, wallpaper.WallpaperType.WALLPAPER_SYSTEM, (error: BusinessError) => {
        if (error) {
            console.error(`failed to setCustomWallpaper because: ${JSON.stringify(error)}`);
            return;
        }
        console.log(`success to setCustomWallpaper.`);
    });
} catch (error) {
    console.error(`failed to setCustomWallpaper because: ${JSON.stringify(error)}`);
}

```

## wallpaper.setCustomWallpaper<sup>10+</sup>

setCustomWallpaper(source: string, wallpaperType: WallpaperType): Promise&lt;void&gt;

Sets a specific ZIP file as the wallpaper. This API works only when **com.ohos.sceneboard** is set. Applications with the **ohos.permission.GET_WALLPAPER** permission have access to the **/data/wallpaper/** directory. This API uses a promise to return the result.

**Required permissions**: ohos.permission.SET_WALLPAPER

**System capability**: SystemCapability.MiscServices.Wallpaper

**System API**: This is a system API.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| source | string | Yes| ZIP file to set as the wallpaper.|
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | Yes| Wallpaper type.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
import { BusinessError } from '@ohos.base';

let wallpaperPath = "/data/storage/el2/base/haps/entry/files/test.zip";
try {
    wallpaper.setCustomWallpaper(wallpaperPath, wallpaper.WallpaperType.WALLPAPER_SYSTEM).then(() => {
        console.log(`success to setCustomWallpaper.`);
    }).catch((error: BusinessError) => {
        console.error(`failed to setCustomWallpaper because: ${JSON.stringify(error)}`);
    });
} catch (error) {
    console.error(`failed to setCustomWallpaper because: ${JSON.stringify(error)}`);
}
```

## wallpaper.on('wallpaperChange')<sup>10+</sup>

on(type: 'wallpaperChange', callback: (wallpaperType: WallpaperType, resourceType: WallpaperResourceType, uri?: string) =&gt; void): void

Subscribes to wallpaper change events. Multi-thread concurrent calls are not supported.

**System capability**: SystemCapability.MiscServices.Wallpaper

**System API**: This is a system API.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type. The value is fixed at **'wallpaperChange'**.|
| callback | function | Yes| Callback used to return the wallpaper type and wallpaper resource type.<br>- **wallpaperType**: wallpaper type.<br>- **resourceType**: wallpaper resource type.<br>- **uri**: URI of the wallpaper resource.|

**Example**

```ts
try {
    let listener = (wallpaperType: wallpaper.WallpaperType, resourceType: wallpaper.WallpaperResourceType): void => {
        console.log(`wallpaper color changed.`);
    };
    wallpaper.on('wallpaperChange', listener);
} catch (error) {
    console.error(`failed to on because: ${JSON.stringify(error)}`);
}
```

## wallpaper.off('wallpaperChange')<sup>10+</sup>

off(type: 'wallpaperChange', callback?: (wallpaperType: WallpaperType, resourceType: WallpaperResourceType, uri?: string) =&gt; void): void

Unsubscribes from wallpaper change events. Multi-thread concurrent calls are not supported.

**System capability**: SystemCapability.MiscServices.Wallpaper

**System API**: This is a system API.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type. The value is fixed at **'wallpaperChange'**.|
| callback | function | No|   Callback used for unsubscription. If this parameter is not set, this API unsubscribes from all callbacks of the specified event type.<br>- **wallpaperType**: wallpaper type.<br>- **resourceType**: wallpaper resource type.<br>- **uri**: URI of the wallpaper resource.|

**Example**

```ts
let listener = (wallpaperType: wallpaper.WallpaperType, resourceType: wallpaper.WallpaperResourceType): void => {
    console.log(`wallpaper color changed.`);
};
try {
    wallpaper.on('wallpaperChange', listener);
} catch (error) {
    console.error(`failed to on because: ${JSON.stringify(error)}`);
}

try {
    // Unsubscribe from the listener.
    wallpaper.off('wallpaperChange', listener);
} catch (error) {
    console.error(`failed to off because: ${JSON.stringify(error)}`);
}

try {
    // Unsubscribe from all callbacks of the 'wallpaperChange' event type.
    wallpaper.off('wallpaperChange');
} catch (error) {
    console.error(`failed to off because: ${JSON.stringify(error)}`);
}
```

## wallpaper.getColorsSync<sup>9+</sup>

getColorsSync(wallpaperType: WallpaperType): Array&lt;RgbaColor&gt;

Obtains the main color information of the wallpaper of the specified type.

**System capability**: SystemCapability.MiscServices.Wallpaper

**System API**: This is a system API.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | Yes| Wallpaper type.|

**Return value**

| Type| Description|
| -------- | -------- |
| Array&lt;[RgbaColor](js-apis-wallpaper.md#rgbacolordeprecated)&gt; | Promise used to return the main color information of the wallpaper.|

**Example**

```ts
try {
    let colors = wallpaper.getColorsSync(wallpaper.WallpaperType.WALLPAPER_SYSTEM);
    console.log(`success to getColorsSync: ${JSON.stringify(colors)}`);
} catch (error) {
    console.error(`failed to getColorsSync because: ${JSON.stringify(error)}`);
}
```

## wallpaper.getMinHeightSync<sup>9+</sup>

getMinHeightSync(): number

Obtains the minimum height of this wallpaper.

**System capability**: SystemCapability.MiscServices.Wallpaper

**System API**: This is a system API.

**Return value**

| Type| Description|
| -------- | -------- |
| number | Promise used to return the minimum wallpaper height, in pixels. If the return value is **0**, no wallpaper is set. In this case, the default height should be used instead.|

**Example**

```ts
let minHeight = wallpaper.getMinHeightSync();
```

## wallpaper.getMinWidthSync<sup>9+</sup>

getMinWidthSync(): number

Obtains the minimum width of this wallpaper.

**System capability**: SystemCapability.MiscServices.Wallpaper

**System API**: This is a system API.

**Return value**

| Type| Description|
| -------- | -------- |
| number | Promise used to return the minimum wallpaper width, in pixels. If the return value is **0**, no wallpaper is set. In this case, the default width should be used instead.|

**Example**

```ts
let minWidth = wallpaper.getMinWidthSync();
```

## wallpaper.restore<sup>9+</sup>

restore(wallpaperType: WallpaperType, callback: AsyncCallback&lt;void&gt;): void

Resets the wallpaper of the specified type to the default wallpaper. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.SET_WALLPAPER

**System capability**: SystemCapability.MiscServices.Wallpaper

**System API**: This is a system API.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | Yes| Wallpaper type.|
| callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result. If the wallpaper is reset, **err** is **undefined**. Otherwise, **err** is an error object.|

**Example**

```ts
import { BusinessError } from '@ohos.base';

wallpaper.restore(wallpaper.WallpaperType.WALLPAPER_SYSTEM, (error: BusinessError) => {
    if (error) {
        console.error(`failed to restore because: ${JSON.stringify(error)}`);
        return;
    }
    console.log(`success to restore.`);
});
```

## wallpaper.restore<sup>9+</sup>

restore(wallpaperType: WallpaperType): Promise&lt;void&gt;

Resets the wallpaper of the specified type to the default wallpaper. This API uses a promise to return the result.

**Required permissions**: ohos.permission.SET_WALLPAPER

**System capability**: SystemCapability.MiscServices.Wallpaper

**System API**: This is a system API.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | Yes| Wallpaper type.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
import { BusinessError } from '@ohos.base';
 
wallpaper.restore(wallpaper.WallpaperType.WALLPAPER_SYSTEM).then(() => {
    console.log(`success to restore.`);
  }).catch((error: BusinessError) => {
    console.error(`failed to restore because: ${JSON.stringify(error)}`);
});
```

## wallpaper.setImage<sup>9+</sup>

setImage(source: string | image.PixelMap, wallpaperType: WallpaperType, callback: AsyncCallback&lt;void&gt;): void

Sets a specified source as the wallpaper of a specified type. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.SET_WALLPAPER

**System capability**: SystemCapability.MiscServices.Wallpaper

**System API**: This is a system API.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| source | string \| [image.PixelMap](../apis-image-kit/js-apis-image.md) | Yes| URI of a JPEG or PNG file, or pixel map of a PNG file.|
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | Yes| Wallpaper type.|
| callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result. If the wallpaper is set, **err** is **undefined**. Otherwise, **err** is an error object.|

**Example**

```ts
import { BusinessError } from '@ohos.base';
import image from '@ohos.multimedia.image';

// The source type is string.
let wallpaperPath = "/data/storage/el2/base/haps/entry/files/js.jpeg";
wallpaper.setImage(wallpaperPath, wallpaper.WallpaperType.WALLPAPER_SYSTEM, (error: BusinessError) => {
    if (error) {
        console.error(`failed to setImage because: ${JSON.stringify(error)}`);
        return;
     }
    console.log(`success to setImage.`);
});
  
// The source type is image.PixelMap.
let imageSource = image.createImageSource("file://" + wallpaperPath);
let opts: image.DecodingOptions = {
    desiredSize: {
        height: 3648,
        width: 2736
    }
};
imageSource.createPixelMap(opts).then((pixelMap: image.PixelMap) => {
    wallpaper.setImage(pixelMap, wallpaper.WallpaperType.WALLPAPER_SYSTEM, (error: BusinessError) => {
        if (error) {
            console.error(`failed to setImage because: ${JSON.stringify(error)}`);
            return;
        }
        console.log(`success to setImage.`);
    });
}).catch((error: BusinessError) => {
    console.error(`failed to createPixelMap because: ${JSON.stringify(error)}`);
});
```

## wallpaper.setImage<sup>9+</sup>

setImage(source: string | image.PixelMap, wallpaperType: WallpaperType): Promise&lt;void&gt;

Sets a specified source as the wallpaper of a specified type. This API uses a promise to return the result.

**Required permissions**: ohos.permission.SET_WALLPAPER

**System capability**: SystemCapability.MiscServices.Wallpaper

**System API**: This is a system API.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| source | string \| [image.PixelMap](../apis-image-kit/js-apis-image.md) | Yes| URI of a JPEG or PNG file, or pixel map of a PNG file.|
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | Yes| Wallpaper type.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
import { BusinessError } from '@ohos.base';
import image from '@ohos.multimedia.image';

// The source type is string.
let wallpaperPath = "/data/storage/el2/base/haps/entry/files/js.jpeg";
wallpaper.setImage(wallpaperPath, wallpaper.WallpaperType.WALLPAPER_SYSTEM).then(() => {
    console.log(`success to setImage.`);
}).catch((error: BusinessError) => {
    console.error(`failed to setImage because: ${JSON.stringify(error)}`);
});

// The source type is image.PixelMap.
let imageSource = image.createImageSource("file://" + wallpaperPath);
let opts: image.DecodingOptions = {
    desiredSize: {
        height: 3648,
        width: 2736
    }
};
imageSource.createPixelMap(opts).then((pixelMap: image.PixelMap) => {
    wallpaper.setImage(pixelMap, wallpaper.WallpaperType.WALLPAPER_SYSTEM).then(() => {
        console.log(`success to setImage.`);
    }).catch((error: BusinessError) => {
        console.error(`failed to setImage because: ${JSON.stringify(error)}`);
    });
}).catch((error: BusinessError) => {
    console.error(`failed to createPixelMap because: ${JSON.stringify(error)}`);
});
```

## wallpaper.getImage<sup>9+</sup>

getImage(wallpaperType: WallpaperType, callback: AsyncCallback&lt;image.PixelMap&gt;): void;

Obtains the pixel map for the wallpaper of the specified type. This API only works for the static wallpaper set using **setImage**. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_WALLPAPER

**System capability**: SystemCapability.MiscServices.Wallpaper

**System API**: This is a system API.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | Yes| Wallpaper type.|
| callback | AsyncCallback&lt;[image.PixelMap](../apis-image-kit/js-apis-image.md)&gt; | Yes| Callback used to return the result. If the operation is successful, the pixel map of the wallpaper is returned. Otherwise, error information is returned.|

**Example**

```ts
import { BusinessError } from '@ohos.base';
import image from '@ohos.multimedia.image';

wallpaper.getImage(wallpaper.WallpaperType.WALLPAPER_SYSTEM, (error: BusinessError, data: image.PixelMap) => {
    if (error) {
        console.error(`failed to getImage because: ${JSON.stringify(error)}`);
        return;
    }
    console.log(`success to getImage: ${JSON.stringify(data)}`);
});
```


## wallpaper.getImage<sup>9+</sup>

getImage(wallpaperType: WallpaperType): Promise&lt;image.PixelMap&gt;

Obtains the pixel map for the wallpaper of the specified type. This API only works for the static wallpaper set using **setImage**. This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_WALLPAPER

**System capability**: SystemCapability.MiscServices.Wallpaper

**System API**: This is a system API.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | Yes| Wallpaper type.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;[image.PixelMap](../apis-image-kit/js-apis-image.md)&gt; | Promise used to return the result. If the operation is successful, the pixel map of the wallpaper is returned. Otherwise, error information is returned.|

**Example**

```ts
import { BusinessError } from '@ohos.base';
import image from '@ohos.multimedia.image';

wallpaper.getImage(wallpaper.WallpaperType.WALLPAPER_SYSTEM).then((data: image.PixelMap) => {
    console.log(`success to getImage: ${JSON.stringify(data)}`);
  }).catch((error: BusinessError) => {
    console.error(`failed to getImage because: ${JSON.stringify(error)}`);
});
```



## wallpaper.getPixelMap<sup>(deprecated)</sup>

getPixelMap(wallpaperType: WallpaperType, callback: AsyncCallback&lt;image.PixelMap&gt;): void;

Obtains the pixel map for the wallpaper of the specified type. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9.

**Required permissions**: ohos.permission.GET_WALLPAPER

**System capability**: SystemCapability.MiscServices.Wallpaper

**System API**: This is a system API.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | Yes| Wallpaper type.|
| callback | AsyncCallback&lt;image.PixelMap&gt; | Yes| Callback used to return the result. If the operation is successful, the pixel map of the wallpaper is returned. Otherwise, error information is returned.|

**Example**

```ts
import { BusinessError } from '@ohos.base';
import image from '@ohos.multimedia.image';

wallpaper.getPixelMap(wallpaper.WallpaperType.WALLPAPER_SYSTEM, (error: BusinessError, data: image.PixelMap) => {
    if (error) {
        console.error(`failed to getPixelMap because: ${JSON.stringify(error)}`);
        return;
    }
    console.log(`success to getPixelMap : ${JSON.stringify(data)}`);
  });
```

## wallpaper.getPixelMap<sup>(deprecated)</sup>

getPixelMap(wallpaperType: WallpaperType): Promise&lt;image.PixelMap&gt;

Obtains the pixel map for the wallpaper of the specified type. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9.

**Required permissions**: ohos.permission.GET_WALLPAPER

**System capability**: SystemCapability.MiscServices.Wallpaper

**System API**: This is a system API.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | Yes| Wallpaper type.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;image.PixelMap&gt; | Promise used to return the result. If the operation is successful, the pixel map of the wallpaper is returned. Otherwise, error information is returned.|

**Example**

```ts
import { BusinessError } from '@ohos.base';
import image from '@ohos.multimedia.image';

wallpaper.getPixelMap(wallpaper.WallpaperType.WALLPAPER_SYSTEM).then((data: image.PixelMap) => {
    console.log(`success to getPixelMap : ${JSON.stringify(data)}`);
  }).catch((error: BusinessError) => {
    console.error(`failed to getPixelMap because: ${JSON.stringify(error)}`);
});
```
## wallpaper.getFile<sup>(deprecated)</sup>

getFile(wallpaperType: WallpaperType, callback: AsyncCallback&lt;number&gt;): void

Obtains the wallpaper of the specified type.

> **NOTE**
> 
> This API is supported since API version 8 and deprecated since API version 9.

**Required permissions**: ohos.permission.GET_WALLPAPER

**System capability**: SystemCapability.MiscServices.Wallpaper

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | Yes| Wallpaper type.|
| callback | AsyncCallback&lt;number&gt; | Yes| Callback used to return the result. If the operation is successful, the file descriptor ID to the wallpaper is returned. Otherwise, error information is returned.|

**Example**

```ts
import { BusinessError } from '@ohos.base';

wallpaper.getFile(wallpaper.WallpaperType.WALLPAPER_SYSTEM, (error: BusinessError, data: number) => {
    if (error) {
        console.error(`failed to getFile because: ${JSON.stringify(error)}`);
        return;
    }
    console.log(`success to getFile: ${JSON.stringify(data)}`);
});
```

## wallpaper.getFile<sup>(deprecated)</sup>

getFile(wallpaperType: WallpaperType): Promise&lt;number&gt;

Obtains the wallpaper of the specified type.

> **NOTE**
>
> This API is supported since API version 8 and deprecated since API version 9.

**Required permissions**: ohos.permission.GET_WALLPAPER

**System capability**: SystemCapability.MiscServices.Wallpaper

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | Yes| Wallpaper type.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;number&gt; | Promise used to return the result. If the operation is successful, the file descriptor ID to the wallpaper is returned. Otherwise, error information is returned.|

**Example**

```ts
import { BusinessError } from '@ohos.base';

wallpaper.getFile(wallpaper.WallpaperType.WALLPAPER_SYSTEM).then((data: number) => {
    console.log(`success to getFile: ${JSON.stringify(data)}`);
  }).catch((error: BusinessError) => {
    console.error(`failed to getFile because: ${JSON.stringify(error)}`);
});
```
