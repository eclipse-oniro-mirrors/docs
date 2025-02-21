# 视频编码

开发者可以调用本模块的Native API接口，完成视频编码，即将未压缩的视频数据压缩成视频码流。

当前支持的编码能力如下：

| 容器规格 | 视频编码类型                 |
| -------- | ---------------------------- |
| mp4      | HEVC（H.265）、 AVC（H.264） |
| m4a      | HEVC（H.265）、 AVC（H.264） |

目前仅支持硬件编码，基于MimeType创建编码器时，支持配置为H264 (OH_AVCODEC_MIMETYPE_VIDEO_AVC) 和 H265 (OH_AVCODEC_MIMETYPE_VIDEO_HEVC)。

## Surface输入与Buffer输入

两者的数据来源不同。

Surface输入是指用OHNativeWindow来传递输入数据，可以与其他模块对接，例如相机模块。

Buffer输入是指有一块预先分配好的内存区域，调用者需要将原始数据拷贝进这块内存区域中。更适用于从文件中读取视频数据等场景。

在接口调用的过程中，两种方式的接口调用方式基本一致，但存在以下差异点：

1. Buffer模式下，应用调用OH_VideoEncoder_PushInputBuffer()输入数据；Surface模式下，应用应在编码器就绪前调用OH_VideoEncoder_GetSurface()，获取OHNativeWindow用于传递视频数据。
2. Buffer模式下，应用调用OH_VideoEncoder_PushInputBuffer()传入结束flag，编码器读取到尾帧后，停止编码；Surface模式下，需要调用OH_VideoEncoder_NotifyEndOfStream()通知编码器输入流结束。

