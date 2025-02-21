# queue.h


## 概述

声明串行队列提供的C接口.

**起始版本：** 10

**相关模块：**[FFRT](_f_f_r_t.md)


## 汇总


### 类型定义

| 名称 | 描述 | 
| -------- | -------- |
|  typedef void \* [ffrt_queue_t](_f_f_r_t.md) | 队列句柄.  | 


### 枚举

| 名称 | 描述 | 
| -------- | -------- |
| [ffrt_queue_type_t](_f_f_r_t.md#ffrt_queue_type_t) { [ffrt_queue_serial](_f_f_r_t.md), **ffrt_queue_max** } | 队列类型.  | 


### 函数

| 名称 | 描述 | 
| -------- | -------- |
| FFRT_C_API int [ffrt_queue_attr_init](_f_f_r_t.md#ffrt_queue_attr_init) ([ffrt_queue_attr_t](ffrt__queue__attr__t.md) \*attr) | 初始化串行队列属性.  | 
| FFRT_C_API void [ffrt_queue_attr_destroy](_f_f_r_t.md#ffrt_queue_attr_destroy) ([ffrt_queue_attr_t](ffrt__queue__attr__t.md) \*attr) | 销毁串行队列属性.  | 
| FFRT_C_API void [ffrt_queue_attr_set_qos](_f_f_r_t.md#ffrt_queue_attr_set_qos) ([ffrt_queue_attr_t](ffrt__queue__attr__t.md) \*attr, [ffrt_qos_t](_f_f_r_t.md) qos) | 设置串行队列qos属性.  | 
| FFRT_C_API [ffrt_qos_t](_f_f_r_t.md)[ffrt_queue_attr_get_qos](_f_f_r_t.md#ffrt_queue_attr_get_qos) (const [ffrt_queue_attr_t](ffrt__queue__attr__t.md) \*attr) | 获取串行队列qos属性.  | 
| FFRT_C_API void [ffrt_queue_attr_set_timeout](_f_f_r_t.md#ffrt_queue_attr_set_timeout) ([ffrt_queue_attr_t](ffrt__queue__attr__t.md) \*attr, uint64_t timeout_us) | 设置串行队列timeout属性.  | 
| FFRT_C_API uint64_t [ffrt_queue_attr_get_timeout](_f_f_r_t.md#ffrt_queue_attr_get_timeout) (const [ffrt_queue_attr_t](ffrt__queue__attr__t.md) \*attr) | 获取串行队列任务执行的timeout时间.  | 
| FFRT_C_API void [ffrt_queue_attr_set_callback](_f_f_r_t.md#ffrt_queue_attr_set_callback) ([ffrt_queue_attr_t](ffrt__queue__attr__t.md) \*attr, [ffrt_function_header_t](ffrt__function__header__t.md) \*f) | 设置串行队列超时回调方法.  | 
| FFRT_C_API [ffrt_function_header_t](ffrt__function__header__t.md) \* [ffrt_queue_attr_get_callback](_f_f_r_t.md#ffrt_queue_attr_get_callback) (const [ffrt_queue_attr_t](ffrt__queue__attr__t.md) \*attr) | 获取串行队列超时回调方法.  | 
| FFRT_C_API [ffrt_queue_t](_f_f_r_t.md)[ffrt_queue_create](_f_f_r_t.md#ffrt_queue_create) ([ffrt_queue_type_t](_f_f_r_t.md#ffrt_queue_type_t) type, const char \*name, const [ffrt_queue_attr_t](ffrt__queue__attr__t.md) \*attr) | 创建队列.  | 
| FFRT_C_API void [ffrt_queue_destroy](_f_f_r_t.md#ffrt_queue_destroy) ([ffrt_queue_t](_f_f_r_t.md) queue) | 销毁队列.  | 
| FFRT_C_API void [ffrt_queue_submit](_f_f_r_t.md#ffrt_queue_submit) ([ffrt_queue_t](_f_f_r_t.md) queue, [ffrt_function_header_t](ffrt__function__header__t.md) \*f, const [ffrt_task_attr_t](ffrt__task__attr__t.md) \*attr) | 提交一个任务到队列中调度执行.  | 
| FFRT_C_API [ffrt_task_handle_t](_f_f_r_t.md)[ffrt_queue_submit_h](_f_f_r_t.md#ffrt_queue_submit_h) ([ffrt_queue_t](_f_f_r_t.md) queue, [ffrt_function_header_t](ffrt__function__header__t.md) \*f, const [ffrt_task_attr_t](ffrt__task__attr__t.md) \*attr) | 提交一个任务到队列中调度执行，并返回任务句柄.  | 
| FFRT_C_API void [ffrt_queue_wait](_f_f_r_t.md#ffrt_queue_wait) ([ffrt_task_handle_t](_f_f_r_t.md) handle) | 等待队列中一个任务执行完成.  | 
| FFRT_C_API int [ffrt_queue_cancel](_f_f_r_t.md#ffrt_queue_cancel) ([ffrt_task_handle_t](_f_f_r_t.md) handle) | 取消队列中一个任务.  | 
