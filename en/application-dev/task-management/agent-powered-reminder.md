# Agent-powered Reminder

## Overview

### Introduction

After an application switches to the background or an application process is terminated, it may have scheduled tasks for reminding users, for example, flash sale reminders for shopping applications. To meet this requirement, the system provides agent-powered reminders (implemented by **reminderAgentManager**). When the application switches to the background or the process is terminated, the system sends reminders on behalf of the application. Currently, the following reminder types are supported: timer, calendar, and alarm.

- Timer: reminders based on countdown timers

- Calendar: reminders based on calendar events

- Alarm: reminders based on alarm clocks

### Constraints

- **Quantity limit**: A third-party application supports a maximum of 30 valid reminders. A system application supports a maximum of 10,000 valid reminders. The entire system supports a maximum of 12,000 valid reminders. (A reminder is considered valid as long as it is published.)

- **Redirection limit**: The application that is redirected to upon a click on the notification must be the application that requested the agent-powered reminder.


## Available APIs

The table below uses promise as an example to describe the APIs used for developing agent-powered reminders. For details about more APIs and their usage, see [reminderAgentManager](../reference/apis/js-apis-reminderAgentManager.md).

**Table 1** Main APIs for agent-powered reminders

| API| Description|
| -------- | -------- |
| publishReminder(reminderReq: ReminderRequest): Promise&lt;number&gt; | Publishes a reminder.|
| cancelReminder(reminderId: number): Promise&lt;void&gt; | Cancels a reminder.|
| getValidReminders(): Promise&lt;Array&lt;ReminderRequest&gt;&gt; | Obtains all valid reminders set by the current application.|
| cancelAllReminders(): Promise&lt;void&gt; | Cancels all reminders set by the current application.|
| addNotificationSlot(slot: NotificationSlot): Promise&lt;void&gt; | Adds a notification slot.|
| removeNotificationSlot(slotType: notification.SlotType): Promise&lt;void&gt; | Removes a notification slot.|


## How to Develop

