# JSVM-API Data Types and APIs

## Data Types

### JSVM_Status

Enum indicating the execution status of a JSVM-API call.

Each time a JSVM-API function is called, a value of **JSVM_Status** is returned indicating the execution result.

```c++
typedef enum {
    JSVM_OK,
    JSVM_INVALID_ARG,
    JSVM_OBJECT_EXPECTED,
    JSVM_STRING_EXPECTED,
    JSVM_NAME_EXPECTED,
    JSVM_FUNCTION_EXPECTED,
    JSVM_NUMBER_EXPECTED,
    JSVM_BOOL_EXPECTED,
    JSVM_ARRAY_EXPECTED,
    JSVM_GENERIC_FAILURE,
    JSVM_PENDING_EXCEPTION,
    JSVM_CENCELLED,
    JSVM_ESCAPE_CALLED_TWICE,
    JSVM_HANDLE_SCOPE_MISMATCH,
    JSVM_CALLBACK_SCOPE_MISMATCH,
    JSVM_QUEUE_FULL,
    JSVM_CLOSING,
    JSVM_BIGINT_EXPECTED,
    JSVM_DATA_EXPECTED,
    JSVM_CALLBACK_SCOPE_MISMATCH,
    JSVM_DETACHABLE_ARRAYBUFFER_EXPECTED,
    JSVM_WOULD_DEADLOCK,  /* unused */
    JSVM_NO_EXTERNAL_BUFFERS_ALLOWED,
    JSVM_CANNOT_RUN_JS
} JSVM_Status;
```

### JSVM_ExtendedErrorInfo

Struct that holds detailed error information when a JSVM-API call fails.

```c++
typedef struct {
    const char* errorMessage;
    void* engineReserved;
    uint32_t engineErrorCode;
    JSVM_Status errorCode;
} JSVM_ExtendedErrorInfo;
```

### JSVM_Value

Pointer used to represent a JavaScript (JS) value.

### JSVM_Env

- Context used by the underlying JSVM-API implementation. It is passed to the native functions when they are invoked, and must be passed back when JSVM-API calls are made.

- When a native addon exits, **JSVM_Env** becomes invalid and this event is passed to **OH_JSVM_SetInstanceData** via a callback.

- Avoid caching **JSVM_Env** or passing **JSVM_Env** between different worker threads.

- If **JSVM_Env** is shared between different threads, the **threadlocal** variable must be isolated across threads. For this purpose, close the env scope of the current thread before switching to another thread and open a new env scope in each thread switched to.

### JSVM_ValueType

Enum indicating the type of **JSVM_Value**. The **JSVM_Value** types include the types defined in ECMAScript. **JSVM_EXTERNAL** indicates an external data type.

```c++
typedef enum {
    JSVM_UNDEFINED,
    JSVM_NULL,
    JSVM_BOOLEAN,
    JSVM_NUMBER,
    JSVM_STRING,
    JSVM_SYMBOL,
    JSVM_OBJECT,
    JSVM_FUNCTION,
    JSVM_EXTERNAL,
    JSVM_BIGINT,
} JSVM_ValueType;
```

### JSVM_TypedarrayType

Enum indicating the data type of the binary **TypedArray** object.

```c++
typedef enum {
    JSVM_INT8_ARRAY,
    JSVM_UINT8_ARRAY,
    JSVM_UINT8_CLAMPED_ARRAY,
    JSVM_INT16_ARRAY,
    JAVM_UINT16_ARRAY,
    JSVM_INT32_ARRAY,
    JSVM_UINT32_ARRAY,
    JSVM_FLOAT32_ARRAY,
    JSVM_FLOAT64_ARRAY,
    JSVM_BIGINT64_ARRAY,
    JSVM_BIGUINT64_ARRAY,
} JSVM_TypedarrayType;
```

### Memory Management Types

JSVM-API provides the following memory management types:

**JSVM_HandleScope**

Data used to manage the lifecycle of JS objects. It allows JS objects to remain active within a certain range for use in JS code. When **JSVM_HandleScope** is created, all JS objects created in this range remain active until the end. This can prevent released objects from being used in JS code, which improves code reliability and performance.

**JSVM_EscapableHandleScope**

- It is created by **OH_JSVM_OpenEscapableHandleScope** and closed by **OH_JSVM_CloseEscapableHandleScope**.

- It is a special type of handle range used to return values created within the scope of **JSVM_EscapableHandleScope** to a parent scope.

- You can use **OH_JSVM_EscapeHandle** to promote **JSVM_EscapableHandleScope** to a JS object so that it is valid for the lifetime of the outer scope.

**JSVM_Ref**

Reference to **JSVM_Value**, which allows you to manage the lifecycle of JS values.

**JSVM_TypeTag**

Struct containing two unsigned 64-bit integers to identify the type of a JSVM-API value.

```c++
typedef struct {
    uint64_t lower;
    uint64_t upper;
} JSVM_TypeTag;
```

- It is a 128-bit value stored as two unsigned 64-bit integers. It is used to tag JS objects to ensure that they are of a certain type.

- This is a stronger check than **OH_JSVM_Instanceof** because **OH_JSVM_Instanceof** may report a false positive if the object's prototype is manipulated.

- The combination of **JSVM_TypeTag** and **OH_JSVM_Wrap** is useful because it ensures that the pointer retrieved from a wrapped object can be safely converted to the native type corresponding to the type tag that had been previously applied to the JS object.

### Callback Types

JSVM-API provides the following callback types:

**JSVM_CallbackInfo**

User-defined native function, which is exposed to JS via JSVM-API. Generally, no handle or callback scope is created inside this callback.

**JSVM_CallbackStruct**

Function pointer type and data for user-provided native functions, which are to be exposed to JS via JSVM-API.

```c++
typedef struct {
  JSVM_Value(*callback)(JSVM_Env env, JSVM_CallbackInfo info);
  void* data;
} JSVM_CallbackStruct;
```

**JSVM_Callback**

User-defined native function exposed to JS. Unless otherwise required in object lifecycle management, no handle or callback scope is created in this callback.

The usage is as follows:

```c++
typedef JSVM_CallbackStruct* JSVM_Callback;
```

**JSVM_Finalize**

Function pointer, which is passed in APIs such as **OH_JSVM_SetInstanceData**, **OH_JSVM_CreateExternal**, and **OH_JSVM_Wrap**. **JSVM_Finalize** is called to release the native object when a JS object is garbage collected.

The format is as follows:

```c++
typedef void (JSVM_Finalize)(JSVM_Env env, void finalizeData, void* finalizeHint);
```

## APIs

JSVM-API provides capabilities of the standard JS engine. JSVM-API can be dynamically linked to JS engine libraries of different versions to shield the differences between engine interfaces. JSVM-API provides capabilities, such as VM lifecycle management, JS context management, JS code execution, JS/C++ interaction, context snapshot management, and code caching. Read on the following for details.

