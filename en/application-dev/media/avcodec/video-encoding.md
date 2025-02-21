# Video Encoding

You can call the native APIs provided by the VideoEncoder module to encode a video, that is, to compress video data into a video stream.

Currently, the following encoding capabilities are supported:

| Container Specification| Video Encoding Type                |
| -------- | ---------------------------- |
| mp4      | HEVC (H.265) and AVC (H.264)|
| m4a      | HEVC (H.265) and AVC (H.264)|

Currently, only hardware encoding is supported. When an encoder is created based on the MIME type, H.264 (OH_AVCODEC_MIMETYPE_VIDEO_AVC) and H.265 (OH_AVCODEC_MIMETYPE_VIDEO_HEVC) are supported.

## Surface Input and Buffer Input

Surface input and buffer input differ in data sources.

Surface input indicates that the OHNativeWindow is used to transfer passed-in data. It supports connection with other modules, such as the camera module.

Buffer input refers to a pre-allocated memory area. The caller needs to copy original data to this memory area. It is more applicable to scenarios such as reading video data from files.

The two also differ slightly in the API calling modes:

- In buffer mode, an application calls **OH_VideoEncoder_PushInputBuffer()** to input data. In surface mode, an application, before the encoder is ready, calls **OH_VideoEncoder_GetSurface()** to obtain the OHNativeWindow for video data transmission.
- In buffer mode, an application calls **OH_VideoEncoder_PushInputBuffer()** to pass in the End of Stream (EOS) flag, and the encoder stops when it reads the last frame. In surface mode, an application calls **OH_VideoEncoder_NotifyEndOfStream()** to notify the encoder of EOS.

