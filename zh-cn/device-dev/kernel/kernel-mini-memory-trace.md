# Trace调测


## 基本概念

Trace调测旨在帮助开发者获取内核的运行流程，各个模块、任务的执行顺序，从而可以辅助开发者定位一些时序问题或者了解内核的代码运行过程。


## 运行机制

内核提供一套Hook框架，将Hook点预埋在各个模块的主要流程中, 在内核启动初期完成Trace功能的初始化，并注册Trace的处理函数到Hook中。

当系统触发到一个Hook点时，Trace模块会对输入信息进行封装，添加Trace帧头信息，包含事件类型、运行的cpuid、运行的任务id、运行的相对时间戳等信息；

Trace提供2种工作模式，离线模式和在线模式。

离线模式会将trace frame记录到预先申请好的循环buffer中。如果循环buffer记录的frame过多则可能出现翻转，会覆盖之前的记录，故保持记录的信息始终是最新的信息。Trace循环buffer的数据可以通过shell命令导出进行详细分析，导出信息已按照时间戳信息完成排序。

![zh-cn_image_0000001168711762](figures/zh-cn_image_0000001168711762.png)

在线模式需要配合IDE使用，实时将trace frame记录发送给IDE，IDE端进行解析并可视化展示。


## 接口说明

OpenHarmony LiteOS-M内核的Trace模块提供下面几种功能，接口详细信息可以查看API参考。

  **表1** Trace模块接口说明

| 功能分类 | 接口名 | 
| -------- | -------- |
| 启停控制 | -&nbsp;LOS_TraceStart：启动Trace<br/>-&nbsp;LOS_TraceStop：停止Trace | 
| 操作Trace记录的数据 | -&nbsp;LOS_TraceRecordDump：输出Trace缓冲区数据<br/>-&nbsp;LOS_TraceRecordGet：获取Trace缓冲区的首地址<br/>-&nbsp;LOS_TraceReset：清除Trace缓冲区中的事件 | 
| 过滤Trace记录的数据 | LOS_TraceEventMaskSet：设置事件掩码，仅记录某些模块的事件 | 
| 屏蔽某些中断号事件 | LOS_TraceHwiFilterHookReg：注册过滤特定中断号事件的钩子函数 | 
| 插桩函数 | LOS_TRACE_EASY:简易插桩<br/>LOS_TRACE:标准插桩 | 

- 当用户需要针对自定义事件进行追踪时，可按规则在目标源代码中进行插桩，系统提供如下2种插桩接口：
  - LOS_TRACE_EASY(TYPE, IDENTITY, params...) 简易插桩。
     - 一句话插桩，用户在目标源代码中插入该接口即可。
     - TYPE有效取值范围为[0, 0xF]，表示不同的事件类型，不同取值表示的含义由用户自定义。
     - IDENTITY类型UINTPTR，表示事件操作的主体对象。
     - Params类型UINTPTR，表示事件的参数。
     - 对文件fd读写操作的简易插桩示例：
       
        ```
        /* 假设自定义读操作为type: 1, 写操作为type: 2 */
        LOS_TRACE_EASY(1, fd, flag, size);  /* 在读fd文件的适当位置插入 */
        LOS_TRACE_EASY(2, fd, flag, size);  /* 在写fd文件的适当位置插入 */
        ```
  - LOS_TRACE(TYPE, IDENTITY, params...) 标准插桩。
     - 相比简易插桩，支持动态过滤事件和参数裁剪，但使用上需要用户按规则来扩展。
     - TYPE用于设置具体的事件类型，可以在头文件los_trace.h中的enum LOS_TRACE_TYPE中自定义事件类型。定义方法和规则可以参考其他事件类型。
     - IDENTITY和Params的类型及含义同简易插桩。
     - 示例：
          1. 定义FS模块的类型，即FS模块的事件掩码
          
        ```
        /* 在enum LOS_TRACE_MASK中定义, 定义规范为TRACE_#MOD#_FLAG, #MOD#表示模块名 */
        TRACE_FS_FLAG = 0x4000
        ```

        2. 定义FS模块的具体事件类型

        
        ```
        /* 定义规范为#TYPE# = TRACE_#MOD#_FLAG | NUMBER,  */
        FS_READ  = TRACE_FS_FLAG | 0; /* 读文件 */
        FS_WRITE = TRACE_FS_FLAG | 1; /* 写文件 */
        ```

        3. 定义事件参数

        
        ```
        /* 定义规范为#TYPE#_PARAMS(IDENTITY, parma1...) IDENTITY, ... */
        #define FS_READ_PARAMS(fp, fd, flag, size)  fp, fd, flag, size /* 宏定义的参数对应于Trace缓冲区中记录的事件参数，用户可对任意参数字段进行裁剪 */
        #define FS_READ_PARAMS(fp, fd, flag, size)                     /* 当定义为空时，表示不追踪该类型事件 */
        ```

        4. 在目标代码中插桩

        
        ```
        /* 定义规范为LOS_TRACE(#TYPE#, #TYPE#_PARAMS(IDENTITY, parma1...)) */
        LOS_TRACE(FS_READ, fp, fd, flag, size); /* 读文件操作的代码桩 */
        ```

        > ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
        > 预置的Trace事件及参数均可以通过上述方式进行裁剪，参数详见kernel\include\los_trace.h。