### Creating a VM Instance and JS Context

#### When to Use

Before executing JS code, you need to create a JS VM and JS context.

#### Available APIs
| API| Description|
| -------- | -------- |
| OH_JSVM_Init| Initializes a JS engine instance.|
| OH_JSVM_CreateVM| Creates a JS VM instance.|
| OH_JSVM_DestroyVM| Destroys a JS VM instance.|
| OH_JSVM_OpenVMScope| Opens a VM scope. The VM instance can be used only within the scope and will not be garbage-collected until the scope is closed.|
| OH_JSVM_CloseVMScope| Closes a VM scope.|
| OH_JSVM_CreateEnv| Creates a JS context and registers the specified native function.|
| OH_JSVM_DestroyEnv| Destroys a JS context.|
| OH_JSVM_OpenEnvScope| Opens a JS context scope. The context can be used only within the scope.|
| OH_JSVM_CloseEnvScope| Closes a JS context scope.|
| OH_JSVM_OpenHandleScope| Opens a handle scope. **JSVM_Value** within the scope will not be garbage-collected.|
| OH_JSVM_CloseHandleScope| Close a handle scope.|

Example:
Create a JS VM instance and then destroy it.

```c++
bool VM_INIT = false;

static JSVM_Value ConsoleInfo(JSVM_Env env, JSVM_CallbackInfo info) {
    size_t argc = 1;
    JSVM_Value args[1];
    char log[256] = "";
    size_t logLength;
    OH_JSVM_GetCbInfo(env, info, &argc, args, NULL, NULL);

    OH_JSVM_GetValueStringUtf8(env, args[0], log, 255, &logLength);
    log[255] = 0;
    OH_LOG_INFO(LOG_APP, "JSVM API TEST: %{public}s", log);
    return nullptr;
}

static JSVM_Value Add(JSVM_Env env, JSVM_CallbackInfo info) {
    size_t argc = 2;
    JSVM_Value args[2];
    OH_JSVM_GetCbInfo(env, info, &argc, args, NULL, NULL);
    double num1, num2;
    env, OH_JSVM_GetValueDouble(env, args[0], &num1);
    OH_JSVM_GetValueDouble(env, args[1], &num2);
    JSVM_Value sum = nullptr;
    OH_JSVM_CreateDouble(env, num1 + num2, &sum);
    return sum;
}

static napi_value MyJSVMDemo([[maybe_unused]] napi_env _env, [[maybe_unused]] napi_callback_info _info) {
    std::thread t([]() {
        if (!VM_INIT) {
            // The JSVM only needs to be initialized once.
            JSVM_InitOptions initOptions;
            memset(&initOptions, 0, sizeof(initOptions));
            OH_JSVM_Init(&initOptions);
            VM_INIT = true;
        }
        // Create a VM instance and open the VM scope.
        JSVM_VM vm;
        JSVM_CreateVMOptions options;
        memset(&options, 0, sizeof(options));
        OH_JSVM_CreateVM(&options, &vm);

        JSVM_VMScope vmScope;
        OH_JSVM_OpenVMScope(vm, &vmScope);

        JSVM_CallbackStruct param[] = {
            {.data = nullptr, .callback = ConsoleInfo},
            {.data = nullptr, .callback = Add},
        };
        JSVM_PropertyDescriptor descriptor[] = {
            {"consoleinfo", NULL, &param[0], NULL, NULL, NULL, JSVM_DEFAULT},
            {"add", NULL, &param[1], NULL, NULL, NULL, JSVM_DEFAULT},
        };
        // Create env, register a native method, and open an env scope.
        JSVM_Env env;
        OH_JSVM_CreateEnv(vm, sizeof(descriptor) / sizeof(descriptor[0]), descriptor, &env);

        JSVM_EnvScope envScope;
        OH_JSVM_OpenEnvScope(env, &envScope);

        // Open a handle scope.
        JSVM_HandleScope handleScope;
        OH_JSVM_OpenHandleScope(env, &handleScope);

        std::string sourceCodeStr = "\
{\
let value = add(4.96, 5.28);\
consoleinfo('Result is:' + value);\
}\
";
        // Compile the JS script.
        JSVM_Value sourceCodeValue;
        OH_JSVM_CreateStringUtf8(env, sourceCodeStr.c_str(), sourceCodeStr.size(), &sourceCodeValue);
        JSVM_Script script;
        OH_JSVM_CompileScript(env, sourceCodeValue, nullptr, 0, true, nullptr, &script);
        JSVM_Value result;
        // Run the JS script.
        OH_JSVM_RunScript(env, script, &result);
        JSVM_ValueType type;
        OH_JSVM_Typeof(env, result, &type);
        OH_LOG_INFO(LOG_APP, "JSVM API TEST type: %{public}d", type);

        // Exit the VM and release the memory.
        OH_JSVM_CloseHandleScope(env, handleScope);

        OH_JSVM_CloseEnvScope(env, envScope);
        OH_JSVM_DestroyEnv(env);

        OH_JSVM_CloseVMScope(vm, vmScope);
        OH_JSVM_DestroyVM(vm);
    });

    t.detach();

    return nullptr;
}
```

### Compiling and Running JS Code

#### When to Use

Compile and run JS code.

#### Available APIs
| API| Description|
| -------- | -------- |
| OH_JSVM_CompileScript| Compiles JS code and returns the compiled script bound to the current environment.|
| OH_JSVM_CreateCodeCache| Creates a code cache for the compiled script.|
| OH_JSVM_RunScript| Runs a JS script.|

Example:
Compile and run JS code (create a VM, register native functions, execute JS code, and destroy the VM).

