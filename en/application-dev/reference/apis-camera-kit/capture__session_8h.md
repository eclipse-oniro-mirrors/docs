# capture_session.h


## Overview

The **capture_session.h** file declares the session capture concepts.

**Library**: libohcamera.so

**System capability**: SystemCapability.Multimedia.Camera.Core

**Since**: 11

**Related module**: [OH_Camera](_o_h___camera.md)


## Summary


### Structs

| Name| Description| 
| -------- | -------- |
| struct&nbsp;&nbsp;[CaptureSession_Callbacks](_capture_session___callbacks.md) | Defines the callbacks used for session capture. | 


### Types

| Name| Description| 
| -------- | -------- |
| typedef struct [Camera_CaptureSession](_o_h___camera.md#camera_capturesession) [Camera_CaptureSession](_o_h___camera.md#camera_capturesession) | Defines the session capture object. | 
| typedef void(\* [OH_CaptureSession_OnFocusStateChange](_o_h___camera.md#oh_capturesession_onfocusstatechange)) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_FocusState](_o_h___camera.md#camera_focusstate) focusState) | Defines the pointer to the callback defined in the [CaptureSession_Callbacks](_capture_session___callbacks.md) struct and used to report session capture focus status changes. | 
| typedef void(\* [OH_CaptureSession_OnError](_o_h___camera.md#oh_capturesession_onerror)) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) errorCode) | Defines the pointer to the callback defined in the [CaptureSession_Callbacks](_capture_session___callbacks.md) struct and used to report capture session errors. | 
| typedef struct [CaptureSession_Callbacks](_capture_session___callbacks.md) [CaptureSession_Callbacks](_o_h___camera.md#capturesession_callbacks) | Defines the callbacks used for session capture. | 


### Functions

| Name| Description| 
| -------- | -------- |
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_RegisterCallback](_o_h___camera.md#oh_capturesession_registercallback) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [CaptureSession_Callbacks](_capture_session___callbacks.md) \*callback) | Registers a callback to listen for session capture events. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_UnregisterCallback](_o_h___camera.md#oh_capturesession_unregistercallback) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [CaptureSession_Callbacks](_capture_session___callbacks.md) \*callback) | Unregisters the callback used to listen for session capture events. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_BeginConfig](_o_h___camera.md#oh_capturesession_beginconfig) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session) | Starts the configuration for session capture. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_CommitConfig](_o_h___camera.md#oh_capturesession_commitconfig) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session) | Commits the configuration for session capture. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_AddInput](_o_h___camera.md#oh_capturesession_addinput) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_Input](_o_h___camera.md#camera_input) \*cameraInput) | Adds a **CameraInput** instance to a session. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_RemoveInput](_o_h___camera.md#oh_capturesession_removeinput) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_Input](_o_h___camera.md#camera_input) \*cameraInput) | Removes a **CameraInput** instance from a session. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_AddPreviewOutput](_o_h___camera.md#oh_capturesession_addpreviewoutput) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_PreviewOutput](_o_h___camera.md#camera_previewoutput) \*previewOutput) | Adds a **PreviewOutput** instance to a session. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_RemovePreviewOutput](_o_h___camera.md#oh_capturesession_removepreviewoutput) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_PreviewOutput](_o_h___camera.md#camera_previewoutput) \*previewOutput) | Removes a **PreviewOutput** instance from a session. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_AddPhotoOutput](_o_h___camera.md#oh_capturesession_addphotooutput) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_PhotoOutput](_o_h___camera.md#camera_photooutput) \*photoOutput) | Adds a **PhotoOutput** instance to a session. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_RemovePhotoOutput](_o_h___camera.md#oh_capturesession_removephotooutput) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_PhotoOutput](_o_h___camera.md#camera_photooutput) \*photoOutput) | Removes a **PhotoOutput** instance from a session. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_AddVideoOutput](_o_h___camera.md#oh_capturesession_addvideooutput) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_VideoOutput](_o_h___camera.md#camera_videooutput) \*videoOutput) | Adds a **VideoOutput** instance to a session. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_RemoveVideoOutput](_o_h___camera.md#oh_capturesession_removevideooutput) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_VideoOutput](_o_h___camera.md#camera_videooutput) \*videoOutput) | Removes a **VideoOutput** instance from a session. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_AddMetadataOutput](_o_h___camera.md#oh_capturesession_addmetadataoutput) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_MetadataOutput](_o_h___camera.md#camera_metadataoutput) \*metadataOutput) | Adds a **MetadataOutput** instance to a session. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_RemoveMetadataOutput](_o_h___camera.md#oh_capturesession_removemetadataoutput) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_MetadataOutput](_o_h___camera.md#camera_metadataoutput) \*metadataOutput) | Removes a **MetadataOutput** instance from a session. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_Start](_o_h___camera.md#oh_capturesession_start) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session) | Starts session capture. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_Stop](_o_h___camera.md#oh_capturesession_stop) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session) | Stops session capture. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_Release](_o_h___camera.md#oh_capturesession_release) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session) | Releases a **CaptureSession** instance. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_HasFlash](_o_h___camera.md#oh_capturesession_hasflash) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, bool \*hasFlash) | Checks whether the device has flash. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_IsFlashModeSupported](_o_h___camera.md#oh_capturesession_isflashmodesupported) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_FlashMode](_o_h___camera.md#camera_flashmode) flashMode, bool \*isSupported) | Checks whether a flash mode is supported. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_GetFlashMode](_o_h___camera.md#oh_capturesession_getflashmode) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_FlashMode](_o_h___camera.md#camera_flashmode) \*flashMode) | Obtains the flash mode in use. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_SetFlashMode](_o_h___camera.md#oh_capturesession_setflashmode) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_FlashMode](_o_h___camera.md#camera_flashmode) flashMode) | Sets a flash mode for the device. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_IsExposureModeSupported](_o_h___camera.md#oh_capturesession_isexposuremodesupported) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_ExposureMode](_o_h___camera.md#camera_exposuremode) exposureMode, bool \*isSupported) | Checks whether an exposure mode is supported. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_GetExposureMode](_o_h___camera.md#oh_capturesession_getexposuremode) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_ExposureMode](_o_h___camera.md#camera_exposuremode) \*exposureMode) | Obtains the exposure mode in use. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_SetExposureMode](_o_h___camera.md#oh_capturesession_setexposuremode) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_ExposureMode](_o_h___camera.md#camera_exposuremode) exposureMode) | Sets an exposure mode for the device. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_GetMeteringPoint](_o_h___camera.md#oh_capturesession_getmeteringpoint) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_Point](_camera___point.md) \*point) | Obtains the metering point in use. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_SetMeteringPoint](_o_h___camera.md#oh_capturesession_setmeteringpoint) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_Point](_camera___point.md) point) | Sets the metering point, which is the center point of the metering rectangle. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_GetExposureBiasRange](_o_h___camera.md#oh_capturesession_getexposurebiasrange) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, float \*minExposureBias, float \*maxExposureBias, float \*step) | Obtains the exposure compensation values of the device. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_SetExposureBias](_o_h___camera.md#oh_capturesession_setexposurebias) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, float exposureBias) | Sets an exposure compensation value for the device. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_GetExposureBias](_o_h___camera.md#oh_capturesession_getexposurebias) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, float \*exposureBias) | Obtains the exposure compensation value in use. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_IsFocusModeSupported](_o_h___camera.md#oh_capturesession_isfocusmodesupported) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_FocusMode](_o_h___camera.md#camera_focusmode) focusMode, bool \*isSupported) | Checks whether a focus mode is supported. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_GetFocusMode](_o_h___camera.md#oh_capturesession_getfocusmode) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_FocusMode](_o_h___camera.md#camera_focusmode) \*focusMode) | Obtains the focus mode in use. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_SetFocusMode](_o_h___camera.md#oh_capturesession_setfocusmode) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_FocusMode](_o_h___camera.md#camera_focusmode) focusMode) | Sets a focus mode for the device. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_GetFocusPoint](_o_h___camera.md#oh_capturesession_getfocuspoint) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_Point](_camera___point.md) \*focusPoint) | Obtains the focal point in use. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_SetFocusPoint](_o_h___camera.md#oh_capturesession_setfocuspoint) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_Point](_camera___point.md) focusPoint) | Sets a focal point for the device. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_GetZoomRatioRange](_o_h___camera.md#oh_capturesession_getzoomratiorange) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, float \*minZoom, float \*maxZoom) | Obtains the supported zoom ratio range. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_GetZoomRatio](_o_h___camera.md#oh_capturesession_getzoomratio) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, float \*zoom) | Obtains the zoom ratio in use. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_SetZoomRatio](_o_h___camera.md#oh_capturesession_setzoomratio) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, float zoom) | Sets a zoom ratio for the device. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_IsVideoStabilizationModeSupported](_o_h___camera.md#oh_capturesession_isvideostabilizationmodesupported) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_VideoStabilizationMode](_o_h___camera.md#camera_videostabilizationmode) mode, bool \*isSupported) | Checks whether a video stabilization mode is supported.  | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_GetVideoStabilizationMode](_o_h___camera.md#oh_capturesession_getvideostabilizationmode) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_VideoStabilizationMode](_o_h___camera.md#camera_videostabilizationmode) \*mode) | Obtains the video stabilization mode in use. | 
| [Camera_ErrorCode](_o_h___camera.md#camera_errorcode) [OH_CaptureSession_SetVideoStabilizationMode](_o_h___camera.md#oh_capturesession_setvideostabilizationmode) ([Camera_CaptureSession](_o_h___camera.md#camera_capturesession) \*session, [Camera_VideoStabilizationMode](_o_h___camera.md#camera_videostabilizationmode) mode) | Sets a video stabilization mode for the device. | 
