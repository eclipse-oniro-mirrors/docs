# JSVM


## 概述

提供标准的JavaScript引擎能力。

功能概述： 标准JS引擎是严格遵守Ecmascript规范的JavaScript代码执行引擎。 支持Ecmascript规范定义的标准库，提供完备的C++交互JS的native API。 通过jit加速代码执行，为应用提供安全、高效的JS执行能力。 标准JS引擎的能力通过一套稳定的ABI，即JSVM-API提供。JSVM-API支持动态链接到不同版本的JS引擎库， 从而为开发者屏蔽掉不同引擎接口的差异。JSVM-API提供引擎生命周期管理、JS context管理、 JS代码执行、JS/C++互操作、执行环境快照、codecache等能力。
使用平台：arm64平台。
使用方法：链接SDK中的libjsvm.so，并在C++代码中包含ark_runtime/jsvm.h头文件。

通过API接口为开发者提供独立、标准、完整的JavaScript引擎能力， 包括管理引擎生命周期、编译运行JS代码、实现JS/C++跨语言调用、拍摄快照等。

**起始版本：** 11


## 汇总


### 文件

| 名称 | 描述 | 
| -------- | -------- |
| [jsvm.h](jsvm_8h.md) | 提供JSVM-API接口定义。 | 
| [jsvm_types.h](jsvm__types_8h.md) | 提供JSVM-API类型定义。 | 


### 结构体

| 名称 | 描述 | 
| -------- | -------- |
| struct&nbsp;&nbsp;[JSVM_CallbackStruct](_j_s_v_m___callback_struct.md) | 用户提供的native函数的回调函数指针和数据，这些函数通过JSVM-API接口暴露给JavaScript。 | 
| struct&nbsp;&nbsp;[JSVM_InitOptions](_j_s_v_m___init_options.md) | 初始化选项，用于初始化JavaScript虚拟机。 | 
| struct&nbsp;&nbsp;[JSVM_CreateVMOptions](_j_s_v_m___create_v_m_options.md) | 创建JavaScript虚拟机的选项。 | 
| struct&nbsp;&nbsp;[JSVM_VMInfo](_j_s_v_m___v_m_info.md) | JavaScript虚拟机信息。 | 
| struct&nbsp;&nbsp;[JSVM_PropertyDescriptor](_j_s_v_m___property_descriptor.md) | 属性描述符。 | 
| struct&nbsp;&nbsp;[JSVM_ExtendedErrorInfo](_j_s_v_m___extended_error_info.md) | 扩展的异常信息。 | 
| struct&nbsp;&nbsp;[JSVM_TypeTag](_j_s_v_m___type_tag.md) | 类型标记，存储为两个无符号64位整数的128位值。 作为一个UUID，通过它，JavaScript对象可以是"tagged"， 以确保它们的类型保持不变。 | 


### 宏定义