```c++
#include <cstring>
#include <fstream>
#include <string>
#include <vector>

// Add the dependency libjsvm.so.
#include "ark_runtime/jsvm.h"

using namespace std;

static JSVM_Value Hello(JSVM_Env env, JSVM_CallbackInfo info) {
    JSVM_Value output;
    void* data = nullptr;
    OH_JSVM_GetCbInfo(env, info, nullptr, nullptr, nullptr, &data);
    OH_JSVM_CreateStringUtf8(env, (char*)data, strlen((char*)data), &output);
    return output;
}

static JSVM_CallbackStruct hello_cb = { Hello, (void*)"Hello" };

static string srcGlobal = R"JS(
const concat = (...args) => args.reduce((a, b) => a + b);
)JS";

static void RunScript(JSVM_Env env, string& src,
                       const uint8_t** dataPtr = nullptr,
                       size_t* lengthPtr = nullptr) {
    JSVM_HandleScope handleScope;
    OH_JSVM_OpenHandleScope(env, &handleScope);

    JSVM_Value jsSrc;
    OH_JSVM_CreateStringUtf8(env, src.c_str(), src.size(), &jsSrc);

    const uint8_t* data = dataPtr ? *dataPtr : nullptr;
    size_t length = lengthPtr ? *lengthPtr : 0;
    bool cacheRejected = true;
    JSVM_Script script;
    // Compile the JS code.
    OH_JSVM_CompileScript(env, jsSrc, data, length, true, &cacheRejected, &script);
    printf("Code cache is %s\n", cacheRejected ? "rejected" : "used");

    JSVM_Value result;
    // Run the JS code.
    OH_JSVM_RunScript(env, script, &result);

    char resultStr[128];
    size_t size;
    OH_JSVM_GetValueStringUtf8(env, result, resultStr, 128, &size);
    printf("%s\n", resultStr);
    if (dataPtr && lengthPtr && *dataPtr == nullptr) {
        // Save the script compiled from the JS source code to the cache to avoid repeated compilation and improve performance.
        OH_JSVM_CreateCodeCache(env, script, dataPtr, lengthPtr);
        printf("Code cache created with length = %ld\n", *lengthPtr);
    }

    OH_JSVM_CloseHandleScope(env, handleScope);
}

static void CreateSnapshot() {
    JSVM_VM vm;
    JSVM_CreateVMOptions options;
    memset(&options, 0, sizeof(options));
    options.isForSnapshotting = true;
    OH_JSVM_CreateVM(&options, &vm);
    JSVM_VMScope vmScope;
    OH_JSVM_OpenVMScope(vm, &vmScope);

    JSVM_Env env;
    // Register the native function as a method that can be called by a JS API. hello_cb holds the pointer and parameters of the native function.
    JSVM_PropertyDescriptor descriptors[] = {
        { "hello", NULL, &hello_cb, NULL, NULL, NULL, JSVM_DEFAULT }
    };
    OH_JSVM_CreateEnv(vm, 1, descriptors, &env);

    JSVM_EnvScope envScope;
    OH_JSVM_OpenEnvScope(env, &envScope);
    // Execute the JS source code src, which can contain any JS syntax. The registered native function can also be invoked.
    string src = srcGlobal + "concat(hello(), ', ', 'World from CreateSnapshot!');";
    RunScript(env, src);

    // Create a snapshot and save the current env to a string. The string can be used to restore the env to avoid repeatedly defining the properties in the env.
    const char* blobData = nullptr;
    size_t blobSize = 0;
    JSVM_Env envs[1] = { env };
    OH_JSVM_CreateSnapshot(vm, 1, envs, &blobData, &blobSize);
    printf("Snapshot blob size = %ld\n", blobSize);

    // If you need to save the snapshot to a file, also consider the read/write permissions on the file in the application.
    ofstream file("/data/storage/el2/base/files/blob.bin", ios::out | ios::binary | ios::trunc);
    file.write(blobData, blobSize);
    file.close();

    OH_JSVM_CloseEnvScope(env, envScope);
    OH_JSVM_DestroyEnv(env);
    OH_JSVM_CloseVMScope(vm, vmScope);
    OH_JSVM_DestroyVM(vm);
}

void RunWithoutSnapshot(const uint8_t** dataPtr, size_t* lengthPtr) {
    // Create a VM instance.
    JSVM_VM vm;
    OH_JSVM_CreateVM(nullptr, &vm);
    JSVM_VMScope vmScope;
    OH_JSVM_OpenVMScope(vm, &vmScope);

    JSVM_Env env;
    // Register the native function as a method that can be called by a JS API. hello_cb holds the pointer and parameters of the native function.
    JSVM_PropertyDescriptor descriptors[] = {
        { "hello", NULL, &hello_cb, NULL, NULL, NULL, JSVM_DEFAULT }
    };
    OH_JSVM_CreateEnv(vm, 1, descriptors, &env);
    JSVM_EnvScope envScope;
    OH_JSVM_OpenEnvScope(env, &envScope);
    // Execute the JS source code src, which can contain any JS syntax. The registered native function can also be invoked.
    auto src = srcGlobal + "concat(hello(), ', ', 'World', ' from RunWithoutSnapshot!')";
    RunScript(env, src, dataPtr, lengthPtr);

    OH_JSVM_CloseEnvScope(env, envScope);
    OH_JSVM_DestroyEnv(env);
    OH_JSVM_CloseVMScope(vm, vmScope);
    OH_JSVM_DestroyVM(vm);
}

void RunWithSnapshot(const uint8_t **dataPtr, size_t *lengthPtr) {
    // The lifetime of blobData must not be shorter than that of the vm.
    // If the snapshot needs to be read from a file, also consider the read/write permissions on the file in the application.
    vector<char> blobData;
    ifstream file("/data/storage/el2/base/files/blob.bin", ios::in | ios::binary | ios::ate);
    size_t blobSize = file.tellg();
    blobData.resize(blobSize);
    file.seekg(0, ios::beg);
    file.read(blobData.data(), blobSize);
    file.close();

    // Create a VM instance.
    JSVM_VM vm;
    JSVM_CreateVMOptions options;
    memset(&options, 0, sizeof(options));
    options.snapshotBlobData = blobData.data();
    options.snapshotBlobSize = blobSize;
    OH_JSVM_CreateVM(&options, &vm);
    JSVM_VMScope vmScope;
    OH_JSVM_OpenVMScope(vm, &vmScope);

    // Create env from a snapshot.
    JSVM_Env env;
    OH_JSVM_CreateEnvFromSnapshot(vm, 0, &env);
    JSVM_EnvScope envScope;
    OH_JSVM_OpenEnvScope(env, &envScope);

    // Run the JS script. Because the snapshot contains hello() defined in env, you do not need to redefine hello(). If dataPtr contains the compiled JS script, the JS script can be directly executed, which avoids repeated compilation from the source code.
    string src = "concat(hello(), ', ', 'World', ' from RunWithSnapshot!')";
    RunScript(env, src, dataPtr, lengthPtr);

    OH_JSVM_CloseEnvScope(env, envScope);
    OH_JSVM_DestroyEnv(env);
    OH_JSVM_CloseVMScope(vm, vmScope);
    OH_JSVM_DestroyVM(vm);
}

void PrintVmInfo() {
    JSVM_VMInfo vmInfo;
    OH_JSVM_GetVMInfo(&vmInfo);
    printf("apiVersion: %d\n", vmInfo.apiVersion);
    printf("engine: %s\n", vmInfo.engine);
    printf("version: %s\n", vmInfo.version);
    printf("cachedDataVersionTag: 0x%x\n", vmInfo.cachedDataVersionTag);
}

static intptr_t externals[] = {
    (intptr_t)&hello_cb,
    0,
};

int main(int argc, char *argv[]) {
    if (argc <= 1) {
        printf("Usage: %s gen-snapshot|use-snapshot|no-snapshot\n", argv[0]);
        return 0;
    }

    JSVM_InitOptions initOptions;
    memset(&initOptions, 0, sizeof(initOptions));
    initOptions.externalReferences = externals;
    // Initialize the VM, which can be initialized only once in a process.
    OH_JSVM_Init(&initOptions);
    PrintVmInfo();

    if (argv[1] == string("gen-snapshot")) {
        CreateSnapshot();
        return 0;
    }

    // The snapshot records the JS context at a certain time and can be used to quickly restore JS context across processes as long as the snapshot is within the lifecycle.
    const auto useSnapshot = argv[1] == string("use-snapshot");
    const auto run = useSnapshot ? RunWithSnapshot : RunWithoutSnapshot;
    const uint8_t* data = nullptr;
    size_t length = 0;
    run(&data, &length);
    run(&data, &length);
    delete[] data;

    return 0;
}
```

