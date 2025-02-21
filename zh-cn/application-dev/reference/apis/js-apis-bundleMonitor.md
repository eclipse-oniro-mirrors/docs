# @ohos.bundle.bundleMonitor (bundleMonitor模块)

本模块提供监听应用安装，卸载，更新的能力。

> **说明：**
>
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import bundleMonitor from '@ohos.bundle.bundleMonitor';
```

## 权限列表

| 权限                                 | 权限等级    | 描述                           |
| ------------------------------------ | ----------- | ------------------------------ |
| ohos.permission.LISTEN_BUNDLE_CHANGE | system_core | 可监听应用的安装，卸载，更新。 |

权限等级参考[权限等级说明](../../security/accesstoken-overview.md#权限等级说明)。

## BundleChangeInfo

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**系统API：**  此接口为系统接口，三方应用不支持调用

| 名称       | 类型   | 可读 | 可写 | 说明                       |
| ---------- | ------ | ---- | ---- | -------------------------- |
| bundleName | string | 是   | 否   | 应用状态发生变化的应用包名。 |
| userId     | number | 是   | 否   | 应用状态发生变化的用户id。   |

## BundleChangedEvent

监听的事件类型。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**系统API：**  此接口为系统接口。

| 名称       | 说明             |
| ---------- | --------------- |
| add        | 监听应用事件。   |
| update     | 监听更新事件。   |
| remove     | 监听删除事件。   |

## bundleMonitor.on

on(type: BundleChangedEvent, callback: Callback\<BundleChangedInfo>): void

注册监听应用的安装、卸载、更新。
>**说明:**
>
>该方法需要与[bundleMonitor.off](#bundlemonitoroff)配合使用，在组件、页面、应用的生命周期结束时，使用[bundleMonitor.off](#bundlemonitoroff)注销对应用的安装、卸载、更新等事件的监听。

**需要权限：** ohos.permission.LISTEN_BUNDLE_CHANGE

**系统API：**  此接口为系统接口，三方应用不支持调用

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名                       | 类型     | 必填 | 说明               |
| ---------------------------- | -------- | ---- | ------------------ |
| type| [BundleChangedEvent](js-apis-bundleMonitor.md#BundleChangedEvent)| 是   | 注册监听的事件类型。 |
| callback | callback\<BundleChangedInfo>| 是   | 注册监听的回调函数。 |

**示例：**

```ts
import bundleMonitor from '@ohos.bundle.bundleMonitor';

try {
    bundleMonitor.on('add', (bundleChangeInfo) => {
        console.info(`bundleName : ${bundleChangeInfo.bundleName} userId : ${bundleChangeInfo.userId}`);
	})
} catch (errData) {
    console.log(`errData is errCode:${errData.errCode}  message:${errData.message}`);
}
```

## bundleMonitor.off

off(type: BundleChangedEvent, callback?: Callback\<BundleChangedInfo>): void

注销监听应用的安装，卸载，更新。

**需要权限：** ohos.permission.LISTEN_BUNDLE_CHANGE

**系统API：**  此接口为系统接口，三方应用不支持调用

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**参数：**

| 参数名                       | 类型     | 必填 | 说明                                                       |
| ---------------------------- | -------- | ---- | ---------------------------------------------------------- |
| type| [BundleChangedEvent](js-apis-bundleMonitor.md#BundleChangedEvent)| 是   | 注销监听的事件类型。                                         |
| callback | callback\<BundleChangedInfo>| 否   | 注销监听的回调函数，当为空时表示注销当前事件的所有callback。 |

**示例：**

```ts
import bundleMonitor from '@ohos.bundle.bundleMonitor';

try {
    bundleMonitor.off('add');
} catch (errData) {
    console.log(`errData is errCode:${errData.errCode}  message:${errData.message}`);
}
```