两种模式的开发步骤详细说明请参考：[Surface模式](#surface模式)和[Buffer模式](#buffer模式)。

## 开发指导

详细的API说明请参考[API文档](../../reference/apis-avcodec-kit/_video_encoder.md)。
如下为视频编码调用关系图：
![Invoking relationship of video encode stream](figures/video-encode.png)

### 在 CMake 脚本中链接动态库

```cmake
target_link_libraries(sample PUBLIC libnative_media_codecbase.so)
target_link_libraries(sample PUBLIC libnative_media_core.so)
target_link_libraries(sample PUBLIC libnative_media_venc.so)
```

### Surface模式

参考以下示例代码，开发者可以完成Surface模式下视频编码的全流程。此处以surface数据输入，编码成H.264格式为例。
本模块目前仅支持异步模式的数据轮转。

1. 添加头文件。

    ```cpp
    #include <multimedia/player_framework/native_avcodec_videoencoder.h>
    #include <multimedia/player_framework/native_avcapability.h>
    #include <multimedia/player_framework/native_avcodec_base.h>
    #include <multimedia/player_framework/native_avformat.h>
    #include <multimedia/player_framework/native_avbuffer.h>
    ```

2. 创建编码器实例对象。

    应用可以通过名称或媒体类型创建编码器。示例中的变量说明如下：

    - videoEnc：视频编码器实例的指针；
    - capability：编解码器能力查询实例的指针；
    - OH_AVCODEC_MIMETYPE_VIDEO_AVC：AVC格式视频码流的名称。

    ```c++
    // 通过codec name创建编码器，应用有特殊需求，比如选择支持某种分辨率规格的编码器，可先查询capability，再根据codec name创建编码器。
    OH_AVCapability *capability = OH_AVCodec_GetCapability(OH_AVCODEC_MIMETYPE_VIDEO_AVC, true);
    const char *codecName = OH_AVCapability_GetName(capability);
    OH_AVCodec *videoEnc = OH_VideoEncoder_CreateByName(codecName);
    ```

    ```c++
    // 通过 MIME TYPE 创建编码器，系统会根据MIME创建最合适的编码器。
    OH_AVCodec *videoEnc = OH_VideoEncoder_CreateByMime(OH_AVCODEC_MIMETYPE_VIDEO_AVC);
    ```

3. 调用OH_VideoEncoder_RegisterCallback()设置回调函数。

    > **说明：**
    >
    > 在回调函数中，对数据队列进行操作时，需要注意多线程同步的问题。
    >

    注册回调函数指针集合OH_AVCodecCallback，包括：

    - 编码器运行错误；
    - 码流信息变化，如格式变化等；
    - 输入回调无作用，用户通过获取的surface输入数据；
    - 运行过程中产生了新的输出数据，即编码完成。

    ```c++
    // 设置 OnError 回调函数
    static void OnError(OH_AVCodec *codec, int32_t errorCode, void *userData)
    {
        (void)codec;
        (void)errorCode;
        (void)userData;
    }

    // 设置 OnStreamChanged 回调函数
    static void OnStreamChanged(OH_AVCodec *codec, OH_AVFormat *format, void *userData)
    {
        (void)codec;
        (void)format;
        (void)userData;
    }

    // 设置 OH_AVCodecOnNeedInputBuffer 回调函数，编码输入帧送入数据队列
    static void OnNeedInputBuffer(OH_AVCodec *codec, uint32_t index, OH_AVBuffer *buffer, void *userData)
    {
        (void)userData;
        (void)index;
        (void)buffer;
        // surface模式下，该回调函数无作用，用户通过获取的surface输入数据
    }

    // 设置 OH_AVCodecOnNewOutputBuffer 回调函数，编码完成帧送入输出队列
    static void OnNewOutputBuffer(OH_AVCodec *codec, uint32_t index, OH_AVBuffer *buffer, void *userData)
    {
        // 完成帧buffer对应的index，送入outIndexQueue队列
        // 完成帧的数据buffer送入outBufferQueue队列
        // 数据处理，请参考:
        // - 释放编码帧
    }

    // 配置异步回调，调用 OH_VideoEncoder_SetCallback 接口
    OH_AVCodecCallback cb = {&OnError, &OnStreamChanged, &OnNeedInputBuffer, &OnNewOutputBuffer};
    int32_t ret = OH_VideoEncoder_RegisterCallback(videoEnc, cb, NULL);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    ```

4. 调用OH_VideoEncoder_Configure()配置编码器。

    详细可配置选项的说明请参考[变量](../../reference/apis-avcodec-kit/_codec_base.md#变量)。
    目前支持的所有格式都必须配置以下选项：视频帧宽度、视频帧高度、视频颜色格式。示例中的变量如下：

    - DEFAULT_WIDTH：320像素宽度；
    - DEFAULT_HEIGHT：240像素高度；
    - DEFAULT_PIXELFORMAT： 颜色格式，因为示例使用YUV的文件保存的颜色格式是NV12，所以设置为 AV_PIXEL_FORMAT_NV12。

    ```c++
    // 配置视频帧宽度（必须）
    constexpr uint32_t DEFAULT_WIDTH = 320; 
    // 配置视频帧高度（必须）
    constexpr uint32_t DEFAULT_HEIGHT = 240;
    // 配置视频颜色格式（必须）
    constexpr OH_AVPixelFormat DEFAULT_PIXELFORMAT = AV_PIXEL_FORMAT_NV12;
    // 配置视频帧速率
    double frameRate = 30.0;
    // 配置视频YUV值范围标志
    bool rangeFlag = false;
    // 配置视频原色
    int32_t primary = static_cast<int32_t>(OH_ColorPrimary::COLOR_PRIMARY_BT709);
    // 配置传输特性
    int32_t transfer = static_cast<int32_t>(OH_TransferCharacteristic::TRANSFER_CHARACTERISTIC_BT709);
    // 配置最大矩阵系数
    int32_t matrix = static_cast<int32_t>(OH_MatrixCoefficient::MATRIX_COEFFICIENT_IDENTITY);
    // 配置编码Profile
    int32_t profile = static_cast<int32_t>(OH_AVCProfile::AVC_PROFILE_BASELINE);
    // 配置编码比特率模式
    int32_t rateMode = static_cast<int32_t>(OH_VideoEncodeBitrateMode::CBR);
    // 配置关键帧的间隔，单位为毫秒
    int32_t iFrameInterval = 23000;
    // 配置所需的编码质量。只有在恒定质量模式下配置的编码器才支持此配置
    int32_t quality = 0;
    // 配置比特率
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
        // 异常处理
    }
    OH_AVFormat_Destroy(format);
    ```

5. 调用OH_VideoEncoder_Prepare()编码器就绪。

    该接口将在编码器运行前进行一些数据的准备工作。

    ```c++
    ret = OH_VideoEncoder_Prepare(videoEnc);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    ```

6. 获取Surface。

    获取编码器Surface模式的OHNativeWindow输入，获取Surface需要在启动编码器之前完成。

    ```c++
    int32_t ret;
    // 获取需要输入的Surface，以进行编码
    OHNativeWindow *nativeWindow;
    ret =  OH_VideoEncoder_GetSurface(videoEnc, &nativeWindow);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    // 通过OHNativeWindow*变量类型，配置输入数据的Surface
    ```

    OHNativeWindow*变量类型的使用方法请参考图形子系统 [OHNativeWindow](../../reference/apis-arkgraphics2d/_native_window.md#ohnativewindow)

7. 调用OH_VideoEncoder_Start()启动编码器。

    ```c++
    int32_t ret;
    // 启动编码器，开始编码
    ret = OH_VideoEncoder_Start(videoEnc);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    ```

8. （可选）在运行过程中动态配置编码器参数。

    ```c++
    OH_AVFormat *format = OH_AVFormat_Create();
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_REQUEST_I_FRAME, true); //目前仅支持动态请求IDR帧
    int32_t ret = OH_VideoEncoder_SetParameter(videoEnc, format);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    ```

9. 写入编码码流。
    在之前的第6步中，开发者已经对OH_VideoEncoder_GetSurface接口返回的OHNativeWindow*类型变量进行配置。因为编码所需的数据，由配置的Surface进行持续地输入，所以开发者无需对OnNeedInputBuffer回调函数进行处理，也无需使用OH_VideoEncoder_PushInputBuffer接口输入数据。

10. 调用OH_VideoEncoder_NotifyEndOfStream()通知编码器码流结束。

    ```c++
    int32_t ret;
    // surface模式：通知视频编码器输入流已结束，只能使用此接口进行通知
    // 不能像buffer模式中将flag设为AVCODEC_BUFFER_FLAGS_EOS，再调用OH_VideoEncoder_PushInputBuffer接口通知编码器输入结束
    ret = OH_VideoEncoder_NotifyEndOfStream(videoEnc);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    ```

11. 调用OH_VideoEncoder_FreeOutputBuffer()释放编码帧。

    以下示例中：

    - index：回调函数OnNewOutputBuffer传入的参数，数据队列的索引。
    - buffer： 回调函数OnNewOutputBuffer传入的参数，可以通过OH_AVBuffer_GetAddr接口得到共享内存地址的指针。

    ```c++
    int32_t ret;
    // 获取解码后信息
    OH_AVCodecBufferAttr info;
    ret = OH_AVBuffer_GetBufferAttr(buffer, &info);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    // 将编码完成帧数据mem写入到对应输出文件中
    outputFile->write(reinterpret_cast<char *>(OH_AVBuffer_GetAddr(buffer)), info.size);
    // 释放已完成写入的数据，index为对应输出队列下标
    ret = OH_VideoEncoder_FreeOutputBuffer(videoEnc, index);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    ```

12. （可选）调用OH_VideoEncoder_Flush()刷新编码器。

    调用OH_VideoEncoder_Flush()后，编码器仍处于运行态，但会将当前队列清空，将已编码的数据释放。

    此时需要调用OH_VideoEncoder_Start()重新开始编码。

    ```c++
    int32_t ret;
    // 刷新编码器videoEnc
    ret = OH_VideoEncoder_Flush(videoEnc);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    // 重新开始编码
    ret = OH_VideoEncoder_Start(videoEnc);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    ```

13. （可选）调用OH_VideoEncoder_Reset()重置编码器。

    调用OH_VideoEncoder_Reset()后，编码器回到初始化的状态，需要调用OH_VideoEncoder_Configure()重新配置。

    ```c++
    int32_t ret;
    // 重置编码器videoEnc
    ret = OH_VideoEncoder_Reset(videoEnc);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    // 重新配置编码器参数
    ret = OH_VideoEncoder_Configure(videoEnc, format);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    ```

14. （可选）调用OH_VideoEncoder_Stop()停止编码器。

    ```c++
    int32_t ret;
    // 终止编码器videoEnc
    ret = OH_VideoEncoder_Stop(videoEnc);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    ```

15. 调用OH_VideoEncoder_Destroy()销毁编码器实例，释放资源。

    > **说明：**
    >
    > 不能在回调函数中调用；
    > 执行该步骤之后，需要开发者将videoEnc指向nullptr，防止野指针导致程序错误。
    >

    ```c++
    int32_t ret;
    // 调用OH_VideoEncoder_Destroy，注销编码器
    ret = OH_VideoEncoder_Destroy(videoEnc);
    videoEnc = nullptr;
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    ```

### Buffer模式

参考以下示例代码，开发者可以完成Buffer模式下视频编码的全流程。此处以YUV文件输入，编码成H.264格式为例。
本模块目前仅支持异步模式的数据轮转。

1. 添加头文件。

    ```cpp
    #include <multimedia/player_framework/native_avcodec_videoencoder.h>
    #include <multimedia/player_framework/native_avcapability.h>
    #include <multimedia/player_framework/native_avcodec_base.h>
    #include <multimedia/player_framework/native_avformat.h>
    #include <multimedia/player_framework/native_avbuffer.h>
    ```

2. 创建编码器实例对象。

    与surface模式相同，此处不再赘述。

    ```c++
    // 通过codec name创建编码器，应用有特殊需求，比如选择支持某种分辨率规格的编码器，可先查询capability，再根据codec name创建编码器。
    OH_AVCapability *capability = OH_AVCodec_GetCapability(OH_AVCODEC_MIMETYPE_VIDEO_AVC, true);
    const char *codecName = OH_AVCapability_GetName(capability);
    OH_AVCodec *videoEnc = OH_VideoEncoder_CreateByName(codecName);
    ```

    ```c++
    // 通过 MIME TYPE 创建编码器，系统会根据MIME创建最合适的编码器。
    OH_AVCodec *videoEnc = OH_VideoEncoder_CreateByMime(OH_AVCODEC_MIMETYPE_VIDEO_AVC);
    ```

3. 调用OH_VideoEncoder_RegisterCallback()设置回调函数。

    > **说明：**
    >
    > 在回调函数中，对数据队列进行操作时，需要注意多线程同步的问题。
    >

    注册回调函数指针集合OH_AVCodecCallback，包括：

    - 编码器运行错误；
    - 码流信息变化，如格式变化等；
    - 运行过程中需要新的输入数据，即编码器已准备好，可以输入YUV/RGB数据；
    - 运行过程中产生了新的输出数据，即编码完成。

    开发者可以通过处理该回调报告的信息，确保编码器正常运转。

    ```c++
    // 编码异常回调OH_AVCodecOnError实现
    static void OnError(OH_AVCodec *codec, int32_t errorCode, void *userData)
    {
        (void)codec;
        (void)errorCode;
        (void)userData;
    }

    // 编码数据流变化回调OH_AVCodecOnStreamChanged实现
    static void OnStreamChanged(OH_AVCodec *codec, OH_AVFormat *format, void *userData)
    {
        (void)codec;
        (void)format;
        (void)userData;
    }

    // 编码输入回调OH_AVCodecOnNeedInputBuffer实现
    static void OnNeedInputBuffer(OH_AVCodec *codec, uint32_t index, OH_AVBuffer *buffer, void *userData)
    {
        // 输入帧buffer对应的index，送入InIndexQueue队列
        // 输入帧的数据buffer送入InBufferQueue队列
        // 数据处理，请参考:
        // - 写入编码码流
        // - 通知编码器码流结束
    }

    // 编码输出回调OH_AVCodecOnNewOutputBuffer实现
    static void OnNewOutputBuffer(OH_AVCodec *codec, uint32_t index, OH_AVBuffer *buffer, void *userData)
    {
        // 完成帧buffer对应的index，送入outIndexQueue队列
        // 完成帧的数据buffer送入outBufferQueue队列
        // 数据处理，请参考:
        // - 释放编码帧
    }

    // 配置异步回调，调用 OH_VideoEncoder_RegisterCallback 接口
    OH_AVCodecCallback cb = {&OnError, &OnStreamChanged, &OnNeedInputBuffer, &OnNewOutputBuffer};
    int32_t ret = OH_VideoEncoder_RegisterCallback(videoEnc, cb, NULL);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    ```

    4. 调用OH_VideoEncoder_Configure()配置编码器。

    与surface模式相同，此处不再赘述。

    ```c++
    // 配置视频帧宽度（必须）
    constexpr uint32_t DEFAULT_WIDTH = 320; 
    // 配置视频帧高度（必须）
    constexpr uint32_t DEFAULT_HEIGHT = 240;
    // 配置视频颜色格式（必须）
    constexpr OH_AVPixelFormat DEFAULT_PIXELFORMAT = AV_PIXEL_FORMAT_NV12;
    
    OH_AVFormat *format = OH_AVFormat_Create();
    // 写入format
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_WIDTH, DEFAULT_WIDTH);
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_HEIGHT, DEFAULT_HEIGHT);
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_PIXEL_FORMAT, DEFAULT_PIXELFORMAT);
    // 配置编码器
    int32_t ret = OH_VideoEncoder_Configure(videoEnc, format);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
        OH_AVFormat_Destroy(format);
    ```

5. 调用OH_VideoEncoder_Prepare()编码器就绪。

    该接口将在编码器运行前进行一些数据的准备工作。

    ```c++
    ret = OH_VideoEncoder_Prepare(videoEnc);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    ```

6. 调用OH_VideoEncoder_Start()启动编码器，进入运行态。

    启动编码器后，回调函数将开始响应事件。所以，需要先配置输入文件、输出文件。

    ```c++
    // 配置待编码文件路径
    std::string_view inputFilePath = "/*yourpath*.yuv";
    std::string_view outputFilePath = "/*yourpath*.h264";
    std::unique_ptr<std::ifstream> inputFile = std::make_unique<std::ifstream>();
    std::unique_ptr<std::ofstream> outputFile = std::make_unique<std::ofstream>();
    inputFile->open(inputFilePath.data(), std::ios::in | std::ios::binary);
    outputFile->open(outputFilePath.data(), std::ios::out | std::ios::binary | std::ios::ate);
    // 启动编码器，开始编码
    int32_t ret = OH_VideoEncoder_Start(videoEnc);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    ```

7. （可选）在运行过程中动态配置编码器参数。

    ```c++
    OH_AVFormat *format = OH_AVFormat_Create();
    OH_AVFormat_SetIntValue(format, OH_MD_KEY_REQUEST_I_FRAME, true); //目前仅支持动态请求IDR帧
    int32_t ret = OH_VideoEncoder_SetParameter(videoEnc, format);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    ```

8. 调用OH_VideoEncoder_PushInputBuffer()写入编码码流。

    送入输入队列进行编码，以下示例中：

    - buffer：回调函数OnNeedInputBuffer传入的参数，可以通过OH_AVBuffer_GetAddr接口得到共享内存地址的指针；
    - index：回调函数OnNeedInputBuffer传入的参数，数据队列的索引；
    - flags：缓冲区标记的类别，请参考[OH_AVCodecBufferFlags](../../reference/apis-avcodec-kit/_core.md#oh_avcodecbufferflags)
    - stride: 获取到的buffer数据的跨距。

    ```c++
        if (stride == DEFAULT_WIDTH) {
            // 处理文件流得到帧的长度，再将需要编码的数据写入到对应index的buffer中
            int32_t frameSize = DEFAULT_WIDTH * DEFAULT_HEIGHT * 3 / 2; // NV12颜色格式下，每帧数据大小的计算公式
            inputFile->read(reinterpret_cast<char *>(OH_AVBuffer_GetAddr(buffer)), frameSize);
        } else {
            // 如果跨距不等于宽，需要用户按照跨距进行偏移
        }
        // 配置buffer info信息
        OH_AVCodecBufferAttr info;
        info.size = frameSize;
        info.offset = 0;
        info.pts = 0;
        info.flags = flags;
        ret = OH_AVBuffer_SetBufferAttr(buffer, &info);
        if (ret != AV_ERR_OK) {
            // 异常处理
        }
        // 送入编码输入队列进行编码，index为对应输入队列的下标
        int32_t ret = OH_VideoEncoder_PushInputBuffer(videoEnc, index);
        if (ret != AV_ERR_OK) {
            // 异常处理
        }
    ```

    硬件编码在处理buffer数据时（推送数据前），一般需要获取数据的宽高、跨距来保证编码输入数据被正确的处理，请参考图形子系统 [OH_NativeBuffer](../../reference/apis-arkgraphics2d/_o_h___native_buffer.md)。

    ```c++
        // OH_NativeBuffer *可以通过图形模块的接口可以获取数据的宽高、跨距等信息。
        OH_NativeBuffer *ohNativeBuffer = OH_AVBuffer_GetNativeBuffer(buffer);
        if (ohNativeBuffer != nullptr) {
            // 获取OH_NativeBuffer_Config结构体，包含OH_NativeBuffer的数据信息
            OH_NativeBuffer_Config config;
            OH_NativeBuffer_GetConfig(ohNativeBuffer, &config);

            // 释放ohNativeBuffer
            ret = OH_NativeBuffer_Unreference(ohNativeBuffer);
            if (ret != AV_ERR_OK) {
                // 异常处理
            }
            ohNativeBuffer = nullptr;
        }
    ```

9. 通知编码器码流结束。

    以下示例中：index：回调函数OnNeedInputBuffer传入的参数，数据队列的索引。

    与“8. 写入编码码流”一样，使用同一个接口OH_VideoEncoder_PushInputBuffer，通知编码器输入结束，需要对flag标识成AVCODEC_BUFFER_FLAGS_EOS

    ```c++
    int32_t ret;
    OH_AVCodecBufferAttr info;
    info.size = 0;
    info.offset = 0;
    info.pts = 0;
    info.flags = AVCODEC_BUFFER_FLAGS_EOS;
    ret = OH_AVBuffer_SetBufferAttr(buffer, &info);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    ret = OH_VideoEncoder_PushInputBuffer(videoEnc, index);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    ```

10. 调用OH_VideoEncoder_FreeOutputBuffer()释放编码帧。
    与surface模式相同，此处不再赘述。

    ```c++
    int32_t ret;
    // 获取解码后信息
    OH_AVCodecBufferAttr info;
    ret = OH_AVBuffer_GetBufferAttr(buffer, &info);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    // 将编码完成帧数据buffer写入到对应输出文件中
    outputFile->write(reinterpret_cast<char *>(OH_AVBuffer_GetAddr(buffer)), info.size);
    // 释放已完成写入的数据，index为对应输出队列的下标
    ret = OH_VideoEncoder_FreeOutputBuffer(videoEnc, index);
    if (ret != AV_ERR_OK) {
        // 异常处理
    }
    ```

后续流程（包括刷新编码器、重置编码器、停止编码器、销毁编码器）与Surface模式一致，请参考[Surface模式](#surface模式)的步骤12-15。
