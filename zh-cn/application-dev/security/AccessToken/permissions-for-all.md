# 开放权限（系统授权）

此列表内所有权限均为系统授权（system_grant）的开放权限，面向所有应用开放。

应用申请了system_grant权限后，系统将在用户安装应用时，自动把相应权限授予给应用。

<!--Del-->
> **说明：**
> 权限级别为normal的权限，不涉及ACL使能字段。
<!--DelEnd-->

## 申请方式

以下权限的授权方式均为[system_grant](app-permission-mgmt-overview.md#system_grant系统授权)，申请方式请参考[声明权限](declare-permissions.md)。

## ohos.permission.USE_BLUETOOTH

允许应用查看蓝牙的配置。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：8

## ohos.permission.GET_BUNDLE_INFO

允许查询应用的基本信息。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：7

## ohos.permission.PREPARE_APP_TERMINATE

允许应用关闭前执行自定义的预关闭动作。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：10

## ohos.permission.PRINT

允许应用获取打印框架的能力。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：10

## ohos.permission.DISCOVER_BLUETOOTH

允许应用配置本地蓝牙，查找远端设备且与之配对连接。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：8

## ohos.permission.ACCELEROMETER

允许应用读取加速度传感器的数据。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：7

## ohos.permission.ACCESS_BIOMETRIC

允许应用使用生物特征识别能力进行身份认证。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：6

## ohos.permission.ACCESS_NOTIFICATION_POLICY

在本设备上允许应用访问通知策略。

仅当控制铃声从静音到非静音时，需要申请该权限。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：7

## ohos.permission.GET_NETWORK_INFO

允许应用获取数据网络信息。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：8

## ohos.permission.GET_WIFI_INFO

允许应用获取Wi-Fi信息。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：8

## ohos.permission.GYROSCOPE

允许应用读取陀螺仪传感器的数据。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：7

## ohos.permission.INTERNET

允许使用Internet网络。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：9

## ohos.permission.KEEP_BACKGROUND_RUNNING

允许Service Ability在后台持续运行。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：8

## ohos.permission.NFC_CARD_EMULATION

允许应用实现卡模拟功能。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：8

## ohos.permission.NFC_TAG

允许应用读写Tag卡片。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：7

## ohos.permission.PRIVACY_WINDOW

允许应用将窗口设置为隐私窗口，禁止截屏录屏。

**权限级别**：API version 9-10为system_basic；从API version 11开始为normal。

**授权方式**：system_grant

**起始版本**：9

## ohos.permission.PUBLISH_AGENT_REMINDER

允许该应用使用后台代理提醒。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：7

## ohos.permission.SET_WIFI_INFO

允许应用配置Wi-Fi设备。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：8

## ohos.permission.VIBRATE

允许应用控制马达振动。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：7

## ohos.permission.CLEAN_BACKGROUND_PROCESSES

允许应用根据包名清理相关后台进程。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：7

## ohos.permission.COMMONEVENT_STICKY

允许应用发布粘性公共事件。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：7

## ohos.permission.MODIFY_AUDIO_SETTINGS

允许应用修改音频设置。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：8

## ohos.permission.RUNNING_LOCK

允许应用获取运行锁，保证应用在后台的持续运行。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：7

## ohos.permission.SET_WALLPAPER

允许应用设置壁纸。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：7

## ohos.permission.ACCESS_CERT_MANAGER

允许应用进行查询证书及私有凭据等操作。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：9

## ohos.permission.hsdr.HSDR_ACCESS

允许应用访问安全检测与响应框架。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：10

## ohos.permission.RUN_DYN_CODE

允许系统方舟运行时引擎在受限模式下执行动态下发的方舟字节码。

该权限相关的API均为系统API，仅部分特定系统应用可申请该权限。 

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：11

## ohos.permission.READ_CLOUD_SYNC_CONFIG

允许接入云空间的应用查询应用云同步相关配置信息。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：11

## ohos.permission.STORE_PERSISTENT_DATA

允许应用存储持久化的数据，该数据直到设备恢复出厂设置或重装系统才会被清除。

**权限级别**: normal

**授权方式**：system_grant

**起始版本**: 11

## ohos.permission.ACCESS_EXTENSIONAL_DEVICE_DRIVER

允许应用使用外接设备增强功能。

**权限级别**: normal

**授权方式**：system_grant

**起始版本**：11

## ohos.permission.READ_ACCOUNT_LOGIN_STATE

允许应用读取用户账号的登录状态。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：12

## ohos.permission.ACCESS_SERVICE_NAVIGATION_INFO

允许应用访问导航信息服务。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：12

## ohos.permission.PROTECT_SCREEN_LOCK_DATA

允许应用在锁屏后保护本应用敏感数据不被访问。

应用获取此权限后，系统将给用户新建一个高安全级别el5的目录。应用可以在此目录下存放数据，这部分数据在锁屏后无法被访问。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：12

## ohos.permission.FILE_ACCESS_PERSIST

允许应用支持持久化访问文件Uri。

<!--RP2--><!--RP2End-->

**权限级别**：API version 11为system_basic; 从API version 12开始为normal。

**授权方式**：system_grant

**起始版本**：11

## ohos.permission.ACCESS_CAR_DISTRIBUTED_ENGINE

允许应用访问出行分布式业务引擎。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：12

## ohos.permission.WINDOW_TOPMOST

允许应用将窗口设置为应用置顶窗口。

**权限级别**：normal

**授权方式**：system_grant

**起始版本**：13

## ohos.permission.kernel.ALLOW_EXECUTABLE_FORT_MEMORY

允许系统JS引擎申请带MAP_FORT标识的匿名可执行内存。

应用申请此权限后，系统引擎可申请带MAP_FORT的匿名可执行内存，做即时编译，提高与形式执行效率。

**权限级别**：system_basic

**授权方式**：system_grant

**起始版本**：14


