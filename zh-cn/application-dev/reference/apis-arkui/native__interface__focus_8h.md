# native_interface_focus.h


## 概述

提供NativeFocus相关接口定义。

**库：** libace_ndk.z.so

**引用文件：** <arkui/native_interface_focus.h>

**系统能力：** SystemCapability.ArkUI.ArkUI.Full 

**起始版本：** 15

**相关模块：**[ArkUI_NativeModule](_ark_u_i___native_module.md)


## 汇总

### ArkUI_KeyProcessingMode

```
enum ArkUI_KeyProcessingMode
```
**描述：**

当组件无法处理按键事件时，确定按键事件处理的优先级。

**起始版本：** 15

| 名称          | 描述        |
| ----------- | --------- |
| ARKUI_KEY_PROCESSING_MODE_FOCUS_NAVIGATION | 默认值，按键事件用于移动焦点。|
| ARKUI_KEY_PROCESSING_MODE_FOCUS_ANCESTOR_EVENT |  按键事件向上传递给祖先组件。 |

### 函数

| 名称 | 描述 | 
| -------- | -------- |
|[ArkUI_ErrorCode](_ark_u_i___native_module.md#arkui_errorcode)  OH_ArkUI_FocusRequest([ArkUI_NodeHandle](_ark_u_i___native_module.md#arkui_nodehandle) node); | 请求焦点。|
| void OH_ArkUI_FocusClear([ArkUI_ContextHandle](_ark_u_i___native_module.md#arkui_contexthandle-12) uiContext); | 将当前焦点清除到根容器节点。 |
| void OH_ArkUI_FocusActivate([ArkUI_ContextHandle](_ark_u_i___native_module.md#arkui_contexthandle-12) uiContext, bool isActive, bool isAutoInactive); | 设置当前界面的焦点激活态，获焦节点显示焦点框。|
| void OH_ArkUI_FocusSetAutoTransfer([ArkUI_ContextHandle](_ark_u_i___native_module.md#arkui_contexthandle-12) uiContext, bool autoTransfer); | 设置页面切换时，焦点转移行为。 | 
| void OH_ArkUI_FocusSetKeyProcessingMode([ArkUI_ContextHandle](_ark_u_i___native_module.md#arkui_contexthandle-12) uiContext, [ArkUI_KeyProcessingMode](#arkui_keyprocessingmode) mode); | 设置页面切换时，焦点转移行为。 | 
