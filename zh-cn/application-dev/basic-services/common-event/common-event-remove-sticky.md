# 移除粘性公共事件（仅对系统应用开放）


## 场景介绍

已发出的粘性公共事件后来订阅者也可以接收到，如果这个事件不再转发，需要事件发布者进行移除。系统提供了粘性公共事件移除接口。

## 接口说明

参考[接口文档](../../reference/apis-basic-services-kit/js-apis-commonEventManager.md)。

| 接口名 | 接口描述 |
| -------- | -------- |
| removeStickyCommonEvent(event: string, callback: AsyncCallback\<void>): void | 移除粘性公共事件 |


## 开发步骤

1. 需要申请`ohos.permission.COMMONEVENT_STICKY`权限，配置方式请参见[声明权限](../../security/AccessToken/declare-permissions.md)。

2. 导入模块。

   ```ts
   import Base from '@ohos.base';
   import commonEventManager from '@ohos.commonEventManager';

   const TAG: string = 'ProcessModel';
   ```

3. 调用[`removeStickyCommonEvent()`](../../reference/apis-basic-services-kit/js-apis-commonEventManager-sys.md#commoneventmanagerremovestickycommonevent10)方法移除对应的粘性公共事件。

   > **说明：**
   >
   > 移除的粘性公共事件，必须是本应用之前已发布的粘性公共事件，发布粘性公共事件参考[公共事件发布](common-event-publish.md)章节。

   ```ts
   // 移除粘性公共事件，其中的event字段需要替换为实际的事件名称。
   commonEventManager.removeStickyCommonEvent('event', (err: Base.BusinessError) => {
     // sticky_event粘性公共事件名
     if (err) {
       console.error(TAG, `Failed to remove sticky common event. Code is ${err.code}, message is ${err.message}`);
       return;
     }
     ...
     console.info(TAG, `Succeeded in removeing sticky event.`);
   });
   ```

