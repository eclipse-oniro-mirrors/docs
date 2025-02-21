# Context

Context模块提供了ability或application的上下文的能力，包括访问特定应用程序的资源等。

> **说明：**
>
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> 本模块接口仅可在Stage模型下使用。

## 导入模块

```ts
import common from '@ohos.app.ability.common';
```

## 属性

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

| 名称          | 类型     | 可读   | 可写   | 说明      |
| ----------- | ------ | ---- | ---- | ------- |
| resourceManager     | resmgr.[ResourceManager](js-apis-resource-manager.md) | 是    | 否    | 资源管理对象。   |
| applicationInfo | [ApplicationInfo](js-apis-bundle-ApplicationInfo.md) | 是    | 否    | 当前应用程序的信息。 |
| cacheDir | string | 是    | 否    | 缓存目录。 |
| tempDir | string | 是    | 否    | 临时目录。 |
| filesDir | string | 是    | 否    | 文件目录。 |
| databaseDir | string | 是    | 否    | 数据库目录。 |
| preferencesDir | string | 是    | 否    | preferences目录。 |
| bundleCodeDir | string | 是    | 否    | 安装包目录。不能拼接路径访问资源文件，请使用[资源管理接口](js-apis-resource-manager.md)访问资源。 |
| distributedFilesDir | string | 是    | 否    | 分布式文件目录。 |
| eventHub | [EventHub](js-apis-inner-application-eventHub.md) | 是    | 否    | 事件中心，提供订阅、取消订阅、触发事件对象。 |
| area | [AreaMode](#areamode) | 是    | 否    | 文件分区信息。 |


## Context.createBundleContext

createBundleContext(bundleName: string): Context;

根据包名创建安装包的上下文Context。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**：该接口为系统接口，三方应用不支持调用。

**参数：**

| 名称       | 类型                     | 必填   | 说明            |
| -------- | ---------------------- | ---- | ------------- |
| bundleName | string | 是    | 包名。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Context | 安装包的上下文Context。 |

**示例：**

```ts
let bundleContext: common.Context;
try {
    bundleContext = this.context.createBundleContext('com.example.test');
} catch (error) {
    console.error('createBundleContext failed, error.code: ${error.code}, error.message: ${error.message}');
}
```

## Context.createModuleContext

createModuleContext(moduleName: string): Context;

根据模块名创建上下文Context。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**

| 名称       | 类型                     | 必填   | 说明            |
| -------- | ---------------------- | ---- | ------------- |
| moduleName | string | 是    | 模块名。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Context | 上下文Context。 |

**示例：**

```ts
let moduleContext: common.Context;
try {
    moduleContext = this.context.createModuleContext('entry');
} catch (error) {
    console.error('createModuleContext failed, error.code: ${error.code}, error.message: ${error.message}');
}
```

## Context.createModuleContext

createModuleContext(bundleName: string, moduleName: string): Context;

根据包名和模块名创建上下文Context。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**系统API**：该接口为系统接口，三方应用不支持调用。

**参数：**

| 名称       | 类型                     | 必填   | 说明            |
| -------- | ---------------------- | ---- | ------------- |
| bundleName | string | 是    | 包名。 |
| moduleName | string | 是    | 模块名。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Context | 上下文Context。 |

**示例：**

```ts
let moduleContext: common.Context;
try {
    moduleContext = this.context.createModuleContext('com.example.test', 'entry');
} catch (error) {
    console.error('createModuleContext failed, error.code: ${error.code}, error.message: ${error.message}');
}
```

## Context.getApplicationContext

getApplicationContext(): ApplicationContext;

获取应用上下文Context。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Context | 应用上下文Context。 |

**示例：**

```ts
let applicationContext: common.Context;
try {
    applicationContext = this.context.getApplicationContext();
} catch (error) {
    console.error('getApplicationContext failed, error.code: ${error.code}, error.message: ${error.message}');
}
```

## AreaMode

文件分区

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

| 名称 | 值 | 说明 |
| -------- | -------- | -------- |
| EL1 | 0 | 设备级加密区，设备开机后可访问的数据区。 |
| EL2 | 1 | 用户级加密区，设备开机，首次输入密码后才能够访问的数据区。 |