### Exception Handling

#### When to Use

Capture, throw, and clear JS exceptions as required.

#### Available APIs
| API| Description|
| -------- | -------- |
| OH_JSVM_Throw| Throws a JS value.|
| OH_JSVM_ThrowTypeError| Throws a JS type error.|
| OH_JSVM_ThrowRangeError| Throws a JS range error.|
| OH_JSVM_IsError| Checks whether a JS value indicates an error.|
| OH_JSVM_CreateError| Creates a JS error.|
| OH_JSVM_CreateTypeError| Creates a JS type error and returns it.|
| OH_JSVM_CreateRangeError| Creates a JS range error and returns it.|
| OH_JSVM_ThrowError| Throws a JS exception.|
| OH_JSVM_GetAndClearLastException| Obtains and clears the last JS exception.|
| OH_JSVM_IsExceptionPending| Checks whether an exception occurs.|
| OH_JSVM_GetLastErrorInfo| Obtains information about the last exception.|
| OH_JSVM_ThrowSyntaxError| Throws a JS syntax error.|
| OH_JSVM_CreateSyntaxError| Creates a JS syntax error and returns it.|

Example:
The following walks you through on how to Create, judge, and throw a JS type error.

```c++
JSVM_Value code = nullptr;
JSVM_Value message = nullptr;
OH_JSVM_CreateStringUtf8(env, "500", JSVM_AUTO_LENGTH, &code);
OH_JSVM_CreateStringUtf8(env, "type error 500", JSVM_AUTO_LENGTH, &message);
JSVM_Value error = nullptr;
OH_JSVM_CreateTypeError(env, code, message, &error);
bool isError = false;
OH_JSVM_IsError(env, error, &isError);
OH_JSVM_ThrowTypeError(env, nullptr, "type error1");
```

Call OH_JSVM_GetAndClearLastException to log the exception information as a string to the console.

```c++
if (status != JSVM_OK) // An exception occurs when the execution fails.
{
    bool isPending = false;
    if (JSVM_OK == OH_JSVM_IsExceptionPending((env), &isPending) && isPending)
    {
        JSVM_Value error;
        if (JSVM_OK == OH_JSVM_GetAndClearLastException((env), &error))
        {
            // Obtain the exception stack.
            JSVM_Value stack;
            OH_JSVM_GetNamedProperty((env), error, "stack", &stack);

            JSVM_Value message;
            OH_JSVM_GetNamedProperty((env), error, "message", &message);

            char stackstr[256];
            OH_JSVM_GetValueStringUtf8(env, stack, stackstr, 256, nullptr);
            OH_LOG_INFO(LOG_APP, "JSVM error stack: %{public}s", stackstr);

            char messagestr[256];
            OH_JSVM_GetValueStringUtf8(env, message, messagestr, 256, nullptr);
            OH_LOG_INFO(LOG_APP, "JSVM error message: %{public}s", messagestr);
        }
    }
}
```

### Object Lifetime Management

When JSVM-API calls are made, handles to objects in the heap for the underlying VM may be returned as **JSVM_Value**s. These handles must hold the objects live until they are no longer required by the native code. Otherwise, the objects will be collected. 

 When an object handle is returned, it is associated with a scope. The lifecycle of the default scope is tied to the lifecycle of the native method call. By default, a handle remains valid and the object associated with it will be held live for the lifecycle of the native method call.

However, in many cases, you may need to adjust the lifecycle to be shorter or longer than that of the native method. The following describes the JSVM-API methods that can be used to change the lifecycle of a handle.

#### Available APIs
| API| Description|
| -------- | -------- |
| OH_JSVM_OpenHandleScope| Opens a handle scope. The object within the scope will not be garbage-collected until the handle scope is closed.|
| OH_JSVM_CloseHandleScope| Closes a handle scope. The object within the scope will be garbage-collected after the handle scope is closed.|
| OH_JSVM_OpenEscapableHandleScope| Opens an escapable handle scope. Before this scope is closed, the object created within the scope has the same lifecycle as its parent scope.|
| OH_JSVM_CloseEscapableHandleScope| Closes an escapable handle scope.|
| OH_JSVM_EscapeHandle| Promotes a handle to a JS object so that it is valid for the lifetime of the outer scope.|
| OH_JSVM_CreateReference| Creates a new reference with the specified reference count to the value passed in. The reference allows objects to be used and shared in different contexts and effectively tracks the lifecycle of the object.|
| OH_JSVM_DeleteReference| Release the reference created by **OH_JSVM_CreateReference**. This allows objects to be correctly released and reclaimed when they are no longer required, avoiding memory leaks.|
| OH_JSVM_ReferenceRef| Increments the reference count of the reference created by **OH_JSVM_CreateReference** so that the object referenced will not be released.|
| OH_JSVM_ReferenceUnref| Decrements the reference count of the reference created by **OH_JSVM_CreateReference** so that the object can be correctly released and reclaimed when it is not referenced.|
| OH_JSVM_GetReferenceValue| Obtains the object referenced by **OH_JSVM_CreateReference**.|

Example:
Use a handle scope to protect an object created within the scope from being reclaimed.

```c++
JSVM_HandleScope scope;
OH_JSVM_OpenHandleScope(env, &scope);
JSVM_Value obj = nullptr;
OH_JSVM_CreateObject(env, &obj);
OH_JSVM_CloseHandleScope(env, scope);
```  

Use an escapable handle scope to protect an object from being reclaimed within its parent scope.

```c++
JSVM_EscapableHandleScope scope;
JSVM_CALL(env, OH_JSVM_OpenEscapableHandleScope(env, &scope));
JSVM_Value output = NULL;
JSVM_Value escapee = NULL;
JSVM_CALL(env, OH_JSVM_CreateObject(env, &output));
JSVM_CALL(env, OH_JSVM_EscapeHandle(env, scope, output, &escapee));
JSVM_CALL(env, OH_JSVM_CloseEscapableHandleScope(env, scope));
return escapee;
```

Reference a JS object and release the reference.

