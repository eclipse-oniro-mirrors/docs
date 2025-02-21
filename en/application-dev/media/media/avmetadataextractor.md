# Obtaining Audio/Video Metadata

You can use **AVMetadataExtractor** to obtain metadata from a raw media asset. This topc walks you through on how to obtain the metadata of an audio asset. The process of obtaining the metadata of a video asset is similar. The only difference is that the process of obtaining the album cover is not required for a video asset, because no album cover is available in the video asset.

The full process of obtaining the metadata of an audio asset includes creating an **AVMetadataExtractor** instance, setting resources, obtaining the metadata, obtaining the album cover, and releasing the instance.

## How to Develop

Read [AVMetadataExtractor](../../reference/apis-media-kit/js-apis-media.md#avmetadataextractor11) for the API reference.

1. Call **createAVMetadataExtractor()** to create an **AVMetadataExtractor** instance.

2. Set resources. Specifically, set the **fdSrc** attribute (indicating the file descriptor) or **dataSrc** attribute (indicating the data source descriptor).
   > **NOTE**
   >
   > You need to check the resource validity and set either attribute based on the actual situation.
   >
   > - To set **fdSrc**, use **ResourceManager.getRawFd** to obtain the file descriptor of the resource file packed in the HAP. For details, see [ResourceManager API Reference](../../reference/apis-localization-kit/js-apis-resource-manager.md#getrawfd9).
   >
   > - To set **dataSrc**, set **callback** in **dataSrc** to ensure that the corresponding resource can be correctly read when the callback is invoked, and use the application sandbox directory to access the resource. For details, see [Obtaining Application File Paths](../../application-models/application-context-stage.md#obtaining-application-file-paths). For details about the application sandbox and how to push files to the application sandbox directory, see [File Management](../../file-management/app-sandbox-directory.md).

3. Obtain the metadata. Specifically, call **fetchMetadata()** to obtain an **AVMetadata** object, the attributes of which are the metadata of the media asset.

4. (Optional) Call **fetchAlbumCover()** to obtain the album cover.

5. Call **release()** to release the **AVMetadataExtractor** instance.

## Sample Code

Refer to the sample code below to set the file descriptor and obtain the metadata and album cover of an audio asset.

```ts
import media from '@ohos.multimedia.media'
import image from '@ohos.multimedia.image'
import type common from '@ohos.app.ability.common';
import fs from '@ohos.file.fs';

const TAG = 'MetadataDemo'
@Entry
@Component
struct Index {
  @State message: string = 'Hello World'

  // Declare a pixelMap object, which is used for image display.
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
          // Set fdSrc and obtain the audio metadata and album cover (callback mode).
          this.testFetchMetadataFromFdSrcByCallback()
          // Set fdSrc and obtain the audio metadata and album cover (promise mode).
          this.testFetchMetadataFromFdSrcByPromise()
          // Set dataSrc and obtain the audio metadata and album cover.
          this.testFetchMetadataFromDataSrc()
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

  // The demo below uses the resource manager API to obtain the audio file packed in the HAP. By setting fdSrc, it obtains and displays the audio metadata,
  // obtains the audio album cover, and displays it on the screen through the Image component. This demo calls APIs in callback mode.
  async testFetchMetadataFromFdSrcByCallback() {
    // Create an AVMetadataExtractor instance.
    let avMetadataExtractor: media.AVMetadataExtractor = await media.createAVMetadataExtractor()

    // Set the fdSrc attribute.
    avMetadataExtractor.fdSrc = await getContext(this).resourceManager.getRawFd('cover.mp3');

    // Obtain the metadata (callback mode).
    avMetadataExtractor.fetchMetadata((error, metadata) => {
      if (error) {
        console.error(TAG, `fetchMetadata callback failed, err = ${JSON.stringify(error)}`)
        return
      }
      console.info(TAG, `fetchMetadata callback success, genre: ${metadata.genre}`)
    })

    // Obtain the album cover (callback mode).
    avMetadataExtractor.fetchAlbumCover((err, pixelMap) => {
      if (err) {
        console.error(TAG, `fetchAlbumCover callback failed, err = ${JSON.stringify(err)}`)
        return
      }
      this.pixelMap = pixelMap

      // Release the instance (callback mode).
      avMetadataExtractor.release((error) => {
        if (error) {
          console.error(TAG, `release failed, err = ${JSON.stringify(error)}`)
          return
        }
        console.info(TAG, `release success.`)
      })
    })
  }

  // The demo below uses the resource manager API to obtain the audio file packed in the HAP. By setting fdSrc, it obtains and displays the audio metadata,
  // obtains the audio album cover, and displays it on the screen through the Image component. This demo calls APIs in promise mode.
  async testFetchMetadataFromFdSrcByPromise() {
    // Create an AVMetadataExtractor instance.
    let avMetadataExtractor: media.AVMetadataExtractor = await media.createAVMetadataExtractor()
    // Set the fdSrc attribute.
    avMetadataExtractor.fdSrc = await getContext(this).resourceManager.getRawFd('cover.mp3');

    // Obtain the metadata (promise mode).
    let metadata = await avMetadataExtractor.fetchMetadata()
    console.info(TAG, `get meta data, hasAudio: ${metadata.hasAudio}`)

    // Obtain the album cover (promise mode).
    this.pixelMap = await avMetadataExtractor.fetchAlbumCover()

    // Release the instance (promise mode).
    avMetadataExtractor.release()
    console.info(TAG, `release success.`)
  }

  // The demo below uses the fs API to open the sandbox directory and obtain the audio file address. By setting dataSrc, it obtains and displays the audio metadata,
  // obtains the audio album cover, and displays it on the screen through the Image component.
  async testFetchMetadataFromDataSrc() {
    let context = getContext(this) as common.UIAbilityContext
    // Obtain the sandbox address filesDir through UIAbilityContext. The stage model is used as an example.
    let filePath: string = context.filesDir + '/cover.mp3';
    let fd: number = fs.openSync(filePath, 0o0).fd;
    let fileSize: number = fs.statSync(filePath).size;
    // Set the dataSrc descriptor, obtain resources from the file through a callback, and write the resources to the buffer.
    let dataSrc: media.AVDataSrcDescriptor = {
      fileSize: fileSize,
      callback: (buffer, len, pos) => {
        if (buffer == undefined || len == undefined || pos == undefined) {
          console.error(TAG, `dataSrc callback param invalid`)
          return -1
        }

        class Option {
          offset: number | undefined = 0;
          length: number | undefined = len;
          position: number | undefined = pos;
        }
        let options = new Option();
        let num = fs.readSync(fd, buffer, options)
        console.info(TAG, 'readAt end, num: ' + num)
        if (num > 0 && fileSize >= pos) {
          return num;
        }
        return -1;
      }
    }

    // Create an AVMetadataExtractor instance.
    let avMetadataExtractor = await media.createAVMetadataExtractor()
    // Set the dataSrc attribute.
    avMetadataExtractor.dataSrc = dataSrc;

    // Obtain the metadata (promise mode).
    let metadata = await avMetadataExtractor.fetchMetadata()
    console.info(TAG, `get meta data, mimeType: ${metadata.mimeType}`)

    // Obtain the album cover (promise mode).
    this.pixelMap = await avMetadataExtractor.fetchAlbumCover()

    // Release the instance (promise mode).
    avMetadataExtractor.release()
    console.info(TAG, `release data source success.`)
  }
}
```
