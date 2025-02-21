# 应用开发导读

> **说明**：
> 您当前正在浏览OpenHarmony 3.2 Release版本的配套文档，请获取与该版本[配套的SDK](../release-notes/OpenHarmony-v3.2-release.md#配套关系)开发应用。

应用开发文档用于指导开发者通过OpenHarmony提供的接口完成应用开发。当前应用开发文档提供了在标准系统上开发应用的JS接口。

在应用开发的文档中，您可以获取到如下几方面的内容：

## 入门

[入门](quick-start/start-overview.md)可以帮助开发者了解应用开发的基本方法。

这一部分包含了快速构建首个应用的快速入门，以及开发OpenHarmony应用所必备的基础知识。

开发的基础知识包含了OpenHarmony应用程序的包结构配置文件说明，以及资源文件的使用指导。

## 开发

为了帮助开发者更好的理解OpenHarmony提供的能力，我们对重点功能提供了开发指导，辅助开发者完成应用的开发。

首先，提供了支撑OpenHarmony应用的两个重要框架：

- 应用程序的框架：[应用模型](application-models/application-model-composition.md)
- UI的框架：[UI开发](ui/arkui-overview.md)

所有应用都应该在这两个框架的基础之上进行功能的开发。

在此基础上，还提供了如下功能的开发指导：

- [Web](web/web-component-overview.md)
- [通知](notification/notification-overview.md)
- [窗口管理](windowmanager/window-overview.md)
- [WebGL](webgl/webgl-overview.md)
- [媒体](media/media-application-overview.md)
- [安全](security/userauth-overview.md)
- [网络与连接](connectivity/ipc-rpc-overview.md)
- [电话服务](telephony/telephony-overview.md)
- [数据管理](database/data-mgmt-overview.md)
- [文件管理](file-management/file-management-overview.md)
- [任务管理](task-management/background-task-overview.md)
- [设备管理](device/usb-overview.md)
- [设备使用信息统计](device-usage-statistics/device-usage-statistics-overview.md)
- [DFX](dfx/hiappevent-guidelines.md)
- [国际化](internationalization/international-overview.md)
- [应用测试](application-test/arkxtest-guidelines.md)
- [一次开发，多端部署](key-features/multi-device-app-dev/foreword.md)
- [IDL工具规格及使用说明书](IDL/idl-guidelines.md)
- [Native API的相关指导](napi/napi-guidelines.md)

## 工具

DevEco Studio工具是OpenHarmony应用开发的推荐IDE工具。
在[工具](https://developer.harmonyos.com/cn/docs/documentation/doc-guides/ohos-deveco-studio-overview-0000001263280421)部分，讲解了DevEco Studio工具的详细用法，包括使用该工具进行工程创建、应用签名、应用调试、应用安装运行的指导。

## 示例教程

我们提供了[Sample工程](https://gitee.com/openharmony/applications_app_samples/blob/OpenHarmony-3.2-Release/README_zh.md)和[Codelab](https://gitee.com/openharmony/codelabs/blob/master/README.md)这两种形式的示例教程，为开发者提供更丰富的开发参考，辅助开发者理解功能逻辑，提升开发效率。

## API参考

API参考提供了OpenHarmony全量组件和接口的参考文档，可以帮助开发者快速查找到指定接口的详细描述和调用方法。

内容包括：

- [ArkTS接口参考](reference/apis/development-intro.md)
- [组件参考（基于TS扩展的声明式开发范式）](reference/arkui-ts/ts-components-summary.md)
- [组件参考（兼容JS的类Web开发范式-ArkUI.Full）](reference/arkui-js/Readme-CN.md)
- [组件参考（兼容JS的类Web开发范式-ArkUI.Lite）](reference/arkui-js-lite/Readme-CN.md)
- [JS服务卡片UI组件参考](reference/js-service-widget-ui/js-service-widget-file.md)
- 接口参考（Native API）
  - [OpenHarmony Native API](reference/native-apis/_o_h___native_x_component.md)
  - [Native API标准库](reference/native-lib/third_party_libc/musl.md)
  - [Node_API](reference/native-lib/third_party_napi/napi.md)