| 名称 | 描述 | 
| -------- | -------- |
| [JSVM_AUTO_LENGTH](#jsvm_auto_length)&nbsp;&nbsp;&nbsp;SIZE_MAX | 自动长度。 | 


### 类型定义

| 名称 | 描述 | 
| -------- | -------- |
| typedef struct JSVM_VM__ \* [JSVM_VM](#jsvm_vm) | 表示JavaScript虚拟机实例。 | 
| typedef struct JSVM_VMScope__ \* [JSVM_VMScope](#jsvm_vmscope) | 表示JavaScript虚拟机作用域。 | 
| typedef struct JSVM_EnvScope__ \* [JSVM_EnvScope](#jsvm_envscope) | 表示用于控制附加到当前虚拟机实例的环境。只有当线程通过 OH_JSVM_OpenEnvScope进入该环境的JSVM_EnvScope后，该环境才 对线程的虚拟机实例可用。 | 
| typedef struct JSVM_Script__ \* [JSVM_Script](#jsvm_script) | 表示一段JavaScript代码。 | 
| typedef struct JSVM_Env__ \* [JSVM_Env](#jsvm_env) | 表示虚拟机特定状态的上下文环境，需要在调用native函数时作为参数传递， 并且传递给后续任何的JSVM-API嵌套调用。 | 
| typedef struct JSVM_Value__ \* [JSVM_Value](#jsvm_value) | 表示JavaScript值。 | 
| typedef struct JSVM_Ref__ \* [JSVM_Ref](#jsvm_ref) | 表示JavaScript值的引用。 | 
| typedef struct JSVM_HandleScope__ \* [JSVM_HandleScope](#jsvm_handlescope) | 表示JavaScript值的作用域，用于控制和修改在特定范围内创建的对象的生命周期。 通常，JSVM-API值是在JSVM_HandleScope的上下文中创建的。当从JavaScript调用native方法时， 将存在默认JSVM_HandleScope。如果用户没有显式创建新的JSVM_HandleScope，将在默认 JSVM_HandleScope中创建JSVM-API值。对于native方法执行之外的任何代码调用（例如，在libuv回调调用期间）， 模块需要在调用任何可能导致创建JavaScript值的函数之前创建一个作用域。JSVM_HandleScope是使用 OH_JSVM_OpenHandleScope创建的，并使用OH_JSVM_CloseHandleScope销毁的。 关闭作用域代表向GC指示在JSVM_HandleScope作用域的生命周期内创建的所有JSVM_Value将不再从当前堆的栈帧中引用。 | 
| typedef struct JSVM_EscapableHandleScope__ \* [JSVM_EscapableHandleScope](#jsvm_escapablehandlescope) | 表示一种特殊类型的handle scope，用于将在特定handle scope内创建的值返回到父作用域。 | 
| typedef struct JSVM_CallbackInfo__ \* [JSVM_CallbackInfo](#jsvm_callbackinfo) | 表示传递给回调函数的不透明数据类型。可用于获取调用该函数的上下文的附加信息。 | 
| typedef struct JSVM_Deferred__ \* [JSVM_Deferred](#jsvm_deferred) | 表示Promise延迟对象。 | 
| typedef [JSVM_CallbackStruct](_j_s_v_m___callback_struct.md) \* [JSVM_Callback](#jsvm_callback) | 用户提供的native函数的函数指针类型，这些函数通过JSVM-API接口暴露给JavaScript。 | 
| typedef void(JSVM_CDECL \* [JSVM_Finalize](#jsvm_finalize)) ([JSVM_Env](#jsvm_env) env, void \*finalizeData, void \*finalizeHint) | 函数指针类型，当native类型对象或数据与JS对象被关联时，传入该指针。该函数将会 在关联的JS对象被GC回收时被调用，用以执行native的清理动作。 | 


### 枚举

| 名称 | 描述 | 
| -------- | -------- |
| [JSVM_PropertyAttributes](#jsvm_propertyattributes) {<br/>JSVM_DEFAULT = 0, JSVM_WRITABLE = 1 &lt;&lt; 0, JSVM_ENUMERABLE = 1 &lt;&lt; 1, JSVM_CONFIGURABLE = 1 &lt;&lt; 2,<br/>JSVM_STATIC = 1 &lt;&lt; 10, JSVM_DEFAULT_METHOD = JSVM_WRITABLE \| JSVM_CONFIGURABLE, JSVM_DEFAULT_JSPROPERTY = JSVM_WRITABLE \| JSVM_ENUMERABLE \| JSVM_CONFIGURABLE<br/>} | 用于控制JavaScript对象属性的行为。 | 
| [JSVM_ValueType](#jsvm_valuetype) {<br/>JSVM_UNDEFINED, JSVM_NULL, JSVM_BOOLEAN, JSVM_NUMBER,<br/>JSVM_STRING, JSVM_SYMBOL, JSVM_OBJECT, JSVM_FUNCTION,<br/>JSVM_EXTERNAL, JSVM_BIGINT<br/>} | 描述JSVM_Value的类型。 | 
| [JSVM_TypedarrayType](#jsvm_typedarraytype) {<br/>JSVM_INT8_ARRAY, JSVM_UINT8_ARRAY, JSVM_UINT8_CLAMPED_ARRAY, JSVM_INT16_ARRAY,<br/>JSVM_UINT16_ARRAY, JSVM_INT32_ARRAY, JSVM_UINT32_ARRAY, JSVM_FLOAT32_ARRAY,<br/>JSVM_FLOAT64_ARRAY, JSVM_BIGINT64_ARRAY, JSVM_BIGUINT64_ARRAY<br/>} | 描述TypedArray的类型。 | 
| [JSVM_Status](#jsvm_status) {<br/>JSVM_OK, JSVM_INVALID_ARG, JSVM_OBJECT_EXPECTED, JSVM_STRING_EXPECTED,<br/>JSVM_NAME_EXPECTED, JSVM_FUNCTION_EXPECTED, JSVM_NUMBER_EXPECTED, JSVM_BOOLEAN_EXPECTED,<br/>JSVM_ARRAY_EXPECTED, JSVM_GENERIC_FAILURE, JSVM_PENDING_EXCEPTION, JSVM_CANCELLED,<br/>JSVM_ESCAPE_CALLED_TWICE, JSVM_HANDLE_SCOPE_MISMATCH, JSVM_CALLBACK_SCOPE_MISMATCH, JSVM_QUEUE_FULL,<br/>JSVM_CLOSING, JSVM_BIGINT_EXPECTED, JSVM_DATE_EXPECTED, JSVM_ARRAYBUFFER_EXPECTED,<br/>JSVM_DETACHABLE_ARRAYBUFFER_EXPECTED, JSVM_WOULD_DEADLOCK, JSVM_NO_EXTERNAL_BUFFERS_ALLOWED, JSVM_CANNOT_RUN_JS<br/>} | 表示JSVM-API调用成功或失败的完整状态码。 | 
| [JSVM_KeyCollectionMode](#jsvm_keycollectionmode) { JSVM_KEY_INCLUDE_PROTOTYPES, JSVM_KEY_OWN_ONLY } | 限制查找属性的范围。 | 
| [JSVM_KeyFilter](#jsvm_keyfilter) {<br/>JSVM_KEY_ALL_PROPERTIES = 0, JSVM_KEY_WRITABLE = 1, JSVM_KEY_ENUMERABLE = 1 &lt;&lt; 1, JSVM_KEY_CONFIGURABLE = 1 &lt;&lt; 2,<br/>JSVM_KEY_SKIP_STRINGS = 1 &lt;&lt; 3, JSVM_KEY_SKIP_SYMBOLS = 1 &lt;&lt; 4<br/>} | 属性过滤器，可以通过使用or来构造一个复合过滤器。 | 
| [JSVM_KeyConversion](#jsvm_keyconversion) { JSVM_KEY_KEEP_NUMBERS, JSVM_KEY_NUMBERS_TO_STRINGS } | 键转换选项。 | 
| [JSVM_MemoryPressureLevel](#jsvm_memorypressurelevel) { JSVM_MEMORY_PRESSURE_LEVEL_NONE, JSVM_MEMORY_PRESSURE_LEVEL_MODERATE, JSVM_MEMORY_PRESSURE_LEVEL_CRITICAL } | 内存压力水平。 | 


### 函数

| 名称 | 描述 | 
| -------- | -------- |
| EXTERN_C_START JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_Init](#oh_jsvm_init) (const [JSVM_InitOptions](_j_s_v_m___init_options.md) \*options) | 初始化一个JavaScript虚拟机。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateVM](#oh_jsvm_createvm) (const [JSVM_CreateVMOptions](_j_s_v_m___create_v_m_options.md) \*options, [JSVM_VM](#jsvm_vm) \*result) | 创建一个虚拟机实例。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_DestroyVM](#oh_jsvm_destroyvm) ([JSVM_VM](#jsvm_vm) vm) | 销毁一个虚拟机实例。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_OpenVMScope](#oh_jsvm_openvmscope) ([JSVM_VM](#jsvm_vm) vm, [JSVM_VMScope](#jsvm_vmscope) \*result) | 为虚拟机实例打开一个新的虚拟机作用域。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CloseVMScope](#oh_jsvm_closevmscope) ([JSVM_VM](#jsvm_vm) vm, [JSVM_VMScope](#jsvm_vmscope) scope) | 关闭虚拟机实例的虚拟机作用域。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateEnv](#oh_jsvm_createenv) ([JSVM_VM](#jsvm_vm) vm, size_t propertyCount, const [JSVM_PropertyDescriptor](_j_s_v_m___property_descriptor.md) \*properties, [JSVM_Env](#jsvm_env) \*result) | 基于新环境上下文的可选属性，创建一个新环境。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateEnvFromSnapshot](#oh_jsvm_createenvfromsnapshot) ([JSVM_VM](#jsvm_vm) vm, size_t index, [JSVM_Env](#jsvm_env) \*result) | 基于虚拟机的起始快照，创建一个新的环境。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_DestroyEnv](#oh_jsvm_destroyenv) ([JSVM_Env](#jsvm_env) env) | 销毁环境。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_OpenEnvScope](#oh_jsvm_openenvscope) ([JSVM_Env](#jsvm_env) env, [JSVM_EnvScope](#jsvm_envscope) \*result) | 打开一个新的环境作用域。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CloseEnvScope](#oh_jsvm_closeenvscope) ([JSVM_Env](#jsvm_env) env, [JSVM_EnvScope](#jsvm_envscope) scope) | 关闭环境作用域。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CompileScript](#oh_jsvm_compilescript) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) script, const uint8_t \*cachedData, size_t cacheDataLength, bool eagerCompile, bool \*cacheRejected, [JSVM_Script](#jsvm_script) \*result) | 编译一串JavaScript代码，并返回编译后的脚本。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateCodeCache](#oh_jsvm_createcodecache) ([JSVM_Env](#jsvm_env) env, [JSVM_Script](#jsvm_script) script, const uint8_t \*\*data, size_t \*length) | 为编译后的脚本创建代码缓存。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_RunScript](#oh_jsvm_runscript) ([JSVM_Env](#jsvm_env) env, [JSVM_Script](#jsvm_script) script, [JSVM_Value](#jsvm_value) \*result) | 执行一串JavaScript代码并返回其结果，其中包含以下注意事项： 与eval不同的是，该函数不允许脚本访问当前词法作用域，因此也不允许访问模块作用域， 这意味着require等伪全局变量将不可用。 脚本可以访问全局作用域。 脚本中的函数和var声明将被添加到全局对象。 使用let和const的变量声明将全局可见，但不会被添加到全局对象。 this的值在脚本内是global。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_SetInstanceData](#oh_jsvm_setinstancedata) ([JSVM_Env](#jsvm_env) env, void \*data, [JSVM_Finalize](#jsvm_finalize) finalizeCb, void \*finalizeHint) | 将data与当前运行的JSVM环境相关联。后续可以使用OH_JSVM_GetInstanceData()检索data。 通过先前调用OH_JSVM_SetInstanceData()设置的任何与当前运行的JSVM环境相关联的现有数据都将 被覆盖。如果先前提供了finalizeCb，则不会调用它。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetInstanceData](#oh_jsvm_getinstancedata) ([JSVM_Env](#jsvm_env) env, void \*\*data) | 检索通过OH_JSVM_SetInstanceData()与当前运行的JSVM环境相关联的数据。 如果未设置任何关联数据，该函数调用将成功，且data设置为NULL。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetLastErrorInfo](#oh_jsvm_getlasterrorinfo) ([JSVM_Env](#jsvm_env) env, const [JSVM_ExtendedErrorInfo](_j_s_v_m___extended_error_info.md) \*\*result) | 检索JSVM_ExtendedErrorInfo结构，其中包含有关发生的最后一个错误的信息。 返回的JSVM_ExtendedErrorInfo的内容仅在对同一env调用JSVM-API函数之前有效。 这包括对OH_JSVM_IsExceptionPending的调用，因此可能经常需要复制信息以便以后使用。 error_message中返回的指针指向一个静态定义的字符串，因此如果你在调用另一个JSVM-API 函数之前将它从error_message字段（将被覆盖）中复制出来，则可以安全地使用该指针。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_Throw](#oh_jsvm_throw) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) error) | 抛出提供的JavaScript值。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_ThrowError](#oh_jsvm_throwerror) ([JSVM_Env](#jsvm_env) env, const char \*code, const char \*msg) | 会抛出带有所提供文本的JavaScript Error。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_ThrowTypeError](#oh_jsvm_throwtypeerror) ([JSVM_Env](#jsvm_env) env, const char \*code, const char \*msg) | 会抛出带有所提供文本的JavaScript TypeError。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_ThrowRangeError](#oh_jsvm_throwrangeerror) ([JSVM_Env](#jsvm_env) env, const char \*code, const char \*msg) | 会抛出带有所提供文本的JavaScript RangeError。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_ThrowSyntaxError](#oh_jsvm_throwsyntaxerror) ([JSVM_Env](#jsvm_env) env, const char \*code, const char \*msg) | 会抛出带有所提供文本的JavaScript SyntaxError。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_IsError](#oh_jsvm_iserror) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, bool \*result) | 查询JSVM_Value以检查它是否表示错误对象。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateError](#oh_jsvm_createerror) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) code, [JSVM_Value](#jsvm_value) msg, [JSVM_Value](#jsvm_value) \*result) | 返回带有所提供文本的JavaScript Error。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateTypeError](#oh_jsvm_createtypeerror) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) code, [JSVM_Value](#jsvm_value) msg, [JSVM_Value](#jsvm_value) \*result) | 返回带有所提供文本的JavaScript TypeError。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateRangeError](#oh_jsvm_createrangeerror) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) code, [JSVM_Value](#jsvm_value) msg, [JSVM_Value](#jsvm_value) \*result) | 返回带有所提供文本的JavaScript RangeError。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateSyntaxError](#oh_jsvm_createsyntaxerror) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) code, [JSVM_Value](#jsvm_value) msg, [JSVM_Value](#jsvm_value) \*result) | 返回带有所提供文本的JavaScript SyntaxError。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetAndClearLastException](#oh_jsvm_getandclearlastexception) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) \*result) | 获取并清除上一次异常。如果出现挂起，则返回JavaScript异常，否则返回NULL。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_IsExceptionPending](#oh_jsvm_isexceptionpending) ([JSVM_Env](#jsvm_env) env, bool \*result) | 查询上一次异常是否由挂起导致的。如果由异常导致，则返回true，否则返回false。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_OpenHandleScope](#oh_jsvm_openhandlescope) ([JSVM_Env](#jsvm_env) env, [JSVM_HandleScope](#jsvm_handlescope) \*result) | 开辟了一个新的作用域。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CloseHandleScope](#oh_jsvm_closehandlescope) ([JSVM_Env](#jsvm_env) env, [JSVM_HandleScope](#jsvm_handlescope) scope) | 关闭传入的作用域。必须按照创建作用域的相反顺序关闭作用域。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_OpenEscapableHandleScope](#oh_jsvm_openescapablehandlescope) ([JSVM_Env](#jsvm_env) env, [JSVM_EscapableHandleScope](#jsvm_escapablehandlescope) \*result) | 会打开一个新作用域，从中可以将一个对象提升到外部作用域。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CloseEscapableHandleScope](#oh_jsvm_closeescapablehandlescope) ([JSVM_Env](#jsvm_env) env, [JSVM_EscapableHandleScope](#jsvm_escapablehandlescope) scope) | 关闭传入的作用域。必须按照创建作用域的相反顺序关闭作用域。 即使存在挂起的JavaScript异常，也可以调用此JSVM_API。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_EscapeHandle](#oh_jsvm_escapehandle) ([JSVM_Env](#jsvm_env) env, [JSVM_EscapableHandleScope](#jsvm_escapablehandlescope) scope, [JSVM_Value](#jsvm_value) escapee, [JSVM_Value](#jsvm_value) \*result) | 提升JavaScript对象的句柄，使其在外部作用域的生命周期内有效。 每个作用域只能调用一次。如果多次调用，将返回错误。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateReference](#oh_jsvm_createreference) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, uint32_t initialRefcount, [JSVM_Ref](#jsvm_ref) \*result) | 对传入的值创建一个具有指定引用计数的新引用。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_DeleteReference](#oh_jsvm_deletereference) ([JSVM_Env](#jsvm_env) env, [JSVM_Ref](#jsvm_ref) ref) | 删除传入的引用。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_ReferenceRef](#oh_jsvm_referenceref) ([JSVM_Env](#jsvm_env) env, [JSVM_Ref](#jsvm_ref) ref, uint32_t \*result) | 增加传入引用的引用计数并返回生成的引用计数。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_ReferenceUnref](#oh_jsvm_referenceunref) ([JSVM_Env](#jsvm_env) env, [JSVM_Ref](#jsvm_ref) ref, uint32_t \*result) | 递减传入引用的引用计数并返回生成的引用计数。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetReferenceValue](#oh_jsvm_getreferencevalue) ([JSVM_Env](#jsvm_env) env, [JSVM_Ref](#jsvm_ref) ref, [JSVM_Value](#jsvm_value) \*result) | 如果仍然有效，此JSVM-API将返回JSVM_Value， 表示与JSVM_Ref关联的JavaScript值。否则，结果将为NULL。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateArray](#oh_jsvm_createarray) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) \*result) | 返回对应于JavaScript Array类型的JSVM-API值。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateArrayWithLength](#oh_jsvm_createarraywithlength) ([JSVM_Env](#jsvm_env) env, size_t length, [JSVM_Value](#jsvm_value) \*result) | 返回对应于JavaScript Array类型的JSVM-API值。Array 的长度属性设置为传入的长度参数。但是，不保证底层缓冲区在创建 数组时由VM预先分配。该行为留给底层VM实现。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateArraybuffer](#oh_jsvm_createarraybuffer) ([JSVM_Env](#jsvm_env) env, size_t byteLength, void \*\*data, [JSVM_Value](#jsvm_value) \*result) | 返回JavaScript ArrayBuffer类型对应的JSVM-API值。ArrayBuffer用于 表示固定长度的二进制数据缓冲区。通常用作TypedArray对象的后备缓冲区。 分配的ArrayBuffer有一个底层字节缓冲区，其大小由传入的length参数决定。 底层缓冲区可选择返回给调用方，调用方可直接操作该缓冲区。 此缓冲区只能直接从native代码写入。如果想从JavaScript写入该缓冲区， 需创建TypedArray或DataView对象。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateDate](#oh_jsvm_createdate) ([JSVM_Env](#jsvm_env) env, double time, [JSVM_Value](#jsvm_value) \*result) | 分配一个JavaScript Date对象。此API不处理闰秒。 这是因为ECMAScript遵循POSIX时间规范，对闰秒进行忽略。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateExternal](#oh_jsvm_createexternal) ([JSVM_Env](#jsvm_env) env, void \*data, [JSVM_Finalize](#jsvm_finalize) finalizeCb, void \*finalizeHint, [JSVM_Value](#jsvm_value) \*result) | 分配一个带有外部数据的JavaScript值。这用于通过JavaScript代码传递外部数据。 后续可以使用OH_JSVM_GetValueExternal由native代码检索。 该API添加了一个JSVM_Finalize回调，当刚刚创建的JavaScript对象被垃圾回收时将调用该回调。 创建的值不是一个对象，因此不支持附加属性。它被认为是一个独特的值类型： 使用外部值调用OH_JSVM_Typeof()会生成JSVM_EXTERNAL。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateObject](#oh_jsvm_createobject) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) \*result) | 分配一个默认的JavaScript对象。该函数功能等同于在JavaScript中执行new Object()。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateSymbol](#oh_jsvm_createsymbol) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) description, [JSVM_Value](#jsvm_value) \*result) | 从UTF8 编码的C字符串创建JavaScript symbol值。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_SymbolFor](#oh_jsvm_symbolfor) ([JSVM_Env](#jsvm_env) env, const char \*utf8description, size_t length, [JSVM_Value](#jsvm_value) \*result) | 在全局注册表中搜索具有给定描述的现有符号。如果该 符号已经存在，它将被返回，否则将在注册表中创建一个新符号。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateTypedarray](#oh_jsvm_createtypedarray) ([JSVM_Env](#jsvm_env) env, [JSVM_TypedarrayType](#jsvm_typedarraytype) type, size_t length, [JSVM_Value](#jsvm_value) arraybuffer, size_t byteOffset, [JSVM_Value](#jsvm_value) \*result) | 基于已有的ArrayBuffer对象，创建一个JavaScript TypedArray对象。TypedArray 对象在底层数据缓冲区上提供了一个类似数组的视图，其中每个元素都具有 相同的底层二进制标量数据类型。要求：（length\* 元素大小）+ byteOffset 小于等于传入的数组的大小（以字节为单位）。否则，将抛出范围错误（RangeError）。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateDataview](#oh_jsvm_createdataview) ([JSVM_Env](#jsvm_env) env, size_t length, [JSVM_Value](#jsvm_value) arraybuffer, size_t byteOffset, [JSVM_Value](#jsvm_value) \*result) | 基于已有的ArrayBuffer对象，创建一个JavaScript DataView对象。DataView 对象在底层数据缓冲区上提供了一个类似数组的视图，其中的元素可以具有不同的大小和类型。 要求：二进制的length + byteOffset 小于或等于传入的数组的大小（以字节为单位）。否则，将抛出范围错误（RangeError）。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateInt32](#oh_jsvm_createint32) ([JSVM_Env](#jsvm_env) env, int32_t value, [JSVM_Value](#jsvm_value) \*result) | 将C int32_t类型的值转换为JavaScript number类型。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateUint32](#oh_jsvm_createuint32) ([JSVM_Env](#jsvm_env) env, uint32_t value, [JSVM_Value](#jsvm_value) \*result) | 将C uint32_t类型的值转换为JavaScript number类型。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateInt64](#oh_jsvm_createint64) ([JSVM_Env](#jsvm_env) env, int64_t value, [JSVM_Value](#jsvm_value) \*result) | 将C int64_t类型的值转换为JavaScript number类型。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateDouble](#oh_jsvm_createdouble) ([JSVM_Env](#jsvm_env) env, double value, [JSVM_Value](#jsvm_value) \*result) | 将C double类型的值转换为JavaScript number类型。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateBigintInt64](#oh_jsvm_createbigintint64) ([JSVM_Env](#jsvm_env) env, int64_t value, [JSVM_Value](#jsvm_value) \*result) | 将C int64_t类型的值转换为JavaScript BigInt类型。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateBigintUint64](#oh_jsvm_createbigintuint64) ([JSVM_Env](#jsvm_env) env, uint64_t value, [JSVM_Value](#jsvm_value) \*result) | 将C uint64_t类型的值转换为JavaScript BigInt类型。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateBigintWords](#oh_jsvm_createbigintwords) ([JSVM_Env](#jsvm_env) env, int signBit, size_t wordCount, const uint64_t \*words, [JSVM_Value](#jsvm_value) \*result) | 将一组无符号64位字转换为单个BigInt值。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateStringLatin1](#oh_jsvm_createstringlatin1) ([JSVM_Env](#jsvm_env) env, const char \*str, size_t length, [JSVM_Value](#jsvm_value) \*result) | 将采用ISO-8859-1编码的C字符串转换为JavaScript string值。 复制原生字符串。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateStringUtf16](#oh_jsvm_createstringutf16) ([JSVM_Env](#jsvm_env) env, const char16_t \*str, size_t length, [JSVM_Value](#jsvm_value) \*result) | 将采用UTF16-LE编码的C字符串转换为JavaScript字符串值。 复制原生字符串。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateStringUtf8](#oh_jsvm_createstringutf8) ([JSVM_Env](#jsvm_env) env, const char \*str, size_t length, [JSVM_Value](#jsvm_value) \*result) | 从UTF8编码的C字符串创建JavaScript string值。 复制原生字符串。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetArrayLength](#oh_jsvm_getarraylength) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, uint32_t \*result) | 返回数组的长度。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetArraybufferInfo](#oh_jsvm_getarraybufferinfo) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) arraybuffer, void \*\*data, size_t \*byteLength) | 用于检索ArrayBuffer的底层数据缓冲区及其长度。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetPrototype](#oh_jsvm_getprototype) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) object, [JSVM_Value](#jsvm_value) \*result) | 返回对象的原型。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetTypedarrayInfo](#oh_jsvm_gettypedarrayinfo) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) typedarray, [JSVM_TypedarrayType](#jsvm_typedarraytype) \*type, size_t \*length, void \*\*data, [JSVM_Value](#jsvm_value) \*arraybuffer, size_t \*byteOffset) | 返回类型化数组的各种属性。如果不需要该属性，则任何输出参数都可以是 NULL。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetDataviewInfo](#oh_jsvm_getdataviewinfo) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) dataview, size_t \*bytelength, void \*\*data, [JSVM_Value](#jsvm_value) \*arraybuffer, size_t \*byteOffset) | 返回DataView的各种属性。 如果不需要某一属性，则任何出参都可以设置为NULL。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetDateValue](#oh_jsvm_getdatevalue) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, double \*result) | 返回给定JavaScript Date的时间值的C双精度基础类型。如果调用成功，返回JSVM_OK。 如果传入一个非JavaScript Date类型的JSVM_Value，返回JSVM_DATA_EXPECTED。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetValueBool](#oh_jsvm_getvaluebool) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, bool \*result) | 返回给定JavaScript Boolean的C布尔基础类型等价值。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetValueDouble](#oh_jsvm_getvaluedouble) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, double \*result) | 返回给定JavaScript number的C双精度基础类型等价值。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetValueBigintInt64](#oh_jsvm_getvaluebigintint64) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, int64_t \*result, bool \*lossless) | 返回给定JavaScript BigInt的C int64_t基础类型等价值。 如果需要，它将截断该值，将lossless设置为false。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetValueBigintUint64](#oh_jsvm_getvaluebigintuint64) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, uint64_t \*result, bool \*lossless) | 返回给定JavaScript BigInt的C uint64_t基础类型等价值。 如果需要，它将截断该值，将lossless设置为false。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetValueBigintWords](#oh_jsvm_getvaluebigintwords) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, int \*signBit, size_t \*wordCount, uint64_t \*words) | 将单个BigInt值转换为符号位、64位小端数组和数组中的元素数。 signBit和words参数可以都设置为NULL。这种情况下，只获取wordCount。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetValueExternal](#oh_jsvm_getvalueexternal) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, void \*\*result) | 检索之前传递给OH_JSVM_CreateExternal()的外部数据指针。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetValueInt32](#oh_jsvm_getvalueint32) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, int32_t \*result) | 返回给定JavaScript number的C int32基础类型等价值。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetValueInt64](#oh_jsvm_getvalueint64) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, int64_t \*result) | 返回给定JavaScript number的C int64基础类型等价值。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetValueStringLatin1](#oh_jsvm_getvaluestringlatin1) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, char \*buf, size_t bufsize, size_t \*result) | 返回对应于传入值的ISO-8859-1编码字符串 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetValueStringUtf8](#oh_jsvm_getvaluestringutf8) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, char \*buf, size_t bufsize, size_t \*result) | 返回对应于传入值的UTF8编码字符串。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetValueStringUtf16](#oh_jsvm_getvaluestringutf16) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, char16_t \*buf, size_t bufsize, size_t \*result) | 基于传入的值，查询对应的采用UTF16编码的字符串。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetValueUint32](#oh_jsvm_getvalueuint32) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, uint32_t \*result) | 返回给定JavaScript number的C uint_32基础类型等价值。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetBoolean](#oh_jsvm_getboolean) ([JSVM_Env](#jsvm_env) env, bool value, [JSVM_Value](#jsvm_value) \*result) | 返回用于表示给定布尔值的JavaScript单例对象。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetGlobal](#oh_jsvm_getglobal) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) \*result) | 返回global对象。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetNull](#oh_jsvm_getnull) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) \*result) | 返回null对象。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetUndefined](#oh_jsvm_getundefined) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) \*result) | 返回Undefined对象。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CoerceToBool](#oh_jsvm_coercetobool) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, [JSVM_Value](#jsvm_value) \*result) | 实现抽象操作ToBoolean()。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CoerceToNumber](#oh_jsvm_coercetonumber) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, [JSVM_Value](#jsvm_value) \*result) | 实现抽象操作ToNumber()。 如果传入的值是对象，则函数可能会运行JavaScript代码。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CoerceToObject](#oh_jsvm_coercetoobject) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, [JSVM_Value](#jsvm_value) \*result) | 实现抽象操作ToObject()。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CoerceToString](#oh_jsvm_coercetostring) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, [JSVM_Value](#jsvm_value) \*result) | 实现抽象操作ToString()。 如果传入的值是对象，则函数可能会运行JavaScript代码。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_Typeof](#oh_jsvm_typeof) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, [JSVM_ValueType](#jsvm_valuetype) \*result) | 提供类似于在定义的对象上调用typeof运算符的行为。 不同点在于，该函数支持检测外部值；它将null检测为单独的类型， 而ECMAScript typeof将用于检测object。如果value的类型无效，则返回错误。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_Instanceof](#oh_jsvm_instanceof) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) object, [JSVM_Value](#jsvm_value) constructor, bool \*result) | 提供类似于在对象上调用instanceof运算符的行为。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_IsArray](#oh_jsvm_isarray) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, bool \*result) | 提供类似于在对象上调用IsArray的行为。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_IsArraybuffer](#oh_jsvm_isarraybuffer) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, bool \*result) | 检查传入的对象是否为ArrayBuffer。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_IsDate](#oh_jsvm_isdate) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, bool \*isDate) | 检查传入的Object是否为日期。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_IsTypedarray](#oh_jsvm_istypedarray) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, bool \*result) | 检查传入的Object是否为类型化数组。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_IsDataview](#oh_jsvm_isdataview) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, bool \*result) | 检查传入的对象是否是DataView。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_StrictEquals](#oh_jsvm_strictequals) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) lhs, [JSVM_Value](#jsvm_value) rhs, bool \*result) | 提供类似调用严格相等算法的行为。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_DetachArraybuffer](#oh_jsvm_detacharraybuffer) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) arraybuffer) | 提供类似于调用ArrayBuffer detach操作的行为。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_IsDetachedArraybuffer](#oh_jsvm_isdetachedarraybuffer) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, bool \*result) | 提供类似调用ArrayBuffer IsDetachedBuffer操作的行为。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetPropertyNames](#oh_jsvm_getpropertynames) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) object, [JSVM_Value](#jsvm_value) \*result) | 以字符数数组的形式返回object的可枚举属性的名称。 key为符号的object的属性将不会被包含在内。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetAllPropertyNames](#oh_jsvm_getallpropertynames) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) object, [JSVM_KeyCollectionMode](#jsvm_keycollectionmode) keyMode, [JSVM_KeyFilter](#jsvm_keyfilter) keyFilter, [JSVM_KeyConversion](#jsvm_keyconversion) keyConversion, [JSVM_Value](#jsvm_value) \*result) | 返回一个数组，其中包含此对象的可用属性的名称。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_SetProperty](#oh_jsvm_setproperty) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) object, [JSVM_Value](#jsvm_value) key, [JSVM_Value](#jsvm_value) value) | 为传入的object设置一个属性。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetProperty](#oh_jsvm_getproperty) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) object, [JSVM_Value](#jsvm_value) key, [JSVM_Value](#jsvm_value) \*result) | 从传入的object中获取请求的属性。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_HasProperty](#oh_jsvm_hasproperty) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) object, [JSVM_Value](#jsvm_value) key, bool \*result) | 检查传入的Object是否具有指定命名的属性。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_DeleteProperty](#oh_jsvm_deleteproperty) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) object, [JSVM_Value](#jsvm_value) key, bool \*result) | 尝试从object中删除key自己的属性。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_HasOwnProperty](#oh_jsvm_hasownproperty) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) object, [JSVM_Value](#jsvm_value) key, bool \*result) | 检查传入的Object是否具有命名的自己的属性。key必须是string或symbol， 否则将抛出错误。JSVM-API不会执行任何数据类型之间的转换。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_SetNamedProperty](#oh_jsvm_setnamedproperty) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) object, const char \*utf8name, [JSVM_Value](#jsvm_value) value) | 此方法等效于调用OH_JSVM_SetProperty， 其中，通过utf8Name传入的字符串用于创建JSVM_Value。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetNamedProperty](#oh_jsvm_getnamedproperty) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) object, const char \*utf8name, [JSVM_Value](#jsvm_value) \*result) | 此方法等效于调用OH_JSVM_GetProperty， 其中，通过utf8Name传入的字符串用于创建JSVM_Value。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_HasNamedProperty](#oh_jsvm_hasnamedproperty) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) object, const char \*utf8name, bool \*result) | 此方法等效于使用从作为utf8Name传入的字符串创建的JSVM_Value 调用OH_JSVM_HasProperty。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_SetElement](#oh_jsvm_setelement) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) object, uint32_t index, [JSVM_Value](#jsvm_value) value) | 在传入的Object上设置一个元素。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetElement](#oh_jsvm_getelement) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) object, uint32_t index, [JSVM_Value](#jsvm_value) \*result) | 获取请求索引处的元素。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_HasElement](#oh_jsvm_haselement) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) object, uint32_t index, bool \*result) | 如果传入的Object在指定的索引处有一个元素，则此JSVM-API返回true。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_DeleteElement](#oh_jsvm_deleteelement) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) object, uint32_t index, bool \*result) | 尝试从object中删除指定index处的元素。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_DefineProperties](#oh_jsvm_defineproperties) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) object, size_t propertyCount, const [JSVM_PropertyDescriptor](_j_s_v_m___property_descriptor.md) \*properties) | 通过此方法可以在给定对象上高效定义多个属性， 这些属性使用属性描述符进行定义。通过一个属性描述符的数组， 此API将为对象依次设置数组中的属性。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_ObjectFreeze](#oh_jsvm_objectfreeze) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) object) | 冻结指定的对象。这样可以防止为其添加新的属性、删除现有属性、更改现有属性的 可枚举性、可配置性或可写性、或者更改现有属性的值。它还可以防止改变对象的原型。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_ObjectSeal](#oh_jsvm_objectseal) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) object) | 封装指定的对象。这样可以防止为其添加新的属性并且将所有现有属性标记为不可配置。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CallFunction](#oh_jsvm_callfunction) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) recv, [JSVM_Value](#jsvm_value) func, size_t argc, const [JSVM_Value](#jsvm_value) \*argv, [JSVM_Value](#jsvm_value) \*result) | 支持从native代码调用JavaScript函数对象， 这是从native代码回调到JavaScript的主要机制。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateFunction](#oh_jsvm_createfunction) ([JSVM_Env](#jsvm_env) env, const char \*utf8name, size_t length, [JSVM_Callback](#jsvm_callback) cb, [JSVM_Value](#jsvm_value) \*result) | 支持在native代码中创建函数对象，这是从JavaScript调用native代码的主要机制。 在此调用之后，新创建的函数在脚本中不再自动可见。相反，必须在JavaScript可见的任何对象上显示设置属性， 才能从脚本访问该函数。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetCbInfo](#oh_jsvm_getcbinfo) ([JSVM_Env](#jsvm_env) env, [JSVM_CallbackInfo](#jsvm_callbackinfo) cbinfo, size_t \*argc, [JSVM_Value](#jsvm_value) \*argv, [JSVM_Value](#jsvm_value) \*thisArg, void \*\*data) | 此方法在回调函数中用于检索有关调用的详细信息， 例如来自给定回调信息的参数和this指针。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetNewTarget](#oh_jsvm_getnewtarget) ([JSVM_Env](#jsvm_env) env, [JSVM_CallbackInfo](#jsvm_callbackinfo) cbinfo, [JSVM_Value](#jsvm_value) \*result) | 返回构造函数调用的new target。 如果当前回调不是构造函数调用，结果为NULL。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_NewInstance](#oh_jsvm_newinstance) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) constructor, size_t argc, const [JSVM_Value](#jsvm_value) \*argv, [JSVM_Value](#jsvm_value) \*result) | 使用给定的JSVM_Value表示的构造函数来实例化新的JavaScript值。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_DefineClass](#oh_jsvm_defineclass) ([JSVM_Env](#jsvm_env) env, const char \*utf8name, size_t length, [JSVM_Callback](#jsvm_callback) constructor, size_t propertyCount, const [JSVM_PropertyDescriptor](_j_s_v_m___property_descriptor.md) \*properties, [JSVM_Value](#jsvm_value) \*result) | 定义一个JavaScript类。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_Wrap](#oh_jsvm_wrap) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) jsObject, void \*nativeObject, [JSVM_Finalize](#jsvm_finalize) finalizeCb, void \*finalizeHint, [JSVM_Ref](#jsvm_ref) \*result) | 在JavaScript对象中封装native实例。native实例 后续可以通过OH_JSVM_Unwrap()进行检索。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_Unwrap](#oh_jsvm_unwrap) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) jsObject, void \*\*result) | 当JavaScript代码调用类的方法或属性访问器时，对应的JSVM_Callback将被调用。 如果回调是针对实例方法或访问器的，则回调的this参数是封装器对象；然后可以通过调用 封装器对象的OH_JSVM_Unwrap()获得作为调用目标的C++实例。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_RemoveWrap](#oh_jsvm_removewrap) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) jsObject, void \*\*result) | 使用OH_JSVM_Wrap()检索先前封装在JavaScript对象js_object中的native实例并移除封装。 如果finalize回调与封装相关联，则当JavaScript对象被垃圾回收时将不再调用它。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_TypeTagObject](#oh_jsvm_typetagobject) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, const [JSVM_TypeTag](_j_s_v_m___type_tag.md) \*typeTag) | 将typeTag指针的值与JavaScript对象或外部值相关联。可调用OH_JSVM_CheckObjectTypeTag() 判断附加在对象上的标记类型，以确保对象的类型正确。如果对象已经有关联的类型标记，则返回JSVM_INVALID_ARG。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CheckObjectTypeTag](#oh_jsvm_checkobjecttypetag) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, const [JSVM_TypeTag](_j_s_v_m___type_tag.md) \*typeTag, bool \*result) | 将类型标签typeTag与JavaScript对象或外部值上的标签作对比。如果找到相同标签， 设置result为true，否则为false。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_AddFinalizer](#oh_jsvm_addfinalizer) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) jsObject, void \*finalizeData, [JSVM_Finalize](#jsvm_finalize) finalizeCb, void \*finalizeHint, [JSVM_Ref](#jsvm_ref) \*result) | 为JavaScript对象添加JSVM_Finalize回调，当JavaScript对象被垃圾回收时调用该回调函数。 可以在单个JavaScript对象上多次调用OH_JSVM_AddFinalizer。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetVersion](#oh_jsvm_getversion) ([JSVM_Env](#jsvm_env) env, uint32_t \*result) | 返回JSVM运行时支持的最高JSVM-API版本。 后续将新增JSVM-API，以便支持更多的功能。引入该API的目的：在支持某功能的JSVM版本， 可以使用新的功能；在不支持某功能的JSVM版本，可以提供回调行为。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_GetVMInfo](#oh_jsvm_getvminfo) ([JSVM_VMInfo](_j_s_v_m___v_m_info.md) \*result) | 返回虚拟机的信息。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_AdjustExternalMemory](#oh_jsvm_adjustexternalmemory) ([JSVM_Env](#jsvm_env) env, int64_t changeInBytes, int64_t \*result) | 此函数将因JavaScript对象而保持活跃的外部分配的内存大小通知给底层虚拟机。 注册外部分配的内存将比其他方式更频繁地触发全局垃圾回收。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_MemoryPressureNotification](#oh_jsvm_memorypressurenotification) ([JSVM_Env](#jsvm_env) env, [JSVM_MemoryPressureLevel](#jsvm_memorypressurelevel) level) | 通知虚拟机系统内存不足并有选择地触发垃圾回收。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreatePromise](#oh_jsvm_createpromise) ([JSVM_Env](#jsvm_env) env, [JSVM_Deferred](#jsvm_deferred) \*deferred, [JSVM_Value](#jsvm_value) \*promise) | 创建一个延迟对象和一个JavaScript promise。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_ResolveDeferred](#oh_jsvm_resolvedeferred) ([JSVM_Env](#jsvm_env) env, [JSVM_Deferred](#jsvm_deferred) deferred, [JSVM_Value](#jsvm_value) resolution) | 通过与之关联的延迟对象来解析JavaScript promise。 它只能用于解析对应的可用的延迟对象的JavaScript Promise。 这意味着Promise必须使用OH_JSVM_CreatePromise()创建，并且 从该调用返回的对象必须保留，才能将其传递给此API。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_RejectDeferred](#oh_jsvm_rejectdeferred) ([JSVM_Env](#jsvm_env) env, [JSVM_Deferred](#jsvm_deferred) deferred, [JSVM_Value](#jsvm_value) rejection) | 通过与之关联的延迟对象来拒绝JavaScript Promise。 它只能用于拒绝对应的可用延迟对象的JavaScript Promise。 这意味着Promise必须使用OH_JSVM_CreatePromise()创建，并且 从该调用返回的对象必须保留，才能将其传递给此API。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_IsPromise](#oh_jsvm_ispromise) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) value, bool \*isPromise) | 查询Promise是否为原生Promise对象。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_JsonParse](#oh_jsvm_jsonparse) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) jsonString, [JSVM_Value](#jsvm_value) \*result) | 解析JSON字符串，并返回成功解析的值。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_JsonStringify](#oh_jsvm_jsonstringify) ([JSVM_Env](#jsvm_env) env, [JSVM_Value](#jsvm_value) jsonObject, [JSVM_Value](#jsvm_value) \*result) | 将对象字符串化，并返回成功转换后的字符串。 | 
| JSVM_EXTERN [JSVM_Status](#jsvm_status)[OH_JSVM_CreateSnapshot](#oh_jsvm_createsnapshot) ([JSVM_VM](#jsvm_vm) vm, size_t contextCount, const [JSVM_Env](#jsvm_env) \*contexts, const char \*\*blobData, size_t \*blobSize) | 创建虚拟机的启动快照。 | 


## 宏定义说明


### JSVM_AUTO_LENGTH

```
#define JSVM_AUTO_LENGTH   SIZE_MAX
```

**描述**

自动长度。

**起始版本：** 11


## 类型定义说明


### JSVM_Callback

```
typedef JSVM_CallbackStruct* JSVM_Callback
```

**描述**

用户提供的native函数的函数指针类型，这些函数通过JSVM-API接口暴露给JavaScript。

**起始版本：** 11


### JSVM_CallbackInfo

```
typedef struct JSVM_CallbackInfo__* JSVM_CallbackInfo
```

**描述**

表示传递给回调函数的不透明数据类型。可用于获取调用该函数的上下文的附加信息。

**起始版本：** 11


### JSVM_Deferred

```
typedef struct JSVM_Deferred__* JSVM_Deferred
```

**描述**

表示Promise延迟对象。

**起始版本：** 11


### JSVM_Env

```
typedef struct JSVM_Env__* JSVM_Env
```

**描述**

表示虚拟机特定状态的上下文环境，需要在调用native函数时作为参数传递， 并且传递给后续任何的JSVM-API嵌套调用。

**起始版本：** 11


### JSVM_EnvScope

```
typedef struct JSVM_EnvScope__* JSVM_EnvScope
```

**描述**

表示用于控制附加到当前虚拟机实例的环境。只有当线程通过 OH_JSVM_OpenEnvScope进入该环境的JSVM_EnvScope后，该环境才 对线程的虚拟机实例可用。

**起始版本：** 11


### JSVM_EscapableHandleScope

```
typedef struct JSVM_EscapableHandleScope__* JSVM_EscapableHandleScope
```

**描述**

表示一种特殊类型的handle scope，用于将在特定handle scope内创建的值返回到父作用域。

**起始版本：** 11


### JSVM_Finalize

```
typedef void(JSVM_CDECL* JSVM_Finalize) (JSVM_Env env, void *finalizeData, void *finalizeHint)
```

**描述**

函数指针类型，当native类型对象或数据与JS对象被关联时，传入该指针。该函数将会 在关联的JS对象被GC回收时被调用，用以执行native的清理动作。

**起始版本：** 11


### JSVM_HandleScope

```
typedef struct JSVM_HandleScope__* JSVM_HandleScope
```

**描述**

表示JavaScript值的作用域，用于控制和修改在特定范围内创建的对象的生命周期。 通常，JSVM-API值是在JSVM_HandleScope的上下文中创建的。当从JavaScript调用native方法时， 将存在默认JSVM_HandleScope。如果用户没有显式创建新的JSVM_HandleScope，将在默认 JSVM_HandleScope中创建JSVM-API值。对于native方法执行之外的任何代码调用（例如，在libuv回调调用期间）， 模块需要在调用任何可能导致创建JavaScript值的函数之前创建一个作用域。JSVM_HandleScope是使用 OH_JSVM_OpenHandleScope创建的，并使用OH_JSVM_CloseHandleScope销毁的。 关闭作用域代表向GC指示在JSVM_HandleScope作用域的生命周期内创建的所有JSVM_Value将不再从当前堆的栈帧中引用。

**起始版本：** 11


### JSVM_Ref

```
typedef struct JSVM_Ref__* JSVM_Ref
```

**描述**

表示JavaScript值的引用。

**起始版本：** 11


### JSVM_Script

```
typedef struct JSVM_Script__* JSVM_Script
```

**描述**

表示一段JavaScript代码。

**起始版本：** 11


### JSVM_Value

```
typedef struct JSVM_Value__* JSVM_Value
```

**描述**

表示JavaScript值。

**起始版本：** 11


### JSVM_VM

```
typedef struct JSVM_VM__* JSVM_VM
```

**描述**

表示JavaScript虚拟机实例。

**起始版本：** 11


### JSVM_VMScope

```
typedef struct JSVM_VMScope__* JSVM_VMScope
```

**描述**

表示JavaScript虚拟机作用域。

**起始版本：** 11


## 枚举类型说明


### JSVM_KeyCollectionMode

```
enum JSVM_KeyCollectionMode
```

**描述**

限制查找属性的范围。

**起始版本：** 11

| 枚举值 | 描述 | 
| -------- | -------- |
| JSVM_KEY_INCLUDE_PROTOTYPES | 也包含对象原型链上的属性。 | 
| JSVM_KEY_OWN_ONLY | 仅包含对象自身属性。 | 


### JSVM_KeyConversion

```
enum JSVM_KeyConversion
```

**描述**

键转换选项。

**起始版本：** 11

| 枚举值 | 描述 | 
| -------- | -------- |
| JSVM_KEY_KEEP_NUMBERS | 将返回整数索引的数字。 | 
| JSVM_KEY_NUMBERS_TO_STRINGS | 将整数索引转换为字符串。 | 


### JSVM_KeyFilter

```
enum JSVM_KeyFilter
```

**描述**

属性过滤器，可以通过使用or来构造一个复合过滤器。

**起始版本：** 11

| 枚举值 | 描述 | 
| -------- | -------- |
| JSVM_KEY_ALL_PROPERTIES | 所有属性的键。 | 
| JSVM_KEY_WRITABLE | 可写的键。 | 
| JSVM_KEY_ENUMERABLE | 可枚举的键。 | 
| JSVM_KEY_CONFIGURABLE | 可配置的键。 | 
| JSVM_KEY_SKIP_STRINGS | 排除字符串类型的键。 | 
| JSVM_KEY_SKIP_SYMBOLS | 排除符号类型的键。 | 


### JSVM_MemoryPressureLevel

```
enum JSVM_MemoryPressureLevel
```

**描述**

内存压力水平。

**起始版本：** 11

| 枚举值 | 描述 | 
| -------- | -------- |
| JSVM_MEMORY_PRESSURE_LEVEL_NONE | 无压力。 | 
| JSVM_MEMORY_PRESSURE_LEVEL_MODERATE | 中等压力。 | 
| JSVM_MEMORY_PRESSURE_LEVEL_CRITICAL | 临界压力。 | 


### JSVM_PropertyAttributes

```
enum JSVM_PropertyAttributes
```

**描述**

用于控制JavaScript对象属性的行为。

**起始版本：** 11

| 枚举值 | 描述 | 
| -------- | -------- |
| JSVM_DEFAULT | 没有在属性上设置显式属性。 | 
| JSVM_WRITABLE | 该属性是可写的。 | 
| JSVM_ENUMERABLE | 该属性是可枚举的。 | 
| JSVM_CONFIGURABLE | 该属性是可配置的。 | 
| JSVM_STATIC | 该属性将被定义为类的静态属性，而不是默认的实例属性。这仅由OH_JSVM_DefineClass使用。 | 
| JSVM_DEFAULT_METHOD | 就像JS类中的方法一样，该属性是可配置和可写的，但不可枚举。 | 
| JSVM_DEFAULT_JSPROPERTY | 就像JavaScript中通过赋值设置的属性一样，属性是可写、可枚举和可配置的。 | 


### JSVM_Status

```
enum JSVM_Status
```

**描述**

表示JSVM-API调用成功或失败的完整状态码。

**起始版本：** 11

| 枚举值 | 描述 | 
| -------- | -------- |
| JSVM_OK | 成功状态。 | 
| JSVM_INVALID_ARG | 无效的状态。 | 
| JSVM_OBJECT_EXPECTED | 期待传入对象类型。 | 
| JSVM_STRING_EXPECTED | 期望传入字符串类型。 | 
| JSVM_NAME_EXPECTED | 期望传入名字类型。 | 
| JSVM_FUNCTION_EXPECTED | 期待传入函数类型。 | 
| JSVM_NUMBER_EXPECTED | 期待传入数字类型。 | 
| JSVM_BOOLEAN_EXPECTED | 期待传入布尔类型。 | 
| JSVM_ARRAY_EXPECTED | 期待传入数组类型。 | 
| JSVM_GENERIC_FAILURE | 泛型失败状态。 | 
| JSVM_PENDING_EXCEPTION | 挂起异常状态。 | 
| JSVM_CANCELLED | 取消状态。 | 
| JSVM_ESCAPE_CALLED_TWICE | 转义调用了两次。 | 
| JSVM_HANDLE_SCOPE_MISMATCH | 句柄作用域不匹配。 | 
| JSVM_CALLBACK_SCOPE_MISMATCH | 回调作用域不匹配。 | 
| JSVM_QUEUE_FULL | 队列满。 | 
| JSVM_CLOSING | 关闭中。 | 
| JSVM_BIGINT_EXPECTED | 期望传入Bigint类型。 | 
| JSVM_DATE_EXPECTED | 期望传入日期类型。 | 
| JSVM_ARRAYBUFFER_EXPECTED | 期望传入ArrayBuffer类型。 | 
| JSVM_DETACHABLE_ARRAYBUFFER_EXPECTED | 可分离的数组缓冲区预期状态。 | 
| JSVM_WOULD_DEADLOCK | 将死锁状态。 | 
| JSVM_NO_EXTERNAL_BUFFERS_ALLOWED | 不允许外部缓冲区。 | 
| JSVM_CANNOT_RUN_JS | 不能执行JS。 | 


### JSVM_TypedarrayType

```
enum JSVM_TypedarrayType
```

**描述**

描述TypedArray的类型。

**起始版本：** 11

| 枚举值 | 描述 | 
| -------- | -------- |
| JSVM_INT8_ARRAY | int8类型。 | 
| JSVM_UINT8_ARRAY | uint8类型。 | 
| JSVM_UINT8_CLAMPED_ARRAY | uint8固定类型。 | 
| JSVM_INT16_ARRAY | int16类型。 | 
| JSVM_UINT16_ARRAY | uint16类型。 | 
| JSVM_INT32_ARRAY | int32类型。 | 
| JSVM_UINT32_ARRAY | uint32类型。 | 
| JSVM_FLOAT32_ARRAY | float32类型。 | 
| JSVM_FLOAT64_ARRAY | float64类型。 | 
| JSVM_BIGINT64_ARRAY | bigint64类型。 | 
| JSVM_BIGUINT64_ARRAY | biguint64类型。 | 


### JSVM_ValueType

```
enum JSVM_ValueType
```

**描述**

描述JSVM_Value的类型。

**起始版本：** 11

| 枚举值 | 描述 | 
| -------- | -------- |
| JSVM_UNDEFINED | 未定义类型。 | 
| JSVM_NULL | Null类型。 | 
| JSVM_BOOLEAN | 布尔类型。 | 
| JSVM_NUMBER | 数字类型。 | 
| JSVM_STRING | 字符串类型。 | 
| JSVM_SYMBOL | 符号类型。 | 
| JSVM_OBJECT | 对象类型。 | 
| JSVM_FUNCTION | 函数类型。 | 
| JSVM_EXTERNAL | 外部类型。 | 
| JSVM_BIGINT | bigint类型。 | 


## 函数说明


### OH_JSVM_AddFinalizer()

```
JSVM_EXTERN JSVM_Status OH_JSVM_AddFinalizer (JSVM_Env env, JSVM_Value jsObject, void * finalizeData, JSVM_Finalize finalizeCb, void * finalizeHint, JSVM_Ref * result )
```

**描述**

为JavaScript对象添加JSVM_Finalize回调，当JavaScript对象被垃圾回收时调用该回调函数。 可以在单个JavaScript对象上多次调用OH_JSVM_AddFinalizer。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| jsObject | 关联native数据的JavaScript对象。 | 
| finalizeData | 要传递给finalizeCb的可选数据。 | 
| finalizeCb | 当JavaScript对象被垃圾回收时，将用于释放native 数据的原生回调。JSVM_Finalize提供了更多详细信息。 | 
| finalizeHint | 传递给finalize回调的可选上下文提示。 | 
| result | 可选的对JavaScript对象的引用。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_INVALID_ARG。


### OH_JSVM_AdjustExternalMemory()

```
JSVM_EXTERN JSVM_Status OH_JSVM_AdjustExternalMemory (JSVM_Env env, int64_t changeInBytes, int64_t * result )
```

**描述**

此函数将因JavaScript对象而保持活跃的外部分配的内存大小通知给底层虚拟机。 注册外部分配的内存将比其他方式更频繁地触发全局垃圾回收。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| changeInBytes | 因JavaScript对象而保持活动状态的外部分配内存的变化。 | 
| result | 调整值。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CallFunction()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CallFunction (JSVM_Env env, JSVM_Value recv, JSVM_Value func, size_t argc, const JSVM_Value * argv, JSVM_Value * result )
```

**描述**

支持从native代码调用JavaScript函数对象， 这是从native代码回调到JavaScript的主要机制。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| recv | 传递给被调用函数的this值。 | 
| func | 表示将调用的JavaScript函数。 | 
| argc | argv数组中的元素个数。 | 
| argv | JSVM_values数组，表示将作为参数传递给函数的JavaScript值。 | 
| result | 表示返回的JavaScript对象。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_PENDING_EXCEPTION或JSVM_GENERIC_FAILURE。


### OH_JSVM_CheckObjectTypeTag()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CheckObjectTypeTag (JSVM_Env env, JSVM_Value value, const JSVM_TypeTag * typeTag, bool * result )
```

**描述**

将类型标签typeTag与JavaScript对象或外部值上的标签作对比。如果找到相同标签， 设置result为true，否则为false。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 待检查类型标记的JavaScript对象或外部值。 | 
| typeTag | 用于比较在对象上找到的任何标签的标签。 | 
| result | 表示指定的类型标记是否与对象上的类型标记匹配。如果在对象上找不到该类型标记，也会返回false。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_CloseEnvScope()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CloseEnvScope (JSVM_Env env, JSVM_EnvScope scope )
```

**描述**

关闭环境作用域。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 目标环境，JSVM-API接口将在该环境下调用。 | 
| scope | 将要关闭的环境作用域。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CloseEscapableHandleScope()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CloseEscapableHandleScope (JSVM_Env env, JSVM_EscapableHandleScope scope )
```

**描述**

关闭传入的作用域。必须按照创建作用域的相反顺序关闭作用域。 即使存在挂起的JavaScript异常，也可以调用此JSVM_API。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| scope | 表示要关闭的作用域。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_HANDLE_SCOPE_MISMATCH。


### OH_JSVM_CloseHandleScope()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CloseHandleScope (JSVM_Env env, JSVM_HandleScope scope )
```

**描述**

关闭传入的作用域。必须按照创建作用域的相反顺序关闭作用域。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| scope | 表示要关闭的作用域。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CloseVMScope()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CloseVMScope (JSVM_VM vm, JSVM_VMScope scope )
```

**描述**

关闭虚拟机实例的虚拟机作用域。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| vm | 目标虚拟机实例。 | 
| scope | 将要关闭的虚拟机作用域。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CoerceToBool()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CoerceToBool (JSVM_Env env, JSVM_Value value, JSVM_Value * result )
```

**描述**

实现抽象操作ToBoolean()。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 要强制转换的JavaScript值。 | 
| result | 代表强制的JavaScript Boolean。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CoerceToNumber()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CoerceToNumber (JSVM_Env env, JSVM_Value value, JSVM_Value * result )
```

**描述**

实现抽象操作ToNumber()。 如果传入的值是对象，则函数可能会运行JavaScript代码。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 要强制转换的JavaScript值。 | 
| result | 代表强制的JavaScript number。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CoerceToObject()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CoerceToObject (JSVM_Env env, JSVM_Value value, JSVM_Value * result )
```

**描述**

实现抽象操作ToObject()。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 要强制转换的JavaScript值。 | 
| result | 代表强制的JavaScript object。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CoerceToString()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CoerceToString (JSVM_Env env, JSVM_Value value, JSVM_Value * result )
```

**描述**

实现抽象操作ToString()。 如果传入的值是对象，则函数可能会运行JavaScript代码。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 要强制转换的JavaScript值。 | 
| result | 代表强制的JavaScript string。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CompileScript()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CompileScript (JSVM_Env env, JSVM_Value script, const uint8_t * cachedData, size_t cacheDataLength, bool eagerCompile, bool * cacheRejected, JSVM_Script * result )
```

**描述**

编译一串JavaScript代码，并返回编译后的脚本。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 目标环境，JSVM-API接口将在该环境下调用。 | 
| script | 包含要编译的脚本的JavaScript代码。 | 
| cachedData | 可选。脚本的代码缓存数据。 | 
| cacheDataLength | cachedData数组的长度。 | 
| eagerCompile | 是否立即编译脚本。 | 
| cacheRejected | 代码缓存是否被编译拒绝。 | 
| result | 编译后的脚本。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_STRING_EXPECTED或JSVM_GENERIC_FAILURE。


### OH_JSVM_CreateArray()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateArray (JSVM_Env env, JSVM_Value * result )
```

**描述**

返回对应于JavaScript Array类型的JSVM-API值。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| result | 代表JavaScript Array的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CreateArraybuffer()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateArraybuffer (JSVM_Env env, size_t byteLength, void ** data, JSVM_Value * result )
```

**描述**

返回JavaScript ArrayBuffer类型对应的JSVM-API值。ArrayBuffer用于 表示固定长度的二进制数据缓冲区。通常用作TypedArray对象的后备缓冲区。 分配的ArrayBuffer有一个底层字节缓冲区，其大小由传入的length参数决定。 底层缓冲区可选择返回给调用方，调用方可直接操作该缓冲区。 此缓冲区只能直接从native代码写入。如果想从JavaScript写入该缓冲区， 需创建TypedArray或DataView对象。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| byteLength | 要创建的数组缓冲区的字节长度。 | 
| data | 指向ArrayBuffer的底层字节缓冲区的指针。data可以选择性地通过传递NULL来忽略。 | 
| result | 代表JavaScript ArrayBuffer的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CreateArrayWithLength()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateArrayWithLength (JSVM_Env env, size_t length, JSVM_Value * result )
```

**描述**

返回对应于JavaScript Array类型的JSVM-API值。Array 的长度属性设置为传入的长度参数。但是，不保证底层缓冲区在创建 数组时由VM预先分配。该行为留给底层VM实现。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| length | 数组的初始长度。 | 
| result | 代表JavaScript Array的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CreateBigintInt64()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateBigintInt64 (JSVM_Env env, int64_t value, JSVM_Value * result )
```

**描述**

将C int64_t类型的值转换为JavaScript BigInt类型。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 要在JavaScript中表现的整数值。 | 
| result | 表示JavaScript BigInt类型的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CreateBigintUint64()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateBigintUint64 (JSVM_Env env, uint64_t value, JSVM_Value * result )
```

**描述**

将C uint64_t类型的值转换为JavaScript BigInt类型。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 要在JavaScript中表示的无符号整数值。 | 
| result | 代表JavaScript BigInt类型的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CreateBigintWords()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateBigintWords (JSVM_Env env, int signBit, size_t wordCount, const uint64_t * words, JSVM_Value * result )
```

**描述**

将一组无符号64位字转换为单个BigInt值。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| signBit | 确定生成的BigInt是正数还是负数。 | 
| wordCount | words数组的长度。 | 
| words | uint64_t little-endian 64位字数组。 | 
| result | 代表JavaScript BigInt类型的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_INVALID_ARG或JSVM_GENERIC_FAILURE。


### OH_JSVM_CreateCodeCache()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateCodeCache (JSVM_Env env, JSVM_Script script, const uint8_t ** data, size_t * length )
```

**描述**

为编译后的脚本创建代码缓存。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 目标环境，JSVM-API接口将在该环境下调用。 | 
| script | 目标编译脚本。 | 
| data | 代码缓存的数据。 | 
| length | 代码缓存数据的长度。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_CreateDataview()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateDataview (JSVM_Env env, size_t length, JSVM_Value arraybuffer, size_t byteOffset, JSVM_Value * result )
```

**描述**

基于已有的ArrayBuffer对象，创建一个JavaScript DataView对象。DataView 对象在底层数据缓冲区上提供了一个类似数组的视图，其中的元素可以具有不同的大小和类型。 要求：二进制的length + byteOffset 小于或等于传入的数组的大小（以字节为单位）。否则，将抛出范围错误（RangeError）。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| length | DataView中的元素个数。 | 
| arraybuffer | 位于DataView底层的ArrayBuffer。 | 
| byteOffset | ArrayBuffer中的字节偏移量，指示投影DataView的开始位置。 | 
| result | 表示JavaScript DataView对象的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_PENDING_EXCEPTION。


### OH_JSVM_CreateDate()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateDate (JSVM_Env env, double time, JSVM_Value * result )
```

**描述**

分配一个JavaScript Date对象。此API不处理闰秒。 这是因为ECMAScript遵循POSIX时间规范，对闰秒进行忽略。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| time | 自1970年1月1日UTC以来的ECMAScript时间值（以毫秒为单位）。 | 
| result | 表示JavaScript Date对象的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_CreateDouble()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateDouble (JSVM_Env env, double value, JSVM_Value * result )
```

**描述**

将C double类型的值转换为JavaScript number类型。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 要在JavaScript中表现的双精度值。 | 
| result | 代表JavaScript number类型的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CreateEnv()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateEnv (JSVM_VM vm, size_t propertyCount, const JSVM_PropertyDescriptor * properties, JSVM_Env * result )
```

**描述**

基于新环境上下文的可选属性，创建一个新环境。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| vm | 虚拟机实例，新环境将在该实例中创建。 | 
| propertyCount | 属性数组中元素的个数。 | 
| properties | 属性描述符的数组。 | 
| result | 创建的新环境。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CreateEnvFromSnapshot()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateEnvFromSnapshot (JSVM_VM vm, size_t index, JSVM_Env * result )
```

**描述**

基于虚拟机的起始快照，创建一个新的环境。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| vm | 虚拟机实例，新环境将在该实例中创建。 | 
| index | 环境在快照中的索引。 | 
| result | 创建的新环境。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_CreateError()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateError (JSVM_Env env, JSVM_Value code, JSVM_Value msg, JSVM_Value * result )
```

**描述**

返回带有所提供文本的JavaScript Error。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| code | 可选的JSVM_Value，带有与错误关联的错误代码的字符串。 | 
| msg | 引用JavaScript string用作Error的消息。 | 
| result | 表示创建的错误。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_STRING_EXPECTED。


### OH_JSVM_CreateExternal()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateExternal (JSVM_Env env, void * data, JSVM_Finalize finalizeCb, void * finalizeHint, JSVM_Value * result )
```

**描述**

分配一个带有外部数据的JavaScript值。这用于通过JavaScript代码传递外部数据。 后续可以使用OH_JSVM_GetValueExternal由native代码检索。 该API添加了一个JSVM_Finalize回调，当刚刚创建的JavaScript对象被垃圾回收时将调用该回调。 创建的值不是一个对象，因此不支持附加属性。它被认为是一个独特的值类型： 使用外部值调用OH_JSVM_Typeof()会生成JSVM_EXTERNAL。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| data | 指向外部数据的原始指针。 | 
| finalizeCb | 收集外部值时调用的可选回调。JSVM_Finalize提供了更多详细信息。 | 
| finalizeHint | 在收集期间传递给最终回调的可选提示。 | 
| result | 表示外部值的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CreateFunction()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateFunction (JSVM_Env env, const char * utf8name, size_t length, JSVM_Callback cb, JSVM_Value * result )
```

**描述**

支持在native代码中创建函数对象，这是从JavaScript调用native代码的主要机制。 在此调用之后，新创建的函数在脚本中不再自动可见。相反，必须在JavaScript可见的任何对象上显示设置属性， 才能从脚本访问该函数。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| utf8Name | 编码为UTF8的函数的可选名称。这在JavaScript中是可见的， 作为新函数对象的name属性。 | 
| length | utf8name的长度（以字节为单位）或JSVM_AUTO_LENGTH（如果以 null 结尾）。 | 
| cb | 调用此函数对象时应调用的native函数。详情请参考JSVM_Callback。 | 
| result | 表示新创建函数的JavaScript函数对象。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CreateInt32()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateInt32 (JSVM_Env env, int32_t value, JSVM_Value * result )
```

**描述**

将C int32_t类型的值转换为JavaScript number类型。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 要在JavaScript中表示的整数值。 | 
| result | 表示JavaScript number类型的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CreateInt64()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateInt64 (JSVM_Env env, int64_t value, JSVM_Value * result )
```

**描述**

将C int64_t类型的值转换为JavaScript number类型。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 要在JavaScript中表示的整数值。 | 
| result | 代表JavaScript number类型的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CreateObject()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateObject (JSVM_Env env, JSVM_Value * result )
```

**描述**

分配一个默认的JavaScript对象。该函数功能等同于在JavaScript中执行new Object()。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| result | 表示JavaScript对象的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CreatePromise()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreatePromise (JSVM_Env env, JSVM_Deferred * deferred, JSVM_Value * promise )
```

**描述**

创建一个延迟对象和一个JavaScript promise。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| deferred | 一个新创建的延迟对象，后续可以传递给OH_JSVM_ResolveDeferred()或 [OH_JSVM_RejectDeferred()](#oh_jsvm_rejectdeferred)以解析resp。或拒绝相关的Promise。 | 
| promise | 与延迟对象关联的JavaScript Promise。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_CreateRangeError()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateRangeError (JSVM_Env env, JSVM_Value code, JSVM_Value msg, JSVM_Value * result )
```

**描述**

返回带有所提供文本的JavaScript RangeError。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| code | 可选的JSVM_Value，带有与错误关联的错误代码的字符串。 | 
| msg | 引用JavaScript string用作Error的消息。 | 
| result | 表示创建的错误。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_STRING_EXPECTED。


### OH_JSVM_CreateReference()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateReference (JSVM_Env env, JSVM_Value value, uint32_t initialRefcount, JSVM_Ref * result )
```

**描述**

对传入的值创建一个具有指定引用计数的新引用。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 正在为其创建引用的JSVM_Value。 | 
| initialRefcount | 新引用的初始引用计数。 | 
| result | 指向新的引用。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CreateSnapshot()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateSnapshot (JSVM_VM vm, size_t contextCount, const JSVM_Env * contexts, const char ** blobData, size_t * blobSize )
```

**描述**

创建虚拟机的启动快照。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| vm | 目标环境，API接口将在该环境下调用。 | 
| contextCount | 上下文个数。 | 
| contexts | 要添加到快照的上下文数组。 | 
| blobData | 快照数据。 | 
| blobSize | 快照数据的大小。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_CreateStringLatin1()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateStringLatin1 (JSVM_Env env, const char * str, size_t length, JSVM_Value * result )
```

**描述**

将采用ISO-8859-1编码的C字符串转换为JavaScript string值。 复制原生字符串。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| str | 表示ISO-8859-1编码的字符串的字符缓冲区。 | 
| length | 字符串的长度，以字节为单位。如果它以null结尾，则为JSVM_AUTO_LENGTH。 | 
| result | 表示JavaScript字符串的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CreateStringUtf16()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateStringUtf16 (JSVM_Env env, const char16_t * str, size_t length, JSVM_Value * result )
```

**描述**

将采用UTF16-LE编码的C字符串转换为JavaScript字符串值。 复制原生字符串。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| str | 表示UTF16-LE编码的字符串的字符缓冲区。 | 
| length | 以两字节代码单元表示的字符串长度，如果它以null终止，则为JSVM_AUTO_LENGTH。 | 
| result | 代表JavaScript string的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CreateStringUtf8()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateStringUtf8 (JSVM_Env env, const char * str, size_t length, JSVM_Value * result )
```

**描述**

从UTF8编码的C字符串创建JavaScript string值。 复制原生字符串。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| str | 表示UTF8编码字符串的字符缓冲区。 | 
| length | 字符串的长度，以字节为单位。如果字符串以null结尾，则为JSVM_AUTO_LENGTH。 | 
| result | 代表JavaScript字符串的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CreateSymbol()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateSymbol (JSVM_Env env, JSVM_Value description, JSVM_Value * result )
```

**描述**

从UTF8 编码的C字符串创建JavaScript symbol值。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| description | 可选的JSVM_Value，它指的是要设置为符号描述的JavaScript string。 | 
| result | 代表JavaScript symbol的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_STRING_EXPECTED。


### OH_JSVM_CreateSyntaxError()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateSyntaxError (JSVM_Env env, JSVM_Value code, JSVM_Value msg, JSVM_Value * result )
```

**描述**

返回带有所提供文本的JavaScript SyntaxError。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| code | 可选的JSVM_Value，带有与错误关联的错误代码的字符串。 | 
| msg | 引用JavaScript string用作Error的消息。 | 
| result | 表示创建的错误。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_STRING_EXPECTED。


### OH_JSVM_CreateTypedarray()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateTypedarray (JSVM_Env env, JSVM_TypedarrayType type, size_t length, JSVM_Value arraybuffer, size_t byteOffset, JSVM_Value * result )
```

**描述**

基于已有的ArrayBuffer对象，创建一个JavaScript TypedArray对象。TypedArray 对象在底层数据缓冲区上提供了一个类似数组的视图，其中每个元素都具有 相同的底层二进制标量数据类型。要求：（length\* 元素大小）+ byteOffset 小于等于传入的数组的大小（以字节为单位）。否则，将抛出范围错误（RangeError）。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| type | TypedArray中元素的标量数据类型。 | 
| length | TypedArray中的元素个数。 | 
| arraybuffer | ArrayBuffer是类型化数组的基础。 | 
| byteOffset | ArrayBuffer中开始投影TypedArray的字节偏移量。 | 
| result | 表示JavaScript TypedArray的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_INVALID_ARG。


### OH_JSVM_CreateTypeError()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateTypeError (JSVM_Env env, JSVM_Value code, JSVM_Value msg, JSVM_Value * result )
```

**描述**

返回带有所提供文本的JavaScript TypeError。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| code | 可选的JSVM_Value，带有与错误关联的错误代码的字符串。 | 
| msg | 引用JavaScript string用作Error的消息。 | 
| result | 表示创建的错误。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_STRING_EXPECTED。


### OH_JSVM_CreateUint32()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateUint32 (JSVM_Env env, uint32_t value, JSVM_Value * result )
```

**描述**

将C uint32_t类型的值转换为JavaScript number类型。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 要在JavaScript中表示的无符号整数值。 | 
| result | 表示JavaScript number类型的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_CreateVM()

```
JSVM_EXTERN JSVM_Status OH_JSVM_CreateVM (const JSVM_CreateVMOptions * options, JSVM_VM * result )
```

**描述**

创建一个虚拟机实例。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| options | 用于创建虚拟机实例的选项。 | 
| result | 新的虚拟机实例。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_INVALID_ARG。


### OH_JSVM_DefineClass()

```
JSVM_EXTERN JSVM_Status OH_JSVM_DefineClass (JSVM_Env env, const char * utf8name, size_t length, JSVM_Callback constructor, size_t propertyCount, const JSVM_PropertyDescriptor * properties, JSVM_Value * result )
```

**描述**

定义一个JavaScript类。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| utf8name | JavaScript构造函数的名称，建议在包装C++类时使用C++类名。 | 
| length | utf8name的长度（以字节为单位）或JSVM_AUTO_LENGTH（如果以 null 结尾）。 | 
| constructor | 用于创建类的构造函数的回调函数。包装C++类时，此方法必须是符合JSVM_Callback。 callback签名的静态成员。不能使用C++类构造函数。详情请参考JSVM_Callback。 | 
| propertyCount | properties数组参数中的项数。 | 
| properties | 类的属性描述符，用于定义类的属性和方法。 | 
| result | 表示类的构造函数的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_DefineProperties()

```
JSVM_EXTERN JSVM_Status OH_JSVM_DefineProperties (JSVM_Env env, JSVM_Value object, size_t propertyCount, const JSVM_PropertyDescriptor * properties )
```

**描述**

通过此方法可以在给定对象上高效定义多个属性， 这些属性使用属性描述符进行定义。通过一个属性描述符的数组， 此API将为对象依次设置数组中的属性。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| object | 待进行属性检索的对象。 | 
| propertyCount | properties数组中的元素数。 | 
| properties | 属性描述符的数组。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_INVALID_ARG或JSVM_GENERIC_FAILURE。


### OH_JSVM_DeleteElement()

```
JSVM_EXTERN JSVM_Status OH_JSVM_DeleteElement (JSVM_Env env, JSVM_Value object, uint32_t index, bool * result )
```

**描述**

尝试从object中删除指定index处的元素。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| object | 待查询的对象。 | 
| index | 要删除的属性的索引。 | 
| result | 表示元素删除是否成功。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_DeleteProperty()

```
JSVM_EXTERN JSVM_Status OH_JSVM_DeleteProperty (JSVM_Env env, JSVM_Value object, JSVM_Value key, bool * result )
```

**描述**

尝试从object中删除key自己的属性。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| object | 待查询的对象。 | 
| key | 待删除的属性名。 | 
| result | 表示属性删除是否成功。result可以选择性地通过传递NULL来忽略。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_DeleteReference()

```
JSVM_EXTERN JSVM_Status OH_JSVM_DeleteReference (JSVM_Env env, JSVM_Ref ref )
```

**描述**

删除传入的引用。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| ref | 需删除的JSVM_Ref。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_DestroyEnv()

```
JSVM_EXTERN JSVM_Status OH_JSVM_DestroyEnv (JSVM_Env env)
```

**描述**

销毁环境。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 待销毁的环境。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_DestroyVM()

```
JSVM_EXTERN JSVM_Status OH_JSVM_DestroyVM (JSVM_VM vm)
```

**描述**

销毁一个虚拟机实例。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| vm | 待销毁的虚拟机实例。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_DetachArraybuffer()

```
JSVM_EXTERN JSVM_Status OH_JSVM_DetachArraybuffer (JSVM_Env env, JSVM_Value arraybuffer )
```

**描述**

提供类似于调用ArrayBuffer detach操作的行为。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| arraybuffer | 待分离的JavaScript ArrayBuffer。 | 

**返回：**

如果成功则返回JSVM_OK。如果传入的是不可拆解的ArrayBuffer， 则返回JSVM_DETACHABLE_ARRAYBUFFER_EXPECTED。


### OH_JSVM_EscapeHandle()

```
JSVM_EXTERN JSVM_Status OH_JSVM_EscapeHandle (JSVM_Env env, JSVM_EscapableHandleScope scope, JSVM_Value escapee, JSVM_Value * result )
```

**描述**

提升JavaScript对象的句柄，使其在外部作用域的生命周期内有效。 每个作用域只能调用一次。如果多次调用，将返回错误。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| scope | 表示当前的作用域。 | 
| escapee | 表示要提升的JavaScript Object。 | 
| result | 被提升的Object在外部作用域中的句柄。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_ESCAPE_CALLED_TWICE。


### OH_JSVM_GetAllPropertyNames()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetAllPropertyNames (JSVM_Env env, JSVM_Value object, JSVM_KeyCollectionMode keyMode, JSVM_KeyFilter keyFilter, JSVM_KeyConversion keyConversion, JSVM_Value * result )
```

**描述**

返回一个数组，其中包含此对象的可用属性的名称。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| object | 从中检索属性的对象。 | 
| keyMode | 是否也检索原型属性。 | 
| keyFilter | 要检索哪些属性（可枚举/可读/可写）。 | 
| keyConversion | 表示是否将编号的属性键转换为字符串。 | 
| result | 表示JavaScript值的数组，这些值表示对象的属性名称。 可以使用OH_JSVM_GetArrayLength和OH_JSVM_GetElement对结果进行迭代。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_INVALID_ARG或JSVM_GENERIC_FAILURE。


### OH_JSVM_GetAndClearLastException()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetAndClearLastException (JSVM_Env env, JSVM_Value * result )
```

**描述**

获取并清除上一次异常。如果出现挂起，则返回JavaScript异常，否则返回NULL。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| result | 如果出现挂起则返回异常，否则为NULL。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_GetArraybufferInfo()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetArraybufferInfo (JSVM_Env env, JSVM_Value arraybuffer, void ** data, size_t * byteLength )
```

**描述**

用于检索ArrayBuffer的底层数据缓冲区及其长度。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| arraybuffer | 代表被查询的ArrayBuffer。 | 
| data | ArrayBuffer的底层数据缓冲区。如果byte_length为0，则该值可能为NULL 或任何其他指针值。 | 
| byteLength | 底层数据缓冲区的字节长度。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_INVALID_ARG。


### OH_JSVM_GetArrayLength()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetArrayLength (JSVM_Env env, JSVM_Value value, uint32_t * result )
```

**描述**

返回数组的长度。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 代表查询长度的JavaScript Array。 | 
| result | uint32代表数组的长度。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_ARRAY_EXPECTED。


### OH_JSVM_GetBoolean()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetBoolean (JSVM_Env env, bool value, JSVM_Value * result )
```

**描述**

返回用于表示给定布尔值的JavaScript单例对象。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 要检索的布尔值。 | 
| result | 表示待检索的JavaScript Boolean单例。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_GetCbInfo()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetCbInfo (JSVM_Env env, JSVM_CallbackInfo cbinfo, size_t * argc, JSVM_Value * argv, JSVM_Value * thisArg, void ** data )
```

**描述**

此方法在回调函数中用于检索有关调用的详细信息， 例如来自给定回调信息的参数和this指针。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| cbinfo | 传入回调函数的回调信息。 | 
| argc | 指定所提供的argv数组的长度并接收参数的实际数量， 可以通过传递NULL来选择性地忽略。 | 
| argv | JSVM_Value的C数组，用于存储复制的参数。如果参数数量超过提供的数量， 则只复制请求数量的参数。如果提供的参数比声明的少，则argv的其余部分将由代表undefined 的JSVM_Value值填充。可以通过传递NULL来忽略argv。 | 
| thisArg | 接收调用的JavaScript this参数。thisArg可以通过传递NULL来进行忽略。 | 
| data | 接收回调的数据指针。data可以通过传递NULL来进行忽略。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_GetDataviewInfo()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetDataviewInfo (JSVM_Env env, JSVM_Value dataview, size_t * bytelength, void ** data, JSVM_Value * arraybuffer, size_t * byteOffset )
```

**描述**

返回DataView的各种属性。 如果不需要某一属性，则任何出参都可以设置为NULL。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| dataview | 表示要查询其属性的DataView。 | 
| bytelength | DataView中的字节个数。 | 
| data | DataView下的数据缓冲区。如果bytelength是0， 则这可能是NULL或任何其他指针值。 | 
| arraybuffer | ArrayBuffer是DataView的基础。 | 
| byteOffset | 开始投影DataView的数据缓冲区中的字节偏移量。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_INVALID_ARG。


### OH_JSVM_GetDateValue()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetDateValue (JSVM_Env env, JSVM_Value value, double * result )
```

**描述**

返回给定JavaScript Date的时间值的C双精度基础类型。如果调用成功，返回JSVM_OK。 如果传入一个非JavaScript Date类型的JSVM_Value，返回JSVM_DATA_EXPECTED。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 代表一个JavaScript Date。 | 
| result | 作为double的时间值表示为自1970年1月1日UTC午夜以来的毫秒数。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_DATE_EXPECTED。


### OH_JSVM_GetElement()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetElement (JSVM_Env env, JSVM_Value object, uint32_t index, JSVM_Value * result )
```

**描述**

获取请求索引处的元素。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| object | 待进行属性检索的对象。 | 
| index | 要获取的属性的索引。 | 
| result | 属性值。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_GetGlobal()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetGlobal (JSVM_Env env, JSVM_Value * result )
```

**描述**

返回global对象。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| result | 代表JavaScript global对象。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_GetInstanceData()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetInstanceData (JSVM_Env env, void ** data )
```

**描述**

检索通过OH_JSVM_SetInstanceData()与当前运行的JSVM环境相关联的数据。 如果未设置任何关联数据，该函数调用将成功，且data设置为NULL。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| data | 之前通过调用OH_JSVM_SetInstanceData()与当前运行的JSVM环境关联的数据项。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_GetLastErrorInfo()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetLastErrorInfo (JSVM_Env env, const JSVM_ExtendedErrorInfo ** result )
```

**描述**

检索JSVM_ExtendedErrorInfo结构，其中包含有关发生的最后一个错误的信息。 返回的JSVM_ExtendedErrorInfo的内容仅在对同一env调用JSVM-API函数之前有效。 这包括对OH_JSVM_IsExceptionPending的调用，因此可能经常需要复制信息以便以后使用。 error_message中返回的指针指向一个静态定义的字符串，因此如果你在调用另一个JSVM-API 函数之前将它从error_message字段（将被覆盖）中复制出来，则可以安全地使用该指针。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| result | 包含有关错误的更多信息的JSVM_ExtendedErrorInfo结构。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_GetNamedProperty()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetNamedProperty (JSVM_Env env, JSVM_Value object, const char * utf8name, JSVM_Value * result )
```

**描述**

此方法等效于调用OH_JSVM_GetProperty， 其中，通过utf8Name传入的字符串用于创建JSVM_Value。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| object | 从中检索属性的对象。 | 
| utf8Name | 要获取的属性名。 | 
| result | 属性值。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_GetNewTarget()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetNewTarget (JSVM_Env env, JSVM_CallbackInfo cbinfo, JSVM_Value * result )
```

**描述**

返回构造函数调用的new target。 如果当前回调不是构造函数调用，结果为NULL。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| cbinfo | 传递给回调函数的回调信息。 | 
| result | 构造函数调用的new target。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_GetNull()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetNull (JSVM_Env env, JSVM_Value * result )
```

**描述**

返回null对象。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| result | 代表JavaScript null对象。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_GetProperty()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetProperty (JSVM_Env env, JSVM_Value object, JSVM_Value key, JSVM_Value * result )
```

**描述**

从传入的object中获取请求的属性。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| object | 从中检索属性的对象。 | 
| key | 要检索的属性的名称。 | 
| result | 属性值。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_GetPropertyNames()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetPropertyNames (JSVM_Env env, JSVM_Value object, JSVM_Value * result )
```

**描述**

以字符数数组的形式返回object的可枚举属性的名称。 key为符号的object的属性将不会被包含在内。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| object | 待进行属性检索的对象。 | 
| result | 表示一个JavaScript值的数组，这些值表示对象的属性名称。 可以使用OH_JSVM_GetArrayLength以及OH_JSVM_GetElement对结果进行迭代。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_GetPrototype()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetPrototype (JSVM_Env env, JSVM_Value object, JSVM_Value * result )
```

**描述**

返回对象的原型。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| object | 表示待返回其原型的JavaScript object。 这将返回Object.getPrototypeOf的等价值（与函数的prototype属性不同）。 | 
| result | 表示给定对象的原型。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_GetReferenceValue()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetReferenceValue (JSVM_Env env, JSVM_Ref ref, JSVM_Value * result )
```

**描述**

如果仍然有效，此JSVM-API将返回JSVM_Value， 表示与JSVM_Ref关联的JavaScript值。否则，结果将为NULL。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| ref | 请求相应值的JSVM_Ref。 | 
| result | JSVM_Ref引用的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_GetTypedarrayInfo()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetTypedarrayInfo (JSVM_Env env, JSVM_Value typedarray, JSVM_TypedarrayType * type, size_t * length, void ** data, JSVM_Value * arraybuffer, size_t * byteOffset )
```

**描述**

返回类型化数组的各种属性。如果不需要该属性，则任何输出参数都可以是 NULL。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| typedarray | 表示要查询其属性的TypedArray。 | 
| type | TypedArray中元素的标量数据类型。 | 
| length | TypedArray中的元素数。 | 
| data | TypedArray底层的数据缓冲区由byte_offset值调整，使其指向TypedArray 中的第一个元素。如果数组的长度是0，这可能是NULL或任何其他指针值。 | 
| arraybuffer | 位于TypedArray下的ArrayBuffer。 | 
| byteOffset | 数组的第一个元素所在的基础原生数组中的字节偏移量。 data 参数的值已经过调整，因此data指向数组中的第一个元素。因此， 原生数组的第一个字节将位于data - byte_offset。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_INVALID_ARG。


### OH_JSVM_GetUndefined()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetUndefined (JSVM_Env env, JSVM_Value * result )
```

**描述**

返回Undefined对象。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 代表JavaScript undefined值。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_GetValueBigintInt64()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetValueBigintInt64 (JSVM_Env env, JSVM_Value value, int64_t * result, bool * lossless )
```

**描述**

返回给定JavaScript BigInt的C int64_t基础类型等价值。 如果需要，它将截断该值，将lossless设置为false。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 代表JavaScript BigInt。 | 
| result | 给定的JavaScript BigInt的C int64_t基础类型等价值。 | 
| lossless | 指示BigInt值是否已无损转换。 | 

**返回：**

成功则返回JSVM_OK。如果传入的值非BigInt，则返回JSVM_BIGINT_EXPECTED。


### OH_JSVM_GetValueBigintUint64()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetValueBigintUint64 (JSVM_Env env, JSVM_Value value, uint64_t * result, bool * lossless )
```

**描述**

返回给定JavaScript BigInt的C uint64_t基础类型等价值。 如果需要，它将截断该值，将lossless设置为false。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 代表JavaScript BigInt。 | 
| result | 给定的JavaScript BigInt的C uint64_t基础类型等价值。 | 
| lossless | 指示BigInt值是否已无损转换。 | 

**返回：**

成功则返回JSVM_OK。如果传入的值非BigInt，则返回JSVM_BIGINT_EXPECTED。


### OH_JSVM_GetValueBigintWords()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetValueBigintWords (JSVM_Env env, JSVM_Value value, int * signBit, size_t * wordCount, uint64_t * words )
```

**描述**

将单个BigInt值转换为符号位、64位小端数组和数组中的元素数。 signBit和words参数可以都设置为NULL。这种情况下，只获取wordCount。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 代表JavaScript BigInt。 | 
| signBit | 表示JavaScript BigInt是正数还是负数的整数。 | 
| wordCount | 必须初始化为words数组的长度。返回后，将被设置为存储此BigInt所需的实际字数。 | 
| words | 指向预分配的64位字数组的指针。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_BIGINT_EXPECTED。


### OH_JSVM_GetValueBool()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetValueBool (JSVM_Env env, JSVM_Value value, bool * result )
```

**描述**

返回给定JavaScript Boolean的C布尔基础类型等价值。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 代表JavaScript Boolean。 | 
| result | 给定JavaScript Boolean的C布尔基础类型等价值。 | 

**返回：**

成功则返回JSVM_OK。如果传入非布尔值的JSVM_Value，则返回JSVM_BOOLEAN_EXPECTED。


### OH_JSVM_GetValueDouble()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetValueDouble (JSVM_Env env, JSVM_Value value, double * result )
```

**描述**

返回给定JavaScript number的C双精度基础类型等价值。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 代表JavaScript number。 | 
| result | 给定的JavaScript number的C双精度基础类型等价值。 | 

**返回：**

成功则返回JSVM_OK。如果传入非数字的JSVM_Value，则返回JSVM_NUMBER_EXPECTED。


### OH_JSVM_GetValueExternal()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetValueExternal (JSVM_Env env, JSVM_Value value, void ** result )
```

**描述**

检索之前传递给OH_JSVM_CreateExternal()的外部数据指针。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 代表JavaScript外部值。 | 
| result | 指向被JavaScript外部值封装的数据的指针。 | 

**返回：**

成功则返回JSVM_OK。如果传入非外部的JSVM_Value，则返回JSVM_INVALID_ARG。


### OH_JSVM_GetValueInt32()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetValueInt32 (JSVM_Env env, JSVM_Value value, int32_t * result )
```

**描述**

返回给定JavaScript number的C int32基础类型等价值。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 代表JavaScript number。 | 
| result | 给定的JavaScript number的C int32基础类型等价值。 | 

**返回：**

成功则返回JSVM_OK。如果传入非数字的JSVM_Value，则返回JSVM_NUMBER_EXPECTED。


### OH_JSVM_GetValueInt64()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetValueInt64 (JSVM_Env env, JSVM_Value value, int64_t * result )
```

**描述**

返回给定JavaScript number的C int64基础类型等价值。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 代表JavaScript number。 | 
| result | 给定的JavaScript number的C int64基础类型等价值。 | 

**返回：**

成功则返回JSVM_OK。如果传入非数字的JSVM_Value，则返回JSVM_NUMBER_EXPECTED。


### OH_JSVM_GetValueStringLatin1()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetValueStringLatin1 (JSVM_Env env, JSVM_Value value, char * buf, size_t bufsize, size_t * result )
```

**描述**

返回对应于传入值的ISO-8859-1编码字符串

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 代表JavaScript number。 | 
| buf | 写入ISO-8859-1编码字符串的缓冲区。如果传入NULL，则将在result中返回 字符串的长度（以字节为单位，不包括null结束符）。 | 
| bufsize | 目的缓冲区大小。当大小不够时，返回的字符串将被截断并以null结尾。 | 
| result | 复制到缓冲区中的字节数，不包括空终止符。 | 

**返回：**

成功则返回JSVM_OK。如果传入非string的JSVM_Value，则返回JSVM_STRING_EXPECTED。


### OH_JSVM_GetValueStringUtf16()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetValueStringUtf16 (JSVM_Env env, JSVM_Value value, char16_t * buf, size_t bufsize, size_t * result )
```

**描述**

基于传入的值，查询对应的采用UTF16编码的字符串。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 代表JavaScript字符串。 | 
| buf | 将UTF16-LE编码字符串写入的缓冲区。如果传入NULL，则返回字符串的 2字节代码单元长度，不包括空终止符。 | 
| bufsize | 目标缓冲区的大小。当此值不足时，返回的字符串将被截断并以null终止。 | 
| result | 复制到缓冲区中的2字节代码单元数，不包括空终止符。 | 

**返回：**

成功则返回JSVM_OK。如果传入非string的JSVM_Value，则返回JSVM_STRING_EXPECTED。


### OH_JSVM_GetValueStringUtf8()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetValueStringUtf8 (JSVM_Env env, JSVM_Value value, char * buf, size_t bufsize, size_t * result )
```

**描述**

返回对应于传入值的UTF8编码字符串。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 代表JavaScript字符串。 | 
| buf | 将UTF8编码的字符串写入的缓冲区。如果传入NULL，则在result中 返回以字节为单位的字符串长度，不包括空终止符。 | 
| bufsize | 目标缓冲区的大小。当此值不足时，返回的字符串将被截断并以null终止。 | 
| result | 复制到缓冲区的字节数，不包括null结束符。 | 

**返回：**

成功则返回JSVM_OK。如果传入非string的JSVM_Value，则返回JSVM_STRING_EXPECTED。


### OH_JSVM_GetValueUint32()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetValueUint32 (JSVM_Env env, JSVM_Value value, uint32_t * result )
```

**描述**

返回给定JavaScript number的C uint_32基础类型等价值。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 代表JavaScript number。 | 
| result | 将给定的JSVM_Value等效为uint32_t 的C基础类型。 | 

**返回：**

成功则返回JSVM_OK。如果传入非数字的JSVM_Value，则返回JSVM_NUMBER_EXPECTED。


### OH_JSVM_GetVersion()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetVersion (JSVM_Env env, uint32_t * result )
```

**描述**

返回JSVM运行时支持的最高JSVM-API版本。 后续将新增JSVM-API，以便支持更多的功能。引入该API的目的：在支持某功能的JSVM版本， 可以使用新的功能；在不支持某功能的JSVM版本，可以提供回调行为。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| result | 支持的最高版本的JSVM-API。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_GetVMInfo()

```
JSVM_EXTERN JSVM_Status OH_JSVM_GetVMInfo (JSVM_VMInfo * result)
```

**描述**

返回虚拟机的信息。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| result | 虚拟机的信息。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_HasElement()

```
JSVM_EXTERN JSVM_Status OH_JSVM_HasElement (JSVM_Env env, JSVM_Value object, uint32_t index, bool * result )
```

**描述**

如果传入的Object在指定的索引处有一个元素，则此JSVM-API返回true。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| object | 待查询的对象。 | 
| index | 待确定是否存在元素的索引位置。 | 
| result | 该属性是否存在于对象上。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_HasNamedProperty()

```
JSVM_EXTERN JSVM_Status OH_JSVM_HasNamedProperty (JSVM_Env env, JSVM_Value object, const char * utf8name, bool * result )
```

**描述**

此方法等效于使用从作为utf8Name传入的字符串创建的JSVM_Value 调用OH_JSVM_HasProperty。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| object | 待查询的对象。 | 
| utf8Name | 待检查的属性名。 | 
| result | 该属性是否存在于对象上。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_HasOwnProperty()

```
JSVM_EXTERN JSVM_Status OH_JSVM_HasOwnProperty (JSVM_Env env, JSVM_Value object, JSVM_Value key, bool * result )
```

**描述**

检查传入的Object是否具有命名的自己的属性。key必须是string或symbol， 否则将抛出错误。JSVM-API不会执行任何数据类型之间的转换。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| object | 待查询的对象。 | 
| key | 要检查其存在的自有属性的名称。 | 
| result | 表示对象上是否存在该自身属性。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_NAME_EXPECTED或JSVM_GENERIC_FAILURE。


### OH_JSVM_HasProperty()

```
JSVM_EXTERN JSVM_Status OH_JSVM_HasProperty (JSVM_Env env, JSVM_Value object, JSVM_Value key, bool * result )
```

**描述**

检查传入的Object是否具有指定命名的属性。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| object | 待查询的对象。 | 
| key | 要检查其存在的属性的名称。 | 
| result | 该属性是否存在于对象上。 | 

**返回：**

成功则返回JSVM_OK，可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_Init()

```
EXTERN_C_START JSVM_EXTERN JSVM_Status OH_JSVM_Init (const JSVM_InitOptions * options)
```

**描述**

初始化一个JavaScript虚拟机。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| options | 用于初始化JavaScript虚拟机的选项。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_Instanceof()

```
JSVM_EXTERN JSVM_Status OH_JSVM_Instanceof (JSVM_Env env, JSVM_Value object, JSVM_Value constructor, bool * result )
```

**描述**

提供类似于在对象上调用instanceof运算符的行为。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 要检查的JavaScript值。 | 
| constructor | 要检查的构造函数的JavaScript函数对象 | 
| result | 如果object instanceof constructor为true，则设置为true的布尔值。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_FUNCTION_EXPECTED或JSVM_GENERIC_FAILURE。


### OH_JSVM_IsArray()

```
JSVM_EXTERN JSVM_Status OH_JSVM_IsArray (JSVM_Env env, JSVM_Value value, bool * result )
```

**描述**

提供类似于在对象上调用IsArray的行为。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 待检查的JavaScript值。 | 
| result | 表示给定的对象是否为数组。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_IsArraybuffer()

```
JSVM_EXTERN JSVM_Status OH_JSVM_IsArraybuffer (JSVM_Env env, JSVM_Value value, bool * result )
```

**描述**

检查传入的对象是否为ArrayBuffer。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 待检查的JavaScript值。 | 
| result | 表示指定的对象是否为ArrayBuffer。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_IsDataview()

```
JSVM_EXTERN JSVM_Status OH_JSVM_IsDataview (JSVM_Env env, JSVM_Value value, bool * result )
```

**描述**

检查传入的对象是否是DataView。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 待检查的JavaScript值。 | 
| result | 给定的JSVM_Value是否代表DataView。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_IsDate()

```
JSVM_EXTERN JSVM_Status OH_JSVM_IsDate (JSVM_Env env, JSVM_Value value, bool * isDate )
```

**描述**

检查传入的Object是否为日期。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 待检查的JavaScript值。 | 
| isDate | 给定的JSVM_Value是否表示JavaScript Date对象。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_IsDetachedArraybuffer()

```
JSVM_EXTERN JSVM_Status OH_JSVM_IsDetachedArraybuffer (JSVM_Env env, JSVM_Value value, bool * result )
```

**描述**

提供类似调用ArrayBuffer IsDetachedBuffer操作的行为。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 待检查的JavaScript ArrayBuffer。 | 
| result | 表示ArrayBuffer是否被分离。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_IsError()

```
JSVM_EXTERN JSVM_Status OH_JSVM_IsError (JSVM_Env env, JSVM_Value value, bool * result )
```

**描述**

查询JSVM_Value以检查它是否表示错误对象。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 待检查的JSVM_Value。 | 
| result | 如果JSVM_Value表示错误，则设置为true的布尔值，否则设置为false。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_IsExceptionPending()

```
JSVM_EXTERN JSVM_Status OH_JSVM_IsExceptionPending (JSVM_Env env, bool * result )
```

**描述**

查询上一次异常是否由挂起导致的。如果由异常导致，则返回true，否则返回false。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| result | 如果异常挂起，则设置为true的布尔值。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_IsPromise()

```
JSVM_EXTERN JSVM_Status OH_JSVM_IsPromise (JSVM_Env env, JSVM_Value value, bool * isPromise )
```

**描述**

查询Promise是否为原生Promise对象。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 待检查的值。 | 
| isPromise | 表示是否为原生Promise对象（即底层引擎创建的promise对象）的标志。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_IsTypedarray()

```
JSVM_EXTERN JSVM_Status OH_JSVM_IsTypedarray (JSVM_Env env, JSVM_Value value, bool * result )
```

**描述**

检查传入的Object是否为类型化数组。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 待检查的JavaScript值。 | 
| result | 给定的JSVM_Value是否代表TypedArray。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_JsonParse()

```
JSVM_EXTERN JSVM_Status OH_JSVM_JsonParse (JSVM_Env env, JSVM_Value jsonString, JSVM_Value * result )
```

**描述**

解析JSON字符串，并返回成功解析的值。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| jsonString | 待解析的字符串。 | 
| result | 成功解析的值。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_STRING_EXPECTED或JSVM_GENERIC_FAILURE。


### OH_JSVM_JsonStringify()

```
JSVM_EXTERN JSVM_Status OH_JSVM_JsonStringify (JSVM_Env env, JSVM_Value jsonObject, JSVM_Value * result )
```

**描述**

将对象字符串化，并返回成功转换后的字符串。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| jsonObject | 待字符串化的对象。 | 
| result | 成功转换后返回的字符串。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_MemoryPressureNotification()

```
JSVM_EXTERN JSVM_Status OH_JSVM_MemoryPressureNotification (JSVM_Env env, JSVM_MemoryPressureLevel level )
```

**描述**

通知虚拟机系统内存不足并有选择地触发垃圾回收。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| level | 要为当前虚拟机设置的内存压力等级。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_NewInstance()

```
JSVM_EXTERN JSVM_Status OH_JSVM_NewInstance (JSVM_Env env, JSVM_Value constructor, size_t argc, const JSVM_Value * argv, JSVM_Value * result )
```

**描述**

使用给定的JSVM_Value表示的构造函数来实例化新的JavaScript值。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| constructor | 表示将作为构造函数调用的JavaScript函数。 | 
| argc | argv数组中的元素个数。 | 
| argv | JavaScript值数组。其中JSVM_Value表示构造函数的参数。 如果argc为零，则可以通过传入NULL来忽略此参数。 | 
| result | 表示返回的JavaScript对象， 在本例中是构造的对象。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_PENDING_EXCEPTION。


### OH_JSVM_ObjectFreeze()

```
JSVM_EXTERN JSVM_Status OH_JSVM_ObjectFreeze (JSVM_Env env, JSVM_Value object )
```

**描述**

冻结指定的对象。这样可以防止为其添加新的属性、删除现有属性、更改现有属性的 可枚举性、可配置性或可写性、或者更改现有属性的值。它还可以防止改变对象的原型。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| object | 待冻结的对象。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_ObjectSeal()

```
JSVM_EXTERN JSVM_Status OH_JSVM_ObjectSeal (JSVM_Env env, JSVM_Value object )
```

**描述**

封装指定的对象。这样可以防止为其添加新的属性并且将所有现有属性标记为不可配置。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| object | 待封装的对象。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_OpenEnvScope()

```
JSVM_EXTERN JSVM_Status OH_JSVM_OpenEnvScope (JSVM_Env env, JSVM_EnvScope * result )
```

**描述**

打开一个新的环境作用域。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 目标环境，JSVM-API接口将在该环境下调用。 | 
| result | 新的环境作用域。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_OpenEscapableHandleScope()

```
JSVM_EXTERN JSVM_Status OH_JSVM_OpenEscapableHandleScope (JSVM_Env env, JSVM_EscapableHandleScope * result )
```

**描述**

会打开一个新作用域，从中可以将一个对象提升到外部作用域。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| result | 代表新作用域。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_OpenHandleScope()

```
JSVM_EXTERN JSVM_Status OH_JSVM_OpenHandleScope (JSVM_Env env, JSVM_HandleScope * result )
```

**描述**

开辟了一个新的作用域。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| result | 代表新作用域。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_OpenVMScope()

```
JSVM_EXTERN JSVM_Status OH_JSVM_OpenVMScope (JSVM_VM vm, JSVM_VMScope * result )
```

**描述**

为虚拟机实例打开一个新的虚拟机作用域。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| vm | 目标虚拟机实例。 | 
| result | 新的虚拟机作用域。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_ReferenceRef()

```
JSVM_EXTERN JSVM_Status OH_JSVM_ReferenceRef (JSVM_Env env, JSVM_Ref ref, uint32_t * result )
```

**描述**

增加传入引用的引用计数并返回生成的引用计数。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| ref | 传入的引用，其引用计数将增加。 | 
| result | 新的引用计数。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_ReferenceUnref()

```
JSVM_EXTERN JSVM_Status OH_JSVM_ReferenceUnref (JSVM_Env env, JSVM_Ref ref, uint32_t * result )
```

**描述**

递减传入引用的引用计数并返回生成的引用计数。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| ref | 将减少其引用计数的JSVM_Ref。 | 
| result | 新的引用计数。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_RejectDeferred()

```
JSVM_EXTERN JSVM_Status OH_JSVM_RejectDeferred (JSVM_Env env, JSVM_Deferred deferred, JSVM_Value rejection )
```

**描述**

通过与之关联的延迟对象来拒绝JavaScript Promise。 它只能用于拒绝对应的可用延迟对象的JavaScript Promise。 这意味着Promise必须使用OH_JSVM_CreatePromise()创建，并且 从该调用返回的对象必须保留，才能将其传递给此API。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| deferred | 要解析其关联promise的延迟对象。 | 
| rejection | 用来拒绝Promise的值。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_RemoveWrap()

```
JSVM_EXTERN JSVM_Status OH_JSVM_RemoveWrap (JSVM_Env env, JSVM_Value jsObject, void ** result )
```

**描述**

使用OH_JSVM_Wrap()检索先前封装在JavaScript对象js_object中的native实例并移除封装。 如果finalize回调与封装相关联，则当JavaScript对象被垃圾回收时将不再调用它。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| jsObject | 与native实例关联的对象。 | 
| result | 指向封装的native实例的指针。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_ResolveDeferred()

```
JSVM_EXTERN JSVM_Status OH_JSVM_ResolveDeferred (JSVM_Env env, JSVM_Deferred deferred, JSVM_Value resolution )
```

**描述**

通过与之关联的延迟对象来解析JavaScript promise。 它只能用于解析对应的可用的延迟对象的JavaScript Promise。 这意味着Promise必须使用OH_JSVM_CreatePromise()创建，并且 从该调用返回的对象必须保留，才能将其传递给此API。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| deferred | 要解析其关联promise的延迟对象。 | 
| resolution | 用来解决Promise的值。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_RunScript()

```
JSVM_EXTERN JSVM_Status OH_JSVM_RunScript (JSVM_Env env, JSVM_Script script, JSVM_Value * result )
```

**描述**

执行一串JavaScript代码并返回其结果，其中包含以下注意事项： 与eval不同的是，该函数不允许脚本访问当前词法作用域，因此也不允许访问模块作用域， 这意味着require等伪全局变量将不可用。 脚本可以访问全局作用域。 脚本中的函数和var声明将被添加到全局对象。 使用let和const的变量声明将全局可见，但不会被添加到全局对象。 this的值在脚本内是global。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| script | 包含要执行的脚本的JavaScript字符串。 | 
| result | 执行脚本产生的值。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_SetElement()

```
JSVM_EXTERN JSVM_Status OH_JSVM_SetElement (JSVM_Env env, JSVM_Value object, uint32_t index, JSVM_Value value )
```

**描述**

在传入的Object上设置一个元素。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| object | 待进行属性设置的对象。 | 
| index | 要设置的属性的索引。 | 
| value | 属性值。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_SetInstanceData()

```
JSVM_EXTERN JSVM_Status OH_JSVM_SetInstanceData (JSVM_Env env, void * data, JSVM_Finalize finalizeCb, void * finalizeHint )
```

**描述**

将data与当前运行的JSVM环境相关联。后续可以使用OH_JSVM_GetInstanceData()检索data。 通过先前调用OH_JSVM_SetInstanceData()设置的任何与当前运行的JSVM环境相关联的现有数据都将 被覆盖。如果先前提供了finalizeCb，则不会调用它。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| data | 可用于此实例的绑定的数据项。 | 
| finalizeCb | 销毁环境时调用的函数，该函数接收data以便释放它。 | 
| finalizeHint | 在收集期间传递给最终回调的可选提示。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_SetNamedProperty()

```
JSVM_EXTERN JSVM_Status OH_JSVM_SetNamedProperty (JSVM_Env env, JSVM_Value object, const char * utf8name, JSVM_Value value )
```

**描述**

此方法等效于调用OH_JSVM_SetProperty， 其中，通过utf8Name传入的字符串用于创建JSVM_Value。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| object | 要对其设置属性的对象。 | 
| utf8Name | 要设置的属性的名称。 | 
| value | 属性值。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_SetProperty()

```
JSVM_EXTERN JSVM_Status OH_JSVM_SetProperty (JSVM_Env env, JSVM_Value object, JSVM_Value key, JSVM_Value value )
```

**描述**

为传入的object设置一个属性。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| object | 将进行属性设置的对象。 | 
| key | 待设置的属性名。 | 
| value | 属性值。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE。


### OH_JSVM_StrictEquals()

```
JSVM_EXTERN JSVM_Status OH_JSVM_StrictEquals (JSVM_Env env, JSVM_Value lhs, JSVM_Value rhs, bool * result )
```

**描述**

提供类似调用严格相等算法的行为。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| lhs | 待检查的JavaScript值。 | 
| rhs | 要检查的JavaScript值。 | 
| result | 表示两个JSVM_Value对象是否相等。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_SymbolFor()

```
JSVM_EXTERN JSVM_Status OH_JSVM_SymbolFor (JSVM_Env env, const char * utf8description, size_t length, JSVM_Value * result )
```

**描述**

在全局注册表中搜索具有给定描述的现有符号。如果该 符号已经存在，它将被返回，否则将在注册表中创建一个新符号。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| utf8description | UTF-8 C 字符串，表示用作符号描述的文本。 | 
| length | 描述字符串的长度，以字节为单位。如果字符串以null结尾，则为JSVM_AUTO_LENGTH。 | 
| result | 表示JavaScript 符号的JSVM_Value。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_Throw()

```
JSVM_EXTERN JSVM_Status OH_JSVM_Throw (JSVM_Env env, JSVM_Value error )
```

**描述**

抛出提供的JavaScript值。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| error | 要抛出的JavaScript值。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_ThrowError()

```
JSVM_EXTERN JSVM_Status OH_JSVM_ThrowError (JSVM_Env env, const char * code, const char * msg )
```

**描述**

会抛出带有所提供文本的JavaScript Error。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| code | 要在错误上设置的可选错误代码。 | 
| msg | 表示与错误关联的文本的C字符串。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_ThrowRangeError()

```
JSVM_EXTERN JSVM_Status OH_JSVM_ThrowRangeError (JSVM_Env env, const char * code, const char * msg )
```

**描述**

会抛出带有所提供文本的JavaScript RangeError。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| code | 要在错误上设置的可选错误代码。 | 
| msg | 表示与错误关联的文本的C字符串。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_ThrowSyntaxError()

```
JSVM_EXTERN JSVM_Status OH_JSVM_ThrowSyntaxError (JSVM_Env env, const char * code, const char * msg )
```

**描述**

会抛出带有所提供文本的JavaScript SyntaxError。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| code | 要在错误上设置的可选错误代码。 | 
| msg | 表示与错误关联的文本的C字符串。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_ThrowTypeError()

```
JSVM_EXTERN JSVM_Status OH_JSVM_ThrowTypeError (JSVM_Env env, const char * code, const char * msg )
```

**描述**

会抛出带有所提供文本的JavaScript TypeError。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| code | 要在错误上设置的可选错误代码。 | 
| msg | 表示与错误关联的文本的C字符串。 | 

**返回：**

成功则返回JSVM_OK。


### OH_JSVM_Typeof()

```
JSVM_EXTERN JSVM_Status OH_JSVM_Typeof (JSVM_Env env, JSVM_Value value, JSVM_ValueType * result )
```

**描述**

提供类似于在定义的对象上调用typeof运算符的行为。 不同点在于，该函数支持检测外部值；它将null检测为单独的类型， 而ECMAScript typeof将用于检测object。如果value的类型无效，则返回错误。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 要查询其类型的JavaScript值。 | 
| result | JavaScript值的类型。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_INVALID_ARG。


### OH_JSVM_TypeTagObject()

```
JSVM_EXTERN JSVM_Status OH_JSVM_TypeTagObject (JSVM_Env env, JSVM_Value value, const JSVM_TypeTag * typeTag )
```

**描述**

将typeTag指针的值与JavaScript对象或外部值相关联。可调用OH_JSVM_CheckObjectTypeTag() 判断附加在对象上的标记类型，以确保对象的类型正确。如果对象已经有关联的类型标记，则返回JSVM_INVALID_ARG。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| value | 要标记的JavaScript对象或外部值。 | 
| typeTag | 要标记对象的标签。 | 

**返回：**

成功则返回JSVM_OK，失败可能返回JSVM_GENERIC_FAILURE或JSVM_INVALID_ARG。


### OH_JSVM_Unwrap()

```
JSVM_EXTERN JSVM_Status OH_JSVM_Unwrap (JSVM_Env env, JSVM_Value jsObject, void ** result )
```

**描述**

当JavaScript代码调用类的方法或属性访问器时，对应的JSVM_Callback将被调用。 如果回调是针对实例方法或访问器的，则回调的this参数是封装器对象；然后可以通过调用 封装器对象的OH_JSVM_Unwrap()获得作为调用目标的C++实例。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| jsObject | 与native实例关联的对象。 | 
| result | 指向封装的native实例的指针。 | 

**返回：**

成功则返回JSVM_OK，如果jsObject传入的不是一个对象，失败返回JSVM_INVALID_ARG。


### OH_JSVM_Wrap()

```
JSVM_EXTERN JSVM_Status OH_JSVM_Wrap (JSVM_Env env, JSVM_Value jsObject, void * nativeObject, JSVM_Finalize finalizeCb, void * finalizeHint, JSVM_Ref * result )
```

**描述**

在JavaScript对象中封装native实例。native实例 后续可以通过OH_JSVM_Unwrap()进行检索。

**起始版本：** 11

**参数:**

| 名称 | 描述 | 
| -------- | -------- |
| env | 调用JSVM-API的环境。 | 
| jsObject | 将成为原生对象封装器的JavaScript对象。 | 
| nativeObject | 将封装在JavaScript对象中的native实例。 | 
| finalizeCb | 可选的原生回调，可用于在 JavaScript 对象被垃圾回收时释放native实例。 | 
| finalizeHint | 传递给完成回调的可选上下文提示。 | 
| result | 对封装对象的可选引用。 | 

**返回：**

成功则返回JSVM_OK，如果jsObject传入的不是一个对象，失败返回JSVM_INVALID_ARG。