```c++
JSVM_Value obj = nullptr;
OH_JSVM_CreateObject(env, &obj);
// Create a reference.
JSVM_Ref reference;
OH_JSVM_CreateReference(env, obj, 1, &reference);

// Create a reference with a JS object.
JSVM_Value result;
OH_JSVM_GetReferenceValue(env, reference, &result);

// Release the reference.
OH_JSVM_DeleteReference(env, reference);
```

### Creating JS Object Types and Basic Types

#### When to Use

Create JS object types and basic types.

#### Available APIs
| API| Description|
| -------- | -------- |
|OH_JSVM_CreateArray | Creates a JS array object.|
|OH_JSVM_CreateArrayWithLength | Creates a JS array object of the specified length.|
|OH_JSVM_CreateArraybuffer | Creates an ArrayBuffer object of the specified size.|
|OH_JSVM_CreateDate | Creates a date object representing the given number of milliseconds.|
|OH_JSVM_CreateExternal | Creates a JS object that wraps an external pointer.|
|OH_JSVM_CreateExternalArraybuffer | Creates a JS object that wraps an external Arraybuffer.|
|OH_JSVM_CreateObject | Creates a default JS object.|
|OH_JSVM_CreateSymbol | Creates a symbol object based on the given descriptor.|
|OH_JSVM_SymbolFor | Searches for a symbol with the given key in a global (runtime-wide) symbol registry. If a match is found, the symbol will be returned. Otherwise, a symbol will be created in the registry.|
|OH_JSVM_CreateTypedarray | Creates a JS TypedArray object for an ArrayBuffer. The TypedArray object provides an array-like view over an underlying data buffer, where each element has the same underlying binary scalar data type.|
|OH_JSVM_CreateDataview | Creates a JS DataView object for an ArrayBuffer. The DataView object provides an array-like view of over an underlying data buffer.|
|OH_JSVM_CreateInt32 | Creates a JS number object from a C Int32_t object.|
|OH_JSVM_CreateUint32 | Creates a JS number object from a C Uint32_t object.|
|OH_JSVM_CreateInt64 | Creates a JS number object from a C Int64_t object.|
|OH_JSVM_CreateDouble | Creates a JS number object from a C Double object.|
|OH_JSVM_CreateBigintInt64 | Creates a JS BigInt object from a C Int64 object.| 
|OH_JSVM_CreateBigintUint64 | Creates a JS BigInt object from a C Uint64 object.|
|OH_JSVM_CreateBigintWords | Creates a JS BigInt object from a C Uint64_t array.|
|OH_JSVM_CreateStringLatin1 | Creates a JS string object from an ISO-8859-1-encoded C string. ISO-8859-1 is also referred to as Latin-1.|
|OH_JSVM_CreateStringUtf16 | Creates a JS string object from a UTF16-encoded C string.|
|OH_JSVM_CreateStringUtf8 | Creates a JS string object from a UTF8-encoded C string.|

Example:
Create a JS array of the specified length.

```c++
size_t arrayLength = 2;
JSVM_Value arr;

OH_JSVM_CreateArrayWithLength(env, arrayLength, &arr);
for (uint32_t i = 0; i < arrayLength; i++)
{
    JSVM_Value element;
    OH_JSVM_CreateUint32(env, i * 2, &element);
    OH_JSVM_SetElement(env, arr, i, element);
}
```

Create a JS Int32Array.

```c++
JSVM_Value arrayBuffer = nullptr;
void *arrayBufferPtr = nullptr;
size_t arrayBufferSize = 16;
size_t typedArrayLength = 4;
OH_JSVM_CreateArraybuffer(env, arrayBufferSize, &arrayBufferPtr, &arrayBuffer);

void *tmpArrayBufferPtr = nullptr;
size_t arrayBufferLength = 0;
OH_JSVM_GetArraybufferInfo(env, arrayBuffer, &tmpArrayBufferPtr, &arrayBufferLength);

JSVM_Value result;
OH_JSVM_CreateTypedarray(env, JSVM_TypedarrayType::JSVM_INT32_ARRAY, typedArrayLength, arrayBuffer, 0, &result);
return result;
```

Create JS numbers and strings.

```c++
const char *testStringStr = "test";
JSVM_Value testString = nullptr;
OH_JSVM_CreateStringUtf8(env, testStringStr, strlen(testStringStr), &testString);

JSVM_Value testNumber1 = nullptr;
JSVM_Value testNumber2 = nullptr;
OH_JSVM_CreateDouble(env, 10.1, &testNumber1);
OH_JSVM_CreateInt32(env, 10, &testNumber2);
```

### Obtaining C Types or JS Type Information from JS Types

#### When to Use

Obtaining C types or JS type information from JS types.

#### Available APIs
| API| Description|
| -------- | -------- |
|OH_JSVM_GetArrayLength | Obtains the length of an array.|
|OH_JSVM_GetArraybufferInfo | Obtains the underlying data buffer of an ArrayBuffer and its length.|
|OH_JSVM_GetPrototype | Obtains the prototype of a JS object.|
|OH_JSVM_GetTypedarrayInfo | Obtains information about a TypedArray object.|
|OH_JSVM_GetDataviewInfo | Obtains information about a DataView object.|
|OH_JSVM_GetDateValue | Obtains the C double primitive of the time value for the given JS **Date** object.|
|OH_JSVM_GetValueBool | Obtains the C Boolean primitive equivalent of the given JS Boolean.|
|OH_JSVM_GetValueDouble | Obtains the C Double primitive equivalent of the given JS number.|
|OH_JSVM_GetValueBigintInt64 | Obtains the C Int64_t primitive equivalent of the given JS BigInt.|
|OH_JSVM_GetValueBigintUint64 | Obtains the C Uint64_t primitive equivalent of the given JS BigInt.|
|OH_JSVM_GetValueBigintWords | Obtains the underlying data of a given JS BigInt object, that is, the word representation of BigInt data.|
|OH_JSVM_GetValueExternal | Obtains the external data pointer previously passed to **OH_JSVM_CreateExternal**.|
|OH_JSVM_GetValueInt32 | Obtains the C Int32 primitive equivalent of the given JS number.|
|OH_JSVM_GetValueInt64 | Obtains the C Int64 primitive equivalent of the given JS number.|
|OH_JSVM_GetValueStringLatin1 | Obtains the ISO-8859-1-encoded string from the given JS string.|
|OH_JSVM_GetValueStringUtf8 | Obtains the UTF8-encoded string from the given JS string.|
|OH_JSVM_GetValueStringUtf16 | Obtains the UTF16-encoded string from the given JS string.|
|OH_JSVM_GetValueUint32 | Obtains the C primitive equivalent (a Uint32) of the given JS number.|
|OH_JSVM_GetBoolean | Obtains a JS singleton object that is used to represent the given Boolean value.|
|OH_JSVM_GetGlobal | Obtains the **global** object of the current environment.|
|OH_JSVM_GetNull | Obtains the JS **null** object.|
|OH_JSVM_GetUndefined | Obtains the JS **Undefined** object.|

