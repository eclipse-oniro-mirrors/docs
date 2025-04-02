# 使用Node-API接口在主线程中进行模块加载

## 场景介绍

Node-API中的napi_load_module接口的功能是在主线程中进行模块的加载，当模块加载出来之后，可以使用函数napi_get_property获取模块导出的变量，也可以使用napi_get_named_property获取模块导出的函数，目前支持以下场景：

- 加载系统模块，例如@ohos.hilog
- 加载ets目录下文件中的模块

## 函数说明

```cpp
napi_status napi_load_module(napi_env env,
                             const char* path,
                             napi_value* result);
```

| 参数            | 说明          |
| :------------- | :----------------------------- |
| env            | 当前的虚拟机环境       |
| path          | 加载的文件路径或者模块名          |
| result         | 加载的模块          |

## 使用限制

- 禁止在非主线程当中使用该接口。
- 禁止在Init函数中使用该接口。
- 禁止在线程安全函数的回调函数当中进行文件路径的加载。

建议使用[napi_load_module_with_info](use-napi-load-module-with-info.md)来进行模块加载，该接口支持了更多的场景。

## 加载系统模块使用示例

使用napi_load_module导出系统模块hilog，并调用info函数。

```cpp
static napi_value loadModule(napi_env env, napi_callback_info info) {
    // 1. 使用napi_load_module加载模块@ohos.hilog
    napi_value result;
    napi_status status = napi_load_module(env, "@ohos.hilog", &result);
    
    // 2. 使用napi_get_named_property获取info函数
    napi_value infoFn;
    napi_get_named_property(env, result, "info", &infoFn);
    
    napi_value tag;
    std::string formatStr = "test";
    napi_create_string_utf8(env, formatStr.c_str(), formatStr.size(), &tag);
    
    napi_value outputString;
    std::string str = "Hello OpenHarmony";
    napi_create_string_utf8(env, str.c_str(), str.size(), &outputString);
    
    napi_value flag;
    napi_create_int32(env, 0, &flag);

    napi_value args[3] = {flag, tag, outputString};
    // 3. 使用napi_call_function调用info函数
    napi_call_function(env, result, infoFn, 3, args, nullptr);
    return result;
}
```

## 加载ArkTS文件中的模块使用示例

当加载文件中的模块时，如以下ArkTS代码：

```javascript
//./src/main/ets/Test.ets
let value = 123;
function test() {
  console.log("Hello OpenHarmony");
}
export {value, test};
```

1. 需要在工程的build-profile.json5文件中进行以下配置：

    ```json
    {
        "buildOption" : {
            "arkOptions" : {
                "runtimeOnly" : {
                    "sources": [
                        "./src/main/ets/Test.ets"
                    ]
                }
            }
        }
    }
    ```

2. 使用napi_load_module加载Test文件，调用函数test以及获取变量value：

    ```cpp
    static napi_value loadModule(napi_env env, napi_callback_info info) {
        napi_value result;
        // 1. 使用napi_load_module加载Test文件中的模块
        napi_status status = napi_load_module(env, "ets/Test", &result);

        napi_value testFn;
        // 2. 使用napi_get_named_property获取test函数
        napi_get_named_property(env, result, "test", &testFn);
        // 3. 使用napi_call_function调用函数test
        napi_call_function(env, result, testFn, 0, nullptr, nullptr);

        napi_value value;
        napi_value key;
        std::string keyStr = "value";
        napi_create_string_utf8(env, keyStr.c_str(), keyStr.size(), &key);
        // 4. 使用napi_get_property获取变量value
        napi_get_property(env, result, key, &value);
        return result;
    }
    ```
