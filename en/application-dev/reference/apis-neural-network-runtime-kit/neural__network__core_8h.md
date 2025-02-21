# neural_network_core.h


## Overview

Defines APIs for the Neural Network Core module. The AI inference framework uses the native interfaces provided by Neural Network Core to build models and perform inference and computing on acceleration hardware.

**NOTE**<br>Currently, the APIs of Neural Network Core do not support multi-thread calling.

**File to include**: &lt;neural_network_runtime/neural_network_core.h&gt;

**Library**: libneural_network_core.so

**System capability**: @Syscap SystemCapability.Ai.NeuralNetworkRuntime

**Since**: 11

**Related module**: [NeuralnetworkRuntime](_neural_network_runtime.md)


## Summary


### Functions

| Name| Description|
| -------- | -------- |
| \*[OH_NNCompilation_Construct](_neural_network_runtime.md#oh_nncompilation_construct) (const [OH_NNModel](_neural_network_runtime.md#oh_nnmodel) \*model) | Creates a model building instance of the [OH_NNCompilation](_neural_network_runtime.md#oh_nncompilation) type.|
| \*[OH_NNCompilation_ConstructWithOfflineModelFile](_neural_network_runtime.md#oh_nncompilation_constructwithofflinemodelfile) (const char \*modelPath) | Creates a build instance based on an offline model file.|
| \*[OH_NNCompilation_ConstructWithOfflineModelBuffer](_neural_network_runtime.md#oh_nncompilation_constructwithofflinemodelbuffer) (const void \*modelBuffer, size_t modelSize) | Creates a build instance based on the offline model buffer.|
| \*[OH_NNCompilation_ConstructForCache](_neural_network_runtime.md#oh_nncompilation_constructforcache) () | Creates an empty build instance for later recovery from the model cache.|
| [OH_NNCompilation_ExportCacheToBuffer](_neural_network_runtime.md#oh_nncompilation_exportcachetobuffer) ([OH_NNCompilation](_neural_network_runtime.md#oh_nncompilation) \*compilation, const void \*buffer, size_t length, size_t \*modelSize) | Writes the model cache to the specified buffer.|
| [OH_NNCompilation_ImportCacheFromBuffer](_neural_network_runtime.md#oh_nncompilation_importcachefrombuffer) ([OH_NNCompilation](_neural_network_runtime.md#oh_nncompilation) \*compilation, const void \*buffer, size_t modelSize) | Reads the model cache from the specified buffer.|
| [OH_NNCompilation_AddExtensionConfig](_neural_network_runtime.md#oh_nncompilation_addextensionconfig) ([OH_NNCompilation](_neural_network_runtime.md#oh_nncompilation) \*compilation, const char \*configName, const void \*configValue, const size_t configValueSize) | Adds extended configurations for custom hardware attributes.|
| [OH_NNCompilation_SetDevice](_neural_network_runtime.md#oh_nncompilation_setdevice) ([OH_NNCompilation](_neural_network_runtime.md#oh_nncompilation) \*compilation, size_t deviceID) | Sets the device for model building and computing.|
| [OH_NNCompilation_SetCache](_neural_network_runtime.md#oh_nncompilation_setcache) ([OH_NNCompilation](_neural_network_runtime.md#oh_nncompilation) \*compilation, const char \*cachePath, uint32_t version) | Sets the cache directory and version for model building.|
| [OH_NNCompilation_SetPerformanceMode](_neural_network_runtime.md#oh_nncompilation_setperformancemode) ([OH_NNCompilation](_neural_network_runtime.md#oh_nncompilation) \*compilation, [OH_NN_PerformanceMode](_neural_network_runtime.md#oh_nn_performancemode) performanceMode) | Sets the performance mode for model computing.|
| [OH_NNCompilation_SetPriority](_neural_network_runtime.md#oh_nncompilation_setpriority) ([OH_NNCompilation](_neural_network_runtime.md#oh_nncompilation) \*compilation, [OH_NN_Priority](_neural_network_runtime.md#oh_nn_priority) priority) | Sets the priority for model computing.|
| [OH_NNCompilation_EnableFloat16](_neural_network_runtime.md#oh_nncompilation_enablefloat16) ([OH_NNCompilation](_neural_network_runtime.md#oh_nncompilation) \*compilation, bool enableFloat16) | Enables float16 for computing.|
| [OH_NNCompilation_Build](_neural_network_runtime.md#oh_nncompilation_build) ([OH_NNCompilation](_neural_network_runtime.md#oh_nncompilation) \*compilation) | Performs model building.|
| [OH_NNCompilation_Destroy](_neural_network_runtime.md#oh_nncompilation_destroy) ([OH_NNCompilation](_neural_network_runtime.md#oh_nncompilation) \*\*compilation) | Destroys a model building instance of the [OH_NNCompilation](_neural_network_runtime.md#oh_nncompilation) type.|
| \*[OH_NNTensorDesc_Create](_neural_network_runtime.md#oh_nntensordesc_create) () | Creates an [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) instance.|
| [OH_NNTensorDesc_Destroy](_neural_network_runtime.md#oh_nntensordesc_destroy) ([NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) \*\*tensorDesc) | Releases an [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) instance.|
| [OH_NNTensorDesc_SetName](_neural_network_runtime.md#oh_nntensordesc_setname) ([NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) \*tensorDesc, const char \*name) | Sets the name of an [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) instance.|
| [OH_NNTensorDesc_GetName](_neural_network_runtime.md#oh_nntensordesc_getname) (const [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) \*tensorDesc, const char \*\*name) | Obtains the name of an [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) instance.|
| [OH_NNTensorDesc_SetDataType](_neural_network_runtime.md#oh_nntensordesc_setdatatype) ([NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) \*tensorDesc, [OH_NN_DataType](_neural_network_runtime.md#oh_nn_datatype) dataType) | Sets the data type of an [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) instance.|
| [OH_NNTensorDesc_GetDataType](_neural_network_runtime.md#oh_nntensordesc_getdatatype) (const [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) \*tensorDesc, [OH_NN_DataType](_neural_network_runtime.md#oh_nn_datatype) \*dataType) | Obtains the data type of an [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) instance.|
| [OH_NNTensorDesc_SetShape](_neural_network_runtime.md#oh_nntensordesc_setshape) ([NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) \*tensorDesc, const int32_t \*shape, size_t shapeLength) | Sets the data shape of an [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) instance.|
| [OH_NNTensorDesc_GetShape](_neural_network_runtime.md#oh_nntensordesc_getshape) (const [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) \*tensorDesc, int32_t \*\*shape, size_t \*shapeLength) | Obtains the shape of an [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) instance.|
| [OH_NNTensorDesc_SetFormat](_neural_network_runtime.md#oh_nntensordesc_setformat) ([NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) \*tensorDesc, [OH_NN_Format](_neural_network_runtime.md#oh_nn_format) format) | Sets the data format of an [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) instance.|
| [OH_NNTensorDesc_GetFormat](_neural_network_runtime.md#oh_nntensordesc_getformat) (const [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) \*tensorDesc, [OH_NN_Format](_neural_network_runtime.md#oh_nn_format) \*format) | Obtains the data format of an [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) instance.|
| [OH_NNTensorDesc_GetElementCount](_neural_network_runtime.md#oh_nntensordesc_getelementcount) (const [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) \*tensorDesc, size_t \*elementCount) | Obtains the number of elements in an [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) instance.|
| [OH_NNTensorDesc_GetByteSize](_neural_network_runtime.md#oh_nntensordesc_getbytesize) (const [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) \*tensorDesc, size_t \*byteSize) | Obtains the number of bytes occupied by the data obtained through calculation based on the shape and data type of an [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) instance.|
| \*[OH_NNTensor_Create](_neural_network_runtime.md#oh_nntensor_create) (size_t deviceID, [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) \*tensorDesc) | Creates an [NN_Tensor](_neural_network_runtime.md#nn_tensor) instance from an [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) instance.|
| \*[OH_NNTensor_CreateWithSize](_neural_network_runtime.md#oh_nntensor_createwithsize) (size_t deviceID, [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) \*tensorDesc, size_t size) | Creates an [NN_Tensor](_neural_network_runtime.md#nn_tensor) instance based on the specified memory size and [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) instance.|
| \*[OH_NNTensor_CreateWithFd](_neural_network_runtime.md#oh_nntensor_createwithfd) (size_t deviceID, [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) \*tensorDesc, int fd, size_t size, size_t offset) | Creates an {\@Link NN_Tensor} instance based on the specified file descriptor of the shared memory and [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) instance.|
| [OH_NNTensor_Destroy](_neural_network_runtime.md#oh_nntensor_destroy) ([NN_Tensor](_neural_network_runtime.md#nn_tensor) \*\*tensor) | Destroys an [NN_Tensor](_neural_network_runtime.md#nn_tensor) instance.|
| \*[OH_NNTensor_GetTensorDesc](_neural_network_runtime.md#oh_nntensor_gettensordesc) (const [NN_Tensor](_neural_network_runtime.md#nn_tensor) \*tensor) | Obtains an [NN_TensorDesc](_neural_network_runtime.md#nn_tensordesc) instance of [NN_Tensor](_neural_network_runtime.md#nn_tensor).|
| \*[OH_NNTensor_GetDataBuffer](_neural_network_runtime.md#oh_nntensor_getdatabuffer) (const [NN_Tensor](_neural_network_runtime.md#nn_tensor) \*tensor) | Obtains the memory address of [NN_Tensor](_neural_network_runtime.md#nn_tensor) data. |
| [OH_NNTensor_GetFd](_neural_network_runtime.md#oh_nntensor_getfd) (const [NN_Tensor](_neural_network_runtime.md#nn_tensor) \*tensor, int \*fd) | Obtains the file descriptor of the shared memory where [NN_Tensor](_neural_network_runtime.md#nn_tensor) data is stored.|
| [OH_NNTensor_GetSize](_neural_network_runtime.md#oh_nntensor_getsize) (const [NN_Tensor](_neural_network_runtime.md#nn_tensor) \*tensor, size_t \*size) | Obtains the size of the shared memory where the [NN_Tensor](_neural_network_runtime.md#nn_tensor) data is stored.|
| [OH_NNTensor_GetOffset](_neural_network_runtime.md#oh_nntensor_getoffset) (const [NN_Tensor](_neural_network_runtime.md#nn_tensor) \*tensor, size_t \*offset) | Obtains the offset of [NN_Tensor](_neural_network_runtime.md#nn_tensor) data in the shared memory.|
| \*[OH_NNExecutor_Construct](_neural_network_runtime.md#oh_nnexecutor_construct) ([OH_NNCompilation](_neural_network_runtime.md#oh_nncompilation) \*compilation) | Creates an [OH_NNExecutor](_neural_network_runtime.md#oh_nnexecutor) instance.|
| [OH_NNExecutor_GetOutputShape](_neural_network_runtime.md#oh_nnexecutor_getoutputshape) ([OH_NNExecutor](_neural_network_runtime.md#oh_nnexecutor) \*executor, uint32_t outputIndex, int32_t \*\*shape, uint32_t \*shapeLength) | Obtains the dimension information about the output tensor.|
| [OH_NNExecutor_Destroy](_neural_network_runtime.md#oh_nnexecutor_destroy) ([OH_NNExecutor](_neural_network_runtime.md#oh_nnexecutor) \*\*executor) | Destroys an executor instance to release the memory occupied by it.|
| [OH_NNExecutor_GetInputCount](_neural_network_runtime.md#oh_nnexecutor_getinputcount) (const [OH_NNExecutor](_neural_network_runtime.md#oh_nnexecutor) \*executor, size_t \*inputCount) | Obtains the number of input tensors.|
| [OH_NNExecutor_GetOutputCount](_neural_network_runtime.md#oh_nnexecutor_getoutputcount) (const [OH_NNExecutor](_neural_network_runtime.md#oh_nnexecutor) \*executor, size_t \*outputCount) | Obtains the number of output tensors.|
| \*[OH_NNExecutor_CreateInputTensorDesc](_neural_network_runtime.md#oh_nnexecutor_createinputtensordesc) (const [OH_NNExecutor](_neural_network_runtime.md#oh_nnexecutor) \*executor, size_t index) | Creates the description of an input tensor based on the specified index value.|
| \*[OH_NNExecutor_CreateOutputTensorDesc](_neural_network_runtime.md#oh_nnexecutor_createoutputtensordesc) (const [OH_NNExecutor](_neural_network_runtime.md#oh_nnexecutor) \*executor, size_t index) | Creates the description of an output tensor based on the specified index value.|
| [OH_NNExecutor_GetInputDimRange](_neural_network_runtime.md#oh_nnexecutor_getinputdimrange) (const [OH_NNExecutor](_neural_network_runtime.md#oh_nnexecutor) \*executor, size_t index, size_t \*\*minInputDims, size_t \*\*maxInputDims, size_t \*shapeLength) | Obtains the dimension range of all input tensors.|
| [OH_NNExecutor_SetOnRunDone](_neural_network_runtime.md#oh_nnexecutor_setonrundone) ([OH_NNExecutor](_neural_network_runtime.md#oh_nnexecutor) \*executor, [NN_OnRunDone](_neural_network_runtime.md#nn_onrundone) onRunDone) | Sets the callback processing function invoked when the asynchronous inference ends.|
| [OH_NNExecutor_SetOnServiceDied](_neural_network_runtime.md#oh_nnexecutor_setonservicedied) ([OH_NNExecutor](_neural_network_runtime.md#oh_nnexecutor) \*executor, [NN_OnServiceDied](_neural_network_runtime.md#nn_onservicedied) onServiceDied) | Sets the callback processing function invoked when the device driver service terminates unexpectedly during asynchronous inference.|
| [OH_NNExecutor_RunSync](_neural_network_runtime.md#oh_nnexecutor_runsync) ([OH_NNExecutor](_neural_network_runtime.md#oh_nnexecutor) \*executor, [NN_Tensor](_neural_network_runtime.md#nn_tensor) \*inputTensor[], size_t inputCount, [NN_Tensor](_neural_network_runtime.md#nn_tensor) \*outputTensor[], size_t outputCount) | Performs synchronous inference.|
| [OH_NNExecutor_RunAsync](_neural_network_runtime.md#oh_nnexecutor_runasync) ([OH_NNExecutor](_neural_network_runtime.md#oh_nnexecutor) \*executor, [NN_Tensor](_neural_network_runtime.md#nn_tensor) \*inputTensor[], size_t inputCount, [NN_Tensor](_neural_network_runtime.md#nn_tensor) \*outputTensor[], size_t outputCount, int32_t timeout, void \*userData) | Performs asynchronous inference.|
| [OH_NNDevice_GetAllDevicesID](_neural_network_runtime.md#oh_nndevice_getalldevicesid) (const size_t \*\*allDevicesID, uint32_t \*deviceCount) | Obtains the ID of the device connected to Neural Network Runtime.|
| [OH_NNDevice_GetName](_neural_network_runtime.md#oh_nndevice_getname) (size_t deviceID, const char \*\*name) | Obtains the name of the specified device.|
| [OH_NNDevice_GetType](_neural_network_runtime.md#oh_nndevice_gettype) (size_t deviceID, [OH_NN_DeviceType](_neural_network_runtime.md#oh_nn_devicetype) \*deviceType) | Obtains the type of the specified device.|

 