- Trace Mask事件过滤接口LOS_TraceEventMaskSet(UINT32 mask)，其入参mask仅高28位生效（对应LOS_TRACE_MASK中某模块的使能位），仅用于模块的过滤，暂不支持针对某个特定事件的细粒度过滤。例如：LOS_TraceEventMaskSet(0x202)，则实际设置生效的mask为0x200（TRACE_QUE_FLAG），QUE模块的所有事件均会被采集。一般建议使用的方法为： LOS_TraceEventMaskSet(TRACE_EVENT_FLAG | TRACE_MUX_FLAG | TRACE_SEM_FLAG | TRACE_QUE_FLAG);

- 如果仅需要简易插桩事件，通过设置Trace Mask为TRACE_MAX_FLAG即可。

- Trace缓冲区有限，事件写满之后会覆盖写，用户可通过LOS_TraceRecordDump中打印的CurEvtIndex识别最新记录。

- Trace的典型操作流程为：LOS_TraceStart、 LOS_TraceStop、 LOS_TraceRecordDump.

- 针对中断事件的Trace, 提供中断号过滤，用于解决某些场景下特定中断号频繁触发导致其他事件被覆盖的情况，用户可自定义中断过滤的规则，
    示例如下：
    
  ```
  BOOL Example_HwiNumFilter(UINT32 hwiNum)
  {
         if ((hwiNum == TIMER_INT) || (hwiNum == DMA_INT)) {
          return TRUE;
      }
      return FALSE;
  }
  LOS_TraceHwiFilterHookReg(Example_HwiNumFilter);
  ```

  则当中断号为TIMER_INT 或者DMA_INT时，不记录中断事件。


## 开发指导


### 开发流程

开启Trace调测的典型流程如下：

1. 配置Trace模块相关宏。
     需要在target_config.h头文件中修改配置：
     | 配置项 | 含义 | 设置值 | 
   | -------- | -------- | -------- |
   | LOSCFG_KERNEL_TRACE | Trace模块的裁剪开关 | YES/NO | 
   | LOSCFG_RECORDER_MODE_OFFLINE | Trace工作模式为离线模式 | YES/NO | 
   | LOSCFG_RECORDER_MODE_ONLINE | Trace工作模式为在线模式 | YES/NO | 
   | LOSCFG_TRACE_CLIENT_INTERACT | 使能与Trace&nbsp;IDE&nbsp;（dev&nbsp;tools）的交互，包括数据可视化和流程控制 | YES/NO | 
   | LOSCFG_TRACE_FRAME_CORE_MSG | 记录CPUID、中断状态、锁任务状态 | YES/NO | 
   | LOSCFG_TRACE_FRAME_EVENT_COUNT | 记录事件的次序编号 | YES/NO | 
   | LOSCFG_TRACE_FRAME_MAX_PARAMS | 配置记录事件的最大参数个数 | INT | 
   | LOSCFG_TRACE_BUFFER_SIZE | 配置Trace的缓冲区大小 | INT | 

2. (可选)预置事件参数和事件桩（或使用系统默认的事件参数配置和事件桩）。

3. (可选)调用LOS_TraceStop停止Trace后，清除缓冲区LOS_TraceReset（系统默认已启动trace）。

4. (可选)调用LOS_TraceEventMaskSet设置需要追踪的事件掩码（系统默认的事件掩码仅使能中断与任务事件），事件掩码参见los_trace.h 中的LOS_TRACE_MASK定义。

5. 在需要记录事件的代码起始点调用LOS_TraceStart。

6. 在需要记录事件的代码结束点调用LOS_TraceStop。

7. 调用LOS_TraceRecordDump输出缓冲区数据（函数的入参为布尔型，FALSE表示格式化输出，TRUE表示输出到windows客户端）。

上述第3-7步中的接口，均封装有对应的shell命令，对应关系如下

- LOS_TraceReset —— trace_reset

- LOS_TraceEventMaskSet —— trace_mask

- LOS_TraceStart —— trace_start

- LOS_TraceStop —— trace_stop

- LOS_TraceRecordDump —— trace_dump


### 编程实例

本实例实现如下功能：

1. 创建一个用于Trace测试的任务。

2. 设置事件掩码。

3. 启动trace。

4. 停止trace。

5. 格式化输出trace数据。


