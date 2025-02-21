# 系统公共事件定义

本文档提供OpenHarmony系统所定义的公共事件类型的索引。
公共事件类型定义在[ohos.commonEvent模块的Support枚举](./js-apis-commonEvent.md#support)中。

**系统能力：** SystemCapability.Notification.CommonEvent

## COMMON_EVENT_BOOT_COMPLETED
提示用户已完成引导并加载系统。
- 值：usual.event.BOOT_COMPLETED
- 订阅者所需权限：ohos.permission.RECEIVER_STARTUP_COMPLETED

## COMMON_EVENT_LOCKED_BOOT_COMPLETED
（预留事件，暂未支持）提示用户已完成引导，系统已加载，但屏幕仍锁定。
- 值：usual.event.LOCKED_BOOT_COMPLETED
- 订阅者所需权限：ohos.permission.RECEIVER_STARTUP_COMPLETED

## COMMON_EVENT_SHUTDOWN
提示设备正在关闭并将继续直至最终关闭。
- 值：usual.event.SHUTDOWN
- 订阅者所需权限：无

## COMMON_EVENT_BATTERY_CHANGED
提示电池充电状态、电量和其他信息发生变化。
- 值：usual.event.BATTERY_CHANGED
- 订阅者所需权限：无

## COMMON_EVENT_BATTERY_LOW
提示电池电量低。
- 值：usual.event.BATTERY_LOW
- 订阅者所需权限：无

## COMMON_EVENT_BATTERY_OKAY
提示电池退出低电量状态。
- 值：usual.event.BATTERY_OKAY
- 订阅者所需权限：无

## COMMON_EVENT_POWER_CONNECTED
提示设备连接到外部电源。
- 值：usual.event.POWER_CONNECTED
- 订阅者所需权限：无


## COMMON_EVENT_POWER_DISCONNECTED
提示设备与外部电源断开。
- 值：usual.event.POWER_DISCONNECTED
- 订阅者所需权限：无


## COMMON_EVENT_SCREEN_OFF
提示设备屏幕关闭且设备处于睡眠状态。
- 值：usual.event.SCREEN_OFF
- 订阅者所需权限：无


## COMMON_EVENT_SCREEN_ON
提示设备屏幕打开且设备处于交互状态。
- 值：usual.event.SCREEN_ON
- 订阅者所需权限：无


## COMMON_EVENT_THERMAL_LEVEL_CHANGED<sup>8+<sup>
提示设备热状态（温度等级）发生变化。
- 值：usual.event.THERMAL_LEVEL_CHANGED
- 订阅者所需权限：无


## COMMON_EVENT_USER_PRESENT
（预留事件，暂未支持）提示用户解锁了设备。
- 值：usual.event.USER_PRESENT
- 订阅者所需权限：无


## COMMON_EVENT_TIME_TICK
提示系统时间发生更改（指时间正常流逝）。
- 值：usual.event.TIME_TICK
- 订阅者所需权限：无


## COMMON_EVENT_TIME_CHANGED
提示系统时间被被重新设置。
- 值：usual.event.TIME_CHANGED
- 订阅者所需权限：无


## COMMON_EVENT_DATE_CHANGED
（预留事件，暂未支持）提示系统日期已更改。
- 值：usual.event.DATE_CHANGED
- 订阅者所需权限：无


## COMMON_EVENT_TIMEZONE_CHANGED
提示系统时区发生变更。
- 值：usual.event.TIMEZONE_CHANGED
- 订阅者所需权限：无


## COMMON_EVENT_CLOSE_SYSTEM_DIALOGS
（预留事件，暂未支持）提示用户关闭临时系统对话框。
- 值：usual.event.CLOSE_SYSTEM_DIALOGS
- 订阅者所需权限：无


## COMMON_EVENT_PACKAGE_ADDED
提示设备上已安装新应用程序包。
- 值：usual.event.PACKAGE_ADDED
- 订阅者所需权限：无


## COMMON_EVENT_PACKAGE_REPLACED
（预留事件，暂未支持）提示设备上已安装的旧版本应用程序已被新版本所替换。
- 值：usual.event.PACKAGE_REPLACED
- 订阅者所需权限：无


## COMMON_EVENT_MY_PACKAGE_REPLACED
（预留事件，暂未支持）提示应用程序包的新版本已取代前一个版本。
- 值：usual.event.MY_PACKAGE_REPLACED
- 订阅者所需权限：无

## COMMON_EVENT_PACKAGE_REMOVED
提示已安装的应用程序已从设备卸载，但应用程序数据得到保留的。
- 值：usual.event.PACKAGE_REMOVED
- 订阅者所需权限：无


## COMMON_EVENT_BUNDLE_REMOVED
（预留事件，暂未支持）提示已从设备中卸载已安装应用程序的附加包，但应用程序数据得到保留。
- 值：usual.event.BUNDLE_REMOVED
- 订阅者所需权限：无


## COMMON_EVENT_PACKAGE_FULLY_REMOVED
（预留事件，暂未支持）提示已从设备中完全卸载已安装的应用程序（包括应用程序数据和代码）。
- 值：usual.event.PACKAGE_FULLY_REMOVED
- 订阅者所需权限：无


## COMMON_EVENT_PACKAGE_CHANGED
提示应用程序包已发生更改（例如，包中的组件已启用或禁用）。
- 值：usual.event.PACKAGE_CHANGED
- 订阅者所需权限：无


## COMMON_EVENT_PACKAGE_RESTARTED
提示用户终止了应用程序的所有进程并重启应用程序。
- 值：usual.event.PACKAGE_RESTARTED
- 订阅者所需权限：无


## COMMON_EVENT_PACKAGE_DATA_CLEARED
提示用户清除了应用包数据。
- 值：usual.event.PACKAGE_DATA_CLEARED
- 订阅者所需权限：无


## COMMON_EVENT_PACKAGES_SUSPENDED
（预留事件，暂未支持）提示应用程序已挂起。
- 值：usual.event.PACKAGES_SUSPENDED
- 订阅者所需权限：无


## COMMON_EVENT_PACKAGES_UNSUSPENDED
（预留事件，暂未支持）提示应用HAP包未挂起（从挂起状态恢复）。
- 值：usual.event.PACKAGES_UNSUSPENDED
- 订阅者所需权限：无


## COMMON_EVENT_MY_PACKAGE_SUSPENDED
提示应用HAP包被挂起的。
- 值：usual.event.MY_PACKAGE_SUSPENDED
- 订阅者所需权限：无


## COMMON_EVENT_MY_PACKAGE_UNSUSPENDED
提示应用包未挂起。
- 值：usual.event.MY_PACKAGE_UNSUSPENDED
- 订阅者所需权限：无


## COMMON_EVENT_UID_REMOVED
（预留事件，暂未支持）提示用户ID已从系统中删除。
- 值：usual.event.UID_REMOVED
- 订阅者所需权限：无


## COMMON_EVENT_PACKAGE_FIRST_LAUNCH
（预留事件，暂未支持）提示首次启动已安装的应用程序。
- 值：usual.event.PACKAGE_FIRST_LAUNCH
- 订阅者所需权限：无


## COMMON_EVENT_PACKAGE_NEEDS_VERIFICATION
（预留事件，暂未支持）提示应用需要系统校验。
- 值：usual.event.PACKAGE_NEEDS_VERIFICATION
- 订阅者所需权限：无


## COMMON_EVENT_PACKAGE_VERIFIED
（预留事件，暂未支持）提示应用已被系统校验。
- 值：usual.event.PACKAGE_VERIFIED
- 订阅者所需权限：无


## COMMON_EVENT_EXTERNAL_APPLICATIONS_AVAILABLE
（预留事件，暂未支持）提示安装在外部存储上的应用程序对系统可用。
- 值：usual.event.EXTERNAL_APPLICATIONS_AVAILABLE
- 订阅者所需权限：无


## COMMON_EVENT_EXTERNAL_APPLICATIONS_UNAVAILABLE
（预留事件，暂未支持）提示安装在外部存储上的应用程序对系统不可用。
- 值：usual.event.EXTERNAL_APPLICATIONS_UNAVAILABLE
- 订阅者所需权限：无


## COMMON_EVENT_CONFIGURATION_CHANGED
（预留事件，暂未支持）提示设备状态（例如，方向、区域设置等）已更改。
- 值：usual.event.CONFIGURATION_CHANGED
- 订阅者所需权限：无


## COMMON_EVENT_LOCALE_CHANGED
（预留事件，暂未支持）提示设备区域设置已更改。
- 值：usual.event.LOCALE_CHANGED
- 订阅者所需权限：无


## COMMON_EVENT_MANAGE_PACKAGE_STORAGE
（预留事件，暂未支持）提示设备存储空间不足。
- 值：usual.event.MANAGE_PACKAGE_STORAGE
- 订阅者所需权限：无


## COMMON_EVENT_DRIVE_MODE
（预留事件，暂未支持）提示系统处于驾驶模式。
- 值：common.event.DRIVE_MODE
- 订阅者所需权限：无


## COMMON_EVENT_HOME_MODE
（预留事件，暂未支持）提示系统处于HOME模式。
- 值：common.event.HOME_MODE
- 订阅者所需权限：无


## COMMON_EVENT_OFFICE_MODE
（预留事件，暂未支持）提示系统处于办公模式。
- 值：common.event.OFFICE_MODE
- 订阅者所需权限：无


## COMMON_EVENT_USER_STARTED
（预留事件，暂未支持）提示用户已启动。
- 值：usual.event.USER_STARTED
- 订阅者所需权限：无


## COMMON_EVENT_USER_BACKGROUND
（预留事件，暂未支持）提示用户已被带到后台。
- 值：usual.event.USER_BACKGROUND
- 订阅者所需权限：无


## COMMON_EVENT_USER_FOREGROUND
（预留事件，暂未支持）提示用户已被带到前台。
- 值：usual.event.USER_FOREGROUND
- 订阅者所需权限：无


## COMMON_EVENT_USER_SWITCHED
提示用户正在切换。
- 值：usual.event.USER_SWITCHED
- 订阅者所需权限：- 订阅者所需权限：ohos.permission.MANAGE_LOCAL_ACCOUNTS


## COMMON_EVENT_USER_STARTING
（预留事件，暂未支持）提示用户正在启动。
- 值：usual.event.USER_STARTING
- 订阅者所需权限：ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS


## COMMON_EVENT_USER_UNLOCKED
（预留事件，暂未支持）在重启后解锁时，提示当前用户的凭据加密存储已解锁。
- 值：usual.event.USER_UNLOCKED
- 订阅者所需权限：无


## COMMON_EVENT_USER_STOPPING
（预留事件，暂未支持）提示要停止用户。
- 值：usual.event.USER_STOPPING
- 订阅者所需权限：ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS


## COMMON_EVENT_USER_STOPPED
（预留事件，暂未支持）提示用户已停止。
- 值：usual.event.USER_STOPPED
- 订阅者所需权限：无


## COMMON_EVENT_WIFI_POWER_STATE
提示Wi-Fi功能状态的变更，如启用或禁用。
- 值：usual.event.wifi.POWER_STATE
- 订阅者所需权限：无


## COMMON_EVENT_WIFI_SCAN_FINISHED
提示Wi-Fi接入点已被扫描并证明可用。
- 值：usual.event.wifi.SCAN_FINISHED
- 订阅者所需权限：ohos.permission.LOCATION


## COMMON_EVENT_WIFI_RSSI_VALUE
提示Wi-Fi信号强度（RSSI）改变。
- 值：usual.event.wifi.RSSI_VALUE
- 订阅者所需权限：ohos.permission.GET_WIFI_INFO


## COMMON_EVENT_WIFI_CONN_STATE
提示Wi-Fi连接状态发生改变。
- 值：usual.event.wifi.CONN_STATE
- 订阅者所需权限：无


## COMMON_EVENT_WIFI_HOTSPOT_STATE
提示Wi-Fi热点功能状态的变更，如启用或禁用。
- 值：usual.event.wifi.HOTSPOT_STATE
- 订阅者所需权限：无


## COMMON_EVENT_WIFI_AP_STA_JOIN
提示有客户端加入当前设备Wi-Fi热点。
- 值：usual.event.wifi.WIFI_HS_STA_JOIN
- 订阅者所需权限：ohos.permission.GET_WIFI_INFO


## COMMON_EVENT_WIFI_AP_STA_LEAVE
提示客户端已断开与当前设备Wi-Fi热点的连接。
- 值：usual.event.wifi.WIFI_HS_STA_LEAVE
- 订阅者所需权限：ohos.permission.GET_WIFI_INFO


## COMMON_EVENT_WIFI_MPLINK_STATE_CHANGE
提示MPLink（增强Wi-Fi功能）状态已更改。
- 值：usual.event.wifi.mplink.STATE_CHANGE
- 订阅者所需权限：ohos.permission.MPLINK_CHANGE_STATE


## COMMON_EVENT_WIFI_P2P_CONN_STATE
提示Wi-Fi P2P连接状态改变。
- 值：usual.event.wifi.p2p.CONN_STATE_CHANGE
- 订阅者所需权限：ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION


## COMMON_EVENT_WIFI_P2P_STATE_CHANGED
提示Wi-Fi P2P状态发生变更，如启用和禁用。
- 值：usual.event.wifi.p2p.STATE_CHANGE
- 订阅者所需权限：ohos.permission.GET_WIFI_INFO


## COMMON_EVENT_WIFI_P2P_PEERS_STATE_CHANGED
提示Wi-Fi P2P对等体状态变化。
- 值：usual.event.wifi.p2p.DEVICES_CHANGE
- 订阅者所需权限：ohos.permission.GET_WIFI_INFO


## COMMON_EVENT_WIFI_P2P_PEERS_DISCOVERY_STATE_CHANGED
提示Wi-Fi P2P发现状态变化。
- 值：usual.event.wifi.p2p.PEER_DISCOVERY_STATE_CHANGE
- 订阅者所需权限：ohos.permission.GET_WIFI_INFO


## COMMON_EVENT_WIFI_P2P_CURRENT_DEVICE_STATE_CHANGED
提示Wi-Fi P2P当前设备状态变化。
- 值：usual.event.wifi.p2p.CURRENT_DEVICE_CHANGE
- 订阅者所需权限：ohos.permission.GET_WIFI_INFO


## COMMON_EVENT_WIFI_P2P_GROUP_STATE_CHANGED
提示Wi-Fi P2P群组信息已更改。
- 值：usual.event.wifi.p2p.GROUP_STATE_CHANGED
- 订阅者所需权限：ohos.permission.GET_WIFI_INFO


## COMMON_EVENT_BLUETOOTH_HANDSFREE_AG_CONNECT_STATE_UPDATE
（预留事件，暂未支持）提示蓝牙免提通信连接状态。
- 值：usual.event.bluetooth.handsfree.ag.CONNECT_STATE_UPDATE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_HANDSFREE_AG_CURRENT_DEVICE_UPDATE
（预留事件，暂未支持）提示连接到具有蓝牙免提功能的设备处于活动状态。
- 值：usual.event.bluetooth.handsfree.ag.CURRENT_DEVICE_UPDATE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_HANDSFREE_AG_AUDIO_STATE_UPDATE
（预留事件，暂未支持）提示蓝牙A2DP连接状态已更改。
- 值：usual.event.bluetooth.handsfree.ag.AUDIO_STATE_UPDATE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_A2DPSOURCE_CONNECT_STATE_UPDATE
（预留事件，暂未支持）提示蓝牙A2DP连接状态。
- 值：usual.event.bluetooth.a2dpsource.CONNECT_STATE_UPDATE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_A2DPSOURCE_CURRENT_DEVICE_UPDATE
（预留事件，暂未支持）提示使用蓝牙A2DP连接的设备处于活动状态。
- 值：usual.event.bluetooth.a2dpsource.CURRENT_DEVICE_UPDATE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_A2DPSOURCE_PLAYING_STATE_UPDATE
（预留事件，暂未支持）提示蓝牙A2DP播放状态发生改变。
- 值：usual.event.bluetooth.a2dpsource.PLAYING_STATE_UPDATE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_A2DPSOURCE_AVRCP_CONNECT_STATE_UPDATE
（预留事件，暂未支持）提示蓝牙A2DP的AVRCP连接状态已更改。
- 值：usual.event.bluetooth.a2dpsource.AVRCP_CONNECT_STATE_UPDATE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_A2DPSOURCE_CODEC_VALUE_UPDATE
（预留事件，暂未支持）提示蓝牙A2DP音频编解码状态更改。
- 值：usual.event.bluetooth.a2dpsource.CODEC_VALUE_UPDATE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_DISCOVERED
（预留事件，暂未支持）提示发现远程蓝牙设备。
- 值：usual.event.bluetooth.remotedevice.DISCOVERED
- 订阅者所需权限：ohos.permission.LOCATION and ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CLASS_VALUE_UPDATE
（预留事件，暂未支持）提示远程蓝牙设备的蓝牙类别已更改。
- 值：usual.event.bluetooth.remotedevice.CLASS_VALUE_UPDATE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_ACL_CONNECTED
（预留事件，暂未支持）提示已与远程蓝牙设备建立低级别（ACL）连接。
- 值：usual.event.bluetooth.remotedevice.ACL_CONNECTED
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_ACL_DISCONNECTED
（预留事件，暂未支持）提示低级别（ACL）连接已从远程蓝牙设备断开。
- 值：usual.event.bluetooth.remotedevice.ACL_DISCONNECTED
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_NAME_UPDATE
（预留事件，暂未支持）提示远程蓝牙设备的友好名称首次被检索或自上次检索以来被更改。
- 值：usual.event.bluetooth.remotedevice.NAME_UPDATE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_PAIR_STATE
（预留事件，暂未支持）提示远程蓝牙设备连接状态更改。
- 值：usual.event.bluetooth.remotedevice.PAIR_STATE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_BATTERY_VALUE_UPDATE
（预留事件，暂未支持）提示远程蓝牙设备的电池电量首次被检索或自上次检索以来被更改。
- 值：usual.event.bluetooth.remotedevice.BATTERY_VALUE_UPDATE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_SDP_RESULT
（预留事件，暂未支持）提示远程蓝牙设备SDP状态。
- 值：usual.event.bluetooth.remotedevice.SDP_RESULT
- 订阅者所需权限：无


## COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_UUID_VALUE
（预留事件，暂未支持）提示远程蓝牙设备UUID连接状态。
- 值：usual.event.bluetooth.remotedevice.UUID_VALUE
- 订阅者所需权限：ohos.permission.DISCOVER_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_PAIRING_REQ
（预留事件，暂未支持）提示远程蓝牙设备配对请求。
- 值：usual.event.bluetooth.remotedevice.PAIRING_REQ
- 订阅者所需权限：ohos.permission.DISCOVER_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_PAIRING_CANCEL
（预留事件，暂未支持）提示取消蓝牙配对。
- 值：usual.event.bluetooth.remotedevice.PAIRING_CANCEL
- 订阅者所需权限：无


## COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CONNECT_REQ
（预留事件，暂未支持）提示远程蓝牙设备连接请求。
- 值：usual.event.bluetooth.remotedevice.CONNECT_REQ
- 订阅者所需权限：无


## COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CONNECT_REPLY
（预留事件，暂未支持）提示远程蓝牙设备连接请求响应。
- 值：usual.event.bluetooth.remotedevice.CONNECT_REPLY
- 订阅者所需权限：无


## COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CONNECT_CANCEL
（预留事件，暂未支持）提示取消与远程蓝牙设备的连接。
- 值：usual.event.bluetooth.remotedevice.CONNECT_CANCEL
- 订阅者所需权限：无


## COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_CONNECT_STATE_UPDATE
（预留事件，暂未支持）提示蓝牙免提连接状态已更改。
- 值：usual.event.bluetooth.handsfreeunit.CONNECT_STATE_UPDATE
- 订阅者所需权限：无


## COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_AUDIO_STATE_UPDATE
（预留事件，暂未支持）提示蓝牙免提音频状态已更改。
- 值：usual.event.bluetooth.handsfreeunit.AUDIO_STATE_UPDATE
- 订阅者所需权限：无


## COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_AG_COMMON_EVENT
（预留事件，暂未支持）提示蓝牙免提音频网关状态已更改。
- 值：usual.event.bluetooth.handsfreeunit.AG_COMMON_EVENT
- 订阅者所需权限：无


## COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_AG_CALL_STATE_UPDATE
（预留事件，暂未支持）提示蓝牙免提呼叫状态已更改。
- 值：usual.event.bluetooth.handsfreeunit.AG_CALL_STATE_UPDATE
- 订阅者所需权限：无


## COMMON_EVENT_BLUETOOTH_HOST_STATE_UPDATE
（预留事件，暂未支持）提示蓝牙适配器状态已更改，例如蓝牙已打开或关闭。
- 值：usual.event.bluetooth.host.STATE_UPDATE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_HOST_REQ_DISCOVERABLE
（预留事件，暂未支持）提示用户允许扫描蓝牙请求。
- 值：usual.event.bluetooth.host.REQ_DISCOVERABLE
- 订阅者所需权限：无


## COMMON_EVENT_BLUETOOTH_HOST_REQ_ENABLE
（预留事件，暂未支持）提示用户打开蓝牙请求。
- 值：usual.event.bluetooth.host.REQ_ENABLE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_HOST_REQ_DISABLE
（预留事件，暂未支持）提示用户关闭蓝牙请求。
- 值：usual.event.bluetooth.host.REQ_DISABLE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_HOST_SCAN_MODE_UPDATE
（预留事件，暂未支持）提示设备蓝牙扫描模式更改。
- 值：usual.event.bluetooth.host.SCAN_MODE_UPDATE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_HOST_DISCOVERY_STARTED
（预留事件，暂未支持）提示设备上已启动蓝牙扫描。
- 值：usual.event.bluetooth.host.DISCOVERY_STARTED
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_HOST_DISCOVERY_FINISHED
（预留事件，暂未支持）提示设备上蓝牙扫描完成。
- 值：usual.event.bluetooth.host.DISCOVERY_FINISHED
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_HOST_NAME_UPDATE
（预留事件，暂未支持）提示设备蓝牙适配器名称已更改。
- 值：usual.event.bluetooth.host.NAME_UPDATE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_A2DPSINK_CONNECT_STATE_UPDATE
（预留事件，暂未支持）提示蓝牙A2DP宿的连接状态已更改。
- 值：usual.event.bluetooth.a2dpsink.CONNECT_STATE_UPDATE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_A2DPSINK_PLAYING_STATE_UPDATE
（预留事件，暂未支持）提示蓝牙A2DP宿的播放状态发生改变。
- 值：usual.event.bluetooth.a2dpsink.PLAYING_STATE_UPDATE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_BLUETOOTH_A2DPSINK_AUDIO_STATE_UPDATE
（预留事件，暂未支持）提示蓝牙A2DP宿的音频状态已更改。
- 值：usual.event.bluetooth.a2dpsink.AUDIO_STATE_UPDATE
- 订阅者所需权限：ohos.permission.USE_BLUETOOTH


## COMMON_EVENT_NFC_ACTION_ADAPTER_STATE_CHANGED
（预留事件，暂未支持）提示设备NFC适配器状态已更改。
- 值：usual.event.nfc.action.ADAPTER_STATE_CHANGED
- 订阅者所需权限：无


## COMMON_EVENT_NFC_ACTION_RF_FIELD_ON_DETECTED
（预留事件，暂未支持）提示检测到NFC设备RF字段处于使能状态。
- 值：usual.event.nfc.action.RF_FIELD_ON_DETECTED
- 订阅者所需权限：ohos.permission.MANAGE_SECURE_SETTINGS


## COMMON_EVENT_NFC_ACTION_RF_FIELD_OFF_DETECTED
（预留事件，暂未支持）提示检测到NFC设备RF字段处于关闭状态。
- 值：usual.event.nfc.action.RF_FIELD_OFF_DETECTED
- 订阅者所需权限：ohos.permission.MANAGE_SECURE_SETTINGS


## COMMON_EVENT_DISCHARGING
提示系统停止为电池充电。
- 值：usual.event.DISCHARGING
- 订阅者所需权限：无


## COMMON_EVENT_CHARGING
提示系统开始为电池充电。
- 值：usual.event.CHARGING
- 订阅者所需权限：无


## COMMON_EVENT_DEVICE_IDLE_MODE_CHANGED
（预留事件，暂未支持）提示系统空闲模式已更改。
- 值：usual.event.DEVICE_IDLE_MODE_CHANGED
- 订阅者所需权限：无


## COMMON_EVENT_POWER_SAVE_MODE_CHANGED
提示系统节能模式更改。
- 值：usual.event.POWER_SAVE_MODE_CHANGED
- 订阅者所需权限：无


## COMMON_EVENT_USER_ADDED
提示用户已添加到系统中。
- 值：usual.event.USER_ADDED
- 订阅者所需权限：ohos.permission.MANAGE_LOCAL_ACCOUNTS


## COMMON_EVENT_USER_REMOVED
提示用户已从系统中删除。
- 值：usual.event.USER_REMOVED
- 订阅者所需权限：ohos.permission.MANAGE_LOCAL_ACCOUNTS


## COMMON_EVENT_ABILITY_ADDED
（预留事件，暂未支持）提示有某个能力已被添加。
- 值：usual.event.ABILITY_ADDED
- 订阅者所需权限：ohos.permission.LISTEN_BUNDLE_CHANGE


## COMMON_EVENT_ABILITY_REMOVED
（预留事件，暂未支持）提示已删除某个能力。
- 值：usual.event.ABILITY_REMOVED
- 订阅者所需权限：ohos.permission.LISTEN_BUNDLE_CHANGE


## COMMON_EVENT_ABILITY_UPDATED
（预留事件，暂未支持）提示能力已更新。
- 值：usual.event.ABILITY_UPDATED
- 订阅者所需权限：ohos.permission.LISTEN_BUNDLE_CHANGE


## COMMON_EVENT_LOCATION_MODE_STATE_CHANGED
（预留事件，暂未支持）提示系统定位模式已更改。
- 值：usual.event.location.MODE_STATE_CHANGED
- 订阅者所需权限：无


## COMMON_EVENT_IVI_SLEEP
（预留事件，暂未支持）提示车辆的车载信息娱乐（IVI）系统正在休眠。
- 值：common.event.IVI_SLEEP
- 订阅者所需权限：无


## COMMON_EVENT_IVI_PAUSE
（预留事件，暂未支持）提示车辆的车载信息娱乐（IVI）系统已休眠，并通知应用程序停止播放。
- 值：common.event.IVI_PAUSE
- 订阅者所需权限：无


## COMMON_EVENT_IVI_STANDBY
（预留事件，暂未支持）提示车辆的车载信息娱乐（IVI）系统中的第三方应用暂停当前工作。
- 值：common.event.IVI_STANDBY
- 订阅者所需权限：无


## COMMON_EVENT_IVI_LASTMODE_SAVE
（预留事件，暂未支持）提示车辆的车载信息娱乐（IVI）系统中的第三方应用保存其最后一个模式。
- 值：common.event.IVI_LASTMODE_SAVE
- 订阅者所需权限：无


## COMMON_EVENT_IVI_VOLTAGE_ABNORMAL
（预留事件，暂未支持）提示车辆电源系统电压异常。
- 值：common.event.IVI_VOLTAGE_ABNORMAL
- 订阅者所需权限：无


## COMMON_EVENT_IVI_HIGH_TEMPERATURE
（预留事件，暂未支持）提示车辆的车载信息娱乐（IVI）系统温度过高。
- 值：common.event.IVI_HIGH_TEMPERATURE
- 订阅者所需权限：无


## COMMON_EVENT_IVI_EXTREME_TEMPERATURE
（预留事件，暂未支持）提示车辆的车载信息娱乐（IVI）系统温度极高。
- 值：common.event.IVI_EXTREME_TEMPERATURE
- 订阅者所需权限：无


## COMMON_EVENT_IVI_TEMPERATURE_ABNORMAL
（预留事件，暂未支持）提示车辆的车载信息娱乐（IVI）系统具有极端温度。
- 值：common.event.IVI_TEMPERATURE_ABNORMAL
- 订阅者所需权限：无


## COMMON_EVENT_IVI_VOLTAGE_RECOVERY
（预留事件，暂未支持）提示车辆电源系统电压恢复正常。
- 值：common.event.IVI_VOLTAGE_RECOVERY
- 订阅者所需权限：无


## COMMON_EVENT_IVI_TEMPERATURE_RECOVERY
（预留事件，暂未支持）提示车载系统温度恢复正常。
- 值：common.event.IVI_TEMPERATURE_RECOVERY
- 订阅者所需权限：无


## COMMON_EVENT_IVI_ACTIVE
（预留事件，暂未支持）提示车载系统电池服务处于活动状态。
- 值：common.event.IVI_ACTIVE
- 订阅者所需权限：无


## COMMON_EVENT_USB_DEVICE_ATTACHED
当用户设备作为USB主机时，提示USB设备已挂载。
- 值：usual.event.hardware.usb.action.USB_DEVICE_ATTACHED
- 订阅者所需权限：无


## COMMON_EVENT_USB_DEVICE_DETACHED
当用户设备作为USB主机时，提示USB设备被卸载。
- 值：usual.event.hardware.usb.action.USB_DEVICE_DETACHED
- 订阅者所需权限：无


## COMMON_EVENT_USB_ACCESSORY_ATTACHED
（预留事件，暂未支持）提示已连接USB附件。
- 值：usual.event.hardware.usb.action.USB_ACCESSORY_ATTACHED
- 订阅者所需权限：无


## COMMON_EVENT_USB_ACCESSORY_DETACHED
（预留事件，暂未支持）提示USB附件被卸载。
- 值：usual.event.hardware.usb.action.USB_ACCESSORY_DETACHED
- 订阅者所需权限：无


## COMMON_EVENT_DISK_REMOVED
（预留事件，暂未支持）提示外部存储设备状态变更为移除。
- 值：usual.event.data.DISK_REMOVED
- 订阅者所需权限：ohos.permission.STORAGE_MANAGER


## COMMON_EVENT_DISK_UNMOUNTED
（预留事件，暂未支持）提示外部存储设备状态变更为卸载。
- 值：usual.event.data.DISK_UNMOUNTED
- 订阅者所需权限：ohos.permission.STORAGE_MANAGER


## COMMON_EVENT_DISK_MOUNTED
（预留事件，暂未支持）提示外部存储设备状态变更为挂载。
- 值：usual.event.data.DISK_MOUNTED
- 订阅者所需权限：ohos.permission.STORAGE_MANAGER


## COMMON_EVENT_DISK_BAD_REMOVAL
（预留事件，暂未支持）提示外部存储设备在挂载状态下被移除。
- 值：usual.event.data.DISK_BAD_REMOVAL
- 订阅者所需权限：ohos.permission.STORAGE_MANAGER


## COMMON_EVENT_DISK_UNMOUNTABLE
（预留事件，暂未支持）提示外部存储设备在插卡情况下无法挂载。
- 值：usual.event.data.DISK_UNMOUNTABLE
- 订阅者所需权限：ohos.permission.STORAGE_MANAGER


## COMMON_EVENT_DISK_EJECT
（预留事件，暂未支持）提示用户已作出弹出外部存储介质的操作（系统软件层面的交互操作，非直接物理弹出）。
- 值：usual.event.data.DISK_EJECT
- 订阅者所需权限：ohos.permission.STORAGE_MANAGER


## COMMON_EVENT_VISIBLE_ACCOUNTS_UPDATED
（预留事件，暂未支持）提示帐户发生可见性的更改。
- 值：usual.event.data.VISIBLE_ACCOUNTS_UPDATED
- 订阅者所需权限：ohos.permission.GET_APP_ACCOUNTS


## COMMON_EVENT_ACCOUNT_DELETED
（预留事件，暂未支持）提示有帐户被删除。
- 值：usual.event.data.ACCOUNT_DELETED
- 订阅者所需权限：ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS


## COMMON_EVENT_FOUNDATION_READY
（预留事件，暂未支持）提示foundation已准备好。
- 值：usual.event.data.FOUNDATION_READY
- 订阅者所需权限：ohos.permission.RECEIVER_STARTUP_COMPLETED


## COMMON_EVENT_AIRPLANE_MODE_CHANGED
提示设备飞行模式发生了切换。
- 值：usual.event.AIRPLANE_MODE
- 订阅者所需权限：无


## COMMON_EVENT_SPLIT_SCREEN<sup>8+<sup>
提示分屏。
- 值：usual.event.SPLIT_SCREEN
- 订阅者所需权限：无

