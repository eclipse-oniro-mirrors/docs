# @ohos.screenshot (屏幕截图)(系统接口)

本模块提供屏幕截图的能力，截取屏幕时支持设置截取的区域、大小等图像信息。

>  **说明：**
>
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```ts
import screenshot from '@ohos.screenshot';
```

## ScreenshotOptions

设置截取图像的信息。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core


| 名称                 | 类型          | 必填 | 说明                                                         |
| ---------------------- | ------------- | ---- | ------------------------------------------------------------ |
| screenRect             | [Rect](#rect) | 否   | 表示截取图像的区域，不传值默认为全屏。                       |
| imageSize              | [Size](#size) | 否   | 表示截取图像的大小，不传值默认为全屏。                       |
| rotation               | number        | 否   | 表示截取图像的旋转角度，当前仅支持输入值为0，默认值为0，该参数应为整数。     |
| displayId<sup>8+</sup> | number        | 否   | 表示截取图像的显示设备[Display](js-apis-display.md#display)的ID号，该参数应为整数。 |


## Rect

表示截取图像的区域。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

| 名称 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| left   | number | 是   | 表示截取图像区域的左边界，单位为px，该参数应为整数。 |
| top    | number | 是   | 表示截取图像区域的上边界，单位为px，该参数应为整数。 |
| width  | number | 是   | 表示截取图像区域的宽度，单位为px，该参数应为整数。 |
| height | number | 是   | 表示截取图像区域的高度，单位为px，该参数应为整数。 |


## Size

表示截取图像的大小。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

| 名称 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| width  | number | 是   | 表示截取图像的宽度，单位为px，该参数应为整数。 |
| height | number | 是   | 表示截取图像的高度，单位为px，该参数应为整数。 |

## screenshot.save

save(options: ScreenshotOptions, callback: AsyncCallback&lt;image.PixelMap&gt;): void

获取屏幕截图。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**需要权限**：ohos.permission.CAPTURE_SCREEN，仅系统应用可用。

**参数：**

| 参数名   | 类型                                    | 必填 | 说明                                                         |
| -------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
| options  | [ScreenshotOptions](#screenshotoptions) | 是   | 该类型的参数包含screenRect、imageSize、rotation、displayId四个参数，可以分别设置这四个参数。 |
| callback | AsyncCallback&lt;[image.PixelMap](../apis-image-kit/js-apis-image.md#pixelmap7)&gt;     | 是   | 回调函数。返回一个PixelMap对象。                                   |

**错误码：**

以下错误码的详细介绍请参见[屏幕错误码](errorcode-display.md)。

| 错误码ID | 错误信息 |
| ------- | -------------------------- |
| 1400001 | Invalid display or screen. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import image from '@ohos.multimedia.image';

let screenshotOptions: screenshot.ScreenshotOptions = {
  "screenRect": {
    "left": 200,
    "top": 100,
    "width": 200,
    "height": 200 },
  "imageSize": {
    "width": 300,
    "height": 300 },
  "rotation": 0,
  "displayId": 0
};
try {
  screenshot.save(screenshotOptions, (err: BusinessError, pixelMap: image.PixelMap) => {
    if (err) {
      console.log('Failed to save screenshot. Code: ' + JSON.stringify(err));
      return;
    }
    console.log('Succeeded in saving screenshot. Pixel bytes number: ' + pixelMap.getPixelBytesNumber());
    pixelMap.release(); // PixelMap使用完后及时释放内存
  });
} catch (exception) {
  console.error('Failed to save screenshot. Code: ' + JSON.stringify(exception));
};
```

## screenshot.save

save(callback: AsyncCallback&lt;image.PixelMap&gt;): void

获取屏幕截图。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**需要权限**：ohos.permission.CAPTURE_SCREEN，仅系统应用可用。

**参数：**

| 参数名   | 类型                                    | 必填 | 说明                                                         |
| -------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback&lt;[image.PixelMap](../apis-image-kit/js-apis-image.md#pixelmap7)&gt;     | 是   | 回调函数。返回一个PixelMap对象。                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import image from '@ohos.multimedia.image';

try {
  screenshot.save((err: BusinessError, pixelMap: image.PixelMap) => {
    if (err) {
      console.log('Failed to save screenshot. Code: ' + JSON.stringify(err));
      return;
    }
    console.log('Succeeded in saving screenshot. Pixel bytes number: ' + pixelMap.getPixelBytesNumber());
    pixelMap.release(); // PixelMap使用完后及时释放内存
  });
} catch (exception) {
  console.error('Failed to save screenshot. Code: ' + JSON.stringify(exception));
};
```

## screenshot.save

save(options?: ScreenshotOptions): Promise&lt;image.PixelMap&gt;

获取屏幕截图。

**系统接口：** 此接口为系统接口。

**系统能力：** SystemCapability.WindowManager.WindowManager.Core

**需要权限**：ohos.permission.CAPTURE_SCREEN，仅系统应用可用。

**参数：**

| 参数名  | 类型                                    | 必填 | 说明                                                         |
| ------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
| options | [ScreenshotOptions](#screenshotoptions) | 否   | 该类型的参数包含screenRect、imageSize、rotation、displayId四个参数，可以分别设置这四个参数。 |

**返回值：**

| 类型                          | 说明                                            |
| ----------------------------- | ----------------------------------------------- |
| Promise&lt;[image.PixelMap](../apis-image-kit/js-apis-image.md#pixelmap7)&gt; | Promise对象。返回一个PixelMap对象。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import image from '@ohos.multimedia.image';

let screenshotOptions: screenshot.ScreenshotOptions = {
  "screenRect": {
    "left": 200,
    "top": 100,
    "width": 200,
    "height": 200 },
  "imageSize": {
    "width": 300,
    "height": 300 },
  "rotation": 0,
  "displayId": 0
};
try {
  let promise = screenshot.save(screenshotOptions);
  promise.then((pixelMap: image.PixelMap) => {
    console.log('Succeeded in saving screenshot. Pixel bytes number: ' + pixelMap.getPixelBytesNumber());
    pixelMap.release(); // PixelMap使用完后及时释放内存
  }).catch((err: BusinessError) => {
    console.log('Failed to save screenshot. Code: ' + JSON.stringify(err));
  });
} catch (exception) {
  console.error('Failed to save screenshot. Code: ' + JSON.stringify(exception));
};
```
