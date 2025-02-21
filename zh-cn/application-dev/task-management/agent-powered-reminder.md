# 代理提醒

## 概述

### 功能介绍

应用退到后台或进程终止后，仍然有一些提醒用户的定时类任务，例如购物类应用抢购提醒等，为满足此类功能场景，系统提供了代理提醒（reminderAgentManager）的能力。当应用退至后台或进程终止后，系统会代理应用做相应的提醒。当前支持的提醒类型包括：倒计时、日历和闹钟。

- 倒计时类：基于倒计时的提醒功能。

- 日历类：基于日历的提醒功能。

- 闹钟类：基于时钟的提醒功能。

### 约束与限制

- **个数限制**：一个三方应用支持最多30个有效提醒（有效即发布成功），一个系统应用支持最多10000个有效提醒，整个系统最多支持12000个有效提醒。

- **跳转限制**：点击提醒通知后跳转的应用必须是申请代理提醒的本应用。


## 接口说明

**表1** 主要接口

以下是代理提醒的相关接口，下表均以Promise形式为例，更多接口及使用方式请见后台代理提醒文档。
| 接口名 | 描述 |
| -------- | -------- |
| publishReminder(reminderReq: ReminderRequest): Promise&lt;number&gt; | 发布一个定时提醒类通知 |
| cancelReminder(reminderId: number): Promise&lt;void&gt; | 取消一个指定的提醒类通知 |
| getValidReminders(): Promise&lt;Array&lt;ReminderRequest&gt;&gt; | 获取当前应用设置的所有有效的提醒 |
| cancelAllReminders(): Promise&lt;void&gt; | 取消当前应用设置的所有提醒 |
| addNotificationSlot(slot: NotificationSlot): Promise&lt;void&gt; | 注册一个提醒类需要使用的通知通道（NotificationSlot） |
| removeNotificationSlot(slotType: notification.SlotType): Promise&lt;void&gt; | 删除指定的通知通道（NotificationSlot） |


## 开发步骤

