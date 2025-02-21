# 应用权限组列表（仅对OpenHarmony开放）


## 使用须知

- 在申请目标权限前，建议开发者先阅读[应用权限管控概述-权限组和子权限](app-permission-mgmt-overview.md#权限组和子权限)，了解相关概念，再合理申请对应的权限组。

- 当应用请求权限时，同一个权限组的权限将会在一个弹窗内一起请求用户授权，用户同意授权后，权限组内权限将被统一授权。地理位置、通讯录、通话记录、电话、信息、日历权限组除外。

- 当前系统支持的权限组如下所示，各子权限的含义请查阅[应用权限列表](permissions-for-all.md)。


## 位置信息

- ohos.permission.LOCATION_IN_BACKGROUND

- ohos.permission.LOCATION

- ohos.permission.APPROXIMATELY_LOCATION


## 相机

- ohos.permission.CAMERA


## 麦克风

- ohos.permission.MICROPHONE


## 通讯录

- ohos.permission.READ_CONTACTS

- ohos.permission.WRITE_CONTACTS


## 日历

- ohos.permission.READ_CALENDAR

- ohos.permission.WRITE_CALENDAR

- ohos.permission.READ_WHOLE_CALENDAR

- ohos.permission.WRITE_WHOLE_CALENDAR


## 健身运动

- ohos.permission.ACTIVITY_MOTION


## 身体传感器

- ohos.permission.READ_HEALTH_DATA


## 图片和视频

- ohos.permission.WRITE_IMAGEVIDEO

- ohos.permission.READ_IMAGEVIDEO

- ohos.permission.MEDIA_LOCATION


## 音乐和音频

- ohos.permission.WRITE_AUDIO

- ohos.permission.READ_AUDIO


## 文件

- ohos.permission.READ_DOCUMENT

- ohos.permission.WRITE_DOCUMENT

- ohos.permission.READ_MEDIA

- ohos.permission.WRITE_MEDIA


## 广告跟踪

- ohos.permission.APP_TRACKING_CONSENT


## 读取已安装应用列表

- ohos.permission.GET_INSTALLED_BUNDLE_LIST


## 多设备协同

- ohos.permission.DISTRIBUTED_DATASYNC


## 蓝牙

- ohos.permission.ACCESS_BLUETOOTH


## 电话

- ohos.permission.ANSWER_CALL

- ohos.permission.MANAGE_VOICEMAIL


## 通话记录

- ohos.permission.READ_CALL_LOG

- ohos.permission.WRITE_CALL_LOG


## 信息

- ohos.permission.READ_CELL_MESSAGES

- ohos.permission.READ_MESSAGES

- ohos.permission.RECEIVE_MMS

- ohos.permission.RECEIVE_SMS

- ohos.permission.RECEIVE_WAP_MESSAGES

- ohos.permission.SEND_MESSAGES


## 剪切板

- ohos.permission.READ_PASTEBOARD 


## 文件夹

- ohos.permission.READ_WRITE_DOWNLOAD_DIRECTORY

- ohos.permission.READ_WRITE_DESKTOP_DIRECTORY

- ohos.permission.READ_WRITE_DOCUMENTS_DIRECTORY
