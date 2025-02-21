# @ohos.uiAppearance (用户界面外观)(系统接口)

用户界面外观提供管理系统外观的一些基础能力，目前仅包括深浅色模式配置。

> **说明：**
>
> 从API Version 10开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。
>
> 本模块接口为系统接口。


## 导入模块

```ts
import uiAppearance from '@ohos.uiAppearance'
```


## DarkMode

深色模式枚举。


**系统能力：** SystemCapability.ArkUI.UiAppearance

| 名称 | 值 | 说明 |
| -- | -- | -- |
| ALWAYS_DARK | 0 | 系统始终为深色。  |
| ALWAYS_LIGHT | 1 | 系统始终为浅色。 |


## uiAppearance.setDarkMode

setDarkMode(mode: DarkMode, callback: AsyncCallback\<void>): void

设置系统深色模式。

**需要权限：** ohos.permission.UPDATE_CONFIGURATION

**系统能力：** SystemCapability.ArkUI.UiAppearance

**参数：** 

| 参数名 | 类型 | 必填 | 说明 |
| -- | -- | -- | -- |
| mode | [DarkMode](#darkmode) | 是 | 指定系统的深色模式配置 |
| callback | AsyncCallback\<void>| 是 | 配置深色模式的异步回调 |

**错误码：**

错误码详细介绍请参考[errcode-uiappearance](errorcode-uiappearance.md)。

| 错误码ID | 错误信息 |
| -- | -- |
| 500001 | Internal error. |

**示例：** 

  ```ts
import uiAppearance from '@ohos.uiAppearance'
import { BusinessError } from '@ohos.base';
try {
    uiAppearance.setDarkMode(uiAppearance.DarkMode.ALWAYS_DARK, (error) => {
      if (error) {
        console.error('Set dark-mode failed, ' + error.message);
      } else {
        console.info('Set dark-mode successfully.');
      }
    })
} catch (error) {
    let message = (error as BusinessError).message;
    console.error('Set dark-mode failed, ' + message);
}
  ```


## uiAppearance.setDarkMode

setDarkMode(mode: DarkMode): Promise\<void>;

设置系统深色模式。

**需要权限：** ohos.permission.UPDATE_CONFIGURATION

**系统能力：** SystemCapability.ArkUI.UiAppearance

**参数：** 

| 参数名 | 类型 | 必填 | 说明 |
| -- | -- | -- | -- |
| mode | [DarkMode](#darkmode) | 是 | 指定系统深色模式配置 |

**返回值：**

| 类型   | 说明                           |
| ------ | ------------------------------ |
| Promise\<void> | Promise对象。无返回结果的Promise对象。|

**错误码：**

错误码详细介绍请参考[errcode-uiappearance](errorcode-uiappearance.md)。

| 错误码ID | 错误信息 |
| -- | -- |
| 500001 | Internal error. |

**示例：** 

  ```ts
import uiAppearance from '@ohos.uiAppearance'
import { BusinessError } from '@ohos.base';
try {
    uiAppearance.setDarkMode(uiAppearance.DarkMode.ALWAYS_DARK).then(() => {
      console.info('Set dark-mode successfully.');
    }).catch((error:Error) => {
      console.error('Set dark-mode failed, ' + error.message);
    });
} catch (error) {
    let message = (error as BusinessError).message;
    console.error('Set dark-mode failed, ' + message);
}
  ```


## uiAppearance.getDarkMode

getDarkMode(): DarkMode;

获取当前的深色模式配置。

**需要权限：** ohos.permission.UPDATE_CONFIGURATION

**系统能力：** SystemCapability.ArkUI.UiAppearance

**返回值：** 

| 类型 | 说明 |
| -- | -- |
|[DarkMode](#darkmode) | 系统当前的深色模式配置 |

**错误码：**

错误码详细介绍请参考[errcode-uiappearance](errorcode-uiappearance.md)。

| 错误码ID | 错误信息 |
| -- | -- |
| 500001 | Internal error. |

**示例：** 

  ```ts
import uiAppearance from '@ohos.uiAppearance'
import { BusinessError } from '@ohos.base';
try {
    let darkMode = uiAppearance.getDarkMode();
    console.info('Get dark-mode ' + darkMode);
} catch (error) {
    let message = (error as BusinessError).message;
    console.error('Get dark-mode failed, ' + message);
}
  ```