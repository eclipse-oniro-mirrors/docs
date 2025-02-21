# 系统电源管理错误码

> **说明：**
>
> 以下仅介绍本模块特有错误码，通用错误码请参考[通用错误码说明文档](errorcode-universal.md)。

## 4900101 连接服务失败

**错误信息**

Operation failed. Cannot connect to service.

**错误描述**

操作失败，连接系统服务发生异常。

**可能原因**

1. 系统服务停止运行。

2. 系统服务内部通讯发生异常。

**处理步骤**

检查系统服务是否正常运行。

1. 在控制台中输入如下命令，查看当前的系统服务列表。

    ```bash
    > hdc shell hidumper -ls
    ```

2. 查看系统服务列表中是否包含PowerManagerService系统服务。

## 4900102 正在关机中

**错误信息**

Operation failed. System is shutting down.

**错误描述**

操作失败，系统正在关机。

**可能原因**

系统正在处于关机过程中。

**处理步骤**

在系统正常运行的状态下进行操作。
