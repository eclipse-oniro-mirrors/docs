# 调度器


## 基本概念

OpenHarmony LiteOS-A内核采用了高优先级优先 + 同优先级时间片轮转的抢占式调度机制，系统从启动开始基于real time的时间轴向前运行，使得该调度算法具有很好的实时性。

OpenHarmony 的调度算法将 tickless 机制天然嵌入到调度算法中，一方面使得系统具有更低的功耗，另一方面也使得 tick 中断按需响应，减少无用的 tick 中断响应，进一步提高系统的实时性。

OpenHarmony 的进程调度策略支持 SCHED_RR（时间片轮转），线程调度策略支持 SCHED_RR 和 SCHED_FIFO（先进先出）。

OpenHarmony 调度的最小单元为线程。


## 运行机制

OpenHarmony 采用进程优先级队列 + 线程优先级队列的方式，进程优先级范围为0-31，共有32个进程优先级桶队列，每个桶队列对应一个线程优先级桶队列；线程优先级范围也为0-31，一个线程优先级桶队列也有32个优先级队列。

  **图1** 调度优先级桶队列示意图

  ![zh-cn_image_0000001199705711](figures/zh-cn_image_0000001199705711.png)

OpenHarmony 在系统启动内核初始化之后开始调度，运行过程中创建的进程或线程会被加入到调度队列，系统根据进程和线程的优先级及线程的时间片消耗情况选择最优的线程进行调度运行，线程一旦调度到就会从调度队列上删除，线程在运行过程中发生阻塞，会被加入到对应的阻塞队列中并触发一次调度，调度其它线程运行。如果调度队列上没有可以调度的线程，则系统就会选择KIdle进程的线程进行调度运行。

  **图2** 调度流程示意图
  
  ![zh-cn_image_0000001199706239](figures/zh-cn_image_0000001199706239.png)


## 开发指导


### 接口说明

| 接口**名称** | 描述 |
| -------- | -------- |
| LOS_Schedule | 触发系统调度 |
| LOS_GetTaskScheduler | 获取指定任务的调度策略 |
| LOS_SetTaskScheduler | 设置指定任务的调度策略 |
| LOS_GetProcessScheduler | 获取指定进程的调度策略 |
| LOS_SetProcessScheduler | 设置指定进程的调度参数，包括优先级和调度策略 |


### 开发流程

> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 系统启动初始化阶段，不允许触发调度。