### 示例代码

示例代码如下：

本演示代码在 ./kernel/liteos_m/testsuites/src/osTest.c 中编译验证，在TestTaskEntry中调用验证入口函数ExampleTraceTest。


```
#include "los_trace.h"
UINT32 g_traceTestTaskId;
VOID Example_Trace(VOID)
{ 
    UINT32 ret;    
    LOS_TaskDelay(10);
    /* 开启trace */
    ret = LOS_TraceStart();    
    if (ret != LOS_OK) {        
        dprintf("trace start error\n");        
        return;    
    }    
    /* 触发任务切换的事件 */    
    LOS_TaskDelay(1);    
    LOS_TaskDelay(1);    
    LOS_TaskDelay(1);    
    /* 停止trace */    
    LOS_TraceStop();    
    LOS_TraceRecordDump(FALSE);
}
UINT32 ExampleTraceTest(VOID){
    UINT32 ret;    
    TSK_INIT_PARAM_S traceTestTask = { 0 };
    /* 创建用于trace测试的任务 */    
    memset(&traceTestTask, 0, sizeof(TSK_INIT_PARAM_S));    
    traceTestTask.pfnTaskEntry = (TSK_ENTRY_FUNC)Example_Trace;    
    traceTestTask.pcName       = "TestTraceTsk";    /* 测试任务名称 */    				     
    traceTestTask.uwStackSize  = 0x800;    
    traceTestTask.usTaskPrio   = 5;    
    traceTestTask.uwResved   = LOS_TASK_STATUS_DETACHED;    
    ret = LOS_TaskCreate(&g_traceTestTaskId, &traceTestTask);    
    if(ret != LOS_OK){        
        dprintf("TraceTestTask create failed .\n");        
        return LOS_NOK;    
    }    
    /* 系统默认情况下已启动trace, 因此可先关闭trace后清除缓存区后，再重启trace */                    	  
    LOS_TraceStop();    
    LOS_TraceReset();    
    /* 开启任务模块事件记录 */    
    LOS_TraceEventMaskSet(TRACE_TASK_FLAG);    
    return LOS_OK;
}
```


### 结果验证

输出结果如下：


```
***TraceInfo begin***
clockFreq = 50000000
CurEvtIndex = 7
Index   Time(cycles)      EventType      CurTask   Identity      params    
0       0x366d5e88        0x45           0x1       0x0           0x1f         0x4       0x0
1       0x366d74ae        0x45           0x0       0x1           0x0          0x8       0x1f
2       0x36940da6        0x45           0x1       0xc           0x1f         0x4       0x9
3       0x3694337c        0x45           0xc       0x1           0x9          0x8       0x1f
4       0x36eea56e        0x45           0x1       0xc           0x1f         0x4       0x9
5       0x36eec810        0x45           0xc       0x1           0x9          0x8       0x1f
6       0x3706f804        0x45           0x1       0x0           0x1f         0x4       0x0
7       0x37070e59        0x45           0x0       0x1           0x0          0x8       0x1f
***TraceInfo end***

根据实际运行环境，上文中的数据会有差异，非固定结果
```

输出的事件信息包括：发生时间、事件类型、事件发生在哪个任务中、事件操作的主体对象、事件的其他参数。

- EventType：表示的具体事件可查阅头文件los_trace.h中的enum LOS_TRACE_TYPE。

- CurrentTask：表示当前运行在哪个任务中，值为taskid。

- Identity：表示事件操作的主体对象，可查阅头文件los_trace.h中的\#TYPE\#_PARAMS。

- params：表示的事件参数可查阅头文件los_trace.h中的\#TYPE\#_PARAMS。

下面以序号为0的输出项为例，进行说明。


```
Index   Time(cycles)      EventType      CurTask   Identity      params
0       0x366d5e88        0x45           0x1       0x0           0x1f         0x4
```

- Time cycles可换算成时间，换算公式为cycles/clockFreq，单位为s。

- 0x45为TASK_SWITCH即任务切换事件，当前运行的任务taskid为0x1。

- Identity和params的含义需要查看TASK_SWITCH_PARAMS宏定义：

  
```
#define TASK_SWITCH_PARAMS(taskId, oldPriority, oldTaskStatus, newPriority, newTaskStatus) \
taskId, oldPriority, oldTaskStatus, newPriority, newTaskStatus
```

  因为\#TYPE\#_PARAMS(IDENTITY, parma1...) IDENTITY, ...，所以Identity为taskId（0x0），第一个参数为oldPriority（0x1f）
> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> params的个数由LOSCFG_TRACE_FRAME_MAX_PARAMS配置，默认为3，超出的参数不会被记录，用户应自行合理配置该值。

综上所述，任务由0x1切换到0x0，0x1任务的优先级为0x1f，状态为0x4，0x0任务的优先级为0x0。