1. 申请ohos.permission.PUBLISH_AGENT_REMINDER权限，配置方式请参阅[配置文件权限声明](../security/accesstoken-guidelines.md#配置文件权限声明)。

2. [使能通知开关](../notification/notification-enable.md)。获得用户授权后，才能使用代理提醒功能。

3. 导入模块。
   
   ```js
   import reminderAgentManager from '@ohos.reminderAgentManager';
   import notificationManager from '@ohos.notificationManager';
   ```

4. 定义目标提醒代理。开发者根据实际需要，选择定义如下类型的提醒。

   - 定义倒计时实例。
     
      ```js
      let targetReminderAgent: reminderAgentManager.ReminderRequestTimer = {
        reminderType: reminderAgentManager.ReminderType.REMINDER_TYPE_TIMER,   // 提醒类型为倒计时类型
        triggerTimeInSeconds: 10,
        actionButton: [ // 设置弹出的提醒通知信息上显示的按钮类型和标题
          {
            title: 'close',
            type: reminderAgentManager.ActionButtonType.ACTION_BUTTON_TYPE_CLOSE
          }
        ],
        wantAgent: {     // 点击提醒通知后跳转的目标UIAbility信息
          pkgName: 'com.example.myapplication',
          abilityName: 'EntryAbility'
        },
        maxScreenWantAgent: { // 全屏显示提醒到达时自动拉起的目标UIAbility信息
          pkgName: 'com.example.myapplication',
          abilityName: 'EntryAbility'
        },
        title: 'this is title', // 指明提醒标题
        content: 'this is content', // 指明提醒内容
        expiredContent: 'this reminder has expired', // 指明提醒过期后需要显示的内容
        notificationId: 100, // 指明提醒使用的通知的ID号，相同ID号的提醒会覆盖
        slotType: notificationManager.SlotType.SOCIAL_COMMUNICATION // 指明提醒的Slot类型
      }
      ```

   - 定义日历实例。
     
      ```js
      let targetReminderAgent: reminderAgentManager.ReminderRequestCalendar = {
        reminderType: reminderAgentManager.ReminderType.REMINDER_TYPE_CALENDAR, // 提醒类型为日历类型
        dateTime: {   // 指明提醒的目标时间
          year: 2023,
          month: 1,
          day: 1,
          hour: 11,
          minute: 14,
          second: 30
        },
        repeatMonths: [1], // 指明重复提醒的月份
        repeatDays: [1], // 指明重复提醒的日期
        actionButton: [ // 设置弹出的提醒通知信息上显示的按钮类型和标题
          {
            title: 'close',
            type: reminderAgentManager.ActionButtonType.ACTION_BUTTON_TYPE_CLOSE
          },
          {
            title: 'snooze',
            type: reminderAgentManager.ActionButtonType.ACTION_BUTTON_TYPE_SNOOZE
          },
        ],
        wantAgent: { // 点击提醒通知后跳转的目标UIAbility信息
          pkgName: 'com.example.myapplication',
          abilityName: 'EntryAbility'
        },
        maxScreenWantAgent: { // 全屏显示提醒到达时自动拉起的目标UIAbility信息
          pkgName: 'com.example.myapplication',
          abilityName: 'EntryAbility'
        },
        ringDuration: 5, // 指明响铃时长（单位：秒）
        snoozeTimes: 2, // 指明延迟提醒次数
        timeInterval: 5, // 执行延迟提醒间隔（单位：秒）
        title: 'this is title', // 指明提醒标题
        content: 'this is content', // 指明提醒内容
        expiredContent: 'this reminder has expired', // 指明提醒过期后需要显示的内容
        snoozeContent: 'remind later', // 指明延迟提醒时需要显示的内容
        notificationId: 100, // 指明提醒使用的通知的ID号，相同ID号的提醒会覆盖
        slotType: notificationManager.SlotType.SOCIAL_COMMUNICATION // 指明提醒的Slot类型
      }
      ```

   - 定义闹钟实例。
    
      ```js
      let targetReminderAgent: reminderAgentManager.ReminderRequestAlarm = {
        reminderType: reminderAgentManager.ReminderType.REMINDER_TYPE_ALARM, // 提醒类型为闹钟类型
        hour: 23, // 指明提醒的目标时刻
        minute: 9, // 指明提醒的目标分钟
        daysOfWeek: [2], // 指明每周哪几天需要重复提醒
        actionButton: [ // 设置弹出的提醒通知信息上显示的按钮类型和标题
          {
            title: 'close',
            type: reminderAgentManager.ActionButtonType.ACTION_BUTTON_TYPE_CLOSE
          },
          {
            title: 'snooze',
            type: reminderAgentManager.ActionButtonType.ACTION_BUTTON_TYPE_SNOOZE
          },
        ],
        wantAgent: { // 点击提醒通知后跳转的目标UIAbility信息
          pkgName: 'com.example.myapplication',
          abilityName: 'EntryAbility'
        },
        maxScreenWantAgent: { // 全屏显示提醒到达时自动拉起的目标UIAbility信息
          pkgName: 'com.example.myapplication',
          abilityName: 'EntryAbility'
        },
        ringDuration: 5, // 指明响铃时长（单位：秒）
        snoozeTimes: 2, // 指明延迟提醒次数
        timeInterval: 5, // 执行延迟提醒间隔（单位：秒）
        title: 'this is title', // 指明提醒标题
        content: 'this is content', // 指明提醒内容
        expiredContent: 'this reminder has expired', // 指明提醒过期后需要显示的内容
        snoozeContent: 'remind later', // 指明延迟提醒时需要显示的内容
        notificationId: 99, // 指明提醒使用的通知的ID号，相同ID号的提醒会覆盖
        slotType: notificationManager.SlotType.SOCIAL_COMMUNICATION // 指明提醒的Slot类型
      }
      ```

5. 发布相应的提醒代理。代理发布后，应用即可使用后台代理提醒功能。
   
   ```js
   try {
     reminderAgentManager.publishReminder(targetReminderAgent).then(res => {
       console.info('Succeeded in publishing reminder. ');
       let reminderId: number = res; // 发布的提醒ID
     }).catch(err => {
       console.error(`Failed to publish reminder. Code: ${err.code}, message: ${err.message}`);
     })
   } catch (err) {
       console.error(`Failed to publish reminder. Code: ${err.code}, message: ${err.message}`);
   }
   ```

6. 根据需要删除提醒任务。
   
   ```js
   try {
       // reminderId的值从发布提醒代理成功之后的回调中获得
       reminderAgentManager.cancelReminder(reminderId).then(() => {
           console.log('Succeeded in canceling reminder.');
       }).catch(err => {
           console.error(`Failed to cancel reminder. Code: ${err.code}, message: ${err.message}`);
       });
   } catch (err) {
       console.error(`Failed to cancel reminder. Code: ${err.code}, message: ${err.message}`);
   }
   ```

## 相关实例

基于代理提醒，有以下相关实例可供参考：

- [后台代理提醒（ArkTS）（API9）](https://gitee.com/openharmony/applications_app_samples/tree/OpenHarmony-3.2-Release/code/BasicFeature/TaskManagement/ReminderAgentManager)

- [翻页闹钟（ArkTS）（API9）](https://gitee.com/openharmony/applications_app_samples/tree/OpenHarmony-3.2-Release/code/Solutions/Tools/FlipClock)

- [闹钟（ArkTS）（API9）](https://gitee.com/openharmony/codelabs/tree/master/CommonEventAndNotification/AlarmClock)