1. Request the **ohos.permission.PUBLISH_AGENT_REMINDER** permission. For details, see [Declaring Permissions in the Configuration File](../security/accesstoken-guidelines.md#declaring-permissions-in-the-configuration-file).

2. [Enable the notification feature](../notification/notification-enable.md). Agent-powered reminders can be used only after being authorized by the user.

3. Import the modules.
   
   ```js
   import reminderAgentManager from '@ohos.reminderAgentManager';
   import notificationManager from '@ohos.notificationManager';
   ```

4. Define a reminder. You can define the following types of reminders based on project requirements.

   - Timer
     
      ```js
      let targetReminderAgent: reminderAgentManager.ReminderRequestTimer = {
        reminderType: reminderAgentManager.ReminderType.REMINDER_TYPE_TIMER,   // The reminder type is timer.
        triggerTimeInSeconds: 10,
        actionButton: [ // Set the button type and title displayed for the reminder in the notification panel.
          {
            title: 'close',
            type: reminderAgentManager.ActionButtonType.ACTION_BUTTON_TYPE_CLOSE
          }
        ],
        wantAgent: {     // Information about the target UIAbility that is displayed after the reminder notification is touched.
          pkgName: 'com.example.myapplication',
          abilityName: 'EntryAbility'
        },
        maxScreenWantAgent: { // Information about the target UIAbility that is automatically started when the specified reminder time arrives is displayed in full screen.
          pkgName: 'com.example.myapplication',
          abilityName: 'EntryAbility'
        },
        title: 'this is title', // Reminder title.
        content: 'this is content', // Reminder content.
        expiredContent: 'this reminder has expired', // Content to be displayed after the reminder expires.
        notificationId: 100, // Notification ID used by the reminder. If there are reminders with the same notification ID, the later one will overwrite the earlier one.
        slotType: notificationManager.SlotType.SOCIAL_COMMUNICATION // Type of the slot used by the reminder.
      }
      ```

   - Calendar
     
      ```js
      let targetReminderAgent: reminderAgentManager.ReminderRequestCalendar = {
        reminderType: reminderAgentManager.ReminderType.REMINDER_TYPE_CALENDAR, // The reminder type is calendar.
        dateTime: {   // Reminder time.
          year: 2023,
          month: 1,
          day: 1,
          hour: 11,
          minute: 14,
          second: 30
        },
        repeatMonths: [1], // Month in which the reminder repeats.
        repeatDays: [1], // Date on which the reminder repeats.
        actionButton: [ // Set the button type and title displayed for the reminder in the notification panel.
          {
            title: 'close',
            type: reminderAgentManager.ActionButtonType.ACTION_BUTTON_TYPE_CLOSE
          },
          {
            title: 'snooze',
            type: reminderAgentManager.ActionButtonType.ACTION_BUTTON_TYPE_SNOOZE
          },
        ],
        wantAgent: { // Information about the target UIAbility that is displayed after the reminder notification is touched.
          pkgName: 'com.example.myapplication',
          abilityName: 'EntryAbility'
        },
        maxScreenWantAgent: { // Information about the target UIAbility that is automatically started when the specified reminder time arrives is displayed in full screen.
          pkgName: 'com.example.myapplication',
          abilityName: 'EntryAbility'
        },
        ringDuration: 5, // Ringing duration, in seconds.
        snoozeTimes: 2, // Number of reminder snooze times.
        timeInterval: 5, // Reminder snooze interval, in seconds.
        title: 'this is title', // Reminder title.
        content: 'this is content', // Reminder content.
        expiredContent: 'this reminder has expired', // Content to be displayed after the reminder expires.
        snoozeContent: 'remind later', // Content to be displayed when the reminder is snoozed.
        notificationId: 100, // Notification ID used by the reminder. If there are reminders with the same notification ID, the later one will overwrite the earlier one.
        slotType: notificationManager.SlotType.SOCIAL_COMMUNICATION // Type of the slot used by the reminder.
      }
      ```

   - Alarm
   
      ```js
      let targetReminderAgent: reminderAgentManager.ReminderRequestAlarm = {
        reminderType: reminderAgentManager.ReminderType.REMINDER_TYPE_ALARM, // The reminder type is alarm.
        hour: 23, // Hour portion of the reminder time.
        minute: 9, // Minute portion of the reminder time.
        daysOfWeek: [2], // Days of a week when the reminder repeats..
        actionButton: [ // Set the button type and title displayed for the reminder in the notification panel.
          {
            title: 'close',
            type: reminderAgentManager.ActionButtonType.ACTION_BUTTON_TYPE_CLOSE
          },
          {
            title: 'snooze',
            type: reminderAgentManager.ActionButtonType.ACTION_BUTTON_TYPE_SNOOZE
          },
        ],
        wantAgent: { // Information about the target UIAbility that is displayed after the reminder notification is touched.
          pkgName: 'com.example.myapplication',
          abilityName: 'EntryAbility'
        },
        maxScreenWantAgent: { // Information about the target UIAbility that is automatically started when the specified reminder time arrives is displayed in full screen.
          pkgName: 'com.example.myapplication',
          abilityName: 'EntryAbility'
        },
        ringDuration: 5, // Ringing duration, in seconds.
        snoozeTimes: 2, // Number of reminder snooze times.
        timeInterval: 5, // Reminder snooze interval, in seconds.
        title: 'this is title', // Reminder title.
        content: 'this is content', // Reminder content.
        expiredContent: 'this reminder has expired', // Content to be displayed after the reminder expires.
        snoozeContent: 'remind later', // Content to be displayed when the reminder is snoozed.
        notificationId: 99, // Notification ID used by the reminder. If there are reminders with the same notification ID, the later one will overwrite the earlier one.
        slotType: notificationManager.SlotType.SOCIAL_COMMUNICATION // Type of the slot used by the reminder.
      }
      ```

5. Publish the reminder. After the reminder is published, your application can use the agent-powered reminder feature.
   
   ```js
   try {
     reminderAgentManager.publishReminder(targetReminderAgent).then(res => {
       console.info('Succeeded in publishing reminder. ');
       let reminderId: number = res; // ID of the published reminder.
     }).catch(err => {
       console.error(`Failed to publish reminder. Code: ${err.code}, message: ${err.message}`);
     })
   } catch (err) {
       console.error(`Failed to publish reminder. Code: ${err.code}, message: ${err.message}`);
   }
   ```

6. Delete the reminder as required.
   
   ```js
   try {
       // The reminder ID is obtained from the callback after the reminder is published.
       reminderAgentManager.cancelReminder(reminderId).then(() => {
           console.log('Succeeded in canceling reminder.');
       }).catch(err => {
           console.error(`Failed to cancel reminder. Code: ${err.code}, message: ${err.message}`);
       });
   } catch (err) {
       console.error(`Failed to cancel reminder. Code: ${err.code}, message: ${err.message}`);
   }
   ```

