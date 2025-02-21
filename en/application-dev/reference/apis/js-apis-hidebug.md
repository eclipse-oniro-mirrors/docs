# @ohos.hidebug (HiDebug)

> **NOTE**
>
> The initial APIs of this module are supported since API version 8. Newly added APIs will be marked with a superscript to indicate their earliest API version.

The **hidebug** module provides APIs for you to obtain the memory usage of an application, including the static heap memory (native heap) and proportional set size (PSS) occupied by the application process. You can also export VM memory slices and collect VM CPU profiling data.

## Modules to Import

```js
import hidebug from '@ohos.hidebug';
```


## hidebug.getNativeHeapSize

getNativeHeapSize(): bigint

Obtains the total heap memory size of this application.

**System capability**: SystemCapability.HiviewDFX.HiProfiler.HiDebug

**Return value**

| Type  | Description                       |
| ------ | --------------------------- |
| bigint | Total heap memory size of the application, in bytes.|


**Example**
  ```js
  let nativeHeapSize = hidebug.getNativeHeapSize();
  ```


## hidebug.getNativeHeapAllocatedSize

getNativeHeapAllocatedSize(): bigint

Obtains the allocated heap memory size of this application.

**System capability**: SystemCapability.HiviewDFX.HiProfiler.HiDebug

**Return value**

| Type  | Description                             |
| ------ | --------------------------------- |
| bigint | Allocated heap memory of the application, in bytes.|


**Example**
  ```js
  let nativeHeapAllocatedSize = hidebug.getNativeHeapAllocatedSize();
  ```


## hidebug.getNativeHeapFreeSize

getNativeHeapFreeSize(): bigint

Obtains the free heap memory size of this application.

**System capability**: SystemCapability.HiviewDFX.HiProfiler.HiDebug

**Return value**

| Type  | Description                           |
| ------ | ------------------------------- |
| bigint | Free heap memory size of the application, in bytes.|

**Example**
  ```js
  let nativeHeapFreeSize = hidebug.getNativeHeapFreeSize();
  ```


## hidebug.getPss

getPss(): bigint

Obtains the size of the physical memory actually used by the application process.

**System capability**: SystemCapability.HiviewDFX.HiProfiler.HiDebug

**Return value**

| Type  | Description                     |
| ------ | ------------------------- |
| bigint | Size of the physical memory actually used by the application process, in KB.|

**Example**
  ```js
  let pss = hidebug.getPss();
  ```


## hidebug.getSharedDirty

getSharedDirty(): bigint

Obtains the size of the shared dirty memory of a process.

**System capability**: SystemCapability.HiviewDFX.HiProfiler.HiDebug

**Return value**

| Type  | Description                      |
| ------ | -------------------------- |
| bigint | Size of the shared dirty memory of the process, in KB.|


**Example**
  ```js
  let sharedDirty = hidebug.getSharedDirty();
  ```

## hidebug.getPrivateDirty<sup>9+<sup>

getPrivateDirty(): bigint

Obtains the size of the private dirty memory of a process.

**System capability**: SystemCapability.HiviewDFX.HiProfiler.HiDebug

**Return value**

| Type  | Description                      |
| ------ | -------------------------- |
| bigint | Size of the private dirty memory of the process, in KB.|


**Example**
  ```js
  let privateDirty = hidebug.getPrivateDirty();
  ```

## hidebug.getCpuUsage<sup>9+<sup>

getCpuUsage(): number

Obtains the CPU usage of a process.

For example, if the CPU usage is **50%**, **0.5** is returned.

**System capability**: SystemCapability.HiviewDFX.HiProfiler.HiDebug

**Return value**

| Type  | Description                      |
| ------ | -------------------------- |
| number | CPU usage of the process.|


**Example**
  ```js
  let cpuUsage = hidebug.getCpuUsage();
  ```

## hidebug.getServiceDump<sup>9+<sup>

getServiceDump(serviceid : number, fd : number, args : Array\<string>) : void

Obtains system service information.

**Required permissions**: ohos.permission.DUMP

**System capability**: SystemCapability.HiviewDFX.HiProfiler.HiDebug

**Parameters**

| Name  | Type  | Mandatory| Description                                                        |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| serviceid | number | Yes  | Obtains the system service information based on the specified service ID.|
| fd | number | Yes  | File descriptor to which data is written by the API.|
| args | Array\<string> | Yes  | Parameter list corresponding to the **Dump** API of the system service.|

**Example**

```js
import fs from '@ohos.file.fs'
import hidebug from '@ohos.hidebug'
import featureAbility from '@ohos.ability.featureAbility'

let context = featureAbility.getContext();
context.getFilesDir().then((data) => {
  var path = data + "/serviceInfo.txt";
  console.info("output path: " + path);
  let file = fs.openSync(path, fs.OpenMode.READ_WRITE | fs.OpenMode.CREATE);
  var serviceId = 10;
  var args = new Array("allInfo");
  try {
    hidebug.getServiceDump(serviceId, file.fd, args);
  } catch (error) {
    console.info(error.code);
    console.info(error.message);
  }
  fs.closeSync(file);
})
```

## hidebug.startJsCpuProfiling<sup>9+</sup>

