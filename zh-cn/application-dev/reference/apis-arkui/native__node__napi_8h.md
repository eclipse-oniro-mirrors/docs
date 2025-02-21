# native_node_napi.h


## 概述

提供ArkTS侧的FrameNode转换NodeHandle的方式。

**库：** libace_ndk.z.so

**引用文件：** <arkui/native_node_napi.h>

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

**起始版本：** 12

**相关模块：**[ArkUI_NativeModule](_ark_u_i___native_module.md)


## 汇总


### 函数

| 名称 | 描述 | 
| -------- | -------- |
| int32_t [OH_ArkUI_GetNodeHandleFromNapiValue](_ark_u_i___native_module.md#oh_arkui_getnodehandlefromnapivalue) (napi_env env, napi_value frameNode, [ArkUI_NodeHandle](_ark_u_i___native_module.md#arkui_nodehandle) \*handle) | 获取ArkTS侧创建的FrameNode节点对象映射到native侧的ArkUI_NodeHandle。  | 
| int32_t [OH_ArkUI_GetContextFromNapiValue](_ark_u_i___native_module.md#oh_arkui_getcontextfromnapivalue) (napi_env env, napi_value value, [ArkUI_ContextHandle](_ark_u_i___native_module.md#arkui_contexthandle-12) \*context) | 获取ArkTS侧创建的UIContext对象映射到native侧的ArkUI_ContextHandle。  | 
| int32_t [OH_ArkUI_GetNodeContentFromNapiValue](_ark_u_i___native_module.md#oh_arkui_getnodecontentfromnapivalue) (napi_env env, napi_value value, [ArkUI_NodeContentHandle](_ark_u_i___native_module.md#arkui_nodecontenthandle) \*content) | 获取ArkTS侧创建的NodeContent对象映射到native侧的ArkUI_NodeContentHandle。  | 
| int32_t [OH_ArkUI_GetDrawableDescriptorFromNapiValue](_ark_u_i___native_module.md#oh_arkui_getdrawabledescriptorfromnapivalue) (napi_env env, napi_value value, [ArkUI_DrawableDescriptor](_ark_u_i___native_module.md#arkui_drawabledescriptor) \*\*drawableDescriptor) | 将ArkTS侧创建的DrawableDescriptor对象映射到native侧的ArkUI_DrawableDescriptor。  | 
| int32_t [OH_ArkUI_GetDrawableDescriptorFromResourceNapiValue](_ark_u_i___native_module.md#oh_arkui_getdrawabledescriptorfromresourcenapivalue) (napi_env env, napi_value value, [ArkUI_DrawableDescriptor](_ark_u_i___native_module.md#arkui_drawabledescriptor) \*\*drawableDescriptor) | 将ArkTS侧创建的$r资源对象映射到native侧的ArkUI_DrawableDescriptor。  | 
| [ArkUI_ErrorCode](_ark_u_i___native_module.md#arkui_errorcode) [OH_ArkUI_GetNavigationId](_ark_u_i___native_module.md#oh_arkui_getnavigationid) ([ArkUI_NodeHandle](_ark_u_i___native_module.md#arkui_nodehandle) node, char \*buffer, int32_t bufferSize, int32_t \*writeLength) | 获取当前节点所在的Navigation组件的ID。  | 
| [ArkUI_ErrorCode](_ark_u_i___native_module.md#arkui_errorcode) [OH_ArkUI_GetNavDestinationName](_ark_u_i___native_module.md#oh_arkui_getnavdestinationname) ([ArkUI_NodeHandle](_ark_u_i___native_module.md#arkui_nodehandle) node, char \*buffer, int32_t bufferSize, int32_t \*writeLength) | 获取当前节点所在的NavDestination组件的名称。  | 
| [ArkUI_ErrorCode](_ark_u_i___native_module.md#arkui_errorcode) [OH_ArkUI_GetNavStackLength](_ark_u_i___native_module.md#oh_arkui_getnavstacklength) ([ArkUI_NodeHandle](_ark_u_i___native_module.md#arkui_nodehandle) node, int32_t \*length) | 根据给定索引值，获取当前节点所在的Navigation栈的长度。  | 
| [ArkUI_ErrorCode](_ark_u_i___native_module.md#arkui_errorcode) [OH_ArkUI_GetNavDestinationNameByIndex](_ark_u_i___native_module.md#oh_arkui_getnavdestinationnamebyindex) ([ArkUI_NodeHandle](_ark_u_i___native_module.md#arkui_nodehandle) node, int32_t index, char \*buffer, int32_t bufferSize, int32_t \*writeLength) | 根据给定索引值，获取当前节点所在的Navigation栈中对应位置的页面名称。 索引值从0开始计数，0为栈底。  | 
| [ArkUI_ErrorCode](_ark_u_i___native_module.md#arkui_errorcode) [OH_ArkUI_GetNavDestinationId](_ark_u_i___native_module.md#oh_arkui_getnavdestinationid) ([ArkUI_NodeHandle](_ark_u_i___native_module.md#arkui_nodehandle) node, char \*buffer, int32_t bufferSize, int32_t \*writeLength) | 获取当前节点所在的NavDestination组件的ID。  | 
| [ArkUI_ErrorCode](_ark_u_i___native_module.md#arkui_errorcode) [OH_ArkUI_GetNavDestinationState](_ark_u_i___native_module.md#oh_arkui_getnavdestinationstate) ([ArkUI_NodeHandle](_ark_u_i___native_module.md#arkui_nodehandle) node, [ArkUI_NavDestinationState](_ark_u_i___native_module.md#arkui_navdestinationstate) \*state) | 获取当前节点所在的NavDestination组件的状态。  | 
| [ArkUI_ErrorCode](_ark_u_i___native_module.md#arkui_errorcode) [OH_ArkUI_GetNavDestinationIndex](_ark_u_i___native_module.md#oh_arkui_getnavdestinationindex) ([ArkUI_NodeHandle](_ark_u_i___native_module.md#arkui_nodehandle) node, int32_t \*index) | 获取当前节点所在的NavDestination组件在页面栈的索引。  | 
| napi_value [OH_ArkUI_GetNavDestinationParam](_ark_u_i___native_module.md#oh_arkui_getnavdestinationparam) ([ArkUI_NodeHandle](_ark_u_i___native_module.md#arkui_nodehandle) node) | 获取当前节点所在的NavDestination组件的参数。  | 
| [ArkUI_ErrorCode](_ark_u_i___native_module.md#arkui_errorcode) [OH_ArkUI_GetRouterPageIndex](_ark_u_i___native_module.md#oh_arkui_getrouterpageindex) ([ArkUI_NodeHandle](_ark_u_i___native_module.md#arkui_nodehandle) node, int32_t \*index) | 获取当前节点所在页面在Router页面栈中的索引。  | 
| [ArkUI_ErrorCode](_ark_u_i___native_module.md#arkui_errorcode) [OH_ArkUI_GetRouterPageName](_ark_u_i___native_module.md#oh_arkui_getrouterpagename) ([ArkUI_NodeHandle](_ark_u_i___native_module.md#arkui_nodehandle) node, char \*buffer, int32_t bufferSize, int32_t \*writeLength) | 获取当前节点所在页面的名称。  | 
| [ArkUI_ErrorCode](_ark_u_i___native_module.md#arkui_errorcode) [OH_ArkUI_GetRouterPagePath](_ark_u_i___native_module.md#oh_arkui_getrouterpagepath) ([ArkUI_NodeHandle](_ark_u_i___native_module.md#arkui_nodehandle) node, char \*buffer, int32_t bufferSize, int32_t \*writeLength) | 获取当前节点所在页面的Page组件的路径。  | 
| [ArkUI_ErrorCode](_ark_u_i___native_module.md#arkui_errorcode) [OH_ArkUI_GetRouterPageState](_ark_u_i___native_module.md#oh_arkui_getrouterpagestate) ([ArkUI_NodeHandle](_ark_u_i___native_module.md#arkui_nodehandle) node, [ArkUI_RouterPageState](_ark_u_i___native_module.md#arkui_routerpagestate) \*state) | 获取当前节点所在页面的Page组件的状态。  | 
| [ArkUI_ErrorCode](_ark_u_i___native_module.md#arkui_errorcode) [OH_ArkUI_GetRouterPageId](_ark_u_i___native_module.md#oh_arkui_getrouterpageid) ([ArkUI_NodeHandle](_ark_u_i___native_module.md#arkui_nodehandle) node, char \*buffer, int32_t bufferSize, int32_t \*writeLength) | 获取当前节点所在页面的Page组件的ID。  | 
