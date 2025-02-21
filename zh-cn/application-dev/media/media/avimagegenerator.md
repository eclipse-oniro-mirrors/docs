# 获取视频缩略图

使用AVImageGenerator可以实现从原始媒体资源中获取视频指定时间的缩略图，本开发指导将以获取一个视频资源的缩略图作为示例，向开发者讲解AVImageGenerator相关功能。

获取视频资源的缩略图的全流程包含：创建AVImageGenerator对象，设置资源，获取缩略图，销毁资源。

## 开发步骤及注意事项

详细的API说明请参考[AVImageGenerator API参考](../../reference/apis-media-kit/js-apis-media-sys.md#avimagegenerator11)。

1. 使用createAVImageGenerator()创建实例。

2. 设置资源：需要设置属性fdSrc（表示文件描述符）。
   > **说明：**
   >
   > 开发者需根据实际情况，确认资源有效性并设置fdSrc, 可以使用ResourceManager.getRawFd打开HAP资源文件描述符，使用方法可参考[ResourceManager API参考](../../reference/apis-localization-kit/js-apis-resource-manager.md#getrawfd9)。

3. 获取缩略图：调用fetchFrameByTime()，可以获取到一个PixelMap对象，该对象可用于图片显示。

4. 释放资源：调用release()销毁实例，释放资源。

## 完整示例

参考以下示例，设置文件描述符，获取一个视频指定时间的缩略图。

```ts
import media from '@ohos.multimedia.media'
import image from '@ohos.multimedia.image'

const TAG = 'MetadataDemo'
@Entry
@Component
struct Index {
  @State message: string = 'Hello World'

  // pixelMap对象声明，用于图片显示
  @State pixelMap: image.PixelMap | undefined = undefined;

  build() {
    Row() {
      Column() {
        Text(this.message).fontSize(50).fontWeight(FontWeight.Bold)
        Button() {
          Text('TestButton')
            .fontSize(30)
            .fontWeight(FontWeight.Bold)
        }
        .type(ButtonType.Capsule)
        .margin({
          top: 20
        })
        .backgroundColor('#0D9FFB')
        .width('60%')
        .height('5%')
        .onClick(() => {
          // 设置fdSrc, 获取视频的缩略图
          this.testFetchFrameByTime()
        })
        Image(this.pixelMap).width(300).height(300)
          .margin({
            top: 20
          })
      }
      .width('100%')
    }
    .height('100%')
  }

  // 在以下demo中，使用资源管理接口获取打包在HAP内的视频文件，通过设置fdSrc属性，
  // 获取视频指定时间的缩略图，并通过Image控件显示在屏幕上。
  async testFetchFrameByTime() {
    // 创建AVImageGenerator对象
    let avImageGenerator: media.AVImageGenerator = await media.createAVImageGenerator()
    // 设置fdSrc
    avImageGenerator.fdSrc = await getContext(this).resourceManager.getRawFd('demo.mp4');

    // 初始化入参
    let timeUs = 0
    let queryOption = media.AVImageQueryOptions.AV_IMAGE_QUERY_NEXT_SYNC
    let param: media.PixelMapParams = {
      width : 300,
      height : 300,
      colorFormat : media.PixelFormat.RGB_565
    }

    // 获取缩略图（promise模式）
    this.pixelMap = await avImageGenerator.fetchFrameByTime(timeUs, queryOption, param)

    // 释放资源（promise模式）
    avImageGenerator.release()
    console.info(TAG, `release success.`)
  }
}
```