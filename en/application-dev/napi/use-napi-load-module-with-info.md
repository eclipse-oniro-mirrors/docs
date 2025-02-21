# Loading a Module Using Node-API

You can use **napi_load_module_with_info** to load a module. After the module is loaded, you can use **napi_get_property** to obtain the variables of the module or use **napi_get_named_property** to obtain the functions of the module. The **napi_load_module_with_info** API can be used in a [newly created ArkTS runtime environment](use-napi-ark-runtime.md).

## Function Description

```cpp
napi_status napi_load_module_with_info(napi_env env,
                                       const char* path,
                                       const char* module_info,
                                       napi_value* result);
```

| Parameter           | Description         |
| :------------- | :----------------------------- |
| env            | Current VM environment.      |
| path          | Path of the file or name of the module to load.         |
| module_info   | Path composed of **bundleName** and **moduleName**.      |
| result         | Module loaded.         |

> **NOTE**
>
> - **bundleName** indicates the project name configured in **AppScope/app.json5**.
> - **moduleName** must be set to the module name configured in the **module.json5** file in the HAP to which the module belongs.
> - You can also use [napi_load_module](use-napi-load-module.md) to load a module. However, **napi_load_module** is limited to loading a module in the main thread only.

## When to Use

| Scenario           | Description          | Description                        |
| :------------- | :----------------------------- | :--------------------------- |
| Local project module  | Load the module file.      | The file path must start with **moduleName**.            |
| Local project module  | Load the HAR module name.          | -                            |
| Remote package        | Load the remote HAR module name.       | -                            |
| Remote package        | Load the ohpm package name.           | -                            |
| API        |    Load **@ohos.** or **@system.**.         | -                            |
| Native library  | Load **libNativeLibrary.so**.| -                            |

> **NOTE**
>
> - The module name to be loaded is the entry file, generally **index.ets/ts**, of the module.
> - To load a HAR to another HAR, ensure that **module_info** is correct. The value of **moduleName** must be that of the HAP.
> - If a third-party package is directly or indirectly used in a HAP/HSP and the third-party package has loaded another module, for example, module A, using **napi_load_module_with_info**, you must add module A in the dependencies of the HAP/HSP.

## How to Use

- **Loading a module file**

Load a module from a file, as shown in the following ArkTS code.

```javascript
//./src/main/ets/Test.ets
let value = 123;
function test() {
  console.log("Hello OpenHarmony");
}
export {value, test};
```

1. Configure the **build-profile.json5** file of the current module as follows:

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