startJsCpuProfiling(filename : string) : void

Starts the profiling method. `startJsCpuProfiling()` and `stopJsCpuProfiling()` are called in pairs. `startJsCpuProfiling()` always occurs before `stopJsCpuProfiling()`; that is, calling the functions in the sequence similar to the following is prohibited: `start->start->stop`, `start->stop->stop`, and `start->start->stop->stop`.

**System capability**: SystemCapability.HiviewDFX.HiProfiler.HiDebug

**Parameters**

| Name  | Type  | Mandatory| Description                                                        |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| filename | string | Yes  | User-defined profile name. The `filename.json` file is generated in the `files` directory of the application based on the specified `filename`.|

**Example**

```js
import hidebug from '@ohos.hidebug'

try {
  hidebug.startJsCpuProfiling("cpu_profiling");
  // ...
  hidebug.stopJsCpuProfiling();
} catch (error) {
  console.info(error.code)
  console.info(error.message)
}
```

## hidebug.stopJsCpuProfiling<sup>9+</sup>

stopJsCpuProfiling() : void

Stops the profiling method. `startJsCpuProfiling()` and `stopJsCpuProfiling()` are called in pairs. `startJsCpuProfiling()` always occurs before `stopJsCpuProfiling()`; that is, calling the functions in the sequence similar to the following is prohibited: `start->start->stop`, `start->stop->stop`, and `start->start->stop->stop`.

**System capability**: SystemCapability.HiviewDFX.HiProfiler.HiDebug

**Parameters**

| Name  | Type  | Mandatory| Description                                                        |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| filename | string | Yes  | User-defined profile name. The `filename.json` file is generated in the `files` directory of the application based on the specified `filename`.|

**Example**

```js
import hidebug from '@ohos.hidebug'

try {
  hidebug.startJsCpuProfiling("cpu_profiling");
  // ...
  hidebug.stopJsCpuProfiling();
} catch (error) {
  console.info(error.code)
  console.info(error.message)
}
```

## hidebug.dumpJsHeapData<sup>9+</sup>

dumpJsHeapData(filename : string) : void

Exports the heap data.

**System capability**: SystemCapability.HiviewDFX.HiProfiler.HiDebug

**Parameters**

| Name  | Type  | Mandatory| Description                                                        |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| filename | string | Yes  | User-defined heap file name. The `filename.heapsnapshot` file is generated in the `files` directory of the application based on the specified `filename`.|

**Example**

```js
import hidebug from '@ohos.hidebug'

try {
  hidebug.dumpJsHeapData("heapData");
} catch (error) {
  console.info(error.code)
  console.info(error.message)
}
```

## hidebug.startProfiling<sup>(deprecated)</sup>

startProfiling(filename : string) : void

> **NOTE**
>
> This API is deprecated since API version 9. You are advised to use [hidebug.startJsCpuProfiling](#hidebugstartjscpuprofiling9).

Starts the profiling method. `startProfiling()` and `stopProfiling()` are called in pairs. `startProfiling()` always occurs before `stopProfiling()`; that is, calling the functions in the sequence similar to the following is prohibited: `start->start->stop`, `start->stop->stop`, and `start->start->stop->stop`.

**System capability**: SystemCapability.HiviewDFX.HiProfiler.HiDebug

**Parameters**

| Name  | Type  | Mandatory| Description                                                        |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| filename | string | Yes  | User-defined profile name. The `filename.json` file is generated in the `files` directory of the application based on the specified `filename`.|

**Example**

```js
hidebug.startProfiling("cpuprofiler-20220216");
// code block
// ...
// code block
hidebug.stopProfiling();
```



## hidebug.stopProfiling<sup>(deprecated)</sup>

stopProfiling() : void

> **NOTE**
>
> This API is deprecated since API version 9. You are advised to use [hidebug.stopJsCpuProfiling](#hidebugstopjscpuprofiling9).

Stops the profiling method. `startProfiling()` and `stopProfiling()` are called in pairs. `startProfiling()` always occurs before `stopProfiling()`; that is, calling the functions in the sequence similar to the following is prohibited: `start->start->stop`, `start->stop->stop`, and `start->start->stop->stop`.

**System capability**: SystemCapability.HiviewDFX.HiProfiler.HiDebug

**Example**

```js
hidebug.startProfiling("cpuprofiler-20220216");
// code block
// ...
// code block
hidebug.stopProfiling();
```

## hidebug.dumpHeapData<sup>(deprecated)</sup>

dumpHeapData(filename : string) : void

> **NOTE**
>
> This API is deprecated since API version 9. You are advised to use [hidebug.dumpJsHeapData](#hidebugdumpjsheapdata9).

Exports the heap data.

**System capability**: SystemCapability.HiviewDFX.HiProfiler.HiDebug

**Parameters**

| Name  | Type  | Mandatory| Description                                                        |
| -------- | ------ | ---- | ------------------------------------------------------------ |
| filename | string | Yes  | User-defined heap file name. The `filename.heapsnapshot` file is generated in the `files` directory of the application based on the specified `filename`.|

**Example**

```js
hidebug.dumpHeapData("heap-20220216");
```
