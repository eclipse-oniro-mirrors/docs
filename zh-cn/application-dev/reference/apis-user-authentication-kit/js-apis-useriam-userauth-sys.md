# @ohos.userIAM.userAuth (用户认证)(系统接口)

提供用户认证能力，可应用于设备解锁、支付、应用登录等身份认证场景。

> **说明：**
>
> - 本模块首批接口从API version 6开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> - 当前页面仅包含本模块的系统接口，其他公开接口参见[@ohos.userIAM.userAuth (用户认证)](js-apis-useriam-userauth.md)。

## 导入模块

```ts
import { userAuth } from '@kit.UserAuthenticationKit';
```

## WindowModeType<sup>10+</sup>

用户认证界面的显示类型。

**系统能力**：SystemCapability.UserIAM.UserAuth.Core

**系统接口**: 此接口为系统接口。

| 名称       | 值   | 说明       |
| ---------- | ---- | ---------- |
| DIALOG_BOX | 1    | 弹框类型。 |
| FULLSCREEN | 2    | 全屏类型。 |

## WidgetParam<sup>10+</sup>

用户认证界面配置相关参数。

**系统能力**：SystemCapability.UserIAM.UserAuth.Core

| 名称                 | 类型                                | 必填 | 说明                                                         |
| -------------------- | ----------------------------------- | ---- | ------------------------------------------------------------ |
| windowMode           | [WindowModeType](#windowmodetype10) | 否   | 代表用户认证界面的显示类型，默认值为WindowModeType.DIALOG_BOX。<br>**系统接口**: 此接口为系统接口。 |

## NoticeType<sup>10+</sup>

用户身份认证的通知类型。

**系统能力**：SystemCapability.UserIAM.UserAuth.Core

**系统接口**: 此接口为系统接口。

| 名称          | 值   | 说明                 |
| ------------- | ---- | -------------------- |
| WIDGET_NOTICE | 1    | 表示来自组件的通知。 |

## userAuth.sendNotice<sup>10+</sup>

sendNotice(noticeType: NoticeType, eventData: string): void

在使用统一身份认证控件进行用户身份认证时，用于接收来自统一身份认证控件的通知。

**需要权限**：ohos.permission.SUPPORT_USER_AUTH

**系统能力**：SystemCapability.UserIAM.UserAuth.Core

**系统接口**: 此接口为系统接口。

**参数：**

| 参数名     | 类型                        | 必填 | 说明       |
| ---------- | --------------------------- | ---- | ---------- |
| noticeType | [NoticeType](#noticetype10) | 是   | 通知类型。 |
| eventData  | string                      | 是   | 事件数据。 |

**错误码：**

以下错误码的详细介绍请参见[用户认证错误码](errorcode-useriam.md)。

| 错误码ID | 错误信息                                |
| -------- | --------------------------------------- |
| 201      | Permission verification failed.         |
| 202      | The caller is not a system application. |
| 401      | Incorrect parameters. Possible causes: 1.Mandatory parameters are left unspecified. 2.Incorrect parameter types. 3.Parameter verification failed.    |
| 12500002 | General operation error.                |

**示例：**

```ts
import { userAuth } from '@kit.UserAuthenticationKit';

interface  EventData {
  widgetContextId: number;
  event: string;
  version: string;
  payload: PayLoad;
}
interface PayLoad {
  type: Object[];
}
try {
  const eventData : EventData = {
    widgetContextId: 123456,
    event: 'EVENT_AUTH_TYPE_READY',
    version: '1',
    payload: {
      type: ['pin']
    } as PayLoad,
  };
  const jsonEventData = JSON.stringify(eventData);
  let noticeType = userAuth.NoticeType.WIDGET_NOTICE;
  userAuth.sendNotice(noticeType, jsonEventData);
  console.log('sendNotice success');
} catch (error) {
  console.error('sendNotice catch error: ' + JSON.stringify(error));
}
```

## UserAuthWidgetMgr<sup>10+</sup>

组件管理接口，可将用身份认证控件注册到UserAuthWidgetMgr中，由UserAuthWidgetMgr进行管理、调度。

### on<sup>10+</sup>

on(type: 'command', callback: IAuthWidgetCallback): void

身份认证控件订阅来自用户认证框架的命令。

**系统能力**：SystemCapability.UserIAM.UserAuth.Core

**系统接口**: 此接口为系统接口。

**参数：**

| 参数名   | 类型                                          | 必填 | 说明                                                         |
| -------- | --------------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | 'command'                                     | 是   | 订阅事件类型，表明该事件用于用户认证框架向身份认证控件发送命令。 |
| callback | [IAuthWidgetCallback](#iauthwidgetcallback10) | 是   | 组件管理接口的回调函数，用于用户认证框架向身份认证控件发送命令。 |

**错误码：**

以下错误码的详细介绍请参见[用户认证错误码](errorcode-useriam.md)。

| 错误码ID | 错误信息                 |
| -------- | ------------------------ |
| 401      | Incorrect parameters. Possible causes: 1.Mandatory parameters are left unspecified. 2.Incorrect parameter types. 3.Parameter verification failed. |
| 12500002 | General operation error. |

**示例：**

```ts
import { userAuth } from '@kit.UserAuthenticationKit';

const userAuthWidgetMgrVersion = 1;
try {
  let userAuthWidgetMgr = userAuth.getUserAuthWidgetMgr(userAuthWidgetMgrVersion);
  console.log('get userAuthWidgetMgr instance success');
  userAuthWidgetMgr.on('command', {
    sendCommand(cmdData) {
      console.log('The cmdData is ' + cmdData);
    }
  })
  console.log('subscribe authentication event success');
} catch (error) {
  console.error('userAuth widgetMgr catch error: ' + JSON.stringify(error));
}
```

### off<sup>10+</sup>

off(type: 'command', callback?: IAuthWidgetCallback): void

身份认证控件取消订阅来自用户认证框架的命令。

**系统能力**：SystemCapability.UserIAM.UserAuth.Core

**系统接口**: 此接口为系统接口。

**参数：**

| 参数名   | 类型                                          | 必填 | 说明                                                         |
| -------- | --------------------------------------------- | ---- | ------------------------------------------------------------ |
| type     | 'command'                                     | 是   | 订阅事件类型，表明该事件用于用户认证框架向身份认证控件发送命令。 |
| callback | [IAuthWidgetCallback](#iauthwidgetcallback10) | 否   | 组件管理接口的回调函数，用于用户认证框架向身份认证控件发送命令。 |

**错误码：**

以下错误码的详细介绍请参见[用户认证错误码](errorcode-useriam.md)。

| 错误码ID | 错误信息                 |
| -------- | ------------------------ |
| 401      | Incorrect parameters. Possible causes: 1.Mandatory parameters are left unspecified. 2.Incorrect parameter types. 3.Parameter verification failed. |
| 12500002 | General operation error. |

**示例：**

```ts
import { userAuth } from '@kit.UserAuthenticationKit';

const userAuthWidgetMgrVersion = 1;
try {
  let userAuthWidgetMgr = userAuth.getUserAuthWidgetMgr(userAuthWidgetMgrVersion);
  console.log('get userAuthWidgetMgr instance success');
  userAuthWidgetMgr.off('command', {
    sendCommand(cmdData) {
      console.log('The cmdData is ' + cmdData);
    }
  })
  console.log('cancel subscribe authentication event success');
} catch (error) {
  console.error('userAuth widgetMgr catch error: ' + JSON.stringify(error));
}
```

## userAuth.getUserAuthWidgetMgr<sup>10+</sup>

getUserAuthWidgetMgr(version: number): UserAuthWidgetMgr

获取UserAuthWidgetMgr对象，用于执行用户身份认证。

> **说明：**
> 每个UserAuthInstance只能进行一次认证，若需要再次进行认证则需重新获取UserAuthInstance。

**需要权限**：ohos.permission.SUPPORT_USER_AUTH

**系统能力**：SystemCapability.UserIAM.UserAuth.Core

**系统接口**: 此接口为系统接口。

**参数：**

| 参数名  | 类型   | 必填 | 说明                 |
| ------- | ------ | ---- | -------------------- |
| version | number | 是   | 表示认证组件的版本。 |

**返回值：**

| 类型                                      | 说明         |
| ----------------------------------------- | ------------ |
| [UserAuthWidgetMgr](#userauthwidgetmgr10) | 认证器对象。 |

**错误码：**

以下错误码的详细介绍请参见[用户认证错误码](errorcode-useriam.md)。

| 错误码ID | 错误信息                                |
| -------- | --------------------------------------- |
| 201      | Permission verification failed.         |
| 202      | The caller is not a system application. |
| 401      | Incorrect parameters. Possible causes: 1.Mandatory parameters are left unspecified. 2.Incorrect parameter types.                                     |
| 12500002 | General operation error.                |

**示例：**

```ts
import { userAuth } from '@kit.UserAuthenticationKit';

let userAuthWidgetMgrVersion = 1;
try {
  let userAuthWidgetMgr = userAuth.getUserAuthWidgetMgr(userAuthWidgetMgrVersion);
  console.log('get userAuthWidgetMgr instance success');
} catch (error) {
  console.error('userAuth widgetMgr catch error: ' + JSON.stringify(error));
}
```

## IAuthWidgetCallback<sup>10+</sup>

认证组件通过该回调获取用户认证框架发送的命令。

### sendCommand<sup>10+</sup>

sendCommand(cmdData: string): void

回调函数，用于用户认证框架向组件发送命令。

**系统能力**：SystemCapability.UserIAM.UserAuth.Core

**系统接口**: 此接口为系统接口。

**参数：**

| 参数名  | 类型   | 必填 | 说明                               |
| ------- | ------ | ---- | ---------------------------------- |
| cmdData | string | 是   | 用户身份认证框架向控件发送的命令。 |

**示例：**

```ts
import { userAuth } from '@kit.UserAuthenticationKit';

const userAuthWidgetMgrVersion = 1;
try {
  let userAuthWidgetMgr = userAuth.getUserAuthWidgetMgr(userAuthWidgetMgrVersion);
  console.log('get userAuthWidgetMgr instance success');
  userAuthWidgetMgr.on('command', {
    sendCommand(cmdData) {
      console.log('The cmdData is ' + cmdData);
    }
  })
  console.log('subscribe authentication event success');
} catch (error) {
  console.error('userAuth widgetMgr catch error: ' + JSON.stringify(error));
}
```
