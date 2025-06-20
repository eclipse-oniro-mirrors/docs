# ArkUI子系统Changelog

## cl.arkui.1 半模态SheetMode.EMBEDDED模式支持响应ESC键退出

**访问级别**

公开接口

**变更原因**

半模态SheetMode.EMBEDDED模式不支持ESC键退出，变更后，支持SheetMode.EMBEDDED模式ESC键退出。

**变更影响**

该变更为不兼容变更。

变更前：SheetMode.OVERLAY模式的半模态响应ESC键退出，SheetMode.EMBEDDED模式的半模态不响应ESC键退出。

变更后：两种模式的半模态都响应ESC键，ESC键退出与手机侧滑体验保持一致。

**起始API Level**

API 12

**变更发生版本**

从OpenHarmony SDK 5.0.0.59开始。

**变更的接口/组件**

bindSheet的SheetMode.EMBEDDED属性。

**适配指导**

变更后，若开发者仍不期望ESC键退出半模态，可以通过半模态的[onWillDismiss](../../../application-dev/reference/apis-arkui/arkui-ts/ts-universal-attributes-sheet-transition.md#sheetoptions)回调控制是否响应ESC和侧滑关闭半模态。
```ts
onWillDismiss: ((DismissSheetAction: DismissSheetAction) => {
    if (DismissSheetAction.reason == DismissReason.PRESS_BACK) {
    } else {
        DismissSheetAction.dismiss() //注册dismiss行为会关闭半模态
    }
}),
```

## cl.ArkUI.2 uiExtension的hideNonSecureWindows接口在2in1设备上不阻止全局悬浮窗创建和显示

**访问级别**

系统接口

**变更原因**

hideNonSecureWindows在2in1设备上不允许全局悬浮窗创建和显示，不满足业务需求，导致2in1设备上部分依赖全局悬浮窗应用异常。

**变更影响**

此变更不涉及应用适配。


变更前：hideNonSecureWindows在2in1设备上不允许全局悬浮窗创建，且会隐藏已经创建的全局悬浮窗。


变更后：hideNonSecureWindows在2in1设备上不阻止全局悬浮窗创建和显示。


**起始API Level**

API 12

**变更发生版本**

从OpenHarmony SDK 5.0.0.59开始。

**变更的接口/组件**

hideNonSecureWindows

**适配指导**

默认行为变更，无需适配。

## cl.ArkUI.3 uiExtension下新增properties必选属性

[uiExtension.d.ts](https://gitee.com/openharmony/interface_sdk-js/blob/master/api/@ohos.arkui.uiExtension.d.ts)中uiExtension命名空间下新增properties必选属性

**访问级别**

公开接口

**变更原因**

[EmbeddedComponent](https://gitee.com/openharmony/docs/blob/master/zh-cn/application-dev/reference/apis-arkui/arkui-ts/ts-container-embedded-component.md)所在的应用窗口移动的场景下，无法获取该组件的大小和位置信息，不满足开发者业务诉求。

**变更影响**

此变更涉及应用适配。

变更前：uiExtension命名空间下的WindowProxy无必选属性properties。

变更后：uiExtension命名空间下的WindowProxy有必选属性properties。

**起始API Level**

API 14

**变更发生版本**

从OpenHarmony SDK 5.0.0.59开始。

**变更的接口/组件**

WindowProxy的properties属性

**适配指导**

升级到API14后，如果应用在自己的业务中实现WindowProxy这个Interface，则需要在自定义的实现中新增必选属性properties。