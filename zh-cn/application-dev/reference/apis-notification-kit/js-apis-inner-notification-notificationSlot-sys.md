# NotificationSlot(系统接口)

描述通知槽。

> **说明：**
>
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>
> 当前界面仅包含本模块的系统接口，其他公开接口参见[NotificationSlot](./js-apis-inner-notification-notificationSlot.md)。

## NotificationSlot

**系统能力：** 以下各项对应的系统能力均为SystemCapability.Notification.Notification

| 名称                 | 类型                  | 必填 | 说明                   |
| -------------------- | --------------------- | --- |----------------------|
| reminderMode<sup>11+</sup> | number                | 否  | 获取当前通知条目的通知提醒模式。<br>**系统接口**：此接口为系统接口。 <br>- bit0：铃声提示。0表示关闭，1表示开启。 <br>- bit1：锁屏。0表示关闭，1表示开启。 <br>- bit2：横幅。0表示关闭，1表示开启。 <br>- bit3：亮屏。0表示关闭，1表示开启。 <br>- bit4：振动。0表示关闭，1表示开启。    |
