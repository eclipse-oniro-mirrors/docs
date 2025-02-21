# @ohos.application.testRunner (TestRunner)

TestRunner模块提供了框架测试的能力。包括准备单元测试环境、运行测试用例。

如果您想实现自己的单元测试框架，您必须继承这个类并覆盖它的所有方法。

> **说明：**
> 
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。  

## 导入模块

```ts
import TestRunner from '@ohos.application.testRunner';
```

## TestRunner.onPrepare

onPrepare(): void

为运行测试用例准备单元测试环境

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**示例：**

```ts
export default class UserTestRunner implements TestRunner {
    onPrepare() {
        console.log('Trigger onPrepare');
    }
    onRun() {}
};
```



## TestRunner.onRun

onRun(): void

运行测试用例

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**示例：**

```ts
export default class UserTestRunner implements TestRunner {
    onPrepare() {}
    onRun() {
        console.log('Trigger onRun');
    }
};
```
