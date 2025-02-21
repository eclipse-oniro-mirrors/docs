# @ohos.multimedia.camera (相机管理)

本模块为开发者提供一套简单且易于理解的相机服务接口，开发者通过调用接口可以开发相机应用。应用通过访问和操作相机硬件，实现基础操作，如预览、拍照和录像；还可以通过接口组合完成更多操作，如控制闪光灯和曝光时间、对焦或调焦等。

> **说明：**
>
> 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import camera from '@ohos.multimedia.camera';
```

## camera.getCameraManager

getCameraManager(context: Context): CameraManager

获取相机管理器实例，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                                             | 必填 | 说明                           |
| -------- | ----------------------------------------------- | ---- | ---------------------------- |
| context  | [Context](../apis-ability-kit/js-apis-inner-application-baseContext.md)      | 是   | 应用上下文。                   |

**返回值：**

| 类型                                             | 说明                           |
| ----------------------------------------------- | ---------------------------- |
| [CameraManager](#cameramanager)           | 相机管理器。                   |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400101                |  Parameter missing or parameter type incorrect.               |
| 7400201                |  Camera service fatal error.                                  |

**示例：**

```ts
import common from '@ohos.app.ability.common';
import { BusinessError } from '@ohos.base';

function getCameraManager(context: common.BaseContext): camera.CameraManager | undefined {
  let cameraManager: camera.CameraManager | undefined = undefined;
  try {
    cameraManager = camera.getCameraManager(context);
  } catch (error) {
    let err = error as BusinessError;
    console.error(`The getCameraManager call failed. error code: ${err.code}`);
  }
  return cameraManager;
}
```

## CameraDevice

相机设备信息。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称           | 类型                               | 只读 | 必填 | 说明        |
| -------------- | --------------------------------- | ---- | ---- |---------- |
| cameraId       | string                            | 是   | 是   | 相机id。|
| cameraPosition | [CameraPosition](#cameraposition) | 是   | 是   | 相机位置。    |
| cameraType     | [CameraType](#cameratype)         | 是   | 是   | 相机类型。    |
| connectionType | [ConnectionType](#connectiontype) | 是   | 是   | 相机连接类型。 |

## CameraPosition

枚举，相机位置。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称                         | 值   | 说明            |
| --------------------------- | ---- | -------------- |
| CAMERA_POSITION_UNSPECIFIED | 0    | 相机位置未指定。  |
| CAMERA_POSITION_BACK        | 1    | 后置相机。       |
| CAMERA_POSITION_FRONT       | 2    | 前置相机。       |
| CAMERA_POSITION_FOLD_INNER<sup>11+</sup>  | 3    | 折叠态相机。     |

## CameraType

枚举，相机类型。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称                     | 值   | 说明            |
| ----------------------- | ---- | -------------- |
| CAMERA_TYPE_DEFAULT     | 0    | 相机类型未指定。  |
| CAMERA_TYPE_WIDE_ANGLE  | 1    | 广角相机。       |
| CAMERA_TYPE_ULTRA_WIDE  | 2    | 超广角相机。     |
| CAMERA_TYPE_TELEPHOTO   | 3    | 长焦相机。       |
| CAMERA_TYPE_TRUE_DEPTH  | 4    | 带景深信息的相机。 |

## ConnectionType

枚举，相机连接类型。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称                          | 值   | 说明           |
| ---------------------------- | ---- | ------------- |
| CAMERA_CONNECTION_BUILT_IN   | 0    | 内置相机。      |
| CAMERA_CONNECTION_USB_PLUGIN | 1    | USB连接的相机。 |
| CAMERA_CONNECTION_REMOTE     | 2    | 远程连接的相机。 |

## CameraStatus

枚举，相机状态。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称                       | 值   | 说明            |
| ------------------------- | ---- | ------------    |
| CAMERA_STATUS_APPEAR      | 0    | 新的相机出现。   |
| CAMERA_STATUS_DISAPPEAR   | 1    | 相机被移除。     |
| CAMERA_STATUS_AVAILABLE   | 2    | 相机可用。       |
| CAMERA_STATUS_UNAVAILABLE | 3    | 相机不可用。     |

## CameraStatusInfo

相机管理器回调返回的接口实例，表示相机状态信息。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称   | 类型                           |    只读   |     必填     | 说明       |
| ------ | ----------------------------- | --------- |------------ | ---------- |
| camera | [CameraDevice](#cameradevice) |     否    |       是     | 相机信息。 |
| status | [CameraStatus](#camerastatus) |     否    |       是     | 相机状态。 |

## Profile

相机配置信息项。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称      | 类型                          | 只读 | 必填 | 说明         |
| -------- | ----------------------------- |---- | ---- | ------------- |
| format   | [CameraFormat](#cameraformat) | 是  |  是  | 输出格式。      |
| size     | [Size](#size)                 | 是  |  是  | 分辨率。       |

## FrameRateRange

帧率范围。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称      | 类型                          | 只读 | 必填 | 说明            |
| -------- | ----------------------------- |----- | ---- | -------------- |
| min      | number                        |  是  |  N/A  | 最小帧率。      |
| max      | number                        |  是  |  N/A  | 最大帧率。      |

## VideoProfile

视频配置信息项，继承[Profile](#profile)。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称                       | 类型                                      | 只读 | 必填 | 说明        |
| ------------------------- | ----------------------------------------- | --- | ---- |----------- |
| frameRateRange            | [FrameRateRange](#frameraterange)         | 是  |  是  | 帧率范围，fps(frames per second)。 |

## CameraOutputCapability

相机输出能力项。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称                           | 类型                                                | 只读 | 必填 | 说明                |
| ----------------------------- | --------------------------------------------------- | ---- | ---- | ------------------- |
| previewProfiles               | Array\<[Profile](#profile)\>                        |  是  | N/A | 支持的预览配置信息。    |
| photoProfiles                 | Array\<[Profile](#profile)\>                        |  是  | N/A | 支持的拍照配置信息。    |
| videoProfiles                 | Array\<[VideoProfile](#videoprofile)\>              |  是  | N/A | 支持的录像配置信息。    |
| supportedMetadataObjectTypes  | Array\<[MetadataObjectType](#metadataobjecttype)\>  |  是  | N/A | 支持的metadata流类型信息。|

## SceneMode<sup>11+</sup>

枚举，相机支持模式。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称                     | 值        | 说明         |
| ----------------------- | --------- | ------------ |
| NORMAL_PHOTO  | 1         | 普通拍照模式。             |
| NORMAL_VIDEO | 2      | 普通录像模式。      |

## CameraErrorCode

相机错误码。

接口使用不正确以及on接口监听error状态返回。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称                       | 值          | 说明            |
| -------------------------  | ----       | ------------    |
| INVALID_ARGUMENT           | 7400101    | 参数缺失或者参数类型不对。   |
| OPERATION_NOT_ALLOWED      | 7400102    | 操作流程不对，不允许。     |
| SESSION_NOT_CONFIG         | 7400103    | session 未配置返回。       |
| SESSION_NOT_RUNNING        | 7400104    | session 未运行返回。    |
| SESSION_CONFIG_LOCKED      | 7400105    | session 配置已锁定返回。     |
| DEVICE_SETTING_LOCKED      | 7400106    | 设备设置已锁定返回。     |
| CONFLICT_CAMERA            | 7400107    | 设备重复打开返回。     |
| DEVICE_DISABLED            | 7400108    | 安全原因摄像头被禁用。     |
| DEVICE_PREEMPTED           | 7400109    | 相机被抢占导致无法使用。     |
| SERVICE_FATAL_ERROR        | 7400201    | 相机服务错误返回。     |

## CameraManager

相机管理器类，使用前需要通过[getCameraManager](#cameragetcameramanager)获取相机管理实例。

### getSupportedCameras

getSupportedCameras(): Array\<CameraDevice\>

获取支持指定的相机设备对象，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型                                             | 说明                           |
| ----------------------------------------------- | ---------------------------- |
|  Array\<[CameraDevice](#cameradevice)>            | 相机设备列表。                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getSupportedCameras(cameraManager: camera.CameraManager): Array<camera.CameraDevice> {
  let cameras: Array<camera.CameraDevice> = [];
  try {
    cameras = cameraManager.getSupportedCameras();
  } catch (error) {
    let err = error as BusinessError;
    console.error(`The getSupportedCameras call failed. error code: ${err.code}`);
  }
  return cameras;
}
```

### getSupportedSceneModes<sup>11+</sup>

getSupportedSceneModes(camera: CameraDevice): Array\<SceneMode\>

获取指定的相机设备对象支持的模式，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名         | 类型                                                            | 必填 | 说明                      |
| ------------ |--------------------------------------------------------------- | -- | -------------------------- |
| camera | [CameraDevice](#cameradevice)                              | 是 | 相机设备，通过 [getSupportedCameras](#getsupportedcameras) 接口获取。       |

**返回值：**

| 类型                                             | 说明                           |
| ----------------------------------------------- | ---------------------------- |
|  Array\<[SceneMode](#scenemode11)>            | 相机支持的模式列表。                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getSupportedSceneModes(cameraManager: camera.CameraManager, camera: camera.CameraDevice): Array<camera.SceneMode> {
  let modes: Array<camera.SceneMode> = [];
  try {
    modes = cameraManager.getSupportedSceneModes(camera);
  } catch (error) {
    let err = error as BusinessError;
    console.error(`The getSupportedSceneModes call failed. error code: ${err.code}`);
  }
  return modes;
}
```

### getSupportedOutputCapability<sup>(deprecated)</sup>

getSupportedOutputCapability(camera: CameraDevice): CameraOutputCapability

查询相机设备支持的输出能力，同步返回结果。

> **说明：**
> 从 API version 10开始支持，从API version 11开始废弃。建议使用[getSupportedOutputCapability](#getsupportedoutputcapability11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名         | 类型                                                            | 必填 | 说明                      |
| ------------ |--------------------------------------------------------------- | -- | -------------------------- |
| camera | [CameraDevice](#cameradevice)                              | 是 | 相机设备，通过 [getSupportedCameras](#getsupportedcameras) 接口获取。       |

**返回值：**

| 类型                                             | 说明                           |
| ----------------------------------------------- | ---------------------------- |
| [CameraOutputCapability](#cameraoutputcapability)            | 相机输出能力。                   |

**示例：**

```ts
function getSupportedOutputCapability(camera: camera.CameraDevice, cameraManager: camera.CameraManager): camera.CameraOutputCapability {
  let cameraOutputCapability: camera.CameraOutputCapability = cameraManager.getSupportedOutputCapability(camera);
  return cameraOutputCapability;
}
```

### getSupportedOutputCapability<sup>11+</sup>

getSupportedOutputCapability(camera: CameraDevice, mode: SceneMode): CameraOutputCapability

查询相机设备在模式下支持的输出能力，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名         | 类型                                                            | 必填 | 说明                      |
| ------------ |--------------------------------------------------------------- | -- | -------------------------- |
| camera | [CameraDevice](#cameradevice)                              | 是 | 相机设备，通过 [getSupportedCameras](#getsupportedcameras) 接口获取。       |
| mode | [SceneMode](#scenemode11)                              | 是 | 相机模式，通过 [getSupportedSceneModes](#getsupportedscenemodes11) 接口获取。       |

**返回值：**

| 类型                                             | 说明                           |
| ----------------------------------------------- | ---------------------------- |
| [CameraOutputCapability](#cameraoutputcapability)            | 相机输出能力。                   |

**示例：**

```ts
function getSupportedOutputCapability(camera: camera.CameraDevice, cameraManager: camera.CameraManager, sceneMode: camera.SceneMode): camera.CameraOutputCapability {
  let cameraOutputCapability: camera.CameraOutputCapability = cameraManager.getSupportedOutputCapability(camera, sceneMode);
  return cameraOutputCapability;
}
```

### isCameraMuted

isCameraMuted(): boolean

查询相机当前的禁用状态（禁用/未禁用）。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                                         |
| ---------- | -------------------------------------------- |
| boolean    | 返回true表示相机被禁用，返回false表示相机未被禁用。 |

**示例：**

```ts
function isCameraMuted(cameraManager: camera.CameraManager): boolean {
  let isMuted: boolean = cameraManager.isCameraMuted();
  return isMuted;
}
```

### createCameraInput

createCameraInput(camera: CameraDevice): CameraInput

使用CameraDevice对象创建CameraInput实例，同步返回结果。

**需要权限：** ohos.permission.CAMERA

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                                         | 必填 | 说明                                               |
| -------- | ------------------------------------------- | ---- |--------------------------------------------------|
| camera  | [CameraDevice](#cameradevice)         | 是   | CameraDevice对象，通过 [getSupportedCameras](#getsupportedcameras) 接口获取。 |

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [CameraInput](#camerainput)    | CameraInput实例。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400101                |  Parameter missing or parameter type incorrect.               |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function createCameraInput(camera: camera.CameraDevice, cameraManager: camera.CameraManager): camera.CameraInput | undefined {
  let cameraInput: camera.CameraInput | undefined = undefined;
  try {
    cameraInput = cameraManager.createCameraInput(camera);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The createCameraInput call failed. error code: ${err.code}`);
  }
  return cameraInput;
}
```

### createCameraInput

createCameraInput(position: CameraPosition, type: CameraType): CameraInput

根据相机位置和类型创建CameraInput实例，同步返回结果。

**需要权限：** ohos.permission.CAMERA

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                                        | 必填 | 说明                                |
| -------- | ------------------------------------------- | ---- | --------------------------------- |
| position | [CameraPosition](#cameraposition)           | 是   | 相机位置，通过 [getSupportedCameras](#getsupportedcameras) 接口获取设备，然后获取设备位置信息。  |
| type     | [CameraType](#cameratype)                   | 是   | 相机类型，通过 [getSupportedCameras](#getsupportedcameras) 接口获取设备，然后获取设备类型信息。 |

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [CameraInput](#camerainput)    | CameraInput实例。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400101                |  Parameter missing or parameter type incorrect.               |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function createCameraInput(camera: camera.CameraDevice, cameraManager: camera.CameraManager): camera.CameraInput | undefined {
  let position: camera.CameraPosition = camera.cameraPosition;
  let type: camera.CameraType = camera.cameraType;
  let cameraInput: camera.CameraInput | undefined = undefined;
  try {
    cameraInput = cameraManager.createCameraInput(position, type);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The createCameraInput call failed. error code: ${err.code}`);
  }
  return cameraInput;
}
```

### createPreviewOutput

createPreviewOutput(profile: Profile, surfaceId: string): PreviewOutput

创建预览输出对象，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                                             | 必填 | 说明                              |
| -------- | ----------------------------------------------- | ---- | ------------------------------- |
| profile  | [Profile](#profile)                             | 是   | 支持的预览配置信息，通过[getSupportedOutputCapability](#getsupportedoutputcapability11)接口获取。|
| surfaceId| string | 是   | 从[XComponent](../apis-arkui/arkui-ts/ts-basic-components-xcomponent.md)或者[ImageReceiver](../apis-image-kit/js-apis-image.md#imagereceiver9)组件获取的surfaceId。|

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [PreviewOutput](#previewoutput)    | PreviewOutput实例。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400101                |  Parameter missing or parameter type incorrect.               |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function createPreviewOutput(cameraOutputCapability: camera.CameraOutputCapability, cameraManager: camera.CameraManager, surfaceId: string): camera.PreviewOutput | undefined {
  let profile: camera.Profile = cameraOutputCapability.previewProfiles[0];
  let previewOutput: camera.PreviewOutput | undefined = undefined;
  try {
    previewOutput = cameraManager.createPreviewOutput(profile, surfaceId);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The createPreviewOutput call failed. error code: ${err.code}`);
  }
  return previewOutput;
}
```

### createPhotoOutput<sup>(deprecated)</sup>

createPhotoOutput(profile: Profile, surfaceId: string): PhotoOutput

创建拍照输出对象，同步返回结果。

> **说明：**
> 从 API version 10开始支持，从API version 11开始废弃。建议使用[createPhotoOutput](#createphotooutput11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                                         | 必填 | 说明                                  |
| -------- | ------------------------------------------- | ---- | ----------------------------------- |
| profile  | [Profile](#profile)                         | 是   | 支持的拍照配置信息，通过[getSupportedOutputCapability](#getsupportedoutputcapability11)接口获取。|
| surfaceId| string            | 是   | 从[ImageReceiver](../apis-image-kit/js-apis-image.md#imagereceiver9)获取的surfaceId。|

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [PhotoOutput](#photooutput)   | PhotoOutput实例。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400101                |  Parameter missing or parameter type incorrect.               |

```ts
import { BusinessError } from '@ohos.base';

