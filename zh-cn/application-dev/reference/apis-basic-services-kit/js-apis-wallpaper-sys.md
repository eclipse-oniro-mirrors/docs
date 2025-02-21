# @ohos.wallpaper (壁纸)(系统接口)

壁纸管理服务为OpenHarmony系统服务，提供壁纸切换功能。从API 9开始壁纸管理的接口调整为系统API，壁纸的切换只能通过系统应用来完成。壁纸管理提供壁纸切换通道，使用壁纸的应用（如：桌面）需订阅壁纸变化通知并刷新壁纸显示。

> **说明：**
> 
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> 当前页面仅包含本模块的系统接口，其他公开接口参见[@ohos.wallpaper (壁纸)](js-apis-wallpaper.md)


## 导入模块


```ts
import wallpaper from '@ohos.wallpaper';
```
## WallpaperResourceType<sup>10+</sup>

定义壁纸资源的枚举类型。

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统接口**：此接口为系统接口。

| 名称 | 值 |说明 |
| -------- | -------- |-------- |
| DEFAULT | 0 |默认为图片资源。 |
| PICTURE | 1 |图片资源。 |
| VIDEO | 2 |视频资源。 |
| PACKAGE | 3 |包资源。 |

## wallpaper.setVideo<sup>10+</sup>

setVideo(source: string, wallpaperType: WallpaperType, callback: AsyncCallback&lt;void&gt;): void

将视频资源设置为桌面或锁屏的动态壁纸。使用callback异步回调。

**需要权限**：ohos.permission.SET_WALLPAPER

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统接口**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| source | string | 是 | mp4文件的Uri路径。 |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | 是 | 壁纸类型。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数，设置壁纸成功，error为undefined，否则返回error信息。 |

**示例：**

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

将视频资源设置为桌面或锁屏的动态壁纸。使用promise异步回调。

**需要权限**：ohos.permission.SET_WALLPAPER

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统接口**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| source | string | 是 | mp4文件的Uri路径。 |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | 是 | 壁纸类型。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

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

将指定的zip资源包设置为桌面或锁屏的壁纸资源，仅当com.ohos.sceneboard存在时，支持使用该接口。且具有ohos.permission.GET_WALLPAPER权限的应用可以访问/data/wallpaper/目录获取设置的资源。使用callback异步回调。

**需要权限**：ohos.permission.SET_WALLPAPER

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统接口**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| source | string | 是 | 指定的zip资源包。 |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | 是 | 壁纸类型。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数，设置壁纸成功，error为undefined，否则返回error信息。 |

**示例：**

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

将指定的zip资源包设置为桌面或锁屏的壁纸资源，仅当com.ohos.sceneboard存在时，支持使用该接口。且具有ohos.permission.GET_WALLPAPER权限的应用可以访问/data/wallpaper/目录获取设置的资源。使用Promise异步回调。

**需要权限**：ohos.permission.SET_WALLPAPER

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统接口**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| source | string | 是 | 指定的zip资源包。 |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | 是 | 壁纸类型。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

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

订阅壁纸变化通知事件。不支持多线程并发调用。

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统接口**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 事件回调类型。支持的事件为'wallpaperChange'，完成壁纸切换后触发该事件。 |
| callback | function | 是 | 壁纸变化触发该回调方法，返回壁纸类型和壁纸资源类型。<br/>- wallpaperType：壁纸类型。<br/>- resourceType：壁纸资源类型。<br/>- uri：壁纸资源地址。 |

**示例：**

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

取消订阅壁纸变化通知事件。不支持多线程并发调用。

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统接口**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| type | string | 是 | 事件回调类型。支持的事件为'wallpaperChange'，完成壁纸切换后触发该事件。 |
| callback | function | 否 |   表示要取消的壁纸变化回调，不填写该参数则取消订阅该type对应的所有回调。<br/>- wallpaperType：壁纸类型。<br/>- resourceType：壁纸资源类型。<br/>- uri：壁纸资源地址。 |

**示例：**

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
    // 取消订阅listener
    wallpaper.off('wallpaperChange', listener);
} catch (error) {
    console.error(`failed to off because: ${JSON.stringify(error)}`);
}

