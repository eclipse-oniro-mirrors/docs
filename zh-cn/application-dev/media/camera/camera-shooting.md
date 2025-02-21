# 拍照(ArkTS)

拍照是相机的最重要功能之一，拍照模块基于相机复杂的逻辑，为了保证用户拍出的照片质量，在中间步骤可以设置分辨率、闪光灯、焦距、照片质量及旋转角度等信息。

## 开发步骤

详细的API说明请参考[Camera API参考](../../reference/apis-camera-kit/js-apis-camera.md)。

1. 导入image接口。创建拍照输出流的SurfaceId以及拍照输出的数据，都需要用到系统提供的image接口能力，导入image接口的方法如下。

   ```ts
   import image from '@ohos.multimedia.image';
   import camera from '@ohos.multimedia.camera';
   import fs from '@ohos.file.fs';
   import photoAccessHelper from '@ohos.file.photoAccessHelper';
   import { BusinessError } from '@ohos.base';
   ```

2. 创建拍照输出流。

   通过[CameraOutputCapability](../../reference/apis-camera-kit/js-apis-camera.md#cameraoutputcapability)类中的photoProfiles属性，可获取当前设备支持的拍照输出流，通过[createPhotoOutput](../../reference/apis-camera-kit/js-apis-camera.md#createphotooutput11)方法传入支持的某一个输出流及步骤一获取的SurfaceId创建拍照输出流。

   ```ts
   function getPhotoOutput(cameraManager: camera.CameraManager, cameraOutputCapability: camera.CameraOutputCapability): camera.PhotoOutput | undefined {
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

3. 设置拍照photoAvailable的回调，并将拍照的buffer保存为图片。

    Context获取方式请参考：[获取UIAbility的上下文信息](../../application-models/uiability-usage.md#获取uiability的上下文信息)。

   ```ts
   let context = getContext(this);

   async function savePicture(buffer: ArrayBuffer, img: image.Image) {
     let accessHelper: photoAccessHelper.PhotoAccessHelper = photoAccessHelper.getPhotoAccessHelper(context);
     let options: photoAccessHelper.CreateOptions = {
       title: Date.now().toString()
     };
     let photoUri: string = await accessHelper.createAsset(photoAccessHelper.PhotoType.IMAGE, 'jpg', options);
     //createAsset的调用需要ohos.permission.READ_IMAGEVIDEO和ohos.permission.WRITE_IMAGEVIDEO的权限
     let file: fs.File = fs.openSync(photoUri, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
     await fs.write(file.fd, buffer);
     fs.closeSync(file);
     img.release(); 
   }

   function setPhotoOutputCb(photoOutput: camera.PhotoOutput) {
   //设置回调之后，调用photoOutput的capture方法，就会将拍照的buffer回传到回调中
     photoOutput.on('photoAvailable', (errCode: BusinessError, photo: camera.Photo): void => {
        console.info('getPhoto start');
        console.info(`err: ${JSON.stringify(errCode)}`);
        if (errCode || photo === undefined) {
          console.error('getPhoto failed');
          return;
        }
        let imageObj: image.Image = photo.main;
        imageObj.getComponent(image.ComponentType.JPEG, (errCode: BusinessError, component: image.Component): void => {
          console.info('getComponent start');
          if (errCode || component === undefined) {
            console.error('getComponent failed');
            return;
          }
          let buffer: ArrayBuffer;
          if (component.byteBuffer) {
            buffer = component.byteBuffer;
          } else {
            console.error('byteBuffer is null');
            return;
          }
          savePicture(buffer, imageObj);
        });
      });
   }
   ```

4. 参数配置。

   配置相机的参数可以调整拍照的一些功能，包括闪光灯、变焦、焦距等。

   ```ts
   function configuringSession(photoSession: camera.PhotoSession): void {
     // 判断设备是否支持闪光灯
     let flashStatus: boolean = false;
     try {
       flashStatus = photoSession.hasFlash();
     } catch (error) {
       let err = error as BusinessError;
       console.error(`Failed to hasFlash. error: ${JSON.stringify(err)}`);
     }
     console.info(`Returned with the flash light support status: ${flashStatus}`);
     if (flashStatus) {
       // 判断是否支持自动闪光灯模式
       let flashModeStatus: boolean = false;
       try {
         let status: boolean = photoSession.isFlashModeSupported(camera.FlashMode.FLASH_MODE_AUTO);
         flashModeStatus = status;
       } catch (error) {
         let err = error as BusinessError;
         console.error(`Failed to check whether the flash mode is supported. error: ${JSON.stringify(err)}`);
       }
       if (flashModeStatus) {
         // 设置自动闪光灯模式
         try {
           photoSession.setFlashMode(camera.FlashMode.FLASH_MODE_AUTO);
         } catch (error) {
           let err = error as BusinessError;
           console.error(`Failed to set the flash mode. error: ${JSON.stringify(err)}`);
         }
       }
     }
     // 判断是否支持连续自动变焦模式
     let focusModeStatus: boolean = false;
     try {
       let status: boolean = photoSession.isFocusModeSupported(camera.FocusMode.FOCUS_MODE_CONTINUOUS_AUTO);
       focusModeStatus = status;
     } catch (error) {
       let err = error as BusinessError;
       console.error(`Failed to check whether the focus mode is supported. error: ${JSON.stringify(err)}`);
     }
     if (focusModeStatus) {
       // 设置连续自动变焦模式
       try {
         photoSession.setFocusMode(camera.FocusMode.FOCUS_MODE_CONTINUOUS_AUTO);
       } catch (error) {
         let err = error as BusinessError;
         console.error(`Failed to set the focus mode. error: ${JSON.stringify(err)}`);
       }
     }
     // 获取相机支持的可变焦距比范围
     let zoomRatioRange: Array<number> = [];
     try {
       zoomRatioRange = photoSession.getZoomRatioRange();
     } catch (error) {
       let err = error as BusinessError;
       console.error(`Failed to get the zoom ratio range. error: ${JSON.stringify(err)}`);
     }
     if (zoomRatioRange.length <= 0 ) {
       return;
     }
     // 设置可变焦距比
     try {
       photoSession.setZoomRatio(zoomRatioRange[0]);
     } catch (error) {
       let err = error as BusinessError;
       console.error(`Failed to set the zoom ratio value. error: ${JSON.stringify(err)}`);
     }
   }
   ```

5. 触发拍照。

   通过photoOutput类的[capture](../../reference/apis-camera-kit/js-apis-camera.md#capture-2)方法，执行拍照任务。该方法有两个参数，第一个参数为拍照设置参数的setting，setting中可以设置照片的质量和旋转角度，第二参数为回调函数。

   ```ts
   function capture(captureLocation: camera.Location, photoOutput: camera.PhotoOutput): void {
     let settings: camera.PhotoCaptureSetting = {
       quality: camera.QualityLevel.QUALITY_LEVEL_HIGH,  // 设置图片质量高
       rotation: camera.ImageRotation.ROTATION_0,  // 设置图片旋转角度0
       location: captureLocation,  // 设置图片地理位置
       mirror: false  // 设置镜像使能开关(默认关)
     };
     photoOutput.capture(settings, (err: BusinessError) => {
       if (err) {
         console.error(`Failed to capture the photo. error: ${JSON.stringify(err)}`);
         return;
       }
       console.info('Callback invoked to indicate the photo capture request success.');
     });
   }
   ```

## 状态监听

在相机应用开发过程中，可以随时监听拍照输出流状态，包括拍照流开始、拍照帧的开始与结束、拍照输出流的错误。

- 通过注册固定的captureStart回调函数获取监听拍照开始结果，photoOutput创建成功时即可监听，拍照第一次曝光时触发，该事件返回此次拍照的captureId。

  ```ts
  function onPhotoOutputCaptureStart(photoOutput: camera.PhotoOutput): void {
    photoOutput.on('captureStartWithInfo', (err: BusinessError, captureStartInfo: camera.CaptureStartInfo) => {
      console.info(`photo capture started, captureId : ${captureStartInfo.captureId}`);
    });
  }
  ```

- 通过注册固定的captureEnd回调函数获取监听拍照结束结果，photoOutput创建成功时即可监听，该事件返回结果为拍照完全结束后的相关信息[CaptureEndInfo](../../reference/apis-camera-kit/js-apis-camera.md#captureendinfo)。

  ```ts
  function onPhotoOutputCaptureEnd(photoOutput: camera.PhotoOutput): void {
    photoOutput.on('captureEnd', (err: BusinessError, captureEndInfo: camera.CaptureEndInfo) => {
      console.info(`photo capture end, captureId : ${captureEndInfo.captureId}`);
      console.info(`frameCount : ${captureEndInfo.frameCount}`);
    });
  }
  ```

- 通过注册固定的error回调函数获取监听拍照输出流的错误结果。callback返回拍照输出接口使用错误时的对应错误码，错误码类型参见[CameraErrorCode](../../reference/apis-camera-kit/js-apis-camera.md#cameraerrorcode)。

  ```ts
  function onPhotoOutputError(photoOutput: camera.PhotoOutput): void {
    photoOutput.on('error', (error: BusinessError) => {
      console.error(`Photo output error code: ${error.code}`);
    });
  }
  ```