Example:
Creates a JS BigInt object from a C Int64 object and obtain the C Int64_t primitive equivalent.

```c++
int64_t testValue = INT64_MAX;
JSVM_Value result = nullptr;
OH_JSVM_CreateBigintInt64(env, testValue, &result);
int64_t resultValue = 0;
bool flag = false;
OH_JSVM_GetValueBigintInt64(env, result, &resultValue, &flag);
```

Create an Int32Array and obtain its information such as the length and byte offset.

```c++
JSVM_Value arrayBuffer = nullptr;
void *arrayBufferPtr = nullptr;
size_t arrayBufferSize = 16;
size_t typedArrayLength = 4;
OH_JSVM_CreateArraybuffer(env, arrayBufferSize, &arrayBufferPtr, &arrayBuffer);

bool isArrayBuffer = false;
OH_JSVM_IsArraybuffer(env, arrayBuffer, &isArrayBuffer);

JSVM_Value result;
OH_JSVM_CreateTypedarray(env, JSVM_TypedarrayType::JSVM_INT32_ARRAY, typedArrayLength, arrayBuffer, 0, &result);

bool isTypedArray = false;
OH_JSVM_IsTypedarray(env, result, &isTypedArray);


JSVM_TypedarrayType type;
size_t length = 0;
void *data = nullptr;
JSVM_Value retArrayBuffer;
size_t byteOffset = -1;
OH_JSVM_GetTypedarrayInfo(env, result, &type, &length, &data, &retArrayBuffer, &byteOffset);


bool retIsArrayBuffer = false;
OH_JSVM_IsArraybuffer(env, retArrayBuffer, &retIsArrayBuffer);
void *tmpArrayBufferPtr = nullptr;
size_t arrayBufferLength = 0;
OH_JSVM_GetArraybufferInfo(env, retArrayBuffer, &tmpArrayBufferPtr, &arrayBufferLength);
```

Creates a JS string object from a UTF8-encoded C string and obtain the C string.

```c++
const char *testStringStr = "testString";
JSVM_Value testString = nullptr;
OH_JSVM_CreateStringUtf8(env, testStringStr, strlen(testStringStr), &testString);

char buffer[128];
size_t bufferSize = 128;
size_t copied;

OH_JSVM_GetValueStringUtf8(env, testString, buffer, bufferSize, &copied);
```

### Working with JS Values and Abstract Operations

#### When to Use

Perform abstract operations on JS values.

#### Available APIs
| API| Description|
| -------- | -------- |
|OH_JSVM_CoerceToBool | Converts a JS value to an object of the Boolean type.|
|OH_JSVM_CoerceToNumber | Converts a JS value to an object of the number type.|
|OH_JSVM_CoerceToObject | Converts a JS value to an object of the object type.|
|OH_JSVM_CoerceToString | Converts a JS value to an object of the string type.|
|OH_JSVM_Typeof | Returns the type of a JS object.|
|OH_JSVM_Instanceof | Checks whether an object is an instance of a constructor.|
|OH_JSVM_IsArray | Checks whether a JS object is an array.|
|OH_JSVM_IsArraybuffer | Checks whether a JS object is an array buffer.|
|OH_JSVM_IsDate | Checks whether a JS object is a date.|
|OH_JSVM_IsTypedarray | Checks whether a JS object is a typed array.|
|OH_JSVM_IsDataview | Checks whether a JS object is a **DataView**.|
|OH_JSVM_StrictEquals | Checks whether two **JSVM_Value** objects are equal.|
|OH_JSVM_DetachArraybuffer | Calls the **Detach()** operation of an **ArrayBuffer** object.|
|OH_JSVM_IsDetachedArraybuffer | Checks whether an **ArrayBuffer** object has been detached.|

Example:
Check whether a JS value is of the array type.

```c++
JSVM_Value array = nullptr;
OH_JSVM_CreateArray(env, &array);
bool isArray = false;
OH_JSVM_IsArray(env, array, &isArray);
```

Converts a JS int32 value to a string.

```c++
int32_t num = 123;
JSVM_Value intValue;
OH_JSVM_CreateInt32(env, num, &intValue);
JSVM_Value stringValue;
OH_JSVM_CoerceToString(env, intValue, &stringValue);

char buffer[128];
size_t bufferSize = 128;
size_t copied = 0;

OH_JSVM_GetValueStringUtf8(env, stringValue, buffer, bufferSize, &copied);
// buffer:"123";
```

Check whether two JS values are of the same type.

```c++
JSVM_Value value = nullptr;
JSVM_Value value1 = nullptr;
OH_JSVM_CreateArray(env, &value);

OH_JSVM_CreateInt32(env, 10, &value1);
bool isArray = true;
OH_JSVM_StrictEquals(env, value, value, &isArray);
```

### Working with JS Properties

#### When to Use

Set, get, delete, and check properties of JS objects.

#### Available APIs
| API| Description|
| -------- | -------- |
|OH_JSVM_GetPropertyNames | Obtains the names of all enumerable properties of a JS object as a JS array.|
|OH_JSVM_GetAllPropertyNames | Obtains the names of all available properties of a JS object as a JS array.|
|OH_JSVM_SetProperty | Sets a property for a JS object.|
|OH_JSVM_GetProperty | Obtains the requested property from a JS object.|
|OH_JSVM_HasProperty | Checks whether a JS object has the named property.|
|OH_JSVM_DeleteProperty | Deletes a property from a JS object.|
|OH_JSVM_HasOwnProperty | Checks whether a JS object has the named own property.|
|OH_JSVM_SetNamedProperty | Sets a property with the given property name for a JS object. This API is equivalent to calling **OH_JSVM_SetNamedProperty** with a **JSVM_Value** created from the string passed in as **utf8Name**.|
|OH_JSVM_GetNamedProperty | Obtains the property from a JS object with the given property name. This API is equivalent to calling **OH_JSVM_GetNamedProperty** with a **JSVM_Value** created from the string passed in as **utf8Name**.|
|OH_JSVM_HasNamedProperty | Checks whether a JS object has the named property. This API is equivalent to calling **OH_JSVM_HasProperty** using a **JSVM_Value** created from the string passed in as **utf8Name**.|
|OH_JSVM_SetElement | Sets an element at the specified index for a JS object.|
|OH_JSVM_GetElement | Obtains the element at the specified index of a JS object.|
|OH_JSVM_HasElement | Checks whether a JS object has an element at the specified index.|
|OH_JSVM_DeleteElement | Deletes the element at the specified index from a JS object.|
|OH_JSVM_DefineProperties |  Defines multiple properties for a JS object.|
|OH_JSVM_ObjectFreeze | Freezes a JS object. Once a JS object is frozen, new properties cannot be added to it, existing properties cannot be removed, the enumerability, configurability, or writability of existing properties cannot be changed, and the values of existing properties cannot be changed.|
|OH_JSVM_ObjectSeal | Seals a JS object. Once a JS object is sealed, new properties cannot be added to it and all existing properties are marked as unconfigurable.|

