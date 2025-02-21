# Node-API

## 简介

Node-API是用于封装JavaScript能力为Native插件的API，独立于底层JavaScript，并作为Node.js的一部分。

## 支持的能力

Node-API可以去除底层的JavaScript引擎的差异，提供一套稳定的接口。

OpenHarmony的Node-API组件对Node-API的接口进行了重新实现，底层对接了ArkJS等引擎。当前支持Node-API标准库中的部分接口。

## 已从Node-API组件标准库中导出的符号列表

从Node-API标准库导出的接口，其使用方法及行为同Node.js一致。相关接口声明及参数约束请参考[Node-API](https://nodejs.org/docs/latest-v8.x/api/n-api.html)文档。

|符号类型|符号名|说明|起始支持API版本|
| --- | --- | --- | --- |
|FUNC|napi_module_register|napi native模块注册接口。|10|
|FUNC|napi_get_last_error_info|获取`napi_extended_error_info`结构体，其中包含最近一次出现的error信息。|10|
|FUNC|napi_throw|抛出一个js value。|10|
|FUNC|napi_throw_error|抛出一个带文本信息的js `Error`。|10|
|FUNC|napi_throw_type_error|抛出一个带文本信息的js `TypeError`。|10|
|FUNC|napi_throw_range_error|抛出一个带文本信息的js `RangeError`。|10|
|FUNC|napi_is_error|判断`napi_value`是否表示为一个error对象。|10|
|FUNC|napi_create_error|创建并获取一个带文本信息的js `Error`。|10|
|FUNC|napi_create_type_error|创建并获取一个带文本信息的js `TypeError`。|10|
|FUNC|napi_create_range_error|创建并获取一个带文本信息的js `RangeError`。|10|
|FUNC|napi_get_and_clear_last_exception|获取并清除最近一次出现的异常。|10|
|FUNC|napi_is_exception_pending|判断是否出现了异常。|10|
|FUNC|napi_fatal_error|引发致命错误以立即终止进程。|10|
|FUNC|napi_open_handle_scope|创建一个上下文环境使用。|10|
|FUNC|napi_close_handle_scope|关闭传入的上下文环境，关闭后，全部在其中声明的引用都将被关闭。|10|
|FUNC|napi_open_escapable_handle_scope|创建出一个可逃逸的handel scope，可将范围内声明的值返回到父作用域。|10|
|FUNC|napi_close_escapable_handle_scope|关闭传入的可逃逸的handel scope。|10|
|FUNC|napi_escape_handle|提升传入的js object的生命周期到其父作用域。|10|
|FUNC|napi_create_reference|为`Object`创建一个reference，以延长其生命周期。调用者需要自己管理reference生命周期。|10|
|FUNC|napi_delete_reference|删除传入的reference。|10|
|FUNC|napi_reference_ref|增加传入的reference的引用计数，并获取该计数。|10|
|FUNC|napi_reference_unref|减少传入的reference的引用计数，并获取该计数。|10|
|FUNC|napi_get_reference_value|获取与reference相关联的js `Object`。|10|
|FUNC|napi_create_array|创建并获取一个js `Array`。|10|
|FUNC|napi_create_array_with_length|创建并获取一个指定长度的js `Array`。|10|
|FUNC|napi_create_arraybuffer|创建并获取一个指定大小的js `ArrayBuffer`。|10|
|FUNC|napi_create_external|分配一个附加有外部数据的js value。|10|
|FUNC|napi_create_external_arraybuffer|分配一个附加有外部数据的js `ArrayBuffer`。|10|
|FUNC|napi_create_object|创建一个默认的js `Object`。|10|
|FUNC|napi_create_symbol|创建一个js `Symbol`。|10|
|FUNC|napi_create_typedarray|通过现有的`ArrayBuffer`创建一个js `TypeArray`。|10|
|FUNC|napi_create_dataview|通过现有的`ArrayBuffer`创建一个js `DataView`。|10|
|FUNC|napi_create_int32|通过一个C的`int32_t`数据创建js `Number`。|10|
|FUNC|napi_create_uint32|通过一个C的`uint32_t`数据创建js `Number`。|10|
|FUNC|napi_create_int64|通过一个C的`int64_t`数据创建js `Number`。|10|
|FUNC|napi_create_double|通过一个C的`double`数据创建js `Number`。|10|
|FUNC|napi_create_string_latin1|通过ISO-8859-1编码的C字符串数据创建js `String`。|10|
|FUNC|napi_create_string_utf8|通过UTF8编码的C字符串数据创建js `String`。|10|
|FUNC|napi_create_string_utf16|通过UTF16编码的C字符串数据创建js `String`。|10|
|FUNC|napi_get_array_length|获取array的length。|10|
|FUNC|napi_get_arraybuffer_info|获取`ArrayBuffer`的底层data buffer及其长度。|10|
|FUNC|napi_get_prototype|获取给定js `Object`的`prototype`。|10|
|FUNC|napi_get_typedarray_info|获取给定`TypedArray`的各种属性。|10|
|FUNC|napi_get_dataview_info|获取给定`DataView`的各种属性。|10|
|FUNC|napi_get_value_bool|获取给定js `Boolean`对应的C bool值。|10|
|FUNC|napi_get_value_double|获取给定js `Number`对应的C double值。|10|
|FUNC|napi_get_value_external|获取先前通过napi_create_external()传递的外部数据指针。|10|
|FUNC|napi_get_value_int32|获取给定js `Number`对应的C int32值。|10|
|FUNC|napi_get_value_int64|获取给定js `Number`对应的C int64值。|10|
|FUNC|napi_get_value_string_latin1|获取给定js vaule对应的ISO-8859-1编码的字符串。|10|
|FUNC|napi_get_value_string_utf8|获取给定js vaule对应的UTF8编码的字符串。|10|
|FUNC|napi_get_value_string_utf16|获取给定js vaule对应的UTF16编码的字符串。|10|
|FUNC|napi_get_value_uint32|获取给定js `Number`对应的C uint32值。|10|
|FUNC|napi_get_boolean|根据给定的C boolean值，获取js bool对象。|10|
|FUNC|napi_get_global|获取`global`对象。|10|
|FUNC|napi_get_null|获取`null`对象。|10|
|FUNC|napi_get_undefined|获取`undefined`对象。|10|
|FUNC|napi_coerce_to_bool|将给定的js value强转成js `Boolean`。|10|
|FUNC|napi_coerce_to_number|将给定的js value强转成js `Number`。|10|
|FUNC|napi_coerce_to_object|将给定的js value强转成js `Object`。|10|
|FUNC|napi_coerce_to_string|将给定的js value强转成js `String`。|10|
|FUNC|napi_typeof|获取给定js value的js type。|10|
|FUNC|napi_instanceof|判断给定object是否为给定constructor的实例。|10|
|FUNC|napi_is_array|判断给定js value是否为array。|10|
|FUNC|napi_is_arraybuffer|判断给定js value是否为`ArrayBuffer`。|10|
|FUNC|napi_is_typedarray|判断给定js value是否表示一个`TypedArray`。|10|
|FUNC|napi_is_dataview|判断给定js value是否表示一个`DataView`。|10|
|FUNC|napi_is_date|判断给定js value是否为js `Date`对象。|10|
|FUNC|napi_strict_equals|判断给定的两个js value是否严格相等。|10|
|FUNC|napi_get_property_names|以字符串数组的形式获取对象的可枚举属性的名称。|10|
|FUNC|napi_set_property|对给定`Object`设置属性。|10|
|FUNC|napi_get_property|获取给定`Object`的给定属性。|10|
|FUNC|napi_has_property|判断给定对象中是否存在给定属性。|10|
|FUNC|napi_delete_property|尝试从给定`Object`中删除给定`key`属性。|10|
|FUNC|napi_has_own_property|判断给定`Object`中是否有名为`key`的own property。|10|
|FUNC|napi_set_named_property|对给定`Object`设置一个给定名称的属性。|10|
|FUNC|napi_get_named_property|获取给定`Object`中指定名称的属性。|10|
|FUNC|napi_has_named_property|判断给定`Object`中是否有给定名称的属性。|10|
|FUNC|napi_set_element|在给定`Object`的指定索引处，设置元素。|10|
|FUNC|napi_get_element|获取给定`Object`指定索引处的元素。|10|
|FUNC|napi_has_element|若给定`Object`的指定索引处拥有属性，获取该元素。|10|
|FUNC|napi_delete_element|尝试删除给定`Object`的指定索引处的元素。|10|
|FUNC|napi_define_properties|批量的向给定`Object`中定义属性。|10|
|FUNC|napi_type_tag_object|将tag指针的值与`Object`关联。|10|
|FUNC|napi_check_object_type_tag|判断给定的tag指针是否被关联到了js `Object`上。|10|
|FUNC|napi_call_function|在Native方法中调用js function，即native call js。|10|
|FUNC|napi_create_function|创建native方法给js使用，以便于js call native。|10|
|FUNC|napi_get_cb_info|从给定的callback info中获取有关调用的详细信息，如参数和this指针。|10|
|FUNC|napi_get_new_target|获取构造函数调用的`new.target`。|10|
|FUNC|napi_new_instance|通过给定的构造函数，构建一个实例。|10|
|FUNC|napi_define_class|定义与C++类相对应的JavaScript类。|10|
|FUNC|napi_wrap|在js object上绑定一个native对象实例。|10|
|FUNC|napi_unwrap|从js object上获取先前绑定的native对象实例。|10|
|FUNC|napi_remove_wrap|从js object上获取先前绑定的native对象实例，并解除绑定。|10|
|FUNC|napi_create_async_work|创建一个异步工作对象。|10|
|FUNC|napi_delete_async_work|释放先前创建的异步工作对象。|10|
|FUNC|napi_queue_async_work|将异步工作对象加到队列，由底层去调度执行。|10|
|FUNC|napi_cancel_async_work|取消入队的异步任务。|10|
|FUNC|napi_async_init|创建一个异步资源上下文环境（不支持与async_hook相关能力）。|11|
|FUNC|napi_make_callback|在异步资源上下文环境中回调JS函数(不支持与async_hook相关能力)。|11|
|FUNC|napi_async_destroy|销毁先前创建的异步资源上下文环境（不支持与async_hook相关能力）。|11|
|FUNC|napi_open_callback_scope|创建一个回调作用域（不支持与async_hook相关能力）。|11|
|FUNC|napi_close_callback_scope|关闭先前创建的回调作用域（不支持与async_hook相关能力）。|11|
|FUNC|napi_get_node_version|获取node的版本信息。|10|
|FUNC|napi_get_version|获取Node运行时支持的最高 N-API 版本。|10|
|FUNC|napi_create_promise|创建一个延迟对象和js promise。|10|
|FUNC|napi_resolve_deferred|resolve与js promise对象关联的延迟函数。|10|
|FUNC|napi_reject_deferred|reject与js promise对象关联的延迟函数。|10|
|FUNC|napi_is_promise|判断给定js value是否为promise对象。|10|
|FUNC|napi_get_uv_event_loop|获取当前libuv loop实例。|10|
|FUNC|napi_create_threadsafe_function|创建线程安全函数。|10|
|FUNC|napi_get_threadsafe_function_context|获取线程安全函数中的context。|10|
|FUNC|napi_call_threadsafe_function|调用线程安全函数。|10|
|FUNC|napi_acquire_threadsafe_function|指示线程安全函数可以开始使用。|10|
|FUNC|napi_release_threadsafe_function|指示线程安全函数将停止使用。|10|
|FUNC|napi_ref_threadsafe_function|指示在主线程上运行的事件循环在线程安全函数被销毁之前不应退出。|10|
|FUNC|napi_unref_threadsafe_function|指示在主线程上运行的事件循环可能会在线程安全函数被销毁之前退出。|10|
|FUNC|napi_create_date|通过一个C的`double`数据创建js `Date`。|10|
|FUNC|napi_get_date_value|获取给定js `Date`对应的C double值。|10|
|FUNC|napi_create_bigint_int64|通过一个C的`int64`数据创建js `BigInt`。|10|
|FUNC|napi_create_bigint_uint64|通过一个C的`uint64`数据创建js `BigInt`。|10|
|FUNC|napi_create_bigint_words|通过一个C的`uint64`数组创建单个js `BigInt`。|10|
|FUNC|napi_get_value_bigint_int64|获取给定js `BigInt`对应的C int64值。|10|
|FUNC|napi_get_value_bigint_uint64|获取给定js `BigInt`对应的C uint64值。|10|
|FUNC|napi_get_value_bigint_words|获取给定js `BigInt`对应的信息，包括符号位、64位小端序数组和数组中的元素个数。|10|
|FUNC|napi_create_buffer|创建并获取一个指定大小的js `Buffer`。|10|
|FUNC|napi_create_buffer_copy|创建并获取一个指定大小的js `Buffer`，并以给定数据进行初始化。|10|
|FUNC|napi_create_external_buffer|创建并获取一个指定大小的js `Buffer`，并以给定数据进行初始化，该接口可为`Buffer`附带额外数据。|10|
|FUNC|napi_get_buffer_info|获取js `Buffer`底层data及其长度。|10|
|FUNC|napi_is_buffer|判断给定js value是否为`Buffer`对象。|10|
|FUNC|napi_object_freeze|冻结给定的对象。|10|
|FUNC|napi_object_seal|密封给定的对象。|10|
|FUNC|napi_get_all_property_names|获取一个数组，其中包含此对象过滤后的属性名称。|10|
|FUNC|napi_detach_arraybuffer|分离给定`ArrayBuffer`的底层数据。|10|
|FUNC|napi_is_detached_arraybuffer|判断给定的`ArrayBuffer`是否已被分离过。|10|
|FUNC|napi_set_instance_data|绑定与当前运行的环境相关联的数据项。|11|
|FUNC|napi_get_instance_data|检索与当前运行的环境相关联的数据项。|11|
|FUNC|napi_add_env_cleanup_hook|注册环境清理钩子函数。|11|
|FUNC|napi_remove_env_cleanup_hook|取消环境清理钩子函数。|11|
|FUNC|napi_add_async_cleanup_hook|注册清理异步钩子函数。|11|
|FUNC|napi_remove_async_cleanup_hook|取消清理异步钩子函数。|11|
|FUNC|node_api_get_module_file_name|用于获取加载项加载位置的绝对路径。|11|
|FUNC|napi_add_finalizer|当js `Object`中的对象被垃圾回收时调用注册的napi_finalize回调。|11|

## 未从Node-API组件标准库中导出的符号列表

|符号类型|符号名|说明|
| --- | --- | --- |
|FUNC|napi_run_script|将给定对象作为js代码运行。|
|FUNC|napi_adjust_external_memory|调整js `Object`持有的外部内存。|
|FUNC|napi_fatal_exception|向js抛出 `UncaughtException`。|

## Node-API组件扩展的符号列表

|符号类型|符号名|说明|起始支持API版本|
| --- | --- | --- | --- |
|FUNC|napi_queue_async_work_with_qos|将异步工作对象加到队列，由底层根据传入的qos优先级去调度执行。|10|
|FUNC|napi_run_script_path|运行abc文件。|10|
|FUNC|napi_load_module|将abc文件作为模块加载，返回模块的命名空间。|11|
|FUNC|napi_create_object_with_properties|使用给定的napi_property_descriptor创建js `Object`。descriptor的键名必须为 string，且不可转为number。|11|
|FUNC|napi_create_object_with_named_properties|使用给定的napi_value和键名创建js `Object`。键名必须为 string，且不可转为number。|11|
|FUNC|napi_coerce_to_native_binding_object|强制将js `Object`和Native对象绑定。|11|
