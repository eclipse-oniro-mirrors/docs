# High-Performance Camera Photographing (for System Applications Only) (ArkTS)

As an important feature of the camera, high-performance photographing enables deferred delivery for photo capture and further reduces the response delay, delivering a better user experience. High-performance photographing is implemented as follows: After an application delivers a photographing request, the system quickly returns a thumbnail to the application, and the application stores the thumbnail and related information in the mediaLibrary. Then the subservice performs scheduling based on the system pressure and custom scenarios and sends the postprocessed original image to the mediaLibrary.

To develop high-performance photographing, perform the following steps:

- Check whether the device supports deferred delivery of a certain type.
- Enable deferred delivery (if supported).
- Listen for thumbnails, obtain a thumbnail proxy class object, and save the thumbnail to the mediaLibrary.

> **NOTE**
> 
> - Deferred delivery varies according to the device and type. Therefore, if the device or type is changed, you must enable the corresponding deferred delivery capability.
> - Deferred delivery must be enabled during the stream configuration. After the stream configuration is complete, enabling deferred delivery does not take effect.

## How to Develop

Read [Camera](../../reference/apis-camera-kit/js-apis-camera.md) for the API reference.

1. Import dependencies. Specifically, import the camera, image, and mediaLibrary modules.

   ```ts
   import camera from '@ohos.multimedia.camera';
   import image from '@ohos.multimedia.image';
   import mediaLibrary from '@ohos.multimedia.mediaLibrary';
   import fs from '@ohos.file.fs';
   import photoAccessHelper from '@ohos.file.photoAccessHelper';
   import { BusinessError } from '@ohos.base';
   ```

2. Determine the photo output stream.

   You can use the **photoProfiles** attribute of the [CameraOutputCapability](../../reference/apis-camera-kit/js-apis-camera.md#cameraoutputcapability) class to obtain the photo output streams supported by the device and use [createPhotoOutput](../../reference/apis-camera-kit/js-apis-camera.md#createphotooutput11) to create a photo output stream.

   ```ts
   function getPhotoOutput(cameraManager: camera.CameraManager, 
                           cameraOutputCapability: camera.CameraOutputCapability): camera.PhotoOutput | undefined {
     let photoProfilesArray: Array<camera.Profile> = cameraOutputCapability.photoProfiles;
     if (!photoProfilesArray) {
       console.error("createOutput photoProfilesArray == null || undefined");
     }
     let photoOutput: camera.PhotoOutput | undefined = undefined;
     try {
       photoOutput = cameraManager.createPhotoOutput(photoProfilesArray[0]);
     } catch (error) {
       let err = error as BusinessError;
       console.error(`Failed to createPhotoOutput. error: ${JSON.stringify(err)}`);
     }
     return photoOutput;
   }
   ```

3. Check whether the device supports deferred delivery of a certain type.

   ```ts
   function isDeferredImageDeliverySupported(photoOutput: camera.PhotoOutput): boolean {
     let isSupported: boolean = false;
     if (photoOutput !== null) {
       isSupported = photoOutput.isDeferredImageDeliverySupported(camera.DeferredDeliveryImageType.PHOTO);
     }
     console.info(`isDeferredImageDeliverySupported isSupported: ${isSupported}`);
     return isSupported;
   }
   ```

4. Enable deferred delivery.

   ```ts
   function EnableDeferredPhotoAbility(photoOutput: camera.PhotoOutput): void {
     photoOutput.deferImageDelivery(camera.DeferredDeliveryImageType.PHOTO);
   }
   ```

5. Check whether deferred delivery is enabled.

   ```ts
   function isDeferredImageDeliveryEnabled(photoOutput: camera.PhotoOutput): boolean {
   	 let isEnabled: boolean = false;
     if (photoOutput !== null) {
   	   isEnabled = photoOutput.isDeferredImageDeliveryEnabled(camera.DeferredDeliveryImageType.PHOTO);
     }
     console.info(`isDeferredImageDeliveryEnabled isEnabled: ${isEnabled}`);
     return isEnabled;
   }
   ```

6. Trigger photographing. This procedure is the same as that in the common photographing mode. For details, see [Camera Photographing](camera-shooting.md).

## Status Listening

1. Listen for thumbnails.

   ```ts
   function onPhotoOutputDeferredPhotoProxyAvailable(photoOutput: camera.PhotoOutput): void {
     photoOutput.on('deferredPhotoProxyAvailable', (err: BusinessError, proxyObj: camera.DeferredPhotoProxy): void => {
       if (err) {
         console.info(`deferredPhotoProxyAvailable error: ${JSON.stringify(err)}.`);
         return;
       }
       console.info('photoOutPutCallBack deferredPhotoProxyAvailable');
       // Obtain the pixel map of a thumbnail.
       proxyObj.getThumbnail().then((thumbnail: image.PixelMap) => {
         AppStorage.setOrCreate('proxyThumbnail', thumbnail);
       });
       // Call the mediaLibrary APIs to flush the thumbnail to the disk. See the code below.
       saveDeferredPhoto(proxyObj);
     });
   }
   ```

   

2. Call the mediaLibrary APIs to flush the thumbnail to the disk

   For details about how to obtain the context, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

   ```ts
   let context = getContext(this);
   
   async function saveDeferredPhoto(proxyObj: camera.DeferredPhotoProxy) {    
     try {
       // Create a photoAsset.
       let photoAccessHelper = PhotoAccessHelper.getPhotoAccessHelper(context);
       let testFileName = 'testFile' + Date.now() + '.jpg';
       let photoAsset = await photoAccessHelper.createAsset(testFileName);
       // Pass the thumbnail proxy class object to the mediaLibrary.
       let mediaRequest: PhotoAccessHelper.MediaAssetChangeRequest = new PhotoAccessHelper.MediaAssetChangeRequest(photoAsset);
       mediaRequest.addResource(PhotoAccessHelper.ResourceType.PHOTO_PROXY, proxyObj);
       let res = await photoAccessHelper.applyChanges(mediaRequest);
       console.info('saveDeferredPhoto success.');
     } catch (err) {
       console.error(`Failed to saveDeferredPhoto. error: ${JSON.stringify(err)}`);
     }
   }
   ```