Example:
Set, get, delete, and check properties of a JS object.

```c++
// Create an empty object.
JSVM_Value myObject = nullptr;
OH_JSVM_CreateObject(env, &myObject);

// Set properties.
const char *testNameStr = "John Doe";
JSVM_Value propValue = nullptr;
JSVM_Value key;
OH_JSVM_CreateStringUtf8(env, "name", JSVM_AUTO_LENGTH, &key);
OH_JSVM_CreateStringUtf8(env, testNameStr, strlen(testNameStr), &propValue);
OH_JSVM_SetProperty(env, myObject, key, propValue);

// Obtain properties.
JSVM_Value propResult = nullptr;
OH_JSVM_GetProperty(env, myObject, key, &propResult);

// Check whether a property exists.
bool hasProperty = false;
OH_JSVM_HasNamedProperty(env, myObject, "name", &hasProperty);
    // The property exists. Perform subsequent processing accordingly.
    if (hasProperty)
    {
        // Obtain all property names of the object.
        JSVM_Value propNames = nullptr;
        OH_JSVM_GetPropertyNames(env, myObject, &propNames);

        bool isArray = false;
        OH_JSVM_IsArray(env, propNames, &isArray);

        uint32_t arrayLength = 0;
        OH_JSVM_GetArrayLength(env, propNames, &arrayLength);
        // Traverse property elements.
        for (uint32_t i = 0; i < arrayLength; i++)
        {
            bool hasElement = false;
            OH_JSVM_HasElement(env, propNames, i, &hasElement);

            JSVM_Value propName = nullptr;
            OH_JSVM_GetElement(env, propNames, i, &propName);

            bool hasProp = false;
            OH_JSVM_HasProperty(env, myObject, propName, &hasProp);

            JSVM_Value propValue = nullptr;
            OH_JSVM_GetProperty(env, myObject, propName, &propValue);
        }
    }

// Delete a property.
OH_JSVM_DeleteProperty(env, myObject, key, &hasProperty);
```

### Working with JS Functions

#### When to Use

Call back JS code into native code and call JS functions from native code.

#### Available APIs
| API| Description|
| -------- | -------- |
|OH_JSVM_CallFunction | Calls a JS function from a C/C++ addon.|
|OH_JSVM_CreateFunction | Creates a JS function object in native code, which allows calling into the native code from JS.|
|OH_JSVM_GetCbInfo | Obtains detailed information about the call, such as the parameters and **this** pointer, from the given callback information.|
|OH_JSVM_GetNewTarget | Obtains the **new.target** of the constructor call.|
|OH_JSVM_NewInstance | Creates an instance based on the given constructor.|

Example:
Create a JS function.

```c++
JSVM_Value SayHello(JSVM_Env env, JSVM_CallbackInfo info)
{
    printf("Hello\n");
    JSVM_Value ret;
    OH_JSVM_CreateInt32(env, 2, &ret);
    return ret;
}

static JSVM_Value JsvmCreateFunction(JSVM_Env env, JSVM_CallbackInfo info)
{
    JSVM_CallbackStruct param;
    param.data = nullptr;
    param.callback = SayHello;

    JSVM_Value funcValue = nullptr;
    JSVM_Status status = OH_JSVM_CreateFunction(env, "func", JSVM_AUTO_LENGTH, &param, &funcValue);
    return funcValue;
}
```

Obtain and call the JS function from C/C++.

```c++
static JSVM_Value CallFunction(JSVM_Env env, JSVM_CallbackInfo info)
{
    size_t argc = 1;
    JSVM_Value args[1];
    JSVM_CALL(env, OH_JSVM_GetCbInfo(env, info, &argc, args, NULL, NULL));

    JSVM_ASSERT(env, argc >= 1, "Wrong number of arguments");

    JSVM_ValueType valuetype;
    JSVM_CALL(env, OH_JSVM_Typeof(env, args[0], &valuetype));
    JSVM_ASSERT(env, valuetype == JSVM_ValueType::JSVM_FUNCTION, "Wrong type of argment. Expects a string.");

    JSVM_Value global;
    JSVM_CALL(env, OH_JSVM_GetGlobal(env, &global));

    JSVM_Value ret;
    JSVM_CALL(env, OH_JSVM_CallFunction(env, global, args[0], 0, nullptr, &ret));
    return ret;
}
```

### Wrapping Objects

#### When to Use

Wrap native classes and instances so that the class constructor and methods can be called from JS.

#### Available APIs
| API| Description|
| -------- | -------- |
|OH_JSVM_DefineClass| Defines a JS class and associated functions within a C/C++ addon. It allows you to define class constructors, methods, and properties that can be accessed from JS.|
|OH_JSVM_Wrap| Wraps a native instance in a JS object. You can use **OH_JSVM_Unwrap()** to retrieve the native instance later.|
|OH_JSVM_Unwrap | Retrieves a native instance from a JS object.|
|OH_JSVM_RemoveWrap | Retrieves a native instance previously wrapped in a JS object and removes the wrapping.|
|OH_JSVM_TypeTagObject | Associates the value of the **type_tag** pointer with a JS object or an external object.|
|OH_JSVM_CheckObjectTypeTag | Checks whether a tag matches the tag type of an object.|
|OH_JSVM_AddFinalizer | Add a **JSVM_Finalize** callback to a JS object. The callback will be invoked to release the native object when the JS object is garbage-collected.|
|OH_JSVM_PostFinalizer | Schedules a **JSVM_Finalize** callback to be called asynchronously in the event loop.|

Example:
Wrap a native object in a JS object.