2. Call **napi_load_module_with_info** to load the **Test.ets** file, call the **test()** function, and obtain the variable values.

    > **NOTE**
    >
    > When a module file is loaded with **useNormalizedOHMUrl** enabled (the **useNormalizedOHMUrl** field of **strictMode** in the application's **build-profile.json5** file in the same directory as **entry** in the project is set to **true**):<br>1. **bundleName** does not affect the loading logic. The corresponding HAP in the process is intelligently indexed based on the module name. For example, the module can be successfully loaded if **bundleName** is set to **com.example.application1** while the actual bundle name of the project is **com.example.application**. <br>2. The file path must start with **packageName**, which is the value of **name** in the **oh-package.json5** file of the module.

    ```cpp
    static napi_value loadModule(napi_env env, napi_callback_info info) {
        napi_value result;
        // 1. Call napi_load_module_with_info to load the module from the Test.ets file.
        napi_status status = napi_load_module_with_info(env, "entry/src/main/ets/Test", "com.example.application/entry", &result);

        napi_value testFn;
        // 2. Call napi_get_named_property to obtain the test function.
        napi_get_named_property(env, result, "test", &testFn);
        // 3. Call napi_call_function to invoke the test function.
        napi_call_function(env, result, testFn, 0, nullptr, nullptr);

        napi_value value;
        napi_value key;
        std::string keyStr = "value";
        napi_create_string_utf8(env, keyStr.c_str(), keyStr.size(), &key);
        // 4. Call napi_get_property to obtain a variable value.
        napi_get_property(env, result, key, &value);
        return result;
    }
    ```

- **Loading a HAR module name**

The **Index.ets** file in the HAR is as follows:

```javascript
//library Index.ets
let value = 123;
function test() {
  console.log("Hello OpenHarmony");
}
export {value, test};
```

1. Configure **dependencies** in the **oh-package.json5** file.

    ```json
    {
        "dependencies": {
            "library": "file:../library"
        }
    }
    ```

2. Configure **build-profile.json5** for the module that uses **library**.

    ```json
    {
        "buildOption" : {
            "arkOptions" : {
                "runtimeOnly" : {
                    "packages": [
                        "library"
                    ]
                }
            }
        }
    }
    ```

3. Call **napi_load_module_with_info** to load **library**, call the **test** function, and obtain the variable values.

    ```cpp
    static napi_value loadModule(napi_env env, napi_callback_info info) {
        napi_value result;
        // 1. Call napi_load_module_with_info to load library.
        napi_status status = napi_load_module_with_info(env, "library", "com.example.application/entry", &result);

        napi_value testFn;
        // 2. Call napi_get_named_property to obtain the test function.
        napi_get_named_property(env, result, "test", &testFn);
        // 3. Call napi_call_function to invoke the test function.
        napi_call_function(env, result, testFn, 0, nullptr, nullptr);

        napi_value value;
        napi_value key;
        std::string keyStr = "value";
        napi_create_string_utf8(env, keyStr.c_str(), keyStr.size(), &key);
        // 4. Call napi_get_property to obtain a variable value.
        napi_get_property(env, result, key, &value);
        return result;
    }
    ```

- **Loading a remote HAR module name**

1. Configure **dependencies** in the **oh-package.json5** file.

    ```json
    {
        "dependencies": {
            "@ohos/hypium": "1.0.16"
        }
    }
    ```

2. Configure **build-profile.json5** for the module that uses @ohos/hypium.

    ```json
    {
        "buildOption" : {
            "arkOptions" : {
                "runtimeOnly" : {
                    "packages": [
                        "@ohos/hypium"
                    ]
                }
            }
        }
    }
    ```

3. Call **napi_load_module_with_info** to load **@ohos/hypium** and obtain the **DEFAULT** variable.

    ```cpp
    static napi_value loadModule(napi_env env, napi_callback_info info) {
        napi_value result;
        // 1. Call napi_load_module_with_info to load @ohos/hypium.
        napi_status status = napi_load_module_with_info(env, "@ohos/hypium", "com.example.application/entry", &result);

        napi_value key;
        std::string keyStr = "DEFAULT";
        napi_create_string_utf8(env, keyStr.c_str(), keyStr.size(), &key);
        // 2. Call napi_get_property to obtain the DEFAULT variable.
        napi_value defaultValue;
        napi_get_property(env, result, key, &defaultValue);
        return result;
    }
    ```

- **Loading an ohpm package name**

1. Configure **dependencies** in the **oh-package.json5** file.

    ```json
    {
        "dependencies": {
            "json5": "^2.2.3"
        }
    }
    ```

2. Configure **build-profile.json5** for the module that uses the .json5 file.

    ```json
    {
        "buildOption" : {
            "arkOptions" : {
                "runtimeOnly" : {
                    "packages": [
                        "json5"
                    ]
                }
            }
        }
    }
    ```

3. Call **napi_load_module_with_info** to load **json5** and call the **stringify** function.

    ```cpp
    static napi_value loadModule(napi_env env, napi_callback_info info) {
        napi_value result;
        // 1. Call napi_load_module_with_info to load json5.
        napi_status status = napi_load_module_with_info(env, "json5", "com.example.application/entry", &result);

        napi_value key;
        std::string keyStr = "default";
        napi_create_string_utf8(env, keyStr.c_str(), keyStr.size(), &key);
        // 2. Call napi_get_property to obtain the default object.
        napi_value defaultValue;
        napi_get_property(env, result, key, &defaultValue);

        napi_value stringifyFn;
        // 3. Call napi_get_named_property to obtain the stringify function.
        napi_get_named_property(env, defaultValue, "stringify", &stringifyFn);
        // 4. Call napi_call_function to invoke the stringify function.
        napi_value argStr;
        std::string text = "call json5 stringify";
        napi_create_string_utf8(env, text.c_str(), text.size(), &argStr);
        napi_value args[1] = {argStr};

        napi_value returnValue;
        napi_call_function(env, defaultValue, stringifyFn, 1, args, &returnValue);
        return result;
    }
    ```

- **Loading an API module**

```cpp
static napi_value loadModule(napi_env env, napi_callback_info info) {
    // 1. Call napi_load_module_with_info to load the @ohos.hilog module.
    napi_value result;
    napi_status status = napi_load_module_with_info(env, "@ohos.hilog", nullptr, &result);
    
    // 2. Call napi_get_named_property to obtain the info function.
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
    // 3. Call napi_call_function to invoke the info function.
    napi_call_function(env, result, infoFn, 3, args, nullptr);
    return result;
}
```

- **Loading a native library**

The **index.d.ts** file of **libentry.so** is as follows:

```javascript
// index.d.ts
export const add: (a: number, b: number) => number;
```

1. Configure **dependencies** in the **oh-package.json5** file.

    ```json
    {
        "dependencies": {
            "libentry.so": "file:../src/main/cpp/types/libentry"
        }
    }
    ```

2. Configure **build-profile.json5** for the module that uses **libentry.so**.

    ```json
    {
        "buildOption" : {
            "arkOptions" : {
                "runtimeOnly" : {
                    "packages": [
                        "libentry.so"
                    ]
                }
            }
        }
    }
    ```

3. Call **napi_load_module_with_info** to load **libentry.so** and call the **add** function.

    ```cpp
    static napi_value loadModule(napi_env env, napi_callback_info info) {
        napi_value result;
        // 1. Call napi_load_module_with_info to load libentry.so.
        napi_status status = napi_load_module_with_info(env, "libentry.so", "com.example.application/entry", &result);

        napi_value addFn;
        // 2. Call napi_get_named_property to obtain the add function.
        napi_get_named_property(env, result, "add", &addFn);
        
        napi_value a;
        napi_value b;
        napi_create_int32(env, 2, &a);
        napi_create_int32(env, 3, &b);
        napi_value args[2] = {a, b};
        // 3. Call napi_call_function to invoke the add function.
        napi_value returnValue;
        napi_call_function(env, result, addFn, 2, args, &returnValue);
        return result;
    }
    ```

- **Loading another HAR module to a HAR**

For example, load **har2** to **har1**. The **Index.ets** file of **har2** is as follows:

```javascript
//har2 Index.ets
let value = 123;
function test() {
  console.log("Hello OpenHarmony");
}
export {value, test};
```

1. Configure **dependencies** in the **oh-package.json5** file in **har1**.

    ```json
    {
        "dependencies": {
            "har2": "file:../har2"
        }
    }
    ```

2. Configure the **build-profile.json5** file for **har1**.

    ```json
    {
        "buildOption" : {
            "arkOptions" : {
                "runtimeOnly" : {
                    "packages": [
                        "har2"
                    ]
                }
            }
        }
    }
    ```

3. Call **napi_load_module_with_info** to load **har2** to **har1**, call the **test** function, and obtain the variable value.

    ```cpp
    static napi_value loadModule(napi_env env, napi_callback_info info) {
        napi_value result;
        // 1. Call napi_load_module_with_info to load har2. Note that moduleName is that of the HAP where the module is located.
        napi_status status = napi_load_module_with_info(env, "har2", "com.example.application/entry", &result);

        napi_value testFn;
        // 2. Call napi_get_named_property to obtain the test function.
        napi_get_named_property(env, result, "test", &testFn);
        // 3. Call napi_call_function to invoke the test function.
        napi_call_function(env, result, testFn, 0, nullptr, nullptr);

        napi_value value;
        napi_value key;
        std::string keyStr = "value";
        napi_create_string_utf8(env, keyStr.c_str(), keyStr.size(), &key);
        // 4. Call napi_get_property to obtain a variable value.
        napi_get_property(env, result, key, &value);
        return result;
    }
    ```
