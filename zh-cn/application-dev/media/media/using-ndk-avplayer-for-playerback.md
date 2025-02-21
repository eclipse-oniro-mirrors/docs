# 使用AVPlayer开发音频播放功能(C/C++)

使用AVPlayer可以实现端到端播放原始媒体资源，本开发指导将以完整地播放一首音乐作为示例，向开发者讲解AVPlayer音频播放相关功能。


播放的全流程包含：创建AVPlayer，设置播放资源，设置播放参数（音量/倍速/焦点模式），播放控制（播放/暂停/跳转/停止），重置，销毁资源。


在进行应用开发的过程中，开发者可以通过AVPlayer的callback主动获取播放过程信息。如果应用在音频播放器处于错误状态时执行操作，系统可能会抛出异常或生成其他未定义的行为。


**图1** 播放状态变化示意图  
![Playback status change](figures/playback-status-change-ndk.png)

状态的详细说明请参考[AVPlayerState](../../reference/apis-media-kit/_a_v_player.md#avplayerstate-1)。当播放处于prepared / playing / paused / completed状态时，播放引擎处于工作状态，这需要占用系统较多的运行内存。当客户端暂时不使用播放器时，调用reset()或release()回收内存资源，做好资源利用。

## 开发步骤及注意事项
在 CMake 脚本中链接动态库
```
target_link_libraries(sample PUBLIC libavplayer.so)
```

开发者通过引入[avplayer.h](../../reference/apis-media-kit/avplayer__base_8h.md)、[avpalyer_base.h](../../reference/apis-media-kit/avplayer__base_8h.md)和[native_averrors.h](../../reference/apis-avcodec-kit/native__averrors_8h.md)头文件，使用音频播放相关API。
详细的API说明请参考[AVPlayer API](../../reference/apis-media-kit/_a_v_player.md)。

1. 创建实例OH_AVPlayer_Create()，AVPlayer初始化idle状态。

2. 设置业务需要的监听事件OH_AVPlayer_SetPlayerCallback()，搭配全流程场景使用。支持的监听事件包括：
   | 事件类型 | 说明 |
   | -------- | -------- |
   | OH_AVPlayerOnInfo | 必要事件，监听播放器的过程信息。 |
   | OH_AVPlayerOnError | 必要事件，监听播放器的错误信息。 |

3. 设置资源：调用OH_AVPlayer_SetURLSource(),设置属性url，AVPlayer进入initialized状态。

4. 准备播放：调用OH_AVPlayer_Prepare()，AVPlayer进入prepared状态，此时可以获取时长，设置音量。

5. 音频播控：播放OH_AVPlayer_Play()，暂停OH_AVPlayer_Pause()，跳转OH_AVPlayer_Seek()，停止OH_AVPlayer_Stop() 等操作。

6. （可选）更换资源：调用OH_AVPlayer_Reset()重置资源，AVPlayer重新进入idle状态，允许更换资源url。

7. 退出播放：调用OH_AVPlayer_Release()销毁实例，AVPlayer进入released状态，退出播放。

## 完整示例

```c
#include "napi/native_api.h"

#include <multimedia/player_framework/avplayer.h>
#include <multimedia/player_framework/avplayer_base.h>
#include <multimedia/player_framework/native_averrors.h>

static char *Url;

void OnInfo(OH_AVPlayer *player, AVPlayerOnInfoType type, int32_t extra)
{
    int32_t ret;
    switch (type) {
        case AV_INFO_TYPE_STATE_CHANGE:
            switch (extra) {
                case AV_IDLE: // 成功调用reset接口后触发该状态机上报
//                    ret = OH_AVPlayer_SetURLSource(player, url); // 设置url
//                    if (ret != AV_ERR_OK) {
//                    // 处理异常
//                    }
                    break;
                case AV_INITIALIZED: 
                    ret = OH_AVPlayer_Prepare(player); //设置播放源后触发该状态上报
                    if (ret != AV_ERR_OK) {
                    // 处理异常
                    }
                    break;
                case AV_PREPARED:  
                    ret = OH_AVPlayer_Play(player); // 调用播放接口开始播放
                    if (ret != AV_ERR_OK) {
                    // 处理异常
                    }
                    break;
                case AV_PLAYING:  
//                    ret = OH_AVPlayer_Pause(player); //调用暂停接口暂停播放
//                    if (ret != AV_ERR_OK) {
//                    // 处理异常
//                    }
                    break;
                case AV_PAUSED:  
//                    ret = OH_AVPlayer_Play(player); // 再次播放接口开始播放
//                    if (ret != AV_ERR_OK) {
//                    // 处理异常
//                    }
//                    break;
                case AV_STOPPED:  
                    ret = OH_AVPlayer_Release(player); //调用reset接口初始化avplayer状态
                    if (ret != AV_ERR_OK) {
                    // 处理异常
                    }
                    break;
                case AV_COMPLETED:  
                    ret = OH_AVPlayer_Stop(player);// 调用播放结束接口
                    if (ret != AV_ERR_OK) {
                    // 处理异常
                    }
                    break;
                default:
                    break;
            }
            break;
        case AV_INFO_TYPE_POSITION_UPDATE:
        // do something
            break;
        default:
            break;
    }
}

void OnError(OH_AVPlayer *player, int32_t errorCode, const char *errorMsg)
{
    // do something
}

// 调用播放方法时，需要在index.d.ts文件内描述映射的play方法，需要传入一个string类型的参数
// ets文件调用播放方法时，传入文件路径 testNapi.play("/data/test/test.mp3")
static napi_value Play(napi_env env, napi_callback_info info)
{
    size_t argc = 1;
    napi_value args[1] = {nullptr};
    
    napi_get_cb_info(env, info, &argc, args, nullptr, nullptr);
    
    // 获取参数类型
    napi_valuetype stringType;
    if (napi_ok != napi_typeof(env, args[0], &stringType)) {
        // 处理异常
        return nullptr;
    }
    
    // 参数校验
    if (napi_null == stringType) {
        // 处理异常
        return nullptr;
    }
    
    // 获取传递的string长度
    size_t length = 0;
    if (napi_ok != napi_get_value_string_utf8(env, args[0], nullptr, 0, &length)) {
        // 处理异常
        return nullptr;
    }
    
    // 如果传入的是""，则直接返回
    if (length == 0) {
        // 处理异常
        return nullptr;
    }
    
    // 读取传入的string放入buffer中
    char *url = new char[length + 1];
    if (napi_ok != napi_get_value_string_utf8(env, args[0], url, length + 1, &length)) {
        delete[] url;
        url = nullptr;
        // 处理异常
        return nullptr;
    }

    Url = url;
    
    // 创建播放实例
    OH_AVPlayer *player = OH_AVPlayer_Create();
    AVPlayerCallback callback;
    callback.onInfo = OnInfo;
    callback.onError = OnError;
    // 设置回调，监听信息
    int32_t ret = OH_AVPlayer_SetPlayerCallback(player, callback);
    if (ret != AV_ERR_OK) {
    // 处理异常
    }
    ret = OH_AVPlayer_SetURLSource(player, url); // 设置url
    if (ret != AV_ERR_OK) {
    // 处理异常
    }
    napi_value value;
    napi_create_int32(env, 0, &value);
    return value;
}

EXTERN_C_START
static napi_value Init(napi_env env, napi_value exports)
{
    napi_property_descriptor desc[] = {
        { "play", nullptr, Play, nullptr, nullptr, nullptr, napi_default, nullptr }
    };
    napi_define_properties(env, exports, sizeof(desc) / sizeof(desc[0]), desc);
    return exports;
}
EXTERN_C_END

static napi_module demoModule = {
    .nm_version =1,
    .nm_flags = 0,
    .nm_filename = nullptr,
    .nm_register_func = Init,
    .nm_modname = "entry",
    .nm_priv = ((void*)0),
    .reserved = { 0 },
};

extern "C" __attribute__((constructor)) void RegisterEntryModule(void)
{
    napi_module_register(&demoModule);
}
```