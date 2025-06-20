# context_constant.h


## 概述

声明上下文相关的枚举。

**库**：libability_runtime.so

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**起始版本**：13

**相关模块**：[AbilityRuntime](_ability_runtime.md)


## 汇总

### 文件

| 名称                                          | 描述                                                         |
| --------------------------------------------- | ------------------------------------------------------------ |
| [context_constant.h](context__constant_8h.md) | 声明上下文相关的枚举。<br/>**引用文件**：<AbilityKit/ability_runtime/context_constant.h><br/>**库**：libability_runtime.so |


### 枚举

| 名称                                                         | 描述               |
| ------------------------------------------------------------ | ------------------ |
| [AbilityRuntime_AreaMode](_ability_runtime.md#abilityruntime_areamode) {<br/>    ABILITY_RUNTIME_AREA_MODE_EL1 = 0,<br/>    ABILITY_RUNTIME_AREA_MODE_EL2 = 1,<br/>    ABILITY_RUNTIME_AREA_MODE_EL3 = 2,<br/>    ABILITY_RUNTIME_AREA_MODE_EL4 = 3,<br/>    ABILITY_RUNTIME_AREA_MODE_EL5 = 4<br/>} | 定义数据加密等级。 |
| [AbilityRuntime_StartVisibility](_ability_runtime.md#abilityruntime_startvisibility) {<br/>    ABILITY_RUNTIME_HIDE_UPON_START = 0,<br/>    ABILITY_RUNTIME_SHOW_UPON_START = 1<br/>} | 定义启动Ability时的窗口和dock栏图标显示模式。     |
| [AbilityRuntime_WindowMode](_ability_runtime.md#abilityruntime_windowmode) {<br/>    ABILITY_RUNTIME_WINDOW_MODE_UNDEFINED = 0,</br>    ABILITY_RUNTIME_WINDOW_MODE_FULL_SCREEN = 1<br/>} | 定义启动Ability时的窗口模式。     |
| [AbilityRuntime_SupportedWindowMode](_ability_runtime.md#abilityruntime_supportedwindowmode) {<br/>    ABILITY_RUNTIME_SUPPORTED_WINDOW_MODE_FULL_SCREEN = 0,<br/>    ABILITY_RUNTIME_SUPPORTED_WINDOW_MODE_SPLIT = 1,<br/>    ABILITY_RUNTIME_SUPPORTED_WINDOW_MODE_FLOATING = 2<br/>} | 定义启动应用时支持的窗口模式。     |