try {
    // 取消所有'wallpaperChange'类型的订阅
    wallpaper.off('wallpaperChange');
} catch (error) {
    console.error(`failed to off because: ${JSON.stringify(error)}`);
}
```

## wallpaper.getColorsSync<sup>9+</sup>

getColorsSync(wallpaperType: WallpaperType): Array&lt;RgbaColor&gt;

获取指定类型壁纸的主要颜色信息。

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统接口**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | 是 | 壁纸类型。 |

**返回值**：

| 类型 | 说明 |
| -------- | -------- |
| Array&lt;[RgbaColor](js-apis-wallpaper.md#rgbacolordeprecated)&gt; | 返回壁纸的主要颜色信息。 |

**示例**：

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

获取壁纸的最小高度值。

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统接口**：此接口为系统接口。

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 返回壁纸的最小高度值，单位是像素。如果返回值等于0，说明没有设置壁纸，调用者应该使用默认显示的高度值代替。 |

**示例：**

```ts
let minHeight = wallpaper.getMinHeightSync();
```

## wallpaper.getMinWidthSync<sup>9+</sup>

getMinWidthSync(): number

获取壁纸的最小宽度值。

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统接口**：此接口为系统接口。

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| number | 壁纸的最小宽度值，单位是像素。如果返回值等于0，说明没有设置壁纸，调用者应该使用默认显示的宽度值代替。 |

**示例：**

```ts
let minWidth = wallpaper.getMinWidthSync();
```

## wallpaper.restore<sup>9+</sup>

restore(wallpaperType: WallpaperType, callback: AsyncCallback&lt;void&gt;): void

移除指定类型的壁纸，恢复为默认显示的壁纸。使用callback异步回调。

**需要权限**：ohos.permission.SET_WALLPAPER

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统接口**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | 是 | 壁纸类型。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数，移除壁纸成功，error为undefined，否则返回error信息。 |

**示例：**

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

移除指定类型的壁纸，恢复为默认显示的壁纸。使用promise异步回调。

**需要权限**：ohos.permission.SET_WALLPAPER

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统接口**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | 是 | 壁纸类型。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

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

将指定资源设置为指定类型的壁纸。使用callback异步回调。

**需要权限**：ohos.permission.SET_WALLPAPER

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统接口**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| source | string \| [image.PixelMap](../apis-image-kit/js-apis-image.md) | 是 | JPEG或PNG文件的Uri路径，或者PNG格式文件的位图。 |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | 是 | 壁纸类型。 |
| callback | AsyncCallback&lt;void&gt; | 是 | 回调函数，设置壁纸成功，error为undefined，否则返回error信息。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import image from '@ohos.multimedia.image';

// source类型为string
let wallpaperPath = "/data/storage/el2/base/haps/entry/files/js.jpeg";
wallpaper.setImage(wallpaperPath, wallpaper.WallpaperType.WALLPAPER_SYSTEM, (error: BusinessError) => {
    if (error) {
        console.error(`failed to setImage because: ${JSON.stringify(error)}`);
        return;
     }
    console.log(`success to setImage.`);
});
  
// source类型为image.PixelMap
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

将指定资源设置为指定类型的壁纸。使用promise异步回调。

**需要权限**：ohos.permission.SET_WALLPAPER

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统接口**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| source | string \| [image.PixelMap](../apis-image-kit/js-apis-image.md) | 是 | JPEG或PNG文件的Uri路径，或者PNG格式文件的位图。 |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | 是 | 壁纸类型。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import image from '@ohos.multimedia.image';

// source类型为string
let wallpaperPath = "/data/storage/el2/base/haps/entry/files/js.jpeg";
wallpaper.setImage(wallpaperPath, wallpaper.WallpaperType.WALLPAPER_SYSTEM).then(() => {
    console.log(`success to setImage.`);
}).catch((error: BusinessError) => {
    console.error(`failed to setImage because: ${JSON.stringify(error)}`);
});

// source类型为image.PixelMap
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

获取壁纸图片的像素图，且只能获取使用setImage设置的静态壁纸。使用callback异步回调。

**需要权限**：ohos.permission.GET_WALLPAPER

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统接口**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | 是 | 壁纸类型。 |
| callback | AsyncCallback&lt;[image.PixelMap](../apis-image-kit/js-apis-image.md)&gt; | 是 | 回调函数，调用成功则返回壁纸图片的像素图对象，调用失败则返回error信息。 |

**示例：**

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

获取壁纸图片的像素图，且只能获取使用setImage设置的静态壁纸。使用promise异步回调。

**需要权限**：ohos.permission.GET_WALLPAPER

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统接口**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | 是 | 壁纸类型。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;[image.PixelMap](../apis-image-kit/js-apis-image.md)&gt; | 调用成功则返回壁纸图片的像素图对象，调用失败则返回error信息。 |

**示例：**

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

获取壁纸图片的像素图。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃。

**需要权限**：ohos.permission.GET_WALLPAPER

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统接口**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | 是 | 壁纸类型。 |
| callback | AsyncCallback&lt;image.PixelMap&gt; | 是 | 回调函数，调用成功则返回壁纸图片的像素图对象，调用失败则返回error信息。 |

**示例：**

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

获取壁纸图片的像素图。

> **说明：**
>
> 从 API version 7开始支持，从API version 9开始废弃。

**需要权限**：ohos.permission.GET_WALLPAPER

**系统能力**: SystemCapability.MiscServices.Wallpaper

**系统接口**：此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | 是 | 壁纸类型。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;image.PixelMap&gt; | 调用成功则返回壁纸图片的像素图对象，调用失败则返回error信息。 |

**示例：**

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

获取指定类型的壁纸文件。

> **说明：**
> 
> 从 API version 8开始支持，从API version 9开始废弃。

**需要权限**：ohos.permission.GET_WALLPAPER

**系统能力**: SystemCapability.MiscServices.Wallpaper

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | 是 | 壁纸类型。 |
| callback | AsyncCallback&lt;number&gt; | 是 | 回调函数，调用成功则返回壁纸文件描述符ID，调用失败则返回error信息。 |

**示例：**

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

获取指定类型的壁纸文件。

> **说明：**
>
> 从 API version 8开始支持，从API version 9开始废弃。

**需要权限**：ohos.permission.GET_WALLPAPER

**系统能力**: SystemCapability.MiscServices.Wallpaper

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| wallpaperType | [WallpaperType](js-apis-wallpaper.md#wallpapertype7) | 是 | 壁纸类型。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise&lt;number&gt; | 调用成功则返回壁纸文件描述符ID，调用失败则返回error信息。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

wallpaper.getFile(wallpaper.WallpaperType.WALLPAPER_SYSTEM).then((data: number) => {
    console.log(`success to getFile: ${JSON.stringify(data)}`);
  }).catch((error: BusinessError) => {
    console.error(`failed to getFile because: ${JSON.stringify(error)}`);
});
```