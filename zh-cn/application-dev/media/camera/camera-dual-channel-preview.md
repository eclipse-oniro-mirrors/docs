# 双路预览(ArkTS)

相机应用通过控制相机，实现图像显示（预览）、照片保存（拍照）、视频录制（录像）等基础操作。相机开发模型为Surface模型，即应用通过Surface进行数据传递，通过ImageReceiver的surface获取拍照流的数据、通过XComponent的surface获取预览流的数据。

如果要实现双路预览，即将拍照流改为预览流，将拍照流中的surface改为预览流的surface，通过ImageReceiver的surface创建previewOutput，其余流程与拍照流和预览流一致。

详细的API说明请参考[Camera API参考](../../reference/apis-camera-kit/js-apis-camera.md)。

## 约束与限制

- 暂不支持动态添加流，即不能在没有调用[session.stop](../../reference/apis-camera-kit/js-apis-camera.md#stop11)的情况下，调用[addOutput](../../reference/apis-camera-kit/js-apis-camera.md#addoutput11)添加流。
- 对ImageReceiver组件获取到的图像数据处理后，需要将对应的图像Buffer释放，确保Surface的BufferQueue正常轮转。

## 调用流程

双路方案调用流程图建议如下：

![dual-preview-streams-instructions](figures/dual-preview-streams-instructions.png)

## 开发步骤

1. 导入image接口。

   创建双路预览流的SurfaceId，除XComponent组件的SurfaceId外，还需要使用ImageReceiver组件创建生成的SurfaceId，需要使用image模块提供的接口。

   ```ts
   import image from '@ohos.multimedia.image';
   ```
2. 创建ImageReceiver对象。
   ```ts
   let size: image.Size = {
       width: 640,
       height: 480
     }
   let receiver: image.ImageReceiver = image.createImageReceiver(size, image.ImageFormat.JPEG, 8);
   ```
3. 获取ImageReceiver组件的SurfaceId。

   ```ts
   async function getImageReceiverSurfaceId(receiver: image.ImageReceiver): Promise<string | undefined> {
     let ImageReceiverSurfaceId: string | undefined = undefined;
     if (receiver !== undefined) {
       console.info('receiver is not undefined');
       let ImageReceiverSurfaceId: string = await receiver.getReceivingSurfaceId();
       console.info(`ImageReceived id: ${ImageReceiverSurfaceId}`);
     } else {
       console.error('createImageReceiver failed');
     }
     return ImageReceiverSurfaceId;
   }
   ```

4. 创建XComponent组件Surface。

   可参考[相机预览指导文档](camera-preview.md)。

   ```ets
   //xxx.ets
   // 创建XComponentController
   @Component
   struct XComponentPage {
     // 创建XComponentController
     mXComponentController: XComponentController = new XComponentController;

     build() {
       Flex() {
         // 创建XComponent
         XComponent({
           id: '',
           type: 'surface',
           libraryname: '',
           controller: this.mXComponentController
         })
           .onLoad(() => {
             // 设置Surface宽高（1920*1080），预览尺寸设置参考前面 previewProfilesArray 获取的当前设备所支持的预览分辨率大小去设置
             this.mXComponentController.setXComponentSurfaceSize({surfaceWidth:1920,surfaceHeight:1080});
             // 获取Surface ID
             let surfaceId: string = this.mXComponentController.getXComponentSurfaceId();
           })
           .width('1920px')
           .height('1080px')
       }
     }
   }
   ```

5. 实现双路预览。

   将步骤2、3生成的两路SurfaceId通过[createPreviewOutput](../../reference/apis-camera-kit/js-apis-camera.md#createpreviewoutput)方法传递到相机服务，创建两路预览流，其余流程按照正常预览流程开发。

   ```ts
   import camera from '@ohos.multimedia.camera';

   async function createDualChannelPreview(cameraManager: camera.CameraManager, XComponentSurfaceId: string, receiver: image.ImageReceiver): Promise<void> {
     // 获取支持的相机设备对象
     let camerasDevices: Array<camera.CameraDevice> = cameraManager.getSupportedCameras();

     // 获取支持的模式类型
     let sceneModes: Array<camera.SceneMode> = cameraManager.getSupportedSceneModes(camerasDevices[0]);
     let isSupportPhotoMode: boolean = sceneModes.indexOf(camera.SceneMode.NORMAL_PHOTO) >= 0;
     if (!isSupportPhotoMode) {
       console.error('photo mode not support');
       return;
     }

     // 获取profile对象
     let profiles: camera.CameraOutputCapability = cameraManager.getSupportedOutputCapability(camerasDevices[0], camera.SceneMode.NORMAL_PHOTO); // 获取对应相机设备profiles
     let previewProfiles: Array<camera.Profile> = profiles.previewProfiles;

     // 预览流1
     let previewProfilesObj: camera.Profile = previewProfiles[0];

     // 预览流2
     let previewProfilesObj2: camera.Profile = previewProfiles[0];

     // 创建 预览流1 输出对象
     let previewOutput: camera.PreviewOutput = cameraManager.createPreviewOutput(previewProfilesObj, XComponentSurfaceId);

     // 创建 预览流2 输出对象
     let imageReceiverSurfaceId: string = await receiver.getReceivingSurfaceId();
     let previewOutput2: camera.PreviewOutput = cameraManager.createPreviewOutput(previewProfilesObj2, imageReceiverSurfaceId);

     // 创建cameraInput对象
     let cameraInput: camera.CameraInput = cameraManager.createCameraInput(camerasDevices[0]);

     // 打开相机
     await cameraInput.open();

     // 会话流程
     let photoSession: camera.PhotoSession = cameraManager.createSession(camera.SceneMode.NORMAL_PHOTO) as camera.PhotoSession;

     // 开始配置会话
     photoSession.beginConfig();

     // 把CameraInput加入到会话
     photoSession.addInput(cameraInput);

     // 把 预览流1 加入到会话
     photoSession.addOutput(previewOutput);

     // 把 预览流2 加入到会话
     photoSession.addOutput(previewOutput2);

     // 提交配置信息
     await photoSession.commitConfig();

     // 会话开始
     await photoSession.start();
   }
   ```

6. 通过ImageReceiver实时获取预览图像。

   通过ImageReceiver组件中imageArrival事件监听获取底层返回的图像数据，详细的API说明请参考[Image API参考](../../reference/apis-image-kit/js-apis-image.md)。

   ```ts
   import { BusinessError } from '@ohos.base';

   function onImageArrival(receiver: image.ImageReceiver): void {
     receiver.on('imageArrival', () => {
       receiver.readNextImage((err: BusinessError, nextImage: image.Image) => {
         if (err || nextImage === undefined) {
           console.error('readNextImage failed');
           return;
         }
         nextImage.getComponent(image.ComponentType.JPEG, (err: BusinessError, imgComponent: image.Component) => {
           if (err || imgComponent === undefined) {
             console.error('getComponent failed');
           }
           if (imgComponent && imgComponent.byteBuffer as ArrayBuffer) {
             // do something...
           } else {
             console.error('byteBuffer is null');
           }
           nextImage.release();
         })
       })
     })
   }
   ```