function createPhotoOutput(cameraOutputCapability: camera.CameraOutputCapability, cameraManager: camera.CameraManager, surfaceId: string): camera.PhotoOutput | undefined {
  let profile: camera.Profile = cameraOutputCapability.photoProfiles[0];
  let photoOutput: camera.PhotoOutput | undefined = undefined;
  try {
    photoOutput = cameraManager.createPhotoOutput(profile, surfaceId);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The createPhotoOutput call failed. error code: ${err.code}`);
  }
  return photoOutput;
}
```

### createPhotoOutput<sup>11+</sup>

createPhotoOutput(profile: Profile): PhotoOutput

创建拍照输出对象，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                                         | 必填 | 说明                                  |
| -------- | ------------------------------------------- | ---- | ----------------------------------- |
| profile  | [Profile](#profile)                         | 是   | 支持的拍照配置信息，通过[getSupportedOutputCapability](#getsupportedoutputcapability11)接口获取。|

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [PhotoOutput](#photooutput)   | PhotoOutput实例。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400101                |  Parameter missing or parameter type incorrect.               |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function createPhotoOutput(cameraOutputCapability: camera.CameraOutputCapability, cameraManager: camera.CameraManager): camera.PhotoOutput | undefined {
  let profile: camera.Profile = cameraOutputCapability.photoProfiles[0];
  let photoOutput: camera.PhotoOutput | undefined = undefined;
  try {
    photoOutput = cameraManager.createPhotoOutput(profile);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The createPhotoOutput call failed. error code: ${err.code}`);
  }
  return photoOutput;
}
```

### createVideoOutput

createVideoOutput(profile: VideoProfile, surfaceId: string): VideoOutput

创建录像输出对象，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                                        | 必填 | 说明                              |
| -------- | ------------------------------------------- | ---- | ------------------------------ |
| profile  | [VideoProfile](#videoprofile)               | 是   | 支持的录像配置信息，通过[getSupportedOutputCapability](#getsupportedoutputcapability11)接口获取。 |
| surfaceId| string          | 是   | 从[AVRecorder](../apis-media-kit/js-apis-media.md#avrecorder9)获取的surfaceId。|

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [VideoOutput](#videooutput)   | VideoOutput实例。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400101                |  Parameter missing or parameter type incorrect.               |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function createVideoOutput(cameraOutputCapability: camera.CameraOutputCapability, cameraManager: camera.CameraManager, surfaceId: string): camera.VideoOutput | undefined {
  let profile: camera.VideoProfile = cameraOutputCapability.videoProfiles[0];
  let videoOutput: camera.VideoOutput | undefined = undefined;
  try {
    videoOutput = cameraManager.createVideoOutput(profile, surfaceId);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The createVideoOutput call failed. error code: ${err.code}`);
  }
  return videoOutput;
}
```

### createMetadataOutput

createMetadataOutput(metadataObjectTypes: Array\<MetadataObjectType\>): MetadataOutput

创建metadata流输出对象，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名                  | 类型                                               | 必填 | 说明                          |
| -------------------- | -------------------------------------------------- | --- | ---------------------------- |
| metadataObjectTypes  | Array\<[MetadataObjectType](#metadataobjecttype)\>  | 是  | metadata流类型信息，通过[getSupportedOutputCapability](#getsupportedoutputcapability11)接口获取。 |

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [MetadataOutput](#metadataoutput)   | MetadataOutput实例。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400101                |  Parameter missing or parameter type incorrect.               |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function createMetadataOutput(cameraManager: camera.CameraManager, cameraOutputCapability: camera.CameraOutputCapability): void {
  let metadataObjectTypes: Array<camera.MetadataObjectType> = cameraOutputCapability.supportedMetadataObjectTypes;
  let metadataOutput: camera.MetadataOutput | undefined = undefined;
  try {
    metadataOutput = cameraManager.createMetadataOutput(metadataObjectTypes);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`createMetadataOutput error. error code: ${err.code}`);
  }
}
```

### createCaptureSession<sup>(deprecated)</sup>

createCaptureSession(): CaptureSession

创建CaptureSession实例，同步返回结果。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[createSession](#createsession11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [CaptureSession](#capturesessiondeprecated)   | CaptureSession实例。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400201                |  Camera service fatal error.               |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function createCaptureSession(cameraManager: camera.CameraManager): camera.CaptureSession | undefined {
  let captureSession: camera.CaptureSession | undefined = undefined;
  try {
    captureSession = cameraManager.createCaptureSession();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`createCaptureSession error. error code: ${err.code}`);
  }
  return captureSession;
}
```

### createSession<sup>11+</sup>

createSession\<T extends Session\>(mode: SceneMode): T

创建指定SceneMode的Session实例，同步返回结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名   | 类型              | 必填 | 说明       |
| -------- | -----------------| ---- | --------- |
| mode     | SceneMode        | 是   | 相机支持的模式。 |

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [T extends Session](#session11)   | Session实例。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400201                |  Camera service fatal error.               |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function createSession(cameraManager: camera.CameraManager, mode: camera.SceneMode): camera.Session | undefined {
  let photoSession: camera.PhotoSession | undefined = undefined;
  try {
    photoSession = cameraManager.createSession(mode) as camera.PhotoSession;
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`createCaptureSession error. error code: ${err.code}`);
  }
  return photoSession;
}
```

### on('cameraStatus')

on(type: 'cameraStatus', callback: AsyncCallback\<CameraStatusInfo\>): void

相机设备状态回调，通过注册回调函数获取相机的状态变化。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型            | 必填 | 说明       |
| -------- | -----------------| ---- | --------- |
| type     | string           | 是   | 监听事件，固定为'cameraStatus'。cameraManager对象获取成功后可监听。目前只支持对设备打开或者关闭会触发该事件并返回对应信息。 |
| callback | AsyncCallback\<[CameraStatusInfo](#camerastatusinfo)\> | 是   | 回调函数，用于获取镜头状态变化信息。 |                 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function callback(err: BusinessError, cameraStatusInfo: camera.CameraStatusInfo): void {
  console.info(`camera : ${cameraStatusInfo.camera.cameraId}`);
  console.info(`status: ${cameraStatusInfo.status}`);
}

function registerCameraStatus(cameraManager: camera.CameraManager): void {
  cameraManager.on('cameraStatus', callback);
}
```

### off('cameraStatus')

off(type: 'cameraStatus', callback?: AsyncCallback\<CameraStatusInfo\>): void

相机设备状态注销回调，通过注销回调函数取消获取相机的状态变化。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型            | 必填 | 说明       |
| -------- | -----------------| ---- | --------- |
| type     | string           | 是   | 监听事件，固定为'cameraStatus'。cameraManager对象获取成功后可监听。 |
| callback | AsyncCallback\<[CameraStatusInfo](#camerastatusinfo)\> | 否   | 回调函数，可选，有就是匹配on('cameraStatus') callback（callback对象不可是匿名函数）。 |

**示例：**

```ts
function unregisterCameraStatus(cameraManager: camera.CameraManager): void {
  cameraManager.off('cameraStatus');
}
```

### isTorchSupported<sup>11+</sup>

isTorchSupported(): boolean

检测设备是否支持手电筒。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| boolean    | 返回true表示设备支持手电筒。 |

**示例：**

```ts
function isTorchSupported(cameraManager: camera.CameraManager): boolean {
  let isSupported = cameraManager.isTorchSupported();
  return isSupported;
}
```

### isTorchModeSupported<sup>11+</sup>

isTorchModeSupported(mode: TorchMode): boolean

检测是否支持设置的手电筒模式。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型             | 必填 | 说明       |
| -------- | --------------- | ---- | --------- |
| mode | [TorchMode](#torchmode11) | 是 | 手电筒模式。 |

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| boolean    | 返回true表示设备支持设置的手电筒模式。 |

**示例：**

```ts
function isTorchModeSupported(cameraManager: camera.CameraManager, torchMode: camera.TorchMode): boolean {
  let isSupported = cameraManager.isTorchModeSupported(torchMode);
  return isSupported;
}
```

### getTorchMode<sup>11+</sup>

getTorchMode(): TorchMode

获取当前设备手电筒模式。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [TorchMode](#torchmode11)    | 返回设备当前手电筒模式。 |

**示例：**

```ts
function getTorchMode(cameraManager: camera.CameraManager): camera.TorchMode | undefined {
  let torchMode: camera.TorchMode | undefined = undefined;
  torchMode = cameraManager.getTorchMode();
  return torchMode;
}
```

### setTorchMode<sup>11+</sup>

setTorchMode(mode: TorchMode): void

设置设备手电筒模式。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型             | 必填 | 说明       |
| -------- | --------------- | ---- | --------- |
| mode | [TorchMode](#torchmode11) | 是 | 手电筒模式。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400101 | Parameter missing or parameter type incorrect. |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function setTorchMode(cameraManager: camera.CameraManager, torchMode: camera.TorchMode): void {
  try {
    cameraManager.setTorchMode(torchMode);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The setTorchMode call failed. error code: ${err.code}`);
  }
}
```

### on('torchStatusChange')<sup>11+</sup>

on(type: 'torchStatusChange', callback: AsyncCallback\<TorchStatusInfo\>): void

手电筒状态变化回调，通过注册回调函数获取手电筒状态变化。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型             | 必填 | 说明       |
| -------- | --------------- | ---- | --------- |
| type     | string          | 是   | 监听事件，固定为'torchStatusChange'。cameraManager对象获取成功后可监听。目前只支持手电筒打开，手电筒关闭，手电筒不可用，手电筒恢复可用会触发该事件并返回对应信息。 |
| callback | AsyncCallback\<TorchStatusInfo> | 是   | 回调函数，用于获取手电筒状态变化信息。               |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function callback(err: BusinessError, torchStatusInfo: camera.TorchStatusInfo): void {
  console.info(`onTorchStatusChange, isTorchAvailable: ${torchStatusInfo.isTorchAvailable}, isTorchActive: ${torchStatusInfo.isTorchActive}, level: ${torchStatusInfo.torchLevel}`);
}

function registerTorchStatusChange(cameraManager: camera.CameraManager): void {
  cameraManager.on('torchStatusChange', callback);
}
```

### off('torchStatusChange')<sup>11+</sup>

off(type: 'torchStatusChange', callback?: AsyncCallback\<TorchStatusInfo\>): void

手电筒状态变化注销回调，通过注销回调函数取消获取手电筒状态变化。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型             | 必填 | 说明       |
| -------- | --------------- | ---- | --------- |
| type     | string          | 是   | 监听事件，固定为'torchStatusChange'。cameraManager对象获取成功后可监听。 |
| callback | AsyncCallback\<TorchStatusInfo> | 否   | 回调函数，可选参数，有就是匹配on('torchStatusChange') callback（callback对象不可是匿名函数）。               |

**示例：**

```ts
function unregisterTorchStatusChange(cameraManager: camera.CameraManager): void {
  cameraManager.off('torchStatusChange');
}
```

## TorchMode<sup>11+</sup>

枚举，手电筒模式。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称                          | 值   | 说明           |
| ---------------------------- | ---- | ------------- |
| OFF    | 0    | 常关模式。      |
| ON  | 1    | 常开模式。 |
| AUTO      | 2    | 自动模式。 |

## TorchStatusInfo<sup>11+</sup>

手电筒回调返回的接口实例，表示手电筒状态信息。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称              | 类型       | 只读 | 必填 | 说明        |
| ---------------- | ---------- | ---- | ---- | ----------- |
| isTorchAvailable | boolean    | 是   | 是   | 手电筒是否可用。|
| isTorchActive    | boolean    | 是   | 是   | 手电筒是否被激活。    |
| torchLevel       | number     | 是   | 是   | 手电筒亮度等级。取值范围为[0,1]，越靠近1，亮度越大。    |

## Size

输出能力查询。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称   | 类型    | 只读 | 必填 | 说明         |
| ------ | ------ | ---- | ---- | ------------ |
| height | number | 否   | N/A  | 图像尺寸高(像素)。 |
| width  | number | 否   | N/A  | 图像尺寸宽(像素)。 |

## Point

点坐标用于对焦、曝光配置。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称    | 类型   | 只读   | 必填   | 说明         |
| ------ | ------ | ------ | ------ | ------------ |
| x      | number | 否     | 是     | 点的x坐标。   |
| y      | number | 否     | 是     | 点的y坐标。   |

## CameraFormat

枚举，输出格式。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称                     | 值        | 说明         |
| ----------------------- | --------- | ------------ |
| CAMERA_FORMAT_RGBA_8888 | 3         | RGBA_888格式的图片。        |
| CAMERA_FORMAT_YUV_420_SP| 1003      | YUV_420_SP格式的图片。      |
| CAMERA_FORMAT_JPEG      | 2000      | JPEG格式的图片。            |
| CAMERA_FORMAT_YCBCR_P010<sup>11+</sup> |   2001    | YCBCR_P010格式的图片。      |
| CAMERA_FORMAT_YCRCB_P010<sup>11+</sup> |   2002    | YCRCB_P010格式的图片。      |

## CameraInput

相机设备输入对象。

会话中[Session](#session11)使用的相机信息。

### open

open(callback: AsyncCallback\<void\>): void

打开相机，通过注册回调函数获取状态。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                  | 必填 | 说明                  |
| -------- | -------------------- | ---- | ------------------- |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400107                |  Can not use camera cause of conflict.               |
| 7400108                |  Camera disabled cause of security reason.                                  |
| 7400201                |  Camera service fatal error.                                  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function openCameraInput(cameraInput: camera.CameraInput): void {
  cameraInput.open((err: BusinessError) => {
    if (err) {
      console.error(`Failed to open the camera, error code: ${err.code}.`);
      return;
    }
    console.info('Callback returned with camera opened.');
  });
}
```

### open

open(): Promise\<void\>

打开相机，通过Promise获取相机的状态。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型           | 说明                      |
| -------------- | ----------------------- |
| Promise\<void\> | 使用Promise的方式获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400107                |  Can not use camera cause of conflict.               |
| 7400108                |  Camera disabled cause of security reason.                                  |
| 7400201                |  Camera service fatal error.                                  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function openCameraInput(cameraInput: camera.CameraInput): void {
  cameraInput.open().then(() => {
    console.info('Promise returned with camera opened.');
  }).catch((error: BusinessError) => {
    let err = error as BusinessError;
    console.error(`Failed to open the camera, error code: ${err.code}.`);
  });
}
```

### close

close(callback: AsyncCallback\<void\>\): void

关闭相机，通过注册回调函数获取状态。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                   | 必填 | 说明                  |
| -------- | -------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400201                |  Camera service fatal error.                                  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function closeCameraInput(cameraInput: camera.CameraInput): void {
  cameraInput.close((err: BusinessError) => {
    if (err) {
      console.error(`Failed to close the cameras, error code: ${err.code}.`);
      return;
    }
    console.info('Callback returned with camera closed.');
  });
}
```

### close

close(): Promise\<void\>

关闭相机，通过Promise获取状态。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型           | 说明                      |
| -------------- | ----------------------- |
| Promise\<void\> | 使用Promise的方式获取结果。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400201                |  Camera service fatal error.                                  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function closeCameraInput(cameraInput: camera.CameraInput): void {
  cameraInput.close().then(() => {
    console.info('Promise returned with camera closed.');
  }).catch((error: BusinessError) => {
    let err = error as BusinessError;
    console.error(`Failed to close the cameras, error code: ${err.code}.`);
  });
}
```

### on('error')

on(type: 'error', camera: CameraDevice, callback: ErrorCallback): void

监听CameraInput的错误事件，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                              | 必填 | 说明                                          |
| -------- | -------------------------------- | --- | ------------------------------------------- |
| type     | string                           | 是   | 监听事件，固定为'error'，CameraInput对象创建成功可监听。相机设备出错情况下可触发该事件并返回结果，比如设备不可用或者冲突等返回对应错误信息。 |
| camera   | [CameraDevice](#cameradevice)    | 是   | CameraDevice对象。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback) | 是   | 回调函数，用于获取结果。返回错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function callback(err: BusinessError): void {
  console.error(`Camera input error code: ${err.code}`);
}

function registerCameraInputError(cameraInput: camera.CameraInput, camera: camera.CameraDevice): void {
  cameraInput.on('error', camera, callback);
}
```

### off('error')

off(type: 'error', camera: CameraDevice, callback?: ErrorCallback): void

注销监听CameraInput的错误事件。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                              | 必填 | 说明                                          |
| -------- | -------------------------------- | --- | ------------------------------------------- |
| type     | string                           | 是   | 监听事件，固定为'error'，CameraInput对象创建成功可监听。相机设备出错情况下可触发该事件并返回结果，比如设备不可用或者冲突等返回对应错误信息。 |
| camera   | [CameraDevice](#cameradevice)    | 是   | CameraDevice对象。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback) | 否   | 回调函数，可选，有就是匹配on('error') callback（callback对象不可是匿名函数）。   |

**示例：**

```ts
function unregisterCameraInputError(cameraInput: camera.CameraInput, camera: camera.CameraDevice): void {
  cameraInput.off('error', camera);
}
```

## CameraOutput

会话中[Session](#session11)使用的输出信息，output的基类。

### release

release(callback: AsyncCallback\<void\>): void

释放输出资源，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                 |
| -------- | -------------------- | ---- | ------------------- |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function releasePreviewOutput(previewOutput: camera.PreviewOutput): void {
  previewOutput.release((err: BusinessError) => {
    if (err) {
      console.error(`Failed to release the PreviewOutput instance ${err.code}`);
      return;
    }
    console.info('Callback invoked to indicate that the previewOutput instance is released successfully.');
  });
}

function releaseVideoOutput(videoOutput: camera.VideoOutput): void {
  videoOutput.release((err: BusinessError) => {
    if (err) {
      console.error(`Failed to release the VideoOutput instance ${err.code}`);
      return;
    }
    console.info('Callback invoked to indicate that the videoOutput instance is released successfully.');
  });
}
```

### release

release(): Promise\<void\>

释放输出资源，通过Promise获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型            | 说明                     |
| -------------- | ----------------------- |
| Promise\<void\> | 使用Promise的方式获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function releasePreviewOutput(previewOutput: camera.PreviewOutput): void {
  previewOutput.release().then(() => {
    console.info('Promise returned to indicate that the PreviewOutput instance is released successfully.');
  }).catch((error: BusinessError) => {
    let err = error as BusinessError;
    console.error(`Failed to previewOutput release, error code: ${err.code}`);
  });
}

function releaseVideoOutput(videoOutput: camera.VideoOutput): void {
  videoOutput.release().then(() => {
    console.info('Promise returned to indicate that the VideoOutput instance is released successfully.');
  }).catch((error: BusinessError) => {
    let err = error as BusinessError;
    console.error(`Failed to videoOutput release, error code: ${err.code}`);
  });
}
```

## PreviewOutput

预览输出类。继承[CameraOutput](#cameraoutput)。

### start<sup>(deprecated)</sup>

start(callback: AsyncCallback\<void\>): void

开始输出预览流，通过注册回调函数获取结果。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Session.start](#start11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                 |
| -------- | -------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function startPreviewOutput(previewOutput: camera.PreviewOutput): void {
  previewOutput.start((err: BusinessError) => {
    if (err) {
      console.error(`Failed to start the previewOutput, error code: ${err.code}.`);
      return;
    }
    console.info('Callback returned with previewOutput started.');
  });
}
```

### start<sup>(deprecated)</sup>

start(): Promise\<void\>

开始输出预览流，通过Promise获取结果。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Session.start](#start11-1)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型            | 说明                     |
| -------------- | ----------------------- |
| Promise\<void\> | 使用Promise的方式获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。|

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function startPreviewOutput(previewOutput: camera.PreviewOutput): void {
  previewOutput.start().then(() => {
    console.info('Promise returned with previewOutput started.');
  }).catch((error: BusinessError) => {
    let err = error as BusinessError;
    console.error(`Failed to previewOutput start, error code: ${err.code}.`);
  });
}
```

### stop<sup>(deprecated)</sup>

stop(callback: AsyncCallback\<void\>): void

停止输出预览流，通过注册回调函数获取结果。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Session.stop](#stop11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                 |
| -------- | -------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function stopPreviewOutput(previewOutput: camera.PreviewOutput): void {
  previewOutput.stop((err: BusinessError) => {
    if (err) {
      console.error(`Failed to stop the previewOutput, error code: ${err.code}.`);
      return;
    }
    console.info('Returned with previewOutput stopped.');
  })
}
```

### stop<sup>(deprecated)</sup>

stop(): Promise\<void\>

停止输出预览流，通过Promise获取结果。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Session.stop](#stop11-1)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型            | 说明                     |
| -------------- | ------------------------ |
| Promise\<void\> | 使用Promise的方式获取结果。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function stopPreviewOutput(previewOutput: camera.PreviewOutput): void {
  previewOutput.stop().then(() => {
    console.info('Callback returned with previewOutput stopped.');
  }).catch((error: BusinessError) => {
    let err = error as BusinessError;
    console.error(`Failed to previewOutput stop, error code: ${err.code}.`);
  });
}
```

### on('frameStart')

on(type: 'frameStart', callback: AsyncCallback\<void\>): void

监听预览帧启动，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                                     |
| -------- | -------------------- | ---- | --------------------------------------- |
| type     | string               | 是   | 监听事件，固定为'frameStart'，previewOutput创建成功可监听。底层第一次开始曝光时触发该事件并返回。 |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。只要有该事件返回就证明预览开始。                    |

**示例：**

```ts
function callback(): void {
  console.info('Preview frame started');
}

function registerPreviewOutputFrameStart(previewOutput: camera.PreviewOutput): void {
  previewOutput.on('frameStart', callback);
}
```

### off('frameStart')

off(type: 'frameStart', callback?: AsyncCallback\<void\>): void

注销监听预览帧启动。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                                     |
| -------- | -------------------- | ---- | --------------------------------------- |
| type     | string               | 是   | 监听事件，固定为'frameStart'，previewOutput创建成功可监听。 |
| callback | AsyncCallback\<void\> | 否   | 回调函数，可选，有就是匹配on('frameStart') callback（callback对象不可是匿名函数）。    |

**示例：**

```ts
function unregisterPreviewOutputFrameStart(previewOutput: camera.PreviewOutput): void {
  previewOutput.off('frameStart');
}
```

### on('frameEnd')

on(type: 'frameEnd', callback: AsyncCallback\<void\>): void

监听预览帧结束，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                                  |
| -------- | -------------------- | ---- | ------------------------------------- |
| type     | string               | 是   | 监听事件，固定为'frameEnd'，previewOutput创建成功可监听。预览完全结束最后一帧时触发该事件并返回。 |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。只要有该事件返回就证明预览结束。                |

**示例：**

```ts
function callback(): void {
  console.info('Preview frame ended');
}

function registerPreviewOutputFrameEnd(previewOutput: camera.PreviewOutput): void {
  previewOutput.on('frameEnd', callback);
}
```

### off('frameEnd')

off(type: 'frameEnd', callback?: AsyncCallback\<void\>): void

注销监听预览帧结束。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                                  |
| -------- | -------------------- | ---- | ------------------------------------- |
| type     | string               | 是   | 监听事件，固定为'frameEnd'，previewOutput创建成功可监听。 |
| callback | AsyncCallback\<void\> | 否   |  回调函数，可选，有就是匹配on('frameEnd') callback（callback对象不可是匿名函数）。                |

**示例：**

```ts
function unregisterPreviewOutputFrameEnd(previewOutput: camera.PreviewOutput): void {
  previewOutput.off('frameEnd');
}
```

### on('error')

on(type: 'error', callback: ErrorCallback): void

监听预览输出的错误事件，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型         | 必填 | 说明                       |
| -------- | --------------| ---- | ------------------------ |
| type     | string        | 是   | 监听事件，固定为'error'，previewOutput创建成功可监听。预览接口使用错误时触发该事件，比如调用[Session.start](#start11-1)，[CameraOutput.release](#release-1)等接口发生错误时返回对应错误信息。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback) | 是   | 回调函数，用于获取错误信息。返回错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function callback(previewOutputError: BusinessError): void {
  console.error(`Preview output error code: ${previewOutputError.code}`);
}

function registerPreviewOutputError(previewOutput: camera.PreviewOutput): void {
  previewOutput.on('error', callback)
}
```

### off('error')

off(type: 'error', callback?: ErrorCallback): void

注销监听预览输出的错误事件。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型         | 必填 | 说明                       |
| -------- | --------------| ---- | ------------------------ |
| type     | string        | 是   | 监听事件，固定为'error'，previewOutput创建成功可监听。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback) | 否   | 回调函数，可选，有就是匹配on('error') callback（callback对象不可是匿名函数）。    |

**示例：**

```ts
function unregisterPreviewOutputError(previewOutput: camera.PreviewOutput): void {
  previewOutput.off('error');
}
```

## ImageRotation

枚举，图片旋转角度。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称          | 值   | 说明           |
| ------------ | ---- | ------------- |
| ROTATION_0   | 0    | 图片旋转0度。   |
| ROTATION_90  | 90   | 图片旋转90度。  |
| ROTATION_180 | 180  | 图片旋转180度。 |
| ROTATION_270 | 270  | 图片旋转270度。 |

## Location

图片地理位置信息。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称          | 类型   | 只读 | 必填 |说明         |
| ------------ | ------ | ---- | --- |------------ |
| latitude     | number |  否  | N/A |纬度(度)。    |
| longitude    | number |  否  | N/A |经度(度)。    |
| altitude     | number |  否  | N/A |海拔(米)。    |

## QualityLevel

枚举，图片质量。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称                  | 值   | 说明         |
| -------------------- | ---- | ------------ |
| QUALITY_LEVEL_HIGH   | 0    | 图片质量高。   |
| QUALITY_LEVEL_MEDIUM | 1    | 图片质量中等。 |
| QUALITY_LEVEL_LOW    | 2    | 图片质量差。   |


## PhotoCaptureSetting

拍摄照片的设置。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称      | 类型                            | 只读 | 必填 | 说明                                                                   |
| -------- | ------------------------------- | ---- | ---- |----------------------------------------------------------------------|
| quality  | [QualityLevel](#qualitylevel)   | 否   | 否   | 图片质量(默认低)。                                                           |
| rotation | [ImageRotation](#imagerotation) | 否   | 否   | 图片旋转角度(默认0度，顺时针旋转)。                                                  |
| location | [Location](#location)           | 否   | 否   | 图片地理位置信息(默认以设备硬件信息为准)。                                               |
| mirror   | boolean                         | 否   | 否   | 镜像使能开关(默认关)。使用之前需要使用[isMirrorSupported](#ismirrorsupported)进行判断是否支持。 |

## Photo<sup>11+</sup>

全质量图对象。

### 属性

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称   | 类型                            |     必填     | 说明       |
| ------ | ----------------------------- | -------------- | ---------- |
| main<sup>11+</sup> | [image.Image](../apis-image-kit/js-apis-image.md#image9) |        是       | 全质量图Image。 |

### release<sup>11+</sup>

release(): Promise\<void\>

释放输出资源，通过Promise获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型            | 说明                     |
| -------------- | ----------------------- |
| Promise\<void\> | 使用Promise的方式获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**示例：**

```ts
async function releasePhoto(photo: camera.Photo): Promise<void> {
  await photo.release();
}
```

## PhotoOutput

拍照会话中使用的输出信息，继承[CameraOutput](#cameraoutput)。

### capture

capture(callback: AsyncCallback\<void\>): void

以默认设置触发一次拍照，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                 |
| -------- | -------------------- | ---- | ------------------- |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400104                |  Session not running.                                  |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function capture(photoOutput: camera.PhotoOutput): void {
  photoOutput.capture((err: BusinessError) => {
    if (err) {
      console.error(`Failed to capture the photo, error code: ${err.code}.`);
      return;
    }
    console.info('Callback invoked to indicate the photo capture request success.');
  });
}
```

### capture

capture(): Promise\<void\>

以默认设置触发一次拍照，通过Promise获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型            | 说明                     |
| -------------- | ------------------------ |
| Promise\<void\> | 使用Promise的方式获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400104                |  Session not running.                                  |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function capture(photoOutput: camera.PhotoOutput): void {
  photoOutput.capture().then(() => {
    console.info('Promise returned to indicate that photo capture request success.');
  }).catch((error: BusinessError) => {
    let err = error as BusinessError;
    console.error(`Failed to photoOutput capture, error code: ${err.code}.`);
  });
}
```

### capture

capture(setting: PhotoCaptureSetting, callback: AsyncCallback\<void\>): void

以指定参数触发一次拍照，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                                         | 必填 | 说明                  |
| -------- | ------------------------------------------- | ---- | -------------------- |
| setting  | [PhotoCaptureSetting](#photocapturesetting) | 是   | 拍照设置。             |
| callback | AsyncCallback\<void\>                        | 是   | 回调函数，用于获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。  |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400101                |  Parameter missing or parameter type incorrect.        |
| 7400104                |  Session not running.                                  |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function capture(photoOutput: camera.PhotoOutput): void {
  let captureLocation: camera.Location = {
    latitude: 0,
    longitude: 0,
    altitude: 0
  }
  let settings: camera.PhotoCaptureSetting = {
    quality: camera.QualityLevel.QUALITY_LEVEL_LOW,
    rotation: camera.ImageRotation.ROTATION_0,
    location: captureLocation,
    mirror: false
  }
  photoOutput.capture(settings, (err: BusinessError) => {
    if (err) {
      console.error(`Failed to capture the photo, error code: ${err.code}.`);
      return;
    }
    console.info('Callback invoked to indicate the photo capture request success.');
  });
}
```

### capture

capture(setting: PhotoCaptureSetting): Promise\<void\>

以指定参数触发一次拍照，通过Promise获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                                         | 必填 | 说明      |
| ------- | ------------------------------------------- | ---- | -------- |
| setting | [PhotoCaptureSetting](#photocapturesetting) | 是   | 拍照设置，传入undefined类型数据按默认无参处理。 |

**返回值：**

| 类型            | 说明                     |
| -------------- | ------------------------ |
| Promise\<void\> | 使用Promise的方式获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400101                |  Parameter missing or parameter type incorrect.        |
| 7400104                |  Session not running.                                  |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function capture(photoOutput: camera.PhotoOutput): void {
  let captureLocation: camera.Location = {
    latitude: 0,
    longitude: 0,
    altitude: 0
  }
  let settings: camera.PhotoCaptureSetting = {
    quality: camera.QualityLevel.QUALITY_LEVEL_LOW,
    rotation: camera.ImageRotation.ROTATION_0,
    location: captureLocation,
    mirror: false
  }
  photoOutput.capture(settings).then(() => {
    console.info('Promise returned to indicate that photo capture request success.');
  }).catch((error: BusinessError) => {
    let err = error as BusinessError;
    console.error(`Failed to photoOutput capture, error code: ${err.code}.`);
  });
}
```

### on('photoAvailable')<sup>11+</sup>

on(type: 'photoAvailable', callback: AsyncCallback\<Photo\>): void

注册监听全质量图上报。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型      | 必填 | 说明                                  |
| -------- | ---------- | --- | ------------------------------------ |
| type     | string     | 是   | 监听事件，固定为'photoAvailable'，photoOutput创建成功后可监听。 |
| callback | AsyncCallback\<[Photo](#photo11)\> | 是   | 回调函数，用于监听全质量图上报。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import image from '@ohos.multimedia.image';

function callback(err: BusinessError, photo: camera.Photo): void {
  let mainImage: image.Image = photo.main;
}

function registerPhotoOutputPhotoAvailable(photoOutput: camera.PhotoOutput): void {
  photoOutput.on('photoAvailable', callback);
}
```

### off('photoAvailable')<sup>11+</sup>

off(type: 'photoAvailable', callback?: AsyncCallback\<Photo\>): void

注销监听全质量图上报。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                    | 必填 | 说明                                       |
| -------- | ---------------------- | ---- | ------------------------------------------ |
| type     | string                 | 是   | 监听事件，固定为'photoAvailable'，photoOutput创建成功后可监听。 |
| callback | AsyncCallback\<[Photo](#photo11)\> | 否   | 回调函数，可选，有就是匹配on('photoAvailable') callback（callback对象不可是匿名函数）。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';
import image from '@ohos.multimedia.image';

function callback(err: BusinessError, photo: camera.Photo): void {
  let mainImage: image.Image = photo.main;
}

function unRegisterPhotoOutputPhotoAvailable(photoOutput: camera.PhotoOutput): void {
  photoOutput.off('photoAvailable', callback);
}
```

### on('captureStartWithInfo')<sup>11+</sup>

on(type: 'captureStartWithInfo', callback: AsyncCallback\<CaptureStartInfo\>): void

监听拍照开始，通过注册回调函数获取CaptureStartInfo。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型      | 必填 | 说明                                  |
| -------- | ---------- | --- | ------------------------------------ |
| type     | string     | 是   | 监听事件，固定为'captureStartWithInfo'，photoOutput创建成功后可监听。 |
| callback | AsyncCallback\<[CaptureStartInfo](#capturestartinfo11)\> | 是   | 使用callback的方式获取Capture ID。|

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function callback(err: BusinessError, captureStartInfo: camera.CaptureStartInfo): void {
  console.info(`photo capture started, captureStartInfo : ${captureStartInfo}`);
}

function registerCaptureStartWithInfo(photoOutput: camera.PhotoOutput): void {
  photoOutput.on('captureStartWithInfo', callback);
}
```

### off('captureStartWithInfo')<sup>11+</sup>

off(type: 'captureStartWithInfo', callback?: AsyncCallback\<CaptureStartInfo\>): void

注销监听拍照。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                    | 必填 | 说明                                       |
| -------- | ---------------------- | ---- | ------------------------------------------ |
| type     | string                 | 是   | 监听事件，固定为'captureStartWithInfo'，photoOutput创建成功后可监听。 |
| callback | AsyncCallback\<[CaptureStartInfo](#capturestartinfo11)\> | 否   | 回调函数，可选，有就是匹配on('captureStartWithInfo') callback（callback对象不可是匿名函数）。            |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function unRegisterCaptureStartWithInfo(photoOutput: camera.PhotoOutput): void {
  photoOutput.off('captureStartWithInfo');
}
```

### isMirrorSupported

isMirrorSupported(): boolean

查询是否支持镜像拍照。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型            | 说明                     |
| -------------- | ----------------------- |
| boolean | 返回是否支持镜像拍照，true表示支持，false表示不支持。 |

**示例：**

```ts
function isMirrorSupported(photoOutput: camera.PhotoOutput): boolean {
  let isSupported: boolean = photoOutput.isMirrorSupported();
  return isSupported;
}
```

### on('captureStart')<sup>(deprecated)</sup>

on(type: 'captureStart', callback: AsyncCallback\<number\>): void

监听拍照开始，通过注册回调函数获取Capture ID。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[on('captureStartWithInfo')](#oncapturestartwithinfo11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                    | 必填 | 说明                                       |
| -------- | ---------------------- | ---- | ------------------------------------------ |
| type     | string                 | 是   | 监听事件，固定为'captureStart'，photoOutput创建成功后可监听。每次拍照，底层开始曝光时触发该事件并返回。 |
| callback | AsyncCallback\<number\> | 是   | 使用callback的方式获取Capture ID。            |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function callback(err: BusinessError, captureId: number): void {
  console.info(`photo capture started, captureId : ${captureId}`);
}

function registerPhotoOutputCaptureStart(photoOutput: camera.PhotoOutput): void {
  photoOutput.on('captureStart', callback);
}
```

### off('captureStart')<sup>(deprecated)</sup>

off(type: 'captureStart', callback?: AsyncCallback\<number\>): void

注销监听拍照开始。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[off('captureStartWithInfo')](#offcapturestartwithinfo11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                    | 必填 | 说明                                       |
| -------- | ---------------------- | ---- | ------------------------------------------ |
| type     | string                 | 是   | 监听事件，固定为'captureStart'，photoOutput创建成功后可监听。 |
| callback | AsyncCallback\<number\> | 否   | 回调函数，可选，有就是匹配on('captureStart') callback（callback对象不可是匿名函数）。  |

**示例：**

```ts
function unregisterPhotoOutputCaptureStart(photoOutput: camera.PhotoOutput): void {
  photoOutput.off('captureStart');
}
```

### on('frameShutter')

on(type: 'frameShutter', callback: AsyncCallback\<FrameShutterInfo\>): void

监听拍照帧输出捕获，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型      | 必填 | 说明                                  |
| -------- | ---------- | --- | ------------------------------------ |
| type     | string     | 是   | 监听事件，固定为'frameShutter'，photoOutput创建成功后可监听。 |
| callback | AsyncCallback\<[FrameShutterInfo](#frameshutterinfo)\> | 是   | 回调函数，用于获取相关信息。该回调返回意味着可以再次下发拍照请求。             |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function callback(err: BusinessError, frameShutterInfo: camera.FrameShutterInfo): void {
  console.info(`CaptureId for frame : ${frameShutterInfo.captureId}`);
  console.info(`Timestamp for frame : ${frameShutterInfo.timestamp}`);
}

function registerPhotoOutputFrameShutter(photoOutput: camera.PhotoOutput): void {
  photoOutput.on('frameShutter', callback);
}
```

### off('frameShutter')

off(type: 'frameShutter', callback?: AsyncCallback\<FrameShutterInfo\>): void

注销监听拍照帧输出捕获。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型      | 必填 | 说明                                  |
| -------- | ---------- | --- | ------------------------------------ |
| type     | string     | 是   | 监听事件，固定为'frameShutter'，photoOutput创建成功后可监听。 |
| callback | AsyncCallback\<[FrameShutterInfo](#frameshutterinfo)\> | 否   | 回调函数，可选，有就是匹配on('frameShutter') callback（callback对象不可是匿名函数）。             |

**示例：**

```ts
function unregisterPhotoOutputFrameShutter(photoOutput: camera.PhotoOutput): void {
  photoOutput.off('frameShutter');
}
```

### on('captureEnd')

on(type: 'captureEnd', callback: AsyncCallback\<CaptureEndInfo\>): void

监听拍照结束，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型           | 必填 | 说明                                       |
| -------- | --------------- | ---- | ---------------------------------------- |
| type     | string          | 是   | 监听事件，固定为'captureEnd'，photoOutput创建成功后可监听。拍照完全结束可触发该事件发生并返回相应信息。 |
| callback | AsyncCallback\<[CaptureEndInfo](#captureendinfo)\> | 是   | 回调函数，用于获取相关信息。                  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function callback(err: BusinessError, captureEndInfo: camera.CaptureEndInfo): void {
  console.info(`photo capture end, captureId : ${captureEndInfo.captureId}`);
  console.info(`frameCount : ${captureEndInfo.frameCount}`);
}

function registerPhotoOutputCaptureEnd(photoOutput: camera.PhotoOutput): void {
  photoOutput.on('captureEnd', callback);
}
```

### off('captureEnd')

off(type: 'captureEnd', callback?: AsyncCallback\<CaptureEndInfo\>): void

注销监听拍照结束。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型           | 必填 | 说明                                       |
| -------- | --------------- | ---- | ---------------------------------------- |
| type     | string          | 是   | 监听事件，固定为'captureEnd'，photoOutput创建成功后可监听。 |
| callback | AsyncCallback\<[CaptureEndInfo](#captureendinfo)\> | 否   | 回调函数，可选，有就是匹配on('captureEnd') callback（callback对象不可是匿名函数）。                  |

**示例：**

```ts
function unregisterPhotoOutputCaptureEnd(photoOutput: camera.PhotoOutput): void {
  photoOutput.off('captureEnd');
}
```

### on('error')

on(type: 'error', callback: ErrorCallback): void

监听拍照输出发生错误，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型         | 必填 | 说明                                 |
| -------- | ------------- | ---- | ----------------------------------- |
| type     | string       | 是   | 监听事件，固定为'error'，photoOutput创建成功后可监听。拍照接口调用时出现错误触发该事件并返回错误信息。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback) | 是   | 回调函数，用于获取错误信息。返回错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。             |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function callback(err: BusinessError): void {
  console.error(`Photo output error code: ${err.code}`);
}

function registerPhotoOutputError(photoOutput: camera.PhotoOutput): void {
  photoOutput.on('error', callback);
}
```

### off('error')

off(type: 'error', callback?: ErrorCallback): void

注销监听拍照输出发生错误。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型         | 必填 | 说明                                 |
| -------- | ------------- | ---- | ----------------------------------- |
| type     | string       | 是   | 监听事件，固定为'error'，photoOutput创建成功后可监听。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback) | 否   | 回调函数，可选，有就是匹配on('error') callback（callback对象不可是匿名函数）。   |

**示例：**

```ts
function unregisterPhotoOutputError(photoOutput: camera.PhotoOutput): void {
  photoOutput.off('error');
}
```

## FrameShutterInfo

拍照帧输出信息。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称       | 类型   | 只读 | 必填 | 说明        |
| --------- | ------ | ---- | ---- | ---------- |
| captureId | number | 否   | 是   | 拍照的ID。  |
| timestamp | number | 否   | 是   | 快门时间戳。 |

## CaptureStartInfo<sup>11+</sup>

拍照开始信息。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称       | 类型    | 只读 | 必填 | 说明       |
| ---------- | ------ | ---- | ---- | --------- |
| captureId  | number | 否   | 是   | 拍照的ID。 |
| time       | number | 否   | 是   | 拍照时间戳。    |

## CaptureEndInfo

拍照停止信息。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称       | 类型    | 只读 | 必填 | 说明       |
| ---------- | ------ | ---- | ---- | ---------|
| captureId  | number | 否   | 是   | 拍照的ID。 |
| frameCount | number | 否   | 是   | 帧数。    |

## VideoOutput

录像会话中使用的输出信息，继承[CameraOutput](#cameraoutput)。

### start

start(callback: AsyncCallback\<void\>): void

启动录制，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                 |
| -------- | -------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function startVideoOutput(videoOutput: camera.VideoOutput): void {
  videoOutput.start((err: BusinessError) => {
    if (err) {
      console.error(`Failed to start the video output, error code: ${err.code}.`);
      return;
    }
    console.info('Callback invoked to indicate the video output start success.');
  });
}
```

### start

start(): Promise\<void\>

启动录制，通过Promise获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型            | 说明                     |
| -------------- | ----------------------- |
| Promise\<void\> | 使用Promise的方式获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function startVideoOutput(videoOutput: camera.VideoOutput): void {
  videoOutput.start().then(() => {
    console.info('Promise returned to indicate that start method execution success.');
  }).catch((error: BusinessError) => {
    let err = error as BusinessError;
    console.error(`Failed to videoOutput start, error code: ${err.code}.`);
  });
}
```

### stop

stop(callback: AsyncCallback\<void\>): void

结束录制，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                 | 必填 | 说明                     |
| -------- | -------------------- | ---- | ------------------------ |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function stopVideoOutput(videoOutput: camera.VideoOutput): void {
  videoOutput.stop((err: BusinessError) => {
    if (err) {
      console.error(`Failed to stop the video output, error code: ${err.code}.`);
      return;
    }
    console.info('Callback invoked to indicate the video output stop success.');
  });
}
```

### stop

stop(): Promise\<void\>

结束录制，通过Promise获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型            | 说明                     |
| -------------- | ----------------------- |
| Promise\<void\> | 使用Promise的方式获取结果。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function stopVideoOutput(videoOutput: camera.VideoOutput): void {
  videoOutput.stop().then(() => {
    console.info('Promise returned to indicate that stop method execution success.');
  }).catch((error: BusinessError) => {
    let err = error as BusinessError;
    console.error(`Failed to videoOutput stop, error code: ${err.code}.`);
  });
}
```

### on('frameStart')

on(type: 'frameStart', callback: AsyncCallback\<void\>): void

监听录像开始，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                                       |
| -------- | -------------------- | ---- | ----------------------------------------- |
| type     | string               | 是   | 监听事件，固定为'frameStart'，videoOutput创建成功后可监听。底层第一次曝光时触发该事件并返回。 |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。  只要有该事件返回就证明录像开始。                     |

**示例：**

```ts
function callback(): void {
  console.info('Video frame started');
}

function registerVideoOutputFrameStart(videoOutput: camera.VideoOutput): void {
  videoOutput.on('frameStart', callback);
}
```

### off('frameStart')

off(type: 'frameStart', callback?: AsyncCallback\<void\>): void

注销监听录像开始。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                                       |
| -------- | -------------------- | ---- | ----------------------------------------- |
| type     | string               | 是   | 监听事件，固定为'frameStart'，videoOutput创建成功后可监听。 |
| callback | AsyncCallback\<void\> | 否   | 回调函数，可选，有就是匹配on('frameStart') callback（callback对象不可是匿名函数）。  |

**示例：**

```ts
function unregisterVideoOutputFrameStart(videoOutput: camera.VideoOutput): void {
  videoOutput.off('frameStart');
}

```

### on('frameEnd')

on(type: 'frameEnd', callback: AsyncCallback\<void\>): void

监听录像结束，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                                       |
| -------- | -------------------- | ---- | ------------------------------------------ |
| type     | string               | 是   | 监听事件，固定为'frameEnd'，videoOutput创建成功后可监听。录像完全结束最后一帧时触发该事件并返回。 |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。 只要有该事件返回就证明录像结束。                      |

**示例：**

```ts
function callback(): void {
  console.info('Video frame ended');
}

function registerVideoOutputFrameEnd(videoOutput: camera.VideoOutput): void {
  videoOutput.on('frameEnd', callback);
}
```

### off('frameEnd')

off(type: 'frameEnd', callback?: AsyncCallback\<void\>): void

注销监听录像结束。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                                       |
| -------- | -------------------- | ---- | ------------------------------------------ |
| type     | string               | 是   | 监听事件，固定为'frameEnd'，videoOutput创建成功后可监听。 |
| callback | AsyncCallback\<void\> | 否   | 回调函数，可选，有就是匹配on('frameEnd') callback（callback对象不可是匿名函数）。    |

**示例：**

```ts
function unregisterVideoOutputFrameEnd(videoOutput: camera.VideoOutput): void {
  videoOutput.off('frameEnd');
}
```

### on('error')

on(type: 'error', callback: ErrorCallback): void

监听录像输出发生错误，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型       | 必填 | 说明                                    |
| -------- | ----------- | ---- | -------------------------------------- |
| type     | string      | 是   | 监听事件，固定为'error'，videoOutput创建成功后可监听。录像接口调用出现错误时触发该事件并返回对应错误码，比如调用[start](#start-1)，[CameraOutput.release](#release-1)接口时出现错误返回对应错误信息。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback) | 是   | 回调函数，用于获取错误信息。返回错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。                 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function callback(err: BusinessError): void {
  console.error(`Video output error code: ${err.code}`);
}

function registerVideoOutputError(videoOutput: camera.VideoOutput): void {
  videoOutput.on('error', callback);
}
```

### off('error')

off(type: 'error', callback?: ErrorCallback): void

注销监听录像输出发生错误。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型         | 必填 | 说明                                 |
| -------- | ------------- | ---- | ----------------------------------- |
| type     | string       | 是   | 监听事件，固定为'error'，photoOutput创建成功后可监听。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback) | 否   | 回调函数，可选，有就是匹配on('error') callback（callback对象不可是匿名函数）。               |

**示例：**

```ts
function unregisterVideoOutputError(videoOutput: camera.VideoOutput): void {
  videoOutput.off('error');
}
```

## MetadataOutput

metadata流。继承[CameraOutput](#cameraoutput)。

### start

start(callback: AsyncCallback\<void\>): void

开始输出metadata，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                 |
| -------- | -------------------------- | ---- | ------------------- |
| callback | AsyncCallback\<void\>       | 是   | 回调函数，用于获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function startMetadataOutput(metadataOutput: camera.MetadataOutput): void {
  metadataOutput.start((err: BusinessError) => {
    if (err) {
      console.error(`Failed to start metadataOutput, error code: ${err.code}.`);
      return;
    }
    console.info('Callback returned with metadataOutput started.');
  });
}
```

### start

start(): Promise\<void\>

开始输出metadata，通过Promise获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型                     | 说明                     |
| ----------------------  | ------------------------ |
| Promise\<void\>          | 使用Promise的方式获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function startMetadataOutput(metadataOutput: camera.MetadataOutput): void {
  metadataOutput.start().then(() => {
    console.info('Callback returned with metadataOutput started.');
  }).catch((error: BusinessError) => {
    let err = error as BusinessError;
    console.error(`Failed to metadataOutput stop, error code: ${err.code}`);
  });
}
```

### stop

stop(callback: AsyncCallback\<void\>): void

停止输出metadata，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                         | 必填 | 说明                  |
| -------- | -------------------------- | ---- | ------------------- |
| callback | AsyncCallback\<void\>       | 是   | 回调函数，用于获取结果。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function stopMetadataOutput(metadataOutput: camera.MetadataOutput): void {
  metadataOutput.stop((err: BusinessError) => {
    if (err) {
      console.error(`Failed to stop the metadataOutput, error code: ${err.code}.`);
      return;
    }
    console.info('Callback returned with metadataOutput stopped.');
  })
}
```

### stop

stop(): Promise\<void\>

停止输出metadata，通过Promise获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型                    | 说明                        |
| ----------------------  | --------------------------- |
| Promise\<void\>         | 使用Promise的方式获取结果。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function stopMetadataOutput(metadataOutput: camera.MetadataOutput): void {
  metadataOutput.stop().then(() => {
    console.info('Callback returned with metadataOutput stopped.');
  }).catch((error: BusinessError) => {
    let err = error as BusinessError;
    console.error(`Failed to metadataOutput stop, error code: ${err.code}`);
  });
}
```

### on('metadataObjectsAvailable')

on(type: 'metadataObjectsAvailable', callback: AsyncCallback\<Array\<MetadataObject\>\>): void

监听检测到的metadata对象，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型         | 必填 | 说明                                  |
| -------- | -------------- | ---- | ------------------------------------ |
| type     | string         | 是   | 监听事件，固定为'metadataObjectsAvailable'，metadataOutput创建成功后可监听。检测到有效的metadata数据时触发该事件发生并返回相应的metadata数据。 |
| callback | AsyncCallback\<Array\<[MetadataObject](#metadataobject)\>\> | 是   | 回调函数，用于获取metadata数据。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function callback(err: BusinessError, metadataObjectArr: Array<camera.MetadataObject>): void {
  console.info('metadata output metadataObjectsAvailable');
}

function registerMetadataObjectsAvailable(metadataOutput: camera.MetadataOutput): void {
  metadataOutput.on('metadataObjectsAvailable', callback);
}
```

### off('metadataObjectsAvailable')

off(type: 'metadataObjectsAvailable', callback?: AsyncCallback\<Array\<MetadataObject\>\>): void

注销监听检测到的metadata对象。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型         | 必填 | 说明                                  |
| -------- | -------------- | ---- | ------------------------------------ |
| type     | string         | 是   | 监听事件，固定为'metadataObjectsAvailable'，metadataOutput创建成功后可监听。 |
| callback | AsyncCallback\<Array\<[MetadataObject](#metadataobject)\>\> | 否   | 回调函数，可选，有就是匹配on('metadataObjectsAvailable') callback（callback对象不可是匿名函数）。 |

**示例：**

```ts
function unregisterMetadataObjectsAvailable(metadataOutput: camera.MetadataOutput): void {
  metadataOutput.off('metadataObjectsAvailable');
}
```

### on('error')

on(type: 'error', callback: ErrorCallback): void

监听metadata流的错误，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型         | 必填 | 说明                                     |
| -------- | ------------- | ---- | --------------------------------------- |
| type     | string        | 是   | 监听事件，固定为'error'，metadataOutput创建成功后可监听。metadata接口使用错误时触发该事件并返回对应错误码，比如调用[start](#start-3)，[CameraOutput.release](#release-1)接口时发生错误返回对应错误信息。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback) | 是   | 回调函数，用于获取错误信息。返回错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。            |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function callback(metadataOutputError: BusinessError): void {
  console.error(`Metadata output error code: ${metadataOutputError.code}`);
}

function registerMetadataOutputError(metadataOutput: camera.MetadataOutput): void {
  metadataOutput.on('error', callback);
}
```

### off('error')

off(type: 'error', callback?: ErrorCallback): void

注销监听metadata流的错误。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型         | 必填 | 说明                                     |
| -------- | ------------- | ---- | --------------------------------------- |
| type     | string        | 是   | 监听事件，固定为'error'，metadataOutput创建成功后可监听。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback) | 否   | 回调函数，可选，有就是匹配on('error') callback（callback对象不可是匿名函数）。           |

**示例：**

```ts
function unregisterMetadataOutputError(metadataOutput: camera.MetadataOutput): void {
  metadataOutput.off('error');
}
```

## MetadataObjectType

枚举，metadata流。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称                       | 值   | 说明              |
| ------------------------- | ---- | ----------------- |
| FACE_DETECTION            | 0    | metadata对象类型，用于人脸检测。<br> 检测点应在0-1坐标系内，该坐标系左上角为(0，0)，右下角为(1，1)。<br> 此坐标系以设备充电口在右侧时的横向设备方向为基准。<br>例如应用的预览界面布局以设备充电口在下侧时的竖向方向为基准，<br>布局宽高为(w，h)， 返回点为(x，y)，则转换后的坐标点为(1-y，x)。 |

## Rect

矩形定义。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称      | 类型   |  只读  |  必填  |           说明         |
| -------- | ------ | ------ | ------ | --------------------- |
| topLeftX | number |   否   |   N/A  | 矩形区域左上角x坐标。   |
| topLeftY | number |   否   |   N/A  | 矩形区域左上角y坐标。   |
| width    | number |   否   |   N/A  | 矩形宽，相对值，范围[0, 1]。  |
| height   | number |   否   |   N/A  | 矩形高，相对值，范围[0, 1]。  |

## MetadataObject

相机元能力信息，[CameraInput](#camerainput)相机信息中的数据来源，通过metadataOutput.on('metadataObjectsAvailable')接口获取。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称         | 类型                                        | 只读 | 必填 |说明                |
| ----------- | ------------------------------------------- | ---- | ---- | ----------------- |
| type        | [MetadataObjectType](#metadataobjecttype)   |  是  |  是  | metadata 类型。    |
| timestamp   | number                                      |  是  |  是  | 当前时间戳（毫秒）。|
| boundingBox | [Rect](#rect)                               |  是  |  是  | metadata 区域框。  |

## FlashMode

枚举，闪光灯模式。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称                    | 值   | 说明        |
| ---------------------- | ---- | ---------- |
| FLASH_MODE_CLOSE       | 0    | 闪光灯关闭。 |
| FLASH_MODE_OPEN        | 1    | 闪光灯打开。 |
| FLASH_MODE_AUTO        | 2    | 自动闪光灯。 |
| FLASH_MODE_ALWAYS_OPEN | 3    | 闪光灯常亮。 |

## ExposureMode

枚举，曝光模式。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称                           | 值   | 说明         |
| ----------------------------- | ---- | ----------- |
| EXPOSURE_MODE_LOCKED          | 0    | 锁定曝光模式。不支持曝光区域中心点设置。 |
| EXPOSURE_MODE_AUTO            | 1    | 自动曝光模式。支持曝光区域中心点设置，可以使用[AutoExposure.setMeteringPoint](#setmeteringpoint11)设置曝光区域中心点。 |
| EXPOSURE_MODE_CONTINUOUS_AUTO | 2    | 连续自动曝光。不支持曝光区域中心点设置。 |

## FocusMode

枚举，焦距模式。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称                        | 值   | 说明          |
| -------------------------- | ---- | ------------ |
| FOCUS_MODE_MANUAL          | 0    | 手动对焦。通过手动修改相机焦距来改变对焦位置，不支持对焦点设置。     |
| FOCUS_MODE_CONTINUOUS_AUTO | 1    | 连续自动对焦。不支持对焦点设置。 |
| FOCUS_MODE_AUTO            | 2    | 自动对焦。支持对焦点设置，可以使用[Focus.setFocusPoint](#setfocuspoint11)设置对焦点，根据对焦点执行一次自动对焦。    |
| FOCUS_MODE_LOCKED          | 3    | 对焦锁定。不支持对焦点设置。     |

## FocusState

枚举，焦距状态。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称                   | 值   | 说明       |
| --------------------- | ---- | --------- |
| FOCUS_STATE_SCAN      | 0    | 触发对焦。  |
| FOCUS_STATE_FOCUSED   | 1    | 对焦成功。  |
| FOCUS_STATE_UNFOCUSED | 2    | 未完成对焦。 |

## VideoStabilizationMode

枚举，视频防抖模式。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称       | 值   | 说明         |
| --------- | ---- | ------------ |
| OFF       | 0    | 关闭视频防抖功能。   |
| LOW       | 1    | 使用基础防抖算法。   |
| MIDDLE    | 2    | 使用防抖效果一般的防抖算法，防抖效果优于LOW类型。   |
| HIGH      | 3    | 使用防抖效果最好的防抖算法，防抖效果优于MIDDLE类型。   |
| AUTO      | 4    | 自动进行选择。   |

## Session<sup>11+</sup>

会话类，保存一次相机运行所需要的所有资源[CameraInput](#camerainput)、[CameraOutput](#cameraoutput)，并向相机设备申请完成相机功能(录像，拍照)。

### beginConfig<sup>11+</sup>

beginConfig(): void

开始配置会话。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400105                |  Session config locked.               |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function beginConfig(session: camera.Session): void {
  try {
    session.beginConfig();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The beginConfig call failed. error code: ${err.code}`);
  }
}
```

### commitConfig<sup>11+</sup>

commitConfig(callback: AsyncCallback\<void\>): void

提交配置信息，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                   | 必填 | 说明                  |
| -------- | -------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400102                |  Operation not allowed.                                  |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function commitConfig(session: camera.Session): void {
  session.commitConfig((err: BusinessError) => {
    if (err) {
      console.error(`The commitConfig call failed. error code: ${err.code}`);
      return;
    }
    console.info('Callback invoked to indicate the commit config success.');
  });
}
```

### commitConfig<sup>11+</sup>

commitConfig(): Promise\<void\>

提交配置信息，通过Promise获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型            | 说明                     |
| -------------- | ------------------------ |
| Promise\<void\> | 使用Promise的方式获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400102                |  Operation not allowed.                                  |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function commitConfig(session: camera.Session): void {
  session.commitConfig().then(() => {
    console.info('Promise returned to indicate the commit config success.');
  }).catch((error: BusinessError) => {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The commitConfig call failed. error code: ${err.code}`);
  });
}
```

### canAddInput<sup>11+</sup>

canAddInput(cameraInput: CameraInput): boolean

判断当前cameraInput是否可以添加到session中。当前函数需要在[beginConfig](#beginconfig11)和[commitConfig](#commitconfig11-1)之间生效。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名        | 类型                          | 必填 | 说明                     |
| ----------- | --------------------------- | ---- | ------------------------ |
| cameraInput | [CameraInput](#camerainput) | 是   | 需要添加的CameraInput实例。 |

**返回值：**

| 类型            | 说明                     |
| -------------- | ------------------------ |
| boolean | 返回true表示支持添加当前cameraInput，返回false表示不支持添加。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function canAddInput(session: camera.Session, cameraInput: camera.CameraInput): void {
  let canAdd: boolean = session.canAddInput(cameraInput);
  console.info(`The input canAddInput: ${canAdd}`);
}
```

### addInput<sup>11+</sup>

addInput(cameraInput: CameraInput): void

把[CameraInput](#camerainput)加入到会话。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名        | 类型                          | 必填 | 说明                     |
| ----------- | --------------------------- | ---- | ------------------------ |
| cameraInput | [CameraInput](#camerainput) | 是   | 需要添加的CameraInput实例。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400101                |  Parameter missing or parameter type incorrect.        |
| 7400102                |  Operation not allowed.                                  |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function addInput(session: camera.Session, cameraInput: camera.CameraInput): void {
  try {
    session.addInput(cameraInput);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The addInput call failed. error code: ${err.code}`);
  }
}
```

### removeInput<sup>11+</sup>

removeInput(cameraInput: CameraInput): void

移除[CameraInput](#camerainput)。当前函数需要在[beginConfig](#beginconfig11)和[commitConfig](#commitconfig11-1)之间生效。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名        | 类型                          | 必填 | 说明                      |
| ----------- | --------------------------- | ---- | ------------------------ |
| cameraInput | [CameraInput](#camerainput) | 是   | 需要移除的CameraInput实例。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400101                |  Parameter missing or parameter type incorrect.        |
| 7400102                |  Operation not allowed.                                  |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function removeInput(session: camera.Session, cameraInput: camera.CameraInput): void {
  try {
    session.removeInput(cameraInput);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The removeInput call failed. error code: ${err.code}`);
  }
}
```

### canAddOutput<sup>11+</sup>

canAddOutput(cameraOutput: CameraOutput): boolean

判断当前cameraOutput是否可以添加到session中。当前函数需要在[addInput](#addinput11)和[commitConfig](#commitconfig11-1)之间生效。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名        | 类型                          | 必填 | 说明                     |
| ----------- | --------------------------- | ---- | ------------------------ |
| cameraOutput | [CameraOutput](#cameraoutput) | 是   | 需要添加的CameraOutput实例。 |

**返回值：**

| 类型            | 说明                     |
| -------------- | ------------------------ |
| boolean | 是否可以添加当前cameraOutput到session中。 |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function canAddOutput(session: camera.Session, cameraOutput: camera.CameraOutput): void {
  let canAdd: boolean = session.canAddOutput(cameraOutput);
  console.info(`This addOutput can add: ${canAdd}`);
}
```

### addOutput<sup>11+</sup>

addOutput(cameraOutput: CameraOutput): void

把[CameraOutput](#cameraoutput)加入到会话。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名           | 类型                             | 必填 | 说明                      |
| ------------- | ------------------------------- | ---- | ------------------------ |
| cameraOutput  | [CameraOutput](#cameraoutput)   | 是   | 需要添加的CameraOutput实例。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400101                |  Parameter missing or parameter type incorrect.        |
| 7400102                |  Operation not allowed.                                  |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function addOutput(session: camera.Session, cameraOutput: camera.CameraOutput): void {
  try {
    session.addOutput(cameraOutput);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The addOutput call failed. error code: ${err.code}`);
  }
}
```

### removeOutput<sup>11+</sup>

removeOutput(cameraOutput: CameraOutput): void

从会话中移除[CameraOutput](#cameraoutput)。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名           | 类型                             | 必填 | 说明                      |
| ------------- | ------------------------------- | ---- | ------------------------ |
| cameraOutput  | [CameraOutput](#cameraoutput)   | 是   | 需要移除的CameraOutput实例。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400101                |  Parameter missing or parameter type incorrect.        |
| 7400102                |  Operation not allowed.                                  |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function removeOutput(session: camera.Session, previewOutput: camera.PreviewOutput): void {
  try {
    session.removeOutput(previewOutput);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The removeOutput call failed. error code: ${err.code}`);
  }
}
```

### start<sup>11+</sup>

start(callback: AsyncCallback\<void\>): void

开始会话工作，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                 |
| -------- | -------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function startCaptureSession(session: camera.Session): void {
  session.start((err: BusinessError) => {
    if (err) {
      console.error(`Failed to start the session, error code: ${err.code}.`);
      return;
    }
    console.info('Callback invoked to indicate the session start success.');
  });
}
```

### start<sup>11+</sup>

start(): Promise\<void\>

开始会话工作，通过Promise获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型            | 说明                     |
| -------------- | ------------------------ |
| Promise\<void\> | 使用Promise的方式获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function startCaptureSession(session: camera.Session): void {
  session.start().then(() => {
    console.info('Promise returned to indicate the session start success.');
  }).catch((error: BusinessError) => {
    let err = error as BusinessError;
    console.error(`Failed to start the session, error code: ${err.code}.`);
  });
}
```

### stop<sup>11+</sup>

stop(callback: AsyncCallback\<void\>): void

停止会话工作，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                 |
| -------- | -------------------- | ---- | ------------------- |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function stopCaptureSession(session: camera.Session): void {
  session.stop((err: BusinessError) => {
    if (err) {
      console.error(`Failed to stop the session, error code: ${err.code}.`);
      return;
    }
    console.info('Callback invoked to indicate the session stop success.');
  });
}
```

### stop<sup>11+</sup>

stop(): Promise\<void\>

停止会话工作，通过Promise获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型            | 说明                     |
| -------------- | ----------------------- |
| Promise\<void\> | 使用Promise的方式获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function stopCaptureSession(session: camera.Session): void {
  session.stop().then(() => {
    console.info('Promise returned to indicate the session stop success.');
  }).catch((error: BusinessError) => {
    let err = error as BusinessError;
    console.error(`Failed to stop the session, error code: ${err.code}.`);
  });
}
```

### release<sup>11+</sup>

release(callback: AsyncCallback\<void\>): void

释放会话资源，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                 |
| -------- | -------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function releaseCaptureSession(session: camera.Session): void {
  session.release((err: BusinessError) => {
    if (err) {
      console.error(`Failed to release the session instance, error code: ${err.code}.`);
      return;
    }
    console.info('Callback invoked to indicate that the session instance is released successfully.');
  });
}
```

### release<sup>11+</sup>

release(): Promise\<void\>

释放会话资源，通过Promise获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型            | 说明                     |
| -------------- | ------------------------ |
| Promise\<void\> | 使用Promise的方式获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function releaseCaptureSession(session: camera.Session): void {
  session.release().then(() => {
    console.info('Promise returned to indicate that the session instance is released successfully.');
  }).catch((error: BusinessError) => {
    let err = error as BusinessError;
    console.error(`Failed to release the session instance, error code: ${err.code}.`);
  });
}
```

## Flash<sup>11+</sup>

闪光灯类，对设备闪光灯操作。

### hasFlash<sup>11+</sup>

hasFlash(): boolean

检测是否有闪光灯，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| boolean    | 返回true表示设备支持闪光灯，false表示不支持。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function hasFlash(photoSession: camera.PhotoSession): boolean {
  let status: boolean = false;
  try {
    status = photoSession.hasFlash();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The hasFlash call failed. error code: ${err.code}`);
  }
  return status;
}
```

### isFlashModeSupported<sup>11+</sup>

isFlashModeSupported(flashMode: FlashMode): boolean

检测闪光灯模式是否支持。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名       | 类型                     | 必填 | 说明                               |
| --------- | ----------------------- | ---- | --------------------------------- |
| flashMode | [FlashMode](#flashmode) | 是   | 指定闪光灯模式。                     |

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| boolean    | 返回true表示支持该闪光灯模式，false表示不支持。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function isFlashModeSupported(photoSession: camera.PhotoSession): boolean {
  let status: boolean = false;
  try {
    status = photoSession.isFlashModeSupported(camera.FlashMode.FLASH_MODE_AUTO);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The isFlashModeSupported call failed. error code: ${err.code}`);
  }
  return status;
}
```

### setFlashMode<sup>11+</sup>

setFlashMode(flashMode: FlashMode): void

设置闪光灯模式。

进行设置之前，需要先检查：

1. 设备是否支持闪光灯，可使用方法[hasFlash](#hasflash11)。
2. 设备是否支持指定的闪光灯模式，可使用方法[isFlashModeSupported](#isflashmodesupported11)。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名       | 类型                     | 必填 | 说明                  |
| --------- | ----------------------- | ---- | --------------------- |
| flashMode | [FlashMode](#flashmode) | 是   | 指定闪光灯模式。       |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function setFlashMode(photoSession: camera.PhotoSession): void {
  try {
    photoSession.setFlashMode(camera.FlashMode.FLASH_MODE_AUTO);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The setFlashMode call failed. error code: ${err.code}`);
  }
}
```

### getFlashMode<sup>11+</sup>

getFlashMode(): FlashMode

获取当前设备的闪光灯模式。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [FlashMode](#flashmode)    | 获取当前设备的闪光灯模式。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getFlashMode(photoSession: camera.PhotoSession): camera.FlashMode | undefined {
  let flashMode: camera.FlashMode | undefined = undefined;
  try {
    flashMode = photoSession.getFlashMode();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getFlashMode call failed.error code: ${err.code}`);
  }
  return flashMode;
}
```

## AutoExposure<sup>11+</sup>

自动曝光类，对设备自动曝光（AE）操作。

### isExposureModeSupported<sup>11+</sup>

isExposureModeSupported(aeMode: ExposureMode): boolean

检测曝光模式是否支持。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                           | 必填  | 说明                           |
| -------- | -------------------------------| ---- | ----------------------------- |
| aeMode   | [ExposureMode](#exposuremode)  | 是   | 曝光模式。                      |

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| boolean    | 获取是否支持曝光模式。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function isExposureModeSupported(photoSession: camera.PhotoSession): boolean {
  let isSupported: boolean = false;
  try {
    isSupported = photoSession.isExposureModeSupported(camera.ExposureMode.EXPOSURE_MODE_LOCKED);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The isExposureModeSupported call failed. error code: ${err.code}`);
  }
  return isSupported;
}
```

### getExposureMode<sup>11+</sup>

getExposureMode(): ExposureMode

获取当前曝光模式。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [ExposureMode](#exposuremode)    | 获取当前曝光模式。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getExposureMode(photoSession: camera.PhotoSession): camera.ExposureMode | undefined {
  let exposureMode: camera.ExposureMode | undefined = undefined;
  try {
    exposureMode = photoSession.getExposureMode();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getExposureMode call failed. error code: ${err.code}`);
  }
  return exposureMode;
}
```

### setExposureMode<sup>11+</sup>

setExposureMode(aeMode: ExposureMode): void

设置曝光模式。进行设置之前，需要先检查设备是否支持指定的曝光模式，可使用方法[isExposureModeSupported](#isexposuremodesupported11)。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                            | 必填 | 说明                    |
| -------- | -------------------------------| ---- | ----------------------- |
| aeMode   | [ExposureMode](#exposuremode)  | 是   | 曝光模式。                |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function setExposureMode(photoSession: camera.PhotoSession): void {
  try {
    photoSession.setExposureMode(camera.ExposureMode.EXPOSURE_MODE_LOCKED);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The setExposureMode call failed. error code: ${err.code}`);
  }
}
```

### getMeteringPoint<sup>11+</sup>

getMeteringPoint(): Point

查询曝光区域中心点。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [Point](#point)    | 获取当前曝光点。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getMeteringPoint(photoSession: camera.PhotoSession): camera.Point | undefined {
  let exposurePoint: camera.Point | undefined = undefined;
  try {
    exposurePoint = photoSession.getMeteringPoint();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getMeteringPoint call failed. error code: ${err.code}`);
  }
  return exposurePoint;
}
```

### setMeteringPoint<sup>11+</sup>

setMeteringPoint(point: Point): void

设置曝光区域中心点，曝光点应在0-1坐标系内，该坐标系左上角为{0，0}，右下角为{1，1}。<br>此坐标系是以设备充电口在右侧时的横向设备方向为基准的，例如应用的预览界面布局以<br>设备充电口在下侧时的竖向方向为基准，布局宽高为{w，h}，且触碰点为{x，y}，<br>则转换后的坐标点为{y/h，1-x/w}。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名           | 类型                            | 必填 | 说明                 |
| ------------- | -------------------------------| ---- | ------------------- |
| point | [Point](#point)                | 是   | 曝光点，x、y设置范围应在[0，1]之内，超过范围，如果小于0设置0，大于1设置1。             |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function setMeteringPoint(photoSession: camera.PhotoSession): void {
  const point: camera.Point = {x: 1, y: 1};
  try {
    photoSession.setMeteringPoint(point);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The setMeteringPoint call failed. error code: ${err.code}`);
  }
}
```

### getExposureBiasRange<sup>11+</sup>

getExposureBiasRange(): Array\<number\>

查询曝光补偿范围。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| Array\<number\>   | 获取补偿范围的数组。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getExposureBiasRange(photoSession: camera.PhotoSession): Array<number> {
  let biasRangeArray: Array<number> = [];
  try {
    biasRangeArray = photoSession.getExposureBiasRange();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getExposureBiasRange call failed. error code: ${err.code}`);
  }
  return biasRangeArray;
}
```

### setExposureBias<sup>11+</sup>

setExposureBias(exposureBias: number): void

设置曝光补偿，曝光补偿值（EV）。

进行设置之前，建议先通过方法[getExposureBiasRange](#getexposurebiasrange11)查询支持的范围。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                            | 必填 | 说明                 |
| -------- | -------------------------------| ---- | ------------------- |
| exposureBias   | number                   | 是   | 曝光补偿，[getExposureBiasRange](#getexposurebiasrange11)查询支持的范围，如果设置超过支持范围的值，自动匹配到就近临界点。<br>曝光补偿存在步长，如步长为0.5。则设置1.2时，获取到实际生效曝光补偿为1.0。<br>接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function setExposureBias(photoSession: camera.PhotoSession, biasRangeArray: Array<number>): void {
  if (biasRangeArray && biasRangeArray.length > 0) {
    let exposureBias = biasRangeArray[0];
    try {
      photoSession.setExposureBias(exposureBias);
    } catch (error) {
      // 失败返回错误码error.code并处理
      let err = error as BusinessError;
      console.error(`The setExposureBias call failed. error code: ${err.code}`);
    }
  }
}
```

