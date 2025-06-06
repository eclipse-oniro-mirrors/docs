# 文件管理错误码

> **说明：**
>
> 以下仅介绍本模块特有错误码，通用错误码请参考[通用错误码说明文档](../errorcode-universal.md)。

文件管理子系统错误码由五部分组成，分别是[基础文件IO错误码](#基础文件io错误码)、[用户数据管理错误码](#用户数据管理错误码)、[公共文件访问错误码](#公共文件访问错误码)、[空间统计错误码](#空间统计错误码)和[端云同步错误码](#端云同步错误码)。

## 基础文件IO错误码

### 13900001 操作不允许

**错误信息**

Operation not permitted

**可能原因**

当前用户文件操作不被允许，URI或path访问未授权。

**处理步骤**

1.根据当前系统的[访问控制机制](../../security/AccessToken/access-token-overview.md)，应用无法使用分享给其他应用的URI。

2.根据[系统Picker](../../application-models/system-app-startup.md)的运行机制，通过Picker获取到的URI仅有临时权限，无法持久化保存使用。

3.URI路径不推荐进行拼接，拼接后的URI默认未授权。

### 13900002 没有这个文件或目录

**错误信息**

No such file or directory

**可能原因**

文件或目录不存在。

**处理步骤**

确认文件路径是否存在。

### 13900003 没有这样的进程

**错误信息**

No such process

**可能原因**

进程不存在。

**处理步骤**

1.确认进程是否被意外杀死。

2.确认相关服务是否已启动。

### 13900004 系统调用被中断

**错误信息**

Interrupted system call

**可能原因**

系统调用被其他线程中断。

**处理步骤**

1.检查多线程代码逻辑。

2.重新进行系统调用。

### 13900005 I/O错误

**错误信息**

I/O error

**可能原因**

IO请求非法。

**处理步骤**

重新进行IO请求。

### 13900006 没有这个设备或地址

**错误信息**

No such device or address

**可能原因**

设备或地址信息错误。

**处理步骤**

确认设备或地址信息。

### 13900007 参数列表太长

**错误信息**

Arg list too long

**可能原因**

参数列表过长。

**处理步骤**

减少参数个数。

### 13900008 坏的文件描述符

**错误信息**

Bad file descriptor

**可能原因**

1.此文件描述符已关闭。

2.读写权限不匹配。

**处理步骤**

1.确认此文件描述符是否已关闭。

2.确认此文件读写权限是否匹配。

### 13900009 没有子进程

**错误信息**

No child processes

**可能原因**

无法创建子进程。

**处理步骤**

确认系统中最大进程数。

### 13900010 资源暂时不可用

**错误信息**

Try again

**可能原因**

资源被阻塞。

**处理步骤**

重新请求资源。

### 13900011 内存溢出

**错误信息**

Out of memory

**可能原因**

内存溢出。

**处理步骤**

1.确认内存开销。

2.管理系统内存开销。

### 13900012 拒绝许可

**错误信息**

Permission denied

**可能原因**

1.文件操作被DAC或selinux拦截。

2.文件沙箱路径地址错误。

**处理步骤**

1.访问被DAC自主式权限控制权限拦截，请排查文件的UGO权限。

2.排查内核日志中是否有[avc拦截日志](https://gitee.com/openharmony/docs/blob/master/zh-cn/device-dev/subsystems/subsys-security-selinux-develop-intro.md)，如果存在avc拦截告警，<!--RP1-->拦截原因分析请参考[SELinux开发说明](../../../device-dev/subsystems/subsys-security-selinux-develop-intro.md)。<!--RP1End-->

3.确认文件的路径是否为应用内的沙箱路径[沙箱路径地址](../../file-management/app-sandbox-directory.md)，文件管理系统禁止操作应用沙箱以外的文档。

### 13900013 错误的地址

**错误信息**

Bad address

**可能原因**

地址错误。

**处理步骤**

确认地址是否正确。

### 13900014 设备或资源忙

**错误信息**

Device or resource busy

**可能原因**

请求的资源不可用。

**处理步骤**

重新请求资源。

### 13900015 文件存在

**错误信息**

File exists

**可能原因**

需创建的文件已存在。

**处理步骤**

确认文件路径是否正确。

### 13900016 无效的交叉链接

**错误信息**

Cross-device link

**可能原因**

跨设备链接失败。

**处理步骤**

确认跨设备是否正常。

### 13900017 设备不存在

**错误信息**

No such device

**可能原因**

设备未被识别。

**处理步骤**

确认设备间连接是否正常。

### 13900018 不是一个目录

**错误信息**

Not a directory

**可能原因**

此路径不是文件夹目录。

**处理步骤**

确认路径是否正确。

### 13900019 是一个目录

**错误信息**

Is a directory

**可能原因**

此路径是文件夹目录。

**处理步骤**

确认路径是否正确。

### 13900020 无效的参数

**错误信息**

Invalid argument

**可能原因**

输入参数非法。

**处理步骤**

确认参数合法性。

### 13900021 打开太多的文件系统

**错误信息**

File table overflow

**可能原因**

进程打开过多的文件描述符。

**处理步骤**

关闭不相关的文件描述符。

### 13900022 打开的文件过多

**错误信息**

Too many open files

**可能原因**

系统打开过多的文件。

**处理步骤**

关闭不需要的文件。

### 13900023 文本文件忙

**错误信息**

Text file busy

**可能原因**

程序的可执行文件正在被使用。

**处理步骤**

关闭正在调试的程序。

### 13900024 文件太大

**错误信息**

File too large

**可能原因**

文件大小超出最大文件大小。

**处理步骤**

确认文件大小是否满足最大文件大小。

### 13900025 设备上没有空间

**错误信息**

No space left on device

**可能原因**

设备存储空间不足。

**处理步骤**

清理设备存储空间。

### 13900026 非法移位

**错误信息**

Illegal seek

**可能原因**

在管道或FIFO中使用seek。

**处理步骤**

确认seek使用。

### 13900027 只读文件系统

**错误信息**

Read-only file system

**可能原因**

文件系统只支持读。

**处理步骤**

确认文件是否只读。

### 13900028 太多的链接

**错误信息**

Too many links

**可能原因**

文件已达最大链接数。

**处理步骤**

清理无用链接。

### 13900029 资源死锁错误

**错误信息**

Resource deadlock would occur

**可能原因**

资源死锁。

**处理步骤**

终止死锁进程。

### 13900030 文件名太长

**错误信息**

Filename too Long

**可能原因**

文件名超过最大长度255字节。

**处理步骤**

确认文件名长度。

### 13900031 功能没有实现

**错误信息**

Function not implemented

**可能原因**

系统不支持此功能。

**处理步骤**

确认系统版本。

### 13900032 目录非空

**错误信息**

Directory not empty

**可能原因**

指定目录不为空。

**处理步骤**

1.确认目录路径。

2.确认路径为空。

### 13900033 符号链接层次太多

**错误信息**

Too many symbolic links encountered

**可能原因**

符号链接层次过多。

**处理步骤**

清理无关符号链接。

### 13900034 操作被阻塞

**错误信息**

Operation would block

**可能原因**

操作被阻塞。

**处理步骤**

重新进行操作。

### 13900035 请求描述符无效

**错误信息**

Invalid request descriptor

**可能原因**

文件描述符非法。

**处理步骤**

确认文件描述符是否合法。

### 13900036 设备不是字符流

**错误信息**

Device not a stream

**可能原因**

文件描述符指向非流设备。

**处理步骤**

确认文件描述符是否指向流设备。

### 13900037 无可用数据

**错误信息**

No data available

**可能原因**

数据不可用。

**处理步骤**

重新请求数据。

### 13900038 对于定义的数据类型,值太大

**错误信息**

Value too large for defined data type

**可能原因**

值超出所定义的数据类型范围。

**处理步骤**

修改数据类型。

### 13900039 文件描述符在坏状态

**错误信息**

File descriptor in bad state

**可能原因**

文件描述符损坏。

**处理步骤**

确认文件描述符合法性。

### 13900040 应该重新启动被中断的系统调用

**错误信息**

Interrupted system call should be restarted

**可能原因**

系统调用被中断。

**处理步骤**

重新进行系统调用。

### 13900041 超出磁盘配额

**错误信息**

Quota exceeded

**可能原因**

磁盘空间不足。

**处理步骤**

清理磁盘存储空间。

### 13900042 未知错误

**错误信息**

Unknown error

**可能原因**

内部错误。

**处理步骤**

1.重试接口。

2.重启服务。

### 13900043 没有可用的锁

**错误信息**

No record is locks available

**可能原因**

系统资源不足。

**处理步骤**

释放锁资源后重试。

### 13900044 网络无法访问

**错误信息**

Network is unreachable

**可能原因**

网络异常。

**处理步骤**

检查网络状态，确认状态正常。

### 13900045 连接失败

**错误信息**

Connection failed

**可能原因**

设备、Wifi或蓝牙状态异常，导致建立链接失败。

**处理步骤**

1.检查设备，确认设备状态正常。

2.检查WiFi和蓝牙，确认状态正常。

### 13900046 软件造成连接中断

**错误信息**

Software caused connection abort

**可能原因**

设备下线或WiFi、蓝牙断连。

**处理步骤**

1.检查设备，确认设备状态正常。

2.检查WiFi和蓝牙，确认状态正常。

## 用户数据管理错误码

### 14000001 文件名非法

**错误信息**

Invalid file name

**可能原因**

文件名存在非法字符。

**处理步骤**

删除非法字符。

### 14000002 非法URI

**错误信息**

Invalid URI

**可能原因**

URI不合法。

**处理步骤**

直接使用查询获取的URI。

### 14000003 文件后缀非法

**错误信息**

Invalid file name extension

**可能原因**

按照文件类型命名。

**处理步骤**

检查文件名后缀。

### 14000004 文件已进入回收站

**错误信息**

File already in the recycle bin

**可能原因**

文件已经被删除进入回收站。

**处理步骤**

检查文件是否已经进入回收站。

### 14000011 系统内部错误

**错误信息**

System inner fail

**可能原因**

系统异常，发生未知错误。

**处理步骤**

清理后台，或重启设备。

### 14000014 成员名非法

**错误信息**

Member is not a valid PhotoKey

**可能原因**

传入的字符串不是类或接口的成员名。

**处理步骤**

确保传入的字符串为类或接口的成员名。

## 空间统计错误码

### 13600001 IPC通信失败

**错误信息**

IPC error

**可能原因**

调用服务不存在。

**处理步骤**

检查服务是否启动。

### 13600002 文件系统类型不支持

**错误信息**

File system not supported

**可能原因**

操作的文件系统类型不支持。

**处理步骤**

修改为正确的文件系统类型。

### 13600003 挂载失败

**错误信息**

Mount failed

**可能原因**

调用挂载命令失败。

**处理步骤**

拔卡尝试重新挂载。

### 13600004 卸载失败

**错误信息**

Unmount failed

**可能原因**

设备繁忙。

**处理步骤**

检查外卡文件是否被线程占用, 杀掉占用线程。

### 13600005 卷状态错误

**错误信息**

Incorrect volume state

**可能原因**

操作的卷状态错误。

**处理步骤**

检查当前卷状态是否正确。

### 13600006 创建目录或者节点失败

**错误信息**

Failed to create the directory or node

**可能原因**

目录或节点已存在。

**处理步骤**

检查待创建目录或节点是否存在。

### 13600007 删除目录或者节点失败

**错误信息**

Failed to delete the directory or node

**可能原因**

目录或节点已删除。

**处理步骤**

检查待删除目录或节点是否存在。

### 13600008 操作对象不存在

**错误信息**

No such object

**可能原因**

1.输入错误的卷id。

2.输入错误的包名。

**处理步骤**

1.检查输入的卷是否存在。

2.检查输入的应用包名是否存在。

### 13600009 用户id超出范围

**错误信息**

User ID out of range

**可能原因**

输入错误的用户id。

**处理步骤**

检查输入的用户id是否处于正常范围。

## 公共文件访问错误码

### 14300001 IPC通信失败

**错误信息**

IPC error

**可能原因**

1.server端服务不在。

2.extension机制异常。

**处理步骤**

检查server端服务是否存在。

### 14300002 URI格式错误

**错误信息**

Invalid URI

**可能原因**

使用非法URI。

**处理步骤**

检查URI格式。

### 14300003 查询server端ability信息失败

**错误信息**

Failed to obtain the server ability information

**可能原因**

BMS接口异常。

**处理步骤**

系统基础能力问题，<!--RP1-->请向OpenHarmony团队反馈，获取支持。<!--RP1End-->

### 14300004 js-server实际返回的结果异常

**错误信息**

Incorrect result returned by js-server

**可能原因**

server端返回实际数据不当。

**处理步骤**

server端返回值检查。

### 14300005 notify注册失败

**错误信息**

Failed to register Notify

**可能原因**

1.server端服务不在。

2.extension机制异常。

**处理步骤**

检查server端服务是否存在。

### 14300006 notify移除失败

**错误信息**

Failed to unregister Notify

**可能原因**

1.server端服务不在。

2.extension机制异常。

**处理步骤**

检查server端服务是否存在。

### 14300007 notify代理初始化失败

**错误信息**

Failed to initialize the Notify agent

**可能原因**

未注册就去取消notify。

**处理步骤**

检查是否注册过。

### 14300008 js-server端通知代理失败

**错误信息**

Failed to notify the agent

**可能原因**

1.服务不在。

2.extension机制异常。

**处理步骤**

检查client是否异常。

## 端云同步错误码

### 22400001 云端状态未ready

**错误信息**

Cloud status not ready

**可能原因**

1.未启用云。

2.应用云同步开关未打开。

**处理步骤**

1.检查是否账号登录。

2.检查云同步开关是否打开。

### 22400002  网络不可用

**错误信息**

Network unavailable

**可能原因**

设备未联网或网络不可用。

**处理步骤**

检查网络状态。

### 22400003  告警电量

**错误信息**

Low battery level

**可能原因**

电量过低。

**处理步骤**

充电状态或电量恢复后再执行。

### 22400004  入参请求超过最大限制

**错误信息**

Exceeded the maximum limit

**可能原因**

请求数量超过接口规格定义的上限。

**处理步骤**

检查入参，保证请求数量符合规格要求。

### 22400005  内部错误

**错误信息**

Inner error

**可能原因**

1.系统内部数据库请求失败或者SQL执行失败。

2.系统出现空指针等异常。

3.系统内存不足或内存异常。

4.JS框架异常。

**处理步骤**

系统基础能力问题，<!--RP1-->请向OpenHarmony团队反馈，获取支持。<!--RP1End-->

### 22400006  已经有同类型任务正在运行

**错误信息**

The same task is already in progress

**可能原因**

有同类型任务正在运行。

**处理步骤**

等待现有同类型任务完成，或通过调用对应业务的stop接口终止现有任务后，再触发新任务。

### 22400007  指定用于替换原始文件的历史版本文件不存在

**错误信息**

The version file specified to replace the original file does not exist

**可能原因**

历史版本文件未下载或已删除。

**处理步骤**

重新下载指定的历史版本文件，保证文件存在。
