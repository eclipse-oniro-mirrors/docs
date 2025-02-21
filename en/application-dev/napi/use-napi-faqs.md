# Node-API FAQs

## What should I do when "undefined/not callable" is reported for an API of a module imported from a .so file?

1. Check whether the module name in the .cpp file used in module registration is the same as that in the .so file name.
   
   If the module name is **entry**, the .so file name must be **libentry.so**, and the **nm_modname** field in **napi_module** must be **entry**. The module names must be of the same case.
   
2. Check whether the .so file is successfully loaded.

   Check the log related to module loading during the application startup. Search for the keyword "dlopen" and check for error information. Possible causes include the following:

   - The file to be loaded does not exist or is in a blocklist.
   - The application does not have the required permission. 
   - The **nm_modname** value does not match the module name in multi-thread scenarios (such as worker threads and taskpool). The module names must be of the same case.

3. Check whether the dependency .so files are successfully loaded.

   Check that all the dependency .so files are packaged into the application and the application has the permission to open them.

4. Check whether the module import mode matches the .so file path.

   If the module is imported by using **import xxx from '\@ohos.yyy.zzz'**, you may find **libzzz.z.so** or **libzzz_napi.z.so** in **/system/lib/module/yyy** (for a 32-bit system) or **/system/lib64/module/yyy** (for a 64-bit system). If the .so file does not exist or the file names do not match, an error containing the keyword "dlopen" will be reported.

    

| **Error Log**| **Solution**|
| -------- | -------- |
| module $SO is not allowed to load in restricted runtime | The module, identified by **$SO**, is not allowed for the worker thread running in a restricted environment and cannot be loaded. You are advised to delete the module.|
| module $SO is in blocklist, loading prohibited | The module, identified by **$SO**, is in a blocklist due to the control of the widget or Extension, and cannot be loaded. You are advised to delete the module. |
| load module failed. $ERRMSG | The dynamic library fails to be loaded. **$ERRMSG** indicates the cause of the loading failure. Possible causes include the following:<br>- The .so file to be loaded does not exist.<br>- The dependency .so file does not exist. <br>- Undefined symbol is found. <br>Locate the cause based on the error message.|
| try to load abc file from $FILEPATH failed. | You can load either a dynamic library or an .abc file. If this log information is displayed when you attempt to load a dynamic library, ignore this message. If it is displayed when you attempt to load an .abc file, the .abc file does not exist. **$FILEPATH** indicates the module path. |

## What should I do when an unexpected value is returned by an API and "occur exception need return" is reported?

Before the call is complete, some Node-API interfaces are checked for JavaScript (JS) exceptions in the VM. If an exception is detected, "occur exception need return" will be reported, with the line number of the code and the Node-API interface name.

You can solve this problem as follows:

- If the exception does not matter, clear the exception.
  
  Call **napi_get_and_clear_last_exception** before "occur exception need return" is printed to clear the exception.
  
- Throw the exception to the ArkTS layer for capture.

  Throw the exception directly to the ArkTS layer without going through the native logic.

## What are the differences between the lifecycle of napi_value and napi_ref?

- **native_value** is managed by **HandleScope**. Generally, you do not need to add **HandleScope** for **native_value** (except for **complete callback** of **uv_queue_work**).

- **napi_ref** must be deleted manually.

## How do I locate the fault if the return value of a Node-API interface is not "napi_ok"?

When a Node-API interface is successfully executed, **napi_ok** is returned. If the return value is not **napi_ok**, locate the fault as follows:

- Check the result of the input parameter null check, which is performed first before a Node-API interface is executed. The code is as follows:

  ```cpp
  CHECK_ENV: null check for env.
  CHECK_ARG: null check for other input parameters.
  ```

- Check the result of the input parameter type check, which is performed for certain Node-API interfaces. For example, **napi_get_value_double** is used to obtain a C double value from a JS number, and the type of the JS value passed in must be number. The parameter type check is as follows:

  ```cpp
  RETURN_STATUS_IF_FALSE(env, nativeValue->TypeOf() == NATIVE_NUMBER, napi_number_expected);
  ```

- Check the return value, which contains the verification result of certain interfaces. For example, **napi_call_function** is used to execute a JS function. If an exception occurs in the JS function, Node-API returns **napi_pending_exception**.

  ```cpp
  auto resultValue = engine->CallFunction(nativeRecv, nativeFunc, nativeArgv, argc);
  RETURN_STATUS_IF_FALSE(env, resultValue != nullptr, napi_pending_exception)
  ```

- Determine the status value returned, and analyze the situation in which the status value is returned.