```c++
static JSVM_Value AssertEqual(JSVM_Env env, JSVM_CallbackInfo info)
{
    size_t argc = 2;
    JSVM_Value args[2];
    JSVM_CALL(env, OH_JSVM_GetCbInfo(env, info, &argc, args, NULL, NULL));

    bool isStrictEquals = false;
    OH_JSVM_StrictEquals(env, args[0], args[1], &isStrictEquals);
    return nullptr;
}

static napi_value TestWrap(napi_env env1, napi_callback_info info)
{
    OH_LOG_ERROR(LOG_APP, "testWrap start");
    JSVM_InitOptions init_options;
    memset(&init_options, 0, sizeof(init_options));
    init_options.externalReferences = externals;
    if (aa == 0) {
        OH_JSVM_Init(&init_options);
        aa++;
    }
    JSVM_VM vm;
    JSVM_CreateVMOptions options;
    memset(&options, 0, sizeof(options));
    OH_JSVM_CreateVM(&options, &vm);
    JSVM_VMScope vm_scope;
    OH_JSVM_OpenVMScope(vm, &vm_scope);
    JSVM_Env env;
    JSVM_CallbackStruct param[1];
    param[0].data = nullptr;
    param[0].callback = AssertEqual;
    JSVM_PropertyDescriptor descriptor[] = {
        {"assertEqual", NULL, &param[0], NULL, NULL, NULL, JSVM_DEFAULT},
    };
    OH_JSVM_CreateEnv(vm, sizeof(descriptor) / sizeof(descriptor[0]), descriptor, &env);
    JSVM_EnvScope envScope;
    OH_JSVM_OpenEnvScope(env, &envScope);
    JSVM_HandleScope handlescope;
    OH_JSVM_OpenHandleScope(env, &handlescope);
    JSVM_Value testClass = nullptr;
    JSVM_CallbackStruct param1;
    param1.data = nullptr;
    param1.callback = [](JSVM_Env env, JSVM_CallbackInfo info) -> JSVM_Value {
        JSVM_Value thisVar = nullptr;
        OH_JSVM_GetCbInfo(env, info, nullptr, nullptr, &thisVar, nullptr);

        return thisVar;
    };
    OH_JSVM_DefineClass(env, "TestClass", JSVM_AUTO_LENGTH, &param1, 0, nullptr, &testClass);

    JSVM_Value instanceValue = nullptr;
    OH_JSVM_NewInstance(env, testClass, 0, nullptr, &instanceValue);

    const char *testStr = "test";
    OH_JSVM_Wrap(
        env, instanceValue, (void *)testStr, [](JSVM_Env env, void *data, void *hint) {}, nullptr, nullptr);
    const char *tmpTestStr = nullptr;
    OH_JSVM_Unwrap(env, instanceValue, (void **)&tmpTestStr);
    const char *tmpTestStr1 = nullptr;
    OH_JSVM_RemoveWrap(env, instanceValue, (void **)&tmpTestStr1);
    OH_JSVM_Unwrap(env, instanceValue, (void **)&tmpTestStr1);
    OH_JSVM_CloseHandleScope(env, handlescope);
    OH_JSVM_CloseEnvScope(env, envScope);
    OH_JSVM_DestroyEnv(env);
    OH_JSVM_CloseVMScope(vm, vm_scope);
    OH_JSVM_DestroyVM(vm);
    OH_LOG_ERROR(LOG_APP, "testWrap pass");
    return nullptr;
}
```

### Version Management

#### When to Use

Obtain version information.

#### Available APIs
| API| Description|
| -------- | -------- |
|OH_JSVM_GetVersion| Obtains the latest JSVM API version supported by the JSVM runtime.|
|OH_JSVM_GetVMInfo| Obtains the VM information.|

Example:
Obtain version information.

```c++
JSVM_VMInfo result;
OH_JSVM_GetVMInfo(&result);
uint32_t versionId = 0;
OH_JSVM_GetVersion(env, &versionId);
```

### Memory Management

#### When to Use

Perform memory management.

#### Available APIs
| API| Description|
| -------- | -------- |
|OH_JSVM_AdjustExternalMemory| Informs the underlying engine that the VM system memory is insufficient and selectively triggers garbage collection.|
|OH_JSVM_MemoryPressureNotification| Creates a deferred object and a JS promise.|

Example:
Perform memory management. 

```c++
int64_t change = 1024 * 1024; // Allocate 1 MB of memory.
int64_t result;
OH_JSVM_AdjustExternalMemory(env, change, &result);
```

### Promises

#### When to Use

Perform operations related to promises.

#### Available APIs
| API| Description|
| -------- | -------- |
|OH_JSVM_CreatePromise| Creates a deferred object and a JS promise.|
|OH_JSVM_ResolveDeferred| Resolves a JS promise by using the deferred object associated with it.|
|OH_JSVM_RejectDeferred| Rejects a JS promise by using the deferred object associated with it.|
|OH_JSVM_IsPromise| Checks whether a promise object is a native promise object.|

Example:
Perform operations related to promises.

```c++
JSVM_Deferred deferred;
JSVM_Value promise;
OH_JSVM_CreatePromise(env, &deferred, &promise);

// Perform an asynchronous operation.
int result = 42;
bool success = true;
if (success)
{
    // Resolve the promise and pass the result.
    JSVM_Value value;
    OH_JSVM_CreateInt32(env, result, &value);
    OH_JSVM_ResolveDeferred(env, deferred, value);
} else {
    // Reject the promise and pass the error information.
    JSVM_Value code = nullptr;
    JSVM_Value message = nullptr;
    OH_JSVM_CreateStringUtf8(env, "600", JSVM_AUTO_LENGTH, &code);
    OH_JSVM_CreateStringUtf8(env, "Async operation failed", JSVM_AUTO_LENGTH, &message);
    JSVM_Value error = nullptr;
    OH_JSVM_CreateError(env, code, message, &error);
    OH_JSVM_RejectDeferred(env, deferred, error);
}
```

### JSON Operations

#### When to Use

Perform JSON operations.

#### Available APIs

| API| Description|
| -------- | -------- |
|OH_JSVM_JsonParse| Parses a JSON string and returns the parsed value.|
|OH_JSVM_JsonStringify| Converts a JS object into a JSON string and returns the converted string.|

Example:
Parse JSON strings.

```c++
std::string sourcecodestr = "{\"name\": \"John\", \"age\": 30, \"city\": \"New York\"}" ;
JSVM_Value jsonString;
OH_JSVM_CreateStringUtf8(env, sourcecodestr.c_str(), sourcecodestr.size(), &jsonString)
JSVM_Value result;
OH_JSVM_JsonParse(env, jsonString, &result);
```

### Creating VM Startup Snapshots

#### When to Use

Create a VM startup snapshot.

#### Available APIs
| API| Description|
| -------- | -------- |
|OH_JSVM_CreateSnapshot| Creates a VM startup snapshot.|

Example:
Create a VM startup snapshot.

```c++
JSVM_VM vm;
JSVM_CreateVMOptions options;
memset(&options, 0, sizeof(options));
OH_JSVM_CreateVM(&options, &vm);
JSVM_Env env;
JSVM_CallbackStruct param[1];
param[0].data = nullptr;
param[0].callback = AssertEqual;
JSVM_PropertyDescriptor descriptor[] = {
    {"test", nullptr, &param[0], nullptr, nullptr, nullptr, JSVM_DEFAULT},
};
OH_JSVM_CreateEnv(vm, sizeof(descriptor) / sizeof(descriptor[0]), descriptor, &env);
const char *blobData = nullptr;
size_t blobSize = 0;
JSVM_Env envs[1] = {env};
OH_JSVM_CreateSnapshot(vm, 1, envs, &blobData, &blobSize);
```
