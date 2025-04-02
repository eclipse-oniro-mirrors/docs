# task


## 命令功能

task命令用于查询进程及线程信息。


## 命令格式

task/task -a


## 参数说明

**表1** 参数说明

| 参数 | 参数说明 | 取值范围 | 
| -------- | -------- | -------- |
| -a | 查看更多信息。 | N/A | 


## 使用指南

参数缺省时默认打印部分任务信息。


## 使用实例

举例：输入task


## 输出说明

**示例** 查询任务部分信息

```
OHOS # task
  allCpu(%):    3.54 sys,  196.46 idle
  PID  PPID PGID       UID  Status VirtualMem ShareMem PhysicalMem CPUUSE10s  PName
    1    -1    1         0 Pending   0x33b000  0xbb000     0x4dc8b      0.0   init
    2    -1    2         0 Pending  0x193318e        0   0x193318e      1.11  KProcess
    3     1    3         7 Pending   0x730000 0x1a2000    0x1d34f6      0.0   foundation
    4     1    4         8 Pending   0x35e000  0xb8000     0x56777      0.0   bundle_daemon
    5     1    5         1 Pending   0xdfa000 0x2e7000    0x1487ce      0.0   appspawn
    6     1    6         0 Pending   0x688000 0x137000    0x11c518      0.0   media_server
    7     1    7         0 Pending   0x9d2000 0x103000     0xa1ddf      0.89  wms_server
    8     1    1      1000 Running   0x2bf000  0x8f000     0x2a8c6      0.0   shell
    9     5    5       101 Pending  0x11ea000 0x2f9000    0x20429d      0.97  com.example.launcher
   11     1   11         0 Pending   0x4d4000 0x112000     0xe0ad7      0.0   deviceauth_service
   12     1   12         0 Pending   0x34f000  0xbd000     0x519ee      0.0   sensor_service
   13     1   13         2 Pending   0x34e000  0xb3000     0x523d9      0.0   ai_server
   14     1   14         0 Pending   0x61f000 0x13b000    0x16841c      0.50  softbus_server
  TID  PID Affi CPU       Status StackSize WaterLine CPUUSE10s    MEMUSE  TaskName
   23    1  0x3  -1      Pending    0x3000     0xe44      0.0           0  init
    1    2  0x1  -1      Pending    0x4000     0x2c4      0.37          0  Swt_Task
    2    2  0x3  -1      Pending    0x4000     0x204      0.0           0  system_wq
    3    2  0x2  -1      Pending    0x4000     0x514      0.65          0  Swt_Task
    4    2  0x3  -1      Pending    0x1000     0x36c      0.0           0  ResourcesTask
    7    2  0x3  -1      Pending    0x4e20     0xa5c      0.0           0  PlatformWorkerThread
```

**表2** 输出说明

| 输出 | 说明 | 
| -------- | -------- |
| PID | 进程ID。 | 
| PPID | 父进程ID。 | 
| PGID | 进程组ID。 | 
| UID | 用户ID。 | 
| Status | 任务当前的状态。 | 
| CPUUSE10s | 10秒内CPU使用率。 | 
| PName | 进程名。 | 
| TID | 任务ID。 | 
| StackSize | 任务堆栈的大小。 | 
| WaterLine | 栈使用的峰值。 | 
| MEMUSE | 内存使用量。 | 
| TaskName | 任务名。 | 
