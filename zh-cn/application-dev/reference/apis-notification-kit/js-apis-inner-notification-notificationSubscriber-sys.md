# NotificationSubscriber(系统接口)

作为订阅通知接口[subscribe](./js-apis-notificationSubscribe-sys.md)的入参，提供订阅者接收到新通知、取消通知等的回调方法。

> **说明：**
>
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>
> 本模块为系统接口。

## 导入模块

```js
import notificationSubscribe from '@ohos.notificationSubscribe';
```

## onConsume

onConsume?: (data: [SubscribeCallbackData](#subscribecallbackdata)) => void

接收到新通知的回调函数。

**系统能力**：SystemCapability.Notification.Notification

**系统接口**: 此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ------------ | ------------------------ | ---- | -------------------------- |
| onConsume | (data: [SubscribeCallbackData](#subscribecallbackdata)) => void | 是 | 新接收到的通知信息。 |

**示例：**

```ts
import Base from '@ohos.base';

let subscribeCallback = (err: Base.BusinessError) => {
  if (err) {
    console.error(`subscribe failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("subscribeCallback");
  }
};

let onConsumeCallback = (data: notificationSubscribe.SubscribeCallbackData) => {
  console.info('===> onConsume in test');
  let req = data.request;
  console.info('===> onConsume callback req.id:' + req.id);
};

let subscriber: notificationSubscribe.NotificationSubscriber = {
  onConsume: onConsumeCallback
};

notificationSubscribe.subscribe(subscriber, subscribeCallback);
```

## onCancel

onCancel?:(data: [SubscribeCallbackData](#subscribecallbackdata)) => void

取消通知的回调函数。

**系统能力**：SystemCapability.Notification.Notification

**系统接口**: 此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ------------ | ------------------------ | ---- | -------------------------- |
| onCancel | (data: [SubscribeCallbackData](#subscribecallbackdata)) => void | 是 | 需要取消的通知信息。 |

**示例：**

```ts
import Base from '@ohos.base';

let subscribeCallback = (err: Base.BusinessError) => {
  if (err) {
    console.error(`subscribe failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("subscribeCallback");
  }
};

let onCancelCallback = (data: notificationSubscribe.SubscribeCallbackData) => {
  console.info('===> onCancel in test');
  let req = data.request;
  console.info('===> onCancel callback req.id:' + req.id);
}

let subscriber: notificationSubscribe.NotificationSubscriber = {
  onCancel: onCancelCallback
};

notificationSubscribe.subscribe(subscriber, subscribeCallback);
```

## onUpdate

onUpdate?:(data: [NotificationSortingMap](js-apis-inner-notification-notificationSortingMap-sys.md)) => void

更新通知排序的回调函数。

**系统能力**：SystemCapability.Notification.Notification

**系统接口**: 此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ------------ | ------------------------ | ---- | -------------------------- |
| onUpdate | (data: [NotificationSortingMap](js-apis-inner-notification-notificationSortingMap-sys.md)) => void | 是 | 最新的通知排序列表。 |

**示例：**

```ts
import Base from '@ohos.base';

let subscribeCallback = (err: Base.BusinessError) => {
  if (err) {
    console.error(`subscribe failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("subscribeCallback");
  }
};

let subscriber: notificationSubscribe.NotificationSubscriber = {
  onUpdate: (map) => {
    console.info('===> onUpdateCallback map:' + JSON.stringify(map));
  }
};

notificationSubscribe.subscribe(subscriber, subscribeCallback);
```

## onConnect

onConnect?:() => void

订阅完成的回调函数。

**系统能力**：SystemCapability.Notification.Notification

**系统接口**: 此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ------------ | ------------------------ | ---- | -------------------------- |
| onConnect | () => void | 是 | 订阅完成的回调。 |

**示例：**

```ts
import Base from '@ohos.base';

let subscribeCallback = (err: Base.BusinessError) => {
  if (err) {
    console.error(`subscribe failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("subscribeCallback");
  }
};

let onConnectCallback = () => {
  console.info('===> onConnect in test');
}

let subscriber: notificationSubscribe.NotificationSubscriber = {
  onConnect: onConnectCallback
};

notificationSubscribe.subscribe(subscriber, subscribeCallback);
```

## onDisconnect

onDisconnect?:() => void

取消订阅的回调函数。

**系统能力**：SystemCapability.Notification.Notification

**系统接口**: 此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ------------ | ------------------------ | ---- | -------------------------- |
| onDisconnect | () => void | 是 | 取消订阅的回调。 |

**示例：**

```ts
import Base from '@ohos.base';

let subscribeCallback = (err: Base.BusinessError) => {
  if (err) {
    console.error(`subscribe failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("subscribeCallback");
  }
};
let unsubscribeCallback = (err: Base.BusinessError) => {
  if (err) {
    console.error(`unsubscribe failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("unsubscribeCallback");
  }
};

let onConnectCallback = () => {
  console.info('===> onConnect in test');
}
let onDisconnectCallback = () => {
  console.info('===> onDisconnect in test');
}

let subscriber: notificationSubscribe.NotificationSubscriber = {
  onConnect: onConnectCallback,
  onDisconnect: onDisconnectCallback
};

// 订阅通知后会收到onConnect回调
notificationSubscribe.subscribe(subscriber, subscribeCallback);
// 取消订阅后会收到onDisconnect回调
notificationSubscribe.unsubscribe(subscriber, unsubscribeCallback);
```

## onDestroy

onDestroy?:() => void

服务失联回调函数。

**系统能力**：SystemCapability.Notification.Notification

**系统接口**: 此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ------------ | ------------------------ | ---- | -------------------------- |
| onDestroy | () => void | 是 | 服务失联的回调。 |

**示例：**

```ts
import Base from '@ohos.base';

let subscribeCallback = (err: Base.BusinessError) => {
  if (err) {
    console.error(`subscribe failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("subscribeCallback");
  }
};

let onDestroyCallback = () => {
  console.info('===> onDestroy in test');
}

let subscriber: notificationSubscribe.NotificationSubscriber = {
  onDestroy: onDestroyCallback
};

notificationSubscribe.subscribe(subscriber, subscribeCallback);
```

## onDoNotDisturbDateChange<sup>8+</sup>(deprecated)

onDoNotDisturbDateChange?:(mode: notification.[DoNotDisturbDate](js-apis-notification-sys.md#donotdisturbdate)) => void

免打扰时间选项发生变更时的回调函数。

> **说明：**
>
> 此接口从API version 8开始支持，从API version 11开始不再维护，建议使用[onDoNotDisturbChanged](js-apis-inner-notification-notificationSubscriber-sys.md#ondonotdisturbchanged11)代替。

**系统能力**：SystemCapability.Notification.Notification

**系统接口**: 此接口为系统接口。

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ------------ | ------------------------ | ---- | -------------------------- |
| onDoNotDisturbDateChange | (mode: notification.[DoNotDisturbDate](js-apis-notification-sys.md#donotdisturbdate)) => void | 是 | 回调返回免打扰时间选项变更。 |

**示例：**

```ts
import Base from '@ohos.base';
import Notification from '@ohos.notification';

let subscribeCallback = (err: Base.BusinessError) => {
  if (err) {
    console.error(`subscribe failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("subscribeCallback");
  }
};

let onDoNotDisturbDateChangeCallback = (mode: Notification.DoNotDisturbDate) => {
  console.info('===> onDoNotDisturbDateChange:' + mode);
}

let subscriber: notificationSubscribe.NotificationSubscriber = {
  onDoNotDisturbDateChange: onDoNotDisturbDateChangeCallback
};

notificationSubscribe.subscribe(subscriber, subscribeCallback);
```

## onDoNotDisturbChanged<sup>11+</sup>

onDoNotDisturbChanged?:(mode: notificationManager.[DoNotDisturbDate](js-apis-notificationManager-sys.md#donotdisturbdate)) => void

免打扰时间选项发生变更时的回调函数。

**系统接口**: 此接口为系统接口。

**系统能力**：SystemCapability.Notification.Notification

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| ------------ | ------------------------ | ---- | -------------------------- |
| onDoNotDisturbChanged | (mode: notificationManager.[DoNotDisturbDate](js-apis-notificationManager-sys.md#donotdisturbdate)) => void | 是 | 回调返回免打扰时间选项变更。 |

**示例：**

```ts
import Base from '@ohos.base';
import NotificationManager from '@ohos.notificationManager';

let subscribeCallback = (err: Base.BusinessError) => {
  if (err) {
    console.error(`subscribe failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("subscribeCallback");
  }
};

let onDoNotDisturbChangedCallback = (mode: NotificationManager.DoNotDisturbDate) => {
  console.info('===> onDoNotDisturbChanged:' + mode);
}

let subscriber: notificationSubscribe.NotificationSubscriber = {
  onDoNotDisturbChanged: onDoNotDisturbChangedCallback
};

notificationSubscribe.subscribe(subscriber, subscribeCallback);
```

## onEnabledNotificationChanged<sup>8+</sup>

onEnabledNotificationChanged?:(callbackData: [EnabledNotificationCallbackData](#enablednotificationcallbackdata8)) => void

监听应用通知使能变化。

**系统能力**：SystemCapability.Notification.Notification

**系统接口**: 此接口为系统接口。

**参数：**

| 参数名 | 类型                                                                                                           | 必填 | 说明 |
| ------------ |--------------------------------------------------------------------------------------------------------------| ---- | -------------------------- |
| onEnabledNotificationChanged | (callbackData: [EnabledNotificationCallbackData](#enablednotificationcallbackdata8)) => void | 是 | 回调返回监听到的应用信息。 |

**示例：**

```ts
import Base from '@ohos.base';

let subscribeCallback = (err: Base.BusinessError) => {
  if (err) {
    console.error(`subscribe failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("subscribeCallback");
  }
};

let onEnabledNotificationChangedCallback = (callbackData: notificationSubscribe.EnabledNotificationCallbackData) => {
  console.info("bundle: ", callbackData.bundle);
  console.info("uid: ", callbackData.uid);
  console.info("enable: ", callbackData.enable);
};

let subscriber: notificationSubscribe.NotificationSubscriber = {
  onEnabledNotificationChanged: onEnabledNotificationChangedCallback
};

notificationSubscribe.subscribe(subscriber, subscribeCallback);
```

## onBadgeChanged<sup>10+</sup>

 onBadgeChanged?:(data: [BadgeNumberCallbackData](#badgenumbercallbackdata10)) => void

监听应用角标个数变化。

**系统能力**：SystemCapability.Notification.Notification

**系统接口**: 此接口为系统接口。

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                       |
| -------- | ------------------------------------------------------------ | ---- | -------------------------- |
| onBadgeChanged | (data: [BadgeNumberCallbackData](#badgenumbercallbackdata10)) => void | 是   | 回调返回监听到的应用信息。 |

**示例：**

```ts
import Base from '@ohos.base';

let subscribeCallback = (err: Base.BusinessError) => {
  if (err) {
    console.error(`subscribe failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("subscribeCallback");
  }
};

let subscriber: notificationSubscribe.NotificationSubscriber = {
  onBadgeChanged: (data) => {
    console.info("bundle: ", data.bundle);
    console.info("uid: ", data.uid);
    console.info("badgeNumber: ", data.badgeNumber);
  }
};

notificationSubscribe.subscribe(subscriber, subscribeCallback);
```


## onBatchCancel<sup>11+</sup>

 onBatchCancel?:(data: Array<[SubscribeCallbackData](#subscribecallbackdata)>) => void

批量删除的回调函数。

**系统能力**：SystemCapability.Notification.Notification

**系统接口**: 此接口为系统接口。

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                       |
| -------- | ------------------------------------------------------------ | ---- | -------------------------- |
| onBatchCancel | (data: Array<[SubscribeCallbackData](#subscribecallbackdata)>) => void | 是   | 批量删除的通知信息。 |

**示例：**

```ts
import Base from '@ohos.base';

let subscribeCallback = (err: Base.BusinessError) => {
  if (err) {
    console.error(`subscribe failed, code is ${err.code}, message is ${err.message}`);
  } else {
    console.info("subscribeCallback");
  }
};

let onBatchCancelCallBack = (data: Array<notificationSubscribe.SubscribeCallbackData>) => {
  console.info('===> onBatchCancel in test');
  let req = data[0].request;
  console.info('===> onBatchCancel callback req.id:' + req.id);
};

let subscriber: notificationSubscribe.NotificationSubscriber = {
  onBatchCancel: onBatchCancelCallBack
};

notificationSubscribe.subscribe(subscriber, subscribeCallback);
```
## SubscribeCallbackData

**系统能力**：以下各项对应的系统能力均为SystemCapability.Notification.Notification

**系统接口**：此接口为系统接口。

| 名称            | 类型                                                                 | 可读 | 可写 | 说明     |
| --------------- |--------------------------------------------------------------------| ---- | --- | -------- |
| request         | [NotificationRequest](js-apis-notification.md#notificationrequest) | 是  | 否  | 通知内容。 |
| sortingMap      | [NotificationSortingMap](js-apis-inner-notification-notificationSortingMap-sys.md) | 是  | 否  | 通知排序信息。 |
| reason          | number                                                             | 是  | 否  | 删除原因（1:点击通知后删除通知，2:用户删除通知） 。|
| sound           | string                                                             | 是  | 否  | 通知声音。 |
| vibrationValues | Array\<number\>                                                    | 是  | 否  | 通知震动。 |


## EnabledNotificationCallbackData<sup>8+</sup>

**系统能力**：以下各项对应的系统能力均为SystemCapability.Notification.Notification

**系统接口**：此接口为系统接口。

| 名称   | 类型    | 可读 | 可写 | 说明             |
| ------ | ------- | ---- | --- | ---------------- |
| bundle | string  | 是  | 否  | 应用的包名。       |
| uid    | number  | 是  | 否  | 应用的uid。        |
| enable | boolean | 是  | 否  | 应用通知使能状态。 |


## BadgeNumberCallbackData<sup>10+</sup>

**系统能力**：以下各项对应的系统能力均为SystemCapability.Notification.Notification

**系统接口**：此接口为系统接口。

| 名称        | 类型   | 可读 | 可写 | 说明         |
| ----------- | ------ | ---- | ---- | ------------ |
| bundle      | string | 是   | 否   | 应用的包名。 |
| uid         | number | 是   | 否   | 应用的uid。  |
| badgeNumber | number | 是   | 否   | 角标个数。   |

