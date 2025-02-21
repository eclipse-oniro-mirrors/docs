# 应用开发导读

应用开发文档用于指导开发者通过OpenHarmony提供的接口完成应用开发。当前应用开发文档提供了在标准系统上开发应用的JS接口。

在应用开发的文档中，您可以获取到如下几方面的内容：

### 入门

[入门](quick-start/Readme-CN.md)可以帮助开发者了解应用开发的基本方法。

这一部分包含了快速构建首个应用的快速入门，以及开发OpenHarmony应用所必备的基础知识。

开发的基础知识包含了OpenHarmony应用程序的包结构配置文件说明，以及资源文件的使用指导。

### 开发

为了帮助开发者更好的理解OpenHarmony提供的能力，我们对重点功能提供了开发指导，辅助开发者完成应用的开发。

首先，提供了支撑OpenHarmony应用的两个重要框架：

- 应用程序的框架：[应用模型](application-models/Readme-CN.md)
- UI的框架：[UI开发](ui/Readme-CN.md)

所有应用都应该在这两个框架的基础之上进行功能的开发。

在此基础上，还提供了如下功能的开发指导：

- [Web](web/web-component-overview.md)
- [通知](notification/Readme-CN.md)
- [窗口管理](windowmanager/Readme-CN.md)
- [WebGL](webgl/Readme-CN.md)
- [媒体](media/Readme-CN.md)
- [安全](security/Readme-CN.md)
- [网络与连接](connectivity/Readme-CN.md)
- [电话服务](telephony/Readme-CN.md)
- [数据管理](database/Readme-CN.md)
- [文件管理](file-management/Readme-CN.md)
- [任务管理](task-management/Readme-CN.md)
- [设备管理](device/Readme-CN.md)
- [设备使用信息统计](device-usage-statistics/Readme-CN.md)
- [DFX](dfx/Readme-CN.md)
- [国际化](internationalization/Readme-CN.md)
- [应用测试](application-test/Readme-CN.md)
- [一次开发，多端部署](key-features/multi-device-app-dev/Readme-CN.md)
- [IDL工具规格及使用说明书](IDL/idl-guidelines.md)
- [Native API的相关指导](napi/Readme-CN.md)

### 工具

DevEco Studio工具是OpenHarmony应用开发的推荐IDE工具。
在[工具](https://developer.harmonyos.com/cn/docs/documentation/doc-guides/ohos-deveco-studio-overview-0000001263280421)部分，讲解了DevEco Studio工具的详细用法，包括使用该工具进行工程创建、应用签名、应用调试、应用安装运行的指导。

### 示例教程

我们提供了[Sample工程](https://gitee.com/openharmony/applications_app_samples/blob/OpenHarmony-3.2-Release/README_zh.md)和[Codelab](https://gitee.com/openharmony/codelabs/blob/master/README.md)这两种形式的示例教程，为开发者提供更丰富的开发参考，辅助开发者理解功能逻辑，提升开发效率。

### API参考

API参考提供了OpenHarmony全量组件和接口的参考文档，可以帮助开发者快速查找到指定接口的详细描述和调用方法。

内容包括：

- [组件参考（基于TS扩展的声明式开发范式）](reference/arkui-ts/Readme-CN.md)
- [组件参考（基于JS扩展的类Web开发范式）](reference/arkui-js/Readme-CN.md)
- [JS服务卡片UI组件参考](reference/js-service-widget-ui/Readme-CN.md) 
- 接口参考
  - [JS及TS API参考](reference/apis/Readme-CN.md)
  - Native API
    - [Native API参考](reference/native-apis/Readme-CN.md)
    - [标准库](reference/native-lib/third_party_libc/musl.md)
    - [Node_API](reference/native-lib/third_party_napi/napi.md)

### Readme

如果需要了解各子系统的原理和基本信息，可以参考“[docs/zh-cn/readme](../readme)”目录中各子系统readme的介绍。
