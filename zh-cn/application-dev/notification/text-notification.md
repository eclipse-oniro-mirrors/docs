# 发布文本类型通知

文本类型通知主要应用于发送短信息、提示信息等，支持普通文本类型和多行文本类型。

**表1** 基础类型通知中的内容分类

| 类型                             | 描述          |
| ------------------------------- | ------------- |
| NOTIFICATION_CONTENT_BASIC_TEXT | 普通文本类型。 |
| NOTIFICATION_CONTENT_MULTILINE  | 多行文本类型。 |

## 接口说明

通知发布接口说明详见下表，通知发布的详情可通过入参[NotificationRequest](../reference/apis-notification-kit/js-apis-inner-notification-notificationRequest.md#notificationrequest)来进行指定，可以包括通知内容，通知ID，通知的通道类型和通知发布时间等信息。

| **接口名** | **描述** |
| -------- | -------- |
| publish(request:&nbsp;NotificationRequest,&nbsp;callback:&nbsp;AsyncCallback&lt;void&gt;):&nbsp;void | 发布通知。                 |
| cancel(id:&nbsp;number,&nbsp;label:&nbsp;string,&nbsp;callback:&nbsp;AsyncCallback&lt;void&gt;):&nbsp;void | 取消指定的通知。           |
| cancelAll(callback:&nbsp;AsyncCallback&lt;void&gt;):&nbsp;void; | 取消所有该应用发布的通知。 |


## 开发步骤

1. 导入模块。
   
   ```ts
   import notificationManager from '@ohos.notificationManager';
   import Base from '@ohos.base';
   ```

2. 构造NotificationRequest对象，并发布通知。
   - 普通文本类型通知由标题、文本内容和附加信息三个字段组成，其中标题和文本内容是必填字段，大小均需要小于200字节。
     
      ```ts
      let notificationRequest: notificationManager.NotificationRequest = {
        id: 1,
        content: {
          notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT, // 普通文本类型通知
          normal: {
            title: 'test_title',
            text: 'test_text',
            additionalText: 'test_additionalText',
          }
        }
      };
      notificationManager.publish(notificationRequest, (err:Base.BusinessError) => {
        if (err) {
          console.error(`Failed to publish notification. Code is ${err.code}, message is ${err.message}`);
          return;
        }
        console.info('Succeeded in publishing notification.');
      });
      ```


   - 多行文本类型通知继承了普通文本类型的字段，同时新增了多行文本内容、内容概要和通知展开时的标题，其字段均小于200字节。通知默认显示与普通文本相同，展开后，标题显示为展开后标题内容，多行文本内容多行显示。
     
      ```ts
      let notificationRequest: notificationManager.NotificationRequest = {
        id: 3,
        content: {
          notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_MULTILINE, // 多行文本类型通知
          multiLine: {
            title: 'test_title',
            text: 'test_text',
            briefText: 'test_briefText',
            longTitle: 'test_longTitle',
            lines: ['line_01', 'line_02', 'line_03', 'line_04'],
          }
        }
      };
      // 发布通知
      notificationManager.publish(notificationRequest, (err:Base.BusinessError) => {
        if (err) {
          console.error(`Failed to publish notification. Code is ${err.code}, message is ${err.message}`);
          return;
        }
        console.info('Succeeded in publishing notification.');
      });
      ```
3. 删除通知。

   ```ts
    notificationManager.cancel(1, (err:Base.BusinessError) => {
      if (err) {
        console.error(`Failed to cancel notification. Code is ${err.code}, message is ${err.message}`);
        return;
      }
      console.info('Succeeded in cancel notification.');
    });
   ```