### getExposureValue<sup>11+</sup>

getExposureValue(): number

查询当前曝光值。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| number    | 获取曝光值。曝光补偿存在步长，如步长为0.5。则设置1.2时，获取到实际生效曝光补偿为1.0。<br>接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getExposureValue(photoSession: camera.PhotoSession): number {
  const invalidValue: number = -1;
  let exposureValue: number = invalidValue;
  try {
    exposureValue = photoSession.getExposureValue();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getExposureValue call failed. error code: ${err.code}`);
  }
  return exposureValue;
}
```

## Focus<sup>11+</sup>

对焦类，对设备对焦操作。

### isFocusModeSupported<sup>11+</sup>

isFocusModeSupported(afMode: FocusMode): boolean

检测对焦模式是否支持。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                     | 必填 | 说明                              |
| -------- | ----------------------- | ---- | -------------------------------- |
| afMode   | [FocusMode](#focusmode) | 是   | 指定的焦距模式。                    |

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| boolean    | 返回true表示支持该焦距模式，false表示不支持。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function isFocusModeSupported(photoSession: camera.PhotoSession): boolean {
  let status: boolean = false;
  try {
    status = photoSession.isFocusModeSupported(camera.FocusMode.FOCUS_MODE_AUTO);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The isFocusModeSupported call failed. error code: ${err.code}`);
  }
  return status;
}
```

### setFocusMode<sup>11+</sup>

setFocusMode(afMode: FocusMode): void

设置对焦模式。

进行设置之前，需要先检查设备是否支持指定的焦距模式，可使用方法[isFocusModeSupported](#isfocusmodesupported11)。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                     | 必填 | 说明                 |
| -------- | ----------------------- | ---- | ------------------- |
| afMode   | [FocusMode](#focusmode) | 是   | 指定的焦距模式。       |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function setFocusMode(photoSession: camera.PhotoSession): void {
  try {
    photoSession.setFocusMode(camera.FocusMode.FOCUS_MODE_AUTO);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The setFocusMode call failed. error code: ${err.code}`);
  }
}
```

### getFocusMode<sup>11+</sup>

getFocusMode(): FocusMode

获取当前的对焦模式。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [FocusMode](#focusmode)   | 获取当前设备的焦距模式。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getFocusMode(photoSession: camera.PhotoSession): camera.FocusMode | undefined {
  let afMode: camera.FocusMode | undefined = undefined;
  try {
    afMode = photoSession.getFocusMode();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getFocusMode call failed. error code: ${err.code}`);
  }
  return afMode;
}
```

### setFocusPoint<sup>11+</sup>

setFocusPoint(point: Point): void

设置焦点，焦点应在0-1坐标系内，该坐标系左上角为{0，0}，右下角为{1，1}。<br>此坐标系是以设备充电口在右侧时的横向设备方向为基准的，例如应用的预览界面布局以<br>设备充电口在下侧时的竖向方向为基准，布局宽高为{w，h}，且触碰点为{x，y}，<br>则转换后的坐标点为{y/h，1-x/w}。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                     | 必填 | 说明                 |
| -------- | ----------------------- | ---- | ------------------- |
| point    | [Point](#point)         | 是   | 焦点。x、y设置范围应在[0，1]之内，超过范围，如果小于0设置0，大于1设置1。   |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function setFocusPoint(photoSession: camera.PhotoSession): void {
  const focusPoint: camera.Point = {x: 1, y: 1};
  try {
    photoSession.setFocusPoint(focusPoint);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The setFocusPoint call failed. error code: ${err.code}`);
  }
}
```

### getFocusPoint<sup>11+</sup>

getFocusPoint(): Point

查询焦点。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [Point](#point)    | 用于获取当前焦点。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getFocusPoint(photoSession: camera.PhotoSession): camera.Point | undefined {
  let point: camera.Point | undefined = undefined;
  try {
    point = photoSession.getFocusPoint();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getFocusPoint call failed. error code: ${err.code}`);
  }
  return point;
}
```

### getFocalLength<sup>11+</sup>

getFocalLength(): number

查询焦距值。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| number    | 用于获取当前焦距，单位mm。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getFocalLength(photoSession: camera.PhotoSession): number {
  const invalidValue: number = -1;
  let focalLength: number = invalidValue;
  try {
    focalLength = photoSession.getFocalLength();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getFocalLength call failed. error code: ${err.code}`);
  }
  return focalLength;
}
```

## SmoothZoomMode<sup>11+</sup>

平滑变焦模式。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称         | 值   | 说明            |
| ------------ | ---- | -------------- |
| NORMAL       | 0    | 贝塞尔曲线模式。  |

## SmoothZoomInfo<sup>11+</sup>

平滑变焦参数信息。

**系统能力：** SystemCapability.Multimedia.Camera.Core

| 名称     | 类型        |   只读   |   必填   | 说明       |
| -------- | ---------- | -------- | -------- | ---------- |
| duration |   number   |   否     |    是    | 平滑变焦总时长，单位ms。 |

## Zoom<sup>11+</sup>

变焦类，对设备变焦操作。

### getZoomRatioRange<sup>11+</sup>

getZoomRatioRange(): Array\<number\>

获取支持的变焦范围。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| Array\<number\>   | 用于获取可变焦距比范围，返回的数组包括其最小值和最大值。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getZoomRatioRange(photoSession: camera.PhotoSession): Array<number> {
  let zoomRatioRange: Array<number> = [];
  try {
    zoomRatioRange = photoSession.getZoomRatioRange();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getZoomRatioRange call failed. error code: ${err.code}`);
  }
  return zoomRatioRange;
}
```

### setZoomRatio<sup>11+</sup>

setZoomRatio(zoomRatio: number): void

设置变焦比，变焦精度最高为小数点后两位，如果设置超过支持的精度范围，则只保留精度范围内数值。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名       | 类型                  | 必填 | 说明                 |
| --------- | -------------------- | ---- | ------------------- |
| zoomRatio | number               | 是   | 可变焦距比，通过[getZoomRatioRange](#getzoomratiorange11)获取支持的变焦范围，如果设置超过支持范围的值，则只保留精度范围内数值。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function setZoomRatio(photoSession: camera.PhotoSession, zoomRatioRange: Array<number>): void {
  if (zoomRatioRange === undefined || zoomRatioRange.length <= 0) {
    return;
  }
  let zoomRatio = zoomRatioRange[0];
  try {
    photoSession.setZoomRatio(zoomRatio);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The setZoomRatio call failed. error code: ${err.code}`);
  }
}
```

### getZoomRatio<sup>11+</sup>

getZoomRatio(): number

获取当前的变焦比。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| number    | 获取当前的变焦比结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getZoomRatio(photoSession: camera.PhotoSession): number {
  const invalidValue: number = -1;
  let zoomRatio: number = invalidValue;
  try {
    zoomRatio = photoSession.getZoomRatio();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getZoomRatio call failed. error code: ${err.code}`);
  }
  return zoomRatio;
}
```

### setSmoothZoom<sup>11+</sup>

setSmoothZoom(targetRatio: number, mode?: SmoothZoomMode): void

触发平滑变焦。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名       | 类型            | 必填 | 说明               |
| ------------ | -------------- | ---- | ----------------- |
| targetRatio  | number         | 是   | 目标值。      |
| mode         | [SmoothZoomMode](#smoothzoommode11) | 否   | 模式。      |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function setSmoothZoom(sessionExtendsZoom: camera.Zoom, targetZoomRatio: number, mode: camera.SmoothZoomMode): void {
  try {
    sessionExtendsZoom.setSmoothZoom(targetZoomRatio, mode);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The setSmoothZoom call failed. error code: ${err.code}`);
  }
}
```

## Stabilization<sup>11+</sup>

防抖类，对设备防抖操作。

### isVideoStabilizationModeSupported<sup>11+</sup>

isVideoStabilizationModeSupported(vsMode: VideoStabilizationMode): boolean

查询是否支持指定的视频防抖模式。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                                              | 必填 | 说明                             |
| -------- | ------------------------------------------------- | ---- | ------------------------------ |
| vsMode   | [VideoStabilizationMode](#videostabilizationmode) | 是   | 视频防抖模式。                    |

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| boolean    | 返回视频防抖模式是否支持，true表示支持，false表示不支持。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function isVideoStabilizationModeSupported(videoSession: camera.VideoSession): boolean {
  let isSupported: boolean = false;
  try {
    isSupported = videoSession.isVideoStabilizationModeSupported(camera.VideoStabilizationMode.OFF);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The isVideoStabilizationModeSupported call failed. error code: ${err.code}`);
  }
  return isSupported;
}
```

### getActiveVideoStabilizationMode<sup>11+</sup>

getActiveVideoStabilizationMode(): VideoStabilizationMode

查询当前正在使用的视频防抖模式。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [VideoStabilizationMode](#videostabilizationmode)    | 视频防抖是否正在使用。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getActiveVideoStabilizationMode(videoSession: camera.VideoSession): camera.VideoStabilizationMode | undefined {
  let vsMode: camera.VideoStabilizationMode | undefined = undefined;
  try {
    vsMode = videoSession.getActiveVideoStabilizationMode();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getActiveVideoStabilizationMode call failed. error code: ${err.code}`);
  }
  return vsMode;
}
```

### setVideoStabilizationMode<sup>11+</sup>

setVideoStabilizationMode(mode: VideoStabilizationMode): void

设置视频防抖模式。需要先检查设备是否支持对应的防抖模式，可以通过[isVideoStabilizationModeSupported](#isvideostabilizationmodesupported11)方法判断所设置的模式是否支持。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                                              | 必填 | 说明                    |
| -------- | ------------------------------------------------- | ---- | --------------------- |
| mode     | [VideoStabilizationMode](#videostabilizationmode) | 是   | 需要设置的视频防抖模式。   |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function setVideoStabilizationMode(videoSession: camera.VideoSession): void {
  try {
    videoSession.setVideoStabilizationMode(camera.VideoStabilizationMode.OFF);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The setVideoStabilizationMode call failed. error code: ${err.code}`);
  }
}
```

## CaptureSession<sup>(deprecated)</sup>

拍照会话类，保存一次相机运行所需要的所有资源[CameraInput](#camerainput)、[CameraOutput](#cameraoutput)，并向相机设备申请完成相机功能(录像，拍照)。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[PhotoSession](#photosession11)、[VideoSession](#videosession11)替代。

### beginConfig<sup>(deprecated)</sup>

beginConfig(): void

开始配置会话。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Session.beginConfig](#beginconfig11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400105         |  Session config locked.               |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function beginConfig(captureSession: camera.CaptureSession): void {
  try {
    captureSession.beginConfig();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The beginConfig call failed. error code: ${err.code}`);
  }
}
```

### commitConfig<sup>(deprecated)</sup>

commitConfig(callback: AsyncCallback\<void\>): void

提交配置信息，通过注册回调函数获取结果。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Session.commitConfig](#commitconfig11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                   | 必填 | 说明                  |
| -------- | -------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode) |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400102                |  Operation not allowed.                                  |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function commitConfig(captureSession: camera.CaptureSession): void {
  captureSession.commitConfig((err: BusinessError) => {
    if (err) {
      console.error(`The commitConfig call failed. error code: ${err.code}`);
      return;
    }
    console.info('Callback invoked to indicate the commit config success.');
  });
}
```

### commitConfig<sup>(deprecated)</sup>

commitConfig(): Promise\<void\>

提交配置信息，通过Promise获取结果。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Session.commitConfig](#commitconfig11-1)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型            | 说明                     |
| -------------- | ------------------------ |
| Promise\<void\> | 使用Promise的方式获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode) |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400102                |  Operation not allowed.                                  |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function commitConfig(captureSession: camera.CaptureSession): void {
  captureSession.commitConfig().then(() => {
    console.info('Promise returned to indicate the commit config success.');
  }).catch((error: BusinessError) => {
    // 失败返回错误码error.code并处理
    console.error(`The commitConfig call failed. error code: ${err.code}`);
  });
}
```

### addInput<sup>(deprecated)</sup>

addInput(cameraInput: CameraInput): void

把[CameraInput](#camerainput)加入到会话。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Session.addInput](#addinput11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名        | 类型                          | 必填 | 说明                     |
| ----------- | --------------------------- | ---- | ------------------------ |
| cameraInput | [CameraInput](#camerainput) | 是   | 需要添加的CameraInput实例。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID   | 错误信息                                          |
|---------|-----------------------------------------------|
| 7400101 | Parameter missing or parameter type incorrect. |
| 7400102 | Operation not allowed.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function addInput(captureSession: camera.CaptureSession, cameraInput: camera.CameraInput): void {
  try {
    captureSession.addInput(cameraInput);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The addInput call failed. error code: ${err.code}`);
  }
}
```

### removeInput<sup>(deprecated)</sup>

removeInput(cameraInput: CameraInput): void

移除[CameraInput](#camerainput)。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Session.removeInput](#removeinput11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名        | 类型                          | 必填 | 说明                      |
| ----------- | --------------------------- | ---- | ------------------------ |
| cameraInput | [CameraInput](#camerainput) | 是   | 需要移除的CameraInput实例。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400101                |  Parameter missing or parameter type incorrect.        |
| 7400102                |  Operation not allowed.                                  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function removeInput(captureSession: camera.CaptureSession, cameraInput: camera.CameraInput): void {
  try {
    captureSession.removeInput(cameraInput);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The removeInput call failed. error code: ${err.code}`);
  }
}
```

### addOutput<sup>(deprecated)</sup>

addOutput(cameraOutput: CameraOutput): void

把[CameraOutput](#cameraoutput)加入到会话。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Session.addOutput](#addoutput11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名           | 类型                             | 必填 | 说明                      |
| ------------- | ------------------------------- | ---- | ------------------------ |
| cameraOutput  | [CameraOutput](#cameraoutput)   | 是   | 需要添加的CameraOutput实例。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400101                |  Parameter missing or parameter type incorrect.        |
| 7400102                |  Operation not allowed.                                  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function addOutput(captureSession: camera.CaptureSession, cameraOutput: camera.CameraOutput): void {
  try {
    captureSession.addOutput(cameraOutput);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The addOutput call failed. error code: ${err.code}`);
  }
}
```

### removeOutput<sup>(deprecated)</sup>

removeOutput(cameraOutput: CameraOutput): void

从会话中移除[CameraOutput](#cameraoutput)。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Session.removeOutput](#removeoutput11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名           | 类型                             | 必填 | 说明                      |
| ------------- | ------------------------------- | ---- | ------------------------ |
| cameraOutput  | [CameraOutput](#cameraoutput)   | 是   | 需要移除的CameraOutput实例。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400101                |  Parameter missing or parameter type incorrect.        |
| 7400102                |  Operation not allowed.                                  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function removeOutput(captureSession: camera.CaptureSession, previewOutput: camera.PreviewOutput): void {
  try {
    captureSession.removeOutput(previewOutput);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The removeOutput call failed. error code: ${err.code}`);
  }
}
```

### start<sup>(deprecated)</sup>

start(callback: AsyncCallback\<void\>): void

开始会话工作，通过注册回调函数获取结果。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Session.start](#start11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                 |
| -------- | -------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function startCaptureSession(captureSession: camera.CaptureSession): void {
  captureSession.start((err: BusinessError) => {
    if (err) {
      console.error(`Failed to start the session, error code: ${err.code}.`);
      return;
    }
    console.info('Callback invoked to indicate the session start success.');
  });
}
```

### start<sup>(deprecated)</sup>

start(): Promise\<void\>

开始会话工作，通过Promise获取结果。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Session.start](#start11-1)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型            | 说明                     |
| -------------- | ------------------------ |
| Promise\<void\> | 使用Promise的方式获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function startCaptureSession(captureSession: camera.CaptureSession): void {
  captureSession.start().then(() => {
    console.info('Promise returned to indicate the session start success.');
  }).catch((err: BusinessError) => {
    console.error(`Failed to start the session, error code: ${err.code}.`);
  });
}
```

### stop<sup>(deprecated)</sup>

stop(callback: AsyncCallback\<void\>): void

停止会话工作，通过注册回调函数获取结果。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Session.stop](#stop11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                 |
| -------- | -------------------- | ---- | ------------------- |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function stopCaptureSession(captureSession: camera.CaptureSession): void {
  captureSession.stop((err: BusinessError) => {
    if (err) {
      console.error(`Failed to stop the session, error code: ${err.code}.`);
      return;
    }
    console.info('Callback invoked to indicate the session stop success.');
  });
}
```

### stop<sup>(deprecated)</sup>

stop(): Promise\<void\>

停止会话工作，通过Promise获取结果。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Session.stop](#stop11-1)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型            | 说明                     |
| -------------- | ----------------------- |
| Promise\<void\> | 使用Promise的方式获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function stopCaptureSession(captureSession: camera.CaptureSession): void {
  captureSession.stop().then(() => {
    console.info('Promise returned to indicate the session stop success.');
  }).catch((err: BusinessError) => {
    console.error(`Failed to stop the session, error code: ${err.code}.`);
  });
}
```

### release<sup>(deprecated)</sup>

release(callback: AsyncCallback\<void\>): void

释放会话资源，通过注册回调函数获取结果。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Session.release](#release11-1)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                  | 必填 | 说明                 |
| -------- | -------------------- | ---- | -------------------- |
| callback | AsyncCallback\<void\> | 是   | 回调函数，用于获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function releaseCaptureSession(captureSession: camera.CaptureSession): void {
  captureSession.release((err: BusinessError) => {
    if (err) {
      console.error(`Failed to release the CaptureSession instance, error code: ${err.code}.`);
      return;
    }
    console.info('Callback invoked to indicate that the CaptureSession instance is released successfully.');
  });
}
```

### release<sup>(deprecated)</sup>

release(): Promise\<void\>

释放会话资源，通过Promise获取结果。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Session.release](#release11-2)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型            | 说明                     |
| -------------- | ------------------------ |
| Promise\<void\> | 使用Promise的方式获取结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400201                |  Camera service fatal error.                           |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function releaseCaptureSession(captureSession: camera.CaptureSession): void {
  captureSession.release().then(() => {
    console.info('Promise returned to indicate that the CaptureSession instance is released successfully.');
  }).catch((err: BusinessError) => {
    console.error(`Failed to release the CaptureSession instance, error code: ${err.code}.`);
  });
}
```

### hasFlash<sup>(deprecated)</sup>

hasFlash(): boolean

检测是否有闪光灯。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Flash.hasFlash](#hasflash11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| boolean    | 返回true表示设备支持闪光灯，false表示不支持。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function hasFlash(captureSession: camera.CaptureSession): boolean {
  let status: boolean = false;
  try {
    status = captureSession.hasFlash();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The hasFlash call failed. error code: ${err.code}`);
  }
  return status;
}
```

### isFlashModeSupported<sup>(deprecated)</sup>

isFlashModeSupported(flashMode: FlashMode): boolean

检测闪光灯模式是否支持。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Flash.isFlashModeSupported](#isflashmodesupported11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名       | 类型                     | 必填 | 说明                               |
| --------- | ----------------------- | ---- | --------------------------------- |
| flashMode | [FlashMode](#flashmode) | 是   | 指定闪光灯模式。                     |

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| boolean    | 返回true表示支持该闪光灯模式，false表示不支持。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function isFlashModeSupported(captureSession: camera.CaptureSession): boolean {
  let status: boolean = false;
  try {
    status = captureSession.isFlashModeSupported(camera.FlashMode.FLASH_MODE_AUTO);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The isFlashModeSupported call failed. error code: ${err.code}`);
  }
  return status;
}
```

### setFlashMode<sup>(deprecated)</sup>

setFlashMode(flashMode: FlashMode): void

设置闪光灯模式。

进行设置之前，需要先检查：

1. 设备是否支持闪光灯，可使用方法[hasFlash](#hasflashdeprecated)。
2. 设备是否支持指定的闪光灯模式，可使用方法[isFlashModeSupported](#isflashmodesupporteddeprecated)。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Flash.setFlashMode](#setflashmode11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                    | 必填 | 说明                 |
| --------- | ----------------------- | ---- | -------------------- |
| flashMode | [FlashMode](#flashmode) | 是   | 指定闪光灯模式。       |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function setFlashMode(captureSession: camera.CaptureSession): void {
  try {
    captureSession.setFlashMode(camera.FlashMode.FLASH_MODE_AUTO);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The setFlashMode call failed. error code: ${err.code}`);
  }
}
```

### getFlashMode<sup>(deprecated)</sup>

getFlashMode(): FlashMode

获取当前设备的闪光灯模式。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Flash.getFlashMode](#getflashmode11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [FlashMode](#flashmode)    | 获取当前设备的闪光灯模式。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getFlashMode(captureSession: camera.CaptureSession): camera.FlashMode | undefined {
  let flashMode: camera.FlashMode | undefined = undefined;
  try {
    flashMode = captureSession.getFlashMode();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getFlashMode call failed.error code: ${err.code}`);
  }
  return flashMode;
}
```

### isExposureModeSupported<sup>(deprecated)</sup>

isExposureModeSupported(aeMode: ExposureMode): boolean

检测曝光模式是否支持。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[AutoExposure.isExposureModeSupported](#isexposuremodesupported11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                           | 必填  | 说明                           |
| -------- | -------------------------------| ---- | ----------------------------- |
| aeMode   | [ExposureMode](#exposuremode)  | 是   | 曝光模式。                      |

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| boolean    | 获取是否支持曝光模式。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function isExposureModeSupported(captureSession: camera.CaptureSession): boolean {
  let isSupported: boolean = false;
  try {
    isSupported = captureSession.isExposureModeSupported(camera.ExposureMode.EXPOSURE_MODE_LOCKED);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The isExposureModeSupported call failed. error code: ${err.code}`);
  }
  return isSupported;
}
```

### getExposureMode<sup>(deprecated)</sup>

getExposureMode(): ExposureMode

获取当前曝光模式。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[AutoExposure.getExposureMode](#getexposuremode11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [ExposureMode](#exposuremode)    | 获取当前曝光模式。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getExposureMode(captureSession: camera.CaptureSession): camera.ExposureMode | undefined {
  let exposureMode: camera.ExposureMode | undefined = undefined;
  try {
    exposureMode = captureSession.getExposureMode();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getExposureMode call failed. error code: ${err.code}`);
  }
  return exposureMode;
}
```

### setExposureMode<sup>(deprecated)</sup>

setExposureMode(aeMode: ExposureMode): void

设置曝光模式。进行设置之前，需要先检查设备是否支持指定的曝光模式，可使用方法[isExposureModeSupported](#isexposuremodesupporteddeprecated)。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[AutoExposure.setExposureMode](#setexposuremode11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                            | 必填 | 说明                    |
| -------- | -------------------------------| ---- | ----------------------- |
| aeMode   | [ExposureMode](#exposuremode)  | 是   | 曝光模式。                |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function setExposureMode(captureSession: camera.CaptureSession): void {
  try {
    captureSession.setExposureMode(camera.ExposureMode.EXPOSURE_MODE_LOCKED);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The setExposureMode call failed. error code: ${err.code}`);
  }
}
```

### getMeteringPoint<sup>(deprecated)</sup>

getMeteringPoint(): Point

查询曝光区域中心点。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[AutoExposure.getMeteringPoint](#getmeteringpoint11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [Point](#point)    | 获取当前曝光点。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getMeteringPoint(captureSession: camera.CaptureSession): camera.Point | undefined {
  let exposurePoint: camera.Point | undefined = undefined;
  try {
    exposurePoint = captureSession.getMeteringPoint();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getMeteringPoint call failed. error code: ${err.code}`);
  }
  return exposurePoint;
}
```

### setMeteringPoint<sup>(deprecated)</sup>

setMeteringPoint(point: Point): void

设置曝光区域中心点，曝光点应在0-1坐标系内，该坐标系左上角为{0，0}，右下角为{1，1}。
此坐标系是以设备充电口在右侧时的横向设备方向为基准的，例如应用的预览界面布局以
设备充电口在下侧时的竖向方向为基准，布局宽高为{w，h}，且触碰点为{x，y}，
则转换后的坐标点为{y/h，1-x/w}。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[AutoExposure.setMeteringPoint](#setmeteringpoint11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名           | 类型                            | 必填 | 说明                 |
| ------------- | -------------------------------| ---- | ------------------- |
| point | [Point](#point)                | 是   | 曝光点，x,y设置范围应在[0,1]之内，超过范围，如果小于0设置0，大于1设置1。             |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function setMeteringPoint(captureSession: camera.CaptureSession): void {
  const point: camera.Point = {x: 1, y: 1};
  try {
    captureSession.setMeteringPoint(point);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The setMeteringPoint call failed. error code: ${err.code}`);
  }
}
```

### getExposureBiasRange<sup>(deprecated)</sup>

getExposureBiasRange(): Array\<number\>

查询曝光补偿范围。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[AutoExposure.getExposureBiasRange](#getexposurebiasrange11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| Array\<number\>   | 获取补偿范围的数组。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getExposureBiasRange(captureSession: camera.CaptureSession): Array<number> {
  let biasRangeArray: Array<number> = [];
  try {
    biasRangeArray = captureSession.getExposureBiasRange();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getExposureBiasRange call failed. error code: ${err.code}`);
  }
  return biasRangeArray;
}
```

### setExposureBias<sup>(deprecated)</sup>

setExposureBias(exposureBias: number): void

设置曝光补偿，曝光补偿值（EV）。

进行设置之前，建议先通过方法[getExposureBiasRange](#getexposurebiasrangedeprecated)查询支持的范围。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[AutoExposure.setExposureBias](#setexposurebias11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                            | 必填 | 说明                 |
| -------- | -------------------------------| ---- | ------------------- |
| exposureBias   | number                   | 是   | 曝光补偿，getExposureBiasRange查询支持的范围，如果设置超过支持范围的值，自动匹配到就近临界点。曝光补偿存在步长，如步长为0.5。则设置1.2时，获取到实际生效曝光补偿为1.0。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function setExposureBias(captureSession: camera.CaptureSession, biasRangeArray: Array<number>): void {
  if (biasRangeArray && biasRangeArray.length > 0) {
    let exposureBias = biasRangeArray[0];
    try {
      captureSession.setExposureBias(exposureBias);
    } catch (error) {
      // 失败返回错误码error.code并处理
      let err = error as BusinessError;
      console.error(`The setExposureBias call failed. error code: ${err.code}`);
    }
  }
}
```

### getExposureValue<sup>(deprecated)</sup>

getExposureValue(): number

查询当前曝光值。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[AutoExposure.getExposureValue](#getexposurevalue11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| number    | 获取曝光值。曝光补偿存在步长，如步长为0.5。则设置1.2时，获取到实际生效曝光补偿为1.0。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getExposureValue(captureSession: camera.CaptureSession): number {
  const invalidValue: number = -1;
  let exposureValue: number = invalidValue;
  try {
    exposureValue = captureSession.getExposureValue();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getExposureValue call failed. error code: ${err.code}`);
  }
  return exposureValue;
}
```

### isFocusModeSupported<sup>(deprecated)</sup>

isFocusModeSupported(afMode: FocusMode): boolean

检测对焦模式是否支持。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Focus.isFocusModeSupported](#isfocusmodesupported11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                     | 必填 | 说明                              |
| -------- | ----------------------- | ---- | -------------------------------- |
| afMode   | [FocusMode](#focusmode) | 是   | 指定的焦距模式。                    |

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| boolean    | 返回true表示支持该焦距模式，false表示不支持。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function isFocusModeSupported(captureSession: camera.CaptureSession): boolean {
  let status: boolean = false;
  try {
    status = captureSession.isFocusModeSupported(camera.FocusMode.FOCUS_MODE_AUTO);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The isFocusModeSupported call failed. error code: ${err.code}`);
  }
  return status;
}
```

### setFocusMode<sup>(deprecated)</sup>

setFocusMode(afMode: FocusMode): void

设置对焦模式。

进行设置之前，需要先检查设备是否支持指定的焦距模式，可使用方法[isFocusModeSupported](#isfocusmodesupporteddeprecated)。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Focus.setFocusMode](#setfocusmode11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                     | 必填 | 说明                 |
| -------- | ----------------------- | ---- | ------------------- |
| afMode   | [FocusMode](#focusmode) | 是   | 指定的焦距模式。       |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function setFocusMode(captureSession: camera.CaptureSession): void {
  try {
    captureSession.setFocusMode(camera.FocusMode.FOCUS_MODE_AUTO);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The setFocusMode call failed. error code: ${err.code}`);
  }
}
```

### getFocusMode<sup>(deprecated)</sup>

getFocusMode(): FocusMode

获取当前的对焦模式。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Focus.getFocusMode](#getfocusmode11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [FocusMode](#focusmode)   | 获取当前设备的焦距模式。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getFocusMode(captureSession: camera.CaptureSession): camera.FocusMode | undefined {
  let afMode: camera.FocusMode | undefined = undefined;
  try {
    afMode = captureSession.getFocusMode();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getFocusMode call failed. error code: ${err.code}`);
  }
  return afMode;
}
```

### setFocusPoint<sup>(deprecated)</sup>

setFocusPoint(point: Point): void

设置焦点，焦点应在0-1坐标系内，该坐标系左上角为{0，0}，右下角为{1，1}。
此坐标系是以设备充电口在右侧时的横向设备方向为基准的，例如应用的预览界面布局以
设备充电口在下侧时的竖向方向为基准，布局宽高为{w，h}，且触碰点为{x，y}，
则转换后的坐标点为{y/h，1-x/w}。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Focus.setFocusPoint](#setfocuspoint11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                     | 必填 | 说明                 |
| -------- | ----------------------- | ---- | ------------------- |
| Point    | [Point](#point)         | 是   | 焦点。x,y设置范围应在[0,1]之内，超过范围，如果小于0设置0，大于1设置1。   |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function setFocusPoint(captureSession: camera.CaptureSession): void {
  const focusPoint: camera.Point = {x: 1, y: 1};
  try {
    captureSession.setFocusPoint(focusPoint);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The setFocusPoint call failed. error code: ${err.code}`);
  }
}
```

### getFocusPoint<sup>(deprecated)</sup>

getFocusPoint(): Point

查询焦点。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Focus.getFocusPoint](#getfocuspoint11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [Point](#point)    | 用于获取当前焦点。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getFocusPoint(captureSession: camera.CaptureSession): camera.Point | undefined {
  let point: camera.Point | undefined = undefined;
  try {
    point = captureSession.getFocusPoint();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getFocusPoint call failed. error code: ${err.code}`);
  }
  return point;
}
```

### getFocalLength<sup>(deprecated)</sup>

getFocalLength(): number

查询焦距值。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Focus.getFocalLength](#getfocallength11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| number    | 用于获取当前焦距。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getFocalLength(captureSession: camera.CaptureSession): number {
  const invalidValue: number = -1;
  let focalLength: number = invalidValue;
  try {
    focalLength = captureSession.getFocalLength();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getFocalLength call failed. error code: ${err.code}`);
  }
  return focalLength;
}
```

### getZoomRatioRange<sup>(deprecated)</sup>

getZoomRatioRange(): Array\<number\>

获取支持的变焦范围。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Zoom.getZoomRatioRange](#getzoomratiorange11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| Array\<number\>   | 用于获取可变焦距比范围，返回的数组包括其最小值和最大值。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getZoomRatioRange(captureSession: camera.CaptureSession): Array<number> {
  let zoomRatioRange: Array<number> = [];
  try {
    zoomRatioRange = captureSession.getZoomRatioRange();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getZoomRatioRange call failed. error code: ${err.code}`);
  }
  return zoomRatioRange;
}
```

### setZoomRatio<sup>(deprecated)</sup>

setZoomRatio(zoomRatio: number): void

设置变焦比，变焦精度最高为小数点后两位，如果设置超过支持的精度范围，则只保留精度范围内数值。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Zoom.setZoomRatio](#setzoomratio11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名       | 类型                  | 必填 | 说明                 |
| --------- | -------------------- | ---- | ------------------- |
| zoomRatio | number               | 是   | 可变焦距比，通过getZoomRatioRange获取支持的变焦范围，如果设置超过支持范围的值，则只保留精度范围内数值。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function setZoomRatio(captureSession: camera.CaptureSession, zoomRatioRange: Array<number>): void {
  if (zoomRatioRange === undefined || zoomRatioRange.length <= 0) {
    return;
  }
  let zoomRatio = zoomRatioRange[0];
  try {
    captureSession.setZoomRatio(zoomRatio);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The setZoomRatio call failed. error code: ${err.code}`);
  }
}
```

### getZoomRatio<sup>(deprecated)</sup>

getZoomRatio(): number

获取当前的变焦比。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Zoom.getZoomRatio](#getzoomratio11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| number    | 获取当前的变焦比结果。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getZoomRatio(captureSession: camera.CaptureSession): number {
  const invalidValue: number = -1;
  let zoomRatio: number = invalidValue;
  try {
    zoomRatio = captureSession.getZoomRatio();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getZoomRatio call failed. error code: ${err.code}`);
  }
  return zoomRatio;
}
```

### isVideoStabilizationModeSupported<sup>(deprecated)</sup>

isVideoStabilizationModeSupported(vsMode: VideoStabilizationMode): boolean

查询是否支持指定的视频防抖模式。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Stabilization.isVideoStabilizationModeSupported](#isvideostabilizationmodesupported11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                                              | 必填 | 说明                             |
| -------- | ------------------------------------------------- | ---- | ------------------------------ |
| vsMode   | [VideoStabilizationMode](#videostabilizationmode) | 是   | 视频防抖模式。                    |

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| boolean    | 返回视频防抖模式是否支持，true表示支持，false表示不支持。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function isVideoStabilizationModeSupported(captureSession: camera.CaptureSession): boolean {
  let isSupported: boolean = false;
  try {
    isSupported = captureSession.isVideoStabilizationModeSupported(camera.VideoStabilizationMode.OFF);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The isVideoStabilizationModeSupported call failed. error code: ${err.code}`);
  }
  return isSupported;
}
```

### getActiveVideoStabilizationMode<sup>(deprecated)</sup>

getActiveVideoStabilizationMode(): VideoStabilizationMode

查询当前正在使用的视频防抖模式。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Stabilization.getActiveVideoStabilizationMode](#getactivevideostabilizationmode11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**返回值：**

| 类型        | 说明                          |
| ---------- | ----------------------------- |
| [VideoStabilizationMode](#videostabilizationmode)    | 视频防抖是否正在使用。接口调用失败会返回相应错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。 |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function getActiveVideoStabilizationMode(captureSession: camera.CaptureSession): camera.VideoStabilizationMode | undefined {
  let vsMode: camera.VideoStabilizationMode | undefined = undefined;
  try {
    vsMode = captureSession.getActiveVideoStabilizationMode();
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The getActiveVideoStabilizationMode call failed. error code: ${err.code}`);
  }
  return vsMode;
}
```

### setVideoStabilizationMode<sup>(deprecated)</sup>

setVideoStabilizationMode(mode: VideoStabilizationMode): void

设置视频防抖模式。需要先检查设备是否支持对应的防抖模式，可以通过[isVideoStabilizationModeSupported](#isvideostabilizationmodesupporteddeprecated)方法判断所设置的模式是否支持。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[Stabilization.setVideoStabilizationMode](#setvideostabilizationmode11)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名      | 类型                                              | 必填 | 说明                    |
| -------- | ------------------------------------------------- | ---- | --------------------- |
| mode     | [VideoStabilizationMode](#videostabilizationmode) | 是   | 需要设置的视频防抖模式。   |

**错误码：**

以下错误码的详细介绍请参见[Camera错误码](errorcode-camera.md)。

| 错误码ID         | 错误信息        |
| --------------- | --------------- |
| 7400103                |  Session not config.                                   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function setVideoStabilizationMode(captureSession: camera.CaptureSession): void {
  try {
    captureSession.setVideoStabilizationMode(camera.VideoStabilizationMode.OFF);
  } catch (error) {
    // 失败返回错误码error.code并处理
    let err = error as BusinessError;
    console.error(`The setVideoStabilizationMode call failed. error code: ${err.code}`);
  }
}
```

### on('focusStateChange')<sup>(deprecated)</sup>

on(type: 'focusStateChange', callback: AsyncCallback\<FocusState\>): void

监听相机聚焦的状态变化，通过注册回调函数获取结果。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[VideoSession.on('focusStateChange')](#onfocusstatechange11-1)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                                      | 必填 | 说明                       |
| -------- | ----------------------------------------- | ---- | ------------------------ |
| type     | string                                    | 是   | 监听事件，固定为'focusStateChange'，session 创建成功可监听。仅当自动对焦模式时,且相机对焦状态发生改变时可触发该事件。 |
| callback | AsyncCallback\<[FocusState](#focusstate)\> | 是   | 回调函数，用于获取当前对焦状态。  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function registerFocusStateChange(captureSession: camera.CaptureSession): void {
  captureSession.on('focusStateChange', (err: BusinessError, focusState: camera.FocusState) => {
    console.info(`Focus state: ${focusState}`);
  });
}
```

### off('focusStateChange')<sup>(deprecated)</sup>

off(type: 'focusStateChange', callback?: AsyncCallback\<FocusState\>): void

注销监听相机聚焦的状态变化。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[VideoSession.off('focusStateChange')](#offfocusstatechange11-1)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                                      | 必填 | 说明                       |
| -------- | ----------------------------------------- | ---- | ------------------------ |
| type     | string                                    | 是   | 监听事件，固定为'focusStateChange'，session 创建成功可监听。|
| callback | AsyncCallback\<[FocusState](#focusstate)\> | 否   | 回调函数，可选，有就是匹配on('focusStateChange') callback（callback对象不可是匿名函数）。  |

**示例：**

```ts
function unregisterFocusStateChange(captureSession: camera.CaptureSession): void {
  captureSession.off('focusStateChange');
}
```

### on('error')<sup>(deprecated)</sup>

on(type: 'error', callback: ErrorCallback): void

监听拍照会话的错误事件，通过注册回调函数获取结果。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[VideoSession.on('error')](#onerror11-1)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                                                                       | 必填 | 说明                           |
| -------- |--------------------------------------------------------------------------| ---- | ------------------------------ |
| type     | string                                                                   | 是   | 监听事件，固定为'error'，session创建成功之后可监听该接口。session调用相关接口出现错误时会触发该事件，比如调用[beginConfig](#beginconfigdeprecated)，[commitConfig](#commitconfigdeprecated-1)，[addInput](#addinputdeprecated)等接口发生错误时返回错误信息。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback) | 是   | 回调函数，用于获取错误信息。返回错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。        |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function registerCaptureSessionError(captureSession: camera.CaptureSession): void {
  captureSession.on('error', (error: BusinessError) => {
    console.error(`Capture session error code: ${error.code}`);
  });
}
```

### off('error')<sup>(deprecated)</sup>

off(type: 'error', callback?: ErrorCallback): void

注销监听拍照会话的错误事件，通过注册回调函数获取结果。

> **说明：**
>从 API version 10开始支持，从API version 11开始废弃。建议使用[VideoSession.off('error')](#offerror11-1)替代。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                                                          | 必填 | 说明                           |
| -------- | ----------------------------------------------------------- | ---- | ------------------------------ |
| type     | string                                                      | 是   | 监听事件，固定为'error'，session创建成功之后可监听该接口。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback)| 否   | 回调函数，可选，有就是匹配on('error') callback（callback对象不可是匿名函数）。       |

**示例：**

```ts
function unregisterCaptureSessionError(captureSession: camera.CaptureSession): void {
  captureSession.off('error');
}
```

## PhotoSession<sup>11+</sup>

PhotoSession extends Session, Flash, AutoExposure, Focus, Zoom

普通拍照模式会话类，继承自[Session](#session11)，用于设置普通拍照模式的参数以及保存所需要的所有资源[CameraInput](#camerainput)、[CameraOutput](#cameraoutput)。

### on('error')<sup>11+</sup>

on(type: 'error', callback: ErrorCallback): void

监听普通拍照会话的错误事件，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                                                          | 必填 | 说明                           |
| -------- | ----------------------------------------------------------- | ---- | ------------------------------ |
| type     | string                                                      | 是   | 监听事件，固定为'error'，session创建成功之后可监听该接口。session调用相关接口出现错误时会触发该事件，比如调用[beginConfig](#beginconfig11)，[commitConfig](#commitconfig11-1)，[addInput](#addinput11)等接口发生错误时返回错误信息。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback)| 是   | 回调函数，用于获取错误信息。返回错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。        |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function callback(err: BusinessError): void {
  console.error(`Photo session error code: ${err.code}`);
}

function registerSessionError(photoSession: camera.PhotoSession): void {
  photoSession.on('error', callback);
}
```

### off('error')<sup>11+</sup>

off(type: 'error', callback?: ErrorCallback): void

注销监听普通拍照会话的错误事件，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                            | 必填 | 说明                           |
| -------- | -------------------------------- | ---- | ------------------------------ |
| type     | string                           | 是   | 监听事件，固定为'error'，session创建成功之后可监听该接口。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback)| 否   | 回调函数，可选，有就是匹配on('error') callback（callback对象不可是匿名函数）。     |

**示例：**

```ts
function unregisterSessionError(photoSession: camera.PhotoSession): void {
  photoSession.off('error');
}
```

### on('focusStateChange')<sup>11+</sup>

on(type: 'focusStateChange', callback: AsyncCallback\<FocusState\>): void

监听相机聚焦的状态变化，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                    | 必填 | 说明                       |
| -------- | ---------------- | ---- | ------------------------ |
| type     | string                                    | 是   | 监听事件，固定为'focusStateChange'，session创建成功可监听。仅当自动对焦模式时，且相机对焦状态发生改变时可触发该事件。 |
| callback | AsyncCallback\<[FocusState](#focusstate)\> | 是   | 回调函数，用于获取当前对焦状态。  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function callback(err: BusinessError, focusState: camera.FocusState): void {
  console.info(`Focus state: ${focusState}`);
}

function registerFocusStateChange(photoSession: camera.PhotoSession): void {
  photoSession.on('focusStateChange', callback);
}
```

### off('focusStateChange')<sup>11+</sup>

off(type: 'focusStateChange', callback?: AsyncCallback\<FocusState\>): void

注销监听相机聚焦的状态变化。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                                      | 必填 | 说明                       |
| -------- | ----------------------------------------- | ---- | ------------------------ |
| type     | string                                    | 是   | 监听事件，固定为'focusStateChange'，session创建成功可监听。 |
| callback | AsyncCallback\<[FocusState](#focusstate)\> | 否   | 回调函数，可选，有就是匹配on('focusStateChange') callback（callback对象不可是匿名函数）。  |

**示例：**

```ts
function unregisterFocusStateChange(photoSession: camera.PhotoSession): void {
  photoSession.off('focusStateChange');
}
```

### on('smoothZoomInfoAvailable')<sup>11+</sup>

on(type: 'smoothZoomInfoAvailable', callback: AsyncCallback\<SmoothZoomInfo\>): void

监听相机平滑变焦的状态变化，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                   | 必填 | 说明                       |
| -------- | ----------------------- | ---- | ------------------------ |
| type     | string                  | 是   | 监听事件，固定为'smoothZoomInfoAvailable'，session创建成功可监听。|
| callback | AsyncCallback\<[SmoothZoomInfo](#smoothzoominfo11)\> | 是   | 回调函数，用于获取当前平滑变焦状态。  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function callback(err: BusinessError, smoothZoomInfo: camera.SmoothZoomInfo): void {
  console.info(`The duration of smooth zoom: ${smoothZoomInfo.duration}`);
}

function registerSmoothZoomInfo(photoSession: camera.PhotoSession): void {
  photoSession.on('smoothZoomInfoAvailable', callback);
}
```

### off('smoothZoomInfoAvailable')<sup>11+</sup>

off(type: 'smoothZoomInfoAvailable', callback?: AsyncCallback\<SmoothZoomInfo\>): void

注销监听相机平滑变焦的状态变化。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                                      | 必填 | 说明                       |
| -------- | ----------------------------------------- | ---- | ------------------------ |
| type     | string              | 是   | 监听事件，固定为'smoothZoomInfoAvailable'，session创建成功可监听。|
| callback | AsyncCallback\<[SmoothZoomInfo](#smoothzoominfo11)\> | 否   | 回调函数，可选，有就是匹配on('smoothZoomInfoAvailable') callback（callback对象不可是匿名函数）。  |

**示例：**

```ts
function unregisterSmoothZoomInfo(photoSession: camera.PhotoSession): void {
  photoSession.off('smoothZoomInfoAvailable');
}
```

## VideoSession<sup>11+</sup>

VideoSession extends Session, Flash, AutoExposure, Focus, Zoom, Stabilization

普通录像模式会话类，继承自[Session](#session11)，用于设置普通录像模式的参数以及保存所需要的所有资源[CameraInput](#camerainput)、[CameraOutput](#cameraoutput)。

### on('error')<sup>11+</sup>

on(type: 'error', callback: ErrorCallback): void

监听普通录像会话的错误事件，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型              | 必填 | 说明                           |
| -------- | ------------------ | ---- | ------------------------------ |
| type     | string             | 是   | 监听事件，固定为'error'，session创建成功之后可监听该接口。session调用相关接口出现错误时会触发该事件，比如调用[beginConfig](#beginconfig11)，[commitConfig](#commitconfig11-1)，[addInput](#addinput11)等接口发生错误时返回错误信息。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback)      | 是   | 回调函数，用于获取错误信息。返回错误码，错误码类型[CameraErrorCode](#cameraerrorcode)。   |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function callback(err: BusinessError): void {
  console.error(`Video session error code: ${err.code}`);
}

function registerSessionError(videoSession: camera.VideoSession): void {
  videoSession.on('error', callback);
}
```

### off('error')<sup>11+</sup>

off(type: 'error', callback?: ErrorCallback): void

注销监听普通录像会话的错误事件，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                          | 必填 | 说明                           |
| -------- | --------------------------- | ---- | ------------------------------ |
| type     | string                    | 是   | 监听事件，固定为'error'，session创建成功之后可监听该接口。 |
| callback | [ErrorCallback](../apis-basic-services-kit/js-apis-base.md#errorcallback)| 否   | 回调函数，可选，有就是匹配on('error') callback（callback对象不可是匿名函数）。      |

**示例：**

```ts
function unregisterSessionError(videoSession: camera.VideoSession): void {
  videoSession.off('error');
}
```

### on('focusStateChange')<sup>11+</sup>

on(type: 'focusStateChange', callback: AsyncCallback\<FocusState\>): void

监听相机聚焦的状态变化，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                    | 必填 | 说明                       |
| -------- | ---------------- | ---- | ------------------------ |
| type     | string                                    | 是   | 监听事件，固定为'focusStateChange'，session创建成功可监听。仅当自动对焦模式时，且相机对焦状态发生改变时可触发该事件。 |
| callback | AsyncCallback\<[FocusState](#focusstate)\> | 是   | 回调函数，用于获取当前对焦状态。  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function callback(err: BusinessError, focusState: camera.FocusState): void {
  console.info(`Focus state: ${focusState}`);
}

function registerFocusStateChange(videoSession: camera.VideoSession): void {
  videoSession.on('focusStateChange', callback);
}
```

### off('focusStateChange')<sup>11+</sup>

off(type: 'focusStateChange', callback?: AsyncCallback\<FocusState\>): void

注销监听相机聚焦的状态变化。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                                      | 必填 | 说明                       |
| -------- | ----------------------------------------- | ---- | ------------------------ |
| type     | string                                    | 是   | 监听事件，固定为'focusStateChange'，session创建成功可监听。 |
| callback | AsyncCallback\<[FocusState](#focusstate)\> | 否  | 回调函数，可选，有就是匹配on('focusStateChange') callback（callback对象不可是匿名函数）。  |

**示例：**

```ts
function unregisterFocusStateChange(videoSession: camera.VideoSession): void {
  videoSession.off('focusStateChange');
}
```

### on('smoothZoomInfoAvailable')<sup>11+</sup>

on(type: 'smoothZoomInfoAvailable', callback: AsyncCallback\<SmoothZoomInfo\>): void

监听相机平滑变焦的状态变化，通过注册回调函数获取结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                   | 必填 | 说明                       |
| -------- | ----------------------- | ---- | ------------------------ |
| type     | string                  | 是   | 监听事件，固定为'smoothZoomInfoAvailable'，session创建成功可监听。|
| callback | AsyncCallback\<[SmoothZoomInfo](#smoothzoominfo11)\> | 是   | 回调函数，用于获取当前平滑变焦状态。  |

**示例：**

```ts
import { BusinessError } from '@ohos.base';

function callback(err: BusinessError, smoothZoomInfo: camera.SmoothZoomInfo): void {
  console.info(`The duration of smooth zoom: ${smoothZoomInfo.duration}`);
}

function registerSmoothZoomInfo(videoSession: camera.VideoSession): void {
  videoSession.on('smoothZoomInfoAvailable', callback);
}
```

### off('smoothZoomInfoAvailable')<sup>11+</sup>

off(type: 'smoothZoomInfoAvailable', callback?: AsyncCallback\<SmoothZoomInfo\>): void

注销监听相机平滑变焦的状态变化。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**参数：**

| 参数名     | 类型                                      | 必填 | 说明                       |
| -------- | ----------------------------------------- | ---- | ------------------------ |
| type     | string              | 是   | 监听事件，固定为'smoothZoomInfoAvailable'，session创建成功可监听。|
| callback | AsyncCallback\<[SmoothZoomInfo](#smoothzoominfo11)\> | 否   | 回调函数，可选，有就是匹配on('smoothZoomInfoAvailable') callback（callback对象不可是匿名函数）。  |

**示例：**

```ts
function unregisterSmoothZoomInfo(videoSession: camera.VideoSession): void {
  videoSession.off('smoothZoomInfoAvailable');
}
```
