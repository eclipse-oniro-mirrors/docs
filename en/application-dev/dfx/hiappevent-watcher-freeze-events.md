# Freeze Event Overview

HiAppEvent provides APIs for subscribing to freeze events.

- [Subscribing to Freeze Events (ArkTS)](hiappevent-watcher-freeze-events-arkts.md)
- [Subscribing to Freeze Events (C/C++)](hiappevent-watcher-freeze-events-ndk.md)

The **params** parameter in the freeze event information is described as follows:

**params**

| Name   | Type  | Description                      |
| ------- | ------ | ------------------------- |
| time     | number | Event triggering time, in ms.|
| foreground | boolean | Whether the application is running in the foreground. The value **true** indicates that the application is in the foreground, and the value **false** indicates the opposite.|
| bundle_version | string | Application version.|
| bundle_name | string | Application name.|
| process_name | string | Process name of the application.|
| pid | number | Process ID of the application.|
| uid | number | User ID of the application.|
| uuid | string | Error ID, which is generated based on fault information and uniquely identifies crash faults of the same type.|
| exception | object | Exception information. For details, see **exception**.|
| hilog | string[] | Log information.|
| event_handler | string[] | Events not yet handled by the main thread.|
| event_handler_size_3s | string | Number of tasks in the task stack at 3s during the [THREAD_BLOCK_6S event](appfreeze-guidelines.md#application-main-thread-timeout). This parameter is valid only in the **THREAD_BLOCK_6S** event.|
| event_handler_size_6s | string | Number of tasks in the task stack at 6s during the **THREAD_BLOCK_6S** event.|
| peer_binder | string[] | Binder call information.|
| threads | object[] | Full thread call stack. For details, see **thread**.|
| memory | object | Memory information. For details, see **memory**.|
| external_log<sup>12+</sup> | string[] | Path of the error log file. If the directory files exceed the threshold (for details, see **log_over_limit**), new log files may fail to be written. Therefore, delete the log files immediately after they are processed.|
| log_over_limit<sup>12+</sup> | boolean | Whether the size of generated fault log files and existing log files exceeds the upper limit (5 MB). The value **true** indicates that the upper limit is exceeded and logs fail to be written. The value **false** indicates that the upper limit is not exceeded.|

**exception**

| Name   | Type  | Description                      |
| ------- | ------ | ------------------------- |
| name | string | Exception type.|
| message | string | Exception cause.|

**thread**

| Name   | Type  | Description                      |
| ------- | ------ | ------------------------- |
| thread_name | string | Thread name.|
| tid | number | Thread ID.|
| frames | object[] | Thread call stack. For details, see **frame**.|

**frame (native)**

| Name   | Type  | Description                      |
| ------- | ------ | ------------------------- |
| symbol | string | Function name. When the device is heavily loaded and the call stack is obtained in low-overhead mode, the function name may be lost.|
| file | string | File name.|
| buildId | string | Unique file ID. When the device is heavily loaded and the call stack is obtained in low-overhead mode, the **buildId** information may be lost.|
| pc | string | PC register address.|
| offset | number | Function offset.|

**frame (JS)**

| Name   | Type  | Description                      |
| ------- | ------ | ------------------------- |
| file | string | File name.|
| packageName | string | Package name of the module.|
| symbol | string | Function name.|
| column | number | The column where an exception occurs.|
| line | number | The line where an exception occurs.|

**memory**

| Name   | Type  | Description                      |
| ------- | ------ | ------------------------- |
| rss | number | Size of the memory allocated for a process, in KB.|
| vss | number | Size of the virtual memory applied by a process from the system, in KB.|
| pss | number | Size of the physical memory actually used by a process, in KB.|
| sys_free_mem | number | Size of free memory, in KB.|
| sys_avail_mem | number | Size of available memory, in KB.|
| sys_total_mem | number | Total memory size, in KB.|