For details about the development procedure, see [Surface Input](#surface-input) and [Buffer Input](#buffer-input).

## How to Develop

Read [VideoEncoder](../../reference/apis-avcodec-kit/_video_encoder.md) for the API reference.

The figure below shows the call relationship of video encoding.

![Call relationship of video encoding](figures/video-encode.png)

### Linking the Dynamic Library in the CMake Script

```cmake
target_link_libraries(sample PUBLIC libnative_media_codecbase.so)
target_link_libraries(sample PUBLIC libnative_media_core.so)
target_link_libraries(sample PUBLIC libnative_media_venc.so)
```

### Surface Input

The following walks you through how to implement the entire video encoding process in surface mode. In this example, surface data is input and encoded into a H.264 stream.

Currently, the VideoEncoder module supports only data rotation in asynchronous mode.

1. Add the header files.

    ```cpp
    #include <multimedia/player_framework/native_avcodec_videoencoder.h>
    #include <multimedia/player_framework/native_avcapability.h>
    #include <multimedia/player_framework/native_avcodec_base.h>
    #include <multimedia/player_framework/native_avformat.h>
    #include <multimedia/player_framework/native_avbuffer.h>
    ```

2. Create an encoder instance.

    You can create an encoder by name or MIME type. In the code snippet below, the following variables are used:

    - **videoEnc**: pointer to the video encoder instance.
    - **capability**: pointer to the encoder's capability.
    - **OH_AVCODEC_MIMETYPE_VIDEO_AVC**: name of an AVC video stream.

    ```c++
    // To create an encoder by name, call OH_AVCapability_GetName to obtain the codec names available and then call OH_VideoEncoder_CreateByName. If your application has special requirements, for example, expecting an encoder that supports a certain resolution, you can call OH_AVCodec_GetCapability to query the capability first.
    OH_AVCapability *capability = OH_AVCodec_GetCapability(OH_AVCODEC_MIMETYPE_VIDEO_AVC, true);
    const char *codecName = OH_AVCapability_GetName(capability);
    OH_AVCodec *videoEnc = OH_VideoEncoder_CreateByName(codecName);
    ```

    ```c++
    // To create an encoder by MIME type, call OH_VideoEncoder_CreateByMime. The system creates the most appropriate encoder based on the MIME type.
    OH_AVCodec *videoEnc = OH_VideoEncoder_CreateByMime(OH_AVCODEC_MIMETYPE_VIDEO_AVC);
    ```

3. Call **OH_VideoEncoder_RegisterCallback()** to register the callback functions.

    > **NOTE**
    >
    > In the callback functions, pay attention to multi-thread synchronization for operations on the data queue.
    >

    Register the **OH_AVCodecCallback** struct that defines the following callback function pointers:

    - **OH_AVCodecOnError**, a callback used to report a codec operation error.
    - **OH_AVCodecOnStreamChanged**, a callback used to report a codec stream change, for example, format change.
    - **OH_AVCodecOnNeedInputBuffer**, a callback used to report input data required. This callback does not take effect, since you input data through the obtained surface.
    - **OH_AVCodecOnNewOutputBuffer**, a callback used to report output data generated, which means that encoding is complete.

    ```c++
    // Set the OH_AVCodecOnError callback function.
    static void OnError(OH_AVCodec *codec, int32_t errorCode, void *userData)
    {
        (void)codec;
        (void)errorCode;
        (void)userData;
    }

    // Set the OH_AVCodecOnStreamChanged callback function.
    static void OnStreamChanged(OH_AVCodec *codec, OH_AVFormat *format, void *userData)
    {
        (void)codec;
        (void)format;
        (void)userData;
    }

    // Set the OH_AVCodecOnNeedInputBuffer callback function, which is used to send an input frame to the data queue.
    static void OnNeedInputBuffer(OH_AVCodec *codec, uint32_t index, OH_AVBuffer *buffer, void *userData)
    {
        (void)userData;
        (void)index;
        (void)buffer;
        // In surface mode, this callback function does not take effect. You can input data by using the obtained surface.
    }

    // Set the OH_AVCodecOnNewOutputBuffer callback function, which is used to send an encoded frame to the output queue.
    static void OnNewOutputBuffer(OH_AVCodec *codec, uint32_t index, OH_AVBuffer *buffer, void *userData)
    {
        // The index of the output frame buffer is sent to outIndexQueue.
        // The encoded frame data (specified by buffer) is sent to outBufferQueue.
        // Perform data processing. For details, see
        // - Release the encoded frame.
    }

    // Call OH_VideoEncoder_SetCallback() to set the callback functions.
    OH_AVCodecCallback cb = {&OnError, &OnStreamChanged, &OnNeedInputBuffer, &OnNewOutputBuffer};
    int32_t ret = OH_VideoEncoder_RegisterCallback(videoEnc, cb, NULL);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    ```

4. Call **OH_VideoEncoder_Configure()** to configure the encoder.

    For details about the configurable options, see [Variables](../../reference/apis-avcodec-kit/_codec_base.md#variables).

    Currently, the following options must be configured for all supported formats: video frame width, video frame height, and video color format. In the code snippet below, the following variables are used:

    - **DEFAULT_WIDTH**: 320 pixels
    - **DEFAULT_HEIGHT**: 240 pixels
    - **DEFAULT_PIXELFORMAT**: **AV_PIXEL_FORMAT_NV12** (the color format of the YUV file is NV12)

    ```c++
    // (Mandatory) Configure the video frame width.
    constexpr uint32_t DEFAULT_WIDTH = 320; 
    // (Mandatory) Configure the video frame height.
    constexpr uint32_t DEFAULT_HEIGHT = 240;
    // (Mandatory) Configure the video color format.
    constexpr OH_AVPixelFormat DEFAULT_PIXELFORMAT = AV_PIXEL_FORMAT_NV12;
    // Configure the video frame rate.
    double frameRate = 30.0;
    // Configure the video YUV range flag.
    bool rangeFlag = false;
    // Configure the video primary color.
    int32_t primary = static_cast<int32_t>(OH_ColorPrimary::COLOR_PRIMARY_BT709);
    // Configure the transfer features.
    int32_t transfer = static_cast<int32_t>(OH_TransferCharacteristic::TRANSFER_CHARACTERISTIC_BT709);
    // Configure the maximum matrix coefficient.
    int32_t matrix = static_cast<int32_t>(OH_MatrixCoefficient::MATRIX_COEFFICIENT_IDENTITY);
    // Configure the encoding profile.
    int32_t profile = static_cast<int32_t>(OH_AVCProfile::AVC_PROFILE_BASELINE);
    // Configure the encoding bit rate mode.
    int32_t rateMode = static_cast<int32_t>(OH_VideoEncodeBitrateMode::CBR);
    // Configure the key frame interval, in milliseconds.
    int32_t iFrameInterval = 23000;
    // Configure the required encoding quality. Only an encoder in constant quality mode supports this configuration.
    int32_t quality = 0;
    // Configure the bit rate.
    int64_t bitRate = 3000000;

    OH_AVFormat *format = OH_AVFormat_Create();
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_WIDTH, DEFAULT_WIDTH);
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_HEIGHT, DEFAULT_HEIGHT);
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_PIXEL_FORMAT, DEFAULT_PIXELFORMAT);

    OH_AVFormat_SetDoubleValue(format, OH_MD_KEY_FRAME_RATE, frameRate);
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_RANGE_FLAG, rangeFlag);
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_COLOR_PRIMARIES, primary);
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_TRANSFER_CHARACTERISTICS, transfer);
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_MATRIX_COEFFICIENTS, matrix);
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_I_FRAME_INTERVAL, iFrameInterval);
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_PROFILE, profile);
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_VIDEO_ENCODE_BITRATE_MODE, rateMode);
    OH_AVFormat_SetLongValue(format, OH_MD_KEY_BITRATE, bitRate);
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_QUALITY, quality);
    int32_t ret = OH_VideoEncoder_Configure(videoEnc, format);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    OH_AVFormat_Destroy(format);
    ```

5. Call **OH_VideoEncoder_Prepare()** to prepare internal resources for the encoder.  

   ```c++
ret = OH_VideoEncoder_Prepare(videoEnc);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    ```
    
6. Obtain a surface.

    Obtain the OHNativeWindow in surface mode. The surface must be obtained before the encoder starts.

    ```c++
    int32_t ret;
    // Obtain the surface used for data input.
    OHNativeWindow *nativeWindow;
    ret = OH_VideoEncoder_GetSurface(videoEnc, &nativeWindow);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    // Configure the surface of the input data through the OHNativeWindow* variable type.
    ```

    For details about how to use the **OHNativeWindow*** variable type, see [OHNativeWindow](../../reference/apis-arkgraphics2d/_native_window.md#ohnativewindow).

7. Call **OH_VideoEncoder_Start()** to start the encoder.

    ```c++
    int32_t ret;
    // Start the encoder.
    ret = OH_VideoEncoder_Start(videoEnc);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    ```

8. (Optional) Dynamically configure encoder parameters during running.

    ```c++
    OH_AVFormat *format = OH_AVFormat_Create();
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_REQUEST_I_FRAME, true); // Currently, dynamically requesting for IDR frames is supported only.
    int32_t ret = OH_VideoEncoder_SetParameter(videoEnc, format);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    ```

9. Write the stream to encode.
   
   In step 6, you have configured the **OHNativeWindow*** variable type returned by **OH_VideoEncoder_GetSurface**. The data required for encoding is continuously input by the surface. Therefore, you do not need to process the **OnNeedInputBuffer** callback function or use **OH_VideoEncoder_PushInputBuffer** to input data.

10. Call **OH_VideoEncoder_NotifyEndOfStream()** to notify the encoder of EOS.

    ```c++
    int32_t ret;
    // In surface mode, you only need to call this API to notify the encoder of EOS.
    // In buffer mode, you need to set the AVCODEC_BUFFER_FLAGS_EOS flag and then call OH_VideoEncoder_PushInputBuffer to notify the encoder of EOS.
    ret = OH_VideoEncoder_NotifyEndOfStream(videoEnc);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    ```

11. Call **OH_VideoEncoder_FreeOutputBuffer()** to release encoded frames.

    In the code snippet below, the following variables are used:

    - **index**: index of the data queue, which is passed in by the callback function **OnNewOutputBuffer**.
    - **buffer**: parameter passed in by the callback function **OnNewOutputBuffer**. You can call **OH_AVBuffer_GetAddr()** to obtain the pointer to the shared memory address.

    ```c++
    int32_t ret;
    // Obtain the encoded information.
    OH_AVCodecBufferAttr info;
    ret = OH_AVBuffer_GetBufferAttr(buffer, &info);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    // Write the encoded frame data (specified by buffer) to the output file.
    outputFile->write(reinterpret_cast<char *>(OH_AVBuffer_GetAddr(buffer)), info.size);
    // Free the output buffer. index is the index of the buffer.
    ret = OH_VideoEncoder_FreeOutputBuffer(videoEnc, index);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    ```

12. (Optional) Call **OH_VideoEncoder_Flush()** to refresh the encoder.

    After **OH_VideoEncoder_Flush()** is called, the encoder remains in the running state, but the current queue is cleared and the buffer storing the encoded data is freed.

    To continue encoding, you must call **OH_VideoEncoder_Start()** again.

    ```c++
    int32_t ret;
    // Refresh the encoder.
    ret = OH_VideoEncoder_Flush(videoEnc);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    // Start encoding again.
    ret = OH_VideoEncoder_Start(videoEnc);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    ```

13. (Optional) Call **OH_VideoEncoder_Reset()** to reset the encoder.

    After **OH_VideoEncoder_Reset()** is called, the encoder returns to the initialized state. To continue encoding, you must call **OH_VideoEncoder_Configure()** and then **OH_VideoEncoder_Start()**.

    ```c++
    int32_t ret;
    // Reset the encoder.
    ret = OH_VideoEncoder_Reset(videoEnc);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    // Reconfigure the encoder.
    ret = OH_VideoEncoder_Configure(videoEnc, format);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    ```

14. (Optional) Call **OH_VideoEncoder_Stop()** to stop the encoder.

    ```c++
    int32_t ret;
    // Stop the encoder.
    ret = OH_VideoEncoder_Stop(videoEnc);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    ```

15. Call **OH_VideoEncoder_Destroy()** to destroy the encoder instance and release resources.

    > **NOTE**
    >
    > This API cannot be called in the callback function.
    > After the call, you must set a null pointer to the encoder to prevent program errors caused by wild pointers.
    >

    ```c++
    int32_t ret;
    // Call OH_VideoEncoder_Destroy to destroy the encoder.
    ret = OH_VideoEncoder_Destroy(videoEnc);
    videoEnc = nullptr;
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    ```

### Buffer Input

The following walks you through how to implement the entire video encoding process in buffer mode. It uses the YUV file input and H.264 encoding format as an example.

Currently, the VideoEncoder module supports only data rotation in asynchronous mode.

1. Add the header files.

    ```cpp
    #include <multimedia/player_framework/native_avcodec_videoencoder.h>
    #include <multimedia/player_framework/native_avcapability.h>
    #include <multimedia/player_framework/native_avcodec_base.h>
    #include <multimedia/player_framework/native_avformat.h>
    #include <multimedia/player_framework/native_avbuffer.h>
    ```

2. Create an encoder instance.

    The procedure is the same as that in surface mode and is not described here.

    ```c++
    // To create an encoder by name, call OH_AVCapability_GetName to obtain the codec names available and then call OH_VideoEncoder_CreateByName. If your application has special requirements, for example, expecting an encoder that supports a certain resolution, you can call OH_AVCodec_GetCapability to query the capability first.
    OH_AVCapability *capability = OH_AVCodec_GetCapability(OH_AVCODEC_MIMETYPE_VIDEO_AVC, true);
    const char *codecName = OH_AVCapability_GetName(capability);
    OH_AVCodec *videoEnc = OH_VideoEncoder_CreateByName(codecName);
    ```

    ```c++
    // To create an encoder by MIME type, call OH_VideoEncoder_CreateByMime. The system creates the most appropriate encoder based on the MIME type.
    OH_AVCodec *videoEnc = OH_VideoEncoder_CreateByMime(OH_AVCODEC_MIMETYPE_VIDEO_AVC);
    ```

3. Call **OH_VideoEncoder_RegisterCallback()** to register the callback functions.

    > **NOTE**
    >
    > In the callback functions, pay attention to multi-thread synchronization for operations on the data queue.
    >

    Register the **OH_AVCodecCallback** struct that defines the following callback function pointers:

    - **OH_AVCodecOnError**, a callback used to report a codec operation error.
    - **OH_AVCodecOnStreamChanged**, a callback used to report a codec stream change, for example, format change.
    - **OH_AVCodecOnNeedInputBuffer**, a callback used to report input data required, which means that the encoder is ready for receiving YUV/RGB data.
    - **OH_AVCodecOnNewOutputBuffer**, a callback used to report output data generated, which means that encoding is complete.

    You need to process the callback functions to ensure that the encoder runs properly.

    ```c++
    // Implement the OH_AVCodecOnError callback function.
    static void OnError(OH_AVCodec *codec, int32_t errorCode, void *userData)
    {
        (void)codec;
        (void)errorCode;
        (void)userData;
    }

    // Implement the OH_AVCodecOnStreamChanged callback function.
    static void OnStreamChanged(OH_AVCodec *codec, OH_AVFormat *format, void *userData)
    {
        (void)codec;
        (void)format;
        (void)userData;
    }

    // Implement the OH_AVCodecOnNeedInputBuffer callback function.
    static void OnNeedInputBuffer(OH_AVCodec *codec, uint32_t index, OH_AVBuffer *buffer, void *userData)
    {
        // The index of the input frame buffer is sent to InIndexQueue.
        // The input frame data (specified by buffer) is sent to InBufferQueue.
        // Perform data processing. For details, see
        // - Write the stream to encode.
        // - Notify the encoder of EOS.
    }

    // Implement the OH_AVCodecOnNewOutputBuffer callback function.
    static void OnNewOutputBuffer(OH_AVCodec *codec, uint32_t index, OH_AVBuffer *buffer, void *userData)
    {
        // The index of the output frame buffer is sent to outIndexQueue.
        // The encoded frame data (specified by buffer) is sent to outBufferQueue.
        // Perform data processing. For details, see
        // - Release the encoded frame.
    }

    // Call OH_VideoEncoder_RegisterCallback() to register the callback functions.
    OH_AVCodecCallback cb = {&OnError, &OnStreamChanged, &OnNeedInputBuffer, &OnNewOutputBuffer};
    int32_t ret = OH_VideoEncoder_RegisterCallback(videoEnc, cb, NULL);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    ```

4. Call **OH_VideoEncoder_Configure()** to configure the encoder.

    The procedure is the same as that in surface mode and is not described here.

    ```c++
    // (Mandatory) Configure the video frame width.
    constexpr uint32_t DEFAULT_WIDTH = 320; 
    // (Mandatory) Configure the video frame height.
    constexpr uint32_t DEFAULT_HEIGHT = 240;
    // (Mandatory) Configure the video color format.
    constexpr OH_AVPixelFormat DEFAULT_PIXELFORMAT = AV_PIXEL_FORMAT_NV12;
    
    OH_AVFormat *format = OH_AVFormat_Create();
    // Set the format.
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_WIDTH, DEFAULT_WIDTH);
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_HEIGHT, DEFAULT_HEIGHT);
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_PIXEL_FORMAT, DEFAULT_PIXELFORMAT);
    // Configure the encoder.
    int32_t ret = OH_VideoEncoder_Configure(videoEnc, format);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
        OH_AVFormat_Destroy(format);
    ```

5. Call **OH_VideoEncoder_Prepare()** to prepare internal resources for the encoder.  

   ```c++
ret = OH_VideoEncoder_Prepare(videoEnc);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    ```
    
6. Call **OH_VideoEncoder_Start()** to start the encoder.

    As soon as the encoder starts, the callback functions will be triggered to respond to events. Therefore, you must configure the input file and output file first.

    ```c++
    // Configure the paths of the input and output files.
    std::string_view inputFilePath = "/*yourpath*.yuv";
    std::string_view outputFilePath = "/*yourpath*.h264";
    std::unique_ptr<std::ifstream> inputFile = std::make_unique<std::ifstream>();
    std::unique_ptr<std::ofstream> outputFile = std::make_unique<std::ofstream>();
    inputFile->open(inputFilePath.data(), std::ios::in | std::ios::binary);
    outputFile->open(outputFilePath.data(), std::ios::out | std::ios::binary | std::ios::ate);
    // Start the encoder.
    int32_t ret = OH_VideoEncoder_Start(videoEnc);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    ```

7. (Optional) Dynamically configure encoder parameters during running.

    ```c++
    OH_AVFormat *format = OH_AVFormat_Create();
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_REQUEST_I_FRAME, true); // Currently, dynamically requesting for IDR frames is supported only.
    int32_t ret = OH_VideoEncoder_SetParameter(videoEnc, format);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    ```

8. Call **OH_VideoEncoder_PushInputBuffer()** to push the stream to the input queue for encoding.

    In the code snippet below, the following variables are used:

    - **buffer**: parameter passed in by the callback function **OnNeedInputBuffer**. You can call **OH_AVBuffer_GetAddr()** to obtain the pointer to the shared memory address.
    - **index**: index of the data queue, which is passed in by the callback function **OnNeedInputBuffer**.
    - **flags**: type of the buffer flag. For details, see [OH_AVCodecBufferFlags](../../reference/apis-avcodec-kit/_core.md#oh_avcodecbufferflags).
    - **stride**: stride of the obtained buffer data.

    ```c++
        if (stride == DEFAULT_WIDTH) {
            // Process the file stream and obtain the frame length, and then write the data to encode to the buffer of the specified index.
            int32_t frameSize = DEFAULT_WIDTH * DEFAULT_HEIGHT * 3 / 2; // Formula for calculating the data size of each frame in NV12 color format.
            inputFile->read(reinterpret_cast<char *>(OH_AVBuffer_GetAddr(buffer)), frameSize);
        } else {
            // If the stride is not equal to the width, you need to perform the offset based on the stride.
        }
        // Configure the buffer information.
        OH_AVCodecBufferAttr info;
        info.size = frameSize;
        info.offset = 0;
        info.pts = 0;
        info.flags = flags;
        ret = OH_AVBuffer_SetBufferAttr(buffer, &info);
        if (ret != AV_ERR_OK) {
            // Exception handling.
        }
        // Send the data to the input buffer for encoding. index is the index of the buffer.
        int32_t ret = OH_VideoEncoder_PushInputBuffer(videoEnc, index);
        if (ret != AV_ERR_OK) {
            // Exception handling.
        }
    ```

    When processing the buffer data (before pushing the data) during hardware encoding, the system must obtain the width, height, and stride of the data to ensure correct processing of the data to encode. For details, see [OH_NativeBuffer](../../reference/apis-arkgraphics2d/_o_h___native_buffer.md) of the graphics module.

    ```c++
        // OH_NativeBuffer * You can obtain information such as the width, height, and stride of the data by calling the APIs of the graphics module.
        OH_NativeBuffer *ohNativeBuffer = OH_AVBuffer_GetNativeBuffer(buffer);
        if (ohNativeBuffer != nullptr) {
            // Obtain the OH_NativeBuffer_Config struct, including the OH_NativeBuffer data information.
            OH_NativeBuffer_Config config;
            OH_NativeBuffer_GetConfig(ohNativeBuffer, &config);

            // Free the OH_NativeBuffer.
            ret = OH_NativeBuffer_Unreference(ohNativeBuffer);
            if (ret != AV_ERR_OK) {
                // Exception handling.
            }
            ohNativeBuffer = nullptr;
        }
    ```

9. Notify the encoder of EOS.

    In the code snippet below, **index** specifies the index of the data queue, which is passed in by the callback function **OnNeedInputBuffer**.

    The API **OH_VideoEncoder_PushInputBuffer** is used to notify the encoder of EOS. This API is also used in step 8 to push the stream to the input queue for encoding. Therefore, in the current step, you must pass in the **AVCODEC_BUFFER_FLAGS_EOS** flag.

    ```c++
    int32_t ret;
    OH_AVCodecBufferAttr info;
    info.size = 0;
    info.offset = 0;
    info.pts = 0;
    info.flags = AVCODEC_BUFFER_FLAGS_EOS;
    ret = OH_AVBuffer_SetBufferAttr(buffer, &info);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    ret = OH_VideoEncoder_PushInputBuffer(videoEnc, index);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    ```

10. Call **OH_VideoEncoder_FreeOutputBuffer()** to release encoded frames.
    
    The procedure is the same as that in surface mode and is not described here.

    ```c++
    int32_t ret;
    // Obtain the encoded information.
    OH_AVCodecBufferAttr info;
    ret = OH_AVBuffer_GetBufferAttr(buffer, &info);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    // Write the encoded frame data (specified by buffer) to the output file.
    outputFile->write(reinterpret_cast<char *>(OH_AVBuffer_GetAddr(buffer)), info.size);
    // Free the output buffer. index is the index of the buffer.
    ret = OH_VideoEncoder_FreeOutputBuffer(videoEnc, index);
    if (ret != AV_ERR_OK) {
        // Exception handling.
    }
    ```

The subsequent processes (including refreshing, resetting, stopping, and destroying the encoder) are the same as those in surface mode. For details, see steps 12-15 in [Surface Input](#surface-input).
