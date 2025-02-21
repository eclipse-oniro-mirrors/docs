# High-Performance Camera Photographing Sample (for System Applications Only) (ArkTS)

This topic provides sample code that covers the complete high-performance photographing process to help you understand the complete API calling sequence.

Before referring to the sample code, you are advised to read [High-Performance Camera Photographing (for System Applications Only) (ArkTS)] (camera-deferred-photo.md), [Device Input Management](camera-device-input.md), [Camera Session Management](camera-session-management.md), and [Camera Photographing](camera-shooting.md).

## Development Process

After obtaining the output stream capabilities supported by the camera, create a photo stream.

## Sample Code

For details about how to obtain the context, see [Obtaining the Context of UIAbility](../../application-models/uiability-usage.md#obtaining-the-context-of-uiability).

```ts
import camera from '@ohos.multimedia.camera';
import image from '@ohos.multimedia.image';
import { BusinessError } from '@ohos.base';
import common from '@ohos.app.ability.common';
import fs from '@ohos.file.fs';
import PhotoAccessHelper from '@ohos.file.photoAccessHelper';

let context = getContext(this);

// Flush the original image in write-file mode.
async function savePicture(photoObj: camera.Photo): Promise<void> {
  let photoAccessHelper = PhotoAccessHelper.getPhotoAccessHelper(context);
  let testFileName = 'testFile' + Date.now() + '.jpg';
  // To call createAsset(), the application must have the ohos.permission.READ_IMAGEVIDEO and ohos.permission.WRITE_IMAGEVIDEO permissions.
  let photoAsset = await photoAccessHelper.createAsset(testFileName);
  const fd = await photoAsset.open('rw');
  let buffer: ArrayBuffer | undefined = undefined;
  photoObj.main.getComponent(image.ComponentType.JPEG, (errCode: BusinessError, component: image.Component): void => {
    if (errCode || component === undefined) {
      console.error('getComponent failed');
      return;
    }
    if (component.byteBuffer) {
      buffer = component.byteBuffer;
    } else {
      console.error('byteBuffer is null');
      return;
    }
  });
  if (buffer) {
    await fs.write(fd, buffer);
  }
  await photoAsset.close(fd);
  await photoObj.release(); 
}

// Flush the thumbnail by calling the mediaLibrary API.
async function saveDeferredPhoto(proxyObj: camera.DeferredPhotoProxy): Promise<void> {    
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

async function deferredPhotoCase(baseContext: common.BaseContext, surfaceId: string): Promise<void> {
  // Create a CameraManager object.
  let cameraManager: camera.CameraManager = camera.getCameraManager(baseContext);
  if (!cameraManager) {
    console.error("camera.getCameraManager error");
    return;
  }
  // Listen for camera status changes.
  cameraManager.on('cameraStatus', (err: BusinessError, cameraStatusInfo: camera.CameraStatusInfo) => {
    console.info(`camera : ${cameraStatusInfo.camera.cameraId}`);
    console.info(`status: ${cameraStatusInfo.status}`);
  });

  // Obtain the camera list.
  let cameraArray: Array<camera.CameraDevice> = cameraManager.getSupportedCameras();
  if (cameraArray.length <= 0) {
    console.error("cameraManager.getSupportedCameras error");
    return;
  }

  for (let index = 0; index < cameraArray.length; index++) {
    console.info('cameraId : ' + cameraArray[index].cameraId);                          // Obtain the camera ID.
    console.info('cameraPosition : ' + cameraArray[index].cameraPosition);              // Obtain the camera position.
    console.info('cameraType : ' + cameraArray[index].cameraType);                      // Obtain the camera type.
    console.info('connectionType : ' + cameraArray[index].connectionType);              // Obtain the camera connection type.
  }

  // Create a camera input stream.
  let cameraInput: camera.CameraInput | undefined = undefined;
  try {
    cameraInput = cameraManager.createCameraInput(cameraArray[0]);
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to createCameraInput errorCode = ' + err.code);
  }
  if (cameraInput === undefined) {
    return;
  }

  // Listen for camera input errors.
  let cameraDevice: camera.CameraDevice = cameraArray[0];
  cameraInput.on('error', cameraDevice, (error: BusinessError) => {
    console.error(`Camera input error code: ${error.code}`);
  })

  // Open a camera.
  await cameraInput.open();

  // Obtain the supported modes.
  let sceneModes: Array<camera.SceneMode> = cameraManager.getSupportedSceneModes(cameraArray[0]);
  let isSupportPhotoMode: boolean = sceneModes.indexOf(camera.SceneMode.NORMAL_PHOTO) >= 0;
  if (!isSupportPhotoMode) {
    console.error('photo mode not support');
    return;
  }
  // Obtain the output streams supported by the camera.
  let cameraOutputCap: camera.CameraOutputCapability = cameraManager.getSupportedOutputCapability(cameraArray[0], camera.SceneMode.NORMAL_PHOTO);
  if (!cameraOutputCap) {
    console.error("cameraManager.getSupportedOutputCapability error");
    return;
  }
  console.info("outputCapability: " + JSON.stringify(cameraOutputCap));

  let previewProfilesArray: Array<camera.Profile> = cameraOutputCap.previewProfiles;
  if (!previewProfilesArray) {
    console.error("createOutput previewProfilesArray == null || undefined");
  }

  let photoProfilesArray: Array<camera.Profile> = cameraOutputCap.photoProfiles;
  if (!photoProfilesArray) {
    console.error("createOutput photoProfilesArray == null || undefined");
  }

  // Create a preview output stream. For details about the surfaceId parameter, see the XComponent. The preview stream uses the surface provided by the XComponent.
  let previewOutput: camera.PreviewOutput | undefined = undefined;
  try {
    previewOutput = cameraManager.createPreviewOutput(previewProfilesArray[0], surfaceId);
  } catch (error) {
    let err = error as BusinessError;
    console.error(`Failed to create the PreviewOutput instance. error code: ${err.code}`);
  }
  if (previewOutput === undefined) {
    return;
  }
  // Listen for preview output errors.
  previewOutput.on('error', (error: BusinessError) => {
    console.error(`Preview output error code: ${error.code}`);
  });
  // Create a photo output stream.
  let photoOutput: camera.PhotoOutput | undefined = undefined;
  try {
    photoOutput = cameraManager.createPhotoOutput(photoProfilesArray[0]);
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to createPhotoOutput errorCode = ' + err.code);
  }
  if (photoOutput === undefined) {
    return;
  }
  // Create a session.
  let photoSession: camera.PhotoSession | undefined = undefined;
  try {
    photoSession = cameraManager.createSession(camera.SceneMode.NORMAL_PHOTO) as camera.PhotoSession;
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to create the photoSession instance. errorCode = ' + err.code);
  }
  if (photoSession === undefined) {
    return;
  }
  // Listen for session errors.
  photoSession.on('error', (error: BusinessError) => {
    console.error(`Capture session error code: ${error.code}`);
  });

  // Start configuration for the session.
  try {
    photoSession.beginConfig();
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to beginConfig. errorCode = ' + err.code);
  }

  // Add the camera input stream to the session.
  try {
    photoSession.addInput(cameraInput);
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to addInput. errorCode = ' + err.code);
  }

  // Add the preview output stream to the session.
  try {
    photoSession.addOutput(previewOutput);
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to addOutput(previewOutput). errorCode = ' + err.code);
  }

  // Add the photo output stream to the session.
  try {
    photoSession.addOutput(photoOutput);
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to addOutput(photoOutput). errorCode = ' + err.code);
  }

  // Register a callback to listen for original images.
  photoOutput.on('photoAvailable', (err: BusinessError, photoObj: camera.Photo): void => {
    if (err) {
      console.info(`photoAvailable error: ${JSON.stringify(err)}.`);
      return;
    }
    savePicture(photoObj).then(() => {
      // Release the photo object after the flushing is complete.
      photoObj.release();
    });
  });

  // Register a callback to listen for thumbnail proxies.
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
    // Call the mediaLibrary API to flush the thumbnail.
    saveDeferredPhoto(proxyObj).then(() => {
      // Release the thumbnail proxy class object after the flushing is complete.
      proxyObj.release();
    });
  });
    
  // Check whether deferred delivery is supported.
  let isSupportDeferred: boolean = photoOutput.isDeferredImageDeliverySupported(camera.DeferredDeliveryImageType.PHOTO);
  console.info('isDeferredImageDeliverySupported res:' + isSupportDeferred);
  if (isSupportDeferred) {
    // Enable deferred delivery.
	photoOutput.deferImageDelivery(camera.DeferredDeliveryImageType.PHOTO);
    // Check whether deferred delivery is enabled.
    let isSupportEnabled: boolean = photoOutput.isDeferredImageDeliveryEnabled(camera.DeferredDeliveryImageType.PHOTO);
    console.info('isDeferredImageDeliveryEnabled res:' + isSupportEnabled);
  }

  // Commit the session configuration.
  await photoSession.commitConfig();

  // Start the session.
  await photoSession.start().then(() => {
    console.info('Promise returned to indicate the session start success.');
  });
  // Check whether the camera has flash.
  let flashStatus: boolean = false;
  try {
    flashStatus = photoSession.hasFlash();
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to hasFlash. errorCode = ' + err.code);
  }
  console.info('Returned with the flash light support status:' + flashStatus);

  if (flashStatus) {
    // Check whether the auto flash mode is supported.
    let flashModeStatus: boolean = false;
    try {
      let status: boolean = photoSession.isFlashModeSupported(camera.FlashMode.FLASH_MODE_AUTO);
      flashModeStatus = status;
    } catch (error) {
      let err = error as BusinessError;
      console.error('Failed to check whether the flash mode is supported. errorCode = ' + err.code);
    }
    if(flashModeStatus) {
      // Set the flash mode to auto.
      try {
        photoSession.setFlashMode(camera.FlashMode.FLASH_MODE_AUTO);
      } catch (error) {
        let err = error as BusinessError;
        console.error('Failed to set the flash mode. errorCode = ' + err.code);
      }
    }
  }

  // Check whether the continuous auto focus is supported.
  let focusModeStatus: boolean = false;
  try {
    let status: boolean = photoSession.isFocusModeSupported(camera.FocusMode.FOCUS_MODE_CONTINUOUS_AUTO);
    focusModeStatus = status;
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to check whether the focus mode is supported. errorCode = ' + err.code);
  }

  if (focusModeStatus) {
    // Set the focus mode to continuous auto focus.
    try {
      photoSession.setFocusMode(camera.FocusMode.FOCUS_MODE_CONTINUOUS_AUTO);
    } catch (error) {
      let err = error as BusinessError;
      console.error('Failed to set the focus mode. errorCode = ' + err.code);
    }
  }

  // Obtain the zoom ratio range supported by the camera.
  let zoomRatioRange: Array<number> = [];
  try {
    zoomRatioRange = photoSession.getZoomRatioRange();
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to get the zoom ratio range. errorCode = ' + err.code);
  }
  if (zoomRatioRange.length <= 0) {
    return;
  }
  // Set a zoom ratio.
  try {
    photoSession.setZoomRatio(zoomRatioRange[0]);
  } catch (error) {
    let err = error as BusinessError;
    console.error('Failed to set the zoom ratio value. errorCode = ' + err.code);
  }
  let photoCaptureSetting: camera.PhotoCaptureSetting = {
    quality: camera.QualityLevel.QUALITY_LEVEL_HIGH, // Set the photo quality to high.
    rotation: camera.ImageRotation.ROTATION_0 // Set the rotation angle of the photo to 0.
  }
  // Use the current photographing settings to take photos.
  photoOutput.capture(photoCaptureSetting, (err: BusinessError) => {
    if (err) {
      console.error(`Failed to capture the photo ${err.message}`);
      return;
    }
    console.info('Callback invoked to indicate the photo capture request success.');
  });
  // Stop the session.
  photoSession.stop();

  // Release the camera input stream.
  cameraInput.close();

  // Release the preview output stream.
  previewOutput.release();

  // Release the photo output stream.
  photoOutput.release();

  // Release the session.
  photoSession.release();

  // Set the session to null.
  photoSession = undefined;
}
```

   