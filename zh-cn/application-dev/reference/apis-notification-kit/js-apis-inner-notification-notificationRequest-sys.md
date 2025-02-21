# NotificationRequest(系统接口)

描述通知的请求。

> **说明：**
>
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
>
> 当前界面仅包含本模块的系统接口，其他公开接口参见[NotificationRequest](./js-apis-inner-notification-notificationRequest.md)。

## NotificationRequest

**系统能力**：以下各项对应的系统能力均为SystemCapability.Notification.Notification

| 名称                            | 类型                                                    |  只读 | 必填 | 说明                                                                    |
|-------------------------------| -------------------------------------------------------- | ----- | --- |-----------------------------------------------------------------------|
| overlayIcon<sup>11+<sup>      | [image.PixelMap](../apis-image-kit/js-apis-image.md#pixelmap7)             |   否  | 否  | 通知重叠图标。可选字段，图像像素的总字节数不超过100KB。<br>**系统接口**: 此接口为系统接口。                                                 |
| classification                | string                                                   |   否  | 否  | 通知分类。<br>**系统接口**: 此接口为系统接口。                               |
| isRemoveAllowed<sup>8+<sup>   | boolean                                                  |   否  | 否  | 通知是否能被移除（点击通知下方删除按钮无法删除，左滑不出现删除按钮）。<br>**系统接口**: 此接口为系统接口。<br>**需要权限**: ohos.permission.SET_UNREMOVABLE_NOTIFICATION |
| source<sup>8+<sup>            | number                                                   |   是  | 否  | 通知源。<br>**系统接口**: 此接口为系统接口。                                |
| deviceId<sup>8+<sup>          | string                                                   |   是  | 否  | 通知源的deviceId。<br>**系统接口**: 此接口为系统接口。                       |

## DistributedOptions

描述分布式选项。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Notification.Notification

| 名称                   | 类型            | 必填 | 说明                               |
| ---------------------- | -------------- | ---- | ---------------------------------- |
| remindType<sup>8+<sup>             | number         | 否   | 通知的提醒方式。<br>**系统接口**: 此接口为系统接口。  |


## NotificationFilter<sup>11+</sup>

描述查询普通实况窗时的筛选条件。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Notification.Notification

**系统接口**: 此接口为系统接口。  

| 名称            | 类型                                   | 必填 | 说明                               |
| ----------------| ------------------------------------- | ---- | ---------------------------------- |
| bundle          | [BundleOption](js-apis-inner-notification-notificationCommonDef.md#bundleoption) | 是   | 实况通知的包信息。|
| notificationKey | [NotificationKey](js-apis-notificationSubscribe-sys.md#notificationkey) | 是   | 通知信息，包含通知ID和通知标签。   |
| extraInfoKeys   | Array\<string>                        | 否   | 筛选附加信息的键值列表。不填表示查询所有的附加信息。|


## NotificationCheckRequest<sup>11+</sup>

描述通知的鉴权信息。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Notification.Notification

**系统接口**: 此接口为系统接口。  

| 名称          | 类型                                                       | 必填 | 说明              |
| --------------| --------------------------------------------------------- | ---- | ----------------- |
| contentType   | [ContentType](js-apis-notificationManager.md#contenttype) | 是   | 通知类型。         |
| slotType      | [SlotType](js-apis-notificationManager.md#slottype)       | 是   | 渠道类型。         |
| extraInfoKeys | Array\<string>                                            | 是   | 实况通知的附加信息。|
