# 魔法键使用方法


## 使用场景

在系统运行出现无响应等情况时，可以通过魔法键功能确定系统是否被锁中断（魔法键也无响应）或者查看系统任务运行状态等信息。

在中断有响应的情况下，可以通过魔法键查看task信息中  cpup（CPU占用率）看是哪个任务长时间占用CPU导致系统其他任务无响应（一般为比较高优先级任务一直抢占CPU，导致低优先级任务无响应）。


## 使用配置

魔法键依赖于宏LOSCFG_ENABLE_MAGICKEY，在kernel/liteos_a中输入make menuconfig命令。此时会弹出配置项，找到Debug选项并进入，在配置项中开启“Enable  MAGIC KEY”：

Debug ---&gt; Enable MAGIC KEY；若关闭该选项，则魔法键失效（默认为选中的）。

> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 可以在menuconfig中，将光标移动到LOSCFG_ENABLE_MAGICKEY上，输入“?”，可以查看帮助信息。

## 使用方法

1. 输入“ctrl + r”键，打开魔法键检测功能。

   在连接UART或者USB转虚拟串口的情况下，输入“ctrl + r” 键，打开魔法键检测功能，输出 “Magic key on”；再输入一次后，则关闭魔法键检测功能，输出“Magic key off”。魔法键功能如下：

   - ctrl + z：帮助键，输出相关魔法键简单介绍；

   - ctrl + t：输出任务相关信息；

   - ctrl + p：系统主动进入panic，输出panic相关信息后，系统会挂住；

   - ctrl + e：系统进行简单完整性内存池检查，检查出错会输出相关错误信息，检查正常会输出“system memcheck  over, all passed!”。

   > **须知：**
   > 魔法键检测功能打开情况下，如果需要通过UART或者USB转虚拟串口输入特殊字符需避免与魔法键值重复，否则魔法键会被误触发，而原有设计功能可能出现错误。